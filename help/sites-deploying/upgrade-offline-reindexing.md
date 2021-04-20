---
title: 使用脱机重新索引减少升级期间的停机时间
description: 了解如何使用脱机重新索引方法来减少执行AEM升级时的系统停机时间。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 0%

---


# 使用脱机重新索引减少升级{#offline-reindexing-to-reduce-downtime-during-upgrades}期间的停机时间

## 简介 {#introduction}

升级Adobe Experience Manager的主要挑战之一是在执行就地升级时与作者环境相关的停机时间。 内容作者在升级期间将无法访问环境。 因此，最好尽量缩短执行升级所花费的时间。 对于大型存储库，特别是AEM Assets项目，它们通常拥有大型数据存储和每小时较高的资产上传率，对Oak索引重新编制索引需要占升级时间的相当大比例。

本节介绍如何使用Oak-run工具在执行升级之前重新索引存储库&#x200B;**，从而减少实际升级期间的停机时间。**&#x200B;所显示的步骤可应用于版本AEM 6.4及更高版本的[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)索引。

## 概述 {#overview}

随着功能集的扩展，新版AEM将对Oak索引定义进行更改。 升级AEM实例时，对Oak索引的更改会强制重新索引。 资源部署需要重新索引，因为会提取和索引资源中的文本（例如，pdf文件中的文本）。 使用MongoMK存储库，数据会通过网络持久保存，从而进一步增加重新索引所需的时间。

大多数客户在升级过程中遇到的问题是缩短停机时间。 解决方案是在升级过程中跳过&#x200B;**重新索引活动。**&#x200B;这可以通过创建新内容&#x200B;**之前**&#x200B;来执行升级，然后在升级期间直接导入来实现。

## 方法 {#approach}

![脱机 — 重新索引 — 升级 — 文本 — 提取](assets/offline-reindexing-upgrade-process.png)

其构思是在升级前使用[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)工具根据目标 AEM版本的索引定义创建索引。 上图显示了脱机重新索引的方法。

此外，这是方法中描述的步骤顺序：

1. 首先提取来自二进制文本
2. 目标索引定义已创建
3. 已创建脱机索引
4. 然后在升级过程中导入索引

### 文本提取 {#text-extraction}

要在AEM中启用完整索引，将提取PDF等二进制文本并将其添加到索引中。 这通常是索引过程中一个昂贵的步骤。 文本提取是一个优化步骤，尤其是在资源存储库存储大量二进制文件时，它们重新索引。

![脱机 — 重新索引 — 升级 — 文本 — 提取](assets/offline-reindexing-upgrade-text-extraction.png)

系统中存储的二进制文本可以使用tika库的oak-run工具提取。 可以在升级之前克隆生产系统，并可用于此文本提取过程。 然后，此过程将通过执行以下步骤创建文本存储：

**1. 遍历存储库并收集二进制文件的详细信息**

此步骤将生成一个CSV文件，其中包含一个二进制元组，其中包含一个路径和一个blob ID。

从要创建索引的目录中执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

使用`--fake-ds-path=temp`参数代替`–fds-path`加快进程。

**2.重用现有索引**&#x200B;中可用的二进制文本存储

从现有系统中转储索引数据并提取文本存储。

可以使用以下命令转储现有索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

其中`nodestore path`是`mongo_ur`或`crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中`oak-index-name`是全文索引的名称，例如&quot;lucene&quot;。

**3.使用tika库运行文本提取进程，以查看上面步骤**&#x200B;中遗漏的二进制文件

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中`datastore path`是二进制数据存储的路径。

将来可以更新创建的文本存储并重复使用，以便为重新索引方案。

有关文本提取过程的详细信息，请参阅[Oak-run文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)。

### 脱机重新索引{#offline-reindexing}

![脱机 — 重新索引 — 升级 — 脱机 — 重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升级前脱机创建Lucene索引。 如果使用MongoMK，建议直接在MongoMk节点之一上运行它，因为这样可避免网络开销。

要脱机创建索引，请执行以下步骤：

**1.为目标 AEM版本**&#x200B;生成Oak Lucene索引定义

转储现有索引定义。 使用目标 AEM版本和oak-run的Adobe Granite存储库捆绑包生成了经过更改的索引定义。

要从&#x200B;**source** AEM实例转储索引定义，请运行以下命令：

>[!NOTE]
>
>有关倾倒索引定义的详细信息，请查阅[Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

其中`datastore path`和`nodestore path`来自&#x200B;**source** AEM实例。

然后，使用目标版本的Granite存储库包从&#x200B;**目标** AEM版本生成索引定义。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 仅从`oak-run-1.12.0`版本开始支持上述索引定义创建过程。 使用Granite存储库包`com.adobe.granite.repository-x.x.xx.jar`完成定位。

上述步骤创建名为`merge-index-definitions_target.json`的JSON文件，该文件是索引定义。

**2.在存储库**&#x200B;中创建检查点

在生产&#x200B;**source** AEM实例中创建具有长生命周期的检查点。 应在克隆存储库之前执行此操作。

通过位于`http://serveraddress:serverport/system/console/jmx`的JMX控制台，转到`CheckpointMBean`并创建具有足够长生命周期的检查点（例如，200天）。 为此，请调用`CheckpointMBean#createCheckpoint`(`17280000000`)作为生命周期的参数，以毫秒为单位。

完成此操作后，复制新创建的检查点ID并使用JMX `CheckpointMBean#listCheckpoints`验证生命周期。

>[!NOTE]
>
> 稍后导入索引时，将删除此检查点。

有关详细信息，请参阅Oak文档中的[检查点创建](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)。

**对生成的索引定义执行脱机索引**

Lucene重新索引可以使用oak-run脱机完成。 此进程在`indexing-result/indexes`下的磁盘中创建索引数据。 它&#x200B;**不**&#x200B;写入存储库，因此不需要停止正在运行的AEM实例。 创建的文本存储库将输入此过程：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

`--doc-traversal-mode`参数的使用对于MongoMK安装很方便，因为它通过将存储库内容假脱机到本地平面文件中，显着缩短了重新索引时间。 但是，它需要额外的磁盘空间来多次存储库的大小。

对于MongoMK，如果此步骤是在离MongoDB实例更近的实例中执行的，则可以加速此过程。 如果在同一台计算机上运行，可避免网络开销。

有关索引的[oak-run文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)中提供了其他技术详细信息。

### 导入索引{#importing-indexes}

在AEM 6.4和更新版本中，AEM具有内置功能，可在启动序列时从磁盘导入索引。 文件夹`<repository>/indexing-result/indexes`在启动过程中会监视是否存在索引数据。 在[升级过程](in-place-upgrade.md#performing-the-upgrade)期间，您可以先将预创建的索引复制到上述位置，然后再从新版本的&#x200B;**目标** AEM jar开始。 AEM会将其导入存储库，并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答{#troubleshooting}

在下面，您将找到一些有用的提示和疑难解答说明。

### 减少对实时生产系统{#reduce-the-impact-on-the-live-production-system}的影响

建议克隆生产系统并使用克隆创建脱机索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook和试用版运行{#prepare-a-runbook-and-trial-run}

建议在生产中运行升级之前准备[runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook)并执行一些试用版。

### 脱机索引{#doc-traversal-mode-with-offline-indexing}的文档遍历模式

脱机索引需要对整个存储库进行多次遍历。 在MongoMK安装中，通过网络访问存储库会影响索引过程的性能。 一个选项是在MongoDB副本本身上运行脱机索引过程，这将消除网络开销。 另一个选项是使用doc遍历模式。

可通过将命令行参数`—doc-traversal`添加到oak-run命令以进行脱机索引来应用文档遍历模式。 此模式将本地磁盘中整个存储库的副本作为平面文件进行假脱机，并使用它运行索引。
