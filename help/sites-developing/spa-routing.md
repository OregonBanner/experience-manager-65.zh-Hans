---
title: SPA模型路由
seo-title: SPA模型路由
description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档介绍了路由选择机制、合同和可用选项。
seo-description: 对于AEM中的单页应用程序，应用程序负责路由。 本文档介绍了路由选择机制、合同和可用选项。
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA模型路由{#spa-model-routing}

对于AEM中的单页应用程序，应用程序负责路由。 本文档介绍了路由选择机制、合同和可用选项。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

## 项目路线 {#project-routing}

应用程序拥有路由，然后由项目前端开发人员实施。 本文档描述特定于AEM服务器返回的模型的路由选择。 页面模型数据结构公开基础资源的URL。 前端项目可以使用提供路由功能的任何自定义或第三方库。 一旦路由需要模型片段，就可以调用 `PageModelManager.getData()` 该函数。 当模型路由发生更改时，必须触发事件以警告监听库，如页面编辑器。

## 架构 {#architecture}

有关详细说明，请参阅SPA Blueprint文 [档的PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 部分。

## ModelRouter {#modelrouter}

启 `ModelRouter` 用后，将封装HTML5历史记录API函数 `pushState` , `replaceState` 并确保预取和可访问给定的模型片段。 然后，它会通知注册的前端组件模型已修改。

## 手动与自动模型路由 {#manual-vs-automatic-model-routing}

模 `ModelRouter` 型的片段自动获取。 但是，作为任何自动化工具集，它都有其局限性。 如果需要， `ModelRouter` 可以使用元属性禁用或配置为忽略路径(请参阅 [SPA页面组件文档的元属性部分](/help/sites-developing/spa-page-component.md) )。 然后，前端开发者可以通过使用该函数请求加载任何给 `PageModelManager` 定的模型片段来实现自己的模型路由 `getData()` 层。

>[!NOTE]
>
>目前，We.Retail Journal示例React项目说明了自动化方法，而Angular项目说明了手动方法。 半自动化方法也是有效的用例。

>[!CAUTION]
>
>当前版本仅支 `ModelRouter` 持使用指向Sling Model入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

## 工艺路线合同 {#routing-contract}

当前实施基于以下假设：SPA项目使用HTML5历史记录API路由到不同的应用程序页。

### 配置 {#configuration}

当 `ModelRouter` 监听和调用预取模型片段时，支持模 `pushState` 型路 `replaceState` 由的概念。 在内部，它触 `PageModelManager` 发加载与给定URL对应的模型，并触发其他模 `cq-pagemodel-route-changed` 块可以侦听的事件。

默认情况下，此行为是自动启用的。 要禁用它，SPA应呈现以下元属性：

```
<meta property="cq:pagemodel_router" content="disable"\>
```

请注意，SPA的每条路由都应与AEM中的可访问资源(例如，“ `/content/mysite/mypage"`)对应，因为一旦选择了该路由， `PageModelManager` 该路径将自动尝试加载相应的页面模型。 但是，如果需要，SPA还可以定义应被以下项忽略的路由“黑名单” `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
