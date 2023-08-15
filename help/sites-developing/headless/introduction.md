---
title: 适用于AEM 6.5站点的Headless开发
description: 了解AEM 6.5强大的Headless功能(如内容模型、内容片段和GraphQL API)如何协同工作，让您能够集中管理体验并跨渠道提供这些体验。
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 36%

---

# 适用于AEM 6.5站点的Headless开发 {#headless-development}

了解AEM 6.5强大的Headless功能(如内容模型、内容片段和GraphQL API)如何协同工作，让您能够集中管理体验并跨渠道提供这些体验。

## 概述 {#overview}

Headless实施在向受众提供体验方面，变得日益重要，无论他们身在何处，也不论他们使用何种渠道。

Headless 实施放弃了传统的全栈和混合解决方案中的页面和组件管理，专注于创建渠道中性的、可重用的内容片段，以及它们的跨渠道投放。这是一种现代化的动态开发模式，用于实施 Web 体验。

![AEM 实施模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Headful 和 Headless 的比较 {#headful-headless}

本文档重点介绍AEM的完整Headless实施模型。 但是，在AEM中，Headful与Headless不一定是一个二选一的选择。 Headless功能可用于将您的内容管理和交付到各种端点，同时还使内容作者可以编辑单页应用程序。 这些都可在 AEM 中实现。

>[!TIP]
>
>有关更多信息，请参阅文档 [AEM 中的 Headful 和 Headless](/help/sites-developing/headful-headless.md)。

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是适用于Headless实施模型的灵活工具，它提供了三种强大的服务：

1. 内容模型
   * 内容模型是内容的结构化表示方式。
   * 这些功能由信息架构师在AEM内容片段模型编辑器中定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容由内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets并在Assets Admin UI中进行管理。
1. 用于投放的内容 API
   * AEM GraphQL API 支持内容片段投放。
   * AEM Assets REST API 支持内容片段 CRUD 操作。
   * 也可以使用直接内容投放 [内容片段核心组件的JSON导出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)

## 使用 AEM Headless 的第一步 {#first-steps}

有许多资源可供您开始使用AEM Headless功能。 它们适用于不同的用例，但它们都为AEM Headless功能提供了可靠的概述。

| 资源 | 描述 | 类型 | 受众 | 估计用时 |
|---|---|---|---|---|
| [Headless 开发人员历程](/help/journey-headless/developer/overview.md) | **适用于初次使用AEM和Headless的用户** 技术，从这里开始全面了解AEM及其Headless功能，从Headless的理论直到您的第一个Headless项目。 | 指南 | **刚开始接触 AEM 和 Headless** 的开发人员 | 1 小时 |
| [Headless 快速入门指南](/help/sites-developing/headless/getting-started/introduction.md) | **面向有经验的 AEM 用户**，在需要关键 AEM Headless 功能的简短摘要时，可以查看此快速入门概览。 | 快速入门 | **具有 AEM 经验**&#x200B;的开发人员、管理员 | 20 分钟 |
| [AEM Headless快速入门实践教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=zh-Hans) | **如果您偏好实践方法并且熟悉AEM**，本教程将直接深入到创建简单的Headless项目。 | 教程 | 开发人员 | 2 小时 |
