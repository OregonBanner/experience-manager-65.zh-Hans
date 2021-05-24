---
title: AEM触屏UI的结构
seo-title: AEM触屏UI的结构
description: 触屏优化UI(在AEM中实施)具有多个基本原则，由几个关键元素组成
seo-description: 触屏优化UI(在AEM中实施)具有多个基本原则，由几个关键元素组成
uuid: 9a255238-1adc-4a40-9c37-30cb53ffb26c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 55dba890-4847-4986-b272-33480bc1d573
exl-id: e562b289-5d8b-4fa8-ad1c-fff5f807a45e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---

# AEM触屏UI的结构{#structure-of-the-aem-touch-enabled-ui}

AEM触屏UI具有多个基本原则，由几个关键元素组成：

## 控制台 {#consoles}

### 基本布局和大小调整{#basic-layout-and-resizing}

虽然UI既适用于移动设备，也适用于桌面设备，但Adobe决定使用一种样式，该样式适用于所有屏幕和设备，而不是创建两种样式。

所有模块都使用相同的基本布局，在AEM中，这可以看作：

![chlimage_1-142](assets/chlimage_1-142.png)

布局遵循响应式设计样式，并会根据您所使用的设备/窗口的大小来调整自身。

例如，当分辨率低于1024像素（与移动设备上的情况一样）时，显示屏将相应地进行调整：

![chlimage_1-143](assets/chlimage_1-143.png)

### 标题栏 {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

标题栏显示全局元素，包括：

* 徽标和您当前使用的特定产品/解决方案；对于AEM，它还会形成指向全局导航的链接
* 搜索
* 用于访问帮助资源的图标
* 用于访问其他解决方案的图标
* 等待您发送的任何警报或收件箱项目的指示器（并可访问）
* “用户”图标，以及指向用户档案管理的链接

### 工具栏 {#toolbar}

这与您的位置息息相关，而且还显示与控制以下页面中的视图或资产相关的工具。 工具栏特定于产品，但元素有一些通用性。

在任意位置，工具栏都会显示当前可用的操作：

![chlimage_1-145](assets/chlimage_1-145.png)

还取决于当前是否选择了某个资源：

![chlimage_1-146](assets/chlimage_1-146.png)

### 左边栏 {#left-rail}

可以根据需要打开/隐藏左边栏以显示：

* **时间轴**
* **引用**
* **筛选器**

默认值为&#x200B;**仅内容**（隐藏的边栏）。

![chlimage_1-147](assets/chlimage_1-147.png)

## 页面创作 {#page-authoring}

创作页面时，结构区域如下所示。

### 内容帧{#content-frame}

页面内容在内容框架中呈现。 内容框架完全独立于编辑器，可确保不会因CSS或Javascript而发生冲突。

内容框架位于窗口的右侧部分工具栏下。

![chlimage_1-148](assets/chlimage_1-148.png)

### 编辑器帧{#editor-frame}

编辑器框架实现编辑功能。

编辑器框架是用于所有&#x200B;*页面创作元素*&#x200B;的容器（抽象）。 它位于内容框架的顶部，包括：

* 顶部工具栏
* 侧面板
* 所有叠加图
* 任何其他页面创作元素；例如，组件工具栏

![chlimage_1-149](assets/chlimage_1-149.png)

### 侧面板{#side-panel}

其中包含两个默认选项卡，用于选择资产和组件；可以从此处拖放到页面上。

默认情况下，侧面板处于隐藏状态。 选择后，该窗口将显示在左侧，或滑过以覆盖整个窗口（当窗口大小低于1024像素的宽度时）；例如，在移动设备上)。

![chlimage_1-150](assets/chlimage_1-150.png)

### 侧面板 — 资产{#side-panel-assets}

在资产选项卡中，您可以从资产范围中进行选择。 您还可以过滤特定术语或选择群组。

![chlimage_1-151](assets/chlimage_1-151.png)

### 侧面板 — 资产组{#side-panel-asset-groups}

在资产选项卡中，您可以使用下拉列表选择特定的资产组。

![chlimage_1-152](assets/chlimage_1-152.png)

### 侧面板 — 组件{#side-panel-components}

在组件选项卡中，您可以从组件范围中进行选择。 您还可以过滤特定术语或选择群组。

![chlimage_1-153](assets/chlimage_1-153.png)

### 叠加 {#overlays}

这些参数覆盖内容框架，并由[层](#layer)使用，以了解如何与组件及其内容进行（完全透明）交互的机制。

叠加图位于编辑器框架中（包含所有其他页面创作元素），但它们实际上会覆盖内容框架中的相应组件。

![chlimage_1-154](assets/chlimage_1-154.png)

### 图层 {#layer}

层是一个独立的功能包，可激活它以：

* 提供页面的不同视图
* 允许您处理和/或与页面交互

与对单个组件执行的特定操作不同，这些层可为整个页面提供复杂的功能。

AEM附带了多个已实施的页面创作层；包括编辑、预览、注释。

>[!NOTE]
>
>层是一个强大的概念，会影响用户对页面内容的查看以及与页面内容的交互。 在开发您自己的层时，您需要确保该层在退出时清理。

### 层切换器{#layer-switcher}

层切换器允许您选择要使用的层。 关闭后，它表示当前正在使用的层。

图层切换器可作为工具栏（位于窗口顶部的编辑器框架内）中的下拉菜单使用。

![chlimage_1-155](assets/chlimage_1-155.png)

### 组件工具栏 {#component-toolbar}

单击组件的每个实例都将显示其工具栏（单击一次或慢速双击）。 工具栏包含可用于页面上的组件实例（可编辑）的特定操作（例如，复制、粘贴、打开编辑器）。

组件工具栏位于相应组件的右上角或右下角，具体取决于可用空间。

![chlimage_1-156](assets/chlimage_1-156.png)

## 更多信息 {#further-information}

有关触屏优化UI相关概念的更多详细信息，请继续阅读文章[AEM触屏优化UI](/help/sites-developing/touch-ui-concepts.md)的概念。

有关更多技术信息，请参阅适用于触屏优化页面编辑器的[JS文档集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。
