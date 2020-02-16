---
title: 视频
description: 了解如何在Dynamic media中处理视频
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
translation-type: tm+mt
source-git-commit: 569c552686e6312ecae0d500147a8b65354c303d

---


# 视频 {#video}

本节介绍如何在 Dynamic Media 中处理视频。

## 快速入门：视频 {#quick-start-videos}

以下工作流分步说明旨在帮助您在Dynamic media中快速设置和运行自适应视频集。每个步骤之后都会交叉引用主题标题，您可以在其中找到更多信息。

>[!NOTE]
>
>在Dynamic media中处理视频之前，请确保AEM管理员已在Dynamic Media - Scene7模式或Dynamic Media - Hybrid模式中启用并配置Dynamic Media Cloud服务。
>
>* 请参 [阅配置Dynamic Media - Scene7模式和Dynamic Media - Scene7模式中](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)[的配置Dynamic Media Cloud服务。](/help/assets/troubleshoot-dms7.md)
   >
   >
* 请参 [阅配置Dynamic Media](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) —— 混合模式中的配置Dynamic Media Cloud Services。
>



1. 通过执行以下操作，**上传 Dynamic Media 视频**：

   * 创建您自己的视频编码配置文件。或者，您只需使用Dynamic Media附带的 _预定义自适应视频编码配置文件_ 。

      * [创建视频编码配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming)。
      * Learn more about [Best practices for video encoding](#best-practices-for-encoding-videos).
   * 将视频处理配置文件关联到一个或多个要上传主视频的文件夹。

      * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。
      * 了解有关[组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)的更多信息。
      * 了解有关[组织数字资产](/help/assets/organize-assets.md)的更多信息。
   * 将主视频上传到文件夹。 您可以上传每个高达20 GB的视频文件。 将视频添加到文件夹时，会根据您为文件夹分配的视频处理配置文件对视频进行编码。

      * [上传视频](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets)。
      * Learn more about [Supported input file formats](/help/assets/assets-formats.md#supported-multimedia-formats).
   * 从资产 [视图或工作流视图](#monitoring-video-encoding-and-youtube-publishing-progress) ，监视视频编码的进度。




1. 通过执行以下任意操作，**管理 Dynamic Media 视频**：

   * 组织、浏览和搜索视频资产

      * [组织数字资产
](/help/assets/organize-assets.md)了解有关[组织数字资产以使用处理配置文件的最佳实践](organize-assets.md)的更多信息

      * [搜索视频资产](search-assets.md#custompredicates) 或搜 [索资产](managing-assets-touch-ui.md#search-assets)
   * 预览和发布视频资产

      * 查看源视频和视频的编码演绎版及其关联的缩略图：
         [预览视频](managing-video-assets.md#upload-and-preview-video-assets) 或预 [览资产](previewing-assets.md)
         [查看视频演绎版](video-renditions.md)
         [管理视频演绎版](managing-assets-touch-ui.md#managing-renditions)

      * [管理查看器预设](managing-viewer-presets.md)
      * [发布资产](publishing-dynamicmedia-assets.md)
   * 处理视频元数据

      * 查看编码视频演绎版的属性，如帧速率、音频和视频比特率以及编解码器：
         [查看视频演绎版属性](video-renditions.md)

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
         [编辑视频属性](managing-assets-touch-ui.md#editing-properties)

      * [管理数字资产的元数据](metadata.md)
      * [元数据架构](metadata-schemas.md)
   * 审核和批准视频，在视频中添加注释，以及保持全面的版本控制

      * [在视频中添加注释](managing-video-assets.md#annotate-video-assets) ，或在资 [产中添加注释](managing-assets-touch-ui.md#annotating)

      * [创建版本](managing-assets-touch-ui.md#asset-versioning)
      * [将工作流应用于资产](assets-workflow.md) ，或者 [请参阅启动资产的工作流](managing-assets-touch-ui.md#starting-a-workflow-on-an-asset)

      * [审核文件夹资产](bulk-approval.md)
      * [项目](../sites-authoring/projects.md)




1. 通过执行以下任一操作，**发布 Dynamic Media 视频**：

   * 如果您使用Adobe Experience manager作为Web内容管理系统，则可以将视频直接添加到网页中。

      * [将视频添加到网页](adding-dynamic-media-assets-to-pages.md)。
   * 如果您使用的是第三方Web内容管理系统，则可以将视频链接或嵌入到您的网页。

      * 使用URL集成视频：
         [将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md).

      * 使用网页上的嵌入代码集成视频：
         [将视频查看器嵌入网页](embed-code.md)。
   * [将视频发布到 YouTube](#publishing-videos-to-youtube)。
   * [生成视频报表](#viewing-video-reports)。

   * [向视频中添加字幕](#adding-captions-to-video)。



## Working with video in Dynamic Media {#working-with-video-in-dynamic-media}

Dynamic media中的视频是一个端到端的解决方案，它使得发布高质量自适应视频以跨多个屏幕（包括桌面、iOS、Android、Blackberry和Windows移动设备）进行流化变得很容易。自适应视频集为同一视频的不同版本编码，这些版本以不同的比特率和格式（如400 kbps、800 kbps和1000 kbps）进行编码。台式计算机或移动设备会检测可用带宽。

例如，在 iOS 移动设备上，设备检测到 3G、4G 或 Wi-Fi 等带宽。设备会随之自动从自适应视频集内的各种视频比特率中选择正确的编码视频。然后，视频会在桌面设备、移动设备或平板电脑上进行流播放。

此外，如果桌面或移动设备上的网络条件发生变化，设备会自动动态地切换视频质量。同时，如果客户在桌面上进入全屏模式，自适应视频集也会做出响应来使用较好的分辨率，从而改善客户的观看体验。使用自适应视频集可为在多个屏幕和设备上播放Dynamic media视频的客户提供最佳回放。

视频播放器用来确定在播放期间要播放或要选择的编码视频的逻辑基于以下算法：

1. 视频播放器根据最接近播放器本身中为“初始比特率”设置的值的比特率加载初始视频片段。
1. 视频播放器根据带宽速度的变化使用以下条件进行切换：

   1. 播放器会选取低于或等于估计带宽的最高带宽流。
   1. 播放器只考虑80%的可用带宽。 但是，如果它正在切换，则更为保守，只有70%，以避免过高估计，并立即切换回去。

有关算法的详细技术信息，请参阅 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

为了管理单个视频和自适应视频集，支持以下内容：

* 用多种支持的视频格式和音频格式上传视频，并将视频编码为 MP4 H.264 格式，以供在多种屏幕上播放。您可以使用预定义的自适应视频预设或单个视频编码预设，或者自定义您自己的编码，来控制视频的质量和大小。

   * 在生成自适应视频集时，会包括 MP4 视频。
   * **注意**：主/源视频不会添加到自适应视频集。

* 在所有HTML5视频查看器中设置视频字幕。
* 组织、浏览和搜索具有全面元数据支持的视频，以实现高效的视频资产管理。
* 将自适应视频集交付到Web以及桌面和移动设备，包括iPhone、iPad、Android、Blackberry和Windows手机。

自适应视频流播放在多种 iOS 平台上受支持。请参阅《[Scene7 查看器参考指南](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_video_reference.html)》。

Dynamic Media supports mobile video playback for MP4 H.264 video. You can find Blackberry devices that support this video format at the following: [Supported video formats on Blackberry](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

请参阅下面的文档，以了解支持此视频格式的 Windows 设备：[Windows Phone 上支持的视频格式](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)。

* 使用 Dynamic Media 视频查看器预设播放视频，包括以下查看器：

   * 单一视频查看器。
   * 将视频和图像内容组合在一起的混合媒体查看器。

* 配置视频播放器以满足您的品牌需求。
* 使用简单的 URL 或嵌入代码将视频集成到您的网站、移动站点或移动应用程序。

See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample.

另请参 [阅《Adobe Scene7查](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_s7_aem_asset_viewers.html) 看器参考指南》中的AEM和Scene7查看器以及AEM资 [产的查看器(仅适用于AEM资产](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_aem_asset_viewers.html) )。

## Best practice: Using the HTML5 video viewer {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5视频查看器预设是功能强大的视频播放器。您可以使用它们避免与HTML5视频播放相关的许多常见问题以及与移动设备相关的问题，如缺少自适应流交付和桌面浏览器访问力有限。

在播放器的设计方面，您可以使用标准的 Web 开发工具设计视频播放器的所有功能。例如，您可以使用 HTML5 和 CSS 设计按钮、控件和自定义标识图像背景，从而帮助您向客户展示自定义的外观。

在查看器的播放方面，查看器可以自动检测浏览器的视频功能。然后，它使用HLS（HTTP实时流）（也称为自适应视频流）来提供视频。 或者，如果这些传送方法不可用，则会改用 HTML5 渐进式流播放。

通过将使用 HTML5 和 CSS 设计播放组件的功能、支持嵌入式播放的功能，以及根据浏览器的容量使用自适应和渐进式流播放的功能整合到单一播放器中，您可以扩大富媒体内容可以传送到的桌面和移动用户的范围，并确保简化视频体验。

另请参阅《Scene7 查看器参考指南》中的“[关于 HTML5 查看器](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_viewers_about.html)”。

### 使用HTML5视频查看器在台式计算机和移动设备上播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动自适应视频流，比特率切换所使用的视频基于自适应视频集中的所有MP4视频。

使用HLS或渐进式视频下载进行视频回放。 在AEM的先前版本（如6.0、6.1和6.2）中，视频通过HTTP进行流化。

但是，在AEM 6.3和上，视频现在通过HTTPS（即HLS）进行流传输，因为DM网关服务URL也始终使用HTTPS。 请注意，此默认行为不会对客户产生影响。 也就是说，除非浏览器不支持，否则视频流将始终通过HTTPS进行。 （请参阅下表）。 因此，

* 如果您有一个HTTPS网站，其中包含HTTPS视频流，则流播放可以。
* 如果您有一个HTTP网站，其中带有HTTPS视频流，则流播放是正常的，并且Web浏览器中不存在混合内容问题。

HLS是Apple的自适应视频流播放标准，可根据网络带宽容量自动调整播放。 它还允许客户“搜索”到视频中的任意点，无需等待视频的其余部分下载。

渐进式视频是通过在用户的桌面系统或移动设备上本地下载和存储视频来交付的。

下表介绍了使用Scene7视频查看器在台式计算机和移动设备上播放视频的设备、浏览器和方法。

<table>
 <tbody>
  <tr>
   <td><strong>设备</strong></td>
   <td><strong>浏览器</strong></td>
   <td><strong>视频播放模式</strong></td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Internet Explorer 9和10</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows 8和Windows 10上——每当请求HLS时强制使用HTTPS。 已知限制：HLS上的HTTP在浏览器／操作系统组合中不工作<br /> 。在Windows 7上 <br /> -渐进式下载。 使用标准逻辑选择HTTP与HTTPS协议。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Firefox 23-44</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Firefox 45或更高版本</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Chrome</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Safari(Mac)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome（Android 6或更早版本）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome（Android 7或更高版本）</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android（默认浏览器）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari(iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(iOS)</td>
   <td>HLS</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>黑莓</td>
   <td>HLS</td>
  </tr>
 </tbody>
</table>

## Architecture of Dynamic Media video solution {#architecture-of-dynamic-media-video-solution}

下图显示了通过DMGateway（在Dynamic Media Hybrid模式下）上传和编码并供公众使用的视频的整体创作工作流程。

![chlimage_1-427](assets/chlimage_1-427.png)

## 用于视频的混合出版架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 视频编码的最佳实践 {#best-practices-for-encoding-videos}

如果 **您已启用Dynamic Media并设置了视频云服务，Dynamic Media Encode Video** 工作流会对视频进行编码。 此工作流捕获工作流进程历史和失败信息。 请参 [阅监视视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。 如果您已启用Dynamic Media并设置了视频云服务，则在您上传视频时， **** Dynamic Media编码视频工作流将自动生效。 (如果您未使用Dynamic Media，则“ **[!UICONTROL DAM更新资产”工作流将生效]** 。)

以下是关于源视频文件编码的最佳实践提示。

有关视频编码的建议，请参阅以下资源：

* [流101:基础知识— 编解码器、带宽、数据速率和分辨率](https://www.adobe.com/go/learn_s7_streaming101_en)。
* [视频编码基础](https://www.adobe.com/go/learn_s7_encoding_en)。

### 源视频文件 {#source-video-files}

在对视频文件进行编码时，请尽可能使用最高质量的源视频文件。避免使用先前已编码的视频文件，因为这样的文件已经压缩，进一步编码会导致创建的视频质量不佳。

下表说明了在编码之前，源视频文件应具有的建议大小、宽高比和最低比特率。

| 大小 | 宽高比 | 最低比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps，适用于大部分视频。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的动作数量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的动作数量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

获取文件元数据的方法如下：通过使用视频编辑工具查看文件的元数据，或者使用专门为获取元数据而设计的应用程序。下面说明了如何使用第三方应用程序 MediaInfo 获取视频文件的元数据：

1. Go to this web page: [https://mediainfo.sourceforge.net/en/Download](https://mediainfo.sourceforge.net/en/Download).
1. 选择并下载 GUI 版本的安装程序，然后按照安装说明进行操作。
1. 完成安装后，右键单击视频文件（仅限 Windows）并选择 MediaInfo，或打开 MediaInfo 并将视频文件拖到该应用程序中。您会看到与该视频文件相关的所有元数据，包括其宽度、高度和每秒帧数。

### 宽高比 {#aspect-ratio}

在为主视频文件选择或创建视频编码预设时，请确保预设的宽高比与主视频文件的宽高比相同。宽高比是视频的宽度与高度的比率。

要确定视频文件的宽高比，请获取该文件的元数据并记下该文件的宽度和高度（请参阅上面的“获取文件的元数据”）。 然后，使用此公式确定宽高比：

宽度/高度 = 宽高比

下表说明了公式结果如何转换成常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，如果一个视频的宽度为 1440，高度为 1080，则其宽高比为 1440/1080，也就是 1.33。在这种情况下，要对该视频文件进行编码，您需要选择宽高比为 4:3 的视频编码预设。

### 比特率 {#bitrate}

比特率是编码成一秒钟视频回放的数据量。 比特率以千比特／秒(Kbps)为单位。

>[!NOTE]
>
>由于所有编解码器都使用有损压缩，因此比特率是视频质量中最重要的因素。 使用有损压缩时，对视频文件的压缩程度越大，质量就降低得越多。因此，所有其他特性（分辨率、帧速率和编解码器）相同，比特率越低，压缩文件的质量越低。

在选择比特率编码时，您可以选择两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR)-在CBR编码过程中，每秒的比特率或位数在整个编码过程中保持不变。 CBR编码将设置的数据速率保留到整个视频中的设置。 此外，CBR编码不会为质量优化媒体文件，但会节省存储空间。
如果视频在整个视频中包含类似的运动级别，则使用CBR。 CBR最常用于流式视频内容。 另请参 [阅使用自定义添加的视频编码参数](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters)。

* **[!UICONTROL 可变比特率编码]** (VBR)- VBR编码根据压缩程序所需的数据，将数据速率调低并调整到您设置的上限。 这意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态地增加或减少。
VBR编码时间较长，但生成的结果最为有利；媒体文件的质量优越。 VBR最常用于视频内容的HTTP渐进式交付。

何时应使用VBR与CRB?
在选择VBR与CBR时，几乎总是建议将VBR用于媒体文件。 VBR以竞争比特率提供更高质量的文件。 使用VBR时，请务必使用两遍编码，并将最大比特率设置为目标视频比特率的1.5倍。

在选择视频编码预设时，请考虑目标最终用户的连接速度。所选预设的数据率应该是目标最终用户连接速度的 80%。例如，如果目标最终用户的连接速度是 1000 Kbps，则最佳预设就是视频数据率为 800 Kbps 的预设。

下表说明了典型连接速度的数据率。

| 速度 (Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型移动连接。对于此类连接，3G 体验的目标数据率范围为 400 至最高 800。 |
| 2000 | 典型宽带桌面连接。对于此连接，目标数据率范围为800-2000 Kbps，大多数目标数据率平均为1200-1500 Kbps。 |
| 5000 | 典型高宽带连接。不建议在此较高范围下进行编码，因为大多数用户并不具备此速度的视频传送条件。 |

### 分辨率 {#resolution}

**分辨率**以像素为单位描述视频文件的高度和宽度。大多数源视频以高分辨率存储（例如，1920 x 1080）。 为了实现流播放，源视频压缩为更小的分辨率（640 x 480或更小）。

分辨率和数据率是两个相互关联、密不可分的因素，它们决定着视频质量。为保持同等的视频质量，视频文件的像素数越高（分辨率越高），数据率就必须越高。例如，考虑分辨率分别为 320 x 240 和 640 x 480 的视频文件的每帧像素数：

| 分辨率 | 每帧像素数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

对于分辨率为 640 x 480 的文件，其每帧像素数高出四倍。为使这两个示例分辨率的文件实现同等的数据率，您需要对分辨率为 640 x 480 的文件应用四倍的压缩，而这会降低视频的质量。因此，如果视频数据率为 250 Kbps，则在 320 x 240 分辨率下观看时质量会很高，但在 640 x 480 分辨率下观看时质量则不高。

总的来说，您使用的数据率越高，视频的画质就越好；您使用的分辨率越高，您保持画质所需的数据率就越高（与较低分辨率相比）。

由于分辨率与数据率相关联，在对视频进行编码时，有两种选择：

* 选择一个数据率，然后使用在选定数据率下看起来效果不错的最高分辨率进行编码。
* 选择一个分辨率，然后使用在选定分辨率下获得高质量视频所需的数据率进行编码。

在为主视频文件选择（或创建）视频编码预设时，请使用此表来确定正确的分辨率：

| 分辨率 | 高度（像素） | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 微型屏幕 |
| 300p | 300 | 通常用于移动设备的小型屏幕 |
| 360p | 360 | 小型屏幕 |
| 480p | 480 | 中型屏幕 |
| 720p | 720 | 大型屏幕 |
| 1080p | 1080 | 高清晰度大型屏幕 |

### Fps (Frames per second) {#fps-frames-per-second}

在美国和日本，大多数视频以 29.97 帧/秒 (fps) 的速率拍摄；在欧洲，大多数视频以 25 fps 的速率拍摄。电影是以 24 fps 的速率拍摄。

选择的视频编码预设应与主视频文件的 fps 速率相匹配。例如，如果您的主视频采用 25 fps，则应选择 25 fps 的编码预设。默认情况下，所有自定义编码均采用主视频文件的 fps。鉴于这一原因，您在创建视频编码预设时不需要明确指定 fps 设置。

### 视频编码尺寸 {#video-encoding-dimensions}

为实现最佳效果，请选择相应编码尺寸，使源视频成为所有编码视频的整数倍数。

要计算此比率，请用源宽度除以编码宽度，得出宽度比。然后，用源高度除以编码高度，得出高度比。

如果计算得出的比率是整数，就意味着视频已得到最佳缩放。如果计算得出的比率不是整数，则会影响视频质量，使显示屏上出现残留像素伪影。当视频含有文本时，这种影响最为明显。

例如，假定源视频的分辨率为 1920 x 1080。在下表中，这三个编码视频提供了可使用的最佳编码设置。

| 视频类型 | 宽度 x 高度 | 宽度比 | 高度比 |
|--- |--- |--- |--- |
| 源 | 1920 x 1080 | 1 | 1 |
| 编码 | 960 x 540 | 2 | 2 |
| 编码 | 640 x 360 | 3 | 3 |
| 编码 | 480 x 270 | 4 | 4 |

### 编码视频文件格式 {#encoded-video-file-format}

Dynamic Media 建议使用 MP4 H.264 视频编码预设。由于 MP4 文件使用 H.264 视频编解码器，因此 MP4 可以提供高质量的视频，但需要压缩文件大小。

## 将视频发布到 YouTube {#publishing-videos-to-youtube}

您可以将内部部署AEM视频资产直接发布到您之前创建的YouTube频道。

要将视频资产发布到YouTube，请设置AEM资产及标记。 您将这些标记与YouTube频道关联。 如果视频资产的标记与YouTube频道的标记匹配，则视频将发布到YouTube。 只要使用关联的标记，发布到YouTube就会与视频的正常发布一起发生。

YouTube自行编码。 因此，上传到AEM的原始视频文件将发布到YouTube，而不是Dynamic media编码创建的任何视频再现。 虽然不需要使用Dynamic media处理视频，但在回放时需要查看器预设时，应该会这样做。

当您绕过视频处理配置文件并直接发布到YouTube时，这仅仅意味着您的AEM资产中的视频资产可能无法获得可查看的缩略图。 这也意味着，如果您以动态媒体或dynamicmedia_scene7运行模式运行，则未编码的视频将不能与任何Dynamic media资产类型一起使用。

将视频资产发布到YouTube服务器需要完成以下任务，以确保使用YouTube进行安全的服务器到服务器身份验证：

1. [配置Google cloud设置](#configuring-google-cloud-settings)
1. [创建YouTube频道](#creating-a-youtube-channel)
1. [添加发布标记](#adding-tags-for-publishing)
1. [启用YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent)
1. [在AEM中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动设置已上传视频的默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [将视频发布到您的 YouTube 频道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证已发布到 YouTube 上的视频](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [将 YouTube URL 关联到您的 Web 应用程序](#linking-youtube-urls-to-your-web-application)

您还可以[取消发布视频以将其从 YouTube 中删除](#unpublishing-videos-to-remove-them-from-youtube)。

### 配置Google cloud设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要一个Google帐户。 如果你有GMAIL账户，那么你已经有了Google账户；如果您没有Google帐户，您可以轻松创建一个。 您需要此帐户，因为您需要凭据才能将视频资产发布到YouTube。 如果您已经创建了帐户，请跳过此任务并直接继续 [创建YouTube频道](#creating-a-youtube-channel)。

与Google cloud一起使用的帐户和用于YouTube的Google帐户不必相同。

请注意，Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与下面介绍的步骤稍有不同。 当您尝试检查视频是否上传到YouTube时，此警告也适用于YouTube。

>[!NOTE]
>
>编写本文时，以下步骤是准确的。 但是，Google会定期更新其网站，恕不另行通知。 因此，这些步骤可能略有不同。

要配置Google cloud设置，请执行以下操作：

1. 创建新Google帐户。
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   如果您已经有Google帐户，请跳到下一步。

1. 请访问 [https://cloud.google.com/](https://cloud.google.com/)。
1. 在Google cloud页面的右上角附近，单击控制 **[!UICONTROL 台]**。

   如有必要，您可能需要使 **[!UICONTROL 用Google帐户凭据登录]** ，才能查看 **[!UICONTROL 控制台选项]** 。

1. 在控制面板页面的 **[!UICONTROL Google Cloud Platform右侧]**，单击项目下拉列表以打开选择项目对话框。
1. 在“选择项目”对话框中，点按“ **[!UICONTROL 新建项目”]**。

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. 在“新建项目”对话框的“项目名称”字段中，键入新项目的名称。

   请注意，您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；创建后无法更改。 此外，您稍后在AEM中设置YouTube时，还需要再次输入相同的项目ID;你可能想写下来。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 执行以下操作之一：

   * 在项目的控制面板中，点按入门卡，浏 **[!UICONTROL 览并启用API]**。
   * 在项目的控制面板上的API卡中，点按转 **[!UICONTROL 到API概述]**。
   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. 在“API和服务”页面顶部附近，点按“启 **[!UICONTROL 用API和服务”]**。
1. 在“API库”页面的左侧的“类别” **[!UICONTROL 下]**，点 **[!UICONTROL 按YouTube]**。 在页面的右侧，点按 **[!UICONTROL YouTube数据API]**。
1. 在YouTube数据API v3页面上，点按启 **[!UICONTROL 用]**。

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. 要使用API，您可能需要凭据。 如有必要，请单击“ **[!UICONTROL 创建凭据]**”。

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 在“向 **[!UICONTROL 项目添加凭据”页]** ，第1步，执行以下操作：

   * 从您 **[!UICONTROL 使用的API中？]** 下拉列表中，选择 **[!UICONTROL YouTube Data API v3]**。

   * 从 **[!UICONTROL Where will calling the API from?]** 下拉列表，选 **[!UICONTROL 择Web服务器（例如node.js、Tomcat）]**

   * 您将访 **[!UICONTROL 问哪些数据？]** 下拉列表中，点按用 **[!UICONTROL 户数据]**。
   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 点按 **[!UICONTROL 我需要哪些凭据？]**
1. 在“将 **[!UICONTROL 凭据添加到项目]** ”页面的“创建OAuth 2.0客户端ID **** ”标题下，根据需要在“名称”字段中输入唯一的名称。 或者，您也可以使用Google指定的默认名称。
1. 在“已授 **[!UICONTROL 权的Javascript源]** ”标题的文本字段中，输入以下路径，用路径中您自己的域和端口号替换，然后按 **[!UICONTROL Enter]** 以添加列表路径：

   `https://<servername.domain>:<port_number>`

   For example, `https://1a2b3c.mycompany.com:4321`

   **注意**:以上路径示例仅用于说明目的。

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 在“已 **[!UICONTROL 授权的重定向URI]** ”标题的文本字段中，输入以下路径，用路径中您自己的域和端口号替换，然后按 **[!UICONTROL Enter]** 以添加列表路径：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   For example, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **注意**:以上路径示例仅用于说明目的。

1. 单击 **[!UICONTROL 创建OAuth客户端ID]**。
1. 在“向项 **[!UICONTROL 目添加凭据]****** ”页面的步骤3中，在“设置OAuth 2.0同意”屏幕标题下，选择您当前使用的Gmail电子邮件地址。

   ![6_5_googleaccount-apis-createcredentials-acconverscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 在显示 **[!UICONTROL 给用户的产品名称标题下]** ，在文本字段中，输入您希望在同意屏幕上显示的内容。

   AEM管理员在YouTube上进行身份验证时，会向其显示同意屏幕；AEM将与YouTube联系以获取许可。

1. 单击“ **[!UICONTROL 继续]**”。
1. 在将凭据添加到项目页面的步骤4中，在“下载凭据 **[!UICONTROL ”标题下]** ，点按 **[!UICONTROL 下载]**。

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 保存文 `client_id.json` 件。

   当您稍后在Adobe Experience manager中设置YouTube时，您将需要此下载的json文件。

1. 单击&#x200B;**[!UICONTROL 完成]**。

   从Google帐户中注销。 您现在将创建一个YouTube频道。

### 创建YouTube频道 {#creating-a-youtube-channel}

将视频发布到YouTube需要您有一个或多个频道。 如果已经创建YouTube频道，则可以跳过此任务，转到添 [加要发布的标记](/help/assets/video.md#adding-tags-for-publishing)。

>[!CAUTION]
>
>在AEM的“YouTube设置”下添加频道之前 *，请确保已在YouTube中设置一个或多个频道(请参阅下* 面的“在AEM中设置YouTube [](#setting-up-youtube-in-aem) ”)。 如果您未能这样做，则不会向您发送任何现有渠道的警告。 但是，添加渠道时仍会进行Google身份验证，但无法选择发送视频的渠道。

要创建YouTube频道，请执行以下操作：

1. 转到https://www.youtube.com [](https://www.youtube.com/) ，然后使用Google帐户凭据登录。
1. 在YouTube页面的右上角，单击您的个人资料图片（也可能以纯色圆形的字母显示），然后单击 **[!UICONTROL YouTube设置]** （圆齿轮图标）。
1. 在“概述”页面的“其他功能”标题下，单击“查 **[!UICONTROL 看我的所有渠道”或创建新渠道]**。
1. 在渠道页面上，单击 **[!UICONTROL 创建新渠道]**。
1. 在品牌帐户页面的品牌帐户名称字段中，输入您选择要发布视频资产的位置的业务名称或任何其他渠道名称，然后单击创 **[!UICONTROL 建]**。

   记住在此处输入的名称，因为在AEM中设置YouTube时，您需要再次输入该名称。

1. （可选）如果需要，请添加更多渠道。

   现在，您将添加用于发布的标记。

### 添加发布标记 {#adding-tags-for-publishing}

要将视频发布到YouTube,AEM会将标记关联到一个或多个YouTube频道。 要添加用于发布的标记，请参阅 [管理标记](/help/sites-administering/tags.md)。

或者，如果您打算在AEM中使用默认标记，则可以跳过此任务，转到启用 [YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent)。

### 启用YouTube发布复制代理 {#enabling-the-youtube-publish-replication-agent}

在启用YouTube发布复制代理后，如果要测试与Google cloud帐户的连接，请点按测 **[!UICONTROL 试连接]**。 浏览器选项卡显示连接结果。 如果已添加YouTube频道，则这些频道的列表将作为测试的一部分显示。

1. 在AEM的左上角，单击AEM徽标，然后在左边栏中，单击 **[!UICONTROL 工具]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **** Agents on AuthorDeployment。
1. 在“作者代理”页面上，单击“ **[!UICONTROL YouTube发布(youTube)”]**。
1. 在工具栏的“设置”右侧，单击“编 **[!UICONTROL 辑”]**。
1. 选中“ **[!UICONTROL 启用]** ”复选框以打开复制代理。
1. 单击&#x200B;**[!UICONTROL 确定]**。

   现在，您将在AEM中设置YouTube。

### Setting up YouTube in AEM {#setting-up-youtube-in-aem}

从AEM 6.4开始，引入了一种新的触控用户界面方法来在AEM中设置YouTube发布。 根据您所使用的AEM安装实例，执行下列操作之一：

* 要在6.4之前的AEM中配置YouTube，请参阅 [在6.4之前的AEM中设置YouTube](/help/assets/video.md#setting-up-youtube-in-aem-before)。
* 要在AEM 6.4或更高版本中配置YouTube，请参 [阅在AEM 6.4和更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later)。

#### 在AEM 6.4和更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 请确保以管理员身份登录到Dynamic Media实例。
1. 在AEM的左上角，点按AEM徽标，然后在左边栏中，点按工具 ****（锤子图标）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube发布配置]**。
1. 点 **[!UICONTROL 按全局]** （请勿选择它）。

1. Near the upper-right corner of the global page, tap **[!UICONTROL Create]**.
1. 在“创建YouTube配置”页面的“Google Cloud Platform Settings”下的“应用程 **[!UICONTROL 序名称]** ”字段中，输入Google项目ID。

   您在之前首次配置Google cloud设置时指定了项目ID。
保持“创建YouTube配置”页面处于打开状态；你稍后会回来。

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在配置Google cloud设置任务中下载并保存 [的JSON文件](/help/assets/video.md#configuring-google-cloud-settings)。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube帐户设置”对话框。 在“ **[!UICONTROL JSON配置”字段]** ，粘贴JSON文本。
1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**。

   您现在将在AEM中设置YouTube频道。

1. 点按 **[!UICONTROL 添加渠道]**。
1. 在“频道名称”字段中，输入您在以前向YouTube添加一个或多个 **[!UICONTROL 频道任务中创建的频道名称]** 。

   如果需要，您可以选择添加说明。

1. 点按 **[!UICONTROL 添加]**。
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google cloud帐户，请跳过此步骤。

   * 输入与上述Google项目ID和JSON文本关联的Google用户名和密码。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 请勿选择电子邮件地址；它不是渠道。
   * 在下一页，点按接 **[!UICONTROL 受]** ，以允许访问此渠道。

1. 点按 **[!UICONTROL 允许]**。

   您现在将设置用于发布的标记。

1. **[!UICONTROL 设置要发布的标记]** -在“云服务”>“YouTube”页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（倒转尖角）可显示AEM中可用标记的列表。
1. 点按一个或多个标记以添加它们。

   To delete a tag you have added, select the tag, and tap **[!UICONTROL X]**.

1. 添加完所需的标记后，点按保 **[!UICONTROL 存]**。

   现在，您可以将视频发布到YouTube频道。

#### 在AEM 6.4之前设置YouTube {#setting-up-youtube-in-aem-before}

1. 请确保以管理员身份登录到Dynamic Media实例。

1. 在AEM的左上角，点按AEM徽标，然后在左边栏中，点按工具 **** （锤子图标）> **[!UICONTROL Deployment]** > **[!UICONTROL Cloud Services]**。
1. 在“第三方服务”标题下的YouTube下，点按“立即 **[!UICONTROL 配置”]**。
1. 在“创建配置”对话框中，在相应的字段中输入标题（必填）和名称（可选）。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube帐户设置”对话框的“应用程 **[!UICONTROL 序名称]** ”字段中，输入Google项目ID。

   您在最初配置Google Cloud设置时 [指定了项目ID](/help/assets/video.md#configuring-google-cloud-settings) 。
使“YouTube帐户设置”对话框保持打开状态；你稍后会回来。

1. 使用纯文本编辑器，打开您之前在配置Google cloud设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube帐户设置”对话框。 在“ **[!UICONTROL JSON配置”字段]** ，粘贴JSON文本。
1. 点按 **[!UICONTROL 确定]**。

   您现在将在AEM中设置YouTube频道。

1. 在可用渠道 **[!UICONTROL 右侧]**，点 **按+** （加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如果需要，您可以选择添加说明。

1. 点按 **[!UICONTROL 确定]**。
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google cloud帐户，请跳过此步骤。

   * 输入与上述Google项目ID和JSON文本关联的Google用户名和密码。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择渠道。 请勿选择电子邮件地址；它不是渠道。
   * 在下一页，点按接 **[!UICONTROL 受]** ，以允许访问此渠道。

1. 点按 **[!UICONTROL 允许]**。

   您现在将设置用于发布的标记。

1. **[!UICONTROL 设置要发布的标记]** -在“云服务”>“YouTube”页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（倒转尖角）可显示AEM中可用标记的列表。
1. 点按一个或多个标记以添加它们。

   To delete a tag you have added, select the tag, and tap **X**.

1. 添加完所需的标记后，点按确 **[!UICONTROL 定]**。

   现在，您可以将视频发布到YouTube频道。

### （可选）自动设置已上传视频的默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择在上传视频时自动设置YouTube属性。 您可以通过在AEM中创建元数据处理配置文件来完成此操作。

要创建元数据处理配置文件，您首先需要从“字段标签 **[!UICONTROL ”、“映射到属性”和“选择”字段复制值]********** ，所有这些字段均位于视频的元数据架构中。 然后，您将通过向YouTube添加这些值来构建您的视频元数据处理配置文件。

要自动设置已上传视频的默认YouTube属性，请执行以下操作：

1. 在AEM的左上角，单击AEM徽标，然后在左边栏中，单击工具 **** （锤子图标）>资产 **[!UICONTROL >元数]** 据架构 ****。
1. 单击 **[!UICONTROL 默认]**。 （请勿在“default”左侧的选择框中添加复选标记。）
1. 在默 **[!UICONTROL 认页面]** ，选中视频左侧的框 ****，然后单击 **编辑]**。
1. 在“元数据架构编辑器”页面上，单击“高 **[!UICONTROL 级]** ”选项卡。
1. 在“YouTube发布”标题下，单击“ **[!UICONTROL YouTube类别”]**。
1. 在页面右侧的“设置”选项卡 **[!UICONTROL 下]** ，执行以下操作：

   * 在“映 **[!UICONTROL 射到属性”文本字段中]** ，选择并复制值。
将复制的值粘贴到开放文本编辑器中。 您以后将在创建元数据处理配置文件时需要此值。 使文本编辑器保持打开状态。

   * 在“ **[!UICONTROL 选择]**”下，选择并复制您要使用的默认值（如“人物和博客”或“科学与技术”）。
将复制的值粘贴到开放文本编辑器中。 您以后将在创建元数据处理配置文件时需要此值。 使文本编辑器保持打开状态。

1. 在“YouTube发布”标题下，单击“ **[!UICONTROL YouTube隐私”]**。
1. 在页面右侧的“设置”选项卡 **[!UICONTROL 下]** ，执行以下操作：

   * 在“映 **[!UICONTROL 射到属性”文本字段中]** ，选择并复制值。
将复制的值粘贴到开放文本编辑器中。 您以后将在创建元数据处理配置文件时需要此值。 使文本编辑器保持打开状态。

   * 在“ **[!UICONTROL 选择]**”下，选择并复制您要使用的默认值。 请注意，“选择”分为两对。 对中的底部字段是要复制的默认值，如公共、未列出或私有。
将复制的值粘贴到开放文本编辑器中。 您以后将在创建元数据处理配置文件时需要此值。 使文本编辑器保持打开状态。

1. 在“元数据架构编辑器”页面的右上角附近，单击“取 **[!UICONTROL 消”]**。
1. 在AEM的左上角，点按AEM徽标，然后在左边栏中，单击工具 **** （锤子图标）>资产 **[!UICONTROL >元数]** 据配置文件 ****。

1. 在元数据配置文件页面的右上角附近，单击创 **[!UICONTROL 建]**。
1. 在“添加元数据配置文件”对话框的“配置文 **[!UICONTROL 件标题]** ”文本字段中，输入名称， `YouTube Video` 然后单击“ **[!UICONTROL 创建]**”。
1. 在“元数据配置文件编辑器”页面上，单击“高 **[!UICONTROL 级]** ”选项卡。
1. 通过执行以下操作，将复制的YouTube发布值添加到配置文件：

   * 在页面的右侧，单击“构建表 **[!UICONTROL 单”选项卡]** 。
   * （可选）将标有“章节标题” **[!UICONTROL 的组件拖至左侧]** ，然后将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** ，以选择组件。
   * （可选）在页面右侧的“设置”选项卡下，在“字段标签”文本字段中输入 `YouTube Publishing`。
   * 单击“构 **[!UICONTROL 建表单]** ”选项卡，然后拖动标有“多值文本”的组件 **[!UICONTROL ，将其放在刚刚创建的]****** YouTube发布标题下。

   * 单 **击[!UICONTROL字段标签** ]以选择组件。
   * 在页面右侧的“设置”选项卡下，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上的各自字段中。 将选择值粘贴到默认值字段中。

1. 通过执行以下操作，将复制的YouTube隐私权值添加到配置文件：

   * 在页面的右侧，单击“构建表 **[!UICONTROL 单”选项卡]** 。
   * （可选）将标有“章节标题” **[!UICONTROL 的组件拖至左侧]** ，然后将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** ，以选择组件。
   * （可选）在页面右侧的“设置”选项卡下，在“字段标签”文本字段中输入 `YouTube Privacy`。
   * 单击“构 **[!UICONTROL 建表单]** ”选项卡，然后拖动标有“多值文本”的组件 **[!UICONTROL ，将其放在您刚刚创建的]****** YouTube隐私标题下。

   * 单击 **[!UICONTROL 字段标签]** ，以选择组件。
   * 在页面右侧的“设置”选项卡下，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上的各自字段中。 将选择值粘贴到默认值字段中。

1. Near the upper-right corner of the page, click **[!UICONTROL Save]**.
1. 将YouTube发布元数据配置文件应用到您要上传视频的文件夹。 您需要同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-profiles.md) 和视 [频配置文件](/help/assets/video-profiles.md)。

### 将视频发布到您的 YouTube 频道 {#publishing-videos-to-your-youtube-channel}

现在，您可以关联之前添加到视频资产的标记。 此过程可让AEM了解要发布到您的YouTube频道的资产。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下运行时，请注意，立即发布不会自动发布到YouTube。 设置Dynamic Media - Scene7模式时，有两个发布选项可供选择：立即 **[!UICONTROL 或]** 激活后 ****。
>
>**[!UICONTROL “立即发布]** ”表示上传的资产在与IPS同步后会自动发布到交付系统。 虽然Dynamic Media是如此，但YouTube则并非如此。 要发布到YouTube，您必须通过AEM作者进行发布。

>[!NOTE]
>
>要从YouTube发布内容，AEM使用“发布到 **[!UICONTROL YouTube]** ”工作流，该工作流允许您监视进度并查看任何失败信息。
>
>请参 [阅监视视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。
>
>有关更详细的进度信息，您可以监视复制下的YouTube日志。 但是，请注意，此类监视需要管理员访问权限。

要将视频发布到您的 YouTube 频道，请执行以下操作：

1. 在AEM中，导航到要发布到YouTube频道的视频资产。
1. 选择视频资产（自适应视频集）。
1. 在工具栏中，单击“ **[!UICONTROL 属性”]**。
1. 在“基本”选项卡的“元数据”标题下，单 **[!UICONTROL 击“标记”字段右侧的]** “打开选择对话框”。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，这些标记必须与YouTube频道相关联。

1. In the upper-right corner of the page, click **[!UICONTROL Select]**.
1. 在视频的属性页面的右上角，单击“保存并 **[!UICONTROL 关闭”]**。
1. 在工具栏中，单击“快 **[!UICONTROL 速发布”]**。

   另请参 [阅将出版物管理与AEM Sites结合使用](https://helpx.adobe.com/experience-manager/kt/sites/using/publication-management-feature-video-use.html)。

   您可以选择验证已发布到YouTube频道上的视频。

### （可选）验证已发布到 YouTube 上的视频{#optional-verifying-the-published-video-on-youtube}

您可以选择监视YouTube发布（或取消发布）的进度。

请参 [阅监视视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。

发布视频所需的时间可能会因诸多因素而有很大不同，这些因素包括主视频的格式、文件大小和上传流量。发布过程所需的时间少则几分钟，多则几小时，这些情况都有可能出现。另请注意，分辨率较高的格式渲染起来会慢很多。例如，分辨率分别为 720p 和 1080p 的视频在渲染时所需的时间会比 480p 的视频显著更长。

如果在八小时后，状态消息仍然显示&#x200B;**[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从我们的站点中删除视频，然后重新上传。

### 将 YouTube URL 关联到您的 Web 应用程序 {#linking-youtube-urls-to-your-web-application}

您可以在发布视频后获取Dynamic media生成的YouTube URL字符串。 在复制该 YouTube URL 时，它会进入“剪贴板”，以便您能够视需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>只有在将视频资产发布到 YouTube 后，才可复制其 YouTube URL。

要将 YouTube URL 关联到您的 Web 应用程序，请执行以下操作：

1. 导航到要复 *制其URL的YouTube已发布视频资产* ，然后选择它。

   Remember that YouTube URLs are only available to copy *after* you have first *published* the video assets to YouTube.

1. 在工具栏中，单击“ **[!UICONTROL 属性”]**。
1. Click the **[!UICONTROL Advanced]** tab.
1. 在“YouTube发布”标题下的“YouTube URL列表”中，选择URL文本并将其复制到您的Web浏览器，以预览资产或添加到您的Web内容页面。

### 取消发布视频以将其从 YouTube 中删除 {#unpublishing-videos-to-remove-them-from-youtube}

在AEM中取消发布视频资产时，该视频将从YouTube中删除。

>[!CAUTION]
>
>如果您直接从YouTube中删除视频，AEM不会察觉并继续像视频仍发布到YouTube一样运行。 始终通过AEM从YouTube取消发布视频资产。

>[!NOTE]
>
>要从YouTube中删除内容，AEM将使用“从YouTube中取消发 **[!UICONTROL 布”工作流]** ，该工作流允许您监视进度并查看任何失败信息。
>
>请参 [阅监视视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress)。

要取消发布视频以将其从 YouTube 中删除，请执行以下操作：

1. 导航到要从YouTube频道取消发布的视频资产。
1. 在资产选择模式下，选择一个或多个已发布的视频资产。
1. 在工具栏中，单击“管 **[!UICONTROL 理发布”]**。 您可能需要点按三个圆点图标(...)在工具栏中，查看 **[!UICONTROL 管理发布]**。
1. 在“管理发布”页面上，点按取 **[!UICONTROL 消发布]**。
1. In the upper-right corner of the page, tap **[!UICONTROL Next]**.
1. In the upper-right corner of the page, tap **[!UICONTROL Unpublish]**.

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

当您将新视频上传到应用了视频编码的文件夹或将视频发布到Youtube时，您可以通过多种方式监控视频编码/Youtube发布的进展（或失败）。 实际的YouTube发布进度仅通过日志提供，但是失败还是成功会按以下过程描述的其他方式列出。 此外，当YouTube发布工作流或视频编码完成或中断时，您可能会收到电子邮件通知。

### 监控进度 {#monitoring-progress}

要监视进度（包括编码/YouTube发布失败），请执行以下操作：

1. 在资产文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资产上。 如果出现错误，则此信息也会显示在资产上。
   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在“处 **[!UICONTROL 理状态]** ”列中。 如果出错，则同一列中显示此消息。
   ![chlimage_1-430](assets/chlimage_1-430.png)

   默认情况下，此列不显示。 要启用该列，请从视图下 **[!UICONTROL 拉菜单中选择查看设置]** ，然后添加处理状态列，然后点按或单击更 **[!UICONTROL 新]******。

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 查看资产详细信息的进度。 点按或单击资产时，请打开下拉菜单，然后选择时 **[!UICONTROL 间轴]**。 要将其缩小为编码或YouTube发布等工作流活动，请选择“工作 **[!UICONTROL 流”]**。

   ![chlimage_1-432](assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包括YouTube频道的名称和YouTube视频URL。 此外，发布完成后，您还会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   >
   >由于重试时的多个工作流配置、重试延迟 **[!UICONTROL ，以及来自https://localhost:4502/system/console/configMgr的超时(例如]**********[](https://localhost:4502/system/console/configMgr):
   >
   >    * Apache Sling作业队列配置
   >    * Adobe Granite Workflow External Process Job Handler
   >    * Granite工作流超时队列
   >
   >在这些配置中 **[!UICONTROL ，您可以调]**&#x200B;整重试 **[!UICONTROL 、]**&#x200B;重试延迟 **[!UICONTROL ,]** 以及超时。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   >您可能需要管理权限才能访问“工 **[!UICONTROL 具]** ”菜单。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   选择该实例，然后点按或单击“打 **[!UICONTROL 开历史记录”]**。

   ![chlimage_1-434](assets/chlimage_1-434.png)

   在“工作流实例”区域中，您还可以暂停、终止或重命名工作流。 有关更 [多信息，请参阅](/help/sites-administering/workflows-administering.md) “管理工作流”。

1. 有关失败的作业，请参阅工具>工作流 **[!UICONTROL >失败]****[!UICONTROL >]** 失败 ****。 “工作 **[!UICONTROL 流失败]** ”(Workflow Failure)列出所有失败的工作流活动。

   >[!NOTE]
   >
   >您可能需要管理权限才能访问“工 **[!UICONTROL 具]** ”菜单。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由于重试时的多个工作流配置、重试延迟 ************[](https://localhost:4502/system/console/configMgr)，以及来自https://localhost:4502/system/console/configMgr的超时(例如：
   >
   >
   >
   >    * Apache Sling作业队列配置
   >    * Adobe Granite Workflow External Process Job Handler
   >    * Granite工作流超时队列
   >
   >
   >在这些配置中 **[!UICONTROL ，您可以调]**&#x200B;整重试 **[!UICONTROL 、]**&#x200B;重试延迟 **[!UICONTROL ,]** 以及超时。

1. 有关已完成的工作流，请参阅工具>工作流 **[!UICONTROL >存档]** >存 **[!UICONTROL 档中的]** 工作流 **[!UICONTROL 存档]**。 “工作 **[!UICONTROL 流存档]** ”列出所有已完成的工作流活动。

   >[!NOTE]
   >
   >您可能需要管理权限才能访问“工 **[!UICONTROL 具]** ”菜单。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 您可能会收到有关中止或失败的工作流作业的电子邮件通知。 管理员可以配置这些电子邮件通知。 See [Configuring email notifications](#configuring-e-mail-notifications).

#### 配置电子邮件通知 {#configuring-e-mail-notifications}

>[!NOTE]
>
>您可能需要管理权限才能访问“工 **[!UICONTROL 具]** ”菜单。

如何配置通知取决于您是希望接收编码作业通知还是YouTube发布作业通知：

* 对于编码作业，您可以访问所有AEM工作流电子邮件通知的配置页 **[!UICONTROL 面(位于]** “工具”>“操作” **[!UICONTROL >“]** Web控制台” **[!UICONTROL )，并通过搜索]****** Day CQ Workflow Email Notification Service Designment来访问Ady CQ Workflow Email Notification Service。 请参阅 [在AEM中配置电子邮件通知](/help/sites-administering/notification.md)。 您可以相应地选中或清除“中止时通 **[!UICONTROL 知”或“完成时通]** 知”复选框 **** 。

* 对于YouTube发布作业，请执行以下操作：

1. 在AEM中，点按工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流]** > **[!UICONTROL 模型]**。
1. 在“工作流模型”页面上，选择 **[!UICONTROL 发布到YouTube]**，然后点按工 **[!UICONTROL 具栏上的编]** 辑。
1. 在“发布到YouTube”工作流页面的右上角附近，点按编 **[!UICONTROL 辑]**。
1. 将鼠标指针悬停在“YouTube上传”组件上，然后点按一次以显示内联工具栏。

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 在内联工具栏中，点按配置图标（扳手）。 Click the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutube工作流——配置图标](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. 在“YouTube上传过程——步骤属性”对话框中，点按“参 **[!UICONTROL 数]** ”选项卡。

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 您可以选中或清除以下复选框：

   * 发布开始
   * 发布失败
   * 发布完成——包括有关渠道和URL的信息
   清除复选框意味着您不会从YouTube发布工作流收到指定的电子邮件通知。

   >[!NOTE]
   >
   >这些电子邮件特定于YouTube，是通用工作流电子邮件通知的补充。 因此，您可能会收到两组电子邮件通知- **[!UICONTROL Day CQ Workflow Email Notification service中提供的通用通知]** ，以及一组特定于YouTube的通知，具体取决于您的配置设置。

1. 完成后，在对话框的右上角附近，点按完成图 **[!UICONTROL 标]** （复选标记）。
1. 在“发布到YouTube”工作流页面的右上角附近，点按同 **[!UICONTROL 步]**。

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报告仅在运行Dynamic Media —— 混合模式时可用。

视频报表显示指定时间段内的多个汇总指标，帮助您监控*已发布*单个和汇总视频是否按预期效果呈现。以下顶级指标数据是整个网站中所有已发布视频的汇总数据：

* 视频开始
* 完成率
* 视频花费的平均时间
* 视频花费的总时间
* 每次访问的视频数

报表中还会列出包含所有&#x200B;*已发布*&#x200B;视频的表格，以便您能够根据视频开始的总次数，跟踪您网站上最常观看的视频。

在您点按列表中的视频名称时，系统会以折线图向您显示该视频的受众保留（流失）报表。该图表显示了视频播放期间任意给定时刻的查看次数。当您播放视频时，垂直条与播放器中的时间指示器同步进行跟踪。折线图数据中的下降趋势表示受众因不感兴趣而停止观看。

如果视频是在 Adobe Experience Manager Dynamic Media 外部编码的，就不会提供受众保留（流失）图表和表中的播放比例数据。

另请参 [阅配置Dynamic Media Cloud服务](/help/assets/config-dynamic.md)。

>[!NOTE]
>
>只有在使用 Dynamic Media 自带的视频播放器及关联的视频播放器预设时，才可跟踪并报告数据。因此，对于通过其他视频播放器播放的视频，您无法进行跟踪和报告。

默认情况下，在您首次进入视频报表时，报表会显示从当月的第一个开始到当月的当日结束的视频数据。但是，您可以通过指定自己的日期范围来覆盖默认日期范围。下次输入视频报表时，将使用您指定的日期范围。

For video reports to work correctly, a Report Suite ID is automatically created when Dynamic Media Cloud Services is configured. At the same time, the Report Suite ID is pushed to the Publish server so that it is available for the Copy URL feature when you preview assets. However, this requires that the Publish server be already set up. If the Publish server is not set up, you can still publish to see the video report, however, you will need to return to the Dynamic Media Cloud Configuration and tap **[!UICONTROL OK]**.

要查看视频报表，请执行以下操作：

1. 在AEM的左上角，点按AEM徽标，然后在左边栏中，点按工具 **** （锤子图标）>资产 **[!UICONTROL >视频]** 报表 ****。
1. 在“视频报表”页面中，执行以下任一操作：

   * 在右上角附近，点按**刷新视频报表**图标。只有在报告的结束日期是当天时，您才需要使用刷新。这可确保您查看自上次运行报告以来发生的视频跟踪。

   * Near the upper-right corner, tap the **Date Picker **icon.
Specify the beginning and end date range for which you want video data, and then tap **[!UICONTROL Run Report]**.
   “顶级指标”组框标识您网站内所有*已发布*视频的各种汇总测量。

1. 在列出顶级已发布视频的表中，点按视频名称以播放视频，还可以查看该视频的受众保留（流失）报表。

### 查看基于使用 Scene7 HMTL5 查看器 SDK 创建的视频查看器的视频报表 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

如果您使用Dynamic media提供的现成视频查看器，或者如果您基于现成的视频查看器创建了自定义查看器预设，则无需执行其他步骤即可查看视频报告。但是，如果您基于Scene7 HTML5查看器SDK创建了自己的视频查看器，请使用以下步骤确保视频查看器将跟踪事件发送到Dynamic Media视频报表。

使用 Scene7 查看器参考和 Scene7 HTML5 查看器 SDK 创建您自己的视频查看器。

请参阅《[Scene7 查看器参考指南](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html)》。

从 Adobe Developer Connection 下载 Scene7 HTML 查看器 SDK。

请参阅 [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html)。

要查看基于使用 Scene7 HMTL5 查看器 SDK 创建的视频查看器的视频报表，请执行以下操作：

1. 导航到任意已发布的视频资产。
1. 在资产页面的左上角附近，从下拉列表中选择查看 **[!UICONTROL 器]**。
1. 选择任意视频查看器预设，并复制嵌入代码。
1. 在嵌入代码中，找到包含以下内容的代码行：

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. 它还是公司特定的预设，其中包含视频报告和客户特定Adobe Analytics配置的配置信息。

   在**嵌入代码**和副本**URL **函数中均可找到config2参数的正确值。在复制**URL **命令的URL中，要查找的参数为 `&config2=<value>` 。 The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. 在您的自定义视频查看器代码中，通过执行以下操作，将 AppMeasurementBridge.jsp 添加到查看器页面：

   * First, determine if you need the `&preset` parameter.
If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

   * 然后，添加AppMeasurementBridge.jsp脚本：
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 通过执行以下操作，创建 TrackingManager 组件：

   * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

   * 通过执行以下操作，将组件连接到 TrackingManager：
在 `s7sdk.Event.SDK_READY` 事件处理程序中，将您要跟踪的组件连接到 TrackingManager。
例如，如果组件是 `videoPlayer`，则添加
      `trackingManager.attach(videoPlayer);`
将组件附加到trackingManager。 要在一个页面上跟踪多个查看器，可使用多个跟踪管理器组件。

   * 通过添加以下内容创建AppMeasurementBridge对象：

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 通过添加以下内容来添加跟踪功能：

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```
   appMeasurementBridge对象具有内置的跟踪功能。但是，您可以提供自己的功能来支持多个跟踪系统或其他功能。

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

## 向视频中添加字幕 {#adding-captions-to-video}

您可以通过向单个视频或自适应视频集添加字幕，将视频的触及范围扩展到全球市场。 通过添加字幕，您可以避免需要对音频进行混音，或者需要使用母语人士为每种不同的语言重新录制音频。 视频以录制的语言播放。 出现外语字幕，使不同语言的用户仍可了解音频部分。

字幕显示还允许对耳聋或听力欠佳的人使用隐藏式字幕，从而提高辅助功能。

>[!NOTE]
>
>您使用的视频播放器必须支持字幕显示。

Dynamic media能够将题注文件转换为JSON（JavaScript对象表示法）格式。 此转换意味着您可以将JSON文本作为视频的隐藏但完整的记录嵌入到网页中。 然后，搜索引擎可以搜索和索引内容，使视频更容易被发现，并向客户提供有关视频内容的更多详细信息。

有 [关在URL中使用JSON函数的更多信息，请参阅](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_serving_static_nonimage_contents.html)** Scene7图像服务API帮助中的服务静态（非图像）内容。

要向视频添加字幕或字幕，请执行以下操作：

1. 使用第三方应用程序或服务创建视频题注／子标题文件。

   确保您创建的文件符合WebVTT（Web视频文本轨道）标准。 字幕文件扩展名为。vtt。 您可以了解有关WebVTT字幕标准的更多信息。

   请参 [阅WebVTT:Web视频文本跟踪格式](https://dev.w3.org/html5/webvtt/)。

   您可以使用免费和高级工具及服务在Dynamic media之外创作字幕／子标题文件。 例如，要创建不带样式的简单视频题注文件，您可以使用以下免费的在线题注创作和编辑工具：

   [WebVTT字幕制作器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   为获得最佳效果，请使用Internet Explorer 9或更高版本、Google Chrome或Safari中的工具。

   在该工具中，在视频文 **[!UICONTROL 件的输入URL字段中]** ，粘贴复制的视频文件的URL，然后单击 **[!UICONTROL加载**。 请参 [阅获取资产的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) ，以获取视频文件本身的URL，然后您可以将该URL粘贴到视频文件 **[!UICONTROL 字段的输入URL中]**。 然后，Internet Explorer、Chrome或Safari可以本机播放视频。

   现在，请按照站点屏幕上的说明创作并保存您的WebVTT文件。 完成后，复制题注文件内容并将其粘贴到纯文本编辑器中，并以。vtt文件扩展名保存它。

   >[!NOTE]
   >
   >要全局支持多语言视频字幕，请注意，WebVTT标准要求您为要支持的每种语言分别创建单独的。vtt文件和调用。

   通常，您希望将字幕VTT文件命名为与视频文件相同的名称，并在其后面附加语言区域设置，如-EN、-FR或-DE等。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。

1. 在AEM中，将WebVTT题注文件上传到DAM。
1. 导航到要与上传的题注文件关联的*已发布*视频资产。

   请记住，只有在先&#x200B;*发布*&#x200B;资产&#x200B;*之后*，才可复制其 URL。

   请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。

1. 执行下列操作之一：

   * 要获得弹出式视频查看器体验，请点按 **[!UICONTROL URL]**。 在“URL”对话框中，选择URL并将其复制到剪贴板，然后将URL传到简单的文本编辑器中。 在复制的视频URL后面附加以下语法：

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      请注意 `,1` 题注路径末尾的。 紧接路径中。vtt文件扩展名后，您可以选择分别设置为或启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕 `,1` 按 `,0`钮。

   * 要获得嵌入式视频查看器体验，请点按 **[!UICONTROL 嵌入代码]**。 在“嵌入代码”对话框中，选择嵌入代码并将其复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 在复制的嵌入代码后面附加以下语法：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      请注意 `,1` 题注路径末尾的。 紧接路径中。vtt文件扩展名后，您可以选择分别设置为或启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕 `,1` 按 `,0`钮。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

通过向单个视频或自适应视频集添加章节标记，您可以更轻松地观看和导航长形视频。 当用户播放视频时，他们可以单击视频时间线上的章节标记（也称为视频浏览条）以轻松导航到他们感兴趣的点，或立即跳转到新内容、演示、教程等。

>[!NOTE]
>
>所使用的视频播放器必须支持使用章节标记。 Dynamic media视频播放器确实支持章节标记，但使用第三方视频播放器可能不支持。

如果需要，您可以创建带有章节的自定义视频查看器并为其添加品牌，而不是使用视频查看器预设。 有关使用章节导航创建您自己的HTML5查看器的说明，请参阅Adobe Scene7 Viewer SDK for HTML5指南中的类和下方的标题“使用修饰符自定义行为” `s7sdk.video.VideoPlayer` 和 `s7sdk.video.VideoScrubber`。 Adobe Scene7查看器SDK可从 [Adobe Developer Connection下载](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html)。

为视频创建章节列表的方式与创建字幕的方式非常相似。 即，创建WebVTT文件。 但是，请注意，该文件必须与您可能也在使用的任何WebVTT题注文件分开；不能将字幕和章节合并到一个WebVTT文件中。

您可以将以下示例用作创建具有章节导航的WebVTT文件所使用格式的示例：

### 带有视频章节导航的WebVTT文件 {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

在上面的示例中，提 `Chapter 1` 示标识符是可选的。 的提示时间 `00:00:000 --> 01:04:364` 以格式指定章节的开始时间和结束时 `00:00:000` 间。 最后三位数字是毫秒，并且可以保留为 `000`（如果首选）。 章节标题 `The bicycle store behind it all` 是章节内容的实际描述。 当用户将鼠标指针悬停在视频时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器的弹出窗口中。

由于您使用的是HTML5视频查看器，请确保您创建的章节文件符合WebVTT（Web视频文本轨道）标准。 章节文件扩展名为。vtt。 您可以了解有关WebVTT字幕标准的更多信息。

请参 [阅WebVTT:Web视频文本轨道格式](https://dev.w3.org/html5/webvtt/)

**要向视频添加章节标记，请执行以下操作：**

1. 以UTF8编码保存。vtt文件，以避免在章节标题文本中出现字符再现问题。

   通常，您希望将章节VTT文件命名为与视频文件相同的名称，并在其后附加章节。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。
1. 在AEM中，上传您的WebVTT章节文件。

   请参阅[上传资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>要获得弹出式视频查看器体验</td>
       <td>
       <ol>
       <li>导航到要 <i>与 </i>您上传的章节文件关联的已发布视频资产。 请记住，只有在先<i>发布</i>资产<i>之后</i>，才可复制其 URL。请参阅<a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产</a>。</li>
       <li>从下拉菜单中，单击或点按查看 <strong>器</strong>。</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频预览将在单独的页面中打开。</li>
       <li>In the left rail, at the bottom, click <strong>URL</strong>.</li>
       <li>在“URL”对话框中，选择URL并将其复制到剪贴板，然后将URL传到简单的文本编辑器中。</li>
       <li><br /> 在复制的视频URL后面附加以下语法，以将其与复制的URL关联到您的章节文件： <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>对于嵌入式视频查看器体验<br /> </td>
       <td>
       <ol>
       <li>导航到要 <i>与 </i>您上传的章节文件关联的已发布视频资产。 请记住，只有在先<i>发布</i>资产<i>之后</i>，才可复制其 URL。请参阅<a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产</a>。</li>
       <li>从下拉菜单中，单击或点按查看 <strong>器</strong>。</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频预览将在单独的页面中打开。</li>
       <li>In the left rail, at the bottom, click <strong>Embed</strong>.</li>
       <li>在“嵌入代码”对话框中，选择整个代码并将其复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>在视频的嵌入代码后面附加以下语法，以将其与复制的URL关联到您的章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## 关于Dynamic Media - Scene7模式中的视频缩略图 {#about-video-thumbnails-in-dynamic-media-scene-mode}

视频缩略图是向客户展示视频的视频帧或图像资产的缩小版本。 缩略图应有助于鼓励客户点击视频。

AEM中的所有视频都必须具有关联的缩略图；您不能删除缩略图而不替换它。 默认情况下，将视频上传到AEM时，第一帧将用作缩略图。 但是，例如，您可以自定义缩略图以用于品牌或视觉搜索。 自定义视频缩略图时，您可以播放视频并暂停要使用的帧，也可以选择已在数字资产管理器中上传和发布 *的图* 像资产。

请注意，您从视频中选择的自定义视频缩略图图像不会提取并另存为单独的独特资产。 但是，您从现有图像资产中选择的自定义视频缩略图会保存到JCR。 选定资产的路径存储在视频资产的节点下，如下面的示例路径所示：

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

只有在将视频配置文件应用到视频所在的文件夹之后，才能自定义视频缩略图。

另请参阅 [关于Dynamic Media —— 混合模式中的视频缩略图](#about-video-thumbnails-in-dynamic-media-hybrid-mode)。

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail}

这些步骤仅适用于在“Dynamicmedia_Scene7”模式下运行的Dynamic Media。

要&#x200B;**添加自定义视频缩略图**,

1. 请确保您已经执行了以下操作：

   * 为视频资产创建了文件夹。
   * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders)。

   * [已将视频上传到文件夹](/help/assets/managing-video-assets.md#uploadingandpreviewingvideoassets)。

1. 导航到要更改其缩略图的已上传视频资产。
1. 在资产选择模式下，从列 **[!UICONTROL 表视图]** 或 ****&#x200B;卡片视图中点按视频资产。
1. 在工具栏上，点 **按[!UICONTROL属性图标** （其中带有“i”的圆）。
1. 在视频的“属性”页面上，点按更改 **[!UICONTROL 缩略图]**。
1. 在“更改缩略图”页面上，执行下列操作之一：

   * 要使用视频中的帧作为新缩略图，请执行以下操作：

      * 在工具栏中，点按从 **[!UICONTROL 视频中选择帧]**。
      * 点按“播放”按钮，然后点按要捕获的帧上的“暂停”按钮作为视频的新缩略图。
   * 要将图像资产用作新缩略图，请执行以下操作：

      * 在工具栏中，点按从 **[!UICONTROL 资产中选择缩略图]**。
      * 点按 **[!UICONTROL 选择缩略图]**。
      * 导航到您要使用的先前已上传和已发布的图像资产。 请注意，资产将自动调整大小以用作视频的缩略图。
      * 选择图像资产，然后点按 **[!UICONTROL 选择]**。


1. 在“更改缩略图”页面上，点按保 **[!UICONTROL 存更改]**。
1. 在视频的“属性”页面的右上角，点按保 **[!UICONTROL 存并关闭]**。

## 关于Dynamic Media中的视频缩略图——混合模式 {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

您可以从Dynamic media自动生成的十张缩略图中选择一张，以添加到您的视频中。 在AEM Sites、AEM Mobile或AEM Screens的创作环境中将视频资产与Dynamic media组件一起使用时，视频播放器会显示选定的缩略图。 缩略图用作最能代表整个视频内容的静态图片，并进一步鼓励用户单击“播放”按钮。

根据视频的总时间，Dynamic media将捕获十个（默认）缩略图，其中1%、11%、21%、31%、41%、51%、61%、71%、81%和91%加入视频。 十个缩览图会保留，这意味着如果您稍后决定选择其他缩览图，则无需重新生成系列。 预览十个缩略图，然后选择要用于视频的图像。 如果要更改为默认值，可以使用CRXDE lite配置生成缩略图的时间间隔。 例如，如果您只想从视频中生成一系列四张均匀间隔的缩略图，则可以将间隔时间配置为24%、49%、74%和99%。

理想情况下，在上传视频后但在网站上发布视频之前，您可以随时添加视频缩略图。

如果您愿意，您可以选择上传自定义缩略图以代表您的视频，而不是使用Dynamic media生成的缩略图。 例如，您可以创建自定义缩略图图像，该图像具有视频的标题、引人注目的打开图像或从视频捕获的非常特定的图像。 您上传的自定义视频缩略图图像的最大分辨率应为1280 x 720像素（最小宽度为640像素）且不大于2MB。

另请参 [阅关于Dynamic Media - Scene7模式中的视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

### 添加视频缩略图 {#adding-a-video-thumbnail}

这些步骤仅适用于在混合模式下运行的Dynamic Media。

要&#x200B;**添加视频缩略图**,

1. 导航到要添加视频缩略图的已上传视频资产。
1. 在资产选择模式下，从列表视图或卡片视图中点按视频资产。
1. 在工具栏中，点按 **[!UICONTROL 查看属性图标]** （其中带有“i”的圆圈）。
1. 在视频的“属性”页面上，点按更改 **[!UICONTROL 缩略图]**。
1. 在“更改缩略图”页面的工具栏中，点按选择 **[!UICONTROL 框架]**。

   Dynamic media根据您自定义的默认时间间隔或时间间隔，从您的视频生成一系列缩略图图像。

1. 预览生成的缩略图图像，然后选择要添加到视频中的缩略图。
1. 点按 **[!UICONTROL 保存更改]**。

   视频的缩略图图像将更新为使用您选择的缩略图。 如果您稍后决定更改缩略图，则可返回“更改缩略图”页 **[!UICONTROL 面]** ，然后选择一个新的缩略图。

   如果您配置了新的默认时间间隔，或者上传了新视频以替换现有视频，则需要Dynamic media重新生成缩略图。

   请参 [阅配置生成视频缩略图的默认时间间隔](#configuring-the-default-time-interval-that-video-thumbnails-are-generated)。

#### 配置生成视频缩略图的默认时间间隔 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

当您配置并保存新的默认时间间隔时，所做的更改将仅自动应用于您将来上传的视频。 它不会自动将新的默认值应用于您之前上传的视频。 对于现有视频，必须重新生成缩略图。

请参 [阅添加视频缩略图](#adding-a-video-thumbnail)。

**要配置生成视频缩略图的默认时间间隔，**

1. 在AEM中，点按工 **[!UICONTROL 具]** >常 **[!UICONTROL 规]** > **[!UICONTROL CRXDE Lite]**。

1. 在CRXDE Lite页面左侧的目录面板中，导航到 `o etc/dam/imageserver/configuration/jcr:content/settings.`

   如果目录面板不可见，则可能需要点按“主页”选项卡左侧的>>图标。

1. 在右下角的面板中，在“属性”选项卡中，双击 `thumbnailtime`。
1. 在“编辑缩览图时间”对话框中，使用文本字段以百分比形式输入间隔值。

   * 点按加号(+)图标以添加一个或多个间隔值字段。 您可能需要滚动到对话框底部才能看到该图标。
   * 点按间隔值字段右侧的减号(-)图标，将其从列表中删除。
   * 点按向上箭头图标和向下箭头图标以重新排序间隔值。

1. 点按 **[!UICONTROL 确定]** ，以返回“属性”选项卡。
1. 在CRXDE lite页面的左上角附近，点按全部保 **[!UICONTROL 存]**，然后点按左上角的返回主页图标以返回到AEM。

   请参 [阅添加视频缩略图。](#adding-a-video-thumbnail)

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail-1}

这些步骤仅适用于在混合模式下运行的Dynamic Media。

要&#x200B;**添加自定义视频缩略图**,

1. 导航到要添加自定义视频缩略图的已上传视频资产。
1. 在资产选择模式下，从列表视图或卡片视图中点按视频资产。
1. 在工具栏中，点按 **[!UICONTROL 查看属性图标]** （其中带有“i”的圆圈）。
1. 在视频的“属性”页面上，点按更改 **[!UICONTROL 缩略图]**。
1. 在“更改缩略图”页面的工具栏中，点按上传 **[!UICONTROL 新缩略图]**。
1. 导航到要使用的缩略图，选择它，然后点按打 **[!UICONTROL 开]** ，开始将图像上传到AEM。 上传后，请确保发布图像。
1. 成功上传并发布图像后，在“更改缩略图”页面中，点按保 **[!UICONTROL 存更改]**。

   自定义缩略图会添加到视频中。

