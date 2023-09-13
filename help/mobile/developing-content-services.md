---
title: Content Services
description: Content Services
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>仅出于预览目的，介绍了内容服务功能。
>
>它可能会随6.3 GA Service Pack 1的发布而更改。

AEM Mobile Content Services是一项轻量级功能，用于请求由AEM管理的内容。 这为所有应用程序开发人员提供了一种高性能的方法，无需深入了解AEM内容存储库(JCR)和Web框架(Sling)即可检索内容。 它允许请求应用程序与内容存储库分离。

Content Services引入了几个新的AEM结构，这些结构使开发人员能够访问AEM管理的内容，而无需了解该内容的存储库结构。

这些构造对于保持灵活性以及通过在AEM管理的内容和使用内容的移动应用程序之间提供一个抽象层来实现未来扩展是必需的。 这使得AEM Content Services可以充当本机应用程序的内容需求与AEM内容存储库之间的抽象层。

Content Services可以将内容作为资源、打包HTML(HTML/CSS/JS)或独立于渠道的内容来交付。

>[!CAUTION]
>
>**前提条件:**
>
>在开始使用Content Services之前，请确保启用Content Services标志。 要在应用程序中启用模型的创建和管理，请在配置浏览器中启用数据模型。
>
>请参阅 **[管理内容服务](/help/mobile/developing-content-services.md)** 和 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。

![chlimage_1-143](assets/chlimage_1-143.png)

设置Content Services标记并在配置浏览器中启用数据模型后，请参阅以下资源以开始使用AEM Mobile Content Services。 熟悉Content Services概念，如模型管理、实体管理，然后是AEM Mobile Content Services的内容交付/渲染。

* 存储库中的模型
* 呈现和交付
