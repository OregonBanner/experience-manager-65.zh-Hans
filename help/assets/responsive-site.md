---
title: 为响应式网站传送优化的图像
description: 如何使用响应式代码功能交付优化的图像
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 11%

---

# 为响应式站点传送优化的图像 {#delivering-optimized-images-for-a-responsive-site}

当您想要与Web开发人员共享用于响应式服务的代码时，请使用响应式代码功能。 复制响应式(**[!UICONTROL RESS]**)代码到剪贴板，以便与Web开发人员共享。

如果您的网站位于第三方WCM上，则此功能很有用。 但是，如果您的网站位于Adobe Experience Manager上，则异地图像服务器会渲染图像并将其提供给网页。

另请参阅 [在网页上嵌入视频查看器](embed-code.md).

另请参阅 [将URL链接到您的Web应用程序](linking-urls-to-yourwebapplication.md).

**要为响应式网站交付优化的图像，请执行以下操作：**

1. 导航到要为其提供响应式代码的图像，然后在下拉菜单中，选择 **[!UICONTROL 节目]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 选择响应式图像预设。 将显 **[!UICONTROL 示]** URL **[!UICONTROL 和]** RESS按钮。

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >必须发布选定的资产&#x200B;*和*&#x200B;选定的图像预设或查看器预设，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按钮可用。
   >
   >Dynamic Media — 混合模式要求发布图像预设；Dynamic Media - Scene7模式会自动发布图像预设。

1. 选择 **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在 **[!UICONTROL 嵌入响应图像]** 对话框，选择并复制响应式代码文本，然后将其粘贴到您的网站中以访问响应式资产。
1. 直接在代码中编辑嵌入代码中的默认断点，以匹配响应式网站的断点。 此外，还测试在不同页面断点提供的不同图像分辨率。

## 使用HTTP/2交付您的Dynamic Media资源 {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是新的、更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供了更快的信息传输速度并减少所需的处理能力。 HTTP/2支持交付Dynamic Media资源，可提供更好的响应和加载时间。

请参阅 [HTTP2内容交付](http2.md) 以了解有关开始将HTTP/2用于您的Dynamic Media帐户的完整详细信息。
