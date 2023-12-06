---
title: 360/VR视频
description: 了解如何在Dynamic Media中使用360和虚拟现实(VR)视频。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: 360 VR Video
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# 360/VR视频 {#vr-video}

360度视频同时记录每个方向的视图。 它们使用全方位相机或一系列相机来拍摄。 在平面显示器上播放期间，用户可控制视角；移动设备上的播放通常使用内置的陀螺仪控制。

Dynamic Media - Scene7模式包括对360个视频资源交付的本机支持。 默认情况下，查看或播放无需其他配置。 您可以使用标准视频扩展名(如.mp4、.mkv和.mov)来交付360视频。 最常见的编解码器是H.264。

本节介绍如何使用360/VR视频查看器渲染等矩形视频，以获得房间、属性、位置、景观、医疗程序等的沉浸式观看体验。

当前不支持空间音频；如果音频混入立体声，则平衡(L/R)不会随着客户改变相机视角而改变。

另请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md).

## 360视频的实际效果 {#video-in-action}

选择 [360号空间站](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 打开浏览器窗口并观看360度视频。 在视频播放过程中，将鼠标指针拖动到新位置以更改视角。

![360个视频样本，国际空间站漂浮在外层空间，其后面是地球和太阳。](assets/6_5_360videoiss_simplified.png)
*来自空间站360的视频帧*

## 360/VR视频和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro查看和编辑360/VR素材。 例如，您可以在场景中正确放置徽标和文本，并应用专门为等矩形介质设计的效果和过渡。

请参阅 [编辑360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## 上传资产以用于360视频查看器 {#uploading-assets-for-use-with-the-video-viewer}

上传到Adobe Experience Manager的360个视频资源将标记为 **多媒体** 在资产页面上，与普通视频资产类似。

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*在卡片视图中看到的已上传360视频资产。 该资产标记为多媒体。*

**上传资产以用于360视频查看器：**

1. 创建了一个专用于您的360视频资产的文件夹。
1. [将自适应视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   与标准的非360视频内容相比，渲染360视频内容对源视频分辨率和编码呈现版本分辨率提出了更高的要求。

   您可以使用随Dynamic Media提供的现成自适应视频配置文件。 但是，对于使用非360视频查看器渲染的相同设置进行编码的非360视频，它导致360视频质量明显降低。 因此，如果需要高品质360视频，请执行以下操作：

   * 理想情况下，原始的360视频内容最好具有以下分辨率之一：

      * 1080p - 1920 x 1080，称为全高清或全高清分辨率，或
      * 2160p - 3840 x 2160，称为4k、UHD或Ultra高清分辨率。 这种大屏幕分辨率通常出现在高端电视机和计算机显示器上。 2160p分辨率通常称为“4k”，因为宽度接近4000像素。 换句话说，它提供的像素是1080p的四倍。

   * [创建自定义自适应视频配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 高质量的节目。 例如，创建包含以下三个设置的自适应视频配置文件：

      * 宽度=自动；高度=720；比特率=2500 kbps
      * 宽度=自动；高度=1080；比特率=5000 kbps
      * 宽度=自动；高度=1440；比特率=6600 kbps

   * 在专门用于360个视频资产的文件夹中处理360个视频内容。

   这种方法给最终用户的网络和CPU提出了更高的要求。

1. [将视频上传到文件夹](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## 覆盖360个视频的默认纵横比  {#overriding-the-default-aspect-ratio-of-videos}

对于已上传的资产，要使其符合与360视频查看器一起使用的360视频资格，该资产的长宽比必须为2。

默认情况下，如果视频的长宽比（宽度/高度）为2.0，则Experience Manager会将视频检测为“360”。如果您是管理员，可以通过设置可选来覆盖默认纵横比设置2 `s7video360AR` CRXDE Lite中的属性：

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **属性类型**  — 双精度
   * **值**  — 浮点宽高比，默认为2.0。

设置此属性后，它会在现有视频和新上传的视频中立即生效。

长宽比适用于资源详细信息页面和 [视频360媒体WCM组件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

首先上传360个视频。

## 预览360视频 {#previewing-video}

您可以使用预览功能来查看客户对360视频的看法，并确保其行为符合预期。

另请参阅 [编辑查看器预设](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

如果对360视频满意，则可发布该视频。

请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md).
请参阅 [将URL链接到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。
请参阅 [将Dynamic Media资源添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md).

**要预览360视频，请执行以下操作：**

1. 在 **[!UICONTROL 资产]**，导航到您创建的现有360视频。 选择360视频资源，以便您可以在预览模式下将其打开。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   选择360视频资源，以便预览视频。

1. 在预览页面的左上角附近，选择下拉列表，然后选择 **[!UICONTROL 查看器]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   从查看器列表中，选择 **[!UICONTROL Video360_social]**，然后执行以下操作之一：

   * 如果要更改静态场景的视角，请将鼠标指针拖动到视频上。
   * 选择视频的 **[!UICONTROL 播放]** 按钮。 在播放视频时，拖动鼠标指针越过视频可改变视角。

   ![地球和太阳在背景中漂浮在外层空间的国际空间站屏幕截图&#x200B;](assets/6_5_360video-preview-video360-social.png)*360度视频截图。*

   * 从查看器列表中，选择 **[!UICONTROL Video360VR]**.

     虚拟现实(VR)视频是使用虚拟现实头戴式耳机访问的沉浸式视频内容。 与普通视频一样，当视频使用360度摄像机进行录制或捕获时，您首先会创建VR视频。

   ![浮动在外层空间的国际空间站特写屏幕截图，背景中部分可见地球和太阳](assets/6_5_360video-preview-video360vr.png)
   *360 VR视频截图。*

1. 在预览页面的右上角附近，选择 **[!UICONTROL 关闭]**.

## 发布360视频 {#publishing-video}

发布360视频以便使用。 发布360视频将激活URL和嵌入代码。 它还将360视频发布到Dynamic Media云，该云与CDN集成以实现可扩展的高性能交付。

请参阅 [发布Dynamic Media资源](/help/assets/publishing-dynamicmedia-assets.md) 以了解有关如何发布360视频的详细信息。
另请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md).
另请参阅 [将URL链接到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的交互式内容包含具有相对URL的链接，尤其是指向Experience Manager Sites页面的链接，则基于URL的链接方法不可用。
另请参阅 [将Dynamic Media资源添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md).
