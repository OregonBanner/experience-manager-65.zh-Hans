---
title: SPA的动态模型到组件映射
description: 了解在JavaScript SPA SDK for Adobe Experience Manager中如何进行动态模型到组件的映射。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# SPA的动态模型到组件映射{#dynamic-model-to-component-mapping-for-spas}

本文档介绍在JavaScript SPA SDK for Adobe Experience Manager (AEM)中如何进行组件动态映射。

>[!NOTE]
>
>SPA编辑器是推荐的解决方案，适用于需要基于SPA框架的客户端渲染(例如React或Angular)的项目。

## 组件映射模块 {#componentmapping-module}

此 `ComponentMapping` 模块作为NPM包提供给前端项目。 它存储前端组件，并为单页应用程序提供一种将前端组件映射到AEM资源类型的方法。 这可以在解析应用程序的JSON模型时启用组件的动态分辨率。

模型中显示的每个项目都包含 `:type` 公开AEM资源类型的字段。 安装后，前端组件可以使用从基础库收到的模型片段来呈现自身。

请参阅 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 有关模型解析和前端组件访问模型的更多信息。

另请参阅npm包： [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序 {#model-driven-single-page-application}

使用JavaScript SPA SDK for AEM的单页应用程序是模型驱动的：

1. 前端组件向 [组件映射存储](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. 然后 [容器](/help/sites-developing/spa-blueprint.md#container)，由提供模型 [模型提供程序](/help/sites-developing/spa-blueprint.md#the-model-provider)，遍历其模型内容( `:items`)。

1. 如果存在页面，则其子页面( `:children`)首先从获取组件类 [组件映射](/help/sites-developing/spa-blueprint.md#componentmapping) 然后实例化它。

## 应用程序初始化 {#app-initialization}

每个组件都扩展了 [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). 因此，初始化采用以下常规形式：

1. 每个模型提供程序都会初始化自身，并侦听对与其内部组件相对应的模型段所做的更改。
1. 此 [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) 必须初始化，表示为 [初始化流程](/help/sites-developing/spa-blueprint.md).

1. 存储后，页面模型管理器会返回应用程序的完整模型。
1. 然后，将此模型传递到前端根 [容器](/help/sites-developing/spa-blueprint.md#container) 应用程序的组件。
1. 模型片段最终传播到每个单独的子元件中。

![app_model_initialization](assets/app_model_initialization.png)
