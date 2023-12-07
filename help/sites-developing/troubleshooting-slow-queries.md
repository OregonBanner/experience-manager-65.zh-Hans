---
title: 排查查询速度较慢的问题
description: 了解如何对Adobe Experience Manager中的缓慢查询进行故障排除。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 0%

---

# 排查查询速度较慢的问题{#troubleshooting-slow-queries}

## 查询分类速度慢 {#slow-query-classifications}

AEM中有三种主要的慢查询分类，按严重性列出：

1. **无索引查询**

   * 执行此类操作的查询 **非** 解析为索引并遍历JCR的内容以收集结果

1. **限制不当（或范围有限）的查询**

   * 解析为索引，但必须遍历所有索引项以收集结果的查询

1. **大型结果集查询**

   * 返回大量结果的查询

查询的前两个分类（无索引和限制较差）较慢。 速度较慢，因为它们强制Oak查询引擎检查每个 **潜在** 要标识属于以下项的结果（内容节点或索引项）： **实际** 结果集。

检查每个潜在结果的行为称为遍历。

由于必须检验每个潜在结果，所以确定实际结果集的成本与潜在结果的数目成线性增长。

添加查询限制和调整索引允许以优化的格式存储索引数据，以便快速检索结果，并且减少或消除了对潜在结果集的线性检查的需要。

在AEM 6.3中，默认情况下，当达到100,000的遍历时，查询失败并引发异常。 默认情况下，在AEM 6.3之前的AEM版本中不存在此限制，但可通过Apache Jackrabbit查询引擎设置OSGi配置和QueryEngineSettings JMX bean（属性LimitReads）进行设置。

### 检测无索引查询 {#detecting-index-less-queries}

#### 开发期间 {#during-development}

说明 **所有** 查询并确保其查询计划不包含 **/&amp;ast；遍历** 解释一下。 遍历查询计划的示例：

* **计划：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署后 {#post-deployment}

* 监控 `error.log` 对于无索引遍历查询：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 仅当没有索引可用并且查询可能遍历多个节点时，才会记录此消息。 如果索引可用，则不会记录消息，但遍历的次数较少，因此速度较快。

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [说明](/help/sites-administering/operations-dashboard.md#explain-query) 查询速度较慢，需要遍历或没有索引查询说明。

### 检测限制较差的查询 {#detecting-poorly-restricted-queries}

#### 开发期间 {#during-development-1}

解释所有查询并确保它们解析为调整后的索引，以匹配查询的属性限制。

* 理想的查询计划覆盖范围具有 `indexRules` 适用于所有属性限制，并且至少适用于查询中最严格的属性限制。
* 对结果进行排序的查询应解析为Lucene属性索引，其中具有用于按设置的属性进行排序的索引规则 `orderable=true.`

#### 例如，缺省值 `cqPageLucene` 没有索引规则 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

添加cq：tags索引规则之前

* **cq：tags索引规则**

   * 不存在开箱即用型

* **查询生成器查询**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **查询计划**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查询解析为 `cqPageLucene` 索引，但因为不存在属性索引规则 `jcr:content` 或 `cq:tags`，当评估此限制时，中 `cqPageLucene` 检查索引以确定匹配项。 因此，如果该指数包含100万 `cq:Page` 然后，检查100万条记录以确定结果集。

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

添加的indexRule `jcr:content/cq:tags` 在 `cqPageLucene` 索引允许 `cq:tags` 要以优化方式存储的数据。

当查询使用 `jcr:content/cq:tags` 执行限制，索引可以按值查找结果。 这意味着，如果 `cq:Page` 节点具有 `myTagNamespace:myTag` 作为一个值，仅返回这100个结果，另外999,000个结果被排除在限制检查之外，性能提高了10,000倍。

更多的查询限制会减少符合条件的结果集，并进一步优化查询优化。

同样，无需为添加额外的索引规则 `cq:tags` 属性，甚至是对具有限制的全文查询 `cq:tags` 将性能不佳，因为索引中的结果将返回所有全文匹配。 对cq：tags的限制将过滤掉。

索引后过滤的另一个原因是访问控制列表，在开发过程中经常会错过。 请尝试确保查询未返回用户可能无法访问的路径。 可以通过更好的内容结构以及对查询提供相关的路径限制来实现这一点。

要识别Lucene索引是否返回了大量结果以返回一个小子集作为查询结果，一种有效的方法是启用调试日志 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. 这样，您就可以查看从索引加载了多少文档。 最终结果数量与加载的文档数量不应不成比例。 有关更多信息，请参阅 [记录](/help/sites-deploying/configure-logging.md).

#### 部署后 {#post-deployment-1}

* 监控 `error.log` 对于遍历查询：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [说明](/help/sites-administering/operations-dashboard.md#explain-query) 查询速度较慢，查找查询计划时无法解决查询属性限制以索引属性规则。

### 检测大型结果集查询 {#detecting-large-result-set-queries}

#### 开发期间 {#during-development-2}

为oak.queryLimitInMemory(例如10000)和oak.queryLimitReads（例如5000）设置低阈值，并在遇到UnsupportedOperationException时优化开销巨大的查询，该异常为“查询读取了超过x个节点……”

设置低阈值有助于避免资源密集型查询（即，不受任何索引支持或受覆盖范围较少的索引支持）。 例如，读取100万个节点的查询会导致大量IO，并对应用程序的整体性能产生负面影响。 因此，任何由于上述限制而失败的查询都应该进行分析和优化。

#### 部署后 {#post-deployment-2}

* 监测日志中触发大型节点遍历或大型栈内存消耗的查询： &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询，以减少遍历的节点数。

* 监视日志中触发大型栈内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少栈内存消耗。

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数来调整节点遍历阈值，以防止大型查询使环境过载。 推荐值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述两个参数默认已预配置，可以通过OSGi QueryEngineSettings进行修改。

下提供了更多信息： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查询性能优化 {#query-performance-tuning}

AEM中查询性能优化的座右铭是：

**“限制越多越好。”**

下面概述了为确保查询性能而建议进行的调整。 首先优化查询，这是一个不太引人入胜的活动，然后如果需要，优化索引定义。

### 调整查询语句 {#adjusting-the-query-statement}

AEM支持以下查询语言：

* 查询生成器
* JCR-SQL2
* XPath

以下示例使用Query Builder作为AEM开发人员最常用的查询语言，但相同的原则适用于JCR-SQL2和XPath。

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

  缺少节点类型限制的查询强制AEM假定 `nt:base` 节点类型，AEM中的每个节点都是其子类型，这实际上不会导致任何节点类型限制。

  设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析到AEM cqPageLucene，将结果限制为节点的子集(仅限 `cq:Page` AEM节点)。

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

  `nt:hierarchyNode` 是父节点类型 `cq:Page`. 假设 `jcr:content/contentType=article-page` 仅应用于 `cq:Page` 通过Adobe的自定义应用程序，此查询仅返回 `cq:Page` 节点位置 `jcr:content/contentType=article-page`. 但是，此流量是次优限制，因为：

   * 其他节点继承自 `nt:hierarchyNode` (例如， `dam:Asset`)向潜在结果集添加不必要的。
   * “ ”不存在AEM提供的索引 `nt:hierarchyNode`，但是，由于为提供了索引 `cq:Page`.

  设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析到AEM cqPageLucene，将结果限制为AEM中的节点子集（仅限cq：Page节点）。

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

  当查询无法按节点类型识别，并且单个属性限制主导结果集时，最好使用属性索引（与Lucene属性索引相反）。

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

  从以下位置设定路径限制的范围 `path=/content`到 `path=/content/my-site/us/en` 允许索引减少必须检查的索引项数。 当查询可以很好地限制路径时，不仅仅是 `/content` 或 `/content/dam`，确保索引具有 `evaluatePathRestrictions=true`.

  使用注释 `evaluatePathRestrictions` 增加索引大小。

1. 如果可能，请避免查询函数和查询操作，例如： `LIKE` 和 `fn:XXXX` 因为它们的成本会随着基于限制的结果的数量而增加。

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

  LIKE条件的计算速度较慢，因为如果文本以通配符(“%。..”)开头，则无法使用索引。 jcr：contains条件允许使用全文索引，因此是首选。 它需要解析的Lucene属性索引具有indexRule `jcr:content/contentType` 替换为 `analayzed=true`.

  使用查询函数，如 `fn:lowercase(..)` 如果没有速度更快的对等项（在更复杂且更棘手的索引分析器配置之外），优化可能更困难。 最好找出其他范围限制以提高整体查询性能，要求函数尽可能对最小集合的潜在结果进行操作。

1. ***此调整是查询生成器特定的，不适用于JCR-SQL2或XPath。***

   使用 [查询生成器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 当整个结果集为 **非** 立即需要。

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

   `p.guessTotal=100` 告知Query Builder仅收集前100个结果。 并且，设置一个布尔标志来指示是否至少还有一个结果（但不指示还有多少个结果，因为计数此数字会导致速度变慢）。 此优化优于分页或无限加载用例，在这些用例中，仅增量显示结果子集。

## 现有索引调整 {#existing-index-tuning}

1. 如果最佳查询解析为属性索引，则由于属性索引最低可微调，因此没有任何可执行的操作。
1. 否则，查询应解析为Lucene属性索引。 如果无法解析索引，请跳到创建索引。
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

   * **从查询生成器查询生成的XPath**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. 将XPath（或JCR-SQL2）提供给Oak索引定义生成器，位于 `https://oakutils.appspot.com/generate/index` 以便生成优化的Lucene属性索引定义。 <!-- The above URL is 404 as of April 24, 2023 -->

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

1. 以累加方式手动将生成的定义合并到现有Lucene属性索引中。 请注意不要删除现有配置，因为它们可用于满足其他查询。

   1. 找到覆盖cq：Page的现有Lucene属性索引（使用索引管理器）。 在本例中， `/oak:index/cqPageLucene`.
   1. 识别优化索引定义(步骤#4)和现有索引(/oak：index/cqPageLucene)之间的配置增量，并将优化索引中缺少的配置添加到现有索引定义中。
   1. 根据AEM重新索引最佳实践，刷新或重新索引将按顺序进行，具体取决于现有内容是否可能受此索引配置更改的影响。

## 创建新索引 {#create-a-new-index}

1. 验证查询是否未解析为现有的Lucene属性索引。 如果出现这种情况，请参阅上面关于优化和现有索引的部分。
1. 根据需要，将查询转换为XPath或JCR-SQL2。

   * **查询生成器查询**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **从查询生成器查询生成的XPath**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. 将XPath（或JCR-SQL2）提供给Oak索引定义生成器，位于 `https://oakutils.appspot.com/generate/index` 以便生成优化的Lucene属性索引定义。 <!-- The above URL is 404 as of April 24, 2023 -->

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

   将由Oak索引定义生成器为新索引提供的XML定义添加到管理Oak索引定义的AEM项目中（请记住，将Oak索引定义视为代码，因为代码依赖于它们）。

   在通常的AEM软件开发生命周期内部署和测试新索引，并验证查询是否解析为索引以及查询是否有效。

   初始部署此索引时，AEM会使用所需数据填充该索引。

## 无索引查询和遍历查询何时正常？ {#when-index-less-and-traversal-queries-are-ok}

由于AEM灵活的内容架构，很难预测并确保内容结构的遍历不随时间演变为不可接受的大规模。

因此，确保索引满足查询，除非路径限制和节点类型限制的组合保证 **遍历的节点少于20个。**

## 查询开发工具 {#query-development-tools}

### 支持的Adobe {#adobe-supported}

* **Query Builder调试器**

   * 用于执行Query Builder查询并生成支持的XPath的WebUI（用于Explain Query或Oak索引定义生成器）。
   * 在AEM上 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查询工具**

   * 用于执行XPath和JCR-SQL2查询的WebUI。
   * 在AEM上 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查询……

* **[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Operations功能板，为任何给定的XPATH或JCR-SQL2查询提供详细说明（查询计划、查询时间和结果数）。

* **[慢速/常见查询](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations功能板，其中列出了最近在AEM上执行的缓慢查询和常用查询。

* **[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 显示AEM实例上索引的AEM Operations WebUI；便于了解存在哪些索引；可以定位或增强。

* **[记录](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查询生成器日志记录

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Oak查询执行日志记录

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Apache Jackrabbit查询引擎设置OSGi配置**

   * 用于配置遍历查询的失败行为的OSGi配置。
   * 在AEM上 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用于估算AEM中内容树中的节点数。
   * 在AEM上 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 支持的社区 {#community-supported}

* **Oak索引定义生成器位于`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * 从XPath或JCR-SQL2查询语句生成最佳Lucence属性索引。

* **[AEM Chrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome Web浏览器扩展可以在浏览器的开发工具控制台中公开每个请求的日志数据，包括已执行的查询及其查询计划。
   * 需要 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 在AEM上安装和启用。
