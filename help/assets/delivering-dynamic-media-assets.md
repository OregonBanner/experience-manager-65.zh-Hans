---
title: 传送 Dynamic Media 资产
description: 了解如何交付动态媒体资产
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
translation-type: tm+mt
source-git-commit: 3eacfe8a79d155dddde8908d05b05790d048b0c5
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 23%

---


# 传送 Dynamic Media 资产{#delivering-dynamic-media-assets}

您如何投放动态媒体资产（视频和图像）取决于网站的实施方式。

通过 Dynamic Media，您可以选择以下方式：

* 如果您的网站托管在 AEM 上，您会希望将 Dynamic Media 资产直接添加到您的页面。
* 如果您的网站不在AEM上，您可以选择：

   * 将视频或图像嵌入您的网站。
   * 将URL关联到您的Web应用程序。当您希望以弹出窗口或模态窗口的形式传送视频播放器时，可使用链接。
   * 如果您的站点是响应式的，您可以[传送优化的图像。](/help/assets/responsive-site.md)

>[!NOTE]
>
>智能成像可以与现有图像预设配合使用，并在投放的最后一毫秒使用智能功能根据浏览器或网络连接速度进一步减小图像文件大小。 有关详细信息，请参阅[智能成像](/help/assets/imaging-faq.md)。

有关更多信息，请参阅下列主题：

* [将Dynamic Media资产添加到网页](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/responsive-site.md)
* [内容的HTTP2投放](/help/assets/http2.md)
* [通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/using-rulesets-to-transform-urls.md)


## HTTP/2投放Dynamic Media资产{#http-delivery-of-dynamic-media-assets}

AEM现在支持通过HTTP/2投放所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 随后，将通过HTTP/2协议传送已发布的资产。 此投放方法改进了浏览器和服务器通信的方式，使所有Dynamic Media资源的响应和加载时间都更好。

请参阅[HTTP/2投放内容常见问题](/help/sites-administering/scene7-http2faq.md)以了解更多信息。
