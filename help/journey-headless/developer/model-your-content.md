---
title: 如何为您的内容建模
description: 在 AEM Headless 开发人员历程的这一部分中，了解如何使用内容建模与内容片段模型和内容片段对 AEM Headless 交付进行内容建模。
exl-id: f75b433f-5a81-4259-a9f5-b58954b87970
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 97%

---

# 如何为您的内容建模 {#model-your-content}

在 [AEM Headless 开发人员历程](overview.md)的这一部分中，您可以了解如何为内容结构建模。之后，使用内容片段模型和内容片段实施 Adobe Experience Manager (AEM) 的结构以便跨渠道重用。

## 迄今为止的故事 {#story-so-far}

[了解 CMS Headless 开发](learn-about.md)的开头涵盖了 Headless 内容交付以及使用它的原因。之后，[AEM Headless 快速入门](getting-started.md)描述了您自己的项目上下文中的 AEM Headless。

在 AEM Headless 历程的上一个文档[首次 AEM Headless 使用体验的路径](path-to-first-experience.md)中，您已了解实施第一个项目所需的步骤。阅读该文档后，您应：

* 了解有关设计内容的重要规划注意事项
* 了解根据您的集成级别要求实施 Headless 的步骤。
* 设置必需的工具和 AEM 配置。
* 了解使您的 Headless 历程顺畅、使内容生成保持高效并确保快速交付内容的最佳实践。

本文基于这些基础知识编写，以便您了解如何准备您自己的 AEM Headless 项目。

## 目标 {#objective}

* **受众**：初学者
* **目标**：了解如何为您的内容结构建模，然后使用 AEM 内容片段模型和内容片段实施该结构：
   * 介绍与数据/内容建模相关的概念和术语。
   * 了解为什么需要进行内容建模才能进行 Headless 内容交付。
   * 了解如何使用 AEM 内容片段模型实施此结构（以及使用内容片段创作内容）。
   * 了解如何为内容建模；带基本示例的准则。

>[!NOTE]
>
>数据建模是一个非常大的领域，因为它将用于开发关系数据库。提供了许多书籍和在线信息来源。
>
>在为用于 AEM Headless 的数据建模时，我们只考虑感兴趣的方面。

## 内容建模 {#content-modeling}

*这是一个大而复杂的领域*。

也许是，也许不是，但它肯定是一个大而&#x200B;***复杂的***&#x200B;领域，数据建模用于定义一个非常（非常）小的子部分的简化呈现，并使用实现特定目的所需的特定信息。

>[!NOTE]
>
>由于 AEM 将处理内容，因此，我们将数据建模称为内容建模。

例如：

虽然学校有很多，但它们都有很多共同点：

* 位置
* 校长
* 许多教师
* 许多非教学员工
* 许多学生
* 许多以前的教师
* 许多以前的学生
* 许多教室
* 很多（很多）书
* 很多（很多）台设备
* 许多课外活动
* 依此类推....

即使在如此小的示例中，列表也似乎是无尽的。但是，如果您只希望您的应用程序执行一项简单的任务，则需要将信息限制为要点。

例如，为该地区的所有学校宣传特别活动：

* 学校名称
* 学校位置
* 校长
* 活动类型
* 活动日期
* 负责组织活动的教师

### 概念 {#concepts}

您想描述的内容称作&#x200B;**实体** – 基本上是我们要存储其相关信息的“事物”。

我们要存储的其相关信息是&#x200B;**特性**（属性），例如教师的姓名和资历。

随后是实体之间的各种&#x200B;**关系**。例如，一所学校通常只有一个校长，但有很多教师（校长通常也是教师）。

分析并定义此信息以及它们之间的关系的过程称作&#x200B;**内容建模**。

### 基本信息 {#basics}

通常，您需要先绘制用于描述实体及其关系的&#x200B;**概念架构**。通常这是高层次的（概念性的）。

在此稳定之后，您可以将模型转换用于描述实体、属性和关系的&#x200B;**逻辑架构**。在此级别，您应仔细检查定义以消除重复项并优化您的设计。

>[!NOTE]
>
>有时，可以将这两个步骤合并，这通常取决于您的场景的复杂性。

例如，需要 `Head Teacher` 和 `Teacher` 的单独实体，还是只需要 `Teacher` 模型的附加属性？

### 确保数据完整性 {#data-integrity}

需要实现数据完整性才能确保您的内容在其整个生命周期内准确且一致。这包括确保内容作者能够轻松了解在何处存储哪些内容 - 因此，以下项目至关重要：

* 清晰的结构
* 尽可能简洁的结构（不降低准确度）
* 单个字段的验证
* 在适当的情况下，将特定字段的内容限制为有意义的内容

### 消除数据冗余 {#data-redundancy}

在内容结构中将同一信息存储两次后，会出现数据冗余。应避免出现这种情况，因为它会导致在创建内容时发生混淆，并导致在查询时出错；更不用说滥用存储空间了。

### 优化和性能 {#optimization-and-performance}

通过优化结构，您可以提高内容创建和查询的性能。

所做的一切都是为了达到平衡，但创建一个过于复杂或具有太多层次的结构可能会：

* 让生成内容的作者感到困惑。

* 如果查询必须访问多个嵌套（引用）的内容片段才能检索所需内容，则会严重影响性能。

## AEM Headless 的内容建模 {#content-modeling-for-aem-headless}

数据建模是一系列成熟的技术，在开发关系数据库时通常会使用这些技术，那么内容建模对 AEM Headless 意味着什么呢？

### 为什么？ {#why}

为了确保您的应用程序能够一致而高效地从 AEM 请求和接收所需内容，必须设置这些内容的结构。

这意味着您的应用程序会预先知道响应的形式，从而了解如何处理它。这比接收自由格式的内容要简单得多，必须对自由格式的内容进行分析以确定它包含什么以及如何使用它。

### 方法简介 {#how}

AEM 使用内容片段提供以 Headless 方式将内容交付到应用程序所需的结构。

内容模型的结构将：

* 由内容片段模型的定义识别，
* 用作用于内容生成的内容片段的基础。

>[!NOTE]
>
>内容片段模型还用作 AEM GraphQL 架构的基础，用于检索您的内容 - 稍后的会话中提供了更多相关信息。

使用 AEM GraphQL API 发出对您的内容的请求，这是标准 GraphQL API 的自定义实施。AEM GraphQL API 让您对内容片段执行（复杂）查询，每个查询都根据特定的模型类型。

然后，您的应用程序可以使用返回的内容。

## 使用内容片段模型创建结构 {#create-structure-content-fragment-models}

内容片段模型提供了各种机制，可让您定义内容的结构。

内容片段模型描述了一个实体。

>[!NOTE]
>您必须在配置浏览器中启用内容片段功能，才能创建新模型。

>[!TIP]
>
>应对模型命名，以便内容作者在创建内容片段时知道选择哪个模型。

在模型中：

1. **数据类型** 允许您定义各个属性。
例如，以**文本**&#x200B;形式定义包含教师姓名的字段，并以&#x200B;**数字**&#x200B;形式定义其服务年数。
1. 数据类型 **内容引用** 和 **片段引用** 允许您创建与AEM中其他内容的关系。
1. **片段引用**&#x200B;数据类型可让您通过嵌套内容片段（根据模型类型）来实施结构的多个层次。这对于您的内容建模是至关重要的。

例如：
![使用内容片段进行内容建模](assets/headless-modeling-01.png "使用内容片段进行内容建模")

### 数据类型 {#data-types}

AEM 提供了以下数据类型以供您用来进行内容建模：

* 单行文本
* 多行文本
* 数字
* 布尔值
* 日期和时间
* 枚举
* 标记
* 内容引用
* 片段引用
* JSON 对象

### 引用和嵌套内容 {#references-nested-content}

两种数据类型都提供了对特定片段之外的内容的引用：

* **内容引用**
这提供了对任意类型的其他内容的简单引用。
例如，您可以在指定位置引用图像。

* **片段引用**
这会提供对其他内容片段的引用。
这种类型的引用用于创建嵌套内容，引入对内容进行建模所需的关系。
数据类型可配置为允许片段作者执行以下操作：
   * 直接编辑引用的片段。
   * 根据相应的模型创建新内容片段

### 创建内容片段模型 {#creating-content-fragment-models}

一开始，您需要为您的站点启用内容片段模型，此操作是在配置浏览器中完成的；在“工具”->“常规”->“配置浏览器”下。您可以选择配置全局条目或创建新的配置。例如：

![定义配置](assets/cfm-configuration.png)

>[!NOTE]
>
>请参阅“其他资源 – 配置浏览器中的内容片段”

之后，可以创建内容片段模型并定义结构。此操作可在“工具” — >“资产” — >“内容片段模型”下完成。 例如：

![内容片段模型](assets/cfm-model.png)

>[!NOTE]
>
>请参阅“其他资源 – 内容片段模型”。

## 使用模型通过内容片段创作内容 {#use-content-to-author-content}

内容片段始终基于内容片段模型。模型提供结构，片段保存内容。

### 选择适当的模型 {#select-model}

在实际创建内容的过程中，第一步是创建内容片段。可使用“资源”->“文件”下的所需文件夹中的“创建”->“内容片段”来执行此操作。该向导将引导您完成这些步骤。

内容片段基于特定的内容片段模型，在创建过程中，您首先会选择该模型。

### 创建和编辑结构化内容 {#create-edit-structured-content}

创建片段后，您可以在内容片段编辑器中打开片段。在此编辑器中，您可以：

* 在正常或全屏架构下编辑您的内容。
* 将您的内容格式化为全文、纯文本或 Markdown。
* 创建和管理内容的变体。
* 关联内容。
* 编辑元数据。
* 显示树结构。
* 预览 JSON 表示形式。

### 创建内容片段 {#creating-content-fragments}

在选择适当的模型后，将在内容片段编辑器中打开一个内容片段以进行编辑：

![内容片段编辑器](assets/cfm-editor.png)

>[!NOTE]
>
>请参阅“其他资源 – 使用内容片段”。

## 开始使用一些示例 {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

有关作为示例的基本结构，请参阅“示例内容片段结构”。

## 后续内容 {#whats-next}

现在您已了解如何为结构建模，并根据它创建内容，下一步是[了解如何使用 GraphQL 查询来访问和检索您的内容片段内容](access-your-content.md)。这将介绍和讨论 GraphQL，然后查看一些示例查询以了解实践中的工作方式。

## 其他资源 {#additional-resources}

* [使用内容片段](/help/assets/content-fragments/content-fragments.md) – 内容片段的导入页面
   * [配置浏览器中的内容片段](/help/assets/content-fragments/content-fragments-configuration-browser.md) – 在配置浏览器中启用内容片段功能
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md) – 创建和编辑内容片段模型
   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md) – 创建和创作内容片段；此页面将您转至其他详细部分
* [AEM GraphQL 架构](access-your-content.md) – GraphQL 如何实施模型
* [示例内容片段结构](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [AEM Headless 快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) – 一个简短的视频教程系列，概述了如何使用 AEM 的 Headless 功能，包括内容建模和 GraphQL
   * [GraphQL 建模基础知识](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html?lang=zh-Hans) – 了解如何在 Adobe Experience Manager (AEM) 中定义和使用内容片段，以便与 GraphQL 一起使用。
