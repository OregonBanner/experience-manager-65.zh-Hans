---
title: 在AEM 6中設定節點存放區和資料存放區
description: 瞭解如何設定節點存放區和資料存放區，以及如何執行資料存放區垃圾收集。
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '3521'
ht-degree: 2%

---

# 在AEM 6中設定節點存放區和資料存放區{#configuring-node-stores-and-data-stores-in-aem}

## 简介 {#introduction}

在Adobe Experience Manager (AEM)中，二進位資料可與內容節點分開儲存。 二進位資料儲存在資料存放區中，而內容節點則儲存在節點存放區中。

資料存放區和節點存放區都可使用OSGi設定進行設定。 每個OSGi設定都使用持續性識別碼(PID)參考。

## 設定步驟 {#configuration-steps}

若要同時設定節點存放區和資料存放區，請執行下列步驟：

1. 將AEM快速入門JAR檔案複製到其安裝目錄。
1. 建立資料夾 `crx-quickstart/install` 安裝目錄中的。
1. 首先，建立包含您要在中使用的節點存放區選項名稱的組態檔，以設定節點存放區。 `crx-quickstart/install` 目錄。

   例如，檔案節點存放區(AEM MongoMK實作的基礎)會使用檔案 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. 編輯檔案，並設定組態選項。
1. 以您要使用之資料存放區的PID建立設定檔。 編輯檔案以設定組態選項。

   >[!NOTE]
   >
   >另請參閱 [節點存放區設定](#node-store-configurations) 和 [資料存放區設定](#data-store-configurations) 以取得設定選項。

1. 啟動AEM。

## 節點存放區設定 {#node-store-configurations}

>[!CAUTION]
>
>較新版本的Oak對OSGi設定檔案採用新的命名方案和格式。 新的命名配置要求設定檔必須命名為 **.config** 而新格式需要輸入值，而且 [在此處記錄](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>如果您從舊版Oak升級，請務必備份 `crx-quickstart/install`資料夾優先。 升級後，將資料夾內容還原至升級安裝，並從修改組態檔的副檔名 **.cfg** 至 **.config**.
>
>如果您正在閱讀本文章，為從升級做準備 **AEM 5.x** 安裝，請務必參閱 [升級](https://experienceleague.adobe.com/docs/) 說明檔案優先。

### 區段節點存放區 {#segment-node-store}

區段節點存放區是Adobe在AEM6中實施TarMK的基礎。 它會使用 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 設定的PID。

>[!CAUTION]
>
>區段節點存放區的PID已變更 `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` / AEM 6至 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` 在AEM 6.3中。請務必進行必要的設定調整以反映此變更。

您可以設定下列選項：

* `repository.home`：存放庫相關資料儲存所在的存放庫首頁的路徑。 依預設，區段檔案儲存在 `crx-quickstart/segmentstore` 目錄。

* `tarmk.size`：區段的大小上限（以MB為單位）。 預設最大為256MB。
* `customBlobStore`：表示使用自訂資料存放區的布林值。 AEM 6.3及更高版本的預設值為true。 AEM 6.3之前的版本預設為false。

以下是範例 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 檔案：

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### 檔案節點存放區 {#document-node-store}

檔案節點存放區是AEM MongoMK實作的基礎。 它會使用 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID。 下列組態選項可供使用：

* `mongouri`：此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 連線至Mongo資料庫時需要。 預設值為 `mongodb://localhost:27017`

* `db`：Mongo資料庫的名稱。 預設值為 **Oak** ``. However, new AEM 6 installations use **aem-author** ``作為預設資料庫名稱。

* `cache`：快取大小（以MB為單位）。 這會分散在DocumentNodeStore中使用的各種快取中。 預設值為 `256`

* `changesSize`：Mongo中用於快取差異輸出的限定集合大小（以MB為單位）。 預設值為 `256`

* `customBlobStore`：表示將使用自訂資料存放區的布林值。 默认为 `false`。

以下是範例 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` 檔案：

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## 資料存放區設定 {#data-store-configurations}

在處理大量二進位檔時，建議使用外部資料存放區，而非預設節點存放區，以最大化效能。

例如，如果您的專案需要許多媒體資產，將它們儲存在File或S3 Data Store底下，比直接將它們儲存在MongoDB中更快地進行存取。

File Data Store的效能比MongoDB更好，而且大量資產的Mongo備份和還原作業速度也較慢。

不同資料存放區和設定的詳細資訊如下所述。

>[!NOTE]
>
>若要啟用自訂資料存放區，您必須確定 `customBlobStore` 設為 `true` 在個別節點存放區設定檔案中([區段節點存放區](/help/sites-deploying/data-store-config.md#segment-node-store) 或 [檔案節點存放區](/help/sites-deploying/data-store-config.md#document-node-store))。

### 文件数据存储 {#file-data-store}

此為的實作 [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) 在Jackrabbit 2中出現。 它提供一種將二進位資料儲存為檔案系統上一般檔案的方法。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID。

這些設定選項可供使用：

* `repository.home`：儲存各種存放庫相關資料的存放庫首頁的路徑。 根據預設，二進位檔案會儲存在 `crx-quickstart/repository/datastore` 目錄

* `path`：儲存檔案的目錄路徑。 若指定，則優先於 `repository.home` 值

* `minRecordLength`：儲存在資料存放區中的檔案大小下限（位元組）。 系統會內嵌小於此值的二進位內容。

>[!NOTE]
>
>使用NAS儲存共用檔案資料存放區時，請務必只使用高效能裝置以避免效能問題。

## Amazon S3資料存放區 {#amazon-s-data-store}

AEM可設定為將資料儲存在Amazon的Simple Storage Service (S3)。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 設定的PID。

若要啟用S3資料存放區功能，必須下載並安裝包含S3資料存放區聯結器的Feature Pack。 前往 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) 並從feature pack 1.10.x版（例如com.adobe.granite.oak.s3connector-1.10.0.zip）下載最新版本。 此外，您必須下載並安裝列於「 」的最新AEM Service Pack [AEM 6.5發行說明](/help/release-notes/release-notes.md) 頁面。

>[!NOTE]
>
>搭配TarMK使用AEM時，二進位檔預設會儲存在 `FileDataStore`. AEM若要搭配S3資料存放區使用TarMK，您必須使用 `crx3tar-nofds` 執行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照以下步驟安裝和設定S3 Connector：

1. 將Feature Pack zip檔案的內容解壓縮至暫存資料夾。

1. 前往暫存資料夾，並導覽至下列位置：

   ```xml
   jcr_root/libs/system/install
   ```

   將以上位置的所有內容複製到 `<aem-install>/crx-quickstart/install.`

1. 如果AEM已設定為搭配Tar或MongoDB儲存體使用，請從***中移除任何現有的設定檔&lt;aem-install>***/*crx-quickstart*/*安裝* 資料夾，然後再繼續。 必須移除的檔案包括：

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回功能套件已擷取的暫存位置，並複製下列資料夾的內容：

   * `jcr_root/libs/system/config`

   到

   * `<aem-install>/crx-quickstart/install`

   請確定您僅複製目前組態所需的組態檔。 對於專用資料存放區和共用資料存放區設定，請複製 `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 檔案。

   >[!NOTE]
   >
   >在叢集設定中，請逐一在叢集的所有節點上執行上述步驟。 此外，請確定對所有節點使用相同的S3設定。

1. 編輯檔案並新增您的設定所需的設定選項。
1. 啟動AEM。

## 升級至新版1.10.x S3 Connector {#upgrading-to-a-new-version-of-the-s-connector}

若要升級至1.10.x S3聯結器的新版本（例如，從1.10.0到1.10.4），請遵循下列步驟：

1. 停止AEM執行個體。

1. 導覽至 `<aem-install>/crx-quickstart/install/15` AEM ，並備份其內容。
1. 備份後，刪除S3 Connector的舊版本及其相依性，方法是刪除 `<aem-install>/crx-quickstart/install/15` 資料夾，例如：

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >上述檔案名稱僅供說明之用。

1. 從下載1.10.x Feature Pack的最新版本 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. 將內容解壓縮至個別資料夾，然後導覽至 `jcr_root/libs/system/install/15`.
1. 將jar檔案複製到 **&lt;aem-install>**/crx-quickstart/install/15在AEM安裝資料夾中。
1. 啟動AEM並檢查聯結器功能。

您可以使用包含下列選項的設定檔案。

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### S3 Connector組態檔選項 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>S3聯結器支援IAM使用者驗證和IAM角色驗證。 若要使用IAM角色驗證，請省略 `accessKey` 和 `secretKey` 設定檔案中的值。 然後S3聯結器會預設為 [IAM角色](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) 指派給執行個體。

| 键 | 描述 | 默认 | 必填 |
| --- | --- | --- | --- |
| accessKey | 有權存取貯體的IAM使用者的存取金鑰ID。 |  | 是，不使用IAM角色時。 |
| secretKey | 可存取貯體的IAM使用者機密存取金鑰。 |  | 是，不使用IAM角色時。 |
| cacheSize | 本機快取的大小（位元組）。 | 64GB | 否. |
| connectionTimeout | 設定初始建立連線時逾時前的等待時間（毫秒）。 | 10000 | 否. |
| maxCachedBinarySize | 大小小於或等於此值（位元組）的二進位檔會儲存在記憶體快取中。 | 17408 (17 KB) | 否. |
| maxConnections | 設定允許的開啟HTTP連線數目上限。 | 50 | 否. |
| maxErrorRetry | 設定失敗（可重試）要求的重試次數上限。 | 3 | 否. |
| minRecordLength | 應儲存在資料存放區中的物件大小下限（位元組）。 | 16384 | 否. |
| 路径 | AEM資料存放區的本機路徑。 | `crx-quickstart/repository/datastore` | 否. |
| proxyHost | 設定使用者端連線的選用代理主機。 |  | 否. |
| proxyPort | 設定使用者端連線通過的可選Proxy連線埠。 |  | 否. |
| s3Bucket | S3儲存貯體的名稱。 |  | 是 |
| s3EndPoint | S3 REST API端點。 |  | 否. |
| s3Region | 儲存貯體所在的區域。 檢視此 [頁面](https://docs.aws.amazon.com/general/latest/gr/s3.html) 以取得更多詳細資料。 | 執行AWS執行個體的區域。 | 否. |
| socketTimeout | 設定在連線逾時及關閉之前，透過已建立且開啟的連線傳輸資料所需的等待時間（毫秒）。 | 50000 | 否. |
| stagingPurgeInterval | 從暫存快取中清除已完成的上傳的時間間隔（以秒為單位）。 | 300 | 否. |
| stagingRetryInterval | 重試失敗的上傳間隔（以秒為單位）。 | 600 | 否. |
| stagingSplitPercentage | 的百分比 `cacheSize` 用於中繼非同步上傳。 | 10 | 否. |
| uploadthreads | 用於非同步上傳的上傳執行緒數目。 | 10 | 否. |
| writeThreads | 用於透過S3傳輸管理器寫入的並行執行緒數目。 | 10 | 否. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### DataStore快取 {#data-store-caching}

>[!NOTE]
>
>的DataStore實作 `S3DataStore`， `CachingFileDataStore` 和 `AzureDataStore` 支援本機檔案系統快取。 此 `CachingFileDataStore` 當DataStore位於NFS （網路檔案系統）上時，實作很有用。

從舊版快取實作（Oak 1.6以前版本）升級時，本機檔案系統快取目錄的結構會有差異。 在舊的快取結構中，下載的檔案和上傳的檔案都直接放在快取路徑下。 新結構會將下載和上傳分開，並將它們儲存在名為的兩個目錄中 `upload` 和 `download` 快取路徑下。 升級程式應是順暢的，任何擱置的上傳都應排程進行上傳，且任何先前下載在快取中的檔案都會在初始化時放入快取中。

您也可以使用，將快取離線升級。 `datastorecacheupgrade` oak-run的命令。 如需如何執行命令的詳細資訊，請檢查 [讀我檔案](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) 用於oak-run模組。

快取具有大小限制，可以使用cacheSize引數加以設定。

#### 下载 {#downloads}

從DataStore存取要求檔案/blob之前，會先檢查本機快取是否有記錄。 當快取超過設定的限制時(請參閱 `cacheSize` 引數)時，某些檔案會被逐出，以回收空間。

#### 非同步上傳 {#async-upload}

快取支援非同步上傳至DataStore。 檔案會在本機暫存於快取中（在檔案系統上），而非同步工作會開始上傳檔案。 非同步上傳的數量受中繼快取大小限制。 使用設定暫存快取的大小 `stagingSplitPercentage` 引數。 此引數會定義用於暫存快取的快取大小百分比。 此外，下載可用的快取百分比計算如下 **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

非同步上傳是多執行緒，並且執行緒數目是使用 `uploadThreads` 引數。

上傳完成後，檔案會移至主下載快取。 當中繼快取大小超過其限制時，檔案會同步上傳至DataStore，直到前一個非同步上傳完成且中繼快取中再次有可用空間為止。 上傳的檔案會透過週期性工作從臨時區域移除，其間隔是由 `stagingPurgeInterval` 引數。

失敗的上傳（例如，由於網路中斷）會置於重試佇列並定期重試。 重試間隔是透過以下方式設定的： `stagingRetryInterval parameter`.

#### 使用Amazon S3設定無二進位檔復寫 {#configuring-binaryless-replication-with-amazon-s}

若要使用S3設定無二進位檔復寫，必須執行下列步驟：

1. 安裝作者和發佈執行個體，並確定它們已正確啟動。
1. 透過開啟以下頁面前往復寫代理程式設定： *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. 按下 **編輯** 中的按鈕 **設定** 區段。
1. 變更 **序列化** 輸入選項至 **少二進位**.

1. 新增引數&quot; `binaryless`= `true`」在傳輸uri中。 變更後，URI看起來應該類似下列：

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. 重新啟動所有製作和發佈執行個體，讓變更生效。

#### 使用S3和MongoDB建立叢集 {#creating-a-cluster-using-s-and-mongodb}

1. 使用以下命令解壓縮CQ快速入門：

   `java -jar cq-quickstart.jar -unpack`

1. 解壓縮AEM後，在安裝目錄中建立一個資料夾 *crx-quickstart*/*安裝*.

1. 在內建立這兩個檔案 `crx-quickstart` 資料夾：

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   建立檔案後，視需要新增設定選項。

1. 如上所述，安裝S3資料存放區所需的兩個套件組合。
1. 請確定已安裝MongoDB並且執行個體 `mongod` 執行中。
1. 使用以下命令啟動AEM：

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. 對第二個AEM例項重複步驟1到4。
1. 啟動第二個AEM執行個體。

#### 設定共用資料存放區 {#configuring-a-shared-data-store}

1. 首先，在共用資料存放區所需的每個執行個體上建立資料存放區設定檔案：

   * 如果您使用 `FileDataStore`，建立名為的檔案 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 並將其放入 `<aem-install>/crx-quickstart/install` 資料夾。

   * 如果使用S3作為資料存放區，請建立名為的檔案o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` 在 `<aem-install>/crx-quickstart/install` 資料夾如上所示。

1. 修改每個執行個體上的資料存放區組態檔，使其指向相同的資料存放區。 如需詳細資訊，請參閱 [本文](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. 如果執行個體是從現有伺服器複製而來，您必須移除 `clusterId` 存放庫離線時使用最新oak-run工具執行的新執行個體。 您必須執行的命令是：

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >如果已設定區段節點存放區，則必須指定存放庫路徑。 依預設，路徑為 `<aem-install-folder>/crx-quickstart/repository/segmentstore.` 如果已設定Document節點存放區，您可以使用 [Mongo連線字串URI](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >Oak-run工具可從以下位置下載：
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >您必須根據您在AEM安裝中使用的Oak版本，使用不同版本的工具。 在使用工具之前，請檢視以下版本需求清單：
   >
   >
   >
   >    * 針對Oak版本 **1.2.x** 使用Oak-run **1.2.12或更新版本**
   >    * 針對Oak版本 **比以上版本更新**，使用與AEM安裝的Oak核心相符的Oak-run版本。


1. 最後，驗證設定。 若要驗證，請尋找由共用該檔案的每個存放庫新增到資料存放區的唯一檔案。 檔案的格式為 `repository-[UUID]`，其中UUID是每個個別存放庫的唯一識別碼。

   因此，正確的設定應具有與共用資料存放區的存放庫相同數目的唯一檔案。

   根據資料存放區，檔案的儲存方式不同：

   * 對於 `FileDataStore` 這些檔案會在資料存放區資料夾的根路徑下建立。
   * 對於 `S3DataStore` 這些檔案會建立在已設定的S3貯體中，位於 `META` 資料夾。

## Azure 数据存储 {#azure-data-store}

可以將AEM設定為將資料儲存在Microsoft®的Azure儲存體服務中。 它會使用 `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` 設定的PID。

若要啟用Azure資料存放區功能，必須下載並安裝包含Azure Connector的功能套件。 前往 [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) 並從feature pack 1.6.x版（例如com.adobe.granite.oak.azureblobconnector-1.6.3.zip）下載最新版本。

>[!NOTE]
>
>搭配TarMK使用AEM時，二進位檔案預設會儲存在FileDataStore中。 AEM若要搭配Azure DataStore使用TarMK，您必須使用 `crx3tar-nofds` 執行模式，例如：

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

下載後，您可以依照以下方式安裝和設定Azure聯結器：

1. 將Feature Pack zip檔案的內容解壓縮至暫存資料夾。

1. 移至暫存資料夾，並複製下列專案的內容： `jcr_root/libs/system/install` 至 `<aem-install>crx-quickstart/install` 資料夾。
1. 如果AEM已設定為搭配Tar或MongoDB儲存體使用，請從 `/crx-quickstart/install` 資料夾，然後再繼續。 必須移除的檔案包括：

   ForMongoMK：

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   若為TarMK：

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. 返回功能套件已擷取的臨時位置，並複製的內容 `jcr_root/libs/system/config` 至 `<aem-install>/crx-quickstart/install` 資料夾。
1. 編輯組態檔，並新增您的設定所需的組態選項。
1. 啟動AEM。

您可以搭配下列選項使用組態檔：

* azureSas=」：在聯結器的1.6.3版本中，新增了Azure共用存取簽名(SAS)支援。 **如果組態檔中同時存在SAS和儲存憑證，則SAS具有優先權。** 如需SAS的詳細資訊，請參閱 [正式檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview). 請確定&#39;=&#39;字元已逸出，如&#39;\=&#39;。

* azureBlobEndpoint=&quot;： Azure Blob端點。 例如， https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;：儲存體帳戶名稱。 如需Microsoft® Azure驗證認證的詳細資訊，請參閱 [正式檔案](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account).

* secretKey=&quot;：儲存體存取金鑰。 請確定&#39;=&#39;字元已逸出，如&#39;\=&#39;。
* container=&quot;： Microsoft® Azure Blob儲存體容器名稱。 容器是一組Blob。 如需其他詳細資訊，請閱讀 [正式檔案](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN).
* maxConnections=&quot;：每個作業同時發出的要求數目。 默认值为 1。
* maxErrorRetry=&quot;&quot;：每個請求的重試次數。 默认值为 3。
* socketTimeout=&quot;&quot;：要求所使用的逾時間隔（毫秒）。 預設值為5分鐘。

除了上述設定外，您也可以設定下列設定：

* path：資料存放區的路徑。 預設值為 `<aem-install>/repository/datastore.`
* RecordLength：應該儲存在資料存放區中的物件大小下限。 預設值為16 KB。
* maxCachedBinarySize：大小小於或等於此大小的二進位檔儲存在記憶體快取中。 大小以位元組為單位。 預設值為17408 (17 KB)。
* cacheSize：快取的大小。 此值是以位元組為單位指定的。 預設值為64 GB。
* 密碼：僅在共用資料存放區設定中使用無二進位檔復寫時使用。
* stagingSplitPercentage：設定為用於中繼非同步上傳的快取大小百分比。 默认值为 10。
* uploadThreads：用於非同步上傳的上傳執行緒數目。 默认值为 10。
* stagingPurgeInterval：從暫存快取中清除已完成的上傳的間隔（秒）。 預設值為300秒（5分鐘）。
* stagingRetryInterval：失敗上傳的重試間隔（以秒為單位）。 預設值為600秒（10分鐘）。

>[!NOTE]
>
>所有設定都應放在引號之間，例如：

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## 資料存放區垃圾收集 {#data-store-garbage-collection}

資料存放區廢棄專案收集程式可用來移除資料存放區中未使用的檔案，藉此在程式中釋放寶貴的磁碟空間。

您可以透過以下方式執行資料存放區垃圾收集：

1. 前往位於的JMX主控台 *https://&lt;serveraddress:port>/system/console/jmx*
1. 正在搜尋 **存放庫管理。** 找到「存放庫管理員MBean」後，按一下它即可顯示可用的選項。
1. 捲動至頁面結尾，然後按一下 **startDataStoreGC（布林值markOnly）** 連結。
1. 在下列對話方塊中，輸入 `false` 的 `markOnly` 引數，然後按一下 **叫用**：

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >此 `markOnly` 參數列示垃圾收集掃描階段是否執行。

## 共用資料存放區的資料存放區垃圾收集 {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>在叢集或共用資料存放區中執行垃圾收集時，設定（使用Mongo或Segment Tar）記錄可能會顯示無法刪除某些blob ID的警告。 其他沒有ID刪除相關資訊的叢集或共用節點，會再次錯誤地參考先前垃圾收藏集中刪除的Blob ID。 因此，當執行垃圾收集時，它會嘗試刪除在上次執行中已刪除的ID時記錄警告。 此行為不會影響效能或功能。

>[!NOTE]
>
>如果您使用共用資料存放區設定，且資料存放區垃圾收集已停用，執行Lucene二進位清理工作可能會突然增加使用的磁碟空間。 請考慮執行下列動作，在所有作者和發佈執行個體上停用BlobTracker：
>
>1. 停止AEM執行個體。
>2. 新增 `blobTrackSnapshotIntervalInSecs=L"0"` 中的引數 `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` 檔案。 此引數需要Oak 1.12.0、1.10.2或更新版本。
>3. 重新啟動AEM執行個體。


使用較新版本的AEM，資料存放區垃圾收集也可以在多個存放庫共用的資料存放區上執行。 若要在共用資料存放區上執行資料存放區垃圾收集，請執行下列步驟：

1. 請確定在共用資料存放區的所有存放庫執行個體上，針對資料存放區垃圾收集設定的任何維護任務都已停用。
1. 執行中所述的步驟 [二進位垃圾收集](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) 個別開啟 **全部** 共用資料存放區的存放庫執行個體。 不過，請務必輸入 `true` 的 `markOnly` 按一下叫用按鈕之前的引數：

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. 在所有執行個體上完成上述程式後，再次從執行資料存放區垃圾收集 **任何** 執行個體的：

   1. 前往JMX主控台，然後選取「儲存區域管理員Mbean」。
   1. 按一下 **按一下startDataStoreGC(boolean markOnly)** 連結。
   1. 在下列對話方塊中，輸入 `false` 的 `markOnly` 引數重新輸入。
   所有找到的檔案都使用之前使用的標籤階段進行整理，並從資料存放區中刪除未使用的其餘檔案。
