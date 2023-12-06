---
title: 在网页上嵌入Dynamic Media视频、图像查看器或维度查看器
description: 了解如何在网页上嵌入Dynamic Media视频、图像或3D图像
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 20%

---

# 在网页上嵌入Dynamic Media视频、图像查看器或维度查看器 {#embedding-the-video-or-image-viewer-on-a-web-page}

当您想 **[!UICONTROL 要播放视频或查看嵌入到网页中的资产时]** ，请使用嵌入代码功能。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在“嵌入代码”对 **[!UICONTROL 话框中编辑代码]** 。

只有在符合以下条件时才嵌入URL： *非* 将Adobe Experience Manager用作WCM。 如果您将Experience Manager用作WCM， [直接在页面上添加资产](adding-dynamic-media-assets-to-pages.md).

请参阅 [将URL链接到您的Web应用程序](linking-urls-to-yourwebapplication.md).

请参阅 [为响应式网站传送优化的图像](responsive-site.md).

>[!NOTE]
>
>在发布选定资产之前，无法复制嵌入代码。 此外，还必须发布查看器预设或图像预设。
>
>请参阅 [发布资源](publishing-dynamicmedia-assets.md).
>
>请参阅 [发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets).
>
>请参阅 [发布图像预设](managing-image-presets.md#publishing-image-presets).

**要在网页上嵌入Dynamic Media视频、图像查看器或维度查看器，请执行以下操作：**

1. 导航至 *已发布* 要复制其嵌入代码的视频或图像资产。

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制嵌入代码。此外，还必须发布查看器预设或图像预设。

   请参阅 [发布资源](publishing-dynamicmedia-assets.md).

   请参阅 [发布查看器预设](managing-viewer-presets.md#publishing-viewer-presets).

   请参阅 [发布图像预设](managing-image-presets.md#publishing-image-presets).

1. 在左边栏中，选择下拉菜单并选择 **[!UICONTROL 查看器]**.
1. 在左边栏中，选择一个查看器预设名称。 查看器预设将应用于资产。
1. 选择 **[!UICONTROL 嵌入]**.
1. 在 **[!UICONTROL 嵌入代码]** 对话框，将整个代码复制到剪贴板，然后选择 **[!UICONTROL 关闭]**.
1. 将嵌入代码粘贴到网页中。

## 使用HTTP/2交付您的Dynamic Media资源 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输速度并减少所需的处理能力。 Dynamic Media资源的交付现在可以通过HTTP/2进行，从而缩短响应时间和加载时间。

请参阅 [HTTP2内容交付](http2.md) 以了解有关开始将HTTP/2用于您的Dynamic Media帐户的完整详细信息。
