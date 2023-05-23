---
title: Oak查詢和索引
seo-title: Oak Queries and Indexing
description: 瞭解如何在AEM中設定索引。
seo-description: Learn how to configure indexes in AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b27a7a1cc2295b1640520dcb56be4f3eb4851499
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 2%

---

# Oak查詢和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文會介紹如何在AEM 6中設定索引。 如需最佳化查詢和索引效能的最佳實務，請參閱 [查詢和建立索引的最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 简介 {#introduction}

不同於Jackrabbit 2，Oak預設不會索引內容。 必要時需要建立自訂索引，就像傳統關聯式資料庫一樣。 如果特定查詢沒有索引，則可能會遍歷許多節點。 查詢可能仍然有效，但速度可能非常慢。

如果Oak遇到沒有索引的查詢，則會列印WARN層級的記錄訊息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支援的查詢語言 {#supported-query-languages}

Oak查詢引擎支援下列語言：

* XPath （建議）
* SQL-2
* SQL （已棄用）
* JQOM

## 索引器型別和成本計算 {#indexer-types-and-cost-calculation}

以Apache Oak為基礎的後端可將不同的索引器插入存放庫。

一個索引子是 **屬性索引**，索引定義會儲存在存放庫本身中。

的實作 **Apache Lucene** 和 **Solr** 預設情況下也可使用，兩者都支援全文檢索索引。

此 **周遊索引** 如果沒有其他可用的索引器，則會使用。 這表示內容未編制索引，系統會周遊內容節點以尋找查詢的相符專案。

如果一個查詢有多個可用的索引器，則每個可用的索引器都會估計執行查詢的成本。 然後Oak會選擇預估成本最低的索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上圖是Apache Oak查詢執行機制的高層級表示。

首先，查詢會剖析為抽象語法樹狀結構。 然後，查詢會被檢查並轉換為SQL-2，這是Oak查詢的原生語言。

接下來，會參考每個索引來估計查詢的成本。 完成後，會擷取最便宜索引的結果。 最後，會篩選結果，以確保目前使用者擁有結果的讀取存取權，且結果與完整查詢相符。

## 設定索引 {#configuring-the-indexes}

>[!NOTE]
>
>對於大型存放庫而言，建立索引是一項耗時的作業。 這適用於初始建立索引和重新建立索引（在變更定義後重建索引）。 另請參閱 [疑難排解Oak索引](/help/sites-deploying/troubleshooting-oak-indexes.md) 和 [防止重新索引緩慢](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

如果非常大的存放庫需要重新索引，尤其是使用MongoDB和進行全文檢索索引時，請考慮文字預先擷取，並使用oak-run建立初始索引和重新索引。

索引會設定為存放庫中的節點，位於 **oak：index** 節點。

索引節點的型別必須是 **oak：QueryIndexDefinition。** 每個索引器都有數個設定選項可作為節點屬性使用。 如需詳細資訊，請參閱以下每個索引器型別的設定詳細資料。

### 屬性索引 {#the-property-index}

對於具有屬性限制但不是全文檢索的查詢，屬性索引通常非常有用。 可依照下列程式進行設定：

1. 開啟CRXDE，方法是前往 `http://localhost:4502/crx/de/index.jsp`
1. 在下建立新節點 **oak：index**
1. 為節點命名 **PropertyIndex**，並將節點型別設為 **oak：QueryIndexDefinition**
1. 為新節點設定下列屬性：

   * **型別：**  `property` （屬於字串型別）
   * **屬性名稱：**  `jcr:uuid` （屬於名稱型別）

   此特定範例會將 `jcr:uuid` 屬性，其工作是公開其所附加節點的通用唯一識別碼(UUID)。

1. 保存更改。

「屬性索引」有以下組態選項：

* 此 **type** 屬性會指定索引的型別，在此情況下，必須將其設為 **屬性**

* 此 **屬性名稱** 屬性指出要儲存在索引中的屬性清單。 如果遺失此名稱，則會使用節點名稱作為屬性名稱參考值。 在此範例中， **jcr：uuid** 其工作是公開其節點之唯一識別碼(UUID)的屬性會新增至索引。

* 此 **獨特** 若設為，則標示為 **true** 在屬性索引上新增唯一性限制。

* 此 **declaringnodetypes** 屬性可讓您指定只套用索引的特定節點型別。
* 此 **重新索引** 標幟設定為 **true**，會觸發完整內容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是Property索引的延伸。 但是，它已被取代。 需要將此型別的索引取代為 [Lucene屬性索引](#the-lucene-property-index).

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6提供以Apache Lucene為基礎的全文檢索器。

如果設定了全文檢索索引，則無論是否有其他條件被索引，也無論是否有路徑限制，所有具有全文檢索條件的查詢都會使用全文檢索索引。

如果未設定全文檢索索引，則具有全文檢索條件的查詢將無法如預期運作。

由於索引是透過非同步背景執行緒來更新，因此在背景處理完成之前，某些全文檢索搜尋將在一段很短的時間內無法使用。

您可以依照以下程式設定Lucene全文索引：

1. 開啟CRXDE並在下方建立新節點 **oak：index**.
1. 為節點命名 **LuceneIndex** 並將節點型別設為 **oak：QueryIndexDefinition**
1. 將下列屬性新增至節點：

   * **型別：**  `lucene` （屬於字串型別）
   * **非同步：**  `async` （屬於字串型別）

1. 保存更改。

Lucene索引有下列設定選項：

* 此 **type** 將指定索引型別的屬性必須設定為 **lucene**
* 此 **非同步** 屬性必須設定為 **非同步**. 這會將索引更新程式傳送至背景執行緒。
* 此 **includePropertyTypes** 屬性，定義要納入索引的屬性型別子集。
* 此 **excludePropertyNames** 將定義屬性名稱清單的屬性 — 應從索引中排除的屬性。
* 此 **重新索引** 標幟設定為 **true**，會觸發完整內容重新索引。

### Lucene屬性索引 {#the-lucene-property-index}

從 **Oak 1.0.8**，Lucene可用來建立涉及非全文檢索之屬性限制的索引。

為了達到Lucene屬性索引 **fulltextEnabled** 屬性必須一律設定為false。

以下列範例查詢為例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

若要為上述查詢定義Lucene屬性索引，您可以在下方建立新節點來新增以下定義 **oak:index:**

* **名称:** `LucenePropertyIndex`
* **类型:** `oak:QueryIndexDefinition`

建立節點後，請新增下列屬性：

* **类型:**

   ```xml
   lucene (of type String)
   ```

* **异步:**

   ```xml
   async (of type String)
   ```

* **fulltextEnabled：**

   ```xml
   false (of type Boolean)
   ```

* **includePropertyNames：** `["alias"] (of type String)`

>[!NOTE]
>
>相較於一般屬性索引，Lucene屬性索引一律設定為非同步模式。 因此，索引傳回的結果不一定能反映存放庫的最新狀態。

>[!NOTE]
>
>如需Lucene屬性索引的詳細資訊，請參閱 [Apache Jackrabbit Oak Lucene檔案頁面](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene分析器 {#lucene-analyzers}

從1.2.0版開始，Oak支援Lucene分析器。

在編制檔案索引時和查詢時，都會使用分析器。 分析器會檢查欄位文字並產生權杖資料流。 Lucene分析器由一系列Tokenizer和篩選類別組成。

分析器可透過 `analyzers` 節點（型別） `nt:unstructured`)內部 `oak:index` 定義。

索引的預設分析器設定於 `default` 分析器節點的子系。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>如需可用分析器的清單，請參閱您所使用Lucene版本的API檔案。

#### 直接指定分析器類別 {#specifying-the-analyzer-class-directly}

如果您想要使用任何現成可用的分析器，可以依照下列程式進行設定：

1. 找出您要搭配分析器使用的索引，位於 `oak:index` 節點。

1. 在索引下，建立名為的子節點 `default` 型別 `nt:unstructured`.

1. 使用下列屬性將屬性新增至預設節點：

   * **名称:** `class`
   * **类型:** `String`
   * **值:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   值是您要使用的分析器類別名稱。

   您也可以使用選用的將分析器設定為與特定lucene版本搭配使用 `luceneMatchVersion` 字串屬性。 搭配Lucene 4.7使用的有效合成為：

   * **名称:** `luceneMatchVersion`
   * **类型:** `String`
   * **值:** `LUCENE_47`

   若 `luceneMatchVersion` 若未提供，Oak將會使用隨附的Lucene版本。

1. 如果您想要將stopwords檔案新增至分析器設定，您可以在 `default` 一個具有下列屬性：

   * **名称:** `stopwords`
   * **类型:** `nt:file`

#### 透過組合建立分析器 {#creating-analyzers-via-composition}

分析器也可以根據 `Tokenizers`， `TokenFilters` 和 `CharFilters`. 您可以指定分析器並建立其選擇性代碼設定器和篩選器的子節點，依列出的順序套用，藉此執行此操作。 另請參閱 [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以這個節點結構為例：

* **名称:** `analyzers`

   * **名称:** `default`

      * **名称:** `charFilters`
      * **类型:** `nt:unstructured`

         * **名称:** `HTMLStrip`
         * **名称:** `Mapping`
      * **名称:** `tokenizer`

         * **属性名称:** `name`

            * **类型:** `String`
            * **值:** `Standard`
      * **名称:** `filters`
      * **类型:** `nt:unstructured`

         * **名称:** `LowerCase`
         * **名称:** `Stop`

            * **属性名称:** `words`

               * **类型:** `String`
               * **值:** `stop1.txt, stop2.txt`
            * **名称:** `stop1.txt`

               * **类型:** `nt:file`
            * **名称:** `stop2.txt`

               * **类型:** `nt:file`





篩選器、charFilters和tokenizer的名稱是透過移除Factory尾碼來形成。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 變成 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 變成 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 變成 `Stop`

工廠所需的任何設定引數都會指定為相關節點的屬性。

在需要載入外部檔案中的內容的情況下（例如載入停用詞），可透過建立子節點來提供內容 `nt:file` 輸入相關檔案。

### Solr索引 {#the-solr-index}

Solr索引的主要用途是全文檢索搜尋，但也可用於依路徑、屬性限制和主要型別限制來索引搜尋。 這表示Oak中的Solr索引可用於任何型別的JCR查詢。

AEM中的整合會在存放庫層級進行，因此Solr是可用於Oak (AEM隨附的新存放庫實作)中的可能索引之一。

它可以設定為與AEM執行個體一起作為遠端伺服器使用。

### 使用單一遠端Solr伺服器設定AEM {#configuring-aem-with-a-single-remote-solr-server}

AEM也可以設定為與遠端Solr伺服器執行處理搭配使用：

1. 下載並解壓縮最新版的Solr。 如需如何執行此動作的詳細資訊，請參閱 [Apache Solr安裝檔案](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. 現在，建立兩個Solr分片。 您可以為Solr解壓縮所在資料夾中的每個分片建立資料夾，以執行此操作：

   * 對於第一個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 對於第二個分片，請建立資料夾：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 找到Solr套裝程式中的範例執行處理。 它通常位於名為「」的資料夾中 `example`」在封裝的根目錄中的。
1. 將下列資料夾從範例例例項複製到兩個分片資料夾( `aemsolr1\node1` 和 `aemsolr2\node2`)：

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 建立名為「」的新資料夾 `cfg`&quot;，分別位於兩個分片資料夾中。
1. 將您的Solr和Zookeeper組態檔案放在新建立的 `cfg` 資料夾。

   >[!NOTE]
   >
   >如需Solr和ZooKeeper組態的詳細資訊，請參閱 [Solr設定檔案](https://wiki.apache.org/solr/ConfiguringSolr) 和 [ZooKeeper快速入門手冊](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 前往「 」，開始支援ZooKeeper的第一個分片 `aemsolr1\node1` 並執行下列指令：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 前往以下位置開始第二個分片： `aemsolr2\node2` 並執行下列指令：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 啟動兩個分片後，請連線至位於的Solr介面，以測試所有元件是否正常運作 `http://localhost:8983/solr/#/`
1. 啟動AEM並前往網頁主控台，網址為 `http://localhost:4502/system/console/configMgr`
1. 在「 」下設定以下設定 **Oak Solr遠端伺服器設定**：

   * Solr HTTP URL： `http://localhost:8983/solr/`

1. 選擇 **遠端Solr** 在下拉式清單中的 **Oak Solr** 伺服器提供者。

1. 前往CRXDE並以管理員身分登入。
1. 建立名為的新節點 **solrIndex** 在 **oak：index**，並設定下列屬性：

   * **型別：** solr （字串型別）
   * **非同步：** 非同步（字串型別）
   * **重新索引：** true （屬於布林型別）

1. 保存更改。

#### 建議的Solr設定 {#recommended-configuration-for-solr}

以下是可搭配本文所述所有三個Solr部署使用的基本設定範例。 它可容納已存在於AEM中且不應與其他應用程式搭配使用的專用屬性索引。

為了正確使用它，您需要將歸檔的內容直接放在Solr主目錄中。 若是多節點部署，則應直接前往每個節點的根資料夾下方。

建議的Solr組態檔

[获取文件](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1也整合了AEM 6.0中提供的兩個索引工具，作為Adobe諮詢服務公域工具集的一部分：

1. **說明查詢**，此工具旨在協助管理員瞭解查詢的執行方式；
1. **Oak索引管理員**，維護現有索引的網頁使用者介面。

您現在可以前往 **工具 — 作業 — 控制面板 — 診斷** 從AEM歡迎畫面。

如需使用方式的詳細資訊，請參閱 [操作儀表板檔案](/help/sites-administering/operations-dashboard.md).

#### 透過OSGi建立屬性索引 {#creating-property-indexes-via-osgi}

ACS Commons套件也會公開可用於建立屬性索引的OSGi設定。

您可以從Web主控台透過搜尋&quot;**確定Oak屬性索引**「。

![chlimage_1-150](assets/chlimage_1-150.png)

### 疑難排解索引問題 {#troubleshooting-indexing-issues}

可能會出現查詢執行時間長，且一般系統回應時間緩慢的情況。

本節提供一組建議，說明需要採取哪些措施來追蹤此類問題的原因，並提供如何解決這些問題的建議。

#### 正在準備偵錯資訊以進行分析 {#preparing-debugging-info-for-analysis}

要取得所執行查詢的所需資訊，最簡單的方式是透過 [說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query). 這可讓您收集對緩慢的查詢進行偵錯所需的精確資訊，而無需查閱記錄層級資訊。 如果您知道正在偵錯的查詢，這會是您理想的作法。

如果由於任何原因而無法執行此操作，您可以將索引記錄收集在單一檔案中，並使用它來疑難排解您的特定問題。

#### 啟用記錄 {#enable-logging}

若要啟用記錄，您必須啟用 **偵錯** 與Oak索引和查詢相關的類別的層級記錄。 這些類別包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

此 **com.day.cq.search** 類別僅適用於使用AEM提供的QueryBuilder公用程式。

>[!NOTE]
>
>請務必在您要疑難排解查詢的執行期間，將記錄檔設為DEBUG，否則隨著時間推移，記錄檔中將會產生大量事件。 因此，收集到所需的記錄後，請切換回INFO層級記錄，以記錄上述類別。

您可以依照下列程式來啟用記錄日誌：

1. 將瀏覽器指向 `https://serveraddress:port/system/console/slinglog`
1. 按一下 **新增記錄器** 按鈕。
1. 在新建立的列中，新增上述類別。 您可以使用 **+** 登入以將多個類別新增至單一記錄器。
1. 選擇 **偵錯** 從 **記錄層級** 下拉式清單。
1. 將輸出檔案設定為 `logs/queryDebug.log`. 這會將所有DEBUG事件關聯至單一記錄檔。
1. 執行查詢或轉譯正在使用您要偵錯的查詢的頁面。
1. 執行查詢後，請返回記錄主控台，並將新建立的記錄器的記錄層級變更為 **資訊**.

#### 索引設定 {#index-configuration}

評估查詢的方式在很大程度上受索引設定影響。 請務必取得索引設定，以便進行分析或傳送給支援人員。 您可以以內容套件形式取得設定，或取得JSON轉譯。

因為大多數情況下，索引設定會儲存在 `/oak:index` 節點，您可在下列位置取得JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引設定在不同的位置，請相應地變更路徑。

#### MBean輸出 {#mbean-output}

在某些情況下，提供索引相關MBean的輸出以進行偵錯會很有幫助。 您可以执行以下操作来实现此目标：

1. 前往位於的JMX主控台：
   `https://serveraddress:port/system/console/jmx`

1. 搜尋下列MBean：

   * Lucene索引統計資料
   * CopyOnRead支援統計資料
   * Oak查詢統計資料
   * 索引統計資料

1. 按一下每個MBean以取得效能統計資料。 建立熒幕擷圖或記下它們，以備需要提交支援時使用。

您也可以在下列URL取得這些統計資料的JSON變體：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您也可以透過以下方式提供整合的JMX輸出： `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. 這將包括JSON格式的所有與Oak相關的MBean細節。

#### 其他詳細資料 {#other-details}

您可以收集其他詳細資訊，以協助疑難排解問題，例如：

1. 執行您執行個體的Oak版本。 您可以透過開啟CRXDE並檢視歡迎頁面右下角的版本來檢視此內容，或透過檢查的版本 `org.apache.jackrabbit.oak-core` 套件組合。
1. 疑難查詢的QueryBuilder Debugger輸出。 此偵錯工具可從以下位置存取： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
