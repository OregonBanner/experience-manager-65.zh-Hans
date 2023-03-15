---
title: AEM Headless 内容架构师历程
description: 简单介绍Adobe Experience Manager强大而灵活的Headless功能，以及如何对项目内容进行建模。
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 89%

---

# 使用 AEM 对 Headless 进行内容建模 – 简介 {#architect-headless-introduction}

在这部分中 [AEM Headless内容架构师历程](overview.md)中，您可以学习必要的（基本）概念和术语，以了解通过Adobe Experience Manager (AEM)进行Headless内容投放的内容建模。

本文档可帮助您了解 Headless 内容交付、AEM 支持 Headless 的方式以及如何对 Headless 进行内容建模。阅读本文档后，您应：

* 了解 Headless 内容交付的基本概念。
* 熟悉 AEM 支持 Headless 和内容建模的方式。

## 目标 {#objective}

* **受众**：初学者
* **目标**：介绍与 Headless 内容建模相关的概念和术语。

## 全栈内容交付 {#full-stack}

自易于使用的大型内容管理系统 (CMS) 兴起以来，组织便已将其用作管理消息、品牌化和通信的中心位置。通过将 CMS 用作管理体验的中心点，消除了在不同的系统中重复任务的需求，从而提高了效率。

![经典全栈 CMS](/help/journey-headless/developer/assets/full-stack.png)

在全栈 CMS 中，用于操作内容的所有功能都在 CMS 中。该系统的各种功能构成了 CMS 堆栈的不同组件。全栈解决方案有许多优点。

* 需要维护一个系统。
* 集中管理内容。
* 系统的所有服务都是集成的。
* 内容创作是无缝进行的。

因此，如果需要添加新渠道或支持新类型的体验，可以将一个（或多个）新组件插入堆栈中，并且只能在一个位置进行更改。

![向堆栈添加新渠道](/help/journey-headless/developer/assets/adding-channel.png)

不过，当堆栈中的其他项目可能需要调整才能适应更改时，堆栈中依赖项的复杂性很快就会变得明显。

## Headless 中的头 {#the-head}

任何系统的头通常都是该系统的输出呈现器，通常采用 GUI 或其他图形输出的形式。

就 Headless CMS 而言，CMS 将管理内容并继续将内容交付给消费者。但是，通过仅以标准化方式交付&#x200B;**内容**，Headless CMS 会省略最终的输出呈现，而只保留要&#x200B;**呈现**&#x200B;给消费服务的内容。

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

消费服务（无论是 AR 体验、网上商店、移动体验、渐进式 Web 应用程序 (PWA) 等）都将从 Headless CMS 获取内容并提供它们自己的呈现。它们负责为您的内容提供它们自己的头。

忽略头将消除复杂性，从而简化 CMS。这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务。

## 内容建模 {#content-modeling}

内容建模（也称为数据建模）是您的专长，那么在对 Headless 进行建模时需要考虑什么呢？

要使 Headless 应用程序能够访问并处理您的内容，内容需要具有预定义的结构。您的内容可以采用自由格式，但这会使应用程序的生命周期变得&#x200B;*非常*&#x200B;复杂。

对于 AEM，作为内容架构师，您将执行内容建模来设计一系列&#x200B;**内容片段模型**。它们定义了内容作者在创建包含内容的&#x200B;**内容片段**&#x200B;时使用的结构。

### 访问内容 {#access-content}

这更像是开发详细信息 - 但您可能会它感兴趣，仅用于完成故事。

在您创建内容片段模型，并且您的作者已使用这些模型生成内容后，Headless 应用程序将需要访问此内容。

Adobe Experience Manager (AEM)可以选择使用AEM GraphQL API访问您的内容片段，以仅返回所需的内容。 利用 API，开发人员可以制定用于选择特定内容的查询。此选择过程基于&#x200B;*您的*&#x200B;内容片段模型。

这意味着您的项目可以实施结构化内容的 Headless 交付以便在您的应用程序中使用。

## 后续内容 {#whats-next}

现在您已了解概念和术语，下一步是[学习使用内容片段模型进行建模的基础知识](basics.md)。

## 其他资源 {#additional-resources}

* AEM Headless 开发人员历程
   * [了解 CMS Headless 开发](/help/journey-headless/developer/learn-about.md)
   * [了解如何为您的内容建模](/help/journey-headless/developer/model-your-content.md)
