---
title: 存储资源提供程序概述
description: 了解社区内容(称为用户生成内容(UGC))如何存储在存储资源提供商(SRP)提供的简单通用存储中。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# 存储资源提供程序概述 {#storage-resource-provider-overview}

## 简介 {#introduction}

截至Adobe Experience Manager (AEM) Communities 6.1，社区内容(通常称为用户生成内容(UGC))存储在由提供的单个公用存储中。 [存储资源提供程序](working-with-srp.md) (SRP)。

有几个SRP选项，所有这些选项都可通过新的AEM Communities界面( [SocialResourceProvider API](srp-and-ugc.md) (SRP API)，包括所有创建、读取、更新和删除(CRUD)操作。

所有SCF组件都是使用SRP API实现的，因此无需知道以下任何一项即可开发代码： [底层拓扑](topologies.md) 或UGC的位置。

***SocialResourceProvider API仅适用于AEM Communities的授权客户。***

>[!NOTE]
>
>**自定义组件**：对于AEM Communities的许可客户，自定义组件的开发人员可以使用SRP API来访问UGC，而与底层拓扑无关。 请参阅 [SRP和UGC Essentials](srp-and-ugc.md).

另请参阅：

* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前SRP实用程序方法。

## 关于存储库 {#about-the-repository}

要了解SRP，了解AEM存储库(Oak)在AEM社区站点中的角色会很有帮助。

**Java™内容存储库(JCR)**
此标准定义了一个数据模型和应用程序编程接口([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))对于内容存储库。 它结合了传统文件系统和关系数据库系统的特点，并添加了内容应用程序通常需要的一些其他功能。

JCR的一个实现是AEM存储库Oak。

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md) 是JCR 2.0的一种实施，它是一个专为以内容为中心的应用程序而设计的数据存储系统。 它是一种针对非结构化和半结构化数据而设计的分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。 用于访问内容的UI为 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR和Oak通常用于引用AEM存储库。

在专用创作环境中开发站点内容后，必须将其复制到公共发布环境。 这通常通过名为的操作来完成 *[复制](deploy-communities.md#replication-agents-on-author)*. 此操作在作者/开发人员/管理员的控制下进行。

对于UGC，内容由公共发布环境中的注册站点访客（社区成员）输入。 这是随机发生的。

对于管理和报告，从专用创作环境访问UGC很有用。 使用SRP时，从“创作”对UGC的访问更一致，并且性能更高，因为无需从“发布”到“创作”进行反向复制。

## 关于SRP {#about-srp}

将UGC保存到共享存储后，在大多数部署中，成员内容的单个实例可以同时从创作环境和发布环境访问。 无论SRP选择如何(MSRP、ASRP、JSRP)，都必须使用SRP API以编程方式访问所有选项。

>[!NOTE]
>
>请参阅 [SRP和UGC Essentials](srp-and-ugc.md) 以了解示例代码和其他详细信息。
>
>请参阅 [使用SRP访问UGC](accessing-ugc-with-srp.md) 以了解编码时的最佳实践。

### ASRP {#asrp}

如果存在ASRP，则UGC不会存储在JCR中，而是存储在由Adobe托管和管理的云服务中。 不能使用CRXDE Lite查看或使用JCR API访问存储在ASRP中的UGC。

请参阅 [ASRP -Adobe存储资源提供程序](asrp.md).

开发人员无法直接访问UGC。

ASRP使用Adobe云进行查询。

### MSRP {#msrp}

如果存在，则MSRP、UGC不存储在JCR中，而是存储在MongoDB中。 可能无法使用CRXDE Lite查看或使用JCR API访问存储在MSRP中的UGC。

请参阅 [MSRP - MongoDB存储资源提供程序](msrp.md).

虽然MSRP可以与ASRP相媲美，但由于所有AEM服务器实例都访问相同的UGC，因此可以使用通用工具直接访问存储在MongoDB中的UGC。

MSRP使用Solr进行查询。

### JSRP {#jsrp}

JSRP是访问单个AEM实例上所有UGC的默认提供程序。 它可让您快速体验AEM Communities 6.1，而无需设置MSRP或ASRP。

请参阅 [JSRP - JCR存储资源提供程序](jsrp.md).

如果在JCR中存储UGC时存在JSRP，并且在CRXDE Lite和JCR API中可访问UGC，则Adobe建议不要使用JCR API来执行此操作。 如果这样做，则以后的更改可能会影响自定义代码。

此外，不共享创作环境和发布环境的存储库。 虽然发布实例集群导致共享发布存储库，但在发布时输入的UGC在Author上不可见，因此无法从作者管理UGC。 UGC仅保留在输入它的实例的AEM存储库(JCR)中。

JSRP使用Oak索引进行查询。

## 关于JCR中的影子节点 {#about-shadow-nodes-in-jcr}

模拟指向UGC的路径的影子节点存在于本地存储库中，以实现两个目的：

1. [访问控制(ACL)](#for-access-control-acls)
1. [非现有资源(NER)](#for-non-existing-resources-ners)

不论SRP实施如何，实际的UGC为 *非* 在与影子节点相同的位置可见。

### 用于访问控制(ACL) {#for-access-control-acls}

有些SRP实现，如ASRP和MSRP，将社区内容存储在未提供ACL验证的数据库中。 影子节点提供本地存储库中可以应用ACL的位置。

使用SRP API，所有SRP选项在所有CRUD操作之前对影子位置执行相同的检查。

ACL检查使用实用程序方法，该方法返回适合检查应用于资源UGC的权限的路径。

请参阅 [SRP和UGC Essentials](srp-and-ugc.md) 以获取示例代码。

### 对于非现有资源(NER) {#for-non-existing-resources-ners}

某些Communities组件包含在脚本中，因此需要Sling可寻址节点来支持Communities功能。 [包含的组件](scf.md#add-or-include-a-communities-component) 称为非现有资源(NER)。

影子节点在存储库中提供Sling可寻址位置。

>[!CAUTION]
>
>由于影子节点具有多种用途，因此影子节点的存在可以 *非* 表示该组件是一个NER。

### 存储位置 {#storage-location}

以下是一个阴影节点的示例，使用 [注释组件](http://localhost:4502/content/community-components/en/comments.html) 在 [社区组件指南](components-guide.md)：

* 该组件存在于本地存储库中，位于：

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 相应的影子节点存在于本地存储库中，位于：

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在影子节点下未找到UGC。

默认行为是在发布实例上设置影子节点，每次引用相关的子树进行读取或写入操作时。

例如，假设部署为 [MSRP](msrp.md) 使用TarMK发布场。

当 [会员](users.md) 在pub1上发布UGC（存储在MongoDB中），在pub1上的JCR中创建影子节点。

首次在pub2上读取UGC时，如果未设置任何内容，则默认行为是创建影子节点。

如果除了所需的默认行为之外，还必须在创作实例上设置此行为，并将其前滚到所有发布实例，这通常是手动过程。
