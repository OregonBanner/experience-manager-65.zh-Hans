---
title: Communities控制台
seo-title: Communities Consoles
description: 社区控制台解释
seo-description: Community Consoles explained
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
source-wordcount: '340'
ht-degree: 2%

---

# Communities控制台 {#communities-consoles}

AEM Communities控制台可在创作环境中从全局导航面板中使用，通过该控制台可访问管理任务，例如：

* [创建社区站点](sites-console.md)
* 添加 [组](groups.md) 嵌套在站点内
* 管理 [社区站点模板](sites.md)
* 管理 [社区成员](members.md)
* [正在审核](moderate-ugc.md) 用户生成内容(UGC)
* 创建 [自定义徽章](badges.md)
* 配置 [UGC的默认存储](srp-config.md)

时间 [UGC存储](working-with-srp.md) 配置为由创作环境和发布环境共享的公用存储， [审核控制台](moderation.md)在创作和发布环境中均可用，可在UGC的单独实例上运行。

在创作环境中，以管理员权限登录后， `Communities` 控制台可从“导航”和“工具”控制台中使用。

>[!NOTE]
>
>在发布环境中， [社区站点](sites-console.md) 将显示 `Administration` 菜单项。

## 全局导航面板 {#global-navigation-panel}

选择 `Adobe Experience Manager` 图标打开全局导航面板并访问两个图标：

* [导航控制台](#navigation-console)
* [工具控制台](tools.md)

## 导航控制台 {#navigation-console}

要访问各种Communities控制台，请从全局导航中选择 **导航，社区**.

![社区](assets/communities.png)

* [Sites](sites-console.md)

   站点控制台可在创作环境中访问，以创建和管理社区站点及其 [组](groups.md).

* [审核](moderation.md)

   “审阅”控制台用于批量审阅UGC和创作环境。 在发布环境中，分配了角色的社区成员可以访问类似的批量审核控制台。 [社区审查方](users.md#publishenvironmentusersandgroups) 用于一个或多个社区站点。

* [成员、组](members.md)

   “成员”和“组”控制台用于从创作环境管理发布环境中存在的社区成员和成员组。

* [报告](reports.md)

   当社区网站具有以下URL时，“报表”控制台可以生成有关分配、页面查看和已发布内容(UGC)的报表： [已启用Adobe Analytics](sites-console.md#analytics). 控制台仅在创作环境中可用。

* [资源](resources.md)

   资源控制台位于 [启用管理器](enablement.md#communitymanagers) 创建、管理和分配资源给成员 [启用社区站点](overview.md#enablement-community). 控制台仅在创作环境中可用。

## “工具”控制台 {#tools-console}

要访问 [Communities工具](tools.md) （前身为administration console），从全局导航中： **[!UICONTROL 工具]** > **[!UICONTROL Communities]**
