---
title: 了解如何在内容片段中使用引用
description: 了解如何在内容片段中对内容、其他片段和其他资源（媒体）使用引用。介绍 Headless CMS 创作的嵌套片段的必要性和机制。
exl-id: d54a0a40-a8af-456a-9bf5-219d84540c97
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 95%

---

# 了解如何在内容片段中使用引用 {#author-headless-references}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[简介](introduction.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

您已学习 Headless CMS 创作的基础知识，并大致了解如何使用 AEMaaCS 进行创作，尤其是创作内容片段。

本文基于这些内容编写，以便您了解如何使用引用来为 AEM Headless 项目创作您自己的内容。

## 目标 {#objective}

* **受众**：高级
* **目标**：介绍如何在 Headless CMS 创作中使用引用。提供了哪些类型的引用，它们的作用是什么：

   * 内容引用
   * 资源/媒体引用
   * 片段引用
   * 文本块中的临时引用

## 什么是引用？ {#what-are-references}

引用只是一种用于连接资源的机制，无论它是其他内容、资源（如图像）还是其他片段。虽然非常相似，但仍有些许不同。

一些引用具有专用数据类型（例如，内容引用和片段引用），而其他引用只是作为引用内容添加到文本块中（资源引用和临时引用）。

![内容片段 – 引用](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 内容引用 {#content-references}

内容引用仅用于此目的，可让您引用任何其他内容。 这将打开一个浏览器以便让您能够选择内容项。

## 资源/媒体引用 {#assets-media-references}

可以使用&#x200B;**插入资源**&#x200B;选项在文本块中引用资源（例如，图像或媒体）。这将打开一个浏览器以便您能够选择资源。

![内容片段 – 插入资源](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 片段引用 {#fragment-references}

片段引用也这样做 — 它们允许您引用另一个片段。 需要进一步说明它很重要的原因。

例如，您可能定义了以下内容片段模型：

* 城市
* 公司
* 人员
* 奖励

似乎很简单，一家公司肯定会有一个 CEO 和众多员工....他们每个人都被定义为一个人员。

一个人员可以获得一个（或两个）奖励。

* 我的公司 – 公司
   * CEO – 人员
   * 员工 – 人员
      * 个人奖励 – 奖励

这只适用于初学者。根据复杂性，奖励可以是特定于公司的，或者公司可以在特定城市设立主要办事处。

可以使用片段引用来表示这些相互关系，因为您（作者）和 Headless 应用程序都已理解它们。

作为作者，虽然您不负责定义这些关系（这项工作由内容架构师在创建内容片段模型时完成），但您需要知道如何识别和编辑引用。

### 如何创作嵌套片段 {#author-nested-fragment}

创作片段引用非常简单（尽管该字段通常将不被标记为&#x200B;**片段引用**）。您可以直接键入引用，或者（更有可能）选择文件夹图标以打开浏览器，以便导航并选择所需的片段。

![内容片段 – 引用](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

内容片段模型控件的定义：

* 是否能选择添加多个引用
* 您可以选择的内容片段的模型类型；内容片段模型定义允许引用的片段模型，因此 AEM 仅显示基于这些模型的片段。

### 如何导航嵌套片段 {#navigate-nested-fragment}

利用内容片段编辑器的&#x200B;**结构树**&#x200B;选项卡，您可以浏览您的片段所引用的片段，然后浏览它们可能包含的任何引用。选择引用会打开该片段进行编辑。

>[!NOTE]
>
>使用主面板中的痕迹导航，您可以导航回起始点。

![内容片段结构树](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 临时引用 {#adhoc-references}

临时引用可作为文本块中的简单链接添加：

![内容片段 – 临时引用](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 后续内容 {#whats-next}

现在您已了解内容片段中的引用和结构，下一步是[了解元数据和标记](metadata-tagging.md)。这将介绍和讨论如何为内容片段定义元数据和标记。

## 其他资源 {#additional-resources}

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [将配置应用到 Assets 文件夹](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [创建内容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [变体 - 创作片段内容](/help/assets/content-fragments/content-fragments-variations.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [内容片段模型 – 数据类型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [内容片段模型 – 属性](/help/assets/content-fragments/content-fragments-models.md#properties)

* 快速入门指南
   * [创建资源文件夹Headless快速入门指南](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless 内容架构师历程](/help/journey-headless/architect/overview.md)

* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md)
