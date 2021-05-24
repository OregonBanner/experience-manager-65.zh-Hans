---
title: SPA页面组件
seo-title: SPA页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。
seo-description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# SPA页面组件{#spa-page-component}

在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 简介 {#introduction}

SPA的页面组件不会通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作将委派给SPA框架。 子组件的表示形式将作为JSON数据结构（即模型）获取。 然后，将根据提供的JSON模型，将SPA组件添加到页面。 因此，页面组件初始主体组合与预呈现的HTML对应组合不同。

## 页面模型管理{#page-model-management}

页面模型的解析和管理被委派给提供的[ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)模块。 当SPA初始化以获取初始页面模型并注册模型更新时，它必须与`PageModelManager`模块进行交互 — 大多数情况下，当作者通过页面编辑器编辑页面时会生成该模块。 `PageModelManager`可由SPA项目作为npm包访问。 `PageModelManager`是AEM和SPA之间的解释器，适用于随SPA一起使用。

要创作页面，必须添加名为`cq.authoring.pagemodel.messaging`的客户端库，以在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件从页面wcm/core组件继承，则可以使用以下选项来使`cq.authoring.pagemodel.messaging`客户端库类别可用：

* 如果模板是可编辑的，请将客户端库类别添加到页面策略中。
* 使用页面组件的`customfooterlibs.html`添加客户端库类别。

请不要忘记将`cq.authoring.pagemodel.messaging`类别的包含限制为页面编辑器的上下文。

## 通信数据类型{#communication-data-type}

通信数据类型在AEM页面组件中使用`data-cq-datatype`属性设置一个HTML元素。 将通信数据类型设置为JSON时，GET请求会命中组件的Sling模型端点。 在页面编辑器中发生更新后，更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会向SPA发出更新警告。

**SPA页面组件 —`body.html`**

```
<div id="page"></div>
```

除了作为不延迟生成DOM的最佳实践之外，SPA框架还要求在主体末尾添加脚本。

**SPA页面组件 —`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA内容的元资源属性：

**SPA页面组件 —`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>在请求元件的Sling模型表示时，会静态设置默认模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`:编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`:应用程序根模型的URL。直接访问子页面时至关重要，因为子页面模型是应用程序根模型的片段。 然后，` [PageModelManager](/help/sites-developing/spa-page-component.md)`系统地将应用程序初始模型重新组合为从其根入口点进入应用程序。

* `cq:pagemodel_router`:启用或禁用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 库的 `PageModelManager` 功能

* `cq:pagemodel_route_filters`:以逗号分隔的列表或正则表达式来提供必须忽略 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 的路由。

>[!CAUTION]
>
>本文档仅将We.Retail Journal应用程序用于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应使用[AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，该原型支持使用React或Angular的SPA项目并利用SPA SDK。AEM上的所有SPA项目都应基于SPA Starter Kit的Maven原型。

## 页面编辑器叠加同步{#page-editor-overlay-synchronization}

由`cq.authoring.page`类提供的相同变异观测器保证叠加的同步。

## Sling模型JSON导出的结构配置{#sling-model-json-exported-structure-configuration}

启用路由功能后，假设由于AEM导航组件的JSON导出，SPA的JSON导出包含不同的应用程序路由。 可以通过以下两个属性在AEM根页面内容策略中配置SPA导航组件的JSON输出：

* `structureDepth`:与导出的树深度对应的编号
* `structurePatterns`:与要导出的页面对应的regex数组的正则表达式

这可以显示在`/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`的SPA示例内容中。
