---
title: 在Adobe Experience Manager资产中支持XMP元数据。
description: 了解Experience Manager资产用于元数据管理的XMP（可扩展元数据平台）元数据标准。 XMP 为在各种应用程序中创建、处理和交换元数据提供了一种标准格式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 66%

---


# XMP 元数据 {#xmp-metadata}

XMP（可扩展元数据平台）是Adobe Experience Manager资产用于所有元数据管理的元数据标准。 XMP 为在各种应用程序中创建、处理和交换元数据提供了一种标准格式。

Aside from offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich [content model](xmp.md#xmp-core-concepts) and is [supported by Adobe](xmp.md#advantages-of-xmp) and other companies, so that users of XMP in combination with Assets have a powerful platform to build upon.

Adobe 支持 [XMP 规范](https://www.adobe.com/devnet/xmp.html)。

## What is XMP? {#what-is-xmp}

 资产在本机支持由 Adobe 率先推出的 XMP，即可扩展元数据平台。XMP是处理和存储数字资产中标准化的专有元数据的标准。 XMP 旨在形成通用标准，从而让多个应用程序能够高效地处理元数据。

例如，专业制作人员可以使用Adobe应用程序中内置的XMP支持，跨多种文件格式传递信息。 资产存储库会提取XMP元数据，并使用它管理内容生命周期，并优惠创建自动化工作流的能力。

XMP 通过提供数据模型、存储模型和架构，使元数据的定义、创建和处理方式实现标准化。本节将介绍所有这些概念。

来自 EXIF、ID3 或 Microsoft Office 的所有旧版元数据都将自动转换为 XMP，而 XMP 可进行扩展，以支持特定于客户的元数据架构，例如产品目录。

XMP 中的元数据包含一组属性。这些属性始终与称为资源的特定实体相关联； 即，属性是“关于”资源的。 对于 XMP，资源始终是指资产。

### Adobe {#adobe}

Adobe 首先在 Adobe Acrobat 软件产品中引入了 XMP 标准。此后，XMP 标准逐渐被广泛采用。

### XMP ecosystem {#xmp-ecosystem}

XMP 定义了一个可与任何定义的元数据项集一起使用的[元数据](https://en.wikipedia.org/wiki/Metadata)模型。XMP 还为基本属性定义了一个特定的[架构[，这些基本属性可用于记录资源经过多个处理步骤的历史记录：从拍摄、](https://en.wikipedia.org/wiki/XML_schema)扫描](https://en.wikipedia.org/wiki/Image_scanner)或创作为文本，到照片编辑步骤（如[裁剪](https://en.wikipedia.org/wiki/Cropping_%28image%29)或颜色调整），再到组合到最终图像中。XMP 允许每个软件程序或设备向数字资源添加其自己的信息，该信息可保留在最终的数字文件中。

XMP 最常使用 [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [资源描述框架](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) 的子集进行序列化和存储，该子集又以 [XML](https://en.wikipedia.org/wiki/XML) 形式表示。

## XMP 的优势 {#advantages-of-xmp}

与其他编码标准和架构相比，XMP 具有以下优势：

* 基于 XMP 的元数据非常强大且精细。
* XMP 允许您为一个属性设置多个值。
* XMP 采用标准化的编码，让您可以轻松交换元数据。
* XMP 具有可扩展性。您可以向资产中添加其他信息。

### 可扩展 {#extensible}

XMP标准设计为可扩展，允许您向XMP数据中添加自定义类型的元数据。 而EXIF则不然——它具有无法扩展的属性的固定列表。

>[!NOTE]
>
>XMP 一般不允许嵌入二进制类型的数据。To carry binary data in XMP, for example, thumbnail images, they must be encoded in an XML-friendly format such as `Base64`.

## XMP 核心概念 {#xmp-core-concepts}

以下各节介绍了 XMP 的核心概念，包括命名空间和架构、属性和值以及替代语言。

### 命名空间和架构 {#namespaces-and-schemata}

XMP 架构是通用 XML 命名空间中的一组属性名称，包括数据类型和描述性信息。
XMP 架构采用其 XML 命名空间 URI 进行标识。使用命名空间可以防止不同架构内名称相同但含义不同的属性之间发生冲突。

For example, the `Creator` property in two independently designed schemas might mean the person who created the asset or it could mean the application that created the asset (for example, Adobe Photoshop).

### 属性和值 {#properties-and-values}

XMP 可以包含来自一个或多个架构的属性。

例如，很多 Adobe 应用程序使用的典型子集包括以下架构：

* 都柏林核心架构：dc:title、dc:creator、dc:subject、dc:format、dc:rights
* XMP 基本架构：xmp:CreateDate、xmp:CreatorTool、xmp:ModifyDate、xmp:metadataDate
* XMP 权限管理架构：xmpRights:WebStatement、xmpRights:Marked
* XMP 媒体管理架构：xmpMM:DocumentID

### 替代语言 {#language-alternatives}

XMP 支持向文本属性添加 `xml:lang` 属性以指定文本的语言。
