---
title: 了解如何在内容片段中使用引用
description: 了解如何在内容片段、内容、其他片段和其他资产（媒体）中使用引用。 介绍无头CMS创作中嵌套片段的必要性和机制。
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# 了解如何在内容片段中使用引用 {#author-headless-references}

## 迄今为止的故事 {#story-so-far}

于 [AEM Headless内容创作历程](overview.md) the [简介](introduction.md) 介绍了与无头创作相关的基本概念和术语。

您通过对使用AEMaCS进行创作的介绍，特别是对内容片段的创作，学习了无头CMS创作的基础知识。

本文以这些内容为基础，以便您了解如何使用引用来为您的AEM无头项目创作您自己的内容。

## 目标 {#objective}

* **受众**:高级
* **目标**:介绍如何使用引用进行无头CMS创作。 提供了哪些类型的引用，以及其用途：

   * 内容引用
   * 资产/媒体引用
   * 片段引用
   * 来自文本块中的临时引用

## 引用内容 {#what-are-references}

引用只是连接资源的一种机制，无论是其他内容、资产（如在图像中一样）还是其他片段。 虽然非常相似，但也存在一些差异。

某些引用具有专用数据类型（例如，内容引用和片段引用），而其他引用则只是作为引用添加到文本块（资产引用和临时引用）中。

![内容片段 — 引用](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## 内容引用 {#content-references}

内容引用仅可执行此操作 — 它们允许您引用任何其他内容。 这将打开一个浏览器，用于选择内容项目。

## 资产/媒体引用 {#assets-media-references}

可以在文本块中通过使用 **插入资产** 选项。 这将打开一个浏览器，用于选择资产。

![内容片段 — 插入资产](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## 片段引用 {#fragment-references}

同样，片段引用也做到了这一点 — 它们允许您引用其他片段。 为什么这很重要，需要多一点解释。

例如，您可能定义了以下内容片段模型：

* 城市
* 公司
* 人员
* 奖项

看起来很简单，但公司当然有CEO和员工…….这些都是人，每个人都定义为人。

一个人可以获得一个奖（或两个奖）。

* 我的公司 — 公司
   * 首席执行官 — 人员
   * 员工 — 人员
      * 个人奖 — 奖

这只是开始。 根据复杂性，奖项可以是特定于公司的，或者公司可以在特定的金融城设立其主要办事处。

使用片段引用可以表示这些相互关系，因为您（作者）和无标题应用程序都了解这些关系。

作为作者，您不负责定义这些关系（由内容架构师在创建内容片段模型时完成），但您需要了解如何识别和编辑引用。

### 如何创作嵌套片段 {#author-nested-fragment}

创作片段引用相当简单(虽然通常字段不会标记为 **片段引用**)。 您可以直接键入引用，也可以（更可能）选择文件夹图标以打开一个浏览器，通过该浏览器可以导航并选择所需的片段。

![内容片段 — 引用](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

内容片段模型控件的定义：

* 是否选择添加多个引用
* 您可以选择的内容片段的模型类型；内容片段模型定义了允许引用的片段模型，因此AEM仅根据这些模型显示片段。

### 如何导航嵌套片段 {#navigate-nested-fragment}

使用 **结构树** 在内容片段编辑器的选项卡中，您可以导航浏览片段引用的片段，然后浏览它们可能包含的任何引用。 选择引用会打开该片段进行编辑。

>[!NOTE]
>
>使用主面板中的痕迹导航，您可以导航回起始点。

![内容片段结构树](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## 临时引用 {#adhoc-references}

临时引用可以作为文本块中的简单链接添加：

![内容片段 — 临时引用](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## 下一步 {#whats-next}

现在，您已经了解内容片段中的引用和结构，接下来的步骤是 [了解元数据和标记的相关信息](metadata-tagging.md). 这将介绍并讨论如何为内容片段定义元数据和标记。

## 其他资源 {#additional-resources}

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [将配置应用到您的Assets文件夹](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [创建内容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [变量 — 创作内容片段](/help/assets/content-fragments/content-fragments-variations.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [内容片段模型 — 数据类型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [内容片段模型 — 属性](/help/assets/content-fragments/content-fragments-models.md#properties)


* 入门指南
   * [创建Assets文件夹无标题快速入门指南](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless Content Architect历程](/help/journey-headless/architect/overview.md)

* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)
