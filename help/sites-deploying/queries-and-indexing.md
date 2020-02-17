---
title: Oak查询和索引
seo-title: Oak查询和索引
description: 了解如何在AEM中配置索引。
seo-description: 了解如何在AEM中配置索引。
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: 1f7a45adc73b407c402a51b061632e72d97ca306

---


# Oak查询和索引{#oak-queries-and-indexing}

>[!NOTE]
>
>本文介绍如何在AEM 6中配置索引。 有关优化查询和索引性能的最佳实践，请参 [阅查询和索引的最佳实践](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

## 简介 {#introduction}

与Jackrabbit 2不同，默认情况下，Oak不为内容编制索引。 需要创建自定义索引，这与传统的关系数据库非常相似。 如果特定查询没有索引，则可能会遍历许多节点。 查询可能仍然有效，但可能非常慢。

如果Oak遇到一个不带索引的查询，则会打印一条WARN级别日志消息：

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## 支持的查询语言 {#supported-query-languages}

Oak查询引擎支持以下语言：

* XPath（建议）
* SQL-2
* SQL（已弃用）
* JQOM

## 索引器类型和成本计算 {#indexer-types-and-cost-calculation}

基于Apache Oak的后端允许将不同的索引器插入存储库。

一个索引器是 **属性索引**，其索引定义存储在存储库本身中。

默认情 **况下，Apache Lucene** 和 **Solr** （两者都支持全文索引）的实现也可用。

如果 **没有其他索引器可用** ，则使用遍历索引。 这意味着内容不会索引，内容节点会被遍历以查找与查询的匹配项。

如果可以查询多个索引器，则每个可用的索引器估计执行查询的成本。 然后，Oak选择成本最低的索引器。

![chlimage_1-148](assets/chlimage_1-148.png)

上图是Apache Oak查询执行机制的高级表示。

首先，将查询解析为抽象语法树。 然后，检查查询并将其转换为SQL-2,SQL-2是Oak查询的本机语言。

接下来，查询每个索引以估计查询的成本。 一旦完成，最便宜的指数的结果就会被检索出来。 最后，过滤结果，以确保当前用户对结果具有读取访问权，并且结果与完整查询相匹配。

## 配置索引 {#configuring-the-indexes}

>[!NOTE]
>
>对于大型存储库，构建索引是一项耗时的操作。 对于最初创建索引和重新构建索引（在更改定义后重建索引），情况是这样。 另请参 [阅Oak索引疑难解答](/help/sites-deploying/troubleshooting-oak-indexes.md)[和防止慢速重新索引](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)。

如果在大型存储库中需要重新构建索引，特别是在使用MongoDB和用于全文索引时，请考虑文本预提取，并使用oak-run构建初始索引和重新索引。

索引将配置为存储库中 **oak:index节点下的节点** 。

索引节点的类型必须 **是oak:QueryIndexDefinition。** 每个索引器都有若干配置选项作为节点属性。 有关详细信息，请参阅下面每个索引器类型的配置详细信息。

### 属性索引 {#the-property-index}

对于具有属性约束但不是全文的查询，“属性索引”通常很有用。 可以按照以下过程进行配置：

1. 通过转到 `http://localhost:4502/crx/de/index.jsp`
1. 在 **oak:index下创建新节点**
1. 将节点命 **名为PropertyIndex**，并将节点类型设置为 **oak:QueryIndexDefinition**
1. 为新节点设置以下属性：

   * **** type: `property` （字符串类型）
   * **** propertyNames: `jcr:uuid` （名称类型）
   此特定示例将索引属 `jcr:uuid` 性，该属性的作业是公开其所连接节点的通用唯一标识符(UUID)。

1. 保存更改。

“属性索引”具有以下配置选项：

* type **属性** 将指定索引的类型，在这种情况下，必须将其设置为属 **性**

* propertyNames **属性** 指示将存储在索引中的属性列表。 如果缺少该属性，则节点名称将用作属性名称引用值。 在此示例中，将 **jcr:uuid** 属性添加到索引中，该属性的作业是公开其节点的唯一标识符(UUID)。

* 唯一 **标志** ，如果设置为 **true** ，则该标志会为属性索引添加唯一性约束。

* clarkiningNodeTypes **** 属性允许您指定索引将仅应用于的特定节点类型。
* 重新 **索引标志** ，如果设置为 **true**，将触发完全内容重新索引。

### 有序索引 {#the-ordered-index}

Ordered索引是属性索引的扩展。 但是，它已弃用。 此类型的索引需要替换为 [Lucene属性索引](#the-lucene-property-index)。

### Lucene全文索引 {#the-lucene-full-text-index}

AEM 6中提供了基于Apache Lucene的全文索引器。

如果配置了全文索引，则所有具有全文条件的查询都使用全文索引，无论是否有其他索引条件，也无论是否有路径限制。

如果未配置全文索引，则具有全文条件的查询将无法按预期工作。

由于索引是通过异步背景线程更新的，因此在后台进程完成之前，某些全文搜索在一小段时间内将不可用。

您可以按照以下步骤配置Lucene全文索引：

1. 打开CRXDE，在 **oak:index下创建一个新节点**。
1. 将节点命 **名为LuceneIndex** ，并将节点类型设置为 **oak:QueryIndexDefinition**
1. 将以下属性添加到节点：

   * **** type: `lucene` （字符串类型）
   * **** 异步： `async` （字符串类型）

1. 保存更改。

Lucene Index具有以下配置选项：

* 必须指定 **索引类型的type** 属性必须设置为lucene ****
* 必须 **设置为** async的async属 **性**。 这将向后台线程发送索引更新进程。
* includePropertyTypes **** 属性，它将定义索引中将包含的属性类型的子集。
* 将 **定义属性名称的黑名单的excludePropertyNames属性** -应从索引中排除的属性。
* 重新 **索引** 标志，当设置为 **true时**，该标志会触发完全内容重新索引。

### Lucene属性指数 {#the-lucene-property-index}

由于 **Oak 1.0.8**,Lucene可用于创建包含非全文的属性约束的索引。

要获得Lucene属性索引，必须 **始终将fulltextEnabled** 属性设置为false。

以下是查询示例：

```xml
select * from [nt:base] where [alias] = '/admin'
```

为了为上述查询定义Lucene属性索引，您可以通过在 **oak:index下创建新节点来添加以下定义：**

* **名称:** `LucenePropertyIndex`
* **类型:** `oak:QueryIndexDefinition`

创建节点后，添加以下属性：

* **类型:**

   ```
   lucene (of type String)
   ```

* **异步:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **** includePropertyNames: `["alias"] (of type String)`

>[!NOTE]
>
>与常规属性索引相比，Lucene属性索引始终以异步模式配置。 因此，索引返回的结果不一定总是反映存储库的最新状态。

>[!NOTE]
>
>有关Lucene属性索引的更多具体信息，请参阅 [Apache Jackrabbit Oak Lucene文档页](https://jackrabbit.apache.org/oak/docs/query/lucene.html)。

### Lucene Analyzers {#lucene-analyzers}

自版本1.2.0起，Oak支持Lucene分析器。

在对文档进行索引时和在查询时都使用分析器。 分析器检查字段文本并生成令牌流。 Lucene分析器由一系列标记器和过滤器类组成。

分析器可以通过定义内 `analyzers` 的节点(类 `nt:unstructured`型)进行 `oak:index` 配置。

索引的默认分析器配置在分析器节 `default` 点的子节点中。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>有关可用分析器的列表，请查阅您所使用的Lucene版本的API文档。

#### 直接指定Analyzer类 {#specifying-the-analyzer-class-directly}

如果您希望使用任何现成的分析器，可以按照以下过程配置它：

1. 在节点下找到要使用分析器的索 `oak:index` 引。

1. 在索引下，创建一个名为类型的 `default` 子节点 `nt:unstructured`。

1. 使用以下属性向默认节点添加属性：

   * **名称:** `class`
   * **类型:** `String`
   * **** 值： `org.apache.lucene.analysis.standard.StandardAnalyzer`
   该值是您要使用的分析器类的名称。

   还可以使用可选字符串属性设置要与特定lucene版本一起使用的分 `luceneMatchVersion` 析器。 与Lucene 4.7一起使用它的有效合成包是：

   * **名称:** `luceneMatchVersion`
   * **类型:** `String`
   * **** 值： `LUCENE_47`
   如果 `luceneMatchVersion` 未提供，Oak将使用随附的Lucene版本。

1. 如果要向分析器配置添加秒词文件，则可以在具有以下属性的节点下 `default` 创建新节点：

   * **名称:** `stopwords`
   * **类型:** `nt:file`

#### 通过合成创建分析器 {#creating-analyzers-via-composition}

分析器也可以基于、 `Tokenizers`和 `TokenFilters` 组成 `CharFilters`。 为此，可指定分析器并创建其可选标记器和过滤器的子节点，这些子节点将按列出顺序应用。 另请参阅 [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

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
            * **** 值： `Standard`
      * **名称:** `filters`
      * **类型:** `nt:unstructured`

         * **名称:** `LowerCase`
         * **名称:** `Stop`

            * **属性名称:** `words`

               * **类型:** `String`
               * **** 值： `stop1.txt, stop2.txt`
            * **名称:** `stop1.txt`

               * **类型:** `nt:file`
            * **名称:** `stop2.txt`

               * **类型:** `nt:file`





过滤器、charFilters和标记器的名称通过删除工厂后缀来形成。 因此：

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` 变成 `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` 变成 `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` 变成 `Stop`

工厂所需的任何配置参数都指定为相关代码的属性。

对于加载需要加载外部文件内容的停止字等情况，可以通过为相关文件创建类型的子节点来提供 `nt:file` 该内容。

### 索尔指数 {#the-solr-index}

Solr索引主要用于全文搜索，但也可用于按路径、属性限制和主要类型限制对搜索进行索引。 这意味着Oak中的Solr索引可用于任何类型的JCR查询。

AEM中的集成在存储库级别进行，因此Solr是可在Oak中使用的索引之一，Oak是AEM附带的新存储库实施。

可以将其配置为作为具有AEM实例的嵌入式服务器或作为远程服务器工作。

### 使用嵌入式Solr服务器配置AEM {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>请勿在生产环境中使用嵌入式Solr服务器。 它只应用于开发环境。

AEM可与可通过Web控制台配置的嵌入式Solr服务器一起使用。 在这种情况下，Solr服务器将在与其嵌入到的AEM实例相同的JVM中运行。

可以通过以下方式配置嵌入式Solr服务器：

1. 转到Web控制台，网址为 `https://serveraddress:4502/system/console/configMgr`
1. 搜索“**Oak Solr服务器提供商**”。
1. 按编辑按钮，在下面的窗口中，在下拉列表中将服务器类 **型设置为** “嵌入式解决程序”。

1. 然后，编辑“**Oak Solr嵌入式服务器配置**”并创建配置。 有关配置选项的更多信息，请访 [问Apache Solr网站](https://lucene.apache.org/solr/documentation.html)。

   >[!NOTE]
   >
   >Solr主目录(solr.home.path)配置将在AEM安装文件夹中查找同名的文件夹。

1. 打开CRXDE并以管理员身份登录。
1. 在oak:index下添 **加ak** :QueryIndexDefinition类型的名为solrlindex的节点 ******** ，该节点具有以下属性：

   * **** type: `solr`（类型为字符串）
   * **** 异步： `async`（类型为字符串）
   * **** 重新索引： `true`（类型为Boolean）

1. 保存更改。

### 使用单台远程Solr服务器配置AEM {#configuring-aem-with-a-single-remote-solr-server}

AEM还可配置为与远程Solr服务器实例一起使用：

1. 下载并提取最新版Solr。 有关如何执行此操作的详细信息，请参阅 [Apache Solr安装文档](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)。
1. 现在，创建两个索尔碎片。 为此，可以在Solr已被更新的文件夹中为每个共享创建文件夹：

   * 对于第一个共享，创建文件夹：
   `<solrunpackdirectory>\aemsolr1\node1`

   * 对于第二个共享，请创建文件夹：
   `<solrunpackdirectory>\aemsolr2\node2`

1. 在Solr包中找到示例实例。 它通常位于包根目录中名 `example`为“”的文件夹中。
1. 将示例实例中的以下文件夹复制到两个共享文件夹( `aemsolr1\node1` 和 `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 在两个共享文件夹中 `cfg`的每个文件夹中都创建一个名为“”的新文件夹。
1. 将您的Solr和Zookeeper配置文件放在新创建的文件夹 `cfg` 中。

   >[!NOTE]
   >
   >有关Solr和ZooKeeper配置的详细信息，请参阅 [Solr配置文档](https://wiki.apache.org/solr/ConfiguringSolr) 和 [ZooKeeper入门指南](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)。

1. 转到并运行以下命令，即可启动支持ZooKeeper `aemsolr1\node1` 的第一个共享区：

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 转到并运行以下命令， `aemsolr2\node2` 开始第二个分片：

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 在启动这两个分片后，通过连接到Solr界面，测试所有内容是否都已启动并运行 `http://localhost:8983/solr/#/`
1. 启动AEM并转到Web控制台，网址为 `http://localhost:4502/system/console/configMgr`
1. 在 **Oak Solr远程服务器配置下设置以下配置**:

   * 解析HTTP URL: `http://localhost:8983/solr/`

1. 在 **Oak Solr服务器提供商下的下拉列表中选择** Remote Solr **** 。

1. 转到CRXDE并以管理员身份登录。
1. 在oak:index下创建一 **个名为solrIndex** 的 **新节点**，并设置以下属性：

   * **** type:solr（类型为字符串）
   * **** 异步：async（字符串类型）
   * **** 重新索引：true（属于Boolean类型）

1. 保存更改。

#### 建议的Solr配置 {#recommended-configuration-for-solr}

下面是一个基本配置的示例，该配置可用于本文中描述的所有三个Solr部署。 它包含AEM中已存在的专用属性索引，不应与其他应用程序一起使用。

为了正确使用它，您需要将存档的内容直接放在Solr主目录中。 在多节点部署的情况下，它应直接位于每个节点的根文件夹下。

推荐的Solr配置文件

[获取文件](assets/recommended-conf.zip)

### AEM索引工具 {#aem-indexing-tools}

AEM 6.1还将AEM 6.0中提供的两个索引编制工具集成到Adobe Consulting Services Commons工具集中：

1. **解释Query**，这是一种旨在帮助管理员理解如何执行查询的工具；
1. **Oak Index Manager**，用于维护现有索引的Web用户界面。

您现在可以通过从AEM欢迎屏幕转 **到工具——操作——仪表板——诊断** ，与他们取得联系。

有关如何使用这些控件的详细信息，请参阅 [Operations Dashboard文档](/help/sites-administering/operations-dashboard.md)。

#### 通过OSGi创建属性索引 {#creating-property-indexes-via-osgi}

ACS Commons包还公开可用于创建属性索引的OSGi配置。

您可以通过搜索“Ensure Oak Property Index”从Web控制台&#x200B;**访问它**。

![chlimage_1-150](assets/chlimage_1-150.png)

### 索引问题疑难解答 {#troubleshooting-indexing-issues}

在查询执行时间较长且一般系统响应时间较慢的情况下，可能会出现这种情况。

本节提出了一组建议，说明为了查明这些问题的原因需要采取哪些措施，并就如何解决这些问题提出了建议。

#### 准备分析调试信息 {#preparing-debugging-info-for-analysis}

获取执行的查询所需信息的最简单方法是通过“解释查询 [”工具](/help/sites-administering/operations-dashboard.md#explain-query)。 这样，您就可以收集调试慢速查询所需的精确信息，而无需查阅日志级别信息。 如果您知道正在调试的查询，这是可取的。

如果由于任何原因无法实现此目的，您可以将索引日志收集到单个文件中，并使用它解决您的特定问题。

#### 启用日志记录 {#enable-logging}

要启用日志记录，您需要为与Oak索引和 **查询相关的类别启用** DEBUG级别日志。 这些类别包括：

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

com.day.cq.se **arch类别** ，仅在您使用AEM提供的QueryBuilder实用程序时才适用。

>[!NOTE]
>
>在执行要进行疑难排解的查询期间，日志仅设置为DEBUG很重要，否则，日志中会随着时间推移生成大量事件。 因此，一旦收集了所需的日志，就会切换回上述类别的“信息”级别日志记录。

您可以通过以下过程启用日志记录：

1. 将您的浏览器指向 `https://serveraddress:port/system/console/slinglog`
1. 单击 **控制台下半部分的** “添加新记录器”按钮。
1. 在新创建的行中，添加上述类别。 可以使用 **+符号** ，向单个记录器添加多个类别。
1. 从“ **日志** ”级别下 **拉列表中选择** “调试”。
1. 将输出文件设置为 `logs/queryDebug.log`。 这会将所有DEBUG事件关联到单个日志文件中。
1. 运行查询或呈现使用要调试的查询的页面。
1. 执行查询后，返回记录控制台，将新创建的记录器的日志级别更改为 **INFO**。

#### 索引配置 {#index-configuration}

查询的评估方式在很大程度上受索引配置的影响。 获取索引配置对于分析或发送给支持人员非常重要。 您可以将配置作为内容包获取或获取JSON再现。

由于大多数情况下，索引配置存储在CRXDE `/oak:index` 中的节点下，因此您可以在以下位置获得JSON版本：

`https://serveraddress:port/oak:index.tidy.-1.json`

如果索引配置在其他位置，请相应地更改路径。

#### MBean输出 {#mbean-output}

在某些情况下，提供与索引相关的MBean的输出以进行调试很有帮助。 您可以通过以下方式执行此操作：

1. 转到JMX控制台：
   `https://serveraddress:port/system/console/jmx`

1. 搜索以下MBean:

   * Lucene Index统计数据
   * CopyOnRead支持统计数据
   * Oak查询统计信息
   * IndexStats

1. 单击每个MBean以获取性能统计信息。 创建屏幕截图或记下它们，以备需要提交支持。

您还可以在以下URL上获取这些统计信息的JSON变体：

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

您还可以通过提供统一的JMX输 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`出。 这将包括JSON格式的所有与Oak相关的MBean详细信息。

#### 其他详细信息 {#other-details}

您可以收集更多详细信息以帮助解决问题，例如：

1. 您的实例正在运行的Oak版本。 打开CRXDE并查看欢迎页面右下角的版本，或检查捆绑包的版本，即可看到这一 `org.apache.jackrabbit.oak-core` 点。
1. 麻烦查询的QueryBuilder调试器输出。 调试器可通过以下网址访问： `https://serveraddress:port/libs/cq/search/content/querydebug.html`

