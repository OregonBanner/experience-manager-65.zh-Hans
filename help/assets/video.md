---
title: Dynamic Media 中的视频
description: 了解如何在Dynamic Media中使用视频，例如编码视频、将视频发布到YouTube以及查看视频报表的最佳实践。 还可了解如何向视频添加隐藏式字幕、字幕或章节标记。
mini-toc-levels: 3
uuid: 97f311a3-a227-479a-91bf-fb54ecd1a55d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 1103b849-0042-4e11-b170-38ee81dd0157
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 28cf9e39-cab4-4278-b6c9-e84cc31964db
source-git-commit: fb287b3082a9376c01fd609edd0f4782278e6b37
workflow-type: tm+mt
source-wordcount: '12760'
ht-degree: 15%

---

# Dynamic Media 中的视频 {#video}

本节介绍如何在 Dynamic Media 中处理视频。

## 快速入门：视频 {#quick-start-videos}

下面的工作流分布说明旨在帮助您在 Dynamic Media 中快速设置并运行自适应视频集。每个步骤之后，都有对主题标题的交叉引用，您可以在其中查找更多信息。

>[!IMPORTANT]
>
>在Dynamic Media中使用视频之前，请确保您的Adobe Experience Manager管理员已在Dynamic Media - Scene7模式或Dynamic Media — 混合模式下启用和配置Dynamic MediaCloud Services。
>
>* 参见 [配置Dynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) 在配置Dynamic Media - Scene7模式和 [Dynamic Media - Scene7模式疑难解答](/help/assets/troubleshoot-dms7.md).
>
>* 参见 [配置Dynamic MediaCloud Services](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) 在配置Dynamic Media — 混合模式中。
>
>Dynamic Media中当前已知的视频播放问题 *仅在Experience Manager6.5.9.0上*：
>
>* 如果发布的视频已更新，则必须再次发布该视频以反映投放中的更改。
>


1. 通过执行以下操作，**上传 Dynamic Media 视频**：

   * 创建您自己的视频编码配置文件。或者，您只需使用预定义的 _自适应视频编码_ Dynamic Media随附的资料。

      * [创建视频编码配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 详细了解 [视频编码的最佳实践](#best-practices-for-encoding-videos).
   * 将视频处理配置文件与一个或多个要上传主源视频的文件夹关联。

      * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * 了解有关[组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)的更多信息。
      * 详细了解 [组织数字资源](/help/assets/organize-assets.md).
   * 将您的主源视频上传到文件夹。 将视频添加到文件夹时，会根据您分配给该文件夹的视频处理配置文件对它们进行编码。

      * Dynamic Media主要支持最长30分钟、最小分辨率大于25 x 25的短格式视频。
      * 您可以上传每个大小不超过15 GB的视频文件。
      * [上传视频](/help/assets/managing-video-assets.md#upload-and-preview-video-assets)。
      * 了解有关[支持的输入文件格式](/help/assets/assets-formats.md#supported-multimedia-formats)的更多信息。
   * 监视方式 [视频编码正在进行](#monitoring-video-encoding-and-youtube-publishing-progress) 从资产或工作流视图中。




1. 通过执行以下任意操作，**管理 Dynamic Media 视频**：

   * 组织、浏览和搜索视频资产

      * [组织数字资源](/help/assets/organize-assets.md)
详细了解 [组织数字资产以使用处理配置文件的最佳实践](organize-assets.md)

      * [搜索视频资产](search-assets.md#custompredicates) 或 [搜索资源](/help/assets/search-assets.md)
   * 预览和发布视频资产

      * 查看源视频、视频的编码演绎版及其相关缩略图：
         [预览视频](managing-video-assets.md#upload-and-preview-video-assets) 或 [预览资源](previewing-assets.md)
         [查看视频演绎版](video-renditions.md)
         [管理视频演绎版](manage-assets.md#managing-renditions)

      * [管理查看器预设](managing-viewer-presets.md)
      * [发布资产](publishing-dynamicmedia-assets.md)
   * 处理视频元数据

      * 查看已编码视频演绎版的属性，如帧速率、音频和视频比特率以及编解码器：
         [查看视频演绎版属性](video-renditions.md)

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
         [编辑视频属性](manage-assets.md#editing-properties)

      * [管理数字资源的元数据](metadata.md)
      * [元数据架构](metadata-schemas.md)
   * 审核和批准视频，在视频中添加注释，以及保持全面的版本控制

      * [为视频添加批注](managing-video-assets.md#annotate-video-assets) 或 [为资源作批注](manage-assets.md#annotating)

      * [创建一个版本](manage-assets.md#asset-versioning)
      * [将工作流应用于资产](assets-workflow.md) 或参阅 [在资产上启动工作流](manage-assets.md#starting-a-workflow-on-an-asset)

      * [审核文件夹资产](bulk-approval.md)
      * [项目](../sites-authoring/projects.md)




1. 通过执行以下任一操作，**发布 Dynamic Media 视频**：

   * 如果您使用Adobe Experience Manager作为Web内容管理系统，则可以直接将视频添加到网页。

      * [将视频添加到网页](adding-dynamic-media-assets-to-pages.md).
   * 如果您使用的是第三方Web内容管理系统，则可以将视频链接或嵌入到网页。

      * 使用URL集成视频：
         [将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md).

      * 在网页上使用嵌入代码集成视频：
         [在网页上嵌入视频查看器](embed-code.md).
   * [将视频发布到YouTube](#publishing-videos-to-youtube).
   * [生成视频报表](#viewing-video-reports).

   * [向视频添加字幕](#adding-captions-to-video).



## 在Dynamic Media中处理视频 {#working-with-video-in-dynamic-media}

Dynamic Media中的视频是一款端到端解决方案，可让您轻松地发布高质量的自适应视频，以便在多个屏幕(包括台式机、iOS、Android™、BlackBerry®和Windows移动设备)上实现流式传输。 自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。台式计算机或移动设备会检测可用带宽。

例如，在 iOS 移动设备上，设备检测到 3G、4G 或 Wi-Fi 等带宽。设备会随之自动从自适应视频集内的各种视频比特率中选择正确的编码视频。然后，视频会在桌面设备、移动设备或平板电脑上进行流播放。

此外，如果桌面或移动设备上的网络条件发生变化，设备会自动动态地切换视频质量。此外，如果客户在桌面上进入全屏模式，自适应视频集将使用更好的分辨率进行响应，从而改善客户的观看体验。 通过使用自适应视频集，客户可以在多个屏幕和设备上播放Dynamic Media视频，您可以获得最佳播放体验。

视频播放器用来确定在播放期间要播放或选择的已编码视频的逻辑基于以下算法：

1. 视频播放器根据比特率加载初始视频片段，该比特率最接近在播放器本身中为“初始比特率”设置的值。
1. 视频播放器根据对带宽速度的更改进行切换，使用的标准如下：

   1. 播放器选择低于或等于估计带宽的最高带宽流。
   1. 播放器只考虑了80%的可用带宽。 然而，如果它调高了，它更保守，只有70%，以避免高估并立即回调。

有关算法的详细技术信息，请参阅 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

对于管理单个视频和自适应视频集，支持以下内容：

* 从多种支持的视频格式和音频格式上传视频并将视频编码为MP4 H.264格式以便在多个屏幕上播放。 您可以使用预定义的自适应视频预设或单个视频编码预设，或者自定义您自己的编码，来控制视频的质量和大小。

   * 在生成自适应视频集时，会包括 MP4 视频。
   * **注意**：主/源视频不会添加到自适应视频集。

* 所有HTML5视频查看器中的视频字幕。
* 组织、浏览和搜索具有全面元数据支持的视频，以实现高效的视频资产管理。
* 将自适应视频集交付到Web、桌面和移动设备，包括iPhone、iPad、Android™、BlackBerry®和Windows phone。

各种iOS平台均支持自适应视频流。 参见 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media支持MP4 H.264视频的移动视频播放。您可以在以下位置找到支持此视频格式的BlackBerry®设备： [BlackBerry®支持的视频格式](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

您可以在以下位置找到支持此视频格式的Windows设备： [Windows Phone 8支持的媒体编解码器](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* 使用 Dynamic Media 视频查看器预设播放视频，包括以下查看器：

   * 单一视频查看器。
   * 将视频和图像内容组合在一起的混合媒体查看器。

* 配置视频播放器以满足您的品牌需求。
* 使用简单的 URL 或嵌入代码将视频集成到您的网站、移动站点或移动应用程序。

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

另请参阅 [Experience Manager Assets和Dynamic Media Classic查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [仅适用于Experience Manager资源的查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## 最佳实践：使用HTML5视频查看器 {#best-practice-using-the-html-video-viewer}

Dynamic Media HTML5视频查看器预设是可靠的视频播放器。您可以使用它们来避免与HTML5视频播放相关的许多常见问题。 此外，还存在着与移动设备相关的问题，例如缺乏自适应比特率流交付以及桌面浏览器访问范围有限。

在播放器的设计方面，您可以使用标准Web开发工具来设计视频播放器的功能。 例如，您可以使用 HTML5 和 CSS 设计按钮、控件和自定义标识图像背景，从而帮助您向客户展示自定义的外观。

在查看器的播放方面，它会自动检测浏览器的视频功能。 然后，它使用HLS（HTTP实时流）或DASH（HTTP上的动态自适应流）提供视频，也称为自适应比特率流。 或者，如果这些传送方法不可用，则会改用 HTML5 渐进式流播放。

通过将以下内容组合到单个播放器中：

* 能够使用HTML5和CSS设计播放组件
* 具有嵌入式播放
* 根据浏览器的功能使用自适应流和渐进式流

您可以将富媒体内容的范围扩展到桌面和移动设备用户，并确保提供简化的视频体验。

另请参阅 [关于HTML5查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### 使用HTML5视频查看器在桌面计算机和移动设备上播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动设备自适应视频流，用于比特率切换的视频基于自适应视频集中的所有MP4视频。

使用DASH或HLS或者渐进式视频下载进行视频播放。 在早期版本的Experience Manager（如6.0、6.1和6.2）中，视频是通过HTTP进行流式传输的。

在Experience Manager6.3及更高版本中，视频现在通过HTTPS（即DASH或HLS）进行流式传输，因为DM网关服务URL也始终使用HTTPS。 此默认行为对客户没有影响。 也就是说，除非浏览器不支持HTTPS，否则始终会通过HTTPS进行视频流。 （见下表）。 因此，

* 如果您的HTTPS网站支持HTTPS视频流，则可以使用流式传输。
* 如果您的HTTP网站包含HTTPS视频流，则可以使用流处理，并且Web浏览器中没有出现混合内容问题。

DASH是国际标准，HLS是Apple标准。 两者都用于自适应视频流。 而且，这两种技术都会根据网络带宽容量自动调整播放。 它还允许客户在视频中的任何位置“搜寻”，而无需等待视频的其余部分下载。

渐进式视频是通过将视频下载并存储到用户的桌面系统或移动设备上的方式交付的。

下表介绍了使用Dynamic Media Video Viewer在桌面计算机和移动设备上播放视频的设备、浏览器和方法。

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
   <td>在Windows 8和Windows 10上 — 每当请求DASH*或HLS时，强制使用HTTPS。 已知限制：DASH*或HLS上的HTTP在此浏览器/操作系统组合中不起作用<br /> <br /> 在Windows 7上 — 渐进式下载。 使用标准逻辑选择HTTP与HTTPS协议。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Firefox 23-44</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Firefox 45或更高版本</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>铬黄</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>桌面设备</td>
   <td>Safari (Mac)</td>
   <td>HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 6或更低版本)</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (Android™ 7或更高版本)</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android™（默认浏览器）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari (iOS)</td>
   <td>HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome (iOS)</td>
   <td>HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>BlackBerry®</td>
   <td>DASH*或HLS自适应比特率流。/td&gt;
  </tr>
 </tbody>
</table>

>[!IMPORTANT]
>
>*要在视频中使用DASH，必须首先由您帐户上的Adobe技术支持启用。 参见 [在您的帐户上启用DASH](#enable-dash).)

## Dynamic Media视频解决方案的架构 {#architecture-of-dynamic-media-video-solution}

下图显示了通过DMGateway(在Dynamic Media混合模式下)上传和编码并可供公众使用的视频的整体创作工作流。

![chlimage_1-427](assets/chlimage_1-427.png)

## 视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 视频编码的最佳实践 {#best-practices-for-encoding-videos}

此 **Dynamic Media编码视频** 如果您已启用Dynamic Media并设置了视频云服务，则工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已启用Dynamic Media并设置了视频云服务，则 **[!UICONTROL Dynamic Media编码视频]** 上传视频时，工作流会自动生效。 (如果您没有使用Dynamic Media，则 **[!UICONTROL DAM更新资产]** 工作流将生效。)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### 源视频文件 {#source-video-files}

在对视频文件进行编码时，请尽可能使用最高质量的源视频文件。避免使用先前已编码的视频文件，因为这样的文件已经压缩，进一步编码会导致创建的视频质量不佳。

* Dynamic Media主要支持最长30分钟、最小分辨率大于25 x 25的短格式视频。
* 您可以上传每个大小最大为15 GB的主源视频文件。

下表描述了源视频文件在编码之前必须具有的建议大小、长宽比和最小比特率：

| 大小 | 宽高比 | 最低比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps，适用于大部分视频。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的动作数量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的动作数量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

您可以通过以下方式获取文件的元数据：使用视频编辑工具查看其元数据，或使用专为获取元数据而设计的应用程序。以下是使用第三方应用程序MediaInfo获取视频文件元数据的说明：

1. 转到 [MediaInfo下载](https://mediaarea.net/en/MediaInfo/Download).
1. 选择并下载 GUI 版本的安装程序，然后按照安装说明进行操作。
1. 完成安装后，右键单击视频文件（仅限 Windows）并选择 MediaInfo，或打开 MediaInfo 并将视频文件拖到该应用程序中。您会看到与该视频文件相关的所有元数据，包括其宽度、高度和每秒帧数。

### 宽高比 {#aspect-ratio}

当您选择或创建主源视频文件的视频编码预设时，请确保预设具有与主源视频文件相同的纵横比。 宽高比是视频的宽度与高度的比率。

要确定视频文件的纵横比，请获取文件的元数据并记下文件的宽度和高度（请参阅上面获取文件的元数据）。然后使用此公式确定纵横比：

宽度/高度 = 宽高比

下表说明了公式结果如何转换成常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，1440宽度x 1080高度的视频的长宽比为1440/1080，即1.33。在这种情况下，您可以选择具有4:3纵横比的视频编码预设来编码视频文件。

### 比特率 {#bitrate}

Bitrate是经过编码以构成视频播放一秒的数据量。 比特率以千位/秒(Kbps)为测量单位。

>[!NOTE]
>
>由于所有的编解码器都使用有损压缩，因此比特率是决定视频质量的最重要因素。 使用有损压缩时，对视频文件的压缩程度越大，质量就降低得越多。因此，所有其他特性（分辨率、帧速率和编解码器）相等，比特率越低，压缩文件的质量就越低。

在选择比特率编码时，可以选择以下两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR) — 在CBR编码期间，比特率或每秒比特数在整个编码过程中保持不变。 CBR编码会在整个视频中将设置的数据速率保留到您的设置中。 此外，CBR编码不会优化媒体文件的质量，但会节省存储空间。
如果您的视频在整个视频中包含类似的运动级别，请使用CBR。 CBR最常用于流视频内容。 另请参阅 [使用添加自定义的视频编码参数](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 可变比特率编码]** (VBR) - VBR编码根据压缩程序所需的数据来向下调整数据速率，并将其调整到您设置的上限。 此功能意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态增加或减少。
VBR的编码时间较长，但产生的结果最理想；媒体文件的质量也更好。 VBR最常用于http渐进式视频内容交付。

您何时使用VBR还是CRB？
在选择VBR与CBR时，几乎总是建议您将VBR用于媒体文件。 VBR以具有竞争力的比特率提供更高质量的文件。 使用VBR时，请确保使用两遍编码，并将最大比特率设置为目标视频比特率的1.5倍。

选择视频编码预设时，请记住目标最终用户的连接速度。 所选预设的数据率应该是目标最终用户连接速度的 80%。例如，如果目标最终用户的连接速度为1000 Kbps，则最佳预设为视频数据速率为800 Kbps的预设。

下表说明了典型连接速度的数据率。

| 速度 (Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型移动连接。对于此类连接，3G 体验的目标数据率范围为 400 至最高 800。 |
| 2000 | 典型的宽带台式机连接。对于这种连接，数据速率目标在800-2000 Kbps范围内，大多数目标平均为1200-1500 Kbps。 |
| 5000 | 典型高宽带连接。不建议在此较高范围下进行编码，因为大多数用户并不具备此速度的视频传送条件。 |

### 解决方法 {#resolution}

**分辨率** 描述视频文件的高度和宽度（以像素为单位）。大多数源视频以高分辨率存储（例如，1920 x 1080）。出于流传输目的，源视频被压缩成较小的分辨率（640 x 480或更小）。

分辨率和数据率是两个相互关联、密不可分的因素，它们决定着视频质量。为保持同等的视频质量，视频文件的像素数越高（分辨率越高），数据率就必须越高。例如，考虑分辨率分别为 320 x 240 和 640 x 480 的视频文件的每帧像素数：

| 解决方法 | 每帧像素数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

对于分辨率为 640 x 480 的文件，其每帧像素数高出四倍。为使这两个示例分辨率的文件实现同等的数据率，您需要对分辨率为 640 x 480 的文件应用四倍的压缩，而这会降低视频的质量。因此，如果视频数据率为 250 Kbps，则在 320 x 240 分辨率下观看时质量会很高，但在 640 x 480 分辨率下观看时质量则不高。

通常，使用的数据速率越高，视频的外观越好，使用的分辨率越高，必须保持的查看质量的数据速率越高（与分辨率较低相比）。

由于分辨率与数据率相关联，在对视频进行编码时，有两种选择：

* 选择一个数据率，然后使用在选定数据率下看起来效果不错的最高分辨率进行编码。
* 选择一个分辨率，然后使用在选定分辨率下获得高质量视频所需的数据率进行编码。

当为主源视频文件选择（或创建）视频编码预设时，请使用此表定位正确的分辨率：

| 解决方法 | 高度（像素） | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 微型屏幕 |
| 300p | 300 | 通常用于移动设备的小型屏幕 |
| 360p | 360 | 小型屏幕 |
| 480p | 480 | 中型屏幕 |
| 720p | 720 | 大型屏幕 |
| 1080p | 1080 | 高清晰度大型屏幕 |

### Fps（每秒帧数） {#fps-frames-per-second}

在美国和日本，大多数视频以 29.97 帧/秒 (fps) 的速率拍摄；在欧洲，大多数视频以 25 fps 的速率拍摄。电影是以 24 fps 的速率拍摄。

选择与主源视频文件的fps速率匹配的视频编码预设。 例如，如果主源视频为25 fps，请选择一个编码预设为25 fps。 默认情况下，所有自定义编码都使用主源视频文件的fps。 鉴于这一原因，您在创建视频编码预设时不需要明确指定 fps 设置。

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

### 在您的帐户上启用DASH {#enable-dash}

DASH(Digital Adaptive Streaming over HTTP)是视频流的国际标准，被广泛用于各种视频观看者。 在您的帐户上启用DASH后，您可以选择使用DASH或HLS进行自适应视频流。 或者，您可以在以下情况下通过自动在播放器之间切换来选择两者 **[!UICONTROL 自动]** 在查看器预设中选择作为播放类型。

在您的帐户上启用DASH的一些主要优势包括：

* 打包用于自适应比特率流的DASH流视频。 这种方法可以提高投放效率。 自适应流媒体可确保为客户提供最佳观看体验。
* 使用Dynamic Media播放器优化浏览器流会在HLS和DASH流之间切换，以确保最佳服务质量。 使用Safari浏览器时，视频播放器会自动切换到HLS。
* 您可以通过编辑视频查看器预设来配置首选的流方法（HLS或DASH）。
* 优化的视频编码确保在启用DASH功能时不会使用额外的存储。 为HLS和DASH创建一组视频编码，以优化视频存储成本。
* 帮助让您的客户更容易访问视频交付。
* 也通过API获取流URL。

   >[!IMPORTANT]
   >
   >当前仅在北美地区才会在您的帐户上启用DASH。

在您的帐户中启用DASH需要两个步骤：

* 将Dynamic Media配置为使用DASH，以便您自行完成此操作。
* 将Experience Manager6.5配置为使用DASH，这是通过您创建和提交的Adobe客户支持案例来完成的。

**要在您的帐户上启用DASH，请执行以下操作：**

1. **配置Dynamic Media**  — 在Experience Manager6.5上的Dynamic Media中，导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 搜索 **AEM Assets Dynamic Media视频高级流** 功能标记。
1. 选中此复选框可启用（打开）短划线。
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. **配置Experience Manager6.5** - [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 按照说明创建支持案例，同时确保提供以下信息：

   * 主要联系人姓名、电子邮件、电话。
   * 您的Dynamic Media帐户的名称。
   * 指定您希望在Experience Manager6.5上启用短划线。

1. Adobe客户支持根据提交请求的顺序将您添加到DASH客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持将联系您以协调并设置启用DASH的目标日期。
1. 客户支持团队会在完成后通知您。
1. 创建您的 [视频查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) 和往常一样。

## 将视频发布到YouTube {#publishing-videos-to-youtube}

您可以将内部部署Experience Manager视频资产直接发布到之前创建的YouTube渠道。

要将视频资产发布到 YouTube，您需要为 Experience Manager Assets 设置标记。将这些标记与YouTube渠道关联。 如果视频资产的标记与YouTube渠道的标记匹配，则视频将发布到YouTube。 只要使用关联的标记，发布到YouTube的过程就会伴随着视频的正常发布。

YouTube自行编码。 因此，上传到Experience Manager的原始视频文件将发布到YouTube，而不是Dynamic Media的编码创建的任何视频演绎版。 虽然不需要使用Dynamic Media处理视频，但预计会在播放需要查看器预设时这样做。

当您绕过视频处理配置文件并直接发布到YouTube时，这仅仅意味着您在Experience Manager资源中的视频资源未获得可查看的缩略图。 这也意味着，如果你跑进 `dynamicmedia` 或 `dynamicmedia_scene7` 运行模式，未编码的视频不适用于任何Dynamic Media资源类型。

将视频资产发布到YouTube服务器需要完成以下任务，以确保使用YouTube进行服务器到服务器身份验证的安全性和安全性：

1. [配置Google云设置](#configuring-google-cloud-settings)
1. [创建YouTube渠道](#creating-a-youtube-channel)
1. [添加标记以进行发布](#adding-tags-for-publishing)
1. [启用YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent)
1. [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem)
1. [（可选）自动为您上传的视频设置默认YouTube属性](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [将视频发布到您的YouTube渠道](#publishing-videos-to-your-youtube-channel)
1. [（可选）验证YouTube上发布的视频](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [将YouTube URL链接到您的Web应用程序](#linking-youtube-urls-to-your-web-application)

您还可以[取消发布视频以将其从 YouTube 中删除](#unpublishing-videos-to-remove-them-from-youtube)。

### 配置Google云设置 {#configuring-google-cloud-settings}

要发布到YouTube，您需要Google帐户。 如果您拥有GMAIL帐户，则表明您已经拥有Google帐户；如果您没有Google帐户，则可以轻松创建一个帐户。 您需要帐户，因为您需要凭据才能将视频资产发布到YouTube。 如果您已创建帐户，请跳过此任务并直接转到 [创建YouTube渠道](#creating-a-youtube-channel).

与Google Cloud一起使用的帐户和用于YouTube的Google帐户无需相同。

Google会定期更改其用户界面。 因此，将视频发布到YouTube的步骤可能与以下文档略有不同。 当您尝试检查视频是否已上传到YouTube时，此注意事项也适用。

>[!NOTE]
>
>在撰写本文时，以下步骤是准确的。 但是，Google会定期更新其网站，恕不另行通知。 因此，这些步骤可能略有不同。

要配置Google Cloud设置，请执行以下操作：

1. 创建Google帐户。
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   如果您已有Google帐户，请跳至下一步。

1. 转到 [https://cloud.google.com/](https://cloud.google.com/).
1. 在Google cloud页面的右上角附近，单击控制 **[!UICONTROL 台]**。

   如有必要， **[!UICONTROL 登录]** 使用您的Google帐户凭据查看 **[!UICONTROL 控制台]** 选项。

1. 在“功能板”页面的 **[!UICONTROL Google Cloud平台]**，单击项目下拉列表以打开选择项目对话框。
1. 在选择项目对话框中，点按 **[!UICONTROL 新建项目]**.

   ![6_5_google帐户 — 新项目](assets/6_5_googleaccount-newproject.png)

1. 在“新建项目”对话框的“项目名称”字段中，键入新项目的名称。

   您的项目ID基于您的项目名称。 因此，请仔细选择项目名称；项目名称在创建后无法更改。 此外，当您稍后在Experience Manager中设置YouTube时，必须再次输入相同的项目ID；请考虑将其写下来。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 执行以下操作之一：

   * 在项目的功能板上，在入门信息卡中，点按 **[!UICONTROL 探索和启用API]**.
   * 在您项目的功能板上的API信息卡中，点按 **[!UICONTROL 转到API概述]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. 在“API和服务”页面顶部附近，点按 **[!UICONTROL 启用API和服务]**.
1. 在“API库”页面的左侧，下方 **[!UICONTROL 类别]**，点按 **[!UICONTROL YouTube]**. 在页面的右侧，点按 **[!UICONTROL YouTube数据API]**.
1. 在YouTube Data API v3页面上，点按 **[!UICONTROL 启用]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. 要使用API，您需要凭据。 如有必要，请单击 **[!UICONTROL 创建凭据]**.

   ![6_5_googleaccount-apis-creategrecredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. 在 **[!UICONTROL 向项目添加凭据]** 第页，第1步，执行以下操作：

   * 从 **[!UICONTROL 您使用的是哪个API？]** 下拉列表，选择 **[!UICONTROL YouTube数据API v3]**.

   * 从 **[!UICONTROL 您从何处调用API？]** 下拉列表，选择 **[!UICONTROL Web服务器（例如，node.js、Tomcat）]**

   * 从 **[!UICONTROL 您正在访问哪些数据？]** 下拉列表，点按 **[!UICONTROL 用户数据]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. 点按 **[!UICONTROL 我需要什么凭据？]**
1. 在&#x200B;**[!UICONTROL 将凭据添加到项目]**&#x200B;页面中步骤 2 的&#x200B;**[!UICONTROL 创建 OAuth 2.0 客户端 ID]** 标题下，根据需要在“名称”字段中输入唯一名称。或者，您也可以使用 Google 指定的默认名称。
1. 在 **[!UICONTROL 授权的JavaScript源]** 标题，在文本字段中输入以下路径，在路径中替换您自己的域和端口号，然后按键 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>`

   例如，`https://1a2b3c.mycompany.com:4321`

   **注释**：上述路径示例仅用于演示目的。

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. 在 **[!UICONTROL 授权的重定向URI]** 标题，在文本字段中输入以下路径，在路径中替换您自己的域和端口号，然后按键 **[!UICONTROL 输入]** 要将路径添加到列表，请执行以下操作：

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例如，`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **注释**：上述路径示例仅用于演示目的。

1. 单击 **[!UICONTROL 创建OAuth客户端ID]**.
1. 在&#x200B;**[!UICONTROL 向项目添加凭据]**&#x200B;页面的步骤 3 中，在&#x200B;**[!UICONTROL 设置 OAuth 2.0 许可屏幕]**&#x200B;标题下，选择您当前使用的 Gmail 电子邮件地址。

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. 在 **[!UICONTROL 向用户显示的产品名称]** 标题，在文本字段中，输入要显示在同意屏幕上的内容。

   当Experience Manager管理员对YouTube进行身份验证时，将会向Experience Manager管理员显示同意屏幕；管理员会联系YouTube以获取权限。

1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 在将凭据添加到项目页面的步骤4中，在“下载凭据 **[!UICONTROL ”标题下]** ，点按 **[!UICONTROL 下载]**。

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. 保存 `client_id.json` 文件。

   稍后在Adobe Experience Manager中设置YouTube时，您需要此下载的json文件。

1. 单击&#x200B;**[!UICONTROL 完成]**。

   注销您的Google帐户。 现在创建一个YouTube渠道。

### 创建YouTube渠道 {#creating-a-youtube-channel}

要将视频发布到YouTube，您需要具有一个或多个渠道。 如果您已创建YouTube渠道，则可以跳过此任务并转到 [添加标记以进行发布](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>确保您已在YouTube中设置了一个或多个渠道 *早于* 您可以在“Experience Manager中的YouTube设置”下添加渠道(请参阅 [在Experience Manager中设置YouTube](#setting-up-youtube-in-aem) （如下所示）。 如果您未能设置一个或多个渠道，则不会警告您不存在渠道。 但是，在添加频道时，Google身份验证仍会发生，但无法选择发送视频的频道。

**要创建YouTube渠道，请执行以下操作：**

1. 转到 [https://www.youtube.com](https://www.youtube.com/) 并使用您的Google帐户凭据登录。
1. 在YouTube页面的右上角，单击您的个人资料图片（也可以显示为实色圆圈中的字母），然后单击 **[!UICONTROL YouTube设置]** （圆齿轮图标）。
1. 在概述页面的其他功能标题下，单击 **[!UICONTROL 查看我的所有渠道或创建渠道]**.
1. 在渠道页面上，单击 **[!UICONTROL 创建新渠道]**.
1. 在“品牌帐户”页面的品牌帐户名称字段中，输入业务名称或您选择要将视频资产发布到的其他渠道名称，然后单击 **[!UICONTROL 创建]**.

   请记住您在此处输入的名称，因为在Experience Manager中设置YouTube时必须再次输入该名称。

1. （可选）如有必要，请添加更多渠道。

   现在添加标记以进行发布。

### 添加标记以进行发布 {#adding-tags-for-publishing}

要将视频发布到YouTube，Experience Manager会将标记与一个或多个YouTube渠道关联。 要添加标记以进行发布，请参阅 [管理标记](/help/sites-administering/tags.md).

或者，如果您打算在Experience Manager中使用默认标记，则可以跳过此任务并转到 [启用YouTube发布复制代理](#enabling-the-youtube-publish-replication-agent).

### 启用YouTube发布复制代理 {#enabling-the-youtube-publish-replication-agent}

启用YouTube发布复制代理后，如果要测试与Google Cloud帐户的连接，请点按 **[!UICONTROL 测试连接]**. 浏览器选项卡显示连接结果。 如果您已添加YouTube渠道，则测试中将显示渠道列表。

1. 单击Experience Manager左上角的Experience Manager徽标，然后在左边栏中，单击 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 复制]** > **[!UICONTROL 作者代理]**.
1. 在“创作代理”页面上，单击 **[!UICONTROL YouTube发布]**.
1. 在工具栏的“设置”右侧，单击 **[!UICONTROL 编辑]**.
1. 选择 **[!UICONTROL 已启用]** 复选框，以便您可以打开复制代理。
1. 单击&#x200B;**[!UICONTROL 确定]**。

   现在在Experience Manager中设置YouTube。

### 在Experience Manager中设置YouTube {#setting-up-youtube-in-aem}

从Experience Manager6.4开始，引入了一种新的触屏用户界面方法，以在Experience Manager中设置YouTube发布。 根据您正在使用的已安装的Experience Manager实例，执行以下操作之一：

* 要在6.4之前的Experience Manager中配置YouTube，请参阅 [在6.4之前的Experience Manager中设置YouTube](/help/assets/video.md#setting-up-youtube-in-aem-before).
* 要在Experience Manager6.4或更高版本中配置YouTube，请参阅 [在Experience Manager6.4及更高版本中设置YouTube](#setting-up-youtube-in-aem-and-later).

#### 在Experience Manager6.4及更高版本中设置YouTube {#setting-up-youtube-in-aem-and-later}

1. 确保以管理员身份登录到Dynamic Media实例。
1. 点按左上角的Experience Manager徽标，然后点按左边栏中的徽标 **[!UICONTROL 工具]**（锤子图标）> **[!UICONTROL Cloud Services]** > **[!UICONTROL YouTube发布配置]**.
1. 点按 **[!UICONTROL 全局]** （请勿选择它）。

1. 在全局页面的右上角附近，点按 **[!UICONTROL 创建]**.
1. 在“创建 YouTube 配置”页面的“Google Cloud Platform 设置”下的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   在之前最初配置Google Cloud设置时，您指定了项目ID。
将“创建YouTube配置”页面保持打开状态；稍后您将返回到它。

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. 使用纯文本编辑器，打开您之前在任务中下载并保存的JSON文件 [配置Google云设置](/help/assets/video.md#configuring-google-cloud-settings).
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 在页面的右上角附近，点按&#x200B;**[!UICONTROL 保存]**。

   现在在Experience Manager中设置YouTube渠道。

1. 点按 **[!UICONTROL 添加渠道]**.
1. 在渠道名称字段中，输入您在任务中创建的渠道的名称 **[!UICONTROL 向YouTube添加一个或多个渠道]** 更早。

   如果需要，您可以选择添加描述。

1. 点按 **[!UICONTROL 添加]**.
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择一个渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，点按 **[!UICONTROL 接受]** 以允许对此渠道的访问。

1. 点按 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Services> YouTube页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（上下颠倒的尖号），以便在Experience Manager中显示可用标记的列表。
1. 点按一个或多个标记，以便添加它们。

   要删除已添加的标记，请选择该标记，然后点按 **[!UICONTROL X]**.

1. 添加完所需的标记后，点按 **[!UICONTROL 保存]**.

   现在，您可以将视频发布到YouTube渠道。

#### 在6.4之前的Experience Manager中设置YouTube {#setting-up-youtube-in-aem-before}

1. 确保以管理员身份登录到Dynamic Media实例。

1. 点按左上角的Experience Manager徽标，然后点按左边栏中的徽标 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 部署]** > **[!UICONTROL Cloud Services]**.
1. 在“第三方服务”标题下方的YouTube下，点按 **[!UICONTROL 立即配置]**.
1. 在创建配置对话框中，在相应字段中输入标题（必需）和名称（可选）。
1. 点按&#x200B;**[!UICONTROL 创建]**。
1. 在“YouTube 帐户设置”对话框的&#x200B;**[!UICONTROL 应用程序名称]**&#x200B;字段中，输入 Google 项目 ID。

   您最初指定项目ID时 [已配置Google云设置](/help/assets/video.md#configuring-google-cloud-settings) 更早。
保持YouTube帐户设置对话框处于打开状态；稍后您将返回到该对话框。

1. 使用纯文本编辑器，打开您之前在配置Google Cloud设置任务中下载并保存的JSON文件。
1. 选择并复制整个JSON文本。
1. 返回至“YouTube 帐户设置”对话框。在 **[!UICONTROL JSON 配置]**&#x200B;字段中，粘贴 JSON 文本。
1. 点按 **[!UICONTROL 确定]**.

   现在在Experience Manager中设置YouTube渠道。

1. 在&#x200B;**[!UICONTROL 可用渠道]**&#x200B;右侧，点按 **+**（加号图标）。
1. 在“YouTube频道设置”对话框的“标题”字段中，输入您在之前向YouTube添加一个或多个频道任务中创建的频道 **[!UICONTROL 名称]** 。

   如果需要，您可以选择添加描述。

1. 点按 **[!UICONTROL 确定]**.
1. 将显示YouTube/Google身份验证。 如果您尚未登录Google Cloud帐户，请跳过此步骤。

   * 输入与Google项目ID关联的Google用户名和密码，以及上面的JSON文本。
   * 根据您的帐户有多少个渠道，您会看到两个或更多项目。 选择一个渠道。 不要选择电子邮件地址；它不是渠道。
   * 在下一页，点按 **[!UICONTROL 接受]** 以允许对此渠道的访问。

1. 点按 **[!UICONTROL 允许]**.

   现在设置标记以进行发布。

1. **[!UICONTROL 设置标记以进行发布]**  — 在Cloud Services> YouTube页面上，点按铅笔图标以编辑要使用的标记列表。
1. 点按下拉列表图标（上下颠倒的尖号），以便在Experience Manager中显示可用标记的列表。
1. 点按一个或多个标记，以便添加它们。

   要删除已添加的标记，请选择该标记，然后点按 **X**.

1. 添加完所需的标记后，点按 **[!UICONTROL 确定]**.

   现在，您可以将视频发布到YouTube渠道。

### （可选）自动为您上传的视频设置默认YouTube属性 {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

您可以选择通过在Experience Manager中创建元数据处理配置文件来在上传视频时自动设置YouTube属性。

要创建元数据处理配置文件，您首先需要从&#x200B;**[!UICONTROL 字段标签]**、**[!UICONTROL 映射到属性]**&#x200B;和&#x200B;**[!UICONTROL 选择]**&#x200B;字段中复制值，所有这些字段均位于视频的元数据架构中。然后，您可以通过向处理配置文件添加这些值来构建您的YouTube视频元数据处理配置文件。

要自动为您上传的视频设置默认YouTube属性，请执行以下操作：

1. 点按左上角的Experience Manager徽标，然后单击左边栏中的 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据架构]**.
1. 单击 **[!UICONTROL 默认]**. （请勿在“default”左侧的选择框中添加复选标记。）
1. 在 **[!UICONTROL 默认]** 页面，选中左侧的框 **[!UICONTROL 视频]**，然后点按 **[!UICONTROL 编辑]**.
1. 在元数据架构编辑器页面上，点按 **[!UICONTROL 高级]** 选项卡。
1. 在“YouTube 发布”标题下，单击 **[!UICONTROL YouTube 类别]**。
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制您要使用的默认值（例如“人员和博客”或“科学与技术”）。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在YouTube Publishing标题下，点按 **[!UICONTROL YouTube隐私]**.
1. 在页面的右侧，在 **[!UICONTROL 设置]** 选项卡，执行以下操作：

   * 在 **[!UICONTROL 映射到属性]** 文本字段，选择并复制值。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

   * 下 **[!UICONTROL 选项]**，选择并复制要使用的默认值。 请注意，“选择”分为两组。 该对中的底部字段是您要复制的默认值，如public、unlisted或private。
将复制的值粘贴到打开的文本编辑器中。 稍后创建元数据处理配置文件时，您将需要此值。 保持文本编辑器处于打开状态。

1. 在“元数据架构编辑器”页面的右上角附近，单击 **[!UICONTROL 取消]**.
1. 点按Experience Manager左上角的Experience Manager徽标，然后单击左边栏中的 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 元数据配置文件]**.

1. 在元数据配置文件页面右上角附近，单击 **[!UICONTROL 创建]**.
1. 在“添加元数据配置文件”对话框的&#x200B;**[!UICONTROL 配置文件]**&#x200B;文本字段中，输入名称 `YouTube Video`，然后单击&#x200B;**[!UICONTROL 创建]**。
1. 在元数据配置文件编辑器页面上，单击 **[!UICONTROL 前进]** 选项卡。
1. 通过执行以下操作，将复制的YouTube发布值添加到配置文件中：

   * 在页面的右侧，单击 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为的组件 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Publishing`.
   * 单击 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube发布]** 您创建的标题。

   * 单击 **[!UICONTROL 字段标签]** 这样即会选中该组件。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 通过执行以下操作，将复制的YouTube隐私值添加到用户档案：

   * 在页面的右侧，单击 **[!UICONTROL 构建表单]** 选项卡。
   * （可选）拖动标记为的组件 **[!UICONTROL 章节标题]** 左侧，并将其放入表单区域。
   * （可选）单击 **[!UICONTROL 字段标签]** 以选择组件。
   * （可选）在页面右侧的设置选项卡下，在字段标签文本字段中输入 `YouTube Privacy`.
   * 单击 **[!UICONTROL 构建表单]** 选项卡，然后拖动标记为的组件 **[!UICONTROL 多值文本]** 然后将其放在 **[!UICONTROL YouTube隐私]** 您创建的标题。

   * 单击 **[!UICONTROL 字段标签]** 这样即会选中该组件。
   * 在页面的右侧，在“设置”选项卡下方，将您之前复制的YouTube发布值（字段标签值和映射到属性值）粘贴到表单上各自的字段中。 将“选项”值粘贴到“默认值”字段中。

1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 保存]**。
1. 将YouTube发布元数据配置文件应用到要上传视频的文件夹。 您必须同时设置元数据配置文件和视频配置文件。

   请参阅 [元数据配置文件](/help/assets/metadata-config.md#metadata-profiles) 和视 [频配置文件](/help/assets/video-profiles.md)。

### 将视频发布到您的YouTube渠道 {#publishing-videos-to-your-youtube-channel}

现在，您可以将之前添加的标记关联到视频资产。 此过程可告知Experience Manager要发布到YouTube渠道的资产。

>[!NOTE]
>
>在Dynamic Media - Scene7模式下运行时，不会立即发布自动发布到YouTube。 在设置Dynamic Media - Scene7模式时，有两种发布选项可供选择： **[!UICONTROL 立即]** 或 **[!UICONTROL 激活时]**.
>
>**[!UICONTROL 立即发布]** 这意味着上传的资产（与IPS同步后）会自动发布到投放系统。 虽然这对Dynamic Media是这样，但对YouTube不是这样。 要发布到YouTube，您必须通过Experience Manager创作进行发布。

>[!NOTE]
>
>要从YouTube发布内容，Experience Manager使用 **[!UICONTROL 发布到YouTube]** 工作流，用于监视进度和查看任何故障信息。
>
>参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>有关更详细的进度信息，您可以在复制下监视YouTube日志。 但是，请注意，此类监视需要管理员访问权限。

**要将视频发布到您的 YouTube 频道，请执行以下操作：**

1. 在Experience Manager中，导航到要发布到YouTube渠道的视频资源。
1. 选择视频资产（自适应视频集）。
1. 在工具栏上，单击 **[!UICONTROL 属性]**.
1. 在基本选项卡的元数据标题下，单击 **[!UICONTROL 打开选择对话框]** 标记字段的右侧。
1. 在“选择标记”页面上，导航到要使用的标记，然后选择一个或多个标记。

   请记住，标记必须与YouTube渠道关联。

1. 在页面的右上角，单击 **[!UICONTROL 选择]**.
1. 在视频属性页面的右上角，单击 **[!UICONTROL 保存并关闭]**.
1. 在工具栏上，单击 **[!UICONTROL 快速发布]**.

   另请参阅 [在Experience Manager Sites中使用发布管理](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   您可以选择在YouTube渠道中验证已发布的视频。

### （可选）验证YouTube上发布的视频 {#optional-verifying-the-published-video-on-youtube}

您可以选择监视YouTube发布（或取消发布）的进度。

参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

发布时间会因多种因素而有很大的差异，这些因素包括主源视频的格式、文件大小和上传流量。 发布过程所需的时间少则几分钟，多则几小时，这些情况都有可能出现。此外，更高分辨率格式的渲染速度要慢得多。 例如，720p和1080p的出现时间比480p长。

8小时后，如果您仍然看到一条状态消息，显示 **[!UICONTROL 已上传（正在处理，请稍候）]**，请尝试从Adobe的网站中移除视频并重新上传。

### 将YouTube URL链接到您的Web应用程序 {#linking-youtube-urls-to-your-web-application}

您可以获取Dynamic Media在发布视频后生成的YouTube URL字符串。 在复制该 YouTube URL 时，它会进入“剪贴板”，以便您能够视需要将其粘贴到网站或应用程序中的页面。

>[!NOTE]
>
>只有在将视频资产发布到 YouTube 后，才可复制其 YouTube URL。

**要将 YouTube URL 关联到您的 Web 应用程序，请执行以下操作：**

1. 导航到 *YouTube已发布* 要复制其URL的视频资源，然后选择它。

   请记住，YouTube URL仅可供复制 *之后* 您拥有 *已发布* 将视频资源载入YouTube。

1. 在工具栏上，单击 **[!UICONTROL 属性]**.
1. 单击 **[!UICONTROL 高级]** 选项卡。
1. 在YouTube发布标题下方的YouTube URL列表中，选择URL文本，然后将其复制到Web浏览器，以预览资源或添加到Web内容页面。

### 取消发布视频，以便从YouTube中删除它们 {#unpublishing-videos-to-remove-them-from-youtube}

当您在 Experience Manager 中取消发布视频资产时，该视频会从 YouTube 中删除。

>[!CAUTION]
>
>如果直接从YouTube中删除视频，则Experience Manager不会察觉，并继续像视频仍发布到YouTube那样行事。 始终通过Experience Manager从YouTube取消发布视频资源。

>[!NOTE]
>
>要从YouTube中删除内容，Experience Manager使用 **[!UICONTROL 从YouTube取消发布]** 工作流，用于监视进度和查看任何故障信息。
>
>参见 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress).

**要取消发布视频以将其从 YouTube 中删除，请执行以下操作：**

1. 导航到要从YouTube渠道取消发布的视频资源。
1. 在资产选择模式下，选择一个或多个已发布的视频资产。
1. 在工具栏上，单击 **[!UICONTROL 管理发布]**. 点按三个圆点图标(...) 工具栏上，因此 **[!UICONTROL 管理发布]** 打开。
1. 在管理发布页面上，点按 **[!UICONTROL 取消发布]**.
1. 在页面的右上角，点按 **[!UICONTROL 下一个]**.
1. 在页面的右上角，点按 **[!UICONTROL 取消发布]**.

## 监控视频编码和YouTube发布进度 {#monitoring-video-encoding-and-youtube-publishing-progress}

在将新视频上传到应用了视频编码的文件夹或将视频发布到YouTube时，您可以监控视频编码/Youtube发布的进展情况。 实际的YouTube发布进度只能通过日志获得。 但是，以下过程中介绍的其他方式会列出其失败或成功。 此外，当YouTube发布工作流或视频编码完成或中断时，您会收到电子邮件通知。

### 监测进度 {#monitoring-progress}

1. 在assets文件夹中查看视频编码进度：

   * 在卡片视图中，视频编码进度按百分比显示在资源上。 如果出现错误，资产上也会显示此信息。

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * 在列表视图中，视频编码进度显示在 **[!UICONTROL 处理状态]** 列。 如果出现错误，则同一列中将显示此消息。

   ![chlimage_1-430](assets/chlimage_1-430.png)

   默认情况下，此列不显示。要启用该列，请从视图下拉菜单中选择&#x200B;**[!UICONTROL 查看设置]**，然后添加&#x200B;**[!UICONTROL 处理状态]**&#x200B;列，然后点按或单击&#x200B;**[!UICONTROL 更新]**。

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. 在资源详细信息中查看进度。 点按或单击资产时，打开下拉菜单并选择 **[!UICONTROL 时间线]**. 要将其缩小到编码或YouTube发布等工作流活动，请选择 **[!UICONTROL 工作流]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   任何工作流信息（如编码）都会显示在时间轴中。 对于YouTube发布，工作流时间轴还包括YouTube渠道的名称和YouTube视频URL。 此外，发布完成后，您会在工作流时间轴中看到任何失败通知。

   >[!NOTE]
   >
   >由于上的多个工作流配置，最终记录失败/错误可能需要较长时间 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 起始日期 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >    * Apache Sling作业队列配置
   >    * AdobeGranite工作流外部进程作业处理程序
   >    * Granite工作流超时队列

   >
   >您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关进行中的工作流，请参阅“工具”>“工作流” **[!UICONTROL >“实例”中提供的“工作流实例]** ” **[!UICONTROL (Workflow]** ) **[!UICONTROL >“]**&#x200B;实例”。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   选择实例并点按 **[!UICONTROL 打开历史记录]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   从“工作流实例”区域，您还可以暂停、终止或重命名工作流。 参见 [管理工作流](/help/sites-administering/workflows-administering.md) 了解更多信息。

1. 有关失败的作业，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 失败]**&#x200B;中显示的“工作流失败”。**[!UICONTROL 工作流失败]**&#x200B;列出所有失败的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >由于上的多个工作流配置，最终记录错误消息可能需要较长时间 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 起始日期 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)例如：
   >
   >
   >
   >    * Apache Sling作业队列配置
   >    * AdobeGranite工作流外部进程作业处理程序
   >    * Granite工作流超时队列

   >
   >
   >您可以调整 **[!UICONTROL 重试]**， **[!UICONTROL 重试延迟]**、和 **[!UICONTROL timeout]** 属性。

1. 有关已完成的工作流，请参阅&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 存档]**&#x200B;中的可用工作流存档。**[!UICONTROL 工作流存档]**&#x200B;列出了所有已完成的工作流活动。

   >[!NOTE]
   >
   >您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 您会收到有关已中止或失败的工作流作业的电子邮件通知。 这些电子邮件通知可由管理员配置。 参见 [配置电子邮件通知](#configuring-e-mail-notifications).

#### 配置电子邮件通知 {#configuring-e-mail-notifications}

>[!NOTE]
>
>您需要管理权限才能访问 **[!UICONTROL 工具]** 菜单。

配置通知的方式取决于您是要接收编码作业还是YouTube发布作业的通知：

* 对于编码作业，您可以在以下位置访问所有Experience Manager工作流电子邮件通知的配置页面： **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 并通过搜索 **[!UICONTROL Day CQ工作流电子邮件通知服务]**. 参见 [在Experience Manager中配置电子邮件通知](/help/sites-administering/notification.md). 您可以选中或清除复选框 **[!UICONTROL 中止时通知]** 或 **[!UICONTROL 完成时通知]** 相应地。

* 对于YouTube发布作业，请执行以下操作：

1. 在Experience Manager中，点按 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.
1. 在“工作流模型”页面上，选择 **[!UICONTROL 发布到YouTube]**，然后点按 **[!UICONTROL 编辑]** 工具栏上。
1. 在“发布到YouTube”工作流页面的右上角附近，点按 **[!UICONTROL 编辑]**.
1. 将鼠标指针悬停在YouTube上传组件上，然后点按一次以显示内联工具栏。

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. 在内联工具栏上，点按配置图标（扳手）。 单击 **[!UICONTROL 参数]** 选项卡。

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. 在YouTube上传流程 — 步骤属性对话框中，点按 **[!UICONTROL 参数]** 选项卡。

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. 您可以选中或清除以下复选框：

   * 发布开始
   * 发布失败
   * 发布完成 — 包含有关渠道和URL的信息

   清除复选框表示您不会从YouTube Publish工作流收到指定的电子邮件通知。

   >[!NOTE]
   >
   >这些电子邮件特定于YouTube，是通用工作流电子邮件通知的补充。 因此，您可以收到两套电子邮件通知，即中提供的通用通知 **[!UICONTROL Day CQ工作流电子邮件通知服务]** 以及特定于YouTube的一个插件，具体取决于您的配置设置。

1. 完成后，在对话框的右上角附近，点按 **[!UICONTROL 完成]** 图标（复选标记）。
1. 在发布到YouTube工作流页面的右上角附近，点按 **[!UICONTROL 同步]**.

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报表仅在运行Dynamic Media — 混合模式时可用。

视频报表会显示指定时间内的多个聚合量度，以帮助您监控*已发布*单个和聚合视频是否按预期执行。 以下顶级量度数据是您整个网站中所有已发布视频的汇总数据。

* 视频开始
* 完成率
* 视频花费的平均时间
* 视频花费的总时间
* 每次访问的视频数

报表中还会列出包含所有&#x200B;*已发布*&#x200B;视频的表格，以便您能够根据视频开始的总次数，跟踪您网站上最常观看的视频。

点按列表中的视频名称时，会以折线图的形式显示视频的受众维系（流失）报表。该图表显示在视频播放期间任何给定时间的查看次数。在播放视频时，垂直条与播放器中的时间指示器同步跟踪。折线图数据中的下降指示受众从无兴趣到何时消失。

如果视频是在 Adobe Experience Manager Dynamic Media 外部编码的，就不会提供受众保留（流失）图表和表中的播放比例数据。

另请参阅 [配置Dynamic MediaCloud Services](/help/assets/config-dynamic.md).

>[!NOTE]
>
>跟踪和报告数据完全基于Dynamic Media自己的视频播放器及相关视频播放器预设的使用。因此，您无法跟踪和报告通过其他视频播放器播放的视频。

默认情况下，首次输入视频报表时，该报表显示从当前月份的第一天开始到当前月份的日期结束的视频数据。但是，您可以通过指定自己的日期范围来覆盖默认日期范围。下次输入视频报表时，将使用指定的日期范围。

为了使视频报表正常工作，会在配置Dynamic MediaCloud Services时自动创建报表包ID。同时，报表包ID会推送到发布服务器，以便在您预览资产时可用于复制URL功能。 但是，此功能要求已设置发布服务器。 如果未设置发布服务器，您仍可以发布以查看视频报表。 但是，您必须返回到Dynamic Media云配置并点按 **[!UICONTROL 确定]**.

**要查看视频报表，请执行以下操作：**

1. 点按Experience Manager左上角的Experience Manager徽标，然后点按左边栏中的徽标 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 视频报表]**.
1. 在“视频报表”页面中，执行以下任一操作：

   * 在右上角附近，点按&#x200B;**刷新视频报表**图标。
仅当报表的结束日期为当天时，才使用刷新。 这样做可确保您查看自上次运行报表以来发生的视频跟踪。

   * 在右上角附近，点按 **日期选取器** 图标。指定要获取其视频数据的开始和结束日期范围，然后点按 **[!UICONTROL 运行报告]**.

   “顶级量度”组框标识您网站中所有&#x200B;*已发布*&#x200B;视频的各种汇总测量数据。

1. 在列出最热门发布的视频的表中，点按视频名称以播放视频，还可以查看视频的受众维系（流失）报表。

### 查看基于您使用Dynamic Media HTML5查看器SDK创建的视频查看器的视频报表 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

如果您使用Dynamic Media提供的开箱即用视频查看器，或者您基于开箱即用视频查看器创建了自定义查看器预设，则无需执行其他步骤即可查看视频报表。 但是，如果您已根据HTML5 Viewer SDK API创建自己的视频查看器，则请使用以下步骤确保视频查看器向Dynamic Media视频报表发送跟踪事件。

使用 [AdobeDynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) 和 [HTML5查看器SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 创建自己的视频查看器。

**要查看基于您使用Dynamic Media HTML5查看器SDK创建的视频查看器的视频报表，请执行以下操作：**

1. 导航到任意已发布的视频资产。
1. 在资产页面的左上角附近，从下拉列表中选择&#x200B;**[!UICONTROL 查看器]**。
1. 选择任意视频查看器预设，并复制嵌入代码。
1. 在嵌入代码中，找到包含以下内容的代码行：

   `videoViewer.setParam("config2", "<value>");`

   此 `config2` 参数可在HTML5查看器中启用跟踪。 它还是一个特定于公司的预设，其中包含用于视频报表的配置信息，以及用于特定于客户的Adobe Analytics配置的信息。

   config2 参数的正确值可在&#x200B;**[!UICONTROL 嵌入代码]**&#x200B;和复制 **[!UICONTROL URL]** 函数中找到。在复制 **[!UICONTROL URL]** 命令的 URL 中，要查找的参数为 `&config2=<value>`。该值几乎总是 `companypreset`，但在某些情况下，也可以是 `companypreset-1`、`companypreset-2` 等。

1. 在您的自定义视频查看器代码中，通过执行以下操作，将 AppMeasurementBridge.jsp 添加到查看器页面：

   * 首先，确定您是否需要 `&preset` 参数。

      如果 `config2` 参数为 `companypreset`，您需要 *非* 需要 `&preset=parameter`.

      如果 `config2` 是其他任何内容，请将预设参数设置为与 `config2` 参数相同。例如，如果 `config2=companypreset-2`，添加 `&param2=companypreset-2` 到AppMeasurementBridge.jsp URL。

   * 然后，添加AppMeasurementBridge.jsp脚本：

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 通过执行以下操作，创建 TrackingManager 组件：

   * 在您调用之后 `s7sdk.Util.init();`，通过添加以下内容创建TrackingManager实例以跟踪事件：

      `var trackingManager = new s7sdk.TrackingManager();`

   * 通过执行以下操作将组件连接到TrackingManager：

      在 `s7sdk.Event.SDK_READY` 事件处理程序，将您要跟踪的组件附加到TrackingManager。

      例如，如果组件为 `videoPlayer`，添加

      `trackingManager.attach(videoPlayer);`

      以将组件附加到trackingManager。 要跟踪页面上的多个查看器，请使用多个跟踪管理器组件。

   * 通过添加以下内容创建AppMeasurementBridge对象：

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 通过添加以下内容来添加跟踪函数：

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   appMeasurementBridge 对象具备内置的跟踪功能。但是，您可以提供自己的对象来支持多个跟踪系统或其他功能。

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## 向视频添加隐藏式字幕或字幕 {#adding-captions-to-video}

通过将隐藏式字幕添加到单个视频或自适应视频集，您可以将视频扩展到全球市场。 通过添加隐藏式字幕，您无需对音频进行混音，也无需使用母语人士重新录制每种语言的音频。 视频以所录制的语言播放。 出现外语字幕是为了让不同语言的人仍然能够理解音频部分。

隐藏式字幕还可以让耳聋或听力缺佳的用户更容易使用。

>[!NOTE]
>
>您使用的视频播放器必须支持显示字幕。

另请参阅 [Dynamic Media中的辅助功能](/help/assets/accessibility-dm.md).

Dynamic Media将字幕文件转换为JSON（JavaScript对象表示法）格式。 此转换意味着，您可以将JSON文本作为隐藏但完整的视频转录内容嵌入到网页中。 然后，搜索引擎可以对内容进行爬网和索引，以使视频更容易被发现，并为客户提供有关视频内容的更多详细信息。

参见 [提供静态（非图像）内容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 在 *Dynamic Media图像服务和渲染API帮助* 有关在URL中使用JSON函数的更多信息。

**要在视频中添加字幕或字幕，请执行以下操作：**

1. 使用第三方应用程序或服务创建视频字幕/字幕文件。

   确保您创建的文件遵循WebVTT（Web视频文本跟踪）标准。 字幕文件扩展名为.vtt。 您可以了解有关WebVTT字幕标准的更多信息。

   参见 [WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/).

   在Dynamic Media之外，您可以使用免费和高级的工具和服务来创作题注/字幕文件。 例如，要创建不带样式的简单视频字幕文件，您可以使用以下免费的在线字幕创作和编辑工具：

   [WebVTT题注生成器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   为了获得最佳结果，请在Internet Explorer 9或更高版本、Google Chrome或Safari中使用该工具。

   在工具中， **[!UICONTROL 输入视频文件的URL]** 字段中，粘贴复制的视频文件URL，然后单击 **[!UICONTROL 加载]**. 参见 [获取资产的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 以获取视频文件本身的URL，然后您可以将其粘贴到 **[!UICONTROL 输入视频文件的URL字段]**. 随后，Internet Explorer、Chrome 或 Safari 可以本机播放视频。

   现在，按照站点中的屏幕说明创作并保存WebVTT文件。 完成后，复制字幕文件内容并将其粘贴到纯文本编辑器中，然后保存 `.vtt` 文件扩展名。

   >[!NOTE]
   >
   >为了在全球范围内支持多种语言的视频字幕，WebVTT标准要求您创建单独的.vtt文件，并为要支持的每种语言调用。

   通常，您希望将字幕VTT文件的名称与视频文件相同，并将其附加到语言区域设置，如 — EN、-FR或 — DE。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。

1. 在Experience Manager中，将您的WebVTT字幕文件上传到DAM。
1. 导航到 *已发布* 要与上传的字幕文件关联的视频资源。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   参见 [发布资产](/help/assets/publishing-dynamicmedia-assets.md).

1. 执行下列操作之一：

   * 要获得弹出式视频查看器体验，请点按 **[!UICONTROL URL]**. 在URL对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。 使用以下语法附加复制的视频URL：

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      请注意 `,1` 标题路径末尾。 紧跟在 `.vtt` 文件扩展名在路径中，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将 `,1` 或 `,0`，则不会显示任何内容。

   * 要获得嵌入式视频查看器体验，请点按 **[!UICONTROL 嵌入代码]**. 在“嵌入代码”对话框中，选择，然后将嵌入代码复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 使用以下语法附加复制的嵌入代码：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      请注意 `,1` 标题路径末尾。 紧跟在 `.vtt` 文件扩展名在路径中，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将 `,1` 或 `,0`，则不会显示任何内容。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

您可以通过将章节标记添加到单个视频或自适应视频集，使长格式视频更容易观看和导航。 当用户播放视频时，他们可以单击视频时间轴上的章节标记（也称为视频洗刷器）以轻松导航到其目标点。 或者，他们可以立即跳转到新内容、演示和教程。

>[!NOTE]
>
>使用的视频播放器必须支持使用章节标记。 Dynamic Media视频播放器支持章节标记，但使用第三方视频播放器可能不支持。

如果需要，您可以创建自己的自定义视频查看器，并将其品牌化为章节，而不是使用视频查看器预设。 有关通过章节导航创建您自己的HTML5查看器的说明，请在AdobeHTML5查看器SDK API中，引用类下的“使用修饰符自定义行为”标题 `s7sdk.video.VideoPlayer` 和 `s7sdk.video.VideoScrubber`. 请参阅 [HTML5查看器SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 文档。

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

您可以像创建字幕一样为视频创建章节列表。 即，创建一个WebVTT文件。 但请注意，此文件必须与您也在使用的任何WebVTT字幕文件分开；不能将字幕和章节合并到一个WebVTT文件中。

您可以使用以下示例作为使用章节导航创建WebVTT文件时所使用的格式示例：

### 包含视频章节导航的WebVTT文件 {#webvtt-file-with-video-chapter-navigation}

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

在上面的示例中， `Chapter 1` 是提示标识符，并且是可选的。 的提示时间 `00:00:000 --> 01:04:364` 指定章节的开始时间和结束时间，单位为 `00:00:000` 格式。 最后三位数是毫秒，可保留为 `000`（如果首选）。 的章节标题 `The bicycle store behind it all` 是章节内容的实际描述。 当用户将鼠标指针悬停在视频时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器弹出窗口中。

由于您使用的是HTML5视频查看器，因此请确保您创建的章节文件遵循WebVTT（Web视频文本跟踪）标准。 章节文件扩展名为 `.vtt`. 您可以了解有关WebVTT字幕标准的更多信息。

参见 [WebVTT： Web视频字幕格式](https://w3c.github.io/webvtt/)

**要添加视频章节导航，请执行以下操作：**

1. 保存 `.vtt` 文件，以避免章节标题文本中的字符演绎版出现问题。

   通常，您希望将章节VTT文件的名称与视频文件相同，并附加章节。 这样，它可以帮助您使用现有Web内容管理系统自动生成视频URL。
1. 在Experience Manager中，上传WebVTT章节文件。

   请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>用于弹出视频查看器体验</td>
       <td>
       <ol>
       <li>导航到 <i>已发布 </i>要与上载的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅<a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产</a>。</li>
       <li>从下拉菜单中，单击或点按 <strong>查看器</strong>.</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频预览在单独的页面中打开。</li>
       <li>在左边栏的底部，单击 <strong>URL</strong>.</li>
       <li>在URL对话框中，选择URL并将其复制到剪贴板，然后将URL粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加复制的视频的URL，以便将其与复制的URL关联到章节文件：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>用于嵌入式视频查看器体验<br /> </td>
       <td>
       <ol>
       <li>导航到 <i>已发布 </i>要与上载的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅<a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产</a>。</li>
       <li>从下拉菜单中，单击或点按 <strong>查看器</strong>.</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频预览在单独的页面中打开。</li>
       <li>在左边栏的底部，单击 <strong>嵌入</strong>.</li>
       <li>在“嵌入代码”对话框中，选择并将整个代码复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>使用以下语法附加视频的嵌入代码，以便将其与复制的URL关联到章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## 关于Dynamic Media - Scene7模式中的视频缩略图 {#about-video-thumbnails-in-dynamic-media-scene-mode}

视频缩略图是视频帧的缩减版本，或者向客户表示视频的图像资产。 缩略图用于鼓励客户单击视频。

Experience Manager中的所有视频都必须有关联的缩略图；如果不替换缩略图，则无法删除缩略图。 默认情况下，将视频上传到Experience Manager时，会使用第一帧作为缩略图。 但是，您可以自定义缩略图，例如，用于品牌推广或视觉搜索目的。 自定义视频缩略图时，可以播放视频并在要使用的帧上暂停。 或者，您可以选择已上传的图像资产，并且 *已发布* 在您的数字资产管理器中。

您从视频中选择的自定义视频缩略图图像不会提取并保存在DAM中，作为单独的独特资产。 但是，您从现有图像资源中选择的自定义视频缩略图会保存到JCR中。 所选资源的路径将存储在视频资源的节点下，如以下示例路径所示：

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

自定义视频缩略图的功能仅在您将视频配置文件应用到视频所在的文件夹之后才可用。

另请参阅 [关于Dynamic Media — 混合模式中的视频缩略图](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail}

这些步骤仅适用于在“Dynamicmedia_Scene7”模式下运行的Dynamic Media。

**要添加自定义视频缩略图，请执行以下操作：**

1. 确保您已完成以下操作：

   * 已为您的视频资产创建文件夹。
   * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [已将您的视频上传到文件夹](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. 导航到要更改其缩略图图像的已上传视频资产。
1. 在资源选择模式下，可以从 **[!UICONTROL 列表视图]** 或 **[!UICONTROL 卡片视图]**，点按视频资产。
1. 在工具栏上，点按 **[!UICONTROL 属性]** 图标（一个圆圈，内有“i”）。
1. 在视频的“属性”页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在“更改缩略图”页面上，执行下列操作之一：

   * 要将视频中的帧用作新缩略图，请执行以下操作：

      * 在工具栏上，点按 **[!UICONTROL 从视频中选择帧]**.
      * 点按“播放”按钮，然后点按要捕获为视频新缩略图的帧上的“暂停”按钮。
   * 要将图像资源用作新缩略图，请执行以下操作：

      * 在工具栏上，点按 **[!UICONTROL 从资源中选择缩略图]**.
      * 点按 **[!UICONTROL 选择缩略图]**.
      * 导航到您想要使用的之前上传和发布的图像资产。 资源会自动调整大小以用作视频的缩略图。
      * 选择图像资源，然后点按 **[!UICONTROL 选择]**.


1. 在更改缩略图页面上，点按 **[!UICONTROL 保存更改]**.
1. 在视频的“属性”页面的右上角，点按 **[!UICONTROL 保存并关闭]**.

## 关于Dynamic Media — 混合模式中的视频缩略图 {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

您可以从Dynamic Media自动生成的十个缩略图图像中选择一个添加到视频中。 当视频资源在Experience Manager Sites、Experience Manager移动设备或Experience Manager Screens的创作环境中与Dynamic Media组件一起使用时，视频播放器会显示您选择的缩略图。 缩略图用作最能代表整个视频内容的静态图片，进一步鼓励用户单击“播放”按钮。

根据视频的总时间，Dynamic Media会捕获10个（默认）缩略图。 在视频中捕获的图像比例为1%、11%、21%、31%、41%、51%、61%、71%、81%和91%。 这10个缩略图仍然存在，这意味着如果您稍后决定选择其他缩略图，则无需重新生成系列。 您可以预览10个缩略图，然后选择要用于视频的缩略图。 如果要更改为默认值，可以使用CRXDE Lite配置生成缩略图图像的时间间隔。 例如，如果只想从视频中生成一系列四个等间距的缩略图，可以将间隔时间配置为24%、49%、74%和99%。

理想情况下，您可以在上传视频之后但在网站上发布视频之前随时添加视频缩略图。

如果您愿意，可以选择上传自定义缩略图来表示您的视频，而不是使用Dynamic Media生成的缩略图。 例如，您可以创建一个自定义缩略图图像，其中包含视频标题、引人注目的开场图像或从视频中捕获的特定图像。 您上传的自定义视频缩略图图像的最大分辨率必须为1280 x 720像素（最小宽度为640像素），并且不得大于2 MB。

另请参阅 [关于Dynamic Media - Scene7模式中的视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### 添加视频缩略图 {#adding-a-video-thumbnail}

这些步骤仅适用于以混合模式运行的Dynamic Media。

**要添加视频缩略图，请执行以下操作：**

1. 导航到要添加视频缩略图的已上传视频资产。
1. 在资产选择模式下，从“列表视图”或“卡片视图”中，点按视频资产。
1. 在工具栏上，点按 **[!UICONTROL 查看属性]** 图标（一个圆圈，内有“i”）。
1. 在视频的“属性”页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在更改缩略图页面的工具栏上，点按 **[!UICONTROL 选择帧]**.

   Dynamic Media会根据您自定义的默认时间间隔或时间间隔，从视频中生成一系列缩略图图像。

1. 预览生成的缩略图图像，然后选择要添加到视频中的图像。
1. 点按 **[!UICONTROL 保存更改]**.

   视频的缩略图图像会更新以使用您选择的缩略图。 如果您稍后决定更改缩略图图像，则可以返回到 **[!UICONTROL 更改缩略图]** 页面并选择新页面。

   如果您配置了新的默认时间间隔，或者您上传了一个新视频来替换现有视频，则由Dynamic Media重新生成缩略图。

   参见 [配置生成视频缩略图的默认时间间隔](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### 配置生成视频缩略图的默认时间间隔 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

当您配置和保存新的默认时间间隔时，所做的更改只会自动应用于您将来上传的视频。 它不会自动将新的默认设置应用于您之前上传的视频。 对于现有视频，必须重新生成缩略图。

参见 [添加视频缩略图](#adding-a-video-thumbnail).

**要配置生成视频缩略图的默认时间间隔，请执行以下操作：**

1. 在Experience Manager中，点按 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

1. 在“CRXDE Lite”页面的左侧目录面板中，导航到 `o etc/dam/imageserver/configuration/jcr:content/settings.`

   如果目录面板不可见，请点按“主页”选项卡左侧的>>图标。

1. 在右下面板的“属性”选项卡中，双击 `thumbnailtime`.
1. 在 **[!UICONTROL 编辑缩略图]** 对话框中，使用文本字段以百分比形式输入间隔值。

   * 如果要添加一个或多个间隔值字段，请点击加号(+)图标。 如有必要，请滚动到对话框的底部以查看图标。
   * 如果要从列表中删除间隔值字段，请点击其右侧的减号(-)图标。
   * 如果要重新排序间隔值，请点按向上箭头图标和向下箭头图标。

1. 点按 **[!UICONTROL 确定]** 并返回到“属性”选项卡。
1. 在“CRXDE Lite”页面的左上角附近，点按 **[!UICONTROL 全部保存]**，然后点按左上角的“返回主页”图标以返回Experience Manager。

   参见 [添加视频缩略图](#adding-a-video-thumbnail).

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail-1}

这些步骤仅适用于以混合模式运行的Dynamic Media。

**要添加自定义视频缩略图，请执行以下操作：**

1. 导航到要添加自定义视频缩略图的已上传视频资产。
1. 在资产选择模式下，从“列表视图”或“卡片视图”中，点按视频资产。
1. 在工具栏上，点按 **[!UICONTROL 查看属性]** 图标（一个圆圈，内有“i”）。
1. 在视频的“属性”页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在更改缩略图页面的工具栏上，点按 **[!UICONTROL 上传新的缩略图]**.
1. 导航到要使用的缩略图图像，选择它，然后点按 **[!UICONTROL 打开]** 以开始将图像上传到Experience Manager。 上传后，请确保发布图像。
1. 成功上传和发布图像后，在更改缩略图页面中，点按 **[!UICONTROL 保存更改]**.

   自定义缩略图将会添加到您的视频中。

## 更改Dynamic Media资源的Dynamic Media URL {#manifest-urls}

处理到Dynamic Media中的视频可以通过现成的查看器使用，也可以直接访问清单URL并通过您自己的自定义查看器播放它们。 以下是获取视频清单URL的API。

### 关于getVideoManifestURI API

此 `getVideoManifestURI`API通过c公开`q-scene7-api:com.day.cq.dam.scene7.api` 和可用于生成以下清单URL：

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### getVideoManifestURI API参数

此API采用以下三个参数：

| 参数 | 描述 |
| --- | --- |
| `resource` | 与Dynamic Media已摄取的视频对应的资源。 |
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果清单URI仅在投放层上发布且可用时生成，则设置为true。 |

要使用上述方法获取视频的清单URL，请添加 [视频编码配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 到“上传视频”文件夹。 Dynamic Media会根据在分配给文件夹的视频编码文件中找到的编码来处理这些视频。 现在，您可以调用上述API以获取已上传视频的清单URL。

### 错误方案

如果出现错误，则API返回null。 异常记录在Experience Manager错误日志中。 所有此类记录错误都开始于 `Could not generate Video Manifest URI`. 以下情况可能会导致出现此类错误：

* An `IllegalArgumentException` 因以下任一情况被记录：

   * 此 `resource` 传递的参数为null。
   * 此 `resource` 传递的参数不是视频。
   * 此 `manifestType` 传递的参数为null。
   * 此 `onlyIfPublished` 参数作为true传递，但视频未发布。
   * 未使用Dynamic Media中的自适应视频集摄取视频。

* `IOException` 在连接到Dynamic Media时出现问题时记录。
* `UnsupportedOperationException` 在以下情况下被记录： `manifestType` 传递的参数为 `ManifestType.DASH`，而视频尚未使用DASH格式进行处理。

以下是使用中编写的servlet的上述API示例 *HTTPWhiteBoard* 规范。 选择每个选项卡以了解代码语法。

>[!BEGINTABS]

>[!TAB 在pom.xml中添加依赖项]

+++**在pom.xml中添加依赖项**

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB 示例servlet]

+++**示例servlet**

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB servlet的响应类]

+++**servlet的响应类**

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB servlet中引用的常量文件]

+++**servlet中引用的常量文件**

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext**

使用装载上述servlet `servletContext`. 以下示例为 `servletContext`.

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]

### 使用示例servlet

通过执行 `GET` 操作位置 `/dmSample/dynamicmedia/video/manifestUrl`. 传递了以下查询参数：

| 查询参数 | 描述 |
| --- | --- |
| `assetPath` | 强制. 针对以下项访问视频的路径： `manifestUrl` 生成。 |
| `manifestType` | 可选。参数可以是DASH或HLS。 如果未传递，则默认为DASH。 |
| `onlyIfPublished` | 可选。如果通过， `manifestUrl` 仅当发布视频时返回。 |

在本例中，我们假定进行以下设置：

* 公司是 `samplecompany`.
* 创作实例为 `http://sample-aem-author.com`.
* 文件夹 `/content/dam/video-example` 应用了视频编码配置文件。
* 视频 `scenery.mp4` 已上传到文件夹 `/content/dam/video-example`.

可以通过以下方式调用servlet：

| 类型 | 描述 |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>如果启用DASH投放：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>在禁用DASH投放的情况下：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| 短划线 | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>如果启用DASH投放：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>在禁用DASH投放的情况下：<br>`{}` |
| 错误：资源路径错误 | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


