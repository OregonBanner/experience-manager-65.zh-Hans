---
title: AEM 6.5站点的无头开发
description: 了解AEM 6.5的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# AEM 6.5站点的无头开发 {#headless-development}

了解AEM 6.5的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。

## 概述 {#overview}

无头实施对于向受众提供体验越来越重要，无论这些体验位于何处，也不论渠道如何。

Headless 实施放弃了传统的全栈和混合解决方案中的页面和组件管理，专注于创建渠道中性的、可重用的内容片段，以及它们的跨渠道投放。这是一种现代化的动态开发模式，用于实施 Web 体验。

![AEM 实施模型](assets/aem-implementation-models.png)

## Headful 和 Headless 的比较 {#headful-headless}

本文档重点介绍AEM的完整无头实施模型。 不过，在 AEM 中，Headful 与 Headless 不一定是一个二选一的选择。无标题功能可用于管理内容并将其交付到各种端点，同时还允许内容作者编辑单页应用程序。 这些都可在 AEM 中实现。

>[!TIP]
>
>有关详细信息，请参阅 [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md)。

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是一款适用于无头实施模型的灵活工具，它提供了三项强大的服务：

1. 内容模型
   * 内容模型是内容的结构化表示方式。
   * 这些量度由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容由内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets中，并在资产管理UI中进行管理。
1. 用于投放的内容 API
   * AEM GraphQL API 支持内容片段投放。
   * AEM Assets REST API 支持内容片段 CRUD 操作。
   * 此外，还可以通过 [内容片段核心组件的JSON导出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)

## 使用 AEM Headless 的第一步 {#first-steps}

您可以使用许多资源来开始使用AEM无头功能。 这些功能适用于不同的用例，但都可以充分概述AEM的无头功能。

| 资源 | 描述 | 类型 | 受众 | 估计用时 |
|---|---|---|---|---|
| [Headless 开发人员历程](/help/journey-headless/developer/overview.md) | **对于初次使用AEM和Headless的用户** 技术，请从此处全面介绍AEM及其无头功能（从无头理论到使用您的第一个无头项目）。 | 指南 | **刚开始接触 AEM 和 Headless** 的开发人员 | 1 小时 |
| [Headless 快速入门指南](/help/sites-developing/headless/getting-started/introduction.md) | **面向有经验的 AEM 用户**，在需要关键 AEM Headless 功能的简短摘要时，可以查看此快速入门概览。 | 快速入门 | **具有 AEM 经验**&#x200B;的开发人员、管理员 | 20 分钟 |
| [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans) | **如果您喜欢实际操作方法并熟悉AEM**，本教程将直接深入探讨如何创建一个简单的无头项目。 | 教程 | 开发人员 | 2 小时 |
