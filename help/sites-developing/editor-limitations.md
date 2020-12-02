---
title: 编辑器限制
seo-title: 编辑器限制
description: 触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用方面以及对于开发人员而言都有一些限制。
seo-description: 触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用方面以及对于开发人员而言都有一些限制。
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: 844d42ed50da153077423190684aa85265bce12f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# 编辑器限制{#editor-limitations}

触屏优化UI中的编辑器利用叠加与iframe中限制的内容交互。 此交互在编辑器的使用方面以及对于开发人员而言都有一些限制。 本页概括了这些限制，并尽可能提供解决方案或解决办法。

## 功能限制{#functional-limitations}

使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接未激活{#links-not-active}

当[编辑页面](/help/sites-authoring/editing-content.md)时，链接不处于活动状态。

* [切换到 **** ](/help/sites-authoring/editing-content.md#preview-mode) Previewmode以使用内容中的链接进行导航。

### 结构页{#structure-pages}

不能命名页面`structure`。 名为`structure`的页面在页面编辑器中将不可编辑。

## CSS限制{#css-limitations}

开发人员在编辑器与CSS的交互时可能会遇到以下限制。

### 绝对定位元素{#absolutely-positioned-elements}

绝对定位的元素可能导致其叠加位置出现问题。

* 如果发生这种情况，请确保绝对定位元素的尺寸正确，因为编辑器将创建尺寸完全相同的叠加。

### Vh单位{#vh-units}

`vh` 不支持iframe高度，因为AEM必须自动调整iframe高度。

### 固定背景图像{#fixed-background-images}

由于固定背景图像嵌入在iframe中，因此在滚动时，固定背景图像可能不显示为固定。

* 在标题栏操作中选择&#x200B;**视图页面作为已发布**&#x200B;可正确显示页面。

### 100%高度{#height}

页面的正文元素不支持100%高度。

* 为了实现全屏机身，可进行如下“拉伸”机身元素：

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

* 解决方案是在主体元素级别添加一个清除器，如：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

