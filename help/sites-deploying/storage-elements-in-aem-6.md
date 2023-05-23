---
title: AEM 6.5中的儲存元素
seo-title: Storage Elements in AEM 6.5
description: 瞭解AEM 6.5中可用的節點儲存實施以及如何維護存放庫。
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 1%

---

# AEM 6.5中的儲存元素{#storage-elements-in-aem}

本文章涵蓋下列內容：

* [AEM 6儲存空間概述](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [維護存放庫](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## AEM 6儲存空間概述 {#overview-of-storage-in-aem}

AEM 6最重要的變更之一是存放庫層級的創新。

目前，AEM6提供兩種節點儲存實作： Tar儲存和MongoDB儲存。

### Tar儲存 {#tar-storage}

#### 使用Tar儲存體執行全新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>區段節點存放區的PID已從org.apache.jackrabbit.oak變更。**外掛程式**.segment.SegmentNodeStoreService (舊版AEM 6中)至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService (AEM 6.3中)。請確定已進行必要的設定調整，以便反映變更。

依預設，AEM 6會使用預設設定選項，使用Tar儲存空間來儲存節點和二進位檔。 您可以執行下列動作，手動設定其儲存設定：

1. 下載AEM 6快速入門jar並將其放入新資料夾中。
1. 透過執行以下動作解壓縮AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 建立名為的資料夾 `crx-quickstart\install` 安裝目錄中的。

1. 建立名為的檔案 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` 在新建立的資料夾中。

1. 編輯檔案並設定組態選項。 以下選項適用於區段節點存放區，這是AEM Tar儲存體實作的基礎：

   * `repository.home`：儲存各種存放庫相關資料的存放庫首頁的路徑。 依預設，區段檔案會儲存在crx-quickstart/segmentstore目錄下。
   * `tarmk.size`：區段的大小上限（以MB為單位）。 預設值為256 MB。

1. 啟動AEM。

### Mongo儲存 {#mongo-storage}

#### 使用Mongo儲存體執行全新安裝的AEM執行個體 {#running-a-freshly-installed-aem-instance-with-mongo-storage}

可以依照以下程式將AEM 6設定為使用MongoDB儲存體執行：

1. 下載AEM 6快速入門jar並將其放入新資料夾中。
1. 透過執行以下命令來解壓縮AEM：

   `java -jar cq-quickstart-6.jar -unpack`

1. 請確定已安裝MongoDB且執行個體為 `mongod` 執行中。 如需詳細資訊，請參閱 [安裝MongoDB](https://docs.mongodb.org/manual/installation/).
1. 建立名為的資料夾 `crx-quickstart\install` 安裝目錄中的。
1. 建立包含您要在中使用的組態名稱的組態檔，以設定節點存放區。 `crx-quickstart\install` 目錄。

   檔案節點存放區(AEM MongoDB儲存體實作的基礎)會使用名為的檔案 `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. 編輯檔案並設定組態選項。 以下选项可供选择：

   * `mongouri`：此 [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) 連線至Mongo資料庫時需要。 預設值為 `mongodb://localhost:27017`
   * `db`：Mongo資料庫的名稱。 預設情況下，新的AEM 6安裝使用 **aem-author** 作為資料庫名稱。
   * `cache`：快取大小(MB)。 此快取大小分佈於DocumentNodeStore中使用的各種快取中。 預設值為256。
   * `changesSize`：Mongo中用於快取差異輸出的限定集合大小（以MB為單位）。 預設值為256。
   * `customBlobStore`：表示使用自訂資料存放區的布林值。 預設值為false。

1. 以您要使用之資料存放區的PID建立設定檔案，並編輯檔案以設定設定選項。 如需詳細資訊，請參閱 [設定節點存放區和資料存放區](/help/sites-deploying/data-store-config.md).

1. 執行，啟動具有MongoDB儲存後端的AEM 6 jar：

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   其中後端執行模式為 **`-r`**，此範例從MongoDB支援開始。

#### 停用透明大型頁面 {#disabling-transparent-huge-pages}

Red Hat® Linux®使用稱為Transparent Great Pages (THP)的記憶體管理演演算法。 雖然AEM會執行微調的讀取和寫入，但THP已針對大型作業最佳化。 因此，建議您在Tar和Mongo儲存空間上停用THP。 若要停用演演算法，請執行下列步驟：

1. 開啟 `/etc/grub.conf` 檔案的文字編輯器。
1. 將下列行新增至 **grub.conf** 檔案：

   ```
   transparent_hugepage=never
   ```

1. 最後，執行以檢查設定是否已生效：

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果停用THP，上述命令的輸出應該是：

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>請參閱下列資源：
>
>* 如需Red Hat® Linux®上透明大型頁面的詳細資訊，請參閱此 [文章](https://access.redhat.com/solutions/46111).
* 如需Linux®調整秘訣，請參閱此 [文章](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=zh-Hans).
>


## 維護存放庫 {#maintaining-the-repository}

存放庫的每次更新都會建立內容修訂版本。 因此，儲存庫的大小會隨著每次更新而成長。 為避免儲存庫成長不受控制，必須清理舊修訂以釋放磁碟資源。 此維護功能稱為「版本清理」。 修訂清除機制會從存放庫中移除過時的資料，以回收磁碟空間。 如需修訂清除的詳細資訊，請閱讀 [修訂清除頁面](/help/sites-deploying/revision-cleanup.md).
