---
title: 使用[!DNL Adobe Experience Manager Assets]处理各种支持的文件格式的最佳实践。
description: 使用[!DNL Experience Manager Assets]处理各种受支持文件类型的最佳实践。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Assets file format best practices {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支持许多专有和第三方文件格式库，以满足用户的各种文件支持要求。 支持的Adobe库包括、 [!DNL Adobe Camera Raw]Gibson、Adobe PDF Rasterizer和 [!DNL Adobe InDesign Server]。 此外，还 [!DNL Experience Manager Assets] 支持第三方库， [!DNL ImageMagick]包括 [!DNL TwelveMonkeys]、等等。

For the supported file formats, see [Assets supported formats](/help/assets/assets-formats.md).

>[!TIP]
>
>如果您使用 [!DNL Experience Manager] 的是Adobe Managed Services(AMS)，则如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户关怀团队。 与Adobe客户关怀代表合作，为您的AMS部署实施这些最佳实践，并为Adobe专有格式选择最佳的工具和模型。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

## [!DNL Adobe Camera Raw] 库 {#adobe-camera-raw-library}

为获得最佳性能，Adobe建议使用 [!DNL Adobe Camera Raw] RAW和DNG文件库。

[!DNL Adobe Camera Raw] 库支持CMYK颜色用户档案作为输入。 但是，它仅支持JPEG格式的输出，并以RGB色彩空间生成输出。 它不会在缩略图中保留源文件色彩空间（例如CMYK）。

有关详细信息，请参 [阅Camera Raw支持](/help/assets/camera-raw.md)。

## Adobe PDF栅格化器库 {#adobe-pdf-rasterizer-library}

为获得最佳效果，Adobe建议对以下文件使用Adobe PDF栅格化器库：

* 内容密集型的PDF文件
* 未开箱生成缩览图的AI文件
* 对于具有专色(PMS)的AI文件

与开箱即用的栅格输出相比，使用PDF栅格化器生成的缩览图和预览的质量更高。 Adobe PDF Rasterizer库不支持任何色彩空间转换。 无论源PDF文件的色彩空间如何，Adobe PDF Rasterizer都只生成RGB输出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建议您使 [!DNL Adobe InDesign Server] 用提取 [!DNL Adobe InDesign]特定的再现，如IDML和HTML。 有关详细信息，请参 [阅在Adobe InDesign中将Experience Manager资产添加为引用](/help/assets/managing-linked-subassets.md#refai)。

## [!DNL Dynamic Media]  {#dynamic-media}

[!DNL Dynamic Media] 通过其全球、可扩展和性能优化的网络实时生成和交付丰富内容的多个变体。 它提供交互式查看体验并简化数字活动管理流程。 有关启用的详细信息， [!DNL Dynamic Media]请参阅 [配置Dynamic Media](/help/assets/config-dynamic.md)。

目前， [!DNL Dynamic Media] 每个文件最多可支持20 GB内容的视频。

## ImageMagick库 {#imagemagick-library}

Adobe建议在以下情况下使用ImageMagick库：

* 为EPS文件生成缩略图再现。
* 保留图像用户档案信息。
* 保留透明度。
* 处理PSD和PSB文件。

要了解如何在中设置库， [!DNL ImageMagick] 请参 [!DNL Experience Manager]阅使 [用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 有关最佳用法，请参 [阅配置ImageMagick的最佳实践](/help/assets/best-practices-for-imagemagick.md)。

## 图像转码库 {#image-transcoding-library}

Adobe Imaging Tronding Library是一款图像处理解决方案，可执行核心图像处理功能，包括图像编码、转码、重新采样、调整大小等。

成像转码库支持以下MIME类型：

* JPG/JPEG
* PNG（8位和16位）
* GIF
* BMP
* TIFF/压缩TIFF（除32位Tiff和PTiff外）。
* ICO
* ICN

有关详细信息，请参阅 [成像转码库](/help/assets/imaging-transcoding-library.md)。
