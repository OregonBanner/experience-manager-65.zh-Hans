---
title: Content Services
seo-title: 内容服务
description: 内容服务
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!CAUTION]
>
>记录的“内容服务”功能仅用于预览目的。
>
>随着6.3 GA Service Pack 1的发布，它可能会发生更改。

AEM Mobile内容服务是一项轻量级的功能，用于请求由AEM管理的内容。 这为所有应用程序开发人员提供了一种高性能的方式来检索内容，而无需深入了解AEM内容存储库(JCR)和Web框架(Sling)。 它允许请求的应用程序与内容存储库分离。

Content Services引入了几种新的AEM结构，使开发人员能够访问AEM托管内容，而无需了解该内容的存储库结构。

这些结构对于保持灵活性和通过在AEM托管内容和使用内容的移动应用程序之间提供抽象层来实现未来扩展是必不可少的。 这允许AEM内容服务在本机应用程序的内容要求和AEM内容存储库之间充当抽象层。

内容服务可以将内容作为资产、打包的HTML(HTML/CSS/JS)或作为与渠道无关的内容进行交付。

>[!CAUTION]
>
>**前提条件:**
>
>在开始使用内容服务之前，请确保启用内容服务标记。 要在应用程序中启用模型的创建和管理，您需要在配置浏览器中启用数据模型。
>
>有关更多信息，请参阅&#x200B;**[管理内容服务](/help/mobile/developing-content-services.md)**&#x200B;和[配置浏览器](/help/sites-administering/configurations.md)文档。

![chlimage_1-143](assets/chlimage_1-143.png)

在配置浏览器中设置内容服务标记并启用数据模型后，请参阅以下资源以开始使用AEM Mobile内容服务，了解内容服务概念，例如模型管理、实体管理，然后是AEM Mobile内容服务的内容交付/渲染。

* 存储库中的模型
* 渲染和交付
