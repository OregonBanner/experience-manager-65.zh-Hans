---
title: SPA和服务器端渲染
seo-title: SPA and Server-Side Rendering
description: "SPA和服务器端渲染"
seo-description: null
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
source-git-commit: f923a3b7d6821f63d059f310de783b11bf3e8ec3
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 2%

---

# SPA和服务器端渲染{#spa-and-server-side-rendering}

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如React或Angular)的项目，建议使用SPA编辑器。

>[!NOTE]
>
>需要AEM 6.5.1.0或更高版本才能使用本文档中所述的SPA服务器端渲染功能。

## 概述 {#overview}

单页应用程序(SPA)可以为用户提供丰富的动态体验，该体验以熟悉的方式反应和行为，通常就像本机应用程序一样。 [这是依靠客户端预先加载内容，然后执行处理用户交互的重提升](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 从而最大限度地减少客户端和服务器之间所需的通信量，使应用程序更具反应性。

但是，这可能会导致初始加载时间较长，尤其是当SPA较大且内容丰富时。 为了优化加载时间，可以在服务器端渲染某些内容。 使用服务器端渲染(SSR)可以加快页面的初始加载，然后将进一步的渲染传递给客户端。

## 何时使用SSR {#when-to-use-ssr}

并非所有项目都需要SSR。 尽管AEM完全支持适用于SPA的JS SSR，但Adobe建议不要为每个项目系统地实施它。

在决定实施SSR时，您必须首先估计增加SSR对项目实际意味着哪些额外的复杂性、工作量和成本，包括长期维护。 只有在增加值明显超过估计成本时，才应选择SSR架构。

当以下任一问题明确为“是”时，SSR通常会提供一些值：

* **SEO：** 是否仍需要SSR才能让带来流量的搜索引擎对您的网站正确编制索引？ 请记住，主搜索引擎爬虫程序现在评估JS。
* **页面速度：** SSR是否可以在实际环境中提供可衡量的速度提升，并增加总体用户体验？

只有当这两个问题中至少有一个问题得到明确的“是”回答时，Adobe才会建议实施SSR。 以下部分介绍了如何使用Adobe I/O Runtime执行此操作。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您 [确信您的项目需要实施SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr)，Adobe推荐的解决方案是使用Adobe I/O Runtime。

有关Adobe I/O Runtime的更多信息，请参阅

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 有关服务的概述
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 有关平台的详细文档

以下部分详细介绍如何使用Adobe I/O Runtime在两种不同的模型中为SPA实施SSR：

* [AEM驱动的通信流](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime驱动的通信流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建议为每个环境（暂存、生产、测试等）使用单独的Adobe I/O Runtime工作区。 这样一来，对于部署到不同环境的单个应用程序的不同版本，就可以采用典型的系统开发生命周期(SDLC)模式。 查看文档 [Project App Builder应用程序的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 了解更多信息。
>
>每个实例（创作、发布）不需要单独的工作区，除非每个实例类型的运行时实施存在差异。

## 远程渲染器配置 {#remote-renderer-configuration}

AEM必须知道可在何处检索远程渲染的内容。 不论 [您选择为SSR实施的模型，](#adobe-i-o-runtime) 您需要向AEM指定如何访问此远程渲染服务。

这是通过 **RemoteContentRenderer — 配置工厂OSGi服务**. 在Web控制台配置控制台中搜索字符串“RemoteContentRenderer”，网址为 `http://<host>:<port>/system/console/configMgr`.

![渲染器配置](assets/rendererconfig.png)

以下字段可用于配置：

* **内容路径模式**  — 正则表达式，以便匹配部分内容（如有必要）
* **远程端点URL**  — 负责生成内容的端点的URL
   * 如果不在本地网络中，则使用安全的HTTPS协议。
* **其他请求标头**  — 要添加到发送到远程端点的请求的其他标头
   * 图案: `key=value`
* **请求超时**  — 远程主机请求超时（以毫秒为单位）

>[!NOTE]
>
>无论您是否选择实施 [AEM驱动的通信流](#aem-driven-communication-flow) 或 [Adobe I/O Runtime驱动的流量，](#adobe-i-o-runtime-driven-communication-flow) 您必须定义远程内容渲染器配置。
>
>如果您选择执行以下操作，则必须定义此配置 [使用自定义Node.js服务器。](#using-node-js)

>[!NOTE]
>
>此配置利用 [远程内容呈现器、](#remote-content-renderer) 提供了其他扩展和自定义选项。

## AEM驱动的通信流 {#aem-driven-communication-flow}

使用SSR时， [组件交互工作流](/help/sites-developing/spa-overview.md#workflow) AEM中的SPA包含在Adobe I/O Runtime上生成应用程序初始内容的阶段。

1. 浏览器从AEM请求SSR内容。

1. AEM将模型发布到Adobe I/O Runtime。

1. Adobe I/O Runtime返回生成的内容。

1. AEM通过后端HTML组件的HTL模板为Adobe I/O Runtime返回的页面提供服务。

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驱动的通信流 {#adobe-i-o-runtime-driven-communication-flow}

上一部分介绍了与AEM中的SPA有关的服务器端渲染的标准实施和建议实施，AEM在该环境中执行内容引导和提供。

或者，可以实现SSR，以便Adobe I/O Runtime负责自引导，有效地反转通信流。

这两个模型均有效，并受AEM支持。 但是，在实施特定模型之前，应该考虑每种模型的优缺点。

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>通过AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM在需要时管理注入库</li>
     <li>仅需在AEM上维护资源<br /> </li>
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
     <li>应用程序所需的Clientlib资源（如CSS和JavaScript）将由AEM开发人员通过 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 属性<br /> </li>
     <li>必须在AEM和Adobe I/O Runtime之间同步资源<br /> </li>
     <li>要启用SPA的创作，可能需要Adobe I/O Runtime的代理服务器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 规划SSR {#planning-for-ssr}

通常只需在服务器端渲染应用程序的一部分。 常见的示例是在服务器端呈现页面初始加载时显示在折叠上方的内容。 这通过向客户端交付已渲染的内容来节省时间。 当用户与SPA交互时，其他内容由客户端渲染。

在考虑为SPA实施服务器端渲染时，您需要查看应用程序的哪些部分需要渲染。

## 使用SSR开发SPA {#developing-an-spa-using-ssr}

SPA组件可由客户端（在浏览器中）或服务器端渲染。 在渲染服务器端时，不存在浏览器属性，例如窗口大小和位置。 因此，SPA组件应当同构，而不对其呈现的位置做出任何假设。

要利用SSR，您需要在AEM以及负责服务器端渲染的Adobe I/O Runtime上部署代码。 大多数代码将相同，但特定于服务器的任务将有所不同。

## AEM中适用于SPA的SSR {#ssr-for-spas-in-aem}

AEM中适用于SPA的SSR需要Adobe I/O Runtime，它用于渲染应用程序内容服务器端。 在应用程序的HTL中，调用Adobe I/O Runtime上的资源来渲染内容。

正如AEM支持开箱即用的Angular和React SPA框架一样，Angular和React应用程序也支持服务器端渲染。 有关更多详细信息，请参阅这两个框架的NPM文档。

* 反应： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* angular： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

有关简单示例，请参阅 [We.Retail日志应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). 它呈现整个应用程序服务器端。 尽管这不是一个现实的例子，但它的确说明了实施SSR所需的条件。

>[!CAUTION]
>
>此 [We.Retail日志应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 仅用于演示目的，因此使用Node.js作为简单示例，而不是推荐的Adobe I/O Runtime。 此示例不应用于任何项目工作。

>[!NOTE]
>
>任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在AEM中为SPA实施SSR的推荐解决方案。

对于预部署AEM实例，还可以使用自定义Node.js实例以与上述相同的方式实施SSR。 虽然Adobe支持此功能，但不建议这样做。

>[!NOTE]
>
>Adobe托管的AEM实例不支持Node.js。

>[!NOTE]
>
>如果必须通过Node.js实施SSR，则Adobe建议为每个AEM环境（创作、发布、暂存等）使用单独的Node.js实例。

## 远程内容渲染器 {#remote-content-renderer}

此 [远程内容渲染器配置](#remote-content-renderer-configuration) 在AEM中将SSR与SPA结合使用时，需要用到更广泛的渲染服务，可根据您的需求对其进行扩展和自定义。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是一项OSGi服务，用于检索在远程服务器上渲染的内容，例如从Adobe I/O中渲染的内容。发送到远程服务器的内容基于传递的请求参数。

`RemoteContentRenderingService` 在需要额外内容操作时，可以通过依赖关系反转插入自定义Sling模型或servlet中。

此服务在内部由 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

此 `RemoteContentRendererRequestHandlerServlet` 可用于以编程方式设置请求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`（提供的默认请求处理程序实施）允许您创建多个OSGi配置，以将内容结构中的位置映射到远程端点。

要添加自定义请求处理程序，请实施 `RemoteContentRendererRequestHandler` 界面。 请务必设置 `Constants.SERVICE_RANKING` 组件属性到大于100的整数，该整数的排名是 `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置默认处理程序的OSGi配置 {#configure-default-handler}

必须按照一节中所述配置默认处理程序的配置 [远程内容渲染器配置](#remote-content-renderer-configuration).

### 远程内容渲染器使用情况 {#usage}

要执行servlet获取并返回一些可以插入到页面中的内容，请执行以下操作：

1. 确保您的远程服务器可访问。
1. 向AEM组件的HTL模板中添加以下代码片段之一。
1. （可选）创建或修改OSGi配置。
1. 浏览网站内容

通常，页面组件的HTL模板是此类功能的主要接收者。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

servlet利用Sling模型导出器来序列化组件数据。 默认情况下， `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支持作为Sling模型适配器。 如有必要，您可以使用 `RemoteContentRendererServlet` 并实施 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 其他类必须扩展 `ComponentExporter`.
