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
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# HTML5表单的屏幕阅读器 {#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 支持HTML5的所有标准浏览器都可以渲染这些表单。 为支持PDF和HTML5表单中的类似PDF forms捕获体验，HTML5表单中保留了数据的布局。

HTML5表单使用标准HTML结构，允许将常规的辅助工具用于这些表单，以便HTML。 如果根据辅助表单的最佳实践设计表单，则该表单可与任何受支持的屏幕阅读器配合使用。 此外，还为键盘导航启用了此类表单。

## 无障碍标准 {#accessibility-standards}

HTML5表单符合第508条有关辅助功能的规定，但存在已知的例外情况。 请参阅 [HTML5表单的VPAT](https://www.adobe.com/content/dam/cc1/en/accessibility/compliance/pdfs/adobe-livecycle-es4-section-508-vpat-portfolio.pdf) 以了解详细信息。

## HTML5表单的经认证的屏幕阅读器 {#certified-screen-readers-for-html-forms}

* Microsoft® Windows上的JAWS 14.0
* macOS X和iPad上的VoiceOver

### 大白鲨 {#jaws}

所有默认键击和快捷键都适用于HTML5表单。 有关使用JAWS的更多信息，请访问 [https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp).

### VoiceOver {#voiceover}

HTML5表单支持Voice over的所有默认键击和手势。 有关设置和使用VoiceOver的详细信息，请参阅 [https://www.apple.com/accessibility/vision/](https://www.apple.com/accessibility/vision/).

## 已知问题 {#known-issues}

* **（仅限内部资源管理器9）** 在HTML5表单中，页面会按需（动态）加载。 按需页面加载会导致屏幕阅读器功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段上且用户按下选项卡时，屏幕阅读器会将焦点返回到表单上第一个页面的第一个字段。
* **（仅限内部资源管理器9）** HTML5表单中的日期选取器控件无法通过键盘完全访问。 在“日期选取器”控件中，如果多次按上/下键，则“日期选取器”控件将关闭，焦点将移至下一个/最后一个字段。

* VoiceOver在iPad Safari上无法检测日期小组件上的箭头键。
