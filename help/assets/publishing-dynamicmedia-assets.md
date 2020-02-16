---
title: 发布 Dynamic Media 资产
description: 如何发布Dynamic Media资产
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 发布 Dynamic Media 资产 {#publishing-dynamic-media-assets}

You publish your Dynamic Media assets by selecting the assets and tapping **[!UICONTROL Publish]**. 在发布Dynamic media资产后，您可以通过URL或通过嵌入方式将其包含在网页中。

您还可以立即发布上传的资产，无需任何用户干预。 请参 [阅配置Dynamic Media - Scene7模式](config-dms7.md)。

在卡片 **[!UICONTROL 视图中]**，资产名称的正下方会显示一个小地球图标，指示资产已发布。 在列 **[!UICONTROL 表视图中]**,“已发 **** 布”列指示已发布或未发布的资产。

>[!NOTE]
>
>如果资产已发布，则您可以使用AEM将资产移至其他文件夹，然后从新位置重新发布，则原始发布的资产位置以及新重新发布的资产仍然可用。但是，原始发布的资产会“丢失”到AEM，无法取消发布。因此，作为最佳实践，在将资产移到其他文件夹之前，请先取消发布资产。

如果您打算在对视频资产进行编码后立即发布这些资产，请确保编码已完成。当视频仍在编码时，系统会告知您视频处理工作流正在进行中。完成视频编码后，您应该能够预览视频演绎版。此时，发布视频时不会出现任何发布错误，这是安全的。

另请参阅[将 URL 关联到您的 Web 应用程序](linking-urls-to-yourwebapplication.md)。

另请参阅[在网页上嵌入视频查看器。](embed-code.md)

>[!NOTE]
>
>* 要使用 URL，必须先发布资产。如果资产未发布，您便无法将 URL 复制并粘贴到 Web 浏览器。
>* 必须激活并发布图像预设和查看器预设才能实时交付。
>



有关发布集或资产的详细信息，请参阅发 [布资产。](managing-assets-touch-ui.md)

## HTTP/2 Dynamic media资产的交付 {#http-delivery-of-dynamic-media-assets}

AEM现在支持通过HTTP/2交付所有Dynamic media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，通过HTTP/2协议传送已发布的资产。 这种交付方法改进了浏览器和服务器通信的方式，使所有Dynamic media资产的响应和加载时间都更好。

请参 [阅HTTP/2交付内容常见问题解答](/help/sites-administering/scene7-http2faq.md) ，以了解更多信息。
