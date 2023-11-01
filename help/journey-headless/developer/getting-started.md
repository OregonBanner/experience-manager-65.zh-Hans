---
title: AEM Headless 快速入门
description: 在 AEM Headless 开发人员历程的这一部分中，了解 AEM Headless 的先决条件。
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '3038'
ht-degree: 97%

---

# AEM Headless 快速入门 {#getting-started}

在 [AEM Headless 开发人员历程](overview.md)的这部分中，了解使用 AEM Headless 启动您自己的项目所需满足的条件。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 历程的上一个文档[了解 CMS Headless 开发](learn-about.md)中，您学习了 Headless CMS 的含义的基本理论，现在应：

* 了解 Headless 内容交付的基本概念和术语。
* 了解为什么需要以及何时需要 Headless
* 从较高层面了解如何使用 Headless 概念以及如何将它们相互关联

本文基于这些基础知识编写，以便您了解如何使用 AEM 实施 Headless 解决方案。

## 目标 {#objective}

本文档可帮助您在自己的项目上下文中了解 AEM Headless。阅读本文档后，您应：

* 了解 AEM 的 Headless 功能的基础知识。
* 了解使用 AEM 的 Headless 功能的先决条件。
* 了解 AEM 的 Headless 集成级别。
* 能够根据范围定义您的项目。

## AEM 基础知识 {#aem-basics}

在 AEM 中定义 Headless 项目之前，请务必了解一些基本的 AEM 概念。

### 创作实例 {#author}

最简单地说，AEM 由一个创作实例和一个[发布实例](#publish)构成，二者协同工作以创建、管理和发布您的内容。

内容在创作实例上开始。内容作者在该实例上创建内容。创作环境为作者提供了各种工具来创建、组织和重用他们的内容。

### 发布实例 {#publish}

在创作实例中创建内容后，必须发布内容以供其他服务使用。发布实例包含所有已发布的内容。

### 复制 {#replication}

复制是一项将内容从创作实例传输到发布实例的操作。当作者或其他具有适当权限的用户发布内容时，AEM 会自动完成此操作。

### AEM 基础知识摘要 {#aem-basics-summary}

在最简单的层面上，在 AEM 中创建数字体验需要执行以下步骤：

1. 您的内容作者在创作实例中创建您的 Headless 内容。
1. 在此内容准备就绪时，它会被复制到发布实例。
1. 之后，可以调用 API 来检索此内容。

AEM Headless 通过提供功能强大的工具来管理 Headless 内容来奠定这一技术基础，这将[在下一部分中介绍](#aem-headless-basics)。

## AEM Headless 基础知识 {#aem-headless-basics}

AEM 的 Headless 功能基于几项关键功能。历程的后面部分将详细解释这些功能。现在，只需要了解有关这些功能的用途和名称的基础知识。

### 内容片段模型 {#content-fragment-models}

内容片段模型定义您在 AEM 中创建和管理的数据及内容的结构。它们在某种程度上用作内容的基架。选择创建内容时，作者将从您定义的内容片段模型中选择，这会引导他们创建内容。

### 内容片段 {#content-fragments}

内容片段允许您设计、创建、管理和发布独立于页面的内容。 利用这些功能，可准备内容以用于多个位置和多个渠道。

内容片段包含结构化内容，可以采用 JSON 格式投放。

### GraphQL API 和 REST API {#apis}

为了以 Headless 方式修改您的内容，AEM 提供了两个功能强大的 API。

* GraphQL API 允许您创建请求来访问和投放内容片段。
* Assets REST API 让您创建和修改内容片段（及其他资源）。

您将在 AEM Headless 历程的后面部分中了解这些 API 及其使用者式。或参阅下面的[其他资源](#additional-resources)部分以获取其他文档。

## Headless 集成级别 {#integration-levels}

AEM 支持 CMS 的完全 Headless 模型和传统的全栈或 Headful 模型。然而，AEM 不仅提供了这两种独特的选择，还支持结合了两者优势的混合模型，从而让您的 Headless 项目具有独特的灵活性。

为了确保您理解 Headless 概念，此 AEM Headless 开发人员历程重点说明了纯 Headless 模型，使您无需在 AEM 中编码即可尽快启动并运行。

但是，在您了解 AEM 的 Headless 功能后，就应意识到额外的混合可能性。下面列出了这些情况以供您了解。在历程结束时，您将更详细地了解这些概念，以防您的项目需要这种灵活性。

### 您有 Headless 内容的外部使用者，例如单页应用程序 (SPA)。 {#already-have-a-spa}

假设您的基本要求是至少将内容从 AEM 交付到现有外部服务。

#### 级别 1：内容片段集成 - 传统 Headless 模型 {#level-1}

此集成级别是传统 Headless 模型，允许您的内容作者在 AEM 中创建内容，并使用 GraphQL 以 Headless 方式将内容交付给任意数量的外部服务，或者使用 Assets API 从外部服务编辑内容。无需在 AEM 中进行编码。

在此模型中，AEM 仅用于使用 AEM 内容片段创建和提供内容。内容的呈现和交互工作将委派给使用的外部应用程序，通常是单页应用程序 (SPA)。

#### 级别 2：将 SPA 嵌入 AEM 中 - 混合模型 {#level-2}

此级别的集成基于级别 1 构建，但也允许将外部应用程序 (SPA) 嵌入到 AEM 中，以便内容作者能够在 AEM 中外部应用程序的上下文中查看内容。该应用程序还可以支持在 AEM 中对外部应用程序进行有限的编辑。

此级别的优势是，允许内容作者以 Headful 方式在 AEM 中灵活地创作内容，其内容将通过嵌入式外部 SPA 在上下文中呈现，同时仍以 Headless 方式交付内容。

#### 级别 3：在 AEM 中嵌入并完全启用 SPA – 混合模型 {#level-3}

此级别的集成基于级别 2 构建，使外部 SPA 中的大部分内容都可在 AEM 中进行编辑。

### 您没有 Headless 内容的外部使用者，例如单页应用程序 (SPA)。 {#do-not-have-a-spa}

如果您的目标是创建一个新的 SPA 来以 Headless 方式使用 AEM 中的内容，则可以使用内容片段等功能来管理您的 Headless 内容，还可以使用 AEM 的 SPA 编辑器框架来构建 SPA。

借助 SPA 编辑器，SPA 不仅可以使用 AEM 中的内容，还可以由内容作者在 AEM 中进行完全编辑，这将使您能够在 AEM 中灵活地进行 Headless 交付和上下文编辑。

## 要求和先决条件 {#requirements-prerequisites}

在开始 Headless AEM 项目之前，需要满足许多要求。

### 知识 {#knowledge}

* GraphQL
* 有关使用 React 或 Angular 框架创建 SPA 的开发经验
* 有关创建内容片段和使用编辑器的基本 AEM 技能

### 工具 {#tools}

* 用于测试部署项目的沙盒访问
* 用于数据建模和测试的本地开发实例
* 您的 Headless AEM 内容的现有外部 SPA 或其他使用者

## 定义项目 {#defining-your-project}

对于任何成功的项目，请务必明确定义项目的要求以及角色和职责。

### 范围 {#scope}

请务必明确定义项目的范围。范围告知验收标准，并让您创建完成的定义。

您必须提出的第一个问题是“我尝试使用 AEM Headless 实现什么目标？”一般来说，答案应该是您拥有或将来会拥有您使用自己的开发工具而非 AEM 构建的体验应用程序。此体验应用程序可以是移动应用程序、网站或任何其他面向最终用户客户的体验应用程序。使用 AEM Headless 的目标是为您的体验应用程序提供在 AEM 中创建、存储和管理的内容，并使用最先进的 API 调用 AEM Headless 以直接从体验应用程序中获取内容甚至完整的 CRUD 内容。如果这不是您想执行的操作，您可能需要[返回 AEM 文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)，并找到更适合您要完成的操作的部分。

### 角色和职责 {#roles-responsibilities}

任意单个项目的角色各不相同，而在 AEM Headless 开发的内容中需要考虑的重要角色是：

* [管理员](#administrator)
* [内容作者](#content-author)
* [内容架构师](#content-architect)
* [开发人员](#developer)

#### 管理员 {#administrator}

管理员负责系统的基本设置和配置。例如，管理员在 Adobe User Management 系统（称为 Identity Management System (IMS)）中设置您的组织。Adobe 在 IMS 中创建您的组织后，管理员是组织中第一个收到来自 Adobe 的电子邮件邀请的用户。管理员可以登录 IMS 并添加其他角色的用户。

管理员配置用户后，将授予他们访问所有AEM资源的权限，以便他们作为参与者完成使用AEM Headless交付Experience应用程序的任务。

管理员应是负责以下工作的用户：设置 AEM 并准备运行时环境以使[内容作者](#content-author)能够创建和更新内容，并使[开发人员](#developer)能够使用 API 来获取或修改其体验应用程序的内容。

#### 内容作者 {#content-author}

内容作者创建和管理 AEM 以 Headless 方式交付的内容。内容作者使用内容片段和 Assets 控制台等 AEM 功能来管理其内容。

内容作者应牢记以下最佳实践。

#### 规划翻译 {#translation}

在项目的一开始就规划翻译。将“翻译专家”视为一个单独的角色，其职责是定义应翻译的内容、不应翻译的内容以及哪些已翻译内容可由区域或本地内容制作者修改。

根据需要的内容翻译制定计划。

* 您是否需要使用不同的语言来适应不同地区的具体情况？
* 您是否希望图像或视频等富媒体内容在不同的区域设置下有所不同？

清楚了解您的内容更新工作流。系统必须支持的审批流程是什么？是否能利用 AEM 工作流来自动实施此过程？

请注意，可以利用您的[内容层级](#content-hierarchy)来简化翻译。

请参阅[其他资源](#additional-resources)部分，了解有关 AEM 工作流和翻译工具的其他文档，包括指向 AEM Headless 翻译历程的链接。

##### 利用内容层级 {#content-hierarchy}

文件夹层级可以解决与内容管理有关的两个主要问题：

* [翻译](#translation) – AEM 通过在特定于区域设置的文件夹中维护内容副本来管理内容翻译。
* 组织 - 文件夹用于定义支持翻译需求以及逻辑管理内容片段所需的内容层级。

AEM 允许灵活的内容结构，并且层级可以任意大。不过，请务必了解一点，文件夹结构中的任何更改都可能对现有查询产生意外后果，这些查询[依赖内容路径。](#developer)因此，预先清楚列明的明确定义的层级可能对您的内容作者会很有用。

也可以将文件夹限制为仅允许某些类型的内容（基于内容片段模型）。建议始终明确指定层级中的所有文件夹允许哪些模型。为给定文件夹指定允许的内容：

* 防止内容作者创作不属于该文件夹的内容。
* 通过在创建期间过滤文件夹中允许的内容类型，以仅显示有效的内容类型来优化内容创建过程。

通过创建适当的内容结构，可以更轻松地跨渠道协调Headless内容创作，以最大限度地提高内容重复使用。 跨多个渠道利用内容可大大提高内容生产效率并增强更改管理。

##### 建立正确的命名惯例 {#naming-conventions}

对于内容作者而言，内容片段名称必须是描述性的。AEM 在存储库级别透明地处理转义和/或截断使用了 ID 的名称。因此，内容作者提供的逻辑名称应始终可读并代表内容。

* 错误名称：`cta_btn_1`
* 正确名称：`Call To Action Button`

有关 AEM 页面命名惯例的其他文档，请参阅[其他资源](#additional-resources)部分。

##### 不要过度扩展内容嵌套 {#content-nesting}

[内容片段](#content-fragments)在 AEM 中用于创建 Headless 内容。AEM 支持内容片段的最多 10 个层次的内容嵌套。不过，请务必记住，AEM 必须以迭代方式解析父内容片段中定义的每个引用，然后检查所有同级元素中是否有任何子引用。这些操作会快速累加并变成性能问题。

作为一般经验法则，内容片段引用的嵌套不应超过五层。

#### 内容架构师 {#content-architect}

内容架构师分析必须以 Headless 方式交付的数据的要求并定义此数据的结构。这些结构在 AEM 中称作[内容片段模型](#content-fragment-models)。内容片段模型用作内容作者创建的内容片段的基础。

定义内容片段模型时的有用方法是，创建映射到使用内容的应用程序的 UX 组件的模型。

由于内容作者在创建新内容时会持续与模型进行交互，因此，将模型与 UX 保持一致有助于它们可视化生成的数字体验。要提高一致性，您可以向表示 UX 元素的内容片段模型分配图标，以便作者能够根据视觉提示直观地选择正确的模型。

#### 开发人员 {#developer}

开发人员负责将在 AEM 中以 Headless 方式创建的内容交付给该内容的使用者，后者通常可以是单页应用程序 (SPA)、渐进式 Web 应用程序 (PWA)、网上商店或 AEM 外部的其他服务。

GraphQL 充当 AEM 和 Headless 内容使用者之间的“粘合剂”。GraphQL 是用于在 AEM 中查询必要内容的语言。

开发人员在计划查询时应记住几条基本建议：

* 查询不应依赖固定路径 (`ByPath`) 来检索内容片段。
   * [内容作者可以完全控制内容片段层级](#content-hierarchy)，并且可以进行将中断此类查询的更改。
   * 查询应改为选择具有动态查询参数的内容片段模型引用，以过滤结果来生成所需的负载。
* 要获得最佳查询性能，请始终在 AEM 中使用持久查询。历程的后面部分将对此进行讨论。
* GraphQL 是声明性的，它奉行的是“确切地询问您需要的东西，并准确地获得它。”这意味着，在创建 GraphQL 查询时，请始终避免可能在关系数据库中创建的 `select *` 类型的查询。

对于[使用 AEM 的典型 Headless 实施](#level-1)，开发人员无需了解 AEM 的编码知识。

### 性能要求 {#performance-requirements}

要使任何项目获得成功，在创建任何内容之前都必须考虑性能。

您必须了解用户/访客的期望并为此进行设计。设置服务水平目标 (SLO) 并进行衡量，了解您是否达到了用户期望。

#### 流量模式 {#traffic-patterns}

要了解流量和流量模式，首先要收集您过去了解的信息，然后预测未来几年的预期增长。需要考虑的一些最重要的变量是：

* 您预计每小时/每天/每月进行多少次 API 调用，是否有可能出现调用峰值和季节性调用？
* 有多少个不同的内容作者？
* 您预计有多少个内容作者同时工作？
* 内容更新的频率是多少？
* 需要多少个内容模型？
* 需要多少个模型实例？

#### 更新频率 {#update-frequency}

通常，不同的体验部分会具有不同的内容更新频率。了解这一点对于能够微调 CDN 和缓存配置非常重要。这也是[内容架构师](#content-architects)的重要输入，因为他们将设计模型来表示您的内容。请考虑：

* 某些类型的内容是否必须在一段时间后过期？
* 是否存在无法缓存的用户特定的元素？

## 后续内容 {#what-is-next}

现在您已完成 AEM Headless 开发人员历程的这一部分，您应：

* 了解 AEM 的 Headless 功能的基础知识。
* 了解使用 AEM 的 Headless 功能的先决条件。
* 了解 AEM 的 Headless 集成级别。
* 能够根据范围定义您的项目。

您应该继续您的 AEM Headless 历程，接下来查看文档[首次 AEM Headless 使用体验的路径](path-to-first-experience.md)，了解如何设置必要的工具以及如何开始思考如何在 AEM 中对数据建模。

## 其他资源 {#additional-resources}

我们建议您查看文档[首次 AEM Headless 使用体验的路径](path-to-first-experience.md)来继续 Headless 开发历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续 Headless 历程所必需的。

* [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md) – 对 AEM 中可用的 Headless 集成级别的完整讨论

* [AEM as a Headless CMS 简介](/help/sites-developing/headless/introduction.md)

* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md) – 此文档历程可让您全面了解 Headless 技术、AEM 如何提供 Headless 内容以及如何翻译 Headless 内容。

* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 使用这些动手实践教程探索如何使用通过 AEM 将内容投放到 Headless 端点的各种选项并选择适合您的选项。
* [使用 GraphQL API 进行 Headless 内容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) – 在本课程中大致了解在 AEM 中实施的 GraphQL API。需要通过 AdobeID 进行的身份验证。
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) – 此 GitHub 项目包含突出显示 AEM 的 GraphQL API 的示例应用程序。
* [创作概念](/help/sites-authoring/author.md) – 有关 AEM 的创作环境的技术文档，包括作者-发布设置的详细信息
* [发布页面](/help/sites-authoring/publishing-pages.md) – 有关在 AEM 上发布内容的技术文档
* [命名惯例](/help/sites-developing/naming-conventions.md) – 有关 AEM 中的页面命名限制的技术文档
* [多站点管理器和翻译](/help/sites-administering/msm-and-translation.md) – 有关 AEM 的强大翻译功能的技术文档
* [AEM 工作流](/help/sites-authoring/workflows.md) – 有关如何在 AEM 中自动实施工作流的技术文档
* [内容片段](/help/assets/content-fragments/content-fragments.md) – 有关内容片段的技术文档。
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) – 有关内容片段模型的技术文档。
* [GraphQL 技术文档](https://graphql.org) – GraphQL 定义（外部链接）
* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) – 说明如何创建请求来访问和交付内容片段的技术文档
* [Assets REST API](/help/assets/assets-api-content-fragments.md) – 说明如何创建和修改内容片段（及其他资源）的技术文档
* [持久查询](/help/sites-developing/headless/graphql-api/persisted-queries.md) – 有关 AEM 中的持久查询的技术文档
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)