---
title: 将 Dynamic Media 资产添加到页面
seo-title: 将 Dynamic Media 资产添加到页面
description: 要向您在网站上使用的资产中添加 Dynamic Media 功能，您可以直接在页面上添加 Dynamic Media 组件或交互式媒体组件。
seo-description: 要向您在网站上使用的资产中添加 Dynamic Media 功能，您可以直接在页面上添加 Dynamic Media 组件或交互式媒体组件。
uuid: 650d0867-a079-4936-a466-55b7a30803a2
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 331f4980-5193-4546-a22e-f27e38bb8250
translation-type: tm+mt
source-git-commit: 23dfcc944a83dd683078cfe00f85c4cc734e7752
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 54%

---


# 将 Dynamic Media 资产添加到页面{#adding-dynamic-media-assets-to-pages}

To add the Dynamic Media functionality to assets you use on your websites, you can add the **[!UICONTROL Dynamic Media]** or **[!UICONTROL Interactive Media]** component directly on the page. You do this by entering [!UICONTROL Design] mode and enabling the dynamic media components. 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic Media 组件和交互式媒体组件是智能组件，它们知道您添加的是图像还是视频，并能据此相应地更改提供的选项。

如果您使用AEM作为WCM，则可以直接将Dynamic Media资产添加到页面。

>[!NOTE]
>
>传送横幅可以使用现成的图像映射功能。

## Adding a Dynamic Media component to a page {#adding-a-dynamic-media-component-to-a-page}

Adding the [!UICONTROL Dynamic Media] or [!UICONTROL Interactive Media] component to a page is the same as adding a component to any page. The [!UICONTROL Dynamic Media] and [!UICONTROL Interactive Media] components are described in detail in the following sections.

要将 Dynamic Media 组件/查看器添加到页面，请执行以下操作：

1. 在 AEM 中，打开您要添加 Dynamic Media 组件的页面。
1. If no Dynamic Media component is available, click the ruler in the [!UICONTROL Sidekick] to enter **[!UICONTROL Design]** mode, click **[!UICONTROL Edit]** parsys, and select **[!UICONTROL Dynamic Media]** to make the Dynamic Media components available.

   >[!NOTE]
   >
   >请参阅[在设计模式中配置组件](/help/sites-authoring/default-components-designmode.md)，以了解更多信息。

1. Return to **[!UICONTROL Edit]** mode by clicking the pencil icon in the [!UICONTROL Sidekick].
1. Drag the **[!UICONTROL Dynamic Media]** or **[!UICONTROL Interactive Media]** component from the **[!UICONTROL Other]** group in the sidekick onto the page in the desired location.
1. 单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开该组件。
1. [](#dynamic-media-component)根据需要编辑该组件，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

## Dynamic Media 组件 {#dynamic-media-components}

[!UICONTROL Dynamic Media] 和 [!UICONTROL 交互式媒体] ，在Sidekick中的 [!UICONTROL Dynamic Media] 下可 **[!UICONTROL 以使用。]**&#x200B;对于任何交互式资产（例如交互式视频、交互式图像或传送集），请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。对于所有其他 Dynamic Media 资产，请使用 **[!UICONTROL Dynamic Media]** 组件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>这些组件在默认情况下不可用，需要先在设计模式中选择这些组件才能使用。[在“设计”模式下使用组件](/help/sites-authoring/default-components-designmode.md)，您可以像添加任何其他AEM组件一样将组件添加到页面。

### Dynamic Media 组件 {#dynamic-media-component}

Dynamic Media组件是智能的——根据您添加的是图像还是视频，您有各种选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器具有响应性。 也就是说，屏幕的大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

>[!NOTE]
>
>When you add the [!UICONTROL Dynamic Media] component, and **[!UICONTROL Dynamic Media Settings]** is blank or you cannot add an asset properly, check the following:
>
>* 您已经[启用了 Dynamic Media](/help/assets/config-dynamic.md)。默认情况下，Dynamic Media 处于禁用状态。
>* 图像具有金字塔 TIFF 文件。在启用 Dynamic Media 之前导入的图像没有金字塔 TIFF 文件。

>



#### 处理图像时 {#when-working-with-images}

The [!UICONTROL Dynamic Media] component lets you add dynamic images, including image sets, spin sets, and mixed media sets. 您可以缩放图像，并在适当的情况下在旋转集内旋转图像，或从其他类型的集合中选择图像。

您还可以直接在组件中配置查看器预设、图像预设或图像格式。要使图像成为响应式图像，您可以设置断点，或应用响应式图像预设。

![chlimage_1-72](assets/chlimage_1-72a.png)

You can edit the following Dynamic Media settings by clicking **[!UICONTROL Edit]** in the component and then clicking the **[!UICONTROL Dynamic Media Settings]** tab.

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 If you want to make it a fixed size, set it in the component in the **[!UICONTROL Advanced]** tab with the **[!UICONTROL Width]** and **[!UICONTROL Height]** properties.

**[!UICONTROL 查看器预设]** -从下拉菜单中选择现有的查看器预设。 如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

如果您查看的是图像集、旋转集或混合媒体集，这是唯一可用的选项。显示的查看器预设也是智能的——仅显示相关的查看器预设。

**[!UICONTROL 图像预设]** -从下拉菜单中选择现有的图像预设。 如果未显示您要查找的图像预设，则可能需要将其显示出来。请参阅[管理图像预设](/help/assets/managing-image-presets.md)。如果您正在使用图像预设，则无法选择查看器预设，反之亦然。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 图像修饰符]** -您可以通过提供其他图像命令来更改图像效果。 These are described in [Managing Image Presets](/help/assets/managing-viewer-presets.md) and the [Command reference](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 断点]** -如果您在响应式站点上使用此资产，则需要添加页面断点。 图像断点之间需要使用逗号 (,) 进行分隔。当图像预设中未定义高度或宽度时，可以使用此选项。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

You can edit the following [!UICONTROL Advanced Settings] by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL 标题]** -更改图像的标题。

**[!UICONTROL 替换文本]** -为关闭图形的用户添加图像标题。

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL URL，打开方式]** -您可以设置资产以打开链接。 Set the **[!UICONTROL URL]** and **[!UICONTROL Open in]** to indicate whether you want it to open in the same window or a new window.

如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

**[!UICONTROL 宽度和高度]** -如果希望图像具有固定大小，请输入以像素为单位的值。 将这两个值留空会使资产成为自适应资产。

#### When working with video {#when-working-with-video}

Use the [!UICONTROL Dynamic Media] component to add dynamic video to your web pages. 编辑该组件时，您可以选择使用预定义的视频查看器预设，以在页面上播放视频。

![chlimage_1-74](assets/chlimage_1-74a.png)

You can edit the following [!UICONTROL Dynamic Media Settings] by clicking **[!UICONTROL Edit]** in the component.

>[!NOTE]
>
>默认情况下，Dynamic Media 视频组件为自适应组件。If you want to make it a fixed size, set it in the component with the **[!UICONTROL Width]** and **[!UICONTROL Height]** in the **[!UICONTROL Advanced]** tab.

**[!UICONTROL 查看器预设]** -从下拉菜单中选择现有的视频查看器预设。 如果未显示您要查找的查看器预设，则可能需要将其显示出来。请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

You can edit the following [!UICONTROL Advanced] settings by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL 标题]** -更改视频的标题。

**[!UICONTROL 宽度和高度]** -如果希望视频具有固定大小，请输入以像素为单位的值。 将这两个值留空会使视频成为自适应资产。

#### 如何安全传输视频 {#how-to-delivery-secure-video}

在 AEM 6.2 中，如果您安装了 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)，则可以控制是通过安全的 SSL 连接 (HTTPS) 还是不安全的连接 (HTTP) 来传输视频。默认情况下，视频传输协议会自动继承嵌入式网页的协议。如果网页通过 HTTPS 加载，则视频也会通过 HTTPS 进行传输。反之，如果网页通过 HTTP 加载，则视频也会通过 HTTP 进行传输。在大多数情况下，此默认行为不会产生问题，故而无需更改任何配置。不过，您可以通过以下方法覆盖此默认行为，以强制使用安全的视频传输方式：将 `VideoPlayer.ssl=on` 附加到 URL 路径末尾或嵌入式代码片段的其他查看器配置参数列表中。

有关视频安全传输和在 URL 路径中使用 `VideoPlayer.ssl` 配置属性的更多信息，请参阅《查看器参考指南》中的[视频安全传输](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html)。除视频查看器外，安全视频投放还可用于混合媒体查看器和交互式视频查看器。

### 交互式媒体组件 {#interactive-media-component}

交互式媒体组件适用于具有交互功能的资产，例如热点或图像映射。如果您具有交互式图像、交互式视频或传送横幅，请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。

The [!UICONTROL Interactive Media] component is smart – depending on whether you add an image or a video, you have various options. 此外，查看器具有响应性。 也就是说，屏幕的大小会根据屏幕大小自动更改。 所有查看器都是基于HTML5的查看器。

![chlimage_1-75](assets/chlimage_1-75a.png)

您可以通过在组件中单击&#x200B;**[!UICONTROL 编辑]**，来编辑以下&#x200B;**[!UICONTROL 常规]**&#x200B;设置。

**[!UICONTROL 查看器预设]** -从下拉菜单中选择现有的查看器预设。 如果未显示您要查找的查看器预设，则可能需要将其显示出来。查看器预设必须先发布，然后才能使用。请参阅管理查看器预设。

**[!UICONTROL 标题]** -更改视频的标题。

**[!UICONTROL 宽度和高度]** -如果希望视频具有固定大小，请输入以像素为单位的值。 将这两个值留空会使视频成为自适应资产。

You can edit the following **[!UICONTROL Add To Cart** settings by clicking **[!UICONTROL Edit]** in the component.

**[!UICONTROL 显示产品资产]** -默认情况下，此值处于选中状态。 产品资产会按“商务”模块中的定义显示产品的图像。清除复选标记不会显示产品资产。

**[!UICONTROL 显示产品价格]** -默认情况下，此值处于选中状态。 产品价格会按“商务”模块中的定义显示项目的价格。清除复选标记不会显示产品价格。

**[!UICONTROL 显示产品表单]** -默认情况下，此值未选中。 产品表单包含所有产品变量，例如大小和颜色。清除复选标记不会显示产品变量。
