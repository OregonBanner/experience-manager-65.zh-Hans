---
title: SPA 简介和演练
description: 本文介绍了 SPA 的概念，演练了如何使用基本 SPA 应用程序进行创作，并展示了它与底层 AEM SPA Editor 的关系。
topic-tags: spa
content-type: reference
exl-id: 95990112-2afc-420a-a7c7-9613f40d4c4a
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 71%

---


# SPA 简介和演练 {#spa-introduction-and-walkthrough}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用 SPA 框架构建站点，而作者则希望能够在 AEM 中顺畅地为使用此类框架构建的站点编辑内容。

SPA 编辑器提供了一个全面的解决方案来支持 AEM 中的 SPA。本文演练了如何使用基本 SPA 应用程序进行创作，并展示了它与底层 AEM SPA Editor 的关系。

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA Framework的客户端渲染(例如React或Angular)的项目。

## 简介 {#introduction}

### 文章目标 {#article-objective}

本文先介绍了 SPA 的基本概念，然后使用简单 SPA 应用程序来演示基本内容编辑，从而引导完成浏览 SPA 编辑器演练。随后，深入探究了页面构造以及 SPA 应用程序如何与 AEM SPA Editor 相关并与之交互。

此简介和演练的目的是，向 AEM 开发人员说明 SPA 为何相关及其通常如何工作、AEM SPA Editor 如何处理 SPA，以及它与标准 AEM 应用程序的差异。

## 要求 {#requirements}

该演练基于标准 AEM 功能和示例 WKND SPA Project 应用程序。要完成本演练，您必须拥有以下资源。

* [AEM版本6.5.4或更高版本](/help/release-notes/release-notes.md)
   * 您必须拥有系统的管理员权限。
* [GitHub 上提供的示例 WKND SPA Project 应用程序](https://github.com/adobe/aem-guides-wknd-spa)
   * 下载 [最新版本的React应用程序。](https://github.com/adobe/aem-guides-wknd-spa/releases) 其命名将类似于 `wknd-spa-react.all.classic-X.Y.Z-SNAPSHOT.zip`.
   * 下载 [最新示例图像](https://github.com/adobe/aem-guides-wknd-spa/releases) 应用程序的。 其命名将类似于 `wknd-spa-sample-images-X.Y.Z.zip`.
   * [使用包管理器](/help/sites-administering/package-manager.md) 以安装包，就像安装AEM中的任何其他包一样。
   * 在本演练中，无需使用 Maven 安装应用程序。

>[!CAUTION]
>
>本文档使用 [WKND Spa项目应用程序](https://github.com/adobe/aem-guides-wknd-spa) 仅供演示之用。 不应将它用于任何项目工作。
>
>任何AEM项目都应利用 [AEM项目原型，](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 支持使用React或Angular的SPA项目，并利用SPA SDK。

### 什么是 SPA？ {#what-is-a-spa}

单页应用程序 (SPA) 与传统页面的不同之处在于，它在客户端呈现且主要由 JavaScript 驱动，并且依靠 Ajax 调用来加载数据和动态更新页面。大多数内容或所有内容在单个页面加载中检索一次，并基于用户与页面的交互按需异步加载其他资源。

这减少了页面刷新需求，并为用户提供了一种无缝、快速且更类似于本机应用程序体验的体验。

利用 AEM SPA Editor，前端开发人员可以创建可集成到 AEM 站点中的 SPA，从而允许内容作者像编辑任何其他 AEM 内容那样轻松地编辑 SPA 内容。

### 为什么使用 SPA？ {#why-a-spa}

SPA 的工作方式的特性使其更快、更流畅且更类似于本机应用程序，从而为网页访客以及营销人员和开发人员提供一种极具吸引力的体验。

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**访客**

* 访客希望在与内容交互时获得与本地体验类似的体验。
* 有数据明确表明，页面越快，转化几率就越高。

**营销人员**

* 营销人员希望提供丰富的、与本地体验类似的体验，以促使访客充分参与互动并与内容产生共鸣。
* 个性化可以使这些体验变得更具吸引力。

**开发人员**

* 开发人员希望完全分离内容和表示形式之间的关注点。
* 完全分离可提高系统的可扩展性，并允许独立的前端开发。

### SPA 的工作原理是什么？ {#how-does-a-spa-work}

SPA的主要思想是减少对服务器的调用和依赖以最大限度地减少服务器调用造成的延迟，使SPA接近本机应用程序的响应速度。

在传统的连续网页中，仅加载即时页面所需的数据。这意味着，当访客移至另一个页面时，将调用服务器以获取其他资源。当访客与页面上的元素进行交互时，可能需要额外的调用。 由于页面必须与访客的请求同步，因此多次调用可能会给人一种滞后或延迟的感觉。

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

为了获得更流畅的体验（接近访客从本机移动设备应用程序中期望的体验），SPA会在首次加载时加载访客的所有必要数据。 虽然最初可能需要花费更长的时间，但随后便不再需要额外的服务器调用。

通过在客户端进行渲染，页面元素可以更快地做出反应，并且访客与页面的交互可以立即进行。 为了最大化页面速度，可能需要的任何其他数据都会异步调用。

>[!NOTE]
>
>有关SPA如何在AEM中工作的技术详细信息，请参阅文章 [AEM中的SPA入门](/help/sites-developing/spa-getting-started-react.md).
>
>要更详细地了解SPA编辑器的设计、架构和技术工作流，请参阅文章 [SPA编辑器概述](/help/sites-developing/spa-overview.md).

## SPA 的内容编辑体验 {#content-editing-experience-with-spa}

构建SPA以利用AEM SPA编辑器时，内容作者在编辑和创建内容时不会注意到任何差异。 提供了常用 AEM 功能，而无需更改作者的工作流。

1. 在 AEM 中编辑 WKND SPA Project 应用程序。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

   ![步骤 1](assets/spa-walkthrough-step-1.png)

1. 选择一个标题组件，并注意工具栏会像任何其他组件一样显示。 选择&#x200B;**编辑**。

   ![步骤2](assets/spa-walkthrough-step-2.png)

1. 在 AEM 中正常编辑内容，会发现更改已保存。

   ![步骤3](assets/spa-walkthrough-step-3.png)

   >[!NOTE]
   >
   >请参阅 [SPA编辑器概述](spa-overview.md#requirements-limitations) 有关就地文本编辑器和SPA的更多信息。

1. 使用资源浏览器将新图像拖放到图像组件中。

   ![步骤4](assets/spa-walkthrough-step-4.png)

1. 将保留更改。

   ![步骤5](assets/spa-walkthrough-step-5.png)

与在任何非 SPA 应用程序一样，支持其他创作工具，例如在页面上拖放其他组件、重新排列组件和修改版面。

>[!NOTE]
>
>SPA 编辑器不修改应用程序的 DOM。SPA 本身负责 DOM。
>
>要了解其工作原理，请继续阅读本文的下一部分 [SPA 应用程序和 AEM SPA Editor](#spa-apps-and-the-aem-spa-editor)。

## SPA 应用程序和 AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

体验SPA对最终用户的行为方式，然后检查SPA页面，有助于更好地了解SAP应用程序如何与AEM中的SPA编辑器配合工作。

### 使用 SPA 应用程序 {#using-an-spa-application}

1. 在发布服务器上或使用页面编辑器中的&#x200B;**页面信息**&#x200B;菜单上的&#x200B;**以发布的形式查看**&#x200B;选项加载 WKND SPA Project 应用程序。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![步骤 1](assets/spa-walkthrough-step-1-1.png)

   请注意页面结构，包括导航到子页面、天气小部件和文章。

1. 使用菜单导航到子页面，可以看到页面将立即加载，而无需刷新。

   ![步骤2](assets/spa-walkthrough-step-1-2.png)

1. 打开浏览器的内置开发人员工具，并在您浏览子页面时监控网络活动。

   ![步骤3](assets/spa-walkthrough-step-1-3.png)

   在应用程序中从一个页面移至另一个页面时，几乎不产生流量。不会重新加载页面，而只请求新图像。

   SPA 完全在客户端管理内容和路由。

那么，如果在子页面中导航时没有重新加载页面，如何加载页面呢？

下一节， [加载SPA应用程序，](#loading-an-spa-application) 深入了解加载SPA的机制，以及如何同步和异步加载内容。

### 加载 SPA 应用程序 {#loading-an-spa-application}

1. 如果未加载，请在发布服务器上或使用页面编辑器中的&#x200B;**页面信息**&#x200B;菜单上的&#x200B;**以发布的形式查看**&#x200B;选项加载 WKND SPA Project 应用程序。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![步骤 1](assets/spa-walkthrough-step-1-1.png)

1. 使用浏览器的内置工具可查看页面的源。
1. 请注意，源的内容极其有限。

   * 页面的正文中没有任何内容。它主要由样式表和对各种脚本（例如 `clientlib-react.min.js`）的调用构成。
   * 这些脚本是此应用程序的主要驱动程序，负责呈现所有内容。

1. 可以使用浏览器的内置工具检查页面。查看完全加载的 DOM 的内容。

   ![步骤4](assets/spa-walkthrough-step-1-4.png)

1. 切换到 **网络** 选项卡，然后重新加载页面。

   忽略图像请求，请注意，为页面加载的主要资源是页面本身、CSS、React JavaScript、其依赖项以及页面的JSON数据。

   ![步骤5](assets/spa-walkthrough-step-1-5.png)

1. 在新选项卡中加载 `react.model.json`。

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![步骤6](assets/spa-walkthrough-step-1-6.png)

   AEM SPA Editor 利用 [AEM 内容服务](/help/assets/content-fragments/content-fragments.md)将页面的全部内容作为 JSON 模型交付。

   通过实施特定接口，Sling 模型为 SPA 提供了必要信息。将 JSON 数据的交付工作向下委派给每个组件（从页面到段落再到组件等）。

   每个组件都会选择它公开的内容及其呈现方式（使用HTL的服务器端或使用React的客户端）。 本文重点介绍使用 React 进行客户端呈现。

1. 该模型还可以对页面进行分组以便同步加载它们，从而减少所需的页面重新加载次数。

   在 WKND SPA Project 应用程序示例中，`home`、`page-1`、`page-2` 和 `page-3` 页面将同步加载，因为访客通常会访问所有这些页面。

   此行为不是强制性的，而是完全可定义的。

   ![步骤7](assets/spa-walkthrough-step-1-7.png)

1. 要查看这种行为差异，请重新加载页面并清除开发人员工具的网络活动。 导航到页面菜单中的 `page-1`，可以看到唯一的网络活动是请求 `page-1` 的图像。`page-1` 本身无需加载。

   ![步骤8](assets/spa-walkthrough-step-1-8.png)

### 与 SPA 编辑器进行交互 {#interaction-with-the-spa-editor}

通过使用示例 WKND SPA Project 应用程序，可以清楚地了解应用程序在发布时的行为和加载方式，如何使用内容服务进行 JSON 内容交付以及如何异步加载资源。

此外，对于内容作者而言，在 AEM 中使用 SPA 编辑器创建内容是无缝操作。

在下一部分中，我们将探究允许 SPA 编辑器将 SPA 中的组件与 AEM 组件相关联并实现此无缝编辑体验的合同。

1. 在编辑器中加载 WKND SPA Project 应用程序并切换到&#x200B;**预览**&#x200B;架构。

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. 使用浏览器的内置开发人员工具检查页面内容。使用选择工具，在页面上选择一个可编辑的组件并查看元素详细信息。

   请注意，该组件具有一个新的数据属性 `data-cq-data-path`。

   ![步骤2](assets/spa-walkthrough-step-2-2.png)

   例如

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   此路径允许检索和关联每个组件的编辑上下文配置对象。

   这是编辑器将组件识别为 SPA 中的可编辑组件所需的唯一标记属性。根据此属性，SPA 编辑器将确定哪项可编辑的配置与组件关联，以便加载正确的框架、工具栏等。

   还为标记占位符和资源拖放功能添加了一些特定的类名。

   >[!NOTE]
   >
   >这是AEM中服务器端渲染页面的行为更改，其中有一个 `cq` 为每个可编辑组件插入的元素。
   >
   >
   >SPA中的此方法无需注入自定义元素，只需依赖其他数据属性，使得前端开发人员更容易标记这些元素。

## 后续步骤 {#next-steps}

现在，您已了解 AEM 中的 SPA 编辑体验以及 SPA 与 SPA 编辑器的关系，请更深入地了解 SPA 的构建方式。

* [AEM中的SPA入门](/help/sites-developing/spa-getting-started-react.md) 显示了如何构建基本SPA以便在AEM中使用SPA编辑器
* [SPA 编辑器概述](/help/sites-developing/spa-overview.md)更深入地介绍了 AEM 和 SPA 之间的通信模型。
* [为 AEM 开发 SPA](/help/sites-developing/spa-architecture.md) 介绍了如何让前端开发人员为 AEM 开发 SPA，以及 SPA 如何与 AEM 的架构进行交互。
