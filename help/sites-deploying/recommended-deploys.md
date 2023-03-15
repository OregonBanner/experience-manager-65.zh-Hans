---
title: 建议的部署
seo-title: Recommended Deployments
description: 本文介绍了推荐的AEM拓扑。
seo-description: This article describes the recommended topologies for AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---

# 建议的部署{#recommended-deployments}

>[!NOTE]
>
>本页介绍AEM推荐的拓扑。 有关群集功能以及如何配置这些功能的详细信息，请参阅 [Apache Sling Discovery API文档](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html).

从AEM 6.2开始，MicroKernels充当持久性管理器。根据您的需要选择一种部署类型，具体取决于实例的用途和您考虑的部署类型。

以下示例旨在指示在最常见的AEM设置中建议使用哪些功能。

## 部署方案 {#deployment-scenarios}

### 单个TarMK实例 {#single-tarmk-instance}

在此方案中，单个TarMK实例在单个服务器上运行。

**这是创作实例的默认部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

其优点是：

* 简单
* 易于维护
* 性能良好

缺点：

* 可扩展性超出服务器容量限制
* 无故障切换容量

### TarMK冷备用 {#tarmk-cold-standby}

一个TarMK实例作为主实例。 将主存储库复制到备用故障转移系统。

冷备用机制也可以用作备份，因为整个存储库会不断复制到故障转移服务器。 故障转移服务器正在冷备用模式下运行，这意味着只有实例的HttpReceiver在运行。

![chlimage_1-16](assets/chlimage_1-16.png)

其优点是：

* 简洁
* 可维护性
* 演出
* 故障转移

缺点：

* 不能扩展至超出服务器容量的限制
* 一台服务器大部分时间处于空闲状态
* 故障转移不是自动的。 必须先在外部检测它，然后故障转移系统才能开始为请求提供服务。

>[!NOTE]
>
>有关如何使用TarMK冷备用配置AEM的更多信息，请参阅 [此](/help/sites-deploying/tarmk-cold-standby.md) 文章。

>[!NOTE]
>
>此TarMK示例中的“冷备用”部署要求主实例和备用实例都单独授予许可，因为可以不断复制到故障转移服务器。 欲知关于许可的详情，请查阅 [Adobe一般许可条款](https://www.adobe.com/cn/legal/terms/enterprise-licensing.html).

### TarMK场 {#tarmk-farm}

多个Oak实例分别运行一个TarMK实例。 TarMK存储库是独立的，需要保持同步。

使存储库保持同步的原因是创作服务器向每个场成员发布相同的内容。 有关更多信息，请参阅 [复制](/help/sites-deploying/replication.md).

对于AEM Communities，从不复制用户生成的内容(UGC)。 有关在TarMK场上支持UGC的信息，请参阅 [AEM Communities的注意事项](#considerations-for-aem-communities).

**这是发布环境的默认部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

其优点是：

* 演出
* 读取访问的可扩展性
* 故障转移

### 带有MongoMK故障转移的Oak群集，可在单个数据中心实现高可用性 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

此方法意味着多个Oak实例在单个数据中心内访问MongoDB副本集，实际上为AEM创作环境创建了一个主动 — 主动群集。 MongoDB中的副本集用于在发生硬件或网络故障时提供高可用性和冗余。

![chlimage_1-18](assets/chlimage_1-18.png)

其优点是：

* 能够使用新的AEM创作实例水平缩放
* 数据层的高可用性、冗余和自动故障切换

缺点：

* 在某些情况下，性能可能会低于TarMK

### 在多个数据中心之间使用MongoMK故障转移的Oak群集 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法意味着多个Oak实例跨多个数据中心访问MongoDB副本集，实际上为AEM创作环境创建了一个主动 — 主动群集。 在多个数据中心中， MongoDB复制提供了相同的高可用性和冗余，但现在包括处理数据中心中断的能力。

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

其优点是：

* 能够使用新的AEM创作实例水平缩放
* 数据层的高可用性、冗余和自动故障切换（包括数据中心中断）

>[!NOTE]
>
>在上图中，假设数据中心2中的AEM服务器与数据中心1中的MongoDB主节点之间的网络延迟高于记录的要求，则AEM Server 3和AEM Server 4将显示为非活动状态 [此处](/help/sites-deploying/aem-with-mongodb.md#checklists). 如果最大延迟与要求兼容（例如通过使用可用区），则数据中心2中的AEM服务器也可以处于活动状态，从而创建跨多个数据中心的主动 — 主动AEM群集。

>[!NOTE]
>
>有关本节所述的MongoDB架构概念的其他信息，请参见 [MongoDB复制](https://docs.mongodb.org/manual/replication/).

## 微内核：使用哪一个 {#microkernels-which-one-to-use}

在两个可用的微内核之间进行选择时需要考虑的基本规则是，TarMK是针对性能而设计的，而MongoMK是针对可扩展性而设计的。

您可以使用这些决策矩阵，确定哪种部署类型最适合您的要求。

Adobe强烈建议将TarMK作为客户在所有部署方案中（对于AEM创作实例和发布实例）使用的默认持久性技术，但以下列出的用例除外。

### 创作实例上选择AEM MongoMK而非TarMK的异常 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

与TarMK相比，选择MongoMK持久性后端的主要原因是要水平缩放实例。 这意味着始终运行两个或多个活动创作实例，并使用MongoDB作为持久性存储系统。 运行多个创作实例的需要通常是由于单个服务器的CPU和内存容量（支持所有并发创作活动）不再可持续。

几乎无法预测新站点上线后确切的并发模型是什么。 因此，Adobe建议您在评估是否使用MongoMK和两个或更多创作活动节点时考虑以下标准：

1. 一天中连接的指定用户数：以千或更多的数量为单位。
1. 并发用户数：以百计或更多。
1. 每天的资产摄取量：数十万或更多。
1. 每天页面编辑量：数十万或更多（例如通过多站点管理器或新闻馈送摄取进行自动更新）。
1. 每天的搜索量：以万或更多。

>[!NOTE]
>
>Tough Day可用于在部署的硬件配置环境中评估客户应用程序的性能。 有关此工具的详细信息 [此处](/help/sites-developing/tough-day.md).

MongoDB的最低部署通常涉及以下拓扑：

* MongoDB副本集由一个主节点和两个辅助节点组成，每个MongoDB实例都在可用性区域中运行，每个节点的延迟时间不到15毫秒；
* 一个创作实例集群，具有一个领导节点、一个非领导节点且两者始终处于活动状态，每个创作实例都在每个数据中心中运行，其中运行MongoDB主实例和辅助实例。

此外，强烈建议在共享文件系统或Amazon S3上配置数据存储，以便资源或二进制文件不存储在MongoDB中。 这将确保部署中的最佳性能。

使用由两个或多个创作实例组成的群集部署MongoDB副本集的另一个好处是，在创作实例、MongoDB副本或完全数据中心故障的情况下，具有自动恢复方案，停机时间最短。 尽管如此，MongoMK与TarMK的选择不应仅受恢复需求的驱动，因为TarMK还可以提供具有受控故障转移机制的最小停机时间解决方案。

如果在部署的前18个月中无法满足上述标准，则鼓励首先使用TarMK部署AEM，然后在满足上述标准时稍后重新评估配置，最后确定是保留在TarMK上还是迁移到MongoMK。

### 在发布实例上选择AEM MongoMK而非TarMK时出现异常 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

不建议为发布实例部署MongoMK。 部署的发布层几乎总是作为运行TarMK的完全独立的发布实例的场部署，这些实例通过从创作实例复制内容来保持同步。 这种“不共享任何内容”的体系结构适用于发布实例，允许发布层的部署以线性方式水平扩展。 场拓扑还提供了滚动应用任何更新或升级以发布实例的好处，因此对发布层的任何更改都不需要停机。

当存在多个发布者时，这不适用于在发布层上使用MongoMK群集的AEM Communities。 如果选择JSRP (请参见 [社区内容存储](/help/communities/working-with-srp.md))，则MongoMK群集将是合适的，与任何已选择MK的发布端群集（例如MongoDB或RDB）一样。

### 使用MongoMK部署AEM时的先决条件和Recommendations {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

如果您考虑使用AEM的MongoMK部署，则提供以下先决条件和建议：

**MongoDB部署的必需先决条件：**

1. 在熟悉AEM的Adobe咨询或MongoDB架构师的帮助下，MongoDB部署体系结构和规模调整必须成为项目实施的一部分；
1. 合作伙伴或客户团队中必须具备MongoDB专业知识，才能有信心维持和维护现有或新的MongoDB环境；
1. 您可以选择部署MongoDB的商业版本或开源版本(AEM同时支持两者)，但必须直接从MongoDB Inc购买MongoDB维护和支持合同；
1. 整体AEM和MongoDB体系结构和基础架构应由AdobeAEM架构师很好地定义和验证；
1. 您必须查看包含MongoDB的AEM部署的支持模型。

**针对MongoDB部署的强大建议：**

* 请参阅Adobe Experience Manager的MongoDB [文章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)；
* 查看MongoDB生产 [清单](https://docs.mongodb.org/manual/administration/production-checklist/)；
* 参加在线提供的MongoDB认证课程 [此处](https://university.mongodb.com/).

>[!NOTE]
>
>有关这些指南、先决条件和建议的所有其他问题，请联系 [Adobe客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html).

### AEM Communities的注意事项 {#considerations-for-aem-communities}

对于计划部署的站点 [AEM Communities](/help/communities/overview.md)，建议执行以下操作 [选择部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions) 针对处理发布环境中的社区成员发布的UGC进行了优化。

通过使用 [公用存储](/help/communities/working-with-srp.md)，UGC无需在创作实例和其他发布实例之间复制即可获得UGC的一致视图。

下面是一组决策矩阵，可帮助您为部署选择最佳类型的持久性：

#### 为创作实例选择部署类型 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 为发布实例选择部署类型 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是第三方软件，未包含在AEM许可包中。 欲了解更多信息，请参见 [MongoDB许可策略](https://www.mongodb.org/about/licensing/) 页面。
>
>为了充分利用AEM部署，Adobe建议许可MongoDB Enterprise版本，以便获得专业支持。
>
>该许可证包含一个标准副本集，该副本集由一个主实例和两个辅助实例组成，这两个实例可用于创作或发布部署。
>
>如果您希望在MongoDB上运行author和publish，则需要购买两个单独的许可证。
>
>欲了解更多信息，请参见 [适用于Adobe Experience Manager的MongoDB页](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
