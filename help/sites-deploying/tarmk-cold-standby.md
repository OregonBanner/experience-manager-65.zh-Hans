---
title: 如何使用TarMK冷待命執行AEM
seo-title: How to Run AEM with TarMK Cold Standby
description: 瞭解如何建立、設定和維護TarMK冷待命設定。
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 0%

---

# 如何使用TarMK冷待命執行AEM{#how-to-run-aem-with-tarmk-cold-standby}

## 简介 {#introduction}

Tar Micro Kernel的「冷待命」容量可讓一或多個待命AEM執行處理連線到主要執行處理。 同步處理只是一種方式，表示它只能從主要執行個體到待命執行個體完成。

待命執行個體的目的是保證主存放庫的即時資料副本，並確保在主存放庫因任何原因無法使用時，能夠快速切換資料，而不會遺失資料。

內容會在主要執行個體和待命執行個體之間線性同步，而不會對檔案或存放庫損毀進行任何完整性檢查。 由於此設計，待命執行個體是主要執行個體的精確副本，無法協助緩解主要執行個體上的不一致。

>[!NOTE]
>
>冷待命功能旨在保護需要高可用性的情況 **作者** 執行個體。 適用於以下需要高可用性的情況： **發佈** 使用Tar Micro Kernel的執行個體，Adobe建議使用發佈陣列。
>
>如需更多可用部署的詳細資訊，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md) 頁面。

>[!NOTE]
>
>設定「待命」執行處理，或從「主要」節點衍生時，它僅允許存取下列主控台（用於管理相關活動）：
>
>* OSGI Web主控台
>
>無法存取其他主控台。

## 運作方式 {#how-it-works}

在主要AEM執行個體上，TCP連線埠已開啟，且正在接聽傳入的訊息。 目前，從屬端會傳送兩種訊息給主端：

* 要求目前標題的區段ID的訊息
* 要求具有指定ID之區段資料的訊息

待命程式會定期要求主要磁頭目前磁頭的區段ID。 如果區段在本機不明，則會擷取它。 如果已存在，則會比較區段並視需要請求引用的區段。

>[!NOTE]
>
>待命執行個體未收到任何型別的請求，因為它們僅以同步模式執行。 待命執行個體上唯一可用的區段是Web主控台，以便於套件和服務設定。

典型的TarMK冷待命部署：

![chlimage_1](assets/chlimage_1.png)

## 其他特性 {#other-characteristics}

### 穩健性 {#robustness}

資料流程的設計目的是自動偵測及處理連線和網路相關問題。 所有封包都隨檢查加總而組合，一旦連線發生問題或損壞的封包觸發重試機制，就會立即執行。

#### 效能 {#performance}

在主要執行個體上啟用TarMK冷待命對效能幾乎沒有可衡量的影響。 額外的CPU耗用量非常低，額外的硬碟和網路IO應該不會產生效能問題。

在待命狀態中，您可以在同步處理期間預期高的CPU耗用量。 由於程式不是多執行緒，因此無法透過使用多個核心來加速該程式。 若無資料變更或轉移，則不會有可測量的活動。 連線速度會依硬體與網路環境而異，但並不取決於存放庫的大小或SSL使用。 在預估初始同步所需的時間或主要節點上的大量資料同時變更時，請記住這一點。

#### 安全性 {#security}

假設所有執行個體都運行在同一個內部網路安全性區域中，安全性違規的風險就會大幅降低。 不過，您可以透過啟用從屬節點和主節點之間的SSL連線來新增額外的安全層。 如此一來，便能避免資料遭到中間人破壞。

此外，您可以限制傳入要求的IP位址，以指定允許連線的待命執行個體。 這應該有助於確保內部網路中的任何人都無法複製存放庫。

>[!NOTE]
>
>建議在Dispatcher與冷待命設定中的伺服器之間新增負載平衡器。 負載平衡器應設定為僅將使用者流量導向至 **主要** 執行個體，以確保一致性，並防止透過冷待命機制以外的方式在待命執行個體上複製內容。

## 建立AEM TarMK冷待命設定 {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>與先前版本相比，AEM 6.3中區段節點存放區和待命存放區服務的PID已變更，如下所示：
>
>* 從org.apache.jackrabbit.oak.**外掛程式**.segment.standby.store.StandbyStoreService重新命名為org.apache.jackrabbit.oak.segment.standby.standby.store.StandbyStoreService
>* 從org.apache.jackrabbit.oak.**外掛程式**.segment.SegmentNodeStoreService重新命名為org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>請務必進行必要的設定調整以反映此變更。

為了建立TarMK冷待命設定，您首先需要執行主要安裝檔案夾的檔案系統複製到新位置，以建立待命執行個體。 然後，您可以使用將指定其角色的執行模式來啟動每個執行個體( `primary` 或 `standby`)。

以下為建立具有一個主要執行個體和一個待命執行個體的設定所需遵循的程式：

1. 安裝AEM。

1. 關閉執行個體，並將其安裝資料夾複製到執行冷待命執行個體的位置。 即使從不同的電腦執行，請務必為每個資料夾指定描述性名稱(例如 *aem-primary* 或 *aem-standby*)以區分執行個體。
1. 前往主要執行個體的安裝資料夾，並：

   1. 檢查並刪除下可能有的任何先前OSGi設定 `aem-primary/crx-quickstart/install`

   1. 建立名為的資料夾 `install.primary` 在 `aem-primary/crx-quickstart/install`

   1. 為下方的偏好節點存放區和資料存放區建立所需設定 `aem-primary/crx-quickstart/install/install.primary`
   1. 建立名為的檔案 `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` 在相同位置，並據此進行設定。 如需設定選項的詳細資訊，請參閱 [設定](/help/sites-deploying/tarmk-cold-standby.md#configuration).

   1. 如果您正在搭配外部資料存放區使用AEM TarMK執行個體，請建立名為的資料夾 `crx3` 在 `aem-primary/crx-quickstart/install` 已命名 `crx3`

   1. 將資料存放區設定檔案放入 `crx3` 資料夾。

   例如，如果您執行的是具有外部檔案資料存放區的AEM TarMK執行個體，則需要下列組態檔：

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   下方提供主要執行個體的設定範例：

   **範例：** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 啟動主要執行模式，確定您指定主要執行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 為以下專案建立新的Apache Sling記錄記錄器 **org.apache.jackrabbit.oak.segment** 封裝。 將記錄層級設為「Debug」，並將其記錄輸出指向個別的記錄檔，例如 */logs/tarmk-coldstandby.log*. 如需詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md).
1. 前往 **待命** 執行個體，並執行jar以啟動它。
1. 建立與主要記錄檔相同的記錄設定。 然後，停止執行個體。
1. 接下來，準備待命執行個體。 您可以執行與主要執行處理相同的步驟來執行此操作：

   1. 刪除下可能有的任何檔案 `aem-standby/crx-quickstart/install`.
   1. 建立名為的新資料夾 `install.standby` 在 `aem-standby/crx-quickstart/install`

   1. 建立兩個名為的組態檔：

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   1. 建立名為的新資料夾 `crx3` 在 `aem-standby/crx-quickstart/install`

   1. 建立資料存放區設定，並將其放在 `aem-standby/crx-quickstart/install/crx3`. 在此範例中，您需要建立的檔案為：

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
   1. 編輯檔案並建立必要的設定。

   以下是典型待命執行個體的組態檔範例：

   **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config範例**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. 開始 **待命** 使用待命執行模式執行個體：

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

您也可以透過以下方式透過Web主控台設定服務：

1. 前往網頁主控台： *https://serveraddress:serverport/system/console/configMgr*
1. 正在尋找名為的服務 **Apache Jackrabbit Oak Segment Tar冷待命服務** 並連按兩下以編輯設定。
1. 儲存設定，然後重新啟動執行個體，讓新設定生效。

>[!NOTE]
>
>您可以隨時檢查執行個體的角色，方法是檢查是否存在 **主要** 或 **待命** Sling設定Web控制檯中的執行模式。
>
>您可以前往 *https://localhost:4502/system/console/status-slingsettings* 並檢查 **「執行模式」** 行。

## 首次同步處理 {#first-time-synchronization}

準備完成且第一次啟動待命後，當待命執行個體追趕到主要執行個體時，執行個體之間會有大量網路流量。 您可以查閱記錄檔以觀察同步處理的狀態。

待命中 *tarmk-coldstandby.log*，您會看到類似以下的專案：

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

待命中 *error.log*，您應該會看到類似以下的專案：

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

在上述記錄檔片段中， *10.20.30.40* 是主要的IP位址。

在 **主要** *tarmk-coldstandby.log*，您會看到類似以下的專案：

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

在這種情況下，記錄中提到的「使用者端」是 **待命** 執行個體。

一旦這些專案停止顯示在記錄中，您就可以安全地假設同步程式已完成。

雖然上述專案顯示輪詢機制運作正常，但瞭解是否有任何資料在輪詢發生時進行同步通常很有用。 若要這麼做，請尋找類似下列的專案：

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

此外，以非共用執行時 `FileDataStore`，類似以下訊息將確認二進位檔案已正確傳輸：

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### 配置 {#configuration}

下列OSGi設定可用於「冷待命」服務：

* **保留設定：** 如果啟用，這會將設定儲存在存放庫中，而不是傳統的OSGi設定檔案。 建議將此設定保留在生產系統上停用，以便待命系統不會提取主要設定。

* **模式(`mode`)：** 這會選擇執行個體的執行模式。

* **連線埠（連線埠）：** 用於通訊的連線埠。 默认为 `8023`。

* **主要主機(`primary.host`)：**  — 主要執行個體的主機。 此設定僅適用於待命狀態。
* **同步間隔(`interval`)：**  — 此設定會決定同步要求之間的間隔，且僅適用於待命執行個體。

* **允許的IP範圍(`primary.allowed-client-ip-ranges`)：**  — 主要伺服器允許連線的IP範圍。
* **安全(`secure`)：** 啟用SSL加密。 若要使用此設定，必須在所有執行個體上啟用它。
* **待命讀取逾時(`standby.readtimeout`)：** 從待命執行個體發出的要求逾時（毫秒）。 使用的預設值為60000 （一分鐘）。

* **待命自動清理(`standby.autoclean`)：** 如果存放區的大小在同步處理週期上增加，請呼叫清除方法。

>[!NOTE]
>
>強烈建議主要和待命資料庫使用不同的存放庫ID，以便讓這些存放庫ID可分別用於解除安裝等服務。
>
>確定這已涵蓋的最佳方式是刪除 *sling.id* 檔案並重新啟動執行個體。

## 容錯移轉程式 {#failover-procedures}

如果主要執行個體因任何原因而失敗，您可以變更啟動執行模式，將其中一個待命執行個體設定為擔任主要執行個體的角色，如下所述：

>[!NOTE]
>
>組態檔也需要修改，以便與主要執行個體使用的設定相符。

1. 前往安裝待命執行個體的位置，然後停止它。

1. 如果您有使用設定設定的負載平衡器，此時您可以從負載平衡器的設定中移除主要負載平衡器。
1. 備份 `crx-quickstart` 資料夾中的待命安裝資料夾。 當設定新的待命時，它可作為起點。

1. 使用重新啟動執行個體 `primary` 執行模式：

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. 將新的主要專案新增至負載平衡器。
1. 建立並啟動新的待命執行個體。 如需詳細資訊，請參閱上述程式： [建立AEM TarMK冷待命設定](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## 將Hotfix套用至冷待命設定 {#applying-hotfixes-to-a-cold-standby-setup}

將Hotfix套用至冷待命設定的建議方法是將其安裝至主要執行個體，然後複製到已安裝了Hotfix的新冷待命執行個體。

您可以依照下列步驟執行此操作：

1. 前往JMX主控台並使用**org.apache.jackrabbit.oak： Status (&quot;Standby&quot;)**bean，停止冷待命執行個體上的同步化程式。 如需如何執行此動作的詳細資訊，請參閱以下章節： [監視](#monitoring).
1. 停止冷待命執行個體。
1. 在主要執行個體上安裝Hotfix。 如需如何安裝Hotfix的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md).
1. 測試執行個體在安裝後是否有問題。
1. 刪除冷待命執行個體的安裝資料夾，以移除冷待命執行個體。
1. 停止主要執行個體，並將它整個安裝資料夾的檔案系統復本複製到冷待命的位置，以複製它。
1. 重新設定新建立的複製品以做為冷待命執行個體。 如需其他詳細資訊，請參閱 [建立AEM TarMK冷待命設定。](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. 啟動主要和冷待命執行處理。

## 监测 {#monitoring}

此功能會公開使用JMX或MBean的資訊。 如此一來，您就可以使用 [JMX主控台](/help/sites-administering/jmx-console.md). 此資訊的單位為 `type org.apache.jackrabbit.oak:type="Standby"`已命名 `Status`.

**待命**

觀察待命執行個體時，您將公開一個節點。 ID通常是通用的UUID。

此節點有五個唯讀屬性：

* `Running:` 表示同步處理序是否正在執行的布林值。

* `Mode:` 使用者端：後面接著用來識別執行個體的UUID。 請注意，每次更新設定時，此UUID都會變更。

* `Status:` 目前狀態的文字表示(例如 `running` 或 `stopped`)。

* `FailedRequests:`連續錯誤的次數。
* `SecondsSinceLastSuccess:` 自上次與伺服器成功通訊以來的秒數。 它將會顯示 `-1` 若未進行任何成功的通訊。

此外還有三種可叫用的方法：

* `start():` 啟動同步程式。
* `stop():` 停止同步處理作業。
* `cleanup():` 在待命系統上執行清除作業。

**主要**

觀察主要會透過MBean公開一些一般資訊，其ID值是TarMK待命服務正在使用的連線埠號碼（預設為8023）。 大部分的方法和屬性與待命相同，但有些方法或屬性有所不同：

* `Mode:` 將一律顯示值 `primary`.

此外，可以擷取最多10個連線至主版的使用者端（待命執行處理）的資訊。 MBean ID是執行個體的UUID。 這些MBean沒有可叫用的方法，但有一些非常實用的唯讀屬性：

* `Name:` 使用者端的ID。
* `LastSeenTimestamp:` 文字表示中最後一個請求的時間戳記。
* `LastRequest:` 使用者端的最後一個要求。
* `RemoteAddress:` 使用者端的IP位址。
* `RemotePort:` 使用者端用於上次要求的連線埠。
* `TransferredSegments:` 傳輸到此使用者端的區段總數。
* `TransferredSegmentBytes:`傳輸至此使用者端的位元組總數。

## 冷待命存放庫維護 {#cold-standby-repository-maintenance}

### 修订版清理 {#revision-clean}

>[!NOTE]
>
>如果您執行 [線上修訂清除](/help/sites-deploying/revision-cleanup.md) 在主要執行個體上，不需要以下顯示的手動程式。 此外，如果您使用「線上修訂清除」，則 `cleanup ()` 待命執行個體上的作業將自動執行。

>[!NOTE]
>
>請勿在待命時執行離線修訂清除。 這並非必要，也不會減少區段存放區大小。

Adobe建議定期執行維護作業，以防止存放庫隨時間過度成長。 若要手動執行冷待命存放庫維護，請遵循下列步驟：

1. 前往JMX主控台並使用 **org.apache.jackrabbit.oak：狀態（「待命」）** bean。 如需如何執行此動作的詳細資訊，請參閱上文 [監視](/help/sites-deploying/tarmk-cold-standby.md#monitoring).

1. 停止主要AEM執行個體。
1. 在主要執行個體上執行Oak壓縮工具。 如需詳細資訊，請參閱 [維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. 啟動主要執行個體。
1. 使用第一個步驟中所述的相同JMX Bean在待命執行個體上啟動待命程式。
1. 觀察記錄並等待同步完成。 此時，待命存放庫可能會大幅增加。
1. 執行 `cleanup()` 在待命執行個體上操作，使用第一步中所述的相同JMX Bean。

待命執行個體完成與主要執行個體的同步化所花的時間可能比平常長，因為離線壓縮會有效重寫存放庫歷史記錄，因此計算存放庫中的變更需要更多時間。 也請注意一點，此程式完成後，待命的存放庫大小將與主要存放庫的大小大致相同。

作為替代方法，主要存放庫可在主要存放庫上執行壓縮後手動複製到待命，基本上每次執行壓縮時都會重建待命。

### 数据存储垃圾收集 {#data-store-garbage-collection}

請務必不時對檔案資料存放區執行個體執行垃圾收集，否則，刪除的二進位檔將保留在檔案系統上，最終會填滿磁碟機。 若要執行垃圾收集，請遵循下列程式：

1. 依照一節所述執行冷待命存放庫維護 [以上](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. 維護程式完成且執行個體已重新啟動後：

   * 在主磁碟機上，透過相關的JMX Bean執行資料存放區垃圾收集，如中所述 [本文](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * 在待命中，資料存放區垃圾收集只能透過 **BlobGarbageCollection** MBean - `startBlobGC()`. 待命狀態無法使用**RepositoryManagement **MBean。

   >[!NOTE]
   >
   >如果您未使用共用資料存放區，垃圾收集必須先在主磁碟區上執行，然後在待命磁碟區上執行。
