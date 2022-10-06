---
title: AEM无头翻译历程
description: 从此处开始，使用AEM功能强大的翻译工具引导您翻译无头内容。
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 45%

---

# AEM无头翻译历程 {#aem-headless-translation-journey}

从此处开始，使用AEM功能强大的翻译工具引导您翻译无头内容。

## 简介 {#introduction}

无头实施对于向受众提供体验越来越重要，无论这些体验位于何处，也不管渠道、区域或区域设置如何。

与全栈解决方案中的传统方式一样，无头实施可用于页面和组件管理，并且重点关注创建不依赖于渠道、可重复使用的内容片段及其跨渠道交付。 通过使用AEM功能强大的翻译工具，这些可重复使用的片段可以轻松翻译并交付给受众，而无论其身在何处。

本指南将引导您完成最重要的无标题翻译主题，以便您在完成该工作后：

* 概述什么是无标题内容交付。
* 基本了解AEM无头功能。
* 了解AEM翻译功能以及它们与无标题内容的相关性。
* 能够开始翻译您自己的无头内容。

其目标是让您广泛了解无头技术、AEM如何提供无头内容以及如何翻译无头内容。 如果您不熟悉其中的任何主题，那么这里就是您的理想起点。

如果您已经熟悉AEM、无头和翻译，则可能已经拥有此历程的基本知识。 请考虑在 [其他资源部分。](#additional-resources)

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想了解Adobe如何建议如何使用AEM解决无头业务案例， [AEM无头历程](/help/journey-headless/home.md) 是开始的位置。

## 受众 {#audience}

此历程专为翻译专家角色（通常称为翻译项目经理 (TPM)）设计。此历程阐述了在AEM中翻译无标题内容的要求、步骤和方法。 此历程可能会定义翻译专家必须与之交互的其他角色，但历程的观点是翻译专家的观点。

此历程假定读者在大型CMS系统上具有翻译内容的经验，但不了解无头技术或AEM。

以下是在此历程中互动的角色。

| 角色 | 描述 | 历程中的角色 |
|---|---|---|
| 翻译专家 | 定义应翻译的内容并管理这些工作流 | 此历程的受众 |
| 内容作者 | 创建并管理无头投放的内容 | 内容作者创建翻译专家必须翻译的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 翻译专家与管理员共同进行翻译所需的配置更改，例如安装翻译连接器。 |
| 内容架构师 | 对必须无头传送的数据要求进行分析，并定义此数据的结构 | 翻译专家与内容架构师共同定义内容的编排以便轻松翻译。 |

虽然此历程中的信息对所有角色都很有用，但一些信息可能对特定角色来说是多余的。请继续关注[即将推出的涵盖其他角色的历程。](/help/journey-documentation/home.md#journeys)

## 无头翻译历程 {#the-journey}

您将在此历程中探究多个主题。以下文章为您提供了在AEM中翻译无标题内容并链接到详细技术文档的基本知识。

虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是初次使用AEM中的无标题翻译，我们建议您从头开始，然后按顺序进行。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM无头翻译历程 | 本文档 |
| 1 | [了解无标题内容以及如何在AEM中翻译](learn-about.md) | 了解无头概念、它们如何映射到AEM以及AEM翻译理论。 |
| 2 | [AEM Headless 翻译快速入门](getting-started.md) | 了解如何组织无头内容以及AEM翻译工具的工作方式。 |
| 3 | [配置翻译连接器](configure-connector.md) | 了解如何将 AEM 连接到翻译服务。 |
| 4 | [配置翻译规则](translation-rules.md) | 了解如何定义翻译规则，标识要翻译的内容。 |
| 5 | [翻译内容](translate-content.md) | 使用翻译连接器和规则翻译无头内容。 |
| 6 | [发布翻译的内容](publish-content.md) | 了解如何发布翻译的内容并在更新基础内容时更新翻译。 |

## 下一步 {#what-is-next}

现在，您已准备好开始Adobe无头翻译历程。 我们鼓励您继续访问历程的下一部分并阅读文章 [了解无标题内容以及如何在AEM中翻译](learn-about.md)

## 其他资源 {#additional-resources}

文档历程向您展示了AEM如何通过提供说明来解决业务问题，说明如何指导您完成复杂且相互关联的流程和功能。 历程说明了多个功能如何协同工作来满足单个业务需求。

因此，这些旅程旨在独立进行。 但是，其中的许多内容可以相互关联。 请查看这些其他历程，了解有关AEM强大功能如何协同工作的更多信息。

* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [无外设架构师历程](/help/journey-headless/architect/overview.md)  — 从此处开始，介绍Adobe Experience Manager强大而灵活的无头功能，以及如何为您的项目建立内容模型。
* [AEM Headless 开发人员历程](/help/journey-headless/developer/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个开发项目中利用它们。
* [AEM 技术文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans) – 如果您已对 AEM 和 Headless 技术有一定的了解，则可能需要直接参阅深入的技术文档。
* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 如果您更喜欢通过实践学习并有技术倾向，请参阅我们的按 API 和框架编排的实践教程，探究如何创建和使用基于 AEM Headless 的应用程序。
