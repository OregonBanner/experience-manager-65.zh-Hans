---
title: AEM Headless 快速入门
description: 在AEM Headless开发人员历程的这一部分中，了解AEM Headless的先决条件。
source-git-commit: 919cef01470dd930884e97b15f2d40a38872c0d0
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 1%

---

# AEM Headless 快速入门 {#getting-started}

在 [AEM Headless开发人员历程,](overview.md) 了解开始使用AEM Headless时需要满足哪些条件才能开始您自己的项目。

## 迄今为止的故事 {#story-so-far}

在AEM无头历程的上一个文档中， [了解CMS无头开发](learn-about.md) 您学习了无头CMS的基本理论，您现在应该：

* 了解无头内容交付的基本概念和术语
* 了解为何需要无头
* 在高级别了解无头概念的使用方式及其相互关系

本文基于这些基础知识，以便您了解如何使用AEM来实施无外设解决方案。

## 目标 {#objective}

本文档可帮助您在自己项目的上下文中了解AEM Headless。 阅读后，您应该：

* 了解AEM无头功能的基础知识。
* 了解使用AEM无头功能的先决条件。
* 请注意AEM无头集成级别。
* 能够根据范围定义项目。

## AEM基础知识 {#aem-basics}

在AEM中定义无头项目之前，请务必了解一些基本的AEM概念。

### 创作实例 {#author}

最简单的方法是， AEM包含一个创作实例和一个 [发布实例](#publish) 可共同创建、管理和发布您的内容。

内容从创作实例开始。 这是内容作者创建其内容的位置。 创作环境为作者提供了各种工具，用于创建、组织和重复使用其内容。

### 发布实例 {#publish}

在创作实例中创建内容后，必须将其发布以供其他服务使用。 发布实例包含已发布的所有内容。

### 复制 {#replication}

复制是将内容从创作实例传输到发布实例的操作。 当作者或其他具有相应权限的用户发布内容时，AEM会自动执行此操作。

### AEM基础知识摘要 {#aem-basics-summary}

在最简单的级别上，在AEM中创建数字体验需要执行以下步骤：

1. 内容作者在创作实例中创建无标题内容。
1. 此内容准备就绪后，会复制到发布实例。
1. 然后，可以调用API以检索此内容。

AEM Headless通过提供功能强大的工具来管理无头内容(这是 [在下一节中进行描述。](#aem-headless-basics)

## AEM Headless基础知识 {#aem-headless-basics}

AEM的无头功能基于一些关键特性。 在历程的后半部分中对这些内容进行了详细解释。 现在，只要了解他们的基本操作和所谓，就很重要了。

### 内容片段模型 {#content-fragment-models}

内容片段模型定义您在AEM中创建和管理的数据和内容的结构。 它们是你内容的脚手架。 选择创建内容时，作者从您定义的内容片段模型中进行选择，这将指导他们创建内容。

### 内容片段 {#content-fragments}

内容片段允许您设计、创建、策划和发布独立于页面的内容。 利用这些功能，可准备内容以准备在多个位置和多个渠道上使用。

内容片段包含结构化内容，可以采用JSON格式交付。

### GraphQL和REST API {#apis}

为了无拘无束地修改内容，AEM提供了两个强大的API。

* GraphQL API允许您创建访问和交付内容片段的请求。
* 资产REST API允许您创建和修改内容片段（和其他资产）。

您将在AEM无头历程的后续部分中了解这些API以及如何使用它们。 或者，请参阅 [其他资源](#additional-resources) 部分以了解其他文档。

## 无头集成级别 {#integration-levels}

AEM支持CMS的全无头模型和传统的全栈或头模型。 但是，AEM不仅提供了这两种独有的选择，还提供了支持混合模型的功能，该混合模型结合了两者的优势，为您的无头项目提供了独特的灵活性。

为确保您了解无头概念，此AEM无头开发人员历程重点介绍纯无头模型，以便您尽快启动并运行，而无需在AEM中进行编码。

但是，您应该了解了解AEM无头功能后，您还会看到其他混合可能性。 下面列出了这些案例，供您了解。 在历程结束时，您将更详细地介绍这些概念，以防您的项目需要这种灵活性。

### 您已经对无标题内容进行了外部使用，例如单页应用程序(SPA)。 {#already-have-a-spa}

假设您的基本要求至少是要将内容从AEM交付到现有的外部服务。

#### 级别1:内容片段集成 — 传统无头模型 {#level-1}

此级集成是传统的无头模型，允许内容作者在AEM中创建内容，并使用GraphQL将内容无头地交付给任意数量的外部服务，或使用Assets API从外部服务编辑这些服务。 在AEM中不需要编码。

在此模型中，AEM仅用于使用AEM内容片段创建和提供内容。 呈现内容以及与内容的交互被委派给消费型外部应用程序，通常是单页应用程序(SPA)。

#### 级别2:将SPA嵌入AEM — 混合模型 {#level-2}

此级别的集成构建于第一级之上，但也允许将外部应用程序(SPA)嵌入到AEM中，以便内容作者可以在AEM内的外部应用程序上下文中查看内容。 该应用程序还支持在AEM中对外部应用程序进行有限编辑。

此级别的优势在于，允许内容作者以标题方式在AEM中灵活创作内容，其内容与嵌入的外部SPA呈现在上下文中，同时仍无拘无束地交付内容。

#### 第3级：在AEM中嵌入和完全启用SPA — 混合模型 {#level-3}

此级别的集成在级别2的基础上构建，具体方法是：允许外部SPA中的大多数内容在AEM中可编辑。

### 您还没有无头内容的外部用户，例如单页应用程序(SPA)。 {#do-not-have-a-spa}

如果您的目标是创建一个无头地使用AEM内容的新SPA，则可以使用内容片段等功能管理您的无头内容，还可以使用AEM SPA编辑器框架构建SPA。

使用SPA编辑器，SPA不仅会使用AEM中的内容，而且内容作者还可以在AEM中完全编辑，从而让您既能够灵活地进行无标题交付，又能够在AEM中进行上下文编辑。

## 要求和先决条件 {#requirements-prerequisites}

在开始您的无外设AEM项目之前，有许多要求。

### 知识 {#knowledge}

* GraphQL
* 使用React或SPA框架创建Angular的开发经验
* 基本AEM技能：创建内容片段和使用编辑器

### 工具 {#tools}

* 用于测试部署项目的沙盒访问
* 用于数据建模和测试的本地开发实例
* 您的无头SPA内容的现有外部AEM或其他使用者

## 定义项目 {#defining-your-project}

对于任何成功的项目，不仅要明确项目的要求，还要明确其角色和责任。

### 范围 {#scope}

必须为项目明确界定范围。 范围会告知接受标准，并允许您确定“完成”的定义。

您必须问的第一个问题是“我尝试使用AEM Headless实现什么？” 答案通常应该是，您将来拥有或将拥有一个体验应用程序，该应用程序是您使用自己的开发工具而不是AEM构建的。 此体验应用程序可以是移动设备应用程序、网站，或任何其他面向客户的最终用户体验应用程序。 使用AEM Headless的目标是使用最新的API，为您的体验应用程序提供在AEM中创建、存储和管理的内容，这些API将调用AEM Headless以直接从您的体验应用程序中获取内容，甚至是完全CRUD内容。 如果这不是你想做的，你可能想 [返回到AEM文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans) 找到更适合您想要实现的部分。

### 角色和职责 {#roles-responsibilities}

任何单个项目的角色各不相同，但在AEM无头开发内容中需要考虑的重要角色包括：

* [管理员](#administrator)
* [内容作者](#content-author)
* [内容架构师](#content-architect)
* [开发人员](#developer)

#### 管理员 {#administrator}

管理员负责系统的基本设置和配置。 例如，管理员在Adobe用户管理系统(称为Identity Management系统(IMS))中设置您的组织。 管理员是组织中第一个在IMS中通过Adobe创建组织后从Adobe收到电子邮件邀请的用户。 管理员能够登录IMS并添加其他角色的用户。

管理员配置用户后，他们将有权访问所有AEM资源，以完成其作为使用AEM Headless交付体验应用程序贡献者的工作。

管理员应是设置AEM并准备要启用的运行时环境的用户 [内容作者](#content-author) 创建和更新内容 [开发人员](#developer) 用于获取或修改其体验应用程序内容的API。

#### 内容作者 {#content-author}

内容作者创建并管理由AEM无头地交付的内容。 内容作者使用AEM功能（如内容片段和资产控制台）管理其内容。

内容作者应牢记以下最佳实践。

#### 翻译计划 {#translation}

在项目开始时计划翻译。 将“翻译专家”视为单独的角色，其职责是定义哪些内容应被翻译、哪些不应被翻译，哪些翻译内容可能由区域或本地内容制作者修改。

创建所需内容翻译的计划。

* 您是否需要不同的语言或语言才能适应地区具体情况？
* 您是否需要富媒体内容（如图像或视频）在不同区域设置中有所不同？

请明确您的内容更新工作流程。 系统必须支持哪些审批流程？ 是否可以利用AEM工作流来自动执行此过程？

请注意，您的 [内容层次结构](#content-hierarchy) 可简化翻译。

请参阅 [其他资源](#additional-resources) 部分以了解有关AEM工作流和翻译工具的其他文档，包括指向AEM无头翻译历程的链接。

##### 利用内容层次结构 {#content-hierarchy}

文件夹层次结构可以解决与内容管理有关的两个主要问题：

* [翻译](#translation) - AEM通过维护特定于区域设置的文件夹中的内容副本来管理内容翻译。
* 组织 — 文件夹用于定义支持翻译需求所需的内容层次结构，以及在逻辑上管理内容片段。

AEM允许灵活的内容结构，并且层级可以任意大。 但是，必须认识到，对文件夹结构所做的任何更改都可能会对现有查询产生意想不到的后果 [依赖内容路径。](#developer) 因此，预先明确定义的层级结构对内容作者可能会有所帮助。

文件夹也可以限制为仅允许某些类型的内容（基于内容片段模型）。 建议始终明确指定允许使用哪些模型来访问层次结构中的所有文件夹。 为给定文件夹指定允许的内容：

* 阻止内容作者创作不属于该文件夹的内容。
* 通过筛选创建期间文件夹中允许的内容类型来优化内容创建过程，以仅显示有效类型的内容。

通过创建适当的内容结构，可以更轻松地跨渠道协调无头内容创作，以最大限度地重复利用内容。 跨多个渠道利用内容可极大地提高内容生产效率和更改管理。

##### 建立良好的命名约定 {#naming-conventions}

内容片段名称必须为内容作者提供描述性。 AEM可透明地处理转义和/或截断存储库级别上使用的ID的名称。 因此，内容作者提供的逻辑名称应始终可读并表示内容。

* 错误名称： `cta_btn_1`
* 好名： `Call To Action Button`

请参阅 [其他资源](#additional-resources) 部分以了解有关AEM页面命名约定的其他文档。

##### 不要过度嵌套内容 {#content-nesting}

[内容片段](#content-fragments) 用于创建无头内容。 AEM最多支持对内容片段嵌套10级内容。 但是，请务必记住，AEM必须迭代解析父内容片段中定义的每个引用，然后检查所有同级中是否存在任何子引用。 这些操作可以快速加总，并成为性能问题。

作为一般经验法则，内容片段引用不应嵌套在五个级别以上。

#### 内容架构师 {#content-architect}

内容架构师会分析必须毫无头绪地提供数据的要求，并定义此数据的结构。 这些结构称为 [内容片段模型](#content-fragment-models) 在AEM中。 内容片段模型用作内容作者创建的内容片段的基础。

定义内容片段模型时的一种有用方法是创建映射到使用内容的应用程序的UX组件的模型。

由于内容作者在创建新内容时会不断与模型交互，因此将模型与UX保持一致有助于他们可视化最终的数字体验。 更进一步地，您可以向内容片段模型分配表示UX元素的图标，以便作者能够根据视觉提示直观地选择正确的模型。

#### 开发人员 {#developer}

开发人员负责将在AEM中无头创建的内容与该内容的消费者连接在一起，这些内容通常可以是单页应用程序(SPA)、渐进式Web应用程序(PWA)、Web Shop或AEM外部的其他服务。

GraphQL充当AEM与无头内容使用者之间的“胶水”。 GraphQL是用于查询AEM所需内容的语言。

开发人员在规划其查询时应牢记一些基本建议：

* 查询不应依赖于固定路径(`ByPath`)来检索内容片段。
   * [内容作者对内容片段层次结构具有完全控制权](#content-hierarchy) 和可以做出会破坏此类查询的更改。
   * 相反，查询应选择包含动态查询参数的内容片段模型引用，以筛选结果以生成所需的有效负载。
* 为获得最佳查询性能，请始终在AEM中使用持久查询。 这些内容将在历程的后面进行讨论。
* GraphQL是遵循以下格言的声明性内容：“请求您确切需要的内容，并准确获取这些内容。” 这意味着在创建GraphQL查询时，应始终避免 `select *`-type查询，您可以在关系数据库中创建该查询。

对于 [使用AEM的典型无头实施，](#level-1) 开发人员不需要AEM的编码知识。

### 性能要求 {#performance-requirements}

要使任何项目成功，必须在创建任何内容之前考虑性能。

您必须了解用户/访客对这些方面的期望和设计。 设置服务级别目标(SLO)并衡量这些目标，以了解您是否满足用户的期望。

#### 流量模式 {#traffic-patterns}

要了解流量和流量模式，首先要收集您过去所了解的信息，然后预测未来几年的预期增长。 需要考虑的一些最重要的变量：

* 您预计每小时/天/月会有多少个API调用，并且有可能出现峰值和季节性？
* 有多少个不同的内容作者？
* 您预计有多少内容作者同时工作？
* 内容更新的频率是多少？
* 需要多少个内容模型？
* 需要多少个模型实例？

#### 更新频度 {#update-frequency}

通常，不同体验部分的内容更新频率不同。 了解这一点对于能够优化CDN和缓存配置非常重要。 这也是 [内容架构师](#content-architects) 设计模型来表示您的内容。 请考虑：

* 某些类型的内容是否会在特定时间段后过期？
* 是否有特定于用户的元素，因此无法缓存？

## 下一步 {#what-is-next}

现在，您已完成AEM Headless开发人员历程的这一部分，接下来您应该：

* 了解AEM无头功能的基础知识。
* 了解使用AEM无头功能的先决条件。
* 请注意AEM无头集成级别。
* 能够根据范围定义项目。

您应该通过下一步审阅文档来继续您的AEM无头历程 [使用AEM Headless获得首个体验的路径](path-to-first-experience.md) 您将在何处了解如何设置必要的工具，以及如何开始考虑在AEM中建模数据。

## 其他资源 {#additional-resources}

虽然建议您通过审阅文档来进入无头开发历程的下一部分 [使用AEM Headless获得首个体验的路径，](path-to-first-experience.md) 以下是一些其他可选资源，可更深入地了解本文档中提到的某些概念，但无需继续进行无头历程。

* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)  — 此文档历程使您能够广泛了解无头技术、AEM如何提供无头内容以及如何翻译无头内容。
* [AEM无头Tutorials](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)  — 使用这些动手实践教程探索如何使用各种选项通过AEM将内容交付到无头端点，并选择适合您的选项。
* [使用GraphQL API的无头内容管理](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses)  — 请阅读本课程，概述在AEM中实施的GraphQL API。 需要通过AdobeID进行身份验证。
* [AEM指南WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql)  — 此GitHub项目包括高亮显示AEM GraphQL API的示例应用程序。
* [创作概念](/help/sites-authoring/author.md)  — 有关AEM创作环境的技术文档，包括有关创作 — 发布设置的详细信息
* [发布页面](/help/sites-authoring/publishing-pages.md)  — 在AEM上发布内容的技术文档
* [命名约定](/help/sites-developing/naming-conventions.md) - AEM中页面命名限制的技术文档
* [多站点管理器与翻译](/help/sites-administering/msm-and-translation.md)  — 关于AEM强大翻译功能的技术文档
* [AEM工作流](/help/sites-authoring/workflows.md)  — 有关如何在AEM中自动执行工作流的技术文档
* [内容片段](/help/assets/content-fragments/content-fragments.md)  — 内容片段技术文档。
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 有关内容片段模型的技术文档。
* [GraphQL技术文档](https://graphql.org) - GraphQL定义（外部链接）
* [GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)  — 说明如何创建访问和交付内容片段的请求的技术文档
* [资产REST API](/help/assets/assets-api-content-fragments.md)  — 说明如何创建和修改内容片段（和其他资产）的技术文档
* [持久化查询](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching)  — 关于AEM中保留查询的技术文档
* [AEM中的Headful和Headless](/help/sites-developing/headful-headless.md)  — 完整讨论AEM中可用的无头集成级别
