---
title: Oak查询和索引
description: 了解如何在AEM中配置索引。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# Oak查询和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文介绍了如何在AEM 6中配置索引。 有关优化查询和索引性能的最佳实践，请参阅 [有关查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## 简介 {#introduction}

与Jackrabbit 2不同，默认情况下，Oak不索引内容。 必要时必须创建自定义索引，与传统关系数据库非常相似。 如果特定查询没有索引，则可能会遍历许多节点。 这个查询可能仍然有效，但速度可能非常慢。

如果Oak遇到没有索引的查询，则会打印WARN级别日志消息：

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

基于Apache Oak的后端允许将不同的索引器插入存储库中。

一个索引器是 **属性索引**，索引定义将存储在该存储库本身中。

的实施 **Apache Lucene** 和 **Solr** 默认情况下也可用，二者都支持全文索引。

此 **遍历索引** 如果没有其他索引器可用，则使用。 这意味着内容未编入索引，内容节点会被遍历以查找与查询匹配的项。

如果一个查询有多个可用的索引器，则每个可用的索引器都会估算执行查询的成本。 然后Oak选择具有最低估计成本的索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上图是Apache Oak查询执行机制的高层表示。

首先，将查询解析为抽象语法树。 然后，查询被检查并转换为SQL-2，这是Oak查询的本地语言。

接下来，查询每个索引以估计查询成本。 完成此操作后，将检索来自最便宜索引的结果。 最后，过滤结果，既确保当前用户拥有对结果的读取权限，又确保结果与完整的查询匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>对于大型存储库而言，构建索引是一项耗时的操作。 这适用于索引的初始创建和重新索引（更改定义后重建索引）。 另请参阅 [Oak索引疑难解答](/help/sites-deploying/troubleshooting-oak-indexes.md) 和 [防止重新索引缓慢](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

如果大型存储库中需要重新索引，尤其是使用MongoDB和进行全文索引时，请考虑文本预提取，并使用oak-run构建初始索引和重新索引。

索引被配置为存储库中位于下的节点。 **Oak：index** 节点。

索引节点的类型必须是 **oak：QueryIndexDefinition。** 每个索引器都有多个配置选项作为节点属性使用。 有关更多信息，请参阅下面每种索引器类型的配置详细信息。

### 属性索引 {#the-property-index}

属性索引对于具有属性约束但不是全文的查询非常有用。 可以按照以下步骤对其进行配置：

1. 打开CRXDE，方法是转到 `http://localhost:4502/crx/de/index.jsp`
1. 在下创建节点 **oak：index**
1. 命名节点 **PropertyIndex**，并将节点类型设置为 **oak：QueryIndexDefinition**
1. 为新节点设置以下属性：

   * **类型：**  `property` （属于字符串类型）
   * **属性名称：**  `jcr:uuid` （属于名称类型）

   此特定示例将 `jcr:uuid` 属性，其工作是公开其所附加节点的通用唯一标识符(UUID)。

1. 保存更改。

属性索引具有以下配置选项：

* 此 **type** 属性指定索引的类型，在这种情况下，必须将其设置为 **属性**

* 此 **属性名称** 属性指明将存储在索引中的属性的列表。 如果缺少节点名称，则使用节点名称作为属性名称引用值。 在此示例中， **jcr：uuid** 其作业是公开其节点的唯一标识符(UUID)的属性将添加到索引中。

* 此 **独特** 标记（如果设置为） **true** 在属性索引中添加唯一性约束。

* 此 **声明节点类型** 属性允许您指定仅应用索引的特定节点类型。
* 此 **重新索引** 标记设置为 **true**，会触发完整的内容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是Property索引的扩展。 但是，它已被弃用。 必须将此类型的索引替换为 [Lucene属性索引](#the-lucene-property-index).

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6中提供了基于Apache Lucene的全文索引器。

如果配置了全文索引，则无论是否有其他条件被索引，也无论是否有路径限制，所有具有全文条件的查询都使用全文索引。

如果未配置全文索引，则具有全文条件的查询将无法按预期工作。

由于索引是通过异步后台线程更新的，因此在后台进程完成之前的很短时间内，某些全文搜索不可用。

您可以按照以下步骤配置Lucene全文索引：

1. 打开CRXDE并在下创建节点 **oak：index**.
1. 命名节点 **LuceneIndex** 并将节点类型设置为 **oak：QueryIndexDefinition**
1. 将以下属性添加到节点：

   * **类型：**  `lucene` （属于字符串类型）
   * **异步：**  `async` （属于字符串类型）

1. 保存更改。

Lucene索引具有以下配置选项：

* 此 **type** 指定索引类型的属性必须设置为 **lucene**
* 此 **异步** 必须设置为的属性 **异步**. 这会将索引更新进程发送到后台线程。
* 此 **includePropertyTypes** 属性，定义索引中包含哪些属性类型的子集。
* 此 **excludePropertyNames** 定义属性名称列表的属性 — 应从索引中排除的属性。
* 此 **重新索引** 标记在设置为时显示的对象 **true**，会触发完整的内容重新索引。

### Lucene属性索引 {#the-lucene-property-index}

从 **Oak 1.0.8**，Lucene可用于创建涉及非全文属性约束的索引。

要实现Lucene属性索引，请 **fulltextEnabled** 属性必须始终设置为false。

以以下示例查询为例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

要为上述查询定义Lucene属性索引，可通过在下创建节点来添加以下定义 **Oak:index:**

* **名称:** `LucenePropertyIndex`
* **类型：** `oak:QueryIndexDefinition`

创建节点后，添加以下属性：

* **类型:**

  ```xml
  lucene (of type String)
  ```

* **异步:**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled：**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames：** `["alias"] (of type String)`

>[!NOTE]
>
>与常规属性索引相比，Lucene属性索引始终在异步模式下配置。 因此，索引返回的结果可能并不总是反映存储库的最新状态。

>[!NOTE]
>
>有关Lucene属性索引的更多具体信息，请参阅 [Apache Jackrabbit Oak Lucene文档页面](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Lucene分析器 {#lucene-analyzers}

从1.2.0版本开始，Oak支持Lucene分析器。

分析器在文档索引和查询时使用。 分析器检查字段的文本并生成令牌流。 Lucene分析器由一系列标记器和过滤类组成。

分析器可通过 `analyzers` 节点（属于类型） `nt:unstructured`)内部 `oak:index` 定义。

索引的默认分析器配置在 `default` 分析器节点的子节点。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>有关可用的分析器列表，请参阅您使用的Lucene版本的API文档。

#### 直接指定分析器类 {#specifying-the-analyzer-class-directly}

如果要使用任何开箱即用的分析器，可以按照以下步骤对其进行配置：

1. 在下，找到要与分析器一起使用的索引 `oak:index` 节点。

1. 在索引下，创建一个名为的子节点 `default` 类型 `nt:unstructured`.

1. 将属性添加到具有以下属性的默认节点：

   * **名称:** `class`
   * **类型：** `String`
   * **值:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   值是要使用的分析器类的名称。

   您还可以使用选项，将分析器设置为与特定Lucene版本一起使用 `luceneMatchVersion` 字符串属性。 将其与Lucene 4.7一起使用的有效语法为：

   * **名称:** `luceneMatchVersion`
   * **类型：** `String`
   * **值:** `LUCENE_47`

   如果 `luceneMatchVersion` 未提供，Oak使用随附的Lucene版本。

1. 如果要将stopwords文件添加到分析器配置，可以在下创建节点 `default` 一个具有以下属性：

   * **名称:** `stopwords`
   * **类型：** `nt:file`

#### 通过组合创建分析器 {#creating-analyzers-via-composition}

分析器也可以根据以下内容组成 `Tokenizers`， `TokenFilters` 和 `CharFilters`. 为此，可指定分析器并为其可选令牌和过滤器创建子节点，这些子节点将按列出的顺序应用。 另请参阅 [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

以此节点结构为例：

* **名称:** `analyzers`

   * **名称:** `default`

      * **名称:** `charFilters`
      * **类型：** `nt:unstructured`

         * **名称:** `HTMLStrip`
         * **名称:** `Mapping`

      * **名称:** `tokenizer`

         * **属性名称:** `name`

            * **类型：** `String`
            * **值:** `Standard`

      * **名称:** `filters`
      * **类型：** `nt:unstructured`

         * **名称:** `LowerCase`
         * **名称:** `Stop`

            * **属性名称:** `words`

               * **类型：** `String`
               * **值:** `stop1.txt, stop2.txt`

            * **名称:** `stop1.txt`

               * **类型：** `nt:file`

            * **名称:** `stop2.txt`

               * **类型：** `nt:file`

过滤器、charFilters和tokenizer的名称是通过删除出厂后缀形成的。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 变为 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 变为 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 变为 `Stop`

工厂所需的任何配置参数均指定为相关节点的属性。

对于需要加载外部文件中的内容的加载停止词，可以通过创建子节点来提供内容 `nt:file` 键入相关文件。

### Solr索引 {#the-solr-index}

Solr索引的用途是全文搜索，但它也可用于按路径、属性限制和主类型限制对搜索进行索引。 这意味着Oak中的Solr索引可用于任何类型的JCR查询。

AEM中的集成发生在存储库级别，因此Solr是可用于Oak(AEM随附的新存储库实施)中的可能索引之一。

它可以配置为作为远程服务器与AEM实例一起使用。

### 使用单个远程Solr服务器配置AEM {#configuring-aem-with-a-single-remote-solr-server}

也可以将AEM配置为与远程Solr服务器实例一起使用：

1. 下载并解压缩最新版本的Solr。 有关如何执行此操作的更多信息，请参阅 [Apache Solr安装文档](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. 现在，创建两个Solr分片。 为此，您可以为Solr解压缩文件夹中的每个分区创建文件夹：

   * 对于第一个分片，创建文件夹：

   `<solrunpackdirectory>\aemsolr1\node1`

   * 对于第二个分片，创建文件夹：

   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr软件包中找到示例实例。 它位于名为“”的文件夹中。 `example`”在包的根目录下。
1. 将以下文件夹从示例实例复制到两个分片文件夹( `aemsolr1\node1` 和 `aemsolr2\node2`)：

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 创建一个名为“”的文件夹 `cfg`”存储在两个分片文件夹的每个文件夹中。
1. 将Solr和Zookeeper配置文件放入新创建的 `cfg` 文件夹。

   >[!NOTE]
   >
   >有关Solr和ZooKeeper配置的更多信息，请参阅 [Solr配置文档](https://wiki.apache.org/solr/ConfiguringSolr) 和 [ZooKeeper快速入门指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. 通过ZooKeeper支持启动第一个分片，方法是 `aemsolr1\node1` 并运行以下命令：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 通过转到开始第二个分片 `aemsolr2\node2` 并运行以下命令：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 两个分片都启动后，通过在以下位置连接到Solr接口，测试所有组件是否均已启动并运行： `http://localhost:8983/solr/#/`
1. 启动AEM并转到Web控制台，网址为 `http://localhost:4502/system/console/configMgr`
1. 在下设置以下配置 **Oak Solr远程服务器配置**：

   * Solr HTTP URL： `http://localhost:8983/solr/`

1. 选择 **远程Solr** 在下拉列表中的 **Oak Solr** 服务器提供程序。

1. 转到CRXDE并以管理员身份登录。
1. 创建一个名为的节点 **solrIndex** 下 **oak：index**，并设置以下属性：

   * **类型：** solr（属于字符串类型）
   * **异步：** 异步（属于字符串类型）
   * **重新索引：** true（属于布尔类型）

1. 保存更改。

#### 推荐的Solr配置 {#recommended-configuration-for-solr}

以下是可用于本文所述所有三个Solr部署的基本配置示例。 它包含AEM中已存在的专用属性索引，这些索引不应与其他应用程序一起使用。

要正确使用它，必须将归档文件的内容直接放在Solr主目录中。 在多节点部署中，它应直接位于每个节点的根文件夹下。

推荐的Solr配置文件

[获取文件](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1还集成了AEM 6.0中存在的两个索引工具，作为Adobe咨询服务公域工具集的一部分：

1. **说明查询**，此工具旨在帮助管理员了解查询的执行方式；
1. **Oak索引管理器**，用于维护现有索引的Web用户界面。

现在，您可以通过以下方式联系他们 **工具 — 操作 — 功能板 — 诊断** 从AEM欢迎屏幕。

有关如何使用它们的更多信息，请参见 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

#### 通过OSGi创建属性索引 {#creating-property-indexes-via-osgi}

ACS Commons包还公开可用于创建属性索引的OSGi配置。

您可以从Web控制台通过搜索“**确保Oak属性索引**“。

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引问题疑难解答 {#troubleshooting-indexing-issues}

可能会出现查询执行时间较长，且一般系统响应时间缓慢的情况。

本节提供了一系列关于必须执行什么操作来跟踪此类问题原因的建议以及如何解决这些问题的建议。

#### 正在准备调试信息以供分析 {#preparing-debugging-info-for-analysis}

要获取所执行查询的必需信息，最简单的方法是通过 [说明查询工具](/help/sites-administering/operations-dashboard.md#explain-query). 这样，您就可以收集调试缓慢查询所需的精确信息，而无需查阅日志级别信息。 如果您知道正在调试的查询，则需要这样做。

如果由于任何原因而无法执行此操作，您可以将索引日志收集到一个文件中，并使用它来解决您的特定问题。

#### 启用日志记录 {#enable-logging}

要启用日志记录，必须启用 **调试** 与Oak索引和查询相关的类别的级别日志。 这些类别包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

此 **com.day.cq.search** 类别仅适用于使用AEM提供的QueryBuilder实用程序的情况。

>[!NOTE]
>
>请务必仅在要排除故障的查询运行期间将日志设置为DEBUG。 否则，日志中会随时间生成大量事件。 因此，在收集到所需的日志后，请切换回上述类别的INFO级别日志记录。

您可以按照以下步骤启用日志记录：

1. 将浏览器指向 `https://serveraddress:port/system/console/slinglog`
1. 单击 **添加新记录器** 按钮来打开此窗口。
1. 在新创建的行中，添加上述类别。 您可以使用 **+** 签名可将多个类别添加到单个日志程序。
1. 选择 **调试** 从 **日志级别** 下拉列表。
1. 将输出文件设置为 `logs/queryDebug.log`. 这会将所有DEBUG事件关联到一个日志文件中。
1. 运行查询或渲染正在使用要调试的查询的页面。
1. 执行查询后，返回日志记录控制台，并将新创建的日志记录器的日志级别更改为 **信息**.

#### 索引配置 {#index-configuration}

查询的评估方式在很大程度上受索引配置的影响。 分析索引配置或将其发送给支持人员是非常重要的。 您可以将配置作为内容包获取，也可以获取JSON演绎版。

通常，索引配置存储在 `/oak:index` 节点，您可以在以下位置获取JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果在不同位置配置了索引，请相应地更改路径。

#### MBean输出 {#mbean-output}

有时，提供与索引相关的MBean的输出用于调试会很有用。 您可以执行以下操作来实现此目标：

1. 转到JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean：

   * Lucene索引统计数据
   * CopyOnRead支持统计数据
   * Oak查询统计数据
   * IndexStat

1. 单击每个MBean可获取性能统计信息。 创建屏幕快照或记下它们，以备需要提交支持时使用。

您还可以通过以下URL获取这些统计信息的JSON变体：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您还可以通过以下方式提供整合的JMX输出 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. 这将包括JSON格式的所有与Oak相关的MBean详细信息。

#### 其他详细信息 {#other-details}

您可以收集其他详细信息以帮助解决问题，例如：

1. 运行实例的Oak版本。 您可以通过打开CRXDE并查看欢迎页面右下角的版本来查看此内容，也可以通过检查的版本 `org.apache.jackrabbit.oak-core` 捆绑。
1. 有问题的查询的QueryBuilder Debugger输出。 可在以下位置访问该调试器： `https://serveraddress:port/libs/cq/search/content/querydebug.html`
