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
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 全景图像{#panoramic-images}

本节介绍如何使用全景图像查看器来渲染球形全景图像，以便在室内、属性、位置或横向享受沉浸式360°的观看体验。

另请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md).

![全景图像2](assets/panoramic-image2.png)

## 上传资产以与全景图像查看器一起使用 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

要将上传的资产限定为要与全景图像查看器一起使用的球形全景图像，该资产必须具有以下任一项或两项：

* 宽高比为2。
您可以在以下位置覆盖CRXDE Lite中的默认宽高比设置2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 使用关键词标记 `equirectangular`或 `spherical`和 `panorama`或 `spherical` 和 `panoramic`. 请参阅 [使用标记](/help/sites-authoring/tags.md).

纵横比和关键字条件都适用于资产详细信息页面的全景资产，以及 `Panoramic Media` WCM组件。

要上传资产以与全景图像查看器一起使用，请参阅 [上传资产](/help/assets/manage-assets.md#uploading-assets).

## 配置Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

要使全景图像查看器在Adobe Experience Manager中正常工作，请将全景图像查看器预设与Dynamic Media Classic和特定于Dynamic Media Classic的元数据同步，以便查看器预设在JCR中进行更新。 要完成此同步，请按如下方式配置Dynamic Media Classic:

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

1. 在页面的右上角附近，选择 **[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**.
1. 在图像服务器发布页面上，从 **[!UICONTROL 发布上下文]** 下拉菜单，选择 **[!UICONTROL 图像提供]**.

1. 在同一图像服务器发布页面上，找到标题 **[!UICONTROL 请求属性]**.
1. 在请求属性标题下，找到 **[!UICONTROL 回复图像大小限制]**. 然后，在关联的“宽度”和“高度”字段中，增加全景图像允许的最大图像大小。

   Dynamic Media Classic的限制为25,000,000像素。 宽高比为2:1的图像的最大允许大小为7000 x 3500。 但是，对于典型的桌面屏幕，4096 x 2048像素就足够了。

   >[!NOTE]
   >
   >仅支持位于允许的最大图像大小范围内的图像。 对大小超过限制的图像的请求将导致403响应。

1. 在“请求属性”标题下，执行以下操作：

   * 将请求模糊处理模式设置为 **[!UICONTROL 已禁用]**.
   * 将请求锁定模式设置为 **[!UICONTROL 已禁用]**.

   使用 `Panoramic Media` WCM组件Experience Manager。

1. 在“图像服务器发布”页面的左侧底部，选择 **[!UICONTROL 保存]**.

1. 在右下角，选择 **[!UICONTROL 关闭]**.

### 对全景媒体WCM组件进行故障诊断 {#troubleshooting-the-panoramic-media-wcm-component}

如果将图像放入WCM中的全景媒体组件中，并且组件占位符折叠，则对以下问题进行故障诊断：

* 如果您遇到403禁止错误，可能是由于请求的图像大小太大所致。 查看 **[!UICONTROL 回复图像大小限制]** 设置 [配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* 对于资产上显示的“锁定无效”或页面上显示的“解析错误”，请选中请求模糊处理模式和请求锁定模式以确保已禁用这些模式。
* 对于受污染的画布错误，请为图像资产的先前请求设置规则集定义文件路径和无效CTN 。
* 如果图像请求的大小超过支持的限制后图像质量变低，请检查 **[!UICONTROL JPEG编码属性>质量]** 设置不为空。 的典型设置 **[!UICONTROL 质量]** 字段 `95`. 您可以在“图像服务器发布”页面上找到该设置。 要访问页面，请参阅 [配置Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## 预览全景图像 {#previewing-panoramic-images}

请参阅 [预览资产](/help/assets/previewing-assets.md).

## 发布全景图像 {#publishing-panoramic-images}

请参阅 [发布资产](/help/assets/publishing-dynamicmedia-assets.md).
