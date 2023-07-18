---
title: 查询生成器 API
description: 资产共享查询生成器的功能通过Java&trade； API和REST API公开。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
pagetitle: Query Builder API
tagskeywords: querybuilder
exl-id: b2288442-d055-4966-8057-8b7b7b6bff28
source-git-commit: a66814fa065b7545ec39fe9109b4c5815fa199da
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 0%

---

# 查询生成器 API{#query-builder-api}

的功能 [资产共享查询生成器](/help/assets/assets-finder-editor.md) 通过Java™ API和REST API公开。 本节介绍了这些API。

服务器端查询生成器( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html))接受查询描述，创建并运行XPath查询，可以选择筛选结果集，并根据需要提取Facet。

查询描述只是一组谓词([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html))。 示例包括一个全文谓词，该谓词对应于 `jcr:contains()` 函数。

对于每个谓词类型，都有一个计算器组件([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html))，知道如何处理XPath、筛选和Facet提取的特定谓词。 可以轻松创建自定义评估器，这些评估器通过OSGi组件运行时插入。

REST API通过HTTP提供对相同功能的访问，响应以JSON发送。

>[!NOTE]
>
>QueryBuilder API是使用JCR API构建的。 您还可以使用OSGi捆绑包中的JCR API查询Adobe Experience Manager JCR。 有关信息，请参阅 [使用JCR API的Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html?lang=en).

## Gem会话 {#gem-session}

[Adobe Experience Manager (AEM) Gems](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/overview.html) 是Adobe专家对Adobe Experience Manager进行的一系列深入技术探讨。 此专门用于查询生成器的会话对于该工具的概述和使用非常有用。

>[!NOTE]
>
>AEM Gem会话 [使用AEM查询生成器轻松搜索表单](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2017/aem-search-forms-using-querybuilder.html) 有关查询生成器的详细概述。

## 示例查询 {#sample-queries}

这些示例以Java™属性样式表示法提供。 要将其与Java™ API结合使用，请使用Java™ `HashMap` 与下面的API示例中一样。

对于 `QueryBuilder` JSON Servlet，每个示例都包含一个指向您的本地CQ安装的链接(位于默认位置， `http://localhost:4502`)。 在使用这些链接之前，您必须登录到CQ实例。

>[!CAUTION]
>
>默认情况下，查询生成器json servlet最多可显示10次点击。
>
>添加以下参数可让servlet显示所有查询结果：
>
>**`p.limit=-1`**

>[!NOTE]
>
>要在浏览器中查看返回的JSON数据，您可能要使用诸如JSONView for Firefox之类的插件。

### 返回所有结果 {#returning-all-results}

以下查询 **返回十个结果** （确切地说，最多为10个），但请注意 **点击次数：** 可用的：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

相同查询（使用参数） `p.limit=-1`)将 **返回所有结果** （根据您的实例，此数字可能会很高）：

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

目的 `p.guessTotal` 参数是返回适当数量的结果，这些结果可以通过组合最小可行p偏移量和p限制值来显示。 使用该参数的优点是改善了性能，且结果集大。 这样可避免计算完整总计(例如，调用result.getSize())和读取整个结果集，从而可优化一直到Oak引擎和索引。 当执行时间和内存使用量都有10万个结果时，这可能存在显着差异。

该参数的缺点是用户看不到确切的总数。 但您可以设置一个最小值，如p.guessTotal=1000，以便它始终可读取多达1000个结果，这样您便可获得较小结果集的精确总计，但是如果大于此值，则只能显示“和更多”。

添加 `p.guessTotal=true` ，以了解其工作原理：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

查询返回 `p.limit` 默认 `10` 结果带有 `0` 偏移：

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

从AEM 6.0 SP2开始，您还可以使用数字值进行计数，以自定义最大结果数。 使用与上述相同的查询，但更改 `p.guessTotal` 到 `50`：

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

它返回一个数字，该数字与偏移量为0的十个结果的缺省限制相同，但最多只显示50个结果：

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### 实施分页 {#implementing-pagination}

默认情况下，查询生成器还会提供点击量。 根据结果大小，这可能需要较长时间，因为确定准确计数涉及检查每个结果的访问控制。 通常，总计用于对最终用户UI实现分页。 由于确定确切计数可能会很慢，因此建议使用guessTotal功能实施分页。

例如，UI可以调整以下方法：

* 获取并显示总点击量的准确计数([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) Querybuilder.json响应中的或total)小于或等于100；
* 设置 `guessTotal` 调用查询生成器时为100。

* 响应可能会产生以下结果：

   * `total=43`， `more=false`  — 表示点击总数为43。 UI可以在第一个页面中显示最多十个结果，并为接下来的三个页面提供分页。 您还可以使用此实施来显示描述性文本，如 **“找到43个结果”**.
   * `total=100`， `more=true`  — 表示点击总数大于100，但确切计数未知。 UI最多可以显示10个作为第一页的一部分，并为接下来的10个页面提供分页。 您还可以使用此选项来显示文本，例如 **“找到100个以上的结果”**. 当用户转到下一页时，调用查询生成器将增加限制 `guessTotal` 以及 `offset` 和 `limit` 参数。

`guessTotal` 在UI需要使用无限滚动以避免Query Builder确定确切点击计数的情况下应使用。

### 查找jar文件并对其进行排序，最新的先排序 {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### 查找所有页面并按上次修改时间对页面进行排序 {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### 查找所有页面并按上次修改时间对页面进行排序，但降序 {#find-all-pages-and-order-them-by-last-modified-but-descending}

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

### 搜索使用特定标记进行标记的页面 {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&tagid=marketing:interest/product&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

使用 `tagid` 谓词（如示例中所示），前提是您知道显式标记ID。

使用 `tag` 标记标题路径的谓词（不含空格）。

在上一个示例中，由于您正在搜索页面( `cq:Page` 节点)，使用该节点的相对路径 `tagid.property` 谓词，即 `jcr:content/cq:tags`. 默认情况下， `tagid.property` 就只是 `cq:tags`.

### 在多个路径下搜索（使用组） {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

此查询使用 *群组* (已命名&quot; `group`“)，它用于在查询中分隔子表达式，就像括号在更标准的符号中一样。 例如，上一个查询可能以更熟悉的样式表示，如：

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

在示例中的组内， `path` 谓词使用多次。 要区分谓词的两个实例并对其进行排序（某些谓词需要排序），必须在谓词的前缀中添加 *N* `_ where`*N* 是排序索引。 在上一个示例中，生成的谓词是 `1_path` 和 `2_path`.

此 `p` 在 `p.or` 是一个特殊分隔符，指示随后出现的内容(在本例中为 `or`)是 *参数* 组的一个子谓词，例如 `1_path`.

如果否 `p.or` 然后对所有谓词进行AND运算，即每个结果必须满足所有谓词。

>[!NOTE]
>
>不能在一个查询中使用相同的数字前缀，即使对于不同的谓词也是如此。

### 搜索属性 {#search-for-properties}

在此，您将使用 `cq:template` 属性：

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

这有一个缺点 `jcr:content` 返回的是页面的节点，而不是页面本身。 要解决此问题，您可以按相对路径搜索：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### 搜索多个属性 {#search-for-multiple-properties}

多次使用属性谓词时，必须再次添加数字前缀：

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### 搜索多个属性值 {#search-for-multiple-property-values}

要在搜索属性的多个值时避免大型组( `"A" or "B" or "C"`)，则可以为提供多个值 `property` 谓词：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

对于多值属性，您还可以要求多个值匹配( `"A" and "B" and "C"`)：

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## 优化返回的内容 {#refining-what-is-returned}

默认情况下，QueryBuilder JSON Servlet返回搜索结果中每个节点的默认属性集（例如，路径、名称和标题）。 要获得对返回哪些属性的控制权，您可以执行以下操作之一：

指定

```
p.hits=full
```

在这种情况下，将包含每个节点的所有属性：

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

并指定要获取的属性

```
p.properties
```

以空格分隔：

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[`http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=Triangle) [p.hits=selective&amp;](http://localhost:4502/bin/querybuilder.json?p.hits=selective&amp;p.nodedepth=5&amp;p.properties=sling%3aresourceType%20jcr%3apath&amp;property=jcr%3atitle&amp;property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3aprimaryType&amp;property=jcr%3atitle&amp;property.value=三角形

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

另一种做法是在QueryBuilder响应中包含子节点。 为此，您必须指定

```
p.nodedepth=n
```

位置 `n` 是您希望查询返回的级别数。 对于要返回的子节点，必须由属性选择器指定

```
p.hits=full
```

示例：

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## 更多谓词 {#morepredicates}

有关更多谓词，请参见 [查询生成器谓词引用页](/help/sites-developing/querybuilder-predicate-reference.md).

您还可以检查 [的Javadoc `PredicateEvaluator` 类](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). 这些类的Javadoc包含您可以使用的属性列表。

类名的前缀(例如， ” `similar`中的“” [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html))是 *主体属性* 是班级的。 此属性也是要在查询中使用的谓词名称（小写）。

对于此类主体属性，您可以缩短查询并使用“ `similar=/content/en`“而不是完全限定的变体” `similar.similar=/content/en`“。 类的所有非主体属性都必须使用完全限定的表单。

## 示例查询生成器API用法 {#example-query-builder-api-usage}

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
>要了解如何构建使用QueryBuilder API并在Adobe Experience Manager应用程序中使用该OSGi包的OSGi包，请参阅 [创建使用查询生成器AP的Adobe CQ OSGi包](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)我。

使用查询生成器(JSON) Servlet通过HTTP执行的相同查询：

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## 存储和加载查询 {#storing-and-loading-queries}

查询可以存储在存储库中，以便您以后使用。 此 `QueryBuilder` 提供&quot; `storeQuery` 具有以下签名的方法：

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

使用时 [`QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) 方法，给定 `Query` 作为文件或属性存储在存储库中，具体情况如下： `createFile` 参数值。 以下示例说明如何保存 `Query` 到路径 `/mypath/getfiles` 作为文件：

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

任何之前存储的查询都可以使用从存储库中加载 [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) 方法：

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

例如， `Query` 存储到路径 `/mypath/getfiles` 可以由以下代码片段加载：

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## 测试和调试 {#testing-and-debugging}

要绕过并调试QueryBuilder查询，您可以使用QueryBuilder调试器控制台，网址为

`http://localhost:4502/libs/cq/search/content/querydebug.html`

或者，查询生成器json servlet位于

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` 只是一个示例)。

### 常规调试Recommendations {#general-debugging-recommendations}

### 通过日志记录获取可解释的XPath {#obtain-explain-able-xpath-via-logging}

说明 **所有** 在开发周期期间针对目标索引集进行查询。

* 为QueryBuilder启用DEBUG日志，以获取基础、可解释的XPath查询

   * 导航到https://&lt;serveraddress>：&lt;serverport>/system/console/slinglog. 为创建记录器 `com.day.cq.search.impl.builder.QueryImpl` 在 **调试**.

* 为上述类启用DEBUG后，日志显示由Query Builder生成的XPath。
* 从关联的QueryBuilder查询的日志条目中复制XPath查询，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 将XPath查询粘贴到 [说明查询](/help/sites-administering/operations-dashboard.md#explain-query) 作为XPath以获取查询计划

### 通过Query Builder调试器获取可解释的XPath {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* 使用AEM QueryBuilder调试器生成可解释的XPath查询：

说明 **所有** 在开发周期期间针对目标索引集进行查询。

**通过日志记录获取可解释的XPath**

* 为QueryBuilder启用DEBUG日志，以获取基础、可解释的XPath查询

   * 导航到https://&lt;serveraddress>：&lt;serverport>/system/console/slinglog. 为创建记录器 `com.day.cq.search.impl.builder.QueryImpl` 在 **调试**.

* 为上述类启用DEBUG后，日志显示由Query Builder生成的XPath。
* 从关联的QueryBuilder查询的日志条目中复制XPath查询，例如：

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* 将XPath查询粘贴到 [说明查询](/help/sites-administering/operations-dashboard.md#explain-query) 作为XPath以获取查询计划

**通过Query Builder调试器获取可解释的XPath**

* 使用AEM QueryBuilder调试器生成可解释的XPath查询：

![chlimage_1-66](assets/chlimage_1-66a.png)

1. 在Query Builder Debugger中提供查询生成器查询
1. 执行搜索
1. 获取生成的XPath
1. 将XPath查询粘贴到Explain Query中作为XPath以获取查询计划

>[!NOTE]
>
>可以直接提供非查询生成器查询(XPath、JCR-SQL2)来解释查询。

有关如何使用QueryBuilder调试查询的下拉列表，请参阅以下视频。

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## 使用日志记录调试查询 {#debugging-queries-with-logging}

>[!NOTE]
>
>记录器的配置在部分中描述 [创建自己的记录器和作者](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers).

执行测试和调试中描述的查询时，查询生成器实施的日志输出（INFO级别）：

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

如果您有一个使用谓词计算器的查询，该计算器过滤或使用按比较器排序的自定义顺序，这也会在查询中记录：

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
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Facet |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | 分段（包含在Facet中） |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | 谓词求值器 |
| [com.day.cq.search.facets.extractors](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Facet提取器（用于评估器） |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | 适用于Querybuilder servlet的JSON结果点击编写器(/bin/querybuilder.json) |
