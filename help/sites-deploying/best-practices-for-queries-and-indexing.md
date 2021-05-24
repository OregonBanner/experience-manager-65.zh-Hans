---
title: 有关查询和索引的最佳实践
seo-title: 有关查询和索引的最佳实践
description: 本文提供了有关如何优化索引和查询的准则。
seo-description: 本文提供了有关如何优化索引和查询的准则。
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4618'
ht-degree: 0%

---

# 有关查询和索引的最佳实践{#best-practices-for-queries-and-indexing}

在AEM 6中，除了过渡到Oak之外，还对查询和索引的管理方式进行了一些重大更改。 在Jackrabbit 2下，默认情况下所有内容都已编入索引，可以自由查询。 在Oak中，必须在`oak:index`节点下手动创建索引。 查询可以在不使用索引的情况下执行，但对于大型数据集，其执行速度会非常慢，甚至会中止。

本文将概述何时创建索引以及何时不需要索引、避免在不需要查询时使用查询的技巧以及优化索引和查询以尽可能发挥最佳性能的提示。

此外，请确保阅读[Oak文档，其中介绍了如何编写查询和索引](/help/sites-deploying/queries-and-indexing.md)。 除了索引是AEM 6中的一个新概念之外，在从以前的AEM安装中迁移代码时，Oak查询中还存在一些语法差异，需要考虑这些差异。

## 何时使用查询{#when-to-use-queries}

### 存储库和分类设计{#repository-and-taxonomy-design}

在设计存储库的分类时，需要考虑几个因素。 其中包括访问控制、本地化、组件和页面属性继承等。

在设计解决这些问题的分类时，还必须考虑索引设计的“可遍历性”。 在此环境中，可遍历性是分类的功能，该功能允许根据内容的路径进行可预测的访问。 这样可以使系统更易于维护，而不是需要执行大量查询的系统。

此外，在设计分类时，务必考虑排序是否重要。 如果不需要显式排序且需要大量同级节点，则最好使用未排序的节点类型，如`sling:Folder`或`oak:Unstructured`。 如果需要订购，则`nt:unstructured`和`sling:OrderedFolder`更合适。

### 组件{#queries-in-components}中的查询

由于查询是在AEM系统上执行的较为繁琐的操作之一，因此最好在组件中避免查询操作。 每次渲染页面时执行多个查询通常会降低系统性能。 有两种策略可用于在渲染组件时避免执行查询：**遍历节点**&#x200B;和&#x200B;**预取结果**。

#### 遍历节点{#traversing-nodes}

如果以允许事先了解所需数据位置的方式设计存储库，则可以部署从必要路径检索此数据的代码，而无需运行查询以便找到它。

例如，渲染符合特定类别的内容。 一种方法是使用可查询的类别属性来组织内容，以填充显示类别中项目的组件。

更好的方法是按类别在分类中构建此内容，以便可以手动检索。

例如，如果内容存储在类似于以下内容的分类中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

可以简单地检索`/content/myUnstructuredContent/parentCategory/childCategory`节点，可以解析其子节点并将其用于渲染组件。

此外，处理小的或同构的结果集时，可以更快地遍历存储库和收集所需的节点，而不是精心编制查询以返回相同的结果集。 作为一般考虑事项，在可能的情况下应避免提出查询。

#### 预取结果{#prefetching-results}

有时，组件的内容或要求将不允许使用节点遍历作为检索所需数据的方法。 在这些情况下，需要在渲染组件之前执行所需的查询，以确保最终用户的最佳性能。

如果在创作组件时可以计算组件所需的结果并且内容没有更改的预期值，则当作者在对话框中应用设置时，可以执行查询。

如果数据或内容会定期更改，则可以按计划或通过侦听器执行查询，以更新基础数据。 然后，结果可写入存储库中的共享位置。 然后，任何需要此数据的组件都可以从此单个节点中提取值，而无需在运行时执行查询。

## 查询优化{#query-optimization}

运行未使用索引的查询时，将记录有关节点遍历的警告。 如果这是将经常运行的查询，则应创建索引。 要确定给定查询正在使用的索引，建议使用[解释查询工具](/help/sites-administering/operations-dashboard.md#explain-query)。 有关更多信息，可以为相关搜索API启用调试日志记录。

>[!NOTE]
>
>修改索引定义后，需要重新构建索引（重新编入索引）。 根据索引的大小，完成此操作可能需要一些时间。

运行复杂查询时，可能会出现这样的情况：将查询划分为多个较小的查询，并在事实更为出色后通过代码连接数据。 这些案例的建议是比较两种方法的绩效，以确定哪个选项更适合相关用例。

AEM允许以三种方式之一编写查询：

* 通过[QueryBuilder API](/help/sites-developing/querybuilder-api.md)（推荐）
* 使用XPath（推荐）
* 使用SQL2

虽然所有查询在运行前都转换为SQL2，但查询转换的开销是极小的，因此，选择查询语言时最关心的是开发团队的可读性和舒适性。

>[!NOTE]
>
>使用QueryBuilder时，它将默认确定结果计数，与Jackrabbit的先前版本相比，Oak中的结果计数速度较慢。 要弥补这一点，您可以使用[guessTotal参数](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### 解释查询工具{#the-explain-query-tool}

与任何查询语言一样，优化查询的第一步是了解如何执行查询。 要启用此活动，您可以使用“操作功能板”中的[说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query)。 使用此工具，可插入并说明查询。 如果查询将导致大型存储库以及将使用的索引的执行时间出现问题，则会显示警告。 该工具还可以加载一系列缓慢且热门的查询，随后可以对这些查询进行说明和优化。

### 查询{#debug-logging-for-queries}的调试日志记录

要获取有关Oak如何选择要使用的索引以及查询引擎如何实际执行查询的其他信息，可以为以下包添加&#x200B;**DEBUG**&#x200B;日志记录配置：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

确保在调试完查询后删除此日志记录器，因为查询将输出大量活动，并最终会用日志文件填充磁盘。

有关如何执行此操作的更多信息，请参阅[日志记录文档](/help/sites-deploying/configure-logging.md)。

### 索引统计数据{#index-statistics}

Lucene注册一个JMX Bean，该Bean将提供有关索引内容的详细信息，包括每个索引中存在的文档大小和数量。

您可以通过访问位于`https://server:port/system/console/jmx`的JMX控制台来访问该控制台

登录到JMX控制台后，请搜索&#x200B;**Lucene索引统计信息**&#x200B;以找到它。 其他索引统计信息可在&#x200B;**IndexStats** MBean中找到。

有关查询统计信息，请查看名为&#x200B;**Oak查询统计信息**&#x200B;的MBean。

如果您希望使用诸如[Luke](https://code.google.com/p/luke/)之类的工具来挖掘索引，则需要使用Oak控制台将索引从`NodeStore`转储到文件系统目录。 有关如何执行此操作的说明，请阅读[Lucene文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您还可以以JSON格式提取系统中的索引。 为此，您需要访问`https://server:port/oak:index.tidy.-1.json`

### 查询限制 {#query-limits}

**开发期间**

为`oak.queryLimitInMemory`设置低阈值(例如 10000)和橡木。 `queryLimitReads` (例如5000)，并在点击UnsupportedOperationException时优化昂贵的查询，该查询会读取超过x个节点……。

这有助于避免资源密集型查询(即， 不受任何索引的支持，或受覆盖范围较小的索引的支持)。 例如，读取100万个节点的查询将导致I/O增加，并对应用程序的整体性能产生负面影响。 任何因超出限制而失败的查询都应进行分析和优化。

#### **部署后** {#post-deployment}

* 监视日志中触发大节点遍历或大堆内存消耗的查询：&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少已遍历的节点数

* 监视日志，以了解触发堆内存大消耗的查询：

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少堆内存消耗

对于AEM 6.0 - 6.2版本，您可以通过AEM启动脚本中的JVM参数调整节点遍历的阈值，以防止大型查询过载环境。

推荐的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2个参数是预配置的OOTB，并可通过OSGi QueryEngineSettings持久保留。

下方提供了更多信息：[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 创建有效索引的提示{#tips-for-creating-efficient-indexes}

### 我应该创建索引吗？{#should-i-create-an-index}

在创建或优化索引时需要问的第一个问题是，是否确实需要索引来满足给定情况。 如果您只打算通过批处理在系统的非高峰时间运行有关查询一次或仅偶尔运行，则最好根本不要创建索引。

创建索引后，每次更新索引数据时，索引也必须更新。 由于这会对系统产生性能影响，因此，只有在实际需要索引时才应创建索引。

此外，仅当索引中包含的数据足够独特，足以保证索引的安全时，索引才有用。 以一本书中的索引及其所涵盖的主题为例。 在文本中索引一组主题时，通常会有数百个或数千个条目，这样您就可以快速跳转到页面的子集，以快速找到要查找的信息。 如果该索引只有两三个条目，每个条目都指向几百个页面，则该索引将不太有用。 这一概念同样适用于数据库索引。 如果只有几个唯一值，则索引将不会非常有用。 话虽如此，一个指数也可能变得过大，无法发挥作用。 要查看索引统计信息，请参阅上面的[索引统计信息](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics)。

### Lucene索引还是属性索引？{#lucene-or-property-indexes}

Lucene索引在Oak 1.0.9中引入，对于AEM 6首次启动时引入的属性索引，它提供了一些强大的优化功能。 在决定是使用Lucene索引还是属性索引时，请考虑以下因素：

* Lucene索引提供的功能比属性索引多。 例如，属性索引只能索引单个属性，而Lucene索引可以包含许多属性。 有关Lucene索引中所有可用功能的更多信息，请参阅[文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引是异步的。 虽然这可以显着提升性能，但在将数据写入存储库和更新索引之间，也可能会导致延迟。 如果让查询返回100%准确结果至关重要，则需要属性索引。
* 由于异步，Lucene索引无法强制实施唯一性约束。 如果需要，则需要设置属性索引。

通常，建议您使用Lucene索引，除非迫切需要使用属性索引，这样您就可以获得更高性能和灵活性的优势。

### 索引{#solr-indexing}

AEM还默认支持Solr索引。 此功能主要用于支持全文搜索，但也可用于支持任何类型的JCR查询。 当AEM实例没有CPU容量来处理搜索密集型部署（如具有大量并发用户的搜索驱动型网站）中所需的查询数时，应考虑Solr。 或者，Solr可以采用基于爬网程序的方法来实施，以利用该平台的一些更高级的功能。

可以将Solr索引配置为在AEM服务器上嵌入用于开发环境，或将其卸载到远程实例，以提高生产和暂存环境中的搜索可扩展性。 虽然卸载搜索将提高可扩展性，但会引起延迟，因此，除非有必要，否则不建议使用。 有关如何配置Solr集成以及如何创建Solr索引的更多信息，请参阅[Oak查询和索引文档](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>而采用集成的Solr搜索方法将允许将索引卸载到Solr服务器。 如果通过基于爬网程序的方法使用Solr服务器的更高级功能，则需要额外的配置工作。 Headwire已创建[开源连接器](https://www.aemsolrsearch.com/#/)以加速这些类型的实施。

采用这种方法的缺点是，虽然在默认情况下，AEM查询将遵循ACL，从而隐藏用户无权访问的结果，但将搜索外部化到Solr服务器将不支持此功能。 如果要以这种方式将搜索外部化，则必须格外小心，以确保用户不会看到他们不应看到的结果。

如果此方法可能适合的潜在用例，则可能需要聚合来自多个源的搜索数据。 例如，您可能在AEM上托管一个网站，在第三方平台上托管另一个网站。 Solr可以配置为爬网两个站点的内容，并将它们存储在聚合索引中。 这将允许进行跨站点搜索。

### 设计注意事项{#design-considerations}

Lucene索引的Oak文档列出了在设计索引时需要注意的几个事项：

* 如果查询使用不同的路径限制，则使用`evaluatePathRestrictions`。 这将允许查询在指定的路径下返回结果的子集，然后根据查询过滤结果。 否则，查询将搜索与存储库中查询参数匹配的所有结果，然后根据路径对其进行筛选。
* 如果查询使用排序，请为sorted属性定义显式属性，并为其设置`ordered`为`true`。 这样，结果就可以在索引中按此顺序排序，并在查询执行时保存成本高昂的排序操作。

* 只把需要的东西写入索引。 添加不需要的功能或属性将导致索引增长和性能降低。
* 在属性索引中，具有唯一属性名称有助于减小索引的大小，但对于Lucene索引，应使用`nodeTypes`和`mixins`来实现内聚索引。 与查询`nt:base`相比，查询特定`nodeType`或`mixin`将更加有效。 使用此方法时，请为相关的`nodeTypes`定义`indexRules`。

* 如果您的查询仅在特定路径下运行，则在这些路径下创建这些索引。 索引不需要存放在存储库的根中。
* 当所有被索引的属性都与允许Lucene在本地评估尽可能多的属性限制相关时，建议使用单个索引。 此外，即使执行连接，查询也将只使用一个索引。

### CopyOnRead {#copyonread}

远程存储`NodeStore`时，可以启用名为`CopyOnRead`的选项。 该选项将在读取远程索引时将其写入本地文件系统。 这有助于提高通常针对这些远程索引运行的查询的性能。

这可以在OSGi控制台的&#x200B;**LuceneIndexProvider**&#x200B;服务下进行配置，默认情况下从Oak 1.0.13开始启用。

### 删除索引{#removing-indexes}

删除索引时，始终建议通过将`type`属性设置为`disabled`来临时禁用该索引，并进行测试，以确保应用程序在实际删除该索引之前能够正常运行。 请注意，索引在禁用时未更新，因此如果重新启用，并且可能需要重新编入索引，则可能没有正确的内容。

在删除TarMK实例上的属性索引后，需要运行压缩以回收任何正在使用的磁盘空间。 对于Lucene索引，实际索引内容位于BlobStore中，因此需要数据存储垃圾收集。

在MongoDB实例上删除索引时，删除成本与索引中的节点数成正比。 由于删除大索引可能会导致问题，因此建议的方法是使用诸如&#x200B;**oak-mongo.js**&#x200B;之类的工具，禁用索引并仅在维护窗口期内将其删除。 请注意，常规节点内容不应使用此方法，因为它可能会导致数据不一致。

>[!NOTE]
>
>有关oak-mongo.js的更多信息，请参阅Oak文档的[命令行工具部分](https://jackrabbit.apache.org/oak/docs/command_line.html)。

## 重新索引{#re-indexing}

本节概述了&#x200B;**仅**&#x200B;为Oak索引重新编制索引的可接受原因。

除了下面所述的原因外，启动Oak索引的重新索引将&#x200B;**不会**&#x200B;更改行为或解决问题，并且不必增加AEM的负载。

除非下表中的原因涵盖，否则应避免重新索引Oak索引。

>[!NOTE]
>
>在咨询下表以确定是否重新编制索引之前，请始终**确认：
>
>* 查询正确
>* 将查询解析为预期索引（使用[Explain Query](/help/sites-administering/operations-dashboard.md#diagnosis-tools)）
>* 索引过程已完成

>



### Oak索引配置更改{#oak-index-configuration-changes}

重新索引Oak索引的唯一可接受的非索引条件是Oak索引的配置发生了更改。

*重新编制索引时应始终适当考虑其对AEM整体性能的影响，并在活动量较低或维护时间较短的期间执行。*

以下是一些可能的问题和决议：

* [属性索引定义更改](#property-index-definition-change)
* [Lucene索引定义更改](#lucene-index-definition-change)

#### 属性索引定义更改{#property-index-definition-change}

* 适用/如果：

   * 所有Oak版本
   * 仅[属性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症状：

   * 属性索引定义更新之前存在的节点在结果中缺失

* 如何验证：

   * 确定是否在部署更新的索引定义之前创建/修改了缺失的节点。
   * 根据索引的修改时间验证任何缺失节点的`jcr:created`或`jcr:lastModified`属性

* 如何解决：

   * [重新索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene索引
   * 或者，触摸（执行良性写入操作）缺少的节点

      * 需要手动触摸或自定义代码
      * 需要已知缺少的节点集
      * 需要更改节点上的任何属性

#### Lucene索引定义更改{#lucene-index-definition-change}

* 适用/如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果
   * 查询结果不反映索引定义的预期行为
   * 查询计划不会根据索引定义报告预期输出

* 如何验证：

   * 使用Lucene索引统计信息JMX Mbean(LuceneIndex)方法`diffStoredIndexDefinition`验证索引定义是否已更改。

* 如何解决：

   * Oak 1.6之前的版本：

      * [重新索引](#how-to-re-index) lucene索引
   * Oak版本1.6+

      * 如果现有内容不受更改影响，则只需刷新

         * [](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) 通过设置oak: [queryIndexDefinition]@refresh=true来刷新lucene索引
      * 否则， [重新索引](#how-to-re-index)lucene索引

         * 注意：在触发新的重新索引之前，将使用上一个正确的重新索引（或初始索引）中的索引状态



### 异常情况{#erring-and-exceptional-situations}

下表介绍了唯一可接受的错误以及重新索引Oak索引将解决该问题的特殊情况。

如果在AEM上遇到与下面所列的条件不匹配的问题，请执行&#x200B;**not**&#x200B;重新编入任何索引的索引，因为这样不会解决该问题。

以下是一些可能的问题和决议：

* [缺少Lucene索引二进制文件](#lucene-index-binary-is-missing)
* [Lucene索引二进制文件已损坏](#lucene-index-binary-is-corrupt)

#### 缺少Lucene索引二进制文件{#lucene-index-binary-is-missing}

* 适用/如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果

* 如何验证：

   * 错误日志文件包含一个异常，表示缺少Lucene索引的二进制文件

* 如何解决：

   * 执行遍历存储库检查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍历存储库可确定是否缺少其他二进制文件（除lucene文件外）

   * 如果缺少除lucene索引之外的二进制文件，请从备份中还原
   * 否则， [重新索引](#how-to-re-index) *所有* lucene索引
   * 注意:

      此条件表示可能导致ANY二进制(例如， 缺少资产二进制文件)。

      在这种情况下，请还原到存储库的最后一个已知良好版本以恢复所有缺失的二进制文件。

#### Lucene索引二进制文件已损坏{#lucene-index-binary-is-corrupt}

* 适用/如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果

* 如何验证：

   * `AsyncIndexUpdate`（每5秒）将失败，error.log中出现异常：

      `...a Lucene index file is corrupt...`

* 如何解决：

   * 删除Lucene索引的本地副本

      1. 停止AEM
      1. 删除位于`crx-quickstart/repository/index`的lucene索引的本地副本
      1. 重新启动AEM
   * 如果这无法解决问题，并且`AsyncIndexUpdate`异常会持续存在，则：

      1. [重新索引](#how-to-re-index) 搜索索引
      1. 另请提交[Adobe支持](https://helpx.adobe.com/support.html)票证


### 如何重新编入{#how-to-re-index}索引

>[!NOTE]
>
>在AEM 6.5中，[oak-run.jar是MongoMK或RDBMK存储库上重新索引的唯一支持方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree)。

#### 重新索引属性索引{#re-indexing-property-indexes}

* 使用[oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)重新索引属性索引
* 在属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 使用Web控制台通过&#x200B;**PropertyIndexAsyncReindex** MBean异步重新编入属性索引；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene属性索引{#re-indexing-lucene-property-indexes}

* 使用[oak-run.jar重新编入](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene属性索引。
* 在lucene属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>前一部分概述了Oak在AEM上下文中[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)中的重新索引指南，并对其进行了说明。

### 二进制文件的文本预提取{#text-pre-extraction-of-binaries}

文本预提取是从二进制文件中提取和处理文本的过程，直接通过独立的流程从数据存储中提取文本，并直接将提取的文本公布到Oak索引的后续重新编/索引中。

* 建议在具有大量包含可提取文本(例如， PDF、Word文档、PPT、TXT等) 符合通过已部署的Oak索引进行全文搜索的条件；例如`/oak:index/damAssetLucene`。
* 文本预提取只会对Lucene索引的重新索引（而非Oak属性索引）有益，因为属性索引不会从二进制文件中提取文本。
* 当对文本密集型二进制文件（PDF、Doc、TXT等）进行全文重新索引时，文本预提取会产生很大的积极影响，在这种情况下，作为图像存储库，由于图像不包含可提取的文本，因此效率将不会相同。
* 文本预提取以超高效率的方式执行全文搜索相关文本的提取，并以超高效率的方式将其公开给Oak重建/索引过程。

#### 何时可以使用文本预提取？{#when-can-text-pre-extraction-be-used}

在启用二进制提取的情况下，重新索引&#x200B;**现有** lucene索引

* 重新索引处理&#x200B;**存储库中所有**&#x200B;候选内容；如果要从中提取全文的二进制文件数量众多或复杂，则对AEM而言，执行全文提取的计算负担会增加。 文本预提取将文本提取的“计算成本高的工作”移入一个可直接访问AEM Data Store的孤立进程中，从而避免AEM中的开销和资源争用。

支持在启用二进制提取的情况下将&#x200B;**new** lucene索引部署到AEM

* 在将新索引（启用了二进制提取）部署到AEM中后，Oak会在下次异步全文索引运行时自动为所有候选内容编制索引。 出于上述重新编制索引中所述的相同原因，这可能会导致AEM负载过重。

#### 何时不能使用文本预提取？{#when-can-text-pre-extraction-not-be-used}

文本预提取不能用于添加到存储库的新内容，也不必。

将新内容添加到存储库后，将自然地通过异步全文索引过程（默认情况下，每5秒）以增量方式将其索引。

在AEM的正常操作下（例如通过Web UI上传资产或以编程方式摄取资产），AEM将自动以全文方式递增地索引新的二进制内容。 由于数据量是增量的且相对较小（大约是在5秒内可保留到存储库的数据量），因此AEM可以在索引期间从二进制文件执行全文提取，而不会影响整体系统性能。

#### 使用文本预提取的先决条件{#prerequisites-to-using-text-pre-extraction}

* 您将重新为执行全文二进制提取的Lucene索引建立索引，或部署一个新索引，该索引将对现有内容的全文索引二进制文件进行索引
* 要从中预提取文本的内容（二进制文件）必须位于存储库中
* 用于生成CSV文件并执行最终重新索引的维护窗口
* Oak版本：1.0.18+,1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 用于存储从索引AEM实例访问的提取文本的文件系统文件夹/共享

   * 文本预提取OSGi配置需要一个指向提取的文本文件的文件系统路径，因此必须直接从AEM实例（本地驱动器或文件共享装载）访问这些文件

#### 如何执行文本预提取{#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下概述的oak-run.jar命令在https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html上进行了完全枚举 [。](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>上图和以下步骤用于解释和补充Apache Oak文档中概述的技术文本预提取步骤。

![文本预提取流程](assets/chlimage_1-139.png)

**生成要预提取的内容列表**

*在维护时段/低使用时段执行步骤1(a-b)，因为在此操作期间会遍历节点存储，这可能会对系统产生重大负载。*

1a。 执行`oak-run.jar --generate`以创建预先提取其文本的节点列表。

1b。 节点列表(1a)以CSV文件形式存储到文件系统中

请注意，每次执行`--generate`时，都会遍历整个节点存储区（由oak-run命令中的路径指定），并创建一个&#x200B;**新** CSV文件。 CSV文件在文本预提取流程的离散执行（步骤1 - 2）之间重复使用，它为&#x200B;**not**。

**将文本预提取到文件系统**

*如果AEM仅与数据存储交互，则在Data Store的正常操作期间可以执行步骤2(a-c)。*

2a。 执行`oak-run.jar --tika`以预提取在(1b)中生成的CSV文件中枚举的二进制节点的文本

2b。 在(2a)中启动的进程会直接访问在数据存储的CSV中定义的二进制节点，并提取文本。

2c。  提取的文本以Oak重新索引过程(3a)可接收的格式存储在文件系统中

预提取的文本在CSV中通过二进制指纹进行标识。 如果二进制文件相同，则可以在AEM实例中使用相同的预提取文本。 由于AEM发布通常是AEM创作的子集，因此从AEM创作预提取的文本通常也可用于为AEM发布重新编入索引（假定AEM发布具有对提取的文本文件的文件系统访问权限）。

预提取的文本可以随着时间的推移逐步添加到中。 文本预提取将跳过对先前提取的二进制文件的提取，因此最好保留预提取的文本，以防将来必须再次重新索引（假定提取的内容不过大）。 如果为，则在中间评估压缩内容，因为文本的压缩效果很好)。

**重新索引Oak索引，从提取的文本文件中获取全文**

*在维护/低使用期间执行重新索引（步骤3a-b），因为在此操作期间会遍历节点存储区，这可能会对系统产生重大负载。*

3a。 [在AEM](#how-to-re-index) 中调用Lucene索引的重新索引

3b。 Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi配置（配置为通过文件系统路径指向提取的文本）会指示Oak从提取的文件中获取全文，并避免直接点击和处理存储在存储库中的数据。
