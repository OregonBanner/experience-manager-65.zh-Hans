---
title: 支持的文件格式和MIME类型
description: ' [!DNL Assets] and [!DNL Dynamic Media] 支持的文件格式和MIME类型以及每种格式支持的功能。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: eaff176bf3ffc197607b8eb39b15c1e945927f8e
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 22%

---


# [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}中支持的格式

[!DNL Experience Manager Assets] 支持各种文件格式，每种功能都对不同的MIME类型提供不同的支持。要将[!DNL Assets]与其他符合标准的数字资产管理(DAM)解决方案和桌面软件集成，请使用Adobe的[!DNL Extensible Metadata Platform](XMP)。

使用图例了解支持级别。

| 支持级别 | 描述 |
| :-----------: | ------------------------------ |
| 选定 | 支持 |
| * | 受支持，但需要附加功能 |
| - | 不适用 |

## [!DNL Experience Manager] {#supported-raster-image-formats}中支持的栅格图像格式

[!DNL Assets]中支持的栅格图像格式为：

| 格式 | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | 编辑 | 元数据写回 | 分析 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| GIF | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 |
| TIFF | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| JPEG | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| BMP | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 |
| PNM | 选定 | 选定 | - | - | - | - | 选定 |
| PGM | 选定 | 选定 | - | - | - | - | 选定 |
| PBM | 选定 | 选定 | - | - | - | - | 选定 |
| PPM | 选定 | 选定 | - | - | - | - | 选定 |
| PSD ‡ | 选定 | 选定 | 选定 | 选定 | - | - | 选定 |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | 选定 | 选定 | 选定 | - | 选定 | - |
| PICT | - | - | - | - | - | - | 选定 |
| PSB | 选定 | 选定 | 选定 | 选定 | - | - | - |

‡合并的图像从PSD文件中提取。 它是由Adobe Photoshop生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

[!DNL Dynamic Media]中支持的栅格图像格式为：

| 格式 | 上传<br>（输入格式） | 创建<br>图像<br>预设<br>（输出格式） | 预览<br>动态<br>再现 | 传送<br>动态<br>再现 | 下载<br> dynamic<br>再现 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | 选定 | 选定 | 选定 | 选定 | 选定 |
| GIF | 选定 | 选定 | 选定 | 选定 | 选定 |
| TIFF | 选定 | 选定 | 选定 | 选定 | 选定 |
| JPEG | 选定 | 选定 | 选定 | 选定 | 选定 |
| BMP | 选定 | - | - | - | - |
| PSD‡ | 选定 | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | 选定 | 选定 | 选定 | 选定 |
| PICT | 选定 | - | - | - | - |

‡合并的图像从PSD文件中提取。 它是由Adobe Photoshop生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

除上述信息外，请考虑以下事项：

* 对EPS文件的支持仅适用于栅格图像。 例如，默认不支持为 EPS 矢量图像生成缩略图。要添加支持，[配置ImageMagick](best-practices-for-imagemagick.md)。 要集成第三方工具以启用其他功能，请参阅[基于命令行的媒体处理程序](media-handlers.md#command-line-based-media-handler)。

* 将元数据写回添加到`NComm`处理函数时，它适用于PSB文件格式。

* 要使用[!DNL Dynamic Media]预览EPS文件并生成动态演绎版，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 对于EPS文件，PostScript文档结构约定(PS-Adobe)3.0版或更高版本支持元数据写回。

## 支持的3D格式{#support-3d-formats}

支持以下3D格式列表。

另请参阅[在Dynamic Media中使用3D资产。](/help/assets/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | 动态媒体投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | 选定 | 选定 | 选定 |  | 选定 | 选定 | - | - |
| gLB | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| gLTF | 选定 | 选定 | 选定 |  | 选定 | - | 选定 | - |
| OBJ | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| STL | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 | 选定 |
| USDz | 选定 | 选定 | 选定 | 选定 | 选定 | - | - | 选定 |

## Dynamic Media {#unsupported-image-formats-dynamic-media}中不支持的栅格图像格式

以下列表描述了Dynamic Media支持的&#x200B;*not*&#x200B;的栅格图像文件格式的子类型。

另请参阅[检测Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)不支持的文件格式。

* IDAT区块大小大于100 MB的PNG文件。
* PSB文件。
* 不支持色彩空间不是CMYK、RGB、灰度或位图的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* 位深度大于16的PSD文件。
* 具有浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEF file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## 支持的PDF光栅器库{#supported-pdf-rasterizer-library}

Adobe PDF光栅化器库为大型和内容密集型[!DNL Adobe Illustrator]和PDF文件生成高质量缩览图和预览。 Adobe建议对以下对象使用PDF光栅器库：

* 需要大量处理的资源的内容密集型AI/PDF文件。
* AI/PDF文件，默认情况下不生成缩略图。
* 具有Pantone Matching System(PMS)颜色的AI文件。

请参阅[使用PDF光栅器](aem-pdf-rasterizer.md)。

## 支持的图像转码库{#supported-image-transcoding-library}

Adobe成像转码库是一款图像处理解决方案，可执行核心图像处理功能，如编码、转码、重新取样和调整大小。

成像转码库支持JPG/JPEG、PNG（8位和16位）、GIF、BMP、TIFF/压缩TIFF（除32位TIFF文件和PTIFF文件外）、ICO和ICN MIME类型。

请参阅[成像转码库](imaging-transcoding-library.md)。

## 支持的相机原始数据{#supported-camera-raw}

[!DNL Adobe Camera Raw]库使[!DNL Assets]能够摄取原始图像。 请参阅[Camera Raw支持](camera-raw.md)。

## 支持的[!DNL Assets]文档格式{#supported-document-formats}

资产管理功能支持的文档格式如下：

| 格式 | 存储 | [元数据管理](metadata.md) | 全文<br>提取 | [元数据提取](metadata.md) | 缩略图<br>生成 | [子资产提取](managing-linked-subassets.md) | [元数据写回](xmp-writeback.md) | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | 选定 | - | 选定 | 选定 | 选定 | 选定 | - |
| DOC | 选定 | 选定 | 选定 | 选定 | - | - | - | 选定 |
| DOCX | 选定 | 选定 | 选定 | 选定 | - | - | - | 选定 |
| ODT | 选定 | 选定 | 选定 | - | - | - | - | 选定 |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| HTML | 选定 | 选定 | 选定 | - | - | - | - | 选定 |
| RTF | 选定 | 选定 | 选定 | - | - | - | - | 选定 |
| TXT | 选定 | 选定 | 选定 | - | - | - | - | 选定 |
| XLS | 选定 | 选定 | 选定 | - | - | - | - | 选定 |
| XLSX | 选定 | 选定 | 选定 | 选定 | - | - | - | 选定 |
| ODS | 选定 | 选定 | 选定 | - | - | - | - | - |
| PPT | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 |
| PPTX | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 | - | 选定 |
| ODP | 选定 | 选定 | 选定 | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | 选定 | 选定 | - | 选定 | 选定 | 选定 | 选定 | - |
| PS | 选定 | 选定 | - | - | - | - | - | - |
| QXP | 选定 | 选定 | - | - | - | - | - | - |
| EPUB | 选定 | 选定 | - | 选定 | 选定 | - | - | - |

## Dynamic Media {#supported-document-formats-dynamic-media}中支持的文档格式

| 格式 | 上传<br>（输入格式） | 创建<br>图像<br>预设<br>（输出格式） | 预览<br>动态<br>再现 | 传送<br>动态<br>再现 | 下载<br> dynamic<br>再现 |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | 选定 | 选定 | 选定 | 选定 | 选定 |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | 选定 | - | - | - | - |

除了上述功能之外，还要考虑以下事项：

* 要使用Dynamic Media为PDF文件生成动态演绎版，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media预览和生成AI文件的动态演绎版，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media为INDD文件生成动态演绎版，请参阅[InDesign(INDD)文件格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## 支持的多媒体格式{#supported-multimedia-formats}

|  | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | FFmpeg转码 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | 选定 | 选定 | - | - | * |
| MIDI | 选定 | 选定 | - | - | * |
| 3GP | 选定 | 选定 | - | - | * |
| MP3 | 选定 | 选定 | 选定 | - | * |
| MPG | 选定 | 选定 | - | - | * |
| OGA | 选定 | 选定 | - | - | * |
| OGG | 选定 | 选定 | - | - | * |
| RA | 选定 | 选定 | - | - | * |
| WAV | 选定 | 选定 | - | - | * |
| WMA | 选定 | 选定 | - | - | * |
| DVI | 选定 | 选定 | - | * | * |
| FLV | 选定 | 选定 | - | * | * |
| M4V | 选定 | 选定 | - | * | * |
| MPEG | 选定 | 选定 | - | * | * |
| OGV | 选定 | 选定 | - | * | * |
| MOV | 选定 | 选定 | - | * | * |
| WMV | 选定 | 选定 | - | * | * |
| SWF | 选定 | 选定 | - | - | - |

## Dynamic Media中支持的用于转码{#supported-input-video-formats-for-dynamic-media-transcoding}的输入视频格式

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen (MSS2)、Microsoft Photo Story (WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV, OGG | Ogg | Theora、VP3、Dirac | - |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro | - |
| MTS | AVCHD | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| R3D, RM | Red Raw Video | MJPEG 2000 | - |
| RAM, RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| FLAC | Native Flac | 免费的无损音频编解码器 | - |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 | - |

## 支持的存档格式{#supported-archive-formats}

下表介绍了支持的存档格式和常见DAM工作流的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 动态媒体投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | 选定 | 选定 | 选定 | 选定 | 选定 | - |
| JAR | 选定 | 选定 | 选定 | 选定 | 选定 | - |
| RAR | 选定 | 选定 | 选定 | 选定 | 选定 | - |
| TAR | 选定 | 选定 | 选定 | 选定 | 选定 | - |
| ZIP | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |

## 其他支持的格式{#other-supported-formats}

下面介绍了几种特定文件格式的常见DAM功能的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 动态媒体投放 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | 选定 | 选定 | 选定 | 选定 | 选定 | - |
| CSS | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| VTT | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| XML | 选定 | 选定 | 选定 | 选定 | 选定 | 选定 |
| JavaScript(当配置有自己的投放域时) | - | - | - | - | - | 选定 |

>[!NOTE]
>
>上传和分发JavaScript文件可能是安全的，也可能不安全。 如果需要，可使用叠加阻止用户上传JS文件。

## 支持的MIME类型{#supported-mime-types}

默认情况下，[!DNL Experience Manager]使用文件扩展名检测文件类型。 [!DNL Experience Manager] 可以从文件内容中检测到它。对于后者，在] Web控制台中，选择]Day CQ DAM Mime类型服务[!UICONTROL 中的从内容[!UICONTROL 检测MIME选项。[!DNL Experience Manager]

支持的MIME类型列表在`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`的CRXDE Lite中可用。

| 文件扩展名 | MIME类型/ Internet媒体类型 | 默认jobParam值 | 允许的jobParam值 |
|---|---|---|---|
| 图像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 默认jobParam适用于所有图像MIME类型资产。<ul><li>[knockoutBackgroundOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[usmsharpMaskOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | 文本/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdf选项](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| TTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [启用基于MIME类型的资产和Dynamic Media Classic上传作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [配置基于MIME类型的上传作业参数支持](config-dynamic.md)。

