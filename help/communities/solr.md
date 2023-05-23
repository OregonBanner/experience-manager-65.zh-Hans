---
title: SRP的Solr設定
seo-title: Solr Configuration for SRP
description: Apache Solr安裝可使用不同的集合在節點存放區(Oak)和通用存放區(SRP)之間共用
seo-description: An Apache Solr installation may be shared between the node store (Oak) and common store (SRP) by using different collections
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: ce6d24e53a27b64a5d0a9db2e4b6672bd77cf9ec
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 2%

---

# SRP的Solr設定 {#solr-configuration-for-srp}

## 適用於AEM平台的Solr {#solr-for-aem-platform}

一個 [Apache Solr](https://solr.apache.org/) 安裝可在以下兩者之間共用： [節點存放區](../../help/sites-deploying/data-store-config.md) (Oak)和 [公用存放區](working-with-srp.md) (SRP)，使用不同的集合。

如果同時大量使用Oak和SRP集合，則可能會基於效能原因安裝第二個Solr。

對於生產環境， [SolrCloud模式](#solrcloud-mode) 比獨立模式（單一本機Solr設定）提供更優異的效能。

### 要求 {#requirements}

下載並安裝Apache Solr：

* [7.0版](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr需要Java™ 1.7或更高版本
* 不需要服務
* 選擇執行模式：

   * 獨立模式
   * [SolrCloud模式](#solrcloud-mode) （建議用於生產環境）

* 選擇多語言搜尋(MLS)

   * [安裝標準MLS](#installing-standard-mls)
   * [安裝進階MLS](#installing-advanced-mls)

## SolrCloud模式 {#solrcloud-mode}

[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) 建議在生產環境中使用模式。 在SolrCloud模式下執行時，必須先安裝並設定SolrCloud，才能安裝多語言搜尋(MLS)。

建議遵循SolrCloud指示進行安裝：

* 3個SolrCloud節點位於同一部伺服器上。
* 外部Apache ZooKeeper。

也建議設定JVM以調整記憶體使用量和記憶體回收。

### JVM設定範例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud設定命令 {#solrcloud-setup-commands}

在SolrCloud模式下執行時，在MLS安裝之前，需要使用和瞭解以下SolrCloud安裝命令。

#### 1.上傳設定至ZooKeeper {#upload-a-configuration-to-zookeeper}

參考資料：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方式： sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server：port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2.建立集合 {#create-a-collection}

參考資料：
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

用途:
./bin/solr建立 \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *連線埠*\
-s *分片數* \
-rf *復本數目*

#### 3.將集合連結至組態集 {#link-a-collection-to-a-configuration-set}

將集合連結至已上傳至ZooKeeper的設定。

參考資料：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方式： sh 。/scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server：port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準與進階MLS的比較 {#comparison-of-standard-and-advanced-mls}

適用於AEM Communities的多語言搜尋(MLS)是針對Solr平台所打造，可跨所有支援的語言（包括英文）提供改良的搜尋功能。

適用於AEM Communities的MLS可作為標準MLS或進階MLS使用。 標準MLS僅包含Solr組態設定，並排除任何外掛程式或資源檔案。 進階MLS是更完整的解決方案，包含Solr組態設定以及外掛程式和相關資源

標準MLS包含針對下列語言的內容搜尋的增強功能：

* 英文：改善嘗試比對文字衍生詞的詞幹分析器。
* 日文：改善半形字元的日文標籤化。

進階MLS包含針對下列語言的內容搜尋的增強功能：

* 英文：以詞尾字元取代詞尾字元。
* 德文：新增解壓縮。
* 法文：新增版本處理。
* 中文（簡體）：新增更聰明的代碼器。
* 各種語言：新增詞幹分析器、停用字清單和標準化程式。

進階MLS總共支援下列33種語言。

| 阿拉伯语 | 德语 | 挪威语 |
|---|---|---|
| 保加利亚语 | 希腊语 | 波兰语 |
| 中文（简体） | 海地克里奧爾語 | 葡萄牙语 |
| 中文（繁体） | 希伯来语 | 罗马尼亚语 |
| 捷克语 | 匈牙利语 | 俄语 |
| 丹麦语 | 印尼语 | 斯洛伐克语 |
| 荷兰语 | 意大利语 | 斯洛文尼亚语 |
| 英语 | 日语 | 西班牙语 |
| 爱沙尼亚语 | 朝鲜语 | 瑞典语 |
| 芬兰语 | 拉脱维亚语 | 泰语 |
| 法语 | 立陶宛语 | 土耳其语 |

#### AEM 6.1 Solr搜尋、標準MLS和進階MLS的比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**： AEM 6.1代表AEM 6.1 Communities FP3及舊版。

![compare-solr-mls](assets/compare-solr-mls.png)

### 安裝標準MLS {#installing-standard-mls}

對於SRP集合（MSRP或DSRP），若要支援標準多語言搜尋(MLS)，必須修改兩個Solr的組態檔：

* **schema.xml**
* **solrconfig.xml**

Solr 4.10的標準MLS檔案(schema.xml、solrconfig.xml)。

Solr 5.x的標準MLS檔案(schema.xml、solrconfig.xml)。

標準MLS檔案儲存在AEM存放庫中。

**注意**：雖然Solr檔案儲存在msrp/資料夾中，但它們也適用於DSRP （不需要變更）。

**下載指示**：取代 `solrX` 替換為 `solr4` 或 `solr5` 視情況而定。

1. 使用CRXDE|Lite，找出：

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. 下載到部署Solr的本機伺服器。

   * 找到 `jcr:content` 節點的 `jcr:data` 屬性。
   * 若要開始下載，請選取「 」 `view`.
   * 確保檔案以適當的名稱和編碼(UTF8)儲存。

1. 請遵循獨立或SolrCloud模式的安裝指示。

#### SolrCloud模式 — 標準MLS {#solrcloud-mode-standard-mls}

1. 在SolrCloud模式下安裝及設定Solr。
1. 準備新設定：

   1. 建立new-config-dir*，例如 `solr-install-dir*/myconfig/`

   1. 將現有Solr組態目錄的內容複製到 *new-config-dir*

      * 對於Solr4：複製 `solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5：複製 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 複製下載的 **schema.xml** 和 **solrconfig.xml** 至 *new-config-dir* 覆寫現有檔案。


1. [上傳新設定](#upload-a-configuration-to-zookeeper) 加入動物園管理員。
1. [建立集合](#create-a-collection) 指定必要的引數，例如分片數目、復本數目和組態名稱。
1. 如果設定名稱是*未*在建立集合期間提供， [連結這個新建立的集合](#link-a-collection-to-a-configuration-set) 將設定上傳至ZooKeeper。

1. 針對MSRP，請執行 [MSRP重新索引工具](msrp.md#msrp-reindex-tool)，除非是全新安裝。

#### 獨立模式 — 標準MLS {#standalone-mode-standard-mls}

1. 以獨立模式安裝Solr。
1. 如果執行Solr5，請建立集合1 （類似Solr4）：

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 備份 **schema.xml** 和 **solrconfig.xml** 在Solr設定目錄中，例如：

   * 對於Solr4： `solr-install-dir/example/solr/collection1/conf/`
   * 已為Solr5建立： `solr-install-dir/server/solr/collection1/conf/`

1. 複製下載的 **schema.xml** 和 **solrconfig.xml** 至相同目錄。

1. 重新啟動Solr。
1. 針對MSRP，請執行 [MSRP重新索引工具](#msrpreindextool)，除非是全新安裝。

### 安裝進階MLS {#installing-advanced-mls}

為了讓SRP集合（MSRP或DSRP）支援進階MLS，除了自訂結構描述和Solr設定外，還需要新的Solr外掛程式。 所有必要專案都會封裝成可下載的zip檔案。 此外，當以獨立模式部署Solr時，也會隨附安裝指令碼。

若要取得進階MLS套件，請參閱 [AEM進階MLS](deploy-communities.md#aem-advanced-mls) 在檔案的部署區段中。

若要開始使用SolrCloud或獨立模式的安裝：

* 下載AEM-SOLR-MLS zip封存至託管Solr的伺服器。
* 將封存解壓縮。

#### SolrCloud模式 — 進階MLS {#solrcloud-mode-advanced-mls}

安裝指示 — 請注意Solr4和Solr5的幾項差異：

1. 在SolrCloud模式下安裝及設定Solr。
1. 將進階MLS套件的內容解壓縮至磁碟。 內容應包括：

   * **schema.xml**
   * **solrconfig.xml**
   * **停用詞/** 資料夾
   * **設定檔/** 資料夾
   * **extra-libs/** 資料夾

1. 準備新設定：

   1. 建立 *new-config-dir*

      * 例如 `solr-install-dir/myconfig/`
      * 建立子資料夾 `stopwords/` 和 `lang/`
   1. 將現有Solr設定目錄的內容複製到 *new-config-dir*

      * 對於Solr4：複製 `solr-install-dir/example/solr/collection1/conf/`
      * 對於Solr5：複製 `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 複製擷取的 **schema.xml** 和 **solrconfig.xml** 至 *new-config-dir* 覆寫現有檔案。
   1. 對於Solr5：複製 `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` 至 `new-config-dir/lang/`
   1. 複製擷取的 **停用詞/** 資料夾至 *new-config-dir* 結果 `new-config-dir/stopwords/*.txt`



1. [上傳新設定](#upload-a-configuration-to-zookeeper) 至ZooKeeper
1. 複製新的 **設定檔/** 資料夾……

   * 對於Solr4：複製到每個節點的資源/資料夾
   * 對於Solr5：複製到每個Solr安裝的伺服器/資源/資料夾。 如果所有節點都位於相同的Solr安裝目錄中，則此步驟只會執行一次。

1. 建立 **lib/** SolrCloud中每個節點的solr-home目錄（包含solr.xml）中的資料夾。 將jar從下列位置複製到每個節點上的新程式庫/資料夾：

   * **extra-libs/** 從進階MLS封裝擷取
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [建立集合](#create-a-collection) 指定必要的引數，例如分片數目、復本數目和組態名稱。
1. 如果設定名稱為 *not* 在建立集合期間提供， [連結這個新建立的集合](#link-a-collection-to-a-configuration-set) 將設定上傳至ZooKeeper。

1. 針對MSRP，請執行 [MSRP重新索引工具](#msrpreindextool)，除非是全新安裝。

#### 獨立模式 — 進階MLS {#standalone-mode-advanced-mls}

進階MLS套件中包含安裝指令碼。

將套裝軟體的內容解壓縮至裝載獨立Solr伺服器的伺服器後，請執行安裝指令碼以安裝必要的資源與組態檔。

* 以獨立模式安裝Solr。
* 如果執行Solr5，請建立集合1 （類似Solr4）：

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* 執行安裝指令碼：安裝 [-v 4|5] [-d solrhome] [-c集合路徑]
其中：

   * -d solrhome

      Solr安裝目錄

   * -c集合路徑

      solr中的集合路徑

   * --帮助

      列印命令列選項

   * -v [4|5]

      設定solr的版本

* Solr 4.10.4的範例：

   * Install.bat -v 4 -d c：/solr-4.10.4 -c：/solr-4.10.4/example/solr/collection1

* Solr 5.4.0的範例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**注意**:

* 安裝指令碼會先備份schema.xml和solrconfig.xml，然後再藉由附加「.orig」來安裝新版本

### 關於solrconfig.xml {#about-solrconfig-xml}

此 **solrconfig.xml** 檔案控制自動認可間隔和搜尋可見度，並需要測試和調整。

`<autoCommit>`：根據預設，自動認可間隔（對穩定儲存的硬式認可）會設為15秒。 搜尋可見性預設為使用預先確認索引。

若要變更搜尋，以使用更新的索引來反映因認可而發生的變更，請變更包含的 `openSearcher` 為true。

`autoSoftCommit`：「soft」認可可確保變更可見（索引已更新），但無法確保變更同步至穩定儲存（硬認可）。 結果是效能提高。 依預設， `autoSoftCommit` 已停用，包含 `maxTime` 設為–1。
