---
title: 排查查询速度缓慢的问题
seo-title: Troubleshooting Slow Queries
description: 排查查询速度缓慢的问题
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 0%

---

# 排查查询速度缓慢的问题{#troubleshooting-slow-queries}

## 查询分类速度慢 {#slow-query-classifications}

AEM中有三种主要的慢查询分类，按严重性列出：

1. **无索引查询**

   * 执行此类操作的查询 **非** 解析为索引并遍历JCR的内容以收集结果

1. **限制不当（或范围有限）的查询**

   * 解析为索引，但必须遍历所有索引项以收集结果的查询

1. **大型结果集查询**

   * 返回大量结果的查询

查询的前2个分类（无索引和限制较差）速度较慢，因为它们强制Oak查询引擎检查每个分类 **潜在** 要标识属于以下类别的结果（内容节点或索引项）： **实际** 结果集。

检查每个潜在结果的行为称为遍历。

由于必须检查每个潜在结果，所以确定实际结果集的成本与潜在结果数是线性增长的。

添加查询限制和调整索引允许以最佳格式存储索引数据，以便快速检索结果，并且减少或消除对潜在结果集的线性检查的需要。

在AEM 6.3中，默认情况下，当达到100,000的遍历时，查询失败并引发异常。 默认情况下，在AEM 6.3之前的AEM版本中不存在此限制，但可通过Apache Jackrabbit查询引擎设置OSGi配置和QueryEngineSettings JMX bean（属性LimitReads）进行设置。

### 检测无索引查询 {#detecting-index-less-queries}

#### 开发期间 {#during-development}

说明 **所有** 查询并确保其查询计划不包含 **/&amp;ast；遍历** 解释一下。 遍历查询计划示例：

* **计划：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署后 {#post-deployment}

* 监控 `error.log` 对于无索引遍历查询：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 仅当没有可用的索引并且查询可能遍历许多节点时，才会记录此消息。 如果索引可用，则不会记录消息，但遍历的量较小，因此速度较快。

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [说明](/help/sites-administering/operations-dashboard.md#explain-query) 查询速度慢，需要遍历或没有索引查询说明。

### 检测限制较差的查询 {#detecting-poorly-restricted-queries}

#### 开发期间 {#during-development-1}

解释所有查询并确保它们解析为调整索引以匹配查询的属性限制。

* 理想的查询计划覆盖范围具有 `indexRules` 用于所有属性限制，并且至少具有查询中最严格的属性限制。
* 对结果进行排序的查询应解析为Lucene属性索引，其中具有按设置的属性进行排序的索引规则 `orderable=true.`

#### 例如，缺省值 `cqPageLucene` 没有索引规则 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

添加cq：tags索引规则之前

* **cq：tags索引规则**

   * 不存在开箱即用的

* **查询生成器查询**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **查询计划**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查询解析为 `cqPageLucene` 索引，但因为不存在属性索引规则 `jcr:content` 或 `cq:tags`，当评估此限制时，中 `cqPageLucene` 检查索引以确定匹配项。 这意味着如果索引包含100万 `cq:Page` 然后检查100万条记录以确定结果集。

添加cq：tags索引规则后

* **cq：tags索引规则**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **查询生成器查询**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **查询计划**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

添加的indexRule `jcr:content/cq:tags` 在 `cqPageLucene` 索引允许 `cq:tags` 以优化方式存储的数据。

当查询使用 `jcr:content/cq:tags` 执行限制，索引可以按值查找结果。 这意味着，如果100 `cq:Page` 节点具有 `myTagNamespace:myTag` 作为一个值，仅返回这100个结果，而其他999,000个结果则被排除在限制检查之外，使性能提高了10,000倍。

当然，进一步的查询限制会减少符合条件的结果集，并进一步优化查询优化。

同样，无需为添加额外的索引规则 `cq:tags` 属性，甚至是对具有限制的全文查询 `cq:tags` 将性能不佳，因为索引中的结果将返回所有全文匹配。 对cq：tags的限制将在它之后被过滤。

索引后过滤的另一个原因是访问控制列表，在开发过程中经常会遗漏。 请尝试确保查询未返回用户可能无法访问的路径。 这通常可以通过更好的内容结构以及对查询提供相关的路径限制来实现。

要识别Lucene索引是否返回了大量结果以返回非常小的子集作为查询结果，一种有用的方法是启用DEBUG日志 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` 并查看从索引加载了多少文档。 最终结果数量与加载的文档数量不应不成比例。 有关更多信息，请参阅 [日志记录](/help/sites-deploying/configure-logging.md).

#### 部署后 {#post-deployment-1}

* 监控 `error.log` 对于遍历查询：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [说明](/help/sites-administering/operations-dashboard.md#explain-query) 查询速度较慢，需要查询计划时无法解决查询属性限制问题，因而无法索引属性规则。

### 检测大型结果集查询 {#detecting-large-result-set-queries}

#### 开发期间 {#during-development-2}

为oak.queryLimitInMemory设置低阈值(例如 10000)和oak.queryLimitReads(例如 5000)并优化在点击UnsupportedOperationException时开销巨大的查询，该异常显示“查询读取了超过x个节点……”

这有助于避免资源密集型查询(即 不受任何索引支持，或受覆盖范围较小的索引支持)。 例如，读取1M节点的查询会导致大量IO，并对应用程序的整体性能产生负面影响。 因此，任何由于上述限制而失败的查询都应该进行分析和优化。

#### 部署后 {#post-deployment-2}

* 监测日志中触发大型节点遍历或大型栈内存消耗的查询： ”

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少遍历的节点数

* 监测日志中触发大型栈内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少栈内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数调整节点遍历的阈值，以防止大型查询使环境过载。 推荐值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，默认预配置上述2个参数，并且可以通过OSGi QueryEngineSettings修改它们。

有关详情，请参阅： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查询性能优化 {#query-performance-tuning}

AEM中查询性能优化的座右铭是：

**“限制越多，越好。”**

下面概述了为确保查询性能而建议的调整。 首先调整查询，这是一项不太引人注目的活动，然后如果需要，调整索引定义。

### 调整查询语句 {#adjusting-the-query-statement}

AEM支持以下查询语言：

* 查询生成器
* JCR-SQL2
* XPath

以下示例使用Query Builder，它是AEM开发人员使用的最常见查询语言，但相同的原则适用于JCR-SQL2和XPath。

1. 添加节点类型限制，以便查询解析为现有的Lucene属性索引。

* **未优化查询**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   缺少节点类型限制的查询强制AEM假设 `nt:base` nodetype，AEM中的每个节点都是其子类型，这实际上不会导致任何节点类型限制。

   设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析为AEM cqPageLucene，将结果限制为节点的子集(仅限 `cq:Page` AEM节点)。

1. 调整查询的节点类型限制，使查询解析为现有的Lucene属性索引。

* **未优化查询**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` 是父节点类型 `cq:Page`，并假定 `jcr:content/contentType=article-page` 仅应用于 `cq:Page` 节点，此查询将仅返回 `cq:Page` 节点位置 `jcr:content/contentType=article-page`. 不过，这是一种次优的限制，因为：

   * 其他节点继承自 `nt:hierarchyNode` (例如： `dam:Asset`)将不必要地添加到潜在结果集。
   * 不存在AEM提供的索引 `nt:hierarchyNode`，但是，由于为 `cq:Page`.
   设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析为AEM cqPageLucene，将结果限制为AEM中的节点子集（仅限cq：Page节点）。

1. 或者，调整属性限制，使查询解析为现有的属性索引。

* **未优化查询**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化查询**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   更改属性限制 `jcr:content/contentType` （自定义值）到已知属性 `sling:resourceType` 允许查询解析为属性索引 `slingResourceType` 用于索引所有内容 `sling:resourceType`.

   当查询未按节点类型识别，并且单个属性限制主导结果集时，最好使用属性索引（与Lucene属性索引相对）。

1. 向查询添加尽可能严格的路径限制。 例如，首选 `/content/my-site/us/en` 超过 `/content/my-site`，或 `/content/dam` 超过 `/`.

* **未优化查询**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化查询**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   从以下位置设定路径限制的范围 `path=/content`到 `path=/content/my-site/us/en` 允许索引减少需要检查的索引项数。 当查询可以很好地限制路径时，不仅仅是 `/content` 或 `/content/dam`，确保索引具有 `evaluatePathRestrictions=true`.

   使用注释 `evaluatePathRestrictions` 会增加索引大小。

1. 如果可能，请避免查询函数/操作，例如： `LIKE` 和 `fn:XXXX` 成本会随着基于限制的结果数量而扩展。

* **未优化查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **优化查询**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   LIKE条件的计算速度较慢，因为如果文本以通配符(“%。..”)开头，则无法使用索引。 jcr：contains条件允许使用全文索引，因此是首选。 这需要解析的Lucene属性索引具有indexRule `jcr:content/contentType` 替换为 `analayzed=true`.

   使用查询函数，如 `fn:lowercase(..)` 由于没有速度更快的对等项（在更复杂和侵入性更强的索引分析器配置之外），可能更难以优化。 最好找出其他范围限制来提高整体查询性能，要求函数对可能的最小结果集进行操作。

1. ***此调整特定于查询生成器，不适用于JCR-SQL2或XPath。***

   使用 [查询生成器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 当整组结果为 **非** 立即需要。

   * **未优化查询**

      ```js
      type=cq:Page
      path=/content
      ```

   * **优化查询**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   对于查询执行速度较快但结果数量较大的情况，p。 `guessTotal` 是Query Builder查询的关键优化。

   `p.guessTotal=100` 告知Query Builder仅收集前100个结果，并设置一个布尔标志，指示是否至少存在一个其他结果（但不指示还有多少个结果，因为计数此数字将导致速度变慢）。 此优化不适用于分页或无限加载用例，在这些用例中，仅以增量方式显示部分结果。

## 现有索引调整 {#existing-index-tuning}

1. 如果最佳查询解析为属性索引，则由于属性索引最低可调整，因此没有其他可执行的操作。
1. 否则，查询应解析为Lucene属性索引。 如果无法解析任何索引，请跳转到创建新索引。
1. 根据需要，将查询转换为XPath或JCR-SQL2。

   * **查询生成器查询**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **从Query Builder查询生成的XPath**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. 将XPath（或JCR-SQL2）提供给 [Oak索引定义生成器](https://oakutils.appspot.com/generate/index) 以生成优化的Lucene属性索引定义。

   **生成的Lucene属性索引定义**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. 以累加方式手动将生成的定义合并到现有Lucene属性索引中。 请注意不要删除现有配置，因为它们可能用于满足其他查询。

   1. 找到涵盖cq：Page的现有Lucene属性索引（使用索引管理器）。 在这个案例中， `/oak:index/cqPageLucene`.
   1. 识别优化索引定义(步骤#4)和现有索引(/oak：index/cqPageLucene)之间的配置增量，并将优化索引中缺少的配置添加到现有索引定义中。
   1. 根据AEM重新索引最佳实践，刷新或重新索引将按顺序进行，具体取决于此索引配置更改是否会影响现有内容。

## 创建新索引 {#create-a-new-index}

1. 验证查询是否未解析为现有Lucene属性索引。 如果是这样，请参阅上面关于优化和现有索引的部分。
1. 根据需要，将查询转换为XPath或JCR-SQL2。

   * **查询生成器查询**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **从Query Builder查询生成的XPath**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. 将XPath（或JCR-SQL2）提供给 [Oak索引定义生成器](https://oakutils.appspot.com/generate/index) 以生成优化的Lucene属性索引定义。

   **生成的Lucene属性索引定义**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. 部署生成的Lucene属性索引定义。

   将Oak索引定义生成器为新索引提供的XML定义添加到管理Oak索引定义的AEM项目中（请记住，将Oak索引定义视为代码，因为代码依赖于它们）。

   在通常的AEM软件开发生命周期内部署和测试新索引，并验证查询解析到该索引以及查询的性能。

   初始部署此索引后，AEM将使用所需数据填充该索引。

## 无索引查询和遍历查询何时正常？ {#when-index-less-and-traversal-queries-are-ok}

由于AEM灵活的内容体系结构，很难预测和确保内容结构的遍历不会随着时间的推移而演变为不可接受的庞大。

因此，确保索引满足查询，除非路径限制和节点类型限制的组合确保 **遍历的节点少于20个。**

## 查询开发工具 {#query-development-tools}

### 支持的Adobe {#adobe-supported}

* **Query Builder调试器**

   * 用于执行Query Builder查询并生成支持的XPath的WebUI（用于Explain Query或Oak索引定义生成器）。
   * 位于AEM上的 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查询工具**

   * 用于执行XPath和JCR-SQL2查询的WebUI。
   * 位于AEM上的 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查询……

* **[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Operations功能板，为任何给定的XPATH或JCR-SQL2查询提供详细说明（查询计划、查询时间和结果数）。

* **[慢速/常见查询](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations功能板，其中列出最近在AEM上执行的缓慢且受欢迎的查询。

* **[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 显示AEM实例上索引的AEM Operations WebUI；有助于了解哪些索引已经存在、可以定位或扩充。

* **[记录](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查询生成器日志记录

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查询执行日志记录

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查询引擎设置OSGi配置**

   * 用于配置遍历查询的失败行为的OSGi配置。
   * 位于AEM上的 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用于估算AEM内容树中的节点数。
   * 位于AEM上的 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 支持的社区 {#community-supported}

* **[Oak索引定义生成器](https://oakutils.appspot.com/generate/index)**

   * 从XPath或JCR-SQL2查询语句生成最佳Lucence属性索引。

* **[AEM Chrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome Web浏览器扩展，在浏览器的开发工具控制台中公开每个请求的日志数据，包括已执行的查询及其查询计划。
   * 需要 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 在AEM上安装和启用。
