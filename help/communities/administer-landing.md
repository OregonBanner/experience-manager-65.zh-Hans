---
title: 社区站点
seo-title: Communities Sites
description: AEM Communities文档概述
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# 社区站点 {#communities-sites}

本节适用于那些管理AEM Communities并假定熟悉AEM Communities功能的人员。

## 概述 {#overview}

有关概述和入门教程，请访问：

* [AEM Communities概述](overview.md)
* [AEM Communities快速入门](getting-started.md)

## 管理和配置主题 {#administration-and-configuration-topics}

### 社区站点创建和管理 {#communities-site-creation-and-management}

* Communities [控制台](consoles.md)

   * [Sites](sites-console.md)

      * [组（子社区）](groups.md)
   * [审核](moderation.md)
   * [成员和组管理](members.md)
   * [报表](reports.md)


* Communities [*工具*](tools.md)：

   * [站点模板](sites.md)
   * [组模板](tools-groups.md)
   * [社区功能](functions.md)
   * [存储配置](srp-config.md)
   * [组件指南](components-guide.md)
   * [徽章](badges.md)


### 用户生成的内容 {#user-generated-content}

AEM Communities的一个主要功能是通过登录网站访客（成员）生成用户生成的内容(UGC)。 要了解有关使用UGC的更多信息，请访问：

* [通用UGC存储](working-with-srp.md)：为UGC的共享存储选择SRP
* [正在审核UGC](moderate-ugc.md)：受信任成员可以批量或上下文中审核UGC
* [标记UGC](tag-ugc.md)：可以将功能配置为允许成员标记内容
* [翻译UGC](translate-ugc.md)：可以将功能配置为翻译所有UGC或允许成员翻译选定的帖子
* [Analytics配置](analytics.md)：启用Adobe Analytics以报告有关成员活动的各种指标

### 社区成员 {#community-members}

* [管理用户和用户组](users.md)：社区成员和成员组（包括拥有权限的成员）的详细信息。
* [贡献限制](limits.md)：限制新成员发布的功能。
* [通道服务](deploy-communities.md#tunnel-service-on-author)：允许从创作环境访问发布端成员和成员组。
* [成员和组控制台](members.md)：允许从创作环境创建和管理发布端成员和成员组。
* [用户同步](sync.md)：用于跨多个发布实例同步成员和成员组。
* [使用Facebook和Twitter进行社交登录](social-login.md)：允许网站访客使用其Facebook或Twitter凭据成为社区成员。
* [评分和徽章](implementing-scoring.md)：能够分配徽章以标识成员的角色，并且成员能够通过参与社区来获取徽章。
* [通知](notifications.md)：能够让成员收到其所关注活动的通知。
* [订阅](subscriptions.md)：成员可使用外部电子邮件与社区进行交互。
* [消息传送](messaging.md)：成员可以使用内部消息与社区进行交互。

### 部署 {#deployment}

部署部分包含特定于AEM Communities的信息。

使用社区内容的性质会影响部署结构：

* [推荐的社区拓扑](topologies.md)

在AEM平台上安装最新的Communities版本很重要：

* [最新的Communities功能包](deploy-communities.md#latestfeaturepack)

有关其他特定于Communities的信息(例如 [升级](upgrade.md)， [调度程序](dispatcher.md) 和 [复制](deploy-communities.md#replication-agents-on-author).

## 相关社区文档 {#related-communities-documentation}

* 访问 [部署社区](deploy-communities.md) 以了解建议的部署。

* 访问 [发展中的社区](communities.md) 了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问 [创作社区组件](author-communities.md) 了解如何使用创作和配置社区组件。
