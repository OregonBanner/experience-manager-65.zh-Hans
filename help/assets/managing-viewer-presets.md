---
title: 管理查看器预设
description: 如何在Dynamic Media中创建、编辑和管理查看器预设。
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
feature: Viewer Presets
role: User, Admin
exl-id: 0899e497-88e9-4fc3-a6be-b3a149fb5b32
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '4520'
ht-degree: 8%

---

# 管理查看器预设{#managing-viewer-presets}

查看器预设是设置集合，用于确定用户在其计算机屏幕和移动设备上查看富媒体资产的方式。 如果您是管理员，则可以创建查看器预设。 设置可用于一系列查看器配置选项。 例如，您可以更改查看器的显示大小或缩放行为。

有关创建和自定义自己的HTML5查看器预设的说明，请参阅AdobeDynamic Media *HTML5查看器SDK API文档*. SDK可在嵌入到SDK本身的IS发布服务器上使用。 每个库版本均包含其自身的SDK文档。

路径: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.\
例如，3.10 SDK： [https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)

另请参阅 [AdobeDynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

本节介绍如何创建、编辑和管理查看器预设。 您可以随时将查看器预设应用于资产，以进行预览。 请参阅 [应用查看器预设](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>编辑任意 *预定义的现成查看器预设* 不受支持的方案。 如果尝试编辑现成的查看器预设，系统将提示您使用新名称保存查看器预设。

## 查看器的键盘辅助功能 {#keyboard-accessibility-for-viewers}

所有开箱即用的查看器都支持键盘辅助功能。

另请参阅 [键盘辅助功能和导航](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html).

## 管理查看器预设 {#managing-viewer-presets-1}

您可以通过点按，在Adobe Experience Manager中添加、编辑、删除、发布、取消发布和预览查看器预设 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>默认情况下，当您在资产的详细信息视图中选择查看器时，系统会显示15个查看器预设。 您可以提高此限制。请参阅[增加显示的查看器预设数量](#increasing-the-number-of-viewer-presets-that-display)。

### 查看器对响应式设计网页的支持 {#viewer-support-for-responsive-designed-web-pages}

不同的网页具有不同的需求。 例如，有时您需要一个网页，该网页会提供一个链接，在单独的浏览器窗口中打开HTML5查看器。 在其他情况下，可能需要直接将HTML5查看器嵌入到托管页面上。 在后一种情况下，网页可能具有静态布局。 或者，它可能会是“响应式”的，并且在不同设备或不同浏览器窗口大小上显示的内容会有所不同。 为了满足这些需求，Dynamic Media附带的所有预定义、开箱即用的HTML5查看器都支持静态网页和响应式设计网页。

请参阅 [响应式图像库](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) 有关如何将响应式查看器嵌入到网页的更多信息。

>[!NOTE]
>
>在首次使用现成查看器之前，请发布这些查看器。
>请参阅 [发布查看器预设].(#publishing-viewer-presets)

### 查看器预设系统兼容性 {#viewer-preset-system-compatibility}

Dynamic Media随附的所有现成查看器预设与以下系统完全兼容：

* 台式机
* Apple iPhone
* Apple iPad
* Android™智能手机
* Android™平板电脑
* 对于视频，为提供了对MP4播放的额外支持 [BlackBerry®](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) 和 [Windows Phone](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs).

### 查看器预设的富媒体类型 {#rich-media-types-for-viewer-presets}

在创建查看器预设时，管理员可以添加和自定义以下富媒体类型。

<table>
 <tbody>
  <tr>
   <td><strong>轮播集</strong><br /> </td>
   <td><p>将热点、图像映射（或两者）添加到一系列两个或多个图像中。 客户可以左右平移图像，然后在图像上选择热点以获取更多详细信息或直接从网站的类别、主页或登陆页面购买。</p> </td>
  </tr>
  <tr>
   <td><strong>尺寸</strong><br /> </td>
   <td><p>显示可让您旋转、平移、缩放或重新居中相机的3D场景。</p> </td>
  </tr>
  <tr>
   <td><strong>弹出缩放</strong></td>
   <td><p>在原始图像旁边显示缩放区域的第二个图像。 没有要使用的控件 — 用户将选定内容移动到要查看的区域上方。</p> <p>在确定此查看器的完整带宽使用情况时，请考虑在查看器中同时提供主图像和弹出图像。 主图像大小（舞台宽度和高度）和缩放因子决定了弹出图像大小。 要防止弹出文件变得过大，请平衡这两个值：如果主图像较大，请降低“缩放因子”值。 （弹出宽度和弹出高度决定了弹出窗口的大小，而不是提供给查看器的弹出图像的大小。）</p> <p>例如，如果主图像大小为350 x 350像素，缩放因子为3，则生成的弹出图像为1050 x 1050像素。 如果您的主图像大小为300 x 300像素，缩放因子为4，则弹出图像为1200 x 1200像素。 根据JPEG质量设置（建议的设置介于80-90之间），您可以显着减小文件大小。 建议的缩放因子为2.5到4，具体取决于主图像的大小。</p> </td>
  </tr>
  <tr>
   <td><strong>内联缩放</strong></td>
   <td>在原始查看器中显示缩放区域的图像。 没有要使用的控件。 即，用户将选定内容移动到要查看的区域上方。</td>
  </tr>
  <tr>
   <td><strong>图像集</strong></td>
   <td>在图像集查看器中，用户通过选择缩略图图像可以查看项目的不同视图或颜色变体。 此查看器还提供了用于仔细检查图像的缩放工具。</td>
  </tr>
  <tr>
   <td><strong>交互式图像</strong></td>
   <td>将热点添加到图像的某些部分，然后客户可以选择这些部分以获取更多详细信息或直接从网站的类别、主页或登陆页面购买。</td>
  </tr>
  <tr>
   <td><strong>交互式视频</strong></td>
   <td>缩略图会添加到视频中的时间轴区段，客户随后可以选择这些区段以获取更多详细信息或直接从网站的类别、主页或登陆页面购买。</td>
  </tr>
  <tr>
   <td><strong>混合媒体</strong></td>
   <td>在一个查看器中显示不同类型的媒体。 您可以包含旋转集、图像集、图像和视频。</td>
  </tr>
  <tr>
   <td><strong>全景图像</strong></td>
   <td><p>全景图像和PanoramicVR查看器可渲染球形全景图像，以便用户沉浸在房间、属性、位置或景观的360度查看体验中。</p> <p>要使上传的图像符合球面全景的条件，该图像必须具有以下一项或两项之一：</p>
    <ul>
     <li>长宽比为2:1。</li>
     <li>已用关键字标记 <code>equirectangular</code>，或 <code>spherical</code> 和 <code>panorama</code>，或 <code>spherical </code>和 <code>panoramic</code>. 请参阅 <a href="/help/sites-authoring/tags.md">使用标记</a>.</li>
    </ul> <p>纵横比和关键字条件都适用于资产详细信息页面和“全景媒体”WCM组件的全景资产。</p> <p><strong>重要</strong>：此查看器仅在Dynamic Media - Scene7模式下可用。</p> </td>
  </tr>
  <tr>
   <td><strong>智能裁剪视频</strong><br /> </td>
   <td><p>使用此查看器可自动检测并裁切到任何视频中的焦点。</p> </td>
  </tr>
  <tr>
   <td><strong>旋转集</strong></td>
   <td>提供图像的多个视图，以便用户可以旋转对象来检查不同的边和角度。</td>
  </tr>
  <tr>
   <td><strong>360视频</strong></td>
   <td><p>使用360/VR视频查看器呈现等矩形视频，沉浸式观看房间、财产、位置、景观或医疗过程的体验。</p> <p>在平面显示器上播放期间，用户可控制视角；在移动设备上播放通常应用其内置的陀螺仪控制。</p> <p>查看器包含对360个视频资产交付的本机支持。 默认情况下，查看或播放无需其他配置。 您可以使用标准视频扩展名(如.mp4、.mkv和.mov)来交付360视频。 最常见的编解码器是H.264。</p> <p><strong>重要</strong>：此查看器仅在Dynamic Media - Scene7模式下可用。</p> </td>
  </tr>
  <tr>
   <td><strong>视频</strong></td>
   <td><p>使用渐进式或自适应比特率流播放视频。 自适应比特率流自动执行设备和带宽检测，以正确格式提供正确质量的视频。</p> </td>
  </tr>
  <tr>
   <td><strong>垂直缩放</strong></td>
   <td><p>垂直缩放查看器可让您最大化产品图像查看体验，以便为用户提供产品的最佳呈现。 样本的垂直位置执行以下操作：</p>
    <ul>
     <li>确保色板“位于折页上方”。<br/> 对于水平色板，根据用户的桌面屏幕大小，只有在用户向下滚动页面后，才会显示这些色板。 通过将色板垂直放置在查看器中，可以确保无论用户的屏幕大小如何，色板均可见。</li>
     <li>最大化主图像大小。<br /> 对于水平色板，需要保留页面上的空间以确保它们可见。 此定位减小了主图像的大小。 但是，对于垂直样本布局，您无需分配此空间。 因此，您可以最大化主图像大小。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>缩放</strong></td>
   <td>允许用户通过选择放大该区域。 用户可以选择控件以放大、缩小图像，以及将图像重置为其默认大小。</td>
  </tr>
 </tbody>
</table>

### 现成查看器预设列表 {#list-of-out-of-the-box-viewer-presets}

下表标识了Dynamic Media随附的所有预定义的现成查看器预设。

另请参阅 [实时演示](https://landing.adobe.com/zh-Hans/na/dynamic-media/ctir-2755/live-demos.html).

有关查看器支持的Web浏览器和操作系统版本的信息，您可以查看查看器发行说明。

请参阅目录中的“查看器发行说明”。 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html).

>[!NOTE]
>
>Dynamic Media中的所有现成查看器预设都已激活（开），但您必须发布它们。
>请参阅 [发布查看器预设](#publishing-viewer-presets).
>
>您创建和添加的任何新查看器预设都必须激活*和*已发布。
>请参阅 [激活或停用查看器预设](#activating-or-deactivating-viewer-presets) 和 [发布查看器预设](#publishing-viewer-presets).

<table>
 <tbody>
  <tr>
   <td><strong>查看器预设标题</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>CSS 文件名称</strong><br /> </td>
  </tr>
  <tr>
   <td>Carousel_Dotted_dark</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Dotted_light</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_dark</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carusel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>尺寸</td>
   <td>尺寸</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>弹出</td>
   <td>弹出缩放</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>图像集_深色</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>图像集光</td>
   <td>图像集</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_dark</td>
   <td>混合媒体</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>混合媒体</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineZoom</td>
   <td>弹出缩放</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_dark</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>混合媒体</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>全景图像</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanoramicImageVR</td>
   <td>Panoramic_Image</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interactive_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_dark</td>
   <td>交互式视频</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>交互式视频</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>旋转集_深色</td>
   <td>旋转集</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>旋转集光</td>
   <td>旋转集</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>视频</p> <p>（包括对隐藏式字幕的支持）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>（包括基本视频播放控制，视频渲染以立体模式完成，手动视点控制关闭但陀螺仪控制开启，并且无社交媒体功能）</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(专为使用虚拟现实眼镜的最终用户而设计。 包括基本视频播放控件和社交媒体功能)</p> </td>
   <td>Video_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video_social</p> <p>（包括对隐藏式字幕和社交媒体的支持）</p> </td>
   <td>视频</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_dark<br /> </td>
   <td>缩放<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>缩放</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_dark<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### 支持的移动查看器手势矩阵 {#supported-mobile-viewers-gestures-matrix}

下表标识了iOS、Android™ 2.x和Android™ 3.x设备支持的移动设备查看器手势。

<table>
 <tbody>
  <tr>
   <td><strong>手势</strong></td>
   <td><strong>弹出缩放</strong></td>
   <td><strong>缩放</strong></td>
   <td><strong>旋转</strong></td>
  </tr>
  <tr>
   <td><p><strong>拖动</strong></p> </td>
   <td><p>潘斯</p> </td>
   <td><p>潘斯</p> </td>
   <td><p>潘斯</p> </td>
  </tr>
  <tr>
   <td><p><strong>选择</strong></p> </td>
   <td><p>显示弹出窗口</p> </td>
   <td><p>显示或隐藏用户界面</p> </td>
   <td><p>显示或隐藏用户界面</p> </td>
  </tr>
  <tr>
   <td><p><strong>双击</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>放大或重置</p> </td>
   <td><p>放大或重置</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏开</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>放大(仅限iOS和Android™ 3x)</p> </td>
   <td><p>放大(仅限iOS和Android™ 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>捏紧关闭</strong></p> </td>
   <td><p>不适用</p> </td>
   <td><p>缩小(仅限iOS和Android™ 3倍)</p> </td>
   <td><p>缩小(仅限iOS和Android™ 3倍)</p> </td>
  </tr>
  <tr>
   <td><p><strong>轻扫</strong></p> </td>
   <td><p>滚动样本栏</p> </td>
   <td><p>滚动图像</p> </td>
   <td><p>旋转</p> </td>
  </tr>
  <tr>
   <td><p><strong>轻触</strong></p> </td>
   <td><p>滚动样本栏</p> </td>
   <td><p>滚动图像</p> </td>
   <td><p>旋转</p> </td>
  </tr>
 </tbody>
</table>

## 增加显示的查看器预设数 {#increasing-the-number-of-viewer-presets-that-display}

Experience Manager在查看资源时会显示各种不同的查看器预设 **[!UICONTROL 详细信息视图]** > **[!UICONTROL 查看器]**. 您可以增加或减少显示的查看器数量。

**增加显示的查看器预设数：**

1. 导航到CRXDE Lite([https://localhost:4502/crx/de](https://localhost:4502/crx/de))。
1. 导航到位于以下位置的查看器预设列表节点：

   `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. 在 **[!UICONTROL limit]** 属性中，将默认设 **[!UICONTROL 置为15的Value]**（值）更改为所需的数字。
1. 导航到位于的查看器预设数据源 `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. 在limit属性中，将数字更改为所需的数字，例如 `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. 选择 **[!UICONTROL 全部保存]**.

## 创建查看器预设 {#creating-a-new-viewer-preset}

通过创建查看器预设，可应用各种设置以查看资产并与之交互。 但是，您无需创建查看器预设。 如果您愿意，可以使用AEM Assets中已提供的默认开箱即用查看器预设。

如果选择创建查看器预设，则在保存查看器预设后，查看器的状态会自动激活(设置为 **[!UICONTROL 开启]**)。 此状态表示在Dynamic Media组件和Interactive Media组件中以及预览图像或视频时，该状态均可见。

某些查看器预设具有独占设置，这些设置可能会影响查看器的使用和整体行为。 根据您创建的查看器预设，您可能需要了解这些特殊注意事项。

请参阅 [创建交互式查看器预设的特殊注意事项](#special-considerations-for-creating-an-interactive-viewer-preset).

请参阅 [创建轮播横幅查看器预设的特殊注意事项](#special-considerations-for-creating-a-carousel-banner-viewer-preset).

**要创建查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产] > [!UICONTROL 查看器预设]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. 在“查看器预设”页面的工具栏上，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 新建查看器预设]** 对话框，在 **[!UICONTROL 预设名称]** 字段中，输入新预设的名称。 请仔细选择名称 — 选择后它们将无法编辑 **[!UICONTROL 创建]**.

   稍后在这些步骤中保存预设时，该名称会显示在查看器预设页面的“预设标题”列标题下。

1. 在富媒体类型下拉菜单中，选择要创建的查看器预设类型，然后在页面的右上角选择 **[!UICONTROL 创建]**.

   请参阅 [查看器预设的富媒体类型](#rich-media-types-for-viewer-presets).

1. 在“查看器预设编辑器”页面上，选择 **[!UICONTROL 外观]** 选项卡。
1. 执行下列操作之一：

   * 在 **[!UICONTROL 选定类型]** 在下拉菜单中，选择要自定义其可视设计的组件。 或者，您可以选择查看器中的任何可视元素，以选择进行配置。

     通过可视编辑器，可查看特定属性对样式有何影响。 设置或调整任何属性，使用编辑器左侧的示例即时查看它对查看器有何影响。

     有关每种类型查看器预设的CSS样式属性，请参阅自定义 *`<viewer name>`* 查看器”中的帮助主题 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果您创建的查看器预设类型为 `Mixed_Media`，请参见 [自定义混合媒体查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) 以获取每个属性的列表和说明。

   * 如果您在单独的CSS文件中定义了样式设置，则可以将CSS文件上传到AEM Assets。 选择 **[!UICONTROL 导入CSS]** 在 **[!UICONTROL 选定类型]** 下拉菜单（如有必要，请向上滚动可视编辑器以查看它），以便您可以查找上传的CSS文件并将其与查看器预设关联。

     导入CSS文件时，可视编辑器将检查CSS是否使用正确的查看器标记。 例如，如果您正在创建缩放查看器，则必须使用其查看器类名定义导入的所有CSS规则 `.s7mixedmediaviewer` 在父查看器元素上定义。

     您可以导入任意的手工制作CSS，只要它正确定义给定查看器的CSS标记即可。 (CSS标记在任何“自定义 *&lt;viewer name=&quot;&quot;>* 查看器”中的帮助主题 [查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html). 例如，如果要阅读有关缩放查看器的CSS标记，请参阅 [自定义缩放查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html).) 但是，可视编辑器可能并不了解某些CSS值。 在这种情况下，可视编辑器会尝试覆盖错误，以便CSS仍然可用。

   >[!NOTE]
   >
   >如果您希望直接在其原始表单中编辑CSS，请选择 **[!UICONTROL 显示/隐藏CSS]** 在“Selected Type（选定类型）”下拉菜单下（如有必要，向上滚动可视编辑器以查看它）。
   >与可视编辑器一样，直接在CSS中更改属性时，您会立即看到该属性对查看器示例有何影响。 并且，该属性会在可视编辑器中同时自动更新。 因此，您可以使用原始CSS编辑器或可视编辑器，也可以交替使用两者。

   >[!NOTE]
   >
   >对于按钮图稿，请选择2x图像并上传高分辨率图稿。 使用交互式图像和购物横幅时，您还可以从各种现成的热点按钮中进行选择。

1. （可选）在编辑查看器预设页面顶部附近，选择 **[!UICONTROL 桌面]**， **[!UICONTROL 平板电脑]**，或 **[!UICONTROL 电话]** 为不同的设备和屏幕类型唯一定义可视样式。
1. 在“查看器预设编辑器”页面上，选择 **[!UICONTROL 行为]** 选项卡。 或者，您可以选择查看器中的任何可视元素，以选择进行配置。
例如，对于 *videoplayer* 类型，在下 **[!UICONTROL 修饰符]** > **[!UICONTROL 播放]**，您可以从三个自适应比特率流选项中选择一个：

   * **[!UICONTROL 短划线]**  — 视频流仅显示为短划线。 但是，在Safari/iOS设备上，您必须选择 **[!UICONTROL hls]** 作为类型。
   * **[!UICONTROL hls]**  — 视频仅以hls形式流式传输。
   * **[!UICONTROL 自动]**  — 最佳做法。 DASH和HLS流的创建已优化存储。 因此，Adobe建议您始终选择 **[!UICONTROL 自动]** 作为播放类型。 视频流采用短划线、HLS或渐进式格式，如以下播放顺序所示：
      * 如果浏览器支持DASH，则首先使用DASH流。
      * 如果浏览器不支持DASH，则使用HLS流，其次是。
      * 如果浏览器不支持DASH或HLS，则最后使用渐进式播放。

   >[!NOTE]
   >
   >要查看和使用 **[!UICONTROL 短划线]** 选项，必须先由您帐户上的Adobe技术支持启用。 请参阅 [在您的帐户上启用DASH](/help/assets/video.md#enable-dash).

1. 从&#x200B;**[!UICONTROL 选定类型]**&#x200B;下拉菜单中，选择要更改其行为的组件。

   可视编辑器中的许多组件都有一个与之关联的详细说明。 展开组件以显示其关联参数时，这些描述会显示在蓝色框中。

   有些“查看器类型”具有的组件允许您在 **[!UICONTROL IS 命令]**&#x200B;文本字段中指定“图像提供”命令。有关可使用的命令列表，请参阅[图像提供 API 参考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html)。

   >[!NOTE]
   >
   >**如果您使用的是触摸设备，例如手机或平板电脑……**
   >
   >
   >在文本字段中键入值后，选择用户界面中的其他位置以提交更改并关闭虚拟键盘。 如果选择Enter，则不执行任何操作。

1. 在页面的右上角附近，选择 **[!UICONTROL 保存]**.
1. 发布您的新查看器预设，以便您可以在网站上使用它。

   请参阅 [发布查看器预设](#publishing-viewer-presets).

   >[!IMPORTANT]
   >
   >对于使用自适应比特率流配置文件的旧视频，URL将继续像往常一样播放（通过HLS流播放），直到您离开 [重新处理视频资产](/help/assets/processing-profiles.md#reprocessing-assets). 在重新处理之后，同一URL将继续工作，但是现在使用 *两者* 已启用DASH和HLS流。

### 创建交互式查看器预设的特殊注意事项 {#special-considerations-for-creating-an-interactive-viewer-preset}

**关于面板中图像缩略图的显示模式**

创建或编辑交互式视频查看器预设时，可以选择要在选择时使用的显示模式设置 `InteractiveSwatches` 从 **[!UICONTROL 选定的组件]** 下的菜单 **[!UICONTROL 行为]** 选项卡。 您选择的显示模式会影响视频播放时缩略图的显示方式和显示时间。 您可以选择 `segment`显示模式（默认）或 `continuous` 显示模式。

<table>
 <tbody>
  <tr>
   <td><strong>显示模式</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>市场细分</td>
   <td><p><code>Segment </code>是现成交互式视频查看器预设的默认显示模式 <code>Shoppable_Video_light</code> 和 <code>Shoppable_Video_dark</code> 以及您自己创建的任何交互式视频查看器预设。</p> <p>在此模式下，当分配给视频区段的缩略图数量少于显示面板中的可见点数时。 此外，下一个或上一个子区段的缩略图包括 <i>非 </i>拉入以填充面板中的任何空点。 也就是说，它可以保留分配给特定视频区段的色板的显示。</p> </td>
  </tr>
  <tr>
   <td>连续</td>
   <td><p>在 <code>continuous </code>显示模式时，如果区段中的缩略图数量小于面板中显示的缩略图数量，则查看器会自动包含下一区段的缩略图显示。 或者，如果显示的是最后一个缩略图，查看器会自动包含上一个区段的缩略图显示。</p> <p>此 <a href="/help/assets/interactive-videos.md">本主题中的视频</a> 是 <code>continuous </code>显示模式。</p> </td>
  </tr>
 </tbody>
</table>

**关于交互式视频查看器中的自动滚动行为**

在交互式视频查看器中，缩略图的自动滚动行为独立于您选择的显示模式。

创建或编辑交互式视频查看器预设时，您可以从“行为”选项卡访问“自动滚动”。在行为选项卡中，从 **[!UICONTROL 选定的组件]** 下拉菜单，选择 **[!UICONTROL 交互式色板]**. “自动滚动”复选框列在“IS 命令”文本字段的下方。

如果在查看器预设中禁用&#x200B;**[!UICONTROL 自动滚动]**（清除复选框），则在用户播放视频时，该面板仅显示整个视频长度的第一个缩略图。但是，如果需要，用户可以使用向上和向下箭头图标手动滚动缩略图。

在查看器预设中启用（选择）**[!UICONTROL 自动滚动]**&#x200B;后，在视频播放过程中，分配给视频区段的缩略图图像会在区段开始时滚动到视图中。但是，在某些情况下，区段内某些缩略图的显示时间是其之前或之后缩略图显示时间的两倍。发生此行为的原因是区段中缩略图的数量大于面板中可见缩略图的数量，且不可平均分割。

举例说明，假设您有一个30秒的视频段。 而且，在30秒内总共会显示九个缩略图。 浏览器的大小调整方式应使显示面板中有四个可见的缩略图位置。 将30秒的视频时间段划分为3个子段。 下表显示了给定时间子区段显示哪些缩略图的细分：

| **视频子区段** | **子区段时间（以秒为单位）** | **在面板中可见的缩略图** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

视频子区段3的扩展范围不超过为其分配的缩略图。 另请注意，缩略图4、6和7在面板中的可见时间是其他缩略图的两倍。

查看器用于根据可用位置数确定在面板中显示缩略图的逻辑如下：

* 子区段数=向上舍入到下一个子区段（缩略图数/缩略图面板中的可见插槽数，基于浏览器窗口大小）。
根据上表中的示例， 9缩略图/ 4个插槽= 2.25；查看器逻辑将其四舍五入到三个子区段。

* 缩略图数=舍入到下一个缩略图（缩略图数/视频子区段数）。
根据上表中的示例，9缩略图/3个视频子区段= 3个缩略图。

* 子区段的持续时间=视频总持续时间/视频子区段数。
使用上表中的示例，30秒/3个视频子区段=每个视频子区段显示10秒。

#### 创建轮播横幅查看器预设的特殊注意事项 {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

在创建Carousel Banner查看器预设时，可以按如下方式访问更改热点的样式：

| | **描述** | **操作** |
|---|---|---|
| **[!UICONTROL 热点图标]** | 更改用于热点的图标 | 要更改热点图标图像，请在 **[!UICONTROL 外观]** 选项卡，在 **[!UICONTROL 选定的组件]**，选择 **[!UICONTROL ImageMapEffect]**. 下 **[!UICONTROL 图标]**，选择 **[!UICONTROL 背景]** 和 **[!UICONTROL 图像]** 字段导航到所需的背景图像。 |

## 激活或取消激活查看器预设 {#activating-or-deactivating-viewer-presets}

用户界面中可用的查看器预设取决于在创作模式下活动的查看器预设。 默认情况下，查看器预设在创建后处于“开”状态。 如果关闭预设，则不会在创作模式下看到该预设。 如果发布预设，则无论是否切换该预设，都会始终发布该预设。 如果列表变得太笨重，或者您不希望查看器预设可用，则可能需要取消激活查看器预设。

**要激活或取消激活查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 在“查看器预设”页面上的 **[!UICONTROL 状态]** 列标题中，选择切换可激活或停用查看器预设。

   已激活的查看器预设会在右侧显示切换开关，它位于蓝色框中；已停用的查看器预设会在左侧显示切换开关，它位于浅灰色框中。

## 发布查看器预设 {#publishing-viewer-presets}

激活（或打开）查看器预设的状态意味着查看器预设在Dynamic Media组件、交互式媒体组件中可见，并且无论何时查看资源。

但是，到 *deliver* 作为具有查看器预设的资产，还必须发布查看器预设。 必须激活所有查看器预设 *和* 已发布，以获取资产的URL或嵌入代码。 请务必激活并发布Dynamic Media附带的所有现成查看器预设。 您创建和添加的自定义查看器预设将自动激活，但也必须发布。

请参阅 [激活或停用查看器预设](#activating-or-deactivating-viewer-presets).

另请参阅 [预览资源](/help/assets/previewing-assets.md).

**要发布查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 选择一个或多个要发布的查看器预设。
1. 在工具栏上，选择 **[!UICONTROL Publish]** 图标。

## 排序查看器预设 {#sorting-viewer-presets}

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 选择 **[!UICONTROL 预设标题]**， **[!UICONTROL 类型]**， **[!UICONTROL 已发布]**，或 **[!UICONTROL 状态]** 以按该列标题排序。 例如，选择 **[!UICONTROL 类型]**  按字母顺序或反向字母顺序对查看器预设类型进行排序。

## 编辑查看器预设 {#editing-viewer-presets}

编辑任意 *预定义的现成查看器预设* 不受支持的方案。 如果编辑现成的查看器预设，系统会提示您使用新名称保存该预设。

**要编辑查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 通过选中查看器预设标题左侧的框选择预设。
1. 在工具栏上，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL 查看器预设编辑器]** 页面上，使用 **[!UICONTROL 外观]** 和 **[!UICONTROL 行为]** 选项卡。

   从 **[!UICONTROL 外观]** 选项卡，在查看器预设编辑器页面的左上角附近，选择 **[!UICONTROL 桌面]**， **[!UICONTROL 平板电脑]**，或 **[!UICONTROL 电话]** 以更改资产的显示模式。

1. 在页面的右上角附近，执行下列操作之一：

   * 选择 **[!UICONTROL 保存]** 以保存所做更改并返回到“查看器预设”页面。
   * 选择 **[!UICONTROL 取消]** 使所做的任何更改失效并返回到“查看器预设”页。

## 删除自定义查看器预设 {#deleting-custom-viewer-presets}

您可以删除已创建并添加到Dynamic Media中的查看器预设。

**要删除自定义查看器预设，请执行以下操作：**

1. 在Experience Manager的左上角，选择Experience Manager徽标，然后在左边栏中选择 **[!UICONTROL 工具]** （锤子图标） **[!UICONTROL 资产]** > **[!UICONTROL 查看器预设]**.
1. 在“查看器预设”页面上，选中预设标题，然后选择 **[!UICONTROL 垃圾桶]** 图标。
1. 选择&#x200B;**[!UICONTROL 删除]**。

## 将查看器预设应用于资产 {#applying-a-viewer-preset-to-an-asset}

如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

**要将查看器预设应用于资产，请执行以下操作：**

1. 打开资产，在页面的左上角附近，选择下拉菜单，然后选择 **[!UICONTROL 查看器]**.

   >[!NOTE]
   >
   >如果已发布资产和选定的查看器，则在选择查看器预设后 **[!UICONTROL 将显示]** “ **[!UICONTROL URL]** ”和“嵌入”按钮。

1. 从左窗格中选择查看器预设，以将其应用于资源。

   您可以 [复制要共享的URL](/help/assets/linking-urls-to-yourwebapplication.md) 和其他用户。

## 通过查看器预设交付资产 {#delivering-assets-with-viewer-presets}

要获取查看器预设的URL，请参阅 [将URL关联到您的Web应用程序](/help/assets/linking-urls-to-yourwebapplication.md). 另请参阅 [在网页上嵌入视频查看器](/help/assets/embed-code.md).

如果您将Experience Manager用作WCM，则可以直接在页面上使用查看器预设添加资源。 请参阅 [将Dynamic Media资源添加到页面](/help/assets/adding-dynamic-media-assets-to-pages.md).
