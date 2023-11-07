---
title: 设计无障碍HTML5表单
seo-title: Designing accessible HTML5 forms
description: HTML5表单使用ARIAHTML5辅助功能标准。 这些表单支持选项卡式导航，经认证与常用屏幕阅读器兼容。
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 设计无障碍HTML5表单 {#designing-accessible-html-forms}

HTML5表单使用ARIAHTML5辅助功能标准生成无障碍的HTML表单。 这些表单支持选项卡式导航（Mozilla FireFox除外），经认证与常用屏幕阅读器兼容。 要生成具有良好辅助功能的HTML5表单，请根据一些基本设计准则来设计XFA表单模板。 设计准则包括配置正确的制表符顺序并为每个表单控件提供“说文本”内容。 AEM Forms Designer支持设置这些表单控件属性，以生成可访问的PDF和HTML5表单。

*注意：选项卡式导航不包含受保护字段，例如显示值总和的计算字段。 要使屏幕阅读器读取受保护字段的值，请在受保护字段的顶部或旁边放置一个空的只读字段。 将受保护字段的值分配给新的只读字段。 屏幕阅读器或选项卡式导航器可以选取此只读字段，并将其作为受保护字段的值发出。*

AEM Forms Designer包含多个“说文字”选项，可传递给屏幕阅读器。 对于表单中的每个对象，用户可以为屏幕阅读器文本指定以下几种设置之一：

* 自定义屏幕阅读器文本，可以使用“辅助功能”面板进行设置。 作者可以注释按钮和字段的名称及其用途。
* 工具提示，可在“辅助功能”面板中设置这些提示。
* 表单中的字段标题。
* 对象名称，在“绑定”选项卡的“名称”选项中指定。

![辅助功能](assets/accessibility.png)

当“表单”控件上有工具提示、“屏幕Reader文本”和“标题”等多个选项可用时，“屏幕”Reader将仅使用这些属性之一。 默认顺序为“自定义屏幕Reader文本”、“工具提示”、“标题”和“名称”。 您可以使用屏幕Reader覆盖默认顺序 **优先级** “辅助功能”面板中的选项。
