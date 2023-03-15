---
title: 可选 – 如何使用 AEM 创建单页应用程序 (SPA)
description: 在 AEM Headless 开发人员历程的这一可选延续部分中，您将了解 AEM 如何将 Headless 交付与传统的全栈 CMS 功能相结合，以及您如何使用 AEM 的 SPA 编辑器框架来创建可编辑的 SPA。
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 100%

---

# 如何使用 AEM 创建单页应用程序 (SPA) {#create-spa}

在 [AEM Headless 开发人员历程](overview.md)的这一可选延续部分中，您将了解 AEM 如何将 Headless 交付与传统的全栈 CMS 功能相结合，您如何使用 AEM 的 SPA 编辑器框架来创建可编辑的 SPA，如何集成外部 SPA，以及根据需要启用编辑功能。

## 迄今为止的故事 {#story-so-far}

此时，您应已完成整个 [AEM Headless 开发人员历程](overview.md)，并已了解 AEM 中的 Headless 交付的基础知识，包括了解：

* Headless 和 Headful 内容交付之间的区别。
* AEM 的 Headless 功能。
* 如何编排 AEM Headless 项目。
* 如何在 AEM 中创建 Headless 内容。
* 如何在 AEM 中检索和更新 Headless 内容。
* 如何使用 AEM Headless 项目上线。

您现在要么已使用第一个 AEM Headless 项目上线，要么已具备执行此操作所需的所有知识。恭喜！

那么，为什么您需要阅读此历程的这一附加可选延续部分呢？您可能还记得，在[快速入门](getting-started.md#integration-levels)中，我们简要讨论了 AEM 如何支持 Headless 交付和传统全栈模型，并支持结合了两者优点的混合模型。虽然此混合模型不是传统 Headless 模型，但它可以为某些项目提供前所未有的灵活性。

本文基于您对 AEM Headless 的了解，深入探究您如何创建自己的单页应用程序 (SPA)，实际上可在 AEM 中编辑这些应用程序。通过这种方式，您可以创建内容并以 Headless 方式将它交付给 SPA，但仍可在 AEM 中编辑此 SPA。

## 目标 {#objective}

本文档将帮助您了解如何使用 AEM SPA Editor 框架来开发单页应用程序。阅读本文档后，您应：

* 了解 SPA 编辑器的基本功能。
* 了解为 AEM 构建完全可编辑的 SPA 的要求。
* 了解如何将外部 SPA 集成到 AEM 中。
* 了解应该或不应该如何实施服务器端呈现。

## 要求和先决条件 {#requirements-prerequisites}

开始在 AEM 中使用 SPA 之前，需要满足许多要求。

### 知识 {#knowledge}

* 有关使用 React 或 Angular 框架创建 SPA 的开发经验
* 有关创建内容片段和使用编辑器的基本 AEM 技能
* 请务必查看文档 [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md)，了解可能的 SPA 集成的各种级别。

### 工具 {#tools}

* 用于测试部署项目的沙盒访问
* 用于数据建模和测试的本地开发实例
* 现有的外部 SPA（可选，具体取决于选择的集成模型）
* AEM 项目原型

## 什么是 SPA？ {#what-is-a-spa}

单页应用程序 (SPA) 与传统页面的不同之处在于，它在客户端呈现且主要由 Javascript 驱动，并且依靠 Ajax 调用来加载数据和动态更新页面。大多数内容或所有内容在单个页面加载中检索一次，并基于用户与页面的交互按需异步加载其他资源。

这减少了页面刷新需求，并为用户提供了一种无缝、快速且更类似于本机应用程序体验的体验。

利用 AEM SPA Editor，前端开发人员可以创建可集成到 AEM 站点中的 SPA，从而允许内容作者像编辑任何其他 AEM 内容那样轻松地编辑 SPA 内容。

## 为什么使用 SPA？ {#why-spa}

SPA 的工作方式的特性使其更快、更流畅且更类似于本机应用程序，从而为网页访客以及营销人员和开发人员提供一种极具吸引力的体验。

有关 SPA 的完整说明以及使用 SPA 的原因，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## AEM 如何处理 SPA

在 AEM 上开发单页应用程序时，假定前端开发人员在创建 SPA 时遵循标准最佳实践。作为前端开发人员，如果您遵循这些一般最佳实践以及一些特定于 AEM 的原则，您的 SPA 将能够使用 AEM 及其内容创作功能。

* **可移植性** – 与任何组件一样，应构建尽可能可移植的 SPA 组件。应使用可移植且可重用的组件构建 SPA。
* **AEM 推动站点结构** – 前端开发人员创建组件并拥有其内部结构，但依赖 AEM 来定义站点的内容结构。
* **动态呈现** – 所有呈现都应是动态的。
* **动态路由** – SPA 负责路由，AEM 负责侦听它并根据它进行提取。任何路由也应是动态的。

有关 AEM 如何处理 SPA 的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## AEM SPA Editor {#aem-spa-editor}

使用 React 和 Angular 等常见 SPA 框架构建的站点通过动态 JSON 加载其内容，并且不提供 AEM 页面编辑器放置编辑控件时所需的 HTML 结构。

要在 AEM 中启用 SPA 编辑，需要 SPA 的 JSON 输出与 AEM 存储库中的内容模型之间的映射以保存对内容所做的更改。

AEM 中的 SPA 支持引入了一个薄的 JS 层，该层在页面编辑器中加载时与 SPA JS 代码进行交互，从而发送事件并激活编辑控件的位置以允许进行上下文编辑。此功能基于内容服务 API 端点概念构建，因为来自 SPA 的内容需要通过内容服务进行加载。

有关 AEM SPA Editor 的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## 适应现有 SPA {#existing-spas}

如果您目前拥有 SPA，AEM 支持将其嵌入 AEM 中，以便内容作者能够在 AEM 编辑器中看到它。对于在将使用通过内容片段创建的内容的最终应用程序的上下文中查看该内容，这很有用。

此外，只需进行少量更改，即可在 AEM 编辑器中启用对外部 SPA 的某些编辑功能。

RemotePage 组件允许在 AEM 中呈现外部 SPA。

有关如何使外部 SPA 在 AEM 中可编辑的完整说明，请参阅[其他资源](#additional-resources)部分，获取指向更深入文档的链接。

## 后续内容 {#what-is-next}

要开始为 AEM 开发您自己的 SPA，请查看以下文档：

* [SPA WKND 教程](/help/sites-developing/spa-wknd.md)
* [使用 React 快速入门](/help/sites-developing/spa-getting-started-react.md)
* [使用 Angular 快速入门](/help/sites-developing/spa-getting-started-angular.md)

如果您需要调整现有 SPA 以在 AEM 中使用它，请查看以下文档：

* [RemotePage 组件](/help/sites-developing/spa-remote-page.md)
* [在 AEM 中编辑外部 SPA](/help/sites-developing/spa-edit-external.md)

请参阅下面的[其他资源](#additional-resources)，更深入地了解 AEM 中的 SPA 主题。

## 其他资源 {#additional-resources}

以下是一些附加资源，它们对本文档中提及的一些概念进行了更深入的探讨。

* [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md) – AEM 中可用的不同交付模型的描述
* [SPA 简介和演练。](/help/sites-developing/spa-walkthrough.md) – 对 AEM 中的 SPA 的适当介绍
* [为 AEM 开发 SPA](/help/sites-developing/spa-architecture.md) – 有关如何为 AEM 开发 SPA 的指南
* [SPA 编辑器概述](/help/sites-developing/spa-overview.md) – SPA 编辑器的工作原理的详细信息
* [服务器端呈现](/help/sites-developing/spa-ssr.md) – 如何为 AEM SPA 配置 SSR
* [SPA 引用文档](/help/sites-developing/spa-reference-materials.md) – JavaScript API 引用以及指向开源 AEM SPA GitHub 项目的链接
* [内容片段](/help/assets/content-fragments/content-fragments.md) – 如何创建内容片段
* [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) – Maven 模板，它创建最小的基于最佳实践的 Adobe Experience Manager (AEM) 项目作为您网站的起点
