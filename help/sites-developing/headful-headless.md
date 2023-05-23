---
title: AEM 中的 Headful 和 Headless
description: AEM專案可以在headful和headless模型中實作，但選擇不是二進位。 利用 AEM，可以在一个项目中灵活地运用这两种模型的优势。
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
source-git-commit: ac70fb534a95c9eee6f8340d9b8720a607b9f79f
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 94%

---

# AEM 中的 Headful 和 Headless {#headful-headless}

Adobe Experience Manager專案可在headful和headless模式中實作，但選擇不是二進位。 利用 AEM，可以在一个项目中灵活地运用这两种模型的优势。本檔案提供不同模式的概觀，並說明SPA整合的等級。

## 概述 {#overview}

AEM 提供了功能强大的工具来管理一个平台上的内容创建和交付操作。这是传统的内容管理“Headful”模型，在该模型中，内容作者和开发人员在同一个平台上工作以将体验交付给内容消费者。

AEM 还可用于简单地管理内容，并允许呈现和交付要由另一个平台管理的内容。这是内容管理“Headless”模型，在该模型中，内容作者和开发人员在不同的平台上工作以将体验交付给内容消费者。

但这不必是一个二选一的选择。AEM 提供了前所未有的灵活性，使您能够在项目中灵活地运用这两种模型的优势。

![AEM 实施模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

在 Headful 或全栈模型中，内容在 AEM 存储库中进行管理，而基于 Java、HTL 等的 AEM 组件用于呈现用户体验的内容。在此模型中，内容的创建、样式设置、呈现和交付操作都在 AEM 中进行。

在 Headless 模型中，内容在 AEM 存储库中管理，但通过 REST 和 GraphQL 等 API 交付到另一个系统以呈现用户体验的内容。在此模型中，内容的创建操作是在 AEM 中进行的，但内容的样式设置、呈现和交付操作是在另一个平台中进行的。

单页应用程序 (SPA) 通常是 AEM 以 Headless 方式交付内容的目标。但是，这些 SPA 不必完全在 AEM 外部。利用 AEM，您可以决定 SPA 集成到 AEM 中的程度。让我们举个例子。

## 网上商店示例 {#web-shop-example}

假设您将公司现有的网上商店作为 SPA，其中包含所有产品详细信息和图像。随后，您引入 AEM 来支持您的营销工作，例如促销网站、博客和活动内容。如何将这两者集成？AEM 支持一系列选项：

* **允许系统单独运行。**
* **通过 GraphQL 向网上商店提供来自 AEM 的有限内容。**&#x200B;内容可以由作者在 AEM 中创建，但只能通过网上商店 SPA 查看。
* **在 AEM 中嵌入网上商店 SPA。**&#x200B;内容可以由作者在 AEM 中创建，并在 AEM 中的网上商店情境中查看，但不能进行操作。
* **在 AEM 中嵌入网上商店 SPA，并启用可编辑点。**&#x200B;内容可以由作者在 AEM 中创建，并在 AEM 中的网上商店情境中查看，并且作者只能对 AEM 中的网上商店 SPA 内容进行有限的操作。
* **在 AEM 中嵌入网上商店 SPA，并启用整个区域以进行编辑。**&#x200B;内容可以由作者在 AEM 中创建，并在 AEM 中的网上商店情境中查看，并且作者只能对 AEM 中的网上商店 SPA 内容进行有限的操作。

在下一部分中，我们将更详细地探究这些集成级别。

>[!NOTE]
>
>当然，您也可以将网上商店 SPA 作为功能齐全的 AEM SPA 重新实施，方式是[使用 AEM SPA Editor 框架。](/help/sites-developing/spa-walkthrough.md)如果您已拥有 AEM 并希望创建新的网上商店或其他 SPA，建议使用此方式，但本文档未对此方式进行介绍。

## SPA 集成级别 {#integration-levels}

SPA 集成归入 AEM 中包含四个级别的系列中。

* **级别 0：无集成**
   * SPA 和 AEM 单独存在，并且不交换任何信息。
   * 在两个独立的系统中单独创建、管理和交付内容。
* **级别 1：内容片段集成**
   * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的有限内容。
   * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
   * 在 AEM 中管理一些内容，在外部系统中管理另一些内容。
   * 只能在 SPA 中查看内容。
* **级别 2：将 SPA 嵌入 AEM**
   * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的内容。
   * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
   * 在 AEM 中管理一些内容，在外部系统中管理另一些内容。
   * 可在 AEM 中的上下文中查看内容。
   * 可在 AEM 中编辑有限内容。
* **级别 3：在 AEM 中嵌入并完全启用 SPA**
   * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的内容。
   * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
   * 可在 AEM 中的上下文中查看内容。
   * 可在 AEM 中编辑大多数内容。

级别 1 是典型 Headless 实施的示例。但是，内容作者只能在 SPA 中的上下文中查看其内容。AEM 只是一项创作工具。

AEM 的优势和灵活性在级别 2 和级别 3 中变得明显，同时仍保留了 SPA 的优势。内容作者既可以在 AEM 中创建其内容，也可以在 AEM 中的上下文中查看其内容。虽然可以在 AEM 中创作 SPA，但它将作为 SPA 交付。

## 实施集成级别 {#implementing}

AEM 中提供了不同的工具，具体取决于您选择的集成级别。每个级别均基于之前使用的工具而构建。以下列表将链接到相关资源。

* **级别 1：**&#x200B;内容片段和 [AEM Headless 框架](/help/sites-developing/headless/introduction.md)可用于将 AEM 内容交付给 SPA。
* **级别 2：**&#x200B;除了级别 1 之外：
   * [RemotePage 组件](/help/sites-developing/spa-remote-page.md)可用于将外部 SPA 嵌入到 AEM 中，这样便能在上下文中查看 AEM 内容。
   * 还可以启用 SPA 上的某些点以[允许在 AEM 中进行有限编辑。](/help/sites-developing/spa-edit-external.md)
* **级别 3：**&#x200B;除了级别 2 之外：
   * 可以启用 SPA 的整个区域以允许在 AEM 中进行全面编辑。
