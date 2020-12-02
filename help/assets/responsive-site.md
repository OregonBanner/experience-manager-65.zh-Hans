---
title: 为响应式网站传送优化的图像
description: 如何使用响应式代码功能传送优化的图像
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 25%

---


# 为响应式网站传送优化的图像 {#delivering-optimized-images-for-a-responsive-site}

如果您希望与 Web 开发人员共享代码以实现响应式服务，可使用响应式代码功能。您将响应式(**[!UICONTROL RESS]**)代码复制到剪贴板，以便与Web开发人员共享它。

如果您的网站位于第三方WCM上，则使用此功能很合理。 但是，如果您的网站位于AEM上，则非现场映像服务器会渲染该映像，并将其提供到网页。

另请参阅[在网页上嵌入视频查看器。](embed-code.md)

另请参阅[将 URL 关联到您的 Web 应用程序。](linking-urls-to-yourwebapplication.md)

**为响应式网站提供优化的图像**:

1. 导航到要为其提供响应式代码的图像，在下拉菜单中，点按&#x200B;**[!UICONTROL 演绎版]**。

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. 选择响应式图像预设。 将显 **[!UICONTROL 示]** URL **[!UICONTROL 和]** RESS按钮。

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >必须发布选定的资产&#x200B;*和*&#x200B;选定的图像预设或查看器预设，才能使 **[!UICONTROL URL]** 或 **[!UICONTROL RESS]** 按钮可用。
   >
   >Dynamic Media —— 混合模式要求您发布图像预设；Dynamic Media -Scene7模式自动发布图像预设。

1. 点按&#x200B;**[!UICONTROL RESS]**。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. 在&#x200B;**[!UICONTROL 嵌入响应式图像]**&#x200B;对话框中，选择并复制响应式代码文本，然后将其粘贴到您的网站中以访问响应式资产。
1. 编辑嵌入代码中的默认断点，使其直接与响应式网站的代码断点相匹配。此外，测试不同页面断点处使用的不同图像分辨率。

## 使用HTTP/2投放Dynamic Media资产{#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2是新的、经过更新的Web协议，它改进了浏览器和服务器的通信方式。 它提供更快的信息传输，并减少所需的处理能力。 HTTP/2支持Dynamic Media资产的投放，可提供更好的响应和加载时间。

有关Dynamic Media帐户HTTP/2快速入门的完整详细信息，请参阅[内容的HTTP2投放](http2.md)。
