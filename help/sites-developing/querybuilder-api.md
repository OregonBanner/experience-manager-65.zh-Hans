---
title: 查询生成器 API
seo-title: Query Builder API
description: Asset Share Query Builder的功能會透過Java API和REST API公開。
seo-description: The functionality of the Asset Share Query Builder is exposed through a Java API and a REST API.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
source-git-commit: 13f15bee38b6b4af4cd59376849810a788f0c467
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 0%

---

# 查询生成器 API{#query-builder-api}

的功能 [資產共用查詢產生器](/help/assets/assets-finder-editor.md) 會透過Java API和REST API公開。 本節將說明這些API。

伺服器端查詢產生器( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))將接受查詢說明、建立並執行XPath查詢、選擇性地篩選結果集，以及視需要擷取Facet。

查詢說明只是一組述詞([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 範例包括全文檢索述詞，其對應至 `jcr:contains()` XPath中的函式。

對於每個述詞型別，都有一個求值器元件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，知道如何處理XPath、篩選和Facet擷取的特定述詞。 建立自訂評估器非常容易，可透過OSGi元件執行階段插入。

REST API可讓您透過HTTP存取完全相同的功能，且回應會以JSON傳送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API建置。 您也可以使用OSGi套件中的JCR API來查詢Adobe Experience Manager JCR。 如需詳細資訊，請參閱 [使用JCR API的Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html?lang=en).

## Gem講座 {#gem-session}

[AEM Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/overview.html) 是Adobe專家為Adobe Experience Manager提供的一系列深入技術探討。 此查詢產生器專用的工作階段對於工具的概述和使用非常有用。

>[!NOTE]
>
>請參閱AEM Gem研討會 [使用AEM查詢建立器輕鬆搜尋表單](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html) 以取得查詢產生器的詳細概觀。

## 範例查詢 {#sample-queries}

這些範例以Java屬性樣式標籤法提供。 若要搭配Java API使用，請使用Java `HashMap` 與下列API範例相同。

對於 `QueryBuilder` JSON Servlet，每個範例都包含本機CQ安裝的連結(在預設位置， `http://localhost:4502`)。 請注意，您必須先登入您的CQ執行個體，才能使用這些連結。

>[!CAUTION]
>
>依預設，查詢產生器json servlet最多可顯示10次點選。
>
>新增以下引數可讓servlet顯示所有查詢結果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>若要在瀏覽器中檢視傳回的JSON資料，您可能會想要使用外掛程式，例如Firefox適用的JSONView。

### 傳回所有結果 {#returning-all-results}

下列查詢將 **傳回10個結果** （精確地說，最多為10個），但通知您 **點選次數：** 實際可用的：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

相同查詢（使用引數） `p.limit=-1`)會 **傳回所有結果** （根據您的執行個體，此數字可能會很高）：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal傳回結果 {#using-p-guesstotal-to-return-the-results}

目的 `p.guessTotal` 引數為傳回適當數目的結果，可藉由結合最小可行p.offset和p.limit值來顯示。 使用此引數的優點是在大型結果集中改善效能。 這樣可以避免計算完整總計(例如呼叫result.getSize())和讀取整個結果集，一直最佳化到OAK引擎和索引。 當執行時間和記憶體使用量都有10萬個結果時，這可能是一個顯著的差異。

此引數的缺點是使用者看不到確切的總數。 但是您可以設定最小值，例如p.guessTotal=1000，這樣它就會一直讀取到1000，所以您可以得到較小結果集的精確總計，但是如果超過此值，您只能顯示「等等」。

新增 `p.guessTotal=true` 若要檢視其運作方式，請執行下列動作：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查詢會傳回 `p.limit` 預設 `10` 結果包含 `0` offset：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

自AEM 6.0 SP2起，您也可以使用數值來計數至自訂的最大結果數量。 使用與上述相同的查詢，但變更值 `p.guessTotal` 至 `50`：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它會傳回一個數字，預設限製為10個結果，位移為0，但最多只會顯示50個結果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 實作分頁 {#implementing-pagination}

依預設，查詢產生器也會提供點選次數。 根據結果大小，這可能需要很長的時間，因為要判斷準確的計數，需要檢查存取控制的每個結果。 總計主要用於為一般使用者UI實作分頁。 由於判斷確切計數可能會變慢，建議使用guessTotal功能來實作分頁。

例如，UI可以調整以下方法：

* 取得並顯示點選總數的精確計數([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) 或total （在querybuilder.json回應中）小於或等於100；
* 設定 `guessTotal` 至100，同時呼叫查詢產生器。

* 回應可能會產生下列結果：

   * `total=43`， `more=false`  — 表示點選總數為43。 UI可以在第一個頁面中顯示最多十個結果，並為接下來的三個頁面提供分頁。 您也可以使用此實作來顯示描述性文字，例如 **「找到43個結果」**.
   * `total=100`， `more=true`  — 表示點選總數大於100，但不確定確切計數。 UI最多可顯示10個做為第一頁的一部分，並為接下來的10個頁面提供分頁。 您也可以使用此選項來顯示文字，例如 **「找到100個以上的結果」**. 當使用者前往下一頁時，對查詢產生器的呼叫將增加限制 `guessTotal` 以及 `offset` 和 `limit` 引數。

`guessTotal` 當UI需要使用無限捲動時，也應使用，以避免Query Builder判斷確切的點選計數。

### 尋找jar檔案並排序，最新的先排序 {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 尋找所有頁面，並按上次修改時間排序 {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 尋找所有頁面，並按上次修改時間降序排序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文檢索搜尋，依分數排序 {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜尋以特定標籤標籤的頁面 {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

使用 `tagid` 如果您知道明確的標籤ID，請依照此範例使用述詞。

使用 `tag` 標籤標題路徑的述詞（不含空格）。

因為在上一個範例中，您搜尋的頁面( `cq:Page` 節點)，則您需要使用該節點的相對路徑 `tagid.property` 述詞，即 `jcr:content/cq:tags`. 根據預設， `tagid.property` 將只是 `cq:tags`.

### 在多個路徑下搜尋（使用群組） {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查詢使用 *群組* (已命名&quot; `group`&quot;)，其作用是在查詢中分隔子運算式，就像括弧在較標準符號中的作用一樣。 例如，先前的查詢可能會以更熟悉的樣式表示，例如：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在範例的群組內， `path` 述詞使用多次。 若要區分和排序述詞的兩個執行個體（某些述詞需要排序），您必須為述詞加上前置詞 *N* `_ where`*N* 是排序索引。 在上一個範例中，產生的述詞是 `1_path` 和 `2_path`.

此 `p` 在 `p.or` 是一個特殊分隔符號，指示接續的內容(在此例中為 `or`)是 *引數* 群組的，而不是群組的子述詞，例如 `1_path`.

若否 `p.or` 然後所有述詞一起進行AND運算，也就是說，每個結果都必須滿足所有述詞。

>[!NOTE]
>
>您無法在一個查詢中使用相同的數值首碼，即使對於不同的述詞亦然。

### 搜尋屬性 {#search-for-properties}

您在這裡使用 `cq:template` 屬性：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

其缺點在於 `jcr:content` 會傳回頁面的節點，而非頁面本身。 若要解決此問題，您可以依相對路徑搜尋：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜尋多個屬性 {#search-for-multiple-properties}

多次使用屬性述詞時，您必須再次新增數字首碼：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜尋多個屬性值 {#search-for-multiple-property-values}

若要在搜尋屬性的多個值時避免大型群組( `"A" or "B" or "C"`)，則可以將多個值提供給 `property` 述詞：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

針對多值屬性，您也可以要求多個值相符( `"A" and "B" and "C"`)：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 精簡傳回的專案 {#refining-what-is-returned}

依預設，QueryBuilder JSON Servlet會傳回搜尋結果中每個節點的預設屬性集（例如路徑、名稱、標題等）。 若要取得傳回哪些屬性的控制權，您可以執行下列任一項作業：

指定

```
p.hits=full
```

在這種情況下，每個節點都將包含所有屬性：

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

使用

```
p.hits=selective
```

並指定要加入的屬性

```
p.properties
```

以空格分隔：

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=三角形

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

另一個您可以做的就是在QueryBuilder回應中包含子節點。 若要這麼做，您需要指定

```
p.nodedepth=n
```

位置 `n` 是您希望查詢傳回的層級數。 請注意，若要傳回子節點，它必須由屬性選取器指定

```
p.hits=full
```

示例:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## 更多述詞 {#morepredicates}

如需更多述詞，請參閱 [查詢產生器述詞參考頁面](/help/sites-developing/querybuilder-predicate-reference.md).

您也可以檢查 [的Javadoc `PredicateEvaluator` 類別](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). 這些類別的Javadoc包含您可以使用的屬性清單。

類別名稱的前置詞(例如&quot; `similar`中的「」 [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html))是 *主體屬性* 類別的。 此屬性也是要在查詢中使用的述詞名稱（小寫）。

對於這類主體屬性，您可以縮短查詢並使用「 `similar=/content/en`「而非完整變體」 `similar.similar=/content/en`「。 類別的所有非主要屬性都必須使用完整表單。

## 查詢產生器API使用範例 {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>若要瞭解如何建立使用QueryBuilder API的OSGi套件組合，並在Adobe Experience Manager應用程式中使用該OSGi套件組合，請參閱 [建立使用查詢產生器AP的Adobe CQ OSGi套件組合](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)I.

使用查詢產生器(JSON) Servlet透過HTTP執行的相同查詢：

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 儲存和載入查詢 {#storing-and-loading-queries}

查詢可以儲存在存放庫中，以便您稍後使用。 此 `QueryBuilder` 提供&quot; `storeQuery` 具有下列簽章的方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用時 [ `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) 方法，給定 `Query` 會根據「 」以檔案或屬性的形式儲存至存放庫 `createFile` 引數值。 以下範例說明如何儲存 `Query` 至路徑 `/mypath/getfiles` 以檔案形式：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

任何先前儲存的查詢都可使用從存放庫載入 [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) 方法：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如， `Query` 儲存至路徑 `/mypath/getfiles` 可透過下列程式碼片段載入：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 測試和偵錯 {#testing-and-debugging}

若要解決和偵錯QueryBuilder查詢，您可以使用QueryBuilder Debugger主控台：

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或選擇位於的querybuilder json servlet

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` 只是一個範例)。

### Recommendations一般偵錯 {#general-debugging-recommendations}

### 透過記錄取得可說明的XPath {#obtain-explain-able-xpath-via-logging}

說明 **全部** 在開發週期期間針對目標索引集進行查詢。

* 啟用QueryBuilder的DEBUG記錄檔，以取得基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>：&lt;serverport>/system/console/slinglog。 建立新的記錄器 `com.day.cq.search.impl.builder.QueryImpl` 於 **偵錯**.

* 為上述類別啟用DEBUG後，記錄會顯示Query Builder產生的XPath。
* 從相關QueryBuilder查詢的記錄專案複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼入 [說明查詢](/help/sites-administering/operations-dashboard.md#explain-query) 作為XPath以取得查詢計畫

### 透過Query Builder Debugger取得可說明的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* 使用AEM QueryBuilder Debugger產生可解釋的XPath查詢：

說明 **全部** 在開發週期期間針對目標索引集進行查詢。

**透過記錄取得可說明的XPath**

* 啟用QueryBuilder的DEBUG記錄檔，以取得基礎、可解釋的XPath查詢

   * 導覽至https://&lt;serveraddress>：&lt;serverport>/system/console/slinglog。 建立新的記錄器 `com.day.cq.search.impl.builder.QueryImpl` 於 **偵錯**.

* 為上述類別啟用DEBUG後，記錄會顯示Query Builder產生的XPath。
* 從相關QueryBuilder查詢的記錄專案複製XPath查詢，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 將XPath查詢貼入 [說明查詢](/help/sites-administering/operations-dashboard.md#explain-query) 作為XPath以取得查詢計畫

**透過Query Builder Debugger取得可說明的XPath**

* 使用AEM QueryBuilder Debugger產生可解釋的XPath查詢：

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在Query Builder Debugger中提供查詢產生器查詢
1. 執行搜尋
1. 取得產生的XPath
1. 將XPath查詢貼入Explain Query做為XPath以取得查詢計畫

>[!NOTE]
>
>非Querybuilder查詢(XPath、JCR-SQL2)可直接提供給Explain Query。

如需有關如何使用QueryBuilder偵錯查詢的下拉式清單，請參閱以下影片。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 使用記錄功能偵錯查詢 {#debugging-queries-with-logging}

>[!NOTE]
>
>區段中會說明記錄器的設定 [建立自己的記錄器和寫入器](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

執行測試和偵錯中所述的查詢時，查詢產生器實作的記錄輸出（INFO層級）：

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

如果您的查詢使用述詞評估器，這些評估器會篩選或使用自訂的比較順序，這也會在查詢中記錄：

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Javadoc連結 {#javadoc-links}

| **Javadoc** | **描述** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 基本QueryBuilder和查詢API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 結果API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 值區（包含在Facet中） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 述詞評估器 |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet擷取器（適用於評估器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Querybuilder servlet的JSON結果點選撰寫器(/bin/querybuilder.json) |
