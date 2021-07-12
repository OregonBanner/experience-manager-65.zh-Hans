---
title: 社区控制台
seo-title: 社区控制台
description: 社区控制台说明
seo-description: 社区控制台说明
uuid: 1c5b2600-9059-4b44-9741-f1b627423d3c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 5fa9ee8b-5893-4ae9-a986-bfdbb00f355f
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# 社区控制台 {#communities-consoles}

AEM Communities控制台（位于全局导航面板的创作环境中）提供了对管理任务的访问，例如：

* [创建社区站点](sites-console.md)
* 添加嵌套在站点中的[组](groups.md)
* 管理[社区站点模板](sites.md)
* 管理[社区成员](members.md)
* [](moderate-ugc.md) 审核用户生成的内容(UGC)
* 创建[自定义徽章](badges.md)
* 为UGC](srp-config.md)配置[默认存储

当将[UGC存储](working-with-srp.md)配置为由创作和发布环境共享的公共存储时，[审核控制台](moderation.md)（可从创作和发布环境中使用）会在UGC的单个实例上运行。

在创作环境中，使用管理员权限登录后，导航和工具控制台中提供了`Communities`控制台。

>[!NOTE]
>
>在发布环境中，当已登录的成员具有适当的权限时，[社区站点](sites-console.md)将显示`Administration`菜单项。

## 全局导航面板 {#global-navigation-panel}

选择左上角的`Adobe Experience Manager`图标以打开全局导航面板并访问两个图标：

* [导航控制台](#navigation-console)
* [工具控制台](tools.md)

## 导航控制台 {#navigation-console}

要访问各种“社区”控制台，请从全局导航中选择&#x200B;**导航、Communities**。

![社区](assets/communities.png)

* [站点](sites-console.md)

   站点控制台可在创作环境中访问，以用于创建和管理社区站点及其[组](groups.md)。

* [审核](moderation.md)

   “审核”控制台可用于在创作环境中批量审核UGC。 在发布环境中，可以向为一个或多个社区站点分配了[社区审核者](users.md#publishenvironmentusersandgroups)角色的社区成员访问类似的批量审核控制台。

* [成员、组](members.md)

   “成员”和“组”控制台用于从创作环境管理发布环境中存在的社区成员和成员组。

* [报告](reports.md)

   在“报表”控制台中，当社区站点启用了[Adobe Analytics](sites-console.md#analytics)时，可以生成有关分配、页面查看和发布内容(UGC)的报表。 控制台仅在创作环境中可用。

* [资源](resources.md)

   在“资源”控制台中， [启用管理器](enablement.md#communitymanagers)可创建资源并管理资源，将其分配给[启用社区站点](overview.md#enablement-community)的成员。 控制台仅在创作环境中可用。

## “工具”控制台 {#tools-console}

要从全局导航中访问[Communities Tools](tools.md)（以前称为管理控制台），请执行以下操作：**[!UICONTROL 工具]** > **[!UICONTROL 社区]**
