---
title: 发展社区
seo-title: 发展社区
description: 创建和自定义社区功能，如论坛、用户组等
seo-description: 创建和自定义社区功能，如论坛、用户组等
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---

# 开发社区{#developing-communities}

## 概述 {#overview}

AEM Communities简化了社区功能（如论坛、用户组、博客、问答、日历、评论、评论、投票、评级和任务）的创建和自定义。 这些功能会导致在发布环境中输入用户生成的内容(UGC)。

[社区站点](overview.md#communitiessites)的基础是[社交组件框架](scf.md)(SCF)。 创建社区站点首先选择由[社区功能](functions.md)组成的[社区站点模板](sites-console.md)。

有关概述和快速入门教程，请访问：

* [AEM Communities概述](overview.md)
* [AEM Communities 快速入门](getting-started.md)
* [AEM Communities启用入门](getting-started-enablement.md)

>[!NOTE]
> 
>强烈建议保持[最新版本](deploy-communities.md#latest-releases)的最新状态。

## 建议的部署{#recommended-deployments}

* [社区内容存储](working-with-srp.md):讨论UGC公用存储的可用SRP选项
* [推荐的社区拓扑](topologies.md):讨论了基于用例的拓扑和SRP选择

## 社交组件框架{#social-component-framework}

* [社交组件框架](scf.md):框架和API概述。
* [SCF Handlebars Helpers](handlebars-helpers.md):默认帮助器，如何编写自定义帮助器。
* [客户端自定义](client-customize.md):自定义在浏览器中运行的代码。
* [服务器端自定义](server-customize.md):自定义在服务器上运行的代码。
* [存储资源提供程序(SRP)](srp.md):社区内容存储概述。
* [编码准则](code-guide.md):准则、提示和技巧。
* [社区组件指南](components-guide.md):交互式开发工具。

## 组件、函数和功能要点{#component-function-and-feature-essentials}

AEM Communities组件、功能和特性为[社区站点](sites-console.md)提供构建基块。

* [组件、功能和功能要点](essentials.md)
* [适用于社区组件的Clientlibs](clientlibs.md)
* [社区功能](functions.md)
* [社区组模板](tools-groups.md)
* [社区站点模板](sites.md)

## 社区成员 {#community-members}

* [管理用户和用户组](users.md)
* [使用Facebook和Twitter进行社交登录](social-login.md)

## 社区组 {#community-groups}

[社](overview.md#communitygroups) 区群组是允许社区成员在社区站点内形成子社区的概念。可以在发布或创作环境中创建社区组。

* [社区组要点](essentials-groups.md)
* [组函数](functions.md#groups-function)
* [社区组模板](tools-groups.md)
* [管理用户和用户组](users.md)
* [作者社区组](creating-groups.md)

## 管理数据{#managing-data}

* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP API实用程序方法和示例
* [标记要点](tag.md)  — 社区成员标记UGC和/或编录启用资源的功能

## 教程 {#tutorials}

* [客户端教程](tutorials.md#client-side-customization)
* [服务器端教程](tutorials.md#server-side-customization)
* [操作说明](tutorials.md#how-to-instructions)

## 疑难解答 {#troubleshooting}

* [疑难解答](troubleshooting.md)
* [已知问题](/help/release-notes/known-issues.md)

## 相关社区文档{#related-communities-documentation}

* 访问[部署Communities](deploy-communities.md)以了解建议的部署和调度程序配置。

* 访问[管理社区站点](administer-landing.md) ，了解有关创建社区站点、配置社区站点模板、审核社区内容、管理成员以及配置消息传送的信息。

* 访问[创作社区组件](author-communities.md) ，了解如何使用和配置社区组件进行创作。
