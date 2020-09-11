---
title: SPA的动态模型到组件映射
seo-title: SPA的动态模型到组件映射
description: 本文描述了在AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。
seo-description: 本文描述了在AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# SPA的动态模型到组件映射{#dynamic-model-to-component-mapping-for-spas}

本文档介绍了AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 组件映射模块 {#componentmapping-module}

该 `ComponentMapping` 模块作为NPM包提供给前端项目。 它存储前端组件，并为单页应用程序将前端组件映射到AEM资源类型提供了一种方法。 这样，在解析应用程序的JSON模型时，可动态解析组件。

模型中存在的每个项目都包含一个 `:type` 公开AEM资源类型的字段。 装载后，前端组件可以使用它从基础库接收的模型片段来呈现自己。

有关模型分 [析和对模型的前端组件访问](/help/sites-developing/spa-blueprint.md) ，请参阅SPA Blueprint文档。

另请参阅npm包： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序 {#model-driven-single-page-application}

利用AEM的Javascript SPA SDK的单页应用程序由模型驱动：

1. 前端组件自行注册到组 [件映射存储](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 然后 [容器](/help/sites-developing/spa-blueprint.md#container)，一旦由模型提供者 [提供了模型](/help/sites-developing/spa-blueprint.md#the-model-provider)，就会迭代其模型内容( `:items`)。

1. 对于页面，其子项() `:children`首先从组件映射中获取组件类 [，然后将](/help/sites-developing/spa-blueprint.md#componentmapping) 它实例化。

## 应用程序初始化 {#app-initialization}

每个组件都通过的功能进行扩展 [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)。 因此，初始化采用以下一般形式：

1. 每个模型提供程序自行初始化，并监听对与其内部组件对应的模型片段所做的更改。
1. 必须 [ 以初始化 `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 流所表示的形式 [初始化](/help/sites-developing/spa-blueprint.md)。

1. 存储后，页面模型管理器将返回应用程序的完整模型。
1. 然后，此模型将传递给应用程序的前 [端根容器](/help/sites-developing/spa-blueprint.md#container) 组件。
1. 模型的片段最终传播到每个单独的子组件。

![app_model_initialization](assets/app_model_initialization.png)

