---
title: 将Dynamic Media资产添加到页面
description: 要将Dynamic Media功能添加到您在网站上使用的资产中，您可以直接在页面上添加Dynamic Media或交互式媒体组件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 30%

---

# 将Dynamic Media资产添加到页面{#adding-dynamic-media-assets-to-pages}

要将Dynamic Media功能添加到您在网站上使用的资产中，您可以直接在页面上添加&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;或&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。 进入&#x200B;**[!UICONTROL 设计]**&#x200B;模式并启用Dynamic Media组件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic Media和交互式媒体组件是智能的 — 它们知道您添加的是图像还是视频，可用的选项会相应地发生更改。

如果您使用Dynamic Media作为WCM，则可以直接将Adobe Experience Manager资产添加到页面。

>[!NOTE]
>
>传送横幅可以使用现成的图像映射功能。

## 将Dynamic Media组件添加到页面 {#adding-a-dynamic-media-component-to-a-page}

将[!UICONTROL Dynamic Media]或[!UICONTROL 交互式媒体]组件添加到页面与将组件添加到任何页面相同。 以下各节详细介绍了[!UICONTROL Dynamic Media]和[!UICONTROL Interactive Media]组件。

要将 Dynamic Media 组件/查看器添加到页面，请执行以下操作：

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 如果没有可用的Dynamic Media组件，请在[!UICONTROL Sidekick]中选择标尺以进入&#x200B;**[!UICONTROL 设计]**&#x200B;模式。
1. 选择&#x200B;**[!UICONTROL Edit]** parsys。
1. 选择&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;以使Dynamic Media组件可用。

   >[!NOTE]
   >
   >请参阅[在设计模式中配置组件](/help/sites-authoring/default-components-designmode.md)，以了解更多信息。

1. 通过单击[!UICONTROL Sidekick]中的铅笔图标，返回到&#x200B;**[!UICONTROL 编辑]**&#x200B;模式。
1. 将&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;或&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件从Sidekick中的&#x200B;**[!UICONTROL 其他]**&#x200B;组拖动到所需位置的页面上。
1. 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以便组件打开。
1. [根据需要](#dynamic-media-component) 编辑组件。
1. 选择&#x200B;**[!UICONTROL OK]**&#x200B;以保存更改。

## Dynamic Media 组件 {#dynamic-media-components}

[!UICONTROL 动态] 媒体和  交互式媒体可在Sidekick下  的Dynamic Media **[!UICONTROL 下找到]**。对于任何交互式资产（例如交互式视频、交互式图像或传送集），请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。对于所有其他Dynamic Media组件，请使用&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>默认情况下，这些组件不可用，在使用之前必须在设计模式下选择这些组件。 [在设计模式下提供这些组件后](/help/sites-authoring/default-components-designmode.md)，您可以像添加任何其他Experience Manager组件一样，将组件添加到页面。

### Dynamic Media 组件 {#dynamic-media-component}

Dynamic Media组件是智能的 — 根据您添加的是图像还是视频，您有各种不同的选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的。 也就是说，屏幕的大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

>[!NOTE]
>
>添加[!UICONTROL Dynamic Media]组件且&#x200B;**[!UICONTROL Dynamic Media设置]**&#x200B;为空或无法正确添加资产时，请检查以下信息：
>
>* 您已经[启用了 Dynamic Media](/help/assets/config-dynamic.md)。默认情况下，Dynamic Media 处于禁用状态。
>* 图像具有金字塔 TIFF 文件。在启用Dynamic Media之前导入的图像没有金字塔tiff文件。

>



#### 处理图像时 {#when-working-with-images}

[!UICONTROL Dynamic Media]组件允许您添加动态图像，包括图像集、旋转集和混合媒体集。 您可以缩放图像，并在适当的情况下在旋转集内旋转图像，或从其他类型的集合中选择图像。

您还可以直接在组件中配置查看器预设、图像预设或图像格式。要使图像具有响应性，您可以设置断点或应用响应式图像预设。

![chlimage_1-72](assets/chlimage_1-72a.png)

您可以编辑以下Dynamic Media设置，方法是：单击组件中的&#x200B;**[!UICONTROL 编辑]**，然后单击&#x200B;**[!UICONTROL Dynamic Media设置]**&#x200B;选项卡。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在&#x200B;**[!UICONTROL Advanced]**&#x200B;选项卡的组件中，使用&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;属性设置它。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择一个现有的查看器预设。如果您要查找的查看器预设不可见，则必须使其可见。 请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

仅当您查看图像集、旋转集或混合媒体集时，此选项才可用。 显示的查看器预设是智能的。 也就是说，只显示相关的查看器预设。

**[!UICONTROL 图像预设]**  — 从下拉菜单中选择一个现有的图像预设。如果您要查找的图像预设不可见，则必须使其可见。 请参阅[管理图像预设](/help/assets/managing-image-presets.md)。如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 图像修饰符]**  — 您可以通过提供其他图像命令来更改图像效果。[管理图像预设](/help/assets/managing-viewer-presets.md)和[命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)中介绍了这些命令。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 断点]**  — 如果您在响应式网站上使用此资产，则必须添加页面断点。图像断点之间用逗号分隔(,)。 当图像预设中未定义高度或宽度时，可以使用此选项。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

您可以通过单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;来编辑以下[!UICONTROL 高级设置]。

**[!UICONTROL 标题]**  — 更改图像的标题。

**[!UICONTROL 替换文本]**  — 为关闭了图形的用户在图像中添加标题。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL URL，在中打开]**  — 您可以设置资产以从中打开链接。设置&#x200B;**[!UICONTROL URL]**&#x200B;和&#x200B;**[!UICONTROL 在]**&#x200B;中打开，以指示您希望在同一窗口还是新窗口中打开该窗口。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 宽度和高度]**  — 如果希望图像具有固定大小，请输入以像素为单位的值。将这两个值留空会使资产成为自适应资产。

#### 使用视频时 {#when-working-with-video}

使用&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;组件将动态视频添加到您的网页。 编辑组件时，您可以选择使用预定义的视频查看器预设来在页面上播放视频。

![chlimage_1-74](assets/chlimage_1-74a.png)

您可以通过单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;来编辑以下[!UICONTROL Dynamic Media设置]。

>[!NOTE]
>
>默认情况下，Dynamic Media 视频组件为自适应组件。如果要使其变为固定大小，请在组件的&#x200B;**[!UICONTROL Advanced]**&#x200B;选项卡中使用&#x200B;**[!UICONTROL Width]**&#x200B;和&#x200B;**[!UICONTROL Height]**&#x200B;设置它。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的视频查看器预设。如果您要查找的查看器预设不可见，则必须使其可见。 请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

您可以通过单击组件中的&#x200B;**[!UICONTROL 编辑]**&#x200B;来编辑以下[!UICONTROL 高级]设置。

**[!UICONTROL 标题]**  — 更改视频的标题。

**[!UICONTROL 宽度和高度]**  — 如果您希望视频具有固定大小，请输入以像素为单位的值。将这两个值留空会使视频成为自适应资产。

#### 提供安全视频 {#how-to-delivery-secure-video}

在Experience Manager6.2中，安装[FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)时，您可以控制是通过安全SSL连接(HTTPS)还是不安全连接(HTTP)来传送视频。 默认情况下，视频传输协议会自动继承嵌入式网页的协议。如果网页通过 HTTPS 加载，则视频也会通过 HTTPS 进行传输。反之，如果网页是HTTP，则视频会通过HTTP传送。 通常，此默认行为是正常的，无需进行任何配置更改。 但是，您可以覆盖此默认行为。 将`VideoPlayer.ssl=on`附加到URL路径的末尾或嵌入代码片段中其他查看器配置参数的列表。 任一操作都会强制确保视频传输安全。

有关视频安全传输和在 URL 路径中使用 `VideoPlayer.ssl` 配置属性的更多信息，请参阅《查看器参考指南》中的[视频安全传输](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)。除了视频查看器之外，安全视频交付也适用于混合媒体查看器和交互式视频查看器。

### 交互式媒体组件 {#interactive-media-component}

交互式媒体组件适用于具有交互功能的资产，例如热点或图像映射。如果您具有交互式图像、交互式视频或传送横幅，请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。

[!UICONTROL 交互式媒体]组件是智能的 — 根据您添加的是图像还是视频，您有各种不同的选项。 此外，查看器是响应式的。 也就是说，屏幕的大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

![chlimage_1-75](assets/chlimage_1-75a.png)

您可以通过在组件中单击&#x200B;**[!UICONTROL 编辑]**，来编辑以下&#x200B;**[!UICONTROL 常规]**&#x200B;设置。

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择一个现有的查看器预设。如果您要查找的查看器预设不可见，则必须使其可见。 查看器预设必须先发布，然后才能使用。请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

**[!UICONTROL 标题]**  — 更改视频的标题。

**[!UICONTROL 宽度和高度]**  — 如果您希望视频具有固定大小，请输入以像素为单位的值。将这两个值留空会使视频成为自适应资产。

您可以通过在组件中单击&#x200B;**[!UICONTROL 编辑]**，来编辑以下&#x200B;**[!UICONTROL 添加到购物车]**&#x200B;设置。

**[!UICONTROL 显示产品资产]**  — 默认情况下，此值处于选中状态。产品资产会按“商务”模块中的定义显示产品的图像。清除复选标记不会显示产品资产。

**[!UICONTROL 显示产品价格]**  — 默认情况下，此值处于选中状态。产品价格会按“商务”模块中的定义显示项目的价格。清除复选标记不会显示产品价格。

**[!UICONTROL 显示产品表单]**  — 默认情况下，未选择此值。产品表单包含所有产品变量，例如大小和颜色。清除复选标记不会显示产品变量。
