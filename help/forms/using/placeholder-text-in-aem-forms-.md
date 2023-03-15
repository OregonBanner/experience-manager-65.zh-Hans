---
title: AEM Forms中的占位符文本
seo-title: Placeholder text in AEM Forms
description: 占位符文本旨在帮助用户在控件没有值时输入数据。 它可以是示例值，也可以是预期格式的简短说明。
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
feature: Adaptive Forms
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# AEM Forms中的占位符文本 {#placeholder-text-in-aem-forms}

占位符文本表示单词或短语。 它旨在帮助用户在控件没有值时输入数据。 占位符文本可以是示例值，也可以是预期格式的简短描述。 占位符文本在用户输入值之前显示，当用户输入或选择值时会被删除。

>[!NOTE]
>
>占位符文本（如果已指定）必须具有不包含新行字符的值。

![带有和不带有占位符文本的日期组件](assets/dat-picker-place-holder-text.png)

**答：** 带有占位符文本的日期组件 **B.** 没有占位符文本的日期组件

AEM Forms支持“密码”框、“日期选取器”、“数字”框和文本框字段的占位符文本。\
本机HTML5日期小部件不支持占位符文本。 要指定占位符文本，请执行以下操作：

1. 右键单击支持占位符文本的组件，然后单击 **编辑**. 将出现“编辑组件”对话框。

1. 打开 **标题和文本** 选项卡。
1. 在中指定单词或短语 **占位符文本框**. 单击&#x200B;**确定**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支持占位符文本。
