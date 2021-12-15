---
title: AEM Headless Content Architect历程
description: 介绍Adobe Experience Manager强大、灵活、无头的功能，以及如何为项目建立内容模型。
index: true
hide: false
hidefromtoc: false
source-git-commit: 99e7bb800da659fb8494eef2d9b9b87a6f263c21
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# 使用AEM实现无头内容建模 — 简介 {#architect-headless-introduction}

在 [AEM Headless Content Architect历程](overview.md)，您可以了解了解使用Adobe Experience Manager(AEM)进行无头内容交付的内容建模所需的（基本）概念和术语。

本文档可帮助您了解无头内容交付、AEM如何支持无头，以及如何为无头内容建模。 阅读后，您应该：

* 了解无头内容交付的基本概念。
* 熟悉AEM如何支持无头和内容建模。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍与无头内容建模相关的概念和术语。

## 全栈内容交付 {#full-stack}

自从易于使用的大型内容管理系统(CMS)兴起以来，各公司一直利用它们作为管理报文传送、品牌推广和通信的中心位置。 将CMS用作管理体验的中心点，通过消除在不同系统中重复任务的需要，提高了效率。

![经典的全栈CMS](/help/journey-headless/developer/assets/full-stack.png)

在全栈CMS中，用于处理内容的所有功能都在CMS中。 系统的功能构成了CMS堆栈的不同组件。 全栈解决方案具有许多优势。

* 有一个系统需要维护。
* 内容是集中管理的。
* 系统的所有服务都已集成。
* 内容创作是无缝的。

因此，如果需要添加新渠道或支持新类型的体验，则可以在堆栈中插入一个（或多个）新组件，并且只有一个位置进行更改。

![向堆栈中添加新渠道](/help/journey-headless/developer/assets/adding-channel.png)

但是，堆栈中依赖项的复杂性会很快变得明显，因为堆栈中的其他项目需要调整以适应更改。

## 无头的头 {#the-head}

任何系统的头通常是该系统的输出渲染器，通常以GUI或其他图形输出的形式。

当我们讨论无头CMS时，CMS会管理内容并继续向消费者提供内容。 但是，通过仅提供 **内容** 无头CMS以标准化方式忽略最终输出渲染，从而将 **演示文稿** 内容到消费服务。

![无头CMS](/help/journey-headless/developer/assets/headless-cms.png)

消费性服务(无论是AR体验、网店、移动体验、渐进式Web应用程序(PWA)等)从无头CMS中获取内容并提供自己的呈现。 他们负责为您的内容提供自己的头脑。

省略头部通过消除复杂性来简化CMS。 这样做还会将呈现内容的责任转移到实际需要内容且通常更适合此类呈现的服务上。

## 内容建模 {#content-modeling}

内容建模（也称为数据建模）是您的专长，因此在为无头进行建模时需要考虑哪些因素？

要使无头应用程序能够访问您的内容并使用它执行一些操作，内容真正需要具有预定义的结构。 你的内容可以是自由形式的，但它可以让你的生活 *非常* 应用程序非常复杂。

对于AEM，作为内容架构师，您将执行内容建模以设计一系列 **内容片段模型**. 这些定义了内容作者在创建 **内容片段** 来保存内容。

### 访问内容 {#access-content}

这更像是一个开发细节 — 但你可能会感兴趣，只是为了完成故事。

创建内容片段模型并且作者使用它们生成内容后，无标题应用程序将需要访问此内容。

Adobe Experience Manager(AEM)可以使用AEM GraphQL API有选择地访问您的内容片段，以仅返回所需的内容。 开发人员可以使用API来制定查询以选择特定内容。此选择过程基于 *您的* 内容片段模型。

这意味着您的项目可以实现结构化内容的无头交付，以供在您的应用程序中使用。

## 下一步 {#whats-next}

既然您已经学习了概念和术语，下一步就是 [了解使用内容片段模型建模的基础知识](basics.md).

## 其他资源 {#additional-resources}

* AEM Headless开发人员历程
   * [了解CMS无头开发](/help/journey-headless/developer/learn-about.md)
   * [了解如何对内容进行建模](/help/journey-headless/developer/model-your-content.md)
