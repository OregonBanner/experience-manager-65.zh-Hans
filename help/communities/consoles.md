---
title: 社区控制台
description: 从全局导航面板了解“创作”环境中可用的Adobe Experience Manager社区控制台。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# 社区控制台 {#communities-consoles}

AEM Communities的控制台可在全局导航面板的创作环境中使用，用于访问管理任务，例如：

* [创建社区站点](sites-console.md)
* 正在添加 [组](groups.md) 嵌套在站点内
* 管理 [社区站点模板](sites.md)
* 管理 [社区成员](members.md)
* [正在审核](moderate-ugc.md) 用户生成内容(UGC)
* 创建 [自定义徽章](badges.md)
* 配置 [UGC的默认存储](srp-config.md)

时间 [UGC存储](working-with-srp.md) 配置为由创作环境和发布环境共享的公用存储， [审核控制台](moderation.md)在创作和发布环境中均可用，在UGC的单独实例上运行。

在创作环境中，以管理员权限登录后， `Communities` 控制台可从“导航”和“工具”控制台中使用。

>[!NOTE]
>
>在“发布”环境中， [社区站点](sites-console.md) 显示 `Administration` 登录成员具有相应权限时的菜单项。

## 全局导航面板 {#global-navigation-panel}

选择 `Adobe Experience Manager` 图标，以便您可以打开全局导航面板并访问两个图标：

* [导航控制台](#navigation-console)
* [工具控制台](tools.md)

## 导航控制台 {#navigation-console}

要访问各种Communities控制台，请从全局导航中选择 **导航，社区**.

![社区](assets/communities.png)

* [Sites](sites-console.md)

  站点控制台可在创作环境中访问，用于创建和管理社区站点及其 [组](groups.md).

* [审核](moderation.md)

  “审阅”控制台用于批量审阅UGC和创作环境。 在“发布”环境中，分配给以下角色的社区成员也可以访问类似的批量审核控制台： [社区审查方](users.md#publishenvironmentusersandgroups) 用于一个或多个社区站点。

* [成员、组](members.md)

  “成员”和“组”控制台用于从创作环境管理发布环境中存在的社区成员和成员组。

* [报表](reports.md)

  在“报表”控制台中，当社区站点满足以下条件时，可能会生成有关工作总揽、页面查看和已发布内容(UGC)的报表 [已启用Adobe Analytics](sites-console.md#analytics). 该控制台仅在创作环境中可用。

## “工具”控制台 {#tools-console}

要访问 [Communities工具](tools.md) （以前称为管理控制台），从全局导航： **[!UICONTROL 工具]** > **[!UICONTROL Communities]**
