---
title: SRP — 社区内容存储
seo-title: SRP — 社区内容存储
description: 自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公共存储中
seo-description: 自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公共存储中
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---


# SRP — 社区内容存储{#srp-community-content-storage}

## 简介 {#introduction}

自AEM Communities 6.1起，用户生成的内容(UGC)存储在由存储资源提供商(SRP)提供的单个公共存储中。 可以选择若干SRP选项，如ASRP、MSRP和JSRP。

与以前的版本不同，UGC在AEM实例中不进行反向/正向复制。 相反，SRP使UGC能够从所有作者实例和发布实例中直接访问创建、读取、更新和删除(CRUD)操作，JSRP除外。

以下是每个SRP选项](#characteristics-of-srp-options)的[特性，在选择适当的SRP和[基础部署](/help/communities/topologies.md)时，这是决策过程的关键信息。

有关UGC使用SRP的详细信息，请参阅[存储资源提供程序概述](/help/communities/srp.md)。

>[!NOTE]
>
>SRP仅适用于社区内容。 它不影响存储站点内容的位置([node store](/help/sites-deploying/data-store-config.md))，也不影响AEM实例之间用户注册、用户用户档案和用户组的安全处理（另请参阅[管理用户数据](#managing-user-data)）。

>[!CAUTION]
>
>自AEM 6.1起，[UGC从不复制](#ugc-never-replicated)。
>
>当部署不包括公用存储（如默认的[JSRP](/help/communities/topologies.md#jsrp)拓扑）时，UGC将仅在输入UGC的AEM发布或作者实例上可见。 仅当拓扑包含发布群集时，UGC才会显示在任何发布实例上。

## SRP选项{#characteristics-of-srp-options}的特性

[ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)

通过此选项，UGC将在由Adobe托管和管理的云服务中远程保留。 它需要额外的许可证并与帐户代表合作来为该特定许可证提供帐户。 ASRP要求：

* 由Adobe提供并支持的用于存储社区内容的关联云服务。
* 在特定地理位置（美国、欧洲、中东和非洲、亚太地区）选择数据中心。

* 所有对UGC的程序化访问都是通过SRP API进行的。

ASRP是合适的：

* 对于TarMK发布场。
* 当没有投资本地存储时。

>[!NOTE]
>
>限制将附件上传到ASRP中的帖子（或评论），这是50 MB。

[MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)

使用此选项，UGC将直接保留在本地MongoDB实例中。

MSRP要求：

* 本地授权的MongoDB安装，用于存储社区内容。
* Apache Solr的本地安装。
* 所有对UGC的程序化访问都是通过SRP API进行的。

ASRP是合适的：

* 用于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 当需要大量社区内容时。

[DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)

使用此选项，UGC将直接保留在本地MySQL数据库实例中。

DSRP要求：

* 本地安装MySQL以存储社区内容。
* Apache Solr的本地安装。
* 所有对UGC的程序化访问都是通过SRP API进行的。

DSRP适合：

* 用于现有TarMK发布场。
* 用于MongoMK或RdbMK群集。
* 当需要大量社区内容时。

[JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

使用默认选项时，不存在通用商店。 UGC仅会与输入UGC的AEM实例保存在同一JCR存储库中。

JSRP:

* 将社区内容存储在AEM作者的JCR存储库中或发布实例中，该实例将发布到该实例。
* 需要通过SRP API对UGC进行所有编程访问。
* 如果部署了多个发布实例，则需要发布群集（TarMK场中的发布实例之间没有复制机制）。
* 仲裁仅在发布环境中执行（在作者和发布之间没有反向/正向复制机制）。
* 最适合开发、演示和培训。

## 配置SRP {#configuring-srp}

通过[存储配置控制台](/help/communities/srp-config.md)指定默认的存储选项（基于基础部署）。

有关每个选项的配置详细信息，请参阅：

* [ASRP -Adobe存储资源提供程序](/help/communities/asrp.md)
* [MSRP - MongoDB存储资源提供程序](/help/communities/msrp.md)
* [DSRP — 关系数据库存储资源提供程序](/help/communities/dsrp.md)
* [JSRP - JCR存储资源提供程序](/help/communities/jsrp.md)

如果未主动选择存储选项，则默认情况下启用JSRP。

## 附加信息 {#additional-information}

### UGC从未复制{#ugc-never-replicated}

在创作环境中，作者创建页面内容并将其复制到发布环境。 当页面包含交互式AEM Communities功能（如注释、审阅、论坛、博客或问题与答案）时，成员(在站点访客中签名)对发布实例的交互会导致用户生成的内容(UGC)进入发布环境。

以前，此社区内容会反向复制到作者实例，并从作者复制到发布实例。 在具有反向和正向复制的AEM实例之间保持一致性是有问题的。

从AEM Communities 6.1开始，已通过使用UGC的共享存储（如上所述），消除了复制UGC的需要。

复制站点内容时，从不复制UGC。

### 管理用户数据{#managing-user-data}

Communities同样感兴趣的是&#x200B;[*用户*、*用户组*&#x200B;和&#x200B;*用户用户档案*](/help/communities/users.md)。 当拓扑为[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)时，当在发布环境中创建和更新此用户相关数据时，需要使其他发布实例可用。

自AEM Communities 6.1起，将使用Sling分发（而非复制）同步与用户相关的数据。 有关详细信息，请访问[用户同步](/help/communities/sync.md)。

### 升级到AEM Communities 6.5 {#upgrading-to-aem-communities}

升级到AEM 6.5社区时，如果需要保留预先存在的UGC，则应根据AEM 5.6.1或AEM 6.0社区是使用Adobe点播存储还是预置存储UGC采取相应步骤。

有关详细信息，请访问[升级到AEM Communities 6.5](/help/communities/upgrade.md)。
