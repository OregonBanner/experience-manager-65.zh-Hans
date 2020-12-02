---
title: 配置表单输出
seo-title: 配置表单输出
description: 了解如何配置表单输出。
seo-description: 了解如何配置表单输出。
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# 配置表单输出{#configuring-form-output}

## 指定返回到Web浏览器的HTML输出类型{#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在管理控制台中，单击“服务”>“表单”。
1. 在“表单输出”下的“输出类型”列表中，选择以下选项之一：

   **完整HTML:** 在完整HTML标记（完整的HTML页）中呈现表单。此值为默认值。

   **表单正文：** 要在标记内呈 `<BODY>` 现表单（不是完整的HTML页面）。

1. 单击保存。

## 指定渲染PDF内容的位置{#specify-the-location-where-pdf-content-is-rendered}

1. 在“表单输出”下的“在列表下渲染”中，选择以下选项之一：

   **客户端：** 在Adobe Acrobat或Adobe Reader内渲染PDF forms。客户端渲染改进了AEM表单的性能，并且仅适用于PDFForm转换。

   **服务器：** 在应用程序服务器上呈现PDF forms。

   **自动：** 在XDP文件的配置值指定的位 `dynamicRender` 置渲染PDF表单。此值为默认值。

1. 单击保存。

## 在表单提交前配置对自定义脚本的调用{#configuring-invocation-of-custom-scripts-before-form-submit}

执行以下步骤以启用该功能：

1. 登录到管理控制台。
1. 转到&#x200B;**服务** > **表单**。
1. 将“输出”类型指定为“表单主体”。
1. 保存设置。
1. 在HTML代码的标题部分声明一个JavaScript变量__CUSTOM_SCRIPTS_VERSION并将其值设置为1。

   >[!NOTE]
   >
   >*要禁用该功能，可删除JavaScript变量或将其值设置为0。*

