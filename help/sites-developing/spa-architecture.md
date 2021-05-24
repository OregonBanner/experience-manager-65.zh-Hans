---
title: 开发SPA for AEM
seo-title: 开发SPA for AEM
description: 本文介绍了在让前端开发人员开发AEM的SPA时应考虑的重要问题，并概述了在部署AEM上开发的SPA时要记住的AEM与SPA的架构。
seo-description: 本文介绍了在让前端开发人员开发AEM的SPA时应考虑的重要问题，并概述了在部署AEM上开发的SPA时要记住的AEM与SPA的架构。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 1%

---

# 开发AEM的SPA{#developing-spas-for-aem}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而作者则希望在AEM中为使用此类框架构建的站点无缝编辑内容。

本文介绍了在让前端开发人员开发SPA for AEM时应考虑的重要问题，并概述了AEM在AEM上部署SPA的架构。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## SPA的AEM开发原则{#spa-development-principles-for-aem}

在AEM上开发单页应用程序时，假定前端开发人员在创建SPA时遵循标准的最佳实践。 如果作为前端开发人员，您遵循这些一般最佳实践以及一些特定于AEM的原则，那么您的SPA将能够与[AEM及其内容创作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)一起使用。

* **[可移植性](/help/sites-developing/spa-architecture.md#portability)  -** 与任何组件一样，组件应构建为尽可能便携。SPA应使用可移植且可重复使用的组件构建。
* **[AEM驱动站点结构](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  — 前端开发人员创建组件并拥有其内部结构，但依赖AEM来定义站点的内容结构。
* **[动态渲染](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  — 所有渲染应为动态。
* **[动态路由](#dynamic-routing)  -** SPA负责路由，AEM会侦听该路由并基于该路由获取。任何路由都应是动态的。

在开发SPA时，如果您牢记这些原则，那么在启用所有受支持的AEM创作功能时，将尽可能灵活地进行未来验证。

如果您不需要支持AEM创作功能，则可能需要考虑其他[SPA设计模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 便携性 {#portability}

与开发任何组件一样，您的组件的设计方式应最大限度地提高其可移植性。 任何与组件的可移植性或可重用性相抵触的模式都应避免，以确保今后的兼容性、灵活性和可维护性。

生成的SPA应使用高度可移植和可重复使用的组件构建。

### AEM驱动器站点结构{#aem-drives-site-structure}

前端开发人员必须认为自己负责创建用于构建应用程序的SPA组件库。 前端显影器对组件的内部结构具有完全的控制。 [但AEM始终拥有网站的结构。](/help/sites-developing/spa-overview.md)

这意味着前端开发人员可以在组件入口点之前或之后添加客户内容，还可以在组件内进行第三方调用。 但是，前端开发人员并不能完全控制组件的嵌套方式，例如。

### 动态渲染{#dynamic-rendering}

SPA应仅依赖于内容的动态渲染。 这是AEM获取并呈现内容结构所有子项的默认期望值。[](/help/sites-developing/spa-architecture.md#portability)

指向特定内容的任何显式渲染均被视为静态渲染，尽管受支持，但将与AEM内容创作功能不兼容。 这也违背了[可移植性](/help/sites-developing/spa-architecture.md#portability)的原则。

### 动态路由{#dynamic-routing}

与渲染一样，所有路由也应是动态的。 在AEM中， [SPA应始终拥有路由](/help/sites-developing/spa-routing.md),AEM侦听路由并基于路由获取内容。

任何静态路由都与可移植性](/help/sites-developing/spa-architecture.md#portability)的原则相抵触，并且由于与AEM的内容创作功能不兼容而限制了作者。 [例如，使用静态路由时，如果内容作者想要更改路由或更改页面，则他/她将必须要求前端开发人员执行此操作。

## AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应使用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## SPA设计模型{#spa-design-models}

如果遵循在AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)中开发SPA的[原则，则您的SPA将能够与所有受支持的AEM内容创作功能一起使用。[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

但是，在有些情况下，这并非完全必要。 下表概述了各种设计模型、其优点和缺点。

<table>
 <tbody>
  <tr>
   <th><strong>设计模型<br /> </strong></th>
   <th><strong>优势</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作无头CMS，而不使用<a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDK框架。</a></td>
   <td>前端开发人员完全控制应用程序。</td>
   <td><p>内容作者无法利用AEM内容创作体验。</p> <p>如果代码包含静态引用或路由，则该代码既不可移植，也不可重复使用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>前端开发人员使用SPA Editor SDK框架，但只向内容作者打开一些区域。</td>
   <td>开发人员只允许在应用程序的限制区域中进行创作，从而保持对应用程序的控制。</td>
   <td><p>内容作者仅受一组有限的AEM内容创作体验的限制。</p> <p>如果代码包含静态引用或路由，则它既不可移植，也不可重复使用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>项目可充分利用SPA Editor SDK，并且前端组件将开发为库，应用程序的内容结构将委派给AEM。</td>
   <td><p>该应用程序可重复使用且可移植。</p> <p>内容作者可以使用AEM内容创作体验编辑应用程序。<br /> </p> <p>SPA与模板编辑器兼容。</p> </td>
   <td><p>开发人员无法控制应用程序的结构和委派给AEM的内容部分。</p> <p>开发人员仍可以将应用程序的区域保留为不打算使用AEM创作的内容。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>尽管AEM支持所有模型，但只有通过实施第三个模型(从而遵循AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)中建议的[SPA开发原则)，内容作者才能像往常一样与AEM中的内容进行交互和编辑。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 将现有SPA迁移到AEM {#migrating-existing-spas-to-aem}

通常，如果您的SPA遵循AEM的[SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，则SPA将在AEM中工作，并且可以使用AEM SPA编辑器进行编辑。

按照以下步骤操作，使现有SPA可以随时使用AEM。

1. **将JS组件设为模块化。**

   使其能够按任意顺序、位置和大小呈现。
1. **使用我们的SDK提供的容器将您的组件放在屏幕上。**

   AEM提供了一个页面和段落系统组件供您使用。
1. **为每个JS组件创建一个AEM组件。**

   AEM组件定义对话框和JSON输出。

## 面向前端开发人员的说明{#instructions-for-front-end-developers}

让前端开发人员为AEM创建SPA的主要任务是就组件及其JSON模型达成一致。

以下是前端开发人员在开发SPA for AEM时需要遵循的步骤概要。

1. **同意组件及其JSON模型**

   前端开发人员和后端AEM开发人员需要就哪些组件是必需的以及模型达成一致，以便从SPA组件到后端组件之间实现一对一的匹配。

   AEM组件在提供编辑对话框和导出组件模型时仍然是必需的。

1. **在React组件中，通过`this.props.cqModel`**

   在同意组件并且JSON模型到位后，前端开发人员可以免费开发SPA，只需通过`this.props.cqModel`访问JSON模型即可。

1. **实现组件的方 `render()` 法**

   前端开发人员按照其认为合适的方式实施`render()`方法，并且可以使用`cqModel`属性的字段。 这会输出将插入页面的DOM和HTML片段。 这是在React中构建应用程序的标准方式。

1. **通过将组件映射到AEM资源类型`MapTo()`**

   该映射存储组件类，并由提供的`Container`组件在内部使用，以基于给定的资源类型检索和动态实例化组件。

   它用作前端和后端之间的“胶水”，以便编辑器了解反应组件对应的组件。

   `Page`和`ResponsiveGrid`是扩展基`Container`的类的好示例。

1. **将组件的定义为 `EditConfig` 参数以`MapTo()`**

   此参数对于告知编辑器组件在尚未渲染或没有要渲染的内容时应该如何命名。

1. **为页面和容 `Container` 器扩展提供的类**

   页面和段落系统应扩展此类，以便委派给内部组件可以按预期工作。

1. **实施使用HTML5 API的路由解决 `History` 方案。**

   启用`ModelRouter`后，调用`pushState`和`replaceState`函数将触发对`PageModelManager`的请求，以获取模型的缺失片段。

   `ModelRouter`的当前版本仅支持使用指向Sling模型入口点实际资源路径的URL。 它不支持使用虚URL或别名。

   可以禁用或配置`ModelRouter`以忽略正则表达式列表。

## 与AEM无关的{#aem-agnostic}

这些代码块说明了您的React和Angular组件不需要任何特定于Adobe或AEM的内容。

* JavaScript组件内的所有内容都与AEM无关。
* 但是，AEM的特定功能是，JS组件必须通过MapTo帮助程序映射到AEM组件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo`帮助程序是“胶水”，它允许后端组件和前端组件匹配在一起：

* 它可告知JS容器（或JS段落系统），JS组件负责渲染JSON中存在的每个组件。
* 它会向JS组件呈现的HTML中添加HTML数据属性，以便SPA编辑器知道在编辑组件时要向作者显示的对话框。

有关一般使用`MapTo`并构建SPA for AEM的更多信息，请参阅所选框架的快速入门指南。

* [AEM - React中的SPA快速入门](/help/sites-developing/spa-getting-started-react.md)
* [AEM SPA快速入门 — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM架构和SPA {#aem-architecture-and-spas}

使用SPA时，AEM的常规架构（包括开发、创作和发布环境）不会发生更改。 但是，了解SPA开发如何融入此架构将会有所帮助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **构建环境**

   这是签出SPA应用程序源和组件源的源位置。

   * NPM clientlib生成器从SPA项目创建客户端库。
   * 该库将由Maven获取，并由Maven Build插件以及组件一起部署到AEM Author。

* **AEM Author**

   内容是在AEM作者上创建的，包括创作SPA。

   在创作环境中使用SPA编辑器编辑SPA时：

   1. SPA请求外部HTML。
   1. 将加载CSS。
   1. 将加载SPA应用程序的Javascript。
   1. 执行SPA应用程序时，将请求JSON，从而允许应用程序构建页面的DOM，其中包括`cq-data`属性。
   1. 此`cq-data`属性允许编辑器加载其他页面信息，以便它知道组件可以使用哪些编辑配置。

* **AEM 发布**

   这是发布创作内容和编译的库(包括SPA应用程序对象、clientlib和组件)以供公众使用的地方。

* **Dispatcher/CDN**

   调度程序用作网站访客的AEM缓存层。

   * 处理请求的方式与在AEM作者中类似，但是没有对页面信息提出请求，因为只有编辑者才需要这样做。
   * Javascript、CSS、JSON和HTML已缓存，可优化页面以便快速交付。

>[!NOTE]
>
>在AEM中，无需执行Javascript构建机制或执行Javascript本身。 AEM仅托管SPA应用程序中的已编译工件。

## 后续步骤{#next-steps}

有关AEM中简单SPA的结构方式及其工作方式的概述，请参阅[React](/help/sites-developing/spa-getting-started-react.md)和[Angular](/help/sites-developing/spa-getting-started-angular.md)的快速入门指南。

有关创建您自己的SPA的分步指南，请参阅[AEM SPA编辑器入门 — WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关动态模型到组件映射以及它如何在AEM的SPA中工作的更多详细信息，请参阅文章[Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为React或Angular以外的框架实施SPA，或者只想深入了解SPA SDK for AEM的工作方式，请参阅[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
