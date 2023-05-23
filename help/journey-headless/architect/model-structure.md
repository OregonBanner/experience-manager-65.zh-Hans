---
title: 了解如何在 AEM 中创建内容片段模型
description: 了解使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。
exl-id: b377e01f-e392-4ef5-a259-73ce9ff941d0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 92%

---

# 了解如何在 AEM 中创建内容片段模型 {#architect-headless-content-fragment-models}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[使用 AEM 对 Headless 进行内容建模的基础知识](basics.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

本文基于这些内容编写，以便您了解如何为 AEM Headless 项目创建您自己的内容片段模型。

## 目标 {#objective}

* **受众**：初学者
* **目标**：使用内容片段模型对 Headless CMS 进行内容建模的概念和机制。

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

之后，可以创建内容片段模型并定义结构。這可以在「工具 — >資產 — >內容片段模型」下完成。

![工具中的内容片段模型](assets/cfm-tools.png)

选择此选项后，您导航到模型的位置并选择&#x200B;**创建**。您可以在此处输入各种关键详细信息。

默认情况下，**启用模型**&#x200B;选项已激活。这意味着，您的模型一经保存即可立即使用（用于创建内容片段）。如果需要，您可以禁用此选项 - 可以稍后启用（或禁用）现有模型。

![创建内容片段模型](/help/assets/content-fragments/assets/cfm-models-02.png)

使用&#x200B;**创建**&#x200B;进行确认，然后可以&#x200B;**打开**&#x200B;您的模型以开始定义结构。

## 定义内容片段模型 {#defining-content-fragment-models}

当您首次打开一个新模型时，您将看到左侧有一个大的空白区域，右侧有一个较长的&#x200B;**数据类型**&#x200B;列表：

![空白模型](/help/assets/content-fragments/assets/cfm-models-03.png)

那么 - 该如何操作？

您可以将&#x200B;**数据类型**&#x200B;的实例拖到左侧空白区域，您已定义模型！

![定义字段](/help/assets/content-fragments/assets/cfm-models-04.png)

在添加数据类型后，您需要为该字段定义&#x200B;**属性**。这些都取决于将使用的类型。例如：

![数据属性](/help/assets/content-fragments/assets/cfm-models-05.png)

可以添加所需数量的字段。例如：

![内容片段模型](/help/assets/content-fragments/assets/cfm-models-07.png)

### 您的内容作者 {#your-content-authors}

您的内容作者看不到您用于创建模型的实际数据类型和属性。这意味着您可能需要提供有关他们如何填写特定字段的帮助和信息。对于基本信息，您可以使用字段标签和默认值，但在更复杂的情况下，可能需要考虑项目特定的文档。

>[!NOTE]
>
>请参阅“其他资源 – 内容片段模型”。

## 管理内容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理内容片段模型涉及：

* 启用（或禁用）内容片段模型 – 这使作者在创建内容片段时能够使用它们。
* 删除 - 始终需要执行删除操作，但您需要注意删除已用于内容片段的模型，特别是已发布的片段。

## 发布 {#publishing}

<!-- needs more details -->

在发布任何相关内容片段时/之前，需要发布内容片段模型。

>[!NOTE]
>
>如果作者尝试发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

模型一经发布，就会&#x200B;*锁定*&#x200B;为作者的只读架构。这旨在阻止进行可能导致现有 GraphQL 架构和查询出错的更改，尤其是在发布环境中。它在控制台中由&#x200B;**已锁定**&#x200B;指示。

当模型处于&#x200B;**已锁定**&#x200B;状态（在只读架构中）时，您可以查看模型的内容和结构，但无法直接编辑它们；但您可以从控制台或模型编辑器中管理&#x200B;**已锁定**&#x200B;模型。

## 后续内容 {#whats-next}

现在您已了解基础知识，下一步是开始创建您自己的内容片段模型。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-authoring/author.md)

* [基本處理](/help/sites-authoring/basic-handling.md)  — 此頁面主要根據 **網站** 主控台，但許多/大多數功能也與導覽至和執行動作相關， **內容片段模型** 在 **資產** 主控台。

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [定义内容片段模型](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [启用或禁用内容片段模型](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [允许在 Assets 文件夹中使用内容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [删除内容片段模型](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [发布内容片段模型](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [取消发布内容片段模型](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [锁定（已发布）内容片段模型](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* 快速入门指南

   * [建立內容片段模型Headless快速入門手冊](/help/sites-developing/headless/getting-started/create-content-model.md)
