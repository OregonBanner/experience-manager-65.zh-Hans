---
title: 元数据架构参考
description: '了解用于描述资产元数据的标准惯例，包括都柏林核心、IPTC和其他元数据模式。 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f3af7041029a1b4dd1cbb4c65bd488b62c7e10c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 81%

---


# Metadata schemata reference {#metadata-schemata-reference}

以下参考内容介绍了关于特定元数据架构（按字母顺序排列）的信息并列出了各个属性及其定义。

## 都柏林核心 {#dublin-core}

都柏林核心元数据提供了一个用于描述资产的标准化惯例集，可使资产更易于查找。在AEM资产中，都柏林核心可描述数字资产，包括视频、声音、图像和文档。

都柏林核心元数据元素集 (DCMES) 很简单，共包含 15 个元数据元素，如下表所示。每个都柏林核心元素都是可选元素，并且可以重复。您可以视需要为特定于媒体类型的元数据添加或删除都柏林核心元数据信息。

In addition to the DCMES, there are other metadata elements created by the Dublin Core Initiative. See the [Dublin Core initiative](https://dublincore.org/) for more information.

| 属性 | 描述 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contributor | 负责贡献内容的个人或公司。 |
| coverage | 资产覆盖的地理位置或时间段。 |
| creator | 负责创建内容的个人或公司。 |
| date | 与资产关联的日期或时间段。 |
| 描述 | 关于资产的详细信息。 |
| format | 资产的文件格式、物理介质或尺寸。AEM用 `dc:format` 于表示资产的MIME类型。 |
| 标识符 | 资产的唯一参考。 |
| 语言 | 资产的语言（例如，en 表示英语）。 |
| publisher | 负责使资产进入可用状态的个人或公司。 |
| relation | 相关的资产。 |
| rights | 关于谁有权使用此资产的信息。 |
| source | 作为资产派生来源的相关资产。 |
| subject | 资产的主题。 |
| 页面 | 资产的名称。 |
| 类型 | 资产的性质或类型。 |

## IPTC {#iptc}

国际出版电讯委员会 (IPTC) 是全世界新闻机构的联盟，其宗旨之一是制定并维护技术标准。IPTC 定义了针对图像的一套照片元数据标准，几乎所有摄影人士都普遍接受这套标准。这些元数据标准从属于一个更广泛的标准，即 20 世纪 90 年代创建的 IPTC 信息交换模型 (IIM)。

尽管 IPTC 标题信息基本上已经被 XMP 所取代，但仍有 IPTC 核心架构和扩展架构可供 XMP 使用。在图像程序中，会同时同步 XMP 属性和 IPTC 属性。
