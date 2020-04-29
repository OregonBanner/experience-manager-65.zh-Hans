---
title: SPA简介和演练
seo-title: SPA简介和演练
description: 本文介绍了SPA的概念，并逐步介绍了如何使用基本的SPA应用程序进行创作，并说明了它与基础AEM SPA编辑器的关系。
seo-description: 本文介绍了SPA的概念，并逐步介绍了如何使用基本的SPA应用程序进行创作，并说明了它与基础AEM SPA编辑器的关系。
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 3d9bcc706a1fa7a15d0ce8729f7b85c4226b394f

---


# SPA简介和演练{#spa-introduction-and-walkthrough}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望在AEM中为使用此框架构建的站点无缝编辑内容。

SPA Editor优惠了一个全面的解决方案，用于在AEM中支持SPA。 本文将逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础AEM SPA Editor的关系。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

## 简介 {#introduction}

### 文章目标 {#article-objective}

本文介绍了SPA的基本概念，然后使用一个简单的SPA应用程序演示基本内容编辑，带领读者浏览SPA编辑器。 然后深入到页面的构建以及SPA应用程序与AEM SPA Editor的关联和交互方式。

此介绍和演练的目标是向AEM开发人员演示SPA的相关性、它们的一般工作方式、AEM SPA编辑器如何处理SPA以及它与标准AEM应用程序有何不同。

该演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：

* [AEM 6.4版（带有Service Pack 2或更高版本）
   ](/help/release-notes/sp-release-notes.md)
* [在此处安装GitHub上提供的示例We.Retail日志应用程序。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

### 什么是SPA? {#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，它在客户端呈现，主要由Javascript驱动，它依赖Ajax调用加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互情况根据需要异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速且感觉更像原生应用程序体验的体验。

AEM SPA Editor允许前端开发人员创建可集成到AEM站点中的SPA，使内容作者能够像编辑任何其他AEM内容一样轻松地编辑SPA内容。

### 为什么选择SPA? {#why-a-spa}

SPA更快、更流畅，更像本机应用程序，因此它不仅对网页的访客非常有吸引力，而且对于营销人员和开发人员也非常有吸引力，因为SPA的工作方式。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**访客数**

* 访客希望在与内容交互时获得类似于本机的体验。
* 有明确的数据显示，页面越快，转化的可能性就越大。

**营销人员**

* 营销人员希望优惠丰富的类似本机的体验，以吸引访客充分参与内容。
* 个性化可让这些体验更加引人注目。

**开发人员**

* 开发人员希望将内容和演示之间的顾虑清晰地分开。
* 清洁分离使系统更具扩展性，并允许独立的前端开发。

### SPA的工作原理 {#how-does-a-spa-work}

SPA的主要思想是减少对服务器的调用和依赖，以最小化由服务器调用引起的延迟，从而使SPA接近本机应用程序的响应性。

在传统的连续网页中，只加载立即页面所需的数据。 这意味着当访客移动到其他页面时，将调用服务器获取其他资源。 当访客与页面上的元素交互时，可能需要进行其他调用。 由于页面必须跟上访客的请求，这些多次调用可能会产生延迟或延迟的感觉。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

为了获得更流畅的体验，SPA将在第一次加载时加载访客所需的所有必要数据，从而接近访客从移动本机应用程序中期望的体验。 尽管这一过程一开始可能需要稍长一些时间，但随后它就不再需要额外的服务器调用。

通过在客户端进行渲染，页面元素的反应会更快，并且访客与页面的交互会立即生效。 可能需要的任何其他数据都将异步调用以最大化页面速度。

>[!NOTE]
>
>有关SPA在AEM中工作方式的技术详细信息，请参阅AEM [中SPA快速入门文章](/help/sites-developing/spa-getting-started-react.md)。
>
>要详细了解SPA编辑器的设计、架构和技术工作流程，请参阅 [SPA编辑器概述文章](/help/sites-developing/spa-overview.md)。

## SPA内容编辑体验 {#content-editing-experience-with-spa}

当构建SPA以利用AEM SPA编辑器时，内容作者在编辑和创建内容时不会发现任何差异。 通用AEM功能可用，无需更改作者的工作流。

>[!NOTE]
>
>该演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：
>
>* [AEM 6.4版（带Service Pack 2）](/help/release-notes/sp-release-notes.md)
>* [在此处安装GitHub上提供的示例We.Retail日志应用程序。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. 在AEM中编辑We.Retail日志应用程序。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 选择一个标题组件，然后注意到工具栏的显示方式与任何其他组件类似。 选择&#x200B;**编辑**。

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. 在AEM中按正常方式编辑内容，并注意更改会持续保留。

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >有关就 [地文本编辑器和SPA的更多信息](spa-overview.md#requirements-limitations) ，请参阅SPA编辑器概述。

1. 使用资产浏览器将新图像拖放到图像组件中。

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. 更改会持续保留。

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

与任何非SPA应用程序一样，支持其他创作工具，如在页面上拖放其他组件、重新排列组件和修改布局。

>[!NOTE]
>
>SPA编辑器不修改应用程序的DOM。 SPA本身负责DOM。
>
>要了解其工作原理，请继续阅读本文 [SPA应用程序和AEM SPA编辑器的下一节](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)。

## SPA应用程序和AEM SPA编辑器 {#spa-apps-and-the-aem-spa-editor}

体验SPA对最终用户的行为，然后检查SPA页面有助于更好地了解SAP应用程序与AEM中SPA编辑器的工作方式。

### 使用SPA应用程序 {#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器中的“页面信息”菜单中的“已发布 **视图”选项** ，加 **** 载We.Retail日志应用程序。

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   请注意页面结构，包括到子页面、天气小部件和文章的导航。

1. 使用菜单导航到子页面，无需刷新即可立即加载页面。

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. 在子页面导航时，打开浏览器的内置开发人员工具并监控网络活动。

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   当您在应用程序中从页面移动到页面时，流量非常少。 不会重新加载页面，只请求新图像。

   SPA完全在客户端管理内容和路由。

因此，如果在子页面之间导航时页面未重新加载，则页面如何加载？

下一节，加 [载SPA应用程序](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)，深入了解加载SPA的机制以及如何同步和异步加载内容。

### 加载SPA应用程序 {#loading-an-spa-application}

1. 如果尚未加载，请在发布服务器上加载We.Retail日志应用程序，或从页面编辑器的“页面信息”菜单中使用“ **视图为已发** 布”选项 **** 。

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

   此React脚本是此应用程序的主要驱动程序，负责呈现所有内容。

1. 使用浏览器的内置工具检查页面。 查看完全加载的DOM内容。

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. 切换到检查器中的“网络”选项卡并重新加载该页面。

   忽略图像请求，请注意为页面加载的主要资源是页面本身、CSS、React Javascript、其依赖关系以及页面的JSON数据。

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. 在新选 `react.model.json` 项卡中加载。

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA Editor利用 [AEM Content Services](/help/assets/content-fragments.md) ，以JSON模型的形式提供页面的整个内容。

   通过实施特定界面，Sling Models为SPA提供必要的信息。 JSON数据的投放会向下委派给每个组件（从页面、段落、组件等）。

   每个组件都选择它公开的内容以及呈现方式（服务器端使用HTL，客户端使用React）。 当然，本文侧重于使用React进行客户端渲染。

1. 该模型还可以将页面组合在一起，以便同步加载页面，从而减少所需的页面重新加载次数。

   在We.Retail日志的示例中，将同 `home`步加载 `blog`、 `aboutus` 和页面，因为访客通常访问所有这些页面。 但是， `weather` 页面是异步加载的，因为访客不太可能访问它。

   此行为不是强制的，并且完全可定义。

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. 要视图此行为差异，请重新加载页面并清除检查器的网络活动。 导航到博客以及页面菜单中关于我们的页面，并查看未报告网络活动。

   导航到天气页面，看看该页面 `weather.model.json` 是异步调用的。

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### 与SPA编辑器交互 {#interaction-with-the-spa-editor}

使用We.Retail日志应用程序示例，可以清楚地了解应用程序的行为和在发布时加载的方式，从而利用内容服务进行JSON内容投放以及异步加载资源。

此外，对于内容作者，使用SPA编辑器创建内容在AEM中是无缝的。

在以下部分中，我们将探索一份合同，该合同允许SPA编辑器将SPA中的组件与AEM组件关联，并实现无缝编辑体验。

1. 在编辑器中加载We.Retail日志应用程序并切换到 **预览模式** 。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. 使用浏览器的内置开发人员工具检查页面内容。 使用选择工具，在页面上选择一个可编辑的组件，然后视图元素详细信息。

   请注意，该组件具有新的数据属性 `data-cq-data-path`。

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   例如

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将其识别为SPA中的可编辑组件所需的唯一标记属性。 根据此属性，SPA编辑器将确定与组件关联的可编辑配置，以便正确的框架、工具栏等。 已加载。

   还为标记占位符和资产拖放功能添加了一些特定类名称。

   >[!NOTE]
   >
   >这是对AEM中服务器端呈现页面行为的更改，在AEM中，每个可编辑组件都插 `cq` 入了一个元素。
   >
   >
   >SPA中的这种方法无需注入自定义元素，只依赖附加的数据属性，从而简化了前端开发者的标记。

## 后续步骤 {#next-steps}

现在，您已了解AEM中的SPA编辑体验以及SPA与SPA编辑器的关系，可以更深入地了解SPA的构建方式。

* [AEM中的SPA快速入门](/help/sites-developing/spa-getting-started-react.md) ，显示了如何构建一个基本SPA以与AEM中的SPA编辑器结合使用
* [SPA编辑器概述](/help/sites-developing/spa-overview.md) ，深入介绍AEM与SPA之间的通信模型。
* [为AEM开发SPA](/help/sites-developing/spa-architecture.md) ，介绍如何吸引前端开发人员来为AEM开发SPA，以及SPA如何与AEM架构交互。
