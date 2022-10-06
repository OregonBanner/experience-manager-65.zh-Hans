---
title: AEM Headless开发人员历程
description: AEM Headless CMS 文档。从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个开发项目中利用它们。
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 29%

---

# AEM Headless开发人员历程 {#aem-headless-developer-journey}

从此处开始，您可以引导您逐步了解AEM强大而灵活的无头功能、其功能，以及如何在您的第一个无头开发项目中利用这些功能。 此历程为您提供开发首个无头应用程序所需的所有AEM无头文档。

## 简介 {#introduction}

与全栈解决方案中的传统方式一样，无头实施可用于页面和组件管理，并且重点关注创建不依赖于渠道、可重复使用的内容片段及其跨渠道交付。 它是一种实现数字体验的现代化、动态的开发模式。

本指南将引导您完成AEM中最无头的实施主题，以便您在完成该工作后：

* 充分了解无头内容交付的含义及其好处。
* 了解AEM无头功能以及它们如何协同工作来提供无头体验。
* 能够采取实施首个AEM无头项目的首要步骤。

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想了解Adobe如何建议如何使用AEM解决无头业务案例， [AEM无头历程](/help/journey-headless/home.md) 是开始的位置。

>[!TIP]
>
> 如果您愿意 **学习** 从技术上讲，您可以访问AEM Headless教程，这些教程由API和框架组织，在 [“其他资源”部分](#additional-resources) 在本文档末尾。

## 受众 {#audience}

此历程专为开发人员角色设计，从开发人员的角度阐述AEM Headless项目的要求、步骤和方法。 历程定义了其他角色，开发人员必须与这些角色进行交互才能使项目取得成功，但历程的视角是开发人员的视角。

以下是在此历程中互动的角色。

| 角色 | 描述 | 此历程中的角色 |
|---|---|---|
| 开发人员（目标受众） | 具有开发无头应用程序的经验，这些应用程序使用来自不同来源的内容 | 此历程的目标受众 |
| 内容作者 | 创建并管理无头投放的内容 | 内容作者创建开发人员随意交付的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 开发人员与管理员合作，进行开发所需的配置更改。 |
| 内容架构师 | 对必须无头传送的数据要求进行分析，并定义此数据的结构 | 开发人员与内容架构师合作，以了解数据的结构和无头提供数据的要求。 |

虽然此历程中的信息对所有角色都很有用，但一些信息可能对特定角色来说是多余的。请继续关注[即将推出的涵盖其他角色的历程。](/help/journey-documentation/home.md#journeys)

## 无头开发人员历程 {#the-journey}

您将在此历程中探究多个主题。以下文章为您提供了有关AEM中无头的基础知识，并链接到详细的技术文档。

虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是初次接触AEM中的无头用户，我们建议您从头开始，然后按顺序前进。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless开发人员历程 | 本文档 |
| 1 | [了解 CMS Headless 开发](learn-about.md) | 了解无头技术以及何时使用它。 |
| 2 | [AEM Headless 快速入门](getting-started.md) | 了解AEM Headless先决条件 |
| 3 | [首次 AEM Headless 使用体验的路径](path-to-first-experience.md) | 设置开发环境，并了解如何将简单的应用程序与AEM Headless集成 |
| 4 | [如何对内容进行建模](model-your-content.md) | 了解如何对内容结构进行建模。 然后，使用内容片段模型和内容片段实现Adobe Experience Manager(AEM)的结构，以便跨渠道重复使用。 |
| 5 | [如何通过 AEM 投放 API 访问您的内容](access-your-content.md) | 了解如何使用GraphQL查询访问内容片段内容。 |
| 6 | [如何通过 AEM Assets API 更新您的内容](update-your-content.md) | 了解如何使用REST API访问和更新内容片段内容。 |
| 7 | [如何将所有内容整合在一起 — 在AEM Headless中查看您的应用程序和内容](put-it-all-together.md) | 了解如何获取您的AEM项目并为使用AEM Headless SDK进行上线做准备。 |
| 8 | [如何使用 Headless 应用程序上线](go-live.md) | 了解如何在Git中实时部署应用程序并获取本地代码，然后将其移至Cloud Manager Git for CI/CD管道。 |
| 9 | [可选 — 如何使用AEM创建单页应用程序(SPA)](create-spa.md) | 了解AEM无标题功能后，请了解如何结合使用无标题和无标题交付，并了解如何使用AEM SPA编辑器框架创建可编辑的SPA。 |

## 下一步 {#what-is-next}

现在，您已准备好开始AdobeHeadless历程。 我们鼓励您继续访问历程的下一部分并阅读文章 [了解CMS无头开发。](learn-about.md)

### 选择您自己的冒险 {#choose-your-path}

但是，无论您的学习风格如何，Adobe都希望您在开始使用AEM Headless项目时取得成功。 所以请考虑这两个选项。

* 如果您希望继续 **了解无头概念和AEM无头技术**，则您应该继续您的AEM无头历程，方法是接下来查看文档 [如何将内容建模为AEM内容模型](model-your-content.md) 其中，您了解如何在AEM中构建内容结构模型。
* 如果您愿意 **学习**，您可以跳转到 [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans) 在这里，您将通过实施一个简单的项目来公开AEM无头内容，从而直接进入AEM开发。

## 其他资源 {#additional-resources}

文档历程向您展示了AEM如何通过提供说明来解决业务问题，说明如何指导您完成复杂且相互关联的流程和功能。 历程说明了多个功能如何协同工作来满足单个业务需求。

因此，这些旅程旨在独立进行。 但是，其中的许多内容可以相互关联。 请查看这些其他历程，了解有关AEM强大功能如何协同工作的更多信息。

* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 如果您更喜欢通过实践学习并有技术倾向，请参阅我们的按 API 和框架编排的实践教程，探究如何创建和使用基于 AEM Headless 的应用程序。
* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)  — 此文档历程使您能够广泛了解无头技术、AEM如何提供无头内容以及如何翻译无头内容。
* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [无外设架构师历程](/help/journey-headless/architect/overview.md)  — 从此处开始，介绍Adobe Experience Manager强大而灵活的无头功能，以及如何为您的项目建立内容模型。
* [AEM 技术文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans) – 如果您已对 AEM 和 Headless 技术有一定的了解，则可能需要直接参阅深入的技术文档。
