---
title: SRP —— 社区内容存储
seo-title: SRP —— 社区内容存储
description: 自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公用存储中
seo-description: 自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公用存储中
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# SRP —— 社区内容存储 {#srp-community-content-storage}

## 简介 {#introduction}

自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公共存储中。 可以从多个SRP选项中进行选择，如ASRP、MSRP和JSRP。

与以前的版本不同，AEM实例之间不存在UGC的反向／正向复制。 相反，SRP使UGC可以直接从所有作者和发布实例创建、读取、更新和删除(CRUD)操作访问，JSRP除外。

以下是每 [个SRP选项的特点](#characteristics-of-srp-options)，这是选择适当的SRP和基础部署时决策过程的关 [键信息](/help/communities/topologies.md)。

有关使用UGC的SRP的详细信息，请参阅 [存储资源提供者概述](/help/communities/srp.md)。

>[!NOTE]
>
>SRP仅适用于社区内容。 它不影响站点内容的存储位置(节点存[储](/help/sites-deploying/data-store-config.md))，并且不影响AEM实例之间用户注册、用户用户档案和用户组的安全处理(另请参阅 [管理用户数据](#managing-user-data))。


>[!CAUTION]
>
>自AEM 6.1起， [UGC不会复制](#ugc-never-replicated)。
>
>当部署不包括公用存储(如默认 [JSRP](/help/communities/topologies.md#jsrp) 拓扑)时，UGC将仅在输入AEM发布或作者实例上可见。 只有当拓扑包含发布群集时，UGC才会在任何发布实例上可见。


## SRP选项的特点 {#characteristics-of-srp-options}

[ASRP - Adobe存储资源提供商](/help/communities/asrp.md)

通过此选项，UGC将在由Adobe托管和管理的云服务中远程保留。 它需要额外的许可证并与客户代表合作为该特定许可证提供帐户。 ASRP要求：

* Adobe提供并支持的用于存储社区内容的关联云服务。
* 在特定地理位置（美国、欧洲、中东和非洲、亚太地区）选择数据中心。

* 对UGC的所有程序化访问都是通过SRP API。

ASRP适合：

* 对于TarMK发布场。
* 当没有投资当地存储的意图时。

>[!NOTE]
>
>在ASRP中，将附件上传到帖子（或评论）的限制为50 MB。


[MSRP - MongoDB存储资源提供商](/help/communities/msrp.md)

使用此选项，UGC将直接保留在本地MongoDB实例中。

MSRP要求：

* 本地许可安装的MongoDB，用于存储社区内容。
* Apache Solr的本地安装。
* 对UGC的所有程序化访问都是通过SRP API。

ASRP适合：

* 用于现有TarMK发布农场。
* 用于MongoMK或RdbMK群集。
* 当需要大量社区内容时。

[DSRP —— 关系数据库存储资源提供程序](/help/communities/dsrp.md)

使用此选项，UGC将直接保留在本地MySQL数据库实例中。

DSRP要求：

* 用于存储社区内容的MySQL的本地安装。
* Apache Solr的本地安装。
* 对UGC的所有程序化访问都是通过SRP API。

DSRP适合：

* 用于现有TarMK发布农场。
* 用于MongoMK或RdbMK群集。
* 当需要大量社区内容时。

[JSRP - JCR存储资源提供商](/help/communities/jsrp.md)

使用默认选项时，不存在公用商店。 UGC仅会与输入AEM实例的JCR存储库中保留。

JSRP:

* 将社区内容存储在AEM作者的JCR存储库中或发布到其的发布实例中。
* 需要通过SRP API以编程方式访问UGC。
* 如果部署了多个发布实例，则需要发布群集（TarMK农场中的发布实例之间没有复制机制）。
* 仲裁仅在发布环境中执行（创作和发布之间没有反向／正向复制机制）。
* 最适合开发、演示和培训。

## 配置SRP {#configuring-srp}

根据基础部署指定默认存储选项是通过存储配置控制 [台进行的](/help/communities/srp-config.md)。

有关每个选项的配置详细信息，请参阅：

* [ASRP - Adobe存储资源提供商](/help/communities/asrp.md)
* [MSRP - MongoDB存储资源提供商](/help/communities/msrp.md)
* [DSRP —— 关系数据库存储资源提供程序](/help/communities/dsrp.md)
* [JSRP - JCR存储资源提供商](/help/communities/jsrp.md)

如果未主动选择存储选项，则默认情况下将启用JSRP。

## 附加信息 {#additional-information}

### UGC从未复制 {#ugc-never-replicated}

在创作环境中，作者创建页面内容并将其复制到发布环境。 当页面包含交互式AEM Communities功能（如评论、评论、论坛、博客或问题与解答）时，成员(在站点访客中签名)对发布实例的交互会导致用户生成的内容(UGC)在发布环境中输入。

以前，此社区内容会反向复制到作者实例中，并从作者复制到发布实例中。 在具有反向和正向复制的AEM实例之间保持一致性存在问题。

从AEM Communities 6.1开始，通过使用UGC的共享存储，消除了复制UGC的需求，如上所述。

复制站点内容时，从不复制UGC。

### 管理用户数据 {#managing-user-data}

社区还关注用 [*户&#x200B;*、用*&#x200B;户组&#x200B;*和用*&#x200B;户用户档案&#x200B;*](/help/communities/users.md)。 在发布环境中创建和更新此用户相关数据后，当拓扑为发布场时，需要使其他发布实例可[用该数据](/help/sites-deploying/recommended-deploys.md#tarmk-farm)。

自AEM Communities 6.1起，与用户相关的数据将使用Sling分发而不是复制进行同步。 有关详细信息，请访 [问用户同步](/help/communities/sync.md)。

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

升级到AEM 6.5 Communities时，如果需要保留先前存在的UGC，则应根据AEM 5.6.1或AEM 6.0社区是使用Adobe点播存储还是UGC的内部部署存储来采取步骤。

有关详细信息， [请访问升级到AEM Communities 6.5](/help/communities/upgrade.md)。
