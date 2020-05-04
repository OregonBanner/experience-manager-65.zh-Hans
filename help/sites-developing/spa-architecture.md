---
title: 为AEM开发SPA
seo-title: 为AEM开发SPA
description: 本文介绍了在使前端开发人员参与为AEM开发SPA时应考虑的重要问题，并概述了在AEM上部署开发的SPA时应牢记的AEM的SPA架构。
seo-description: 本文介绍了在使前端开发人员参与为AEM开发SPA时应考虑的重要问题，并概述了在AEM上部署开发的SPA时应牢记的AEM的SPA架构。
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# 为AEM开发SPA{#developing-spas-for-aem}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，作者希望在AEM中为使用此类框架构建的站点无缝编辑内容。

本文介绍了在让前端开发人员为AEM开发SPA时要考虑的重要问题，并概述了AEM在AEM上部署SPA的架构。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## AEM的SPA开发原则 {#spa-development-principles-for-aem}

在AEM上开发单页应用程序时，假定前端开发人员在创建SPA时遵循标准最佳实践。 如果您作为前端开发人员，遵循以下一般最佳实践以及少数特定于AEM的原则，您的SPA将能够与AEM及其 [内容创作功能一起正常运行](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)。

* **[可移植](/help/sites-developing/spa-architecture.md#portability)-**与任何组件一样，组件应构建为尽可能便携。 SPA应使用可移植、可重用的组件。
* **[AEM Drives Site](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**Structure —— 前端开发人员创建组件并拥有其内部结构，但依赖AEM定义站点的内容结构。
* **[动态渲染](/help/sites-developing/spa-architecture.md#dynamic-rendering)**-所有渲染应为动态渲染。
* **[动态路由](#dynamic-routing)-**SPA负责路由,AEM会监听该并基于其获取。 任何路由也应该是动态的。

如果您在开发SPA时牢记这些原则，它将尽可能灵活和在将来验证，同时启用所有受支持的AEM创作功能。

如果您不需要支持AEM创作功能，则可能需要考虑其他 [SPA设计模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 便携性 {#portability}

与开发任何组件一样，您的组件的设计方式应最大限度地提高其可移植性。 任何与组件的可移植性或可重用性相抵触的模式都应避免，以确保今后的兼容性、灵活性和可维护性。

最终的SPA应使用高度可移植和可重复使用的组件。

### AEM驱动器站点结构 {#aem-drives-site-structure}

前端开发人员必须认为自己负责创建用于构建应用程序的SPA组件库。 前端开发者完全控制组件的内部结构。 [但是，AEM始终拥有该站点的结构。](/help/sites-developing/spa-overview.md)

这意味着前端开发人员可以在组件入口点之前或之后添加客户内容，还可以在组件内进行第三方呼叫。 但是，前端开发人员并不完全控制组件的嵌套方式，例如。

### 动态渲染 {#dynamic-rendering}

SPA应仅依赖内容的动态呈现。 这是AEM获取和呈现内容结构的所有子项的默认期望值。 [](/help/sites-developing/spa-architecture.md#portability)

任何指向特定内容的显式渲染均视为静态渲染，尽管受支持，但与AEM的内容创作功能不兼容。 这也违背了便携性 [原则](/help/sites-developing/spa-architecture.md#portability)。

### 动态路由 {#dynamic-routing}

与渲染一样，所有路由也应是动态的。 在AEM中， [SPA应始终拥有路由](/help/sites-developing/spa-routing.md) ,AEM将监听该并基于其获取内容。

任何静态路由均 [违反可移植性原则](/help/sites-developing/spa-architecture.md#portability) ，并且与AEM的内容创作功能不兼容，从而限制了作者。 例如，使用静态路由时，如果内容作者希望更改路由或更改页面，则他／她必须要求前端开发人员完成此操作。

## AEM 项目原型 {#aem-project-archetype}

任何AEM项目都应利 [用AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，该原型支持使用React或Angular的SPA项目并利用SPA SDK。

## SPA设计模型 {#spa-design-models}

如果遵循 [了在AEM中开发SPA的原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) ，则您的SPA将能够与所有受支持的AEM内容创作功能一起正常工作。 [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

然而，在有些情况下，这并非完全必要。 下表概述了各种设计模型、它们的优点和缺点。

<table>
 <tbody>
  <tr>
   <th><strong>设计模型<br /> </strong></th>
   <th><strong>优势</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作无外设CMS，无需使 <a href="/help/sites-developing/spa-reference-materials.md">用SPA编辑器SDK框架。</a></td>
   <td>前端开发人员完全控制应用程序。</td>
   <td><p>内容作者无法利用AEM的内容创作体验。</p> <p>如果代码包含静态引用或路由，则它既不可移植，也不可重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>前端开发人员使用SPA Editor SDK框架，但只向内容作者打开部分区域。</td>
   <td>开发人员只在应用程序的受限区域中启用创作，从而保持对应用程序的控制。</td>
   <td><p>内容作者仅限于有限的AEM内容创作体验集。</p> <p>如果代码包含静态引用或路由，则它既不可移植，也不可重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>项目完全利用SPA Editor SDK，前端组件作为库进行开发，应用程序的内容结构委托给AEM。</td>
   <td><p>该应用程序可重用、可移植。</p> <p>内容作者可以使用AEM的内容创作体验编辑应用程序。<br /> </p> <p>SPA与模板编辑器兼容。</p> </td>
   <td><p>开发人员无法控制应用程序的结构和委托给AEM的内容部分。</p> <p>开发人员仍可为非要使用AEM创作的内容保留应用程序的区域。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>尽管AEM中支持所有模型，但只有通过实施第三种模型(并因此遵循AEM中推荐的 [SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))，内容作者才能在AEM中与SPA内容进行交互并编辑它们所习惯的内容。
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## 将现有SPA迁移到AEM {#migrating-existing-spas-to-aem}

通常，如果您的SPA遵 [循AEM的SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，则您的SPA将在AEM中工作，并可使用AEM SPA编辑器进行编辑。

按照以下步骤操作，使您的现有SPA可以随时与AEM一起使用。

1. **使JS组件模块化。**

   使它们能够按任何顺序、位置和大小进行渲染。
1. **使用我们的SDK提供的容器将您的组件放在屏幕上。**

   AEM提供供您使用的页面和段落系统组件。
1. **为每个JS组件创建AEM组件。**

   AEM组件定义对话框和JSON输出。

## 前端开发人员的说明 {#instructions-for-front-end-developers}

吸引前端开发人员为AEM创建SPA的主要任务是同意组件及其JSON模型。

以下概述了前端开发人员在为AEM开发SPA时需要遵循的步骤。

1. **同意组件及其JSON模型**

   前端开发人员和后端AEM开发人员需要商定哪些组件是必需的以及一个模型，这样SPA组件与后端组件之间就会有一对一的匹配。

   AEM组件在提供编辑对话框和导出组件模型时仍是必需的。

1. **在React组件中，通过`this.props.cqModel`**

   在商定组件并且JSON模型就位后，前端开发人员可以免费开发SPA，只需通过访问JSON模型即可 `this.props.cqModel`。

1. **实现组件的方`render()`法**

   前端开发者根据他／她 `render()` 认为合适的方法实施该方法，并可以使用属性的 `cqModel` 字段。 这将输出将插入页面的DOM和HTML片段。 这是在React中构建应用程序的标准方式。

1. **通过`MapTo()`**

   该映射存储组件类，并且由提供的组件在内部使用， `Container` 以基于给定的资源类型检索和动态地实例化组件。

   它用作前端和后端之间的“胶水”，以便编辑者知道反应组件对应的组件。

   和 `Page` 是 `ResponsiveGrid` 扩展基的类的好示例 `Container`。

1. **将组件定义`EditConfig`为参数以`MapTo()`**

   此参数是告知编辑者如何命名组件（只要尚未渲染或没有要渲染的内容）的必需参数。

1. **为页面`Container`和容器扩展提供的类**

   页面和段落系统应扩展此类，以使委派到内部组件正常工作。

1. **实施使用HTML5 API的路由解决`History`方案。**

   启用 `ModelRouter` 后，调用和 `pushState` 函数 `replaceState` 将触发请求， `PageModelManager` 以获取模型的缺失片段。

   当前版本仅支 `ModelRouter` 持使用指向Sling Model入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

   可以 `ModelRouter` 禁用或配置忽略常规表达式的列表。

## 与AEM无关 {#aem-agnostic}

这些代码块说明您的React和Angular组件不需要任何特定于Adobe或AEM的内容。

* JavaScript组件中的所有内容都与AEM无关。
* 但是，AEM的特定功能是，JS组件必须使用MapTo帮助程序映射到AEM组件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

帮 `MapTo` 助程序是“粘合剂”，它允许后端和前端组件相匹配：

* 它告诉JS容器（或JS段落系统）JS组件负责呈现JSON中存在的每个组件。
* 它会向JS组件呈现的HTML添加HTML数据属性，以便SPA编辑器知道在编辑组件时向作者显示什么对话框。

有关使用和构 `MapTo` 建适用于AEM的SPA的详细信息，请参阅所选框架的入门指南。

* [AEM中SPA快速入门——反应](/help/sites-developing/spa-getting-started-react.md)
* [AEM中SPA快速入门——角度](/help/sites-developing/spa-getting-started-angular.md)

## AEM架构和SPA {#aem-architecture-and-spas}

AEM的常规架构(包括开发、创作和发布环境)在使用SPA时不会更改。 但是，了解SPA开发如何适合此体系架构是很有帮助的。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **构建环境**

   这是检出SPA应用程序源和组件源的源。

   * NPM clientlib生成器从SPA项目创建客户端库。
   * 该库将由Maven使用，并由Maven Build插件以及组件部署到AEM作者。

* **AEM Author**

   内容是在AEM作者上创建的，包括创作SPA。

   当使用创作环境上的SPA编辑器编辑SPA时：

   1. SPA请求外部HTML。
   1. CSS已加载。
   1. 加载SPA应用程序的Javascript。
   1. 执行SPA应用程序时，会请求JSON，使应用程序能够构建页面的DOM，包括属 `cq-data` 性。
   1. 此属 `cq-data` 性允许编辑者加载其他页面信息，以便知道组件可以使用哪些编辑配置。

* **AEM 发布**

   这是创作内容和编译库（包括SPA应用程序对象、clientlibs和组件）的发布位置，以供公众使用。

* **调度程序/CDN**

   调度程序充当AEM的缓存层，供访客访问站点。

   * 处理请求的方式与在AEM作者处理请求的方式类似，但是没有请求页面信息，因为这只是编辑者需要的。
   * Javascript、CSS、JSON和HTML已缓存，可优化页面以快速投放。

>[!NOTE]
>
>在AEM中，无需执行Javascript构建机制或执行Javascript本身。 AEM仅托管SPA应用程序中的已编译对象。

## 后续步骤 {#next-steps}

有关AEM中简单SPA的结构及其工作方式的概述，请参阅React和Angular的入 [门指](/help/sites-developing/spa-getting-started-react.md) 南 [](/help/sites-developing/spa-getting-started-angular.md)。

有关创建您自己的SPA的分步指南，请参 [阅AEM SPA编辑器入门- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关动态模型到组件映射以及它在AEM中的SPA中的工作方式的更多详细信息，请参 [阅SPA的动态模型到组件映射文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为React或Angular之外的框架实施SPA，或只是希望深入了解AEM的SPA SDK的工作方式，请参阅 [SPA Blueprint文章](/help/sites-developing/spa-blueprint.md) 。
