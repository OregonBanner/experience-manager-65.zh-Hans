---
title: Adobe Experience Manager触屏优化UI的结构
description: 在Adobe Experience Manager中实现的触屏优化UI具有几个基础原则并且由几个关键元素组成
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 2%

---

# Adobe Experience Manager触屏优化UI的结构{#structure-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM)触屏优化UI具有多个基础原则，并且由多个关键元素组成：

## 控制台 {#consoles}

### 基本布局和调整大小 {#basic-layout-and-resizing}

UI同时适用于移动设备和桌面设备，不过Adobe决定使用一种适用于所有屏幕和设备的样式，而不是创建两种样式。

所有模块都使用相同的基本布局，在AEM中，这可以理解为：

![chlimage_1-142](assets/chlimage_1-142.png)

布局遵循响应式设计样式，并根据您所使用的设备/窗口的大小进行自适应。

例如，当分辨率低于1024 px（就像在移动设备上一样）时，显示器将相应地进行调整：

![chlimage_1-143](assets/chlimage_1-143.png)

### 标题栏 {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

标题栏显示全局元素，包括：

* 徽标以及您当前使用的特定产品/解决方案；对于AEM，这也将构成指向全局导航的链接
* 搜索
* 用于访问帮助资源的图标
* 用于访问其他解决方案的图标
* 任何等待您的警报或收件箱项目的指示器（以及对这些警报或收件箱项目的访问权限）
* 用户图标以及指向配置文件管理的链接

### 工具栏 {#toolbar}

这与您的位置以及与控制以下页面中的视图或资产相关的表面工具相关。 工具栏是特定于产品的，但这些元素有一些共同之处。

在任意位置，工具栏都会显示当前可用的操作：

![chlimage_1-145](assets/chlimage_1-145.png)

还取决于是否选择了资源：

![chlimage_1-146](assets/chlimage_1-146.png)

### 左边栏 {#left-rail}

可以根据需要打开/隐藏左边栏以显示：

* **时间线**
* **引用**
* **过滤器**

默认为 **仅内容** （隐藏边栏）。

![chlimage_1-147](assets/chlimage_1-147.png)

## 页面创作 {#page-authoring}

创作页面时，结构区域如下所示。

### 内容框架 {#content-frame}

页面内容在内容框架中呈现。 内容框架独立于编辑器，可确保不会因CSS或JavaScript而发生冲突。

内容框架位于窗口的右侧部分工具栏下。

![chlimage_1-148](assets/chlimage_1-148.png)

### 编辑器框架 {#editor-frame}

编辑器框架实现编辑功能。

编辑器框架是所有 *页面创作元素*. 它位于内容框架顶部，包括：

* 顶部工具栏
* 侧面板
* 所有叠加
* 任何其他页面创作元素；例如，组件工具栏

![chlimage_1-149](assets/chlimage_1-149.png)

### 侧面板 {#side-panel}

它包含两个默认选项卡，允许您选择资源和组件。 可以从此处将其拖放到页面上。

默认情况下，侧面板处于隐藏状态。 选中后，它将显示在左侧，或滑过以覆盖整个窗口（当窗口大小低于1024像素的宽度时；例如，在移动设备上）。

![chlimage_1-150](assets/chlimage_1-150.png)

### 侧面板 — 资源 {#side-panel-assets}

在“资源”选项卡中，您可以从资源范围中进行选择。 您还可以按特定术语进行筛选，或选择组。

![chlimage_1-151](assets/chlimage_1-151.png)

### 侧面板 — 资产组 {#side-panel-asset-groups}

在资源选项卡中，有一个可用于选择特定资源组的下拉列表。

![chlimage_1-152](assets/chlimage_1-152.png)

### 侧面板 — 组件 {#side-panel-components}

在“组件”选项卡中，可以从组件范围中进行选择。 您还可以按特定术语进行筛选，或选择组。

![chlimage_1-153](assets/chlimage_1-153.png)

### 叠加 {#overlays}

这些组件覆盖内容框架，并由 [图层](#layer) 实现如何（透明）与组件及其内容交互的机制。

叠加在编辑器框架中处于活动状态（包含所有其他页面创作元素），但它们实际上叠加了内容框架中的相应组件。

![chlimage_1-154](assets/chlimage_1-154.png)

### 图层 {#layer}

层是独立的功能束，可以激活它来：

* 提供页面的其他视图
* 允许您处理页面和/或与之交互

这些层为整个页面提供了完善的功能，而不是为单个组件执行的特定操作。

AEM附带了多个已为页面创作实施的层；例如，包括编辑、预览、批注。

>[!NOTE]
>
>层是一个强有力的概念，它影响用户对页面内容的查看以及与页面内容的交互。 在开发自己的层时，必须确保层在退出时进行清理。

### 图层切换器 {#layer-switcher}

层切换器允许您选择要使用的层。 关闭时，它表示当前使用的层。

图层切换器可以从工具栏的下拉菜单（位于窗口顶部的编辑器框架中）中使用。

![chlimage_1-155](assets/chlimage_1-155.png)

### 组件工具栏 {#component-toolbar}

单击组件（一次或缓慢双击）时，组件的每个实例都会显示其工具栏。 工具栏包含页面上组件实例（可编辑）可用的特定操作（例如，复制、粘贴、打开编辑器）。

根据可用空间，组件工具栏位于相应组件的上角或右下角。

![chlimage_1-156](assets/chlimage_1-156.png)

## 更多信息 {#further-information}

有关触屏UI相关概念的更多详细信息，请阅读 [AEM触屏优化UI的概念](/help/sites-developing/touch-ui-concepts.md).

有关详细信息，请参阅 [JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) （适用于启用了触屏的页面编辑器）。
