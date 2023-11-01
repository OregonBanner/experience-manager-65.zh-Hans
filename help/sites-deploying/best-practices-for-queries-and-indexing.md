---
title: 有关查询和索引的最佳实践
description: 本文提供了有关如何优化索引和查询的指南。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '4609'
ht-degree: 6%

---

# 有关查询和索引的最佳实践{#best-practices-for-queries-and-indexing}

迁移到AEM 6中的Oak后，对查询和索引的管理方式做出了一些重大更改。 在Jackrabbit 2下，所有内容均默认编制索引，并可自由查询。 在Oak中，必须在下手动创建索引 `oak:index` 节点。 可以在没有索引的情况下执行查询，但对于大型数据集，查询将运行缓慢，甚至中止。

本文概述了何时创建索引以及在不需要索引时，避免使用不必要查询的技巧，以及优化索引和查询以尽可能发挥最佳性能的提示。

另外，请务必阅读 [关于编写查询和索引的Oak文档](/help/sites-deploying/queries-and-indexing.md). 除了索引是AEM 6中的一个新概念之外，从以前的AEM安装中迁移代码时，还需要考虑Oak查询中的语法差异。

## 何时使用查询 {#when-to-use-queries}

### 存储库和分类设计 {#repository-and-taxonomy-design}

在设计存储库的分类时，需要考虑几个因素。其中包括访问控制、本地化、组件和页面属性继承等。

在设计涵盖这些方面的分类法时，考虑索引设计的“可通行性”也很重要。在这种情况下，可通行性是分类法的能力，该分类法允许基于内容的路径以可预测地方式访问内容。 这将使系统比需要运行许多查询的系统更易于维护。

此外，在设计分类法时，考虑排序是否重要也很重要。 如果不需要显式排序，并且需要许多同级节点，则最好使用无序节点类型，例如 `sling:Folder` 或 `oak:Unstructured`. 如果需要排序， `nt:unstructured`、和 `sling:OrderedFolder` 更合适。

### 组件中的查询 {#queries-in-components}

由于查询可能是在AEM系统上执行的最繁重的操作之一，因此最好在组件中避免查询。 每次呈现页面时执行多个查询通常会降低系统的性能。有两种策略可用于在呈现组件时避免执行查询： **遍历节点** 和 **预取结果**.

#### 遍历节点 {#traversing-nodes}

如果存储库的设计允许事先了解所需数据的位置，则可以部署从必要路径检索此数据的代码，而无需运行查询来查找它。

这方面的一个例子是呈现适合特定类别的内容。一种方法是使用类别属性组织内容，并且可以通过查询该属性来填充显示类别中项目的组件。

更好的方法是按类别通过分类法构造此内容，以便可以手动检索。

例如，如果内容存储在类似于以下的分类法中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

此 `/content/myUnstructuredContent/parentCategory/childCategory` 可以简单地检索节点，解析其子节点并用于呈现组件。

此外，当您处理一个小的或同质的结果集时，遍历存储库并收集所需的节点会比通过手工创建查询来返回相同的结果集更快。 作为一般考虑，应尽可能避免查询。

#### 预取结果 {#prefetching-results}

有时，组件周围的内容或需求将不允许使用节点遍历作为检索所需数据的方法。 在这些情况下，需要在呈现组件之前执行所需的查询，以确保最终用户获得最佳性能。

如果可以在编写组件时计算组件所需的结果，并且预期内容不会更改，则可以在作者在对话框中应用设置时执行查询。

如果数据或内容会定期更改，则可以按计划或通过侦听器执行查询，以更新基础数据。然后，可以将结果写入存储库中的共享位置。任何需要此数据的组件都可以从该单个节点提取值，而无需在运行时执行查询。

## 查询优化 {#query-optimization}

运行不使用索引的查询时，将记录有关节点遍历的警告。 如果这是一个经常运行的查询，请创建一个索引。 要确定给定查询正在使用的索引，请 [说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query) 推荐。 有关更多信息，可以为相关搜索API启用DEBUG日志记录。

>[!NOTE]
>
>修改索引定义后，必须重建索引（重新编制索引）。 根据索引的大小，完成此操作可能需要一些时间。

运行复杂查询时，可能会出现以下情况：将查询分解为多个较小的查询，然后通过代码联接数据，这实际上更有效。 对这些案例的建议是比较两种方法的性能，以确定哪种选项更适合相关用例。

AEM允许使用以下三种方式之一编写查询：

* 通过 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) （推荐）
* 使用XPath（推荐）
* 使用SQL2

虽然所有查询在运行前都转换为SQL2，但是查询转换的开销是最小的，因此，在选择查询语言时最大的关注是开发团队的可读性和舒适度。

>[!NOTE]
>
>使用QueryBuilder时，它会确定默认结果计数，这在Oak中比早期版本的Jackrabbit慢。 为了弥补这一点，您可以使用 [guessTotal参数](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Explain查询工具 {#the-explain-query-tool}

与任何查询语言一样，优化查询的第一步是了解它将如何运行。 要启用此活动，您可以使用 [说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query) 它是“操作仪表板”的一部分。 使用此工具，可以插入查询并对其进行说明。 如果查询将导致大型存储库和运行时以及将使用的索引出现问题，则会显示警告。 该工具还可以加载一系列慢查询和常用查询，然后可以对其进行解释和优化。

### DEBUG查询日志记录 {#debug-logging-for-queries}

要获取有关Oak如何选择要使用的索引以及查询引擎如何实际执行查询的其他信息，请 **调试** 可以为以下包添加日志记录配置：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

完成查询调试后，请确保删除此日志程序。 它往往会输出大量活动，而且最终可能会向磁盘中填充日志文件。

有关如何执行此操作的更多信息，请参见 [日志记录文档](/help/sites-deploying/configure-logging.md).

### 索引统计信息 {#index-statistics}

Lucene注册一个JMX Bean，它将提供有关索引内容的详细信息，包括每个索引中存在的文档大小和数量。

您可以通过访问位于以下位置的JMX控制台来访问该控制台： `https://server:port/system/console/jmx`

登录到JMX控制台后，执行搜索 **Lucene索引统计数据** 找到它。 其他索引统计数据可在以下位置找到： **IndexStat** MBean。

有关查询统计数据，请查看命名的MBean **Oak查询统计数据**.

如果您希望使用之类的工具深入了解索引 [Luke](https://code.google.com/archive/p/luke/)中，您必须使用Oak控制台转储来自 `NodeStore` 到文件系统目录。 有关如何执行此操作的说明，请阅读 [Lucene文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

您还可以以JSON格式提取系统中的索引。 为此，您需要访问 `https://server:port/oak:index.tidy.-1.json`

### 查询限制 {#query-limits}

**开发期间**

设置低阈值 `oak.queryLimitInMemory` (例如，10000)和Oak。 `queryLimitReads` （例如，5000）并优化在点击UnsupportedOperationException时开销巨大的查询，该异常显示“查询读取了超过x个节点……”

这有助于避免资源密集型查询（即，不受任何索引支持或较少覆盖的索引支持）。 例如，读取100万个节点的查询会提高I/O，并对应用程序的整体性能产生负面影响。 任何由于上述限制而失败的查询都应进行分析和优化。

#### **部署后** {#post-deployment}

* 监测日志中触发大型节点遍历或大型栈内存消耗的查询： &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少遍历的节点数

* 监测日志中触发大型栈内存消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少栈内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数来调整节点遍历阈值，以防止大型查询使环境过载。

推荐值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述两个参数是预配置的OOTB，可以通过OSGi QueryEngineSettings持久保留。

下提供了更多信息： [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 创建高效索引的提示 {#tips-for-creating-efficient-indexes}

### 是否应该创建索引？ {#should-i-create-an-index}

在创建或优化索引时，首先要问的问题是给定情况下是否需要索引。 如果系统通过批处理仅运行一次或偶尔在非高峰时间运行有问题的查询，则最好根本不创建索引。

创建索引后，每次更新索引数据时，也必须更新索引。 由于这会对系统产生性能影响，因此应仅在需要索引时才创建索引。

此外，只有在索引中包含的数据足够独特，可以进行保证时，索引才有用。 以一本书中的索引及其涵盖的主题为例。 在文本中索引一组主题时，通常会有数百或数千个条目，这使您能够快速跳转到页面的子集，以快速找到您正在寻找的信息。 如果该索引只有两个或三个条目，每个条目都指向数百个页面，则该索引将不起作用。 这一概念同样适用于数据库索引。 如果只有几个唯一值，则索引将没有用。 话虽如此，一个指数也可能变得太大而不能使用。 要查看索引统计信息，请参阅 [索引统计信息](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) 以上。

### Lucene索引或属性索引？ {#lucene-or-property-indexes}

Lucene索引是在Oak 1.0.9中引入的，对于在AEM 6最初发布时引入的属性索引，它提供了一些强大的优化功能。 在决定使用Lucene索引还是属性索引时，请考虑以下因素：

* Lucene索引比属性索引提供更多的功能。 例如，属性索引只能索引单个属性，而Lucene索引可以包含多个属性。 有关Lucene索引中所有可用功能的更多信息，请参阅 [文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Lucene索引是异步的。 虽然这大大提高了性能，但它也会导致在将数据写入存储库和更新索引之间出现延迟。 如果让查询返回100%准确结果至关重要，则需要属性索引。
* 由于是异步的，Lucene索引无法强制执行唯一性约束。 如果需要，则需要设置属性索引。

通常，建议使用Lucene索引，除非迫切需要使用属性索引以便获得更高性能和灵活性的好处。

### Solr索引 {#solr-indexing}

默认情况下，AEM还支持Solr索引。 本文用于支持全文搜索，但也可用于支持任何类型的JCR查询。 当AEM实例没有足够的CPU容量来处理“搜索密集型”部署（如具有大量并发用户的搜索驱动网站）中所需的查询数量时，应考虑使用Solr。 或者，Solr可以通过基于爬虫的方法实现，以使用平台的一些更高级的功能。

可以将Solr索引配置为在用于开发环境的AEM服务器上运行，也可以将索引卸载到远程实例，以提高生产和暂存环境中的搜索可扩展性。 虽然卸载搜索提高了可扩展性，但它会导致延迟，因此，除非有必要，否则不建议这样做。 有关如何配置Solr集成以及如何创建Solr索引的更多信息，请参见 [Oak查询和索引文档](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>虽然采用集成的Solr搜索方法允许将索引卸载到Solr服务器。 如果通过基于爬网程序的方法使用Solr服务器的更高级功能，则需要执行额外的配置工作。

使用此方法的缺点是，虽然默认情况下，AEM查询会遵循ACL，从而隐藏用户无权访问的结果，但将搜索外部化到Solr服务器将无法支持此功能。 如果要以这种方式将搜索外部化，则必须格外注意确保用户不会看到他们不应看到的结果。

在可能需要汇总来自多个源的搜索数据的情况下，此方法可能适用的潜在用例。 例如，您可能将某个站点托管在AEM上，将另一个站点托管在第三方平台上。 可以将Solr配置为对两个站点的内容进行爬网并将其存储在聚合索引中。 这将允许跨站点搜索。

### 设计注意事项 {#design-considerations}

Lucene索引的Oak文档列出了设计索引时需要考虑的几个事项：

* 如果查询使用不同的路径限制，请使用 `evaluatePathRestrictions`. 这允许查询返回指定路径下的结果子集，然后根据查询筛选它们。 否则，查询将搜索与存储库中的查询参数匹配的所有结果，然后根据路径筛选它们。
* 如果查询使用排序，则为已排序的属性设置明确的属性定义 `ordered` 到 `true` 为了它。 这样可以在索引中对结果按原样排序，并节省查询执行时开销巨大的排序操作。

* 只将所需的内容放入索引。 添加不需要的功能或属性会导致索引增长并减慢性能。
* 在属性索引中，具有唯一的属性名称有助于减小索引的大小，但对于Lucene索引，请使用 `nodeTypes` 和 `mixins` 指标具有凝聚性。 查询特定 `nodeType` 或 `mixin` 将比查询性能更强 `nt:base`. 使用此方法时，定义 `indexRules` 对于 `nodeTypes` 有疑问。

* 如果查询仅在特定路径下运行，则在这些路径下创建这些索引。 索引无需位于存储库的根目录下。
* 当所有被索引的属性都相关时，建议使用单个索引，以允许Lucene尽可能多地在本机评估属性限制。 此外，查询将只使用一个索引，即使在执行连接时也是如此。

### CopyonRead {#copyonread}

如果 `NodeStore` 远程存储，一个称为 `CopyOnRead` 可以启用。 选项导致在读取远程索引时将远程索引写入本地文件系统。 这有助于提高经常针对这些远程索引运行的查询的性能。

这可以在OSGi控制台中的 **LuceneIndexProvider** 并从Oak 1.0.13开始默认启用。

### 删除索引 {#removing-indexes}

删除索引时，始终建议通过设置 `type` 属性至 `disabled` 并进行测试，以确保您的应用程序在实际删除之前可以正常运行。 禁用索引时不会更新，因此，如果重新启用索引，则可能没有正确内容，并且可能需要重新编制索引。

删除TarMK实例上的属性索引后，必须运行压缩以回收任何正在使用的磁盘空间。 对于Lucene索引，实际的索引内容存在于BlobStore中，因此需要数据存储垃圾收集。

删除MongoDB实例上的索引时，删除成本与索引中的节点数成正比。 由于删除大型索引可能会导致问题，因此推荐的方法是禁用该索引，并仅在维护时段期间使用（例如）删除它 **oak-mongo.js**. 请注意，不应将此方法用于常规节点内容，因为它可能会引入数据不一致。

>[!NOTE]
>
>有关oak-mongo.js的更多信息，请参见 [“命令行工具”部分](https://jackrabbit.apache.org/oak/docs/command_line.html) Oak文档的URL值。

### JCR查询备忘单 {#jcrquerycheatsheet}

为了支持创建高效的 JCR 查询和索引定义，[JCR 查询备忘表](assets/JCR_query_cheatsheet-v1.1.pdf)可供下载，并可在开发过程中用作参考。它包含 QueryBuilder、XPath 和 SQL-2 的示例查询，并涵盖了在查询性能方面表现不同的多个场景。它还提供了关于如何构建或定制 Oak 索引的建议。本备忘单的内容适用于AEM 6.5和AEMas a Cloud Service。

## 重新索引 {#re-indexing}

本节概述了 **仅限** 重新索引Oak索引的可接受原因。

除下面列出的原因外，启动Oak索引的重新索引会 **非** 更改行为或解决问题，从而不必要地增加AEM上的负载。

除非下表中的原因涵盖，否则应避免对Oak索引重新编制索引。

>[!NOTE]
>
>在参阅下表以确定重新索引是否有用之前， **始终** 验证：
>
>* 查询正确
>* 查询解析为预期的索引(使用 [说明查询](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引过程已完成
>

### Oak索引配置更改 {#oak-index-configuration-changes}

重新索引Oak索引唯一可接受的不出错条件是Oak索引的配置已更改。

*处理重新索引时，应始终适当考虑它对AEM整体性能的影响，并在活动较少或维护时段执行。*

以下详细列出了可能的问题以及解决方案：

* [属性索引定义更改](#property-index-definition-change)
* [Lucene索引定义更改](#lucene-index-definition-change)

#### 属性索引定义更改 {#property-index-definition-change}

* 适用于/if：

   * 所有Oak版本
   * 仅 [属性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症状:

   * 结果中缺少属性索引的定义更新之前存在的节点

* 如何验证：

   * 确定在部署更新的索引定义之前是否创建/修改了缺少的节点。
   * 验证 `jcr:created` 或 `jcr:lastModified` 针对索引的修改时间的任何缺失节点的属性

* 如何解决：

   * [重新索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene索引
   * 或者，触摸（执行良性的写入操作）丢失的节点

      * 需要手动接触或自定义代码
      * 需要知道缺失节点集
      * 需要更改节点上的任何属性

#### Lucene索引定义更改 {#lucene-index-definition-change}

* 适用于/if：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含预期结果
   * 查询结果未反映索引定义的预期行为
   * 查询计划未根据索引定义报告预期输出

* 如何验证：

   * 验证是否使用Lucene索引统计数据JMX Mbean (LuceneIndex)方法更改了索引定义 `diffStoredIndexDefinition`.

* 如何解决：

   * 1.6之前的Oak版本：

      * [重新索引](#how-to-re-index) lucene索引

   * Oak 1.6及更高版本

      * 如果现有内容不受更改的影响，则只需刷新

         * [刷新](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) 通过设置的lucene索引 [oak：queryIndexDefinition]@refresh=true

      * 否则， [重新索引](#how-to-re-index) lucene索引

         * 注意：将使用上次良好重新索引（或初始索引）后的索引状态，直到触发新的重新索引为止

### 错误和特殊情况 {#erring-and-exceptional-situations}

下表描述了重新索引Oak索引可解决该问题的唯一可接受错误和异常情况。

如果AEM上遇到与下面列出的标准不匹配的问题，请 **非** 重新索引任何索引，因为这不能解决问题。

以下详细列出了可能的问题以及解决方案：

* [缺少Lucene索引二进制文件](#lucene-index-binary-is-missing)
* [Lucene索引二进制文件损坏](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二进制文件 {#lucene-index-binary-is-missing}

* 适用于/if：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含预期结果

* 如何验证：

   * 错误日志文件包含一个异常，表示Lucene索引的二进制文件缺失

* 如何解决：

   * 执行遍历存储库检查；例如：

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     遍历存储库可确定是否缺少其他二进制文件（Lucene文件除外）

   * 如果缺少Lucene索引以外的二进制文件，则从备份中还原
   * 否则， [重新索引](#how-to-re-index) *所有* lucene索引
   * 注意:

     此条件表示数据存储配置错误，可能会导致ANY二进制文件（例如，资产二进制文件）丢失。

     在这种情况下，请还原到存储库的最后一个已知良好版本以恢复所有丢失的二进制文件。

#### Lucene索引二进制文件损坏 {#lucene-index-binary-is-corrupt}

* 适用于/if：

   * 所有Oak版本
   * 仅 [lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状:

   * Lucene索引不包含预期结果

* 如何验证：

   * 此 `AsyncIndexUpdate` （每五秒一次）将失败，但error.log中有一个异常：

     `...a Lucene index file is corrupt...`

* 如何解决：

   * 删除Lucene索引的本地副本

      1. 停止AEM
      1. 删除位于的Lucene索引的本地副本 `crx-quickstart/repository/index`
      1. 重新启动AEM

   * 如果这不能解决问题，并且 `AsyncIndexUpdate` 例外情况会持续存在，则：

      1. [重新索引](#how-to-re-index) 出错的索引
      1. 同时提交 [Adobe支持](https://helpx.adobe.com/support.html) 票证

### 如何重新索引 {#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中， [oak-run.jar是唯一支持的方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) 有关对MongoMK或RDBMK存储库重新编制索引的信息。

#### 重新索引属性索引 {#re-indexing-property-indexes}

* 使用 [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) 重新索引属性索引
* 在属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web控制台，通过 **PropertyIndexAsyncReindex** 马来西亚电信；

  例如，

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene属性索引 {#re-indexing-lucene-property-indexes}

* 使用 [oak-run.jar以重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene属性索引。
* 在lucene属性索引上，将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>上一节总结了来自AEM的Oak重新索引指导并提供了框架。 [Apache Oak文档](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) 在AEM的上下文中。

### 二进制文件的文本预提取 {#text-pre-extraction-of-binaries}

文本预提取是指从二进制文件中提取和处理文本的过程，通过隔离的过程直接从数据存储中提取和处理文本，并将提取的文本直接公开给后续的Oak索引重新/索引的过程。

* 建议使用Oak文本预提取对存储库中的Lucene索引进行重新索引，这些存储库具有大量包含可提取文本(例如，PDF、Word文档、PPT、TXT等)且可通过部署的Oak索引进行全文搜索的文件（二进制文件）；例如， `/oak:index/damAssetLucene`.
* 文本预提取仅有利于Lucene索引的重新编入/索引，而非Oak属性索引，因为属性索引不会从二进制文件中提取文本。
* 当对文本密集型二进制文件(PDF、Doc、TXT等)进行全文重新索引时，文本预提取会产生非常积极的影响，而由于图像不包含可提取文本，因此图像存储库将不会享有相同的效率。
* 文本预提取以超高效的方式执行全文搜索相关文本的提取，并以超高效的方式将其公开给Oak重新/索引过程。

#### 何时可以使用文本预提取？ {#when-can-text-pre-extraction-be-used}

重新索引一个 **现有** 已启用二进制提取的lucene索引

* 重新索引处理 **所有** 存储库中的候选内容；当要从中提取全文的二进制文件数量众多或复杂时，AEM上会增加执行全文提取的计算负担。 文本预提取将文本提取的“计算成本高昂的工作”转移到直接访问AEM数据存储的独立进程中，从而避免了AEM中的开销和资源争用。

支持部署 **新建** 启用了二进制提取的Lucene索引到AEM

* 当新索引（启用了二进制提取）部署到AEM中时，Oak会在下次异步全文索引运行时自动索引所有候选内容。 出于上述重新索引中描述的相同原因，这可能会导致在AEM上产生不适当的负载。

#### 何时才能使用文本预提取？ {#when-can-text-pre-extraction-not-be-used}

文本预提取不能用于添加到存储库的新内容，也不一定需要。

向存储库添加新内容时，将采用异步全文索引过程（默认情况下，每5秒索引一次）以自然和递增方式索引这些内容。

在AEM的正常操作下，例如通过Web UI上传资源或以编程方式摄取资源，AEM将自动以增量方式全文索引新的二进制内容。 由于数据量是增量式的，并且相对较小（大约是可在5秒内保留到存储库中的数据量），因此AEM可以在索引期间从二进制文件执行全文提取，而不会影响整体系统性能。

#### 使用文本预提取的先决条件 {#prerequisites-to-using-text-pre-extraction}

* 您将重新索引执行全文二进制提取的Lucene索引，或部署将全文索引现有内容的二进制文件的新索引
* 要从中预提取文本的内容（二进制文件）必须位于存储库中
* 用于生成CSV文件和执行最终重新索引的维护窗口
* Oak版本：1.0.18及更高版本、1.2.3及更高版本
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)版本1.7.4+
* 文件系统文件夹/共享用于存储可从索引AEM实例访问的提取文本

   * 文本预提取OSGi配置需要指向提取的文本文件的文件系统路径，因此必须可直接从AEM实例（本地驱动器或文件共享装载）访问这些文件

#### 如何执行文本预提取 {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***下面列出的oak-run.jar命令在 [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上图和以下步骤用于解释和补充Apache Oak文档中概述的技术文本预提取步骤。

![文本预提取流程](assets/chlimage_1-139.png)

**生成要预提取的内容列表**

*在此操作期间遍历节点存储时，在维护时段/低使用时段运行步骤1(a-b)，这可能会导致系统产生大量负载。*

1a. 运行 `oak-run.jar --generate` 创建将预提取其文本的节点列表。

1b. 节点列表(1a)以CSV文件形式存储到文件系统

每次都会遍历整个节点存储（由oak-run命令中的路径指定） `--generate` 执行，并且 **新建** 创建CSV文件。 CSV文件为 **非** 在文本预提取过程的离散执行之间重用（步骤1 - 2）。

**将文本预提取到文件系统**

*在AEM的正常操作期间，可以执行步骤2(a-c)，因为它只与数据存储交互。*

2a. 运行 `oak-run.jar --tika` 为在(1b)中生成的CSV文件中枚举的二进制节点预提取文本

2b. 在(2a)中启动的进程直接访问数据存储中CSV中定义的二进制节点，并提取文本。

2c. 提取的文本以可由Oak重新索引过程(3a)摄取的格式存储在文件系统上

预先提取的文本在CSV中由二进制指纹识别。 如果二进制文件相同，则可以跨AEM实例使用相同的预提取文本。 由于AEM Publish通常是AEM Author的子集，因此从AEM Author预提取的文本通常也可用于重新索引AEM Publish(假设AEM Publish具有对所提取文本文件的文件系统访问权限)。

预先提取的文本可随着时间的推移逐步添加到。 文本预提取将跳过之前提取的二进制文件的提取，因此最佳实践是保留预提取的文本，以防将来再次进行重新索引（假设提取的内容不会太大）。 如果是，则评估在过渡期间压缩内容（因为文本压缩得不错）。

**重新索引Oak索引，从提取的文本文件中获取全文**

*在此操作期间遍历节点存储时，在维护/低使用期间运行重新索引（步骤3a-b），这可能会导致系统产生大量负载。*

3a. [重新索引](#how-to-re-index) 在AEM中调用的Lucene索引。

3b. Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi配置（配置为通过文件系统路径指向提取的文本）指示Oak从提取的文件中获取全文文本，并避免直接点击和处理存储在存储库中的数据。
