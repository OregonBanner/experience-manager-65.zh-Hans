---
title: 使用Edge Delivery Services
description: 使用Edge Delivery Services
source-git-commit: 0c0e14ec3d022b7e9efd17edf2997990f5ac3dc2
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# 使用Edge Delivery Services {#usingedge}

借助Edge Delivery，您可以创建快速开发环境，以便作者能够快速更新和发布内容，并快速启动新站点。 为此，您可以在同一网站上使用多个内容源，并且无论您选择什么源，发布过程都将无缝且高效。 因此，从编辑到在Internet上实时查看内容，只需要几秒钟即可完成。

## 创作 {#authoring-edge}

使用Edge Delivery，创作变得简单、快速和灵活。 在Edge Delivery Services的上下文中，可以采用两种不同的创作路径：

* 基于文档的创作(例如Microsoft Word或Google文档)- [有关更多详细信息，请参阅此链接](https://www.hlx.live/docs/authoring).
* 页面编辑器/通用编辑器 — 请联系您的Adobe销售代表。

在基于文档的创作中，您可以使用各种源，如Microsoft Word和Google Docs。 来自这些来源的文档将成为您网站上的页面。 标题、列表、图像、字体元素和视频都可以从初始源传输到您的网站。 您可以添加元数据以进行SEO，或使用块来处理结构化内容并添加功能。

## 发布 {#publishing-edge}

通过Edge Delivery，无论内容来源如何，均可无缝发布内容。 过程如下：使用 [sidekick扩展](#using-sidekick) 以触发发布机制，您的内容将在几秒钟后可在您的网站上实时可用。

## Edge Delivery Services和GitHub {#github-edge}

Edge交付利用GitHub，因此客户可以直接从其GitHub存储库管理和部署代码。 例如，您可以在Google文档或Microsoft Word中编写内容，并在GitHub中使用CSS和JavaScript开发站点的功能。 从内容预览到生产，将为每个分支自动创建网站。 您放入GitHub存储库中的每个资源都可在您的网站上使用，而无需构建过程。

## 使用Sidekick {#using-sidekick}

AEM Sidekick提供了一个带上下文感知选项的工具栏，以便您轻松编辑、预览和发布内容。 之后 [安装](https://www.hlx.live/docs/sidekick-extension) AEM sidekick扩展可用于项目环境或编辑内容(例如，在Google文档中)。 根据环境，它有多种可用操作，如：预览、重新加载、编辑和发布。 在使用Sidekick时，您还可以将环境从预览切换到生产，反之亦然。

**要发布**，在预览页面上打开Sidekick并使用Publish操作。 单击发布后，页面的当前预览版本将在实时环境和生产环境中可用。

## 将AEM Assets与基于文档的创作集成 {#integrate-assets-edge}

通过Edge Delivery，您可以在创作Microsoft Word或Google文档时，使用AEM Assets存储库中可用的图像。

在文档中使用图像的选项仅在 [配置AEM Assets sidekick插件](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

适用于AEM Assets的sidekick插件支持访问：

* AEM Assets as a Cloud Service

* AEM Assets Essentials

配置AEM Assets Sidekick插件后，您可以 [开始在Google文档或Microsoft Word文档中使用图像](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## 进一步阅读 {#further-reading}

有关更多详细信息，请参阅以下页面：

* 有关如何开始使用Edge Delivery的详细信息，请参阅 [生成](https://www.hlx.live/docs/#build) Edge投放文档的部分内容。
* 要了解如何使用Edge Delivery创作和发布内容，请参阅 [发布部分](https://www.hlx.live/docs/authoring).
* 要了解如何使用sidekick扩展，请参阅 [使用副手](https://www.hlx.live/docs/sidekick) 页面。
* 有关AEM创作，请参阅 [“创作概念”页](/help/sites-authoring/author.md))
