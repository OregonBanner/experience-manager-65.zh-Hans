---
title: 了解创作基础知识
description: 了解使用内容片段为无头CMS创作内容的概念和机制。
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 3%

---

# 使用AEM创作无头的基础知识 {#author-headless-basics}

## 迄今为止的故事 {#story-so-far}

于 [AEM Headless内容创作历程](overview.md) the [简介](introduction.md) 介绍了与无头创作相关的基本概念和术语。

本文以这些内容为基础，以便您了解如何为AEM无头项目创作您自己的内容。

## 目标 {#objective}

* **受众**:初学者
* **目标**:介绍无头CMS创作的基础知识：
   * AEMaCS创作简介
   * 内容片段简介

## 基本操作 {#basic-handling}

在您了解内容片段之前，请先简要介绍如何使用AEM....但是，没有什么东西能真正取代登录和尝试使用系统的体验。

### 创作和发布 {#author-preview-publish}

AEM 安装通常至少包含两个环境：

* 作者
* 发布

您可以登录，然后使用创作环境生成内容。 准备就绪后，您可以发布内容，以便内容可正常使用。 如果没有头，这将适用于其他应用程序，对于网页，这将适用于网上的读者。

有关更多详细信息，请参阅创作概念。

### 登录 {#signing-in}

与大多数系统一样，您需要登录。 作为作者，您将获得：

* 用户（帐户）名称
* 密码
* 用于访问登录屏幕的链接

您的帐户将配置了您需要的任何权限。 如果您有任何问题，我们建议您联系您的内部项目支持团队。

### 导航 {#navigation}

首次登录小型在线教程时，将重点介绍用户界面的一些主要功能。

然后，您可以使用导航面板访问AEM的关键区域。 对于内容片段，您将使用 **资产控制台**.

可通过选择左上角的Adobe图标，然后选择小罗盘图标来打开导航面板：

![“导航”面板](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>尽管内容片段是AEM的一项功能 **站点**，则可在 **资产** 控制台。 这是一个技术详细信息，不应影响您，但可能有助于您了解。

在控制台中，您可以选择要导航到内容片段的文件夹，或选择痕迹导航（在标题中）以导航回树。

![痕迹导航](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### 操作，选择，查看 {#actions-selecting-viewing}

的 **资产** 控制台具有专用 **操作工具栏**&#x200B;和 **快速操作** 在选择资源（例如，文件夹或内容片段）后可以使用的附加内容。

快速操作适用于单个资源，请参阅 **巴塞尔** 在以下示例中：

![快速操作](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

“操作”工具栏提供了对所有操作（适用于当前方案）的访问权限。 可用的操作可能会发生变化；例如，取决于您的位置，或您是否选择了多个资源：

![操作工具栏](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

您可以使用视图选择器选择查看资源的格式：

![视图选择器](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

您可以使用边栏选择器查看有关项目的其他信息。 这还允许访问其他操作。

![左边栏](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## 创作内容片段 {#authoring-content-fragments}

因此，这是对AEM用户界面(UI)的非常快速的介绍，但希望您有机会试用它。 现在，我们开始关注您真正感兴趣的内容片段 — Headless的内容片段。

我们必须从头到尾逐步完成相关操作，但您的实例可能已经创建了文件夹和/或片段，这些文件夹和/或片段可能位于不同位置。 原则是一样的。

### 组织和导航 {#organizing-and-navigating}

除非您有很少的内容片段，否则您将需要组织这些片段 — 以便您（和其他人）能够再次找到它们。

#### 创建文件夹 {#creating-folder}

为此，可在 **文件** 的子菜单。 选择 **创建** 选项（右上方），后跟 **文件夹**:

![“创建文件夹”选项](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

此时将打开一个对话框，您可以在其中输入详细信息，然后使用进行确认 **创建**:

![“创建文件夹”对话框](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路径和标记限制文件夹中可用的内容片段模型 {#tags-paths-for-models-in-folder}

此部分的级别稍高一些。 如果你只是开始尝试一些东西，你并不需要它，但是 *非常* 当您有大量片段时很有用。 因此，即使你还没用到，了解情况也是件好事。

您的内容架构师将创建当前项目所需的所有内容片段模型，也可能创建其他一些项目所需的所有内容片段模型。 为了帮助您自己和其他作者保持简单，您可以限制适用于特定文件夹的模型列表。

创建文件夹后，可以打开该文件夹 **属性**. 此处提供了各种选项卡，其中包含有关文件夹的信息和配置详细信息。 特别是对于内容片段，您可以使用 **策略** 选项卡来定义此文件夹的特定路径和/或标记。 这限制了可在文件夹中使用的内容片段模型，因为这意味着内容片段模型必须满足这些要求，才能在此文件夹中用于生成片段。

![创建文件夹属性 — 策略](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以在内容片段模型 — 允许资产文件夹上的内容片段模型下阅读更多详细信息。

然后，在这些文件夹中导航以创建和编辑内容片段。

#### 以防万一 — 文件夹Cloud Services配置 {#cloud-services-folder}

以防……

您可能会得到一个初始文件夹，您可以在其中创建文件夹。 这是因为某些配置详细信息必须（通常由开发人员或系统管理员）应用到根文件夹。 您可能不会感兴趣，但如有必要，您可以检查 **配置** 在 **Cloud Services** 文件夹的 **属性**:

![创建文件夹属性 — 配置](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以在将配置应用到您的资产文件夹下阅读更多内容。

### 创建内容片段 {#creating-fragment}

创建内容片段非常相似 — 您只需使用 **内容片段** 选项：

![“创建内容片段”选项](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

此时将打开向导。 第一步是选择片段将基于的内容片段模型：

![创建内容片段 — 选择模型](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

继续 **下一个** 您可以提供详细信息(**基本** 和 **高级**):

![创建内容片段 — 提供名称](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

使用确认 **创建** 你可以 **打开** 您的片段。

### 编辑片段 {#editing-fragment}

您可以在创建片段后立即打开该片段，或者从资产控制台中选择该片段以将其打开。

编辑器首次打开时，您将看到：

* 左侧的图标列表 — 允许您访问各个功能区域。 编辑器将在 **变体** 选项卡，这是大多数编辑操作的位置。 您可能对 **批注** 和 **元数据** 选项卡。

* 包含片段信息以及各种操作访问权限的标头。

* 主编辑区域 — 这取决于用于创建片段的模型。

例如：

* 仅需要多个信息片段的片段，其中一些信息具有特定类型。 对于无头内容，引用是关键，您将在历程的稍后部分了解这些内容。

   ![内容片段编辑器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 允许您写入长段文本的片段。 此处提供了用于管理和设置文本格式的其他选项。 您甚至可以在全屏编辑器中打开各个文本字段（使用右侧的小屏幕样图标）

   ![内容片段编辑器 — 阿拉斯加精灵](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>要帮助作者详细了解如何成功填写某些字段，可能需要特定于项目的文档。
>
>有关一般详细信息，请参阅内容片段模型 — 数据类型和属性。

通过以下任一方式确认您的更新 **保存** 或 **保存并关闭**.

>[!NOTE]
>
>有关更多详细信息，您可以阅读变体 — 创作内容片段。

#### 你（可能）不需要担心的 {#what-you-probably-do-not-need-to-worry-about}

好，这看起来有点奇怪，但是一旦您打开内容片段编辑器并开始探索，您将看到各种选项（可能），这些选项并不适用于您作为内容作者的无头历程。 因此，这只是关于在无头环境中应该忽略的内容的快速提示：

* **内容片段模型**

   您将在编辑器的顶部看到内容片段模型的名称 — 直接在片段名称下方。 这也是指向模型编辑器的链接。
内容片段模型在定义您使用的结构时，对于内容片段而言实际上至关重要。 但是，创建和编辑角色（通常）由其他角色（内容架构师）负责。

   >[!NOTE]
   >
   >如果您想了解更多信息，可以阅读AEM Headless Content Architect历程。

* **关联的内容**

   这个很明显，因为它是编辑中的一个选项卡。

   AEM中提供了许多版本的内容片段。 最初，在创作页面时，可以使用“传统”方式来创作页面…….而它们仍然在这种环境下使用。 这可能涉及到关联资产（例如图像），这些资产（虽然未嵌入到片段中）在创作页面时需要供作者使用。

* **预览**

   这是编辑器中的另一个选项卡，提供了技术视图，主要面向开发人员。

* **更新页面引用**

   此操作可从 **...** （省略号）下拉菜单。 对于无头作者而言，此内容并不有趣，因为它与页面创作相关。

### 发布 {#publishing}

<!-- needs more details -->

完成片段后，您可以 **发布** 这样，它就可用于无头应用。

发布操作在编辑器中(或从 **资产** 控制台):

![内容片段编辑器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 下一步 {#whats-next}

既然您已经学习了基础知识，下一步就是 [了解参考资料](references.md). 这将介绍和讨论各种可用的引用，以及如何使用片段引用创建结构级别 — 无头创作的关键部分。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-authoring/author.md)

* [基本操作](/help/sites-authoring/basic-handling.md)  — 此页面主要基于 **站点** 控制台，但许多/大多数功能也与创作相关 **内容片段** 下 **资产** 控制台。

   * [“导航”面板](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [标题](/help/sites-authoring/basic-handling.md#the-header)

   * [操作工具栏](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)

   * [查看和选择资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [边栏选择器](/help/sites-authoring/basic-handling.md#rail-selector)

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [将配置应用到您的Assets文件夹](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [创建内容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [变量 — 创作内容片段](/help/assets/content-fragments/content-fragments-variations.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [内容片段模型 — 数据类型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [内容片段模型 — 属性](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [内容片段模型 — 允许在Assets文件夹中使用内容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* 入门指南
   * [创建Assets文件夹无标题快速入门指南](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless Content Architect历程](/help/journey-headless/architect/overview.md)

* [AEM无头翻译历程](/help/journey-headless/translation/overview.md)
