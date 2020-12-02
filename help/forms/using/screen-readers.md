---
title: HTML5表单的屏幕阅读器
seo-title: HTML5表单的屏幕阅读器
description: 列表HTML5表单支持的屏幕阅读器。
seo-description: 列表HTML5表单支持的屏幕阅读器。
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# HTML5表单的屏幕阅读器{#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 所有支持HTML5的标准浏览器都可以呈现这些表单。 为支持PDF和HTML5表单中的类似数据捕获体验，HTML5表单中保留PDF forms的布局。

HTML5表单使用标准HTML构造，使HTML能够与这些表单一起使用常规的辅助工具工具。 如果表单是根据可访问表单的最佳实践设计的，则它可与任何支持的屏幕阅读器一起使用。 此外，还启用了此类表单进行键盘导航。

## 辅助功能标准{#accessibility-standards}

HTML5表单符合第508条有关辅助功能的规定，但有已知例外。 有关详细信息，请参阅[VPAT for HTML5 forms](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html)。

## HTML5表单{#certified-screen-readers-for-html-forms}的认证屏幕阅读器

* JAWS 14.0 on Microsoft Windows
* Mac OS X和iPad上的VoiceOver

### JAWS {#jaws}

所有默认按键和快捷键均适用于HTML5表单。 有关使用JAWS的更多信息，请访问[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### VoiceOver {#voiceover}

HTML5表单支持Voice over的所有默认按键和手势。 有关设置和使用VoiceOver的详细信息，请参阅[https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)。

## 已知问题 {#known-issues}

* **(仅限内部资源管理器** 9)在HTML5表单中，页面按需加载（动态）。按需页面加载导致屏幕阅读器功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段并且用户按下选项卡时，屏幕阅读器会将焦点返回到表单第一页的第一个字段，而不是将焦点设置到下一页的第一个字段。
* **(仅限内部资源管理器** 9)HTML5表单中的日期选取器控件无法通过键盘完全访问。在“日期选取器”(Date Picker)控件中，如果多次按上／下键，则“日期选取器”(Date Picker)控件将关闭，焦点将移至下一个／最后一个字段。

* iPad safari上的日期构件上的VoiceOver检测不到箭头键。
