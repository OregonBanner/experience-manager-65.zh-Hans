---
title: Adobe Experience Manager與MongoDB
description: 瞭解成功使用MongoDB部署Adobe Experience Manager所需的工作和考量。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 0%

---

# Adobe Experience Manager與MongoDB{#aem-with-mongodb}

本文旨在增進對成功使用MongoDB部署AEM (Adobe Experience Manager)所需之任務和考量的瞭解。

如需與部署相關的詳細資訊，請參閱 [部署和維護](/help/sites-deploying/deploy.md) 區段。

## 搭配AEM使用MongoDB的時機 {#when-to-use-mongodb-with-aem}

MongoDB通常用於支援AEM作者部署，其中需符合下列其中一項條件：

* 每天超過1000位不重複使用者；
* 同時有100位以上的使用者；
* 大量頁面編輯；
* 大型轉出或啟用。

上述條件僅適用於作者執行個體，不適用於所有應以TarMK為基礎之發佈執行個體。 由於作者執行個體不允許未驗證的存取，因此使用者數量會參考已驗證的使用者。

如果不符合條件，則建議使用TarMK作用中/待命部署來解決可用性問題。 一般而言，在縮放需求大於單一硬體專案所能達成的需求時，應考慮MongoDB。

>[!NOTE]
>
>有關作者執行個體規模及同時使用者定義的其他資訊，請參閱 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### 針對AEM的最低限度的MongoDB部署 {#minimal-mongodb-deployment-for-aem}

以下是MongoDB上AEM的最低部署。 為簡化起見，已將SSL終止和HTTP Proxy元件概括。 它包含單一MongoDB復本集，包含一個主要和兩個次要復本。

![chlimage_1-4](assets/chlimage_1-4.png)

最低部署需要三個 `mongod` 設定為復本集的執行個體。 一個執行個體被選為主要，而其他執行個體被選為次要，選舉由管理 `mongod`. 附加到每個執行個體是本機磁碟。 因此，叢集可支援負載，建議使用每秒12 MB的最小輸送量，以及每秒3000多個I/O作業(IOPS)。

AEM作者已連線至 `mongod` 例項，讓每個AEM作者連線到全部三個 `mongod` 執行個體。 寫入會傳送至主要執行個體，而讀取可從任何執行個體讀取。 流量會根據Dispatcher的負載分配至任何一個作用中的AEM編寫執行個體。 Oak資料存放區是 `FileDataStore`和MongoDB監控由MMS或MongoDB Ops Manager提供，視部署位置而定。 作業系統層級和記錄檔監控由第三方解決方案提供，例如Splunk或Ganglia。

在此部署中，需要所有元件才能成功實作。 任何遺漏的元件都會讓實作無法運作。

### 作業系統 {#operating-systems}

如需AEM 6支援的作業系統清單，請參閱 [技術需求頁面](/help/sites-deploying/technical-requirements.md).

### 环境 {#environments}

如果執行專案的不同技術團隊之間有良好的溝通，則支援虛擬化環境。 這項支援包括執行AEM的團隊、擁有作業系統的團隊以及管理虛擬化基礎建設的團隊。

MongoDB執行個體的I/O容量有特定需求，必須由管理虛擬化環境的團隊管理。 如果專案使用雲端部署(例如Amazon Web Services)，則執行個體必須布建足夠的I/O容量和一致性，以支援MongoDB執行個體。 否則，MongoDB程式和Oak存放庫會執行不可靠且不規則。

在虛擬化環境中，MongoDB需要特定的I/O和VM設定，以確保MongoDB的儲存引擎不會受到VMWare資源配置原則的損害。 成功的實作可確保各個團隊之間沒有障礙，並且所有團隊都已註冊以提供所需的效能。

## 硬體考量事項 {#hardware-considerations}

### 存储 {#storage}

為了達到最佳效能的讀寫傳輸量，而不需要過早的水準擴充，MongoDB通常需要SSD儲存或儲存裝置，其效能相當於SSD。

### RAM {#ram}

使用MMAP儲存引擎的MongoDB 2.6和3.0版要求資料庫的工作集及其索引符合RAM。

RAM不足會導致效能大幅降低。 工作集和資料庫的大小高度取決於應用程式。 雖然可以做出一些估計，但最可靠的判斷所需RAM數量的方法是建置AEM應用程式並進行負載測試。

為了協助負載測試過程，可以假設工作集與資料庫總大小的比率如下：

* SSD儲存為1:10
* 1:3用於硬碟儲存

這些比率意味著，對於SSD部署，2 TB的資料庫需要200 GB的RAM。

雖然相同的限制適用於MongoDB 3.0中的WiredTiger儲存引擎，但工作集、RAM和頁面錯誤之間的關聯性並不強。 WiredTiger使用的記憶體對應方式與MMAP儲存引擎不同。

>[!NOTE]
>
>Adobe建議針對使用MongoDB 3.0的AEM 6.1部署使用WiredTiger儲存引擎。

### 資料存放區 {#data-store}

由於MongoDB工作集限制，建議獨立於MongoDB維護資料存放區。 在大多數環境中， `FileDataStore` 應該使用可用於所有AEM執行個體的NAS。 若是使用Amazon Web Services的情況，也有 `S3 DataStore`. 如果由於任何原因，資料存放區是在MongoDB中維護，資料存放區的大小應新增到資料庫總大小，工作集計算應適當調整。 此大小調整可能表示布建更多RAM以維持效能，而不發生頁面錯誤。

## 监测 {#monitoring}

監視對於成功實作專案至關重要。 只要有足夠知識，便可在MongoDB上執行AEM而不需要監視。 不過，這些知識通常是由專屬於部署各個區段的工程師來找到。

這些專業知識通常包括研究Apache Oak Core的研發工程師和MongoDB專家。

若未在所有層級進行監視，則需要程式碼庫的詳細知識才能診斷問題。 監控功能就緒且針對主要統計資料提供適當指引，實作團隊便可對異常狀況作出適當反應。

雖然可以使用命令列工具來取得叢集操作的快速快照，但要在許多主機上即時執行此作業幾乎是不可能的。 命令列工具很少在幾分鐘後提供歷史資訊，也絕不允許不同型別量度之間的交叉關聯。 一段短暫的慢速背景 `mongod` 同步作業需要大量手動操作，以針對I/O等待或來自顯然未連線之虛擬機器器之共用儲存資源的過度寫入層級建立關聯。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免費服務，可監控和管理MongoDB執行個體。 它可即時檢視MongoDB叢集的效能和健康狀況。 它同時管理雲端和私下託管的執行個體，前提是執行個體可以存取Cloud Manager監控伺服器。

它需要安裝在MongoDB執行個體上的代理程式，以連線至監控伺服器。 代理程式有三個層級：

* 可完全自動化MongoDB伺服器上所有內容的自動化代理程式，
* 可監控的監控代理程式 `mongod` 例項，
* 備份代理程式，可執行資料的排程備份。

雖然使用Cloud Manager來自動維護MongoDB叢集可讓許多例行工作變得更輕鬆，但這並非必要，而且也不會將其用於備份。 但是選擇Cloud Manager進行監視時，需要監視。

如需MongoDB Cloud Manager的詳細資訊，請參閱 [MongoDB檔案](https://docs.cloud.mongodb.com/).

### MongoDB作業管理員 {#mongodb-ops-manager}

MongoDB Ops Manager與MongoDB Cloud Manager的軟體相同。 註冊後，Ops Manager即可下載並安裝在本機私人資料中心或任何其他筆記型電腦或桌上型電腦上。 它使用本機MongoDB資料庫來儲存資料，並以與Cloud Manager相同的方式與受管理的伺服器通訊。 如果您的安全性原則禁止監控代理程式，則應使用MongoDB Ops Manager。

### 作業系統監視 {#operating-system-monitoring}

執行AEM MongoDB叢集需要作業系統層級監視。

Ganglia就是這類系統的好例子，它提供超出基本健康狀態量度（例如CPU、平均負載和可用磁碟空間）所需資訊的範圍與詳細資訊。 若要診斷問題，需要較低層級的資訊，例如平均資訊量集區層級、CPU I/O等待、FIN_WAIT2狀態的通訊端。

### 記錄彙總 {#log-aggregation}

若使用多部伺服器的叢集，生產系統需要集中記錄彙總。 Splunk等軟體支援記錄彙總，可讓團隊分析應用程式的行為模式，而無需手動收集記錄。

## 檢查清單 {#checklists}

本節說明您應採取的各種步驟，以確保在實作專案前已正確設定AEM和MongoDB部署。

### 网络 {#network}

1. 首先，請確定所有主機都有DNS專案
1. 所有主機應可透過其DNS專案從所有其他可路由主機解析
1. 所有MongoDB主機都可從相同叢集中的所有其他MongoDB主機路由
1. MongoDB主機可以將封包路由到MongoDB Cloud Manager和其他監控伺服器
1. AEM伺服器可以將封包路由到所有MongoDB伺服器
1. 任何AEM伺服器與任何MongoDB伺服器之間的封包延遲都小於2毫秒，沒有封包遺失，且標準分佈為1毫秒或更短。
1. 確保AEM和MongoDB伺服器之間最多有兩個躍點
1. 兩個MongoDB伺服器之間最多只有兩個躍點
1. 任何核心伺服器(MongoDB或AEM或任何組合)之間都沒有高於OSI Level 3的路由器。
1. 如果使用VLAN中繼或任何形式的網路通道，就必須遵守封包延遲檢查。

### AEM設定 {#aem-configuration}

#### 節點存放區設定 {#node-store-configuration}

AEM執行個體必須設定為將AEM與MongoMK搭配使用。 AEM中MongoMK實作的基礎是檔案節點存放區。

如需如何設定節點存放區的詳細資訊，請參閱 [在AEM中設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md).

以下是最小MongoDB部署的Document Node Store設定範例：

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

其中：

* `mongodburi`
MongoDB伺服器AEM必須連線到。 與預設復本集的所有已知成員建立連線。 如果使用MongoDB Cloud Manager，則會啟用伺服器安全性。 因此，連線字串必須包含合適的使用者名稱和密碼。 非企業版本的MongoDB僅支援使用者名稱和密碼驗證。 如需連線字串語法的詳細資訊，請參閱 [檔案](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
資料庫的名稱。 AEM的預設值為 
`aem-author`。

* `customBlobStore`
如果部署將二進位檔儲存在資料庫中，則二進位檔會成為工作集的一部分。 因此，請勿在MongoDB中儲存二進位檔案，偏好使用替代資料存放區，例如 
`FileSystem` nas上的資料存放區。

* `cache`
快取大小(MB)。 此空間分佈於以下專案中使用的各種快取中： 
`DocumentNodeStore`. 預設值為256 MB。 不過，Oak的讀取效能會受益於較大的快取。

* `blobCacheSize`
AEM可能會快取經常使用的Blob，以避免從資料存放區重新擷取它們。 這樣做對效能的影響更大，尤其是將Blob儲存在MongoDB資料庫時。 所有以檔案系統為基礎的資料存放區都受益於作業系統層級的磁碟快取。

#### 資料存放區設定 {#data-store-configuration}

資料存放區是用來儲存大於臨界值的檔案。 低於該臨界值時，檔案會儲存為檔案節點存放區中的屬性。 如果 `MongoBlobStore` 會使用，在MongoDB中建立專用集合來儲存blob。 此集合對下列專案的工作集有貢獻： `mongod` 執行個體，並要求 `mongod` 擁有更多RAM以避免效能問題。 因此，建議的設定是避免 `MongoBlobStore` 用於生產部署與使用 `FileDataStore` 由所有AEM執行個體共用的NAS作為後盾。 因為作業系統層級快取在管理檔案時很有效率，所以磁碟上的檔案大小下限應該設定為接近磁碟的區塊大小。 這樣做可確保檔案系統得到有效使用，並且許多小檔案不會過度影響的工作集 `mongod` 執行個體。

以下是使用MongoDB進行最低AEM部署的典型資料存放區設定：

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

其中：

* `minRecordLength`
大小（字节）. 小於或等於此大小的二進位檔會儲存在檔案節點存放區。 不會儲存blob的ID，而是儲存二進位檔的內容。 對於大於此大小的二進位檔，二進位檔的ID會儲存為節點集合中Document的屬性。 而且，二進位檔的主體會儲存在 
`FileDataStore` 在磁碟上。 4096位元組是典型的檔案系統區塊大小。

* `path`
資料存放區根的路徑。 對於MongoMK部署，此路徑必須是所有AEM執行個體都可用的共用檔案系統。 通常使用網路附加儲存(NAS)伺服器。 對於Amazon Web Services等雲端部署， 
`S3DataFileStore` 也可供使用。

* `cacheSizeInMB`
二進位快取的總大小（以MB為單位）。 用來快取小於下列值的二進位檔： 
`maxCacheBinarySize` 設定。

* `maxCachedBinarySize`
在二進位快取中快取的二進位檔案大小上限（位元組）。 如果使用檔案系統型資料存放區，不建議對資料存放區快取使用高值，因為作業系統已快取二進位檔案。

#### 停用查詢提示 {#disabling-the-query-hint}

建議您新增屬性，以停用隨所有查詢傳送的查詢提示 `-Doak.mongo.disableIndexHint=true` 當您啟動AEM時。 如此可確保MongoDB會根據內部統計資料，計算最適合使用的索引。

如果未停用查詢提示，索引的任何效能調整都不會影響AEM的效能。

#### 啟用MongoMK的永久性快取 {#enable-persistent-cache-for-mongomk}

建議為MongoDB部署啟用持續快取設定，以針對具有高I/O讀取效能的環境來最大化速度。 如需詳細資訊，請參閱 [Jackrabbit Oak檔案](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB作業系統最佳化 {#mongodb-operating-system-optimizations}

### 作業系統支援 {#operating-system-support}

MongoDB 2.6使用記憶體對應儲存引擎，對RAM和磁碟之間作業系統層級管理的某些方面很敏感。 MongoDB執行個體的查詢和讀取效能取決於避免或消除常稱為頁面錯誤的緩慢I/O操作。 這些問題為套用至 `mongod` 尤其是流程。 不要與作業系統層級的頁面錯誤混淆。

為了快速操作，MongoDB資料庫應該只存取已經在RAM中的資料。 它必須存取的資料是由索引和資料所組成。 這個索引和資料的集合稱為工作集。 當工作集大於可用的RAM時，MongoDB必須從磁碟中分頁該資料，這會產生I/O成本，並逐出已在記憶體中的其他資料。 如果逐出導致資料從磁碟重新載入，頁面錯誤會主導且效能會降低。 如果工作集是動態和可變的，則會產生更多頁面錯誤以支援操作。

MongoDB可在數種作業系統上執行，包括各種Linux®風格、Windows和macOS。 另請參閱 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 以取得其他詳細資訊。 視您的作業系統選擇而定，MongoDB有不同的作業系統層級建議。 記錄在 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 為了方便起見，在這裡進行了總結。

#### Linux® {#linux}

* 關閉透明的hugpages和defraging。 另請參閱 [透明的大型頁面設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 以取得詳細資訊。
* [調整預讀設定](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 在儲存資料庫檔案的裝置上，以符合您的使用案例。

   * 對於MMAPv1儲存引擎，如果您的工作集大於可用的RAM，而且檔案存取模式是隨機的，請考慮將讀取提前數降低到32或16。 評估不同的設定，以便找出最佳值，最大化常駐記憶體並降低頁面錯誤數目。
   * 對於WiredTiger儲存引擎，無論儲存媒體型別（旋轉、SSD等）為何，請將預先讀取設定為0。 一般而言，除非測試顯示可測量、可重複及可靠的好處，以獲得更高的預讀值，否則請使用建議的預讀設定。 [MongoDB Professional支援](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可針對非零預先讀取設定提供建議和指引。

* 如果您在虛擬環境中執行RHEL 7 / CentOS 7，請停用調整工具。
* 當RHEL 7/CentOS 7在虛擬環境中執行時，調整工具會自動叫用從效能輸送量衍生的效能設定檔，這會自動將預先讀取設定設定設為4 MB。 此設定可能會對效能造成負面影響。
* 使用SSD磁碟機的noop或截止日期磁碟排程器。
* 使用適用於客體VM中虛擬化磁碟機的noop磁碟排程器。
* 停用NUMA或設定 `vm.zone_reclaim_mode` 至0並執行 [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有節點交錯(Node Interleaving)的例項。 請參閱： [MongoDB與NUMA硬體](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 以取得詳細資訊。

* 調整硬體上的限制值，使其符合您的使用案例。 若為多個 [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古文](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 執行個體在相同使用者下執行，請相應地縮放極限值。 請參閱： [UNIX® ulimit設定](https://docs.mongodb.com/manual/reference/ulimit/) 以取得詳細資訊。

* 使用noatim進行 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 掛接點。
* 為部署設定足夠的檔案控制代碼(fs.file-max)、核心pid限制(kernel.pid_max)和每個處理序的最大執行緒數(kernel.threads-max)。 對於大型系統，下列值可提供良好的起點：

   * fs.file-max值98000，
   * 64000的kernel.pid_max值，
   * andkernel.threads-64000的最大值

* 確定系統已設定交換空間。 如需適當大小的詳細資訊，請參閱作業系統的檔案。
* 確定系統預設的TCP keepalive已正確設定。 300的值通常可為復本集和共用叢集提供更好的效能。 請參閱： [TCP keepalive時間是否會影響MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 如需詳細資訊，請參閱常見問題集。

#### Windows {#windows}

* 請考慮停用NTFS「上次存取時間」更新。 此設定類似於在類似Unix的系統上停用atime。

### WiredTiger {#wiredtiger}

從MongoDB 3.2開始，MongoDB的預設儲存引擎是WiredTiger儲存引擎。 此引擎提供一些強大且可擴充的功能，使其更適合全面的一般資料庫工作負載。 以下各節將說明這些功能。

#### 檔案層級並行 {#document-level-concurrency}

WiredTiger使用檔案層級的並行控制來執行寫入作業。 因此，多個使用者端可同時修改集合的不同檔案。

對於大多數的讀取和寫入作業，WiredTiger使用樂觀的並行控制。 WiredTiger只使用全域、資料庫和集合層級的意圖鎖定。 當儲存引擎偵測到兩個作業之間有衝突時，其中一個作業會發生寫入衝突，導致MongoDB透明地重試該作業。 某些全域作業（通常為涉及多個資料庫的短期作業）仍需要全域「執行個體範圍」鎖定。

有些其他作業（例如卸除集合）仍需要專屬的資料庫鎖定。

#### 快照和查核點 {#snapshots-and-checkpoints}

WiredTiger使用MultiVersion Concurrency Control (MVCC)。 在作業開始時，WiredTiger會提供交易資料的時間點快照。 快照會顯示記憶體內資料的一致檢視。

寫入磁碟時，WiredTiger會以一致的方式將快照中的所有資料寫入磁碟，所有資料檔案皆如此。 現在 —  [耐用](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 資料在資料檔案中當作查核點。 查核點可確保資料檔案與上一個查核點一致（含上一個查核點）。 也就是說，查核點可作為復原點。

MongoDB會設定WiredTiger，以60秒或2 GB的日誌資料為間隔建立檢查點（即將快照資料寫入磁碟）。

在寫入新查核點期間，先前的查核點仍然有效。 因此，即使MongoDB在寫入新查核點時終止或發生錯誤，在重新啟動時，MongoDB仍可從最後一個有效的查核點復原。

當WiredTiger的中繼資料表自動更新以參考新的查核點時，新的查核點將變為可存取且永久性。 存取新查核點後，WiredTiger會從舊查核點釋放頁面。

使用WiredTiger，即使不使用 [日誌](https://docs.mongodb.com/manual/reference/glossary/#term-durable)，MongoDB可以從上一個查核點復原；不過，若要復原上一個查核點之後所做的變更，請使用執行 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 日志 {#journal}

WiredTiger使用預先寫入交易登入組合，搭配 [查核點](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 以確保資料耐久性。

WiredTiger日誌會在查核點之間儲存所有資料修改。 如果MongoDB在查核點之間結束，它會使用日誌來重播自上次查核點以來修改的所有資料。 如需MongoDB寫入日誌資料至磁碟的頻率資訊，請參閱 [日誌程式](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger日誌是使用 [快速處理](https://docs.mongodb.com/manual/core/journaling/#journal-process) 壓縮程式庫。 若要指定替代壓縮演演算法或不壓縮，請使用 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定。

另請參閱 [使用WiredTiger進行日誌](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger的最小記錄大小為128位元組。 如果記錄檔記錄為128個位元組或更小，WiredTiger不會壓縮該記錄。
>
>您可以透過設定來停用日誌 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 設為false，可以減少維護分錄的額外負荷。
>
>對象 [獨立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 執行個體（未使用日誌）表示當MongoDB在查核點之間意外退出時，您會遺失一些資料修改。 針對下列成員： [復本集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)，復製程式可提供足夠的耐用性保證。

#### 压缩 {#compression}

有了WiredTiger，MongoDB支援所有集合和索引的壓縮。 壓縮會以犧牲額外的CPU為代價，將儲存空間的使用降至最低。

根據預設，WiredTiger使用區塊壓縮 [快速處理](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 所有集合和的壓縮程式庫 [字首壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 用於所有索引。

若為集合，則使用區塊壓縮 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 也可供使用。 若要指定替代壓縮演演算法或不壓縮，請使用 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定。

對於索引，為停用 [字首壓縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 設定。

壓縮設定也可以在集合和索引建立期間根據每個集合和每個索引進行配置。 另請參閱 [指定儲存引擎選項](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 選項。

對於大部分的工作負載，預設壓縮設定可平衡儲存效率與處理需求。

WiredTiger日誌也會依預設壓縮。 如需有關分錄壓縮的資訊，請參閱 [日誌](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 記憶體使用率 {#memory-use}

使用WiredTiger時，MongoDB會同時使用WiredTiger內部快取與檔案系統快取。

從3.4版開始，WiredTiger內部快取預設會使用以下兩者中較大的一項：

* 50%的RAM減去1 GB，或
* 256毫巴

根據預設，WiredTiger會對所有集合使用Snappy區塊壓縮，並對所有索引使用前置詞壓縮。 壓縮預設值可在全域層級設定，也可以在集合和索引建立期間根據集合和索引進行設定。

WiredTiger內部快取與磁碟格式中的資料使用不同的表示方式：

* 檔案系統快取中的資料與磁碟上的格式相同，包括資料檔案的任何壓縮優點。 作業系統使用檔案系統快取來減少磁碟I/O。

載入到WiredTiger內部快取的索引與磁碟上的格式有不同的資料表示法，但是仍然可以利用索引首碼壓縮來減少RAM使用量。

索引首碼壓縮會從索引欄位中刪除重複的前碼。

WiredTiger內部快取中的集合資料是未壓縮的，並使用與磁碟格式不同的表示方式。 區塊壓縮可大幅節省磁碟上的儲存空間，但資料必須解壓縮才能由伺服器操作。

透過檔案系統快取，MongoDB會自動使用WiredTiger快取或其他處理序未使用的所有可用記憶體。

若要調整WiredTiger內部快取的大小，請參閱 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). 避免將WiredTiger內部快取大小增加到超過其預設值。

### NUMA {#numa}

NUMA （非統一記憶體存取）可讓核心管理記憶體對應到處理器核心的方式。 雖然此程式會嘗試讓核心的記憶體存取速度更快，以確保核心能夠存取所需的資料，但NUMA會干擾MMAP，導致無法預測讀取情形，造成額外的延遲。 因此，必須為以下專案停用NUMA `mongod` 在所有支援的作業系統上處理。

本質上，在NUMA架構中，記憶體會連線至CPU，而CPU會連線至匯流排。 在SMP或UMA架構中，記憶體會連線至匯流排並由CPU共用。 當執行緒在NUMA CPU上分配記憶體時，它會根據原則進行分配。 預設值是配置連線到執行緒本機CPU的記憶體，除非沒有可用空間，此時會以較高的成本使用可用的CPU的記憶體。 配置之後，記憶體不會在CPU之間移動。 配置是由從父系執行緒繼承的原則執行，這最終是啟動處理序的執行緒。

在許多將電腦視為多核心統一記憶體架構的資料庫中，此情況會導致初始CPU先滿滿，而次要CPU稍後再滿。 如果中央執行緒負責配置記憶體緩衝區，則特別正確。 解決方案是變更用來啟動「 」的主執行緒的NUMA原則 `mongod` 透過執行以下命令來處理：

```shell
numactl --interleaved=all <mongod> -f config
```

此原則會以循環配置方式為所有CPU節點配置記憶體，以確保所有節點上的均分分佈。 它不會產生記憶體的最高效能存取，如同具有多個CPU硬體的系統。 大約一半的記憶體操作速度較慢，而且是在匯流排上進行，但是 `mongod` 並未以最佳方式寫入NUMA目標，因此這是合理的折衷。

### NUMA問題 {#numa-issues}

如果 `mongod` 處理程式是從以下位置以外的位置啟動： `/etc/init.d` 資料夾，可能尚未以正確的NUMA原則開頭。 根據預設原則的不同，可能會出現問題。 原因是各種MongoDB的Linux® Package Manager安裝程式也安裝了包含組態檔的服務 `/etc/init.d` 會執行上述步驟。 如果您直接從封存安裝並執行MongoDB ( `.tar.gz`)，您必須手動執行mongod，在 `numactl` 程式。

>[!NOTE]
>
>如需有關可用NUMA原則的詳細資訊，請參閱 [numactl檔案](https://linux.die.net/man/8/numactl).

MongoDB程式在不同配置原則下的行為不同：

```

```

* `-membind=<nodes>`
僅在列出的節點上配置。 Mongod不會在列出的節點上配置記憶體，而且可能不會使用所有可用的記憶體。

* `-cpunodebind=<nodes>`
只在節點上執行。 Mongod只會在指定的節點上執行，而且只會使用這些節點上的可用記憶體。

* `-physcpubind=<nodes>`
僅於列出的CPU （核心）上執行。 Mongod只會在列出的CPU上執行，而且只使用這些CPU上可用的記憶體。

* `--localalloc`
一律在目前節點上配置記憶體，但使用執行緒執行的所有節點。 如果一個執行緒執行配置，則只會使用該CPU可用的記憶體。

* `--preferred=<node>`
偏好配置至節點，但如果偏好節點已滿，則會退回給其他節點。 可以使用定義節點的相對表示法。 此外，執行緒會在所有節點上執行。

某些原則可能會造成提供給的所有可用RAM不足 `mongod` 程式。 與MySQL不同，MongoDB主動避免作業系統層級分頁，因此 `mongod` 處理序可能會取得較少的可用記憶體。

#### 交換 {#swapping}

由於資料庫的記憶體密集性質，作業系統層級交換必須停用。 MongoDB程式會避免依設計進行交換。

#### 遠端檔案系統 {#remote-filesystems}

不建議將NFS等遠端檔案系統用於MongoDB的內部資料檔案（Mongod處理資料庫檔案），因為它們會導致太多延遲。 不要混淆Oak Blob (FileDataStore)儲存（建議使用NFS）所需的共用檔案系統。

#### 預讀 {#read-ahead}

向前調整讀取，以便在使用隨機讀取來分頁頁面時，不會從磁碟讀取不必要的區塊。 這樣的結果意味著不必要的I/O頻寬消耗。

### Linux®需求 {#linux-requirements}

#### 最小核心版本 {#minimum-kernel-versions}

* **2.6.23** 的 `ext4` 檔案系統

* **2.6.25** 的 `xfs` 檔案系統

#### 資料庫磁碟的建議設定 {#recommended-settings-for-database-disks}

**關閉時間**

建議您 `atime` 會關閉包含資料庫的磁碟。

**設定NOOP磁碟排程器**

执行以下操作：

首先，檢查透過執行以下命令設定的I/O排程器：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果回應為 `noop`，您無需執行任何其他動作。

如果NOOP不是已設定的I/O排程器，您可以透過執行來變更它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**調整預先讀取值**

建議您在執行MongoDB資料庫的磁碟上使用32的值。 此值總計為16 KB。 您可以執行下列動作加以設定：

```shell
sudo blockdev --setra <value> <device>
```

#### 啟用NTP {#enable-ntp}

請確定您已在裝載MongoDB資料庫的機器上安裝並執行NTP。 例如，您可以在CentOS電腦上使用yum Package Manager進行安裝：

```shell
sudo yum install ntp
```

安裝NTP精靈並成功啟動後，您可以檢查伺服器的時間偏移檔案。

#### 停用透明的大型頁面 {#disable-transparent-huge-pages}

Red Hat® Linux®使用稱為Transparent Great Pages (THP)的記憶體管理演演算法。 如果您使用作業系統處理資料庫工作負載，建議您停用它。

您可以依照下列程式將其停用：

1. 開啟 `/etc/grub.conf` 檔案的文字編輯器。
1. 將下列行加入grub.conf檔案：

   ```xml
   transparent_hugepage=never
   ```

1. 最後，執行以檢查設定是否已生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果停用THP，上述命令的輸出應該是：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>如需透明大型頁面的詳細資訊，請參閱此 [文章](https://access.redhat.com/solutions/46111).

#### 停用NUMA {#disable-numa}

在啟用NUMA的大多數安裝中，如果MongoDB精靈是從 `/etc/init.d` 資料夾。

如果不是這種情況，您可以對每個處理序層級停用NUMA。 若要停用，請執行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

位置 `<path_to_process>` 是mongod流程的路徑。

接著，執行以停用區域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 調整mongod程式的ulimit設定 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®可讓您透過以下方式設定資源配置的控制權： `ulimit` 命令。 此設定可依使用者或每個程式來完成。

建議您根據以下規則設定mongod程式的ulimit [MongoDB建議的上限設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### 測試MongoDB I/O效能 {#test-mongodb-i-o-performance}

MongoDB提供一個工具，稱為 `mongoperf` 這是為了測試I/O效能而設計的。 建議您使用它來測試組成您基礎建設的所有MongoDB執行個體的效能。

有關如何使用的資訊 `mongoperf`，檢視 [MongoDB檔案](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>此 `mongoperf` 是在執行它的平台上顯示MongoDB效能的指標。 因此，不應將結果視為生產系統效能的最終結果。
>
>如需更精確的效能結果，您可以使用 `fio` Linux®工具。

**在組成您部署的虛擬機器器上測試讀取效能**

安裝工具後，切換至MongoDB資料庫目錄以執行測試。 然後，執行以開始第一個測試 `mongoperf`使用此設定：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

對於所有MongoDB執行個體，所需的輸出應高達每秒2 GB (2 GB/s)和以32個執行緒執行的500.000 IOPS。

執行第二次測試，這次使用記憶體對應檔案，方法是設定 `mmf:true` 引數：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二次測試的輸出應該會比第一次高很多，表示記憶體傳輸效能。

>[!NOTE]
執行測試時，請檢查作業系統監視系統中相關虛擬機器器的I/O使用狀況統計資料。 如果I/O讀取的值低於100%，表示您的虛擬機器器可能有問題。

**測試主要MongoDB執行個體的寫入效能**

接下來，執行以檢查主要MongoDB執行個體的I/O寫入效能 `mongoperf` 從MongoDB資料庫目錄，使用相同的設定值：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的輸出應為每秒12 MB，並達到約3000 IOPS，而且執行緒數目幾乎沒有差異。

## 虛擬化環境的步驟 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果您使用WMWare ESX來管理和部署虛擬化環境，請務必從ESX主控台執行下列設定，以適應MongoDB的操作：

1. 關閉記憶體膨脹
1. 為裝載MongoDB資料庫的虛擬機器器預先配置和保留記憶體
1. 使用儲存I/O控制將足夠的I/O配置給 `mongod` 程式。
1. 透過設定來保證裝載MongoDB的電腦的CPU資源 [CPU保留](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. 請考慮使用ParaVirtual I/O驅動程式。 另請參閱 [知識庫文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

如需有關如何使用Amazon Web Services設定MongoDB的檔案，請檢視 [設定AWS整合](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB網站上的文章。

## 部署前保護MongoDB {#securing-mongodb-before-deployment}

檢視此文章於 [安全地部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 瞭解部署前如何保護資料庫設定的安全建議。

## Dispatcher {#dispatcher}

### 選擇Dispatcher的作業系統 {#choosing-the-operating-system-for-the-dispatcher}

為了正確為您的MongoDB部署提供服務，託管Dispatcher的作業系統必須正在執行 **Apache httpd** **版本2.4或更新版本。**

此外，請確定組建中使用的所有程式庫都是最新的，以將對安全性的影響降至最低。

### Dispatcher設定 {#dispatcher-configuration}

典型的Dispatcher設定會讓單一AEM執行個體的請求輸送量多出10到20倍。

由於Dispatcher是無狀態的，因此它可以輕鬆水平縮放。 在某些部署中，作者必須限制存取特定資源。 建議您搭配編寫執行個體使用Dispatcher。

在沒有Dispatcher的情況下執行AEM需要由其他應用程式執行SSL終止和負載平衡。 此為必要操作，因為工作階段必須與其建立所在的AEM執行個體具有相似性，這個概念稱為粘性連線。 原因是為了確保內容的更新顯示最小的延遲。

檢查 [Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 以取得如何設定的詳細資訊。

### 其他設定 {#additional-configuration}

#### 粘性连接 {#sticky-connections}

粘性連線可確保同一個使用者的個人化頁面和工作階段資料都在AEM的相同執行個體上撰寫。 此資料會儲存在執行個體上，因此來自相同使用者的後續請求會傳回至相同執行個體。

建議對路由傳送請求至AEM執行個體的所有內部層啟用粘性連線，鼓勵後續請求到達相同的AEM執行個體。 這麼做有助於將延遲降至最低，否則在執行個體之間更新內容時，延遲現象會非常明顯。

#### 過期時間長 {#long-expires}

依預設，從AEM Dispatcher傳送的內容具有Last-Modified和Etag標頭，沒有內容到期的指示。 此流程可確保使用者介面一律取得最新版本的資源。 這也表示瀏覽器會執行GET作業，以檢視資源是否已變更。 因此，它可能會導致HTTP回應為304 （未修改）的多個請求，具體取決於頁面載入。 對於未過期的資源，設定Expires標頭並移除Last-Modified和ETag標頭會導致快取內容。 而且，在符合Expires標頭中的日期之前，不會再提出更新請求。

不過，使用此方法表示沒有合理的方式可讓資源在Expires標頭過期之前在瀏覽器中過期。 若要緩解此工作流程，可以將HtmlClientLibraryManager設定為使用使用者端程式庫不可變的URL。

這些URL保證不會變更。 當URL中包含的資源內文變更時，這些變更會反映在URL中，以確保瀏覽器要求正確版本的資源。

預設設定會將選取器新增至HtmlClientLibraryManager。 作為選擇器，資源會在Dispatcher中快取，而選擇器保持不變。 此外，此選擇器也可用來確保正確的到期行為。 預設選擇器會遵循 `lc-.*?-lc` 模式。 下列Apache httpd設定指令可確保符合該模式的所有請求都以適當的到期時間提供。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 無嗅探 {#no-sniff}

在不使用內容型別的情況下傳送內容時，許多瀏覽器會嘗試透過讀取內容的前幾個位元組來猜測內容型別。 此方法稱為「探查」。 嗅探會開啟安全性弱點，因為可以寫入存放庫的使用者可能會上傳沒有內容型別的惡意內容。

因此，建議您新增 `no-sniff` Dispatcher提供的資源的標頭。 不過，Dispatcher不會快取標頭。 因此，這表示任何從本機檔案系統提供的內容都會由其擴充功能決定其內容型別，而不是使用來自其原始AEM伺服器的原始內容型別標頭。

如果已知網頁應用程式從未在沒有檔案型別的情況下提供快取資源，則無法安全地啟用嗅探。

您可以啟用「無探查」：

```xml
Header set X-Content-Type-Options "nosniff"
```

也可以選擇啟用：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 內容安全性原則 {#content-security-policy}

預設的Dispatcher設定允許開放的內容安全性原則，也稱為CSP。 這些設定可讓頁面從受瀏覽器沙箱的預設原則約束的所有網域載入資源。

最好限制可從何處載入資源，以避免從不受信任或未驗證的外部伺服器將程式碼載入JavaScript引擎。

CSP可微調原則。 不過，在複雜的應用程式中，開發CSP標頭時須謹慎，因為過於嚴格的原則可能會破壞部分使用者介面。

>[!NOTE]
如需此運作方式的詳細資訊，請參閱 [內容安全性原則的OWASP頁面](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### 大小調整 {#sizing}

如需有關大小調整的詳細資訊，請參閱 [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md).

### MongoDB效能最佳化 {#mongodb-performance-optimization}

如需MongoDB效能的一般資訊，請參閱 [分析MongoDB效能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 已知限制 {#known-limitations}

### 同時安裝 {#concurrent-installations}

雖然MongoMK支援同時使用單一資料庫的多個AEM執行個體，但並不支援同時安裝。

若要解決此問題，請確定先使用單一成員執行安裝，並在第一個成員完成安裝後新增其他成員。

### 頁面名稱長度 {#page-name-length}

如果AEM在MongoMK持續性管理員部署上執行， [頁面名稱長度上限為150個字元。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
請參閱 [MongoDB檔案](https://docs.mongodb.com/manual/reference/limits/) 以便熟悉MongoDB的已知限制和臨界值。
