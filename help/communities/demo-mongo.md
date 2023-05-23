---
title: 如何設定MongoDB以進行示範
seo-title: How to Setup MongoDB for Demo
description: 如何為一個製作執行個體和一個發佈執行個體設定MSRP
seo-description: How to setup MSRP for one author instance and one publish instance
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# 如何設定MongoDB以進行示範 {#how-to-setup-mongodb-for-demo}

## 简介 {#introduction}

本教學課程說明如何設定 [MSRP](msrp.md) 的 *一位作者* 執行個體和 *一個發佈* 執行個體。

透過此設定，社群內容可從製作和發佈環境存取，而無需轉送或反向復寫使用者產生的內容(UGC)。

此設定適用於 *非生產* 環境，例如開發和/或示範。

**A *生產* 環境應：**

* 使用復本集執行MongoDB
* 使用SolrCloud
* 包含多個發行者執行個體

## MongoDB {#mongodb}

### 安裝MongoDb {#install-mongodb}

* 下載MongoDB，從 [https://www.mongodb.org/](https://www.mongodb.org/)

   * 選擇作業系統：

      * Linux
      * Mac 10.8
      * Windows 7
   * 版本選擇：

      * 至少使用2.6版


* 基本設定

   * 遵循MongoDB安裝指示。
   * 設定mongod：

      * 不需要設定蒙哥或分片。
   * 安裝的MongoDB資料夾將稱為 &lt;mongo-install>.
   * 定義的資料目錄路徑將參照為 &lt;mongo-dbpath>.


* MongoDB可在與AEM相同的主機上執行或遠端執行。

### 啟動MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

這將使用預設連線埠27017啟動MongoDB伺服器。

* 對於Mac，請使用開頭為&#39;ulimit -n 2048&#39;的ulimit增加

>[!NOTE]
>
>如果MongoDB已啟動 *晚於* AEM， **重新啟動** 全部 **AEM** 執行個體，使其正確連線至MongoDB。

### 示範生產選項：設定MongoDB復本集 {#demo-production-option-setup-mongodb-replica-set}

下列指令是在localhost上以3個節點設定復本集的範例：

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### 安裝Solr {#install-solr}

* 下載Solr來源 [Apache Lucene](https://archive.apache.org/dist/lucene/solr/)：

   * 適用於任何作業系統。
   * Solr 7.0版。
   * Solr需要Java 1.7或更高版本。

* 基本設定

   * 遵循&#39;example&#39; Solr設定。
   * 不需要服務。
   * 安裝的Solr資料夾將稱為 &lt;solr-install>.

### 為AEM Communities設定Solr {#configure-solr-for-aem-communities}

若要設定MSRP的Solr集合以進行示範，有兩個決定需要做（請選取主要檔案的連結以取得詳細資訊）：

1. 以獨立或獨立方式執行Solr [SolrCloud模式](msrp.md#solrcloudmode).
1. 安裝 [標準](msrp.md#installingstandardmls) 或 [進階](msrp.md#installingadvancedmls) 多語言搜尋(MLS)。

### 獨立Solr {#standalone-solr}

執行Solr的方法可能會因安裝的版本和方式而異。 此 [Solr參考指南](https://archive.apache.org/dist/lucene/solr/ref-guide/) 是權威檔案。

為簡單起見，以4.10版為例，以獨立模式啟動Solr：

* cd至 &lt;solrinstall>/example
* java -jar start.jar

這會使用預設連線埠8983啟動Solr HTTP伺服器。 您可以瀏覽至Solr主控台，取得Solr主控台以進行測試。

* 預設Solr主控台： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>如果Solr主控台無法使用，請檢查 &lt;solrinstall>/example/logs. 檢視SOLR是否嘗試繫結至無法解析的特定主機名稱（例如「user-macbook-pro」）。
若是如此，請使用此主機名稱的新專案更新etc/hosts檔案（例如127.0.0.1 user-macbook-pro），Solr將正常啟動。

### SolrCloud {#solrcloud}

若要執行非常基本的（非生產） solrCloud設定，請啟動solr並執行下列動作：

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## 將MongoDB識別為通用存放區 {#identify-mongodb-as-common-store}

視需要啟動作者和發佈AEM例項。

如果AEM在MongoDB啟動之前執行，則需要重新啟動AEM執行個體。

請依照主要檔案頁面上的指示操作： [MSRP - MongoDB公用存放區](msrp.md)

## 测试 {#test}

若要測試和驗證MongoDB通用存放區，請在發佈執行個體上張貼註解並在製作執行個體上檢視它，以及在MongoDB和Solr中檢視UGC：

1. 在發佈執行個體上，瀏覽至 [社群元件指南](http://localhost:4503/content/community-components/en/comments.html) 頁面並選取「註解」元件。
1. 登入以發表評論：
1. 在註解文字輸入方塊中輸入文字，然後按一下 **[!UICONTROL Post]**

   ![post-comment](assets/post-comment.png)

1. 只要在 [作者執行個體](http://localhost:4502/content/community-components/en/comments.html) （可能仍以管理員/管理員身分登入）。

   ![view-comment](assets/view-comment.png)

   注意：雖然下有JCR節點， *asith* 在作者上，這些用於SCF框架。 實際的UGC不在JCR中，而是在MongoDB中。

1. 在mongodb中檢視UGC **[!UICONTROL Communities]** > **[!UICONTROL 集合]** > **[!UICONTROL 內容]**

   ![ugc-content](assets/ugc-content.png)

1. 在Solr中檢視UGC：

   * 瀏覽至Solr儀表板： [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * 使用者 `core selector` 以選取 `collection1`.
   * 选择 `Query`.
   * 选择 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## 疑难解答 {#troubleshooting}

### 未出現UGC {#no-ugc-appears}

1. 請確定MongoDB已安裝且正常執行。

1. 請確定MSRP已設定為預設提供者：

   * 在所有作者和發佈AEM執行個體上，重新造訪 [儲存設定主控台](srp-config.md) 或檢查AEM存放庫：

   * 在JCR中，如果 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 不包含 [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) 節點，這表示儲存提供者為JSRP。
   * 如果srpc節點存在且包含節點 [default設定](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)，defaultconfiguration的屬性應將MSRP定義為預設提供者。

1. 請確定在選取MSRP後重新啟動AEM。
