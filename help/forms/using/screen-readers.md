---
title: HTML5表单的屏幕阅读器
seo-title: HTML5表单的屏幕阅读器
description: 列出HTML5表单支持的屏幕阅读器。
seo-description: 列出HTML5表单支持的屏幕阅读器。
uuid: 035354e2-957f-4eb6-bc16-4ca96ec7ac74
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 53c57180-7004-4534-9146-603f7770a6fe
feature: 移动设备表单
exl-id: 07d20c2f-7d13-48ac-8d58-b367eb194558
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# HTML5表单的屏幕阅读器{#screen-readers-for-html-forms}

HTML5表单组件将XFA表单模板渲染为HTML5格式。 所有支持HTML5的标准浏览器都可以渲染这些表单。 为支持PDF和HTML5表单中类似的PDF forms捕获体验，HTML5表单中保留了数据的布局。

HTML5表单使用标准HTML结构，允许将HTML的常规辅助工具用于这些表单。 如果根据辅助表单的最佳实践设计表单，则该表单可与任何受支持的屏幕阅读器配合使用。 此外，还为键盘导航启用了此类表单。

## 无障碍标准{#accessibility-standards}

HTML5表单符合第508节的辅助功能，但已知情况除外。 有关详细信息，请参阅HTML5表单的[VPAT](https://www.adobe.com/mena_en/accessibility/compliance/livecycle-mobile-forms-es4-section-508-vpat.html)。

## HTML5表单的经认证的屏幕阅读器{#certified-screen-readers-for-html-forms}

* Microsoft Windows上的JAWS 14.0
* Mac OS X和iPad上的VoiceOver

### 大白鲨 {#jaws}

所有默认键击和快捷键都适用于HTML5表单。 有关使用JAWS的更多信息，请访问[https://www.freedomscientific.com/jaws-hq.asp](https://www.freedomscientific.com/jaws-hq.asp)。

### VoiceOver {#voiceover}

HTML5表单支持Voice over的所有默认键击和手势。 有关设置和使用VoiceOver的更多信息，请参阅[https://www.apple.com/accessibility/voiceover/](https://www.apple.com/accessibility/voiceover/)。

## 已知问题 {#known-issues}

* **（仅限内部资源管理器9）** 在HTML5表单中，页面会按需（动态）加载。按需页面加载会导致屏幕阅读器功能出现问题。 当屏幕阅读器的焦点位于页面的最后一个字段且用户按下选项卡时，屏幕阅读器不会将焦点设置在下一页的第一个字段上，而是会将焦点返回到表单第一页的第一个字段。
* **（仅限内部资源管理器9）** HTML5表单中的日期选取器控件无法通过键盘完全访问。在“日期选取器”控件中，如果多次按上/下键，则“日期选取器”控件将关闭，焦点将移至下一个/最后一个字段。

* 在iPad Safari上，VoiceOver无法检测日期小组件上的箭头键。
