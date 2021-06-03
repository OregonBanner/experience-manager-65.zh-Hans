---
title: 传送 Dynamic Media 资产
description: 了解如何交付Dynamic Media资产
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: Business Practitioner, Administrator
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: 资产管理，演绎版
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 14%

---

# 传送 Dynamic Media 资产{#delivering-dynamic-media-assets}

如何交付Dynamic Media资产（包括视频和图像）取决于网站的实施方式。

使用Dynamic Media，您有以下几个选项：

* 如果您的网站托管在Adobe Experience Manager上，则您希望将Dynamic Media资产直接添加到您的页面。
* 如果您的网站未Experience Manager，则可以选择以下任一选项：

   * 在您的网站上嵌入视频或图像。
   * 将URL关联到您的Web应用程序。当您希望将视频播放器作为弹出窗口或模式窗口进行传送时，请使用链接。
   * 如果您的网站是响应式的，您可以[传送优化的图像。](/help/assets/responsive-site.md)

>[!NOTE]
>
>智能成像可与您现有的图像预设配合使用，并在交付的最后一毫秒内使用智能功能，根据浏览器或网络连接速度进一步减小图像文件大小。 有关更多信息，请参阅[智能成像](/help/assets/imaging-faq.md)。

有关更多信息，请参阅下列主题：

* [将Dynamic Media Assets添加到网页](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [在网页上嵌入视频查看器或图像查看器](/help/assets/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)
* [为响应式网站传送优化的图像](/help/assets/responsive-site.md)
* [HTTP2内容交付](/help/assets/http2.md)
* [通过Dynamic Media Classic使CDN缓存失效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换URL](/help/assets/using-rulesets-to-transform-urls.md)


## HTTP/2交付Dynamic Media资产{#http-delivery-of-dynamic-media-assets}

Experience Manager现在支持通过HTTP/2交付所有Dynamic Media内容（图像和视频）。 即，图像或视频的已发布URL或嵌入代码可与接受托管资产的任何应用程序集成。 然后，将通过HTTP/2协议来交付已发布的资产。 这种交付方法改进了浏览器和服务器通信的方式，从而可以缩短所有Dynamic Media资产的响应和加载时间。

要了解更多信息，请参阅[HTTP/2内容交付常见问题解答](/help/sites-administering/scene7-http2faq.md)。
