---
title: 编辑器限制
seo-title: 编辑器限制
description: 触屏优化UI中的编辑器利用叠加与iFrame中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。
seo-description: 触屏优化UI中的编辑器利用叠加与iFrame中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 14%

---

# 编辑器限制{#editor-limitations}

触屏优化UI中的编辑器利用叠加与iFrame中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。本页概述了这些限制，并尽可能提供解决方案或解决方法。

## 功能限制{#functional-limitations}

使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接未处于活动状态{#links-not-active}

在[编辑页面](/help/sites-authoring/editing-content.md)时，链接不处于活动状态。

* [切换到 **** ](/help/sites-authoring/editing-content.md#preview-mode) 预览模式，以使用内容中的链接进行导航。

### 结构页面{#structure-pages}

页面不能命名`structure`。 名为`structure`的页面在页面编辑器中将不可编辑。

## CSS限制{#css-limitations}

开发人员在编辑器与CSS的交互时可能会遇到以下限制。

### 绝对定位的元素{#absolutely-positioned-elements}

绝对定位的元素可能会导致其叠加位置出现问题。

* 如果发生这种情况，请确保绝对定位元素的尺寸正确无误，因为编辑器将创建一个具有相同尺寸的叠加图。

### Vh单元{#vh-units}

`vh` 不支持设备，因为iframe高度必须由AEM自动调整。

### 固定背景图像{#fixed-background-images}

由于固定背景图像嵌入在iFrame中，因此在滚动时，该图像可能不显示为固定背景图像。

* 在标题栏操作中选择&#x200B;**查看已发布的页面**&#x200B;可正确显示页面。

### 100%高 {#height}

页面的主体元素不支持100%高度。

* 为了通过“拉伸”主体元素来实现全屏主体，可以进行如下工作：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 边距折叠{#margin-collapsing}

如果主体元素的第一个子元素具有边距，则可以看到边距折叠问题。

* 解决方案是在主体元素级别添加clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
