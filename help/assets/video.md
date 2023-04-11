---
title: Dynamic Media 中的视频
description: 了解如何在Dynamic Media中处理视频，例如，对视频进行编码、将视频发布到YouTube以及查看视频报表的最佳实践。 还了解如何向视频添加隐藏式字幕、字幕或章节标记。
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
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '8098'
ht-degree: 3%

---

# Dynamic Media 中的视频 {#video}

本节介绍如何在Dynamic Media中处理视频。

## 快速入门：视频 {#quick-start-videos}

以下工作流分步描述旨在帮助您在Dynamic Media中快速设置并运行自适应视频集。 在每个步骤之后，都会对主题标题进行交叉引用，您可以在其中找到更多信息。

>[!IMPORTANT]
>
>在Dynamic Media中处理视频之前，请确保Adobe Experience Manager管理员已在Dynamic Media - Scene7模式或Dynamic Media — 混合模式中启用并配置了Dynamic MediaCloud Services。
>
>* 请参阅 [配置Dynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) 配置Dynamic Media - Scene7模式和 [Dynamic Media - Scene7模式故障诊断](/help/assets/troubleshoot-dms7.md).
>
>* 请参阅 [配置Dynamic MediaCloud Services](/help/assets/config-dynamic.md#configuring-dynamic-media-cloud-services) 在配置Dynamic Media — 混合模式中。
>
>Dynamic Media中当前已知的视频播放问题 *仅在Experience Manager6.5.9.0上*:
>
>* 如果已发布的视频已更新，则必须再次发布该视频，以反映投放时的更改。
>


1. **上传Dynamic Media视频** 通过执行以下操作：

   * 创建您自己的视频编码配置文件。 或者，您只需使用预定义的 _自适应视频编码_ Dynamic Media的个人资料。

      * [创建视频编码配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * 详细了解 [视频编码最佳实践](#best-practices-for-encoding-videos).
   * 将视频处理配置文件关联到一个或多个要在其中上传主要源视频的文件夹。

      * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).
      * 详细了解 [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).
      * 详细了解 [组织数字资产](/help/assets/organize-assets.md).
   * 将主源视频上传到文件夹。 将视频添加到文件夹后，这些视频会根据您分配给文件夹的视频处理配置文件进行编码。

      * Dynamic Media主要支持长度最长为30分钟且最小分辨率大于25 x 25的短格式视频。
      * 您可以上传每个最大15 GB的视频文件。
      * [上传视频](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).
      * 详细了解 [支持的输入文件格式](/help/assets/assets-formats.md#supported-multimedia-formats).
   * 监控方式 [视频编码正在进行中](#monitoring-video-encoding-and-youtube-publishing-progress) 从资产或工作流视图。




1. **管理Dynamic Media视频** 执行以下任一操作：

   * 组织、浏览和搜索视频资产

      * [组织数字资产](/help/assets/organize-assets.md)
详细了解 [组织数字资产以使用处理配置文件的最佳实践](organize-assets.md)

      * [搜索视频资产](search-assets.md#custompredicates) 或 [搜索资产](/help/assets/search-assets.md)
   * 预览和发布视频资产

      * 查看源视频以及视频的编码演绎版及其关联的缩略图：
         [预览视频](managing-video-assets.md#upload-and-preview-video-assets) 或 [预览资产](previewing-assets.md)
         [查看视频演绎版](video-renditions.md)
         [管理视频演绎版](manage-assets.md#managing-renditions)

      * [管理查看器预设](managing-viewer-presets.md)
      * [发布资产](publishing-dynamicmedia-assets.md)
   * 使用视频元数据

      * 查看编码视频呈现的属性，如帧速率、音频和视频比特率以及编解码器：
         [查看视频演绎版属性](video-renditions.md)

      * 编辑视频的属性，如标题、描述和标记、自定义元数据字段：
         [编辑视频属性](manage-assets.md#editing-properties)

      * [管理数字资产的元数据](metadata.md)
      * [元数据架构](metadata-schemas.md)
   * 审阅、批准和批注视频，以及维护完全版本控制

      * [在视频中添加批注](managing-video-assets.md#annotate-video-assets) 或 [在资产中添加批注](manage-assets.md#annotating)

      * [创建一个版本](manage-assets.md#asset-versioning)
      * [将工作流应用于资产](assets-workflow.md) 或查看 [在资产上启动工作流](manage-assets.md#starting-a-workflow-on-an-asset)

      * [审核文件夹资产](bulk-approval.md)
      * [项目](../sites-authoring/projects.md)




1. **发布Dynamic Media视频** 执行下列操作之一：

   * 如果您将Adobe Experience Manager用作Web内容管理系统，则可以将视频直接添加到您的网页。

      * [将视频添加到网页](adding-dynamic-media-assets-to-pages.md).
   * 如果您使用的是第三方Web内容管理系统，则可以将视频链接或嵌入到您的网页。

      * 使用URL集成视频：
         [将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md).

      * 使用网页上的嵌入代码集成视频：
         [在网页上嵌入视频查看器](embed-code.md).
   * [将视频发布到YouTube](#publishing-videos-to-youtube).
   * [生成视频报表](#viewing-video-reports).

   * [在视频中添加字幕](#adding-captions-to-video).



## 在Dynamic Media中处理视频 {#working-with-video-in-dynamic-media}

Dynamic Media中的视频是一个端到端解决方案，它可以轻松发布高质量自适应视频，以便在多个屏幕(包括台式机、iOS、Android™、BlackBerry®和Windows移动设备)上进行流播放。 自适应视频集是同一视频的一组版本，这些版本以不同的比特率和格式进行编码，如400 kbps、800 kbps和1000 kbps。 台式计算机或移动设备会检测可用带宽。

例如，在iOS移动设备上，它会检测到3G、4G或Wi-Fi等带宽。 然后，它会自动从自适应视频集中的各种视频比特率中选择正确的编码视频。 视频会流式传输到台式机、移动设备或平板电脑。

此外，如果桌面或移动设备上的网络条件发生更改，则会自动动态切换视频质量。 此外，如果客户在桌面上进入全屏模式，自适应视频集将使用更好的分辨率做出响应，从而改善客户的观看体验。 对于在多个屏幕和设备上播放Dynamic Media视频的客户，使用自适应视频集可以为您提供最佳的播放方式。

视频播放器在播放期间用于确定要播放或要选择的编码视频的逻辑，基于以下算法：

1. 视频播放器根据与播放器本身中为“初始比特率”设置的值最接近的比特率来加载初始视频片段。
1. 视频播放器根据带宽速度的更改使用以下条件进行切换：

   1. 播放器会选取低于或等于估计带宽的最高带宽流。
   1. 播放器仅考虑可用带宽的80%。 但是，如果它正在切换，则更为保守，仅为70%，以避免过高估计并立即切换回来。

有关算法的详细技术信息，请参阅 [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

要管理单个视频和自适应视频集，支持以下操作：

* 从多种支持的视频格式和音频格式上传视频，并将视频编码为MP4 H.264格式，以便在多个屏幕中播放。 您可以使用预定义的自适应视频预设和单个视频编码预设，或自定义您自己的编码以控制视频的质量和大小。

   * 生成自适应视频集时，它将包含MP4视频。
   * **注意**:主控/源视频未添加到自适应视频集。

* 在所有HTML5视频查看器中设置视频字幕。
* 使用完整的元数据支持组织、浏览和搜索视频，以有效管理视频资产。
* 将自适应视频集交付到Web和桌面，以及移动设备，包括iPhone、iPad、Android™、BlackBerry®和Windows手机。

各种iOS平台均支持自适应视频流播放。 请参阅 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference.html#video).

Dynamic Media支持为MP4 H.264视频播放移动设备视频。 您可以在以下位置找到支持此视频格式的BlackBerry®设备： [BlackBerry®上支持的视频格式](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

您可以在以下位置找到支持此视频格式的Windows设备： [Windows Phone 8支持的媒体编解码器](https://learn.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs)



* 使用Dynamic Media视频查看器预设播放视频，包括以下内容：

   * 单个视频查看器。
   * 结合了视频和图像内容的混合媒体查看器。

* 配置视频播放器以满足您的品牌需求。
* 使用简单的URL或嵌入代码将视频集成到您的网站、移动设备网站或移动设备应用程序。

<!-- See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

另请参阅 [Experience Manager Assets和Dynamic Media Classic查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html#viewers-aem-assets-dmc) 和 [仅用于Experience Manager资产的查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

## 最佳实践：使用HTML5视频查看器 {#best-practice-using-the-html-video-viewer}

Dynamic MediaHTML5视频查看器预设是强大的视频播放器。 您可以使用它们来避免与HTML5视频播放相关的许多常见问题。 此外，还存在与移动设备相关的问题，例如缺少自适应比特率流传输以及桌面浏览器访问范围有限。

在播放器的设计方面，您可以使用标准Web开发工具来设计视频播放器的功能。 例如，您可以使用HTML5和CSS设计按钮、控件和自定义海报图像背景，以帮助您通过自定义外观联系客户。

在查看器的播放端，查看器会自动检测浏览器的视频功能。 然后，它使用HLS（HTTP实时流）或DASH（通过HTTP的动态自适应流）（也称为自适应比特率流）来提供视频。 或者，如果这些投放方法不存在，则改用HTML5渐进式。

通过将以下内容组合到单个播放器中：

* 使用HTML5和CSS设计播放组件的功能
* 嵌入了播放
* 根据浏览器的功能使用自适应流和渐进式流

您可以将富媒体内容的访问范围扩展到桌面用户和移动设备用户，并确保简化视频体验。

另请参阅 [关于HTML5查看器](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers.html#viewers-for-aem-assets-only).

### 在台式计算机和移动设备上使用HTML5视频查看器播放视频 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

对于桌面和移动设备自适应视频流播放，用于比特率切换的视频基于自适应视频集中的所有MP4视频。

使用短划线或HLS或渐进式视频下载进行视频播放。 在以前版本的Experience Manager（如6.0、6.1和6.2）中，视频通过HTTP进行流处理。

在Experience Manager6.3及更高版本中，视频现在通过HTTPS（即DASH或HLS）进行流式传输，因为DM网关服务URL也始终使用HTTPS。 此默认行为不会对客户造成任何影响。 也就是说，视频流始终通过HTTPS进行，除非浏览器不支持。 （请参阅下表）。 因此，

* 如果您的HTTPS网站使用HTTPS视频流，则可以进行流播放。
* 如果您的HTTP网站使用HTTPS视频流，则流处理可以正常进行，并且Web浏览器中不会出现混合内容问题。

DASH是国际标准，HLS是Apple标准。 这两种方法都用于自适应视频流播放。 而且，这两种技术都可根据网络带宽容量自动调整播放。 它还允许客户“搜寻”视频中的任意点，而无需等待视频的其余部分下载。

通过在用户的桌面系统或移动设备上本地下载和存储视频来传送渐进式视频。

下表介绍了使用Dynamic Media视频查看器在台式计算机和移动设备上播放视频的设备、浏览器和方法。

<table>
 <tbody>
  <tr>
   <td><strong>设备</strong></td>
   <td><strong>浏览器</strong></td>
   <td><strong>视频播放模式</strong></td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 9和10</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Internet Explorer 11+</td>
   <td>在Windows 8和Windows 10上 — 请求DASH*或HLS时，强制使用HTTPS。 已知限制：HTTP on DASH*或HLS在此浏览器/操作系统组合中不起作用<br /> <br /> 在Windows 7上 — 渐进式下载。 使用标准逻辑选择HTTP与HTTPS协议。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 23-44</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Firefox 45或更高版本</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>铬黄</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>桌面</td>
   <td>Safari(Mac)</td>
   <td>HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(Android™ 6或更早版本)</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(Android™ 7或更高版本)</td>
   <td>DASH*或HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Android™（默认浏览器）</td>
   <td>渐进式下载。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Safari(iOS)</td>
   <td>HLS自适应比特率流。</td>
  </tr>
  <tr>
   <td>移动设备</td>
   <td>Chrome(iOS)</td>
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
>*要对视频使用DASH，必须先由您帐户上的Adobe技术支持人员启用。 请参阅 [在您的帐户上启用短划线](#enable-dash).

## Dynamic Media视频解决方案的架构 {#architecture-of-dynamic-media-video-solution}

下图显示了视频的整体创作工作流程，这些视频通过DMGateway(在Dynamic Media混合模式下)上传和编码，并可供公众使用。

![chlimage_1-427](assets/chlimage_1-427.png)

## 视频的混合发布架构 {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## 视频编码最佳实践 {#best-practices-for-encoding-videos}

的 **Dynamic Media编码视频** 如果您已启用Dynamic Media并设置了视频云服务，则工作流会对视频进行编码。 此工作流会捕获工作流进程历史记录和失败信息。请参阅 [监控视频编码和YouTube发布进度](#monitoring-video-encoding-and-youtube-publishing-progress). 如果您已启用Dynamic Media并设置了视频云服务，则 **[!UICONTROL Dynamic Media编码视频]** 在您上传视频时，工作流会自动生效。 (如果您没有使用Dynamic Media，则 **[!UICONTROL DAM更新资产]** 工作流生效。)

<!-- DEAD The following are best-practice tips for encoding source video files.

For advice about video encoding, see [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en).

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en). -->

### 源视频文件 {#source-video-files}

在对视频文件进行编码时，请使用尽可能高质量的源视频文件。 避免使用之前编码的视频文件，因为这些文件已经压缩，而进一步编码会创建质量欠佳的视频。

* Dynamic Media主要支持长度最长为30分钟且最小分辨率大于25 x 25的短格式视频。
* 您可以上载每个最大15 GB的主源视频文件。

下表描述了源视频文件在编码之前必须具有的推荐大小、宽高比和最小比特率：

| 大小 | 宽高比 | 最小比特率 |
|--- |--- |--- |
| 1024 X 768 | 4:3 | 4500 kbps，适用于大多数视频。 |
| 1280 X 720 | 16:9 | 3000 - 6000 kbps，具体取决于视频中的运动量。 |
| 1920 X 1080 | 16:9 | 6000 - 8000 kbps，具体取决于视频中的运动量。 |

### 获取文件的元数据 {#obtaining-a-file-s-metadata}

您可以通过以下方法获取文件的元数据：使用视频编辑工具查看文件的元数据，或使用为获取元数据而设计的应用程序。 以下是有关使用第三方应用程序MediaInfo获取视频文件元数据的说明：

1. 转到 [MediaInfo下载](https://mediaarea.net/en/MediaInfo/Download).
1. 选择并下载GUI版本的安装程序，然后按照安装说明操作。
1. 安装后，右键单击视频文件（仅限Windows）并选择“媒体信息”，或打开“媒体信息”并将视频文件拖到应用程序中。 您会看到与视频文件关联的所有元数据，包括其宽度、高度和fps。

### 宽高比 {#aspect-ratio}

在为主源视频文件选择或创建视频编码预设时，请确保预设的宽高比与主源视频文件的宽高比相同。 宽高比是视频宽度与高度的比率。

要确定视频文件的宽高比，请获取文件的元数据并记下文件的宽度和高度（请参阅上面的获取文件的元数据）。 然后，使用下式确定宽高比：

宽高=宽高比

下表描述了公式结果如何转换为常见的宽高比选项：

| 公式结果 | 宽高比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例如，宽度为1440 x 1080的视频的宽高比为1440/1080或1.33。在这种情况下，请选择宽高比为4:3的视频编码预设，以对视频文件进行编码。

### 比特率 {#bitrate}

比特率是经过编码，构成视频播放一秒的数据量。 比特率以千比特每秒(Kbps)为单位进行测量。

>[!NOTE]
>
>由于所有编解码器都使用有损压缩，因此比特率是视频质量中最重要的因素。 使用有损压缩时，对视频文件的压缩越多，质量就降低得越多。 因此，所有其他特性（分辨率、帧速率和编解码器）均相等，比特率越低，压缩文件的质量就越低。

选择比特率编码时，可以选择以下两种类型：

* **[!UICONTROL 恒定比特率编码]** (CBR) — 在CBR编码期间，比特率或每秒比特数在整个编码过程中保持不变。 CBR编码会在整个视频中将设置的数据速率保留为您的设置。 此外，CBR编码不会为质量优化媒体文件，但会节省存储空间。
如果您的视频在整个视频中包含相似的运动级别，则使用CBR。 CBR最常用于流式传输视频内容。 另请参阅 [使用自定义添加的视频编码参数](/help/assets/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL 可变比特率编码]** (VBR)- VBR编码根据压缩程序所需的数据，将数据速率调低并调整到您设置的上限。 此功能意味着在VBR编码过程中，媒体文件的比特率会根据媒体文件的比特率需求动态增加或减少。
VBR需要较长的编码时间，但会产生最有利的结果；媒体文件的质量优于其他文件。 VBR最常用于视频内容的http渐进式交付。

何时使用VBR与CRB?
选择VBR与CBR时，几乎总是建议将VBR用于媒体文件。 VBR以具有竞争力的比特率提供高质量文件。 使用VBR时，请务必对两遍编码进行使用，并将最大比特率设置为目标视频比特率的1.5倍。

选择视频编码预设时，请记住目标最终用户的连接速度。 选择数据率为该速度80%的预设。 例如，如果目标最终用户的连接速度为1000 Kbps，则最佳预设是视频数据率为800 Kbps的预设。

此表描述了典型连接速度的数据率。

| 速度(Kbps) | 连接类型 |
|--- |--- |
| 256 | 拨号连接。 |
| 800 | 典型的移动连接。 对于此连接，为3G体验定位数据率（范围为400到最大800）。 |
| 2000 | 典型的宽带桌面连接。 对于此连接，目标数据率范围为800-2000 Kbps，大多数目标数据率平均为1200-1500 Kbps。 |
| 5000 | 典型的高宽带连接。 不建议在此上限范围内进行编码，因为大多数用户无法以此速度进行视频交付。 |

### 解决方法 {#resolution}

**分辨率** 以像素为单位描述视频文件的高度和宽度。 大多数源视频以高分辨率存储（例如，1920 x 1080）。 出于流播放目的，源视频会压缩为较小的分辨率（640 x 480或更低）。

分辨率和数据率是决定视频质量的两个相互关联的因素。 要保持相同的视频质量，视频文件中的像素数越高（分辨率越高），数据率就必须越高。 例如，请考虑分辨率为320 x 240和分辨率为640 x 480的视频文件中每帧的像素数：

| 解决方法 | 每帧像素数 |
|--- |--- |
| 320 x 240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480文件的每帧像素数是原来的四倍。 为了使这两个示例分辨率的数据率保持相同，您需要对640 x 480文件应用四倍的压缩，这会降低视频质量。 因此，250 Kbps的视频数据率在320 x 240分辨率下，而在640 x 480分辨率下，会产生高质量的观看效果。

通常，您使用的数据率越高，视频外观越好，使用的分辨率越高，您必须保持查看质量的数据率就越高（与分辨率较低的数据相比）。

由于分辨率和数据率是相关的，因此在对视频进行编码时有两个选项可供选择：

* 选择一个数据率，然后以在所选数据率中看起来不错的最高分辨率进行编码。
* 选择一个分辨率，然后按所需的数据速率进行编码，以便以您选择的分辨率获得高质量视频。

当您为主源视频文件选择（或创建）视频编码预设时，请使用此表来确定正确的分辨率：

| 解决方法 | 高度(像素) | 屏幕大小 |
|--- |--- |--- |
| 240p | 240 | 小屏幕 |
| 300p | 300 | 通常用于移动设备的小屏幕 |
| 360p | 360 | 小屏幕 |
| 480p | 480 | 中型屏幕 |
| 720p | 720 | 大屏幕 |
| 1080p | 1080 | 高清大屏幕 |

### Fps（每秒帧数） {#fps-frames-per-second}

在美国和日本，大多数视频以29.97帧/秒(fps)的速度拍摄；在欧洲，大多数视频以25 fps的速率拍摄。 电影以24 fps的速率拍摄。

选择与主源视频文件的fps速率匹配的视频编码预设。 例如，如果主源视频的帧数为25 fps，请选择25 fps的编码预设。 默认情况下，所有自定义编码都使用主源视频文件的fps。 因此，在创建视频编码预设时，您无需明确指定fps设置。

### 视频编码维度 {#video-encoding-dimensions}

为获得最佳结果，请选择编码维度，以便源视频是所有编码视频的整数倍。

要计算此比率，请将源宽度除以编码宽度，得到宽度比。 然后，将源高度除以编码高度，得到高度比。

如果生成的比率是整数，则表示视频已得到最佳缩放。 如果生成的比率不是整数，则会通过在显示器上留下残留像素伪影来影响视频质量。 当视频包含文本时，此效果最为明显。

例如，假定源视频为1920 x 1080。 在下表中，三个编码视频提供了要使用的最佳编码设置。

| 视频类型 | 宽x高 | 宽度比例 | 高度比 |
|--- |--- |--- |--- |
| 源 | 1920x1080 | 1 | 1 |
| 已编码 | 960 x 540 | 2 | 2 |
| 已编码 | 640 x 360 | 3 | 3 |
| 已编码 | 480 x 270 | 4 | 4 |

### 编码视频文件格式 {#encoded-video-file-format}

Dynamic Media建议使用MP4 H.264视频编码预设。 由于MP4文件使用H.264视频编解码器，因此它提供高质量视频，但文件大小已压缩。

### 在您的帐户上启用短划线 {#enable-dash}

DASH（HTTP上的数字自适应流播放）是视频流播放的国际标准，在不同的视频查看器中得到广泛采用。 在您的帐户上启用短划线后，您可以选择从短划线或HLS中选择自适应视频流播放。 或者，您可以在 **[!UICONTROL 自动]** 在“查看器预设”中选择作为播放类型。

在您的帐户中启用DASH的一些主要优势包括：

* 包含用于自适应比特率流播放的短划线流视频。 这种方法可提高投放效率。 自适应流播放可确保为客户提供最佳的观看体验。
* 使用Dynamic Media播放器优化的流播放在HLS和DASH流之间切换，以确保最佳服务质量。 当使用Safari浏览器时，视频播放器会自动切换到HLS。
* 您可以通过编辑视频查看器预设来配置首选的流播放方法（HLS或DASH）。
* 优化的视频编码可确保在启用短划线功能时不使用额外存储。 为HLS和DASH创建一组视频编码，以优化视频存储成本。
* 帮助让客户更易于访问视频交付。
* 也可以通过API获取流URL。

   >[!IMPORTANT]
   >
   >目前，在您的帐户上启用DASH仅在亚太和北美地区提供；即将在欧洲 — 中东 — 非洲推出。

在您的帐户中启用DASH需要两个步骤：

* 将Dynamic Media配置为使用DASH，您可以轻松自己执行该操作。
* 配置Experience Manager6.5以使用DASH，DASH是通过您创建并提交的Adobe客户支持案例来完成的。

**要在您的帐户上启用DASH，请执行以下操作：**

1. **配置Dynamic Media**  — 在Experience Manager6.5的Dynamic Media中，导航到 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 搜索 **AEM Assets Dynamic Media视频高级流** 功能标记。
1. 选中此复选框可启用（打开）短划线。
1. 选择&#x200B;**[!UICONTROL 保存]**。
1. **配置Experience Manager6.5** - [使用Admin Console开始创建新的支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html).
1. 按照相关说明创建支持案例，同时确保提供以下信息：

   * 主要联系人姓名、电子邮件、电话。
   * 您的Dynamic Media帐户的名称。
   * 指定希望在Experience Manager6.5中启用短划线。

1. Adobe客户支持根据请求提交顺序将您添加到DASH客户等待列表。
1. 当Adobe准备好处理您的请求时，客户支持团队会联系您，以协调并设置启用短划线的目标日期。
1. 客户支持部门在完成后会通知您。
1. 创建 [视频查看器预设](/help/assets/managing-viewer-presets.md#creating-a-new-viewer-preset) 和往常一样。

## 查看视频报表 {#viewing-video-reports}

>[!NOTE]
>
>视频报表仅在运行Dynamic Media — 混合模式时可用。

视频报表显示指定时间内的多个汇总量度，以帮助您监控 *发布* 单个视频和聚合视频将按预期执行。 以下热门量度数据是针对整个网站中所有已发布视频的汇总数据：

* 视频开始
* 完成率
* 视频平均逗留时间
* 视频播放总时间
* 每次访问视频数

全部表格 *发布* 视频也会列出，以便您可以根据视频开始总数跟踪网站上查看次数最多的视频。

当您点按列表中的视频名称时，它将以折线图形式显示视频的受众保留（下拉）报表。 该图表显示视频播放期间任何给定时刻的查看次数。 播放视频时，垂直条会与播放器中的时间指示器同步跟踪。 折线图数据中的数据显示受众因不感兴趣而停止观看的位置。

如果视频是在Adobe Experience Manager Dynamic Media之外进行编码，则将不提供受众保留（流失）图表和表中的播放百分比数据。

另请参阅 [配置Dynamic MediaCloud Services](/help/assets/config-dynamic.md).

>[!NOTE]
>
>跟踪和报告数据完全基于使用Dynamic Media自己的视频播放器和关联的视频播放器预设。 因此，您无法跟踪和报告通过其他视频播放器播放的视频。

默认情况下，在您首次进入视频报表时，报表会显示从当月的第一个开始到当月日期结束的视频数据。 但是，您可以通过指定您自己的日期范围来覆盖默认日期范围。 下次输入视频报表时，将使用您指定的日期范围。

为了使视频报表正常工作，在配置Dynamic MediaCloud Services时会自动创建报表包ID。 同时，报表包ID会被推送到发布服务器，以便在预览资产时，该ID可用于复制URL功能。 但是，此功能要求发布服务器已经设置。 如果未设置发布服务器，您仍可以通过发布查看视频报表。 但是，您必须返回到Dynamic Media云配置，然后点按 **[!UICONTROL 确定]**.

**要查看视频报表，请执行以下操作：**

1. 点按Experience Manager左上角的Experience Manager徽标，然后点按左边栏中的 **[!UICONTROL 工具]** （锤子图标）> **[!UICONTROL 资产]** > **[!UICONTROL 视频报表]**.
1. 在“视频报表”页面上，执行以下操作之一：

   * 在右上角附近，点按 **刷新视频报表** 图标。
仅当报表的结束日期为当天时，才使用“刷新”。 这样做可确保您查看自上次运行报表以来发生的视频跟踪。

   * 在右上角附近，点按 **日期选取器** 图标。
指定您希望视频数据的开始和结束日期范围，然后点按 **[!UICONTROL 运行报表]**.

   “热门量度”组框标识所有 *发布* 视频。

1. 在列出热门已发布视频的表中，点按视频名称以播放视频，并查看视频的受众保留（流失）报表。

### 查看基于您使用Dynamic Media HTML5查看器SDK创建的视频查看器的视频报表 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

如果您使用Dynamic Media提供的现成视频查看器，或者如果您基于现成视频查看器创建了自定义查看器预设，则无需执行其他步骤即可查看视频报表。 但是，如果您基于Adobe Viewer SDK API创建了自己的视频查看器，请执行以下步骤以确保您的视频查看器将跟踪事件发送到Dynamic Media视频报表。

使用 [AdobeDynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources.html) 和 [HTML5查看器SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 创建您自己的视频查看器。

**要查看基于您使用Dynamic Media HTML5查看器SDK创建的视频查看器的视频报表，请执行以下操作：**

1. 导航到任何已发布的视频资产。
1. 在资产页面的左上角附近，从下拉列表中选择&#x200B;**[!UICONTROL 查看器]**。
1. 选择任意视频查看器预设并复制嵌入代码。
1. 在嵌入代码中，找到包含以下内容的行：

   `videoViewer.setParam("config2", "<value>");`

   的 `config2` 参数可在HTML5查看器中启用跟踪。 它还是一个特定于公司的预设，其中包含视频报表的配置信息以及特定于客户的Adobe Analytics配置。

   config2 参数的正确值可在&#x200B;**[!UICONTROL 嵌入代码]**&#x200B;和复制 **[!UICONTROL URL]** 函数中找到。在复制 **[!UICONTROL URL]** 命令的 URL 中，要查找的参数为 `&config2=<value>`。该值几乎总是 `companypreset`，但在某些情况下，也可以是 `companypreset-1`、`companypreset-2` 等。

1. 在自定义视频查看器代码中，通过执行以下操作，将AppMeasurementBridge .jsp添加到查看器页面：

   * 首先，确定您是否需要 `&preset` 参数。

      如果 `config2` 参数为 `companypreset`, *not* 需要 `&preset=parameter`.

      如果 `config2` 为其他任何内容，请将预设参数设置为与 `config2` 参数。 例如，如果 `config2=companypreset-2`，添加 `&param2=companypreset-2` 到AppMeasurementBridge.jsp URL。

   * 然后，添加AppMeasurementBridge.jsp脚本：

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 通过执行以下操作，创建TrackingManager组件：

   * 在您调用 `s7sdk.Util.init();`，通过添加以下内容创建一个TrackingManager实例以跟踪事件：

      `var trackingManager = new s7sdk.TrackingManager();`

   * 通过执行以下操作，将组件连接到TrackingManager:

      在 `s7sdk.Event.SDK_READY` 事件处理程序，将要跟踪的组件附加到TrackingManager。

      例如，如果组件为 `videoPlayer`，添加

      `trackingManager.attach(videoPlayer);`

      将组件附加到trackingManager。 要跟踪页面上的多个查看器，请使用多个跟踪管理器组件。

   * 通过添加以下内容，创建AppMeasurementBridge对象：

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 通过添加以下内容添加跟踪函数：

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   appMeasurementBridge对象具有内置的跟踪函数。 但是，您可以提供自己的，以支持多个跟踪系统或其他功能。

<!--    For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

## 在视频中添加隐藏式字幕或字幕 {#adding-captions-to-video}

您可以通过向单个视频或自适应视频集添加隐藏式字幕，将视频的覆盖范围扩展到全球市场。 通过添加隐藏式字幕，您无需对音频进行调音，也无需使用母语人士为每个不同语言重新录制音频。 视频以录制的语言播放。 出现外语字幕，使不同语言的人仍然能够理解音频部分。

隐藏式字幕还允许耳聋或听力欠佳的用户更方便地访问。

>[!NOTE]
>
>您使用的视频播放器必须支持字幕的显示。

另请参阅 [Dynamic Media中的辅助功能](/help/assets/accessibility-dm.md).

Dynamic Media将题注文件转换为JSON（JavaScript对象表示法）格式。 这种转换意味着您可以将JSON文本作为视频的隐藏但完整的记录嵌入到网页中。 然后，搜索引擎可以爬网并索引内容，以便更容易发现视频，并为客户提供有关视频内容的更多详细信息。

请参阅 [提供静态（非图像）内容](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents.html#image-serving-api) 在 *Dynamic Media图像提供和渲染API帮助* 有关在URL中使用JSON函数的更多信息。

**要在视频中添加字幕或字幕，请执行以下操作：**

1. 使用第三方应用程序或服务创建视频字幕/子标题文件。

   确保您创建的文件遵循WebVTT（Web视频文本跟踪）标准。 字幕文件扩展名为.vtt。 您可以了解有关WebVTT字幕标准的更多信息。

   请参阅 [WebVTT:Web视频文本跟踪格式](https://w3c.github.io/webvtt/).

   在Dynamic Media之外，您可以使用免费和优质的工具和服务来创作字幕/子标题文件。 例如，要创建不带样式的简单视频字幕文件，您可以使用以下免费的在线字幕创作和编辑工具：

   [WebVTT字幕制作器](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   为获得最佳结果，请使用Internet Explorer 9或更高版本、Google Chrome或Safari中的工具。

   在工具中，在 **[!UICONTROL 输入视频文件的URL]** 字段中，粘贴复制的视频文件的URL，然后单击 **[!UICONTROL 加载]**. 请参阅 [获取资产的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset) 以获取视频文件的URL，然后您可以将其粘贴到 **[!UICONTROL 输入视频文件字段的URL]**. 随后，Internet Explorer、Chrome 或 Safari 可以本机播放视频。

   现在，按照网站上的屏幕说明来创作和保存您的WebVTT文件。 完成后，复制题注文件内容并将其粘贴到纯文本编辑器中，并使用 `.vtt` 文件扩展名为。

   >[!NOTE]
   >
   >为全球支持多种语言的视频字幕，WebVTT标准要求您为要支持的每种语言分别创建单独的.vtt文件和调用。

   通常，您要将字幕VTT文件命名为与视频文件同名，并附加语言区域设置，如 — EN、-FR或 — DE。 这样，您就可以使用现有的Web内容管理系统自动生成视频URL。

1. 在Experience Manager中，将WebVTT字幕文件上传到DAM。
1. 导航到 *发布* 要与您上传的题注文件关联的视频资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制 URL。

   请参阅 [发布资产](/help/assets/publishing-dynamicmedia-assets.md).

1. 执行下列操作之一：

   * 要获取弹出式视频查看器体验，请点按 **[!UICONTROL URL]**. 在“URL”对话框中，选择URL并将其复制到剪贴板，然后将该URL传递到简单的文本编辑器中。 使用以下语法附加复制的视频URL:

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      请注意 `,1` 标题路径的末尾。 紧跟 `.vtt` 文件名扩展名，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将设置为 `,1` 或 `,0`，分别为。

   * 要获取嵌入式视频查看器体验，请点按 **[!UICONTROL 嵌入代码]**. 在“嵌入代码”对话框中，选择嵌入代码，并将其复制到剪贴板，然后将该代码粘贴到简单的文本编辑器中。 将复制的嵌入代码附加以下语法：

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      请注意 `,1` 标题路径的末尾。 紧跟 `.vtt` 文件名扩展名，您可以选择启用（打开）或禁用（关闭）视频播放器栏上的隐藏式字幕按钮，方法是将设置为 `,1` 或 `,0`，分别为。

## 向视频添加章节标记 {#adding-chapter-markers-to-video}

您可以通过向单个视频或自适应视频集添加章节标记，来更轻松地观看和导航长形视频。 当用户播放视频时，他们可以单击视频时间轴上的章节标记（也称为视频清理器），以轻松导航到其目标点。 或者，他们可以立即跳转到新内容、演示和教程。

>[!NOTE]
>
>使用的视频播放器必须支持使用章节标记。 Dynamic Media视频播放器确实支持章节标记，但使用第三方视频播放器可能不支持。

如果需要，您可以创建带有章节的自定义视频查看器并为其添加品牌标识，而不是使用视频查看器预设。 有关使用章节导航创建您自己的HTML5查看器的说明，请在AdobeHTML5查看器SDK API中，引用类下的标题“使用修饰符自定义行为” `s7sdk.video.VideoPlayer` 和 `s7sdk.video.VideoScrubber`. 请参阅 [HTML5查看器SDK API](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html) 文档。

<!-- If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

为视频创建章节列表的方式与创建字幕的方式大致相同。 即，创建一个WebVTT文件。 但是，请注意，此文件必须与您同时使用的任何WebVTT字幕文件分开；不能将字幕和章节合并到一个WebVTT文件中。

您可以使用以下示例作为创建包含章节导航的WebVTT文件所使用的格式示例：

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

在上例中， `Chapter 1` 是提示标识符，是可选的。 的提示时间 `00:00:000 --> 01:04:364` 指定章节的开始时间和结束时间(在 `00:00:000` 格式。 最后三位是毫秒，可保留为 `000`，如果首选。 的章节标题 `The bicycle store behind it all` 是章节内容的实际描述。 当用户将鼠标指针悬停在视频时间轴中的可视提示点上时，提示标识符、开始提示时间和章节标题都会显示在视频播放器弹出窗口中。

由于您使用的是HTML5视频查看器，因此请确保您创建的章节文件遵循WebVTT（Web视频文本跟踪）标准。 章节文件扩展名为 `.vtt`. 您可以了解有关WebVTT字幕标准的更多信息。

请参阅 [WebVTT:Web视频文本跟踪格式](https://w3c.github.io/webvtt/)

**要添加视频章节导航，请执行以下操作：**

1. 保存 `.vtt` 文件，以避免章节标题文本中的字符呈现出现问题。

   通常，您需要使用与视频文件相同的名称命名章节VTT文件，并在其后附加章节。 这样，您就可以使用现有的Web内容管理系统自动生成视频URL。
1. 在Experience Manager中，上传您的WebVTT章节文件。

   请参阅 [上传资产](/help/assets/manage-assets.md#uploading-assets).

1. 执行下列操作之一：

   <table>
     <tbody>
      <tr>
       <td>用于弹出式视频查看器体验</td>
       <td>
       <ol>
       <li>导航到 <i>发布 </i>要与您上传的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅 <a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产。</a></li>
       <li>从下拉菜单中，单击或点按 <strong>查看器</strong>.</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频的预览将在单独的页面中打开。</li>
       <li>在左边栏的底部，单击 <strong>URL</strong>.</li>
       <li>在“URL”对话框中，选择URL并将其复制到剪贴板，然后将该URL传递到简单的文本编辑器中。</li>
       <li>将复制的视频URL附加以下语法，以便将其与复制的URL关联到您的章节文件：<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>对于嵌入式视频查看器体验<br /> </td>
       <td>
       <ol>
       <li>导航到 <i>发布 </i>要与您上传的章节文件关联的视频资产。 请注意，只有在首次<i>发布</i>资产<i>后</i>，才可复制 URL。请参阅 <a href="/help/assets/publishing-dynamicmedia-assets.md">发布资产。</a></li>
       <li>从下拉菜单中，单击或点按 <strong>查看器</strong>.</li>
       <li>在左边栏中，点按或单击视频查看器预设名称。 视频的预览将在单独的页面中打开。</li>
       <li>在左边栏的底部，单击 <strong>嵌入</strong>.</li>
       <li>在“嵌入代码”对话框中，选择整个代码，并将其复制到剪贴板，然后将其粘贴到简单的文本编辑器中。</li>
       <li>将视频的嵌入代码附加以下语法，以便将其与复制的URL关联到您的章节文件：<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>

## 关于Dynamic Media - Scene7模式中的视频缩略图 {#about-video-thumbnails-in-dynamic-media-scene-mode}

视频缩略图是视频帧或向客户展示视频的图像资产的缩小版本。 缩略图可鼓励客户单击视频。

Experience Manager中的所有视频都必须具有关联的缩略图；不替换缩略图，就无法删除缩略图。 默认情况下，当您将视频上传到Experience Manager时，第一帧将用作缩略图。 但是，您可以自定义缩略图以用于品牌策略或视觉搜索，例如。 自定义视频缩略图时，您可以播放视频并暂停要使用的帧。 或者，您也可以选择已上传的图像资产，并 *发布* 的子项。

您从视频中选择的自定义视频缩略图图像不会提取并保存在DAM中，作为单独且不重复的资产。 但是，您从现有图像资产中选择的自定义视频缩略图会保存到JCR。 与以下示例路径一样，选定资产的路径存储在视频资产的节点下：

`/content/dam/*<folder_name*>/<*video_name*>/jcr:content/manualThumbnail`

只有在将视频配置文件应用到视频所在的文件夹后，才能自定义视频缩略图。

另请参阅 [关于Dynamic Media — 混合模式中的视频缩略图](#about-video-thumbnails-in-dynamic-media-hybrid-mode).

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail}

这些步骤仅适用于在“Dynamicmedia_Scene7”模式下运行的Dynamic Media。

**要添加自定义视频缩略图，请执行以下操作：**

1. 确保您已经执行了以下操作：

   * 为您的视频资产创建了一个文件夹。
   * [将视频配置文件应用到文件夹](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   * [已将您的视频上传到文件夹](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

1. 导航到要更改其缩略图图像的已上传视频资产。
1. 在资产选择模式下，从 **[!UICONTROL 列表视图]** 或 **[!UICONTROL 卡片视图]**，点按视频资产。
1. 在工具栏中，点按 **[!UICONTROL 属性]** 图标（其中包含“i”的圆圈）。
1. 在视频的属性页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在“更改缩略图”页面上，执行下列操作之一：

   * 要将视频中的帧用作新缩略图，请执行以下操作：

      * 在工具栏中，点按 **[!UICONTROL 从视频中选择帧]**.
      * 点按播放按钮，然后点按要捕获的帧上的暂停按钮，作为视频的新缩略图。
   * 要将图像资产用作新缩略图，请执行以下操作：

      * 在工具栏中，点按 **[!UICONTROL 从资产中选择缩略图]**.
      * 点按 **[!UICONTROL 选择缩略图]**.
      * 导航到您之前上传和发布的要使用的图像资产。 资产会自动调整大小，以用作视频的缩略图。
      * 选择图像资产，然后点按 **[!UICONTROL 选择]**.


1. 在更改缩略图页面上，点按 **[!UICONTROL 保存更改]**.
1. 在视频的属性页面的右上角，点按 **[!UICONTROL 保存并关闭]**.

## 关于Dynamic Media — 混合模式中的视频缩略图 {#about-video-thumbnails-in-dynamic-media-hybrid-mode}

您可以从Dynamic Media自动生成的十个缩略图中选择一个，以将其添加到您的视频中。 当在Experience Manager Sites、Adobe Mobile或Experience Manager Screens的创作环境中将视频资产与Dynamic Media组件一起使用时，视频播放器会显示您选择的缩略图。 缩略图用作最能反映整个视频内容的静态图片，进一步鼓励用户单击“播放”按钮。

Dynamic Media会根据视频的总时间捕获十个（默认）缩略图图像。 在视频中，图像的捕获率为1%、11%、21%、31%、41%、51%、61%、71%、81%和91%。 这十个缩略图会一直保留，这意味着如果您稍后决定选择其他缩略图，则无需重新生成该系列。 您预览十个缩略图图像，然后选择要在视频中使用的缩略图。 如果要更改为默认设置，可以使用CRXDE Lite配置生成缩略图的时间间隔。 例如，如果您只想从视频中生成一系列间隔均匀的四幅缩略图图像，则可以将间隔时间配置为24%、49%、74%和99%。

理想情况下，您可以在上传视频后的任何时间，以及在网站上发布视频之前添加视频缩略图。

如果您愿意，可以选择上传自定义缩略图以表示您的视频，而不是使用由Dynamic Media生成的缩略图。 例如，您可以创建一个自定义缩略图图像，该缩略图图像的标题为视频、引人注目的开场图像或从视频中捕获的特定图像。 您上传的自定义视频缩略图图像的最大分辨率必须为1280 x 720像素（最小宽度为640像素）且不得大于2 MB。

另请参阅 [关于Dynamic Media - Scene7模式中的视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

### 添加视频缩略图 {#adding-a-video-thumbnail}

这些步骤仅适用于在混合模式下运行的Dynamic Media。

**要添加视频缩略图，请执行以下操作：**

1. 导航到您要添加视频缩略图的已上传视频资产。
1. 在资产选择模式下，从列表视图或卡片视图中，点按视频资产。
1. 在工具栏中，点按 **[!UICONTROL 查看属性]** 图标（其中包含“i”的圆圈）。
1. 在视频的属性页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在更改缩略图页面的工具栏中，点按 **[!UICONTROL 选择框架]**.

   Dynamic Media会根据您自定义的默认时间间隔或时间间隔，从您的视频生成一系列缩略图图像。

1. 预览生成的缩略图图像，然后选择要添加到视频中的缩略图。
1. 点按 **[!UICONTROL 保存更改]**.

   视频的缩略图图像会更新为使用您选择的缩略图。 如果您稍后决定更改缩略图图像，可以返回到 **[!UICONTROL 更改缩略图]** 页面，然后选择一个新页面。

   如果您配置了新的默认时间间隔，或者上传了新视频以替换现有视频，请让Dynamic Media重新生成缩略图。

   请参阅 [配置生成视频缩略图的默认时间间隔](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

#### 配置生成视频缩略图的默认时间间隔 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

当您配置并保存新的默认时间间隔时，您所做的更改会自动仅应用于您将来上传的视频。 它不会自动将新的默认设置应用于您之前上传的视频。 对于现有视频，必须重新生成缩略图。

请参阅 [添加视频缩略图](#adding-a-video-thumbnail).

**要配置生成视频缩略图的默认时间间隔，请执行以下操作：**

1. 在Experience Manager中，点按 **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL CRXDE Lite]**.

1. 在CRXDE Lite页面左侧的目录面板中，导航到 `o etc/dam/imageserver/configuration/jcr:content/settings.`

   如果未显示目录面板，请点按“主页”选项卡左侧的>>图标。

1. 在右下方的“属性”选项卡中，双击 `thumbnailtime`.
1. 在 **[!UICONTROL 编辑缩览图时间]** 框中，使用文本字段输入百分比的间隔值。

   * 如果要添加一个或多个间隔值字段，请点按加号(+)图标。 如有必要，请滚动到对话框底部以查看图标。
   * 如果要从列表中删除间隔值字段右侧的减号(-)图标。
   * 如果要重新排序间隔值，请点按向上箭头图标和向下箭头图标。

1. 点按 **[!UICONTROL 确定]** 并返回到属性选项卡。
1. 在CRXDE Lite页面的左上角附近，点按 **[!UICONTROL 全部保存]**，然后点按左上角的“返回主页”图标以返回Experience Manager。

   请参阅 [添加视频缩略图](#adding-a-video-thumbnail).

### 添加自定义视频缩略图 {#adding-a-custom-video-thumbnail-1}

这些步骤仅适用于在混合模式下运行的Dynamic Media。

**要添加自定义视频缩略图，请执行以下操作：**

1. 导航到您要添加自定义视频缩略图的已上传视频资产。
1. 在资产选择模式下，从列表视图或卡片视图中，点按视频资产。
1. 在工具栏中，点按 **[!UICONTROL 查看属性]** 图标（其中包含“i”的圆圈）。
1. 在视频的属性页面上，点按 **[!UICONTROL 更改缩略图]**.
1. 在更改缩略图页面的工具栏中，点按 **[!UICONTROL 上传新缩略图]**.
1. 导航到要使用的缩略图图像，将其选中，然后点按 **[!UICONTROL 打开]** 开始将图像上传到Experience Manager。 上传后，请确保发布图像。
1. 成功上传和发布图像后，在更改缩略图页面中，点按 **[!UICONTROL 保存更改]**.

   自定义缩略图会添加到您的视频中。

## 更改Dynamic Media资产的Dynamic Media URL {#manifest-urls}

处理到Dynamic Media中的视频可通过现成的查看器使用，也可以通过直接访问清单URL并通过您自己的自定义查看器播放它们。 以下是用于获取视频清单URL的API。

### 关于getVideoManifestURI API

的 `getVideoManifestURI`API通过c公开`q-scene7-api:com.day.cq.dam.scene7.api` 和可用于生成以下清单URL:

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
| `resource` | 与Dynamic Media摄取的视频对应的资源。 |
| `manifestType` | 可以是 `ManifestType.DASH` 或 `ManifestType.HLS` |
| `onlyIfPublished` | 如果清单uri仅在发布后且在投放层上可用时才生成，则设置为true。 |

要使用上述方法获取视频的清单URL，请添加 [视频编码配置文件](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 到“上传视频”文件夹。 Dynamic Media会根据在分配给文件夹的视频编码文件中找到的编码来处理这些视频。 现在，您可以调用上述API来获取上传视频的清单URL。

### 错误方案

如果存在错误，API将返回空值。 Experience Manager错误日志中记录了异常。 所有此类记录错误均以 `Could not generate Video Manifest URI`. 以下情况可能会导致出现此类错误：

* 安 `IllegalArgumentException` 将记录以下任一项：

   * 的 `resource` 传递的参数为null。
   * 的 `resource` 传递的参数不是视频。
   * 的 `manifestType` 传递的参数为null。
   * 的 `onlyIfPublished` 参数将作为true进行传递，但视频未发布。
   * 未使用从Dynamic Media中设置的自适应视频集摄取视频。

* `IOException` 在连接到Dynamic Media时出现问题时被记录。
* `UnsupportedOperationException` 在 `manifestType` 传递的参数 `ManifestType.DASH`，而视频未使用短划线格式进行处理。

以下是上述API使用中编写的Servlet的示例 *HTTPWhiteBoard* 规范。 为代码语法选择每个选项卡。

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

>[!TAB 示例Servlet]

+++**示例Servlet**

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

>[!TAB Servlet的响应类]

+++**Servlet的响应类**

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

>[!TAB Servlet中引用的常量文件]

+++**Servlet中引用的常量文件**

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

使用 `servletContext`. 以下示例 `servletContext`.

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

### 使用示例Servlet

通过执行 `GET` 操作 `/dmSample/dynamicmedia/video/manifestUrl`. 传递以下查询参数：

| 查询参数 | 描述 |
| --- | --- |
| `assetPath` | 强制. 视频的路径，其 `manifestUrl` 生成。 |
| `manifestType` | 可选. 参数可以是短划线或HLS。 如果未传递，则默认为DASH。 |
| `onlyIfPublished` | 可选. 如果通过，则 `manifestUrl` 仅在视频发布时返回。 |

在本例中，我们假定设置如下：

* 公司是 `samplecompany`.
* 创作实例为 `http://sample-aem-author.com`.
* 文件夹 `/content/dam/video-example` 应用了视频编码配置文件。
* 视频 `scenery.mp4` 已上传到文件夹 `/content/dam/video-example`.

您可以通过以下方式调用Servlet:

| 类型 | 描述 |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>如果启用了DASH投放：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>如果禁用DASH投放：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| 短划线 | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>如果启用了DASH投放：<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>如果禁用DASH投放：<br>`{}` |
| 错误：资产路径错误 | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |


