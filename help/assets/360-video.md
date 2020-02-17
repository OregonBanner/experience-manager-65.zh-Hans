---
title: 360/VR视频
description: 了解如何在Dynamic media中处理360和虚拟现实(VR)视频。
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 360/VR视频 {#vr-video}

360度全景视频同时录制每个方向的视图。 它们使用全方位相机或一组相机拍摄。 在平面显示器上播放时，用户可以控制观看角度；在移动设备上播放通常利用其内置的陀螺仪控件。

Dynamic Media - Scene7模式包含对交付360个视频资产的本机支持。 默认情况下，查看或回放不需要任何其他配置。 使用标准视频扩展（如。mp4、.mkv和。mov）交付360视频。 最常见的编解码器是H.264。

本节介绍如何与360/VR视频查看器一起渲染等长形视频，以实现房间、属性、位置、风景、医疗程序等的沉浸式观看体验。

目前不支持空间音频；如果音频在立体声中混合，则余额(L/R)不会随客户更改摄像机视角而改变。

See also [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

## 360视频实际操作情况 {#video-in-action}

点 [击空间站360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) ，打开浏览器窗口并观看360度全方位视频。 在视频播放过程中，将鼠标指针拖动到新位置以更改观看角度。

![360来自空间站](assets/6_5_360videoiss_simplified.png)*的视频样本视频帧360*

## 360/VR视频和Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用Adobe Premier pro查看和编辑360/VR素材。 例如，您可以将徽标和文本正确放置到场景中，并应用专门为等矩形媒体设计的效果和过渡。

请参 [阅编辑360/VR视频](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)。

## 上传资产以与360视频查看器一起使用 {#uploading-assets-for-use-with-the-video-viewer}

上传到AEM的360个视频资产在资产页面上标记为“ **Multimedia** ”，与普通视频资产类似。

![6_5_360video-select以预览在卡片](assets/6_5_360video-selecttopreview.png)*视图中看到的已上载360个视频资产。 资产将标记为“多媒体”。*

**要上传资产以与360视频查看器一起使用，请执行以下操作：**

1. 已创建专用于360视频资产的文件夹。
1. [将自适应视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   与标准非360视频内容相比，渲染360视频内容对源视频分辨率和编码再现分辨率的要求更高。

   您可以使用Dynamic media附带的现成自适应视频配置文件。 但是，请注意，对于使用非360视频查看器渲染的相同设置进行编码的非360视频，其视频质量将明显低于360。 因此，如果需要高质量的360视频，请执行以下操作：

   * 理想情况下，原始360视频内容应具有以下任一分辨率：

      * 1080p - 1920 x 1080，称为全高清或全高清分辨率，或
      * 2160p - 3840 x 2160，称为4K、UHD或Ultra HD分辨率。 这种非常大的显示分辨率通常出现在高级电视机和计算机显示器上。 2160p分辨率通常称为“4K”，因为宽度接近4000像素。 换句话说，它提供的像素是1080p的4倍。
   * [创建具有更高质量再现的自定义自适应视频配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 。 例如，您可能希望创建包含以下三个设置的自适应视频配置文件：

      * width=auto;height=720;比特率=2500 kbps
      * width=auto;height=1080;比特率=5000 kbps
      * width=auto;height=1440;比特率=6600 kbps
   * 处理专用于360个视频资源的文件夹中的360个视频内容。
   请注意，此方法还将对最终用户的网络和CPU提出更高的要求。

1. [将视频上传到文件夹](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets)。

## 覆盖360个视频的默认长宽比 {#overriding-the-default-aspect-ratio-of-videos}

要使上传的资产符合您要与360视频查看器一起使用的360视频，该资产的长宽比必须为2。

默认情况下，如果视频的长宽比（宽度／高度）为2.0，则AEM会将视频检测为“360”。如果您是管理员，则可以通过在CRXDE Lite中的以下位置设置可选属性来覆盖默认的长宽比设置2: `s7video360AR`

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **属性类型**:Double
   * **值**:浮点长宽比，默认为2.0。

设置此属性后，该属性将立即对现有视频和新上传的视频生效。

资产详细信息页面和视频360 Media WCM组件的360 [个视频资产宽高比](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components)。

首先上传360个视频。

## Previewing 360 Video {#previewing-video}

您可以使用“预览”来查看您的360视频对客户的外观，并确保其正常运行。

See also [Editing Viewer Presets](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

如果您对360视频满意，可以发布它。

请参阅[在网页上嵌入视频查看器或图像查看器](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html)。请参阅[将 URL 关联到您的 Web 应用程序](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html)。请注意，如果您的交互式内容具有相对URL的链接，特别是指向AEM站点页面的链接，则无法使用基于URL的链接方法。
See [Adding Dynamic Media Assets to pages.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)

**预览360个视频**

1. 在资 **[!UICONTROL 产中]**，导航到您创建的现有360视频。 点按360视频资产以在预览模式下将其打开。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   点按360视频资产以预览视频。

1. 在预览页面的左上角附近，点按下拉列表，然后选择查看 **[!UICONTROL 器]**。

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   从“查看器”列表中，点 **[!UICONTROL 按Video360_social]**，然后执行下列操作之一：

   * 在视频上拖动鼠标指针可改变静态场景的观看角度。
   * 点击视频的“播 **[!UICONTROL 放]** ”按钮开始播放；播放视频时，在视频上拖动鼠标指针以改变您的观看角度。
   ![6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360视频屏幕截图。*

   * 从“查看器”列表中，点 **[!UICONTROL 按视频360VR]**。

      虚拟现实(VR)视频是通过使用虚拟现实头盔访问的沉浸式视频内容。 与普通视频一样，您可以在使用360度摄像机录制或捕捉视频时，在开始时创建VR视频。
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *360 VR视频屏幕截图。*

1. Near the upper-right of the preview page, tap **[!UICONTROL Close]**.

## 发布360视频 {#publishing-video}

您需要发布360视频才能使用它。 发布360视频时，将激活URL和嵌入代码。 它还将360视频发布到Dynamic Media云中，该云与CDN集成以实现可升级和高性能交付。

有关 [如何发布360视频的详细信息](/help/assets/publishing-dynamicmedia-assets.md) ，请参阅发布Dynamic Media资产。
See also [Embedding the Video or Image Viewer on a Web Page](https://helpx.adobe.com/experience-manager/6-5/help/assets/embed-code.html).
See also [Linking URLs to your web application](https://helpx.adobe.com/experience-manager/6-5/help/assets/linking-urls-to-yourwebapplication.html). 请注意，如果您的交互式内容具有相对URL的链接，特别是指向AEM站点页面的链接，则无法使用基于URL的链接方法。
See also [Adding Dynamic Media Assets to pages.](https://helpx.adobe.com/experience-manager/6-5/help/assets/adding-dynamic-media-assets-to-pages.html)
