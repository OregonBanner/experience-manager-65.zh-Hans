---
title: 360/VR视频
description: 了解如何在Dynamic Media中使用360和虚拟现实(VR)视频。
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR 视频
role: Business Practitioner, Administrator
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: a4e9a4003bf0ce686578d3f8b3fddc19bc49dfb4
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# 360/VR视频{#vr-video}

360度视频同时记录每个方向的视图。 它们是用全方位相机或一组相机拍摄的。 在平面显示器上播放时，用户可以控制观看角度；移动设备上的播放通常使用其内置的陀螺仪控件。

Dynamic Media - Scene7模式包括对交付360个视频资产的本机支持。 默认情况下，查看或播放不需要任何其他配置。 您使用标准视频扩展名(如.mp4、.mkv和.mov)交付360视频。 最常见的编解码器是H.264。

本节介绍如何与360/VR视频查看器一起渲染等矩形视频，以体验房间、属性、位置、景观、医疗程序等的沉浸式观看体验。

当前不支持空间音频；如果音频在立体声中混合，则余额(L/R)不会随客户更改相机视角而改变。

另请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

## 360视频正在播放{#video-in-action}

点按[空间站360](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS)以打开浏览器窗口并观看360度视频。 在视频播放期间，将鼠标指针拖动到新位置以更改观看角度。

![360视频采](assets/6_5_360videoiss_simplified.png)
*样来自空间站的视频帧360*

## 360/VR视频和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro查看和编辑360/VR素材。 例如，您可以将徽标和文本正确放置在场景中，并应用专为等矩形媒体设计的效果和过渡。

请参阅[编辑360/VR视频](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上传资产以与360视频查看器{#uploading-assets-for-use-with-the-video-viewer}一起使用

上传到Adobe Experience Manager中的360个视频资产在资产页面上标记为&#x200B;**Multimedia**，与常规视频资产类似。

![6_5_360 video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*在卡片视图中看到已上传的360个视频资产。资产将标记为多媒体。*

**要上传资产以与360视频查看器一起使用，请执行以下操作：**

1. 创建了专用于360视频资产的文件夹。
1. [将自适应视频配置文件应用到该文件夹。](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)

   与标准非360视频内容相比，渲染360视频内容对源视频分辨率和编码呈现分辨率提出了更高的要求。

   您可以使用已随附的现成自适应视频配置文件Dynamic Media。 但是，对于使用非360视频查看器呈现的相同设置进行编码的非360视频，其视频质量会明显低于预期的360视频质量。 因此，如果需要高品质的360视频，请执行以下操作：

   * 理想情况下，您的原始360视频内容最好具有以下任一分辨率：

      * 1080p - 1920 x 1080，称为全高清或全高清分辨率，或
      * 2160p - 3840 x 2160，称为4K、UHD或UltraHD分辨率。 这种大的显示分辨率通常出现在高档电视机和电脑显示器上。 2160p分辨率通常称为“4K”，因为宽度接近4000像素。 换句话说，它的像素数是1080p的四倍。
   * [创建具有更高质量演绎版](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 的自定义自适应视频配置文件。例如，创建一个包含以下三个设置的自适应视频配置文件：

      * width=auto;height=720;bitrate=2500 kbps
      * width=auto;height=1080;bitrate=5000 kbps
      * width=auto;height=1440;bitrate=6600 kbps
   * 在专门用于360个视频资产的文件夹中处理360个视频内容。

   这种方法对最终用户的网络和CPU提出了更高的要求。

1. [将视频上传到文件夹](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。

## 覆盖360个视频的默认宽高比{#overriding-the-default-aspect-ratio-of-videos}

对于要将上传的资产视为您打算与360视频查看器一起使用的360视频，资产的宽高比必须为2。

默认情况下，如果视频的宽高比（宽高）为2.0，则Experience Manager会将视频检测为“360”。如果您是管理员，则可以通过在CRXDE Lite中设置以下位置的可选`s7video360AR`属性来覆盖默认宽高比设置2:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **属性类型**:双精度
   * **值**:浮点长宽比，默认为2.0。

设置此属性后，该属性会立即对现有视频和新上传的视频生效。

宽高比适用于资产详细信息页面和[Video 360 Media WCM组件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)的360个视频资产。

首先上传360个视频。

## 预览360视频{#previewing-video}

您可以使用“预览”功能来查看您的360视频对客户的外观，并确保其行为符合预期。

另请参阅[编辑查看器预设](/help/assets/managing-viewer-presets.md#editing-viewer-presets)。

如果您对360视频满意，可以发布该视频。

请参阅[在网页上嵌入视频查看器或图像查看器。
](/help/assets/embed-code.md)请参阅[将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。
请参阅[将Dynamic Media Assets添加到页面。](/help/assets/adding-dynamic-media-assets-to-pages.md)

**要预览360个视频，请执行以下操作：**

1. 在&#x200B;**[!UICONTROL Assets]**&#x200B;中，导航到您创建的现有360视频。 点按360视频资产，以便在预览模式下将其打开。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   点按360视频资产，以便预览视频。

1. 在预览页面的左上角附近，点按下拉列表，然后选择&#x200B;**[!UICONTROL 查看器。]**

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   从“查看器”列表中，点按&#x200B;**[!UICONTROL Video360_social]**，然后执行下列操作之一：

   * 如果要更改静态场景的观看角度，请在视频中拖动鼠标指针。
   * 如果要开始播放，请点按视频的&#x200B;**[!UICONTROL 播放]**&#x200B;按钮。 在视频播放时，将鼠标指针拖动到视频上以更改观看角度。

   ![6_5_360video-preview-video360-socialA 360 ](assets/6_5_360video-preview-video360-social.png)*视频屏幕截图。*

   * 从查看器列表中，点按&#x200B;**[!UICONTROL Video360VR。]**

      虚拟现实(VR)视频是使用虚拟现实耳机访问的沉浸式视频内容。 与普通视频一样，在视频被录制或捕获时，您会在开始时使用360度摄像机创建VR视频。
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR视频屏幕截图。*

1. 在预览页面的右上角附近，点按&#x200B;**[!UICONTROL 关闭。]**

## 发布360视频{#publishing-video}

发布360视频，以便您使用。 发布360视频可激活URL和嵌入代码。 它还会将360视频发布到Dynamic Media云，该云与CDN集成以进行可扩展且性能出众的交付。

有关如何发布360视频的详细信息，请参阅[发布Dynamic Media Assets](/help/assets/publishing-dynamicmedia-assets.md)。
另请参阅[在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)。
另请参阅[将URL关联到Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md)。 如果您的交互式内容具有包含相对URL的链接，特别是指向Experience Manager站点页面的链接，则无法使用基于URL的链接方法。
另请参阅[将Dynamic Media Assets添加到页面。](/help/assets/adding-dynamic-media-assets-to-pages.md)
