---
title: 了解元数据概念
description: 了解元数据的需求和类型，更轻松地分类和组织资源。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2720'
ht-degree: 40%

---

# 了解元数据概念 {#why-we-need-metadata}

元数据是指关于数据的数据。在这方面，数据是指您的数字资产，例如图像。 元数据对于高效的资源管理非常关键。

元数据是某个资源的所有可用数据的集合，但不一定包含在该图像中。 元数据的一些示例包括：

* 资源的名称。
* 上次修改的时间和日期。
* 资源存储在存储库中的大小。
* 包含它的文件夹的名称。
* 相关资源或应用的标记。

以上是基本元数据属性，这些属性 [!DNL Experience Manager] 可以管理资产，这允许用户查看所有资产。 例如，在尝试发现最近添加的资产时，按上次修改日期对资产排序很有用。

您可以向数字资产中添加更多高级别的数据，例如：

* 资源类型（图像、视频、音频剪辑或文档）。
* 资产的所有者。
* 资源的标题。
* 资源的描述。
* 分配给资源的标记。

较多的元数据可以帮助您进一步对资产分类，随着数字信息量的增多，元数据会非常有用。可以仅根据文件名管理数百个文件。 但是，这种方法不具备扩展性。当涉及的人数以及管理的资产数量增加时，这种方法很快就会出现不足。

随着元数据的增加，数字资源的价值会随之增长，因为资源会变得：

* 更易于访问 - 系统和用户可以轻松地找到它。
* 更易于管理 - 您可以轻松地找到具有一组相同属性的资源并对其应用更改。
* 完整 - 元数据越多，资源就能携带更多信息和具体情境。

出于这些原因， [!DNL Assets] 为您提供创建、管理和交换数字资源元数据的正确方法。

## 元数据的类型 {#types-of-metadata}

元数据的两种基本类型是技术元数据和描述性元数据。

技术性元数据对于处理数字资产的软件应用程序而言非常有用，因此不应该手动维护。[!DNL Experience Manager Assets] 和其他软件会自动确定技术元数据，元数据可能会在资产被修改时发生变化。 资产的可用技术性元数据主要取决于资产的文件类型。技术元数据的一些示例包括：

* 文件的大小。
* 图像的Dimension（高度和宽度）。
* 音频或视频文件的比特率。
* 图像的分辨率（细节级别）。

描述性元数据是与应用程序域相关的元数据，例如，资产所来自的业务。描述性元数据无法自动确定。它是手动或半自动创建的。 例如，启用了GPS的相机可以自动跟踪纬度和经度，并在图像中添加地理标签。

手动创建描述性元数据信息的成本很高。 因此，制定了各种标准来简化软件系统和组织之间的元数据交换。 [!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

## 编码标准 {#encoding-standards}

可通过多种方式将元数据嵌入文件。 支持一系列编码标准选项：

* XMP：使用者 [!DNL Assets] 将提取的元数据存储在存储库中。
* ID3：适用于音频和视频文件。
* Exif：用于图像文件。
* 其他/旧版：来自 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]，等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一个开放标准，用于 [!DNL Experience Manager Assets] 用于所有元数据管理。 标准提供了可嵌入到所有文件格式的通用元数据编码。 Adobe和其他公司支持XMP标准，因为它提供了丰富的内容模型。 XMP标准的用户和 [!DNL Experience Manager Assets] 拥有强大的平台进行构建。 有关更多信息，请参阅 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

当您在计算机或便携式 MP3 播放器上播放数字音频文件时，会显示这些 ID3 标记中存储的数据。

ID3 标记是专为 MP3 文件格式而设计。有关各种格式的其他信息如下：

* ID3标记适用于MP3和mp3PRO文件。
* WAV 无标记。
* WMA具有不允许开源实施的专有标记。
* Ogg Vorbis 使用嵌入在 Ogg 容器中的 Xiph 注释。
* AAC 使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数字摄影中最常用的元数据格式。 它提供了一种以多种文件格式(如JPEG、TIFF、RIFF和WAV)嵌入元数据属性的固定词汇的方法。 Exif将元数据存储为元数据名称和元数据值的对。这些元数据名称 — 值对也称为标记，切勿与中的标记混淆。 [!DNL Experience Manager]. 现代数码相机创建Exif元数据，现代图形软件支持该元数据。 Exif格式是元数据管理（尤其是图像）的最低通用分母。

Exif的一个主要限制是一些流行的图像文件格式(如BMP、GIF或PNG)不支持它。

由Exif定义的元数据字段通常具有技术性质，在描述性元数据管理中的用处有限。 出于这个原因， [!DNL Experience Manager Assets] 提供将Exif属性映射到 [通用元数据架构](metadata-schemas.md) 并进入 [XMP](xmp-writeback.md).

### 其他元数据 {#other-metadata}

可从文件中嵌入的其他元数据包括 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]，等等。

## 了解元数据架构 {#metadata-schemata}

元数据架构是元数据属性定义的预定义集，可用于各种应用程序。 属性始终与资源关联，这意味着属性与资源是“关于”的。

如果不存在符合您需求的元数据架构，您还可以设计自己的元数据架构。 不要复制现有信息。 在组织内，分隔架构使元数据共享更加容易。 [!DNL Experience Manager] 为您提供最受欢迎的元数据架构的默认列表。 列表可帮助您快速启动元数据策略并快速选择所需的元数据属性。

下面列出了支持的元数据架构。

### 标准元数据 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一组重要且广泛使用的元数据。
* DICOM - 医学数字成像和通信.
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 国际新闻传播标准包含许多特定主题的元数据。
* RDF — 资源描述框架 — 用于通用语义Web元数据。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本作业单据。

### 特定于应用程序的元数据 {#application-specific-metadata}

特定于应用程序的元数据包括技术和描述性元数据。 如果您使用此类元数据，则其他应用程序可能无法使用该元数据。 例如，其他图像渲染应用程序可能无法访问 [!DNL Adobe Photoshop] 元数据。 您可以创建工作流步骤，以将特定于应用程序的属性更改为标准属性。

* ACDSee — 由管理的元数据 [!DNL ACDSee] 程序。 参见 [www.acdsee.com/](https://www.acdsee.com/).
* 相册 —  [!DNL Adobe Photoshop Album].
* CQ — 使用者 [!DNL Experience Manager Assets].
* DAM — 使用者 [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] 是用于Windows操作系统的元数据和文件管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP - Microsoft照片。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM)元数据 {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [图片授权通用系统](https://www.useplus.com).
* 棱镜 —  [发布行业标准元数据的要求](https://www.idealliance.org/prism-metadata).
* PRL — 棱镜权限语言。
* PUR - PRISM使用权限。
* `xmpPlus` - PLUS与XMP的集成。

### 特定于摄影的元数据 {#photography-specific-metadata}

* Exif — 相机中的技术信息，包括GPS位置。
* CRS - [!DNL Camera Raw] 架构。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 图像元数据(不适用于TIFF图像)。

### 打印特定的元数据 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和第三方应用程序。
* 棱镜 —  [发布行业标准元数据的要求](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — 分页文本的XMP元数据。

### 特定于多媒体的元数据 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 介质管理。

## 元数据架构引用 {#metadata-schemata-reference}

以下参考内容介绍了关于特定元数据架构（按字母顺序排列）的信息并列出了各个属性及其定义。

### 都柏林核心 {#dublin-core}

都柏林核心元数据提供了一个用于描述资产的标准化惯例集，可使资产更易于查找。In [!DNL Assets]的Dublin Core介绍了数字资产，包括视频、声音、图像和文档。

都柏林核心元数据元素集 (DCMES) 很简单，共包含 15 个元数据元素，如下表所示。每个都柏林核心元素都是可选元素，并且可以重复。您可以视需要为特定于媒体类型的元数据添加或删除都柏林核心元数据信息。

除了DCMES之外，还有由都柏林核心计划创建的其他元数据元素。请参阅 [都柏林核心计划](https://dublincore.org/) 了解更多信息。

| 属性 | 描述 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | 负责贡献内容的个人或公司。 |
| coverage | 资产覆盖的地理位置或时间段。 |
| creator | 负责创建内容的个人或公司。 |
| date | 与资产关联的日期或时间段。 |
| 描述 | 关于资产的详细信息。 |
| format | 资产的文件格式、物理介质或尺寸。[!DNL Experience Manager] 用途 `dc:format` 表示资源的MIME类型。 |
| 标识符 | 资产的唯一参考。 |
| 语言 | 资源的语言(例如， `en` （英语）。 |
| publisher | 负责使资产进入可用状态的个人或公司。 |
| relation | 相关的资产。 |
| rights | 关于谁有权使用此资产的信息。 |
| source | 作为资产派生来源的相关资产。 |
| subject | 资产的主题。 |
| 页面 | 资产的名称。 |
| 类型 | 资产的性质或类型。 |

### IPTC {#iptc}

国际出版电讯委员会 (IPTC) 是全世界新闻机构的联盟，其宗旨之一是制定并维护技术标准。IPTC 定义了针对图像的一套照片元数据标准，几乎所有摄影人士都普遍接受这套标准。这些元数据标准从属于一个更广泛的标准，即 20 世纪 90 年代创建的 IPTC 信息交换模型 (IIM)。

尽管 IPTC 标题信息基本上已经被 XMP 所取代，但仍有 IPTC 核心架构和扩展架构可供 XMP 使用。在图像程序中，会同时同步 XMP 属性和 IPTC 属性。

## 元数据驱动的工作流 {#metadata-driven-workflows}

创建元数据驱动的工作流可帮助您自动化某些流程，从而提高效率。 在元数据驱动的工作流中，工作流管理系统会读取该工作流，然后相应地执行某些预定义操作。例如，以下是可以利用元数据驱动的工作流实现的功能：

* 工作流可以检查图像是否具有标题。 如果不包含，系统会通知添加标题。
* 工作流可以检查资产上的版权声明是否允许分发。 因此，系统会将资产发送到一台服务器或另一台服务器。
* 工作流可以检查没有预定义的强制性元数据的资产，或者检查具有以下特征的资产： *无效* 元数据。

## XMP 元数据 {#xmp-metadata}

XMP（可扩展元数据平台）是使用的元数据标准 [!DNL Adobe Experience Manager Assets] 用于所有元数据管理。 XMP 为在各种应用程序中创建、处理和交换元数据提供了一种标准格式。

除了提供可以嵌入到所有文件格式的通用元数据编码之外，XMP还提供丰富的 [内容模型](#xmp-core-concepts) 和 [受Adobe支持](#advantages-of-xmp) 和其他公司，以便XMP的用户能够与 [!DNL Assets] 拥有强大的平台进行构建。

Adobe 支持 [XMP 规范](https://www.adobe.com/devnet/xmp.html)。

### 什么是 XMP？ {#what-is-xmp}

Adobe 首先在 Adobe Acrobat 软件产品中引入了 XMP 标准。此后，XMP 标准逐渐被广泛采用。[!DNL Assets] 在本机支持由 Adobe 率先推出的 XMP，即可扩展元数据平台。XMP 是一项用于处理和存储数字资产中的标准化专有元数据的标准。XMP 旨在形成通用标准，从而让多个应用程序能够高效地处理元数据。

例如，专业生产人士可以使用 Adobe 应用程序中内置的 XMP 支持，在多种文件格式之间传递信息。[!DNL Assets] 存储库提取XMP元数据并使用它来管理内容生命周期，并提供创建自动化工作流的功能。

XMP 通过提供数据模型、存储模型和架构，使元数据的定义、创建和处理方式实现标准化。本节将介绍所有这些概念。

来自 EXIF、ID3 或 Microsoft Office 的所有旧版元数据都将自动转换为 XMP，而 XMP 可进行扩展，以支持特定于客户的元数据架构，例如产品目录。

XMP 中的元数据包含一组属性。这些属性始终与称为资源的特定实体相关联；即，这些属性是“关于”资源的。 对于 XMP，资源始终是指资产。

### XMP生态系统 {#xmp-ecosystem}

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP 的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP 具有以下优势：

* 基于 XMP 的元数据非常强大且精细。
* XMP 允许您为一个属性设置多个值。
* XMP 采用标准化的编码，让您可以轻松交换元数据。
* XMP 具有可扩展性。您可以将其他信息添加到资源中。

XMP标准设计为可扩展，允许您向XMP数据添加自定义类型的元数据。 而EXIF则否 — 它有一个无法扩展的固定属性列表。

>[!NOTE]
>
>XMP 一般不允许嵌入二进制类型的数据。要在XMP中携带二进制数据（例如缩略图图像），必须以XML友好格式对其进行编码，例如 `Base64`.

### XMP概念 {#xmp-core-concepts}

以下各节介绍了 XMP 的核心概念，包括命名空间和架构、属性和值以及替代语言。

#### 命名空间和架构 {#namespaces-and-schemata}

XMP 架构是通用 XML 命名空间中的一组属性名称，包括数据类型和描述性信息。
XMP 架构采用其 XML 命名空间 URI 进行标识。使用命名空间可以防止不同架构内名称相同但含义不同的属性之间发生冲突。

例如， `Creator` 两个独立设计的架构中的资产可能是指创建资产的人，也可能是指创建资产的应用程序(例如，Adobe Photoshop)。

#### 属性和值 {#properties-and-values}

XMP 可以包含来自一个或多个架构的属性。例如，很多 Adobe 应用程序使用的典型子集包括以下架构：

* 都柏林核心模式： `dc:title`， `dc:creator`， `dc:subject`， `dc:format`， `dc:rights`.
* XMP基本架构： `xmp:CreateDate`， `xmp:CreatorTool`， `xmp:ModifyDate`， `xmp:metadataDate`.
* XMP权限管理架构： `xmpRights:WebStatement`， `xmpRights:Marked`.
* XMP媒体管理模式： `xmpMM:DocumentID`.

#### 替代语言 {#language-alternatives}

XMP允许您添加 `xml:lang` 属性到文本属性以指定文本的语言。

## 使用IPTC元数据 {#support-for-iptc-metadata}

了解如何 [!DNL Adobe Experience Manager Assets] 支持通过以下方式添加到资源的IPTC元数据、创意评级和关键词 [!DNL Adobe Bridge] 和其他 [!DNL Adobe Creative Cloud] 应用程序。

[!DNL Adobe Experience Manager Assets] 支持广泛用于描述资源的IPTC元数据标准。 这边， [!DNL Assets] 提高了摄影师、创意机构、图书馆、博物馆等各方对它的接受。

现在，资产的默认元数据架构整合了IPTC Core和IPTC扩展元数据架构，以定义全面的元数据属性，允许用户添加有关图像中所示的人员、位置和产品的精确而可靠的数据。 它还支持有关创建映像的日期、名称和标识符，以及表达权限信息的灵活方式。

资产的“属性”页面现在包含单独的选项卡，以便在可编辑字段中显示IPTC核心和IPTC扩展元数据。

1. 从 [!DNL Assets] 用户界面中，选择一个图像。
1. 单击 **[!UICONTROL 属性]** 工具栏中。
1. 单击 **[!UICONTROL IPTC]** 选项卡以查看资产的IPTC元数据。
1. 根据需要编辑IPTC元数据属性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 单击 **[!UICONTROL IPTC扩展]** 选项卡以查看资产的IPTC扩展元数据。
1. 根据需要编辑IPTC扩展元数据属性。
1. 单击 **[!UICONTROL 保存并关闭]** 以保存更改。

### 创意评级支持 {#creative-rating-support}

除了显示单个用户评级和聚合评级之外，“属性”页面现在还显示通过Adobe Bridge和其他创意应用程序分配给资产的评级

这些评级位于&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡的&#x200B;**[!UICONTROL 创意评分]**&#x200B;部分下。

此评级为只读属性，范围为1-5。 您可以从搜索面板中根据资产的创意评级搜索资产。

但是，此属性当前未编入索引，以避免与用户所做的自定义更改发生任何冲突。

### 关键词支持 {#keyword-support}

此 **[!UICONTROL IPTC]** 的选项卡 [!UICONTROL 属性] 页面还显示通过Adobe Bridge和其他Adobe Creative Cloud应用程序添加到资源的关键字。 您还可以编辑这些关键字，并从 **[!UICONTROL IPTC]** 选项卡。

![关键词](assets/keywords-in-iptc-tab.png)
