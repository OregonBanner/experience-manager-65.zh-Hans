---
title: 为AEM开发SPA
seo-title: 为AEM开发SPA
description: 本文介绍了在使前端开发人员开发SPA AEM时应考虑的重要问题，并概述了AEM的体系结构，在部署已开发的SPA  AEM时要记住的SPA。
seo-description: 本文介绍了在使前端开发人员开发SPA AEM时应考虑的重要问题，并概述了AEM的体系结构，在部署已开发的SPA  AEM时要记住的SPA。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 0%

---


# 开发SPA for AEM{#developing-spas-for-aem}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望无缝编辑AEM中的内容，以便使用此类框架构建站点。

本文介绍了在让前端开发者开发SPA for AEM时应考虑的重要问题，并概述了AEM的体系结构以及部署SPA on AEM的方法。

>[!NOTE]
>
>SPA编辑器是需要SPA框架的客户端渲染（例如，React或Angular）的项目的推荐解决方案。

## SPA{#spa-development-principles-for-aem}的AEM开发原则

在AEM上开发单页应用程序时，假定前端开发人员在创建SPA时遵循标准最佳做法。 如果您作为前端开发者，遵循这些一般的最佳实践以及AEM特定的一些原则，SPA将能够与[AEM及其内容创作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)一起发挥作用。

* **[可移植](/help/sites-developing/spa-architecture.md#portability) -** 与任何组件一样，组件应构建为尽可能便携。SPA应使用可移植、可重用的组件构建。
* **[AEM驱动站点结构](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** -前端开发人员创建组件并拥有其内部结构，但依赖AEM定义站点的内容结构。
* **[动态渲染](/help/sites-developing/spa-architecture.md#dynamic-rendering)** -所有渲染应为动态渲染。
* **[动态路由](#dynamic-routing) -** SPA负责路由和AEM监听它并基于它获取。任何路由也应该是动态的。

如果您在开发SPA时牢记这些原则，它将尽可能灵活和将来验证，同时启用所有受支持的AEM创作功能。

如果您不需要支持AEM创作功能，则可能需要考虑不同的[SPA设计模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 移植{#portability}

与开发任何组件一样，您的组件的设计方式应最大限度地提高其可移植性。 任何与组件的可移植性或可重用性相抵触的模式都应避免，以确保今后的兼容性、灵活性和可维护性。

最终的SPA应使用高度可移植和重用的组件构建。

### AEM驱动器站点结构{#aem-drives-site-structure}

前端开发人员必须认为自己负责创建用于构建应用程序的SPA组件库。 前端开发者完全控制组件的内部结构。 [但AEM始终拥有该站点的结构。](/help/sites-developing/spa-overview.md)

这意味着前端开发人员可以在组件入口点之前或之后添加客户内容，还可以在组件内进行第三方呼叫。 但是，前端开发人员并不完全控制组件的嵌套方式，例如。

### 动态渲染{#dynamic-rendering}

SPA只应依赖内容的动态呈现。 这是AEM获取和呈现内容结构的所有子级的默认期望。[](/help/sites-developing/spa-architecture.md#portability)

任何指向特定内容的显式渲染均视为静态渲染，尽管受支持，但与AEM内容创作功能不兼容。 这也违背了[可移植性](/help/sites-developing/spa-architecture.md#portability)的原则。

### 动态路由{#dynamic-routing}

与渲染一样，所有路由也应是动态的。 在AEM中，[SPA应始终拥有路由](/help/sites-developing/spa-routing.md)并AEM监听它并基于它获取内容。

任何静态路由均与可移植性[原则相抵触，并且与AEM的内容创作功能不兼容，从而限制了作者。 ](/help/sites-developing/spa-architecture.md#portability)例如，使用静态路由时，如果内容作者希望更改路由或更改页面，则他／她必须要求前端开发人员完成此操作。

## AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应利用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并利用SPA SDK。

## SPA设计模型{#spa-design-models}

如果遵循在AEM中开发SPA的[原则，则您的SPA将可以与所有支持的AEM内容创作功能一起使用。[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

然而，在有些情况下，这并非完全必要。 下表概述了各种设计模型、它们的优点和缺点。

<table>
 <tbody>
  <tr>
   <th><strong>设计模型<br /> </strong></th>
   <th><strong>优势</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作无外设CMS，而不使用<a href="/help/sites-developing/spa-reference-materials.md">SPA编辑器SDK框架。</a></td>
   <td>前端开发人员完全控制应用程序。</td>
   <td><p>内容作者无法利用AEM内容创作体验。</p> <p>如果代码包含静态引用或路由，则它既不可移植，也不可重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>前端开发人员使用SPA Editor SDK框架，但只向内容作者打开部分区域。</td>
   <td>开发人员只在应用程序的受限区域中启用创作，从而保持对应用程序的控制。</td>
   <td><p>内容作者仅限于有限的AEM内容创作体验集。</p> <p>如果代码包含静态引用或路由，则它既不可移植，也不可重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>项目完全利用SPA Editor SDK，前端组件作为库进行开发，应用程序的内容结构委托给AEM。</td>
   <td><p>该应用程序可重用、可移植。</p> <p>内容作者可以使用AEM内容创作体验编辑应用程序。<br /> </p> <p>SPA与模板编辑器兼容。</p> </td>
   <td><p>开发人员无法控制应用程序的结构以及委派给AEM的内容部分。</p> <p>开发人员仍然可以为不打算使用AEM创作的内容保留应用程序的区域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>尽管AEM支持所有模型，但只有通过实施第三种模式(并因此遵循AEM&lt;a](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)中建议的[SPA开发原则)，内容作者才能与SPA中的内容进行交互并编辑它们习惯的内容。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 将现有SPA迁移到AEM {#migrating-existing-spas-to-aem}

通常，如果SPA遵循AEM的[SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，则SPA将在AEM中工作，并可使用AEM编辑器进行编辑。

按照以下步骤操作，使现有SPA可以与AEM一起使用。

1. **使JS组件模块化。**

   使它们能够按任何顺序、位置和大小进行渲染。
1. **使用我们的SDK提供的容器将您的组件放在屏幕上。**

   AEM提供供您使用的页面和段落系统组件。
1. **为每个JS组件创建AEM组件。**

   AEM组件定义对话框和JSON输出。

## 前端开发人员的说明{#instructions-for-front-end-developers}

引导前端开发人员创建AEM的主要任务是同意组件及其JSON模型。

下面概述了前端开发人员在开发SPA for AEM时需要遵循的步骤。

1. **同意组件及其JSON模型**

   前端开发人员和后端AEM开发人员需要商定哪些组件是必需的以及一个模型，以便从SPA组件到后端组件实现一对一匹配。

   AEM组件在提供编辑对话框和导出组件模型时仍然很有必要。

1. **在React组件中，通过`this.props.cqModel`**

   在商定组件并部署JSON模型后，前端开发人员可以免费开发SPA，只需通过`this.props.cqModel`访问JSON模型。

1. **实现组件的方 `render()` 法**

   前端开发者按照自己认为合适的方式实施`render()`方法，并可以使用`cqModel`属性的字段。 这将输出将插入页面的DOM和HTML片段。 这是在React中构建应用程序的标准方式。

1. **通过`MapTo()`**

   映射存储组件类，并由提供的`Container`组件在内部使用，以基于给定的资源类型检索和动态实例化组件。

   它用作前端和后端之间的“胶水”，以便编辑者知道反应组件对应的组件。

   `Page`和`ResponsiveGrid`是扩展基`Container`的类的好示例。

1. **将组件定义 `EditConfig` 为参数`MapTo()`**

   此参数是告知编辑者如何命名组件（只要尚未渲染或没有要渲染的内容）的必需参数。

1. **为页面和 `Container` 容器扩展提供的类**

   页面和段落系统应扩展此类，以使委派到内部组件正常工作。

1. **实施使用HTML5 API的路由解决 `History` 方案。**

   启用`ModelRouter`后，调用`pushState`和`replaceState`函数将触发对`PageModelManager`的请求，以获取模型的缺失片段。

   `ModelRouter`的当前版本仅支持使用指向Sling Model入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

   可以禁用`ModelRouter`或将&lt;a0/>配置为忽略常规列表。

## AEM-不可知{#aem-agnostic}

这些代码块说明您的React和Angular组件无需任何特定于Adobe或AEM的内容。

* JavaScript组件中的所有内容都与AEM无关。
* 但是，AEM的特有特点是，JS组件必须映射到具有MapTo帮助程序的AEM组件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo`帮助程序是允许后端和前端组件相匹配的“粘合剂”:

* 它告诉JS容器（或JS段落系统）JS组件负责呈现JSON中存在的每个组件。
* 它向JS组件呈现的HTML中添加HTML数据属性，这样SPA Editor就知道在编辑组件时向作者显示什么对话框。

有关一般使用`MapTo`和构建SPA for AEM的详细信息，请参阅所选框架的入门指南。

* [SPA AEM入门——反应](/help/sites-developing/spa-getting-started-react.md)
* [SPA AEM入门——角度](/help/sites-developing/spa-getting-started-angular.md)

## AEM体系结构和SPA {#aem-architecture-and-spas}

AEM的一般架构(包括开发、创作和发布环境)在使用SPA时不会发生变化。 但是，了解SPA开发如何适合此体系架构是有帮助的。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **构建环境**

   这是检出SPA应用程序源和组件源的源的位置。

   * NPM clientlib生成器从SPA项目创建客户端库。
   * 该库将由Maven使用，并由Maven Build插件以及组件部署到AEM作者。

* **AEM Author**

   内容是在AEM作者(包括创作SPA)上创建的。

   当SPA在创作环境中使用SPA编辑器进行编辑时：

   1. SPA请求外部HTML。
   1. CSS已加载。
   1. 已加载SPA应用程序的Javascript。
   1. 执行SPA应用程序时，将请求JSON，允许应用程序构建页面的DOM，包括`cq-data`属性。
   1. 此`cq-data`属性允许编辑器加载其他页面信息，以便它知道组件可以使用哪些编辑配置。

* **AEM 发布**

   这是创作内容和编译库(包括SPA应用程序对象、clientlibs和组件)的发布位置，用于公开使用。

* **调度程序/CDN**

   调度程序充当AEM的缓存层，访客到站点。

   * 处理请求的方式与在AEM作者处理请求的方式类似，但是没有请求页面信息，因为这只是编辑者需要的。
   * Javascript、CSS、JSON和HTML已缓存，可优化页面以快速投放。

>[!NOTE]
>
>在AEM中，无需执行Javascript构建机制或执行Javascript本身。 AEM仅托管SPA应用程序中的已编译对象。

## 后续步骤{#next-steps}

有关AEM中简单SPA的结构及其工作原理的概述，请参见[React](/help/sites-developing/spa-getting-started-react.md)和[Angular](/help/sites-developing/spa-getting-started-angular.md)的入门指南。

有关创建自己的SPA的分步指南，请参阅[AEM SPA编辑器入门- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关动态模型到组件映射以及它在AEM中的工作方式的更多详细信息，请参阅文章[SPA的动态模型到组件映射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中实施SPA以实现除React或Angular之外的框架，或只想深入了解AEM SDK for SPA的工作方式，请参阅[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
