---
title: 设计可访问的HTML5表单
seo-title: 设计可访问的HTML5表单
description: HTML5表单使用ARIA HTML5辅助工具标准。 这些表单支持选项卡式导航，并经过认证可与常见屏幕阅读器兼容。
seo-description: HTML5表单使用ARIA HTML5辅助工具标准。 这些表单支持选项卡式导航，并经过认证可与常见屏幕阅读器兼容。
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 设计可访问的HTML5表单 {#designing-accessible-html-forms}

HTML5表单使用ARIA HTML5辅助工具标准生成可访问的HTML表单。 这些表单支持选项卡式导航（Mozilla FireFox除外），并经认证可与常见屏幕阅读器兼容。 要生成具有良好辅助功能的HTML5表单，请根据一些基本设计准则设计XFA表单模板。 设计准则包括配置正确的跳位顺序并为每个表单控件提供演讲文本内容。 AEM Forms Designer支持设置这些表单控件属性以生成可访问的PDF和HTML5表单。

*注意：选项卡式导航不涵盖受保护的字段，如显示值总和的计算字段。 要使屏幕阅读器读取受保护字段的值，请在受保护字段的顶部或旁边放置一个空的只读字段。 将受保护字段的值指定到新的只读字段。 屏幕阅读器或选项卡式导航可以选取此只读字段，并将其作为受保护字段的值进行说明。*

AEM Forms Designer包括许多可传递给屏幕阅读器的“讲话文本”选项。 对于表单中的每个对象，用户可以为屏幕阅读器文本指定以下几种设置之一：

* 自定义屏幕阅读器文本，可使用“辅助功能”调板设置。 作者可以对按钮和字段的名称及其用途添加注释。
* 工具提示，可在“辅助功能”调板中设置。
* 表单中字段的题注。
* 对象的名称，在“绑定”选项卡的“名称”选项中指定。

![辅助功能](assets/accessibility.png)

当多个选项（如工具提示、屏幕阅读器文本和题注）在表单控件上可用时，屏幕阅读器只使用这些属性中的一个。 默认顺序为“自定义屏幕阅读器文本”、“工具提示”、“题注”和“名称”。 您可以使用“辅助功能”调板中的“屏幕阅读器优 **先级** ”选项覆盖默认顺序。
