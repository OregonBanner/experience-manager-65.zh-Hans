---
title: 支持的文件格式和MIME类型
description: ' [!DNL Assets] and [!DNL Dynamic Media] 支持的文件格式和MIME类型以及每种格式支持的功能。'
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: 资产管理，演绎版
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: f0a0ea53675afa16463a3cf863257020ba5374d3
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 22%

---

# [!DNL Adobe Experience Manager Assets]中支持的格式 {#assets-supported-formats}

[!DNL Experience Manager Assets] 支持多种文件格式，每种功能都支持不同的MIME类型。要将[!DNL Assets]与其他符合标准的数字资产管理(DAM)解决方案和桌面软件集成，请使用Adobe的[!DNL Extensible Metadata Platform](XMP)。

使用图例了解支持级别。

| 支持级别 | 描述 |
| :-----------: | ------------------------------ |
| ✓ | 支持 |
| * | 受支持，但需要附加功能 |
| - | 不适用 |

## [!DNL Experience Manager]中支持的光栅图像格式 {#supported-raster-image-formats}

[!DNL Assets]中支持的光栅图像格式包括：

| 格式 | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | 编辑 | 元数据写回 | 分析 |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

从PSD文件中提取合并的图像。 它是由Adobe Photoshop生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际的图像，也可能不是实际的图像。

[!DNL Dynamic Media]中支持的光栅图像格式包括：

| 格式 | 上载<br>（输入格式） | 创建<br>图像<br>预设<br>（输出格式） | 预览<br>动态<br>演绎版 | 传递<br>动态<br>演绎版 | 下载<br> dynamic<br>演绎版 |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | - | - | - | - |
| PSD ? | ✓ | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ | - | - | - | - |

从PSD文件中提取合并的图像。 它是由Adobe Photoshop生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际的图像，也可能不是实际的图像。

除上述信息外，请考虑以下事项：

* 对EPS文件的支持仅适用于光栅图像。 例如，默认不支持为 EPS 矢量图像生成缩略图。要添加支持，请[配置ImageMagick](best-practices-for-imagemagick.md)。 要集成第三方工具以启用其他功能，请参阅[基于命令行的媒体处理程序](media-handlers.md#command-line-based-media-handler)。

* 元数据写回在添加到`NComm`处理程序时对PSB文件格式有效。

* 要使用[!DNL Dynamic Media]预览和生成EPS文件的动态呈现，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 对于EPS文件， PostScript文档结构约定(PS-Adobe)版本3.0或更高版本支持元数据写回。

## 支持的3D格式 {#support-3d-formats}

支持以下3D格式列表。

另请参阅[在Dynamic Media中使用3D资产。](/help/assets/assets-3d.md)

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 缩略图预览 | 3D预览 | Dynamic Media交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## Dynamic Media中不支持的栅格图像格式 {#unsupported-image-formats-dynamic-media}

下表描述了Dynamic Media中支持的&#x200B;*not*&#x200B;光栅图像文件格式的子类型。

另请参阅[检测不支持的Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html)文件格式。

* IDAT区块大于100 MB的PNG文件。
* PSB文件。
* 不支持具有非CMYK、RGB、灰度或位图的色彩空间的PSD文件。 不支持DuoTone、Lab和索引色彩空间。
* 位深度大于16的PSD文件。
* 具有浮点数据的TIFF文件。
* 具有Lab色彩空间的TIFF文件。

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## 支持的PDF光栅器库 {#supported-pdf-rasterizer-library}

Adobe PDF光栅化器库可为大型且内容密集型[!DNL Adobe Illustrator]和PDF文件生成高质量缩略图和预览。 Adobe建议为以下内容使用PDF光栅器库：

* 需要大量处理的内容密集型AI/PDF文件。
* AI/PDF文件，默认情况下不会为其生成缩略图。
* 具有Pantone匹配系统(PMS)颜色的AI文件。

请参阅[使用PDF光栅器](aem-pdf-rasterizer.md)。

## 支持的图像转码库 {#supported-image-transcoding-library}

Adobe图像转码库是一款图像处理解决方案，可执行核心的图像处理功能，例如编码、转码、重新取样和调整大小。

图像转码库支持JPG/JPEG、PNG（8位和16位）、GIF、BMP、TIFF/压缩TIFF（除了32位TIFF文件和PTIFF文件外）、ICO和ICN MIME类型。

请参阅[成像转码库](imaging-transcoding-library.md)。

## 支持的Camera Raw {#supported-camera-raw}

[!DNL Adobe Camera Raw]库允许[!DNL Assets]摄取原始图像。 请参阅[Camera Raw支持](camera-raw.md)。

## 支持的[!DNL Assets]文档格式 {#supported-document-formats}

资产管理功能支持的文档格式如下：

| 格式 | 存储 | [元数据管理](metadata.md) | 全文<br>提取 | [元数据提取](metadata.md) | 缩略图<br>生成 | [子资产提取](managing-linked-subassets.md) | [元数据写回](xmp-writeback.md) | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| EPUB | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## Dynamic Media中支持的文档格式 {#supported-document-formats-dynamic-media}

| 格式 | 上载<br>（输入格式） | 创建<br>图像<br>预设<br>（输出格式） | 预览<br>动态<br>演绎版 | 传递<br>动态<br>演绎版 | 下载<br> dynamic<br>演绎版 |
|---|:---:|:---:|:---:|:---:|:---:|
| [人工智能](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |

除了上述功能外，还请考虑以下事项：

* 要使用Dynamic Media为PDF文件生成动态演绎版，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media预览和生成AI文件的动态呈现，请参阅[Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media为INDD文件生成动态呈现，请参阅[InDesign(INDD)文件格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## 支持的多媒体格式 {#supported-multimedia-formats}

|  | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | FFmpeg转码 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | * |
| MIDI | ✓ | ✓ | - | - | * |
| 3GP | ✓ | ✓ | - | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ | - | - | * |
| OGA | ✓ | ✓ | - | - | * |
| OGG | ✓ | ✓ | - | - | * |
| RA | ✓ | ✓ | - | - | * |
| WAV | ✓ | ✓ | - | - | * |
| WMA | ✓ | ✓ | - | - | * |
| DVI | ✓ | ✓ | - | * | * |
| FLV | ✓ | ✓ | - | * | * |
| M4V | ✓ | ✓ | - | * | * |
| MPEG | ✓ | ✓ | - | * | * |
| OGV | ✓ | ✓ | - | * | * |
| MOV | ✓ | ✓ | - | * | * |
| WMV | ✓ | ✓ | - | * | * |
| SWF | ✓ | ✓ | - | - | - |

## Dynamic Media中支持的用于转码的输入视频格式 {#supported-input-video-formats-for-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（所有配置文件） | - |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft®屏幕(MSS2)、Microsoft®照片文章(WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3(IV30)、MJPEG、Microsoft® Video 1(MS-CRAM) |
| WebM | WebM | Google VP8 | - |
| OGV、OGG | Ogg | Theora、VP3、Dirac | - |
| MKV | Matroska | H264/AVC | - |
| RAM、RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 | - |

## 支持的存档格式 {#supported-archive-formats}

下表介绍了支持的存档格式以及常用DAM工作流的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## 其他支持的格式 {#other-supported-formats}

下面介绍了一些特定文件格式通常的DAM功能的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | Dynamic Media交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（使用自己的交付域配置时） | - | - | - | - | - | ✓ |

>[!NOTE]
>
>上传和分发JavaScript文件可能是安全的，也可能不安全。 如有必要，您可以使用叠加来阻止用户上传JS文件。

## 支持的MIME类型 {#supported-mime-types}

默认情况下，[!DNL Experience Manager]会使用文件扩展名检测文件类型。 [!DNL Experience Manager] 可以从文件内容中检测到它。对于后者，在[!DNL Experience Manager]Web控制台中，选择[!UICONTROL Day CQ DAM Mime类型服务]中的[!UICONTROL 从内容中检测MIME]选项。

`/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`的CRXDE Lite中提供了支持的MIME类型列表。

| 文件扩展名 | MIME类型/ Internet媒体类型 | 默认jobParam值 | 允许的jobParam值 |
|---|---|---|---|
| 图像 | 图像/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 默认的jobParam适用于所有图像MIME类型资产。<ul><li>[knouckBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[usmarpMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| 文档 | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>图像/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[illustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| TTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | 视频/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [启用基于MIME类型的资产和Dynamic Media Classic上传作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。
>* [为上传作业参数支持配置基于MIME类型](config-dynamic.md)。

