---
title: 使用 Dynamic Media
description: 了解如何使用Dynamic Media来提供可在Web、移动和社交网站上使用的资源。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 7%

---

# 使用Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) 帮助按需提供丰富的视觉推销和营销资产，自动针对Web、移动和社交网站上的消费进行扩展。 Dynamic Media使用一组主要源资源，通过其可扩展、性能优化的全球网络实时生成并提供多种丰富内容变体。

Dynamic Media提供交互式查看体验，包括缩放、360度旋转和视频。 Dynamic Media独特地整合了Adobe Experience Manager数字资产管理(Assets)解决方案的工作流，以简化和简化数字营销活动管理流程。

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## 使用Dynamic Media可以做什么 {#what-you-can-do-with-dynamic-media}

通过Dynamic Media，您可以在发布资产之前管理资产。 中详细介绍了如何使用一般资产 [使用数字资产](manage-assets.md). 一般主题包括上传、下载、编辑和发布资源；查看和编辑属性以及搜索资源。

仅限Dynamic Media的功能包括：

* [传送横幅](carousel-banners.md)
* [图像集](image-sets.md)
* [交互式图像](interactive-images.md)
* [交互式视频](interactive-videos.md)
* [混合媒体集](mixed-media-sets.md)
* [全景图像](panoramic-images.md)

* [旋转集](spin-sets.md)
* [视频](video.md)
* [投放 Dynamic Media 资源](delivering-dynamic-media-assets.md)
* [管理资源](managing-assets.md)
* [使用 Quickview 创建自定义弹出窗口](custom-pop-ups.md)

另请参阅 [设置Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>要了解使用Dynamic Media与将Dynamic Media Classic与Adobe Experience Manager集成之间的区别，请参阅 [Dynamic Media Classic集成与Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## 启用Dynamic Media与禁用Dynamic Media {#dynamic-media-on-versus-dynamic-media-off}

您可以通过以下特征来判断是否已启用（打开）Dynamic Media：

* 下载或预览资源时，可以使用动态演绎版。
* 图像集、旋转集和混合媒体集均可用。
* 创建PTIFF演绎版。

当您选择图像资源时，资源的视图与Dynamic Media不同 [已启用](config-dynamic.md#enabling-dynamic-media). Dynamic Media使用按需HTML5查看器。

### 动态演绎版 {#dynamic-renditions}

动态演绎版，例如图像和查看器预设(在 **[!UICONTROL 动态]**)在启用Dynamic Media时可用。

![chlimage_1-358](assets/chlimage_1-358.png)

### 图像集、旋转集、混合媒体集 {#image-sets-spins-sets-mixed-media-sets}

如果启用了Dynamic Media，则可以使用图像集、旋转集和混合媒体集。

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF演绎版 {#ptiff-renditions}

启用了Dynamic Media的资源包括 `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### 资源视图更改 {#asset-views-change}

启用Dynamic Media后，您可以通过单击 `+` 和 `-` 按钮。 您还可以单击放大特定区域。 还原将您带入原始版本，您可以通过单击对角线箭头使图像变为全屏。 已启用Dynamic Media的示例如下：

![chlimage_1-361](assets/chlimage_1-361.png)

禁用Dynamic Media后，您可以放大、缩小并恢复到原始大小：

![chlimage_1-362](assets/chlimage_1-362.png)
