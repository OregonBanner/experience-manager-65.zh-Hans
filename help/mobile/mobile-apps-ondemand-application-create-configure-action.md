---
title: 应用程序创建和配置操作
seo-title: Application Create and Configuration Actions
description: 创建应用程序通常是创建和管理AEM Mobile On-Demand内容的第一步。 关注此页面以了解更多信息。
seo-description: Creating an app is often the first step towards creating and managing AEM Mobile On-Demand content. Follow this page to learn more.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 应用程序创建和配置操作{#application-create-and-configuration-actions}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

## 创建按需应用程序 {#creating-an-on-demand-application}

创建应用程序通常是创建和管理AEM Mobile On-Demand内容的第一步，通常在AEM管理员级别执行。 它表示可在移动设备上查看的内容外壳，可随时显示作者创建的内容，例如文章、图像、收藏集等。

您可以在功能板或AEM Mobile控制中心中查看应用程序的详细信息。

>[!NOTE]
>
>“功能板”是一系列有用的拼贴，可概述应用程序的内容、元数据和AEM Mobile On-Demand连接状态。
>
>参见 [AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 了解详细信息。

**要创建按需应用程序，请执行以下操作：**

1. 选择 **移动设备** 从侧边栏上删除。
1. 选择 **应用程序** 从导航中。
1. 单击 **创建** 并选择 **应用程序** 从下拉菜单中。
1. 选择移动设备应用程序模板并单击 **下一个**.
1. 输入应用程序属性，例如 **标题**， **名称**， **描述**.
1. 单击&#x200B;**下一步**。
1. 如果已知，请输入云配置详细信息，否则请单击 **创建**.
1. 单击 **完成** 以在目录中查看新的AEM Mobile应用程序。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>此过程允许您在AEM中创建应用程序实例。

## 使用应用程序模板 {#using-app-templates}

应用程序模板提供了一种简单的方式来利用开发人员创建的现有设计，这些设计用于在AEM中创建新的应用程序。

什么是应用程序模板？ 可将其视为页面模板和组件的集合，这些模板和组件表示应用程序的基线或基础。
在基于其他应用程序的模板创建新应用程序时，您将获得一个应用程序，其起点代表从中创建该应用程序的应用程序。

您必须拥有现有的移动设备应用程序模板（或已安装的应用程序具有应用程序模板），才能使用此功能。

### 下一步 {#the-next-step}

从应用程序仪表板创建按需应用程序后，下一步是将您的应用程序与云配置相关联。

参见 [将应用程序与云配置关联](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 了解更多详细信息。

### 快速入门 {#getting-ahead}

在您熟悉了创建按需应用程序并将应用程序与云配置关联后，请参阅 [内容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**内容管理操作** 涉及以下内容的创建和管理：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
