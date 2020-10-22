---
title: 创作
seo-title: 创作
description: 在 AEM 中进行创作的概念
seo-description: 在 AEM 中进行创作的概念
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 18dcbf04bd88f63335ef36e2ec7ea81835e11b51
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 82%

---


# 创作{#authoring}

## Concept of Authoring (and Publishing) {#concept-of-authoring-and-publishing}

AEM 提供了两种环境：

* 作者
* 发布

通过这些交互可以将内容放到您的网站上，以便您的访客可以阅读该内容。

创作环境提供了用于在实际发布内容前创建、更新和审查该内容的机制：

* 作者创建并审查将要在某一时刻发布到网站的
* 这些内容将在某一时刻发布到您的网站。

![chlimage_1-132](assets/chlimage_1-132.png)

在创作环境中，AEM 的功能通过两种 UI 来提供。对于发布环境，可以设计提供给用户使用的界面的整体外观。

### 创作环境 {#author-environment}

作者在称为&#x200B;**创作环境**&#x200B;的环境中工作。这为创建内容提供了易于使用的界面（图形用户界面（GUI 或 UI））。它通常位于公司防火墙之后，防火墙能够提供全方位保护，并且要求作者使用分配了相应访问权限的帐户登录。

>[!NOTE]
>
>您的帐户需要适当的访问权限才能创建、编辑或发布内容。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 在页面上生成新内容或编辑现有内容
* 使用预定义模板来创建新内容页面
* 创建、编辑和管理资产和收藏集
* 创建、编辑和管理发布内容
* 开发营销活动和相关资源
* 开发和管理社区站点
* 移动、复制或删除内容页面、资产等
* 发布（或取消发布）页面、资产等

此外，还有一些管理任务可帮助管理内容：

* 可用于控制如何管理更改内容的工作流，例如，在发布之前实施审核
* 协调各个任务的项目

>[!NOTE]
>
>在创作环境中也可以对 AEM 进行[管理](/help/sites-administering/home.md)（适用于大多数任务）。

#### 发布环境 {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. 在该环境中，根据设计界面的具体观感，目标受众可以使用网站页面。

通常，发布环境位于内网与外网的“隔离区”中；换句话说，可用于 Internet，但不再处于内部网络的完全保护之下。

如果 AEM 站点是一个[社区站点](/help/communities/overview.md)或包含[社区组件](/help/communities/author-communities.md)，则已登录的网站访客（成员）可以与社区功能交互。例如，他们可以发布到论坛、发布评论或关注其他成员。 会员可以被授予执行通常仅限于作者环境的活动的权限，例如创建新页面（社区组）、博客文章和审核其他成员的帖子。

>[!NOTE]
>
>很遗憾，使用的术语有时存在重叠。以下术语可能存在这种情况：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
   >
   >
* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
   >
   >
* **复制**
   >  这些是用于指示数据（例如页面内容、文件、代码、用户评论）从一个环境到另一个的移动的技术术语；例如，在发布或反向复制用户注释时。
>



#### Dispatcher {#dispatcher}

为优化网站访问性能，**[调度程序](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)实施了负载平衡和缓存。**
