---
title: Content Services
seo-title: Content Services
description: 'null'
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>“内容服务”功能仅用于预览目的。
>
>随着6.3 GA Service Pack 1的发布，它可能会发生变化。

AEM Mobile Content services是一项轻量级功能，用于请求由AEM管理的内容。 这为所有应用程序开发人员提供了一种高性能的方式来检索内容，而无需深入了解AEM的内容存储库(JCR)和Web框架(Sling)。 它允许请求应用程序与内容存储库分离。

Content services引入了几个新的AEM构造，使开发人员能够访问AEM管理的内容，而无需了解该内容的存储库结构。

为了保持灵活性，并通过在AEM管理的内容与使用该内容的移动应用程序之间提供一个抽象层，从而支持未来扩展，这些构造是必需的。 这允许AEM Content services在本机应用程序的内容要求与AEM内容存储库之间充当抽象层。

内容服务可以将内容作为资产、打包的HTML(HTML/CSS/JS)或渠道无关内容提供。

>[!CAUTION]
>
>**前提条件:**
>
>在开始使用Content Services之前，请确保启用Content services标记。 要在应用程序中创建和管理模型，您需要在配置浏览器中启用数据模型。
>
>有关详 **[细信息，请参阅管](/help/mobile/developing-content-services.md)**理内容服务。

![chlimage_1-143](assets/chlimage_1-143.png)

在配置浏览器中设置Content services标志并启用数据模型后，请参阅以下资源，以开始使用AEM Mobile Content Services，熟悉Content services概念，如模型管理、实体管理，然后是AEM Mobile Content services的内容交付／呈现。

* 存储库中的模型
* 渲染和交付

