---
title: 存储资源提供程序概述
seo-title: Storage Resource Provider Overview
description: 社区通用存储
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# 存储资源提供程序概述 {#storage-resource-provider-overview}

## 简介 {#introduction}

从AEM Communities 6.1开始，社区内容(通常称为用户生成内容(UGC))存储在由提供的单个通用存储中。 [存储资源提供程序](working-with-srp.md) (SRP)。

有多个SRP选项，所有这些选项都可通过新的AEM Communities界面( [SocialResourceProvider API](srp-and-ugc.md) (SRP API)，包括所有创建、读取、更新和删除(CRUD)操作。

所有SCF组件都是使用SRP API实现的，因此无需知道任何一个，即可开发代码 [底层拓扑](topologies.md) 或UGC的位置。

***SocialResourceProvider API仅适用于AEM Communities的授权客户。***

>[!NOTE]
>
>**自定义组件**：对于AEM Communities的许可客户，自定义组件的开发人员可以使用SRP API访问UGC，而无需考虑底层拓扑。 参见 [SRP和UGC Essentials](srp-and-ugc.md).

另请参阅：

* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。
* [SocialUtils重构](socialutils.md)  — 将已弃用的实用程序方法映射到当前的SRP实用程序方法。

## 关于存储库 {#about-the-repository}

要了解SRP，了解AEM存储库(OAK)在AEM社区站点中的角色很有帮助。

**Java内容存储库(JCR)**
该标准定义了一个数据模型和应用程序编程接口([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))对于内容存储库。 它结合了传统文件系统和关系数据库系统的特点，并增加了内容应用程序经常需要的一些附加功能。

JCR的一个实现是AEM存储库OAK。

**Apache Jackrabbit Oak (OAK)**
[OAK](../../help/sites-deploying/platform.md) 是JCR 2.0的一种实施，它是一个专为以内容为中心的应用程序而设计的数据存储系统。 它是一种针对非结构化和半结构化数据而设计的分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。 用于访问内容的UI是 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR和OAK通常用于引用AEM存储库。

在专用创作环境中开发站点内容后，必须将其复制到公共发布环境。 这通常通过名为的操作来完成 *[复制](deploy-communities.md#replication-agents-on-author)*. 此操作在作者/开发人员/管理员的控制下进行。

对于UGC，内容由公共发布环境中的注册站点访客（社区成员）输入。 这是随机发生的。

对于管理和报告，从专用创作环境访问UGC很有用。 使用SRP时，从“创作”访问UGC更加一致，并且性能更高，因为无需从“发布”到“创作”进行反向复制。

## 关于SRP {#about-srp}

将UGC保存到共享存储后，在大多数部署中，成员内容的单个实例既可以从创作环境也可以从发布环境访问。 无论SRP选项如何( MSRP 、 ASRP 、 JSRP )，所有选项都必须使用SRP API以编程方式访问。

>[!NOTE]
>
>参见 [SRP和UGC Essentials](srp-and-ugc.md) 示例代码和其他详细信息。
>
>参见 [使用SRP访问UGC](accessing-ugc-with-srp.md) 以了解编码时的最佳实践。

### ASRP {#asrp}

对于ASRP，UGC不会存储在JCR中，而是存储在由Adobe托管和管理的云服务中。 存储在ASRP中的UGC既不能使用CRXDE Lite查看，也不能使用JCR API访问。

参见 [ASRP -Adobe存储资源提供程序](asrp.md).

开发人员无法直接访问UGC。

ASRP使用Adobe云进行查询。

### MSRP {#msrp}

对于MSRP，UGC不存储在JCR中，而是存储在MongoDB中。 存储在MSRP中的UGC既不能使用CRXDE Lite查看，也不能使用JCR API访问。

参见 [MSRP - MongoDB存储资源提供程序](msrp.md).

虽然MSRP与ASRP相当，但由于所有AEM服务器实例都访问同一UGC，因此可以使用通用工具直接访问存储在MongoDB中的UGC。

MSRP使用Solr进行查询。

### JSRP {#jsrp}

JSRP是访问单个AEM实例上的所有UGC的默认提供程序。 它提供了快速体验AEM Communities 6.1的能力，而无需设置MSRP或ASRP。

参见 [JSRP - JCR存储资源提供程序](jsrp.md).

对于JSRP，虽然UGC存储在JCR中，并可通过CRXDE Lite和JCR API访问，但强烈建议不要使用JCR API执行此操作，否则未来的更改可能会影响自定义代码。

此外，不共享创作和发布环境的存储库。 虽然发布实例集群导致共享发布存储库，但在发布时输入的UGC在作者中不可见，因此无法从作者管理UGC。 UGC仅保留在输入它的实例的AEM存储库(JCR)中。

JSRP使用Oak索引进行查询。

## 关于JCR中的阴影节点 {#about-shadow-nodes-in-jcr}

模拟指向UGC的路径的影子节点存在于本地存储库中，用于两个目的：

1. [访问控制(ACL)](#for-access-control-acls)
1. [非现有资源(NER)](#for-non-existing-resources-ners)

不论SRP实施如何，实际的UGC都*不会*在与影子节点相同的位置可见。

### 用于访问控制(ACL) {#for-access-control-acls}

一些SRP实现（如ASRP和MSRP ）将社区内容存储在不提供ACL验证的数据库中。 影子节点提供本地存储库中可以应用ACL的位置。

使用SRP API，所有SRP选项在所有CRUD操作之前对阴影位置执行相同的检查。

ACL检查使用实用程序方法，该方法返回适合检查应用于资源UGC的权限的路径。

参见 [SRP和UGC Essentials](srp-and-ugc.md) 以获取示例代码。

### 对于非现有资源(NER) {#for-non-existing-resources-ners}

某些Communities组件可包含在脚本中，因此需要Sling可寻址节点来支持Communities功能。 [包含的组件](scf.md#add-or-include-a-communities-component) 称为非现有资源(NER)。

影子节点在存储库中提供Sling可寻址位置。

>[!CAUTION]
>
>由于影子节点具有多种用途，因此影子节点的存在具有多种用途 *非* 暗示该组件是一个NER。

### 存储位置 {#storage-location}

以下是使用 [评论组件](http://localhost:4502/content/community-components/en/comments.html) 在 [社区组件指南](components-guide.md)：

* 该组件存在于本地存储库中，位于：

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 相应的影子节点存在于本地存储库中，位于：

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在影子节点下找不到UGC。

默认行为是在发布实例上设置影子节点，只要相关子树被引用进行读取或写入。

例如，假设部署为 [MSRP](msrp.md) 使用TarMK发布场。

当 [会员](users.md) 在pub1上发布UGC（存储在MongoDB中），在pub1上的JCR中创建影子节点。

首次在pub2上读取UGC时，如果未设置任何内容，则默认行为是创建影子节点。

如果需要默认行为以外的其他行为，则必须在创作实例上设置该行为，并将其前滚到所有发布实例，这通常是手动过程。
