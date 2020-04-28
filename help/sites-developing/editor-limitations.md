---
title: 编辑器限制
seo-title: 编辑器限制
description: 触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用和开发人员的使用方面都有一些限制。
seo-description: 触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用和开发人员的使用方面都有一些限制。
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: 844d42ed50da153077423190684aa85265bce12f

---


# 编辑器限制{#editor-limitations}

触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用和开发人员的使用方面都有一些限制。 本页总结了这些限制，并尽可能提供解决方案或解决办法。

## 功能限制 {#functional-limitations}

在使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接不活动 {#links-not-active}

编辑 [页面时](/help/sites-authoring/editing-content.md)，链接不处于活动状态。

* [切换到 **预览** 模式](/help/sites-authoring/editing-content.md#preview-mode) ，以使用内容中的链接进行导航。

### 结构页面 {#structure-pages}

无法命名页面 `structure`。 命名的页面在页 `structure` 面编辑器中将不可编辑。

## CSS限制 {#css-limitations}

开发人员在编辑器与CSS的交互方面可能遇到以下限制。

### 绝对定位的元素 {#absolutely-positioned-elements}

绝对定位的元素可能会导致其叠加位置出现问题。

* 如果发生这种情况，请确保绝对定位的元素的尺寸正确，因为编辑器将创建尺寸完全相同的叠加。

### vh Units {#vh-units}

`vh` 不支持iframe高度，因为AEM必须自动调整iframe高度。

### 固定背景图像 {#fixed-background-images}

由于固定背景图像嵌入iframe中，因此在滚动时，固定背景图像可能不显示为固定。

* 在标 **题栏操作中选择视图页面** “已发布”后，将正确显示页面。

### 100% Height {#height}

页面的body元素不支持100%高度。

* 为了通过如下“拉伸”身体元素来实现全屏体，可以进行修复：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 边距折叠 {#margin-collapsing}

如果主体元素的第一子元素具有边距，则可以看到边距折叠问题。

* 解决方案是在主体元素级别添加一个清除器，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

