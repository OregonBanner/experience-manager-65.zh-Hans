---
title: SPA和服务器端渲染
seo-title: SPA和服务器端渲染
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA和服务器端渲染{#spa-and-server-side-rendering}

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

>[!NOTE]
>
>需要AEM 6.5.1.0或更高版本才能使用本文档中所述的SPA服务器端渲染功能。

## 概述 {#overview}

单页应用程序(SPA)可以为用户提供丰富的动态体验，这种体验以熟悉的方式反应和行为，通常就像本机应用程序一样。 [这是通过依赖客户端预先加载内容，然后进行处理用户交互的繁重工作来实现的](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) ，从而最小化客户端和服务器之间需要的通信量，使应用更加被动。

但是，这可能导致较长的初始加载时间，尤其是当SPA较大且内容丰富时。 为了优化加载时间，某些内容可在服务器端呈现。 使用服务器端渲染(SSR)可以加快页面的初始加载，然后将进一步的渲染传递给客户端。

## 何时使用SSR {#when-to-use-ssr}

并非所有项目都需要SSR。 Althgouh AEM完全支持SPA的JS SSR,Adobe不建议对每个项目系统地实施它。

在决定实施SSR时，首先要估计SSR的实际代价，包括长期维护，SSR的额外复杂度、工作量和成本增加。 SSR结构的选择只有当增加值明显超过估计成本时。

SSR通常在以下任一问题有明确的“是”时提供一些值：

* **** SEO:SSR是否仍然需要SSR才能由带来流量的搜索引擎正确索引？ 请记住，主搜索引擎爬虫程序现在会评估JS。
* **** 页面速度：SSR是否提供了可衡量的实际环境中的速度提升，并增加了整体用户体验？

只有在这两个问题中至少有一个得到明确的“是”回答时，Adobe才建议实施SSR。 以下各节介绍如何使用Adobe I/O Runtime实现此操作。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您 [确信您的项目需要实施SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr)，则Adobe建议的解决方案是使用Adobe I/O Runtime。

有关Adobe I/O Runtime的更多信息，请参阅

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) —— 有关服务的概述
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) —— 有关该平台的详细文档

以下各节详细介绍了如何使用Adobe I/O Runtime在两种不同的模型中为您的SPA实施SSR:

* [AEM驱动的通信流](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O运行时驱动的通信流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建议为每个AEM环境（创作、发布、舞台等）使用单独的Adobe I/O Runtime实例。

## AEM驱动的通信流 {#aem-driven-communication-flow}

使用SSR时，AEM中 [](/help/sites-developing/spa-overview.md#workflow) SPA的组件交互工作流程包括在Adobe I/O Runtime上生成应用程序初始内容的阶段。

1. 浏览器从AEM请求SSR内容。

1. AEM将模型发布到Adobe I/O Runtime。

1. Adobe I/O Runtime返回生成的内容。

1. AEM通过后端页面组件的HTL模板为Adobe I/O Runtime返回的HTML提供服务。

![服务器端渲染-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O运行时驱动的通信流 {#adobe-i-o-runtime-driven-communication-flow}

上一节介绍了与AEM中的SPA相关的服务器端渲染的标准实施和建议实施，AEM在AEM中执行内容的引导和服务。

或者，SSR可以实现，这样Adobe I/O Runtime负责引导，有效地逆转了通信流。

两种型号均有效，且受AEM支持。 但是，在实施特定模型之前，应该考虑每个模型的优缺点。

<table>
 <tbody>
  <tr>
   <th><strong>引导</strong></th>
   <th><strong>优势</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>通过AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM根据需要管理注入库</li>
     <li>只需在AEM上维护资源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA开发人员可能不熟悉<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>通过Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA开发人员更熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM开发人员需要通过属性使应用程序（如CSS和JavaScript）所需的Clientlib资源可 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 用<br /> </li>
     <li>必须在AEM和Adobe I/O Runtime之间同步资源<br /> </li>
     <li>要启用SPA的创作，可能需要Adobe I/O Runtime的代理服务器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR规划 {#planning-for-ssr}

通常，只需在服务器端呈现应用程序的一部分。 通用示例是呈现服务器端时，将在页面初始加载时折叠上方显示的内容。 这通过将已呈现的内容交付到客户端来节省时间。 当用户与SPA交互时，客户端将呈现其他内容。

在考虑为SPA实施服务器端渲染时，您需要查看应用程序的哪些部分是必需的。

## 用SSR开发SPA {#developing-an-spa-using-ssr}

SPA组件可由客户端（在浏览器中）或服务器端呈现。 呈现服务器端时，浏览器属性（如窗口大小和位置）不存在。 因此，SPA组件应是同构的，不要假设它们将呈现在何处。

要利用SSR，您需要在AEM以及负责服务器端渲染的Adobe I/O Runtime上部署代码。 大多数代码将相同，但特定于服务器的任务将不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中SPA的SSR需要Adobe I/O Runtime，这用于渲染应用程序内容服务器端。 在应用程序的HTL中，将调用Adobe I/O Runtime上的资源来呈现内容。

正如AEM支持Angular和React SPA框架即装即用，Angular和React应用程序也支持服务器端渲染。 有关更多详细信息，请参阅两个框架的NPM文档。

* 反应： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* 角度： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

有关简单化的示例，请参阅 [We.Retail Journal应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 它呈现整个应用程序服务器端。 虽然这不是一个真实的例子，但它确实说明了实现SSR所需要的。

>[!CAUTION]
>
>We. [Retail Journal应用程序仅用于演示目的](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) ，因此将Node.js用作一个简单示例，而不是推荐的Adobe I/O Runtime。 此示例不应用于任何项目工作。

>[!NOTE]
>
>AEM上的所有SPA项目应基于 [Maven Archetype for SPA Starter Kit](https://github.com/adobe/aem-spa-project-archetype)。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在AEM中为SPA实施SSR的推荐解决方案。

对于预置AEM实例，也可以像上述那样使用自定义Node.js实例实现SSR。 尽管Adobe支持此功能，但不建议这样做。

>[!NOTE]
>
>Adobe托管的AEM实例不支持Node.js。

>[!NOTE]
>
>如果必须通过Node.js实现SSR,Adobe建议为每个AEM环境（作者、发布、舞台等）单独使用Node.js实例。
