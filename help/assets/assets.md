---
title: Introduction to [!DNL Adobe Experience Manager Assets].
description: 了解数字资产管理、其使用案例和 [!DNL Adobe Experience Manager Asset] 分支。
contentOwner: AG
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 33%

---


# 关 [!DNL Adobe Experience Manager Assets] 于DAM解决方案 {#administering-assets}

[!DNL Assets] 是一种数字资产管理(DAM)工具，它是平台的一个 [!DNL Experience Manager] 组成部分，使您的企业能够管理和分发数字资产。 组织内的用户可以管理、存储和访问多种类型的数字资产，如图像、视频、文档、音频剪辑、3D文件和富媒体，以用于Web、印刷和数字分发。

## What is Digital Asset Management? {#what-is-digital-asset-management}

[!DNL Assets] 允许在整个企业范围内共享和分发某组织的关键数字资产。整个组织的用户可以通过Web界面（或CIFS或WebDAV文件夹）存储、管理和访问数字资产，如图像、图形、音频、视频和文档。

[!DNL Assets] 功能 [!DNL Experience Manager] 允许您执行以下操作：

* 添加和共享多种文件格式的图像、文档、音频文件和视频文件。
* 通过按标记、Lightbox或星形（您的收藏夹）对资产进行分组来管理资产。 可以在资产中添加批注。
* 通过搜索文件名、完整的文档文本、日期、文档类型和标记来查找资产。
* 添加或编辑资产的元数据信息。元数据会与相应的资产一起自动进行版本控制。 您可以导入或导出资产元数据。
* 执行图像编辑功能，例如缩放和添加图像筛选器。使用 WebDAV 或 CIFS 文件夹同时导入和导出多个数字资产。
* 使用工作流和通知联合处理和下载任意资产集并管理资产的访问权限。

### [!DNL Experience Manager Assets] 与 [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 与所有用 [!DNL Sites] 例完全集成并无缝工作。 例如，在创作网页时，作 [!DNL Sites] 者可以通过内容查找器查找和使用数字资产。 其用户界 [!DNL Assets] 面与之相同 [!DNL Sites]。 有关 [完整详细信息](/help/sites-authoring/page-authoring.md) ，请参阅站点概述。

基本用户界面与基本用户界面相同 [!DNL Sites]。 有关 [完整详细信息](/help/sites-authoring/page-authoring.md) ，请参阅站点概述。

### 数字资产管理与图像组件 {#digital-asset-management-versus-image-component}

在确定是将图像放入DAM存储库还是使用图像组件时，请考虑图像生命周期：

* 如果图像具有与页面相同的生命周期，请使用图像组件。
* 如果图像具有单独的生命周期，例如，如果您使用图像两次或在 WCM 之外使用图像，则使用 [!DNL Assets].

## What are digital assets? {#what-are-digital-assets}

资产是指数字文档、图像、视频或音频（或其一部分），可以具有多个演绎版，并可以具有子资产（例如，photoshop文件中的图层、PowerPoint文件中的幻灯片、pdf中的页面、ZIP中的文件）。

资产本质上是一个具有元数据、演绎版和子资产的二进制文件。有关详细信息，请参阅 [DAM 性能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>Uploading and/or editing a large volume of assets (particularly images) can impact the performance of your [!DNL Experience Manager] deployment.

### [!DNL Experience Manager Assets] 术语 {#aem-assets-terminology}

When working with digital assets in [!DNL Experience Manager], you need to understand the following terminology:

* **集合**:资产集合，基于物理位置（文件夹）、常用属性（保存的搜索文件夹）或用户选择（lightbox文件夹）。

* **元数据**[!DNL Assets] 包含元数据；例如，作者、到期日、DRM信息(Digital Rights Management)等。 元数据受访问控制。[!DNL Assets] 支持以下各种常见的现成元数据架构：

   * Dublin Core：包括作者、描述、日期、主题等。
   * IPTC：包括事件、模型、位置等。
   * WCM:包括页面属 [!UICONTROL 性、开] 始 [!UICONTROL 时间和结束]时间，等等。

* **标记**: [!DNL Assets] 可以标记和分类。 请参阅 [组织资产](/help/assets/organize-assets.md)。

* **演绎版**:演绎版是资产的二进制表示形式。 [!DNL Assets] 始终具有主要表示形式——已上载文件的表示形式。 它们可以采用创建的任何数量的其他表示形式，例如定制工作流程步骤或资产上传时创建的表示形式。演绎版可能大小不同、分辨率不同、添加了水印，或者更改了其他一些特性。

* **版本**:版本控制可创建数字资产在特定时间点的快照。 您可以将资产恢复至以前的版本。See [versioning in Assets](manage-assets.md#asset-versioning).

* **子资产**:子资产是组成资产的资产，例如，文件中的图层 [!DNL Adobe Photoshop] 或PDF文件中的页面。 In [!DNL Assets], you can manage sub-assets as you would assets.

### How to work with assets {#how-to-work-with-assets}

您可以对资产或收藏集执行操作。这些操作包括创建或修改资产、收藏集和演绎版。您对资产执行的许多基本操作——上传、删除、更新、保存子资产——都会触发预配置工作流。 These are automatically turned on in [!DNL Assets] and are described in detail in [!DNL Assets] media handlers.

您可以通过以下预配置任务执行工作流:

* 将资产保存到存储库中，或从存储库中删除资产。
* 提取和保存资产的元数据；单个元数据项将保存为XMP。
* 为资产生成演绎版和缩略图；包括根据需要自动调整大小和裁剪。
* 在必要时转码资产。 例如，用于移动和Web使用的视频以每秒24帧的速率进行转码，下载每秒30帧的视频。 用于移动和Web的音频以128 Kbps的速率进行转码，用于下载的音频以192 Kbps的速率进行转码。

当然，您也可以手动应用工作流。请参阅 [ Assets 媒体处理程序](/help/assets/media-handlers.md)，以获取默认工作流的列表。

## [!DNL Experience Manager Assets] 和 [!DNL MediaLibrary] {#cq-dam-vs-cq-medialibrary}

有关 [差异的信息](/help/assets/medialibrary.md) ，请参阅资产和媒体库。
