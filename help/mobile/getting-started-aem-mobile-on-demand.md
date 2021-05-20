---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 要启动新的AEM Mobile应用程序体验，需要先协调各个角色，然后才能为内容编辑做好准备。 请阅读本页，以开始使用AEM Mobile On-Demand Services。
seo-description: 要启动新的AEM Mobile应用程序体验，需要先协调各个角色，然后才能为内容编辑做好准备。 请阅读本页，以开始使用AEM Mobile On-Demand Services。
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

>[!NOTE]
>
>如果您没有将AEM用作内容管理源，请参阅[AEM Mobile On-demand Services帮助](https://helpx.adobe.com/digital-publishing-solution/topics.html)。

AEM提供了多种工具，使您能够将内容集成到移动设备应用程序中。

下图说明了AEM Mobile和On-Demand Services的各个组件如何结合使用来向移动设备应用程序交付内容。

AEM Preflight应用程序可视为在发布之前预览应用程序和内容的测试环境；而AEM Mobile应用程序是为分发而构建的最终应用程序。

>[!NOTE]
>
>要深入了解Preflight应用程序，请参阅AEM Mobile On-demand Services帮助中的[使用AEM Preflight应用程序](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html)。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上图中，将典型部署方案部署到AEM Mobile On-demand Services时不需要AEM发布实例。

## 启动新的移动设备应用程序{#starting-a-new-mobile-app}

AEM Mobile只是构成完整AEM平台的一个支柱。

要启动新的AEM Mobile应用程序体验，需要先协调各个角色，然后才能为内容编辑做好准备。 以下角色为创建新的AEM Mobile应用程序提供了一个起点：

* **管理员**
* **开发人员**
* **创作**

>[!NOTE]
>
>在使用AEM Mobile并执行本快速入门指南中的步骤之前，用户应该熟悉AEM。 在此处](/help/sites-deploying/deploy.md)了解AEM的基础知识。[

### 了解AEM Mobile应用程序功能板{#understanding-the-aem-mobile-application-dashboard}

在了解角色和职责之前，用户应该对&#x200B;**AEM Mobile控制中心**&#x200B;或&#x200B;**应用程序功能板**&#x200B;有足够的了解。 单击[此处](/help/mobile/mobile-apps-ondemand-application-dashboard.md)可深入了解。

### AEM 管理员 {#aem-administrator}

***AEM管理员***&#x200B;负责通过使用创建向导创建新应用程序或导入现有应用程序，将新应用程序添加到AEM Mobile目录。 使用AEM Mobile的&#x200B;*创建向导*&#x200B;创建新应用程序的AEM管理员，通常会从我们的现成引用示例中选择一个所需的应用程序模板，或者（在大多数情况下）从AEM开发人员创建的自定义应用程序模板中选择一个所需的应用程序模板。**

使用AEM创建应用程序时， AEM Mobile On-demand Services管理员负责执行以下任务：

* [设置AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [配置用户和用户组](/help/mobile/aem-mobile-configure-users.md)
* [使用预检预览](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理内容服务](/help/mobile/developing-content-services.md)

要开始使用管理员的角色和职责，请参阅[管理内容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)。

## AEM开发人员{#aem-developer}

**AEM开发人员**&#x200B;扩展并创建自定义Web模板和组件，以使*AEM作者*能够创建美观且引人入胜的移动体验。 这些模板和组件不仅针对移动设备应用程序领域进行了优化；但是，要与设备和AEM服务器（任何远程服务器）通信到全渠道服务端点。 *AEM作者*&#x200B;使用AEM内置内容编辑器在应用程序中创建丰富且相关的体验，包括与Adobe Marketing Cloud其他部分的集成。

使用AEM创建应用程序时， AEM Mobile On-demand Services开发人员负责执行以下任务：

* [应用程序模板和组件](/help/mobile/app-templates-and-components1.md)
* [具有内容同步的移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [内容属性和导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [开发AEM Mobile内容服务](/help/mobile/developing-content-services.md)

要开始使用开发人员的角色和职责，请参阅[为AEM Mobile On-demand Services开发AEM内容](/help/mobile/aem-mobile-on-demand.md)。

>[!NOTE]
>
>*AEM开发人员的*&#x200B;角色不会从模板和组件的开发开始和结束。 *AEM开发人员*&#x200B;可以创建一个全新的应用程序，而不是简单地扩展现成的引用实施示例。

## AEM Author {#aem-author}

***AEM作者*（或&#x200B;*营销人员*）**使用自定义开发或现成可用的模板和组件来添加和编辑页面，拖放组件以及添加DAM中所有类型的媒体，包括图像、视频和文本片段（内容片段）。 然后，*AEM作者*使用AEM内置内容编辑器在应用程序中创建丰富且相关的体验，包括与Adobe Marketing Cloud其他部分的集成。

使用AEM创建应用程序时，AEM Mobile On-demand Services作者必须了解以下主题：

* [AEM Mobile应用程序功能板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [应用程序创建和配置操作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [云配置](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理内容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [内容服务概述](/help/mobile/develop-content-as-a-service.md)

要开始了解作者的角色和职责，请参阅[为AEM Mobile On-demand Services应用程序创作AEM内容](/help/mobile/mobile-apps-ondemand.md)。

>[!NOTE]
>
>AEM作者还负责设置授权、创建信息卡和布局以及发送推送通知。 此外，还提供了有关内容创作方法的更多信息；管理文章和收藏；在AEM Mobile中创建横幅、卡片和布局，请参阅[AEM Mobile按需门户](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)。
