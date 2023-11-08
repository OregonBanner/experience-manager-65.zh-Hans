---
title: 使用离线重新索引以减少升级期间的停机时间
description: 了解如何使用离线重新索引方法以减少执行AEM升级时的系统停机时间。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 1%

---

# 使用离线重新索引以减少升级期间的停机时间 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 简介 {#introduction}

升级Adobe Experience Manager的主要挑战之一是执行就地升级时与创作环境相关的停机时间。 内容作者在升级期间将无法访问环境。 因此，希望最小化执行升级所需的时间。 对于大型存储库，特别是AEM Assets项目，通常具有大型数据存储和每小时高级别的资源上传，重新索引Oak索引需要花费升级时间的很大百分比。

本节介绍如何使用Oak-run工具重新索引资料档案库 **早于** 执行升级，从而减少实际升级期间的停机时间。 所介绍的步骤适用于 [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) AEM 6.4及更高版本的索引。

## 概述 {#overview}

随着功能集的扩展，新版本的AEM引入了Oak索引定义的更改。 对Oak索引所做的更改会在升级AEM实例时强制重新索引。 由于资源中的文本（例如PDF文件中的文本）被提取并编制索引，因此重新索引对于资源部署而言代价高昂。 使用MongoMK存储库，数据通过网络保留，从而进一步增加重新索引所花费的时间。

大多数客户在升级过程中面临的问题是缩短停机时间。 解决方案是 **跳过** 在升级期间重新索引活动。 这可以通过创建新指令来实现 **优先** 执行升级，然后在升级期间直接导入它们。

## 方针 {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

其思想是在升级之前使用，根据目标AEM版本的索引定义创建索引 [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 工具。 上图显示了离线重新索引方法。

此外，这是方法中描述的步骤顺序：

1. 首先提取二进制文件中的文本
2. 将创建目标索引定义
3. 已创建脱机索引
4. 然后，在升级过程中导入索引

### 文本提取 {#text-extraction}

要在AEM中启用完全索引，将提取二进制文件(如PDF)中的文本并将其添加到索引中。 在索引过程中，这通常是代价高昂的步骤。 文本提取是一个优化步骤，尤其适合在资产存储库存储大量二进制文件时对其重新编制索引。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

使用带有tika库的oak-run工具，可以提取存储在系统中的二进制文件中的文本。 可以在升级之前克隆生产系统，并可用于此文本提取过程。 然后，此过程将执行以下步骤来创建文本存储：

**1. 遍历资料档案库并收集二进制文件的详细信息**

此步骤会生成一个包含二进制文件元组的CSV文件，其中包含一个路径和一个blob ID。

从要创建索引的目录执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用 `--fake-ds-path=temp` 参数而不是 `–fds-path` 以加快进程。

**2. 重用现有索引中可用的二进制文本存储**

从现有系统中转储索引数据并提取文本存储。

可以使用以下命令转储现有的索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

位置 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

位置 `oak-index-name` 是全文索引的名称，例如“lucene”。

**3. 使用tika库为上述步骤中错过的二进制文件运行文本提取过程**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

位置 `datastore path` 是二进制数据存储的路径。

创建的文本存储区可以更新，并可在将来重新索引方案。

有关文本提取过程的更多详细信息，请参阅 [Oak-run文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### 脱机重新索引 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升级前脱机创建Lucene索引。 如果使用MongoMK，则建议直接在某个MongoMk节点上运行它，因为这可避免网络开销。

要脱机创建索引，请执行以下步骤：

**1. 为目标AEM版本生成Oak Lucene索引定义**

转储现有的索引定义。 发生更改的索引定义是使用目标AEM版本的AdobeGranite存储库包和oak-run生成的。

转储中的索引定义 **源** AEM实例，运行此命令：

>[!NOTE]
>
>有关转储索引定义的更多详细信息，请参阅 [Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

位置 `datastore path` 和 `nodestore path` 来自 **源** AEM实例。

然后，从生成索引定义 **目标** 使用AEM版本的Granite存储库包的Granite版本。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>仅支持以上索引定义创建过程 `oak-run-1.12.0` 版本开始。 使用Granite存储库包进行定位 `com.adobe.granite.repository-x.x.xx.jar`.

上述步骤会创建一个名为的JSON文件 `merge-index-definitions_target.json` 即索引定义。

**2. 在存储库中创建检查点**

在生产中创建检查点 **源** 生命周期较长的AEM实例。 此操作应在克隆存储库之前完成。

通过位于的JMX控制台 `http://serveraddress:serverport/system/console/jmx`，转到 `CheckpointMBean` 并创建一个具有足够长的生命周期（例如，200天）的检查点。 为此，调用 `CheckpointMBean#createCheckpoint` 替换为 `17280000000` 作为生命周期持续时间（以毫秒为单位）的参数。

完成此操作后，复制新创建的检查点ID并使用JMX验证生命周期 `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>此检查点将在稍后导入索引时删除。

欲知更多详情，请参阅 [检查点创建](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) 来自Oak文档。

**为生成的索引定义执行脱机索引**

可以使用oak-run离线完成Lucene重新索引。 此进程在下面的磁盘中创建索引数据 `indexing-result/indexes`. 确实如此 **非** 写入存储库，因此不需要停止正在运行的AEM实例。 创建的文本存储将馈送到此进程：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

的使用情况 `--doc-traversal-mode` 使用MongoMK安装时，参数非常方便，因为它通过将存储库内容假脱机到本地平面文件来显着缩短重新索引时间。 但是，它需要两倍于存储库大小的额外磁盘空间。

如果存在MongoMK，则如果在更靠近MongoDB实例的实例中执行此步骤，则可以加快此进程。 如果在同一台计算机上运行，则可以避免网络开销。

欲知其他技术详情，请访问 [oak-run索引文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### 导入索引 {#importing-indexes}

使用AEM 6.4及更高版本，AEM具有按启动顺序从磁盘导入索引的内置功能。 文件夹 `<repository>/indexing-result/indexes` 在启动期间观察是否存在索引数据。 在执行以下操作期间，您可以将预先创建的索引复制到上述位置 [升级过程](in-place-upgrade.md#performing-the-upgrade) 在开始使用新版本的 **目标** AEM jar。 AEM会将其导入到存储库中，并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答 {#troubleshooting}

在下方，您将找到一些有用的提示和故障排除说明。

### 减少对实时生产系统的影响 {#reduce-the-impact-on-the-live-production-system}

建议克隆生产系统并使用克隆创建离线索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook并试运行 {#prepare-a-runbook-and-trial-run}

建议准备 [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 并在生产环境中运行升级之前，执行一些试验。

### 带脱机索引的文档遍历模式 {#doc-traversal-mode-with-offline-indexing}

离线索引需要遍历整个存储库。 使用MongoMK安装时，通过网络访问存储库会影响索引过程的性能。 一种选择是在MongoDB副本本身上运行离线索引过程，这将消除网络开销。 另一个选项是使用文档遍历模式。

可以通过添加命令行参数来应用文档遍历模式 `—doc-traversal` 到oak-run命令以进行离线索引。 此模式将本地磁盘中整个存储库的副本作为平面文件卷动，并使用它来运行索引。
