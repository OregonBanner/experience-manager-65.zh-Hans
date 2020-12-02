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
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# 全景图像{#panoramic-images}

本节介绍如何使用全景图像查看器渲染球面全景图像，实现房间、属性、位置或风景的沉浸式360°查看体验。

另请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

![panoramic-image2](assets/panoramic-image2.png)

## 上传资产以用于全景图像查看器{#uploading-assets-for-use-with-the-panoramic-image-viewer}

要使上传的资产成为您要与全景图像查看器一起使用的球面全景图像，该资产必须具有以下一种或两种：

* 宽高比为2。
您可以在以下CRXDE Lite中覆盖默认的宽高比设置：2:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* 使用关键字`equirectangular`、`spherical`和`panorama`、`spherical`和`panoramic`进行标记。 请参阅[使用标记](/help/sites-authoring/tags.md)。

长宽比和关键字条件都适用于资产详细信息页面和`Panoramic Media` WCM组件的全景资产。

要上传资产以用于全景图像查看器，请参阅[上传资产](/help/assets/manage-assets.md#uploading-assets)。

## 配置Dynamic Media Classic(Scene7){#configuring-dynamic-media-classic-scene}

要使全景图像查看器在AEM中正常工作，您必须将全景图像查看器预设与特定于Dynamic Media Classic(Scene7)和Dynamic Media Classic(Scene7)的元数据同步，以便查看器预设在JCR中进行更新。 为此，请按照以下方式配置Dynamic Media Classic(Scene7):

1. [为每个Scene7帐户登录Dynamic Media Classic(](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 公司)实例。

1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器。]**
1. 在“图像服务器发布”页面上，从顶部附近的&#x200B;**[!UICONTROL 发布上下文]**&#x200B;下拉菜单中，选择&#x200B;**[!UICONTROL 图像服务。]**

1. 在同一图像服务器发布页面上，找到标题&#x200B;**[!UICONTROL 请求属性。]**
1. 在请求属性标题下，找到&#x200B;**[!UICONTROL 回复图像大小限制。]** 然后，在关联的“宽度”和“高度”字段中，增加全景图像允许的最大图像大小。

   Dynamic Media Classic(Scene7)的像素限制为25,000,000像素。 宽高比为2:1的图像的最大允许大小为7000 x 3500。 但是，对于典型的桌面屏幕，4096 x 2048像素就足够了。

   >[!NOTE]
   >
   >仅支持在允许的最大图像大小范围内的图像。 对超过大小限制的图像的请求将产生403响应。

1. 在“请求属性”标题下，执行以下操作：

   * 将请求模糊化模式设置为&#x200B;**[!UICONTROL 禁用。]**
   * 将请求锁定模式设置为&#x200B;**[!UICONTROL 禁用。]**

   在AEM中使用`Panoramic Media` WCM组件时，必须进行这些设置。

1. 在“图像服务器发布”页面的左侧，单击“保存”。****

1. 在右下角，单击&#x200B;**[!UICONTROL 关闭。]**

### 全景媒体WCM组件{#troubleshooting-the-panoramic-media-wcm-component}疑难解答

如果您将图像放到WCM中的Panoramic Media组件中，并且组件占位符折叠，您可能希望对以下问题进行疑难解答：

* 如果遇到“403禁止”错误，则可能是由于请求的图像大小过大所致。 查看[配置Dynamic Media Classic(Scene7)](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)中的&#x200B;**[!UICONTROL 回复图像大小限制]**&#x200B;设置。

* 对于资产上显示的“无效锁定”或“解析错误”，请选中请求模糊处理模式和请求锁定模式以确保它们被禁用。
* 对于受污染的画布错误，请为图像资产的先前请求设置规则集定义文件路径和失效CTN。
* 如果图像请求的大小超过支持的限制后图像质量变得非常低，请检查“**[!UICONTROL JPEG编码属性>质量]**”设置是否不为空。 **[!UICONTROL Quality]**&#x200B;字段的典型设置为`95`。 您可以在“图像服务器发布”页面上找到该设置。 要访问该页面，请参阅[配置Dynamic Media Classic(Scene7)](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene)。

## 预览全景图像{#previewing-panoramic-images}

请参阅[预览资产](/help/assets/previewing-assets.md)。

## 发布全景图像{#publishing-panoramic-images}

请参阅[发布资产](/help/assets/publishing-dynamicmedia-assets.md)。
