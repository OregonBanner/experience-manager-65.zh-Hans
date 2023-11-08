---
title: 使用 Edge Delivery Services
description: 使用 Edge Delivery Services (EDS)
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 93%

---

# 使用 Edge Delivery Services {#usingedge}

利用 Edge Delivery，您可以创建快速开发环境，作者可在其中快速地更新和发布内容，并快速地推出新网站。为此，您可以在同一网站上使用多个内容源，无论您选择的源如何，都可以轻松进行无缝发布。因此，从在 Internet 上实时编辑内容到查看内容只需几秒钟。

## 创作 {#authoring-edge}

Edge Delivery 让创作变得简单、快速且灵活。您可以在 Edge Delivery Services 的上下文中采用两种不同的路径进行创作：

* 基于文档的创作（例如 Microsoft Word 或 Google Docs）- [请参阅此链接以了解更多详细信息](https://www.hlx.live/docs/authoring)。
* 页面编辑器/Universal Editor - 请联系您的 Adobe 销售代表。

如果存在基于文档的创作，则可以使用各种源，如Microsoft Word和Google Docs。 来自这些源的文档将成为您网站上的页面。标题、列表、图像、字体元素、视频都可以从初始源转移到网站中。您可以出于 SEO 目的添加元数据，也可以使用块来处理结构化内容并添加功能。

## 发布 {#publishing-edge}

利用 Edge Delivery，无论内容源如何，都可以无缝发布内容。过程如下：您使用 [Sidekick 扩展](#using-sidekick)触发发布机制，您的内容将在几秒钟内显示在您的网站上。

## Edge Delivery Services 和 GitHub {#github-edge}

Edge Delivery使用GitHub，因此客户可以直接从其GitHub存储库管理和部署代码。 例如，您可以在 Google Docs 或 Microsoft Word 中编写内容，并且可以使用 GitHub 中的 CSS 和 JavaScript 来开发站点功能。从内容预览到生产，将自动为您的每个分支创建网站。您放入 GitHub 存储库中的每个资源都在您的网站上可供使用，无需构建过程。

## 使用 Sidekick {#using-sidekick}

AEM Sidekick 提供了一个带上下文感知选项的工具栏，可让您轻松编辑、预览和发布内容。[安装](https://www.hlx.live/docs/sidekick-extension) AEM Sidekick 扩展后，可以在项目环境中或在编辑内容时使用（例如，在 Google Docs 中）使用此扩展。根据环境，它有多种可用操作，例如：预览、重新加载、编辑和发布。您还可以在使用 Sidekick 时切换环境，从预览切换到生产，反之亦然。

**要进行发布**，请在预览页面上打开 Sidekick 并使用“发布”操作。单击“发布”后，页面的当前预览版本将在实时环境和生产环境中可用。

## 将 AEM Assets 与基于文档的创作集成 {#integrate-assets-edge}

有了 Edge Delivery，在 Microsoft Word 或 Google Docs 中创作文档时，可以使用 AEM Assets 存储库中提供的图像。

仅在[配置 AEM Assets Sidekick 插件](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin)后，可以使用用于在文档中使用图像的选项。

AEM Assets 的 Sidekick 插件支持访问以下项目：

* AEM Assets as a Cloud Service

* AEM Assets Essentials

在配置 AEM Assets Sidekick 插件后，您可以[开始在 Google Docs 或 Microsoft Word 文档中使用图像](https://www.hlx.live/docs/aem-assets-sidekick-plugin)。

## 深入阅读 {#further-reading}

有关更多详细信息，请参阅以下页面：

* 有关如何开始使用 Edge Delivery 的详细信息，请参阅 Edge Delivery 文档的[构建](https://www.hlx.live/docs/#build)部分。
* 要了解如何使用 Edge Delivery 创作和发布内容，请参阅[“发布”部分](https://www.hlx.live/docs/authoring)。
* 要了解如何使用 Sidekick 扩展，请参阅[使用 Sidekick](https://www.hlx.live/docs/sidekick) 页面。
* 对于 AEM 创作，请参阅[创作概念页面](/help/sites-authoring/author.md)）
