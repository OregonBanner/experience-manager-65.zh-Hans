---
title: 发行说明 [!DNL Adobe Experience Manager Assets] 6.5。
description: 对 [!DNL Adobe Experience Manager] 6.5 [!DNL Assets]的新功能和增强。
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 41%

---


# [!DNL Adobe Experience Manager Assets] 发行说明  {#aem-assets-release-notes}

以下是[!DNL Adobe Experience Manager] 6.5 [!DNL Assets]版本的主要功能和亮点。

## 与[!DNL Adobe Creative Cloud]和创意工作流{#integration-with-adobe-creative-cloud-and-creative-workflows}集成

[!DNL Adobe Experience Manager] 提供了多种方法来与 集成并共享资产，以供在创意、营销或业务团队密切合作的工作流中使用。[!DNL Adobe Creative Cloud][!DNL Experience Manager] 6.5 将继续改进并进一步简化该集成，以提供更多商机和简化现有方法。

阅读以了解[!DNL Experience Manager] 6.5的特定功能和集成，这些功能和集成可以帮助您更好地支持内容速度使用案例。

### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 在内容创建过程中加强创意人员和营销人员之间的协作。创意人员可以访问存储在[!DNL Experience Manager Assets]中的内容，而无需离开他们最熟悉的应用程序。 创意人员可以使用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]应用程序中的应用程序内面板无缝地浏览、搜索、注销和登记资产。

[!DNL Adobe Asset Link] 是企业产品 [Creative Cloud的](https://www.adobe.com/cn/creativecloud/business/enterprise.html) 一部分。有关此部署的详细信息（包括[!DNL Experience Manager]部署的必要配置），请参阅[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。

![在Adobe Photoshop搜索资产](assets/asset_search_photoshop.png)

### [!DNL Adobe Stock] 集成  {#stock}

您的组织可以在[!DNL Experience Manager Assets]中使用其[!DNL Adobe Stock]企业计划，确保许可资产广泛适用于您的创意和营销项目。 您可以使用[!DNL Experience Manager]的强大DAM功能快速查找、预览和许可以Experience Manager保存的[!DNL Adobe Stock]资源。

[!DNL Adobe Stock] 服务为设计师和企业提供了数百万种可用于所有创意项目的高品质、精选、免版税的照片、矢量、插图、视频、模板和 3D 资产。

有关详细信息，请参阅[在Experience Manager资产](/help/assets/aem-assets-adobe-stock.md)中使用Adobe Stock资产。

![预览Adobe Stock图像和许可从Experience Manager资产内部获得](assets/stock_image_preview_license_options.png)

*图：预览 [!DNL Adobe Stock] 图像和许可证 [!DNL Experience Manager Assets]。*

![在Experience Manager中搜索和过滤获得许可的Adobe Stock图像](assets/aem-search-filters2.jpg)

*图：在中搜索和过滤许 [!DNL Adobe Stock] 可的图 [!DNL Experience Manager]像。*

### [!DNL Adobe InDesign] {#dynamic-references-in-indesign}中的动态引用

[!DNL Experience Manager Assets] 文件中 [!DNL Adobe InDesign] 使用的是动态的。如果引用的资产在存储库中移动，则引用会自动更新。 有关详细信息，请参阅[如何管理复合资产](/help/assets/managing-linked-subassets.md)。

## Brand Portal 功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 可帮助您轻松获取及有效控制已批准的资产，并在设备间安全地将该资产分发给外部供应商/代理商和内部企业用户。它有助于提高资产共享的效率、加快资产的上市时间，并消除不合规使用和未授权访问的风险。

有关更多信息，请参阅 [Brand Portal 中的新增功能](https://helpx.adobe.com/experience-manager/brand-portal/using/whats-new.html)。

## 连接的资产 {#connectedassets}

在大型企业中，可以分发创建网站所需的基础环境。有时，网站创建功能和所需的数字资产位于不同的容器中。

[!DNL Experience Manager Sites] 提供了创建网页的功能， 是为网站提供所需资产的数字资产管理 (DAM) 系统。[!DNL Experience Manager Assets][!DNL Experience Manager] 现在通过集成和支持上述用 [!DNL Sites] 例 [!DNL Assets]。请参阅[如何配置和使用“已连接资产”功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![将资产从部署拖 [!DNL Experience Manager] 动到其 [!DNL Sites] 他部署的页 [!DNL Experience Manager] 面](assets/connected-assets-drag-and-drop-only.gif)

*图：将资产从部署拖 [!DNL Experience Manager] 动到其 [!DNL Sites] 他部署的页面 [!DNL Experience Manager] 上。*

## Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 提供增强的富媒体创作和投放 [!DNL Experience Manager Assets] 功能，以推动身临其境和个性化的前沿体验。通过上传单个高质量主控资产，并使用我们的高级云渲染和查看器，您可以实时传送任意组合的演绎版以支持组织的媒体战略。

有关新增[!DNL Dynamic Media]功能的详细信息，请参阅[Dynamic Media发行说明](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/release-notes/s7rn2017.html)。

### 360视频支持{#video-support}

使用最先进的查看器直接在[!DNL Experience Manager]中管理360视频文件，将VR体验交付到台式机、移动设备和VR头盔。 有关更多信息，请参阅[使用 360 视频](/help/assets/360-video.md)。

### 自定义视频缩略图{#custom-video-thumbnails}

您现在可以使用视频本身的帧或存储在 DAM 中的其他内容自定义视频资产的缩略图。有关其他说明，请参阅[关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

### 辅助功能增强功能 {#accessibility-enhancements}

[!DNL Dynamic Media] 查看器现在支持增强的辅助功能，如Aria支持、屏幕阅读器和替代文本。有关其他详细信息，请参阅 [Dynamic Media 查看器发行说明](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)。

## 搜索体验增强功能  {#experience-enhancement-for-searching}

[!DNL Experience Manager] 6.5之后，营销人员可以在搜索结果页面更快地发现所需资产。即使还未应用搜索筛选器，也会为搜索 Facet 更新资产数量。查看筛选后的预计计数有助于用户有效地浏览搜索结果。有关详细信息，请参阅[在Experience Manager](../assets/search-assets.md)中搜索资产。

![在搜索 Facet 中查看未筛选搜索结果时的资产数量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*图：在搜索彩块化中查看未筛选搜索结果的资产数量。*

## 可用性增强功能 {#usability-enhancement}

现在，您可以一次性从文件夹或搜索结果中选择所有加载的资产。 该功能可以帮助您快速管理多个资产。此复选框将选择所有符合此方案的资产（例如搜索结果），而不仅仅是[!DNL Experience Manager]界面中可见的资产。

![使用全选选项，只需单击一次即可选择所有加载的资产。](assets/select-all-in-aem-assets.gif)

*图：使用全选选项，只需单击一次即可选择所有加载的资产。*

## 元数据增强功能 {#metadata-enhancements}

[!DNL Assets] 允许您为资产文件夹创建元数据架构，这些架构定义了文件夹属性页面中显示的布局和元数据。您现在既可以将文件夹元数据架构分配给现有文件夹，也可以在创建新文件夹时分配。有关更多信息，请参阅[文件夹元数据架构](/help/assets/metadata-config.md#folder-metadata-schema)。

指定级联元数据时，可以在运行时从 JSON 文件加载选项，而不是在表单中手动键入选项。有关详细信息，请参阅[层叠元数据](/help/assets/metadata-schemas.md#cascading-metadata)。

## 报告增强功能 {#reporting-enhancements}

内容片段和链接共享现在包含在下载的报告中。 有关更多信息，请参阅 [Assets 报表](/help/assets/asset-reports.md)。
