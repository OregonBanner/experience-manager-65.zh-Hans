---
title: 带有MongoDB的Adobe Experience Manager
description: 了解成功使用MongoDB部署Adobe Experience Manager所需的任务和注意事项。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '6184'
ht-degree: 0%

---

# 带有MongoDB的Adobe Experience Manager{#aem-with-mongodb}

本文意在增进对使用MongoDB成功部署AEM (Adobe Experience Manager)所必需的任务和注意事项的了解。

有关更多与部署相关的信息，请参阅 [部署和维护](/help/sites-deploying/deploy.md) 一节。

## 何时将MongoDB与AEM一起使用 {#when-to-use-mongodb-with-aem}

MongoDB通常用于支持符合以下条件之一的AEM创作部署：

* 每天超过1000个独特用户；
* 并发用户超过100个；
* 大量页面编辑；
* 大型转出或激活。

上述标准仅适用于创作实例，不适用于所有应基于TarMK的任何发布实例。 用户数是指经过身份验证的用户，因为创作实例不允许进行未经身份验证的访问。

如果不满足标准，则建议使用TarMK活动/备用部署来解决可用性问题。 通常，在缩放要求超过单项硬件所能达到的要求时，应考虑使用MongoDB。

>[!NOTE]
>
>有关创作实例的大小和并发用户定义的其他信息，请参阅 [硬件大小调整准则](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### 针对AEM的最小MongoDB部署 {#minimal-mongodb-deployment-for-aem}

以下是MongoDB上AEM的最低部署。 为简单起见，已推广SSL终止和HTTP代理组件。 它包含一个MongoDB副本集，包括一个主副本集和两个辅助副本集。

![chlimage_1-4](assets/chlimage_1-4.png)

最低的部署需要三个 `mongod` 配置为复制副本集的实例。 一个实例被选为初级实例，而其他实例被选为次级实例，该选举由管理 `mongod`. 连接到每个实例的是本地磁盘。 因此，群集可以支持该负载，建议最小吞吐量为每秒12 MB，并且每秒I/O操作(IOPS)超过3000个。

AEM作者已连接到 `mongod` 实例，每个AEM作者都连接到所有三个 `mongod` 实例。 写操作被发送到主数据库，并且可以从任何实例读取数据。 流量根据Dispatcher的负载分发到任何一个活动的AEM创作实例。 Oak数据存储是 `FileDataStore`和MongoDB监控由MMS或MongoDB Ops Manager提供，具体取决于部署的位置。 操作系统级别和日志监控由第三方解决方案（如Splunk或Ganglia）提供。

在此部署中，需要所有组件才能成功实施。 任何缺少的组件都会使实施无法正常运行。

### 操作系统 {#operating-systems}

有关AEM 6支持的操作系统的列表，请参见 [“技术要求”页面](/help/sites-deploying/technical-requirements.md).

### 环境 {#environments}

如果运行项目的不同技术团队之间通信良好，则支持虚拟化环境。 这种支持包括运行AEM的团队、拥有操作系统的团队以及管理虚拟化基础架构的团队。

有些特定要求涵盖MongoDB实例的I/O容量，这些要求必须由管理虚拟化环境的团队进行管理。 如果项目使用云部署(如Amazon Web Services)，则必须为实例配置足够的I/O容量和一致性，以支持MongoDB实例。 否则，MongoDB进程和Oak存储库会不可靠和不稳定地执行。

在虚拟化环境中，MongoDB需要特定的I/O和VM配置，以确保MongoDB的存储引擎不会受到VMWare资源分配策略的损害。 成功的实施可确保各个团队之间不存在障碍，并且所有团队都已注册以提供所需的性能。

## 硬件注意事项 {#hardware-considerations}

### 存储 {#storage}

为实现最佳性能的读写吞吐量，而无需过早进行水平扩展，MongoDB通常需要SSD存储或性能相当于SSD的存储。

### RAM {#ram}

使用MMAP存储引擎的MongoDB版本2.6和3.0要求数据库的工作集及其索引适应RAM。

RAM不足会导致性能显着降低。 工作集和数据库的大小与应用程序高度相关。 虽然可以做出一些估计，但确定所需RAM数量的最可靠方法是构建AEM应用程序并对其进行负载测试。

为了帮助执行负载测试过程，可以假定工作集与数据库总大小的比率如下：

* 固态硬盘存储为1:10
* 硬盘存储为1:3

这些比率意味着对于SSD部署，2 TB的数据库需要200 GB的RAM。

MongoDB 3.0中的WiredTiger存储引擎也存在同样的限制，但工作集、RAM和页面故障之间的相关性并不强。 WiredTiger使用的内存映射与MMAP存储引擎不同。

>[!NOTE]
>
>Adobe建议对使用MongoDB 3.0的AEM 6.1部署使用WiredTiger存储引擎。

### 数据存储 {#data-store}

由于MongoDB工作集限制，建议独立于MongoDB维护数据存储。 在大多数环境中， `FileDataStore` 应使用可用于所有AEM实例的NAS。 对于使用Amazon Web Services的情况，还有 `S3 DataStore`. 如果出于任何原因，数据存储在MongoDB中维护，则数据存储的大小应添加到总数据库大小中，并且工作集计算应进行适当的调整。 此大小调整可能意味着预配更多RAM以保持性能，而不会出现页面故障。

## 监测 {#monitoring}

监测对于项目的成功实施至关重要。 在充分了解的情况下，可以在MongoDB上运行AEM而不进行监视。 但是，这些知识通常由专门处理部署每个部分的工程师掌握。

这些专门知识通常涉及使用Apache Oak Core的研发工程师和MongoDB专家。

如果没有在所有级别进行监控，则需要具备详细的代码库知识才能诊断问题。 在主要统计数据得到适当监测和指导后，实施团队可以对异常作出适当反应。

虽然可以使用命令行工具快速获取群集操作的快照，但要在许多主机上实时执行此操作几乎是不可能的。 命令行工具很少在几分钟后提供历史信息，并且永远不允许不同类型的量度之间相互关联。 一段短暂的慢速背景 `mongod` 同步需要大量手动操作，以便与似乎未连接的虚拟机向共享存储资源的I/O等待或过度写入级别相关联。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的免费服务，用于监视和管理MongoDB实例。 它提供了实时查看MongoDB群集的性能和运行状况的视图。 它同时管理云实例和私有托管实例，前提是实例可以访问Cloud Manager监控服务器。

它要求在MongoDB实例上安装连接到监控服务器的代理。 代理分为三个级别：

* 能够完全自动化MongoDB服务器上所有内容的自动化代理，
* 可以监视的监视代理 `mongod` 实例，
* 可对数据进行定时备份的备份代理。

虽然使用Cloud Manager来自动维护MongoDB群集使许多例行任务更加容易，但它不是必需的，也不用于备份。 但是，在选择Cloud Manager进行监视时，需要监视。

有关MongoDB Cloud Manager的更多信息，请参阅 [MongoDB文档](https://docs.cloud.mongodb.com/).

### MongoDB操作管理器 {#mongodb-ops-manager}

MongoDB Ops Manager与MongoDB Cloud Manager是相同的软件。 注册后，可以下载Ops Manager并在本地安装在私有数据中心或任何其他笔记本电脑或台式机上。 它使用本地MongoDB数据库存储数据，并以与Cloud Manager相同的方式与受控服务器进行通信。 如果您的安全策略禁止监视代理，则应使用MongoDB Ops Manager。

### 操作系统监控 {#operating-system-monitoring}

运行AEM MongoDB群集需要操作系统级别的监控。

Ganglia是此类系统的一个良好示例，它提供了所需信息的范围和详细信息，这些信息超出基本运行状况指标，如CPU、平均负载和可用磁盘空间。 要诊断问题，需要较低级别的信息，例如熵池级别、CPU I/O等待、处于FIN_WAIT2状态的套接字。

### 日志聚合 {#log-aggregation}

对于由多台服务器组成的群集，生产系统要求进行中央日志聚合。 Splunk等软件支持日志聚合，允许团队分析应用程序的行为模式，而无需手动收集日志。

## 核对清单 {#checklists}

本部分介绍在实施项目之前，为确保正确设置AEM和MongoDB部署而应执行的各个步骤。

### 网络 {#network}

1. 首先，确保所有主机都有DNS条目
1. 所有主机应该可以通过其DNS条目从所有其他可路由主机中解析
1. 所有MongoDB主机均可从同一群集中的所有其他MongoDB主机路由
1. MongoDB主机可以将数据包路由到MongoDB Cloud Manager和其他监控服务器
1. AEM Server可以将数据包路由到所有MongoDB服务器
1. 任何AEM服务器与任何MongoDB服务器之间的数据包延迟都小于2毫秒，没有数据包丢失，标准分布为1毫秒或更少。
1. 确保AEM与MongoDB服务器之间的跃点数不超过两个
1. 两个MongoDB服务器之间的跳数不能超过两个
1. 任何核心服务器(MongoDB或AEM或任何组合)之间都没有高于OSI级别3的路由器。
1. 如果使用VLAN中继或任何形式的网络隧道，则必须遵守数据包延迟检查。

### AEM配置 {#aem-configuration}

#### 节点存储配置 {#node-store-configuration}

必须将AEM实例配置为将AEM与MongoMK一起使用。 AEM中MongoMK实现的基础是文档节点存储。

有关如何配置节点存储的详细信息，请参阅 [在AEM中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md).

以下是最小MongoDB部署的Document Node Store配置示例：

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

其中：

* `mongodburi`
MongoDB服务器AEM必须连接到。 与默认复制副本集的所有已知成员建立连接。 如果使用MongoDB Cloud Manager，则启用服务器安全性。 因此，连接字符串必须包含合适的用户名和密码。 MongoDB的非企业版本仅支持用户名和密码身份验证。 有关连接字符串语法的更多信息，请参阅 [文档](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
数据库的名称。 AEM的默认值为 `aem-author`.

* `customBlobStore`
如果部署将二进制文件存储在数据库中，则它们构成工作集的一部分。 因此，建议不要在MongoDB中存储二进制文件，更喜欢替代数据存储，如 `FileSystem` NAS上的数据存储。

* `cache`
高速缓存大小(MB)。 此空间分布在 `DocumentNodeStore`. 默认值为256 MB。 但是，Oak读取性能受益于较大的缓存。

* `blobCacheSize`
AEM可能会缓存经常使用的Blob，以避免从数据存储中重新获取它们。 这样做对性能影响更大，尤其是在MongoDB数据库中存储Blob时。 所有基于文件系统的Data Stores都受益于操作系统级别的磁盘缓存。

#### 数据存储配置 {#data-store-configuration}

数据存储用于存储大于阈值的文件。 低于该阈值时，文件将作为属性存储在文档节点存储中。 如果 `MongoBlobStore` 之后，将在MongoDB中创建专用收藏集来存储Blob。 此收藏集对的工作集有 `mongod` 实例，并要求 `mongod` 具有更多内存以避免性能问题。 因此，建议的配置是避免 `MongoBlobStore` 用于生产部署和使用 `FileDataStore` 由在所有AEM实例之间共享的NAS作为后盾。 由于操作系统级缓存可以高效地管理文件，因此磁盘上文件的最小大小应设置为接近磁盘的块大小。 这样做可确保文件系统得到有效使用，并且许多小文档不会过度影响的工作集 `mongod` 实例。

以下是使用MongoDB进行最低AEM部署的典型数据存储配置：

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

其中：

* `minRecordLength`
字节大小。 小于或等于此大小的二进制文件存储在文档节点存储中。 存储二进制文件的内容而不是存储blob的ID。 对于大于此大小的二进制文件，二进制文件的ID将作为Document的属性存储在节点集合中。 而且，二进制文件的正文存储在 `FileDataStore` 在磁盘上。 4096字节是典型的文件系统块大小。

* `path`
数据存储根的路径。 对于MongoMK部署，此路径必须是所有AEM实例都可用的共享文件系统。 通常使用网络连接存储(NAS)服务器。 对于Amazon Web Services等云部署， `S3DataFileStore` 也可用。

* `cacheSizeInMB`
二进制缓存的总大小（以MB为单位）。 它用于缓存小于以下值的二进制文件 `maxCacheBinarySize` 设置。

* `maxCachedBinarySize`
二进制缓存中缓存的二进制文件的最大大小（以字节为单位）。 如果使用基于文件系统的数据存储，则建议不要为数据存储缓存使用高值，因为操作系统已缓存二进制文件。

#### 禁用查询提示 {#disabling-the-query-hint}

建议您通过添加属性来禁用随所有查询一起发送的查询提示 `-Doak.mongo.disableIndexHint=true` 启动AEM时。 这样做可确保MongoDB根据内部统计数据计算使用的最合适的索引。

如果未禁用查询提示，则索引的任何性能调整都不会影响AEM的性能。

#### 为MongoMK启用永久缓存 {#enable-persistent-cache-for-mongomk}

建议为MongoDB部署启用持久缓存配置，以便最大化具有高I/O读取性能的环境的速度。 欲知更多详情，请参见 [Jackrabbit Oak文档](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB操作系统优化 {#mongodb-operating-system-optimizations}

### 操作系统支持 {#operating-system-support}

MongoDB 2.6使用内存映射存储引擎，该引擎对RAM和磁盘之间操作系统级别管理的某些方面很敏感。 MongoDB实例的查询和读取性能依赖于避免或消除通常称为页面错误的慢速I/O操作。 这些问题都是适用于 `mongod` 尤其是流程。 不要与操作系统级别的页面错误混淆。

为了快速操作，MongoDB数据库应仅访问RAM中已存在的数据。 它必须访问的数据由索引和数据组成。 此索引和数据集合称为工作集。 当工作集大于可用RAM时，MongoDB必须从磁盘中分页该数据，从而产生I/O开销，并逐出内存中已有的其他数据。 如果逐出导致从磁盘重新加载数据，则页面故障会占主导地位，性能会降低。 如果工作集是动态的、可变的，则会产生更多的页面错误来支持操作。

MongoDB运行在多种操作系统上，包括各种Linux®风格、Windows和macOS。 请参阅 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 以了解更多详细信息。 根据您选择的操作系统，MongoDB具有不同的操作系统级别建议。 文档位于 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 为了方便起见，请单击此处进行总结。

#### Linux® {#linux}

* 关闭透明的拥抱和碎片整理。 请参阅 [透明的大页面设置](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 以了解更多信息。
* [调整预读设置](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 在存储数据库文件的设备上，以适合您的用例。

   * 对于MMAPv1存储引擎，如果您的工作集大于可用的RAM，并且文档访问模式是随机的，请考虑将预读数降低到32或16。 评估不同的设置，以便找到使驻留内存最大化并降低页面错误数的最佳值。
   * 对于WiredTiger存储引擎，无论存储介质类型（旋转、SSD等）如何，均将预读设置为0。 通常，使用推荐的预读设置，除非测试显示可在更高的预读值中获得可衡量、可重复和可靠的好处。 [MongoDB Professional支持](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可以为非零预读配置提供建议和指导。

* 如果在虚拟环境中运行RHEL 7 / CentOS 7，请禁用优化工具。
* 当RHEL 7/CentOS 7在虚拟环境中运行时，优化工具会自动调用从性能吞吐量派生的性能配置文件，该配置文件会自动将预读设置设置为4 MB。 此设置可能会对性能产生负面影响。
* 为SSD驱动器使用空磁盘调度程序或截止日期磁盘调度程序。
* 对来宾VM中的虚拟化驱动器使用noop磁盘调度程序。
* 禁用NUMA或设置 `vm.zone_reclaim_mode` 到0并运行 [蒙古](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有节点交织的实例。 请参阅： [MongoDB和NUMA硬件](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 以了解更多信息。

* 调整硬件上的极限值，使其适合您的使用情形。 如果多个 [蒙古](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古族](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 实例在同一用户下运行，请相应地缩放极限值。 请参阅： [UNIX® ulimit设置](https://docs.mongodb.com/manual/reference/ulimit/) 以了解更多信息。

* 使用noatime进行 [数据库路径](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 装入点。
* 为部署配置足够的文件句柄(fs.file-max)、内核pid限制(kernel.pid_max)和每个进程的最大线程数(kernel.threads-max)。 对于大型系统，以下值是一个很好的起点：

   * fs.file-max值98000，
   * kernel.pid_max值64000，
   * andkernel.threads-64000的最大值

* 确保系统已配置交换空间。 有关适当大小的详细信息，请参阅操作系统的文档。
* 确保正确设置系统默认的TCP keepalive。 值为300通常为副本集和共享群集提供更好的性能。 请参阅： [TCP keepalive时间是否影响MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) ，以了解更多信息。

#### Windows {#windows}

* 请考虑禁用NTFS“上次访问时间”更新。 此设置类似于在类似Unix的系统上禁用atime。

### WiredTiger {#wiredtiger}

从MongoDB 3.2开始，MongoDB的默认存储引擎是WiredTiger存储引擎。 此引擎提供了一些强大且可扩展的功能，使其更适合各种通用数据库工作负载。 以下各节介绍了这些功能。

#### 文档级别并发 {#document-level-concurrency}

WiredTiger使用文档级并发控制执行写入操作。 因此，多个客户端可以同时修改收藏集的不同文档。

对于大多数读写操作， WiredTiger使用乐观的并发控制。 WiredTiger仅使用全局、数据库和收集级别的意图锁。 当存储引擎检测到两个操作之间的冲突时，其中一个操作会发生写入冲突，导致MongoDB透明地重试该操作。 某些全局操作（通常为涉及多个数据库的短期操作）仍需要全局“实例范围”锁定。

某些其他操作（如删除集合）仍需要独占数据库锁。

#### 快照和检查点 {#snapshots-and-checkpoints}

WiredTiger使用MultiVersion Concurrency Control (MVCC)。 在开始操作时， WiredTiger为事务提供数据的时间点快照。 快照呈现内存中数据的一致视图。

在写入磁盘时，WiredTiger会以一致的方式将所有快照中的数据写入磁盘。 现在 —  [持久](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 数据充当数据文件中的检查点。 检查点确保数据文件与上一个检查点一致，包括上一个检查点。 即，检查点可以充当恢复点。

MongoDB配置WiredTiger以60秒或2 GB的日志数据为间隔创建检查点（即将快照数据写入磁盘）。

在写入新检查点期间，上一个检查点仍然有效。 因此，即使MongoDB在写入新检查点时终止或遇到错误，在重新启动时，MongoDB也可以从最后一个有效检查点恢复。

当WiredTiger的元数据表自动更新以引用新检查点时，新检查点将变为可访问且永久性的。 一旦新检查点可供访问，WiredTiger将从旧检查点释放页面。

使用WiredTiger，即使没有 [日记](https://docs.mongodb.com/manual/reference/glossary/#term-durable)，MongoDB可以从上一个检查点恢复；但是，要恢复在上一个检查点之后所做的更改，请使用运行 [日记](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 日志 {#journal}

WiredTiger使用预写事务登录组合 [检查点](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 以确保数据持久性。

WiredTiger日志会在检查点之间保留所有数据修改。 如果MongoDB在检查点之间退出，则它使用日志重放自上次检查点以来修改的所有数据。 有关MongoDB将日志数据写入磁盘的频率的信息，请参见 [日志处理过程](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger日志使用 [跳动](https://docs.mongodb.com/manual/core/journaling/#journal-process) 压缩库。 要指定替代压缩算法或不压缩，请使用 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 设置。

请参阅 [与WiredTiger进行日记](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger的最小日志记录大小为128字节。 如果日志记录为128字节或更小，则WiredTiger不压缩该记录。
>
>您可以通过设置禁用日志记录 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 设置为false，这可以降低维护日志的开销。
>
>对象 [独立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 实例，而不使用日志意味着当MongoDB在检查点之间意外退出时，您将丢失某些数据修改。 对于成员 [副本集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)因此，复制过程可以提供足够的耐久性保证。

#### 压缩 {#compression}

使用WiredTiger时，MongoDB支持对所有集合和索引进行压缩。 压缩以牺牲额外的CPU为代价，将存储使用降至最低。

默认情况下，WiredTiger使用块压缩 [跳动](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 所有收藏集和的压缩库 [前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) 用于所有索引。

对于收藏集，使用块压缩 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 也可用。 要指定替代压缩算法或不压缩，请使用 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 设置。

对于索引，禁用 [前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 设置。

压缩设置也可以在集合和索引创建期间基于每个集合和每个索引进行配置。 请参阅 [指定存储引擎选项](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 选项。

对于大多数工作负载，默认压缩设置可平衡存储效率和处理要求。

默认情况下，WiredTiger日志也会被压缩。 有关日记帐压缩的信息，请参阅 [日志](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 内存使用 {#memory-use}

使用WiredTiger时，MongoDB同时使用WiredTiger内部缓存和文件系统缓存。

从3.4开始，默认情况下，WiredTiger内部缓存使用以下两者中较大的一个：

* 50%的RAM减去1 GB，或
* 256兆字节

默认情况下，WiredTiger对所有集合使用Snappy块压缩，对所有索引使用前缀压缩。 压缩默认值可在全局级别进行配置，也可在集合和索引创建期间基于集合和索引进行设置。

WiredTiger内部缓存中的数据与磁盘格式的数据使用不同的表示形式：

* 文件系统缓存中的数据与磁盘上的格式相同，包括任何数据文件压缩的优点。 操作系统使用文件系统缓存来减少磁盘I/O。

加载到WiredTiger内部缓存中的索引与磁盘格式的数据表示不同，但仍可以利用索引前缀压缩来减少RAM使用量。

索引前缀压缩从索引字段中去除重复的公共前缀。

在WiredTiger内部缓存中的收集数据是未压缩的，并且使用与磁盘格式不同的表示方式。 数据块压缩可以显着节省磁盘上的存储空间，但是数据必须解压缩才能由服务器操作。

通过文件系统缓存，MongoDB自动使用WiredTiger缓存或其他进程未使用的所有可用内存。

要调整WiredTiger内部缓存的大小，请参见 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). 避免将WiredTiger内部缓存的大小增加到超过其默认值。

### NUMA {#numa}

NUMA（非统一内存访问）允许内核管理如何将内存映射到处理器内核。 尽管此过程尝试使核心的内存访问速度更快，以确保它们能够访问所需数据，但NUMA会干扰MMAP，引入额外的延迟，因为无法预测读取次数。 因此，必须为禁用NUMA `mongod` 会在所有支持该功能的操作系统上进行处理。

实质上，在NUMA体系结构中，存储器连接到CPU，CPU连接到总线。 在SMP或UMA体系结构中，内存连接到总线并由CPU共享。 当线程在NUMA CPU上分配内存时，它会根据策略进行分配。 缺省值是分配连接到线程的本地CPU的内存，除非没有可用内存，否则此时它会以较高的成本使用可用CPU的内存。 分配后，内存不会在CPU之间移动。 分配由从父线程（最终是启动进程的线程）继承的策略执行。

在许多将计算机视为多核统一内存体系结构的数据库中，这种情形会导致初始CPU先被占满，然后次要CPU被占满。 如果中心线程负责分配内存缓冲区，则尤其如此。 解决方案是更改用于启动 `mongod` 通过运行以下命令来处理：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略以循环方式为所有CPU节点分配内存，确保所有节点上的内存分布均匀。 与具有多个CPU硬件的系统不同，它不会产生对内存的最高性能访问。 大约一半的内存操作速度较慢，而且是在总线上执行的，但是 `mongod` 并未以最佳方式针对NUMA，因此这是一个合理的折衷方案。

### NUMA问题 {#numa-issues}

如果 `mongod` 进程是从其他位置启动的 `/etc/init.d` 文件夹，可能尚未使用正确的NUMA策略开始。 根据默认策略的不同，可能会出现问题。 原因是用于MongoDB的各种Linux® Package Manager安装程序也安装了包含配置文件的服务 `/etc/init.d` ，以执行上述步骤。 如果直接从归档安装和运行MongoDB ( `.tar.gz`)，您必须手动运行 `numactl` 进程。

>[!NOTE]
>
>有关可用NUMA政策的更多信息，请参阅 [numactl文档](https://linux.die.net/man/8/numactl).

MongoDB进程在不同的分配策略下的行为有所不同：

```

```

* `-membind=<nodes>`
仅在列出的节点上分配。 Mongod不会在列出的节点上分配内存，并且可能无法使用所有可用内存。

* `-cpunodebind=<nodes>`
仅在节点上运行。 Mongod仅在指定的节点上运行，并且仅使用这些节点上可用的内存。

* `-physcpubind=<nodes>`
仅在列出的CPU（内核）上运行。 Mongod只在列出的CPU上运行，并且只使用这些CPU上可用的内存。

* `--localalloc`
始终在当前节点上分配内存，但使用线程运行的所有节点。 如果一个线程执行分配，则仅使用该CPU可用的内存。

* `--preferred=<node>`
优先分配至某个节点，但如果首选节点已满，则回退至其他节点。 可以使用用于定义节点的相对表示法。 此外，线程在所有节点上运行。

某些策略可能会使分配给的所有可用RAM不足 `mongod` 进程。 与MySQL不同，MongoDB主动避免操作系统级别分页，因此 `mongod` 进程可能获得更少的可用内存。

#### 交换 {#swapping}

由于数据库的内存密集型特性，必须禁用操作系统级别交换。 MongoDB进程避免通过设计进行交换。

#### 远程文件系统 {#remote-filesystems}

不建议将NFS等远程文件系统用于MongoDB的内部数据文件（mongod进程数据库文件），因为它们引入太多延迟。 不要混淆Oak Blob (FileDataStore)的存储所需的共享文件系统，建议使用NFS。

#### 预读 {#read-ahead}

提前调整读取，以便当使用随机读取分页页时，不会从磁盘读取不必要的块。 这种结果意味着不必要的I/O带宽消耗。

### Linux®要求 {#linux-requirements}

#### 最低内核版本 {#minimum-kernel-versions}

* **2.6.23** 对象 `ext4` 文件系统

* **2.6.25** 对象 `xfs` 文件系统

#### 数据库磁盘的建议设置 {#recommended-settings-for-database-disks}

**关闭时间**

建议 `atime` 对于包含数据库的磁盘，将关闭。

**设置NOOP磁盘计划程序**

执行以下操作：

首先，检查通过运行以下命令设置的I/O计划程序：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果响应为 `noop`，您无需执行任何其他操作。

如果NOOP不是所设置的I/O计划程序，可以通过运行以下命令来更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**调整预读值**

建议对运行MongoDB数据库的磁盘使用值32。 该值总计为16 KB。 您可以通过运行以下命令进行设置：

```shell
sudo blockdev --setra <value> <device>
```

#### 启用NTP {#enable-ntp}

确保在托管MongoDB数据库的计算机上安装并运行了NTP。 例如，您可以在CentOS计算机上使用yum包管理器安装它：

```shell
sudo yum install ntp
```

安装NTP守护程序并成功启动后，可以检查服务器的偏移时间文件。

#### 禁用透明超大页面 {#disable-transparent-huge-pages}

Red Hat® Linux®使用称为Transparent Great Pages (THP)的内存管理算法。 如果您使用操作系统处理数据库工作负载，建议您禁用它。

您可以按照以下步骤禁用它：

1. 打开 `/etc/grub.conf` 文件中的文本编辑器。
1. 将以下行添加到grub.conf文件中：

   ```xml
   transparent_hugepage=never
   ```

1. 最后，通过运行以下命令，检查设置是否已生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用THP，上述命令的输出应为：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>有关透明超大页面的更多信息，请参阅此 [文章](https://access.redhat.com/solutions/46111).

#### 禁用NUMA {#disable-numa}

在启用了NUMA的大多数安装中，如果MongoDB守护程序作为服务从运行，则会自动禁用它。 `/etc/init.d` 文件夹。

如果不是这种情况，您可以在每个进程级别禁用NUMA。 要禁用此功能，请运行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

位置 `<path_to_process>` 是通往蒙戈德进程的道路。

然后，通过运行以下命令禁用区域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 调整mongod进程的ulimit设置 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®允许通过 `ulimit` 命令。 此配置可以按用户或按进程完成。

建议您根据以下规则为mongod进程配置ulimit [MongoDB建议的ulimit设置](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### 测试MongoDB I/O性能 {#test-mongodb-i-o-performance}

MongoDB提供了一个名为 `mongoperf` 旨在测试I/O性能。 建议您使用它来测试组成基础架构的所有MongoDB实例的性能。

有关如何使用的信息 `mongoperf`，查看 [MongoDB文档](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>此 `mongoperf` 是在其运行的平台上MongoDB性能的指示器。 因此，不应将结果视为生产系统性能的最终结果。
>
>为了获得更准确的性能结果，您可以使用 `fio` Linux®工具。

**在构成部署的虚拟机上测试读取性能**

安装该工具后，切换到MongoDB数据库目录以运行测试。 然后，通过运行来开始第一次测试 `mongoperf`使用此配置：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

对于所有MongoDB实例，所需的输出应高达每秒2 GB (2 GB/s)和以32个线程运行的500.000 IOPS。

再次运行测试，这次使用内存映射文件，方法是设置 `mmf:true` 参数：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二次测试的输出应远高于第一次测试，这表示内存传输性能。

>[!NOTE]
>
执行测试时，请检查操作系统监控系统中相关虚拟机的I/O使用情况统计数据。 如果这些值指示的I/O读取值低于100%，则表示您的虚拟机可能存在问题。

**测试主MongoDB实例的写入性能**

接下来，通过运行检查主MongoDB实例的I/O写入性能 `mongoperf` 从MongoDB数据库目录中使用相同的设置：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的输出应为12 MB/秒，达到3000 IOPS左右，线程数之间几乎没有变化。

## 虚拟化环境的步骤 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果您使用WMWare ESX来管理和部署虚拟化环境，请确保从ESX控制台执行以下设置以适应MongoDB操作：

1. 关闭内存膨胀
1. 为托管MongoDB数据库的虚拟机预分配和保留内存
1. 使用存储I/O控制将足够的I/O分配给 `mongod` 进程。
1. 通过设置来保证托管MongoDB的计算机的CPU资源 [CPU保留](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. 考虑使用ParaVirtual I/O驱动程序。 请参阅 [知识库文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

有关如何使用Amazon Web Services设置MongoDB的文档，请查看 [配置AWS集成](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB网站上的文章。

## 在部署之前保护MongoDB {#securing-mongodb-before-deployment}

查看此帖子的日期 [安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 以获取有关如何在部署之前保护数据库配置安全的建议。

## Dispatcher {#dispatcher}

### 为Dispatcher选择操作系统 {#choosing-the-operating-system-for-the-dispatcher}

要为MongoDB部署正确提供服务，托管Dispatcher的操作系统必须正在运行 **Apache httpd** **版本2.4或更高版本。**

此外，请确保内部版本中使用的所有库都是最新的，以最大限度地减少安全影响。

### Dispatcher配置 {#dispatcher-configuration}

典型的Dispatcher配置的请求吞吐量是单个AEM实例的10到20倍。

由于Dispatcher是无状态的，因此它可以轻松水平缩放。 在某些部署中，必须限制作者访问某些资源。 建议您将Dispatcher与创作实例一起使用。

在不使用Dispatcher的情况下运行AEM需要由其他应用程序执行SSL终止和负载平衡。 之所以需要这样做，是因为会话必须与创建它们的AEM实例具有相关性，这个概念称为粘性连接。 原因是要确保对内容的更新显示最小的延迟。

查看 [Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en) 有关如何配置的详细信息。

### 其他配置 {#additional-configuration}

#### 粘性连接 {#sticky-connections}

粘性连接可确保同一个用户的个性化页面和会话数据全部在AEM的同一实例上撰写。 此数据存储在实例上，因此来自同一用户的后续请求将返回到同一实例。

建议为将请求路由到AEM实例的所有内部层启用粘性连接，鼓励后续请求访问同一个AEM实例。 这样做有助于最大限度地减少延迟，否则，当内容在实例之间更新时，延迟会非常明显。

#### 长过期 {#long-expires}

默认情况下，从AEM Dispatcher发送的内容具有Last-Modified和Etag标头，不指示内容过期。 此流程可确保用户界面始终获得最新版本的资源。 它还意味着浏览器执行GET操作以查看资源是否已更改。 因此，它可能会导致HTTP响应为304（未修改）的多个请求，具体取决于页面加载。 对于未过期的资源，设置Expires标头并删除Last-Modified和ETag标头会导致缓存内容。 并且，在满足Expires标头中的日期之前，不会提出进一步的更新请求。

但是，使用此方法意味着在Expires标头过期之前，没有合理的方法导致资源在浏览器中过期。 要缓解此工作流，可以将HtmlClientLibraryManager配置为对客户端库使用不可变URL。

这些URL保证不会更改。 当URL中包含的资源正文发生更改时，这些更改将反映在URL中，从而确保浏览器请求的资源版本正确。

默认配置向HtmlClientLibraryManager添加一个选择器。 作为选择器，资源缓存在Dispatcher中，且选择器保持不变。 此外，此选择器还可用于确保正确的过期行为。 默认选择器遵循 `lc-.*?-lc` 模式。 以下Apache httpd配置指令可确保符合该模式的所有请求都以合适的过期时间提供。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 无嗅探 {#no-sniff}

在没有内容类型的情况下发送内容时，许多浏览器尝试通过读取内容的前几个字节来猜测内容的类型。 此方法称为“探查”。 探查会打开一个安全漏洞，因为可以写入存储库的用户可能会上传没有内容类型的恶意内容。

因此，建议添加 `no-sniff` 标头到Dispatcher提供的资源。 但是，Dispatcher不缓存标头。 因此，它意味着从本地文件系统提供的任何内容的内容类型由其扩展决定，而不是使用来自其原始AEM服务器的原始内容类型标头。

如果已知的Web应用程序从不提供没有文件类型的缓存资源，则无法安全地启用嗅探。

您可以启用“无探查”：

```xml
Header set X-Content-Type-Options "nosniff"
```

它还可以有选择地启用：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 内容安全策略 {#content-security-policy}

默认Dispatcher设置允许打开内容安全策略（也称为CSP）。 这些设置允许页面根据浏览器沙盒的默认策略从所有域加载资源。

希望限制可从何处加载资源，以避免从不受信任或未验证的外部服务器将代码加载到JavaScript引擎中。

CSP允许微调策略。 但是，在复杂的应用程序中，开发CSP标头时必须小心，因为过于严格的策略可能会破坏部分用户界面。

>[!NOTE]
>
有关其工作原理的更多信息，请参见 [有关内容安全策略的OWASP页面](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### 大小调整 {#sizing}

有关大小调整的详细信息，请参见 [硬件大小调整准则](/help/managing/hardware-sizing-guidelines.md).

### MongoDB性能优化 {#mongodb-performance-optimization}

有关MongoDB性能的一般信息，请参见 [分析MongoDB性能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 已知限制 {#known-limitations}

### 并发安装 {#concurrent-installations}

虽然MongoMK支持在单个数据库中并发使用多个AEM实例，但不支持并发安装。

要解决此问题，请确保先使用单个成员运行安装，然后在第一个成员完成安装后添加其他成员。

### 页面名称长度 {#page-name-length}

如果AEM在MongoMK持久性管理器部署上运行， [页面名称长度限制为150个字符。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
请参阅 [MongoDB文档](https://docs.mongodb.com/manual/reference/limits/) 以便您熟悉MongoDB的已知限制和阈值。
