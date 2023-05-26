---
title: SRP — 社区内容存储
seo-title: SRP - Community Content Storage
description: 从AEM Communities 6.1开始，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公用存储中
seo-description: As of AEM Communities 6.1, user generated content (UGC) is stored in a single, common store provided by a storage resource provider (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# SRP — 社区内容存储 {#srp-community-content-storage}

## 简介 {#introduction}

从AEM Communities 6.1开始，用户生成的内容(UGC)存储在由存储资源提供程序(SRP)提供的单个公用存储中。 有几种SRP选项可供选择，如ASRP、MSRP和JSRP。

与以前的版本不同，UGC不会跨AEM实例进行反向/正向复制。 相反，SRP让UGC可从所有创作和发布实例中直接访问创建、读取、更新和删除(CRUD)操作，但JSRP除外。

以下是 [每个SRP选项的特性](#characteristics-of-srp-options)，在选择合适的SRP和时，这对于决策过程至关重要。 [基础部署](/help/communities/topologies.md).

有关使用SRP for UGC的详细信息，请参阅 [存储资源提供程序概述](/help/communities/srp.md).

>[!NOTE]
>
>SRP仅适用于社区内容。 它不影响网站内容的存储位置([节点存储](/help/sites-deploying/data-store-config.md))，并且不影响在AEM实例之间安全处理用户注册、用户配置文件和用户组(另请参阅 [管理用户数据](#managing-user-data))。

>[!CAUTION]
>
>自AEM 6.1起， [从不复制UGC](#ugc-never-replicated).
>
>当部署不包含公用存储时，例如默认存储 [JSRP](/help/communities/topologies.md#jsrp) 拓扑、UGC将仅在输入它的AEM发布或创作实例上可见。 仅当拓扑包含发布群集时，UGC才会在任何发布实例上可见。

## SRP选项的特性 {#characteristics-of-srp-options}

[ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)

利用此选项，UGC将远程保留在由Adobe托管和管理的云服务中。 它需要额外的许可证，并需要与帐户代表合作，为该特定许可证设置帐户。 ASRP要求：

* 由Adobe提供和支持的用于存储社区内容的关联云服务。
* 在特定地区（美国、欧洲、中东和非洲、亚太地区）选择数据中心。

* 所有对UGC的编程访问都必须通过SRP API。

ASRP适合：

* 对于TarMK发布场。
* 当无意投资本地存储时。

>[!NOTE]
>
>在ASRP中，将附件上载到帖子（或注释）存在限制，即50 MB。

[MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)

利用此选项，UGC将直接保留在本地MongoDB实例中。

MSRP要求：

* 本地授权安装MongoDB以存储社区内容。
* Apache Solr的本地安装。
* 所有对UGC的编程访问都必须通过SRP API。

ASRP适合：

* 对于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 需要大量社区内容时。

[DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)

使用此选项，UGC将直接保留在本地MySQL数据库实例中。

DSRP要求：

* 本地安装的MySQL用于存储社区内容。
* Apache Solr的本地安装。
* 所有对UGC的编程访问都必须通过SRP API。

DSRP适合：

* 对于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 需要大量社区内容时。

[JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

使用默认选项，没有公用存储。 UGC仅保留在与输入它的AEM实例相同的JCR存储库中。

JSRP：

* 将社区内容存储在社区内容发布到的AEM创作或发布实例的JCR存储库中。
* 要求通过SRP API访问UGC的所有程序化权限。
* 如果部署了多个发布实例，则需要发布群集（TarMK场中的发布实例之间没有复制机制）。
* 审核仅在发布环境中执行（创作和发布之间没有反向/正向复制机制）。
* 最适合用于开发、演示和培训。

## 配置SRP {#configuring-srp}

根据基础部署指定默认存储选项，操作是通过 [存储配置控制台](/help/communities/srp-config.md).

有关每个选项的配置详细信息，请参阅：

* [ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)
* [MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)
* [DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)
* [JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

如果未主动选择存储选项，则默认启用JSRP。

## 附加信息 {#additional-information}

### 从未复制UGC {#ugc-never-replicated}

在创作环境中，作者会创建页面内容并将其复制到发布环境。 当页面包含交互式AEM Communities功能（如评论、评论、论坛、博客或QnA）时，成员在发布实例上的交互（登录网站访客）会导致在发布环境中输入用户生成的内容(UGC)。

以前，此社区内容反向复制到创作实例，并从创作复制到发布实例。 使用反向和正向复制保持AEM实例之间的一致性存在问题。

从AEM Communities 6.1开始，通过为UGC使用共享存储，消除了UGC复制的需要，如上所述。

在复制站点内容时，从不复制UGC。

### 管理用户数据 {#managing-user-data}

社区感兴趣的还有 [*用户*， *用户组*、和 *用户配置文件*](/help/communities/users.md). 当拓扑为时，在发布环境中创建和更新此用户相关数据时，需要使其可用于其他发布实例 [发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

从AEM Communities 6.1开始，使用Sling分发同步用户相关数据，而不是使用复制。 有关详细信息，请访问 [用户同步](/help/communities/sync.md).

### 升级到AEM Communities 6.5 {#upgrading-to-aem-communities}

在升级到AEM 6.5 Communities时，如果需要保留预先存在的UGC，则应该根据AEM 5.6.1或AEM 6.0社区使用的是Adobe按需存储还是UGC本地存储来采取步骤。

有关详细信息，请访问 [升级到AEM Communities 6.5](/help/communities/upgrade.md).
