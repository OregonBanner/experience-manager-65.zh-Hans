---
title: 存储资源提供者概述
seo-title: 存储资源提供者概述
description: 社区通用存储
seo-description: 社区通用存储
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# 存储资源提供者概述 {#storage-resource-provider-overview}

## 简介 {#introduction}

自AEM Communities6.1起，社区内容(通常称为用户生成内容(UGC))存储在由存储资源提供商(SRP)提供的单 [个公共存储](working-with-srp.md) 中。

有几个SRP选项，所有选项都通过新的AEM Communities界面 [SocialResourceProvider API](srp-and-ugc.md) (SRP API)访问UGC，其中包括所有创建、读取、更新和删除(CRUD)操作。

所有SCF组件都使用SRP API实现，允许在不了解UGC底层拓扑或位置的情 [况下](topologies.md) ，开发代码。

***SocialResourceProvider API仅对AEM Communities的许可客户可用。***

>[!NOTE]
>
>**自定义组件**:对于AEM Communities的许可客户，SRP API可供自定义组件的开发人员使用，以便访问UGC而不考虑底层拓扑。 请参 [阅SRP和UGC Essentials](srp-and-ugc.md)。


另请参阅：

* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) —— 编码指南。
* [SocialUtils重构](socialutils.md) -将已弃用的实用程序方法映射到当前SRP实用程序方法。

## 关于存储库 {#about-the-repository}

要了解SRP，了解AEM存储库(OAK)在AEM社区站点中的角色将很有帮助。

**Java内容存储库(JCR)此标**&#x200B;准为内容存储库定义了数据模[型和应用程序编程接口](https://jackrabbit.apache.org/jcr/jcr-api.html)(JCR API)。 它将传统文件系统的特性与关系数据库的特性相结合，并添加了内容应用程序经常需要的许多附加功能。

JCR的一个实施是AEM存储库OAK。

**Apache Jackrabbit Oak(OAK)**[](../../help/sites-deploying/platform.md) OAK是JCR 2.0的一个实现，该数据存储系统专门为以内容为中心的应用程序设计。 它是为非结构化和半结构化数据设计的一种分层数据库。 存储库不仅存储面向用户的内容，还存储应用程序使用的所有代码、模板和内部数据。 访问内容的UI是 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。

JCR和OAK通常都用于引用AEM存储库。

在专用作者环境中开发站点内容后，必须将其复制到公共发布环境。 这通常通过称为复制的操作 *[完成](deploy-communities.md#replication-agents-on-author)*。 这在作者／开发人员／管理员的控制下发生。

对于UGC，内容由注册站点访客（社区成员）在公共发布环境中输入。 这是随机发生的。

出于管理和报告目的，从私人作者环境访问UGC非常有用。 通过SRP，作者对UGC的访问更加一致，而且性能也不需要从发布到作者的反向复制。

## 关于SRP {#about-srp}

将UGC保存到共享存储后，会有一个成员内容实例，在大多数部署中，该实例可以从作者和发布环境访问。 无论SRP选择如何(MSRP、ASRP、JSRP)，都必须通过SRP API以编程方式访问。

>[!NOTE]
>
>有关 [示例代码和其他详细信息](srp-and-ugc.md) ，请参阅SRP和UGC Essentials。
>
>请参 [阅使用SRP访问UGC](accessing-ugc-with-srp.md) ，了解编码时的最佳实践。


### ASRP {#asrp}

对于ASRP,UGC不存储在JCR中，它存储在由Adobe托管和管理的云服务中。 存储在ASRP中的UGC既不能通过CRXDE Lite查看，也不能使用JCR API访问。

请参 [阅ASRP -Adobe存储资源提供者](asrp.md)。

开发人员无法直接访问UGC。

ASRP使用Adobe云为查询。

### MSRP {#msrp}

对于MSRP,UGC不存储在JCR中，它存储在MongoDB中。 存储在MSRP中的UGC不能通过CRXDE Lite查看，也不能使用JCR API访问。

请参 [阅MSRP - MongoDB存储资源提供程序](msrp.md)。

MSRP与ASRP类似，因为所有AEM服务器实例都在访问同一UGC，因此可以使用通用工具直接访问存储在MongoDB中的UGC。

MSRP使用Solr查询。

### JSRP {#jsrp}

JSRP是访问单个AEM实例上的所有UGC的默认提供程序。 它提供快速体验AEM Communities6.1的能力，无需设置管理系统更新项目或ASRP。

请参 [阅JSRP - JCR存储资源提供程序](jsrp.md)。

对于JSRP，虽然UGC存储在JCR中，并可通过CRXDE Lite和JCR API访问，但强烈建议不要使用JCR API进行访问，否则将来的更改可能会影响自定义代码。

此外，不共享创作和发布环境的存储库。 虽然发布实例群集导致共享发布存储库，但发布时输入的UGC在作者中不可见，因此无法从作者管理UGC。 UGC仅保留在输入UGC的实例的AEM存储库(JCR)中。

JSRP将Oak索引用于查询。

## 关于JCR中的阴影节点 {#about-shadow-nodes-in-jcr}

模仿UGC路径的阴影节点存在于本地存储库中，用于两个用途：

1. [访问控制(ACL)](#for-access-control-acls)
1. [非现有资源(NER)](#for-non-existing-resources-ners)

无论SRP实施如何，实际UGC *不会在与阴影节点相同的位置显示。

### 对于访问控制(ACL) {#for-access-control-acls}

某些SRP实现（如ASRP和MSRP）将社区内容存储在不提供ACL验证的数据库中。 卷影节点在可应用ACL的本地存储库中提供一个位置。

使用SRP API，所有SRP选项在执行所有CRUD操作之前对阴影位置执行相同的检查。

ACL检查使用一种实用程序方法，该方法返回一条路径，用于检查应用于资源UGC的权限。

有关 [示例代码，请参阅](srp-and-ugc.md) SRP和UGC Essentials。

### 针对非现有资源(NER) {#for-non-existing-resources-ners}

某些社区组件可包含在脚本中，因此需要Sling可寻址节点来支持社区功能。 [包含的组件](scf.md#add-or-include-a-communities-component) ，称为非现有资源(NER)。

卷影节点在存储库中提供Sling可寻址位置。

>[!CAUTION]
>
>由于阴影节点具有多种用途，因此存在阴影 *节点* 并不表示组件是NER。


### 存储位置 {#storage-location}

以下是使用《社区组件指南》中的“注 [释”组件](http://localhost:4502/content/community-components/en/comments.html)[的阴影节点示例](components-guide.md):

* 此组件存在于本地存储库中：

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 相应的卷影节点存在于本地存储库中：

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在阴影节点下找不到UGC。

默认行为是在引用相关子树进行读或写时，在发布实例上设置卷影节点。

例如，假定部署为具有TarMK [发布场](msrp.md) 的MSRP。

当成 [员将](users.md) UGC发布到pub1（存储在MongoDB中）时，阴影节点将在pub1的JCR中创建。

首次在pub2上读取UGC时，如果未设置任何内容，则默认行为是创建阴影节点。

如果不需要默认行为，则必须在作者实例上设置它并转发到所有发布实例，这通常是一个手动过程。
