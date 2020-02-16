---
title: Oak-run.jar索引使用案例
seo-title: Oak-run.jar索引使用案例
description: 了解使用Oak-run工具执行索引的各种用户案例。
seo-description: 了解使用Oak-run工具执行索引的各种用户案例。
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Oak-run.jar索引使用案例{#oak-run-jar-indexing-use-cases}

Oak-run支持在命令行上为用例编制索引，无需通过AEM的JMX控制台编排这些用例的执行。

使用oak-run.jar索引命令方法管理Oak索引的主要好处是：

1. Oak-run index命令为AEM 6.4提供了一个新的索引编制工具集。
1. Oak-run缩短了重新索引的时间，从而缩短了在较大存储库上重新索引的时间。
1. Oak-run减少了在AEM中重新构建索引期间的资源消耗，从而总体上提高了系统性能。
1. Oak-run提供带外重新索引，支持生产必须可用的情况，并且不能容忍维护或停机，否则需要重新索引。

以下部分将提供示例命令。 oak-run索引命令支持所有NodeStore和BlobStore设置。 下面提供的示例围绕具有FileDataStore和SegmentNodeStore的设置。

## 用例1 —— 索引一致性检查 {#usercase1indexconsistencycheck}

这是与索引损坏相关的用例。 在某些情况下，无法确定哪些索引已损坏。 因此，Adobe提供了以下工具：

1. 对所有索引执行索引一致性检查，并提供索引有效和无效的报告；
1. 即使AEM不可访问，工具也可用；
1. 它易于使用。

可以通过以下操作检查损坏的 `--index-consistency-check` 索引：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

这将在中生成报告 `indexing-result/index-consistency-check-report.txt`。 有关示例报告，请参见下文：

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### 优势 {#uc1benefits}

现在，支持部门和系统管理员可以使用此工具快速确定哪些索引已损坏，然后对它们重新编制索引。

## 用例2 —— 索引统计数据 {#usecase2indexstatistics}

为了诊断查询性能方面的一些情况，Adobe通常需要现有的索引定义，从客户设置中索引相关统计信息。 到目前为止，这些信息分散在多种资源中。 为了简化疑难解答，Adobe创建了以下工具：

1. 将系统上存在的所有索引定义转储为一个JSON文件；

1. 从现有索引中转储重要统计数据；

1. 转储索引内容以进行脱机分析；

1. 即使AEM不可访问，也将可用

现在，可以通过以下操作索引命令执行上述操作：

* `--index-info` -收集和转储与索引相关的各种统计信息

* `--index-definitions` -收集和转储索引定义

* `--index-dump` -转储索引内容

请参见下面一个示例，了解这些命令的实际工作方式：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

将在和中生成报 `indexing-result/index-info.txt` 告 `indexing-result/index-definitions.json`

此外，还通过Web控制台提供了相同的详细信息，这些详细信息将成为配置转储zip的一部分。 可以在以下位置访问它们：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 优势 {#uc2benefits}

此工具集可快速收集与索引或查询问题相关的所有必需详细信息，并缩短提取此信息所花费的时间。

## 用例3 —— 重新构建索引 {#usecase3reindexing}

根据情 [况](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，在某些情况下需要执行重新索引。 当前，通过CRXDE或Index Manager用户界 `reindex` 面将标志设 `true` 置为索引定义节点中的标志，即可重新构建索引。 设置标志后，将异步完成重新索引。

重新编制索引时应注意的几点：

* 与所有内容都是本地内容的设 `DocumentNodeStore` 置相比，在设 `SegmentNodeStore` 置中重新索引的速度要慢得多；

* 在当前设计中，当重新索引发生时，异步索引器被阻止并且所有其他异步索引都变得陈旧，并且在索引期间不获取更新。 因此，如果系统在使用中，用户可能看不到最新结果；
* 重新构建索引涉及遍历整个存储库，这会给AEM设置带来高负载，从而影响最终用户体验；
* 对于重 `DocumentNodeStore` 新构建索引可能需要相当长时间的安装，如果在操作过程中与Mongo数据库的连接失败，则必须从头开始重新构建索引；

* 在某些情况下，由于文本提取，重新构建索引可能需要很长时间。 这主要针对具有大量PDF文件的设置，在这些设置中，文本提取所花费的时间会影响索引时间。

为了实现这些目标，Oak运行的索引工具支持不同的重新索引模式，这些模式可以根据需要使用。 oak-run index命令具有以下优点：

* **带外重新索引** - oak-run重新索引可以与正在运行的AEM设置分开进行，因此可以将对正在使用的AEM实例的影响降至最低；

* **跨通道重新索引** -重新索引在不影响索引编制操作的情况下进行。 这意味着异步索引器可以继续索引其他索引；

* **简化的DocumentNodeStore安装重新索引** -对于安装 `DocumentNodeStore` ，只需使用一个命令即可重新索引，这可确保以最佳方式重新索引；

* **支持更新索引定义和引入新的索引定义**

### 重新索引- DocumentNodeStore {#reindexdocumentnodestore}

对于 `DocumentNodeStore` 安装，可通过单个oak-run命令重新构建索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

这提供了以下优点

* 对运行AEM实例的影响最小。 大多数读取操作都可从从属服务器执行，并且由于重新构建索引所需的所有遍历操作，运行AEM缓存不会受到反向影响；
* 用户还可以通过选项提供新索引或更新索引的JSON `--index-definitions-file` 。

### 重新索引- SegmentNodeStore {#reindexsegmentnodestore}

对于 `SegmentNodeStore` 安装，可以通过以下方式之一重新构建索引：

#### 在线重新索引- SegmentNodeStore {#onlinereindexsegmentnodestore}

按照既定的方式，通过设置标志重新构建索 `reindex` 引。

#### 联机重新索引- SegmentNodeStore - AEM实例正在运行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

对于 `SegmentNodeStore` 安装，只有一个进程可以在读写模式下访问段文件。 由于这一原因，在oak-run索引中的某些操作需要执行额外的手动步骤。

这将涉及以下事项：

1. 步骤文本
1. 将AEM在 `oak-run` 只读模式下使用的同一存储库连接并执行索引。 有关如何实现此目的的示例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最后，通过操作从oak-run运行上述命 `IndexerMBean#importIndex` 令后保存索引文件的路径导入创建的索引文件。

在此方案中，您不必停止AEM服务器或配置任何新实例。 但是，由于索引涉及遍历整个存储库，因此会增加安装的I/O负载，从而对运行时性能产生负面影响。

#### 在线重新索引- SegmentNodeStore - AEM实例已关闭 {#onlinereindexsegmentnodestoreaeminstanceisdown}

对于 `SegmentNodeStore` 安装，可通过单个oak-run命令重新构建索引。 但是，AEM实例需要关闭。

可以使用以下命令触发重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法与上述方法的区别在于检查点创建和索引导入是自动完成的。 不利之处在于AEM在此过程中需要关闭。

#### 带外重新索引- SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此用例中，您可以对克隆的设置执行重新索引，以将对正在运行的AEM实例的影响降至最低：

1. 通过JMX操作创建检查点。 您可以通过转到 [JMX控制台并搜索](/help/sites-administering/jmx-console.md) 来执行此操作 `CheckpointManager`。 然后，使用高 **值单击createCheckpoint(long p1)** ，以秒为单位过期(例如， **2592000**)。
1. 将文件夹 `crx-quickstart` 复制到新计算机
1. 通过oak-run索引命令执行重新索引

1. 将生成的索引文件复制到AEM服务器

1. 通过JMX导入索引文件。

在此用例中，假定数据存储可在另一个实例上访问，如果放在EBS等基于云的存储解决 `FileDataStore` 方案上，则该实例可能无法访问。 这不包括同时克隆 `FileDataStore` 的方案。 如果索引定义不执行全文索引，则不需要访 `DataStore` 问该索引。

## 用例4 —— 更新索引定义 {#usecase4updatingindexdefinitions}

目前，您可以通过 [ACS Ensure Index包发送索引定义更改](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) 。 这允许通过内容包发送索引定义，后者需要通过将标志设置为执行重新 `reindex` 索引 `true`。

这对于重新构建索引不需要很长时间的较小安装非常有效。 但是，对于超大的存储库，重新构建索引将在更长的时间内完成。 对于这类情况，我们现在可以使用oak-run索引工具。

Oak-run现在支持以JSON格式提供索引定义，并在带外模式下创建索引，在带外模式下，实时实例不会执行任何更改。

您需要考虑的此用例过程是：

1. 开发人员将更新本地实例上的索引定义，然后通过该选项生成索引定义JSON文 `--index-definitions` 件

1. 更新后的JSON随后将交给系统管理员
1. 系统管理员采用带外方法，在其他安装上准备索引
1. 完成此操作后，将在正在运行的AEM安装中导入生成的索引文件。

