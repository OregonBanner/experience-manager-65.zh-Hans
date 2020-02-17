---
title: SPA页面组件
seo-title: SPA页面组件
description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 本文档解释了这如何使SPA的页面组件独一无二。
seo-description: 在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 本文档解释了这如何使SPA的页面组件独一无二。
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA页面组件{#spa-page-component}

在SPA中，页面组件不提供其子组件的HTML元素，而是将其委派到SPA框架。 本文档解释了这如何使SPA的页面组件独一无二。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

## 简介 {#introduction}

SPA的页面组件不通过JSP或HTL文件和资源对象提供其子组件的HTML元素。 此操作委托给SPA框架。 子组件的表示形式将作为JSON数据结构（即模型）获取。 然后，SPA组件会根据提供的JSON模型添加到页面。 因此，页面组件初始主体合成与其预渲染的HTML对应内容不同。

## 页面模型管理 {#page-model-management}

页面模型的解析和管理被委托给提供的模 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 块。 SPA在初始化时必须与模块交互，以获取初始页面模型并注册模型更新——大多数情况下，当作者通过页面编辑器编辑页面时生成。 `PageModelManager` SPA项 `PageModelManager` 目可以作为npm包访问。 作为AEM与SPA之间的解释员，该 `PageModelManager` 服务器应随SPA一起提供。

要允许创作页面，必须添加一个名为的客 `cq.authoring.pagemodel.messaging` 户端库，以在SPA和页面编辑器之间提供通信通道。 如果SPA页面组件从页面wcm/核心组件继承，则有以下选项可使客户端库类 `cq.authoring.pagemodel.messaging` 别可用：

* 如果模板是可编辑的，请将客户端库类别添加到页面策略。
* 使用页面组件添加客 `customfooterlibs.html` 户端库类别。

不要忘记将类别包含在页 `cq.authoring.pagemodel.messaging` 面编辑器的上下文中。

## 通信数据类型 {#communication-data-type}

通信数据类型使用属性在AEM页面组件中设置一个HTML元 `data-cq-datatype` 素。 当通信数据类型设置为JSON时，GET请求将点击组件的Sling model端点。 在页面编辑器中进行更新后，更新组件的JSON表示形式将发送到页面模型库。 然后，页面模型库会警告SPA更新。

**SPA页面组件-`body.html`**

```
<div id="page"></div>
```

SPA框架除了是不延迟DOM生成的良好实践之外，还要求在主体末尾添加脚本。

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
>在请求元件的Sling模型表示时，将静态设置默认模型选择器。

## 元属性 {#meta-properties}

* `cq:wcmmode`:编辑器的WCM模式（例如，页面、模板）
* `cq:pagemodel_root_url`:应用程序的根模型的URL。 直接访问子页面时至关重要，因为子页面模型是应用程序根模型的片段。 然后 ` [PageModelManager](/help/sites-developing/spa-page-component.md)` 系统地将应用程序初始模型重新组合为从其根入口点进入应用程序。

* `cq:pagemodel_router`:启用或禁用 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 库的功 `PageModelManager` 能

* `cq:pagemodel_route_filters`:以逗号分隔的列表或正则表达式来提供必须忽 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 略的路由。

## 页面编辑器叠加同步 {#page-editor-overlay-synchronization}

叠加的同步由类提供的相同的变异观测器来保 `cq.authoring.page` 证。

## Sling Model JSON导出的结构配置 {#sling-model-json-exported-structure-configuration}

启用路由功能后，假定SPA的JSON导出包含应用程序的不同路由，这要归功于AEM导航组件的JSON导出。 AEM导航组件的JSON输出可通过以下两个属性在SPA的根页面内容策略中进行配置：

* `structureDepth`:与导出的树的深度对应的编号
* `structurePatterns`:与要导出的页面对应的正则表达式数组的正则表达式

这可以在中的SPA示例内容中显示 `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`。
