---
title: SPA模型路由
seo-title: SPA模型路由
description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档描述了路由机制、合同和可用选项。
seo-description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档描述了路由机制、合同和可用选项。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# SPA型号路由{#spa-model-routing}

对于AEM中的单页应用程序，应用程序负责路由。 本文档描述了路由机制、合同和可用选项。

>[!NOTE]
>
>SPA编辑器是需要SPA框架的客户端渲染（例如，React或Angular）的项目的推荐解决方案。

## 项目路由{#project-routing}

应用程序拥有路由，然后由项目前端开发人员实施。 此文档描述特定于AEM服务器返回的模型的路由。 页面模型数据结构公开基础资源的URL。 前端项目可以使用提供路由功能的任何自定义或第三方库。 一旦路由需要模型片段，就可以调用`PageModelManager.getData()`函数。 当模型路由发生更改时，必须触发事件以警告监听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参阅SPA Blueprint文档的[PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)部分。

## ModelRouter {#modelrouter}

`ModelRouter` —— 启用后——封装HTML5历史API函数`pushState`和`replaceState`，以确保预取和访问给定的模型片段。 然后，它会通知已注册的前端组件模型已修改。

## 手动与自动模型路由{#manual-vs-automatic-model-routing}

`ModelRouter`自动获取模型的片段。 但是，作为任何自动化工具集，它都有局限性。 如果需要，可以禁用`ModelRouter`或将&lt;a0/>配置为使用元属性忽略路径(请参阅[SPA页面组件](/help/sites-developing/spa-page-component.md)文档的元属性部分)。 然后，前端开发者可以使用`getData()`函数请求`PageModelManager`加载任何给定的模型片段，从而实现自己的模型路由层。

>[!NOTE]
>
>目前，We.Retail日志范例React项目演示了自动化方法，而Angular项目则演示了手动方法。 半自动化方法也是有效的用例。

>[!CAUTION]
>
>`ModelRouter`的当前版本仅支持使用指向Sling Model入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

## 路由合同{#routing-contract}

当前实施基于SPA项目使用HTML5 History API路由到不同应用程序页面的假设。

### 配置 {#configuration}

`ModelRouter`在监听`pushState`和`replaceState`调用预取模型片段时支持模型路由的概念。 在内部，它触发`PageModelManager`以加载与给定URL对应的模型，并触发其他模块可以侦听的`cq-pagemodel-route-changed`事件。

默认情况下，此行为会自动启用。 要禁用它，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

请注意，SPA的每条路由都应与AEM中的可访问资源（例如，“ `/content/mysite/mypage"`）对应，因为选择路由后，`PageModelManager`将自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义`PageModelManager`应忽略的路由的“阻止列表”:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
