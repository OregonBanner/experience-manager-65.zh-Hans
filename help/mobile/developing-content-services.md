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
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 2%

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Content Services功能仅记录为预览之用。
>
>随着6.3 GA Service Pack 1的发布，它可能会发生变化。

AEM Mobile内容服务是一项轻量级功能，用于请求由AEM管理的内容。 这为所有应用程序开发人员提供了一种高性能方式来检索内容，而无需深入了解AEM内容存储库(JCR)和Web框架(Sling)。 它允许请求的应用程序与内容存储库分离。

Content Services引入了几个新的AEM构造，使开发人员能够访问AEM托管内容，而无需了解该内容的存储库结构。

通过在AEM托管内容和使用内容的移动应用程序之间提供抽象层，这些结构是保持灵活性和实现未来扩展所必需的。 这允许AEM Content Services在本机应用程序的内容要求和AEM内容存储库之间充当抽象层。

内容服务可以将内容作为资产、打包的HTML(HTML/CSS/JS)或独立于渠道的内容提供。

>[!CAUTION]
>
>**前提条件:**
>
>开始使用Content Services之前，请确保启用Content Services标志。 要在应用程序中启用模型的创建和管理，您需要在配置浏览器中启用数据模型。
>
>有关 **[详细信息](/help/mobile/developing-content-services.md)** ，请参 [阅管理内](/help/sites-administering/configurations.md) 容服务和配置浏览器文档。

![chlimage_1-143](assets/chlimage_1-143.png)

在配置浏览器中设置内容服务标志并启用数据模型后，请参阅以下资源，开始使用AEM Mobile内容服务，熟悉内容服务概念，如模型管理、实体管理，然后是AEM Mobile内容服务的内容投放/渲染。

* 存储库中的模型
* 渲染和投放
