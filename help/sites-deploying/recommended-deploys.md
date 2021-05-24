---
title: 推荐的部署
seo-title: 推荐的部署
description: 本文介绍了AEM的推荐拓扑。
seo-description: 本文介绍了AEM的推荐拓扑。
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
source-wordcount: '1802'
ht-degree: 0%

---

# 推荐的部署{#recommended-deployments}

>[!NOTE]
>
>本页介绍了AEM的推荐拓扑。 有关群集功能以及如何配置这些功能的更多信息，请参阅[Apache Sling Discovery API文档](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)。

从AEM 6.2开始，MicroKernel用作持久性管理器。选择一个以满足您的需求取决于实例的用途和您考虑的部署类型。

以下示例用于指示在最常见的AEM设置中，推荐使用哪些功能。

## 部署方案{#deployment-scenarios}

### 单个TarMK实例{#single-tarmk-instance}

在此方案中，单个TarMK实例在单台服务器上运行。

**这是创作实例的默认部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

优点：

* 简单
* 易于维护
* 性能良好

缺点：

* 不能超出服务器容量的限制进行扩展
* 无故障切换容量

### TarMK冷备用{#tarmk-cold-standby}

一个TarMK实例用作主实例。 从主存储库复制到备用故障切换系统。

冷备用机制也可用作备份，因为完整存储库会不断复制到故障转移服务器。 故障转移服务器在冷备用模式下运行，这意味着只运行实例的HttpReceiver。

![chlimage_1-16](assets/chlimage_1-16.png)

优点：

* 简单
* 可维护性
* 演出
* 故障转移

缺点：

* 不能超出服务器容量的限制进行扩展
* 大多数情况下，一台服务器处于空闲状态
* 故障转移不是自动的。 必须在外部检测到它，然后故障切换系统才能开始提供请求。

>[!NOTE]
>
>有关如何使用TarMK冷备用配置AEM的更多信息，请参阅[此](/help/sites-deploying/tarmk-cold-standby.md)文章。

>[!NOTE]
>
>此TarMK示例中的Cold Standby部署要求主实例和备用实例都单独获得许可，因为有到故障转移服务器的持续复制。 有关许可的更多信息，请参阅[Adobe一般许可条款](https://www.adobe.com/cn/legal/terms/enterprise-licensing.html)。

### TarMK场{#tarmk-farm}

每个Oak实例使用一个TarMK实例运行。 TarMK存储库是独立的，需要保持同步。

为保持存储库同步，提供了以下事实：作者服务器正在向每个场成员发布相同的内容。 有关更多信息，请参阅[Replication](/help/sites-deploying/replication.md)。

对于AEM Communities，用户生成的内容(UGC)从不复制。 有关在TarMK场上支持UGC的信息，请参阅[有关AEM Communities](#considerations-for-aem-communities)的注意事项。

**这是发布环境的默认部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

优点：

* 演出
* 读取访问的可扩展性
* 故障转移

### 具有MongoMK故障转移的Oak群集，在单个数据中心内实现高可用性{#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

这种方法意味着在单个数据中心内访问MongoDB复制副本集的多个Oak实例，这实际上是为AEM创作环境创建一个活动 — 活动群集。 MongoDB中的副本集用于在出现硬件或网络故障时提供高可用性和冗余。

![chlimage_1-18](assets/chlimage_1-18.png)

优点：

* 能够使用新的AEM创作实例水平缩放
* 数据层的高可用性、冗余和自动故障切换

缺点：

* 某些情况下，性能可能低于使用TarMK时的性能

### 具有跨多个数据中心的MongoMK故障转移的Oak群集{#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

这种方法意味着有多个Oak实例跨多个数据中心访问一个MongoDB复制副本集，这实际上是为AEM创作环境创建一个活动群集。 MongoDB复制具有多个数据中心，提供相同的高可用性和冗余，但现在包括了处理数据中心故障的能力。

![okclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

优点：

* 能够使用新的AEM创作实例水平缩放
* 数据层的高可用性、冗余和自动故障切换（包括数据中心停机）

>[!NOTE]
>
>在上图中，AEM Server 3和AEM Server 4呈现非活动状态，假定数据中心2的AEM服务器与数据中心1的MongoDB主节点之间的网络延迟高于[此处](/help/sites-deploying/aem-with-mongodb.md#checklists)所述的要求。 如果最大延迟与要求兼容（例如，通过使用可用区），则数据中心2中的AEM服务器也可以处于活动状态，从而跨多个数据中心创建活动 — 活动的AEM群集。

>[!NOTE]
>
>有关本节中描述的MongoDB体系结构概念的其他信息，请参阅[MongoDB复制](https://docs.mongodb.org/manual/replication/)。

## 微内核：哪个使用{#microkernels-which-one-to-use}

在两个可用的微内核之间进行选择时需要考虑的基本规则是，TarMK是针对性能而设计的，而MongoMK是针对可扩展性而设计的。

您可以使用这些决策矩阵来确定最适合您需求的部署类型。

Adobe强烈建议将TarMK作为客户在所有部署方案（AEM创作实例和发布实例）中使用的默认持久性技术，以下所列用例除外。

### 在创作实例{#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}上选择AEM MongoMK而不是TarMK的例外

与TarMK相比，选择MongoMK持久性后端的主要原因是横向缩放实例。 这意味着始终运行两个或多个活动创作实例，并将MongoDB用作持久性存储系统。 运行多个创作实例的需求通常是由于单个服务器的CPU和内存容量（支持所有并发创作活动）不再可持续所致。

在新网站上线后，几乎无法预测确切的并发模型。 因此，Adobe建议在评估是否使用MongoMK和两个或多个创作活动节点时考虑以下标准：

1. 一天内连接的指定用户数：数以千计甚至更多。
1. 并发用户数：数以百计甚至更多。
1. 每天的资产摄取量：数十万甚至更多。
1. 每日的页面编辑量：数以十万计（例如，通过多站点管理器或新闻源摄取的自动更新）。
1. 每日搜索量：数以万计甚至更多。

>[!NOTE]
>
>Tough Day可用于在部署的硬件配置环境中评估客户应用程序的性能。 [此处](/help/sites-developing/tough-day.md)提供了有关此工具的更多信息。

MongoDB的最低部署通常涉及以下拓扑：

* 一个MongoDB副本集，由一个主节点、两个次节点组成，每个MongoDB实例在可用区中运行，每个节点的延迟少于15毫秒；
* 创作实例群集，具有一个领导节点、一个非领导节点和两者始终处于活动状态，每个创作实例在每个数据中心中运行，其中MongoDB主实例和次实例正在运行。

此外，还强烈建议在共享文件系统或Amazon S3上配置数据存储，以便资产或二进制文件不存储在MongoDB中。 这将确保部署内的最佳性能。

部署具有两个或多个创作实例群集的MongoDB复制副本集的额外好处之一是，在创作实例、MongoDB复制副本或完全数据中心故障的情况下，具有自动化恢复方案，并且停机时间最短。 尽管如此，选择MongoMK而不是TarMK不应仅受恢复要求的驱动，因为TarMK还可以通过受控故障切换机制提供最小的停机时间解决方案。

如果预计在部署后的头18个月内不满足上述标准，我们建议首先使用TarMK部署AEM，然后在以后应用上述标准时重新评估您的配置，最后确定是保留在TarMK上还是迁移到MongoMK。

### 在发布实例{#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}上选择AEM MongoMK而不是TarMK的例外

不建议为发布实例部署MongoMK。 部署的发布层几乎总是部署为运行TarMK的完全独立的发布实例的场，这些实例通过从创作实例复制内容来保持同步。 此适用于发布实例的“无共享”架构允许发布层部署以线性方式水平扩展。 场拓扑还可以以滚动方式对发布实例应用任何更新或升级，这样对发布层所做的任何更改都不需要停机。

当有多个发布者时，这不适用于在发布层上使用MongoMK群集的AEM Communities。 如果选择JSRP（请参阅[社区内容存储](/help/communities/working-with-srp.md)），则MongoMK群集将是合适的，与任何发布端群集一样，无论选择的MK如MongoDB或RDB。

### 使用MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}部署AEM时的先决条件和Recommendations

如果您考虑部署AEM的MongoMK，可以使用一组先决条件和建议：

**MongoDB部署的必需先决条件：**

1. MongoDB部署架构和大小调整必须在项目实施的一部分，并且需要获得熟悉AEM的Adobe咨询或MongoDB架构师的帮助；
1. MongoDB的专业知识必须存在于合作伙伴或客户团队中，以便能够维持和维护现有或新的MongoDB环境；
1. 您可以选择部署商用或开源版本的MongoDB(AEM支持两者)，但必须直接从MongoDB公司购买MongoDB维护和支持合同；
1. 总的AEM和MongoDB体系结构和基础架构应由AdobeAEM架构师进行明确定义和验证；
1. 您必须查看包含MongoDB的AEM部署的支持模型。

**对MongoDB部署的强项建议：**

* 请查阅Adobe Experience Manager的MongoDB [文章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* 查看MongoDB生产[核对清单](https://docs.mongodb.org/manual/administration/production-checklist/);
* 参加在线[此处](https://university.mongodb.com/)的MongoDB认证课程。

>[!NOTE]
>
>有关这些准则、先决条件和建议的所有其他问题，请联系[Adobe客户关怀](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)。

### 有关AEM Communities的注意事项{#considerations-for-aem-communities}

对于计划部署[AEM Communities](/help/communities/overview.md)的站点，建议[选择一个部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions)，该部署已优化，以处理由社区成员从发布环境发布的UGC。

通过使用[公共存储](/help/communities/working-with-srp.md)，无需在创作实例和其他发布实例之间复制UGC，即可获得UGC的一致视图。

下面是一组决策矩阵，可帮助您为部署选择最佳类型的持久性：

#### 为创作实例{#choosing-the-deployment-type-for-author-instances}选择部署类型

![chlimage_1-19](assets/chlimage_1-19.png)

#### 为发布实例{#choosing-the-deployment-type-for-publish-instances}选择部署类型

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是第三方软件，未包含在AEM授权包中。 有关详细信息，请参阅[MongoDB授权策略](https://www.mongodb.org/about/licensing/)页。
>
>为了充分利用AEM部署，Adobe建议授权MongoDB企业版本，以便从专业支持中受益。
>
>该许可证包含一个标准副本集，该副本集由一个主实例和两个辅助实例组成，这两个实例可用于创作或发布部署。
>
>如果您希望在MongoDB上同时运行创作和发布，则需要购买两个单独的许可证。
>
>有关更多信息，请参阅[MongoDB for Adobe Experience Manager页面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。
