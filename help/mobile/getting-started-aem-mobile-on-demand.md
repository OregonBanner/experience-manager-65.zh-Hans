---
title: Adobe Experience Manager Mobile On-Demand
description: 要开始新的Adobe Experience Manager (AEM)移动设备应用程序体验，需要先凝聚多个角色，然后才能编辑内容。 关注此页面以开始使用AEM Mobile On-Demand Services。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>对于需要基于单页应用程序框架的客户端渲染（例如React）的项目，Adobe建议使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>如果您没有使用Adobe Experience Manager (AEM)作为内容管理源，请参阅 [AEM Mobile On-demand Services帮助](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM提供了多种工具，使您能够将内容集成到移动应用程序中。

下图说明了AEM Mobile和On-Demand Services的各个组件如何组合在一起，向移动设备应用程序交付内容。

可以将AEM Preflight应用程序视为一个测试环境，用于在发布之前预览应用程序和内容；而AEM Mobile应用程序则是为分发构建的最终应用程序。

>[!NOTE]
>
>要深入了解预检应用程序，请参阅 [使用AEM预检应用程序](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) 在AEM Mobile On-demand Services帮助中。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上图中，对于AEM Mobile On-demand Services的典型部署方案，不需要AEM发布实例。

## 启动新的移动设备应用程序 {#starting-a-new-mobile-app}

AEM Mobile只是构成整个AEM平台的支柱之一。

在开始新的AEM Mobile应用程序体验之前，需要多个角色相互融合，然后才能编辑内容。 以下角色为创建AEM Mobile应用程序提供了起点：

* **管理员**
* **开发人员**
* **创作**

>[!NOTE]
>
>在使用AEM Mobile并按照本快速入门指南中的步骤操作之前，用户应该熟悉AEM。 了解AEM的基础知识 [此处](/help/sites-deploying/deploy.md).

### 了解AEM Mobile应用程序功能板 {#understanding-the-aem-mobile-application-dashboard}

在了解角色和职责之前，用户应充分了解 **AEM Mobile控制中心** 或 **应用程序功能板**. 单击 [此处](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 以深入了解。

### AEM 管理员 {#aem-administrator}

An ***AEM管理员*** 负责将应用程序添加到AEM Mobile目录，方法是使用创建向导创建应用程序，或导入现有应用程序。 使用AEM Mobile创建应用程序的AEM管理员 *创建向导* 通常从Adobe的开箱即用参考示例或（通常）由创建的自定义应用程序模板中选择所需的应用程序模板之一 *AEM开发人员。*

使用AEM Mobile On-demand Services创建应用程序时，AEM管理员负责以下任务：

* [设置AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [配置用户和用户组](/help/mobile/aem-mobile-configure-users.md)
* [使用Preflight预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理内容服务](/help/mobile/developing-content-services.md)

要开始使用管理员的角色和职责，请参阅 [管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM开发人员 {#aem-developer}

An **AEM开发人员** 扩展和创建自定义Web模板和组件，以使*AEM创作*创建精美而引人入胜的移动体验。 这些模板和组件不仅针对移动应用程序世界进行了优化，而且还与设备通信，并与全渠道服务端点的AEM服务器（任何远程服务器）通信。 AEM内置内容编辑器由使用 *AEM作者* 在应用程序中创建丰富的相关体验，包括与Adobe Experience Cloud其余部分的集成。

AEM开发人员在使用AEM Mobile On-demand Services创建应用程序时负责以下任务：

* [应用程序模板和组件](/help/mobile/app-templates-and-components1.md)
* [通过内容同步移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [内容属性和导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [开发AEM Mobile内容服务](/help/mobile/developing-content-services.md)

要开始使用开发人员的角色和职责，请参阅 [为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM开发人员的* 角色不是以开发模板和组件开始和结束。 An *AEM开发人员* 可以创建全新的应用程序，而不是简单地扩展现成的引用实施示例。

## AEM Author {#aem-author}

An ***AEM创作* (或 *营销人员*)**使用自定义开发或现成的模板和组件来添加和编辑页面、拖放组件以及从DAM添加所有类型的媒体，包括图像、视频和文本片段（内容片段）。 随后，使用AEM内置内容编辑器的是 *AEM作者* 在应用程序中创建丰富的相关体验，包括与Adobe Experience Cloud其余部分的集成。

使用AEM Mobile On-demand Services创建应用程序时，AEM作者必须了解以下主题：

* [AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [应用程序创建和配置操作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [云配置](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理内容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [内容服务概述](/help/mobile/develop-content-as-a-service.md)

要开始使用作者的角色和职责，请参阅 [为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM作者还负责设置权利、创建卡和布局以及发送推送通知。 此外，有关创作内容的方法、管理文章和收藏集，以及在AEM Mobile中创建横幅、卡片和布局的更多信息，请参阅 [AEM Mobile On-Demand门户](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
