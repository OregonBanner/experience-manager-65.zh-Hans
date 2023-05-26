---
title: 为表单字段创作上下文帮助
seo-title: Authoring in-context help for form fields
description: AEM Forms允许您将上下文帮助作为文本或富媒体（包括视频）添加到自适应表单字段和面板。
seo-description: AEM Forms allows you to add in-context help to adaptive form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: Adaptive Forms
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 为表单字段创作上下文帮助{#authoring-in-context-help-for-form-fields}

## 简介 {#introduction}

在某些情况下，最终用户填写表单时不确定如何在特定表单字段中填写详细信息。 为了解决此类问题，自适应表单支持向表单字段添加文本或富文本上下文帮助。 它有助于改善表单填写体验并避免最终用户出现任何歧义。

本文讨论表单作者如何在创作自适应Forms时添加上下文帮助。

## 添加上下文帮助 {#add-in-context-help}

您可以使用侧边栏中“属性”选项卡的“帮助内容”部分中的以下选项指定上下文帮助。

* [简短描述](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [详细描述](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![表单字段的上下文帮助](assets/descriptions.png)

>[!NOTE]
>
>长描述将覆盖短描述。 如果已同时指定两者，则只显示详细描述。

### 简短描述 {#short-description}

简短描述字段提供有关填写表单字段的快速和简短提示。 将鼠标悬停在简短描述字段中时，该字段中指定的文本会显示为工具提示。

![用于为表单字段添加上下文内帮助的简短描述](assets/tooltip.png)

>[!NOTE]
>
>选择 **始终显示简短描述** 以永久显示字段下方的帮助文本。

![字段下的永久简短上下文帮助](assets/short1.png)

### 详细描述 {#long-description}

您可以使用详细描述字段指定长文本或嵌入富媒体内容（包括视频）作为上下文帮助。 例如，下图显示了如何嵌入视频作为上下文帮助。

![添加富媒体作为表单字段的上下文内帮助](assets/long-descriptions.png)

添加详细描述将显示 **？** 字段旁边的图标。 单击该图标将显示在详细描述部分中添加的内容。

![富媒体上下文内帮助示例](assets/photoshop.png)

### 面板级帮助 {#panel-level-help}

除了表单字段的上下文帮助之外，还可以在面板编辑对话框的“帮助内容”选项卡中指定面板级别的帮助。

![为表单面板添加上下文帮助](assets/panel-level-help.png)

添加面板帮助显示 **？** 图标。 单击图标将显示在面板编辑对话框的“帮助内容”部分中添加的内容。

![表单面板级别的上下文帮助示例](assets/photoshop-1.png)
