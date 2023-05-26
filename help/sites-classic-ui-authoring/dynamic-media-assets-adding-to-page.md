---
title: 将 Dynamic Media 资源添加到页面
description: 要将Dynamic Media功能添加到您在网站上使用的资源，您可以直接在页面上添加Dynamic Media或交互式媒体组件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 3%

---

# 将 Dynamic Media 资源添加到页面{#adding-dynamic-media-assets-to-pages}

要将Dynamic Media功能添加到您在网站上使用的资源，您可以添加 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 交互式媒体]** 组件直接显示在页面上。 输入 **[!UICONTROL 设计]** 模式和启用Dynamic Media组件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic Media和交互式媒体组件是智能的，它们知道您添加的是图像还是视频，并且可用的选项会相应地发生更改。

如果您使用Dynamic Media作为WCM，则可以直接将Adobe Experience Manager资源添加到页面。

>[!NOTE]
>
>可开箱即用于传送横幅的图像映射。

## 将Dynamic Media组件添加到页面 {#adding-a-dynamic-media-component-to-a-page}

添加 [!UICONTROL Dynamic Media] 或 [!UICONTROL 交互式媒体] 将组件添加到页面与将组件添加到任何页面相同。 此 [!UICONTROL Dynamic Media] 和 [!UICONTROL 交互式媒体] 以下各节将详细介绍组件。

要将Dynamic Media组件/查看器添加到页面，请执行以下操作：

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 如果没有可用的Dynamic Media组件，请在 [!UICONTROL Sidekick] 输入 **[!UICONTROL 设计]** 模式。
1. 选择 **[!UICONTROL 编辑]** parsys。
1. 选择 **[!UICONTROL Dynamic Media]** 以使得Dynamic Media组件可用。

   >[!NOTE]
   >
   >参见 [在设计模式下配置组件](/help/sites-authoring/default-components-designmode.md) 了解更多信息。

1. 返回到 **[!UICONTROL 编辑]** 模式，方法是单击 [!UICONTROL Sidekick].
1. 拖动 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 交互式媒体]** 组件来自 **[!UICONTROL 其他]** 在sidekick中分组到所需位置的页面上。
1. 选择 **[!UICONTROL 编辑]** 因此组件将打开。
1. [编辑组件](#dynamic-media-component) 视需要而定。
1. 选择 **[!UICONTROL 确定]** 以保存更改。

## Dynamic Media组件 {#dynamic-media-components}

[!UICONTROL Dynamic Media] 和 [!UICONTROL 交互式媒体] 中提供 [!UICONTROL Sidekick] 下 **[!UICONTROL Dynamic Media]**. 您使用 **[!UICONTROL 交互式媒体]** 交互式资产（如交互式视频、交互式图像或轮播集）的组件。 对于所有其他Dynamic Media组件，请使用 **[!UICONTROL Dynamic Media]** 组件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>默认情况下，这些组件不可用，在使用之前必须在“设计”模式下选择它们。 [在“设计”模式下可用它们之后](/help/sites-authoring/default-components-designmode.md)中，您可以将组件添加到页面，就像添加任何其他Experience Manager组件一样。

### Dynamic Media组件 {#dynamic-media-component}

Dynamic Media组件是智能的 — 根据您添加的是图像还是视频，您有各种不同的选项。 该组件支持图像预设、基于图像的查看器（如图像集、旋转集、混合媒体集和视频）。 此外，查看器会做出响应。 也就是说，屏幕大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

>[!NOTE]
>
>当您添加 [!UICONTROL Dynamic Media] 组件，和 **[!UICONTROL Dynamic Media设置]** 为空，或者无法正确添加资产，请检查以下各项：
>
>* 您有 [已启用Dynamic Media](/help/assets/config-dynamic.md). Dynamic Media默认处于禁用状态。
>* 图像具有金字塔tiff文件。 在启用Dynamic Media之前导入的图像没有金字塔tiff文件。
>


#### 使用图像时 {#when-working-with-images}

此 [!UICONTROL Dynamic Media] 组件允许您添加动态图像，包括图像集、旋转集和混合媒体集。 您可以放大、缩小旋转集中的图像或从其他类型的旋转集中选择图像（如果适用）。

您还可以直接在组件中配置查看器预设、图像预设或图像格式。 要使图像具有响应性，您可以设置断点或应用响应式图像预设。

![chlimage_1-72](assets/chlimage_1-72a.png)

您可以通过单击来编辑以下Dynamic Media设置 **[!UICONTROL 编辑]** ，然后单击 **[!UICONTROL Dynamic Media设置]** 选项卡。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在的组件中设置它 **[!UICONTROL 高级]** 制表符 **[!UICONTROL 宽度]** 和 **[!UICONTROL 高度]** 属性。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 参见 [管理查看器预设](/help/assets/managing-viewer-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

此选项仅在查看图像集、旋转集或混合媒体集时可用。 显示的查看器预设是智能的。 也就是说，只显示相关的查看器预设。

**[!UICONTROL 图像预设]**  — 从下拉菜单中选择现有的图像预设。 如果您要查找的图像预设不可见，则必须使其可见。 参见 [管理图像预设](/help/assets/managing-image-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

如果要查看图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 图像修饰符]**  — 通过提供其他图像命令可以更改图像效果。 这些命令在 [管理图像预设](/help/assets/managing-viewer-presets.md) 和 [命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

如果要查看图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 断点]**  — 如果您在响应式网站上使用此资产，则必须添加页面断点。 图像断点由逗号(，)分隔。 当图像预设中未定义高度或宽度时，此选项有效。

如果要查看图像集、旋转集或混合媒体集，则此选项不可用。

您可以编辑以下内容 [!UICONTROL 高级设置] 通过单击 **[!UICONTROL 编辑]** 在组件中。

**[!UICONTROL 标题]**  — 更改图像的标题。

**[!UICONTROL 替换文字]**  — 为已关闭图形的用户在图像中添加标题。

如果要查看图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL URL，打开方式]**  — 您可以从设置资产以打开链接。 设置 **[!UICONTROL URL]** 和 **[!UICONTROL 打开方式]** 以指明希望它在同一窗口还是新窗口中打开。

如果要查看图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 宽度和高度]**  — 如果希望图像为固定大小，请输入以像素为单位的值。 将这些值留空可使资源具有自适应性。

#### 使用视频时 {#when-working-with-video}

使用 **[!UICONTROL Dynamic Media]** 用于将动态视频添加到网页的组件。 编辑组件时，您可以选择使用预定义的视频查看器预设来播放页面上的视频。

![chlimage_1-74](assets/chlimage_1-74a.png)

您可以编辑以下内容 [!UICONTROL Dynamic Media设置] 通过单击 **[!UICONTROL 编辑]** 在组件中。

>[!NOTE]
>
>默认情况下，Dynamic Media视频组件是自适应的。 如果要使其变为固定大小，请在组件中设置它，并使用 **[!UICONTROL 宽度]** 和 **[!UICONTROL 高度]** 在 **[!UICONTROL 高级]** 选项卡。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的视频查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 参见 [管理查看器预设](/help/assets/managing-viewer-presets.md).

您可以编辑以下内容 [!UICONTROL 高级] 通过单击设置 **[!UICONTROL 编辑]** 在组件中。

**[!UICONTROL 标题]**  — 更改视频的标题。

**[!UICONTROL 宽度和高度]**  — 如果希望视频为固定大小，请输入以像素为单位的值。 将这些值留空可使其自适应。

#### 投放安全视频 {#how-to-delivery-secure-video}

在Experience Manager6.2中，当您安装 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)中，您可以控制是通过安全SSL连接(HTTPS)还是不安全连接(HTTP)来交付视频。 默认情况下，视频投放协议自动继承自嵌入网页的协议。 如果网页是通过HTTPS加载的，则视频也通过HTTPS传输。 反过来，如果网页位于HTTP上，则视频将通过HTTP发送。 通常，此默认行为是正常的，无需进行任何配置更改。 但是，您可以覆盖此默认行为。 附加 `VideoPlayer.ssl=on` 指向URL路径的末尾或嵌入代码片段中其他查看器配置参数的列表。 这两个操作中的任何一个都会强制进行安全视频交付。

有关安全视频交付和使用的更多信息， `VideoPlayer.ssl` configuration attribute中，请参见 [安全视频交付](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) 在查看器参考指南中。 除了视频查看器之外，安全视频交付还可用于混合媒体查看器和交互式视频查看器。

### 交互式媒体组件 {#interactive-media-component}

交互式媒体组件适用于在其上具有交互性的资源，例如热点或图像映射。 如果您有交互式图像、交互式视频或轮播横幅，请使用 **[!UICONTROL 交互式媒体]** 组件。

此 [!UICONTROL 交互式媒体] 组件是智能的 — 根据您添加的是图像还是视频，您拥有各种选项。 此外，查看器会做出响应。 也就是说，屏幕大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

![chlimage_1-75](assets/chlimage_1-75a.png)

您可以编辑以下内容 **[!UICONTROL 常规]** 通过单击设置 **[!UICONTROL 编辑]** 在组件中。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 必须先发布查看器预设，然后才能使用它们。 参见 [管理查看器预设](/help/assets/managing-viewer-presets.md).

**[!UICONTROL 标题]**  — 更改视频的标题。

**[!UICONTROL 宽度和高度]**  — 如果希望视频为固定大小，请输入以像素为单位的值。 将这些值留空可使其自适应。

您可以编辑以下内容 **[!UICONTROL 添加到购物车]** 通过单击设置 **[!UICONTROL 编辑]** 在组件中。

**[!UICONTROL 显示产品资产]**  — 默认情况下，此值处于选中状态。 产品资产会按照商务模块中的定义显示产品的图像。 清除复选标记将不显示产品资产。

**[!UICONTROL 显示产品价格]**  — 默认情况下，此值处于选中状态。 产品价格显示项目价格，如商务模块中所定义。 清除复选标记将不显示产品价格。

**[!UICONTROL 显示产品表单]**  — 默认情况下，不选中此值。 产品表单包括任何产品变体，如大小和颜色。 清除复选标记将不显示产品变型。
