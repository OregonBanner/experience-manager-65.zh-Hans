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
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 1%

---


# 360/VR Video {#vr-video}

360度视频同时在每个方向记录一个视图。 它们使用全方位相机或一组相机拍摄。 在平面显示器上播放时，用户可以控制观看角度； 在移动设备上播放通常利用其内置的陀螺仪控件。

Dynamic Media- Scene7模式包含对360个视频资产投放的本机支持。 默认情况下，查看或回放不需要任何其他配置。 您可以使用标准视频扩展（如。mp4、.mkv和。mov）交付360视频。 最常见的编解码器是H.264。

本节介绍如何与360/VR视频查看器一起渲染等长方形视频，实现房间、属性、位置、景观、医疗过程等的沉浸式观看体验。

当前不支持空间音频； 如果音频在立体声中混合，则余额(L/R)不会随客户更改摄像机视角而改变。

See also [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

## 360视频实际操作情况 {#video-in-action}

点 [击空间站](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 360打开浏览器窗口并观看360度视频。 在视频播放过程中，将鼠标指针拖动到新位置以更改视角。

![360来自空间](assets/6_5_360videoiss_simplified.png)*站的视频样本视频帧360*

## 360/VR视频和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用Adobe Premier Pro视图和编辑360/VR素材。 例如，您可以将徽标和文本正确放置到场景中，并应用专为等长方形媒体设计的效果和过渡。

请参 [阅编辑360/VR视频](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上传要与360视频查看器一起使用的资产 {#uploading-assets-for-use-with-the-video-viewer}

上传到AEM的360个视频资产在资产页面上 **会被标** 记为“多媒体”，这与普通视频资产类似。

![6_5_360video-select以预览已上](assets/6_5_360video-selecttopreview.png)*传的360视频资产，该资产显示在卡视图中。 资产将标记为“多媒体”。*

**要上传资产以用于360视频查看器，请执行以下操作：**

1. 已创建专用于360视频资产的文件夹。
1. [将自适应视频用户档案应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   渲染360视频内容比标准非360视频内容对源视频分辨率和编码演绎版分辨率的要求更高。

   您可以使用现成的自适应视频用户档案，它已随Dynamic Media提供。 但是，请注意，对于使用非360视频查看器渲染的设置进行编码的非360视频，其视频质量将明显低于您的360视频质量。 因此，如果需要高质量的360视频，请执行以下操作：

   * 理想情况下，原始360视频内容应具有以下任一分辨率：

      * 1080p - 1920 x 1080，称为全高清或全高清分辨率，或
      * 2160p - 3840 x 2160，称为4K、UHD或Ultra HD分辨率。 这种非常大的显示分辨率通常出现在高级电视机和计算机显示器上。 2160p分辨率通常称为“4K”，因为宽度接近4000像素。 换句话说，它优惠1080p像素的4倍。
   * [创建具有更高质量再现的自定](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 义自适应视频用户档案。 例如，您可能希望创建包含以下三种设置的自适应视频用户档案:

      * width=auto; height=720; 比特率=2500 kbps
      * width=auto; height=1080; 比特率=5000 kbps
      * width=auto; height=1440; 比特率=6600 kbps
   * 处理专用于360个视频资源的文件夹中的360个视频内容。

   请注意，这种方法也会对最终用户的网络和CPU提出更大的要求。

1. [将视频上传到文件夹](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets)。

## 覆盖360个视频的默认长宽比  {#overriding-the-default-aspect-ratio-of-videos}

要使已上传资产符合360视频查看器使用条件，资产的长宽比必须为2。

默认情况下，如果视频的长宽比（宽／高）为2.0，则AEM会将其检测为“360”。如果您是管理员，则可以通过在CRXDE Lite中的以下位置设置可选属性来覆盖默认 `s7video360AR` 的长宽比设置2:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **属性类型**: 多次
   * **值**: 浮点长宽比，默认为2.0。

设置此属性后，该属性将立即对现有视频和新上传的视频生效。

长宽比适用于资产详细信息页面和视频360媒体WCM组 [件的360视频资产](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)。

开始，上传360个视频。

## Previewing 360 Video {#previewing-video}

您可以使用预览来查看您的360视频对客户的外观，并确保其按预期行事。

See also [Editing Viewer Presets](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

如果您对360视频感到满意，可以发布该视频。

请参阅[在网页上嵌入视频查看器或图像查看器](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)。请参阅[将 URL 关联到您的 Web 应用程序](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html)。请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页的链接，则无法使用基于URL的链接方法。
See [Adding Dynamic Media Assets to pages.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)

**预览360个视频**

1. 在 **[!UICONTROL 资产]**&#x200B;中，导航到您创建的现有360视频。 点按360视频资产以在预览模式下打开它。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   点按360视频资产以预览视频。

1. 在预览页面的左上角附近，点按下拉列表，然后选择查看 **[!UICONTROL 器。]**

   ![6_5_360video-预览-viewers](assets/6_5_360video-preview-viewers.png)

   在“查看器”列表卡 **[!UICONTROL 中，点按Video360]**_social，然后执行下列操作之一：

   * 在视频上拖动鼠标指针可改变静态场景的观看角度。
   * 点击视频的“播 **[!UICONTROL 放]** ”按钮开始播放； 播放视频时，在视频上拖动鼠标指针以改变观看角度。

   ![6_5_360video-预览-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360视频屏幕截图。*

   * 在“查看器”列表卡中， **[!UICONTROL 点按Video360VR。]**

      虚拟现实(VR)视频是一种身临其境的视频内容，可通过使用虚拟现实头盔来访问。 与普通视频一样，您可以在开始使用360度视频摄像机录制或捕捉视频时创建VR视频。
   ![6_5_360video-预览-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR视频屏幕截图。*

1. Near the upper-right of the preview page, tap **[!UICONTROL Close.]**

## 发布360视频 {#publishing-video}

您需要发布360视频才能使用它。 发布360视频时，将激活URL和嵌入代码。 它还将360视频发布到Dynamic Media云，该云与CDN集成，可扩展且高性能投放。

有关 [如何发布360视频](/help/assets/publishing-dynamicmedia-assets.md) ，请参阅发布Dynamic Media资产。
See also [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html).
See also [Linking URLs to your web application](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). 请注意，如果您的交互式内容包含相对URL的链接，特别是指向AEM Sites页的链接，则无法使用基于URL的链接方法。
See also [Adding Dynamic Media Assets to pages.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)
