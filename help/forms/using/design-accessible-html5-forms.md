---
title: 设计无障碍的HTML5表单
seo-title: 设计无障碍的HTML5表单
description: HTML5表单使用ARIA HTML5辅助功能标准。 这些表单支持选项卡式导航，并经认证与通用屏幕阅读器兼容。
seo-description: HTML5表单使用ARIA HTML5辅助功能标准。 这些表单支持选项卡式导航，并经认证与通用屏幕阅读器兼容。
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: 移动设备表单
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 设计可访问的HTML5表单{#designing-accessible-html-forms}

HTML5表单使用ARIA HTML5辅助功能标准生成无障碍的HTML表单。 这些表单支持选项卡式导航（Mozilla FireFox除外），并经认证与常见屏幕阅读器兼容。 要生成具有良好辅助功能的HTML5表单，请根据一些基本设计准则设计XFA表单模板。 设计准则包括配置正确的选项卡顺序并为每个表单控件提供讲话文本内容。 AEM Forms Designer支持设置这些表单控件属性以生成无障碍的PDF和HTML5表单。

*注：选项卡式导航不涵盖受保护的字段，如显示值总和的计算字段。为了让屏幕阅读器读取受保护字段的值，请在受保护字段的顶部或旁边放置一个空的只读字段。 将受保护字段的值分配给新的只读字段。 屏幕阅读器或选项卡式导航可选取此只读字段，并将其作为受保护字段的值来标注。*

AEM Forms Designer包含许多可传递给屏幕阅读器的“讲话文本”选项。 对于表单中的每个对象，用户可以为屏幕阅读器文本指定以下几个设置之一：

* 自定义屏幕阅读器文本，可使用辅助功能面板进行设置。 作者可以对按钮和字段的名称及其用途添加批注。
* 工具提示，可在辅助功能面板中设置。
* 表单中字段的字幕。
* 对象的名称，在“绑定”(Binding)选项卡的“名称”(Name)选项中指定。

![辅助功能](assets/accessibility.png)

当表单控件上有多个选项(如工具提示、屏幕Reader文本和标题)可用时，屏幕Reader仅使用这些属性之一。 默认顺序为“自定义屏幕Reader文本”、“工具提示”、“标题”和“名称”。 您可以使用辅助功能面板中的屏幕Reader **优先级**&#x200B;选项覆盖默认顺序。
