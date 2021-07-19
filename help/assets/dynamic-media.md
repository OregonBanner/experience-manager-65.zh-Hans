---
title: 使用Dynamic Media
description: 了解如何使用Dynamic Media交付资产以在Web、移动设备和社交网站上使用。
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: 协作，资产管理
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 28%

---

# 使用 Dynamic Media {#working-with-dynamic-media}

[Dynamic Media 有助于按需提供丰富的产品销售和市场营销可视资产，还能根据 Web、移动设备、社交网站等不同销售渠道的各种需求自动调整资产供应情况。](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html)Dynamic Media使用一组主源资产，通过其全球、可扩展、性能优化的网络，实时生成并传送多种丰富内容变体。

Dynamic Media提供交互式查看体验，包括缩放、360度旋转和视频。Dynamic Media以独特的方式整合了Adobe Experience Manager数字资产管理（资产）解决方案的工作流程，以简化和简化数字营销活动管理流程。

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Dynamic Media 的功能 {#what-you-can-do-with-dynamic-media}

通过 Dynamic Media，您可以在发布资产前对其进行管理。[处理数字资产](manage-assets.md)中详细介绍了如何处理资产的一般方法。 一般主题包括上传、下载、编辑和发布资产；查看和编辑属性，以及搜索资产。

仅Dynamic Media功能包括：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)

* [旋转集](spin-sets.md)
* [视频](video.md)
* [交付Dynamic Media资产](delivering-dynamic-media-assets.md)
* [管理资产](managing-assets.md)
* [使用概览创建自定义弹出窗口](custom-pop-ups.md)

另请参阅[设置Dynamic Media](administering-dynamic-media.md)。

>[!NOTE]
>
>要了解使用Dynamic Media与将Dynamic Media Classic与Adobe Experience Manager集成之间的差异，请参阅[Dynamic Media Classic集成与Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)。

## Dynamic Media启用与Dynamic Media禁用 {#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征判断Dynamic Media是否已启用（打开）：

* 下载或预览资产时，可以使用动态演绎版。
* 可以使用图像集、旋转集、混合媒体集。
* 创建了 PTIFF 演绎版。

选择图像资产时，Dynamic Media [enabled](config-dynamic.md#enabling-dynamic-media)会显示不同的资产视图。 Dynamic Media使用按需HTML5查看器。

### 动态演绎版 {#dynamic-renditions}

当 Dynamic Media 处于启用状态时，可以使用图像和查看器预设等动态演绎版（在&#x200B;**[!UICONTROL 动态]**&#x200B;下）。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集和混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

当 Dynamic Media 处于启用状态时，可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF演绎版 {#ptiff-renditions}

启用了Dynamic Media的资产包括`pyramid.tiffs`。

![chlimage_1-360](assets/chlimage_1-360.png)

### 资产视图更改 {#asset-views-change}

启用Dynamic Media后，您可以通过单击`+`和`-`按钮来放大和缩小。您还可以单击/点按以放大特定区域。还原后，您可以转到原始版本，并通过单击对角箭头来使图像全屏显示。Dynamic Media启用如下所示：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大和缩小并还原到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
