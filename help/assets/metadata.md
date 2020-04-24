---
title: 在[!DNL Adobe Experience Manager]中管理数字资产的元数据。
description: 了解元数据的类型以及[!DNL Adobe Experience Manager Assets]如何帮助管理资产的元数据，从而更轻松地对资产进行分类和组织。
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Manage metadata for digital assets {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] 保留每个资产的元数据。 这使您可以更加方便地分类和组织资产，并且还有助于用户查找特定的资产。With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage arbitrary metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

* [XMP 元数据](xmp.md)
* [如何编辑或添加元数据](meta-edit.md)
* [元数据架构参考](meta-ref.md)

## 为何需要元数据 {#why-we-need-metadata}

元数据是指关于数据的数据。在这方面，数据是指您处理的资产，例如图像。元数据很重要，因为它使用户可以更高效地管理资产。

元数据是此图像可用的所有数据的集合，但该数据不一定包含在该图像中，例如：

* 资产的名称
* 资产的上次修改日期和时间
* 图像在存储库中的存储大小
* 资产所在的文件夹名称

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

您可以向数字资产中添加更多高级别的数据，例如：

* 资产的类型（它是图像、视频、音频剪辑，还是文档？）
* 资产的所有者
* 资产的标题
* 资产的描述
* 为资产分配的标记

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。尽管一位用户可以只根据文件名管理数百个文件的列表，但当参与文件管理的用户数和所管理资产的数量增多时，这种方法便不尽如人意了。

向资产中添加元数据后，资产会变得更有价值，因为资产会在以下方面得到改进

* 更易于访问 - 用户可以更轻松地查找资产
* 更易于管理 - 您可以更轻松地查找具有相同属性集的资产，并对它们应用更改
* 更复杂 - 向资产中添加的元数据越多，元数据管理就会变得越重要

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## 元数据基础知识 {#metadata-basics}

在导入（摄取）资产时，会从资产中提取元数据。此外，添加元数据还可帮助您进一步对资产分类。

本节介绍元数据的类型和编码标准。

### 元数据的类型 {#types-of-metadata}

有两种基本类型的元数据：

* 技术性元数据
* 描述性元数据

#### 技术性元数据 {#technical-metadata}

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。Technical metadata can be determined automatically by [!DNL Experience Manager Assets] and other software and may change when the asset is modified. 资产的可用技术性元数据主要取决于资产的文件类型。技术性元数据的示例如下：

* 文件的大小
* 图像的尺寸（高和宽）
* 音频或视频文件的比特率
* 图像的分辨率（细节级别）

#### 描述性元数据 {#descriptive-metadata}

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它必须以手动或半自动方式创建。例如，启用了 GPS 的照相机可以自动跟踪拍摄图像时所处的经度和纬度，并将此信息添加到图像的元数据。

由于创建描述性元数据信息需要手动操作，人工成本较高，因此人们建立了相关标准，以便于在软件系统和组织之间交换元数据。

[!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

鉴于元数据的重要性，以及创建元数据需要很大的手动工作量，人们建立了相关标准，以便于简化元数据交换。

### 编码标准 {#encoding-standards}

向文件中嵌入元数据的方法有很多种。支持一系列编码标准选项：

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3：适用于音频和视频文件。
* EXIF：适用于图像文件。
* 其他／旧版：Microsoft Word、PowerPoint、Excel等。

#### XMP {#xmp}

XMP means Extensible Metadata Platform and is the metadata standard that is used by [!DNL Experience Manager Assets] for all metadata management. Besides offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich content model and is supported by Adobe and other companies, so that users of XMP in combination with [!DNL Experience Manager Assets] have a powerful platform to build upon.

#### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3 标记适用于 MP3 和 MP3pro 文件。
* WAV 无标记。
* WMA 使用专有标记，不允许开源实现。
* Ogg Vorbis 使用嵌入在 Ogg 容器中的 Xiph 注释。
* AAC 使用专有标记格式。

#### EXIF {#exif}

EXIF 是指可交换图像文件格式，它是数字摄影领域最常用的元数据格式。它提供了一种将固定的元数据属性词汇嵌入多种文件格式（如JPEG、TIFF、RIFF和WAV）的方法。

EXIF 的主要局限性在于，其他一些常用的图像文件格式（例如，BMP、GIF 或 PNG）不支持这种编码标准。

EXIF 将元数据存储为元数据名称和元数据值对。These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager].

由于 EXIF 是由现代数码相机自动创建，并通过现代图形软件来支持，因此它在元数据管理中可被视为最不常用的标准。

由 EXIF 定义的大多数元数据字段都具有很强的技术性，并且在描述性元数据管理方面的作用比较有限。For this reason, [!DNL Assets] offers mapping of EXIF properties into [common metadata schemata](metadata-schemas.md) and into [XMP](xmp-writeback.md), the powerful metadata format [!DNL Assets] uses for metadata management.

#### 其他元数据 {#other-metadata}

可以从文件中嵌入的其他元数据包括Microsoft Word、PowerPoint、Excel等。

## 元数据架构 {#metadata-schemata}

元数据模式是预定义的元数据属性定义集，可用于各种应用程序。属性始终与资产关联，这意味着属性与资源相关。

如果不存在能满足您需求的元数据架构，您也可以自行设计元数据架构（但是，请注意避免创建与已有架构重复的内容）。在组织内部对架构予以划分，可简化各组织之间的元数据共享。

[!DNL Experience Manager] 为您提供了最流行的元数据架构的现成列表，允许您跳转开始元数据策略并从已定义的架构中选择所需的元数据属性。

下一节列出了支持的元数据架构。

### 标准元数据 {#standard-metadata}

* dc - 都柏林核心 - 最重要、应用最广泛的元数据集
* DICOM - 医学数字成像和通信
* Iptc4xmpCore和iptc4xmpExt - International Press Communications Standard —— 许多特定于主题的元数据
* rdf - 资源描述框架 - 适用于通用语义 Web 元数据
* xmp - 可扩展元数据平台
* xmpBJ - 基本工单

### 特定于应用程序的元数据 {#application-specific-metadata}

>[!NOTE]
>
>特定于应用程序的元数据包括技术性元数据和描述性元数据。如果您使用这类元数据，其他应用程序将无法使用这些元数据。例如，如果您的某个资产使用 Adobe Photoshop 元数据，则当其他图像渲染应用程序尝试访问该资产的元数据时，便无法访问这些元数据。
>
>如果您发现您的资产中有很多特定于应用程序的元数据，您可以创建一个工作流步骤，将特定于应用程序的属性更改为标准属性。

* acdsee - metadata managed by the ACDSee program [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - used by [!DNL Experience Manager Assets]
* dam —— 使用者 [!DNL Experience Manager Assets]
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto和MP - Microsoft Photo
* pdf amd pdfx
* photoshop 和 psAux - Adobe Photoshop

### 数字权限管理元数据 {#digital-rights-management-metadata}

* cc - Creative Commons
* xmpRights
* plus —— 图片授权通用系统- https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata行业标准元数据的发布要求
* prl - Prism 权限语言
* pur - Prism 使用权限
* xmpPlus - PLUS 与 XMP 的集成

### 特定于摄影领域的元数据 {#photography-specific-metadata}

* exif - 照相机中的大量技术性信息，包括 GPS 定位
* crs - Photoshop Camera Raw
* Iptc4xmpCore和iptc4xmpExt
* TIFF - 图像元数据（并非只适用于 TIFF 图像）

### 特定于打印领域的元数据 {#print-specific-metadata}

* pdf和pdfx - Adobe PDF和第三方应用程序
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata
* xmp
* xmpPG - 适用于分页文本的 xmp

### 特定于多媒体的元数据 {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - 媒体管理

## 元数据驱动的工作流 {#metadata-driven-workflows}

创建元数据驱动的工作流可以帮助您实现一些流程的自动化，从而提高效率。在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。

例如，以下是可以利用元数据驱动的工作流实现的功能：

* 该工作流可以检查图像是否含有标题。如果图像没有标题，系统会通知特定用户添加标题。
* 该工作流可以检查资产上的版权声明是否允许分发。如果允许分发，系统会将资产发送到某台服务器。如果不允许分发，系统会将资产发送到另一台服务器。
