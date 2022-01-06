---
title: 了解如何在AEM中创建内容片段模型
description: 了解使用内容片段模型为无头CMS建模内容的概念和机制。
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 2%

---

# 了解如何在AEM中创建内容片段模型 {#architect-headless-content-fragment-models}

## 迄今为止的故事 {#story-so-far}

于 [AEM Headless内容创作历程](overview.md) the [使用AEM实现无头的内容建模基础知识](basics.md) 介绍了与无头创作相关的基本概念和术语。

本文以这些内容为基础，以便您了解如何为您的AEM无头项目创建您自己的内容片段模型。

## 目标 {#objective}

* **受众**:初学者
* **目标**:使用内容片段模型为无头CMS建模内容的概念和机制。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## 创建内容片段模型 {#creating-content-fragment-models}

然后，可以创建内容片段模型并定义结构。 这可以在工具 — >资产 — >内容片段模型下完成。

![工具中的内容片段模型](assets/cfm-tools.png)

选择此选项后，导航到模型的位置并选择 **创建**. 您可以在此输入各种关键详细信息。

选项 **启用模型** 默认情况下，处于激活状态。 这意味着，当您保存模型后，即可使用（在创建内容片段时）。 如果需要，您可以停用此模型 — 有机会稍后启用（或禁用）现有模型。

![创建内容片段模型](/help/assets/content-fragments/assets/cfm-models-02.png)

使用确认 **创建** 你可以 **打开** 模型以开始定义结构。

## 定义内容片段模型 {#defining-content-fragment-models}

首次打开新模型时，您将看到 — 左侧有一个较大的空白，以及 **数据类型** 在右侧：

![空模型](/help/assets/content-fragments/assets/cfm-models-03.png)

那么，该怎么办？

您可以拖动 **数据类型** 在左边空格上 — 您已经在定义模型了！

![定义字段](/help/assets/content-fragments/assets/cfm-models-04.png)

添加数据类型后，您将需要定义 **属性** 对于该字段。 具体取决于所使用的类型。 例如：

![数据属性](/help/assets/content-fragments/assets/cfm-models-05.png)

您可以添加所需数量的字段。 例如：

![内容片段模型](/help/assets/content-fragments/assets/cfm-models-07.png)

### 您的内容作者 {#your-content-authors}

内容作者看不到用于创建模型的实际数据类型和属性。 这意味着您可能必须提供有关它们如何完成特定字段的帮助和信息。 有关基本信息，您可以使用字段标签和默认值，但更复杂的情况可能需要考虑项目特定文档。

>[!NOTE]
>
>请参阅其他资源 — 内容片段模型。

## 管理内容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理内容片段模型涉及：

* 启用（或禁用）这些片段 — 这样可在创建内容片段时供作者使用。
* 删除 — 始终需要删除，但您需要了解删除已用于内容片段（特别是已发布的片段）的模型。

## 发布 {#publishing}

<!-- needs more details -->

在发布任何相关内容片段时/之前，需要发布内容片段模型。

>[!NOTE]
>
>如果作者尝试发布模型尚未发布的内容片段，则会显示一个选择列表以指示该情况，并且模型将随该片段一起发布。

模型一经发布，就会 *锁定* 在创作时进入只读模式。 这旨在防止更改会导致现有GraphQL架构和查询出错，尤其是在发布环境中。 它在控制台中由 **已锁定**.

当模型为 **已锁定** （在只读模式下），您可以查看模型的内容和结构，但不能直接对其进行编辑；但您可以 **已锁定** 从控制台或模型编辑器中选择模型。

## 下一步 {#whats-next}

现在，您已经学习了基础知识，接下来的步骤是开始创建您自己的内容片段模型。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-authoring/author.md)

* [基本操作](/help/sites-authoring/basic-handling.md)  — 此页面主要基于 **站点** 控制台，但许多/大多数功能也与导航到并对其执行操作相关， **内容片段模型** 下 **资产** 控制台。

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [定义内容片段模型](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [启用或禁用内容片段模型](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [允许在Assets文件夹中使用内容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [删除内容片段模型](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [发布内容片段模型](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [取消发布内容片段模型](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [锁定（已发布）内容片段模型](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* 入门指南

   * [创建内容片段模型无头快速入门指南](/help/sites-developing/headless/getting-started/create-content-model.md)
