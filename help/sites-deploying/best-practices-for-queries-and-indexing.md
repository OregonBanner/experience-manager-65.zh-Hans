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
workflow-type: tm+mt
source-wordcount: '4618'
ht-degree: 0%

---


# 查询和索引的最佳实践{#best-practices-for-queries-and-indexing}

与在AEM 6公司对Oak公司的过渡一样，对查询和索引的管理方式进行了一些重大改变。 在Jackrabbit 2下，默认情况下所有内容都已编制索引，并可以自由查询。 在Oak中，必须在`oak:index`节点下手动创建索引。 查询可以在没有索引的情况下执行，但对于大数据集，执行速度会非常慢，甚至会中止。

本文将概述何时以及何时不需要索引、避免在不需要查询时使用索引的技巧以及优化索引和查询以尽可能优化执行的技巧。

此外，请务必阅读[关于编写查询和索引](/help/sites-deploying/queries-and-indexing.md)的Oak文档。 除了索引是AEM 6中的一个新概念之外，Oak查询中还存在语法差异，在从以前的AEM安装迁移代码时，需要考虑这些差异。

## 何时使用查询{#when-to-use-queries}

### 存储库和分类设计{#repository-and-taxonomy-design}

在设计存储库的分类时，需要考虑几个因素。 这些属性包括访问控制、本地化、组件和页面属性继承等。

在设计能够解决这些问题的分类时，还必须考虑索引设计的“可遍历性”。 在此上下文中，可遍历性是一种分类功能，它允许根据内容的路径进行可预测的访问。 这样可以实现比需要执行大量查询的系统更易于维护的性能更高的系统。

此外，在设计分类时，务必考虑排序是否重要。 如果不需要显式排序并且需要大量同级节点，则最好使用未排序的节点类型，如`sling:Folder`或`oak:Unstructured`。 如果需要订购，则`nt:unstructured`和`sling:OrderedFolder`更合适。

### 组件{#queries-in-components}中的查询

由于查询可能是在AEM系统上执行的较繁琐的操作之一，因此最好在组件中避免使用它们。 每次呈现页面时执行多个查询通常会降低系统性能。 呈现组件时，有两种策略可用于避免执行查询:**遍历节点**&#x200B;和&#x200B;**预取结果**。

#### 遍历节点{#traversing-nodes}

如果存储库的设计方式允许事先知道所需数据的位置，则可以部署从必要路径检索此数据的代码，而不必运行查询才能找到它。

一个例子是渲染适合特定类别的内容。 一种方法是使用类别属性组织内容，该属性可进行查询以填充显示类别中项目的组件。

更好的方法是按类别在分类中构建此内容，以便手动检索它。

例如，如果内容存储在类似于以下内容的分类中：

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

可以简单地检索`/content/myUnstructuredContent/parentCategory/childCategory`节点，可以分析其子节点并使用其呈现组件。

此外，当您处理小的或同质的结果集时，可以更快地遍历存储库并收集所需的节点，而不是制作查询以返回相同的结果集。 作为一般考虑，在可能的情况下应避免查询。

#### 预取结果{#prefetching-results}

有时，组件周围的内容或要求将不允许使用节点遍历作为检索所需数据的方法。 在这些情况下，需要在渲染组件之前执行所需的查询，以确保最终用户的最佳性能。

如果创作组件时可以计算所需的结果并且内容没有更改的预期值，则当作者在对话框中应用设置时可以执行查询。

如果查询或内容会定期更改，则可以在计划上或通过监听器执行该以更新基础数据。 然后，结果可写入存储库中的共享位置。 任何需要此数据的组件随后都可以从此单个节点提取值，而无需在运行时执行查询。

## 查询优化{#query-optimization}

运行未使用索引的查询时，将记录有关节点遍历的警告。 如果这是将经常运行的查询，则应创建索引。 要确定给定查询使用的索引，建议使用[解释查询工具](/help/sites-administering/operations-dashboard.md#explain-query)。 有关详细信息，可以为相关搜索API启用DEBUG日志记录。

>[!NOTE]
>
>修改索引定义后，需要重新构建（重新索引）索引。 根据索引的大小，可能需要一些时间才能完成此操作。

在运行复杂查询时，可能会有这样的情况：将查询分解为多个较小的查询，并在事实性能更高后通过代码连接数据。 这些情况的建议是比较两种方法的绩效，以确定哪种方法更适合所述用例。

AEM允许通过以下三种方式编写查询:

* 通过[QueryBuilder API](/help/sites-developing/querybuilder-api.md)（建议）
* 使用XPath（建议）
* 使用SQL2

虽然所有查询在运行前都转换为SQL2，但查询转换的开销很小，因此，选择查询语时最关心的问题是开发团队的可读性和舒适性。

>[!NOTE]
>
>使用QueryBuilder时，它将确定默认的结果计数，与Jackrabbit的先前版本相比，Oak中的结果计数较慢。 要弥补这一缺陷，可使用[guessTotal参数](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results)。

### 说明查询工具{#the-explain-query-tool}

与任何查询语言一样，优化查询的第一步是了解如何执行该语言。 要启用此活动，可以使用作为“操作”仪表板的一部分的[解释查询工具](/help/sites-administering/operations-dashboard.md#explain-query)。 使用此工具，可插入并解释查询。 如果查询将导致大型存储库以及执行时间和将使用的索引出现问题，将显示警告。 该工具还可以加载一列表慢速和流行的查询，然后可以解释和优化这些数据。

### 查询{#debug-logging-for-queries}的调试日志记录

要获取有关Oak如何选择要使用的索引以及查询引擎如何实际执行查询的其他信息，可以为以下包添加&#x200B;**DEBUG**&#x200B;日志记录配置：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

确保在调试完查询后删除此记录器，因为它将输出大量活动并最终会用日志文件填满您的磁盘。

有关如何执行此操作的详细信息，请参阅[日志记录文档](/help/sites-deploying/configure-logging.md)。

### 索引统计数据{#index-statistics}

Lucene注册一个JMX Bean，它提供有关索引内容的详细信息，包括每个索引中存在的文档的大小和数量。

您可以通过访问位于`https://server:port/system/console/jmx`的JMX控制台来访问它

登录JMX控制台后，请执行搜索&#x200B;**Lucene索引统计信息**&#x200B;以找到它。 其他索引统计信息可在&#x200B;**IndexStats** MBean中找到。

对于查询统计信息，请查看名为&#x200B;**Oak查询统计信息**&#x200B;的MBean。

如果要使用[Luke](https://code.google.com/p/luke/)等工具挖掘索引，您需要使用Oak控制台将索引从`NodeStore`转储到文件系统目录。 有关如何执行此操作的说明，请阅读[Lucene文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

您还可以以JSON格式提取系统中的索引。 为此，您需要访问`https://server:port/oak:index.tidy.-1.json`

### 查询限制 {#query-limits}

**在开发过程中**

为`oak.queryLimitInMemory`设置低阈值(如 10000)和橡木。 `queryLimitReads` (例如5000)，并在点击UnsupportedOperationException时优化昂贵的查询，说“查询读取的节点数超过x节点……”

这有助于避免资源密集型查询(即 不受任何索引或覆盖索引较少支持)。 例如，读取100万个节点的查询会导致I/O的增加，并对应用程序的整体性能产生负面影响。 任何因超出限制而失败的查询应进行分析和优化。

#### **部署后** {#post-deployment}

* 监视日志，以查看触发大节点遍历或大堆内存消耗的查询:&quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * 优化查询以减少遍历的节点数

* 监视日志，以查看触发大堆内存消耗的查询:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * 优化查询以减少堆内存消耗

对于AEM 6.0 - 6.2版本，可以通过AEM开始脚本中的JVM参数调整节点遍历的阈值，以防止大查询过载环境。

建议的值为：

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

在AEM 6.3中，上述2个参数是预配置的OOTB，并可通过OSGi QueryEngineSettings进行保留。

更多信息可在以下位置获取：[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## 创建有效索引的提示{#tips-for-creating-efficient-indexes}

### 我应该创建索引吗？{#should-i-create-an-index}

创建或优化索引时要问的第一个问题是，是否确实需要索引才能满足特定情况。 如果您只要通过批处理在系统非高峰时间运行问题查询一次或仅偶尔运行，则最好不要创建索引。

创建索引后，每次更新索引数据时，索引也必须更新。 由于这会对系统产生性能影响，因此仅应在实际需要索引时才创建索引。

此外，只有在索引中包含的数据足够唯一以保证其安全时，索引才有用。 请考虑书籍中的索引及其所涵盖的主题。 在为文本中的一组主题建立索引时，通常会有成百上千的条目，这样您就可以快速跳转到页面的子集，以快速找到您要查找的信息。 如果该索引只有两三个条目，每个条目指向几百个页面，则该索引将不太有用。 这一概念同样适用于数据库索引。 如果只有两个唯一值，则索引将不会很有用。 话虽如此，一个指数也变得太大而无用。 要查看索引统计信息，请参阅上面的[索引统计信息](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics)。

### Lucene或属性索引？{#lucene-or-property-indexes}

Lucene索引在Oak 1.0.9中引入，并对AEM 6最初发布时引入的属性索引进行了一些强大的优化优惠。 在决定是使用Lucene索引还是属性索引时，请考虑以下因素：

* Lucene索引优惠的功能比属性索引多。 例如，属性索引只能索引单个属性，而Lucene索引可以包含许多属性。 有关Lucene索引中可用的所有功能的详细信息，请查阅[文档](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。
* Lucene索引是异步的。 虽然这优惠了显着的性能提升，但它也会在将数据写入存储库和更新索引之间产生延迟。 如果让查询返回100%准确结果至关重要，那么就需要一个属性指数。
* 由于异步，Lucene索引无法强制实施唯一性约束。 如果需要，则需要设置属性索引。

通常，建议您使用Lucene索引，除非迫切需要使用属性索引，这样您就可以获得更高的性能和灵活性的优势。

### 索尔索引{#solr-indexing}

默认情况下，AEM还支持Solr索引。 这主要用于支持全文搜索，但也可用于支持任何类型的JCR查询。 当AEM实例没有CPU容量来处理搜索密集型部署（如同时拥有大量用户的搜索驱动型网站）所需的查询数时，应考虑Solr。 或者，Solr可以在基于爬虫的方法中实现，以利用该平台的一些更高级的特性。

可以将Solr索引配置为运行嵌入在AEM服务器上以用于开发环境，也可以将索引卸载到远程实例，以提高生产和分阶环境上的搜索可伸缩性。 虽然卸载搜索可提高可伸缩性，但会引入延迟，因此除非需要，否则不建议这样做。 有关如何配置Solr集成以及如何创建Solr索引的详细信息，请参阅[Oak查询和索引文档](/help/sites-deploying/queries-and-indexing.md#the-solr-index)。

>[!NOTE]
>
>而采用集成的Solr搜索方法将允许将索引卸载到Solr服务器。 如果通过基于Crawler的方法使用Solr服务器的更高级功能，则需要额外的配置工作。 Headwire已创建了[开放源连接器](https://www.aemsolrsearch.com/#/)以加速这些类型的实现。

采用这种方法的缺点是，尽管默认情况下，AEM查询会遵守ACL，从而隐藏用户无权访问的结果，将搜索外部化到Solr服务器将不支持此功能。 如果要以这种方式将搜索外部化，则必须格外小心，以确保用户不会看到他们不应看到的结果。

如果此方法可能适合的潜在使用情形，则可能需要聚集来自多个来源的搜索数据。 例如，您可能有一个托管在AEM上的站点，另一个托管在第三方平台上的站点。 Solr可以配置为爬网两个站点的内容并将它们存储在聚合索引中。 这将允许跨站点搜索。

### 设计注意事项{#design-considerations}

Lucene索引的Oak文档列表了设计索引时要考虑的几个因素：

* 如果查询使用不同的路径限制，则使用`evaluatePathRestrictions`。 这将允许查询返回指定路径下的结果子集，然后根据查询筛选结果。 否则，查询将搜索与存储库中的查询参数匹配的所有结果，然后根据路径筛选这些结果。
* 如果查询使用排序，则为sorted属性定义显式属性，并将其设置为`ordered`为`true`。 这将允许结果在索引中按此顺序排序，并在查询执行时节省代价高昂的排序操作。

* 只将所需内容放入索引中。 添加不需要的功能或属性将导致索引增长并降低性能。
* 在属性索引中，具有唯一属性名称有助于减小索引的大小，但对于Lucene索引，应使用`nodeTypes`和`mixins`来实现内聚索引。 查询特定`nodeType`或`mixin`比查询`nt:base`更有效。 使用此方法时，请为相关的`nodeTypes`定义`indexRules`。

* 如果查询仅在某些路径下运行，则在这些路径下创建这些索引。 索引不必存在于存储库的根中。
* 建议在所有被索引的属性都相关时使用单个索引，以允许Lucene在本机评估尽可能多的属性限制。 此外，查询将仅使用一个索引，即使执行连接时也是如此。

### CopyOnRead {#copyonread}

在远程存储`NodeStore`的情况下，可以启用名为`CopyOnRead`的选项。 此选项将在读取远程索引时将其写入本地文件系统。 这有助于提高通常针对这些远程索引运行的查询的性能。

可以在OSGi控制台的&#x200B;**LuceneIndexProvider**&#x200B;服务下配置，默认情况下从Oak 1.0.13开始启用。

### 删除索引{#removing-indexes}

删除索引时，始终建议将`type`属性设置为`disabled`以临时禁用索引，并进行测试以确保应用程序在实际删除之前能够正确运行。 请注意，索引在禁用时不会更新，因此，如果重新启用并且可能需要重新编制索引，则它可能没有正确的内容。

在删除TarMK实例上的属性索引后，需要运行压缩以回收正在使用的任何磁盘空间。 对于Lucene索引，实际索引内容位于BlobStore中，因此需要数据存储垃圾收集。

删除MongoDB实例上的索引时，删除成本与索引中的节点数成比例。 由于删除大索引可能会导致问题，建议的方法是使用&#x200B;**oak-mongo.js**&#x200B;等工具禁用索引并仅在维护窗口期删除它。 请注意，此方法不应用于常规节点内容，因为它可能会导致数据不一致。

>[!NOTE]
>
>有关oak-mongo.js的详细信息，请参阅Oak文档的[命令行工具部分](https://jackrabbit.apache.org/oak/docs/command_line.html)。

## 重新建立索引{#re-indexing}

本节概述了&#x200B;**仅**&#x200B;为Oak索引重新编制索引的可接受理由。

在下述原因之外，启动Oak索引的重新索引将&#x200B;**不会改变行为或解决问题，并且不必增加AEM的负载。**

除非下表中有原因，否则应避免对Oak索引重新编制索引。

>[!NOTE]
>
>在咨询下表以确定重新编制索引是否有用之前，**始终**验证：
>
>* 查询正确
>* 查询解析为预期索引(使用[解释查询](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* 索引过程已完成

>



### Oak索引配置更改{#oak-index-configuration-changes}

重新索引Oak索引的唯一可接受的非重新索引条件是Oak索引的配置已经更改。

*应始终适当考虑重新索引对AEM总体性能的影响，并在活动或维护时间较短时执行。*

下面详细列出了可能的问题和决议：

* [属性索引定义更改](#property-index-definition-change)
* [Lucene索引定义更改](#lucene-index-definition-change)

#### 属性索引定义更改{#property-index-definition-change}

* 适用／如果：

   * 所有Oak版本
   * 仅[属性索引](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* 症状：

   * 属性索引定义更新之前存在的节点在结果中缺失

* 如何验证：

   * 确定在部署更新的索引定义之前是否创建／修改了缺失的节点。
   * 根据索引的修改时间验证任何缺失节点的`jcr:created`或`jcr:lastModified`属性

* 如何解决：

   * [重新索引](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) lucene指数
   * 或者，对缺少的节点进行触摸（执行良性写入操作）

      * 需要手动触摸或自定义代码
      * 需要已知缺少的节点集
      * 需要更改节点上的任何属性

#### Lucene索引定义更改{#lucene-index-definition-change}

* 适用／如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果
   * 查询结果不反映索引定义的预期行为
   * 查询计划不根据索引定义报告预期输出

* 如何验证：

   * 使用Lucene索引统计信息JMX Mbean(LuceneIndex)方法`diffStoredIndexDefinition`验证索引定义是否已更改。

* 如何解决：

   * Oak 1.6之前的版本：

      * [重新索引](#how-to-re-index) lucene指数
   * Oak版本1.6+

      * 如果现有内容不受更改影响，则只需刷新

         * [通](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) 过设置oak:queryIndexDefinition []@refresh=true刷新lucene索引
      * 否则，[重新索引](#how-to-re-index)lucene索引

         * 注意：在触发新的重新索引之前，将使用上次正确索引（或初始索引）的索引状态



### 错误和特殊情况{#erring-and-exceptional-situations}

下表描述了重新索引Oak索引将解决该问题的唯一可接受的错误和特殊情况。

如果AEM上遇到的问题与下面列出的条件不匹配，请执行&#x200B;**not**&#x200B;重新索引任何索引，因为它不会解决该问题。

下面详细列出了可能的问题和决议：

* [缺少Lucene索引二进制](#lucene-index-binary-is-missing)
* [Lucene索引二进制文件已损坏](#lucene-index-binary-is-corrupt)

#### Lucene索引二进制文件缺失{#lucene-index-binary-is-missing}

* 适用／如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果

* 如何验证：

   * 错误日志文件包含一个异常，表示缺少Lucene索引的二进制文件

* 如何解决：

   * 执行遍历库检查；例如：

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      遍历存储库可确定是否缺少其他二进制文件（除lucene文件外）

   * 如果缺少lucene索引以外的二进制文件，则从备份中恢复
   * 否则，[重新索引](#how-to-re-index) *所有* lucene索引
   * 注意:

      此条件表示可能导致ANY二进制(如 资源二进制文件)。

      在这种情况下，请恢复到存储库的上一个已知良好的版本以恢复所有缺失的二进制文件。

#### Lucene索引二进制文件已损坏{#lucene-index-binary-is-corrupt}

* 适用／如果：

   * 所有Oak版本
   * 仅[lucene索引](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* 症状：

   * Lucene索引不包含预期结果

* 如何验证：

   * `AsyncIndexUpdate`（每5秒）将失败，error.log中出现异常：

      `...a Lucene index file is corrupt...`

* 如何解决：

   * 删除lucene索引的本地副本

      1. 停止AEM
      1. 删除位于`crx-quickstart/repository/index`的lucene索引的本地副本
      1. 重新启动AEM
   * 如果这无法解决问题，且`AsyncIndexUpdate`异常仍然存在，则：

      1. [重新](#how-to-re-index) 索引索引
      1. 另请提交[Adobe支持](https://helpx.adobe.com/support.html)票证


### 如何重新索引{#how-to-re-index}

>[!NOTE]
>
>在AEM 6.5中，[oak-run.jar是ONLY支持的方法](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree)，用于在MongoMK或RDBMK存储库上重新建立索引。

#### 重新索引属性索引{#re-indexing-property-indexes}

* 使用[oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing)重新索引属性索引
* 在属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

* 通过&#x200B;**PropertyIndexAsyncReindex** MBean，使用Web控制台异步重新索引属性索引；

   例如，

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### 重新索引Lucene属性索引{#re-indexing-lucene-property-indexes}

* 使用[oak-run.jar重新索引](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) Lucene属性索引。
* 在lucene属性索引上将async-reindex属性设置为true

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>前一节总结并描述AEM上下文中[Apache Oak文档](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)中的Oak重新索引指南。

### 二进制文本预提取{#text-pre-extraction-of-binaries}

文本预提取是从二进制文件中提取和处理文本的过程，直接通过一个独立的过程从数据存储中提取文本，并直接将提取的文本呈现给Oak索引的后续重新编制／索引。

* 建议使用Oak文本预提取来重新／索引具有大量文件（二进制文件）的存储库上的Lucene索引，这些文件包含可提取的文本(例如， PDF、Word Docs、PPT、TXT等) 通过部署的Oak索引进行全文搜索；例如`/oak:index/damAssetLucene`。
* 文本预提取将只有利于Lucene索引的重新／索引，而不有利于Oak属性索引，因为属性索引不会从二进制文件中提取文本。
* 当重文本二进制文件（PDF、Doc、TXT等）的全文重新索引时，文本预提取会产生很大的积极影响，因为作为图像存储库，由于图像不包含可提取的文本，因此效率不会相同。
* 文本预提取以一种特效的方式执行全文搜索相关文本的提取，并以一种特效的消费方式将其呈现给Oak重新／索引过程。

#### 何时使用CAN文本预提取?{#when-can-text-pre-extraction-be-used}

在启用二进制提取的情况下重新索引&#x200B;**现有** lucene索引

* 重新索引处理存储库中的&#x200B;**所有**&#x200B;候选内容；当要从中提取全文的二进制文件数量众多或复杂时，执行全文提取的计算负担将增加到AEM上。 文本预提取将文本提取的“计算成本高的工作”移入一个隔离的过程，该过程直接访问AEM数据存储，避免了AEM中的开销和资源争用。

支持将&#x200B;**new** lucene索引部署到启用二进制提取的AEM

* 在AEM中部署新索引(启用二进制提取)后，Oak会在下次运行异步全文索引时自动为所有候选内容建立索引。 由于上述重新编制索引中所述的相同原因，这可能导致AEM负载过重。

#### 何时不能使用文本预提取?{#when-can-text-pre-extraction-not-be-used}

文本预提取不能用于添加到存储库的新内容，也不必使用。

将新内容添加到存储库后，将通过异步全文索引过程（默认情况下，每5秒）自然地以增量方式为新内容编制索引。

在AEM的正常操作下（例如，通过Web UI上传资产或以编程方式收集资产）,AEM将自动以增量方式为新的二进制内容建立全文索引。 由于数据量是增量的且相对较小（大约是5秒后可保留到存储库的数据量）,AEM可以在索引过程中从二进制文件执行全文提取，而不会影响总体系统性能。

#### 使用文本预提取{#prerequisites-to-using-text-pre-extraction}的先决条件

* 您将重新为执行全文二进制提取的lucene索引建立索引，或部署将现有内容的全文索引二进制文件的新索引
* 要从中预提取文本的内容（二进制文件）必须位于存储库中
* 用于生成CSV文件并执行最终重新索引的维护窗口
* Oak版本：1.0.18+,1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* 用于存储从索引AEM实例访问的提取文本的文件系统文件夹／共享

   * 文本预提取OSGi配置需要解压文本文件的文件系统路径，因此必须直接从AEM实例（本地驱动器或文件共享装载）访问它们

#### 如何执行文本预提取{#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***以下概述的oak-run.jar命令在https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html上完全枚举 [。](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>以上示意图和以下步骤用于说明和补充Apache Oak文档中概述的技术文本预提取步骤。

![文本预提取流程](assets/chlimage_1-139.png)

**生成要预提取的内容列表**

*在维护窗口／低使用期间执行步骤1(a-b)，因为在此操作期间会遍历节点存储，这可能会对系统产生重大负载。*

1a。 执行`oak-run.jar --generate`以创建预提取其文本的节点列表。

1b。 节点列表(1a)作为CSV文件存储到文件系统

请注意，每次执行`--generate`时，都会遍历整个节点存储区（如oak-run命令中的路径所指定），并创建一个&#x200B;**new** CSV文件。 CSV文件&#x200B;**不**&#x200B;在文本预提取过程的离散执行之间重新使用（步骤1 - 2）。

**将文本预提取到文件系统**

*步骤2(a-c)可在AEM的正常操作期间执行，因为它只与数据存储交互。*

2a。 执行`oak-run.jar --tika`以预提取在(1b)中生成的CSV文件中枚举的二进制节点的文本

2b。 在(2a)中启动的进程直接访问在数据存储中的CSV中定义的二进制节点，并提取文本。

2c  提取的文本以Oak重新索引过程(3a)可接受的格式存储在文件系统中

预提取的文本在CSV中通过二进制指纹进行标识。 如果二进制文件相同，则可以跨AEM实例使用相同的预提取文本。 由于AEM发布通常是AEM作者的子集，因此从AEM作者预提取的文本通常也可以用于重新索引AEM发布（假定AEM发布具有对提取的文本文件的文件系统访问权限）。

预提取的文本可以随时间递增地添加到其中。 文本预提取将跳过先前提取的二进制文件的提取，因此最好保留预提取的文本，以防将来必须再次重新索引（假定提取的内容不过大）。 如果是，则评估在中间压缩内容，因为文本压缩良好)。

**重新为Oak索引编制索引，从提取的文本文件获取全文**

*在维护／低使用期间执行重新索引（步骤3a-b），因为在此操作期间会遍历节点存储，这可能会对系统产生重大负载。*

3a。 [在AEM中](#how-to-re-index) 调用Lucene索引的重新索引

3b。 Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi配置（配置为通过文件系统路径指向“提取的文本”）指示Oak从“提取的文件”中采集全文文本，并避免直接访问和处理存储在存储库中的数据。

