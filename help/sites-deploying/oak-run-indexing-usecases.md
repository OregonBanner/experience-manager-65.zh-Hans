---
title: Oak-run.jar索引用例
seo-title: Oak-run.jar索引用例
description: 了解使用Oak-run工具执行索引的各种用例。
seo-description: 了解使用Oak-run工具执行索引的各种用例。
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---

# Oak-run.jar索引用例{#oak-run-jar-indexing-use-cases}

Oak-run支持在命令行上索引用例，而无需通过AEM JMX控制台编排这些用例的执行。

使用oak-run.jar index命令方法管理Oak索引的主要优势包括：

1. Oak-run index命令为AEM 6.4提供了新的索引工具集。
1. Oak-run可缩短重新索引的时间，从而缩短大型存储库上的重新索引时间。
1. Oak-run可减少在AEM中重新索引期间的资源消耗，从而整体提高系统性能。
1. Oak-run提供带外重新索引，支持必须提供生产的情况，并且不能容忍重新索引所需的维护或停机。

以下部分将提供示例命令。 oak-run index命令支持所有NodeStore和BlobStore设置。 以下提供的示例涉及具有FileDataStore和SegmentNodeStore的设置。

## 用例1 — 索引一致性检查 {#usercase1indexconsistencycheck}

这是与索引损坏相关的用例。 在某些情况下，无法确定哪些索引已损坏。 因此，Adobe提供了以下工具：

1. 对所有索引执行索引一致性检查，并提供索引有效和无效的报告；
1. 即使AEM不可访问，工具也可用；
1. 易于使用。

可通过`--index-consistency-check`操作检查损坏的索引：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

这将在`indexing-result/index-consistency-check-report.txt`中生成报告。 有关示例报表，请参阅下文：

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

### 优点 {#uc1benefits}

支持人员和系统管理员现在可以使用此工具快速确定哪些索引已损坏，然后重新编入索引。

## 用例2 — 索引统计 {#usecase2indexstatistics}

为了诊断查询性能Adobe的某些情况，通常需要现有索引定义，需要从客户设置中索引相关统计信息。 到目前为止，这些信息分散在多个资源中。 为了更轻松地进行故障诊断，Adobe创建了工具，工具将：

1. 将系统上存在的所有索引定义转储到一个JSON文件中；

1. 从现有索引中转储重要统计信息；

1. 转储索引内容以进行离线分析；

1. 即使AEM无法访问，也将可用

现在可以通过以下操作索引命令完成上述操作：

* `--index-info`  — 收集和转储与索引相关的各种统计信息

* `--index-definitions`  — 收集和转储索引定义

* `--index-dump`  — 转储索引内容

请参阅下面命令在实践中的工作原理示例：

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

将在`indexing-result/index-info.txt`和`indexing-result/index-definitions.json`中生成报告

此外，还通过Web控制台提供了相同的详细信息，这些信息将包含在配置转储zip文件中。 可在以下位置访问它们：

`https://serverhost:serverport/system/console/status-oak-index-defn`

### 优点 {#uc2benefits}

此工具能够快速收集与索引或查询问题相关的所有必需详细信息，并减少提取此信息所花费的时间。

## 用例3 — 重新索引 {#usecase3reindexing}

根据[情景](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)，在某些情况下需要执行重新索引。 目前，可通过CRXDE或通过索引管理器用户界面将`reindex`标记设置为索引定义节点中的`true`来完成重新索引。 标记设置完成后，将异步重新编入索引。

有关重新索引的一些注意事项：

* 与所有内容都是本地的`SegmentNodeStore`设置相比，`DocumentNodeStore`设置的索引重新建立速度要慢得多；

* 使用当前设计时，如果重新编制索引，则异步索引器会被阻止，并且所有其他异步索引都会失效，并且在索引期间不会获取更新。 因此，如果系统正在使用，用户可能看不到最新的结果；
* 重新索引涉及遍历整个存储库，这会给AEM设置带来高负载，从而影响最终用户体验；
* 对于`DocumentNodeStore`安装，重新编制索引可能需要相当长的时间，如果与Mongo数据库的连接在操作中间失败，则必须从头开始重新编制索引；

* 在某些情况下，由于文本提取，重新索引可能需要很长时间。 这主要适用于具有大量PDF文件的设置，在这些设置中，文本提取所花费的时间可能会影响索引时间。

为实现这些目标，oak-run索引工具支持不同的重新索引模式，这些模式可以根据需要使用。 oak-run index命令具有以下优势：

* **带外重新索引**  - oak-run重新索引可以与正在运行的AEM设置分开执行，从而最大限度地减少对正在使用的AEM实例的影响；

* **异地重新索引**  — 重新索引在不影响索引操作的情况下进行。这意味着异步索引器可以继续索引其他索引；

* **简化了DocumentNodeStore安装的重新索引**  — 对于 `DocumentNodeStore` 安装，只需使用一个命令即可重新索引，这可确保以最佳方式重新索引；

* **支持更新索引定义并引入新的索引定义**

### 重新索引 — DocumentNodeStore {#reindexdocumentnodestore}

对于`DocumentNodeStore`安装，可通过单个oak-run命令完成重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

这具备以下优势

* 对运行AEM实例的影响最小。 大多数读取操作都可从辅助服务器完成，并且运行AEM缓存不会因为重新索引所需的所有遍历而受到影响；
* 用户还可以通过`--index-definitions-file`选项提供新索引或更新索引的JSON。

### 重新索引 — SegmentNodeStore {#reindexsegmentnodestore}

对于`SegmentNodeStore`安装，可通过以下方式之一重新编制索引：

#### 联机重新索引 — SegmentNodeStore {#onlinereindexsegmentnodestore}

通过设置`reindex`标记，按照已建立的方式完成重新索引。

#### 联机重新索引 — SegmentNodeStore -AEM实例正在运行 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

对于`SegmentNodeStore`安装，只有一个进程可以以读写模式访问区段文件。 由于这一原因，在oak-run索引中执行某些操作需要执行额外的手动步骤。

这将涉及以下内容：

1. 步骤文本
1. 将`oak-run`连接到AEM在只读模式下使用的同一存储库并执行索引。 有关如何实现此操作的示例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最后，通过`IndexerMBean#importIndex`操作，从oak-run运行上述命令后保存索引文件的路径中导入创建的索引文件。

在这种情况下，您不必停止AEM服务器或配置任何新实例。 但是，由于索引涉及遍历整个存储库，因此会增加安装的I/O负载，从而对运行时性能产生负面影响。

#### 联机重新索引 — SegmentNodeStore - AEM实例已关闭 {#onlinereindexsegmentnodestoreaeminstanceisdown}

对于`SegmentNodeStore`安装，可通过单个oak-run命令重新建立索引。 但是，需要关闭AEM实例。

您可以使用以下命令触发重新索引：

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

此方法与上述方法的区别在于，检查点创建和索引导入是自动完成的。 缺点是在该过程中AEM需要关闭。

#### 带外重新索引 — SegmentNodeStore {#outofbandreindexsegmentnodestore}

在此用例中，您可以对克隆的设置执行重新索引，以最大限度地减少对运行的AEM实例的影响：

1. 通过JMX操作创建检查点。 为此，您可以转到[JMX控制台](/help/sites-administering/jmx-console.md)并搜索`CheckpointManager`。 然后，单击&#x200B;**createCheckpoint(long p1)**&#x200B;操作，使用高值（以秒为单位）过期(例如，**2592000**)。
1. 将`crx-quickstart`文件夹复制到新计算机
1. 通过oak-run index命令执行重新索引

1. 将生成的索引文件复制到AEM服务器

1. 通过JMX导入索引文件。

在此用例下，假定数据存储可在另一个实例上访问，如果`FileDataStore`被放置在基于云的存储解决方案（如EBS）上，则可能无法访问该实例。 这不包括同样克隆`FileDataStore`的方案。 如果索引定义不执行全文索引，则不需要访问`DataStore`。

## 用例4 — 更新索引定义 {#usecase4updatingindexdefinitions}

目前，您可以通过[ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html)包发送索引定义更改。 这允许通过内容包发送索引定义，后者需要通过将`reindex`标记设置为`true`来执行重新索引。

这非常适用于重新建立索引不需要很长时间的较小安装。 但是，对于非常大的存储库，重新编制索引将在相当长的时间内完成。 对于此类情况，我们现在可以使用oak-run索引工具。

Oak-run现在支持以JSON格式提供索引定义，并在带外模式下创建索引，在带外模式下，实时实例不会执行任何更改。

对于此用例，您需要考虑的流程是：

1. 开发人员将更新本地实例上的索引定义，然后通过`--index-definitions`选项生成索引定义JSON文件

1. 更新的JSON随后将提供给系统管理员
1. 系统管理员遵循带外方法并准备其他安装上的索引
1. 完成此操作后，将在运行AEM安装时导入生成的索引文件。
