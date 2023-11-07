---
title: 了解元数据概念
description: 了解简化资产分类和组织的元数据的需求和类型。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 9%

---

# 了解元数据概念 {#why-we-need-metadata}

元数据是指有关数据的数据。 就这一点而言，数据是指您的数字资产，例如图像。 元数据对于高效的资源管理非常关键。

元数据是某个资源的所有可用数据的集合，但并不一定包含在该图像中。 元数据的一些示例包括：

* 资源的名称。
* 上次修改的时间和日期。
* 资源存储在存储库中的大小。
* 包含它的文件夹的名称。
* 相关资源或应用的标记。

以上是基本的元数据属性， [!DNL Experience Manager] 可以管理资产，这允许用户查看所有资产。 例如，在尝试发现最近添加的资产时，按上次修改日期对资产排序很有用。

例如，您可以向数字资产添加更多高级数据：

* 资源类型（图像、视频、音频剪辑或文档）。
* 资产的所有者。
* 资源的标题。
* 资源的描述。
* 分配给资产的标记。

更多元数据可帮助您进一步分类资源，在数字信息量增长时非常有用。 它可以仅根据文件名管理数百个文件。 但是，这种方法不具备扩展性。随着涉及的人数以及管理的资源数的增加，这种方法很快就会出现不足。

随着元数据的增加，数字资源的价值会随之增长，因为资源会变得：

* 更易于访问 - 系统和用户可以轻松地找到它。
* 更易于管理 - 您可以轻松地找到具有一组相同属性的资源并对其应用更改。
* 完整 - 元数据越多，资源就能携带更多信息和具体情境。

出于这些原因， [!DNL Assets] 为您提供合适的方法来创建、管理和交换数字资源的元数据。

## 元数据的类型 {#types-of-metadata}

元数据的两种基本类型是技术元数据和描述性元数据。

技术元数据对于处理数字资产的软件应用程序非常有用，不应手动维护。 [!DNL Experience Manager Assets] 和其他软件会自动确定技术元数据，元数据在资产被修改时可能会发生更改。 资源的可用技术元数据在很大程度上取决于资源的文件类型。 技术元数据的一些示例包括：

* 文件的大小。
* 图像的Dimension（高度和宽度）。
* 音频或视频文件的比特率。
* 图像的分辨率（细节级别）。

描述性元数据是与应用程序域相关的元数据，例如资产来自的业务。 无法自动确定描述性元数据。 它是手动或半自动创建的。 例如，启用了GPS的相机可以自动跟踪纬度和经度，并在图像中添加地理标签。

手动创建描述性元数据信息的成本很高。 因此，我们制定了各种标准来简化软件系统和组织之间的元数据交换。 [!DNL Experience Manager Assets] 支持元数据管理的所有相关标准。

## 编码标准 {#encoding-standards}

可通过多种方式在文件中嵌入元数据。 支持选择编码标准：

* XMP：使用者 [!DNL Assets] 将提取的元数据存储在存储库中。
* ID3：用于音频和视频文件。
* Exif：用于图像文件。
* 其他/旧版：来自 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]，等等。

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP)是一个开放标准，用于 [!DNL Experience Manager Assets] 用于所有元数据管理。 标准提供了可嵌入到所有文件格式的通用元数据编码。 Adobe和其他公司都支持XMP标准，因为它提供了丰富的内容模型。 XMP Standard的用户和 [!DNL Experience Manager Assets] 拥有强大的平台进行构建。 有关更多信息，请参阅 [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

当您在计算机上或便携式MP3播放器上播放数字音频文件时，将显示这些ID3标记中存储的数据。

ID3标记是针对MP3文件格式而设计的。 有关格式的其他信息：

* ID3标记可用于MP3和mp3PRO文件。
* WAV没有标记。
* WMA具有不允许开源实施的专有标记。
* Ogg Vorbis使用嵌入到Ogg容器中的Xiph注释。
* AAC使用专有标记格式。

### Exif {#exif}

可交换图像文件格式(Exif)是数字摄影中最常用的元数据格式。 它提供了一种以多种文件格式(如JPEG、TIFF、RIFF和WAV)嵌入元数据属性的固定词汇的方法。 Exif将元数据存储为元数据名称和元数据值对。 这些元数据名称 — 值对也称为标记，切勿与中的标记混淆。 [!DNL Experience Manager]. 现代数码相机创建Exif元数据并提供现代图形软件支持。 Exif格式是元数据管理（尤其是图像）的最低通用分母。

Exif的一个主要限制是一些流行的图像文件格式(如BMP、GIF或PNG)不支持它。

由Exif定义的元数据字段通常具有技术性质，在描述性元数据管理中的用处有限。 因此， [!DNL Experience Manager Assets] 提供将Exif属性映射到 [通用元数据架构](metadata-schemas.md) 并进入 [XMP](xmp-writeback.md).

### 其他元数据 {#other-metadata}

可以从文件中嵌入的其他元数据包括 [!DNL Microsoft Word]， [!DNL PowerPoint]， [!DNL Excel]，等等。

## 了解元数据架构 {#metadata-schemata}

元数据架构是可在各种应用程序中使用的元数据属性定义的预定义集。 属性始终与资产关联，这意味着属性与资源“关于”。

如果不存在符合您需求的元数据架构，您还可以设计自己的元数据架构。 不要复制现有信息。 在组织内，将架构分隔开可以更轻松地共享元数据。 [!DNL Experience Manager] 为您提供最常用元数据架构的默认列表。 列表可帮助您快速启动元数据策略并快速选择所需的元数据属性。

下面列出了支持的元数据架构。

### 标准元数据 {#standard-metadata}

* DC - [!DNL Dublin Core] 是一组重要且广泛使用的元数据。
* DICOM — 医学数字成像和通信。
* `Iptc4xmpCore` 和 `iptc4xmpExt`  — 国际新闻通讯标准包含许多特定主题的元数据。
* RDF — 资源描述框架 — 用于通用语义Web元数据。
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ`  — 基本作业票证。

### 特定于应用程序的元数据 {#application-specific-metadata}

特定于应用程序的元数据包括技术和描述性元数据。 如果使用此类元数据，则其他应用程序可能无法使用该元数据。 例如，其他图像渲染应用程序可能无法访问 [!DNL Adobe Photoshop] 元数据。 您可以创建工作流步骤，将特定于应用程序的资产更改为标准资产。

* ACDSee — 由管理的元数据 [!DNL ACDSee] 程序。 请参阅 [www.acdsee.com/](https://www.acdsee.com/).
* 专辑 —  [!DNL Adobe Photoshop Album].
* CQ — 使用者 [!DNL Experience Manager Assets].
* DAM — 使用者 [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] 是用于Windows操作系统的元数据和文件管理的工具集合。
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto和MP - Microsoft Photo。
* PDF和PDF/X。
* Photoshop和psAux - [!DNL Adobe Photoshop].

### Digital Rights Management(DRM)元数据 {#digital-rights-management-metadata}

* 抄送 - [!DNL Creative Commons].
* [!DNL XMPRights]。
* 加 —  [图片授权通用系统](https://www.useplus.com).
* 棱镜 —  [发布行业标准元数据的要求](https://www.idealliance.org/prism-metadata).
* PRL — 棱镜权限语言。
* PUR - PRISM使用权限。
* `xmpPlus` - PLUS与XMP的集成。

### 特定于照片的元数据 {#photography-specific-metadata}

* Exif — 摄像头提供的技术信息，包括GPS位置。
* CRS - [!DNL Camera Raw] 架构。
* `iptc4xmpCore` 和 `iptc4xmpExt`.
* TIFF — 图像元数据(不仅适用于TIFF图像)。

### 打印特定的元数据 {#print-specific-metadata}

* PDF和PDF/X - Adobe PDF和第三方应用程序。
* 棱镜 —  [发布行业标准元数据的要求](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG`  — 分页文本的XMP元数据。

### 特定于多媒体的元数据 {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM`  — 介质管理。

## 元数据架构引用 {#metadata-schemata-reference}

以下参考包含有关特定元数据架构（按字母顺序）的信息，以及属性及其定义的列表。

### 都柏林核心 {#dublin-core}

都柏林核心元数据提供了一套标准化的约定，用于描述资源以便于查找。 在 [!DNL Assets]的Dublin Core介绍了数字资产，包括视频、声音、图像和文档。

简单的Dublin核心元数据元素集(DCMES)包含15个元数据元素，如下表所示。 每个Dublin Core元素都是可选的，并且可以重复。 您可以添加或删除都柏林核心元数据信息，就像添加或删除特定于媒体类型的元数据信息一样。

除了DCMES之外，还有由Dublin核心计划创建的其他元数据元素。 请参阅 [都柏林核心计划](https://dublincore.org/) 以了解更多信息。

| 属性 | 描述 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| 参与者 | 负责向内容投稿的个人或公司。 |
| 覆盖 | 资产覆盖的地理位置或时间段。 |
| 创建者 | 负责创建内容的人或公司。 |
| 日期 | 与资产关联的日期或时间段。 |
| 说明 | 有关资产的更多信息。 |
| 格式 | 资源的文件格式、物理介质或尺寸。 [!DNL Experience Manager] 用途 `dc:format` 表示资产的MIME类型。 |
| 标识符 | 对资源的唯一引用。 |
| 语言 | 资源的语言(例如， `en` （英语）。 |
| 发布者 | 负责提供资产的个人或公司。 |
| 关系 | 相关资产。 |
| 权限 | 有关谁拥有此资源的权限的信息。 |
| source | 从中派生资产的相关资产。 |
| 对象 | 资源的主题。 |
| 标题 | 资源的名称。 |
| 类型 | 资产的性质或类型。 |

### IPTC {#iptc}

国际新闻通讯委员会(IPTC)是由世界各地的新闻机构组成的联盟，其目标之一是制定和维护技术标准。 IPTC为图像定义了一组照片元数据标准，这些标准几乎为摄影师所普遍接受。 这些元数据标准是20世纪90年代创建的更广泛标准IPTC信息交换模型(IIM)的一部分。

虽然IPTC标头信息已大部分被XMP取代，但XMP可以使用IPTC核心架构和扩展架构。 在图像程序中，XMP和IPTC属性都是同步的。

## 元数据驱动的工作流 {#metadata-driven-workflows}

创建元数据驱动的工作流可帮助您自动化某些流程，从而提高效率。 在元数据驱动的工作流中，工作流管理系统读取工作流并因此执行一些预定义的操作。 例如，可以使用元数据驱动工作流的某些方法：

* 工作流可以检查图像是否具有标题。 如果不包含，系统会通知您添加标题。
* 工作流可以检查资产上的版权声明是否允许分发。 因此，系统会将资产发送到一台服务器或另一台服务器。
* 工作流可以检查没有预定义、强制性元数据的资产，或者检查具有 *无效* 元数据。

## XMP 元数据 {#xmp-metadata}

XMP（可扩展元数据平台）是使用的元数据标准 [!DNL Adobe Experience Manager Assets] 用于所有元数据管理。 XMP为各种应用程序的元数据的创建、处理和交换提供了一个标准格式。

除了提供可以嵌入到所有文件格式的通用元数据编码之外，XMP还提供了 [内容模型](#xmp-core-concepts) 和 [受Adobe支持](#advantages-of-xmp) 和其他公司，以便将XMP的用户与 [!DNL Assets] 拥有强大的平台进行构建。

此 [XMP规范](https://www.adobe.com/devnet/xmp.html) 可在Adobe中使用。

### 什么是XMP？ {#what-is-xmp}

Adobe首先引入了XMP标准作为Adobe Acrobat软件产品的一部分。 从那时起，XMP标准被广泛采用。 [!DNL Assets] 原生支持XMP — 由Adobe带头的可扩展元数据平台。 XMP是在数字资产中处理和存储标准化的专有元数据的标准。 XMP旨在作为允许多个应用程序有效地使用元数据的通用标准。

例如，生产专业人员使用Adobe应用程序中内置的XMP支持跨多种文件格式传递信息。 [!DNL Assets] 存储库提取XMP元数据并使用它来管理内容生命周期，并提供创建自动化工作流程的功能。

XMP通过提供数据模型、存储模型和架构，标准化元数据的定义、创建和处理方式。 本节将介绍所有这些概念。

来自EXIF、ID3或Microsoft Office的所有旧元数据会自动转换为XMP，可以扩展该架构以支持客户特定的元数据架构，例如产品目录。

XMP中的元数据由一组属性组成。 这些属性始终与称为资源的特定实体相关联；即，属性与资源相关。 对于XMP，资源始终是资源。

### XMP生态系统 {#xmp-ecosystem}

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

### XMP的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP具有以下优势：

* 基于XMP的元数据功能非常强大且粒度非常细。
* XMP允许您为一个资产设置多个值。
* XMP具有标准化的编码，这使您能够轻松交换元数据。
* XMP是可扩展的。 您可以将其他信息添加到资源中。

XMP标准设计为可扩展，允许您向XMP数据添加自定义类型的元数据。 而EXIF则否 — 它有一个无法扩展的固定属性列表。

>[!NOTE]
>
>XMP通常不允许嵌入二进制数据类型。 要在XMP中携带二进制数据（例如缩略图图像），必须以XML友好格式对其进行编码，例如 `Base64`.

### XMP概念 {#xmp-core-concepts}

以下部分介绍XMP的核心概念，包括命名空间和架构、属性和值以及语言替代项。

#### 命名空间和架构 {#namespaces-and-schemata}

XMP架构是公共XML命名空间中的一组属性名称，其中包括数据类型和描述性信息。 XMP架构由其XML命名空间URI标识。 使用命名空间可以防止不同架构中具有相同名称但不同含义的属性之间发生冲突。

例如， `Creator` 两个独立设计的架构中的资产可能是指创建资产的人，也可能是指创建资产的应用程序(例如，Adobe Photoshop)。

#### 属性和值 {#properties-and-values}

XMP可能包括来自一个或多个架构的属性。 例如，许多Adobe应用程序使用的典型子集可能包括：

* 都柏林核心架构： `dc:title`， `dc:creator`， `dc:subject`， `dc:format`， `dc:rights`.
* XMP基本架构： `xmp:CreateDate`， `xmp:CreatorTool`， `xmp:ModifyDate`， `xmp:metadataDate`.
* XMP权限管理架构： `xmpRights:WebStatement`， `xmpRights:Marked`.
* XMP媒体管理模式： `xmpMM:DocumentID`.

#### 替代语言 {#language-alternatives}

XMP允许您添加 `xml:lang` 属性到文本属性以指定文本的语言。

## 使用IPTC元数据 {#support-for-iptc-metadata}

了解如何 [!DNL Adobe Experience Manager Assets] 支持通过以下方式添加到资产的IPTC元数据、创意评级和关键字 [!DNL Adobe Bridge] 和其他 [!DNL Adobe Creative Cloud] 应用程序。

[!DNL Adobe Experience Manager Assets] 支持广泛用于描述资源的IPTC元数据标准。 这边， [!DNL Assets] 提高了摄影师、创意公司、图书馆、博物馆等各方对其形象的接受度。

现在，资产的默认元数据架构采用IPTC Core和IPTC扩展元数据架构来定义全面的元数据属性，这些属性允许用户添加有关图像中显示的人员、位置和产品的精确可靠数据。 它还支持有关创建映像的日期、名称和标识符，以及表达权限信息的灵活方式。

资产的“属性”页面现在包含单独的选项卡，以便在可编辑字段中显示IPTC核心和IPTC扩展元数据。

1. 从 [!DNL Assets] 用户界面，选择图像。
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

此 **[!UICONTROL IPTC]** 选项卡 [!UICONTROL 属性] 页面还显示通过Adobe Bridge和其他Adobe Creative Cloud应用程序添加到资源的关键字。 您还可以编辑这些关键字并从 **[!UICONTROL IPTC]** 选项卡。

![关键字](assets/keywords-in-iptc-tab.png)
