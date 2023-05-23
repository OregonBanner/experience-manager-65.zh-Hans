---
title: 投放 Dynamic Media 资源
description: 瞭解如何傳遞Dynamic Media資產
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 13%

---

# 投放 Dynamic Media 资源{#delivering-dynamic-media-assets}

如何傳遞Dynamic Media資產（包括影片和影像）取決於網站的實作方式。

Dynamic Media提供幾個選項：

* 如果您的網站託管於Adobe Experience Manager上，那麼您想要直接將Dynamic Media資產新增至您的頁面。
* 如果您的網站不在Experience Manager上，您可以選擇以下任一選項：

   * 將您的影片或影像內嵌在網站上。
   * 将 URL 关联到您的 Web 应用程序. 當您想要以快顯視窗或強制回應視窗的形式傳送視訊播放器時，請使用連結。
   * 如果您的網站有回應，您可以 [傳遞最佳化的影像](/help/assets/responsive-site.md).

>[!NOTE]
>
>智慧型影像處理可搭配您現有的影像預設集運作，並在傳送的最後毫秒內運用智慧功能，根據瀏覽器或網路連線速度，進一步縮減影像檔案大小。 另請參閱 [智慧型影像](/help/assets/imaging-faq.md) 以取得詳細資訊。

如需詳細資訊，請參閱下列主題：

* [將Dynamic Media資產新增至網頁](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md)
* [在 Dynamic Media 中激活热链接保护](/help/assets/hotlink-protection.md)
* [将 URL 关联到您的 Web 应用程序](/help/assets/linking-urls-to-yourwebapplication.md)
* [为响应式站点传送优化的图像](/help/assets/responsive-site.md)
* [HTTP2 内容交付](/help/assets/http2.md)
* [透過Dynamic Media Classic使CDN快取失效](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [使用规则集转换 URL](/help/assets/using-rulesets-to-transform-urls.md)


## Dynamic Media資產的HTTP/2傳送 {#http-delivery-of-dynamic-media-assets}

Experience Manager現在支援透過HTTP/2傳送所有Dynamic Media內容（影像和視訊）。 也就是說，影像或視訊的已發佈URL或內嵌程式碼可整合至任何接受託管資產的應用程式。 然後會透過HTTP/2通訊協定傳遞該已發佈的資產。 此傳遞方法可改善瀏覽器和伺服器的通訊方式，讓您的所有Dynamic Media資產獲得更好的回應和載入時間。

若要深入瞭解，請參閱 [HTTP/2內容傳送常見問題](/help/sites-administering/scene7-http2faq.md).
