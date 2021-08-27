---
title: 通过GraphQL使用内容片段交付无头内容
description: 了解如何将AEM内容片段与GraphQL结合使用来进行无头内容交付。
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# 通过GraphQL使用内容片段交付无头内容 {#headless-content-delivery-using-content-fragments-with-graphQL}

借助Adobe Experience Manager(AEM)，您可以使用内容片段和AEM GraphQL API（一种基于标准GraphQL的自定义实施）来无头地交付结构化内容，以供在您的应用程序中使用。 通过自定义单个API查询的功能，您可以检索和交付您想要/需要渲染的特定内容（作为对单个API查询的响应）。

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>GraphQL当前用于Adobe Experience Manager(AEM)中的两个（单独）方案：
>
>* [AEM Commerce通过GraphQL从商务平台使用数据](/help/commerce/cif/integrating/magento.md)。
>* [AEM内容片段可与AEM GraphQL API（一种基于标准GraphQL的自定义实施）一起使用，来提供结构化内容以供在应用程序中使用](/help/assets/content-fragments/graphql-api-content-fragments.md)。


## 无头CMS {#headless-cms}

无头内容管理系统(CMS)包括：

* &quot;*无头内容管理系统或无头CMS是从头开始构建的仅后端内容管理系统(CMS)，作为内容存储库，使内容可通过API访问以在任何设备上显示。*

   请参阅[Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system)。

在AEM中创作内容片段时，这意味着：

* 您可以使用内容片段创作主要不打算在带格式的页面上直(1:1)发布的内容。

* 内容片段的内容将按照预先确定的方式 — 根据内容片段模型进行构建。 这简化了对应用程序的访问，这将进一步处理您的内容。

## GraphQL — 概述 {#graphql-overview}

GraphQL是：

* &quot;*...API的查询语言和用于使用现有数据执行这些查询的运行时。*&quot;。

   请参阅[GraphQL.org](https://graphql.org)

[AEM GraphQL API](#aem-graphql-api)允许您对[内容片段](/help/assets/content-fragments/content-fragments.md)执行（复杂）查询；每个查询都根据特定的模型类型。 然后，您的应用程序可以使用返回的内容。

## AEM GraphQL API {#aem-graphql-api}

对于Adobe Experience，已开发标准GraphQL API的自定义实施。 有关详细信息，请参阅[AEM GraphQL API以与内容片段](/help/assets/content-fragments/graphql-api-content-fragments.md)一起使用。

AEM GraphQL API实施基于[GraphQL Java库](https://graphql.org/code/#java)。

## 用于AEM GraphQL API的内容片段 {#content-fragments-use-with-aem-graphql-api}

[内](#content-fragments) 容片段可用作AEM查询的GraphQL的基础，如下所示：

* 它们允许您设计、创建、组织和发布独立于页面的内容。
* [内容片段模型](#content-fragments-models)通过定义的数据类型提供所需的结构。
* 定义模型时可用的[片段引用](#fragment-references)可用于定义其他结构层。

![与GraphQLContent片段一起使](assets/cfm-nested-01.png "用的内容片段与GraphQL一起使用")

### 内容片段 {#content-fragments}

内容片段:

* 包含结构化内容。

* 它们基于[内容片段模型](#content-fragments-models)，该模型为生成片段的结构进行了预定义。

### 内容片段模型 {#content-fragments-models}

以下[内容片段模型](/help/assets/content-fragments/content-fragments-models.md):

* 在&#x200B;**Enabled**&#x200B;之后，用于生成[Schema](https://graphql.org/learn/schema/)。

* 提供GraphQL所需的数据类型和字段。 它们确保您的应用程序仅请求可能的内容，并接收预期内容。

* 数据类型&#x200B;**[片段引用](#fragment-references)**&#x200B;可在模型中使用以引用其他内容片段，因此可引入其他级别的结构。

### 片段引用 {#fragment-references}

**[片段引用](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* 与GraphQL结合使用时特别感兴趣。

* 是可在定义内容片段模型时使用的特定数据类型。

* 引用另一个片段，具体取决于特定的内容片段模型。

* 用于检索结构化数据。

   * 当定义为&#x200B;**多源**&#x200B;时，主片段可以引用（检索）多个子片段。

### JSON预览 {#json-preview}

为帮助设计和开发内容片段模型，您可以预览[JSON输出](/help/assets/content-fragments/content-fragments-json-preview.md)。

## 了解如何将GraphQL与AEM结合使用 — 示例内容和查询 {#learn-graphql-with-aem-sample-content-queries}

请参阅[了解如何将GraphQL与AEM结合使用 — 示例内容和查询](/help/assets/content-fragments/content-fragments-graphql-samples.md)，以了解有关使用AEM GraphQL API的简介。

## 教程 — AEM Headless和GraphQL快速入门

正在查找动手实践教程？ 请参阅[AEM无头和GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)端到端入门教程，其中演示了如何在无头CMS方案中使用AEM GraphQL API构建和公开内容，以及如何使用外部应用程序使用的内容。
