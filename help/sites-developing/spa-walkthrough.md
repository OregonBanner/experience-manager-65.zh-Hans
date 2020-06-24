---
title: SPA简介和演练
seo-title: SPA简介和演练
description: 本文介绍SPA的概念，并逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础AEM SPA编辑器的关系。
seo-description: 本文介绍SPA的概念，并逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础AEM SPA编辑器的关系。
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 307a1db2e5bbb72d730c89ba14f5ce02b96c108d
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 0%

---


# SPA简介和演练{#spa-introduction-and-walkthrough}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，作者希望在AEM中为使用此类框架构建的站点无缝编辑内容。

SPA编辑器为在AEM中支持SPA提供了全面的解决方案。 本文将逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础AEM SPA编辑器的关系。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 简介 {#introduction}

### 文章目标 {#article-objective}

本文介绍了SPA的基本概念，然后使用一个简单的SPA应用程序演示基本内容编辑，带领读者演练SPA编辑器。 然后深入到页面的构建以及SPA应用程序与AEM SPA编辑器的关联和交互。

此简介和演练的目的是向AEM开发人员演示SPA的相关性、它们的一般工作方式、AEM SPA编辑器如何处理SPA以及它与标准AEM应用程序有何不同。

演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：

* [AEM 6.4版（带Service Pack 2或更高版本）
   ](/help/release-notes/sp-release-notes.md)
* [在GitHub上安装We.Retail日志应用程序示例。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>此文档仅将 [We.Retail日志应用程序用](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应利 [用AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，该原型支持使用React或Angular的SPA项目并利用SPA SDK。

### 什么是SPA? {#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，它在客户端呈现，主要由Javascript驱动，它依赖Ajax调用加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互情况按需异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速的体验，更像原生的App体验。

AEM SPA编辑器允许前端开发人员创建可集成到AEM站点的SPA，使内容作者能够像编辑任何其他AEM内容一样轻松地编辑SPA内容。

### 为什么要做SPA? {#why-a-spa}

SPA更快、更流畅，更像本机应用程序，它不仅对网页的访客非常有吸引力，而且对营销人员和开发人员也极具吸引力，因为SPA的工作方式。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**访客数**

* 访客在与内容交互时需要类似于原生的体验。
* 有明确的数据表明，页面越快，转换的可能性就越大。

**营销人员**

* 营销人员希望优惠丰富的类似于原生的体验，以吸引访客充分参与内容。
* 个性化可以让这些体验更加引人注目。

**开发人员**

* 开发人员希望将内容和演示之间的疑虑清晰地分开。
* 清洁分离使系统更具扩展性，并允许独立的前端开发。

### SPA如何工作？ {#how-does-a-spa-work}

SPA的主要思想是减少对服务器的调用和依赖，以最大限度地减少由服务器调用引起的延迟，使SPA接近本机应用程序的响应。

在传统的连续网页中，只加载立即页面所需的数据。 这意味着当访客移到其他页面时，将调用服务器获取其他资源。 当访客与页面上的元素交互时，可能需要进行其他调用。 由于页面必须跟上访客的请求，因此这些多次调用可能会产生延迟或延迟。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

要获得更流畅的体验，即接近访客从移动本机应用程序中期望的体验，SPA在第一次加载时加载访客的所有必要数据。 尽管这一过程一开始可能需要稍长一些，但随后它就不再需要额外的服务器调用。

通过在客户端进行渲染，页面元素可以更快地反应，并且访客可以立即与页面进行交互。 可能需要的任何其他数据都将异步调用，以最大化页面速度。

>[!NOTE]
>
>有关SPA在AEM中的工作方式的技术详细信息，请参 [阅AEM中SPA快速入门文章](/help/sites-developing/spa-getting-started-react.md)。
>
>要详细了解SPA编辑器的设计、架构和技术工作流程，请参阅文章SPA [编辑器概述](/help/sites-developing/spa-overview.md)。

## SPA内容编辑体验 {#content-editing-experience-with-spa}

当构建SPA以利用AEM SPA编辑器时，内容作者注意到在编辑和创建内容时没有区别。 通用AEM功能可用，无需更改作者的工作流。

>[!NOTE]
>
>演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：
>
>* [AEM 6.4版（带Service Pack 2）](/help/release-notes/sp-release-notes.md)
>* [在GitHub上安装We.Retail日志应用程序示例。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>



1. 在AEM中编辑We.Retail日志应用程序。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 选择一个标题组件，然后注意工具栏的显示方式与任何其他组件的显示方式相同。 选择&#x200B;**编辑**。

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. 在AEM中按正常方式编辑内容，并注意这些更改会被保留。

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >有关就 [地文本编辑器](spa-overview.md#requirements-limitations) 和SPA的更多信息，请参阅SPA编辑器概述。

1. 使用资产浏览器将新图像拖放到图像组件中。

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. 更改将被保留。

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

与任何非SPA应用程序一样，支持其他创作工具，如在页面上拖放其他组件、重新排列组件以及修改布局。

>[!NOTE]
>
>SPA编辑器不修改应用程序的DOM。 SPA本身负责DOM。
>
>要了解其工作方式，请继续阅读本文SPA应 [用程序和AEM SPA编辑器的下一节](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)。

## SPA应用程序和AEM SPA编辑器 {#spa-apps-and-the-aem-spa-editor}

了解SPA对最终用户的作用，然后检查SPA页面有助于更好地了解SAP应用程序如何与AEM中的SPA编辑器配合使用。

### 使用SPA应用程序 {#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器的“页面信息”菜单中的“ **视图为已发布****”选项加** 载We.Retail日志应用程序。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   请注意页面结构，包括到子页面、天气构件和文章的导航。

1. 使用菜单导航到子页面，无需刷新即可立即加载页面。

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. 在导航子页面时，打开浏览器的内置开发人员工具并监视网络活动。

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   应用程序中的页面之间移动时，流量非常小。 不会重新加载页面，只请求新图像。

   SPA完全在客户端管理内容和路由。

因此，如果在子页面之间导航时页面未重新加载，页面如何加载？

下一节加 [载SPA应用程序](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)，深入探讨加载SPA的机制以及如何同步和异步加载内容。

### 加载SPA应用程序 {#loading-an-spa-application}

1. 如果尚未加载，请在发布服务器上加载We.Retail日志应用程序，或从页面编辑器的“页面信息” **菜单中使用** “ **视图为已发布** ”选项。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. 使用浏览器的内置工具视图页面源。
1. 请注意，源的内容非常有限。

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   页面的正文中没有任何内容。 它主要由样式表和对React脚本的调用组成 `we-retail-journal-react.js`。

   此React脚本是此应用程序的主要驱动程序，负责渲染所有内容。

1. 使用浏览器的内置工具检查页面。 查看完全加载的DOM的内容。

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. 切换到检查器中的“网络”选项卡并重新加载该页。

   忽略图像请求，请注意为页面加载的主要资源包括页面本身、CSS、React Javascript、其依赖项以及页面的JSON数据。

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. 在新选 `react.model.json` 项卡中加载。

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA编辑器利 [用AEM Content](/help/assets/content-fragments/content-fragments.md) Services将页面的整个内容作为JSON模型提供。

   通过实现特定界面，Sling Models为SPA提供必要的信息。 JSON投放的会向下委派给每个组件（从页面、段落、组件等）。

   每个组件都选择它公开的内容和呈现方式（在服务器端使用HTL，在客户端使用React）。 当然，本文侧重于使用React进行客户端渲染。

1. 该模型还可以将页面分组在一起，以便它们同步加载，从而减少需要重新加载的页面数。

   在We.Retail日志的示例中，将同 `home`步加 `blog`载、 `aboutus` 和页面，因为访客通常访问所有这些页面。 但是， `weather` 页面是异步加载的，因为访客不太可能访问它。

   此行为不是强制的，并且完全可以定义。

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. 要视图行为上的这种差异，请重新加载页面并清除检查器的网络活动。 导航到页面菜单中的博客和关于我们的页面，并查看没有报告网络活动。

   导航到天气页面，并查看异 `weather.model.json` 步调用天气。

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### 与SPA编辑器交互 {#interaction-with-the-spa-editor}

使用示例We.Retail日志应用程序，您可以清楚地了解应用程序的行为和发布时的加载方式，为JSON内容投放提供内容服务，并异步加载资源。

此外，对于内容作者而言，使用SPA编辑器创建内容在AEM中是无缝的。

在下一节中，我们将探索允许SPA编辑器将SPA中的组件与AEM组件关联并实现无缝编辑体验的合同。

1. 在编辑器中加载We.Retail日志应用程序并切换到 **预览模式** 。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. 使用浏览器内置的开发人员工具检查页面内容。 使用选择工具，在页面上选择一个可编辑的组件，然后视图元素详细信息。

   请注意，该组件具有新的数据属性 `data-cq-data-path`。

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   例如

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将其识别为SPA中的可编辑组件所需的唯一标记属性。 根据此属性，SPA编辑器将确定与组件关联的可编辑配置，以便正确的框架、工具栏等。 已加载。

   还为标记占位符和资产拖放功能添加了一些特定类名称。

   >[!NOTE]
   >
   >这是对AEM中服务器端呈现页面行为的更改，在AEM中，每个可编辑组件 `cq` 都插入了一个元素。
   >
   >
   >SPA中的这种方法消除了注入自定义元素的需要，只依赖附加的数据属性，使得前端开发者的标记更简单。

## 后续步骤 {#next-steps}

现在，您已了解AEM中的SPA编辑体验以及SPA与SPA编辑器的关系，进一步了解SPA的构建方式。

* [AEM中的SPA入门](/help/sites-developing/spa-getting-started-react.md) ，可显示如何构建基本SPA以与AEM中的SPA编辑器配合使用
* [SPA编辑器概述](/help/sites-developing/spa-overview.md) 深入介绍AEM与SPA之间的通信模型。
* [为AEM开发SPA](/help/sites-developing/spa-architecture.md) ，介绍如何吸引前端开发人员来为AEM开发SPA，以及SPA如何与AEM架构交互。
