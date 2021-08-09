---
title: 全景图像
description: 了解如何在Dynamic Media中处理全景图像。
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: 全景图像，资产管理
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 全景图像{#panoramic-images}

本节介绍如何使用全景图像查看器来渲染球形全景图像，以便在室内、属性、位置或横向享受沉浸式360°的观看体验。

另请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

![全景图像2](assets/panoramic-image2.png)

## 上传资产以与全景图像查看器一起使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

要将上传的资产限定为要与全景图像查看器一起使用的球形全景图像，该资产必须具有以下任一项或两项：

* 宽高比为2。
您可以在以下位置覆盖CRXDE Lite中的默认宽高比设置2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 使用关键字`equirectangular`、`spherical`和`panorama`或`spherical`和`panoramic`进行标记。 请参阅[使用标记](/help/sites-authoring/tags.md)。

纵横比和关键字条件都适用于资产详细信息页面和`Panoramic Media` WCM组件的全景资产。

要上传资产以与全景图像查看器一起使用，请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

## 配置Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

要使全景图像查看器在Adobe Experience Manager中正常工作，请将全景图像查看器预设与特定于Dynamic Media Classic和Dynamic Media Classic的元数据同步，以便查看器预设在JCR中进行更新。 要完成此同步，请按如下方式配置Dynamic Media Classic:

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**。
1. 在“图像服务器发布”页面上，从顶部附近的&#x200B;**[!UICONTROL 发布上下文]**&#x200B;下拉菜单中，选择&#x200B;**[!UICONTROL 图像服务]**。

1. 在同一图像服务器发布页面上，找到标题&#x200B;**[!UICONTROL 请求属性]**。
1. 在“请求属性”标题下，找到&#x200B;**[!UICONTROL 回复图像大小限制]**。 然后，在关联的“宽度”和“高度”字段中，增加全景图像允许的最大图像大小。

   Dynamic Media Classic的限制为25,000,000像素。 宽高比为2:1的图像的最大允许大小为7000 x 3500。 但是，对于典型的桌面屏幕，4096 x 2048像素就足够了。

   >[!NOTE]
   >
   >仅支持位于允许的最大图像大小范围内的图像。 对大小超过限制的图像的请求会导致403响应。

1. 在“请求属性”标题下，执行以下操作：

   * 将“请求模糊处理模式”设置为&#x200B;**[!UICONTROL Disabled]**。
   * 将“请求锁定模式”设置为&#x200B;**[!UICONTROL Disabled]**。

   在Experience Manager中使用`Panoramic Media` WCM组件时，需要使用这些设置。

1. 在“图像服务器发布”页面底部的左侧，选择&#x200B;**[!UICONTROL Save]**。

1. 在右下角，选择&#x200B;**[!UICONTROL 关闭]**。

### 对全景媒体WCM组件进行故障诊断 {#troubleshooting-the-panoramic-media-wcm-component}

如果将图像放入WCM中的全景媒体组件中，并且组件占位符折叠，则对以下问题进行故障诊断：

* 如果您遇到403禁止错误，可能是由于请求的图像大小太大所致。 查看[配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)中的&#x200B;**[!UICONTROL 回复图像大小限制]**&#x200B;设置。

* 对于资产上显示的“锁定无效”或页面上显示的“解析错误”，请选中请求模糊处理模式和请求锁定模式以确保已禁用这些模式。
* 对于受污染的画布错误，请为图像资产的先前请求设置规则集定义文件路径和无效CTN 。
* 如果图像请求的大小超过支持的限制后图像质量变低，请检查&#x200B;**[!UICONTROL JPEG编码属性>质量]**&#x200B;设置是否不为空。 **[!UICONTROL Quality]**&#x200B;字段的典型设置为`95`。 您可以在“图像服务器发布”页面上找到该设置。 要访问该页面，请参阅[配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

## 预览全景图像 {#previewing-panoramic-images}

请参阅[预览资产](/help/assets/previewing-assets.md)。

## 发布全景图像 {#publishing-panoramic-images}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
