---
title: 关于AEM资产
description: 了解什么是数字资产管理、其使用案例以及Adobe的AEM Asset产品
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 管理资产 {#administering-assets}

资产是一种数字资产管理(DAM)工具，它与AEM平台完全集成，使您的企业能够共享和分发数字资产。 整个组织范围内的用户都可以管理、存储和访问图像、视频、文档、音频剪辑和富媒体（例如 Flash 文件），以供在 Web 中使用、进行印刷及数字分发。

## What is Digital Asset Management? {#what-is-digital-asset-management}

Assets 允许在整个企业范围内共享和分发某组织的关键数字资产。组织内的用户可以通过Web界面（或CIFS或WebDAV文件夹）存储、管理和访问数字资产，如图像、图形、音频、视频和文档。

AEM Assets集成到AEM中后，您可以执行以下操作：

* 添加和共享多种文件格式的图像、文档、音频文件和视频文件。
* 通过按标记、Lightbox或星形（您的收藏夹）对资产进行分组来管理资产。 可以在资产中添加批注。
* 通过搜索文件名、完整的文档文本、日期、文档类型和标记来查找资产。
* 添加或编辑资产的元数据信息。元数据会与相应的资产一起自动版本化。 您可以导入或导出资产元数据。
* 执行图像编辑功能，例如缩放和添加图像筛选器。使用 WebDAV 或 CIFS 文件夹同时导入和导出多个数字资产。
* 使用工作流和通知联合处理和下载任意资产集并管理资产的访问权限。

### AEM Assets已完全集成到CQ WCM中 {#aem-assets-fully-integrated-in-cq-wcm}

AEM资产与CQ WCM完全集成，且功能可通过DAM图标使用：

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png) ![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

然后，可以通过WCM的内容查找器访问在CQ DAM中管理的资产：

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png)

>[!NOTE]
>
>基本的GUI处理与WCM的其他部分相同——有关完整 [的详细信息，请参阅GUI控制台的概述](/help/sites-authoring/page-authoring.md) 。

### 数字资产管理与图像组件 {#digital-asset-management-versus-image-component}

在确定是将图像放入AEM资产还是使用AEM image组件时，请考虑图像生命周期：

* 如果图像具有与页面相同的生命周期，请使用图像组件。
* 如果图像具有单独的生命周期，例如，如果您使用图像两次或在 WCM 之外使用图像，则使用 AEM Assets。

## What are digital assets? {#what-are-digital-assets}

资产是指可以有多个演绎版且可以具有子资产（例如，Photoshop文件中的图层、PowerPoint文件中的幻灯片、pdf中的页面、ZIP中的文件）的数字文档、图像、视频或音频（或其一部分）。

资产本质上是一个具有元数据、演绎版和子资产的二进制文件。有关详细信息，请参阅 [DAM 性能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>上传和／或编辑大量资产（尤其是图像）可能会影响CQ实例的性能。

### AEM Assets terminology {#aem-assets-terminology}

在 AEM 中使用数字资产时，您需要了解以下术语：

* **收藏集** ：资产的收藏集，基于实际位置（文件夹）、常用属性（保存的搜索文件夹）或用户选择（lightbox文件夹）。

* **元数据** 、资产和元数据；例如，作者、到期日、DRM信息（数字权限管理）等。 元数据受访问控制。AEM Assets 支持以下各种常见的现成元数据架构：

   * Dublin Core：包括作者、描述、日期、主题等。
   * IPTC：包括事件、模型、位置等。
   * WCM:包括页面属 [!UICONTROL 性、开始][!UICONTROL 时间和结束时间]，等等。

* **可以标记** “标记资产”并对其进行分类。 请参阅使用标记和管理标记。

* **演绎版** 演绎版是资产的二进制表示形式。 资产始终采用主要表示形式，即已上传文件的表示形式。它们可以采用创建的任何数量的其他表示形式，例如定制工作流程步骤或资产上传时创建的表示形式。演绎版可能大小不同、分辨率不同、添加了水印，或者更改了其他一些特性。

* **版本** “版本控制”可创建数字资产在特定时间点的快照。 您可以将资产恢复至以前的版本。请参阅 AEM Assets 中的版本控制。

* **子资产** -子资产是组成资产的资产，例如，Adobe Photoshop文件中的图层或PDF文件中的页面。 在 AEM Assets 中，您可以像管理资产一样管理子资产。

### How to work with assets {#how-to-work-with-assets}

您可以对资产或收藏集执行操作。这些操作包括创建或修改资产、收藏集和演绎版。您对资产执行的许多基本操作——上传、删除、更新、保存子资产——都会触发预配置的工作流。 这些工作流将在 AEM Assets 中自动开启，AEM Assets 媒体处理程序中对这些工作流进行了详细介绍。

您可以通过以下预配置工作流执行的任务：

* 在存储库中保存或删除资产。
* 提取和保存资产的元数据；单个元数据项目会保存为 XMP。
* 生成资产的演绎版和缩略图；包括在必要时自动调整大小和裁剪。
* 在必要时转码资产。例如，移动和Web使用视频的转码每秒24帧，下载每秒30帧的视频。 供移动设备和 Web 使用的音频将以 128 kbps 的速率转码，供下载的音频将以 192 kbps 的速率转码。

当然，您也可以手动应用工作流。请参阅 [AEM Assets 媒体处理程序](/help/assets/media-handlers.md)，以获取默认工作流的列表。

## AEM Assets and AEM MediaLibrary {#cq-dam-vs-cq-medialibrary}

有关 [差异的信息，请参阅AEM资产和AEM MediaLibrary](/help/assets/medialibrary.md) 。
