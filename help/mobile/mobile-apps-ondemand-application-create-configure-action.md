---
title: 应用程序创建和配置操作
seo-title: 应用程序创建和配置操作
description: 创建应用程序通常是创建和管理AEM Mobile On-Demand内容的第一步。 请阅读本页以了解更多信息。
seo-description: 创建应用程序通常是创建和管理AEM Mobile On-Demand内容的第一步。 请阅读本页以了解更多信息。
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# 应用程序创建和配置操作{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

## 创建按需应用程序{#creating-an-on-demand-application}

创建应用程序通常是创建和管理AEM Mobile On-Demand内容的第一步，通常在AEM管理员级别执行。 它表示内容外壳，可在移动设备上查看，可随时显示作者创建的内容，如文章、图像、收藏集等。

您可以在功能板或AEM Mobile控制中心查看应用程序的详细信息。

>[!NOTE]
>
>功能板是一系列有用的图块，用于概述应用程序的内容、元数据和AEM Mobile按需连接状态。
>
>有关详细信息，请参阅[AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

**要创建按需应用程序，请执行以下操作：**

1. 从侧边栏中选择&#x200B;**Mobile**。
1. 从导航中选择&#x200B;**Apps**。
1. 单击&#x200B;**创建**&#x200B;并从下拉列表中选择&#x200B;**应用程序**。
1. 选择移动设备应用程序模板，然后单击&#x200B;**下一步**。
1. 输入应用程序属性，如&#x200B;**标题**、**名称**、**描述**。
1. 单击&#x200B;**下一步**。
1. 如果已知，请输入云配置详细信息，否则，单击&#x200B;**创建**。
1. 单击&#x200B;**完成**&#x200B;以在目录中查看新的AEM Mobile应用程序。

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>此过程允许您在AEM中创建应用程序实例。

## 使用应用程序模板{#using-app-templates}

应用程序模板提供了一种轻松的方法来利用开发人员创建的现有设计，这些设计用于在AEM中创建新应用程序。

什么是应用程序模板？ 可将其视为页面模板和组件的集合，这些模板和组件代表应用程序的基线或基础。
根据其他应用程序的模板创建新应用程序时，您将获得一个具有起点代表的应用程序，该应用程序是从中创建该应用程序的。

您必须拥有现有的移动设备应用程序模板（或安装了应用程序模板的应用程序）才能使用此功能。

### 下一步{#the-next-step}

从应用程序功能板创建按需应用程序后，下一步是将您的应用程序关联到云配置。

有关更多详细信息，请参阅[将您的应用程序关联到云配置](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)。

### 提前{#getting-ahead}

熟悉如何创建按需应用程序并将该应用程序关联到云配置后，请参阅[内容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

**内容管** 理操作涉及创建和管理以下内容：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理横幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理收藏集](/help/mobile/mobile-on-demand-managing-collections.md)
* [上传共享资源](/help/mobile/mobile-on-demand-shared-resources.md)
* [发布取消发布内容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

要了解管理员和开发人员的角色和职责，请参阅以下资源：

* [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)
* [管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
