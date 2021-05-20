---
title: 设置国际化选项
seo-title: 设置国际化选项
description: 了解如何指定用于呈现表单的区域设置，以及如何指定用于对输出流进行编码的字符集。
seo-description: 了解如何指定用于呈现表单的区域设置，以及如何指定用于对输出流进行编码的字符集。
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---

# 设置国际化选项{#setting-internationalization-options}

## 指定用于呈现表单的区域设置{#specify-the-locale-used-to-render-forms}

您可以指定渲染PDF表单时使用的区域设置。 PDF表单上的字段使用指定的区域设置来显示数据。 例如，如果区域设置为德语，则表单对数字值使用德语小数分隔符。 区域设置还用于将验证消息作为HTML转换的一部分发送到客户端设备（如Web浏览器）。

1. 在管理控制台中，单击服务> Forms。
1. 在“国际化”的“语言”列表下，选择用于呈现表单的区域设置。 默认值为英语（美国）。
1. 单击保存。

## 指定用于编码输出流{#specify-the-character-set-used-to-encode-the-output-stream}的字符集

1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置取决于所使用的API，即renderHTMLForm或renderPDFForm。 要指定所列字符集以外的字符集，请选择“自定义”，然后在显示的框中指定编码值。

   对于HTML转换，AEM表单支持由`java.nio.charset`包定义的字符编码值。 如果sFormPreference是PDFForm，则仅支持特定字符集。 字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击保存。
