---
title: AEM Headless 开发人员历程
description: AEM Headless CMS 文档。从这里开始，引导您了解AEM强大而灵活的Headless特性、它们的功能以及如何在您的第一个开发项目中使用它们。
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 76%

---

# AEM Headless 开发人员历程 {#aem-headless-developer-journey}

从这里开始，引导您了解AEM强大而灵活的Headless特性、它们的功能以及如何在您的第一个Headless开发项目中使用它们。 此历程提供了开发您的第一个Headless应用程序所需的所有AEM Headless文档。

## 简介 {#introduction}

Headless 实施放弃了传统的全栈解决方案中的页面和组件管理，专注于创建渠道中性的、可重用的内容片段，以及它们的跨渠道交付。这是一种现代化的动态开发模式，用于实施数字体验。

本指南将指导您逐步了解AEM中最常用的Headless实施主题，以便在完成后：

* 完全了解 Headless 内容交付的含义和好处。
* 了解 AEM 的 Headless 功能以及它们如何协作以提供 Headless 体验。
* 有能力迈出实施您的第一个 AEM Headless 项目的第一步。

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想了解 Adobe 就如何使用 AEM 解决 Headless 业务案例提出的建议，则可以从 [AEM Headless 历程](/help/journey-headless/home.md)开始。

>[!TIP]
>
>如果您愿意 **通过实践学习** 具有技术倾向的AEM Headless教程，这些教程按API和框架组织，可在 [其他资源部分](#additional-resources) 本文档末尾。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐释了 AEM Headless 项目的要求、步骤和方法。此历程将定义开发人员为成功实施项目而必须与之互动的其他角色，但历程的观点是开发人员的观点。

以下是在此历程中互动的角色。

| 角色 | 描述 | 此历程中的角色 |
|---|---|---|
| 开发人员（目标受众） | 拥有开发使用不同来源内容的 Headless 应用程序的经验 | 此历程的目标受众 |
| 内容作者 | 创建和管理以 Headless 方式交付的内容 | 内容作者创建开发人员以 Headless 方式交付的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 开发人员与管理员合作以进行开发所需的配置更改。 |
| 内容架构师 | 分析必须以 Headless 方式交付的数据的要求并定义此数据的结构 | 开发人员与内容架构师合作，了解数据结构和以 Headless 方式交付数据的要求。 |

此历程中的信息对所有角色都很有用，但一些信息可能对特定角色来说是多余的。 请继续关注[即将推出的涵盖其他角色的历程。](/help/journey-documentation/home.md#journeys)

## Headless 开发人员历程 {#the-journey}

您将在此历程中探究多个主题。以下文章为您提供了 AEM 中的 Headless 的基础知识以及指向详细技术文档的链接。

虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是初次使用 AEM 中的 Headless，Adobe 建议您从头开始，然后循序渐进。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless 开发人员历程 | 本文档 |
| 1 | [了解 CMS Headless 开发](learn-about.md) | 了解 Headless 技术以及何时使用它。 |
| 2 | [AEM Headless 快速入门](getting-started.md) | 了解 AEM Headless 先决条件 |
| 3 | [首次 AEM Headless 使用体验的路径](path-to-first-experience.md) | 设置您的开发环境并了解如何将简单的应用程序与 AEM Headless 集成 |
| 4 | [如何为您的内容建模](model-your-content.md) | 了解如何为您的内容结构建模。之后，使用内容片段模型和内容片段实施 Adobe Experience Manager (AEM) 的结构以便跨渠道重用。 |
| 5 | [如何通过 AEM 交付 API 访问您的内容](access-your-content.md) | 了解如何使用 GraphQL 查询来访问您的内容片段内容。 |
| 6 | [如何通过 AEM Assets API 更新您的内容](update-your-content.md) | 了解如何使用 REST API 来访问和更新您的内容片段内容。 |
| 7 | [如何汇总您的应用程序和 AEM Headless 中的内容](put-it-all-together.md) | 了解如何获取您的 AEM Project 并准备好使用 AEM Headless SDK 上线。 |
| 8 | [如何使用 Headless 应用程序上线](go-live.md) | 了解如何实时部署应用程序，在Git中获取本地代码并将其移动到Cloud Manager Git中以用于CI/CD管道。 |
| 9 | [可选 – 如何使用 AEM 创建单页应用程序 (SPA)](create-spa.md) | 了解AEM Headless功能后，探索如何将Headless投放与Headless投放结合使用，并了解如何使用AEM SPA Editor框架创建可编辑的SPA。 |

## 后续内容 {#what-is-next}

您现在已准备好开始您的 Adobe Headless 历程。我们鼓励您继续此历程的下一部分，并阅读此文章 [了解CMS Headless开发。](learn-about.md)

### 选择您自己的冒险 {#choose-your-path}

但是，Adobe希望您能够在开始使用AEM Headless项目时取得成功，无论您的学习方式如何。 所以，考虑一下这两个选项。

* 如果您更喜欢继续&#x200B;**了解 Headless 概念和 AEM 的 Headless 技术**，您应按照建议继续您的 AEM Headless 历程，即接下来查看文档[如何将内容建模为 AEM 内容模型](model-your-content.md)，您可从中了解如何在 AEM 中为内容结构建模。
* 如果您更喜欢&#x200B;**通过实践学习**，则可以跳转到 [AEM Headless 快速入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans)，在该教程中，您将实施一个简单项目来公开 AEM Headless 内容，从而直接跳转到 AEM Headless 开发。

## 其他资源 {#additional-resources}

文档历程将提供叙述来指导您完成复杂、相互关联的流程和使用相关功能，从而向您说明 AEM 如何解决业务问题。历程说明了多项功能如何协作以满足单一业务需求。

因此，旅程旨在自立。 但是，其中多个可以相互关联。 查看这些附加历程，详细了解 AEM 的强大功能如何协作。

* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 如果您更喜欢通过实践学习并有技术倾向，请参阅我们的按 API 和框架编排的实践教程，探究如何创建和使用基于 AEM Headless 的应用程序。
* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md) – 此文档历程可让您全面了解 Headless 技术、AEM 如何提供 Headless 内容以及如何翻译 Headless 内容。
* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [Headless架构师历程](/help/journey-headless/architect/overview.md)  — 从这里开始了解Adobe Experience Manager强大而灵活的Headless功能，以及如何对项目内容进行建模。
* [AEM 技术文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans) – 如果您对 AEM 和 Headless 技术的了解颇为扎实，则您可能想要直接查阅我们详尽的技术文档。

   * [AEM as a Headless CMS 简介](/help/sites-developing/headless/introduction.md)

* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
