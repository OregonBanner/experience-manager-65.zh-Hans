---
title: 简介 [!DNL Adobe Experience Manager Assets]
description: 了解什么是数字资产管理、其用例以及 [!DNL Adobe Experience Manager Asset] 主动出击。
contentOwner: AG
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 38%

---

# 关于 [!DNL Adobe Experience Manager Assets] 作为DAM解决方案 {#administering-assets}

[!DNL Assets] 是一个数字资产管理(DAM)工具，它是 [!DNL Experience Manager] 平台，使您的企业能够管理和分发数字资产。 组织内的用户可以管理、存储和访问多种类型的数字资产，如图像、视频、文档、音频剪辑、3D文件和富媒体，以便在Web上使用、在印刷品中使用和进行数字分发。

## 什么是数字资产管理？ {#what-is-digital-asset-management}

[!DNL Assets] 允许在整个企业范围内共享和分发某组织的关键数字资产。组织内的用户可以通过 Web 界面（或者 CIFS 或 WebDAV 文件夹）存储、管理和访问数字资产，例如图像、图表、音频、视频和文档。

[!DNL Assets] 功能 [!DNL Experience Manager] 可让您执行以下操作：

* 添加和共享多种文件格式的图像、文档、音频文件和视频文件。
* 通过按标记、灯箱或星星（您的收藏夹）对资源进行分组来管理资源。 可以在资产中添加批注。
* 通过搜索文件名、完整的文档文本、日期、文档类型和标记来查找资产。
* 添加或编辑资产的元数据信息。元数据会与相应的资产一起自动进行版本控制。您可以导入或导出资产元数据。
* 执行图像编辑功能，例如缩放和添加图像筛选器。使用 WebDAV 或 CIFS 文件夹同时导入和导出多个数字资产。
* 使用工作流和通知联合处理和下载任意资产集并管理资产的访问权限。

### [!DNL Experience Manager Assets] 与集成 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 与完全集成 [!DNL Sites] 和可以无缝地用于所有用例。 例如，在创作网页时， [!DNL Sites] 作者可以通过Content Finder查找和使用数字资产。 的用户界面 [!DNL Assets] 与 [!DNL Sites]. 参见 [Sites概述](/help/sites-authoring/page-authoring.md) 以了解完整的详细信息。

基本用户界面与相同 [!DNL Sites]. 参见 [站点概述](/help/sites-authoring/page-authoring.md) 以了解完整的详细信息。

### 数字资产管理与图像组件 {#digital-asset-management-versus-image-component}

在决定是将图像放入DAM存储库还是使用图像组件时，请考虑图像生命周期：

* 如果图像与页面具有相同的生命周期，请使用图像组件。
* 如果图像具有单独的生命周期，例如，如果您使用图像两次或在 WCM 之外使用图像，则使用 [!DNL Assets].

## 什么是数字资产？ {#what-are-digital-assets}

资产是指数字文档、图像、视频或音频（或其中任一部分），它们可以具有多个演绎版，并可以具有子资产（例如，Photoshop文件中的图层、PowerPoint文件中的幻灯片、PDF中的页面、ZIP中的文件）。

资产本质上是一个具有元数据、演绎版和子资产的二进制文件。有关详细信息，请参阅 [DAM 性能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>上传和/或编辑大量资产（特别是图像）可能会影响性能 [!DNL Experience Manager] 部署。

### [!DNL Experience Manager Assets] 术语 {#aem-assets-terminology}

在中使用数字资产时 [!DNL Experience Manager]，您需要了解以下术语：

* **收藏集**：资产集合，基于物理位置（文件夹）、公共属性（保存的搜索文件夹）或用户选择（灯箱文件夹）。

* **元数据** [!DNL Assets] 具有元数据；例如，作者、到期日、DRM信息(Digital Rights Management)等。 元数据受访问控制。[!DNL Assets] 支持以下各种常见的现成元数据架构：

   * Dublin Core：包括作者、描述、日期、主题等。
   * IPTC：包括事件、模型、位置等。
   * WCM：包括页面属性、 [!UICONTROL 准时] 和 [!UICONTROL 关闭时间]，等等。

* **标记**： [!DNL Assets] 可以进行标记和分类。 参见 [组织资源](/help/assets/organize-assets.md).

* **演绎版**：演绎版是资源的二进制表示形式。 [!DNL Assets] 始终具有主要表示形式 — 已上传文件的主要表示形式。 它们可以采用创建的任何数量的其他表示形式，例如定制工作流程步骤或资产上传时创建的表示形式。演绎版可能大小不同、分辨率不同、添加了水印，或者更改了其他一些特性。

* **版本**：版本控制可在特定时间点创建数字资产的快照。 您可以将资产恢复至以前的版本。参见 [版本控制 [!DNL Assets]](manage-assets.md#asset-versioning).

* **子资产**：子资产是构成资产的资产，例如，中的层 [!DNL Adobe Photoshop] PDF文件中的一个或多个页。 In [!DNL Assets]，您可以像管理资产一样管理子资产。

### 如何使用数字资产 {#how-to-work-with-assets}

您可以对资产或收藏集执行操作。这些操作包括创建或修改资产、收藏集和演绎版。您在资产上执行的许多基本操作（上传、删除、更新、保存子资产）都会触发预配置的工作流。 这些功能会自动打开 [!DNL Assets] 并在以下部分中进行了详细描述： [!DNL Assets] 媒体处理程序。

您可以使用这些预配置的工作流执行的任务：

* 将资源保存在存储库中，或从存储库中删除资源。
* 提取并保存资源的元数据；单个元数据项将另存为XMP。
* 为资源生成演绎版和缩略图；包括根据需要自动调整大小和裁切。
* 必要时对资产进行转码。 例如，供移动设备和 Web 使用的视频将以 24 帧/秒的速率转码，供下载的视频将以 30 帧/秒的速率转码。用于移动和Web的音频使用128 Kbps进行转码，用于下载的音频使用192 Kbps。

当然，您也可以手动应用工作流。请参阅 [ Assets 媒体处理程序](media-handlers.md)，以获取默认工作流的列表。

## [!DNL Experience Manager Assets] 和 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

参见 [Assets和Media Library](medialibrary.md) 以了解关于这些差异的信息。

>[!MORELIKETHIS]
>
>* [视频介绍 — Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [了解元数据概念](/help/assets/metadata-concepts.md)

