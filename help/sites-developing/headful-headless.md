---
title: AEM 中的 Headful 和 Headless
description: AEM项目可以采用无头和无头模型来实施，但选择不是二进制的。 AEM可以灵活地在一个项目中利用这两个模型的优势。
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# AEM 中的 Headful 和 Headless {#headful-headless}

Adobe Experience Manager项目可以在头部和无头两种模型中实施，但选择不是二进制的。 AEM可以灵活地在一个项目中利用这两个模型的优势。 本文档概述了不同的模型并描述了SPA集成的级别。

## 概述 {#overview}

AEM提供了强大的工具，可在一个平台中管理内容的创建及其交付。 这是一种传统的“头戴式”内容管理模型，内容作者和开发人员在同一平台上工作，以向内容消费者提供体验。

AEM还可用于简单地管理内容，从而允许由其他平台管理内容的演示和交付。 这是内容管理的“无头”模型，内容作者和开发人员在不同的平台上工作，以向内容消费者提供体验。

但这不一定是二选一。 AEM提供了前所未有的灵活性，允许您利用这两个模型在项目中的优势。

![AEM 实施模型](headless/assets/aem-implementation-models.png)

在标题式或全堆栈式模型中，内容基于Java、HTL等在AEM存储库和AEM组件中进行管理。 用于呈现用户体验的内容。 在此模型中，可在AEM中创建内容、为其设置样式、演示内容并交付所有内容。

在无头模型中，内容在AEM存储库中进行管理，但通过REST和GraphQL等API交付到其他系统，以呈现用户体验的内容。 在此模型中，内容是在AEM中创建的，但是会为其设置样式、呈现内容并在其他平台上交付所有内容。

单页应用程序(SPA)通常是AEM无缝交付内容的目标。 但是，这些SPA不必完全是AEM的外部组件。 AEM允许您决定将SPA集成到AEM的程度。 让我们举个例子。

## Web Shop示例 {#web-shop-example}

假设您现有一个Web商店，供您的公司用作SPA。 其中包含您的所有产品详细信息和图像。 然后，您将引入AEM以支持营销工作，如促销网站、博客和营销活动内容。 如何将二者相结合？ AEM可启用一系列选项：

* **允许系统独立运行。**
* **通过GraphQL从AEM中为Web商店提供有限的内容。** 内容可由作者在AEM中创建，但只能通过Web商店SPA查看。
* **在AEM中嵌入Web Shop SPA。** 内容可由作者在AEM中创建，并在AEM的Web Shop上下文中查看，但不能进行操作。
* **在AEM中嵌入Web Shop SPA，并启用可编辑的点。** 内容可由作者在AEM中创建，并在AEM中在Web Shop的上下文中查看，而且作者在AEM中处理Web Shop SPA内容的能力有限。
* **在AEM中嵌入网页商店SPA，并启用整个区域进行编辑。** 内容可由作者在AEM中创建，并在AEM中在Web Shop的上下文中查看，而且作者在AEM中处理Web Shop SPA内容的能力有限。

下一节将更详细地探讨这些级别的集成。

>[!NOTE]
>
>当然，您还可以将Web Shop SPA作为一个功能完备的AEM SPA进行重新实施 [使用AEM SPA Editor框架。](/help/sites-developing/spa-walkthrough.md) 如果您已经拥有AEM，并且希望创建新的Web商店或其他SPA，则建议使用此方法，但此方法不在本文档的涵盖范围内。

## SPA集成级别 {#integration-levels}

SPA集成属于AEM中的四个级别。

* **级别0:无集成**
   * SPA和AEM单独存在，且不交换任何信息。
   * 内容是在两个不同的系统中独立创建、管理和交付的。
* **级别1:内容片段集成**
   * [内容片段](/help/assets/content-fragments/content-fragments.md) 用于创建和管理SPA的有限内容。
   * SPA通过AEM检索此内容 [GraphQL API。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 某些内容在AEM中进行管理，而某些内容则在外部系统中管理。
   * 内容只能在SPA中查看。
* **级别2:在AEM中嵌入SPA**
   * [内容片段](/help/assets/content-fragments/content-fragments.md) 用于创建和管理SPA的内容。
   * SPA通过AEM检索此内容 [GraphQL API。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 某些内容在AEM中进行管理，而某些内容则在外部系统中管理。
   * 可以在AEM内在上下文中查看内容。
   * 可以在AEM中编辑有限的内容。
* **第3级：在AEM中嵌入并完全启用SPA**
   * [内容片段](/help/assets/content-fragments/content-fragments.md) 用于创建和管理SPA的内容。
   * SPA通过AEM检索此内容 [GraphQL API。](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * 可以在AEM内在上下文中查看内容。
   * 大多数内容都可以在AEM中编辑。

1级是典型无头实施的示例。 但是，内容作者只能在SPA中在上下文中查看其内容。 AEM只是一个创作工具。

在级别2和级别3中，AEM的优势和灵活性变得显而易见，同时仍保留SPA的优势。 内容作者可以在AEM中创建其内容，但也可以在AEM中在上下文中查看内容。 SPA具有在AEM中创作的功能，但仍作为SPA提供。

## 实施集成级别 {#implementing}

AEM中提供了不同的工具，具体取决于您选择的集成级别。 每个级别都基于上一个级别中使用的工具。 以下列表链接到相关资源。

* **级别1:** 内容片段和 [AEM headless框架](/help/sites-developing/headless/introduction.md) 用于将AEM内容交付到SPA。
* **级别2:** 除第一级外：
   * [RemotePage组件](/help/sites-developing/spa-remote-page.md) 可用于将外部SPA嵌入到AEM中，以便在上下文中查看AEM内容。
   * SPA上的某些点也可以 [允许在AEM中进行有限编辑。](/help/sites-developing/spa-edit-external.md)
* **第3级：** 除第二级外：
   * 可以启用SPA的整个区域，以便在AEM中进行全面编辑。
