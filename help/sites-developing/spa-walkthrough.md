---
title: SPA简介和演练
seo-title: SPA简介和演练
description: 本文介绍SPA的概念，并逐步介绍使用基本的SPA应用程序进行创作，显示它与基础的SPA editor的关系。
seo-description: 本文介绍SPA的概念，并逐步介绍使用基本的SPA应用程序进行创作，显示它与基础的SPA editor的关系。
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 0%

---


# SPA简介和演练{#spa-introduction-and-walkthrough}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望无缝编辑AEM中的内容，以便使用此类框架构建站点。

SPA Editor优惠了在AEM内支持SPA的全面解决方案。 本文将逐步介绍如何使用基本的SPA应用程序进行创作，并说明它与基础的AEM SPA编辑器的关系。

>[!NOTE]
>
>SPA编辑器是需要SPA框架的客户端渲染（例如，React或Angular）的项目的推荐解决方案。

## 简介 {#introduction}

### 文章目标{#article-objective}

本文介绍SPA的基本概念，然后引导读者通过使用简单的SPA应用程序演示基本内容编辑过程来演练SPA编辑器。 然后深入到页面的构造以及SPA应用程序与AEM SPA编辑器的关联和交互。

此简介和演练的目的是向AEM开发人员演示SPA的相关性、其一般工作方式、SPA如何由AEM editor处理以及它与标准的AEM应用程序有何不同。

该演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：

* [AEM 6.4版（带有service pack 2）或更高版本](/help/release-notes/sp-release-notes.md)
* [在GitHub上安装We.Retail日志应用程序示例。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>此文档仅将[We.Retail日志应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)用于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应利用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

### 什么是SPA?{#what-is-a-spa}

单页应用程序(SPA)与传统页面不同，它呈现在客户端，主要由Javascript驱动，依靠Ajax调用加载数据和动态更新页面。 大多数或所有内容在单页加载中检索一次，并根据用户与页面的交互情况按需异步加载其他资源。

这减少了页面刷新的需求，并为用户提供了无缝、快速的体验，更像原生的App体验。

AEM SPA编辑器允许前端开发人员创建可集成到AEM站点的SPA，使内容作者能够像编辑任何其他AEM内容一样轻松地编辑SPA内容。

### 为什么是SPA?{#why-a-spa}

SPA更快、更流畅，更像本机应用程序，它不仅对网页的访客非常有吸引力，而且对于营销人员和开发人员也极具吸引力，因为SPA的工作方式。

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

### SPA如何工作？{#how-does-a-spa-work}

SPA的主要思想是减少对服务器的调用和依赖，以最大限度地减少由服务器调用引起的延迟，使SPA接近本机应用程序的响应。

在传统的连续网页中，只加载立即页面所需的数据。 这意味着当访客移到其他页面时，将调用服务器获取其他资源。 当访客与页面上的元素交互时，可能需要进行其他调用。 由于页面必须跟上访客的请求，因此这些多次调用可能会产生延迟或延迟。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

要获得更流畅的体验，即接近访客从移动、本机应用程序中期望的效果，SPA在第一次加载时为访客加载所有必要的数据。 尽管这一过程一开始可能需要稍长一些，但随后它就不再需要额外的服务器调用。

通过在客户端进行渲染，页面元素可以更快地反应，并且访客可以立即与页面进行交互。 可能需要的任何其他数据都将异步调用，以最大化页面速度。

>[!NOTE]
>
>有关SPA在AEM中如何工作的技术详细信息，请参阅文章[AEM在](/help/sites-developing/spa-getting-started-react.md)快速入门。
>
>要详细了解SPA Editor的设计、体系结构和技术工作流程，请参阅文章[SPA Editor概述](/help/sites-developing/spa-overview.md)。

## SPA {#content-editing-experience-with-spa}的内容编辑体验

当构建SPA以利用AEM SPA编辑器时，内容作者注意到在编辑和创建内容时没有区别。 通用的AEM功能可用，无需更改作者的工作流程。

>[!NOTE]
>
>该演练基于标准AEM功能和示例We.Retail日志应用程序。 必须满足以下要求：
>
>* [AEM 6.4版（带有service pack 2）](/help/release-notes/sp-release-notes.md)
>* [在GitHub上安装We.Retail日志应用程序示例。](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>



1. 在AEM中编辑We.Retail日志应用程序。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. 选择一个标题组件，然后注意工具栏的显示方式与任何其他组件的显示方式相同。 选择&#x200B;**编辑**。

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. 按照AEM中的正常方式编辑内容，并注意更改会保留。

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >有关就地文本编辑器和SPA的更多信息，请参见[SPA Editor概述](spa-overview.md#requirements-limitations)。

1. 使用资产浏览器将新图像拖放到图像组件中。

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. 更改将被保留。

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

与任何非SPA应用程序一样，支持其他创作工具，如在页面上拖放其他组件、重新排列组件以及修改布局。

>[!NOTE]
>
>SPA编辑器不修改应用程序的DOM。 SPA本身负责DOM。
>
>要了解其工作原理，请继续阅读本文[SPA应用程序和AEM SPA编辑器](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)的下一节。

## SPA应用程序和AEM SPA编辑器{#spa-apps-and-the-aem-spa-editor}

了解SPA对最终用户的作用，然后检查SPA页面有助于更好地了解SAP应用程序与AEM editor在SPA中的工作方式。

### 使用SPA应用程序{#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器中的&#x200B;**页面信息**&#x200B;菜单中的选项&#x200B;**视图作为发布**&#x200B;加载We.Retail日志应用程序。

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

下一节[加载SPA应用程序](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)深入探讨了加载SPA以及如何同步和异步加载内容的机制。

### 加载SPA应用程序{#loading-an-spa-application}

1. 如果尚未加载，请在发布服务器上或从页面编辑器的&#x200B;**页面信息**&#x200B;菜单中使用选项&#x200B;**视图作为发布**&#x200B;加载We.Retail日志应用程序。

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

   页面的正文中没有任何内容。 它主要由样式表和对React脚本的调用组成， `we-retail-journal-react.js`。

   此React脚本是此应用程序的主要驱动程序，负责渲染所有内容。

1. 使用浏览器的内置工具检查页面。 查看完全加载的DOM的内容。

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. 切换到检查器中的“网络”选项卡并重新加载该页。

   忽略图像请求，请注意为页面加载的主要资源包括页面本身、CSS、React Javascript、其依赖项以及页面的JSON数据。

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. 在新选项卡中加载`react.model.json`。

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA编辑器利用[AEM Content Services](/help/assets/content-fragments/content-fragments.md)将页面的整个内容作为JSON模型提供。

   通过实现特定界面，Sling模型为SPA提供必要的信息。 JSON投放的会向下委派给每个组件（从页面、段落、组件等）。

   每个组件都选择它公开的内容和呈现方式（在服务器端使用HTL，在客户端使用React）。 当然，本文侧重于使用React进行客户端渲染。

1. 该模型还可以将页面分组在一起，以便它们同步加载，从而减少需要重新加载的页面数。

   在We.Retail日志的示例中，`home`、`blog`和`aboutus`页面同步加载，因为访客通常访问所有这些页面。 但是，`weather`页面是异步加载的，因为访客不太可能访问它。

   此行为不是强制的，并且完全可以定义。

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. 要视图行为上的这种差异，请重新加载页面并清除检查器的网络活动。 导航到页面菜单中的博客和关于我们的页面，并查看没有报告网络活动。

   导航到天气页面，看看`weather.model.json`是异步调用的。

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### 与SPA Editor {#interaction-with-the-spa-editor}交互

使用示例We.Retail日志应用程序，您可以清楚地了解应用程序的行为和发布时的加载方式，为JSON内容投放提供内容服务，并异步加载资源。

此外，对于内容作者而言，使用SPA编辑器创建内容在AEM中是无缝的。

在下一节中，我们将探索允许SPA编辑器将SPA组件与AEM组件关联并实现无缝编辑体验的合同。

1. 在编辑器中加载We.Retail日志应用程序并切换至&#x200B;**预览**&#x200B;模式。

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. 使用浏览器内置的开发人员工具检查页面内容。 使用选择工具，在页面上选择一个可编辑的组件，然后视图元素详细信息。

   请注意，该组件具有新的数据属性`data-cq-data-path`。

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   例如

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将其识别为SPA中的可编辑组件所需的唯一标记属性。 SPA Editor将根据此属性确定与组件关联的可编辑配置，以便正确的框架、工具栏等。 已加载。

   还为标记占位符和资产拖放功能添加了一些特定类名称。

   >[!NOTE]
   >
   >这是AEM中服务器端呈现页面的行为变化，其中每个可编辑组件都插入了`cq`元素。
   >
   >
   >SPA中的此方法消除了注入自定义元素的需要，只依赖附加的数据属性，使前端开发者的标记更简单。

## 后续步骤{#next-steps}

现在，您已了解AEM的SPA编辑体验以及SPA与SPA编辑器的关系，并进一步了解SPA是如何构建的。

* [在AEM中快速入](/help/sites-developing/spa-getting-started-react.md) 门演示如何构建基本的SPA以与AEM中的SPA编辑器一起使用
* [SPA ](/help/sites-developing/spa-overview.md) Editor Overview深入探讨AEM与SPA之间的通信模型。
* [为AEM开](/help/sites-developing/spa-architecture.md) 发SPA介绍如何吸引前端开发人员来开发SPA  ，以及SPA如何与AEM体系架构交互。
