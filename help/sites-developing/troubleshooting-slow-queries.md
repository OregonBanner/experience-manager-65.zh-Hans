---
title: 慢速查询疑难解答
seo-title: 慢速查询疑难解答
description: 慢速查询疑难解答
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 0%

---


# 对慢查询{#troubleshooting-slow-queries}进行疑难解答

## 慢速查询分类{#slow-query-classifications}

AEM中慢查询有3种主要分类，按严重性列出：

1. **无索引查询**

   * 执行&#x200B;**not**&#x200B;的查询解析为索引并遍历JCR的内容以收集结果

1. **限制不足（或范围不宽）的查询**

   * 查询解析为索引，但必须遍历所有索引条目以收集结果

1. **大结果集查询**

   * 返回大量结果的查询

前2个查询分类（无索引且限制不足）速度较慢，因为它们迫使Oak查询引擎检查每个&#x200B;**潜在**&#x200B;结果（内容节点或索引条目）以确定哪些属于&#x200B;**实际**&#x200B;结果集。

检查每个潜在结果的操作称为“遍历”。

由于必须检查每个潜在结果，因此确定实际结果集的成本与电势结果的数量成线性增长。

添加查询限制和调整索引允许以优化格式存储索引数据，提供快速结果检索，并且减少或消除对潜在结果集的线性检查的需要。

在AEM 6.3中，默认情况下，当访问100,000时，查询失败并引发异常。 默认情况下，AEM 6.3之前的AEM版本中不存在此限制，但可以通过Apache Jackrabbit查询引擎设置OSGi配置和QueryEngineSettings JMX bean（属性LimitReads）设置此限制。

### 检测无索引查询{#detecting-index-less-queries}

#### 开发过程{#during-development}

解释&#x200B;**所有**&#x200B;查询，并确保其查询计划不包含&#x200B;**/&amp;ast;traverse**&#x200B;说明。 遍历查询计划示例：

* **计划：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### 部署后{#post-deployment}

* 监视`error.log`的无索引遍历查询:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * 仅当没有可用索引且查询可能遍历许多节点时，才记录此消息。 如果某个索引可用，但遍历的量很小，因此速度很快，则不记录消息。

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance)操作控制台和[说明](/help/sites-administering/operations-dashboard.md#explain-query)查找遍历或没有索引查询说明的慢查询。

### 检测受限查询{#detecting-poorly-restricted-queries}

#### 开发过程{#during-development-1}

解释所有查询，确保它们解析为调整为与查询的属性限制相匹配的索引。

* 理想的查询计划涵盖所有属性限制的`indexRules`，对于查询中最紧的属性限制，至少包含。
* 对结果排序的查询应解析为具有按设置`orderable=true.`的属性排序的索引规则的Lucene属性索引

#### 例如，默认`cqPageLucene`没有`jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}的索引规则

添加cq:tags索引规则之前

* **cq:tags索引规则**

   * 不存在

* **查询 Builder查询**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **查询计划**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

此查询解析到`cqPageLucene`索引，但由于`jcr:content`或`cq:tags`不存在属性索引规则，因此，当评估此限制时，将检查`cqPageLucene`索引中的每个记录以确定匹配项。 这意味着，如果索引包含1百万个`cq:Page`节点，则检查1百万条记录以确定结果集。

添加cq:tags索引规则后

* **cq:tags索引规则**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **查询 Builder查询**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **查询计划**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

在`cqPageLucene`索引中添加`jcr:content/cq:tags`的indexRule允许以优化方式存储`cq:tags`数据。

当执行具有`jcr:content/cq:tags`限制的查询时，索引可以按值查找结果。 这意味着，如果100个`cq:Page`节点将`myTagNamespace:myTag`作为值，则只返回100个结果，而其他999,000则从限制检查中排除，性能提高10,000倍。

当然，进一步的查询限制会减少符合条件的结果集并进一步优化查询优化。

同样，如果没有`cq:tags`属性的额外索引规则，即使对`cq:tags`具有限制的全文查询也会表现不佳，因为索引的结果将返回所有全文匹配项。 cq:tags的限制将在其后过滤。

索引后过滤的另一个原因是访问控制列表，开发过程中经常会漏掉这些数据。 尝试确保查询不返回用户可能无法访问的路径。 这通常可以通过更好的内容结构以及对查询提供相关路径限制来实现。

一种有用的方法，用于确定Lucene索引是否返回大量结果以返回很小的子集作为查询结果，即为`org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`启用DEBUG日志，并查看从索引加载了多少个文档。 最终结果数与加载文档数之间不应不成比例。 有关详细信息，请参阅[日志记录](/help/sites-deploying/configure-logging.md)。

#### 部署后{#post-deployment-1}

* 监视`error.log`的遍历查询:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* 访问AEM [查询性能](/help/sites-administering/operations-dashboard.md#query-performance)操作控制台和[说明](/help/sites-administering/operations-dashboard.md#explain-query)查找不解决查询属性限制以索引属性规则的查询计划的慢速查询。

### 检测大结果集查询{#detecting-large-result-set-queries}

#### 开发过程{#during-development-2}

为oak.queryLimitInMemory设置低阈值(例如 10000)和oak.queryLimitReads(例如 5000)，并在点击UnsupportedOperationException时优化昂贵的查询，该UnsupportedOperationException说“查询读取的节点多于x节点……”

这有助于避免资源密集型查询(即 不受任何索引的支持，也不受覆盖索引的支持)。 例如，读取1M个节点的查询会导致大量IO，并会对应用程序的整体性能产生负面影响。 因此，任何因超限而失效的查询都应进行分析和优化。

#### 部署后{#post-deployment-2}

* 监视日志，以查看触发大节点遍历或大堆内存消耗的查询:&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少遍历的节点数

* 监视日志以查看触发大堆内存消耗的查询:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少堆内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM 开始脚本中的JVM参数调整节点遍历的阈值，以防止大型查询过载环境。 建议的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2个参数默认预配置，并可通过OSGi QueryEngineSettings进行修改。

下面提供了更多信息：[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 查询性能调整{#query-performance-tuning}

AEM中查询性能优化的口号是：

**“限制越多越好。”**

以下概述了为确保查询性能而建议的调整。 首先调整查询(一种不那么显眼的活动)，然后根据需要调整索引定义。

### 调整查询语句{#adjusting-the-query-statement}

AEM支持以下查询语言：

* 查询生成器
* JCR-SQL2
* XPath

以下示例使用查询 Builder作为AEM开发人员使用的最常见的查询语言，但JCR-SQL2和XPath同样适用这些原则。

1. 添加nodetype限制，以便查询解析为现有Lucene属性索引。

* **未优化查询**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化的查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   查询缺少nodetype限制力，AEM采用`nt:base` nodetype，而AEM中的每个节点都是其子类型，这有效地导致了nodetype限制。

   设置`type=cq:Page`将此查询限制为仅`cq:Page`节点，并将查询解析为AEM cqPageLucene，将结果限制为AEM中的一个节点子集（仅`cq:Page`节点）。

1. 调整查询的nodetype限制，使查询解析为现有的Lucene属性索引。

* **未优化查询**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化的查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` 是的父节点类 `cq:Page`型，并且假 `jcr:content/contentType=article-page` 定仅通过我们 `cq:Page` 的自定义应用程序应用 `cq:Page` 于节点，则此查询将只返回其中的 `jcr:content/contentType=article-page`节点。不过，这是一个次优的限制，因为：

   * 其他节点继承自`nt:hierarchyNode`(例如 `dam:Asset`)不必要地添加到潜在结果集。
   * `nt:hierarchyNode`不存在AEM提供的索引，但`cq:Page`提供了索引。
   设置`type=cq:Page`将此查询限制为仅`cq:Page`节点，并将查询解析为AEM cqPageLucene，将结果限制为AEM中的一个节点子集（仅cq:Page节点）。

1. 或者，调整属性限制，使查询解析为现有属性索引。

* **未优化查询**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化的查询**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   将属性限制从`jcr:content/contentType`（自定义值）更改为已知属性`sling:resourceType`使查询能够解析到属性索引`slingResourceType`，该属性索引按`sling:resourceType`对所有内容进行索引。

   当查询不通过nodetype识别，并且结果集由单个属性限制主导时，最好使用属性索引（与Lucene属性索引相对）。

1. 将最紧的路径限制添加到查询。 例如，优先`/content/my-site/us/en`，而非`/content/my-site`，或者`/content/dam`，而非`/`。

* **未优化查询**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **优化的查询**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   将路径限制范围从`path=/content`限定为`path=/content/my-site/us/en`允许索引减少需要检查的索引条目数。 当查询可以很好地限制路径时，除`/content`或`/content/dam`之外，请确保索引具有`evaluatePathRestrictions=true`。

   注意，使用`evaluatePathRestrictions`会增大索引大小。

1. 尽可能避免查询函数/操作超过：`LIKE`和`fn:XXXX`，因为费用随基于限制的结果数量而增加。

* **未优化查询**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **优化的查询**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   LIKE条件的计算速度很慢，因为如果文本开始带有通配符(“%。..”)，则不能使用索引。 jcr:contains条件允许使用全文索引，因此是首选。 这要求已解析的Lucene属性索引具有`analayzed=true`的`jcr:content/contentType`的indexRule。

   使用`fn:lowercase(..)`等查询函数可能更难优化，因为没有更快的等效值（在更复杂、更引人注目的索引分析器配置之外）。 最好确定其他范围限制以改进总体查询性能，要求这些函数在尽可能小的潜在结果集上操作。

1. ***此调整特定于查询 Builder，不适用于JCR-SQL2或XPath。***

   当需要&#x200B;**不**&#x200B;完整结果集时，使用[查询 Builder的guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

   * **未优化查询**

      ```js
      type=cq:Page
      path=/content
      ```

   * **优化的查询**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   如果查询执行速度快，但结果数量大，则为p。`guessTotal`是对查询 Builder查询的关键优化。

   `p.guessTotal=100` 指示查询 Builder仅收集前100个结果，并设置一个布尔标志，指示是否存在至少一个结果（但不存在多少结果），因为计算此数量会导致速度变慢。这种优化在分页或无限加载用例方面是卓越的，在这些用例中，只增量显示结果的子集。

## 现有索引调整{#existing-index-tuning}

1. 如果最佳查询解析为属性索引，则无需执行任何操作，因为属性索引是最小可调的。
1. 否则，查询应解析为Lucene属性索引。 如果无法解析索引，请跳到创建新索引。
1. 根据需要将查询转换为XPath或JCR-SQL2。

   * **查询 Builder查询**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath从查询 Builder查询生成**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. 将XPath（或JCR-SQL2）提供给[Oak索引定义生成器](https://oakutils.appspot.com/generate/index)以生成优化的Lucene属性索引定义。

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

1. 以添加方式将生成的定义手动合并到现有Lucene属性索引中。 请务必注意，不要删除现有配置，因为它们可能用于满足其他查询。

   1. 找到覆盖cq:Page的现有Lucene属性索引（使用索引管理器）。 在这种情况下，`/oak:index/cqPageLucene`。
   1. 确定优化索引定义(步骤#4)与现有索引(/oak:index/cqPageLucene)之间的配置增量，并将优化索引中缺失的配置添加到现有索引定义中。
   1. 根据AEM重新编制最佳做法的索引，根据现有内容是否受此索引配置更改的影响而进行刷新或重新编制索引。

## 创建新索引{#create-a-new-index}

1. 验证查询未解析为现有Lucene属性索引。 如果确实如此，请参阅上面有关调整和现有索引的部分。
1. 根据需要将查询转换为XPath或JCR-SQL2。

   * **查询 Builder查询**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath从查询 Builder查询生成**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. 将XPath（或JCR-SQL2）提供给[Oak索引定义生成器](https://oakutils.appspot.com/generate/index)以生成优化的Lucene属性索引定义。

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

   将Oak Index Definition Generator为新索引提供的XML定义添加到管理Oak索引定义的AEM项目（请记住，将Oak索引定义视为代码，因为代码取决于它们）。

   在通常的AEM软件开发生命周期后部署和测试新索引，并验证查询解析到索引且查询是否正常。

   在初始部署此索引时，AEM将使用必需数据填充索引。

## 无索引和遍历查询何时可以？{#when-index-less-and-traversal-queries-are-ok}

由于AEM的灵活内容架构，很难预测和确保内容结构的遍历不会随着时间的推移而演化为无法接受的大。

因此，确保索引满足查询，除非路径限制和节点类型限制的组合保证遍历&#x200B;**少于20个节点。**

## 查询开发工具{#query-development-tools}

### Adobe支持{#adobe-supported}

* **查询 Builder调试器**

   * 用于执行查询 Builder查询并生成支持XPath的WebUI(用于“解释查询”或Oak Index Definition Generator)。
   * 位于AEM上[/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite-查询工具**

   * 用于执行XPath和JCR-SQL2查询的WebUI。
   * 位于AEM上，地址为[/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) >工具>查询...

* **[说明查询](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 一个AEM操作仪表板，它为任何给定的XPATH或JCR-SQL2查询提供详细说明(查询计划、查询时间和结果数)。

* **[慢速/常用查询](/help/sites-administering/operations-dashboard.md#query-performance)**

   * 一个AEM操作仪表板，列出在AEM上执行的最近缓慢且受欢迎的查询。

* **[索引管理器](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * 显示AEM实例上的索引的AEM Operations WebUI;有助于了解哪些索引已经存在，可以定位或增强。

* **[记录](/help/sites-administering/operations-dashboard.md#log-messages)**

   * 查询 Builder日志记录

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak查询执行日志

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit查询引擎设置OSGi配置**

   * 配置用于检查查询的失败行为的OSGi配置。
   * 位于AEM上，地址为[/system/console/configMgr#org.apache.jackrabbit.oak.查询.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * JMX MBean用于估计AEM中内容树中的节点数。
   * 位于AEM上[/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### 支持的社区{#community-supported}

* **[Oak Index Definition Generator](https://oakutils.appspot.com/generate/index)**

   * 从XPath或JCR-SQL2查询语句生成最佳Lucence属性索引。

* **[AEM Chrome插件](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Google Chrome Web浏览器扩展，在浏览器的开发工具控制台中显示每个请求的日志数据，包括已执行的查询及其查询计划。
   * 要求在AEM上安装并启用[Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi)。
