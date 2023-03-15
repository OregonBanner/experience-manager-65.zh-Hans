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
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

>[!NOTE]
>
>要使用SPA服务器端渲染功能，需要AEM 6.5.1.0或更高版本，如本文档中所述。

## 概述 {#overview}

单页应用程序(SPA)可以为用户提供丰富的动态体验，这种体验可以以熟悉的方式反应和行为，通常与本机应用程序类似。 [这是通过依靠客户端在前面加载内容，然后进行处理用户交互的重量提升来实现的](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 从而最大限度地减少客户端与服务器之间需要的通信量，从而使应用程序更加被动。

但是，这可能会导致较长的初始加载时间，尤其是当SPA较大且内容丰富时。 为了优化加载时间，某些内容可以在服务器端呈现。 使用服务器端渲染(SSR)可以加快页面的初始加载速度，然后将进一步的渲染传递到客户端。

## 何时使用SSR {#when-to-use-ssr}

并非所有项目都需要SSR。 尽管AEM完全支持SPA的JS SSR，但是，Adobe不建议为每个项目系统地实施它。

在决定实施SSR时，您必须首先估计项目实际上所代表的额外复杂性、工作量和增加成本，包括长期维护。 SSR架构只有在增值明显超过估计成本时才应选择。

SSR通常在以下任一问题出现明确的“是”时提供一些值：

* **SEO:** 网站是否仍需要SSR才能被带来流量的搜索引擎正确索引？ 请记住，主搜索引擎爬取程序现在会评估JS。
* **页面速度：** SSR是否在现实环境中提供了可衡量的速度提升，并且增加了整体用户体验？

只有在对您的项目至少回答了这两个问题中的一个并明确给出“是”时，Adobe才建议实施SSR。 以下各节介绍如何使用Adobe I/O Runtime实现此目的。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您 [确信您的项目需要实施SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr),Adobe的推荐解决方案是使用Adobe I/O Runtime。

有关Adobe I/O Runtime的更多信息，请参阅

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 服务概述
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 有关平台的详细文档

以下各节详细介绍了如何在两种不同的模型中使用Adobe I/O Runtime来为SPA实施SSR:

* [AEM驱动的通信流](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime驱动的通信流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建议每个环境（暂存、生产、测试等）单独使用Adobe I/O Runtime工作区。 这允许使用典型的系统开发生命周期(SDLC)模式，将单个应用程序的不同版本部署到不同的环境。 查看文档 [适用于项目应用程序生成器应用程序的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 以了解更多信息。
>
>除非每个实例类型的运行时实施存在差异，否则不需要每个实例（创作、发布）单独的工作区。

## 远程渲染器配置 {#remote-renderer-configuration}

AEM必须知道可在何处检索远程渲染的内容。 无论 [选择为SSR实施的模型，](#adobe-i-o-runtime) 您需要指定以AEM如何访问此远程渲染服务。

这是通过 **RemoteContentRenderer - Configuration Factory OSGi服务**. 在Web控制台配置控制台中搜索字符串“RemoteContentRenderer”(位于 `http://<host>:<port>/system/console/configMgr`.

![渲染器配置](assets/rendererconfig.png)

以下字段可用于配置：

* **内容路径模式**  — 正则表达式以匹配部分内容（如有必要）
* **远程端点URL**  — 负责生成内容的端点的URL
   * 如果不在本地网络中，则使用安全HTTPS协议。
* **其他请求头**  — 要添加到发送到远程端点的请求的其他标头
   * 图案: `key=value`
* **请求超时**  — 远程主机请求超时（以毫秒为单位）

>[!NOTE]
>
>无论您是否选择实施 [AEM驱动的通信流](#aem-driven-communication-flow) 或 [Adobe I/O Runtime驱动的流，](#adobe-i-o-runtime-driven-communication-flow) 您必须定义远程内容渲染器配置。
>
>如果您选择 [使用自定义Node.js服务器。](#using-node-js)

>[!NOTE]
>
>此配置利用 [远程内容渲染器、](#remote-content-renderer) 具有其他可用的扩展和自定义选项。

## AEM驱动的通信流 {#aem-driven-communication-flow}

使用SSR时， [组件交互工作流](/help/sites-developing/spa-overview.md#workflow) AEM中的SPA包含在Adobe I/O Runtime上生成应用程序初始内容的阶段。

1. 浏览器从AEM请求SSR内容。

1. AEM将模型发布到Adobe I/O Runtime。

1. Adobe I/O Runtime会返回生成的内容。

1. AEM会提供Adobe I/O Runtime通过后端页面组件的HTL模板返回的HTML。

![服务器端渲染 — cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驱动的通信流 {#adobe-i-o-runtime-driven-communication-flow}

上一节介绍了与AEM中的SPA有关的服务器端渲染的标准实施和建议实施，AEM在其中执行内容的引导和服务。

或者，SSR可以实现，以便Adobe I/O Runtime负责引导，有效地逆转通信流。

这两个模型都有效，且受AEM支持。 但是，在实施特定模式之前，应考虑每个模式的利弊。

<table>
 <tbody>
  <tr>
   <th><strong>引导</strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <th><strong>通过AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM在需要时管理注入库</li>
     <li>只需在AEM上维护资源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>可能不熟悉SPA开发人员<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>通过Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>更熟悉SPA开发人员<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM开发人员需要通过 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 属性<br /> </li>
     <li>必须在AEM和Adobe I/O Runtime之间同步资源<br /> </li>
     <li>要启用SPA的创作功能，可能需要Adobe I/O Runtime的代理服务器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR规划 {#planning-for-ssr}

通常，只需要在服务器端呈现应用程序的一部分。 常见的示例是，在页面的初始加载时，将在折页上方显示的内容会在服务器端呈现。 这通过将已呈现的内容传送到客户端来节省时间。 当用户与SPA交互时，客户端会呈现其他内容。

在考虑为SPA实施服务器端渲染时，您需要查看应用程序的哪些部分是必需的。

## 用SSR开发SPA {#developing-an-spa-using-ssr}

SPA组件可由客户端（在浏览器中）或服务器端呈现。 呈现服务器端时，浏览器属性（如窗口大小和位置）不存在。 因此，SPA组件应当是同构的，不应假设它们将在何处呈现。

要利用SSR，您需要在AEM以及负责服务器端渲染的Adobe I/O Runtime上部署代码。 大多数代码将相同，但特定于服务器的任务将有所不同。

## AEM中的SPA SSR {#ssr-for-spas-in-aem}

AEM中的SPA的SSR需要Adobe I/O Runtime，这用于渲染应用程序内容服务器端。 在应用程序的HTL中，调用Adobe I/O Runtime上的资源来渲染内容。

正如AEM支持Angular和React SPA框架即装即用一样，Angular和React应用程序也支持服务器端渲染。 有关更多详细信息，请参阅这两个框架的NPM文档。

* React: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

有关简单化的示例，请参阅 [We.Retail Journal应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). 它呈现整个应用程序服务器端。 尽管这不是一个真实的例子，但它确实说明了实施SSR所需要的内容。

>[!CAUTION]
>
>的 [We.Retail Journal应用程序](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 仅用于演示目的，因此使用Node.js作为简单示例，而不是推荐的Adobe I/O Runtime。 不应将此示例用于任何项目工作。

>[!NOTE]
>
>任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在AEM中实施SPA SSR的推荐解决方案。

对于预先创建的AEM实例，还可以使用自定义Node.js实例来实施SSR，其方式与上述方法相同。 尽管Adobe支持此功能，但不建议这样做。

>[!NOTE]
>
>托管Adobe的AEM实例不支持Node.js。

>[!NOTE]
>
>如果SSR必须通过Node.js来实施，则Adobe建议为每个AEM环境（创作、发布、暂存等）使用单独的Node.js实例。

## 远程内容渲染器 {#remote-content-renderer}

的 [远程内容渲染器配置](#remote-content-renderer-configuration) AEM中的SPA与SSR结合使用时，需要点按到更广义的渲染服务，该服务可根据您的需求进行扩展和自定义。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是用于检索在远程服务器上呈现的内容的OSGi服务，例如从Adobe I/O。发送到远程服务器的内容基于传递的请求参数。

`RemoteContentRenderingService` 当需要进行其他内容处理时，可通过依赖关系反转插入自定义Sling模型或servlet中。

此服务由 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

的 `RemoteContentRendererRequestHandlerServlet` 可用于以编程方式设置请求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`，提供的默认请求处理程序实施，允许您创建多个OSGi配置，以将内容结构中的位置映射到远程端点。

要添加自定义请求处理程序，请实施 `RemoteContentRendererRequestHandler` 界面。 请务必设置 `Constants.SERVICE_RANKING` 组件属性更改为大于100的整数，这是 `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置默认处理程序的OSGi配置 {#configure-default-handler}

必须按照部分中的所述配置默认处理程序 [远程内容渲染器配置](#remote-content-renderer-configuration).

### 远程内容渲染器使用情况 {#usage}

要让Servlet获取并返回一些可插入页面的内容，请执行以下操作：

1. 确保远程服务器可访问。
1. 将以下代码片段之一添加到AEM组件的HTL模板。
1. （可选）创建或修改OSGi配置。
1. 浏览网站的内容

通常，页面组件的HTL模板是此类功能的主收件人。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

Servlet利用Sling模型导出程序序列化组件数据。 默认情况下， `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支持作为Sling模型适配器。 如有必要，您可以添加类，请求应修改为使用 `RemoteContentRendererServlet` 和实施 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 其他类必须扩展 `ComponentExporter`.
