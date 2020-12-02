---
title: AEM与MongoDB
seo-title: AEM与MongoDB
description: 了解成功部署AEM的MongoDB所需的任务和注意事项。
seo-description: 了解成功部署AEM的MongoDB所需的任务和注意事项。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a
workflow-type: tm+mt
source-wordcount: '6513'
ht-degree: 0%

---


# AEM with MongoDB{#aem-with-mongodb}

本文旨在提高对成功部署MongoDB的Adobe Experience Manager所需任务和考虑事项的了解。

有关部署的详细信息，请参阅文档的[部署和维护](/help/sites-deploying/deploy.md)部分。

## 何时将MongoDB与AEM {#when-to-use-mongodb-with-aem}一起使用

MongoDB通常用于支持AEM作者部署，其中满足以下条件之一：

* 每天有1000多个独立用户；
* 100多个并发用户；
* 大量的页面编辑；
* 大型推广或激活。

以上条件仅适用于作者实例，不适用于所有应基于TarMK的发布实例。 由于作者实例不允许未经身份验证的访问，因此用户数引用经过身份验证的用户。

如果不满足标准，则建议进行TarMK活动／备用部署以解决可用性问题。 通常，在扩展要求大于单个硬件项所能实现的情况下，应考虑MongoDB。

>[!NOTE]
>
>有关作者实例大小调整和并发用户定义的其他信息，请参阅[硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)。

### AEM {#minimal-mongodb-deployment-for-aem}的最小MongoDB部署

下面是AEM在MongoDB上的最低部署。 为简单起见，SSL终止和HTTP代理组件已被推广。 它由一个MongoDB复制副本集组成，具有一个主副本和两个辅助副本。

![chlimage_1-4](assets/chlimage_1-4.png)

最小部署需要3个`mongod`实例配置为复制副本集。 一个实例将被选为主实例，而另一个实例是辅助实例，其选举由`mongod`管理。 附加到每个实例的是本地磁盘。 为了使群集支持负载，建议最低吞吐量为12MB/s，每秒操作数超过3000次(IOPS)。

AEM作者连接到`mongod`实例，每个AEM作者都连接到所有三个`mongod`实例。 写入被发送到主实例，读取可以从任何实例中读取。 流量根据调度程序对任何一个活动AEM作者实例的负载进行分配。 OAK数据存储是`FileDataStore`,MongoDB监控由MMS或MongoDB Ops Manager提供，具体取决于部署位置。 操作系统级别和日志监视由第三方解决方案（如Splunk或Ganglia）提供。

在此部署中，成功实施需要所有组件。 任何缺少的组件都将使实施无法正常工作。

### 操作系统{#operating-systems}

有关AEM 6支持的操作系统的列表，请参见[技术要求页面](/help/sites-deploying/technical-requirements.md)。

### 环境 {#environments}

支持虚拟化环境，前提是运行项目的不同技术团队之间有良好的通信。 这包括运行AEM的团队、拥有操作系统的团队以及管理虚拟化基础架构的团队。

对于需要由管理虚拟化环境的团队管理的MongoDB实例的I/O容量，有特定要求。 如果项目利用云部署(如AmazonWeb服务)，则需要为实例配置足够的I/O容量和一致性以支持MongoDB实例。 否则，MongoDB进程和Oak存储库将不可靠且不可靠地执行。

在虚拟化环境中，MongoDB将需要特定的I/O和VM配置，以确保MongoDB的存储引擎不会因VMWare资源分配策略而受损。 成功的实施将确保各个团队之间不存在障碍，所有团队都已经注册，以提供所需的性能。

## 硬件注意事项{#hardware-considerations}

### 存储 {#storage}

为了实现最佳性能的读写吞吐量而无需过早进行水平缩放，MongoDB通常要求SSD存储或性能与SSD相当的存储。

### RAM {#ram}

使用MMAP存储引擎的MongoDB版本2.6和3.0要求数据库的工作集及其索引适合RAM。

RAM不足将导致性能显着降低。 工作集和数据库的大小高度依赖于应用程序。 虽然可以做出一些估计，但确定所需RAM量的最可靠方法是构建AEM应用程序并对其进行负载测试。

为了帮助进行负载测试，可以采用以下工作集与数据库总大小的比率：

* 1:10,SSD存储
* 硬盘存储1:3

这意味着在SSD部署中，2TB数据库需要200GB内存。

虽然MongoDB 3.0中的WiredTiger存储引擎也存在同样的限制，但工作集、内存和页面故障之间的关联并不像WiredTiger使用内存映射的方式与MMAP存储引擎不同。

>[!NOTE]
>
>Adobe建议对使用MongoDB 3.0的AEM 6.1部署使用WiredTiger存储引擎。

### 数据存储{#data-store}

由于MongoDB工作集的限制，强烈建议将数据存储与MongoDB无关地进行维护。 在大多数环境中，应使用`FileDataStore`(使用所有AEM实例都可用的NAS)。 对于使用AmazonWeb服务的情况，还有`S3 DataStore`。 如果由于任何原因在MongoDB中维护数据存储，则应将数据存储的大小添加到数据库总大小中，并相应地调整工作集计算。 这可能意味着设置大量RAM以保持性能，而不出现页面错误。

## 监测 {#monitoring}

监测对于项目的成功实施至关重要。 虽然拥有足够的知识，在MongoDB上运行AEM是不进行监控，但通常在专门负责部署每个部分的工程师中都可以找到这种知识。

这通常涉及一名在Apache Oak Core工作的研发工程师和一名MongoDB专家。

在不进行所有级别监控的情况下，诊断问题需要详细了解代码库。 在对主要统计进行监测和适当指导的情况下，执行小组将能够对异常作出适当反应。

虽然可以使用命令行工具快速获取群集操作的快照，但在许多主机上实时执行此操作几乎是不可能的。 命令行工具很少提供几分钟以上的历史信息，并且不允许不同类型的度量之间的交叉关联。 短时间的慢速后台同步`mongod`需要大量手动操作，以根据I/O等待或过多写入级别与共享存储资源（从明显未连接的虚拟机）进行关联。

### MongoDB云管理器{#mongodb-cloud-manager}

MongoDB云管理器是MongoDB提供的免费服务，允许监视和管理MongoDB实例。 它为MongoDB集群的性能和运行提供了实时视图。 它管理云实例和私有托管实例，前提是该实例可以连接到Cloud Manager监视服务器。

它需要安装在连接到监控服务器的MongoDB实例上的代理。 代理有3个级别：

* 一个自动化代理，可以完全自动处理MongoDB服务器上的所有内容，
* 可监视`mongod`实例的监视代理，
* 可执行数据定时备份的备份代理。

虽然使用Cloud Manager实现MongoDB群集的维护自动化使许多常规任务变得更轻松，但它不是必需的，而且也不使用它进行备份。 但是，在选择要监视的云管理器时，需要进行监视。

有关MongoDB云管理器的详细信息，请查阅[MongoDB文档](https://docs.cloud.mongodb.com/)。

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager与MongoDB Cloud Manager是同一软件。 注册后，Ops Manager可以下载并安装在本地的专用数据中心或任何其他笔记本电脑或台式机上。 它使用本地MongoDB数据库存储数据，并以与Cloud Manager与受控服务器完全相同的方式进行通信。 如果您有禁止监视代理的安全策略，则应使用MongoDB Ops Manager。

### 操作系统监视{#operating-system-monitoring}

运行AEM MongoDB群集需要操作系统级别监视。

Ganglia是这样一个系统的一个很好的例子，它提供了所需信息的范围和细节，这些信息超出了CPU、平均负载和可用磁盘空间等基本健康指标。 要诊断问题，需要较低级别的信息，如熵池级别、CPU I/O等待、FIN_WAIT2状态中的套接字。

### 日志聚合{#log-aggregation}

对于多个服务器群集，中央日志聚合是生产系统的一个要求。 Splunk等软件支持日志聚合，并允许团队分析应用程序的行为模式而无需手动收集日志。

## 检查列表{#checklists}

本节介绍在实施项目之前应采取的各种步骤，以确保AEM和MongoDB部署设置正确。

### 网络{#network}

1. 首先，确保所有主机都有DNS条目
1. 所有主机都应通过其DNS条目从所有其他可路由主机解析
1. 所有MongoDB主机都可从同一群集中的所有其他MongoDB主机路由
1. MongoDB主机可以将数据包路由到MongoDB云管理器和其他监控服务器
1. AEM服务器可以将数据包路由到所有MongoDB服务器
1. 任何AEM服务器和任何MongoDB服务器之间的数据包延迟均小于两毫秒，没有数据包丢失，标准分发时间为1毫秒或更短。
1. 确保AEM和MongoDB服务器之间不超过两跳
1. 两台MongoDB服务器之间不超过两跳
1. 任何核心服务器(MongoDB、AEM或任何组合)之间没有高于OSI 3级的路由器。
1. 如果使用VLAN中继或任何形式的网络通道，则必须符合数据包延迟检查。

### AEM配置{#aem-configuration}

#### 节点存储配置{#node-store-configuration}

必须将AEM实例配置为将AEM与MongoMK一起使用。 AEM中MongoMK实现的基础是文档节点存储。

有关如何配置节点存储的详细信息，请参阅[在AEM](/help/sites-deploying/data-store-config.md)中配置节点存储和数据存储。

以下是文档节点存储配置的示例，用于最小的MongoDB部署：

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
这是MongoDB服务器AEM需要连接到的。将连接到默认复制副本集的所有已知成员。 如果使用MongoDB云管理器，则启用服务器安全。 因此，连接字符串必须包含合适的用户名和密码。 非企业版MongoDB仅支持用户名和密码验证。 有关连接字符串语法的详细信息，请查阅[文档](https://docs.mongodb.org/manual/reference/connection-string/)。

* `db`
数据库的名称。AEM的默认值是 
`aem-author`。

* `customBlobStore`
如果部署将二进制文件存储在数据库中，它们将构成工作集的一部分。因此，建议不要在MongoDB中存储二进制文件，请提供类似 
`FileSystem` 数据存储。

* `cache`
缓存大小(MB)。它分布于 
`DocumentNodeStore`.默认为256MB。 但是，Oak读取性能将得益于更大的缓存。

* `blobCacheSize`
经常使用的blob可由AEM缓存，以避免从数据存储中重新获取它们。这将对性能产生更大的影响，尤其是在MongoDB数据库中存储blob时。 所有基于文件系统的数据存储都将从操作系统级别的磁盘缓存中受益。

#### 数据存储配置{#data-store-configuration}

数据存储用于存储大于阈值的文件。 低于此阈值时，文件将作为属性存储在文档节点存储中。 如果使用`MongoBlobStore`，则在MongoDB中创建专用集合以存储blob。 此集合有助于`mongod`实例的工作集，并且需要`mongod`具有更多RAM以避免性能问题。 因此，建议的配置是避免生产部署的`MongoBlobStore`，并使用由所有AEM实例之间共享的NAS支持的`FileDataStore`。 由于操作系统级缓存在管理文件方面非常有效，因此磁盘上文件的最小大小应设置为接近磁盘的块大小，这样文件系统就可以高效地使用，并且许多小的文档不会过度地贡献于`mongod`实例的工作集。

下面是典型的数据存储配置，它使用MongoDB实现最小的AEM部署：

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
大小（字节）. 小于或等于此大小的二进制文件随文档节点存储存储存储。 二进制文件的内容不是存储blob的ID。 对于大于此大小的二进制文件，二进制文件的ID作为文档的属性存储在节点集合中，而二进制文件的正文存储在 
`FileDataStore` 在磁盘上。4096字节是典型的文件系统块大小。

* `path`
数据存储根的路径。对于MongoMK部署，此部署必须是所有AEM实例都可用的共享文件系统。 通常使用网络连接存储(NAS)服务器。 对于AmazonWeb服务等云部署， 
`S3DataFileStore` 的双曲余切值。

* `cacheSizeInMB`
二进制缓存的总大小(MB)。它用于缓存小于 
`maxCacheBinarySize` 。

* `maxCachedBinarySize`
在二进制缓存中缓存的二进制文件的最大大小（以字节为单位）。如果使用基于文件系统的数据存储，则不建议对数据存储缓存使用高值，因为二进制文件已经由操作系统缓存。

#### 禁用查询提示{#disabling-the-query-hint}

建议您通过添加属性来禁用与所有查询一起发送的查询提示

`-Doak.mongo.disableIndexHint=true`

启动AEM时。 这样，MongoDB将根据内部统计数据计算最合适的索引。

如果未禁用查询提示，则对索引进行任何性能调整都不会影响AEM的性能。

#### 为MongoMK {#enable-persistent-cache-for-mongomk}启用永久缓存

建议为MongoDB部署启用永久缓存配置，以最大化具有高I/O读取性能的环境的速度。 有关详细信息，请参阅[Jackrabbit Oak文档](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)。

## MongoDB操作系统优化{#mongodb-operating-system-optimizations}

### 操作系统支持{#operating-system-support}

MongoDB 2.6使用内存映射存储引擎，该引擎对RAM和磁盘之间操作系统级别管理的某些方面很敏感。 查询和读取MongoDB实例的性能依赖于避免或消除通常称为页面错误的慢速I/O操作。 这些是特别适用于`mongod`进程的页面错误。 它们不应与操作系统级别的页面错误混淆。

为实现快速操作，MongoDB数据库应仅访问已在RAM中的数据。 它需要访问的数据由索引和数据组成。 此索引和数据集合称为工作集。 当工作集大于可用RAM时，MongoDB必须从产生I/O成本的磁盘将该数据页入，从而驱逐内存中已有的其他数据。 如果迁出导致数据从磁盘页面重新加载，将主导性能下降。 如果工作集是动态的和可变的，则支持操作会产生更多页面故障。

MongoDB可运行于多种操作系统上，包括各种Linux版本、Windows和Mac OS。 有关更多详细信息，请参阅[https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms)。 根据您的操作系统选择，MongoDB有不同的操作系统级别建议。 有[https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration)的文档介绍，为方便起见，请在此进行总结。

#### Linux {#linux}

* 关闭透明的页面和碎片整理。 有关详细信息，请参阅[透明大页设置](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)。
* [调整存储数](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 据库文件的设备上的readaewaid设置以适合您的用例。

   * 对于MMAPv1存储引擎，如果工作集大于可用RAM，且文档访问模式是随机的，请考虑将预读数降低到32或16。 评估不同设置，以找到最佳值，最大化驻留内存并减少页面故障数。
   * 对于WiredTiger存储引擎，无论存储介质类型（旋转、SSD等）如何，请将readaew设置为0。 通常，除非测试显示更高的预读值具有可衡量、可重复和可靠的优势，否则请使用建议的预读设置。 [MongoDB专业支](https://docs.mongodb.com/manual/administration/production-notes/#readahead) 持可以就非零预读配置提供建议和指导。

* 如果您在虚拟环境中运行RHEL 7 / CentOS 7，请禁用调谐工具。
* 当RHEL 7/CentOS 7在虚拟环境中运行时，调整工具会自动调用从性能吞吐量派生的性能用户档案，该性能会自动将预读设置设置为4MB。 这会对性能产生负面影响。
* 使用SSD驱动器的noop或deadine磁盘调度程序。
* 对来宾VM中的虚拟化驱动器使用noop磁盘调度程序。
* 禁用NUMA或将vm.zone_recallim_mode设置为0并运行带节点交织的[mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead)实例。 请参阅：[MongoDB和NUMA硬件](https://docs.mongodb.com/manual/administration/production-notes/#readahead)以了解详细信息。

* 调整硬件上的上限值以适合您的用例。 如果同一用户下运行多个[mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod)或[mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos)实例，请相应地缩放上限值。 请参阅：[UNIX上限设置](https://docs.mongodb.com/manual/reference/ulimit/)以了解详细信息。

* 对[dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath)装载点使用noatime。
* 为部署配置足够的文件句柄(fs.file-max)、内核pid限制(kernel.pid_max)和每个进程的最大线程(kernel.threads-max)。 对于大型系统，以下值提供了一个良好的起点：

   * fs.file-max值98000,
   * kernel.pid_max值为64000,
   * andkernel.threads-max值64000

* 确保系统已配置交换空间。 有关相应大小调整的详细信息，请参阅操作系统的文档。
* 确保系统默认TCP keepalive设置正确。 值300通常为副本集和共享的群集提供更好的性能。 请参阅：[TCP keepalive时间是否会影响MongoDB部署？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) 的双曲正切值。

#### Windows {#windows}

* 考虑禁用NTFS“上次访问时间”更新。 这类似于在类似Unix的系统上禁用atime。

### WiredTiger {#wiredtiger}

自MongoDB 3.2起，MongoDB的默认存储引擎是WiredTiger存储引擎。 该引擎提供许多强大且可伸缩的功能，使其更适合全方位的一般数据库工作负载。 以下各节介绍了这些功能。

#### 文档级并发{#document-level-concurrency}

WiredTiger使用文档级并发控制进行写操作。 因此，多个客户端可以同时修改集合的不同文档。

对于大多数读写操作，WiredTiger使用乐观的并发控制。 WiredTiger仅在全局、数据库和集合级别使用意图锁。 当存储引擎检测到两个操作之间的冲突时，就会产生写冲突，导致MongoDB透明地重试该操作。一些全局操作，通常是涉及多个数据库的短时间操作，仍需要全局“实例范围”锁。

某些其他操作（如删除集合）仍需要独占数据库锁。

#### 快照和检查点{#snapshots-and-checkpoints}

WiredTiger使用多版本并发控制(MVCC)。 在操作开始,WiredTiger为事务提供数据的时间点快照。 快照显示内存中数据的一致视图。

写入磁盘时，WiredTiger将所有数据以一致的方式写入快照中的所有数据到磁盘，并跨所有数据文件。 现在[持久](https://docs.mongodb.com/manual/reference/glossary/#term-durable)的数据充当数据文件中的检查点。 检查点确保数据文件在最后一个检查点之前的一致性；即检查点可以充当恢复点。

MongoDB将WiredTiger配置为以60秒或2GB的日志数据间隔创建检查点（即将快照数据写入磁盘）。

在写入新检查点期间，以前的检查点仍然有效。 因此，即使MongoDB在写入新检查点时终止或遇到错误，在重新启动时，MongoDB也可以从最后一个有效检查点恢复。

当WiredTiger的元数据表自动更新以引用新检查点时，新检查点将变得可访问且永久。 新检查点可访问后，WiredTiger将页面从旧检查点中解除。

使用WiredTiger，即使没有[日志](https://docs.mongodb.com/manual/reference/glossary/#term-durable) , MongoDB也可以从最后一个检查点恢复；但是，要恢复在上一个检查点之后所做的更改，请使用[ journaling](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)运行。

#### 日志 {#journal}

WiredTiger结合[检查点](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)使用预写事务日志来确保数据的持久性。

WiredTiger日志在检查点之间保留所有数据修改。 如果MongoDB在检查点之间退出，则它使用日志重播自上次检查点以来修改的所有数据。 有关MongoDB将日志数据写入磁盘的频率的信息，请参见[日志记录过程](https://docs.mongodb.com/manual/core/journaling/#journal-process)。

WiredTiger日志是使用[snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process)压缩库进行压缩的。 要指定替代压缩算法或不指定压缩，请使用[存储.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor)设置。

有关详细信息，请参阅：[与WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)联系。

>[!NOTE]
>
>WiredTiger的最小日志记录大小为128字节。 如果日志记录为128字节或更小，则WiredTiger不压缩该记录。
>
>可以通过将[存储.日志.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled)设置为false来禁用日志，这可以减少维护日志的开销。
>
>对于[standalone](https://docs.mongodb.com/manual/reference/glossary/#term-standalone)实例，不使用日志意味着当MongoDB意外退出检查点时，您将丢失一些数据修改。 对于[复制集](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)的成员，复制过程可以提供足够的耐用性保证。

#### 压缩 {#compression}

借助WiredTiger,MongoDB支持对所有集合和索引进行压缩。 压缩可以最大限度地减少存储的使用，而不需要额外的CPU。

默认情况下，WiredTiger对所有集合使用[snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy)压缩库和所有索引使用[前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)的块压缩。

对于集合，还提供具有[zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib)的块压缩。 要指定替代压缩算法或不指定压缩，请使用[存储.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib)设置。

对于索引，要禁用[前缀压缩](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)，请使用[存储.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression)设置。

在创建集合和索引期间，还可以按每个集合和每个索引配置压缩设置。 请参阅[指定存储引擎选项](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options)和[db.collection.createIndex()storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options)选项。

对于大多数工作负载，默认的压缩设置平衡了存储效率和处理要求。

默认情况下，WiredTiger日志也会被压缩。 有关日志压缩的信息，请参阅[日志](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)。

#### 内存使用{#memory-use}

MongoDB使用WiredTiger内部缓存和文件系统缓存。

默认情况下，从3.4开始，WiredTiger内部缓存将使用以下任一大写：

* 50%的内存减去1 GB，或
* 256 MB

默认情况下，WiredTiger对所有集合使用Snappy块压缩，对所有索引使用前缀压缩。 压缩默认值可以在全局级别进行配置，还可以在创建集合和索引期间按每个集合和每个索引进行设置。

WiredTiger内部缓存中的数据与磁盘格式的数据使用不同的表示法：

* 文件系统缓存中的数据与磁盘上的格式相同，包括数据文件的任何压缩的优点。 操作系统使用文件系统缓存来减少磁盘I/O。

加载到WiredTiger内部缓存中的索引对磁盘格式具有不同的数据表示形式，但仍然可以利用索引前缀压缩来减少内存的使用。

索引前缀压缩会消除索引字段中的常用前缀。

WiredTiger内部缓存中的收集数据是未压缩的，并且使用不同于磁盘格式的表示形式。 块压缩可以大幅节省磁盘上的存储，但数据必须解压缩才能由服务器处理。

通过文件系统缓存，MongoDB自动使用WiredTiger缓存或其他进程未使用的所有空闲内存。

要调整WiredTiger内部缓存的大小，请参阅[存储.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB)和[—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb)。 避免将WiredTiger内部缓存大小增加到其默认值以上。

### NUMA {#numa}

非均匀内存访问(NUMA)允许内核管理如何将内存映射到处理器核心。 尽管NUMA试图加快内存访问速度，确保内核能够访问所需数据，但MMAP会干扰MMAP引入额外的延迟，因为读数无法预测。 因此，需要为具有此功能的所有操作系统上的`mongod`进程禁用NUMA。

本质上，在NUMA体系结构中，存储器连接到CPU,CPU连接到总线。 在SMP或UMA架构中，存储器连接到总线并由CPU共享。 当线程在NUMA CPU上分配内存时，它会根据策略分配内存。 默认情况是，除非没有空闲，否则将分配附加到线程的本地CPU的内存，此时它以较高的成本使用来自空闲CPU的内存。 分配后，内存不会在CPU之间移动。 分配由从父线程继承的策略执行，该策略最终是启动该进程的线程。

在许多将计算机视为多核统一内存体系结构的数据库中，这会导致初始CPU首先满足，而次CPU稍后填充，尤其是当中央线程负责分配内存缓冲区时。 解决方案是更改用于开始`mongod`进程的主线程的NUMA策略。

这可以通过运行以下命令来完成：

```shell
numactl --interleaved=all <mongod> -f config
```

此策略在所有CPU节点上以循环方式分配内存，确保在所有节点上均匀分配。 它不会像在具有多CPU硬件的系统中那样生成对内存的最高性能访问。 大约一半的内存操作会比较慢，而且在总线上，但`mongod`尚未以最佳方式写入目标NUMA，因此它是合理的折衷。

### NUMA问题{#numa-issues}

如果`mongod`进程是从`/etc/init.d`文件夹以外的位置启动的，则可能不会使用正确的NUMA策略启动。 根据默认策略的不同，可能会出现问题。 这是因为MongoDB的各种Linux包管理器安装程序还安装了一个包含配置文件的服务，该配置文件位于`/etc/init.d`中，执行上述步骤。 如果直接从存档(`.tar.gz`)安装并运行MongoDB，则需要在`numactl`进程下手动运行mongod。

>[!NOTE]
>
>有关NUMA策略的详细信息，请查阅[numactl文档](https://linux.die.net/man/8/numactl)。

在不同的分配策略下，MongoDB进程的行为将有所不同：

```

```

* `-membind=<nodes>`
仅在列出的节点上分配。Mongod不会在列出的节点上分配内存，并且可能不会使用所有可用内存。

* `-cpunodebind=<nodes>`
仅在节点上执行。Mongod将仅在指定的节点上运行，并且仅使用这些节点上可用的内存。

* `-physcpubind=<nodes>`
仅对列出的CPU（核心）执行。Mongod将仅在列出的CPU上运行，并仅使用这些CPU上可用的内存。

* `--localalloc`
始终在当前节点上分配内存，但使用线程运行时的所有节点。如果一个线程执行分配，则只使用该CPU可用的内存。

* `--preferred=<node>`
优先分配到节点，但如果首选节点已满，则优先分配到其他节点。可以使用用于定义节点的相对记号。 此外，线程在所有节点上运行。

某些策略可能导致分配给`mongod`进程的可用RAM少于所有可用RAM。 与MySQL不同，MongoDB主动避免操作系统级别分页，因此`mongod`进程可能获得的可用内存较少。

#### 交换{#swapping}

由于数据库的内存密集型特性，必须禁用操作系统级别交换。 MongoDB流程将避免通过设计进行交换。

#### 远程文件系统{#remote-filesystems}

不建议对MongoDB的内部数据文件（mongod进程数据库文件）使用远程文件系统（如NFS），因为它们会引入太多延迟。 这不要与建议使用NFS的Oak Blob(FileDataStore)存储所需的共享文件系统混淆。

#### 预读{#read-ahead}

需要调整提前读取，以便当使用随机读取页面时，不必要的块不会从磁盘中读取，从而导致不必要的I/O带宽消耗。

### Linux要求{#linux-requirements}

#### 最低内核版本{#minimum-kernel-versions}

* **2.6.23用于** 文件 `ext4` 系统

* **2.6.25用于** 文件 `xfs` 系统

#### 数据库磁盘{#recommended-settings-for-database-disks}的推荐设置

**关闭时间**

建议对将包含数据库的磁盘关闭`atime`。

**设置NOOP磁盘调度程序**

可通过以下方式执行此操作：

首先，检查当前设置的I/O调度程序。 这可以通过运行以下命令来完成：

```shell
cat /sys/block/sdg/queue/scheduler
```

如果响应为`noop`，则无需执行任何操作。

如果NOOP不是已设置的I/O调度程序，则可以通过运行以下各项来更改它：

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**调整预读值**

建议将值32用于MongoDB数据库所从的磁盘。 这相当于16千字节。 您可以通过运行以下项来设置它：

```shell
sudo blockdev --setra <value> <device>
```

#### 启用NTP {#enable-ntp}

确保在承载MongoDB数据库的计算机上安装并运行NTP。 例如，您可以在CentOS计算机上使用yum包管理器来安装它：

```shell
sudo yum install ntp
```

安装NTP守护程序并成功启动后，您可以检查漂移文件中服务器的时间偏移。

#### 禁用透明大页{#disable-transparent-huge-pages}

Red Hat Linux使用一种称为“透明大页”(THP)的内存管理算法。 如果您使用操作系统处理数据库工作负载，建议禁用它。

您可以按照以下过程禁用它：

1. 在您选择的文本编辑器中打开`/etc/grub.conf`文件。
1. 将以下代码行添加到grub.conf文件：

   ```xml
   transparent_hugepage=never
   ```

1. 最后，通过运行以检查设置是否生效：

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   如果禁用了THP，则上述命令的输出应为：

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>有关透明大页的详细信息，请参阅此[文章](https://access.redhat.com/solutions/46111)。

#### 禁用NUMA {#disable-numa}

在启用NUMA的大多数安装中，如果MongoDB守护程序作为服务从`/etc/init.d`文件夹运行，它将自动禁用。

如果不是这样，您可以在每个进程级别禁用NUMA。 要禁用它，请运行以下命令：

```shell
numactl --interleave=all <path_to_process>
```

其中`<path_to_process>`是mongod进程的路径。

然后，通过运行以下项来禁用区域回收：

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### 调整mongod进程{#tweak-the-ulimit-settings-for-the-mongod-process}的ulimit设置

Linux允许通过`ulimit`命令对资源分配进行可配置的控制。 这可以由用户完成，也可以按每个流程完成。

建议根据[MongoDB建议的ulimit设置](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)配置mongod进程的ulimit。

#### 测试MongoDB I/O性能{#test-mongodb-i-o-performance}

MongoDB提供一个名为`mongoperf`的工具，用于测试I/O性能。 建议您使用它测试构成基础结构的所有MongoDB实例的性能。

有关如何使用`mongoperf`的信息，请视图[MongoDB文档](https://docs.mongodb.org/manual/reference/program/mongoperf/)。

>[!NOTE]
>
>请注意，`mongoperf`设计为在其运行的平台上的MongoDB性能的指标。 因此，不应将结果视为生产系统性能的确定结果。
>
>要获得更准确的性能结果，您可以使用`fio` Linux工具运行补充测试。

**在构成部署的虚拟机上测试读取性能**

安装该工具后，切换到MongoDB数据库目录以运行测试。 然后，使用此配置运行`mongoperf`开始第一个测试：

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

所有MongoDB实例的所需输出应达到每秒2GB(2GB/s)和每秒500.000 IOPS（在32个线程中运行）。

通过设置`mmf:true`参数，再次运行测试（此次使用内存映射文件）:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

第二测试的输出应该比第一测试的输出要高得多，这表明存储器传输性能。

>[!NOTE]
>
>执行测试时，检查操作系统监视系统中相关虚拟机的I/O使用情况统计信息。 如果它们表示I/O读取的值低于100%，则您的虚拟机可能会出现问题。

**测试主MongoDB实例的写入性能**

接下来，使用相同设置从MongoDB数据库目录运行`mongoperf`来检查主MongoDB实例的I/O写性能：

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

期望的输出应为12 MB/秒，达到约3000 IOPS，线程数之间的变化很小。

## 虚拟化环境{#steps-for-virtualised-environments}的步骤

### VMWare {#vmware}

如果您使用WMWare ESX管理和部署虚拟化环境，请确保从ESX控制台中执行以下设置以适应MongoDB操作：

1. 关闭内存膨胀
1. 为承载MongoDB数据库的虚拟机预分配和保留内存
1. 使用存储I/O控件为`mongod`进程分配足够的I/O。
1. 通过设置[CPU保留](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)确保承载MongoDB的计算机的CPU资源

1. 考虑使用ParaVirtual I/O驱动程序。 有关如何执行此操作的详细信息，请查看此[知识库文章](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398)。

### AmazonWeb服务{#amazon-web-services}

有关如何使用AmazonWeb服务设置MongoDB的文档，请查看MongoDB网站上的[配置AWS集成](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/)文章。

## 部署{#securing-mongodb-before-deployment}前保护MongoDB

请参阅[安全部署MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html)上的此帖子，了解如何在部署前保护数据库的配置。

## Dispatcher {#dispatcher}

### 为调度程序{#choosing-the-operating-system-for-the-dispatcher}选择操作系统

为了正确服务您的MongoDB部署，将托管调度程序的操作系统必须运行&#x200B;**Apache httpd** **版本2.4或更高版本。**

此外，请确保构建中使用的所有库都是最新的，以最大限度地降低安全影响。

### 调度程序配置{#dispatcher-configuration}

典型的调度程序配置将提供单个AEM实例的请求吞吐量的十到二十倍。

由于调度程序主要是无状态的，因此它可以轻松地水平缩放。 在某些部署中，作者需要受到限制才能访问某些资源。 因此，强烈建议将调度程序与创作实例一起使用。

运行AEM而不运行调度程序将需要SSL终止，并需要其他应用程序执行负载平衡。 这是必需的，因为会话必须具有到其创建的AEM实例的关联，该概念称为粘性连接。 其目的是确保内容更新具有最小延迟。

请查阅[调度程序文档](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)以了解有关如何配置它的详细信息。

### 其他配置{#additional-configuration}

#### 粘性连接{#sticky-connections}

黏性连接可确保一个用户的个性化页面和会话数据都在AEM的同一实例上进行组合。 此数据存储在实例中，因此来自同一用户的后续请求将返回到同一实例。

建议为发往AEM实例的所有内层路由请求启用粘性连接，从而鼓励后续请求访问同一AEM实例。 这将有助于最大限度地减少在实例之间更新内容时会出现的延迟。

#### 长期过期{#long-expires}

默认情况下，从AEM调度程序发出的内容具有“上次修改时间”和“标记”标头，不表示内容到期。 这可确保用户界面始终获得资源的最新版本，同时也意味着浏览器将执行GET操作以检查资源是否已更改。 这可能导致HTTP响应为304（未修改）的多个请求，具体取决于页面加载。 对于已知不会过期的资源，设置“过期”标题并删除“上次修改时间”和“ETag”标题将导致内容被缓存，直到“过期”标题中的日期满足后，才会发出更新请求。

但是，使用此方法意味着在过期标题过期之前，没有合理的方法在浏览器中导致资源过期。 为了减轻这种影响，可以将HtmlClientLibraryManager配置为对客户端库使用不可变的URL。

这些URL保证不会更改。 当URL中包含的资源正文发生更改时，这些更改将自动反映在URL中，以确保浏览器将请求资源的正确版本。

默认配置会向HtmlClientLibraryManager添加一个选择器。 作为选择器，资源将缓存在调度程序中，并且选择器保持不变。 此选择器还可用于确保正确的过期行为。 默认选择器遵循`lc-.*?-lc`模式。 以下Apache httpd配置指令将确保所有与该模式匹配的请求都在适当的到期时间提供。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### 无嗅探{#no-sniff}

如果内容发出时没有内容类型，许多浏览器将尝试通过读取内容的前几个字节来猜测内容类型。 这叫“嗅探”。 嗅探会打开一个安全漏洞，因为可以写入存储库的用户可能上传没有内容类型的恶意内容。

因此，建议将`no-sniff`头添加到调度程序所服务的资源。 但是，调度程序不缓存标头。 这意味着，从本地文件系统提供的任何内容都将由其扩展确定其内容类型，而不是使用其AEM服务器的来源的原始内容类型头。

如果已知Web应用程序从不提供没有文件类型的缓存资源，则无法安全地启用嗅探。

可以包含启用“无嗅探”:

```xml
Header set X-Content-Type-Options "nosniff"
```

还可以有选择地启用它：

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### 内容安全策略{#content-security-policy}

默认调度程序设置允许打开的内容安全策略，也称为CSP。 这允许页面从受浏览器沙箱默认策略约束的所有域加载资源。

最好限制资源可从何处加载，以避免从不可信或未经验证的外来服务器将代码加载到javascript引擎中。

CSP允许对策略进行微调。 但是，在复杂的应用程序中，CSP头需要谨慎地开发，因为限制过度的策略可能会破坏用户界面的部分部分。

>[!NOTE]
>
>有关此操作方式的详细信息，请参见Content Security Policy（内容安全策略）[OWASP页](https://www.owasp.org/index.php/Content_Security_Policy)。

### 调整大小{#sizing}

有关调整大小的详细信息，请参阅[硬件调整指南](/help/managing/hardware-sizing-guidelines.md)。

### MongoDB性能优化{#mongodb-performance-optimization}

有关MongoDB性能的一般信息，请参见[分析MongoDB性能](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)。

## 已知限制{#known-limitations}

### 并发安装{#concurrent-installations}

MongoMK支持将多个AEM实例与单个数据库同时使用，但不支持并发安装。

要解决此问题，请确保先使用单个成员运行安装，并在第一个成员完成安装后添加其他成员。

### 页面名称长度{#page-name-length}

如果AEM在MongoMK持久性管理器部署上运行，则[页面名称限制为150个字符。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[请参阅MongoDB文](https://docs.mongodb.com/manual/reference/limits/) 档，熟悉MongoDB本身的已知限制和阈值。

