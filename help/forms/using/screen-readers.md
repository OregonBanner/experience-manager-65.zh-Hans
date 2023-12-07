---
title: HTML5表单的屏幕阅读器
description: 列出HTML5表单支持的屏幕阅读器。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# HTML5表单的屏幕阅读器 {#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 支持HTML5的所有标准浏览器都可以呈现这些表单。 为了支持跨PDF和HTML5表单进行类似的数据捕获体验，PDF forms的布局保留在HTML5表单中。

HTML5表单使用标准HTML结构，允许将用于HTML的常规无障碍工具与这些表单一起使用。 如果表单是根据可访问表单的最佳实践而设计的，则它可与任何受支持的屏幕阅读器配合使用。 此外，此类表单还支持键盘导航。

## 辅助功能标准 {#accessibility-standards}

HTML5表单符合关于可访问性的Section 508，但存在已知例外。 请参阅 [适用于HTML5表单的VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) 以了解详细信息。

## 经认证的HTML5表单屏幕阅读器 {#certified-screen-readers-for-html-forms}

* Microsoft® Windows上的JAWS 14.0
* macOS X和iPad上的Voicover

### 颌骨 {#jaws}

所有默认击键和快捷键均适用于HTML5表单。 有关使用JAWS的更多信息，请访问 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### 配音 {#voiceover}

HTML5表单支持所有默认的“语音切换”按键和手势。 有关设置和使用语音的详情，请参阅 [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## 已知问题 {#known-issues}

* **（仅限Internal Explorer 9）** 在HTML5表单中，将按需加载页面（动态）。 按需页面加载导致屏幕阅读器的功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段并且用户按下Tab键时，屏幕阅读器将焦点返回到表单上第一页的第一字段。
* **（仅限Internal Explorer 9）** 无法完全通过键盘访问HTML5表单中的日期选取器控件。 在日期选择器控件中，如果多次按向上/向下键，则日期选择器控件将关闭，并且焦点将移至下一个/最后一个字段。

* VoiceOver无法在iPad safari上的日期小部件上检测箭头键。
