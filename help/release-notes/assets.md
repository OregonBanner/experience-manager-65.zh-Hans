---
title: AEM Assets 发行说明
description: Adobe Experience Manager 6.5 Assets 的新增功能和增强功能。
uuid: f785029d-e0fd-494f-b215-7b4caca4e806
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 1ab34a42-2f0e-4b05-a7b6-2fc8dca07ef5
docset: aem65
translation-type: tm+mt
source-git-commit: 95d9ed8a0ccfa7651b83058d337511dd6b15665f

---


# AEM Assets 发行说明{#aem-assets-release-notes}

以下是 AEM 6.5 Assets 发行版的主要功能。

## 与 Adobe Creative Cloud 和创意工作流集成 {#integration-with-adobe-creative-cloud-and-creative-workflows}

AEM 提供了多种方法来与 Adobe Creative Cloud 集成并共享资产，以供在创意、营销或业务团队密切合作的工作流中使用。AEM 6.5 将继续改进并进一步简化该集成，以提供更多商机和简化现有方法。

继续阅读以了解 AEM 6.5 的具体功能和集成，您可以利用这些功能和集成来更好地支持您的内容速度用例。

### Adobe Asset Link {#aal}

Adobe Asset Link 加强了内容创建过程中创意人员与营销人员之间的协作。创意人员无需离开他们最熟悉的应用程序，就可以访问存储在 Adobe Experience Manager Assets (AEM Assets) 中的内容。创意人员可以使用 Photoshop、Illustrator 和 InDesign 应用程序中的应用程序内面板无缝浏览、搜索、签出和签入资产。

Adobe Asset Link 是 [Creative Cloud 企业版](https://www.adobe.com/creativecloud/business/enterprise.html)产品的一部分。有关更多信息，包括 AEM 部署的必要配置，请参阅 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)。

![资产搜索 Photoshop](assets/asset_search_photoshop.png)

### Adobe Stock 集成 {#stock}

贵组织可以在AEM资产中使用其Adobe Stock企业计划，以确保许可资产广泛适用于您的创意和营销项目。 您可以使用AEM的强大DAM功能快速查找、预览和许可保存在AEM中的Adobe Stock资源。

Adobe Stock 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。

有关更多信息，请参阅[在 AEM Assets 中使用 Adobe Stock 资产](/help/assets/aem-assets-adobe-stock.md)。

![在 AEM Assets 中预览 Adobe Stock 图像和许可证](assets/stock_image_preview_license_options.png)

在 AEM Assets 中预览 Adobe Stock 图像和许可证

![在 AEM 中搜索并筛选已许可 Adobe Stock 图像](assets/aem-search-filters2.jpg)

在 AEM 中搜索并筛选已许可 Adobe Stock 图像

### Dynamic references in Adobe InDesign {#dynamic-references-in-indesign}

Adobe InDesign 文件中使用的 AEM Assets 是动态的。如果在 JCR 层次结构中移动引用的资产，则引用会自动更新。有关更多信息，请参阅[管理合成资产](/help/assets/managing-linked-subassets.md)。

## Brand Portal 功能 {#brand-portal-capabilities}

AEM Assets Brand Portal 可帮助您轻松获取及有效控制已批准的资产，并在设备间安全地将该资产分发给外部供应商/代理商和内部企业用户。它有助于提高资产共享的效率、加快资产的上市时间，并消除不合规使用和未授权访问的风险。

有关更多信息，请参阅 [Brand Portal 中的新增功能](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html)。

## 连接的资产 {#connectedassets}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和所需的数字资产位于不同的容器中。

AEM Sites 提供了创建网页的功能，AEM Assets 是为网站提供所需资产的数字资产管理 (DAM) 系统。AEM 现在可通过集成 AEM Sites 和 AEM Assets 来支持上述用例。

有关更多信息，请参阅[使用“连接的资产”中的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

![将 DAM 资产从 Sites 页面中的 AEM 实例拖放到其他 AEM 实例上](assets/connected-assets-drag-and-drop-only.gif)

将 DAM 资产从 Sites 页面中的 AEM 实例拖放到其他 AEM 实例上

## Dynamic Media {#dynamic-media}

Dynamic Media 在 AEM Assets 中提供了增强的富媒体创作和交付，以提供沉浸式的个性化前沿体验。通过上传单个高品质主资产并使用我们的高级云渲染和查看器，您可以即时提供任意演绎版组合，以支持贵组织的媒体策略。

有关新 Dynamic Media 功能的更多详细信息，请参阅 [Dynamic Media 发行说明](https://marketing.adobe.com/resources/help/en_US/s7/release_notes/)。

### 360 视频支持 {#video-support}

使用 Dynamic Media 的前沿查看器可直接在 AEM 中管理您的 360 视频文件，以向桌面、移动设备和 VR 头戴设备交付 VR 体验。有关更多信息，请参阅[使用 360 视频](/help/assets/360-video.md)。

### 自定义视频缩略图 {#custom-video-thumbnails}

您现在可以使用视频本身的帧或存储在 DAM 中的其他内容自定义视频资产的缩略图。有关其他说明，请参阅[关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

### 辅助功能增强功能 {#accessibility-enhancements}

Dynamic Media 查看器现在支持增强的辅助功能，如 Aria 支持、屏幕阅读器和替换文本。有关其他详细信息，请参阅 [Dynamic Media 查看器发行说明](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html)。

## 搜索体验增强功能 {#search-experience-enhancement}

从AEM 6.5开始，营销人员可以从搜索结果页面更快地发现所需的资产。 即使还未应用搜索筛选器，也会为搜索 Facet 更新资产数量。查看筛选后的预计计数有助于用户有效地浏览搜索结果。有关详细信息，请参 [阅在AEM中搜索资产](../assets/search-assets.md)。

![在搜索 Facet 中查看未筛选搜索结果时的资产数量](/help/assets/assets/asset_search_results_in_facets_filters.png)

在搜索 Facet 中查看未筛选搜索结果时的资产数量。

## 可用性增强功能 {#usability-enhancement}

您现在可以一次性选择文件夹中或搜索结果中的所有资产。该功能可以帮助您快速管理多个资产。选中该复选框即可选择适合该方案（例如搜索结果）的所有资产，而不仅仅是 AEM 界面中可见的资产。

![使用“全选”选项可一键选择所有资产。](assets/select-all-in-aem-assets.gif)

使用“全选”选项可一键选择所有资产。

## 元数据增强功能 {#metadata-enhancements}

Assets 允许您为资产文件夹创建元数据架构，这些架构定义了文件夹属性页面中显示的布局和元数据。您现在既可以将文件夹元数据架构分配给现有文件夹，也可以在创建新文件夹时分配。有关更多信息，请参阅[文件夹元数据架构](/help/assets/folder-metadata-schema.md)。

指定级联元数据时，可以在运行时从 JSON 文件加载选项，而不是在表单中手动键入选项。有关更多信息，请参阅[级联元数据](/help/assets/cascading-metadata.md)。

## 报告增强功能 {#reporting-enhancements}

内容片段和链接共享现已包含在“已下载资产”报表中。有关更多信息，请参阅 [Assets 报表](/help/assets/asset-reports.md)。
