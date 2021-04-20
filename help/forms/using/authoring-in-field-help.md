---
title: 为表单域创作上下文帮助
seo-title: 为表单域创作上下文帮助
description: AEM Forms允许您将上下文帮助作为文本或富媒体（包括视频）添加到自适应表单字段和面板。
seo-description: AEM Forms允许您将上下文帮助作为文本或富媒体（包括视频）添加到自适应表单字段和面板。
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 创作表单字段的上下文帮助{#authoring-in-context-help-for-form-fields}

## 简介 {#introduction}

在某些情况下，最终用户在填写表单时不确定如何填写特定表单字段中的详细信息。 为了解决这些问题，自适应表单支持向表单字段添加文本或富上下文帮助。 它有助于改善表单填写体验，并避免最终用户遇到任何歧义。

本文讨论表单作者在创作自适应Forms时如何添加上下文帮助。

## 添加上下文帮助{#add-in-context-help}

您可以使用侧栏属性选项卡的“帮助内容”部分中的以下选项指定上下文内帮助。

* [简短描述](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [长描述](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![表单域的上下文帮助](assets/descriptions.png)

>[!NOTE]
>
>长描述将覆盖短描述。 如果您同时指定了这两项，则只显示“长”描述。

### 简短描述{#short-description}

“简短说明”字段用于提供有关填写表单字段的快速提示和简短提示。 将鼠标悬停在“简短说明”字段上时，将以工具提示的形式显示在“简短说明”字段中指定的文本。

![有关为表单域添加上下文帮助的简短说明](assets/tooltip.png)

>[!NOTE]
>
>选择&#x200B;**始终显示简短描述**&#x200B;以在字段下永久显示帮助文本。

![现场下的永久简短上下文帮助](assets/short1.png)

### 详细说明{#long-description}

您可以使用“长描述”字段指定长文本或嵌入富媒体内容（包括视频）作为上下文帮助。 例如，下图显示了如何将视频作为上下文帮助嵌入。

![将富媒体添加为表单域的上下文帮助](assets/long-descriptions.png)

添加长说明时显示&#x200B;**?** 图标。单击该图标将显示在长描述部分中添加的内容。

![富媒体上下文帮助示例](assets/photoshop.png)

### 面板级帮助{#panel-level-help}

除了表单域的上下文帮助外，您还可以在面板编辑对话框的“帮助”内容选项卡的面板级别指定帮助。

![为表单面板添加上下文帮助](assets/panel-level-help.png)

添加面板帮助时显示&#x200B;**?** 图标。单击该图标会显示在面板编辑对话框的“帮助内容”部分添加的内容。

![表单面板级的上下文帮助示例](assets/photoshop-1.png)

