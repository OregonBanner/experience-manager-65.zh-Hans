---
title: 使用Adobe Experience Manager创作无头
description: 介绍Adobe Experience Manager强大、灵活、无头的功能，以及如何为项目创作内容。
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 90%

---

# 使用 AEM 为 Headless 创作 – 简介 {#author-headless-introduction}

在 [AEM Headless内容创作历程](overview.md)，您可以了解使用Adobe Experience Manager(AEM)创作无头内容交付所需的（基本）概念和术语。

## 目标 {#objective}

* **受众**：初学者
* **目标**：介绍与 Headless 创作相关的概念和术语。

## 内容管理系统 (CMS) {#content-management-system}

什么是内容管理系统？

顾名思义，内容管理系统 (CMS) 是一种用于管理内容的计算机系统。这有点笼统，更准确地说，它（通常）用于管理您希望在您的网站上提供的内容。

## Headless CMS {#headless-cms}

Headless 是一个用来描述系统的术语，指的是有效地将内容与其在 Web 页面中的展示方式分离开来。

传统上，您将在 CMS 中管理您的内容，并且同一 CMS 将负责在您的网页上渲染该内容。

现在，Headless 意味着您的内容集可在 CMS 中进行管理，然后由一个或多个（独立的）应用程序访问。

这意味着，您的内容可采用一系列广泛的格式传送到任意设备。这将使整个过程变得更加灵活，同时意味着您无需担心版面和格式设置。

>[!NOTE]
>
>如果您想详细了解 Headless CMS 的技术细节，可以参阅“了解 CMS Headless 开发”中的更多内容。

## Adobe Experience Manager {#aem-cms}

那么，什么是 AEM 呢？

首先，AEM 是一个具有一系列广泛功能的内容管理系统，也可以自定义这些功能以满足您的要求。

这都意味着它可以用作：

* Headless CMS
   * 对于 Headless 来说，可以将内容创作为&#x200B;**内容片段**。
它们是独立内容项，可以由一系列应用程序直接访问，因为它们具有基于**内容片段模型**的预定义结构。
这意味着您的内容可采用一系列广泛的格式与多种功能一起传输到多种设备。
（如果需要，也可以在构建 AEM 网页时使用这些片段，为您带来双倍效果。）

* “传统”CMS
   * 内容是为网页创作的，并使用一系列组件来定义内容在网站上的呈现方式。即使在这样的情况下，AEM 也非常灵活，因为您的项目团队可以开发自定义组件。

## 内容建模 {#content-modeling}

内容建模（也称为数据建模）是另一个技术术语。作为作者，您为什么会对它感兴趣呢？

要使 Headless 应用程序能够访问并处理您的内容，您的内容需要具有预定义的结构。您的内容可以采用自由格式，但这会使应用程序的生命周期变得&#x200B;*非常*&#x200B;复杂。

基本上，在定义内容要遵循的结构的过程中需要设计模型，这称作数据建模。

对于 AEM，内容架构师角色（通常是不同的人员）将执行数据建模以设计一系列&#x200B;**内容片段模型**，随后，您将通过使用&#x200B;**内容片段**&#x200B;来将该模型用作内容的基础。

>[!NOTE]
>
>如果您想了解有关数据建模的更多信息，可以参阅“AEM Headless 内容架构师历程”下的更多内容。

## 后续内容 {#whats-next}

现在您已了解概念和术语，下一步是[学习有关创作内容片段的基础知识](basics.md)。这将介绍 AEM 的基本处理以及如何创作内容片段。

## 其他资源 {#additional-resources}

* AEM Headless 开发人员历程
   * [了解 CMS Headless 开发](/help/journey-headless/developer/learn-about.md)

* [AEM Headless 内容架构师历程](/help/journey-headless/architect/overview.md)

* [AEM Headless 内容翻译历程](/help/journey-headless/translation/overview.md)
