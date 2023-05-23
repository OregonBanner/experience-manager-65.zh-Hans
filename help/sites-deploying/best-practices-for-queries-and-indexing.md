---
title: 查詢和建立索引的最佳實務
seo-title: Best Practices for Queries and Indexing
description: 本文提供如何最佳化索引和查詢的准則。
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '4663'
ht-degree: 10%

---

# 查詢和建立索引的最佳實務{#best-practices-for-queries-and-indexing}

除了在AEM 6中轉換至Oak外，也針對管理查詢和索引的方式進行了一些重大變更。 在Jackrabbit 2中，所有內容都預設編制索引，並可自由查詢。 在Oak中，必須在以下位置手動建立索引： `oak:index` 節點。 可以在沒有索引的情況下執行查詢，但是對於大型資料集，查詢執行速度會非常慢，甚至會中止。

本文會概述何時建立索引以及何時不需要索引、避免在不需要查詢時使用查詢的技巧，以及最佳化索引和查詢以儘可能最佳執行的相關提示。

此外，請務必閱讀 [有關編寫查詢和索引的Oak檔案](/help/sites-deploying/queries-and-indexing.md). 除了索引是AEM 6的新概念之外，從舊版AEM安裝移轉程式碼時，需要考慮Oak查詢的語法差異。

## 何时使用查询 {#when-to-use-queries}

### 存储库和分类设计 {#repository-and-taxonomy-design}

在设计存储库的分类时，需要考虑几个因素。其中包括存取控制、本地化、元件和頁面屬性繼承等。

在设计涵盖这些方面的分类法时，考虑索引设计的“可通行性”也很重要。在這種情況下，可通行性是分類法的能力，允許根據其路徑以可預測的方式存取內容。 這將造就一個比需要執行大量查詢的系統更易於維護的更高效能系統。

此外，在设计分类法时，考虑排序是否重要也很关键。如果不需要显式排序，并且需要大量同级节点，则最好使用无序节点类型，如`sling:Folder`或`oak:Unstructured`。在需要排序的情况下，`nt:unstructured` 和 `sling:OrderedFolder` 更合适。

### 组件中的查询 {#queries-in-components}

由于查询可能是在 AEM 系统上执行的最繁重的操作之一，因此最好在组件中避免查询。每次呈现页面时执行多个查询通常会降低系统的性能。有兩種策略可用來避免在轉譯元件時執行查詢： **周遊節點** 和 **預先擷取結果**.

#### 遍历节点 {#traversing-nodes}

如果存储库的设计允许事先了解所需数据的位置，则可以部署从必要路径检索此数据的代码，而无需运行查询来查找它。

这方面的一个例子是呈现适合特定类别的内容。一种方法是使用类别属性组织内容，并且可以通过查询该属性来填充显示类别中项目的组件。

更好的方法是按类别通过分类法构造此内容，以便可以手动检索。

例如，如果内容存储在类似于以下的分类法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

可以简单地检索 `/content/myUnstructuredContent/parentCategory/childCategory` 节点，解析其子节点并用于呈现组件。

此外，当您处理一个小的或同质的结果集时，遍历存储库并收集所需的节点可能比通过手工创建查询来返回相同的结果集更快。作为一般考虑，应尽可能避免查询。

#### 预取结果 {#prefetching-results}

有時，元件周圍的內容或需求不允許使用節點周遊作為擷取所需資料的方法。 在這些情況下，需要在轉譯元件之前執行所需的查詢，以確保一般使用者的最佳效能。

如果元件所需的結果可在編寫時計算，且預期內容不會變更，則可在作者在對話方塊中套用設定時執行查詢。

如果数据或内容会定期更改，则可以按计划或通过侦听器执行查询，以更新基础数据。然后，可以将结果写入存储库中的共享位置。任何需要此数据的组件都可以从该单个节点提取值，而无需在运行时执行查询。

## 查詢最佳化 {#query-optimization}

執行未使用索引的查詢時，將記錄有關節點周遊的警告。 如果這是經常執行的查詢，則應建立索引。 若要判斷指定的查詢正在使用哪個索引，請 [說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 建議使用。 如需其他資訊，可以為相關搜尋API啟用DEBUG記錄。

>[!NOTE]
>
>修改索引定義後，需要重新建立索引（重新索引）。 根據索引的大小，這可能需要一些時間才能完成。

執行複雜查詢時，在某些情況下，將查詢劃分為多個較小的查詢，並在事後透過程式碼聯結資料的效能會更高。 對於這些案例，建議比較兩種方法的效能，以判斷哪一種選項更適合相關使用案例。

AEM允許以下列三種方式之一寫入查詢：

* 透過 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) （建議）
* 使用XPath （建議）
* 使用SQL2

雖然所有查詢在執行前都會轉換為SQL2，但查詢轉換的額外開銷最小，因此，選擇查詢語言時最大的考量將是開發團隊的可讀性和舒適度。

>[!NOTE]
>
>使用QueryBuilder時，依預設會判斷結果計數，這在Oak中比舊版Jackrabbit要慢。 為了彌補此問題，您可以使用 [guessTotal引數](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Explain查詢工具 {#the-explain-query-tool}

和任何查詢語言一樣，最佳化查詢的第一步是瞭解其執行方式。 若要啟用此活動，您可以使用 [說明查詢工具](/help/sites-administering/operations-dashboard.md#explain-query) 它是「操作圖示板」的一部分。 使用此工具，可以插入查詢並加以說明。 如果查詢會造成大型存放庫以及執行時間和將使用的索引發生問題，則會顯示警告。 此工具也可以載入緩慢和熱門查詢的清單，然後加以說明和最佳化。

### 查詢的DEBUG記錄 {#debug-logging-for-queries}

若要瞭解更多關於Oak如何選擇要使用的索引，以及查詢引擎實際執行查詢的方式，請參閱 **偵錯** 可以為以下套件新增記錄設定：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

完成查詢偵錯後，請務必移除此記錄器，因為此記錄器會輸出許多活動，而且最終可能會將記錄檔填滿磁碟。

如需如何執行此動作的詳細資訊，請參閱 [記錄檔案](/help/sites-deploying/configure-logging.md).

### 索引統計資料 {#index-statistics}

Lucene會註冊一個JMX Bean，以提供索引內容的詳細資訊，包括每個索引中存在的檔案大小和數量。

您可以存取JMX主控台來存取它，網址為 `https://server:port/system/console/jmx`

登入JMX主控台後，請搜尋 **Lucene索引統計資料** 以找到它。 其他索引統計資料可在以下網址找到： **索引統計資料** MBean。

如需查詢統計資料，請檢視命名的MBean **Oak查詢統計資料**.

如果您想要使用類似以下的工具深入瞭解您的索引： [Luke](https://code.google.com/archive/p/luke/)，您必須使用Oak主控台從以下傾印索引： `NodeStore` 檔案系統目錄。 如需操作的相關說明，請閱讀 [Lucene檔案](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

您也可以使用JSON格式擷取系統中的索引。 若要這麼做，您需要存取 `https://server:port/oak:index.tidy.-1.json`

### 查询限制 {#query-limits}

**開發期間**

設定以下專案的低臨界值 `oak.queryLimitInMemory` (例如： 10000)和oak. `queryLimitReads` (例如： 5000)，並在點選UnsupportedOperationException時最佳化昂貴的查詢，指出「查詢讀取超過x個節點……」

這有助於避免資源密集的查詢(即 不受任何索引支援，或受涵蓋範圍較少的索引支援)。 例如，讀取100萬個節點的查詢會導致I/O增加，並對整體應用程式效能造成負面影響。 應分析和最佳化任何因上述限制而失敗的查詢。

#### **部署後** {#post-deployment}

* 監控查詢記錄以觸發大型節點周遊或大型棧積記憶體消耗： 」

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 最佳化查詢以減少周遊的節點數

* 監控觸發大型棧積記憶體使用量的查詢記錄：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 最佳化查詢以降低棧積記憶體耗用量

對於AEM 6.0 - 6.2版本，您可以透過AEM開始指令碼中的JVM引數調整節點周遊的臨界值，以防止大型查詢使環境過載。

建議值為：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2個引數是預先設定的OOTB，並可透過OSGi QueryEngineSettings持續存在。

如需詳細資訊，請前往： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 建立有效率索引的秘訣 {#tips-for-creating-efficient-indexes}

### 我應該建立索引嗎？ {#should-i-create-an-index}

建立或最佳化索引時，首先要問的問題是特定情況下是否確實需要索引。 如果您只打算透過批次程式在系統的非尖峰時段執行一次有問題的查詢，最好根本不建立索引。

建立索引後，每次更新索引資料時，也必須更新索引。 由於這會對系統造成效能影響，因此應該僅在實際需要索引時建立索引。

此外，只有在索引中包含的資料足夠獨特，足以保證使用時，索引才有用。 考量書籍中的索引及其涵蓋的主題。 在文字中索引一組主題時，通常會有數百或數千個專案，這可讓您快速跳至頁面子集，以快速找到您要尋找的資訊。 如果該索引只有兩個或三個專案，而每個專案都指向數百個頁面，則該索引將不是很有用。 這個概念同樣適用於資料庫索引。 如果只有幾個唯一值，則索引將不是很有用。 也就是說，索引也可能變得太大而無法使用。 若要檢視索引統計資料，請參閱 [索引統計資料](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 以上。

### Lucene或屬性索引？ {#lucene-or-property-indexes}

Lucene索引在Oak 1.0.9中引入，並針對AEM 6首次推出時引入的屬性索引提供一些強大的最佳化。 在決定是否使用Lucene索引或屬性索引時，請考慮以下因素：

* Lucene索引提供的功能比屬性索引多得多。 例如，屬性索引只能索引單一屬性，而Lucene索引可以包含多個屬性。 如需Lucene索引中所有可用功能的詳細資訊，請參閱 [檔案](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Lucene索引為非同步。 雖然如此可大幅提升效能，但也可能造成將資料寫入存放庫和更新索引之間的延遲。 如果讓查詢傳回100%準確結果很重要，則需要屬性索引。
* 由於不同步，Lucene索引無法強制執行唯一性限制。 如果需要，則需要建立屬性索引。

一般而言，除非迫切需要使用屬性索引，否則建議您使用Lucene索引，以便獲得更高效能和彈性的好處。

### Solr索引 {#solr-indexing}

AEM也依預設提供Solr索引支援。 這主要用於支援全文檢索搜尋，但也可用來支援任何型別的JCR查詢。 當AEM執行個體沒有CPU容量來處理大量搜尋部署（例如具有大量同時使用者的搜尋驅動網站）所需的查詢數量時，應該考慮Solr。 或者，Solr也可以以爬行者程式為基礎的方法實作，以利用平台的一些更進階的功能。

Solr索引可以設定為針對開發環境在AEM伺服器上執行內嵌，也可以解除安裝到遠端執行個體，以改善生產和中繼環境的搜尋擴充性。 雖然解除安裝搜尋可改善擴充性，但會造成延遲，因此除非有需要，否則不建議使用。 如需有關如何設定Solr整合以及如何建立Solr索引的詳細資訊，請參閱 [Oak查詢和索引檔案](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>雖然採用整合式Solr搜尋方法可允許將索引解除安裝到Solr伺服器。 如果透過爬行者程式方法使用Solr伺服器的進階功能，則需要額外的設定工作。

採用此方法的缺點在於，雖然依預設，AEM查詢會遵循ACL，因而隱藏使用者無權存取的結果，但對Solr伺服器外部化搜尋將不會支援此功能。 如果要以這種方式將搜尋外部化，則必須格外小心以確保使用者不會看到他們不應該看到的結果。

在可能需要彙總來自多個來源的搜尋資料的情況下，此方法可能適合的潛在使用案例。 例如，您可能將某個網站託管在AEM上，並將第二個網站託管在協力廠商平台上。 Solr可設定為對兩個網站的內容進行編目，並將它們儲存在彙總索引中。 這將允許跨網站搜尋。

### 設計考量 {#design-considerations}

Lucene索引的Oak檔案列出在設計索引時要注意的幾個事項：

* 如果查詢使用不同的路徑限制，請使用 `evaluatePathRestrictions`. 這將允許查詢傳回指定路徑下的結果子集，然後根據查詢篩選它們。 否則，查詢將搜尋與存放庫中查詢引數相符的所有結果，然後根據路徑篩選它們。
* 如果查詢使用排序，請為已排序的屬性設定明確的屬性定義，並設定 `ordered` 至 `true` 為了它。 這樣可讓結果在索引中依此方式排序，並節省查詢執行時昂貴的排序作業。

* 只將所需的內容放入索引中。 新增不需要的功能或屬性會導致索引增加和效能降低。
* 在屬性索引中，擁有唯一的屬性名稱有助於減小索引的大小，但對於Lucene索引，請使用 `nodeTypes` 和 `mixins` 應該達到有凝聚力的索引。 查詢特定 `nodeType` 或 `mixin` 將比查詢更有效 `nt:base`. 使用此方法時，定義 `indexRules` 的 `nodeTypes` 有疑問。

* 如果您的查詢只在某些路徑下執行，則在這些路徑下建立這些索引。 索引不需要位於存放庫的根目錄。
* 當所有要編制索引的屬性都相關時，建議使用單一索引，以允許Lucene在本機評估儘可能多的屬性限制。 此外，即使執行聯結，查詢也只使用一個索引。

### CopyonRead {#copyonread}

在 `NodeStore` 會從遠端儲存，稱為 `CopyOnRead` 可以啟用。 此選項將導致遠端索引在讀取時寫入本機檔案系統。 這有助於改善經常針對這些遠端索引執行的查詢效能。

這可以在OSGi主控台中的 **LuceneIndexProvider** 並從Oak 1.0.13起預設啟用。

### 移除索引 {#removing-indexes}

移除索引時，一律建議透過設定 `type` 屬性至 `disabled` 並進行測試，以確保您的應用程式在實際刪除前可正常運作。 請注意，索引在停用時不會更新，因此，如果重新啟用，可能沒有正確的內容，並且可能需要重新索引。

移除TarMK執行個體上的屬性索引後，需要執行壓縮以回收任何使用的磁碟空間。 對於Lucene索引，實際的索引內容存在於BlobStore中，因此需要資料存放區垃圾收集。

移除MongoDB執行個體上的索引時，刪除的成本與索引中的節點數量成比例。 由於刪除大型索引可能會造成問題，建議方法是停用索引，並僅在維護期間使用（例如）工具將其刪除 **oak-mongo.js**. 請注意，不應針對一般節點內容使用此方法，因為這會造成資料不一致。

>[!NOTE]
>
>如需oak-mongo.js的詳細資訊，請參閱 [命令列工具區段](https://jackrabbit.apache.org/oak/docs/command_line.html) Oak檔案的詳細資訊。

### JCR查詢速查表 {#jcrquerycheatsheet}

为了支持创建高效的 JCR 查询和索引定义，[JCR 查询备忘表](assets/JCR_query_cheatsheet-v1.1.pdf)可供下载，并可在开发过程中用作参考。它包含QueryBuilder、XPath和SQL-2的範例查詢，涵蓋了在查詢效能方面表現不同的多個情境。 它还提供了关于如何构建或定制 Oak 索引的建议。本速查表內容適用於AEM 6.5和AEMas a Cloud Service。

## 重新索引 {#re-indexing}

本節概述 **僅限** 重新索引Oak索引的可接受原因。

除了下面列出的原因外，起始Oak索引的重新索引將 **not** 變更行為或解決問題，而不必要地增加AEM的負載。

除非下表中原因涵蓋，否則應避免重新索引Oak索引。

>[!NOTE]
>
>在參閱下表以判斷是否重新索引之前很有用， **一律** 驗證：
>
>* 查詢正確
>* 查詢解析為預期的索引(使用 [說明查詢](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引程式已完成
>


### Oak索引設定變更 {#oak-index-configuration-changes}

重新索引Oak索引唯一可接受的不錯誤條件是Oak索引的設定已變更。

*重新索引一律應考慮對AEM整體效能的影響，並在活動較少或維護期間執行。*

以下詳細說明可能的問題及解決方法：

* [屬性索引定義變更](#property-index-definition-change)
* [Lucene索引定義變更](#lucene-index-definition-change)

#### 屬性索引定義變更 {#property-index-definition-change}

* 適用於/if：

   * 所有Oak版本
   * 僅限 [屬性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症状:

   * 結果中遺漏屬性索引的定義更新之前的節點

* 如何驗證：

   * 決定是否在部署更新的索引定義之前建立/修改遺漏的節點。
   * 驗證 `jcr:created` 或 `jcr:lastModified` 針對索引的修改時間的任何遺失節點屬性

* 如何解決：

   * [重新編列索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene索引
   * 或者，也可以觸控（執行良性寫入操作）遺失的節點

      * 需要手動接觸或自訂程式碼
      * 需要知道一組遺失的節點
      * 需要變更節點上的任何屬性

#### Lucene索引定義變更 {#lucene-index-definition-change}

* 適用於/if：

   * 所有Oak版本
   * 僅限 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含預期的結果
   * 查詢結果未反映索引定義的預期行為
   * 查詢計畫未根據索引定義報告預期輸出

* 如何驗證：

   * 驗證是否已使用Lucene索引統計資料JMX Mbean (LuceneIndex)方法變更索引定義 `diffStoredIndexDefinition`.

* 如何解決：

   * 1.6之前的Oak版本：

      * [重新編列索引](#how-to-re-index) lucene索引
   * Oak 1.6+版

      * 如果現有內容不受變更影響，則只需要重新整理

         * [重新整理](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) lucene索引（透過設定） [oak：queryIndexDefinition]@refresh=true
      * 否則， [重新索引](#how-to-re-index) lucene索引

         * 注意：將會使用上次良好重新索引（或初始索引）後的索引狀態，直到觸發新的重新索引為止



### 錯誤和特殊情況 {#erring-and-exceptional-situations}

下表說明重新索引Oak索引將解決此問題的唯一可接受錯誤和例外情況。

如果AEM上遇到不符合下列條件的問題，請 **not** 重新索引任何索引，因為這不能解決問題。

以下詳細說明可能的問題及解決方法：

* [缺少Lucene索引二進位檔](#lucene-index-binary-is-missing)
* [Lucene索引二進位檔已損毀](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二進位檔 {#lucene-index-binary-is-missing}

* 適用於/if：

   * 所有Oak版本
   * 僅限 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含預期的結果

* 如何驗證：

   * 錯誤記錄檔包含例外狀況，指出Lucene索引的二進位檔案遺失

* 如何解決：

   * 執行周遊存放庫檢查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      周遊存放庫會判斷是否有其他二進位檔案（lucene檔案除外）遺失

   * 如果缺少lucene索引以外的二進位檔案，請從備份還原
   * 否則， [重新索引](#how-to-re-index) *全部* lucene索引
   * 注意:

      此條件表示資料存放區設定錯誤，可能會導致ANY二進位(例如 assets二進位檔案)遺失。

      在此情況下，請還原至存放庫的最後一個已知良好版本，以復原所有遺失的二進位檔案。

#### Lucene索引二進位檔已損毀 {#lucene-index-binary-is-corrupt}

* 適用於/if：

   * 所有Oak版本
   * 僅限 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含預期的結果

* 如何驗證：

   * 此 `AsyncIndexUpdate` （每5秒）會失敗，但error.log中會有例外狀況：

      `...a Lucene index file is corrupt...`

* 如何解決：

   * 移除lucene索引的本機副本

      1. 停止AEM
      1. 刪除位於的Lucene索引的本機副本 `crx-quickstart/repository/index`
      1. 重新啟動AEM
   * 如果這不能解決問題，而且 `AsyncIndexUpdate` 例外狀況持續存在，則：

      1. [重新編列索引](#how-to-re-index) 錯誤索引
      1. 另外請將 [Adobe支援](https://helpx.adobe.com/support.html) 票證


### 如何重新編列索引 {#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中， [oak-run.jar是唯一支援的方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) ，以便在MongoMK或RDBMK存放庫上重新索引。

#### 重新索引屬性索引 {#re-indexing-property-indexes}

* 使用 [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 重新索引屬性索引
* 在屬性索引上將async-reindex屬性設定為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web主控台，透過以下非同步方式重新索引屬性索引： **PropertyIndexAsyncReindex** 兆順電子；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene屬性索引 {#re-indexing-lucene-property-indexes}

* 使用 [oak-run.jar以重新編列索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene屬性索引。
* 在lucene屬性索引上，將async-reindex屬性設定為true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>上一節概述並構架了Oak重新索引指南，來自 [Apache Oak檔案](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) 在AEM內容中。

### 二進位檔的文字預先擷取 {#text-pre-extraction-of-binaries}

文字預先擷取是指透過獨立程式，直接從資料存放區從二進位檔擷取及處理文字的程式，並直接將擷取的文字公開給後續的Oak索引重新/索引。

* 建議使用Oak文字預先擷取，在具有大量包含可擷取文字的檔案（二進位檔）的存放庫上重新編排Lucene索引(例如 PDF、Word檔案、PPT、TXT等) 透過部署的Oak索引符合全文檢索搜尋資格的物件，例如 `/oak:index/damAssetLucene`.
* 文字預先擷取將只對Lucene索引和NOT Oak屬性索引的重新編列/索引有利，因為屬性索引不會從二進位檔案中擷取文字。
* 當對大量文字的二進位檔(PDF、Doc、TXT等)進行全文重新索引時，文字預先擷取會有很高的正面影響，其中作為影像存放庫將無法享有相同的效率，因為影像不包含可擷取的文字。
* 文字預先擷取會以特別有效率的方式執行全文檢索搜尋相關文字的擷取，並以特別有效率的方式將其公開給Oak重新索引/編制索引過程。

#### 何時可以使用TEXT預先擷取？ {#when-can-text-pre-extraction-be-used}

重新索引和 **現有** 已啟用二進位擷取的lucene索引

* 重新索引處理 **全部** 存放庫中的候選內容；當要從中擷取全文檢索的二進位檔數量眾多或複雜時，AEM上會增加執行全文檢索擷取的運算負擔。 文字預先擷取會將文字擷取的「運算成本高的工作」移入直接存取AEM Data Store的隔離處理序，避免AEM中的開銷和資源爭用。

支援部署 **新** 已啟用二進位擷取的lucene索引至AEM

* 當新索引（已啟用二進位擷取）部署到AEM時，Oak會在下次非同步全文檢索索引執行時自動索引所有候選內容。 基於上述重新索引中所述的相同原因，這可能會導致AEM上的過度載入。

#### 何時可以使用文字預先擷取？ {#when-can-text-pre-extraction-not-be-used}

文字預先擷取無法用於新增到存放庫的新內容，也不需要。

新內容新增到存放庫時，非同步全文檢索索引程式（預設為每5秒一次）會自然且逐步地進行索引。

在AEM的正常運作中（例如透過網頁UI上傳資產或以程式設計方式擷取資產），AEM會自動以漸進方式完整索引新的二進位內容。 由於資料量是增量且相對較少（大約可以在5秒內保留到存放庫的資料量），AEM可以在索引期間從二進位檔案執行全文擷取，而不會影響整體系統效能。

#### 使用文字預先擷取的先決條件 {#prerequisites-to-using-text-pre-extraction}

* 您將重新索引執行全文檢索二進位擷取的Lucene索引，或部署將現有內容的全文檢索二進位索引的新索引
* 要從中預先擷取文字的內容（二進位檔）必須位於儲存庫中
* 產生CSV檔案並執行最終重新索引的維護視窗
* Oak版本： 1.0.18+、1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)1.7.4+版
* 儲存可透過索引AEM例項存取之擷取文字的檔案系統資料夾/共用

   * 文字預先解壓縮OSGi設定需要解壓縮文字檔案的檔案系統路徑，因此必須可直接從AEM執行個體（本機磁碟機或檔案共用掛載）存取

#### 如何執行文字預先擷取 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下列出的oak-run.jar命令完整列舉於 [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上述圖表和以下步驟可用於說明和補充Apache Oak檔案中概述的技術文字預先擷取步驟。

![文字預先擷取程式流程](assets/chlimage_1-139.png)

**產生要預先擷取的內容清單**

*在此作業期間周遊節點存放區時，在維護期間/低使用期間執行步驟1(a-b)，這可能會導致系統產生大量負載。*

1a. 執行 `oak-run.jar --generate` 建立節點清單，預先擷取其文字。

1b. 節點清單(1a)會以CSV檔案形式儲存至檔案系統

請注意，每次都會周遊整個節點存放區（如oak-run命令中的路徑所指定） `--generate` 「 」已執行，且 **新** CSV檔案已建立。 CSV檔案是 **not** 在文字預先擷取程式的獨立執行之間重複使用（步驟1 - 2）。

**將文字預先擷取至檔案系統**

*在AEM的正常操作期間，步驟2(a-c)可以執行，因為它只會與資料存放區互動。*

2a. 執行 `oak-run.jar --tika` 預先擷取在(1b)中產生之CSV檔案中所列舉之二進位節點的文字

2b. 在(2a)中起始的程式會直接存取Data Store中CSV定義的二進位節點，並擷取文字。

2c.  擷取的文字會以可由Oak重新索引程式(3a)擷取的格式儲存在檔案系統上

預先擷取的文字會在CSV中由二進位指紋識別。 如果二進位檔案相同，AEM執行個體之間可以使用相同的預先擷取文字。 由於AEM Publish通常是AEM Author的子集，從AEM Author預先擷取的文字通常也可以用來重新索引AEM Publish （假設AEM Publish具有擷取文字檔案的檔案系統存取權）。

預先擷取的文字可隨著時間逐漸新增至。 預先擷取的文字將略過先前擷取之二進位檔的擷取，因此最佳實務是保留預先擷取的文字，以防未來必須再次進行重新索引（假設擷取的內容不會太大）。 如果是，請評估在過渡期間壓縮內容（因為文字壓縮得不錯）。

**重新索引Oak索引，從擷取的文字檔案取得全文檢索**

*在此操作期間周遊節點存放區時，在維護/低使用期間執行重新索引（步驟3a-b），這可能會導致系統產生大量負載。*

3a. [重新編列索引](#how-to-re-index) 在AEM中叫用的Lucene索引

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi設定（設定為透過檔案系統路徑指向已擷取的文字）會指示Oak從已擷取的檔案取得全文檢索文字，並避免直接點選及處理儲存於存放庫中的資料。
