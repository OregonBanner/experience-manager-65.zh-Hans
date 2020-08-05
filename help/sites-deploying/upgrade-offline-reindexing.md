---
title: 使用脱机重新索引减少升级期间的停机时间
description: 了解如何在执行AEM升级时使用脱机重新索引方法来减少系统停机时间。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: d3a69bbbc9c3707538be74fd05f94f20a688d860
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# 使用脱机重新索引减少升级期间的停机时间 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 简介 {#introduction}

升级Adobe Experience Manager的一个关键挑战是执行就地升级时与作者环境相关的停机时间。 内容作者在升级过程中将无法访问环境。 因此，最好尽量缩短执行升级所花费的时间。 对于大型存储库，特别是AEM Assets项目，它通常拥有大型数据存储和每小时高级别的资产上传，重新为Oak索引编制索引需要相当大比例的升级时间。

本节介绍如何使用Oak-run工具在执行升级之前 **重新** 索引存储库，从而减少实际升级过程中的停机时间。 所提出的步骤可应用 [于AEM](https://jackrabbit.apache.org/oak/docs/query/lucene.html) 6.4及更高版本的Lucene索引。

## 概述 {#overview}

新版AEM在功能集扩展时对Oak索引定义进行了更改。 升级AEM实例时，对Oak索引所做的更改会强制重新索引。 资产部署需要重新索引，因为会提取和索引资产（例如pdf文件中的文本）中的文本。 使用MongoMK存储库，数据会通过网络持久保存，从而进一步增加重新建立索引所需的时间。

大多数客户在升级过程中遇到的问题是减少停机时间。 解决方案是在 **升级期** 间跳过重新索引活动。 这可以通过以下方式实现：在执行升 **级之前** 创建新的插件，然后在升级过程中直接导入它们。

## 方法 {#approach}

![脱机——重新索引——升级——文本-提取](assets/offline-reindexing-upgrade-process.png)

其构思是在升级前根据目标AEM版本的索引定义使用Oak-run工 [具创建索引](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 。 上图显示了脱机重新索引的方法。

此外，这是方法中所述步骤的顺序：

1. 首先提取二进制文本
2. 目标索引定义已创建
3. 创建脱机索引
4. 然后在升级过程中导入索引

### 文本提取 {#text-extraction}

要在AEM中启用完整索引，将提取来自二进制文本（如PDF）的文本并将其添加到索引中。 这通常是索引过程中一个昂贵的步骤。 文本提取是一个优化步骤，尤其是在资源存储库存储大量二进制文件时，它们应重新索引。

![脱机——重新索引——升级——文本-提取](assets/offline-reindexing-upgrade-text-extraction.png)

系统中存储的二进制文本可以使用tika库中的oak-run工具进行提取。 可以在升级之前克隆生产系统，并可用于此文本提取过程。 然后，此过程将通过执行以下步骤创建文本存储：

**1. 遍历存储库并收集二进制文件的详细信息**

此步骤将生成一个CSV文件，其中包含二进制元组，其中包含路径和blob ID。

从要从中创建索引的目录中执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

位 `nodestore path` 置是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用参 `--fake-ds-path=temp` 数而不 `–fds-path` 是加速进程。

**2. 重用现有索引中可用的二进制文本存储**

从现有系统转储索引数据并提取文本存储。

您可以使用以下命令转储现有索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

位 `nodestore path` 置是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其 `oak-index-name` 中是全文索引的名称，例如“lucene”。

**3. 使用tika库运行文本提取进程，以查看上一步中遗漏的二进制文件**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中 `datastore path` 是二进制数据存储的路径。

将来可以更新创建的文本存储并重复使用，以重新为场景建立索引。

有关文本提取过程的更多详细信息，请 [参阅Oak-run文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 脱机重新索引 {#offline-reindexing}

![脱机——重新索引——升级——脱机——重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升级之前脱机创建Lucene索引。 如果使用MongoMK，建议直接在MongoMk节点之一上运行它，因为这避免了网络开销。

要脱机创建索引，请执行以下步骤：

**1. 为目标AEM版本生成Oak Lucene索引定义**

转储现有索引定义。 使用AdobeAEM版和oak-run的目标Granite存储库捆绑生成了经过更改的索引定义。

要从源AEM实例转储索引 **定义** ，请运行以下命令：

>[!NOTE]
>
>有关倾销指数定义的更多详细信息，请查阅 [Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

来 `datastore path` 自 `nodestore path` 源AEM实例 **的位置** 。

然后，使用目标版的 **Granite** 存储库包从AEM版本生成索引定义。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 上述索引定义创建过程仅从版本开始 `oak-run-1.12.0` 受支持。 定位是使用Granite存储库捆绑完成的 `com.adobe.granite.repository-x.x.xx.jar`。

上述步骤创建名为的JSON文 `merge-index-definitions_target.json` 件，该文件是索引定义。

**2. 在存储库中创建检查点**

在生产源AEM实例中 **创建检查点** ，具有较长的生命周期。 应在克隆存储库之前执行此操作。

通过位于的JMX `http://serveraddress:serverport/system/console/jmx`控制台， `CheckpointMBean` 转到并创建具有足够长生命周期的检查点（例如，200天）。 对于此，调 `CheckpointMBean#createCheckpoint` 用 `17280000000` 为生命周期持续时间的参数（以毫秒为单位）。

完成此操作后，复制新创建的检查点ID并使用JMX验证生命周期 `CheckpointMBean#listCheckpoints`。

>[!NOTE]
>
> 稍后导入索引时，将删除此检查点。

有关详细信息，请参 [阅Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) 中的检查点创建。

**为生成的索引定义执行脱机索引**

Lucene可以使用oak-run脱机完成重新索引。 此过程在磁盘下创建索引数据 `indexing-result/indices`。 它不 **会写入** 存储库，因此不需要停止运行的AEM实例。 创建的文本存储将输入到此过程中：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indices in this file will be re-indexed.
```

在MongoMK安装 `--doc-traversal-mode` 中，使用该参数很方便，因为它通过将存储库内容假脱机到本地平面文件，大大缩短了重新索引时间。 但是，它需要额外的磁盘空间，多次存储库的大小。

对于MongoMK，如果此步骤是在离MongoDB实例更近的实例中执行的，则可以加速此过程。 如果在同一台计算机上运行，则可避免网络开销。

有关索引的其它技术详 [细信息，请参阅oak-run文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)。

### 导入索引 {#importing-indices}

对于AEM 6.4和更高版本，AEM具有内置功能，可在启动序列时从磁盘导入索引。 文件夹 `<repository>/indexing-result/indices` 在启动过程中会监视是否存在索引数据。 在升级过程中，您可以先将预创建的索引复 [制到上述位置](in-place-upgrade.md#performing-the-upgrade) ，然后再从新版本的AEM **jar开始** 。 AEM将其导入存储库并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答 {#troubleshooting}

在下面，您将找到一些有用的提示和疑难解答说明。

### 减少对实时生产系统的影响 {#reduce-the-impact-on-the-live-production-system}

建议克隆生产系统并使用克隆创建脱机索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook和试用版运行 {#prepare-a-runbook-and-trial-run}

建议先准备Runbook [](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) ，然后在生产中运行升级。

### 带有脱机索引的文档遍历模式 {#doc-traversal-mode-with-offline-indexing}

脱机索引需要对整个存储库进行多次遍历。 在MongoMK安装中，通过网络访问存储库会影响索引过程的性能。 一种方法是在MongoDB副本本身上运行脱机索引建立过程，这将消除网络开销。 另一个选项是使用doc遍历模式。

文档遍历模式可以通过向oak-run命令添加命令行参 `—doc-traversal` 数来应用，以便脱机索引。 此模式将本地磁盘中整个存储库的副本作为平面文件假脱机，并使用它运行索引。
