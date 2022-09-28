---
title: Oak查询和索引
seo-title: Oak Queries and Indexing
description: 了解如何在AEM中配置索引。
seo-description: Learn how to configure indexes in AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b27a7a1cc2295b1640520dcb56be4f3eb4851499
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Oak查询和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文介绍如何在AEM 6中配置索引。 有关优化查询和索引性能的最佳实践，请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 简介 {#introduction}

与Jackrabbit 2不同，默认情况下，Oak不会为内容编入索引。 需要创建自定义索引（如有必要），这与使用传统关系数据库非常类似。 如果特定查询没有索引，则可能会遍历许多节点。 查询可能仍然有效，但可能非常慢。

如果Oak遇到没有索引的查询，则会打印一条“警告”级别的日志消息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支持的查询语言 {#supported-query-languages}

Oak查询引擎支持以下语言：

* XPath（推荐）
* SQL-2
* SQL（已弃用）
* JQOM

## 索引器类型和成本计算 {#indexer-types-and-cost-calculation}

基于Apache Oak的后端允许将不同的索引器插入存储库。

一个索引器是 **属性索引**，索引定义存储在存储库本身中。

实施 **Apache Lucene** 和 **索尔** 默认情况下，也可用，两者都支持全文索引。

的 **遍历索引** 如果没有其他索引器可用，则使用。 这意味着内容未编入索引，并且内容节点会经过遍历以查找与查询的匹配项。

如果一个查询有多个索引器，则每个可用索引器估计执行查询的成本。 然后，Oak以最低的估计成本选择索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上图是对Apache Oak查询执行机制的高级表示。

首先，将查询解析为抽象语法树。 然后，将查询检查并转换为SQL-2,SQL-2是Oak查询的本机语言。

接下来，将参考每个索引以估算查询的成本。 完成后，将检索最便宜指数的结果。 最后，过滤结果，以确保当前用户具有对结果的读取权限，并且结果与完整查询匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>对于大型存储库，构建索引是一项非常耗时的操作。 对于初始创建索引和重新索引（在更改定义后重建索引），都是如此。 另请参阅 [Oak索引疑难解答](/help/sites-deploying/troubleshooting-oak-indexes.md) 和 [防止慢速重新索引](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

如果在非常大的存储库中需要重新编制索引，特别是在使用MongoDB和对全文索引时，请考虑文本预提取，使用oak-run构建初始索引并重新编制索引。

索引将配置为位于 **oak:index** 节点。

索引节点的类型必须为 **oak:QueryIndexDefinition。** 每个索引器都有几个配置选项作为节点属性。 有关详细信息，请参阅下面每个索引器类型的配置详细信息。

### 属性索引 {#the-property-index}

属性索引通常适用于具有属性约束但不是全文的查询。 它可以按照以下过程进行配置：

1. 通过转到 `http://localhost:4502/crx/de/index.jsp`
1. 在下创建新节点 **oak:index**
1. 命名节点 **属性索引**，并将节点类型设置为 **oak:QueryIndexDefinition**
1. 为新节点设置以下属性：

   * **类型：**  `property` （字符串类型）
   * **propertyNames:**  `jcr:uuid` （名称类型）

   此特定示例将将 `jcr:uuid` 属性，其工作是公开其所连接节点的通用唯一标识符(UUID)。

1. 保存更改。

属性索引具有以下配置选项：

* 的 **type** 属性将指定索引的类型，在这种情况下，必须将其设置为 **属性**

* 的 **propertyNames** 属性指示将存储在索引中的属性列表。 如果缺少该值，则节点名称将用作属性名称引用值。 在本例中， **jcr:uuid** 其作业是显示其节点的唯一标识符(UUID)的属性会添加到索引中。

* 的 **独特** 标记其中，如果设置为 **true** 对属性索引添加唯一性约束。

* 的 **声明NodeTypes** 属性允许您指定索引将仅应用于的特定节点类型。
* 的 **重新索引** 标记如果设置为 **true**，将触发完整内容的重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是属性索引的扩展。 但是，它已被弃用。 此类型的索引需要替换为 [Lucene属性索引](#the-lucene-property-index).

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6中提供了基于Apache Lucene的全文索引器。

如果配置了全文索引，则所有具有全文条件的查询都使用全文索引，无论是否有其他条件已编入索引，也无论是否存在路径限制。

如果未配置全文索引，则包含全文条件的查询将无法按预期工作。

由于索引是通过异步后台线程更新的，因此在后台进程完成之前，某些全文搜索在一段较短的时间内将不可用。

您可以按照以下步骤配置Lucene全文索引：

1. 打开CRXDE并在下创建新节点 **oak:index**.
1. 命名节点 **LuceneIndex** 并将节点类型设置为 **oak:QueryIndexDefinition**
1. 将以下属性添加到节点：

   * **类型：**  `lucene` （字符串类型）
   * **异步：**  `async` （字符串类型）

1. 保存更改。

Lucene索引具有以下配置选项：

* 的 **type** 将指定索引类型的属性必须设置为 **绿色**
* 的 **异步** 必须设置为的属性 **异步**. 这会将索引更新过程发送到后台线程。
* 的 **includePropertyTypes** 属性，该属性将定义索引中将包含的属性类型子集。
* 的 **excludePropertyNames** 属性，该属性将定义属性名称列表 — 应从索引中排除的属性。
* 的 **重新索引** 标记当设置为 **true**，则会触发完整内容重新索引。

### Lucene属性索引 {#the-lucene-property-index}

自 **Oak 1.0.8**，则Lucene可用于创建包含非全文属性约束的索引。

为了实现Lucene属性索引， **fulltextEnabled** 属性必须始终设置为false。

以下查询示例为例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

为了为上述查询定义Lucene属性索引，您可以通过在 **oak:index:**

* **名称:** `LucenePropertyIndex`
* **类型:** `oak:QueryIndexDefinition`

创建节点后，添加以下属性：

* **类型:**

   ```xml
   lucene (of type String)
   ```

* **异步:**

   ```xml
   async (of type String)
   ```

* **fulltextEnabled:**

   ```xml
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>与常规属性索引相比，Lucene属性索引始终在异步模式下配置。 因此，索引返回的结果可能并不总是反映存储库的最新状态。

>[!NOTE]
>
>有关Lucene属性索引的更多具体信息，请参阅 [Apache Jackrabbit Oak Lucene文档页](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene分析程序 {#lucene-analyzers}

自版本1.2.0起，Oak支持Lucene分析程序。

在文档编入索引时和在查询时都使用分析程序。 分析器检查字段文本并生成令牌流。 Lucene分析器由一系列标记器和过滤器类组成。

分析程序可通过 `analyzers` 节点（类型） `nt:unstructured`) `oak:index` 定义。

索引的默认分析器在 `default` 分析程序节点的子项。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>有关可用分析程序的列表，请查阅您所使用的Lucene版本的API文档。

#### 直接指定分析器类 {#specifying-the-analyzer-class-directly}

如果您希望使用任何现成的分析器，可以按照以下过程对其进行配置：

1. 在 `oak:index` 节点。

1. 在索引下，创建一个名为 `default` 类型 `nt:unstructured`.

1. 将具有以下属性的属性添加到默认节点：

   * **名称:** `class`
   * **类型:** `String`
   * **值：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   该值是您希望使用的分析器类的名称。

   您还可以使用可选的 `luceneMatchVersion` 字符串属性。 在Lucene 4.7中使用它的有效合成酶是：

   * **名称:** `luceneMatchVersion`
   * **类型:** `String`
   * **值：** `LUCENE_47`

   如果 `luceneMatchVersion` 未提供，Oak将使用随附的Lucene版本。

1. 如果要向分析器配置添加秒表文件，则可以在 `default` 一个具有以下属性：

   * **名称:** `stopwords`
   * **类型:** `nt:file`

#### 通过合成创建分析程序 {#creating-analyzers-via-composition}

分析器也可以基于 `Tokenizers`, `TokenFilters` 和 `CharFilters`. 为此，您可以指定一个分析器，并创建其可选令牌和过滤器的子节点，这些节点将按列表顺序应用。 另请参阅 [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以此节点结构为例：

* **名称:** `analyzers`

   * **名称:** `default`

      * **名称:** `charFilters`
      * **类型:** `nt:unstructured`

         * **名称:** `HTMLStrip`
         * **名称:** `Mapping`
      * **名称:** `tokenizer`

         * **属性名称:** `name`

            * **类型:** `String`
            * **值：** `Standard`
      * **名称:** `filters`
      * **类型:** `nt:unstructured`

         * **名称:** `LowerCase`
         * **名称:** `Stop`

            * **属性名称:** `words`

               * **类型:** `String`
               * **值：** `stop1.txt, stop2.txt`
            * **名称:** `stop1.txt`

               * **类型:** `nt:file`
            * **名称:** `stop2.txt`

               * **类型:** `nt:file`





过滤器、charFilters和令牌器的名称通过删除工厂后缀来形成。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 变量 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 变量 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 变量 `Stop`

工厂所需的任何配置参数都指定为相关代码的属性。

对于诸如需要加载来自外部文件的内容的停止词之类的情况，可以通过创建的子节点来提供内容 `nt:file` 键入相关文件。

### 索尔指数 {#the-solr-index}

索尔索引的目的主要是全文搜索，但也可以用于按路径、属性限制和主要类型限制进行索引搜索。 这意味着Oak中的Solr索引可用于任何类型的JCR查询。

AEM中的集成在存储库级别进行，因此Solr是可在Oak中使用的索引之一，Oak是AEM附带的新存储库实施。

它可以配置为与AEM实例一起作为远程服务器使用。

### 使用单个远程Solr服务器配置AEM {#configuring-aem-with-a-single-remote-solr-server}

AEM还可以配置为与远程Solr服务器实例一起使用：

1. 下载并提取最新版本的Solr。 有关如何执行此操作的更多信息，请参阅 [Apache Solr安装文档](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. 现在，创建两个索尔碎片。 为此，您可以在Solr已解压的文件夹中为每个共享创建文件夹：

   * 对于第一个共享，创建文件夹：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 对于第二个共享，创建文件夹：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr包中找到示例实例。 它通常位于名为“ `example`”。
1. 将以下文件夹从示例实例复制到两个共享文件夹( `aemsolr1\node1` 和 `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 创建一个名为“ `cfg`”。
1. 将您的Solr和Zookeeper配置文件放置在新创建的 `cfg` 文件夹。

   >[!NOTE]
   >
   >有关Solr和ZooKeeper配置的更多信息，请参阅 [解决方案配置文档](https://wiki.apache.org/solr/ConfiguringSolr) 和 [ZooKeeper快速入门指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 在ZooKeeper支持下，通过访问 `aemsolr1\node1` 和运行以下命令：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 通过转到 `aemsolr2\node2` 和运行以下命令：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 启动这两个分片后，通过连接Solr界面(位于 `http://localhost:8983/solr/#/`
1. 启动AEM，然后转到Web控制台(位于 `http://localhost:4502/system/console/configMgr`
1. 在 **Oak Solr远程服务器配置**:

   * 解决方案HTTP URL: `http://localhost:8983/solr/`

1. 选择 **远程解决方案** 在下面的下拉列表中 **奥克索尔** 服务器提供程序。

1. 转到CRXDE并以管理员身份登录。
1. 创建一个名为 **solrIndex** 在 **oak:index**，并设置以下属性：

   * **类型：** solr（字符串类型）
   * **异步：** async（字符串类型）
   * **重新索引：** true（布尔类型）

1. 保存更改。

#### 推荐的Solr配置 {#recommended-configuration-for-solr}

以下是基本配置示例，该示例可用于本文中描述的所有三个Solr部署。 它包含AEM中已存在且不应与其他应用程序一起使用的专用属性索引。

要正确使用它，您需要将存档的内容直接放入Solr Home Directory中。 对于多节点部署，它应直接位于每个节点的根文件夹下。

推荐的Solr配置文件

[获取文件](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1还集成了AEM 6.0中存在的两个索引工具，作为Adobe咨询服务共用工具集的一部分：

1. **解释查询**，该工具旨在帮助管理员了解查询的执行方式；
1. **Oak索引管理器**，用于维护现有索引的Web用户界面。

现在，您可以通过 **工具 — 操作 — 功能板 — 诊断** 从AEM欢迎屏幕中。

有关如何使用这些源代码的更多信息，请参阅 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

#### 通过OSGi创建属性索引 {#creating-property-indexes-via-osgi}

ACS Commons包还公开了可用于创建属性索引的OSGi配置。

您可以通过搜索“**确保Oak属性索引**&quot;

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引问题疑难解答 {#troubleshooting-indexing-issues}

出现查询执行时间较长，且一般系统响应时间较慢的情况。

本节就需要采取哪些措施来跟踪这些问题的原因提出一系列建议，并就如何解决这些问题提出建议。

#### 准备用于分析的调试信息 {#preparing-debugging-info-for-analysis}

获取正在执行的查询所需信息的最简单方法是通过 [解释查询工具](/help/sites-administering/operations-dashboard.md#explain-query). 这样，您就可以收集调试慢速查询所需的准确信息，而无需查阅日志级别信息。 如果您知道正在调试的查询，则此操作是理想的。

如果由于任何原因无法实现此目的，您可以将索引日志收集到单个文件中，并使用它来解决您的特定问题。

#### 启用日志记录 {#enable-logging}

要启用日志记录，您需要启用 **调试** 与Oak索引和查询相关的类别的级别日志。 这些类别包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

的 **com.day.cq.search** 类别仅在您使用AEM提供的QueryBuilder实用程序时才适用。

>[!NOTE]
>
>在执行要进行故障诊断的查询的过程中，日志只设置为DEBUG，这一点很重要，否则日志中会随着时间的推移生成大量事件。 因此，在收集到所需日志后，会针对上述类别切换回信息级别日志记录。

您可以通过以下过程启用日志记录：

1. 将您的浏览器指向 `https://serveraddress:port/system/console/slinglog`
1. 单击 **添加新的日志记录器** 按钮。
1. 在新创建的行中，添加上述类别。 您可以使用 **+** 登录以向单个日志记录器添加多个类别。
1. 选择 **调试** 从 **日志级别** 下拉列表。
1. 将输出文件设置为 `logs/queryDebug.log`. 这会将所有调试事件关联到单个日志文件中。
1. 运行查询或渲染使用要调试的查询的页面。
1. 执行查询后，返回到日志记录控制台，并将新创建的日志记录器的日志级别更改为 **信息**.

#### 索引配置 {#index-configuration}

查询的评估方式在很大程度上受索引配置的影响。 获取索引配置以便进行分析或发送给支持非常重要。 您可以作为内容包获取配置，也可以获取JSON呈现版本。

由于在大多数情况下，索引配置存储在 `/oak:index` 节点中，您可以在以下位置获取JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引配置在其他位置，请相应地更改路径。

#### MBean输出 {#mbean-output}

在某些情况下，提供与索引相关的MBean的输出以进行调试会很有帮助。 您可以执行以下操作来实现此目标：

1. 转到JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean:

   * Lucene索引统计
   * CopyOnRead支持统计信息
   * Oak查询统计信息
   * IndexStats

1. 单击每个MBean以获取性能统计信息。 创建屏幕截图或记下它们，以备需要提交支持。

您还可以通过以下URL获取这些统计信息的JSON变体：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您还可以通过 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. 这将包含JSON格式的所有与Oak相关的MBean详细信息。

#### 其他详细信息 {#other-details}

您可以收集其他详细信息以帮助解决问题，例如：

1. 您的实例运行的Oak版本。 您可以通过打开CRXDE并查看欢迎页面右下角的版本，或检查 `org.apache.jackrabbit.oak-core` 捆绑。
1. 麻烦查询的QueryBuilder Debugger输出。 调试器可在以下位置访问： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
