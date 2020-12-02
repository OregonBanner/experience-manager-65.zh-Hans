---
title: 建议的部署
seo-title: 建议的部署
description: 本文介绍AEM的推荐拓扑。
seo-description: 本文介绍AEM的推荐拓扑。
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 0%

---


# 建议的部署{#recommended-deployments}

>[!NOTE]
>
>本页介绍AEM的推荐拓扑。 有关群集功能以及如何配置这些功能的详细信息，请参阅[Apache Sling Discovery API文档](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)。

从AEM 6.2开始，MicroKernel充当持久性管理器。选择一个以满足您的需求取决于实例的用途和您考虑的部署类型。

以下示例旨在说明它们在最常见的AEM设置中的推荐用途。

## 部署方案{#deployment-scenarios}

### 单个TarMK实例{#single-tarmk-instance}

在这种情况下，单个TarMK实例在单台服务器上运行。

**这是作者实例的默认部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

优势：

* 简单
* 轻松维护
* 良好性能

缺点是：

* 不能超出服务器容量的限制
* 无故障转移容量

### TarMK冷待机{#tarmk-cold-standby}

一个TarMK实例充当主实例。 从主资料库复制到备用故障转移系统。

冷备用机制也可以用作备份，因为完整的存储库会不断复制到故障转移服务器。 故障转移服务器以冷待机模式运行，这意味着只运行实例的HttpReceiver。

![chlimage_1-16](assets/chlimage_1-16.png)

优势：

* 简单
* 可维护性
* 演出
* 故障转移

缺点是：

* 不能超出服务器容量的限制
* 大多数时候，一台服务器处于空闲状态
* 故障转移不是自动的。 在故障转移系统能够开始服务请求之前，必须在外部检测到它。

>[!NOTE]
>
>有关如何使用TarMK Cold Standby配置AEM的详细信息，请参阅[此](/help/sites-deploying/tarmk-cold-standby.md)文章。

>[!NOTE]
>
>此TarMK示例中的Cold Standby部署要求分别为主实例和备用实例授予许可，因为存在到故障转移服务器的持续复制。 有关许可的详细信息，请查阅[Adobe一般许可条款](https://www.adobe.com/cn/legal/terms/enterprise-licensing.html)。

### TarMK Farm {#tarmk-farm}

使用一个TarMK实例分别运行多个Oak实例。 TarMK存储库是独立的，需要保持同步。

使存储库保持同步的前提是作者服务器向每个农场成员发布相同的内容。 有关详细信息，请参阅[复制](/help/sites-deploying/replication.md)。

对于AEM Communities，用户生成的内容(UGC)从不复制。 有关在TarMK农场上支持UGC的信息，请参见[有关AEM Communities的注意事项](#considerations-for-aem-communities)。

**这是发布环境的默认部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

优势：

* 演出
* 可扩展性，可读访问
* 故障转移

### 具有MongoMK故障转移的Oak群集，在单个数据中心{#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}中实现高可用性

此方法意味着访问单个数据中心内的MongoDB副本集的多个Oak实例，实际上是为AEM作者环境创建一个活动——活动群集。 MongoDB中的副本集用于在硬件或网络故障事件提供高可用性和冗余。

![chlimage_1-18](assets/chlimage_1-18.png)

优势：

* 能借助新的AEM作者实例水平缩放
* 数据层的高可用性、冗余和自动故障切换

缺点是：

* 在某些情况下，性能可能低于TarMK

### 具有跨多个数据中心的MongoMK故障转移的Oak群集{#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法意味着多个Oak实例访问跨多个数据中心的MongoDB副本集，实际上为AEM作者环境创建了一个活动——活动群集。 MongoDB复制具有多个数据中心，提供相同的高可用性和冗余，但现在包括处理数据中心中断的能力。

![okclustermongo故障转移数据中心](assets/oakclustermongofailover2datacenters.png)

优势：

* 能借助新的AEM作者实例水平缩放
* 数据层的高可用性、冗余和自动故障转移（包括数据中心停机）

>[!NOTE]
>
>在上图中，AEM Server 3和AEM Server 4呈现非活动状态，假定数据中心2的AEM服务器与数据中心1的MongoDB主节点之间的网络延迟高于此处记录的[](/help/sites-deploying/aem-with-mongodb.md#checklists)的要求。 如果最大延迟与要求兼容，例如通过使用可用区，则数据中心2中的AEM服务器也可以处于活动状态，跨多个数据中心创建活动——活动的AEM群集。

>[!NOTE]
>
>有关本节所述的MongoDB体系结构概念的其他信息，请参见[MongoDB复制](https://docs.mongodb.org/manual/replication/)。

## 微内核：哪个使用{#microkernels-which-one-to-use}

在两种可用的微内核之间进行选择时需要考虑的基本规则是TarMK是为性能而设计，而MongoMK是为可扩展性而设计的。

您可以使用这些决策表来确定哪种部署类型最适合您的需求。

Adobe强烈建议TarMK成为客户在所有部署方案（AEM作者实例和发布实例除外）中使用的默认持久性技术，下面概述的用例除外。

### 在创作实例{#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}上选择AEM MongoMK而不是TarMK的例外

选择MongoMK持久性后端而非TarMK的主要原因是水平缩放实例。 这意味着始终运行两个或更多个活动的作者实例，并将MongoDB用作持久性存储系统。 需要运行多个创作实例通常是由于单个服务器的CPU和内存容量支持所有并发创作活动已不可持续。

几乎不可能预测新站点发布后的确切并发模型。 因此，Adobe建议在评估是否使用MongoMK和两个或更多作者活动节点时考虑以下条件：

1. 一天内连接的指定用户数：数以千计。
1. 并发用户数：数以百计的。
1. 每天资产摄取量：数十万甚至更多。
1. 每天编辑的页面数量：（包括通过多站点管理器或新闻源获取的自动更新）。
1. 每天的搜索量：数以万计甚至更多。

>[!NOTE]
>
>Tough Day可用于在部署的硬件配置环境中评估客户应用程序的性能。 有关此工具的详细信息，请[此处](/help/sites-developing/tough-day.md)。

使用MongoDB进行的最低部署通常涉及以下拓扑：

* 由一个主节点、两个辅助节点组成的MongoDB复制副本集，每个MongoDB实例在可用区中运行，每个节点的延迟低于15毫秒；
* 创作实例群集，其中一个领导节点、一个非领导节点并且两者始终处于活动状态，每个创作实例在每个数据中心中运行，其中MongoDB主实例和次实例正在运行。

此外，强烈建议在共享文件系统或AmazonS3上配置数据存储，以使资源或二进制不存储在MongoDB中。 这将确保部署内的最佳性能。

使用两个或多个作者实例的群集部署MongoDB副本集的额外好处之一是，在创作实例、MongoDB副本或整个数据中心故障的情况下，可以在最短的停机时间内实现自动恢复。 尽管如此，选择MongoMK而不是TarMK不应完全由恢复要求驱动，因为TarMK还可以提供具有受控故障转移机制的最小停机时间解决方案。

如果预计在部署的头18个月内不满足上述标准，则建议首先使用TarMK部署AEM，然后在以后应用上述标准时重新评估您的配置，最后确定是保留在TarMK上还是迁移到MongoMK。

### 在发布实例{#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}上选择AEM MongoMK而不是TarMK的例外

不建议为发布实例部署MongoMK。 部署的发布层几乎始终部署为运行TarMK的完全独立发布实例的场，这些实例通过从创作实例复制内容而保持同步。 此“无共享”架构适用于发布实例，允许发布层的部署以线性方式水平缩放。 农场拓扑还可以对发布实例进行滚动应用任何更新或升级，这样对发布层的任何更改都不需要停机。

这不适用于在发布层上使用MongoMK群集的AEM Communities，只要有多个发布者。 如果选择JSRP(请参阅[社区内容存储](/help/communities/working-with-srp.md))，则MongoMK群集将是合适的，与任何发布端群集一样，无论选择的MK如MongoDB或RDB。

### 使用MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}部署AEM的先决条件和Recommendations

如果您正在考虑为AEM部署MongoMK，则可以获得一套先决条件和建议：

**MongoDB部署的必需先决条件：**

1. 在Adobe咨询或熟悉AEM的MongoDB架构师的帮助下，MongoDB部署架构和规模必须成为项目实施的一部分；
1. MongoDB的专业知识必须在合作伙伴或客户团队中，以便能够维持和维持现有或新的MongoDB环境;
1. 您可以选择部署MongoDB的商业或开放源版本(AEM支持两者)，但必须直接从MongoDB公司购买MongoDB维护和支持合同；
1. 总的AEM和MongoDB体系结构和基础架构应由AdobeAEM架构师进行明确定义和验证；
1. 您必须查看包含MongoDB的AEM部署的支持模型。

**对MongoDB部署的强烈建议：**

* 请查阅Adobe Experience Manager的MongoDB [文章](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* 查看MongoDB产品[清单](https://docs.mongodb.org/manual/administration/production-checklist/);
* 参加在线[的MongoDB认证课程](https://university.mongodb.com/)。

>[!NOTE]
>
>有关这些准则、先决条件和建议的所有其他问题，请与[Adobe客户服务部](https://helpx.adobe.com/cn/marketing-cloud/contact-support.html)联系。

### 对AEM Communities的考虑{#considerations-for-aem-communities}

对于计划部署[AEM Communities](/help/communities/overview.md)的站点，建议[选择为处理由社区成员从发布环境发布的UGC而优化的部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions)。

通过使用[公用存储](/help/communities/working-with-srp.md)，无需在作者实例和其他发布实例之间复制UGC，即可获得一致的UGC视图。

下面是一组决策矩阵，可帮助您为部署选择最佳类型的持久性：

#### 选择作者实例的部署类型{#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 选择发布实例的部署类型{#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是第三方软件，不包含在AEM授权包中。 有关详细信息，请参阅[MongoDB授权策略](https://www.mongodb.org/about/licensing/)页。
>
>为了充分利用AEM部署，Adobe建议授权许可MongoDB企业版，以从专业支持中受益。
>
>该许可证包含一个标准副本集，该副本集由一个主实例和两个可用于作者或发布部署的辅助实例组成。
>
>如果您希望在MongoDB上运行作者和发布，则需要购买两个单独的许可证。
>
>有关详细信息，请参阅[MongoDB forAdobe Experience Manager页面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

