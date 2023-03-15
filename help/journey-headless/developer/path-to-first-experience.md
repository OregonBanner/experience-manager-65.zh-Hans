---
title: 首次 AEM Headless 使用体验的路径
description: 在 AEM Headless 开发人员历程的这一部分中，您将了解在 AEM 中实施您的第一个 Headless 体验（包括规划注意事项）的步骤，并了解最佳实践以让您的历程尽可能顺畅。
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 97%

---

# 首次 AEM Headless 使用体验的路径 {#path-to-first-experience}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，您将了解在 AEM 中实施您的第一个 Headless 体验（包括规划注意事项）的步骤，并了解最佳实践以让您的历程尽可能顺畅。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档 [AEM Headless 快速入门](getting-started.md)中，您学习了 Headless CMS 的含义的基本理论，现在应：

* 了解 AEM 的 Headless 功能的基础知识。
* 了解使用 AEM 的 Headless 功能的先决条件。
* 了解 AEM 的 Headless 集成级别。
* 能够根据范围定义您的项目。

本文基于这些基础知识编写，以便您了解如何准备您自己的 AEM Headless 项目。

## 目标 {#objective}

本文档可帮助您了解实施第一个项目所需的步骤。阅读该文档后，您应：

* 了解有关设计内容的重要规划注意事项。
* 了解在 AEM 中实施 Headless 的步骤。
* 了解需要哪些必要的工具和 AEM 配置。
* 了解使您的 Headless 历程顺畅、使内容生成保持高效并确保快速交付内容的最佳实践。

## 要求 {#requirements}

在继续阅读本文档之前，请确保您已查看 AEM Headless 开发人员历程中的上一个文档 [AEM Headless 快速入门](getting-started.md)，确保您：

* 符合列出的要求。
* 已考虑您自己的项目定义，包括范围、角色和性能。

## 做好规划以获得成功 {#planning-for-success}

要开始您的第一个 AEM Headless 项目，您需要确保您拥有一个内容模型，该模型将支持您希望跨所有渠道进行的个性化设置和更新。

与AEM不同，如果您构建的是客户端应用程序，那么还需要确保设置正确的开发环境，以便针对对AEM的API调用测试客户端。

### 定义内容模型和 API {#defining-models}

您想推动一致的体验并管理跨渠道的个性化营销活动，因此，您可以将每个单独的渠道和表面视为其自己独特的内容结构来交付。不过，让每个渠道都有自己的内容模型将导致难以进行维护。

相反，您应考虑如何基于编排原则（例如，品牌和产品层级、商品或表面的类别或客户历程中的步骤）来关联不同表面上的内容。例如，如果您有一组支持所制造的特定品牌汽车的表面，您可能希望从内容模型开始，以获取适用于整个汽车的一般信息，然后使用更具体的内容，例如汽车启动到出现服务问题时所需的内容。此类模型将强制继承一般汽车品牌内容，并允许根据所需的特定上下文进行转换。它还有助于对此内容的更新的将来管理，因为您可以根据角色实施控制，例如整个汽车品牌的整体营销人员或产品经理与负责“启动汽车”体验的作者。

一旦您拥有内容模型并清晰地了解需要在其上显示内容的各种客户端，您就需要确保将与访问各种内容模型关联的 GraphQL/API 发布到需要此内容的所有客户端。关于访问某些内容的方式，提供了不同的选项。您可以请求一段特定的静态内容，以便缓存内容并提高性能。您还可以请求动态生成的内容，而这将需要进行更多的处理。确保客户端使用的是最能满足其业务需求的 API。

## 了解您的环境 {#understanding-environments}

AEM 中有三种类型的环境：开发、暂存和生产。

开发环境（可以拥有多个）是试验和尝试想法的安全场所。在项目的初始阶段，Adobe 建议使用开发环境来尝试内容模型的变体，并查看哪些模型为表面提供了预期输出。

Headless 项目的暂存环境用于在新的 AEM 产品版本发布到生产环境之前对其进行验证。在那里保留最新的生产内容模型列表和内容子集，以便呈现 JSON 文件来比较它们是否仍提供相同的输出，因为您已进行更改或 AEM 版本引入了更改

生产环境是内容作者创建和管理其实际内容的地方。生产中的模型更改必须谨慎进行，并考虑向后兼容性。

在开发阶段，建议您使用开发环境和暂存环境。在转至性能测试时，您将需要迁移到生产环境。

### 开发人员和内容作者的合作 {#cooperation}

开发人员需要使用填充的内容模型设置 AEM 开发环境。由于内容作者仍在创建内容，因此，开发人员开发的客户端将使用 AEM Headless 中的内容。这就是 API 定义之所以如此重要的原因。通过利用 AEM SDK，开发人员可以创建一个测试挂钩，以便创建客户端和单元测试来确保客户端能够正确地呈现内容。

内容作者根据在暂存环境中定义的内容模型来创建内容。利用内容片段创作工具，作者可以创建新的内容片段或编辑现有的内容片段。在发布内容之前，作者可以预览它在客户端中的外观，方式是与开发人员合作，将内容模型推送到开发中，或设置一个开发人员环境以仅供作者预览它在客户端中的外观。

## 设置 {#setup}

在开始使用 AEM Headless 之前，您需要确保已启用所有必需的功能。此部分概述了所需项目。在 [AEM Headless 开发人员历程](#overview.md)中，稍后将详细介绍完成这些步骤所需的实际步骤。

您也可以选择参考[其他资源](#additional-resources)，了解有关各个主题的更多信息。

### 配置 {#configuration}

1. 启用内容片段
1. 启用 GraphQL
1. 设置 Headless SDK

## 实施您的第一个 AEM Headless 应用程序

这概述了使用 AEM 实施第一个 Headless 应用程序来交付内容所需的项目。Headless 开发人员历程的后面部分将详细描述如何执行这些步骤。

1. 创建内容片段模型
1. 创建内容片段
1. 使用 GraphQL 查询内容

## 最佳实践 {#best-practices}

Headless 项目之所以能够获得成功，既要归功于实施的技术，又要归功于良好的规划和项目治理。以下是您在规划项目时要牢记的面向内容作者和开发人员的大量最佳实践。

### 组织您的内容 {#organizing-content}

* 根据需要设定结构的复杂度，但尽可能使其保持简单。更简单的内容结构有助于简化内容监管并提高系统性能。
* 在策略中优先考虑内容重用。创建可跨多个更高级别的模型和渠道重用的子模型和内容引用。
* 尽可能使内容结构一目了然，以便内容作者能够快速学习并适应创作任务。
* 如果您具有访问限制，请尝试使内容模型符合访问要求。
* 如果您有访问要求，它们应推动您的内容层级。将由同一组人员编辑的内容组合在一起。
* 将相似内容分组到一个文件夹中。
   * 内容作者更有可能复制并粘贴现有内容来创建新内容。因此，在同一文件夹中完成此操作会更高效。
   * AEM 允许为每个文件夹设置允许的模型，因此，**新建**&#x200B;按钮将仅显示该位置支持的模型。
* 如果在模型中设置根文件夹，则可以简化新内容片段的内联内容片段编辑器创建。之后，从业人员不必选择位置，只需提供名称即可开始编辑新引用。

### 创作内容 {#authoring}

* 对于内容的渠道特定版本，请考虑使用内容片段变体。变体针对内容母版进行同步，以简化内容更改管理。
* 邀请其他内容制作者审查内容并提供带注释和评论的反馈，它们在内容片段编辑器中可用，并且可以在内容片段 Admin Console 中跨片段全局使用。
* 使用尽可能少的强制性元素来继续操作。强制性元素会阻止工作流。

### 创作全局内容 {#localization}

* 建立适用于内容翻译的规则和治理。要减少系统负载，可以将翻译构建为一个可按较长间隔运行的异步过程。留出时间进行本地化质量控制和错误修复。
* 利用翻译技术系统提供的所有功能，可以将这些功能与 AEM 集成（例如翻译记忆库）。
* 了解图像和视频等富媒体内容是否需要进行本地化。

## 后续内容 {#what-is-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 了解有关设计内容的重要规划注意事项。
* 了解在 AEM 中实施 Headless 的步骤。
* 了解需要哪些必要的工具和 AEM 配置。
* 了解使您的 Headless 历程顺畅、使内容生成保持高效并确保快速交付内容的最佳实践。

我们希望您基于此基础知识来充分了解 AEM Headless 的强大功能和灵活性，以便您能够将其用于自己的项目。为此，您有以下选择。

### 选择您自己的冒险 {#choose-your-path}

无论您的学习风格如何，Adobe 都希望您在开始使用 AEM Headless 项目时获得成功。

* 如果您更喜欢继续&#x200B;**了解 Headless 概念和 AEM 的 Headless 技术**，您应继续您的 AEM Headless 历程，即接下来查看文档[如何将内容建模为 AEM 内容模型](model-your-content.md)，您可从中了解如何在 AEM 中为内容结构建模。
* 如果您更喜欢&#x200B;**通过实践学习**，则可以跳转到 [AEM Headless 快速入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans)，在该教程中，您将实施一个简单项目来公开 AEM Headless 内容，从而直接跳转到 AEM Headless 开发。

## 其他资源 {#additional-resources}

我们建议您查看文档[如何将内容建模为 AEM 内容模型](model-your-content.md)来继续 Headless 开发历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续 Headless 历程所必需的。

* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md) - 此文档历程可让您全面了解 Headless 技术、AEM 如何提供 Headless 内容以及如何翻译 Headless 内容。
* [AEM Sites 的 Headless 开发](/help/sites-developing/headless/introduction.md) - 简要介绍如何帮助 AEM Headless 开发人员熟悉必要的功能
* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 使用这些动手实践教程，探究如何使用各种选项通过 AEM 将内容交付到 Headless 端点，并选择适合您的选项。
* [使用 GraphQL API 进行 Headless 内容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) – 在本课程中大致了解在 AEM 中实施的 GraphQL API。需要通过 AdobeID 进行的身份验证。
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) – 此 GitHub 项目包含突出显示 AEM 的 GraphQL API 的示例应用程序。
* [Headless快速入门指南](/help/sites-developing/headless/introduction.md#getting-started)  — 向已了解AEM的用户简要介绍AEM Headless功能。
* [创建内容片段模型](/help/assets/content-fragments/content-fragments-models.md) – 有关内容片段模型的技术文档
* [创建内容片段](/help/assets/content-fragments/content-fragments.md) – 有关内容片段的技术文档
* [使用 GraphQL 查询内容](/help/assets/content-fragments/graphql-api-content-fragments.md) – 关于 GraphQL API 的技术文档
