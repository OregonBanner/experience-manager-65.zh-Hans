---
title: 为表单字段创作上下文内帮助
seo-title: 为表单字段创作上下文内帮助
description: AEM Forms允许您将上下文内帮助添加到自适应表单字段和面板中（作为文本或富媒体，包括视频）。
seo-description: AEM Forms允许您将上下文内帮助添加到自适应表单字段和面板中（作为文本或富媒体，包括视频）。
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 为表单字段创作上下文内帮助{#authoring-in-context-help-for-form-fields}

## 简介 {#introduction}

在某些情况下，最终用户填写表单时不确定如何在特定表单字段中填写详细信息。 为解决这些问题，自适应表单支持向表单字段添加文本或丰富的上下文帮助。 它有助于改善表单填写体验，并避免最终用户的歧义。

本文讨论了表单作者在创作自适应表单时如何添加上下文帮助。

## 添加上下文帮助 {#add-in-context-help}

您可以使用提要栏中属性选项卡的“帮助内容”部分中的以下选项指定上下文内帮助。

* [简短说明](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [长描述](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![表单字段的上下文帮助](assets/descriptions.png)

>[!NOTE]
>
>长描述将取代短描述。 如果您同时指定了这两者，则只显示长描述。

### Short description {#short-description}

“简短说明”字段用于提供有关填写表单字段的快速提示和简短提示。 将鼠标悬停在“简短说明”字段上时，在“简短说明”字段中指定的文本将显示为工具提示。

![有关为表单字段添加上下文内帮助的简短说明](assets/tooltip.png)

>[!NOTE]
>
>选择 **始终显示简短说明** ，以永久显示字段下方的帮助文本。

![现场下的永久简短上下文帮助](assets/short1.png)

### Long description {#long-description}

您可以使用长描述字段指定长文本或嵌入富媒体内容（包括视频），作为上下文帮助。 例如，下图显示了如何嵌入视频作为上下文帮助。

![将富媒体添加为表单字段的上下文帮助](assets/long-descriptions.png)

添加长描述时是否显示 **?** 图标。 单击该图标会显示在长描述部分中添加的内容。

![富媒体上下文帮助示例](assets/photoshop.png)

### 面板级帮助 {#panel-level-help}

除了表单字段的上下文内帮助之外，您还可以在面板编辑对话框的“帮助内容”选项卡的面板级别指定帮助。

![为表单面板添加上下文内帮助](assets/panel-level-help.png)

添加面板帮助时，会显示 **?** 图标。 单击该图标会显示在面板编辑对话框的“帮助内容”部分中添加的内容。

![表单面板级的上下文内帮助示例](assets/photoshop-1.png)

