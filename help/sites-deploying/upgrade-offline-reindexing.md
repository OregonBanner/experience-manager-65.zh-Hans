---
title: 使用离线重新索引以减少升级期间的停机时间
description: 了解如何使用离线重新索引方法来减少执行AEM升级时的系统停机时间。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: 升级
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 0%

---

# 使用离线重新索引来减少升级期间的停机时间{#offline-reindexing-to-reduce-downtime-during-upgrades}

## 简介 {#introduction}

升级Adobe Experience Manager的一个关键挑战是，在执行就地升级时，与创作环境相关的停机时间。 内容作者在升级期间将无法访问该环境。 因此，最好将执行升级所花费的时间最小化。 对于大型存储库(特别是AEM Assets项目)，其通常具有大数据存储和每小时高级别的资产上传，因此重新索引Oak索引占用了升级时间的相当大比例。

本节介绍如何在执行升级前使用Oak-run工具重新索引存储库&#x200B;**，从而减少实际升级期间的停机时间。**&#x200B;所示步骤可应用于版本AEM 6.4及更高版本的[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)索引。

## 概述 {#overview}

新版AEM在扩展功能集时对Oak索引定义进行了更改。 升级AEM实例时，对Oak索引所做的更改会强制重新索引。 由于资产中的文本（例如pdf文件中的文本）会被提取并编入索引，因此对于资产部署而言，重新索引非常昂贵。 使用MongoMK存储库，数据会通过网络持久保留，从而进一步增加重新索引所需的时间。

大多数客户在升级过程中遇到的问题是缩短停机时间。 解决方案是在升级期间跳过&#x200B;**重新索引活动。**&#x200B;要实现此目的，可先创建新的内部代码&#x200B;**，然后再执行升级，然后只需在升级期间导入它们即可。**

## 方法 {#approach}

![脱机 — 重新索引 — 升级 — text-extraction](assets/offline-reindexing-upgrade-process.png)

其思想是在升级之前，使用[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)工具根据目标AEM版本的索引定义创建索引。 上图显示了离线重新索引方法。

此外，这是方法中所述步骤的顺序：

1. 首先从二进制文件中提取文本
2. 已创建目标索引定义
3. 脱机索引已创建
4. 然后，将在升级过程中导入索引

### 文本提取 {#text-extraction}

要在AEM中启用完整索引，将提取来自二进制文件（如PDF）的文本并将其添加到索引。 在索引过程中，这通常是一个费用高昂的步骤。 文本提取是一个优化步骤，主张在资产存储库存储大量二进制文件时，对其重新索引。

![脱机 — 重新索引 — 升级 — text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

使用带有tika库的oak-run工具，可以从系统中存储的二进制文件中提取文本。 可以在升级前克隆生产系统，并可用于此文本提取过程。 然后，此过程会通过执行以下步骤来创建文本存储：

**1. 遍历存储库并收集二进制文件的详细信息**

此步骤将生成一个CSV文件，其中包含二进制文件元组，其中包含路径和Blob ID。

从要从中创建索引的目录中执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

使用`--fake-ds-path=temp`参数而不是`–fds-path`来加快进程。

**2.重复使用现有索引**&#x200B;中可用的二进制文本存储

从现有系统中转储索引数据并提取文本存储。

您可以使用以下命令转储现有索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储区：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中`oak-index-name`是全文索引的名称，例如“lucene”。

**3.使用tika库为上述步骤**&#x200B;中缺失的二进制文件运行文本提取流程

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中，`datastore path`是二进制数据存储的路径。

将来可以更新创建的文本存储并重复使用，以便重新索引方案。

有关文本提取过程的更多详细信息，请参阅[Oak-run文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 脱机重新索引{#offline-reindexing}

![脱机 — 重新索引 — 升级 — 脱机 — 重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升级之前脱机创建Lucene索引。 如果使用MongoMK，建议直接在其中一个MongoMk节点上运行它，因为这样可避免网络开销。

要脱机创建索引，请执行以下步骤：

**1.为目标AEM版本**&#x200B;生成Oak Lucene索引定义

转储现有索引定义。 更改的索引定义是使用目标AEM版本和oak-run的AdobeGranite存储库包生成的。

要从&#x200B;**source** AEM实例转储索引定义，请运行以下命令：

>[!NOTE]
>
>有关倾倒指数定义的更多详细信息，请参阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

其中`datastore path`和`nodestore path`来自&#x200B;**源** AEM实例。

然后，使用目标版本的Granite存储库包从&#x200B;**target** AEM版本生成索引定义。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 仅从`oak-run-1.12.0`版本开始，才支持上述索引定义创建过程。 使用Granite存储库包`com.adobe.granite.repository-x.x.xx.jar`完成定位。

上述步骤将创建一个名为`merge-index-definitions_target.json`的JSON文件，该文件是索引定义。

**2.在存储库**&#x200B;中创建检查点

在生产&#x200B;**source** AEM实例中创建一个具有较长生命周期的检查点。 此操作应在克隆存储库之前完成。

通过位于`http://serveraddress:serverport/system/console/jmx`的JMX控制台，转到`CheckpointMBean`并创建具有足够长生命周期的检查点（例如，200天）。 为此，请调用`CheckpointMBean#createCheckpoint`，其中`17280000000`作为生命周期的参数（以毫秒为单位）。

完成此操作后，复制新创建的检查点ID并使用JMX `CheckpointMBean#listCheckpoints`验证生命周期。

>[!NOTE]
>
> 稍后导入索引时，将删除此检查点。

有关更多详细信息，请参阅Oak文档中的[检查点创建](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) 。

**为生成的索引定义执行脱机索引**

Lucene可以使用oak-run离线完成重新索引。 此过程会在`indexing-result/indexes`下的磁盘中创建索引数据。 它会&#x200B;**不**&#x200B;写入存储库，因此不需要停止运行的AEM实例。 创建的文本存储库将馈送到此过程中：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

使用`--doc-traversal-mode`参数对于MongoMK安装非常方便，因为它通过将存储库内容假装到本地平面文件中，可显着缩短重新索引时间。 但是，它需要额外的磁盘空间，其大小是存储库大小的两倍。

对于MongoMK，如果此步骤是在更接近MongoDB实例的实例中执行，则可以加速此过程。 如果在同一台计算机上运行，则可以避免网络开销。

有关索引](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)的[oak-run文档中提供了其他技术详细信息。

### 导入索引{#importing-indexes}

在AEM 6.4及更高版本中，AEM具有在启动序列时从磁盘导入索引的内置功能。 在启动期间，会监视文件夹`<repository>/indexing-result/indexes`是否存在索引数据。 在从新版本的&#x200B;**target** AEM jar开始之前，您可以在[升级过程](in-place-upgrade.md#performing-the-upgrade)期间将预创建的索引复制到上述位置。 AEM会将其导入存储库，并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答 {#troubleshooting}

在下面，您将找到一些有用的提示和疑难解答说明。

### 减少对实时生产系统的影响{#reduce-the-impact-on-the-live-production-system}

建议克隆生产系统并使用克隆创建脱机索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook和试用运行{#prepare-a-runbook-and-trial-run}

建议先准备[runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook)并执行一些试用，然后再在生产环境中运行升级。

### 离线索引{#doc-traversal-mode-with-offline-indexing}的文档遍历模式

脱机索引需要多次遍历整个存储库。 在MongoMK安装中，通过网络访问存储库会影响索引过程的性能。 一个选项是在MongoDB副本本身上运行脱机索引过程，这将消除网络开销。 另一个选项是使用文档遍历模式。

可通过将命令行参数`—doc-traversal`添加到oak-run命令以进行脱机索引来应用文档遍历模式。 此模式将本地磁盘中整个存储库的副本作为平面文件进行处理，并使用它来运行索引。
