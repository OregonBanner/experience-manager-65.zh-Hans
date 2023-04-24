---
title: 慢速查询疑难解答
seo-title: Troubleshooting Slow Queries
description: 慢速查询疑难解答
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 0%

---

# 慢速查询疑难解答{#troubleshooting-slow-queries}

## 查询分类速度缓慢 {#slow-query-classifications}

AEM中慢速查询有三个主要分类，按严重性列出：

1. **无索引查询**

   * 查询 **not** 解析到索引并遍历JCR的内容以收集结果

1. **限制不当（或范围较广）的查询**

   * 解析为索引，但必须遍历所有索引条目以收集结果的查询

1. **大型结果集查询**

   * 返回大量结果的查询

前两个查询分类（无索引和限制较差）速度较慢。 测试速度缓慢，因为它们会强制Oak查询引擎检查每个 **潜在** 结果（内容节点或索引条目），用于标识属于 **实际** 结果集。

检查每个潜在结果的操作即称为“遍历”。

由于必须检查每个潜在结果，因此确定实际结果集的成本随电位结果的数量线性增加。

添加查询限制和调整索引允许索引数据以优化格式存储，提供快速的结果检索，并且减少或消除对潜在结果集的线性检查的需要。

在AEM 6.3中，默认情况下，当访问100,000时，查询失败并引发异常。 默认情况下，AEM 6.3之前的AEM版本中不存在此限制，但可以通过Apache Jackrabbit查询引擎设置OSGi配置和QueryEngineSettings JMX Bean（属性LimitReads）进行设置。

### 检测无索引查询 {#detecting-index-less-queries}

#### 开发期间 {#during-development}

解释 **全部** 查询，并确保其查询计划不包含 **/&amp;ast;横移** 解释。 遍历查询计划的示例：

* **计划：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署后 {#post-deployment}

* 监控 `error.log` 对于无索引遍历查询：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 仅当没有可用索引，并且查询可能遍历多个节点时，才会记录此消息。 如果索引可用，则不会记录消息，但遍历量较小，因此速度很快。

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [解释](/help/sites-administering/operations-dashboard.md#explain-query) 查找遍历或没有索引查询说明的查询速度缓慢。

### 检测受限性差的查询 {#detecting-poorly-restricted-queries}

#### 开发期间 {#during-development-1}

解释所有查询，并确保它们解析到调整为匹配查询属性限制的索引。

* 理想的查询计划范围 `indexRules` ，并且至少对于查询中最紧的属性限制。
* 对结果进行排序的查询应解析为Lucene属性索引，该索引具有按设置的属性排序的索引规则 `orderable=true.`

#### 例如，默认 `cqPageLucene` 没有的索引规则 `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

添加cq:tags索引规则之前

* **cq:tags索引规则**

   * 不存在即装即用

* **查询生成器查询**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **查询计划**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查询解析为 `cqPageLucene` 索引，但是由于没有属性索引规则 `jcr:content` 或 `cq:tags`，在评估此限制时， `cqPageLucene` 检查索引以确定匹配项。 如果指数包含100万， `cq:Page` 节点，然后检查100万条记录以确定结果集。

添加cq:tags索引规则后

* **cq:tags索引规则**

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

添加了 `jcr:content/cq:tags` 在 `cqPageLucene` 索引允许 `cq:tags` 以优化方式存储的数据。

当使用 `jcr:content/cq:tags` 限制，索引可以按值查找结果。 这意味着如果 `cq:Page` 节点 `myTagNamespace:myTag` 作为值，仅返回这100个结果，而其他99,000则从限制检查中排除，使性能提高了10,000倍。

更多查询限制会减少符合条件的结果集，并进一步优化查询优化。

同样，对于 `cq:tags` 属性，甚至包含 `cq:tags` 将性能不佳，因为索引的结果将返回所有全文匹配。 cq:tags的限制将在其后进行过滤。

索引后过滤的另一个原因是访问控制列表，在开发过程中经常会漏掉该列表。 尝试确保查询不返回用户可能无法访问的路径。 通过更好的内容结构以及对查询提供相关路径限制，可以执行此操作。

识别Lucene索引是否返回了许多结果以返回作为查询结果的小子集的有效方法是，为 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. 这样，您就可以查看从索引加载的文档数量。 最终结果的数量与加载文档的数量之间不应有过度差异。 有关更多信息，请参阅 [记录](/help/sites-deploying/configure-logging.md).

#### 部署后 {#post-deployment-1}

* 监控 `error.log` 对于遍历查询：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance) 操作控制台和 [解释](/help/sites-administering/operations-dashboard.md#explain-query) 查询查找查询计划时速度缓慢，无法将查询属性限制解析为索引属性规则。

### 检测大结果集查询 {#detecting-large-result-set-queries}

#### 开发期间 {#during-development-2}

为oak.queryLimitInMemory(例如10000)和oak.queryLimitReads（例如5000）设置低阈值，并在点击“查询读取的节点数多于x...”的UnsupportedOperationException时优化昂贵的查询

设置低阈值有助于避免资源密集型查询（即，不受任何索引的支持或受覆盖索引较少的支持）。 例如，一个读取100万个节点的查询将导致大量的IO，并对整个应用程序性能产生负面影响。 因此，任何因超出限制而失败的查询都应进行分析和优化。

#### 部署后 {#post-deployment-2}

* 监视日志中触发大节点遍历或大堆内存消耗的查询：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询，以减少已遍历的节点数。

* 监控日志以了解触发大堆内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询，以减少堆内存消耗。

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数调整节点遍历的阈值，以防止大型查询过载环境。 推荐的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述两个参数默认进行了预配置，并可通过OSGi QueryEngineSettings进行修改。

下方提供了更多信息： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查询性能优化 {#query-performance-tuning}

AEM中查询性能优化的基本思想是：

**“限制越多越好。”**

以下概述了为确保查询性能而建议的调整。 首先优化查询，使其更不显眼，然后根据需要优化索引定义。

### 调整查询语句 {#adjusting-the-query-statement}

AEM支持以下查询语言：

* 查询生成器
* JCR-SQL2
* XPath

以下示例使用查询生成器，因为查询生成器是AEM开发人员使用的最常用的查询语言，但JCR-SQL2和XPath也适用相同的原则。

1. 添加nodetype限制，以便查询解析为现有Lucene属性索引。

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

   缺少nodetype限制的查询强制AEM采用 `nt:base` nodetype(AEM中的每个节点都是的子类型)，有效地不产生nodetype限制。

   设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析为AEM cqPageLucene，将结果限制为节点的子集(仅 `cq:Page` 节点)。

1. 调整查询的nodetype限制，以便查询解析为现有Lucene属性索引。

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

   `nt:hierarchyNode` 是的父节点类型 `cq:Page`. 假设 `jcr:content/contentType=article-page` 仅应用于 `cq:Page` 节点，则此查询仅返回 `cq:Page` 节点所在位置 `jcr:content/contentType=article-page`. 但此流量是次优限制，因为：

   * 其他节点继承自 `nt:hierarchyNode` (例如， `dam:Asset`)会不必要地向潜在结果集添加。
   * 不存在AEM提供的索引 `nt:hierarchyNode`，但是，由于 `cq:Page`.
   设置 `type=cq:Page` 将此查询限制为仅 `cq:Page` 节点，并将查询解析为AEM cqPageLucene，从而将结果限制为AEM中的一个子集节点（仅cq:Page节点）。

1. 或者，调整属性限制，以便查询解析为现有的属性索引。

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

   将属性限制从 `jcr:content/contentType` （自定义值）到已知属性 `sling:resourceType` 允许查询解析到属性索引 `slingResourceType` 对所有内容进行索引的依据 `sling:resourceType`.

   当查询不能通过nodetype识别，并且结果集由单个属性限制主导时，最好使用属性索引（与Lucene属性索引相对）。

1. 向查询添加最紧的路径限制。 例如，首选 `/content/my-site/us/en` over `/content/my-site`或 `/content/dam` over `/`.

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

   将路径限制范围从 `path=/content`to `path=/content/my-site/us/en` 允许索引减少必须检查的索引条目数。 当查询能够很好地限制路径时，不仅仅 `/content` 或 `/content/dam`，请确保索引具有 `evaluatePathRestrictions=true`.

   注释使用 `evaluatePathRestrictions` 增加索引大小。

1. 尽可能避免查询函数和查询操作，例如： `LIKE` 和 `fn:XXXX` 因为其成本会随着限制结果的数量而增加。

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

   LIKE条件评估速度缓慢，因为如果文本以通配符(&quot;%。..&quot;)开头，则无法使用索引。 jcr:contains条件允许使用全文索引，因此首选使用该条件。 它要求解析的Lucene属性索引具有的indexRule `jcr:content/contentType` with `analayzed=true`.

   使用查询函数，如 `fn:lowercase(..)` 优化可能比较困难，因为没有更快的等效项（在更复杂和更突出的索引分析器配置之外）。 最好确定其他范围界定限制以改进整体查询性能，要求函数对尽可能小的潜在结果集进行操作。

1. ***此调整特定于查询生成器，不适用于JCR-SQL2或XPath。***

   使用 [查询生成器的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) 当结果的完整集 **not** 立即需要。

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
   如果查询执行速度快但结果数量大，则为p。 `guessTotal` 是查询生成器查询的关键优化。

   `p.guessTotal=100` 告知查询生成器仅收集前100个结果。 并且，要设置布尔标记，以指示是否存在至少一个结果（但不存在多少个结果，因为计数此数字会导致速度缓慢）。 这种优化优于分页或无限负载用例，在这些用例中，仅递增显示结果子集。

## 现有索引优化 {#existing-index-tuning}

1. 如果将最佳查询解析为属性索引，则无需执行任何操作，因为属性索引是最小可调的。
1. 否则，查询应解析为Lucene属性索引。 如果无法解析索引，请跳转到创建新索引。
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

1. 将XPath（或JCR-SQL2）提供给Oak索引定义生成器(位于 `https://oakutils.appspot.com/generate/index` 以便生成优化的Lucene属性索引定义。 <!-- The above URL is 404 as of April 24, 2023 -->

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

1. 以添加方式将生成的定义手动合并到现有Lucene属性索引中。 请注意，不要删除现有配置，因为它们可能用于满足其他查询。

   1. 找到包含cq:Page的现有Lucene属性索引（使用索引管理器）。 在这种情况下， `/oak:index/cqPageLucene`.
   1. 识别优化索引定义(步骤#4)与现有索引(/oak:index/cqPageLucene)之间的配置增量，并将优化索引中缺少的配置添加到现有索引定义中。
   1. 根据AEM重新索引最佳实践，根据现有内容是否可能受此索引配置更改的影响，按顺序进行刷新或重新索引。

## 创建新索引 {#create-a-new-index}

1. 验证查询未解析为现有Lucene属性索引。 如果有，请参阅上面有关调整和现有索引的部分。
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

1. 将XPath（或JCR-SQL2）提供给Oak索引定义生成器(位于 `https://oakutils.appspot.com/generate/index` 以便生成优化的Lucene属性索引定义。 <!-- The above URL is 404 as of April 24, 2023 -->

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

   将Oak索引定义生成器为新索引提供的XML定义添加到管理Oak索引定义的AEM项目中（记住，将Oak索引定义视为代码，因为代码取决于它们）。

   在常规的AEM软件开发生命周期后部署和测试新索引，并验证查询是否解析为该索引且查询性能良好。

   在初次部署此索引时，AEM会使用必需的数据填充索引。

## 无索引查询和遍历查询何时可以？ {#when-index-less-and-traversal-queries-are-ok}

由于AEM具有灵活的内容架构，因此很难预测并确保内容结构的遍历不会随着时间的推移而演变为大到无法接受的程度。

因此，确保索引满足查询，除非路径限制和节点类型限制的组合保证 **遍历的节点数少于20个。**

## 查询开发工具 {#query-development-tools}

### Adobe支持 {#adobe-supported}

* **查询生成器调试器**

   * 用于执行查询生成器查询并生成支持的XPath的WebUI（用于解释查询或Oak索引定义生成器）。
   * 在AEM上 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — 查询工具**

   * 用于执行XPath和JCR-SQL2查询的WebUI。
   * 在AEM上 [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查询……

* **[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)**

   * “AEM操作”功能板，为任何给定的XPATH或JCR-SQL2查询提供详细说明（查询计划、查询时间和结果数）。

* **[慢速/热门查询](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations功能板，其中列出了在AEM上执行的最近缓慢且热门的查询。

* **[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM操作WebUI，显示AEM实例上的索引；有助于了解哪些索引存在；可以定位或增强。

* **[记录](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查询生成器日志记录

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查询执行日志记录

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查询引擎设置OSGi配置**

   * 用于配置用于遍历查询的失败行为的OSGi配置。
   * 在AEM上 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用于估计AEM中内容树中的节点数。
   * 在AEM上 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 社区支持 {#community-supported}

* **位于的Oak索引定义生成器`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * 从XPath或JCR-SQL2查询语句生成最佳Lucence属性索引。

* **[AEM Chrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome Web浏览器扩展，可在浏览器的开发工具控制台中公开按请求发送的日志数据，包括已执行的查询及其查询计划。
   * 需要 [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) 以在AEM上安装和启用。
