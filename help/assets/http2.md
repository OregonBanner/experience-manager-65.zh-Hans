---
title: HTTP2 内容交付
description: HTTP/2改善了瀏覽器和伺服器的通訊方式，允許更快速地傳輸資訊，同時減少所需的處理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
source-git-commit: a78de999992d4ab2fc63b5f7e796aa0d5527cb26
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 3%

---

# HTTP/2 内容交付 {#http-delivery-of-content}

Adobe 很高兴地宣布推出 HTTP/2 内容交付功能，这意味着性能将全面提升。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。

## 什麼是HTTP/2？ {#what-is-http}

HTTP/2改善了瀏覽器和伺服器的通訊方式，允許更快速地傳輸資訊，同時減少所需的處理能力。

以下網站以簡單明瞭的方式說明HTTP/2及其優點：

[您必須瞭解的HTTP/2相關資訊](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 轉移至HTTP/2進行內容傳送的主要優點為何？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能提升可能大相逕庭。 此量度取決於許多因素，例如您的網站程式碼、您如何使用Dynamic Media、消費者的裝置、畫面和位置。

Adobe自己的測試產生以下結果：

* 對於影像，回應時間改善7%至28%，視裝置和瀏覽器而定。 效能提升最顯著的是iOS裝置。
* 對於檢視器而言，載入時間效能提升了15%。

下列示範說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列要求：

* 針對您的多媒體請求使用安全HTTPS。
* 使用Adobe隨附的CDN （內容傳遞網路），作為Dynamic Media授權的一部分。
* 使用專用（非公司h.assetsadobe#.com）網域。

   如果您已有專屬網域，則可透過Adobe客戶支援選擇加入。

   如果您沒有專用網域，Adobe計畫在2018年安排您轉換至HTTP/2。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

您起始切換至HTTP/2的要求，但不會自動為您完成。

1. 若要切換至HTTP/2，請啟動Adobe客戶支援請求。 另請參閱 [開啟支援票證](https://experienceleague.adobe.com/?support-solution=General&amp;lang=en&amp;support-tab=home#support).

   1. 在您的支援請求中提供下列資訊：

      1. 主要連絡人姓名、電子郵件、電話。
      1. 所有要轉換為HTTP/2的網域。
      1. 確認您使用安全HTTPS處理多媒體請求。
      1. 確認您透過Adobe使用CDN，且未透過直接關係進行管理。
      1. 確認您使用專用網域。 如果您使用Dynamic Media，則請使用專用網域。
   1. 客戶支援會根據提交請求的順序，將您新增至HTTP/2客戶輪候清單。
   1. 當Adobe準備好處理您的請求時，客戶支援會聯絡您以協調轉變並設定目標日期。
   1. 完成後您會收到通知，並可以驗證是否成功轉換到HTTP2。

      由於瀏覽器未說明此事實，因此必須下載擴充功能。

      Firefox和Chrome有一個名為「HTTP/2和SPDY Indicator」的擴充功能。 瀏覽器僅安全地支援http/2，因此有必要呼叫具有https的URL以進行驗證。 如果支援http/2，擴充功能會以藍色Flash符號和標頭「X-Firefox-Spdy」的形式表示：「h2」。


## 我何時可以轉換為HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

請求會依客戶支援收到的順序進行處理。

>[!NOTE]
>
>由於轉換至HTTP/2的過程涉及清除快取，因此可能會有很長的前置時間。 因此，一次只能處理幾個客戶轉換。

## 移至HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN上的快取，因為它牽涉到移至新的CDN設定。

非快取內容會直接點選Adobe的原始伺服器，直到再次重建快取為止。 因此，Adobe計劃一次處理一些客戶轉換，以便在從來源提取請求時維持可接受的效能。

## 如何驗證URL或網站是否以HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由於瀏覽器未說明此事實，因此必須下載擴充功能。

Firefox和Chrome有一個名為「HTTP/2和SPDY Indicator」的擴充功能。 瀏覽器僅安全地支援http/2，因此有必要呼叫具有https的URL以進行驗證。 如果支援http/2，則會以藍色Flash符號和標頭的形式來表示擴充功能 `X-Firefox-Spdy` ： `h2`.
