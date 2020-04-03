---
title: 查询Builder API
seo-title: 查询Builder API
description: 资产共享查询构建器的功能通过Java API和REST API公开。
seo-description: 资产共享查询构建器的功能通过Java API和REST API公开。
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: a491d4e9bd9ffc68c4ba7cac3149f48cf7576ee8

---


# 查询Builder API{#query-builder-api}

资产共享 [查询构建器的功能](/help/assets/assets-finder-editor.md) ，通过Java API和REST API公开。 本节介绍这些API。

服务器端查询构建器( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))将接受查询描述，创建并运行XPath查询，有选择地过滤结果集，并根据需要提取彩块化。

查询描述只是一组谓词([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 例如，全文谓词与XPath中的函 `jcr:contains()` 数相对应。

对于每个谓词类型，都有一个计算器组件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，它知道如何处理XPath、筛选和facet提取的特定谓词。 很容易创建自定义求值器，它们通过OSGi组件运行时插入。

REST API通过HTTP提供对完全相同功能的访问，响应以JSON形式发送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API构建的。 您还可以从OSGi捆绑包中使用JCR API，来查询Adobe Experience Manager JCR。 有关信息，请参 [阅使用JCR API查询Adobe Experience Manager数据](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## Gem会议 {#gem-session}

[AEM Gems是](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Adobe专家提供的一系列深入探讨Adobe Experience Manager的技术知识。 此专用于查询构建器的会话对于工具的概述和使用非常有用。

>[!NOTE]
>
>有关查询构建器的 [详细概述，请参阅AEM Gem会话“搜索表单”](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) （使用AEM Querybuilder轻松搜索表单）。

## 示例查询 {#sample-queries}

这些范例以Java属性样式表示法提供。 要将它们与Java API一起使用，请使用Java, `HashMap` 如下面的API范例中所示。

对于 `QueryBuilder` JSON Servlet，每个示例都包含一个指向本地CQ安装的链接(位于默认位置 `http://localhost:4502`)。 请注意，您必须先登录到CQ实例，然后才能使用这些链接。

>[!CAUTION]
>
>默认情况下，查询构建器json servlet最多显示10次点击。
>
>添加以下参数后，servlet便可显示所有查询结果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>要在浏览器中视图返回的JSON数据，您可能希望使用插件，如JSONView for Firefox。

### 返回所有结果 {#returning-all-results}

以下查询将 **返回十个结果** （或精确到最多十个），但会通知您点击 **次数：** 它们实际上可用：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

同一查询(带有参 `p.limit=-1`数)将 **返回所有结果** （根据您的实例，此数字可能较高）:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### 使用p.guessTotal返回结果 {#using-p-guesstotal-to-return-the-results}

该参数的目 `p.guessTotal` 的是返回通过组合最小可行的p.offset和p.limit值可以显示的适当数目的结果。 使用此参数的优点是提高了大结果集的性能。 这避免了计算完全总数(例如调用result.getSize())和读取整个结果集，并一直优化到OAK引擎和索引。 当结果达到100,000个时，这可能是显着的差异，无论是执行时间和内存使用。

该参数的缺点是用户看不到确切的总数。 但是，您可以设置一个像p.guessTotal=1000这样的最小数字，这样它将始终读取1000，因此您可以获得较小结果集的精确总数，但如果它大于此值，则只能显示“和更多”。

添加 `p.guessTotal=true` 到以下查询，了解其工作方式：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查询将返回具有 `p.limit` 偏移 `10` 的默认结果 `0` 值：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

自AEM 6.0 SP2起，您还可以使用一个数值计算最多自定义数量的最大结果。 使用与上述查询相同的，但将其值更改 `p.guessTotal` 为 `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它将返回一个与默认限制相同的数字：10个结果，0个偏移，但最多只显示50个结果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 实施分页 {#implementing-pagination}

默认情况下，查询生成器还将提供点击数。 由于确定准确计数涉及检查每个结果的访问控制，因此，这可能需要很长时间。 大多数情况下，总数用于为最终用户UI实现分页。 由于确定准确计数可能会很慢，建议使用guessTotal功能来实现分页。

例如，UI可以调整以下方法：

* 获取并显示准确的总点击数([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) ，或querybuilder.json响应中的总点击数)小于或等于100;
* 拨 `guessTotal` 叫查询生成器时设置为100。

* 响应可能具有以下结果：

   * `total=43`, `more=false` -指示点击总数为43。 UI在第一页中最多可显示十个结果，并为后三页提供分页。 您还可以使用此实现显示描述性文本，如“ **找到43个结果”**。
   * `total=100`, `more=true` -指示点击总数大于100且不知道确切计数。 UI在第一页中最多可显示十个，并为接下来的十个页面提供分页。 您还可以使用它显示文本，如“ **找到100个以上结果”**。 当用户转到下一页时，对查询生成器进行的调用将增加和参数 `guessTotal` 的限制以 `offset` 及限 `limit` 制。

`guessTotal` 也应用于UI需要使用无限滚动的情况，以避免查询生成器确定确切的命中计数。

### 查找jar文件并对其排序，最新优先 {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有页面并按上次修改时间对它们进行排序 {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有页面并按上次修改时间（但以降序排列）对它们进行排序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### 全文搜索，按得分排序 {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### 搜索带有特定标记的页面 {#search-for-pages-tagged-with-a-certain-tag}

“http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags”

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

如果您 `tagid` 知道显式标记ID，请使用示例中的谓词。

使用标 `tag` 签标题路径的谓词（不带空格）。

因为，在上一个示例中，您正在搜索页面( `cq:Page` 节点)，所以您需要将该节点的相对路径用于谓 `tagid.property` 词，即 `jcr:content/cq:tags`。 默认情况下，这 `tagid.property` 只是一种情 `cq:tags`况。

### 在多个路径下搜索（使用组） {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查询使用 *组*`group`（名为“”），该组的作用是在查询中分隔子表达式，就像括号在更标准的符号中所做的那样。 例如，上一个查询可能以更熟悉的样式表示为：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在示例中的组中，该谓 `path` 词被多次使用。 要区分谓词的两个实例并对其进行排序（某些谓词需要排序），您必须在谓词前面加 *N*`_ where`*N *是排序索引。 在上一个示例中，生成的谓词是`1_path`和`2_path`。

in是 `p` 一 `p.or` 个特殊分隔符，指示后面的内容(本例中为 `or`)是组的参数 *，而不是组的子谓词，例如*`1_path`。

如果没有 `p.or` 给出谓词，则所有谓词将一起使用，即每个结果必须满足所有谓词。

>[!NOTE]
>
>不能在一个查询中使用相同的数字前缀，即使对于不同的谓词也是如此。

### 搜索属性 {#search-for-properties}

在此，您将使用以下属性搜索给定模板的所有 `cq:template` 页面：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

这样做的缺点是返 `jcr:content` 回页面的节点，而不是页面本身。 要解决此问题，您可以按相对路径进行搜索：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜索多个属性 {#search-for-multiple-properties}

当多次使用属性谓词时，您必须再次添加数字前缀：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜索多个属性值 {#search-for-multiple-property-values}

要避免在搜索属性( `"A" or "B" or "C"`)的多个值时出现大组，您可以为谓词提供多个 `property` 值：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

对于多值属性，您还可以要求多个值匹配( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 优化返回内容 {#refining-what-is-returned}

默认情况下，QueryBuilder JSON Servlet将为搜索结果中的每个节点返回一组默认属性（如路径、名称、标题等）。 要控制返回的属性，您可以执行下列操作之一：

指定

```
p.hits=full
```

在这种情况下，每个节点都将包含所有属性：

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

用法

```
p.hits=selective
```

并指定要加入的属性

```
p.properties
```

以空格分隔：

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle)[p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.nodedepth=5&p.properties=sling%3aresourceType%20jcr%3apath&property=jcr%3atitle&property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

您还可以做的另一件事是在QueryBuilder响应中包含子节点。 为此，您需要指定

```
p.nodedepth=n
```

其中 `n` 是您希望查询返回的级别数。 请注意，要返回子节点，必须由属性选择器指定它

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

## 更多谓词 {#morepredicates}

有关更多谓词，请参阅“ [查询生成器谓词引用”页](/help/sites-developing/querybuilder-predicate-reference.md)。

您还可以检查类 [的Javadoc `PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)。 这些类的Javadoc包含可使用的属性的列表。

类名的前缀(例如，“” `similar`在 [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)中)是 *类的主属性* 。 此属性也是要在查询中使用的谓词的名称（小写）。

对于此类主体属性，您可以缩短查询，并使用“ `similar=/content/en`”而不是完全限定的变体“ `similar.similar=/content/en`”。 完全限定的表单必须用于类的所有非主属性。

## 查询构建器API使用示例 {#example-query-builder-api-usage}

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
>要了解如何构建使用QueryBuilder API的OSGi捆绑包并在Adobe Experience Manager应用程序中使用该OSGi捆绑包，请参阅 [Creating Adobe CQ OSGi捆绑包(使用查询Builder](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)API)。

使用查询构建器(JSON)Servlet通过HTTP执行的同一查询:

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 存储和加载查询 {#storing-and-loading-queries}

查询可以存储到存储库，以便您以后可以使用它们。 提供 `QueryBuilder` 了“具有 `storeQuery` 以下签名的方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

当使用该方 [ 法时，给定的 `QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) 内容会作为文件或根据参数值作为属性存储在存储库 `Query``createFile` 中。 以下示例演示如何将路径 `Query` 另存为 `/mypath/getfiles` 文件：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

使用以下方法，可以从存储库中加载任何以前存储的查询 [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) :

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如，存储 `Query` 到路径的代码 `/mypath/getfiles` 片断可以由以下代码片断加载：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 测试和调试 {#testing-and-debugging}

要播放和调试querybuilder查询，可使用QueryBuilder调试器控制台(位于

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或者，在

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` 仅是示例)。

### 一般调试建议 {#general-debugging-recommendations}

### 通过记录获得可解释的XPath {#obtain-explain-able-xpath-via-logging}

根据 **目标指** 数集，说明开发周期中的所有查询。

* 为QueryBuilder启用DEBUG日志以获取基础的、可解释的XPath查询

   * 导航到https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在 `com.day.cq.search.impl.builder.QueryImpl` DEBUG中创建新的记 **录**&#x200B;器。

* 为上述类启用DEBUG后，日志将显示由查询生成器生成的XPath。
* 从关联的QueryBuilder查询的日志条目中复制XPath查询，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 将XPath查询粘贴到 [Explain查询中](/help/sites-administering/operations-dashboard.md#explain-query) ，作为XPath获得查询计划

### 通过查询Builder调试器获得可解释的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* 使用AEM QueryBuilder调试器生成一个可解释的XPath查询:

根据 **目标指** 数集，说明开发周期中的所有查询。

**通过记录获得可解释的XPath**

* 为QueryBuilder启用DEBUG日志以获取基础的、可解释的XPath查询

   * 导航到https://&lt;serveraddress>:&lt;serverport>/system/console/slinglog。 在 `com.day.cq.search.impl.builder.QueryImpl` DEBUG中创建新的记 **录**&#x200B;器。

* 为上述类启用DEBUG后，日志将显示由查询生成器生成的XPath。
* 从关联的QueryBuilder查询的日志条目中复制XPath查询，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 将XPath查询粘贴到 [Explain查询中](/help/sites-administering/operations-dashboard.md#explain-query) ，作为XPath以获得查询计划

**通过查询Builder调试器获得可解释的XPath**

* 使用AEM QueryBuilder调试器生成一个可解释的XPath查询:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在查询生成器调试器中提供查询生成器查询
1. 执行搜索
1. 获取生成的XPath
1. 将XPath查询粘贴到Explain查询中作为XPath，以获得查询计划

>[!NOTE]
>
>非querybuilder查询(XPath、JCR-SQL2)可直接提供给“解释查询”。

有关如何使用QueryBuilder调试查询的运行说明，请观看以下视频。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 使用记录调试查询 {#debugging-queries-with-logging}

>[!NOTE]
>
>有关登录程序的配置，请参阅创建您 [自己的登录程序和作者一节](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers)。

执行测试和调试中所述的查询时，查询生成器实现的日志输出（INFO级别）:

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

如果您有使用谓词计算器进行筛选的查询，或者使用按比较器进行的自定义顺序，则查询中也将记录这一点：

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

## Javadoc链接 {#javadoc-links}

| **Javadoc** | **描述** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | 基本QueryBuilder和查询API |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | 结果API |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | 彩块化 |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 存储段（包含在彩块化中） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 谓词计算器 |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet提取器（用于计算器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | 针对Querybuilder servlet的JSON结果命中写入程序(/bin/querybuilder.json) |

