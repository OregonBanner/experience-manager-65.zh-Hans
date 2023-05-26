---
title: 创作
seo-title: Authoring
description: 在 AEM 中进行创作的概念
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 32%

---

# 创作{#authoring}

## 创作（和发布）概念 {#concept-of-authoring-and-publishing}

AEM为您提供了两个环境：

* 创作
* 发布

通过这些交互，您可以在网站上提供内容，以便访客能够阅读这些内容。

创作环境提供了用于在实际发布此内容之前创建、更新和审阅此内容的机制：

* 作者创建和查看内容（可以是多种类型；例如，页面、资产、出版物等）
* 在某个时候，它会发布到您的网站。

![chlimage_1-132](assets/chlimage_1-132.png)

在创作环境中，AEM的功能可通过两个UI使用。 对于发布环境，可以设计提供给用户使用的界面的整体外观。

### 创作环境 {#author-environment}

作者在称为&#x200B;**创作环境**&#x200B;的环境中工作。这为创建内容提供了易于使用的界面（图形用户界面（GUI 或 UI））。它通常位于公司防火墙的后面，可提供全面保护，并要求作者使用分配了相应访问权限的帐户登录。

>[!NOTE]
>
>您的帐户需要适当的访问权限才能创建、编辑或发布内容。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 在页面上生成新内容或编辑现有内容
* 使用预定义模板创建新内容页面
* 创建、编辑和管理您的资源和收藏集
* 创建、编辑和管理您的出版物
* 开发您的营销活动和相关资源
* 开发和管理社区站点
* 移动、复制或删除内容页面、资产等
* 发布（或取消发布）页面、资产等

此外，还有一些管理任务可帮助管理内容：

* 控制更改管理方式的工作流；例如。 发布前强制执行审核
* 协调各个任务的项目

>[!NOTE]
>
>AEM也是 [已管理](/help/sites-administering/home.md) （适用于大多数任务）来自创作环境。

#### 发布环境 {#publish-environment}

准备就绪后，AEM站点的内容将发布到 **发布环境**. 在该环境中，根据设计界面的具体观感，目标受众可以使用网站页面。

通常，发布环境位于非军事区内；换句话说，发布环境可供Internet使用，但不再受内部网络的完全保护。

当AEM站点为 [社区站点](/help/communities/overview.md)，或包含 [Communities组件](/help/communities/author-communities.md)，登录的网站访客（成员）可以与Communities功能进行交互。 例如，他们可能会向论坛发帖、发表评论或关注其他成员。 可以授予成员执行通常仅限于创作环境的活动的权限，例如创建新页面（社区组）、博客文章和审核其他成员的帖子。

>[!NOTE]
>
>遗憾的是，使用的术语有时存在重叠。 这种情况可能发生在以下位置：
>
>* **发布/取消发布**
   >  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
   >  这两个术语与发布/取消发布同义。
>
>* **复制**
   >  这些是技术术语，用于指示数据（如页面内容、文件、代码、用户注释）从一个环境移动到另一个环境；即发布或反向复制用户注释时。
>


#### Dispatcher {#dispatcher}

为了优化网站访客体验，**[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 实施了负载平衡和缓存。**
