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
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 创作{#authoring}

## Concept of Authoring (and Publishing) {#concept-of-authoring-and-publishing}

AEM 提供了两种环境：

* 创作
* 发布

通过这些交互可以将内容放到您的网站上，以便您的访客可以阅读该内容。

创作环境提供了用于在实际发布内容前创建、更新和审查该内容的机制：

* 作者创建并审查将要在某一时刻发布到网站的
* 这些内容将在某一时刻发布到您的网站。

![chlimage_1-132](assets/chlimage_1-132.png)

在创作环境中，AEM 的功能通过两种 UI 来提供。对于发布环境，可以设计提供给用户使用的界面的整体外观。

>[!NOTE]
>
>AEM 本身被用于创作 AEM 文档。
>
>还可以与调度程序一起用于发布。

### 创作环境 {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

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

When ready, the AEM site&#39;s content is published to the **publish environment**. 此处，根据设计界面的外观和风格，网站页面可供目标受众使用。

通常，发布环境位于内网与外网的“隔离区”中；换句话说，可用于 Internet，但不再处于内部网络的完全保护之下。

如果 AEM 站点是一个[社区站点](/help/communities/overview.md)或包含[社区组件](/help/communities/author-communities.md)，则已登录的网站访客（成员）可以与社区功能交互。例如，他们可以发布到论坛、发布评论或关注其他成员。 可授予会员执行通常仅限于创作环境的活动的权限，例如创建新页面（社区组）、博客文章和审核其他会员的帖子。

>[!NOTE]
>
>很遗憾，使用的术语有时存在重叠。以下术语可能存在这种情况：
>
>* **发布/取消发布**
   >  这些是使内容在发布环境中公开可用（或不公开）的主要操作条款。
   >
   >
* **激活／取消激活**
   >  这些术语与发布／取消发布同义。
   >
   >
* **复制**
   >  这些是用于指示数据（例如，页面内容、文件、代码、用户评论）从一个环境移动到另一个环境的技术术语；例如，在发布或反向复制用户注释时。
>



#### Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
