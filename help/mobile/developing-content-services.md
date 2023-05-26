---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>仅出于预览目的，记录了内容服务功能。
>
>它可能会随6.3 GA Service Pack 1的发布而更改。

AEM Mobile Content Services是一项轻量级功能，用于请求由AEM管理的内容。 这为所有应用程序开发人员提供了一种高性能的方法来检索内容，而无需深入了解AEM content repository (JCR)和Web framework (Sling)。 它允许请求应用程序与内容存储库分离。

Content Services引入了多种新的AEM结构，使开发人员能够访问AEM托管内容，而无需了解该内容的存储库结构。

这些结构对于保持灵活性以及支持未来扩展是必需的，方法是在AEM托管内容和使用内容的移动应用程序之间提供一个抽象层。 这使得AEM Content Services可以充当本机应用程序的内容要求与AEM内容存储库之间的抽象层。

Content Services可以将内容作为资产、打包HTML(HTML/CSS/JS)或独立于渠道的内容提供。

>[!CAUTION]
>
>**前提条件:**
>
>在开始使用Content Services之前，请确保启用Content Services标记。 要在应用程序中启用模型的创建和管理，您需要在配置浏览器中启用数据模型。
>
>参见 **[管理内容服务](/help/mobile/developing-content-services.md)** 和 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。

![chlimage_1-143](assets/chlimage_1-143.png)

在配置浏览器中设置Content Services标志并启用数据模型后，请参阅以下资源以开始使用AEM Mobile Content Services，熟悉Content Services概念（例如模型管理、实体管理），然后熟悉AEM Mobile Content Services的内容交付/渲染。

* 存储库中的模型
* 呈现和交付
