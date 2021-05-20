---
title: 'AEM Forms中的占位符文本 '
seo-title: 'AEM Forms中的占位符文本 '
description: 占位符文本旨在在控件没有值时帮助用户输入数据。 它可以是示例值或预期格式的简要说明。
seo-description: 占位符文本旨在在控件没有值时帮助用户输入数据。 它可以是示例值或预期格式的简要说明。
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: 自适应表单
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# AEM Forms中的占位符文本{#placeholder-text-in-aem-forms}

占位符文本表示一个单词或短短语。 它旨在在控件没有值时帮助用户输入数据。 占位符文本可以是示例值或预期格式的简要说明。 占位符文本在用户输入值之前显示，在用户输入或选择值时，会将其删除。

>[!NOTE]
>
>如果指定占位符文本，则其值必须不包含任何新行字符。

![包含和不包含占位符文本的日期组件](assets/dat-picker-place-holder-text.png)

**A.带有** 占位符文本的日期组 **件B.** 不带占位符文本的日期组件

AEM Forms支持“密码”框、“日期选取器”、“数字”框和“文本框”字段的占位符文本。\
本机HTML5日期小组件不支持占位符文本。 要指定占位符文本，请执行以下操作：

1. 右键单击支持占位符文本的组件，然后单击&#x200B;**编辑**。 此时将出现“编辑组件”对话框。

1. 打开&#x200B;**标题和文本**&#x200B;选项卡。
1. 在&#x200B;**占位符文本框**&#x200B;中指定单词或短短语。 单击&#x200B;**确定**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支持占位符文本。
