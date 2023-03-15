---
title: HTML5表单的屏幕阅读器
seo-title: Screen readers for HTML5 forms
description: 列出HTML5表单支持的屏幕阅读器。
seo-description: Lists the screen readers supported with HTML5 forms.
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: Mobile Forms
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# HTML5表单的屏幕阅读器 {#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 支持HTML5的所有标准浏览器都可以呈现这些表单。 为了支持跨PDF表单和HTML5表单的类似数据捕获体验，PDF forms布局保留在HTML5表单中。

HTML5表单使用标准HTML结构，允许使用这些表单的常规无障碍HTML工具。 如果表单根据无障碍表单的最佳实践而设计，则它可与任何支持的屏幕阅读器配合使用。 此外，为键盘导航启用此类表单。

## 辅助功能标准 {#accessibility-standards}

HTML5表单符合第508条关于可访问性的规定，但有已知例外。 参见 [适用于HTML5表单的VPAT](https://wwwimages.adobe.com/content/dam/acom/en/accessibility/compliance/pdfs/livecycle-mobile-forms-es4-section-508-vpat.pdf) 了解详细信息。

## 针对HTML5表单的认证屏幕阅读器 {#certified-screen-readers-for-html-forms}

* Microsoft Windows上的JAWS 14.0
* Mac OS X和iPad上的VoiceOver

### 下巴 {#jaws}

所有默认击键和快捷键都适用于HTML5表单。 有关使用JAWS的更多信息，请访问 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### 配音 {#voiceover}

HTML5表单支持所有默认按键和语音切换手势。 有关设置和使用VoiceOver的详细信息，请参阅 [https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/).

## 已知问题 {#known-issues}

* **（仅限Internal Explorer 9）** 在HTML5表单中，页面会按需加载（动态）。 按需页面加载导致屏幕阅读器的功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段并且用户按下Tab键时，屏幕阅读器将焦点返回到表单第一页的第一字段，而不是设置在下一页的第一字段上。
* **（仅限Internal Explorer 9）** HTML5表单中的日期选取器控件无法通过键盘完全访问。 在日期选择器控件中，如果多次按向上/向下键，则日期选择器控件将关闭，并且焦点将移动到下一个/最后一个字段。

* VoiceOver无法在iPad safari上的日期小部件上检测箭头键。
