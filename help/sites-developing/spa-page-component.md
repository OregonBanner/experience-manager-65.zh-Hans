---
title: SPA 页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA Framework。 本文档将说明如何使SPA的页面组件具有唯一性。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 8%

---

# SPA 页面组件{#spa-page-component}

在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派给SPA Framework。 本文档将说明如何使SPA的页面组件具有唯一性。

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA Framework的客户端渲染(例如React或Angular)的项目。

## 简介 {#introduction}

SPA的页面组件不通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作将委派给 SPA 框架。子组件的表示形式作为JSON数据结构（即模型）获取。 然后，根据提供的JSON模型将SPA组件添加到页面。 因此，页面组件初始正文构成不同于其预渲染的HTML对应内容。

## 页面模型管理 {#page-model-management}

页面模型的决议和管理委托给提供的用户。 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 模块。 SPA必须与 `PageModelManager` 模块，用于初始化获取初始页面模型并注册模型更新 — 大多在作者通过页面编辑器编辑页面时生成。 此 `PageModelManager` 可由SPA项目作为npm包访问。 作为AEM和SPA之间的解释者， `PageModelManager` 旨在伴随SPA。

要允许创作页面，请名为的客户端库 `cq.authoring.pagemodel.messaging` 必须添加以在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件继承自页面wcm/核心组件，则可以使用以下选项来将 `cq.authoring.pagemodel.messaging` 可用的客户端库类别：

* 如果模板可编辑，请将客户端库类别添加到页面策略中。
* 使用添加客户端库类别 `customfooterlibs.html` 页面组件的。

不要忘记限制包含 `cq.authoring.pagemodel.messaging` 类别到页面编辑器上下文的链接。

## 通信数据类型 {#communication-data-type}

使用在AEM Page组件中设置HTML元素来设置通信数据类型 `data-cq-datatype` 属性。 当通信数据类型设置为JSON时，GET请求会命中组件的Sling模型端点。 在页面编辑器中执行更新后，已更新组件的 JSON 表示形式将发送到页面模型库。然后，页面模型库会向SPA发出更新警告。

**SPA 页面组件 -`body.html`**

```
<div id="page"></div>
```

除了是不延迟DOM生成的良好做法之外，SPA框架还要求在正文末尾添加脚本。

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
>请求组件的Sling模型表示时，将静态设置默认模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`：编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`：应用程序根模型的URL。 由于子页面模型是应用程序根模型的片段，因此直接访问子页面时至关重要。 此 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 然后，在从应用程序根入口点进入应用程序时，系统地重组应用程序初始模型。

* `cq:pagemodel_router`：启用或禁用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 的 `PageModelManager` 库

* `cq:pagemodel_route_filters`：逗号分隔列表或正则表达式，用于提供路由 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 必须忽略。

>[!CAUTION]
>
>本文档仅将We.Retail日志应用程序用于演示目的。 请勿用于任何项目工作。
>
>任何AEM项目都应使用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用React或Angular的SPA项目并使用SPA SDK。AEM上的所有SPA项目都应基于Maven Archetype for SPA Starter Kit。

## 页面编辑器叠加同步 {#page-editor-overlay-synchronization}

叠加的同步由提供的完全相同的变异观察器来保证 `cq.authoring.page` 类别。

## Sling模型JSON导出结构配置 {#sling-model-json-exported-structure-configuration}

启用路由功能后，会假设在SPA的JSON导出中，包含应用程序的不同路由，这与AEM导航组件的JSON导出不同。 AEM导航组件的JSON输出可通过以下两个属性在SPA根页面内容策略中进行配置：

* `structureDepth`：与导出的树深度对应的数字
* `structurePatterns`：与要导出的页面对应的正则表达式数组正则表达式

这可以在中的SPA示例内容中显示 `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
