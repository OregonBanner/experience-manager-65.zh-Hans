---
title: 配置表单输出
seo-title: Configuring form output
description: 了解如何配置表单输出。
seo-description: Learn how to configure form output.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# 配置表单输出{#configuring-form-output}

## 指定返回到Web浏览器的HTML输出的类型 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在管理控制台中，单击服务>表单。
1. 在“表单输出”下的“输出类型”列表中，选择以下选项之一：

   **完整HTML：** 在完整的HTML标签(完整的HTML页面)内呈现表单。 此值为默认值。

   **表单正文：** 在中呈现表单 `<BODY>` 标签(不是完整的HTML页面)。

1. 单击“保存”。

## 指定PDF内容的呈现位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在“表单输出”下的“渲染位置”列表中，选择以下选项之一：

   **客户端：** 在Adobe Acrobat或Adobe Reader中渲染PDF forms。 客户端渲染可提高AEM表单的性能，并且仅适用于PDFForm转换。

   **服务器：** 在应用程序服务器上渲染PDF forms。

   **自动：** 在指定的位置渲染PDF表单 `dynamicRender` xdp文件的配置值。 此值为默认值。

1. 单击“保存”。

## 配置在表单提交前调用自定义脚本 {#configuring-invocation-of-custom-scripts-before-form-submit}

执行以下步骤以启用该功能：

1. 登录到管理控制台。
1. 转到 **服务** > **表单**.
1. 将输出类型指定为表单主体。
1. 保存设置。
1. 在HTML代码的head部分中声明JavaScript变量__CUSTOM_SCRIPTS_VERSION，并将其值设置为1。

   >[!NOTE]
   >
   >*要禁用该功能，可以删除JavaScript变量或将其值设置为0。*
