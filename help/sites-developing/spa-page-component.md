---
title: SPA页面组件
seo-title: SPA页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 此文档说明这如何使SPA的页面组件独一无二。
seo-description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 此文档说明这如何使SPA的页面组件独一无二。
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579

---


# SPA页面组件{#spa-page-component}

在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 此文档说明这如何使SPA的页面组件独一无二。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 简介 {#introduction}

SPA的页面组件不会通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作被委派到SPA框架。 子组件的表示形式被提取为JSON数据结构（即模型）。 然后，SPA组件会根据提供的JSON模型添加到页面。 因此，页面组件初始主体合成与预先渲染的HTML相同。

## 页面模型管理 {#page-model-management}

页面模型的解析和管理被委托给提供的 [ 模 `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 块。 SPA在初始化时必 `PageModelManager` 须与模块交互，以获取初始页面模型并注册模型更新——大多数情况下，当作者通过页面编辑器编辑页面时生成。 SPA `PageModelManager` 项目可以作为npm包访问。 作为AEM和SPA之间的解 `PageModelManager` 释员，SPA应随同提供。

要允许创作页面，必须添加一个名为的客 `cq.authoring.pagemodel.messaging` 户端库，以在SPA和页面编辑器之间提供通信渠道。 如果SPA页面组件从页面wcm/core组件继承内容，则有以下选项可使客户端库 `cq.authoring.pagemodel.messaging` 类别可用：

* 如果模板是可编辑的，请将客户端库类别添加到页面策略。
* 使用页面组件添加客 `customfooterlibs.html` 户端库类别。

不要忘记将类别包含在页 `cq.authoring.pagemodel.messaging` 面编辑器的上下文中。

## 通信数据类型 {#communication-data-type}

通信数据类型使用属性在AEM页面组件中设置一个HTML元 `data-cq-datatype` 素。 当通信数据类型设置为JSON时，GET请求将点击组件的Sling Model端点。 在页面编辑器中进行更新后，已更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会警告更新的SPA。

**SPA页面组件-`body.html`**

```
<div id="page"></div>
```

除了不延迟DOM生成的良好实践之外，SPA框架还要求在主体末尾添加脚本。

**SPA页面组件-`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

描述SPA内容的元资源属性：

**SPA页面组件-`customheaderlibs.html`**

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
>在请求元件的“吊索模型”表示时，将静态设置缺省模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`: 编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`: 应用程序的根模型的URL。 由于子页面模型是应用程序根模型的片段，因此在直接访问子页面时至关重要。 然后 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 系统地将应用程序初始模型重新组合为从其根入口点进入应用程序。

* `cq:pagemodel_router`: 启用或禁用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 库 `PageModelManager` 的

* `cq:pagemodel_route_filters`: 以逗号分隔的列表或常规表达式提供必须忽 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 略的路由。

>[!CAUTION]
>
>此文档仅将We.Retail日志应用程序用于演示目的。 它不应用于任何项目工作。
>
>任何AEM项目都应利 [用AEM项目原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)，该原型支持使用React或Angular的SPA项目并利用SPA SDK。AEM上的所有SPA项目均应基于SPA入门套件的Maven原型。

## 页面编辑器叠加同步 {#page-editor-overlay-synchronization}

叠加的同步由类别提供的相同的变异观测器来保 `cq.authoring.page` 证。

## Sling Model JSON导出结构配置 {#sling-model-json-exported-structure-configuration}

启用路由功能后，假定SPA的JSON导出包含应用程序的不同路由，这要归功于AEM导航组件的JSON导出。 AEM导航组件的JSON输出可以通过以下两个属性在SPA的根页面内容策略中进行配置：

* `structureDepth`: 与导出的树的深度对应的编号
* `structurePatterns`: 与要导出的页面对应的正则表达式数组的正则表达式

这可以在中的SPA示例内容中显示 `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`。
