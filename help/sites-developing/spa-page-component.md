---
title: SPA 页面组件
seo-title: SPA Page Component
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。
seo-description: In an SPA the page component doesn't provide the HTML elements of its child components, but instead delegates this to the SPA framework. This document explains how this makes the page component of an SPA unique.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 17c198c744111753ffffcc0758f98859524c964e
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 3%

---

# SPA 页面组件{#spa-page-component}

在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 本文档介绍如何使SPA的页面组件具有唯一性。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 简介 {#introduction}

SPA的HTML组件不会通过JSP或HTL文件和资源对象提供其子组件的页面元素。 此操作将委派给SPA框架。 子组件的表示形式将作为JSON数据结构（即模型）获取。 然后，将根据提供的JSON模型，将SPA组件添加到页面。 因此，页面组件初始主体构成与其预呈现的HTML对应体不同。

## 页面模型管理 {#page-model-management}

页面模型之解决方案及管理乃委派予提供 [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 模块。 SPA必须与 `PageModelManager` 模块，以获取初始页面模型并注册模型更新 — 大多数情况下，作者通过页面编辑器编辑页面时会生成该模块。 的 `PageModelManager` 可由SPA项目作为npm包访问。 作为AEM和SPA之间的解释器， `PageModelManager` 将随SPA一起使用。

要允许创作页面，客户端库名为 `cq.authoring.pagemodel.messaging` 必须添加才能在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件从页面wcm/核心组件继承，则可以使用以下选项来 `cq.authoring.pagemodel.messaging` 客户端库类别可用：

* 如果模板是可编辑的，请将客户端库类别添加到页面策略中。
* 使用 `customfooterlibs.html` 的子目录访问。

不要忘记限制 `cq.authoring.pagemodel.messaging` 类别。

## 通信数据类型 {#communication-data-type}

通信数据类型在AEM页面组件中使用 `data-cq-datatype` 属性。 将通信数据类型设置为JSON时，GET请求会命中组件的Sling模型端点。 在页面编辑器中发生更新后，更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会向SPA发出更新警告。

**SPA 页面组件 -`body.html`**

```
<div id="page"></div>
```

除了作为不延迟生成DOM的最佳实践之外，SPA框架还要求在主体末尾添加脚本。

**SPA 页面组件 -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA内容的元资源属性：

**SPA 页面组件 -`customheaderlibs.html`**

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
* `cq:pagemodel_root_url`:应用程序根模型的URL。 直接访问子页面时至关重要，因为子页面模型是应用程序根模型的片段。 的 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 然后系统地将应用程序初始模型重新组合为从其根入口点进入应用程序。

* `cq:pagemodel_router`:启用或禁用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 的 `PageModelManager` 库

* `cq:pagemodel_route_filters`:用于提供路由的逗号分隔列表或正则表达式 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 必须忽略。

>[!CAUTION]
>
>本文档仅将We.Retail Journal应用程序用于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应利用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用SPA或Angular的SPA项目并利用SPA SDK。AEM上的所有项目都应基于SPA Starter Kit的Maven Archetype。

## 页面编辑器叠加同步 {#page-editor-overlay-synchronization}

叠加的同步由提供的相同的突变观测器保证 `cq.authoring.page` 类别。

## Sling模型JSON导出的结构配置 {#sling-model-json-exported-structure-configuration}

启用路由功能后，假设由于AEM导航组件的JSON导出，SPA的JSON导出包含不同的应用程序路由。 可以通过以下两个属性在AEM根页面内容策略中配置SPA导航组件的JSON输出：

* `structureDepth`:与导出的树深度对应的编号
* `structurePatterns`:与要导出的页面对应的regex数组的正则表达式

这可以显示在的SPA示例内容中 `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
