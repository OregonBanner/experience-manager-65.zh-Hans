---
title: 'AEM Forms中的占位符文本 '
seo-title: 'AEM Forms中的占位符文本 '
description: 占位符文本旨在帮助用户在控件没有值时输入数据。 它可以是示例值或预期格式的简短描述。
seo-description: 占位符文本旨在帮助用户在控件没有值时输入数据。 它可以是示例值或预期格式的简短描述。
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# AEM Forms {#placeholder-text-in-aem-forms}中的占位符文本

占位符文本表示单词或短短语。 它旨在帮助用户在控件没有值时输入数据。 占位符文本可以是示例值或预期格式的简短说明。 占位符文本在用户输入值之前显示，在用户输入或选择值时将删除该文本。

>[!NOTE]
>
>如果指定，占位符文本必须具有不包含新行字符的值。

![包含和不包含占位符文本的日期组件](assets/dat-picker-place-holder-text.png)

**A.带有** 占位符文本的日 **期组** 件B.不带占位符文本的日期组件

AEM Forms支持“密码”框、“日期”选取器、“数字”框和文本框字段的占位符文本。\
本机HTML5日期构件不支持占位符文本。 要指定占位符文本，请执行以下操作：

1. 右键单击支持占位符文本的组件，然后单击&#x200B;**编辑**。 此时将显示“编辑组件”对话框。

1. 打开&#x200B;**标题和文本**&#x200B;选项卡。
1. 在&#x200B;**占位符文本框**&#x200B;中指定单词或短短语。 单击&#x200B;**确定**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支持占位符文本。

