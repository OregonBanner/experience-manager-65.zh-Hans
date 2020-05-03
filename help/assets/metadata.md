---
title: 在[!DNL Adobe Experience Manager]中管理数字资产的元数据。
description: 了解元数据的类型以及[!DNL Adobe Experience Manager资产]如何帮助管理资产的元数据，从而更轻松地对资产进行分类和组织。 [!DNL Experience Manager]允许根据资产的元数据自动组织和处理资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c32e64d4921d7239d07f57ab9e12c744758faa0a

---


# 管理数字资产的元数据 {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 为每个资产保留元数据。 它可以更轻松地对资产进行分类和组织，并帮助寻找特定资产的用户。 With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. 利用资产的元数据保留和管理功能，您可以根据资产的元数据自动组织和处理资产。

* [XMP 元数据](xmp.md).
* [如何编辑或添加元数据](meta-edit.md)。
* [元数据架构引用](meta-ref.md)。

## 为何需要元数据 {#why-we-need-metadata}

元数据是指关于数据的数据。在这方面，数据是指您的数字资产，如图像。 元数据对于有效管理资产至关重要。

元数据是资产可用的所有数据的集合，但该数据不一定包含在该图像中。 一些元数据示例包括：

* 资产的名称。
* 上次修改的时间和日期。
* 资产存储在存储库中时的大小。
* 其所包含的文件夹的名称。
* 相关资产或已应用的标记。

以上是Experience Manager可以为资产管理的基本元数据属性，通过这些属性，用户可以查看所有资产。 例如，在尝试发现最近添加的资产时，按上次修改日期对资产进行排序会很有用。

您可以向数字资产中添加更多高级别的数据，例如：

* 资源类型(它是图像、视频、音频剪辑还是文档?)。
* 资产的所有者。
* 资产的标题。
* 资产的描述。
* 分配给资产的标记。

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。仅根据文件名管理数百个文件是可能的。 但是，此方法不可扩展。 当所涉人员数量和管理资产数量增加时，这个数字就不够了。

随着元数据的添加，数字资产的价值会增加，因为资产会变得

* 更易于访问——系统和用户可以轻松找到它。
* 更易于管理——您可以更轻松地查找具有相同属性集的资产，并将更改应用到这些资产。
* 完整——资产包含更多信息和上下文以及更多元数据。

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## 元数据的类型 {#types-of-metadata}

两种基本类型的元数据是技术性元数据和描述性元数据。

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。[!DNL Experience Manager Assets] 而其他软件会自动确定技术性元数据，并且修改资产时，元数据可能会发生更改。 资产的可用技术性元数据主要取决于资产的文件类型。技术元数据的一些示例包括：

* 文件的大小。
* 图像的尺寸（高度和宽度）。
* 音频或视频文件的比特率。
* 图像的分辨率（详细程度）。

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它是手动或半自动创建的。 例如，启用GPS的相机可自动跟踪经纬度并添加地理标记图像。

手动创建描述性元数据信息的成本很高。 因此，我们制定标准以简化跨软件系统和组织的元数据交换。 [!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

## Encoding standards {#encoding-standards}

在文件中嵌入元数据有多种方法。 支持一系列编码标准选项：

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：适用于音频和视频文件。
* Exif: 。
* 其他／旧版： 从 [!DNL Microsoft Word]、 [!DNL PowerPoint][!DNL Excel]等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一个开放标准，用于所 [!DNL Experience Manager Assets] 有元数据管理。 标准优惠可嵌入到所有文件格式的通用元数据编码。 Adobe和其他公司支持XMP标准，因为它提供丰富的内容模型。 XMP标准和的用户 [!DNL Experience Manager Assets] 拥有强大的基础平台。 有关详细信息，请参 [阅XMP](https://www.adobe.com/products/xmp.html)。

### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3标记在MP3和mp3PRO文件中有效。
* WAV 无标记。
* WMA具有不允许开放源码实现的专有标签。
* Ogg Vorbis 使用嵌入在 Ogg 容器中的 Xiph 注释。
* AAC 使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数字摄影中最常用的元数据格式。 它提供了一种在多种文件格式（如JPEG、TIFF、RIFF和WAV）中嵌入固定的元数据属性词汇的方法。 Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager].  现代数码相机创建Exif元数据，现代图形软件支持它。 Exif格式是元数据管理的最小公分母，对于图像尤为如此。

Exif的一个主要限制是一些常用的图像文件格式（如BMP、GIF或PNG）不支持它。

由Exif定义的元数据字段通常是技术性的，在描述性元数据管理中的用途有限。 因此，将Exif属 [!DNL Experience Manager Assets] 性映射到通用元数 [据架构](metadata-schemas.md) 和XMP [中的优惠](xmp-writeback.md)。

### Other metadata {#other-metadata}

可以从文件中嵌入的其他元数据包括Microsoft Word、PowerPoint、Excel等。

## Metadata schemata {#metadata-schemata}

元数据模式是预定义的元数据属性定义集，可用于各种应用程序。 属性始终与资产关联，这意味着属性是资源的“关于”。

如果不存在能满足您需求的元数据架构，您还可以设计自己的元数据架构。 请勿重复现有信息。 在组织内，将架构分开，可更轻松地共享元数据。 [!DNL Experience Manager] 为您提供最常用元数据架构的默认列表。 该列表可帮助您快速启动元数据战略并快速选择所需的元数据属性。

支持的元数据架构列于下面。

### Standard metadata {#standard-metadata}

* DC - [!DNL Dublin Core] 是一组重要且广泛使用的元数据。
* DICOM - 医学数字成像和通信.
* `Iptc4xmpCore` 和- `iptc4xmpExt` International Press Communications Standard包含许多特定于主题的元数据。
* RDF —— 资源描述框架——用于通用语义Web元数据。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` -基本工单。

### Application-specific metadata {#application-specific-metadata}

特定于应用程序的元数据包括技术性元数据和描述性元数据。 如果您使用此类元数据，其他应用程序可能无法使用该元数据。 例如，其他图像渲染应用程序可能无法访问元数 [!DNL Adobe Photoshop] 据。 您可以创建将应用程序特定属性更改为标准属性的工作流步骤。

* ACDSee —— 由项目管理的元 [!DNL ACDSee] 数据。 请参 [阅www.acdsee.com/](https://www.acdsee.com/)。
* 相册- [!DNL Adobe Photoshop Album].
* CQ - Used by [!DNL Experience Manager Assets].
* DAM —— 使用方 [!DNL Experience Manager Assets]。
* DEX - [Optima SC Description](http://www.optimasc.com/products/dex/index.html) explorer是用于Windows操作系统元数据和文件管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop]。

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata).
* PRL - PRISM权限语言。
* PUR - PRISM使用权。
* `xmpPlus` - PLUS与XMP集成。

### Photography-specific metadata {#photography-specific-metadata}

* Exif —— 相机技术信息，包括GPS定位。
* CRS - [!DNL Camera Raw] 模式
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF —— 图像元数据（不仅适用于TIFF图像）。

### Print-specific metadata {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和第三方应用程序。
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.prismstandard.org).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` -分页文本的XMP元数据。

### Multimedia-specific metadata {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` -媒体管理。

## Metadata-driven workflows {#metadata-driven-workflows}

创建元数据驱动的工作流可以帮助您实现一些流程的自动化，从而提高效率。 在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。例如，以下是可以利用元数据驱动的工作流实现的功能：

* 该工作流可以检查图像是否具有标题。 如果没有，系统将通知您添加标题。
* 该工作流可以检查资产上的版权声明是否允许分发。 因此，系统会将资产发送给一台或另一台服务器。
* 工作流可以检查没有预定义的强制元数据的资产，或具有无效元数据 *的资产* 。
