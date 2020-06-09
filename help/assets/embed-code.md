---
title: 在网页上嵌入Dynamic Media视频查看器或图像查看器
description: 了解如何将Dynamic Media视频或图像嵌入网页
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 572b856fbdd1ef916f8f897ba86ddefafee324fc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 30%

---


# 在网页上嵌入Dynamic Media视频、图像查看器或维查看器 {#embedding-the-video-or-image-viewer-on-a-web-page}

当您想 **[!UICONTROL 要播放视频或查看嵌入到网页中的资产时]** ，请使用嵌入代码功能。 将嵌入代码复制到剪贴板，以便将其粘贴到网页中。 不允许在“嵌入代码”对 **[!UICONTROL 话框中编辑代码]** 。

仅当您未将AEM用作 _WCM_ 时，才嵌入URL。 如果您将AEM用作WCM, [则可以直接在页面上添加资产。](adding-dynamic-media-assets-to-pages.md)

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

   请注意，只有在首次&#x200B;*发布*&#x200B;资产&#x200B;*后*，才可复制嵌入代码。此外，还必须发布查看器预设或图像预设。

   请参阅[发布资产](publishing-dynamicmedia-assets.md)。

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. 在左边栏中，选择下拉菜单并点按查 **[!UICONTROL 看器]**。
1. 在左边栏中，点按查看器预设名称。查看器预设会应用于资产。
1. 点按&#x200B;**[!UICONTROL 嵌入]**。
1. In the **[!UICONTROL Embed Code]** dialog box, copy the entire code to the clipboard, and then tap **[!UICONTROL Close]**.
1. 将嵌入代码粘贴到网页中。

## 使用HTTP/2交付Dynamic Media资产 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供更快的信息传输，并减少所需的处理能力。 Dynamic Media资产的投放现在可以通过HTTP/2，从而提供更好的响应和加载时间。

有 [关使用Dynamic Media帐户](http2.md) HTTP/2入门的完整详细信息，请参阅内容的HTTP2投放。
