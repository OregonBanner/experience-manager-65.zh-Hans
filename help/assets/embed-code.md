---
title: 在网页上嵌入Dynamic Media视频查看器或图像查看器
description: 了解如何将Dynamic media视频或图像嵌入网页
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Embedding the Dynamic Media Video or Image viewer on a web page {#embedding-the-video-or-image-viewer-on-a-web-page}

Use the **[!UICONTROL Embed Code]** feature when you want to play the video or view an asset embedded on a web page. You copy the embed code to the clipboard so you can paste it in your web pages. Editing of the code is not permitted in the **[!UICONTROL Embed Code]** dialog box.

仅当您未将AEM用作WCM _时_ ，才嵌入URL。 如果您使用AEM作为WCM, [则直接在页面上添加资产。](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>只有在发布选定的资产后，才可复制其嵌入代码。此外，您还必须发布查看器预设或图像预设。
>
>请参阅[发布资产](publishing-dynamicmedia-assets.md)。
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

**在网页上嵌入Dynamic Media视频查看器或图像查看器**

1. Navigate to the *published* video or image asset whose embed code you want to copy.

   Remember that the embed code is only available to copy *after* you have first *published* the assets. 此外，还必须发布查看器预设或图像预设。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. 在左边栏中，选择下拉菜单并点按查看 **[!UICONTROL 器]**。
1. 在左边栏中，点按查看器预设名称。查看器预设将应用于资产。
1. 点按&#x200B;**[!UICONTROL 嵌入]**。
1. In the **[!UICONTROL Embed Code]** dialog box, copy the entire code to the clipboard, and then tap **[!UICONTROL Close]**.
1. 将嵌入代码粘贴到网页中。

## 使用HTTP/2交付Dynamic Media资产 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器通信的方式。 它提供了更快的信息传输，并减少了所需的处理能力。 Dynamic media资产的交付现在可以通过HTTP/2进行，从而提供更好的响应和加载时间。

有关 [Dynamic Media帐户的HTTP/2快速入门的完整详细信息，请参阅](http2.md) HTTP2内容交付。
