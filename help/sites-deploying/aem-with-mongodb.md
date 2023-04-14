---
title: Adobe Experience Manager和MongoDB
description: 了解成功使用MongoDB部署Adobe Experience Manager所需的任务和注意事项。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 0%

---

# Adobe Experience Manager和MongoDB{#aem-with-mongodb}

本文旨在提高对成功部署带有MongoDB的AEM(Adobe Experience Manager)所需任务和注意事项的了解。

有关更多与部署相关的信息，请参阅 [部署和维护](/help/sites-deploying/deploy.md) 文档的子目录访问Advertising Cloud帮助。

## 何时将MongoDB与AEM结合使用 {#when-to-use-mongodb-with-aem}

MongoDB通常用于支持满足以下条件之一的AEM创作部署：

* 每天独特用户超过1000人；
* 100多个并行用户；
* 页面编辑量大；
* 大型转出或激活。

上述标准仅适用于创作实例，而不适用于所有应均基于TarMK的发布实例。 用户数是指经过身份验证的用户，因为创作实例不允许未经身份验证的访问。

如果不满足标准，则建议使用TarMK活动/备用部署来解决可用性问题。 通常，在扩展要求比单个硬件项目所能实现的要高的情况下，应考虑MongoDB。

>[!NOTE]
>
>有关创作实例大小以及并发用户定义的其他信息，请参阅 [硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### 用于AEM的MongoDB部署最小 {#minimal-mongodb-deployment-for-aem}

以下是MongoDB上AEM的最小部署。 为简单起见，SSL终止和HTTP代理组件已得到推广。 它由单个MongoDB复制副本集组成，具有一个主副本和两个辅助副本。

![chlimage_1-4](assets/chlimage_1-4.png)

最低的部署需要三个 `mongod` 实例配置为复制副本集。 一个实例被选为主实例，而另一个实例是辅助实例，其选举由 `mongod`. 附加到每个实例的是本地磁盘。 因此，群集可以支持负载，建议每秒最小吞吐量为12 MB，每秒运行3000次I/O操作(IOPS)。

AEM作者已连接到 `mongod` 实例，使每个AEM作者都连接到所有三个 `mongod` 实例。 写操作将发送到主实例，读操作可从任何实例中读取。 流量是根据Dispatcher向任何活动AEM创作实例的加载进行分配的。 Oak数据存储是 `FileDataStore`、和MongoDB监控由MMS或MongoDB Ops Manager根据部署位置提供。 操作系统级别和日志监控由第三方解决方案（如Splunk或Ganglia）提供。

在此部署中，成功实施需要所有组件。 缺少的任何组件都会使实施无法正常运行。

### 操作系统 {#operating-systems}

有关AEM 6支持的操作系统列表，请参阅 [技术要求页面](/help/sites-deploying/technical-requirements.md).

### 环境 {#environments}

支持虚拟化环境，前提是运行项目的不同技术团队之间有良好的沟通。 此支持包括运行AEM的团队、拥有操作系统的团队以及管理虚拟化基础架构的团队。

对MongoDB实例的I/O容量有特定要求，这些要求必须由管理虚拟化环境的团队来管理。 如果项目使用云部署(如Amazon Web Services)，则必须为实例配置足够的I/O容量和一致性，以支持MongoDB实例。 否则， MongoDB进程和Oak存储库会不可靠、不可靠地执行。

在虚拟化环境中， MongoDB需要特定的I/O和VM配置，以确保MongoDB的存储引擎不会因VMWare资源分配策略而受损。 成功的实施可确保各个团队之间不存在任何障碍，所有团队都已注册以提供所需的性能。

## 硬件注意事项 {#hardware-considerations}

### 存储 {#storage}

为了实现最佳性能的读写吞吐量而无需过早进行水平扩展，MongoDB通常需要SSD存储或与SSD性能相当的存储。

### RAM {#ram}

使用MMAP存储引擎的MongoDB版本2.6和3.0要求数据库及其索引的工作集适合RAM。

RAM不足导致性能显着降低。 工作集和数据库的大小高度依赖于应用程序。 虽然可以做出一些估计，但确定所需RAM量的最可靠方法是构建AEM应用程序并对其进行负载测试。

为了帮助进行负载测试过程，可以假定工作集与总数据库大小的比率如下：

* 1:10用于SSD存储
* 硬盘存储1:3

这些比率意味着，对于SSD部署，2 TB数据库需要200 GB的RAM。

虽然MongoDB 3.0中的WiredTiger存储引擎也存在同样的限制，但工作集、RAM和页面故障之间的关联并不那么强。 WiredTiger使用内存映射的方式与MMAP存储引擎不同。

>[!NOTE]
>
>Adobe建议使用WiredTiger存储引擎进行AEM 6.1部署，这些部署使用的是MongoDB 3.0。

### 数据存储 {#data-store}

由于MongoDB工作集的限制，建议独立于MongoDB维护数据存储。 在大多数环境中， `FileDataStore` 应使用可用于所有AEM实例的NAS。 对于使用Amazon Web Services的情况，还有 `S3 DataStore`. 如果出于任何原因，数据存储在MongoDB内，数据存储的大小应添加到数据库总大小中，并且工作集计算会相应地进行调整。 此大小调整可能意味着设置更多RAM以保持性能，而不会出现页面故障。

## 监测 {#monitoring}

监测对于成功实施该项目至关重要。 如果了解足够的信息，则可以在MongoDB上运行AEM而不进行监控。 但是，这些知识通常在专门负责部署每个部分的工程师中找到。

这一专门知识通常涉及一名在Apache Oak Core工作的研发工程师和一名MongoDB专家。

如果不在所有级别进行监控，则需要详细了解代码库以诊断问题。 在对主要统计数据进行监测和适当指导的情况下，实施小组可以对异常情况作出适当反应。

虽然可以使用命令行工具快速获取群集操作的快照，但在许多主机上实时执行此操作几乎是不可能的。 命令行工具很少提供几分钟以上的历史信息，并且绝不允许不同类型的量度之间进行交叉关联。 一段缓慢的时期 `mongod` 同步需要手动进行大量工作，以便与I/O等待或从显然未连接的虚拟机到共享存储资源的过多写入级别相关联。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager是MongoDB提供的一项免费服务，允许监控和管理MongoDB实例。 它实时地对MongoDB集群的性能和运行状况进行了分析。 它可管理云实例和私有托管实例，前提是实例可以访问Cloud Manager监控服务器。

它需要在连接到监控服务器的MongoDB实例上安装一个代理。 代理有三个级别：

* 一个自动化代理，可以完全自动化MongoDB服务器上的所有功能，
* 可监视 `mongod` 实例，
* 执行数据定时备份的备份代理。

虽然使用Cloud Manager实现MongoDB群集的维护自动化使许多日常任务变得更轻松，但并非必需，而且也不用它进行备份。 但是，在选择Cloud Manager进行监视时，需要进行监视。

有关MongoDB Cloud Manager的更多信息，请参阅 [MongoDB文档](https://docs.cloud.mongodb.com/).

### MongoDB Ops管理器 {#mongodb-ops-manager}

MongoDB Ops Manager与MongoDB Cloud Manager是相同的软件。 注册后，可以在本地的专用数据中心或任何其他笔记本电脑或台式机上下载并安装Ops Manager。 它使用本地MongoDB数据库来存储数据，并以与Cloud Manager与托管服务器相同的方式进行通信。 如果您的安全策略禁止监视代理，则应使用MongoDB Ops Manager。

### 操作系统监控 {#operating-system-monitoring}

运行AEM MongoDB群集需要操作系统级别监控。

Ganglia是此类系统的一个好示例，它提供了所需信息的范围和详细信息，这些信息超出了CPU、负载平均值和可用磁盘空间等基本健康指标。 要诊断问题，需要低级别信息，如熵池级别、CPU I/O等待、FIN_WAIT2状态的插座。

### 日志聚合 {#log-aggregation}

对于由多台服务器组成的群集，中央日志聚合是生产系统的一项要求。 诸如Splunk之类的软件支持日志聚合，并允许团队分析应用程序的行为模式，而无需手动收集日志。

## 检查列表 {#checklists}

本节介绍在实施项目之前，您应采取的各种步骤，以确保正确设置AEM和MongoDB部署。

### 网络 {#network}

1. 首先，确保所有主机都具有DNS条目
1. 所有主机都应通过其DNS条目从所有其他可路由的主机中解析
1. 所有MongoDB主机都可从同一群集中的所有其他MongoDB主机路由
1. MongoDB主机可以将数据包路由到MongoDB Cloud Manager和其他监控服务器
1. AEM服务器可以将数据包路由到所有MongoDB服务器
1. 任何AEM服务器与任何MongoDB服务器之间的数据包延迟都小于两毫秒，没有数据包丢失，标准分布为1毫秒或更短。
1. 确保AEM和MongoDB服务器之间不会有两个以上的跳数
1. 两台MongoDB服务器之间不超过两跳
1. 任何核心服务器(MongoDB或AEM或任何组合)之间没有高于OSI Level 3的路由器。
1. 如果使用VLAN中继或任何形式的网络隧道，则必须符合数据包延迟检查。

### AEM配置 {#aem-configuration}

#### 节点存储配置 {#node-store-configuration}

必须将AEM实例配置为将AEM与MongoMK结合使用。 AEM中MongoMK实现的基础是文档节点存储。

有关如何配置节点存储的详细信息，请参阅 [在AEM中配置节点存储和数据存储](/help/sites-deploying/data-store-config.md).

以下是用于最小MongoDB部署的文档节点存储配置示例：

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

其中：

* `mongodburi`
MongoDB服务器AEM必须连接到。 将连接到默认副本集的所有已知成员。 如果使用MongoDB云管理器，则会启用服务器安全性。 因此，连接字符串必须包含适当的用户名和密码。 MongoDB的非企业版本仅支持用户名和密码验证。 有关连接字符串语法的更多信息，请参阅 [文档](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
数据库的名称。 AEM的默认设置为 
`aem-author`。

* `customBlobStore`
如果部署将二进制文件存储在数据库中，则它们构成工作集的一部分。 因此，建议不要在MongoDB中存储二进制文件，而应使用替代数据存储，如 
`FileSystem` 数据存储。

* `cache`
高速缓存大小(MB)。 此空间分布在 
`DocumentNodeStore`. 默认为256 MB。 但是，Oak读取性能从更大的缓存中受益。

* `blobCacheSize`
AEM可能会缓存常用的Blob，以避免从数据存储中重新获取它们。 这样做对性能的影响更大，尤其是在MongoDB数据库中存储Blob时。 所有基于文件系统的数据存储都从操作系统级别的磁盘缓存中受益。

#### 数据存储配置 {#data-store-configuration}

数据存储用于存储大于阈值的文件。 在该阈值以下，文件将作为属性存储在文档节点存储区中。 如果 `MongoBlobStore` ，则会在MongoDB中创建专用集合来存储Blob。 此集合适用于 `mongod` 实例，并要求 `mongod` 具有更多RAM以避免性能问题。 因此，建议的配置是避免 `MongoBlobStore` 用于生产部署和使用 `FileDataStore` 由所有AEM实例之间共享的NAS作为备份。 由于操作系统级别的缓存在管理文件方面非常有效，因此应将磁盘上文件的最小大小设置为接近磁盘块大小。 这样做可确保文件系统的使用效率，并且许多小文档不会对的工作集产生过多的贡献 `mongod` 实例。

以下是使用MongoDB实现最小AEM部署的典型数据存储配置：

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
大小（字节）. 小于或等于此大小的二进制文件将与文档节点存储一起存储。 二进制文件的内容不是存储Blob的ID，而是存储。 如果二进制文件大于此大小，则二进制文件的ID将作为Document的属性存储在节点集合中。 并且，二进制文件的主体存储在 
`FileDataStore` 在磁盘上。 4096字节是典型的文件系统块大小。

* `path`
数据存储的根路径。 对于MongoMK部署，此路径必须是所有AEM实例都可用的共享文件系统。 通常使用网络连接存储(NAS)服务器。 对于Amazon Web Services等云部署， 
`S3DataFileStore` 中，此变量将被删除。

* `cacheSizeInMB`
二进制缓存的总大小(MB)。 用于缓存小于的二进制文件 
`maxCacheBinarySize` 设置。

* `maxCachedBinarySize`
在二进制缓存中缓存的二进制文件的最大大小（以字节为单位）。 如果使用基于文件系统的数据存储，则不建议为数据存储缓存使用高值，因为操作系统已经缓存了二进制文件。

#### 禁用查询提示 {#disabling-the-query-hint}

建议您通过添加属性来禁用随所有查询一起发送的查询提示 `-Doak.mongo.disableIndexHint=true` 开始AEM时。 这样做可确保MongoDB根据内部统计数据计算最合适的索引。

如果未禁用查询提示，则对索引的任何性能调整都不会影响AEM的性能。

#### 为MongoMK启用永久缓存 {#enable-persistent-cache-for-mongomk}

建议为MongoDB部署启用永久缓存配置，以最大化I/O读取性能高的环境的速度。 有关更多详细信息，请参阅 [Jackrabbit Oak文档](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB操作系统优化 {#mongodb-operating-system-optimizations}

### 操作系统支持 {#operating-system-support}

MongoDB 2.6使用内存映射的存储引擎，该引擎对RAM和磁盘之间操作系统级别管理的某些方面非常敏感。 查询和读取MongoDB实例的性能依赖于避免或消除通常称为页面故障的慢速I/O操作。 这些问题是适用于 `mongod` 特别是流程。 请勿将与操作系统级别的页面错误混淆。

要执行快速操作，MongoDB数据库应仅访问RAM中已有的数据。 它必须访问的数据由索引和数据组成。 此索引和数据集合称为工作集。 如果工作集大于可用RAM MongoDB，则必须将该数据从磁盘中页入，从而产生I/O成本，从而驱逐内存中已有的其他数据。 如果驱逐导致从磁盘重新加载数据，则页面故障将占主导地位，性能会降低。 如果工作集是动态的和可变的，则支持操作会出现更多页面故障。

MongoDB在多个操作系统上运行，包括各种Linux®版本、Windows和macOS。 请参阅 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) 以了解更多详细信息。 MongoDB具有不同的操作系统级别建议，具体取决于您的操作系统选择。 有文档记录在 [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 为方便起见，在这里总结。

#### Linux® {#linux}

* 关闭透明的页面和碎片整理。 请参阅 [透明的大页设置](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) 以了解更多信息。
* [调整预读设置](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 在存储数据库文件的设备上，以便适合您的用例。

   * 对于MMAPv1存储引擎，如果工作集大于可用RAM，且文档访问模式是随机的，请考虑将提前读取降低到32或16。 评估不同的设置，以便找到最佳值，最大化驻留内存并减少页面故障数。
   * 对于WiredTiger存储引擎，无论存储介质类型（旋转、固态硬盘等）如何，都应将其提前设置为0。 通常，除非测试显示出更高的提前读取值具有可衡量、可重复和可靠的优势，否则请使用建议的提前读取设置。 [MongoDB专业支持](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 可以就非零预读配置提供建议和指导。

* 如果您在虚拟环境中运行RHEL 7 / CentOS 7，请禁用该调整工具。
* 当RHEL 7/CentOS 7在虚拟环境中运行时，调谐的工具会自动调用从性能吞吐量派生的性能配置文件，该性能配置文件会自动将提前读取设置设置为4 MB。 此设置可能会对性能产生负面影响。
* 使用SSD驱动器的noop或截止时间磁盘计划程序。
* 在来宾VM中对虚拟化驱动器使用noop磁盘调度程序。
* 禁用NUMA或设置 `vm.zone_reclaim_mode` 至0，运行 [蒙古](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 具有节点交织的实例。 请参阅： [MongoDB和NUMA硬件](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 以了解更多信息。

* 调整硬件上的上限值，使其适合您的用例。 如果为多个 [蒙古](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) 或 [蒙古](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) 实例在同一用户下运行，请相应地缩放ulimit值。 请参阅： [UNIX®上限设置](https://docs.mongodb.com/manual/reference/ulimit/) 以了解更多信息。

* 在 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) 装载点。
* 为您的部署配置足够的文件句柄(fs.file-max)、内核pid限制(kernel.pid_max)以及每个进程的最大线程数(kernel.threads-max)。 对于大型系统，以下值提供了一个良好的起点：

   * fs.file-max值为98000,
   * kernel.pid_max值为64000,
   * andkernel.threads-max值为64000

* 确保系统配置了交换空间。 有关相应大小调整的详细信息，请参阅操作系统文档。
* 确保系统默认的TCP keepalive设置正确。 值为300通常为副本集和共享的群集提供更好的性能。 请参阅： [TCP保持活动时间是否会影响MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 中的。

#### Windows {#windows}

* 请考虑禁用NTFS“上次访问时间”更新。 此设置类似于在类似Unix的系统上禁用atime。

### WiredTiger {#wiredtiger}

从MongoDB 3.2开始，MongoDB的默认存储引擎是WiredTiger存储引擎。 此引擎提供一些强大且可扩展的功能，使其更适合于所有一般数据库工作负载。 以下各节介绍了这些功能。

#### 文档级并发 {#document-level-concurrency}

WiredTiger使用文档级并发控制进行写入操作。 因此，多个客户端可以同时修改集合的不同文档。

对于大多数读写操作，WiredTiger使用乐观的并发控制。 WiredTiger仅在全局、数据库和收集级别使用意图锁定。 当存储引擎检测到两个操作之间的冲突时，一个操作会产生写入冲突，导致MongoDB透明地重试该操作。 一些全局操作（通常涉及多个数据库的操作时间很短）仍需要全局“实例范围”锁。

某些其他操作（如删除集合）仍需要独占数据库锁。

#### 快照和检查点 {#snapshots-and-checkpoints}

WiredTiger使用多版本并发控制(MVCC)。 在操作开始时，WiredTiger会向事务提供数据的时间点快照。 快照提供了内存中数据的一致视图。

写入磁盘时，WiredTiger以一致的方式将快照中的所有数据写入磁盘，并跨所有数据文件。 现在 —  [耐用](https://docs.mongodb.com/manual/reference/glossary/#term-durable) 数据充当数据文件中的检查点。 检查点可确保数据文件在最后一个检查点之前（包括最后一个检查点）保持一致。 也就是说，检查点可以充当恢复点。

MongoDB将WiredTiger配置为以60秒或2 GB的日志数据间隔创建检查点（即将快照数据写入磁盘）。

在写入新检查点期间，上一个检查点仍然有效。 因此，即使MongoDB在写入新检查点时终止或遇到错误，重新启动后，MongoDB也可以从最后一个有效检查点恢复。

当WiredTiger的元数据表自动更新以引用新检查点时，新检查点将变为可访问和永久的。 一旦可以访问新检查点，WiredTiger将从旧检查点中释放页面。

使用WiredTiger，即使没有 [日记](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB可以从最后一个检查点恢复；但是，要恢复在上一个检查点之后所做的更改，请运行 [日记](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 日志 {#journal}

WiredTiger使用预写事务登录组合， [检查点](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) 以确保数据的持久性。

WiredTiger日志保留检查点之间的所有数据修改。 如果MongoDB在检查点之间退出，则它使用日志重播自上次检查点以来修改的所有数据。 有关MongoDB将日志数据写入磁盘的频率的信息，请参见 [日记帐过程](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger日志使用 [快照](https://docs.mongodb.com/manual/core/journaling/#journal-process) 压缩库。 要指定替代压缩算法或不进行压缩，请使用 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 设置。

请参阅 [《连线虎杂志》](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger的最小日志记录大小为128字节。 如果日志记录为128字节或更小，则WiredTiger不压缩该记录。
>
>您可以通过设置 [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) 为false，这可以降低维护日志的开销。
>
>对于 [独立](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) 实例，不使用日志意味着当MongoDB意外退出检查点之间时，您会丢失一些数据修改。 对于 [复制集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)，则复制过程可提供足够的耐用性保证。

#### 压缩 {#compression}

使用WiredTiger，MongoDB支持对所有集合和索引进行压缩。 压缩可以最大限度地减少存储使用，而不会增加CPU。

默认情况下，WiredTiger使用块压缩 [快照](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 用于所有收藏集的压缩库 [前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) （适用于所有索引）。

对于收藏集，块压缩 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 中，此变量将被删除。 要指定替代压缩算法或不进行压缩，请使用 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 设置。

对于索引，禁用 [前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，则使用 [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 设置。

在收集和索引创建期间，还可以按收藏集和按索引配置压缩设置。 请参阅 [指定存储引擎选项](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) 和 [db.collection.createIndex()storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) 选项。

对于大多数工作负载，默认的压缩设置平衡了存储效率和处理要求。

默认情况下，WiredTiger日志也会压缩。 有关日记帐压缩的信息，请参阅 [日志](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### 内存使用 {#memory-use}

使用WiredTiger时， MongoDB同时使用WiredTiger内部缓存和文件系统缓存。

从3.4开始，WiredTiger内部缓存默认使用以下任一值中的较大值：

* 50%的RAM减去1 GB，或
* 256 MB

默认情况下，WiredTiger对所有集合使用Snappy块压缩，对所有索引使用前缀压缩。 压缩默认值可在全局级别进行配置，也可以在收集和索引创建期间基于每个收藏集和每个索引进行设置。

与磁盘格式相比，WiredTiger内部缓存中的数据使用不同的表示形式：

* 文件系统缓存中的数据与磁盘上的格式相同，包括任何数据文件压缩的好处。 操作系统使用文件系统缓存来减少磁盘I/O。

在WiredTiger内部缓存中加载的索引与磁盘格式的数据表示方式不同，但仍然可以利用索引前缀压缩来减少RAM的使用。

索引前缀压缩会删除来自索引字段的重复公共前缀。

WiredTiger内部缓存中的收集数据未压缩，且使用与磁盘格式不同的表示形式。 块压缩可以显着节省磁盘上的存储，但数据必须未压缩才能由服务器处理。

通过文件系统缓存， MongoDB自动使用WiredTiger缓存或其他进程未使用的所有空闲内存。

要调整WiredTiger内部缓存的大小，请参阅 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) 和 [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). 避免将WiredTiger内部缓存大小增加到其默认值以上。

### 努马 {#numa}

NUMA（非统一内存访问）允许内核管理内存映射到处理器内核的方式。 尽管此过程尝试加快内核的内存访问速度，确保内核能够访问所需数据，但NUMA会干扰MMAP引入额外的延迟，因为读取无法预测。 因此，必须为 `mongod` 处理所有可用的操作系统。

本质上，NUMA体系结构内存与CPU连接，CPU与总线连接。 在SMP或UMA架构中，存储器连接到总线并由CPU共享。 当线程在NUMA CPU上分配内存时，它会根据策略进行分配。 缺省设置是分配连接到线程的本地CPU的内存，除非没有空闲内存，此时它以较高的成本使用来自空闲CPU的内存。 分配后，内存不会在CPU之间移动。 分配由从父线程继承的策略执行，该策略最终是启动该进程的线程。

在许多将计算机视为多核统一内存体系结构的数据库中，这种情况会导致初始CPU先满，然后次CPU再满。 如果中央线程负责分配内存缓冲区，则尤其如此。 解决方案是更改用于启动 `mongod` 进程：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略可以在所有CPU节点上以循环方式分配内存，以确保在所有节点上均匀分配。 它不会像在具有多个CPU硬件的系统中那样生成对内存的最高性能访问。 大约一半的内存操作速度比总线慢，但 `mongod` 尚未以最佳方式写入目标NUMA，因此这是一个合理的妥协。

### NUMA问题 {#numa-issues}

如果 `mongod` 进程从以下位置启动： `/etc/init.d` 文件夹，则可能尚未开始使用正确的NUMA策略。 根据默认策略，可能会出现问题。 原因是MongoDB的各种Linux® Package Manager安装程序还安装了一项包含 `/etc/init.d` 执行上述步骤。 如果直接从存档( `.tar.gz`)，则必须在 `numactl` 进程。

>[!NOTE]
>
>欲知关于联马军政策的详情，请查阅 [numactl文档](https://linux.die.net/man/8/numactl).

MongoDB进程在不同分配策略下的行为方式不同：

```

```

* `-membind=<nodes>`
仅在列出的节点上分配。 Mongod不会在列出的节点上分配内存，并且可能不会使用所有可用内存。

* `-cpunodebind=<nodes>`
仅在节点上运行。 Mongod仅在指定的节点上运行，并且仅使用这些节点上可用的内存。

* `-physcpubind=<nodes>`
仅在列出的CPU（核心）上运行。 Mongod仅在列出的CPU上运行，并且仅使用这些CPU上可用的内存。

* `--localalloc`
始终在当前节点上分配内存，但使用线程运行的所有节点。 如果一个线程执行分配，则仅使用该CPU可用的内存。

* `--preferred=<node>`
首选向节点分配，但如果首选节点已满，则回退到其他节点。 可以使用用于定义节点的相对符号。 此外，线程在所有节点上运行。

某些策略可能会导致提供给的可用RAM少于所有 `mongod` 进程。 与MySQL不同， MongoDB主动避免操作系统级别分页，因此 `mongod` 进程可能获得的可用内存较少。

#### 交换 {#swapping}

由于数据库的内存密集性，必须禁用操作系统级别的交换。 MongoDB进程避免了通过设计进行交换。

#### 远程文件系统 {#remote-filesystems}

MongoDB的内部数据文件（mongod进程数据库文件）不建议使用NFS等远程文件系统，因为它们会引起太多延迟。 请勿将与存储Oak Blob(FileDataStore)所需的共享文件系统相混淆，其中建议使用NFS。

#### 提前阅读 {#read-ahead}

将“Tune Read aew”（预先调整读取），以便当使用随机读取的方式在页面中调入时，不会从磁盘读取不必要的块。 这种结果意味着I/O带宽的不必要消耗。

### Linux®要求 {#linux-requirements}

#### 最低内核版本 {#minimum-kernel-versions}

* **2.6.23** 表示 `ext4` 文件系统

* **2.6.25** 表示 `xfs` 文件系统

#### 数据库磁盘的建议设置 {#recommended-settings-for-database-disks}

**关闭时间**

建议 `atime` 对于包含数据库的磁盘，将关闭。

**设置NOOP磁盘调度程序**

执行以下操作：

首先，检查通过运行以下命令设置的I/O调度程序：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果响应为 `noop`，则无需执行其他操作。

如果NOOP不是已设置的I/O调度程序，则可以通过运行以下命令来更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**调整读前值**

建议对运行MongoDB数据库的磁盘使用值32。 此值大于16 KB。 您可以通过运行以下命令来设置它：

```shell
sudo blockdev --setra <value> <device>
```

#### 启用NTP {#enable-ntp}

确保在托管MongoDB数据库的计算机上安装并运行NTP。 例如，您可以在CentOS计算机上使用yum包管理器来安装它：

```shell
sudo yum install ntp
```

安装NTP守护程序并成功启动后，您可以检查漂移文件中服务器的时间偏移。

#### 禁用透明大页 {#disable-transparent-huge-pages}

Red Hat® Linux®使用称为“透明大页”(THP)的内存管理算法。 如果您使用操作系统处理数据库工作负载，建议您禁用它。

您可以按照以下过程禁用该功能：

1. 打开 `/etc/grub.conf` 文件。
1. 将以下行添加到grub.conf文件：

   ```xml
   transparent_hugepage=never
   ```

1. 最后，通过运行以检查该设置是否生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，则上述命令的输出应为：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>有关透明大页的详细信息，请参阅此 [文章](https://access.redhat.com/solutions/46111).

#### 禁用NUMA {#disable-numa}

在启用NUMA的大多数安装中，如果MongoDB守护程序作为服务从 `/etc/init.d` 文件夹。

如果情况并非如此，您可以在每个进程级别上禁用NUMA。 要禁用此功能，请运行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

其中 `<path_to_process>` 是通往蒙古进程的道路。

然后，通过运行以下命令来禁用区域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 为单一流程调整上限设置 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®允许通过 `ulimit` 命令。 此配置可以基于用户或每个流程完成。

建议您根据 [MongoDB建议的上限设置](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### 测试MongoDB I/O性能 {#test-mongodb-i-o-performance}

MongoDB提供了一个名为 `mongoperf` 用于测试I/O性能。 建议您使用它来测试构成基础架构的所有MongoDB实例的性能。

有关如何使用的信息 `mongoperf`，查看 [MongoDB文档](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>的 `mongoperf` 是运行该数据库的平台上MongoDB性能的指标。 因此，不应将结果视为生产系统性能的确定结果。
>
>为了获得更准确的性能结果，您可以使用 `fio` Linux®工具。

**在构成部署的虚拟机上测试读取性能**

安装该工具后，请切换到MongoDB数据库目录以运行测试。 然后，通过运行 `mongoperf`使用此配置：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

对于所有MongoDB实例，所需输出应高达每秒2GB(2 GB/s)和以32个线程运行的500.000 IOPS。

通过设置 `mmf:true` 参数：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二测试的输出应该比第一测试的输出要高很多，这表示存储器传输性能。

>[!NOTE]
执行测试时，请检查操作系统监控系统中相关虚拟机的I/O使用情况统计信息。 如果它们指示I/O读取的值低于100%，则虚拟机可能会出现问题。

**测试主MongoDB实例的写入性能**

接下来，通过运行 `mongoperf` 从具有相同设置的MongoDB数据库目录中：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

所需的输出应为12 MB/秒，达到约3000 IOPS，线程数之间的变化很小。

## 虚拟化环境的步骤 {#steps-for-virtualised-environments}

### VMWare {#vmware}

如果您使用WMWare ESX来管理和部署虚拟化环境，请确保从ESX控制台中执行以下设置以适应MongoDB操作：

1. 关闭内存气球
1. 为托管MongoDB数据库的虚拟机预分配和保留内存
1. 使用存储I/O控制为 `mongod` 进程。
1. 通过设置 [CPU保留](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. 考虑使用ParaVirtual I/O驱动程序。 请参阅 [知识库文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

有关如何使用Amazon Web Services设置MongoDB的文档，请查看 [配置AWS集成](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) MongoDB网站上的文章。

## 部署前保护MongoDB {#securing-mongodb-before-deployment}

查看此帖子的位置 [安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) 有关如何在部署前保护数据库配置的建议。

## Dispatcher {#dispatcher}

### 为调度程序选择操作系统 {#choosing-the-operating-system-for-the-dispatcher}

要正确提供MongoDB部署，承载Dispatcher的操作系统必须运行 **Apache httpd** **版本2.4或更高版本。**

此外，请确保内部版本中使用的所有库都是最新的，以最大限度地减少对安全性的影响。

### 调度程序配置 {#dispatcher-configuration}

典型的Dispatcher配置提供的请求吞吐量是单个AEM实例的十到20倍。

由于Dispatcher是无状态的，因此它可以轻松地水平缩放。 在某些部署中，必须限制作者访问某些资源。 建议您将Dispatcher与创作实例结合使用。

在没有Dispatcher的情况下运行AEM需要SSL终止和负载平衡，才能由其他应用程序执行。 此过程是必需的，因为会话必须与创建这些会话的AEM实例具有亲和度，这一概念称为粘性连接。 其原因是要确保内容更新显示的延迟最少。

检查 [Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans) 以了解有关如何配置它的详细信息。

### 其他配置 {#additional-configuration}

#### 粘性连接 {#sticky-connections}

粘性连接可确保一个用户的个性化页面和会话数据全部在同一个AEM实例上撰写。 此数据存储在实例中，因此来自同一用户的后续请求将返回到同一实例。

建议为所有内部层启用粘性连接，以将请求路由到AEM实例，从而鼓励后续请求到达同一AEM实例。 这样做有助于最大限度地减少在实例之间更新内容时出现的滞后。

#### 长期过期 {#long-expires}

默认情况下，从AEM Dispatcher发出的内容具有“上次修改时间”和“Etag”标头，不表示内容已到期。 此流程可确保用户界面始终获取资源的最新版本。 它还意味着浏览器执行GET操作以查看资源是否已更改。 因此，根据页面加载情况，可能会导致HTTP响应为304（未修改）的多个请求。 对于未过期的资源，设置Expires标头并删除Last-Modified和ETag标头会导致内容被缓存。 而且，在满足Expires标头中的日期之前，不会再发出更新请求。

但是，使用此方法意味着在Expires标头过期之前，没有合理的方法可导致资源在浏览器中过期。 要缓解此工作流，可以将HtmlClientLibraryManager配置为对客户端库使用不可变URL。

这些URL保证不会更改。 当URL中包含的资源正文发生更改时，这些更改将反映在URL中，以确保浏览器请求正确的资源版本。

默认配置会向HtmlClientLibraryManager中添加一个选择器。 作为选择器，资源将缓存在Dispatcher中，并且选择器将保持不变。 此外，还可以使用此选择器来确保正确的过期行为。 默认选择器遵循 `lc-.*?-lc` 模式。 以下Apache httpd配置指令可确保在适当的过期时间内提供与该模式匹配的所有请求。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 无嗅 {#no-sniff}

当内容在不包含内容类型的情况下发出时，许多浏览器会尝试通过读取内容的前几个字节来猜测内容类型。 此方法称为“嗅探”。 嗅探操作会打开一个安全漏洞，因为能够写入存储库的用户可能上载没有内容类型的恶意内容。

因此，建议添加 `no-sniff` 指向Dispatcher提供的资源的标头。 但是，Dispatcher不缓存标头。 因此，这意味着从本地文件系统提供的任何内容都由其扩展决定其内容类型，而不是使用其AEM源服务器中的原始内容类型标头。

如果已知Web应用程序从不提供没有文件类型的缓存资源，则无法安全地启用嗅探。

您可以包含以下内容：

```xml
Header set X-Content-Type-Options "nosniff"
```

还可以选择性地启用该功能：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 内容安全策略 {#content-security-policy}

默认的Dispatcher设置允许打开的内容安全策略，也称为CSP。 这些设置允许页面从受浏览器沙盒默认策略限制的所有域加载资源。

最好限制资源可从何处加载，以避免从不受信任的或未经验证的外来服务器将代码加载到JavaScript引擎中。

CSP允许对策略进行微调。 但是，在复杂的应用程序中，必须谨慎开发CSP标头，因为过于受限的策略可能会破坏用户界面的部分部分。

>[!NOTE]
有关此功能的工作方式的更多信息，请参阅 [内容安全策略上的OWASP页面](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### 大小 {#sizing}

有关大小调整的更多信息，请参阅 [硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md).

### MongoDB性能优化 {#mongodb-performance-optimization}

有关MongoDB性能的一般信息，请参阅 [分析MongoDB性能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 已知限制 {#known-limitations}

### 并行安装 {#concurrent-installations}

MongoMK支持将多个AEM实例与单个数据库并发使用，但不支持并发安装。

要解决此问题，请确保先使用单个成员运行安装，然后在完成安装后添加其他成员。

### 页面名称长度 {#page-name-length}

如果AEM在MongoMK持久性管理器部署中运行， [页面名称限制为150个字符。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
请参阅 [MongoDB文档](https://docs.mongodb.com/manual/reference/limits/) 以便您熟悉MongoDB的已知限制和阈值。
