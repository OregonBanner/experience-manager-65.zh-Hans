---
title: 如何对内容进行建模
description: 在AEM无头开发人员历程的这一部分中，了解如何使用内容片段模型和内容片段的内容建模来为AEM无头交付构建内容模型。
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 2%

---

# 如何对内容进行建模 {#model-your-content}

在 [AEM Headless开发人员历程](overview.md)，您可以了解如何对内容结构进行建模。 然后，使用内容片段模型和内容片段实现Adobe Experience Manager(AEM)的结构，以便跨渠道重复使用。

## 迄今为止的故事 {#story-so-far}

开始时 [了解CMS无头开发](learn-about.md) 涵盖了无标题内容交付以及应使用它的原因。 然后 [AEM Headless快速入门](getting-started.md) 在您自己的项目上下文中描述了AEM Headless。

在AEM无头历程的上一个文档中， [使用AEM Headless获得首个体验的路径](path-to-first-experience.md)之后，您便了解了实施第一个项目所需的步骤。 阅读完该文档后，您应：

* 了解设计内容时的重要规划注意事项
* 了解根据集成级别要求实施无头的步骤。
* 设置必要的工具和AEM配置。
* 了解最佳实践，以使您的无头历程顺畅、保持内容生成的高效性，并确保内容快速交付。

本文基于这些基础知识，以便您了解如何准备自己的AEM无头项目。

## 目标 {#objective}

* **受众**:初学者
* **目标**:了解如何对内容结构进行建模，然后使用AEM内容片段模型和内容片段实现该结构：
   * 介绍与数据/内容建模相关的概念和术语。
   * 了解为何需要内容建模才能交付无头内容。
   * 了解如何使用AEM内容片段模型（以及包含内容片段的创作内容）实现此结构。
   * 了解如何对内容进行建模；原则和基本样本。

>[!NOTE]
>
>数据建模是一个非常大的领域，因为它在开发关系数据库时使用。 有许多书籍和在线信息源可供使用。
>
>我们仅会考虑在建模数据以与AEM Headless一起使用时需要注意的方面。

## 内容建模 {#content-modeling}

*这是个大坏世界*.

也许，也许不是，但这肯定是个大问题 ***复杂*** 世界之外，数据建模用于定义非常（非常）小的子区域的简化表示，使用特定目的所需的特定信息。

>[!NOTE]
>
>在AEM处理内容时，我们将数据建模称为内容建模。

例如：

学校有很多，但它们有各种共同之处：

* 位置
* 校长
* 许多教师
* 许多非教职人员
* 许多学生
* 许多前教师
* 许多前学生
* 许多教室
* 许多（许多）书籍
* 许多（许多）设备
* 许多课外活动
* 等等…….

即使在如此小的例子中，这份名单也可能看起来无穷无尽。 但是，如果您只想让应用程序执行一个简单的任务，则需要将信息限制在基本内容中。

例如，为该地区所有学校宣传特别活动：

* 学校名称
* 学校位置
* 校长
* 事件类型
* 事件日期
* 教师组织活动

### 概念  {#concepts}

您要描述的内容称为 **实体**  — 基本上是我们要存储有关信息的“内容”。

我们要存储的关于这些数据的信息是 **属性** （属性），如教师的姓名和资格。

然后是多种 **关系** 之间。 例如，一所学校通常只有一位校长，而许多教师（而校长通常也是一位教师）。

分析和定义这些信息的过程，以及这些信息之间的关系，称为 **内容建模**.

### 基本信息 {#basics}

通常，您需要首先绘制 **概念架构** 描述实体及其关系的。 通常情况下，这是高级别（概念性）。

稳定后，您可以将模型转换为 **逻辑架构** 用于描述实体、属性和关系的属性。 在此级别，您应仔细检查定义，以消除重复并优化设计。

>[!NOTE]
>
>有时，这两个步骤会合并，通常取决于您方案的复杂性。

例如，您是否需要单独的实体 `Head Teacher` 和 `Teacher`，或者只是 `Teacher` 模型？

### 确保数据完整性 {#data-integrity}

需要数据完整性才能确保内容在整个生命周期中的准确性和一致性。 这包括确保内容作者可以轻松地了解要在何处存储的内容 — 因此，以下内容至关重要：

* 清晰的结构
* 尽可能简洁（不牺牲精度）的结构
* 验证单个字段
* 在适当情况下，将特定字段的内容限制为有意义的内容

### 消除数据冗余 {#data-redundancy}

在内容结构中存储相同信息两次时，会发生数据冗余。 应避免这种情况，因为它在创建内容时可能会导致混淆，在查询时会导致错误；更别提存储空间的滥用了。

### 优化和性能 {#optimization-and-performance}

通过优化结构，您可以提高内容创建和查询的性能。

一切都是一种平衡行为，但创建一个过于复杂或层次过多的结构，可以：

* 对于生成内容的作者而言，这会令人困惑。

* 如果查询必须访问多个嵌套（引用）内容片段才能检索所需内容，则会严重影响性能。

## AEM Headless的内容建模 {#content-modeling-for-aem-headless}

数据建模是一组已建立的技术，通常在开发关系数据库时使用，因此“内容建模”对AEM Headless意味着什么？

### 为什么？ {#why}

要确保您的应用程序能够始终如一地高效地从AEM请求和接收所需内容，必须对此内容进行结构化。

这意味着您的应用程序事先知道响应的形式，因此知道如何处理。 这比接收自由格式内容要容易得多，后者必须进行解析以确定内容包含的内容，因此，还要确定内容的使用方式。

### 如何介绍？ {#how}

AEM使用内容片段来提供向应用程序无头交付内容所需的结构。

内容模型的结构是：

* 通过定义内容片段模型实现，
* 用作内容生成所用内容片段的基础。

>[!NOTE]
>
>内容片段模型还用作AEM GraphQL架构的基础，用于检索内容 — 有关更多信息，请参阅以后的会话。

对内容的请求使用AEM GraphQL API（标准GraphQL API的自定义实施）进行。 AEM GraphQL API允许您对内容片段执行（复杂）查询，每个查询均根据特定的模型类型而定。

然后，您的应用程序可以使用返回的内容。

## 使用内容片段模型创建结构 {#create-structure-content-fragment-models}

内容片段模型提供了多种机制，允许您定义内容的结构。

内容片段模型描述实体。

>[!NOTE]
>您必须在配置浏览器中启用内容片段功能，才能创建新模型。

>[!TIP]
>
>应该命名模型，以便内容作者知道在创建内容片段时要选择的模型。

在模型中：

1. **数据类型** 允许您定义单个属性。
例如，将包含教师姓名的字段定义为 **文本** 和他们服役的年月 **数值**.
1. 数据类型 **内容参考** 和 **片段引用** 允许您创建与AEM中其他内容的关系。
1. 的 **片段引用** 数据类型允许您通过嵌套内容片段（根据模型类型）来实现多级结构。 这对于内容建模至关重要。

例如：
![使用内容片段进行内容建模](assets/headless-modeling-01.png "使用内容片段进行内容建模")

### 数据类型 {#data-types}

AEM提供了以下数据类型来为内容建模：

* 单行文本
* 多行文本
* 数字
* 布尔型
* 日期和时间
* 枚举
* 标记
* 内容引用
* 片段引用
* JSON 对象

### 引用和嵌套内容 {#references-nested-content}

两种数据类型提供对特定片段外部内容的引用：

* **内容参考**
这为任何类型的其他内容提供了简单的引用。
例如，您可以引用指定位置的图像。

* **片段引用**
这提供了对其他内容片段的引用。
此类引用用于创建嵌套内容，其中介绍了为内容建模所需的关系。
数据类型可配置为允许片段作者执行以下操作：
   * 直接编辑引用的片段。
   * 根据相应的模型创建新内容片段

### 创建内容片段模型 {#creating-content-fragment-models}

最初，您需要为网站启用内容片段模型，这是在配置浏览器中完成的；在工具 — >常规 — >配置浏览器下。 您可以选择配置全局条目，也可以创建新配置。 例如：

![定义配置](assets/cfm-configuration.png)

>[!NOTE]
>
>请参阅其他资源 — 配置浏览器中的内容片段

然后，可以创建内容片段模型并定义结构。 这可以在工具 — >资产 — >内容片段模型下完成。 例如：

![内容片段模型](assets/cfm-model.png)

>[!NOTE]
>
>请参阅其他资源 — 内容片段模型。

## 使用模型创作包含内容片段的内容 {#use-content-to-author-content}

内容片段始终基于内容片段模型。 模型提供了结构，片段包含内容。

### 选择相应的模型 {#select-model}

实际创建内容的第一步是创建内容片段。 可以使用Assets ->文件下所需文件夹中的创建 — >内容片段来完成。 向导将指导您完成各个步骤。

内容片段基于特定的内容片段模型，您可以选择该模型作为创建过程的第一步。

### 创建和编辑结构化内容 {#create-edit-structured-content}

创建片段后，您可以在内容片段编辑器中打开该片段。 在此对话框中，您可以：

* 以正常或全屏模式编辑内容。
* 将内容格式设置为全文、纯文本或标记。
* 创建和管理内容的变体。
* 关联内容.
* 编辑元数据。
* 显示树结构。
* 预览JSON表示形式。

### 创建内容片段 {#creating-content-fragments}

选择相应的模型后，将打开内容片段，以在内容片段编辑器中进行编辑：

![内容片段编辑器](assets/cfm-editor.png)

>[!NOTE]
>
>请参阅其他资源 — 使用内容片段。

## 一些示例快速入门 {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

有关示例的基本结构，请参阅示例内容片段结构。

## 下一步 {#whats-next}

既然您已经学习了如何对结构建模并创建基于此的内容，那么下一步就是 [了解如何使用GraphQL查询访问和检索内容片段内容](access-your-content.md). 这将介绍和讨论GraphQL，然后查看一些示例查询，以了解实际操作情况。

## 其他资源 {#additional-resources}

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)  — 内容片段的前置页面
   * [配置浏览器中的内容片段](/help/assets/content-fragments/content-fragments-configuration-browser.md)  — 在配置浏览器中启用内容片段功能
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 创建和编辑内容片段模型
   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 创建和创作内容片段；此页面将引导您查看其他详细章节
* [AEM GraphQL架构](access-your-content.md) - GraphQL如何实现模型
* [示例内容片段结构](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [AEM Headless快速入门](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 一个简短的视频教程系列概述了如何使用AEM无标题功能，包括内容建模和GraphQL
   * [GraphQL建模基础知识](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html)  — 了解如何在Adobe Experience Manager(AEM)中定义和使用内容片段，以与GraphQL一起使用。
