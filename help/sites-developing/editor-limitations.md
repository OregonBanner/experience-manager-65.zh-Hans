---
title: 编辑器限制
seo-title: Editor Limitations
description: 觸控式UI中的編輯器會使用覆蓋來與限制在iframe中的內容互動。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 10%

---

# 编辑器限制{#editor-limitations}

觸控式UI中的編輯器會使用覆蓋來與限制在iframe中的內容互動。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。本頁面會概述這些限制，並儘可能提供解決方案或因應措施。

## 功能限制 {#functional-limitations}

使用編輯器編寫頁面時，作者可能會遇到下列功能限制。

### 連結未啟用 {#links-not-active}

時間 [編輯頁面](/help/sites-authoring/editing-content.md)，連結未啟用。

* [切換至 **預覽** 模式](/help/sites-authoring/editing-content.md#preview-mode) 以使用內容中的連結進行導覽。

### 結構頁面 {#structure-pages}

頁面無法命名 `structure`. 已命名的頁面 `structure` 在頁面編輯器中將不可編輯。

## CSS限制 {#css-limitations}

開發人員在編輯器與CSS的互動中可能會遇到下列限制。

### 絕對定位的元素 {#absolutely-positioned-elements}

絕對定位的元素可能會導致其覆蓋的位置出現問題。

* 如果發生此情況，請確定絕對位置元素的維度正確，因為編輯器將會使用完全相同的維度建立覆蓋。

### vh單位 {#vh-units}

`vh` 不支援單位，因為iframe高度必須由AEM自動調整。

### 固定背景影像 {#fixed-background-images}

由於固定背景影像內嵌於iframe中，捲動時可能無法顯示為固定背景影像。

* 選取 **以發佈的形式檢視頁面** 標題列動作可正確顯示頁面。

### 100%高度 {#height}

頁面的內文元素不支援100%高度。

* 您可以透過以下方式「拉伸」body元素，實作全熒幕主體：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 邊界收合 {#margin-collapsing}

如果body元素的第一個子元素有邊界，則會出現邊界收合問題。

* 解決方案是在主體元素層級新增clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
