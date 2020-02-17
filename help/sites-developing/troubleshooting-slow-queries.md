---
title: 慢速查询疑难解答
seo-title: 慢速查询疑难解答
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 慢速查询疑难解答{#troubleshooting-slow-queries}

## 查询分类缓慢 {#slow-query-classifications}

在AEM中，慢速查询有3个主要分类，按严重性列出：

1. **无索引查询**

   * 不解析 **到索引** ，并遍历JCR内容以收集结果的查询

1. **受限性不强（或限定范围）的查询**

   * 解析为索引但必须遍历所有索引条目以收集结果的查询

1. **大型结果集查询**

   * 返回大量结果的查询

前2个查询分类（无索引和受限性差）速度较慢，因为它们迫使Oak查询引擎检查每个潜在结果 **（内容节点或索引条目）以识别哪些属于实际** 结果集 **** 。

检查每个潜在结果的操作称为“遍历”。

由于必须检查每个电位结果，因此确定实际结果集的成本与电位结果的数量成线性增长。

添加查询限制和调整索引允许索引数据以提供快速结果检索的优化格式存储，并且减少或消除对潜在结果集的线性检查的需要。

在AEM 6.3中，默认情况下，当访问100,000时，查询将失败并引发异常。 此限制在AEM 6.3之前的AEM版本中默认不存在，但可通过Apache Jackrabbit查询引擎设置OSGi配置和QueryEngineSettings JMX Bean（属性LimitReads）设置。

### 检测无索引查询 {#detecting-index-less-queries}

#### 开发过程中 {#during-development}

解 **释所有** ，确保查询计划不包含 **/&amp;ast;遍历** 。 遍历查询计划的示例：

* **** 计划： `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署后 {#post-deployment}

* 监视无 `error.log` 索引遍历查询：

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 仅当没有可用索引且查询可能遍历许多节点时，才记录此消息。 如果某个索引可用，但遍历的量很小，因此速度很快，则不记录消息。

* 访问AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) Operations控制台和 [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slaw queryses查找遍历或没有索引查询说明。

### 检测受限性差的查询 {#detecting-poorly-restricted-queries}

#### 开发过程中 {#during-development-1}

解释所有查询，并确保它们解析为与查询的属性限制相匹配的索引。

* 理想的查询计划覆盖 `indexRules` 范围适用于所有属性限制，并且至少适用于查询中最严格的属性限制。
* 对结果排序的查询应解析为Lucene属性索引，该索引具有按设置的属性排序的索引规则 `orderable=true.`

#### 例如，默认的 `cqPageLucene``jcr:content/cq:tags` 索引规则不适用于 {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

添加cq:tags索引规则之前

* **cq:tags索引规则**

   * 现成不存在

* **Query Builder查询**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=my:tag
      ```

* **查询计划**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查询解析到索 `cqPageLucene` 引，但是由于不存在属性索引规则， `jcr:content` 或 `cq:tags``cqPageLucene` ，当评估此限制时，检查索引中的每个记录以确定匹配项。 这意味着如果索引包含100万个节 `cq:Page` 点，则检查100万个记录以确定结果集。

添加cq:tags索引规则后

* **cq:tags索引规则**

   * 
      ```
      /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
       @name=jcr:content/cq:tags
       @propertyIndex=true
      ```

* **Query Builder查询**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=myTagNamespace:myTag
      ```

* **查询计划**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

在索引中添加indexRule `jcr:content/cq:tags` 后， `cqPageLucene` 可 `cq:tags` 以优化方式存储数据。

当执行具有限制 `jcr:content/cq:tags` 的查询时，索引可以按值查找结果。 这意味着，如果100个节 `cq:Page``myTagNamespace:myTag` 点有一个值，则只返回这100个结果，而另外999,000个结果将从限制检查中排除，性能将提高10,000倍。

当然，进一步的查询限制会减少符合条件的结果集并进一步优化查询优化。

同样，如果没有属性的其他索引规则， `cq:tags``cq:tags` 即使具有限制的全文查询也会表现不佳，因为索引的结果将返回所有全文匹配项。 cq:tags的限制将在其后筛选。

索引后筛选的另一个原因是在开发过程中经常遗漏的访问控制列表。 尝试确保查询不返回用户可能无法访问的路径。 这通常可以通过更好的内容结构以及对查询提供相关路径限制来完成。

确定Lucene索引是否返回大量结果以返回很小的子集作为查询结果的一个有用方法是启用DEBUG日志并查看从索引中加载的文档数。 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` 最终结果的数量与加载文档的数量之间不应不成比例。 有关详细信息，请参 [阅记录](/help/sites-deploying/configure-logging.md)。

#### 部署后 {#post-deployment-1}

* 监控遍历 `error.log` 查询的情况：

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 访问AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations控制台和 [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries，查找查询计划（该计划不解析查询属性限制以索引属性规则）。

### 检测大结果集查询 {#detecting-large-result-set-queries}

#### 开发过程中 {#during-development-2}

为oak.queryLimitInMemory设置低阈值(例如 10000)和oak.queryLimitReads(例如 5000)，并在点击UnsupportedOperationException时优化昂贵的查询，该查询的读取次数超过x节点……。

这有助于避免资源密集型查询(即 不受任何索引的支持，也不受覆盖索引的支持)。 例如，读取1M个节点的查询将导致大量IO，并对应用程序的整体性能产生负面影响。 因此，任何因超出限制而失败的查询都应进行分析和优化。

#### 部署后 {#post-deployment-2}

* 监视日志以查找触发大节点遍历或大堆内存消耗的查询：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少经过的节点数

* 监视日志以查找触发大堆内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少堆内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数调整节点遍历的阈值，以防止大型查询过载环境。 建议的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2个参数默认预配置，并可通过OSGi queryEngineSettings进行修改。

更多信息，请访问： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查询性能调整 {#query-performance-tuning}

AEM中查询性能优化的口号是：

**“限制越多越好。”**

以下概述了为确保查询性能而推荐的调整。 首先调整查询，这是一个不那么显眼的活动，然后根据需要调整索引定义。

### 调整查询语句 {#adjusting-the-query-statement}

AEM支持以下查询语言：

* 查询生成器
* JCR-SQL2
* XPath

以下示例使用Query Builder作为AEM开发人员使用的最常见的查询语言，但同样的原则适用于JCR-SQL2和XPath。

1. 添加nodetype限制，以便查询解析到现有Lucene属性索引。

   * **未优化查询**

      * 
         ```
          property=jcr:content/contentType
          property.value=article-page
         ```
   * **优化查询**

      * 
         ```
          type=cq:Page
          property=jcr:content/contentType
          property.value=article-page
         ```
   缺少nodetype限制的查询强制AEM采用nodetype，而 `nt:base` AEM中的每个节点都是nodetype的子类型，这有效地导致了nodetype限制。

   设置 `type=cq:Page` 将此查询限制为仅节点 `cq:Page` ，并将查询解析为AEM的cqPageLucene，将结果限制为AEM中节点的子集(仅 `cq:Page` 节点)。

1. 调整查询的nodetype限制，使查询解析为现有的Lucene属性索引。

   * **未优化查询**

      * 
         ```
         type=nt:hierarchyNode
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **优化查询**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.value=article-page
         ```
   `nt:hierarchyNode` 是的父节点类 `cq:Page`型，并且假定仅 `jcr:content/contentType=article-page` 通过我们的自定义应 `cq:Page` 用程序应用于节点，则此查询将只返回 `cq:Page` 其中的节点 `jcr:content/contentType=article-page`。 但这是次优的限制，因为：

   * 其他节点继承 `nt:hierarchyNode` 自(例如 `dam:Asset`)不必要地添加到一组潜在结果中。
   * 不存在AEM提供的索引， `nt:hierarchyNode`但是，由于提供了索引 `cq:Page`。
   设置 `type=cq:Page``cq:Page` 将此查询限制为仅节点，并将查询解析为AEM的cqPageLucene，从而将结果限制为AEM中节点的子集（仅cq:Page节点）。

1. 或者，调整属性限制，使查询解析为现有的属性索引。

   * **未优化查询**

      * 
         ```
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **优化查询**

      * 
         ```
         property=jcr:content/sling:resourceType
         property.value=my-site/components/structure/article-page
         ```
   将属性限制从 `jcr:content/contentType` （自定义值）更改为已知属性 `sling:resourceType` 允许查询解析为属性索引，该属性索引按此索 `slingResourceType` 引索引所有内容 `sling:resourceType`。

   当查询不通过nodetype识别，而单个属性限制主导结果集时，最好使用属性索引（与Lucene属性索引相对）。

1. 为查询添加最紧密的路径限制。 例如，优先 `/content/my-site/us/en` 于 `/content/my-site`或 `/content/dam` 优先 `/`。

   * **未优化查询**

      * 
         ```
         type=cq:Page
         path=/content
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **优化查询**

      * 
         ```
         type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         ```
   将路径限制范围 `path=/content`从 `path=/content/my-site/us/en` 到允许索引减少需要检查的索引条目数。 当查询能够很好地限制路径时，除了或之外， `/content` 确 `/content/dam`保索引具有 `evaluatePathRestrictions=true`。

   注意，使 `evaluatePathRestrictions` 用会增加索引大小。

1. 尽可能避免查询函数／操作查询：随 `LIKE` 着成 `fn:XXXX` 本的增长，基于限制的结果也会增加。

   * **未优化查询**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.operation=like
         property.value=%article%
         ```
   * **优化查询**

      * 
         ```
         type=cq:Page
         fulltext=article
         fulltext.relPath=jcr:content/contentType
         ```
   LIKE条件的计算速度很慢，因为如果文本以通配符(&quot;%。..&quot;)开头，则无法使用索引。 jcr:contains条件允许使用全文索引，因此是首选条件。 这要求已解析的Lucene属性索引具有的indexRule `jcr:content/contentType` 与 `analayzed=true`。

   使用查询函数(如 `fn:lowercase(..)` 查询函数)可能较难优化，因为没有更快的等效函数（在更复杂、更显眼的索引分析器配置之外）。 最好确定其他范围界定限制以改进整体查询性能，要求函数对尽可能小的潜在结果集进行操作。

1. ***此调整特定于Query Builder，不适用于JCR-SQL2或XPath。***

   当完 [整的结果集是](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) **不是立即需要的**时，请使用Query Builder的guessTotal。

   * **未优化查询**

      * 
         ```
         type=cq:Page
         path=/content
         ```
   * **优化查询**

      * 
         ```
         type=cq:Page
         path=/content
         p.guessTotal=100
         ```
   对于查询执行速度快但结果数量大的情况，p.是Query builder查询的 `guessTotal` 关键优化。

   `p.guessTotal=100` 告知Query builder仅收集前100个结果，并设置一个布尔标志，指示是否存在至少一个结果（但不存在多少个结果），因为计算此数字将导致运行缓慢。 这种优化在分页或无限加载使用情况方面表现出色，在这些情况下，只有一部分结果以增量方式显示。

## 现有索引调整 {#existing-index-tuning}

1. 如果最佳查询解析为属性索引，则无需再做任何操作，因为属性索引是最小限度的可调整的。
1. 否则，查询应解析为Lucene属性索引。 如果无法解析索引，请跳到创建新索引。
1. 根据需要，将查询转换为XPath或JCR-SQL2。

   * **Query Builder查询**

      * 
         ```
         query type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         orderby=@jcr:content/publishDate
         orderby.sort=desc
         ```
   * **从Query builder查询生成的XPath**

      * 
         ```
         /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
         ```


1. 将XPath（或JCR-SQL2）提供给 [Oak索引定义生成器](https://oakutils.appspot.com/generate/index) ，以生成优化的Lucene属性索引定义。

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

   1. 找到涵盖cq:Page的现有Lucene属性索引（使用索引管理器）。 在这个例子中， `/oak:index/cqPageLucene`.
   1. 确定优化索引定义（第4步）与现有索引(/oak:index/cqPageLucene)之间的配置增量，并将优化索引中缺少的配置添加到现有索引定义中。
   1. 根据AEM的重新索引最佳实践，根据现有内容是否会受此索引配置更改的影响而进行刷新或重新索引。

## 创建新索引 {#create-a-new-index}

1. 验证查询未解析为现有Lucene属性索引。 如果确实如此，请参阅上节介绍调整和现有索引。
1. 根据需要，将查询转换为XPath或JCR-SQL2。

   * **Query Builder查询**

      * 
         ```
         type=myApp:Author
         property=firstName
         property.value=ira
         ```
   * **从Query builder查询生成的XPath**

      * 
         ```
         //element(*, myApp:Page)[@firstName = 'ira']
         ```


1. 将XPath（或JCR-SQL2）提供给 [Oak索引定义生成器](https://oakutils.appspot.com/generate/index) ，以生成优化的Lucene属性索引定义。

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

   将Oak Index Definition Generator为新索引提供的XML定义添加到管理Oak索引定义的AEM项目（记住，将Oak索引定义视为代码，因为代码取决于它们）。

   在AEM软件开发的常规生命周期后部署和测试新索引，并验证该查询解析到索引且该查询是否有效。

   在初始部署此索引后，AEM将使用必需的数据填充索引。

## 无索引和遍历查询何时可以？ {#when-index-less-and-traversal-queries-are-ok}

由于AEM的灵活内容架构，很难预测和确保内容结构的遍历不会随着时间推移而演变为无法接受的大。

因此，确保索引满足查询，除非路径限制和节点类型限制的组合保证 **了少于20个节点被遍历。**

## 查询开发工具 {#query-development-tools}

### Adobe支持 {#adobe-supported}

* **Query builder调试器**

   * 用于执行Query builder查询并生成支持XPath的WebUI（用于Explain Query或Oak Index Definition Generator）。
   * 位于AEM上，网址为 [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite —— 查询工具**

   * 用于执行XPath和JCR-SQL2查询的WebUI。
   * 位于AEM上，网址 [为/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查询……

* **[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)**

   * AEM Operations控制面板，提供任何给定XPATH或JCR-SQL2查询的详细说明（查询计划、查询时间和结果数）。

* **[慢速／常用查询](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM Operations功能板列出了在AEM上执行的近期缓慢且受欢迎的查询。

* **[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 显示AEM实例上的索引的AEM Operations webUI;有助于了解哪些索引已经存在，可以定位或增强。

* **[记录](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query builder日志记录

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查询执行日志记录

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查询引擎设置OSGi配置**

   * 配置用于遍历查询的失败行为的OSGi配置。
   * 位于AEM的 [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用于估计AEM中内容树中的节点数。
   * 位于AEM的 [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 社区支持 {#community-supported}

* **[Oak Index Definition Generator](https://oakutils.appspot.com/generate/index)**

   * 从XPath或JCR-SQL2查询语句生成最佳Lucence属性索引。

* **[AEM Chrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome web浏览器扩展，可在浏览器的开发工具控制台中显示每个请求的日志数据，包括执行的查询及其查询计划。
   * 需要 [在AEM上安装和启用](https://sling.apache.org/downloads.cgi) Sling Log Tracer 1.0.2+。

