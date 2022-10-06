---
title: 使用离线重新索引以减少升级期间的停机时间
description: 了解如何使用离线重新索引方法来减少执行AEM升级时的系统停机时间。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---

# 使用离线重新索引以减少升级期间的停机时间 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## 简介 {#introduction}

升级Adobe Experience Manager的一个关键挑战是，在执行就地升级时，与创作环境相关的停机时间。 内容作者在升级期间将无法访问该环境。 因此，最好将执行升级所花费的时间最小化。 对于大型存储库(特别是AEM Assets项目)，其通常具有大数据存储和每小时高级别的资产上传，因此重新索引Oak索引占用了升级时间的相当大比例。

本节介绍如何使用Oak-run工具重新索引存储库 **之前** 执行升级，从而减少实际升级期间的停机时间。 所介绍的步骤可应用于 [卢塞内](https://jackrabbit.apache.org/oak/docs/query/lucene.html) AEM 6.4及更高版本的索引。

## 概述 {#overview}

新版AEM在扩展功能集时对Oak索引定义进行了更改。 升级AEM实例时，对Oak索引所做的更改会强制重新索引。 由于资产中的文本（例如pdf文件中的文本）会被提取并编入索引，因此对于资产部署而言，重新索引非常昂贵。 使用MongoMK存储库，数据会通过网络持久保留，从而进一步增加重新索引所需的时间。

大多数客户在升级过程中遇到的问题是缩短停机时间。 解决方案是 **跳过** 升级期间的重新索引活动。 可以通过创建新的索引来实现这一点 **先前** 要执行升级，只需在升级期间导入即可。

## 方法 {#approach}

![脱机 — 重新索引 — 升级 — text-extraction](assets/offline-reindexing-upgrade-process.png)

其构思是在升级之前，使用 [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) 工具。 上图显示了离线重新索引方法。

此外，这是方法中所述步骤的顺序：

1. 首先提取来自二进制文件的文本
2. 已创建目标索引定义
3. 脱机索引已创建
4. 然后，将在升级过程中导入索引

### 文本提取 {#text-extraction}

要在AEM中启用完整索引，将提取来自二进制文件(如PDF)的文本并将其添加到索引中。 在索引过程中，这通常是一个费用高昂的步骤。 文本提取是一个优化步骤，主张在资产存储库存储大量二进制文件时对其重新索引。

![脱机 — 重新索引 — 升级 — text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

使用带有tika库的oak-run工具，可以从系统中存储的二进制文件中提取文本。 可以在升级前克隆生产系统，并可用于此文本提取过程。 然后，此过程会通过执行以下步骤来创建文本存储：

**1. 遍历存储库并收集二进制文件的详细信息**

此步骤将生成一个CSV文件，其中包含二进制文件元组，其中包含路径和Blob ID。

从要从中创建索引的目录中执行以下命令。 以下示例假定存储库主目录。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

其中 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

使用 `--fake-ds-path=temp` 参数而不是 `–fds-path` 来加快进程。

**2. 重复使用现有索引中可用的二进制文本存储**

从现有系统中转储索引数据并提取文本存储。

您可以使用以下命令转储现有索引数据：

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

其中 `nodestore path` 是 `mongo_ur` 或 `crx-quickstart/repository/segmentstore/`

然后，使用上述索引转储填充存储区：

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

其中 `oak-index-name` 是全文索引的名称，例如“lucene”。

**3. 使用tika库为上述步骤中缺失的二进制文件运行文本提取流程**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

其中 `datastore path` 是二进制数据存储的路径。

将来可以更新创建的文本存储并重复使用，以便重新索引方案。

有关文本提取流程的更多详细信息，请参阅 [Oak运行文档](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### 脱机重新索引 {#offline-reindexing}

![脱机 — 重新索引 — 升级 — 脱机 — 重新索引](assets/offline-reindexing-upgrade-offline-reindexing.png)

在升级之前脱机创建Lucene索引。 如果使用MongoMK，建议直接在其中一个MongoMk节点上运行它，因为这样可避免网络开销。

要脱机创建索引，请执行以下步骤：

**1. 为目标AEM版本生成Oak Lucene索引定义**

转储现有索引定义。 更改的索引定义是使用目标AEM版本和oak-run的AdobeGranite存储库包生成的。

从 **来源** AEM实例，运行此命令：

>[!NOTE]
>
>有关倾销指数定义的更多详细信息，请查阅 [Oak文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

其中 `datastore path` 和 `nodestore path` 来自 **来源** AEM实例。

然后，从 **目标** AEM版本（使用target版本的Granite存储库包）。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 仅支持通过 `oak-run-1.12.0` 从版本开始。 使用Granite存储库包完成定位 `com.adobe.granite.repository-x.x.xx.jar`.

上述步骤将创建一个名为 `merge-index-definitions_target.json` 即索引定义。

**2. 在存储库中创建检查点**

在生产中创建检查点 **来源** 存留期较长的AEM实例。 此操作应在克隆存储库之前完成。

通过位于 `http://serveraddress:serverport/system/console/jmx`，转到 `CheckpointMBean` 并创建一个具有足够长生命周期的检查点（例如，200天）。 为此，请调用 `CheckpointMBean#createCheckpoint` with `17280000000` 作为生命周期持续时间的参数（以毫秒为单位）。

完成此操作后，复制新创建的检查点ID并使用JMX验证生命周期 `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> 稍后导入索引时，将删除此检查点。

有关更多详细信息，请查阅 [检查点创建](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) ，请参阅Oak文档。

**为生成的索引定义执行脱机索引**

Lucene可以使用oak-run离线完成重新索引。 此过程会在 `indexing-result/indexes`. 确实如此 **not** 写入存储库，因此不需要停止运行的AEM实例。 创建的文本存储库将馈送到此过程中：

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

使用 `--doc-traversal-mode` 参数在MongoMK安装中非常方便，因为它通过将存储库内容假脱机到本地平面文件中，可显着缩短重新索引时间。 但是，它需要额外的磁盘空间，其大小是存储库的两倍。

对于MongoMK，如果此步骤是在更接近MongoDB实例的实例中执行，则可以加速此过程。 如果在同一台计算机上运行，则可以避免网络开销。

其他技术详细信息可在 [用于索引的oak运行文档](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### 导入索引 {#importing-indexes}

在AEM 6.4及更高版本中，AEM具有在启动序列时从磁盘导入索引的内置功能。 文件夹 `<repository>/indexing-result/indexes` 在启动期间监视索引数据是否存在。 在 [升级过程](in-place-upgrade.md#performing-the-upgrade) 新版本的 **目标** AEM jar。 AEM会将其导入存储库，并从系统中删除相应的检查点。 因此，完全避免了重新索引。

## 其他提示和疑难解答 {#troubleshooting}

在下面，您将找到一些有用的提示和疑难解答说明。

### 减少对实时生产系统的影响 {#reduce-the-impact-on-the-live-production-system}

建议克隆生产系统并使用克隆创建脱机索引。 这消除了对生产系统的任何潜在影响。 但是，生产系统中需要存在导入索引所需的检查点。 因此，在获取克隆之前创建检查点至关重要。

### 准备Runbook和试用运行 {#prepare-a-runbook-and-trial-run}

建议您准备 [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) 和在生产环境中运行升级之前先执行一些试用。

### Doc遍历模式，脱机索引 {#doc-traversal-mode-with-offline-indexing}

脱机索引需要多次遍历整个存储库。 在MongoMK安装中，通过网络访问存储库会影响索引过程的性能。 一个选项是在MongoDB副本本身上运行脱机索引过程，这将消除网络开销。 另一个选项是使用文档遍历模式。

可通过添加命令行参数来应用文档遍历模式 `—doc-traversal` 到oak-run命令进行脱机索引。 此模式将本地磁盘中整个存储库的副本作为平面文件进行处理，并使用它来运行索引。
