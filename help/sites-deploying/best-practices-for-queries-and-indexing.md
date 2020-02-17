---
title: 查询和索引的最佳实践
seo-title: 查询和索引的最佳实践
description: 本文提供有关如何优化索引和查询的指南。
seo-description: 本文提供有关如何优化索引和查询的指南。
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 查询和索引的最佳实践{#best-practices-for-queries-and-indexing}

在AEM 6中，随着向Oak的过渡，对查询和索引的管理方式进行了一些重大更改。 在Jackrabbit 2下，默认情况下已索引所有内容，并可以自由查询。 在Oak中，必须在节点下手动创建 `oak:index` 索引。 无需索引即可执行查询，但对于大数据集，查询执行速度会非常慢，甚至会中止。

本文将概述何时创建索引以及何时不需要索引，避免在不需要查询时使用的技巧，以及优化索引和查询以尽可能优化它们的提示。

此外，请务必阅读有关编写查 [询和索引的Oak文档](/help/sites-deploying/queries-and-indexing.md)。 除了索引是AEM 6中的一个新概念之外，在从以前的AEM安装迁移代码时，Oak查询中还有语法差异，需要考虑这些差异。

## 何时使用查询 {#when-to-use-queries}

### 存储库和分类设计 {#repository-and-taxonomy-design}

在设计存储库分类时，需要考虑几个因素。 这包括访问控制、本地化、组件和页面属性继承等。

在设计可解决这些问题的分类时，还应考虑索引设计的“可遍历性”。 在此上下文中，可遍历性是分类的功能，它允许根据内容的路径对内容进行可预测的访问。 这样，系统将变得更加高效，并且比需要执行大量查询的系统更容易维护。

此外，在设计分类时，务必考虑排序是否重要。 如果不需要显式排序并且需要大量同级节点，则最好使用无序节点类型，如 `sling:Folder` 或 `oak:Unstructured`。 如果需要订购， `nt:unstructured` 则 `sling:OrderedFolder` 更合适。

### 组件中的查询 {#queries-in-components}

由于查询可能是对AEM系统执行的较繁琐的操作之一，因此最好在组件中避免查询。 每次呈现页面时执行多个查询通常会降低系统的性能。 有两种策略可用于在呈现组件时避免执行查询：遍 **历节点** , **并预取结果**。

#### 遍历节点 {#traversing-nodes}

如果所述储存库被设计为允许事先了解所需数据的位置，则可以部署从所需路径检索该数据的代码而无需运行查询以找到它。

这方面的一个示例是渲染适合特定类别的内容。 一种方法是使用类别属性组织内容，该类别属性可通过查询来填充显示类别中项目的组件。

更好的方法是按类别将此内容结构化，以便可以手动检索。

例如，如果内容存储在类别中，类似于：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

该节 `/content/myUnstructuredContent/parentCategory/childCategory` 点可以简单地检索，其子节点可以解析并用于渲染组件。

此外，当您处理小的或同构的结果集时，可以更快地遍历存储库和收集所需的节点，而不是生成查询以返回相同的结果集。 作为一般考虑，应当尽可能避免提出问题。

#### 预取结果 {#prefetching-results}

有时组件周围的内容或要求将不允许使用节点遍历作为检索所需数据的方法。 在这些情况下，需要在呈现组件之前执行所需的查询，以确保最终用户的最佳性能。

如果创作组件时可以计算组件所需的结果并且内容不会更改的预期值，则当作者在对话框中应用设置时可以执行查询。

如果数据或内容将定期更改，则可以按计划或通过监听器执行查询以更新基础数据。 然后，结果可写入存储库中的共享位置。 任何需要此数据的组件随后都可以从此单个节点中提取值，无需在运行时执行查询。

## 查询优化 {#query-optimization}

运行不使用索引的查询时，将记录有关节点遍历的警告。 如果这是一个将经常运行的查询，则应创建索引。 要确定给定查询使用的索引，建议使 [用“解释查询](/help/sites-administering/operations-dashboard.md#explain-query) ”工具。 有关其他信息，可以为相关搜索API启用DEBUG日志记录。

>[!NOTE]
>
>修改索引定义后，需要重新构建（重新索引）索引。 根据索引的大小，完成此操作可能需要一些时间。

在运行复杂查询时，可能存在将查询分解为多个较小的查询并在事实性能提高后通过代码连接数据的情况。 这些案例的建议是比较两种方法的绩效，以确定哪个选项更适合所述用例。

AEM允许通过以下三种方式之一编写查询：

* 通过 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) （建议）
* 使用XPath（建议）
* 使用SQL2

虽然所有查询在运行前都转换为SQL2，但查询转换的开销很小，因此选择查询语言时最关心的问题是开发团队的可读性和舒适性。

>[!NOTE]
>
>使用QueryBuilder时，它将确定默认的结果计数，与Jackrabbit的先前版本相比，Oak中的结果计数较慢。 要弥补这一缺点，您可以使用 [guessTotal参数](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### Explain Query Tool {#the-explain-query-tool}

与任何查询语言一样，优化查询的第一步是了解如何执行该查询。 要启用此活动，您可以使用“ [操作控制板](/help/sites-administering/operations-dashboard.md#explain-query) ”中的“解释查询”工具。 使用此工具，可插入并解释查询。 如果查询将导致大型存储库以及执行时间和将使用的索引出现问题，则会显示警告。 该工具还可加载慢速和常用查询列表，然后可以解释和优化这些查询。

### 查询的DEBUG日志记录 {#debug-logging-for-queries}

要获取有关Oak如何选择要使用的索引以及查询引擎如何实际执行查询的其他信息，可以为以下包添加 **DEBUG** logging configuration:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

在调试完查询后，请务必删除此记录器，因为它将输出大量活动并最终会用日志文件填充磁盘。

有关如何执行此操作的详细信息，请参阅日 [志记录文档](/help/sites-deploying/configure-logging.md)。

### 索引统计 {#index-statistics}

Lucene注册一个JMX Bean，它将提供有关索引内容的详细信息，包括每个索引中存在的文档的大小和数量。

访问JMX控制台， `https://server:port/system/console/jmx`

登录到JMX控制台后，请执行搜索 **Lucene索引统计信息** ，以便找到它。 其他索引统计信息可在 **IndexStats** MBean中找到。

有关查询统计信息，请查看名为 **Oak查询统计信息的MBean**。

如果要使用 [Luke](https://code.google.com/p/luke/)等工具挖掘索引，您需要使用Oak控制台将索引从文件系统目录 `NodeStore` 转储到文件系统目录。 有关如何执行此操作的说明，请阅读 [Lucene文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您还可以以JSON格式提取系统中的索引。 为此，您需要访问 `https://server:port/oak:index.tidy.-1.json`

### 查询限制 {#query-limits}

**开发过程中**

设置低阈值( `oak.queryLimitInMemory` 例如 10000)和橡木。 `queryLimitReads` (例如 5000)，并在点击UnsupportedOperationException时优化昂贵的查询，该查询的读取次数超过x节点……。

这有助于避免资源密集型查询(即 不受任何索引的支持，也不受覆盖索引的支持)。 例如，读取100万个节点的查询将导致I/O的增加，并对应用程序的整体性能产生负面影响。 应分析并优化因超出限制而失败的任何查询。

#### **部署后**{#post-deployment}

* 监视日志以查找触发大节点遍历或大堆内存消耗的查询：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少经过的节点数

* 监视日志以查找触发大堆内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少堆内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数调整节点遍历的阈值，以防止大型查询过载环境。

建议的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2个参数是预配置的OOTB，并可通过OSGi queryEngineSettings进行保留。

更多信息，请访问： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 创建有效索引的提示 {#tips-for-creating-efficient-indexes}

### 我应该创建索引吗？ {#should-i-create-an-index}

创建或优化索引时要问的第一个问题是，是否确实需要索引才能满足给定的情况。 如果您只要通过批处理在系统的非高峰时间运行所述查询一次或仅偶尔运行，则最好不要创建索引。

创建索引后，每次更新索引数据时，索引也必须更新。 由于这会对系统产生性能影响，因此仅应在实际需要索引时创建索引。

此外，只有索引中包含的数据足够独特，足以保证索引的唯一性时，索引才有用。 考虑书籍中的索引及其所涵盖的主题。 在文本中为一组主题建立索引时，通常会有成百上千的条目，这样您就可以快速跳转到页面的子集以快速找到您要查找的信息。 如果该索引只有两三个条目，每个条目指向几百个页面，则该索引将不太有用。 这一概念同样适用于数据库索引。 如果只有几个唯一值，则索引将不会很有用。 话虽如此，一个指数也可能变得过大，无法发挥作用。 要查看索引统计信息，请参阅上 [述索引统计](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 。

### Lucene或属性索引？ {#lucene-or-property-indexes}

Lucene索引在Oak 1.0.9中引入，并对AEM 6的初始启动中引入的属性索引提供了一些强大的优化。 在决定是使用Lucene索引还是属性索引时，请考虑以下因素：

* Lucene索引提供的功能比属性索引更多。 例如，属性索引只能索引单个属性，而Lucene索引可以包含许多属性。 有关Lucene索引中可用的所有功能的详细信息，请查阅 [文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引是异步的。 虽然这可以显着提高性能，但在将数据写入存储库和更新索引之间也会产生延迟。 如果让查询返回100%准确结果至关重要，则需要属性索引。
* 由于异步，Lucene索引不能强制执行唯一性约束。 如果需要，则需要设置属性索引。

通常，建议您使用Lucene索引，除非迫切需要使用属性索引，这样您就可以获得更高性能和灵活性的优势。

### 索尔索引 {#solr-indexing}

默认情况下，AEM还支持Solr索引。 这主要用于支持全文搜索，但也可用于支持任何类型的JCR查询。 当AEM实例没有CPU容量来处理搜索密集型部署（如具有大量并发用户的搜索驱动型网站）中所需的查询数时，应考虑Solr。 或者，Solr可以在基于爬虫的方法中实现，以利用该平台的一些更高级的功能。

可以将Solr索引配置为运行嵌入在AEM服务器上的开发环境，或将索引卸载到远程实例，以提高生产和暂存环境中的搜索可伸缩性。 虽然分载搜索可提高可伸缩性，但会引入延迟，因此，除非需要，否则不建议这样做。 有关如何配置Solr集成以及如何创建Solr索引的更多信息，请参阅 [Oak查询和索引文档](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>采用集成的Solr搜索方法时，将允许将索引分载到Solr服务器。 如果通过基于Crawler的方法使用Solr服务器的更高级功能，则需要额外的配置工作。 Headwire已经创建了开 [放源连接器](https://www.aemsolrsearch.com/#/) ，以加速这些类型的实现。

采用此方法的缺点是，默认情况下，AEM查询会遵循ACL，从而隐藏用户无权访问的结果，将搜索外部化到Solr服务器将不支持此功能。 如果要以这种方式将搜索外部化，则必须格外小心，以确保用户不会看到他们不应看到的结果。

此方法可能适合的潜在使用情形是指可能需要汇总多个来源的搜索数据。 例如，您可能有一个站点在AEM上托管，另一个站点在第三方平台上托管。 Solr可配置为搜索两个站点的内容并将它们存储在聚合索引中。 这将允许跨站点搜索。

### 设计注意事项 {#design-considerations}

Lucene索引的Oak文档列出了设计索引时要考虑的几个事项：

* 如果查询使用不同的路径限制，则使用 `evaluatePathRestrictions`。 这将允许查询返回指定路径下的结果子集，然后根据查询过滤它们。 否则，查询将搜索库中与查询参数匹配的所有结果，然后根据路径筛选它们。
* 如果查询使用排序，则为sorted属性定义显式属性，并为其 `ordered` 设置 `true` 为属性。 这将允许在索引中按此顺序对结果进行排序，并在查询执行时节省代价高昂的排序操作。

* 只需将所需内容放入索引中。 添加不需要的功能或属性将导致索引增长并降低性能。
* 在属性索引中，具有唯一的属性名称有助于减小索引的大小，但对于Lucene索引，应使用 `nodeTypes``mixins` 并应该实现内聚索引。 查询特定 `nodeType` 或 `mixin` 比查询性能更高 `nt:base`。 使用此方法时，请为 `indexRules` 相关内 `nodeTypes` 容定义。

* 如果查询仅在某些路径下运行，则在这些路径下创建这些索引。 索引不必存在于存储库的根中。
* 当所有被索引的属性都与属性相关时，建议使用单个索引，以允许Lucene在本机评估尽可能多的属性限制。 此外，即使执行连接，查询也只使用一个索引。

### CopyOnRead {#copyonread}

如果远程存 `NodeStore` 储，则可启用名为 `CopyOnRead` 的选项。 此选项将导致读取远程索引时将其写入本地文件系统。 这有助于提高查询的性能，这些查询通常针对这些远程索引运行。

这可以在OSGi控制台中的 **LuceneIndexProvider** service下进行配置，并在默认情况下从Oak 1.0.13开始启用。

### 删除索引 {#removing-indexes}

删除索引时，始终建议通过将属性设置为并进行测试来临时禁用索引，以确保应用程序在实际删除之前能够正 `type` 确 `disabled` 地运行。 请注意，索引在禁用时不会更新，因此如果重新启用并且可能需要重新索引，则它可能没有正确的内容。

在删除TarMK实例上的属性索引后，需要运行压缩以回收使用中的任何磁盘空间。 对于Lucene索引，实际索引内容位于BlobStore中，因此需要数据存储垃圾收集。

在删除MongoDB实例上的索引时，删除成本与索引中的节点数成比例。 由于删除大索引可能会导致问题，建议的方法是仅在维护窗口期间使用 **oak-mongo.js等工具禁用并删除索引**。 请注意，此方法不应用于常规节点内容，因为它可能会导致数据不一致。

>[!NOTE]
>
>有关oak-mongo.js的详细信息，请参阅Oak文 [档的命令行工具部分](https://jackrabbit.apache.org/oak/docs/command_line.html) 。

## 重新构建索引 {#re-indexing}

本节概述了重新 **编制** Oak索引的唯一可接受理由。

在下述原因之外，启动Oak索引的重新索引不会 **更改行为** 或解决问题，并且不必增加AEM上的负载。

除非下表中有原因说明，否则应避免对Oak索引重新编制索引。

>[!NOTE]
>
>在咨询下表以确定重新索引是否有用之前，**始终**验证：
>
>* 查询正确
>* 该查询解析到预期索引(使用“解 [释查询”](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引过程已完成
>



### Oak索引配置更改 {#oak-index-configuration-changes}

重新索引Oak索引的唯一可接受的非索引条件是Oak索引的配置已经更改。

*应始终考虑重新编制索引对AEM整体性能的影响，并在活动量较低或维护时间较短的期间执行。*

以下是一些可能的问题和决议：

* [属性索引定义更改](#property-index-definition-change)
* [Lucene索引定义更改](#lucene-index-definition-change)

#### 属性索引定义更改 {#property-index-definition-change}

* 适用于／如果：

   * 所有Oak版本
   * 仅属 [性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症状：

   * 属性索引定义之前存在的节点在结果中缺少更新

* 如何验证：

   * 确定是否在部署更新的索引定义之前创建／修改了缺失的节点。
   * 根据索 `jcr:created` 引的修 `jcr:lastModified` 改时间验证任何缺失节点的或属性

* 如何解决：

   * [重新索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene指数
   * 或者，对缺少的节点进行触摸（执行良性写入操作）

      * 需要手动触摸或自定义代码
      * 需要知道缺少的节点集
      * 需要更改节点上的任何属性

#### Lucene索引定义更改 {#lucene-index-definition-change}

* 适用于／如果：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene指数不包含预期结果
   * 查询结果不反映索引定义的预期行为
   * 查询计划不根据索引定义报告预期输出

* 如何验证：

   * 使用Lucene索引统计信息JMX Mbean(LuceneIndex)方法验证索引定义是否已更改 `diffStoredIndexDefinition`。

* 如何解决：

   * Oak版本低于1.6:

      * [重新索引](#how-to-re-index) lucene指数
   * Oak版本1.6+

      * 如果现有内容不受更改的影响，则只需刷新

         * [通过设置](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) oak:queryIndexDefinition []@refresh=true，刷新lucene索引
      * 否则， [重新为lucene指数](#how-to-re-index) 编制索引

         * 注意：在触发新的重新索引之前，将使用上次正确重新索引（或初始索引）中的索引状态



### 异常情况 {#erring-and-exceptional-situations}

下表描述了重新索引Oak索引将解决该问题的唯一可接受的错误和特殊情况。

如果AEM遇到问题，但该问题与下面列出的条件不符，请不要重新为任何索引编制索引 **** ，因为它不会解决该问题。

以下是一些可能的问题和决议：

* [缺少Lucene索引二进制文件](#lucene-index-binary-is-missing)
* [Lucene索引二进制文件损坏](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二进制文件 {#lucene-index-binary-is-missing}

* 适用于／如果：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene指数不包含预期结果

* 如何验证：

   * 错误日志文件包含一个异常，表示缺少Lucene索引的二进制文件

* 如何解决：

   * 执行遍历存储库检查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍历存储库可确定是否缺少其他二进制文件（除lucene文件外）

   * 如果缺少lucene索引以外的二进制文件，则从备份中恢复
   * 否则，重 [新索引所有](#how-to-re-index)*lucene索引*
   * 注意:

      此条件表示可能导致ANY二进制(例如， assets二进制文件)。

      在这种情况下，请恢复到存储库的上一个已知良好的版本以恢复所有缺失的二进制文件。

#### Lucene索引二进制文件损坏 {#lucene-index-binary-is-corrupt}

* 适用于／如果：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene指数不包含预期结果

* 如何验证：

   * 错 `AsyncIndexUpdate` 误（每5秒）将失败，error.log中有例外：

      `...a Lucene index file is corrupt...`

* 如何解决：

   * 删除lucene索引的本地副本

      1. 停止AEM
      1. 删除lucene索引的本地副本 `crx-quickstart/repository/index`
      1. 重新启动AEM
   * 如果这不能解决问题，且例外情 `AsyncIndexUpdate` 况会持续存在：

      1. [重新索引](#how-to-re-index) erring索引
      1. 另请提交 [Adobe支持票证](https://helpx.adobe.com/support.html)


### 如何重新编入索引 {#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中， [oak-run.jar是在MongoMK或RDBMK存储库上重新构建索引的唯一受支持方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) 。

#### 重新索引属性索引 {#re-indexing-property-indexes}

* 使 [用oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) ，重新索引属性索引
* 在属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 通过PropertyIndexAsyncReindex **MBean，使用Web控制台异步为属性索引重** 新编制索引；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene属性索引 {#re-indexing-lucene-property-indexes}

* 使 [用oak-run.jar重新为Lucene属性索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 。
* 在lucene属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>前一节总结了AEM上下文中 [Apache Oak文档中的Oak重新索引指南](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) ，并将其框定为框架。

### 二进制文本预提取 {#text-pre-extraction-of-binaries}

文本预提取是从二进制文件中提取和处理文本的过程，直接通过隔离的过程从数据存储中提取和处理文本，并直接将提取的文本暴露给Oak索引的后续重新编制／索引。

* 建议对于具有大量包含可提取文本(例如， PDF、Word Docs、PPT、TXT等)通过部署的Oak索引进行全文搜索；例如 `/oak:index/damAssetLucene`,
* 文本预提取只有利于Lucene索引的重新索引，而非Oak属性索引，因为属性索引不会从二进制中提取文本。
* 当重文本二进制文件（PDF、Doc、TXT等）的全文重新索引时，文本预提取会产生很大的积极影响，因为作为图像存储库，由于图像不包含可提取的文本，因此，文本预提取将不会获得相同的效率。
* 文本预提取以一种非常有效的方式执行全文搜索相关文本的提取，并以一种非常有效的消费方式将其呈现给Oak重建／索引过程。

#### 何时使用CAN文本预提取？ {#when-can-text-pre-extraction-be-used}

在启用二进制提取的情 **况下** ，重新索引现有lucene索引

* 重新索引处理 **库中** 的所有候选内容；当要从中提取全文的二进制文件数量众多或复杂时，AEM上会增加执行全文提取的计算负担。 文本预提取将文本提取的“计算成本高昂的工作”移入一个可直接访问AEM数据存储的隔离进程，从而避免了AEM中的开销和资源争用。

支持在启用二进制提取的 **情况下** ，将新的lucene索引部署到AEM

* 在AEM中部署新索引（启用了二进制提取）后，Oak会在下次运行异步全文索引时自动为所有候选内容建立索引。 由于上述重新构建索引中所述的相同原因，这可能导致AEM负载过重。

#### 何时不能使用文本预提取？ {#when-can-text-pre-extraction-not-be-used}

文本预提取不能用于添加到存储库的新内容，也不必使用。

新内容添加到存储库后，将通过异步全文索引过程（默认情况下，每5秒）自然地以增量方式索引新内容。

在AEM的正常操作下（例如，通过Web UI上传资产或以编程方式获取资产）,AEM将自动以增量方式为新的二进制内容建立全文索引。 由于数据量是增量式的，并且相对较小（大约在5秒内可持续保留到存储库的数据量），因此AEM可以在索引过程中从二进制文件执行全文提取，而不会影响总体系统性能。

#### 使用文本预提取的先决条件 {#prerequisites-to-using-text-pre-extraction}

* 您将重新索引lucene索引，该索引执行全文二进制提取或部署新索引，该索引将为现有内容的全文索引二进制文件
* 要从中预提取文本的内容（二进制文件）必须位于存储库中
* 用于生成CSV文件并执行最终重新索引的维护窗口
* Oak版本：1.0.18+, 1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 用于存储可从AEM实例索引访问的提取文本的文件系统文件夹／共享

   * 文本预提取OSGi配置需要解压文本文件的文件系统路径，因此必须直接从AEM实例（本地驱动器或文件共享装载）访问它们

#### 如何执行文本预提取 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下概述的oak-run.jar命令在https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html上完全枚举[。](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上图和下面的步骤用于解释和补充Apache Oak文档中概述的技术文本预提取步骤。

![文本预提取流程](assets/chlimage_1-139.png)

**生成要预提取的内容列表**

*在维护窗口／低使用期间执行步骤1(a-b)，因为在此操作期间会遍历节点存储，这可能会对系统产生重大负载。*

1a. 执 `oak-run.jar --generate` 行以创建预提取其文本的节点列表。

1b. 节点(1a)列表作为CSV文件存储到文件系统

请注意，每次执行时都会遍历整个节点存储区（由oak-run命令中的路径指定）, `--generate` 并创建一 **个新** CSV文件。 在文本预提取 **过程** （步骤1 - 2）的离散执行之间不会重复使用CSV文件。

**将文本预提取到文件系统**

*如果步骤2(a-c)仅与数据存储交互，则可在AEM的正常操作过程中执行。*

2a。 执 `oak-run.jar --tika` 行以预提取在(1b)中生成的CSV文件中枚举的二进制节点的文本

2b. 在(2a)中启动的进程直接访问在数据存储的CSV中定义的二进制节点，并提取文本。

2c.  提取的文本以Oak重新索引过程(3a)可接受的格式存储在文件系统中

预先提取的文本在CSV中通过二进制指纹进行标识。 如果二进制文件相同，则可以在AEM实例中使用相同的预提取文本。 由于AEM发布通常是AEM作者的子集，因此从AEM作者预先提取的文本通常也可用于为AEM发布重新编制索引（假定AEM发布具有对提取的文本文件的文件系统访问权限）。

预提取的文本可以随时间递增地添加到其中。 文本预提取将跳过先前提取的二进制文件的提取，因此最好保留预提取的文本，以防将来必须再次重新索引（假定提取的内容不过大）。 如果是，则评估在中间压缩内容，因为文本压缩效果很好)。

**重新为Oak索引编制索引，从提取的文本文件获取全文**

*在维护／低使用期间执行重新索引（步骤3a-b），因为在此操作期间会遍历节点存储，这可能会对系统产生大量负载。*

3a。 [在AEM中调用](#how-to-re-index) Lucene索引的重新索引

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi配置（配置为通过文件系统路径指向“提取的文本”）指示Oak从“提取的文件”中获取全文文本，并避免直接点击和处理存储在存储库中的数据。

