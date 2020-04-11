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

---


# HTML5表单的屏幕阅读器 {#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 所有支持HTML5的标准浏览器都可以呈现这些表单。 为支持跨PDF和HTML5表单的类似数据捕获体验，PDF表单的布局将保留在HTML5表单中。

HTML5表单使用标准HTML构造，允许与这些表单一起使用HTML的常规辅助工具。 如果表单是根据可访问表单的最佳实践设计的，则它可与任何支持的屏幕阅读器一起使用。 此外，此类表单还可用于键盘导航。

## 辅助功能标准 {#accessibility-standards}

HTML5表单符合第508条有关辅助功能的规定，但有已知例外。 有关详 [细信息，请参阅HTML5表单的](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html) VPAT。

## HTML5表单的认证屏幕阅读器 {#certified-screen-readers-for-html-forms}

* JAWS 14.0 on Microsoft Windows
* Mac OS X和iPad上的VoiceOver

### JAWS {#jaws}

所有默认按键和快捷键都适用于HTML5表单。 有关使用JAWS的更多信息，请访 [问https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### VoiceOver {#voiceover}

HTML5表单支持Voice over的所有默认按键和手势。 有关设置和使用VoiceOver的详细信息，请参 [阅https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)。

## 已知问题 {#known-issues}

* **（仅限Internal Explorer 9）** 在HTML5表单中，页面按需加载（动态）。 按需页面加载会导致屏幕阅读器功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段上且用户按下选项卡时，屏幕阅读器不会将焦点设置在下一页的第一个字段上，而是将焦点返回到表单第一页的第一个字段。
* **（仅限Internal Explorer 9）** HTML5表单中的“日期选取器”控件无法通过键盘完全访问。 在“日期选取器”控件中，如果多次按上／下键，则“日期选取器”控件将关闭，焦点将移至下一个／最后一个字段。

* VoiceOver在iPad safari上检测不到日期构件上的箭头键。
