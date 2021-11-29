---
title: 'AEM 6.5站点的无头开发 '
description: 了解AEM 6.5的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。
source-git-commit: 03285545d8cc04d97513fb5fee3b3c616551ccdc
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 2%

---


# AEM 6.5站点的无头开发 {#headless-development}

了解AEM 6.5的无头功能（如内容模型、内容片段和GraphQL API）如何协同工作，从而让您能够集中管理您的体验并跨渠道提供它们。

## 概述 {#overview}

无头实施对于向受众提供体验越来越重要，无论这些体验位于何处，也不论渠道如何。

与传统的全栈和混合解决方案一样，无头实施可用于页面和组件管理，并着重于创建渠道中性、可重复使用的内容片段及其跨渠道交付。 它是一种用于实施Web体验的现代化、动态开发模式。

![AEM实施模型](assets/aem-implementation-models.png)

## 比较头部和无头部 {#headful-headless}

本文档重点介绍AEM的完整无头实施模型。 但是，在AEM中，“头部”与“无头”不必是二进制选择。 无标题功能可用于管理内容并将其交付到各种端点，同时还允许内容作者编辑单页应用程序。 全部在AEM中。

<!-- HM-Links
>[!TIP]
>
>See the document [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) for more information.
-->

## AEM 6.5和Headless {#aem-headless}

AEM 6.5是一款适用于无头实施模型的灵活工具，它提供了三项强大的服务：

1. 内容模型
   * 内容模型是内容的结构化表示形式。
   * 这些量度由AEM内容片段模型编辑器中的信息架构师定义。
   * 内容模型用作内容片段的基础。
1. 内容片段
   * 内容片段是内容模型的实例化。
   * 这些内容由内容作者使用AEM内容片段编辑器创建。
   * 它们存储在AEM Assets中，并在资产管理UI中进行管理。
1. 用于交付的内容API
   * AEM GraphQL API支持内容片段交付。
   * AEM Assets REST API支持内容片段CRUD操作。
   * 此外，还可以通过 [内容片段核心组件的JSON导出。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## 使用AEM Headless实现首要步骤 {#first-steps}

您可以使用许多资源来开始使用AEM无头功能。 这些功能适用于不同的用例，但都可以充分概述AEM的无头功能。

| 资源 | 描述 | 类型 | 受众 | 是。 时间 |
|---|---|---|---|---|
| [AEM Headless动手操作入门教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **如果您喜欢实际操作方法并熟悉AEM**，本教程将直接深入探讨如何创建一个简单的无头项目。 | 教程 | 开发人员 | 2小时 |

<!-- HM-Links
|Resource|Description|Type|Audience|Est. Time|
|---|---|---|---|---|
|[Headless Developer Journey](/help/journey-headless/developer/overview.md)|**For users new to AEM and headless** technologies, start here for a comprehensive introduction to AEM and its headless features from the theory of headless through going live with your first headless project.|Guide|Developers **new to AEM and headless**|1 hour|
|[Headless Getting Started Guide](/help/implementing/developing/headless/getting-started/introduction.md)|**For experienced AEM users** who need a short summary of the key AEM headless features, check out this quick start overview.|Quick Start|Developers, Administrators **with AEM experience**|20 minutes|
|[Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)|**If you prefer a hands-on approach and are familiar with AEM**, this tutorial dives directly into creating a simple headless project.|Tutorial|Developers|2 hours|
-->
