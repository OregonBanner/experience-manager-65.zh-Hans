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
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# Panoramic images{#panoramic-images}

本节介绍如何使用全景图像查看器渲染球面全景图像，实现房间、属性、位置或风景的沉浸式360°查看体验。

See also [Managing Viewer Presets](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## 上传资产以用于全景图像查看器 {#uploading-assets-for-use-with-the-panoramic-image-viewer}

要使上传的资产成为您要与全景图像查看器一起使用的球面全景图像，该资产必须具有以下一种或两种：

* 宽高比为2。
您可以在以下位置覆盖CRXDE Lite中的默认宽高比设置2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 用关键字 `equirectangular`标记， `spherical`或和 `panorama`，或 `spherical` 和 `panoramic`。 请参 [阅使用标记](/help/sites-authoring/tags.md)。

Both the aspect ratio and keyword criteria apply to panoramic assets for the asset details page and the `Panoramic Media` WCM component.

要上传资产以用于全景图图像查看器，请参阅 [上传资产](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

## 配置Dynamic Media经典(Scene7) {#configuring-dynamic-media-classic-scene}

要使全景图像查看器在AEM中正常工作，您必须将全景图图像查看器预设与Dynamic Media经典(Scene7)和Dynamic Media经典(Scene7)特定的元数据同步，以便查看器预设在JCR中进行更新。 为此，请按照以下方式配置Dynamic Media经典(Scene7):

1. [登录每个Dynamic Media帐户的公司经典(Scene7](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) )实例。

1. 在页面的右上角附近，单击“设置”>“应 **[!UICONTROL 用程序设置”>“发布设置”>“图像服务器”。]**
1. 在“图像服务器发布”页面上，从 **[!UICONTROL 顶部附近的]** “发布上下文”下拉菜单中，选择 **[!UICONTROL 图像服务。]**

1. 在同一图像服务器发布页面上，找到标题请求 **[!UICONTROL 属性。]**
1. 在“请求属性”标题下，找到“ **[!UICONTROL 回复图像大小限制”。]** 然后，在关联的“宽度”和“高度”字段中，增加全景图像允许的最大图像大小。

   Dynamic Media经典(Scene7)的像素数限制为25,000,000像素。 宽高比为2:1的图像的最大允许大小为7000 x 3500。 但是，对于典型的桌面屏幕，4096 x 2048像素就足够了。

   >[!NOTE]
   >
   >仅支持在允许的最大图像大小范围内的图像。 对超过大小限制的图像的请求将产生403响应。

1. 在“请求属性”标题下，执行以下操作：

   * 将“请求模糊化模式”设置为 **[!UICONTROL 禁用。]**
   * 将“请求锁定模式”设置 **[!UICONTROL 为“禁用”。]**
   在AEM中使用WCM组 `Panoramic Media` 件时，这些设置是必需的。

1. 在“图像服务器发布”页面的左侧，单击“保 **[!UICONTROL 存”。]**

1. 在右下角，单击“关闭”( **[!UICONTROL Close)。]**

### 全景媒体WCM组件疑难解答 {#troubleshooting-the-panoramic-media-wcm-component}

如果您将图像放到WCM中的Panoramic Media组件中，并且组件占位符折叠，您可能希望对以下问题进行疑难解答：

* 如果遇到“403禁止”错误，则可能是由于请求的图像大小过大所致。 查看配 **[!UICONTROL 置Dynamic Media经典]** (Scene7) [中的“回复图像大小限制”设置](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7))。

* 对于资产上显示的“无效锁定”或“解析错误”，请选中请求模糊处理模式和请求锁定模式以确保它们被禁用。
* 对于受污染的画布错误，请为图像资产的先前请求设置规则集定义文件路径和失效CTN。
* 如果图像请求的大小超过支持的限制后图像质量变得非常低，请检查“JPEG编 **[!UICONTROL 码属性”>“质量]** ”设置是否为空。 “质量”字段的 **[!UICONTROL 典型设]** 置是 `95`。 您可以在“图像服务器发布”页面上找到该设置。 要访问页面，请参 [阅配置Dynamic Media经典(Scene7)](/help/assets/panoramic-images.md#configuring%20dynamic%20media%20classic%20(scene7))。

## 预览全景图像 {#previewing-panoramic-images}

See [Previewing Assets](/help/assets/previewing-assets.md).

## 发布全景图像 {#publishing-panoramic-images}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
