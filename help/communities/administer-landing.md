---
title: 社区站点
seo-title: 社区站点
description: AEM Communities文档概述
seo-description: AEM Communities文档概述
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

本节面向管理AEM Communities并假定熟悉AEM Communities功能的用户。

## 概述 {#overview}

有关概述和快速入门教程，请访问：

* [AEM Communities概述](overview.md)
* [AEM Communities 快速入门](getting-started.md)
* [AEM Communities for Enablement快速入门](getting-started-enablement.md)

## 管理和配置主题 {#administration-and-configuration-topics}

### 社区站点创建和管理 {#communities-site-creation-and-management}

* 社区控制 [台](consoles.md)

   * [Sites](sites-console.md)

      * [组（子社区）](groups.md)
   * [审核](moderation.md)
   * [成员和组管理](members.md)
   * [Enablement Resources](resources.md)
   * [报告](reports.md)


* 社区 [*工具&#x200B;*](tools.md):

   * [站点模板](sites.md)
   * [组模板](tools-groups.md)
   * [社区功能](functions.md)
   * [存储配置](srp-config.md)
   * [组件指南](components-guide.md)
   * [徽章](badges.md)


### 用户生成的内容 {#user-generated-content}

AEM Communities的一个主要功能是通过登录站点访问者（成员）生成用户生成的内容(UGC)。 要了解有关使用UGC的更多信息，请访问：

* [通用UGC商店](working-with-srp.md):UGC共享存储的SRP选择
* [审核UGC](moderate-ugc.md):受信任的成员可以批量审核UGC或在上下文中审核UGC
* [标记UGC](tag-ugc.md):功能可配置为允许成员标记内容
* [翻译UGC](translate-ugc.md):可以配置转换所有UGC的功能或允许成员转换选定的帖子
* [分析配置](analytics.md):使Adobe Analytics能够报告与成员活动相关的各种指标

### 社区成员 {#community-members}

* [管理用户和用户组](users.md):社区成员和成员组（包括特权成员）的详细信息
* [贡献限制](limits.md):限制新成员发布的能力
* [隧道服务](deploy-communities.md#tunnel-service-on-author):允许从创作环境访问发布端成员和成员组
* [“成员”和“组”控制台](members.md):允许从创作环境创建和管理发布端成员和成员组
* [用户同步](sync.md):用于在多个发布实例中同步成员和成员组
* [使用Facebook和Twitter进行社交登录](social-login.md):站点访问者使用其Facebook或Twitter凭据成为社区成员的能力
* [评分和徽章](implementing-scoring.md):为会员分配徽章以识别其角色的能力，并为会员通过参与社区获得徽章的能力
* [通知](notifications.md):能够通知成员关注的活动
* [订阅](subscriptions.md):使会员能够使用外部电子邮件与社区进行交互
* [消息](messaging.md):使成员能够使用内部消息与社区交互

### 支持功能 {#enablement-features}

* [配置启用](enablement.md):正确设置启用功能的必要信息
* [分析配置](analytics.md):启用Adobe Analytics for Communities功能的必要信息
* [标记支持资源](tag-resources.md):创建支持目录的必要条件

### 部署 {#deployment}

部署部分包含特定于AEM Communities的信息。

使用社区内容的性质会影响部署的结构：

* [推荐的社区拓扑](topologies.md)

在AEM平台上安装最新的Communities版本很重要：

* [最新社区功能包](deploy-communities.md#latestfeaturepack)

有关其他特定于Communities的信息(如升级、Dispatcher和 [复制](upgrade.md))，请 [参阅部署页](dispatcher.md)[](deploy-communities.md#replication-agents-on-author)。

## 相关社区文档 {#related-communities-documentation}

* 访问 [部署社区](deploy-communities.md) ，了解推荐的部署。

* 访问 [开发社区](communities.md) ，了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问 [创作社区组件](author-communities.md) ，了解如何创作和配置社区组件。
