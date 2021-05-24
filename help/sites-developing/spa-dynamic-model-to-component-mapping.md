---
title: 适用于SPA的动态模型到组件映射
seo-title: 适用于SPA的动态模型到组件映射
description: 本文介绍了在适用于AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。
seo-description: 本文介绍了在适用于AEM的Javascript SPA SDK中如何进行动态模型到组件的映射。
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# SPA{#dynamic-model-to-component-mapping-for-spas}的动态模型到组件映射

本文档介绍如何在适用于AEM的Javascript SPA SDK中进行动态模型到组件的映射。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 组件映射模块{#componentmapping-module}

`ComponentMapping`模块作为NPM包提供到前端项目。 它存储前端组件，并为单页应用程序提供了一种将前端组件映射到AEM资源类型的方法。 这样，在解析应用程序的JSON模型时，就可以动态解析组件。

模型中存在的每个项目都包含一个公开AEM资源类型的`:type`字段。 装载后，前端组件可以使用从基础库收到的模型片段呈现自身。

请参阅[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文档，以了解有关模型解析和对模型的前端组件访问的详细信息。

另请参阅npm包：[https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## 模型驱动的单页应用程序{#model-driven-single-page-application}

使用适用于AEM的Javascript SPA SDK的单页应用程序由模型驱动：

1. 前端组件自行注册到[组件映射存储](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)。
1. 然后， [Container](/help/sites-developing/spa-blueprint.md#container)一旦由[模型提供程序](/help/sites-developing/spa-blueprint.md#the-model-provider)提供了模型，则会迭代其模型内容(`:items`)。

1. 对于页面，其子项(`:children`)首先从[组件映射](/help/sites-developing/spa-blueprint.md#componentmapping)中获取组件类，然后将其实例化。

## 应用程序初始化{#app-initialization}

每个组件都通过[ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)的功能进行扩展。 因此，初始化采用以下一般形式：

1. 每个模型提供程序自行初始化，并侦听对与其内部组件对应的模型段所做的更改。
1. [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)必须初始化，如[初始化流程](/help/sites-developing/spa-blueprint.md)所示。

1. 存储后，页面模型管理器会返回应用程序的完整模型。
1. 然后，此模型将传递到应用程序的前端根[容器](/help/sites-developing/spa-blueprint.md#container)组件。
1. 模型段最终会传播到每个单独的子组件。

![app_model_initialization](assets/app_model_initialization.png)
