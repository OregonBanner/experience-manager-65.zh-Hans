---
title: AEM Mobile点播
seo-title: AEM Mobile点播
description: 要开始新的AEM Mobile应用体验，需要在准备好进行内容编辑之前保持角色的一致性。 可查看本页以开始使用AEM移动点播服务。
seo-description: 要开始新的AEM Mobile应用体验，需要在准备好进行内容编辑之前保持角色的一致性。 可查看本页以开始使用AEM移动点播服务。
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---


# AEM Mobile点播{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如，React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>如果您未将AEM用作内容管理源，请参阅[AEM Mobile On-demand Services帮助](https://helpx.adobe.com/digital-publishing-solution/topics.html)。

AEM提供了多种工具，使您能够将内容集成到移动应用程序中。

下图说明了AEM Mobile和点播服务的各个组件如何相互配合，将内容交付到移动App。

AEM Preflight应用程序可被视为在发布前预览应用程序和内容的测试环境;而AEM Mobile应用程序是最终为分发而构建的应用程序。

>[!NOTE]
>
>要详细了解Preflight应用程序，请参阅AEM Mobile On-demand Services帮助中的[使用AEM Preflight应用程序](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html)。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上图中，到AEM Mobile On-demand Services的典型部署方案不需要AEM发布实例。

## 启动新移动应用程序{#starting-a-new-mobile-app}

AEM Mobile只是构成整个AEM平台的支柱之一。

要开始新的AEM Mobile应用体验，需要在准备好进行内容编辑之前保持角色的一致性。 以下角色为创建新的AEM Mobile应用程序提供了一个起点：

* **管理员**
* **开发人员**
* **创作**

>[!NOTE]
>
>在与AEM Mobile合作并遵循本入门指南中的步骤之前，用户应熟悉AEM。 在此处了解AEM [的基础知识。](/help/sites-deploying/deploy.md)

### 了解AEM Mobile应用程序仪表板{#understanding-the-aem-mobile-application-dashboard}

在了解角色和责任之前，用户应充分了解&#x200B;**AEM Mobile控制中心**&#x200B;或&#x200B;**应用程序仪表板**。 单击[此处](/help/mobile/mobile-apps-ondemand-application-dashboard.md)可深入了解。

### AEM 管理员 {#aem-administrator}

***AEM administrator***&#x200B;负责通过使用创建向导创建新应用程序或导入现有应用程序将新应用程序添加到AEM Mobile目录。 使用AEM Mobile的&#x200B;*创建向导*&#x200B;创建新应用程序的AEM管理员通常从我们的现成参考范例中选择一个所需的应用程序模板，或者（在大多数情况下）从&#x200B;*AEM开发人员创建的自定义应用程序模板中选择一个所需的应用程序模板。*

AEM管理员在使用AEM Mobile On-demand Services创建应用程序时负责以下任务:

* [建立AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [配置用户和用户组](/help/mobile/aem-mobile-configure-users.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理内容服务](/help/mobile/developing-content-services.md)

要开始管理员的角色和职责，请参阅[管理要使用AEM Mobile On-demand Services的内容](/help/mobile/aem-mobile.md)。

## AEM开发人员{#aem-developer}

**AEM开发人员**&#x200B;扩展并创建自定义Web模板和组件，使*AEM作者*能够创建精美、引人入胜的移动体验。 这些模板和组件不仅针对移动App世界进行了优化；但可以同时与设备和AEM服务器（任何远程服务器）通信到全渠道服务端点。 *AEM作者*&#x200B;使用AEM内置内容编辑器在应用程序中创建丰富且相关的体验，包括与Adobe Marketing Cloud其他地区的集成。

AEM开发人员在使用AEM Mobile On-demand Services创建应用程序时负责以下任务:

* [应用程序模板和组件](/help/mobile/app-templates-and-components1.md)
* [内容同步的移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [内容属性和导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [开发AEM Mobile内容服务](//help/mobile/developing-content-services.md)

要开始了解开发人员的角色和职责，请参阅[为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)。

>[!NOTE]
>
>*AEM开发人员的*&#x200B;角色不开始模板和组件的开发并结束。 *AEM developer*&#x200B;可以创建一个全新的应用程序，而不是简单地扩展现成的参考实现示例。

## AEM Author {#aem-author}

***AEM作者*（或&#x200B;*营销人员*）**使用自定义开发或现成模板及组件添加和编辑页面，拖放组件以及添加DAM中所有类型的媒体，包括图像、视频和文本片段（内容片段）。 *AEM作者*随后使用AEM内置内容编辑器在应用程序中创建丰富且相关的体验，包括与Adobe Marketing Cloud其他地区的集成。

AEM作者在使用AEM Mobile On-demand Services创建应用程序时必须了解以下主题：

* [AEM Mobile应用程序仪表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [应用程序创建和配置操作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [云配置](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理内容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [内容服务概述](/help/mobile/develop-content-as-a-service.md)

要开始使用作者的角色和职责，请参阅[为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)。

>[!NOTE]
>
>AEM作者还负责设置授权、创建卡和布局以及发送推送通知。 此外，有关创作内容的方法的更多信息；管理文章和集合；在AEM Mobile创建横幅、卡和布局，请参阅[AEM Mobile点播门户](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)。

