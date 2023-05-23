---
title: HTTP2 内容投放常见问题解答
description: 瞭解HTTP2內容傳送。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 2%

---

# HTTP2 内容投放常见问题解答{#http-delivery-of-content-faq}

Adobe很高興宣佈推出HTTP/2內容傳送。 當您使用HTTP/2時，會注意到整體效能提高。

## 什麼是HTTP/2？ {#what-is-http}

HTTP/2改善了瀏覽器和伺服器的通訊方式，允許更快速地傳輸資訊，同時減少所需的處理能力。

以下網站以簡單明瞭的方式說明HTTP/2及其優點：

[您必須瞭解的HTTP/2相關資訊](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html).

## 轉移至HTTP/2進行內容傳送的主要優點為何？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能改善會因您網站的程式碼、您如何使用Dynamic Media、客戶的裝置、畫面和位置等因素而有很大的差異。

Adobe自己的測試產生以下結果：

* 對於影像，回應時間改善7%至28%，視裝置和瀏覽器而定。 效能提升最顯著的是iOS裝置。
* 對於檢視器而言，載入時間效能提升了15%。

下列示範說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列要求：

* 針對您的多媒體請求使用安全HTTPS。
* 使用Adobe隨附的CDN （內容傳遞網路），作為Dynamic Media授權的一部分。
* 使用專用網域(即 `images.company.com` 或 `mycompany.scene7.com`)，而不是通用的Dynamic Media網域(也就是說， `s7d1.scene7.com`， `s7d2.scene7.com`，或 `s7d13.scene7.com`)。

   若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或多個帳戶。 然後導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**. 尋找標示為的欄位 **已發佈的伺服器名稱**. 如果您目前使用一般Dynamic Media網域，您可以在此轉變中要求移至您自己的自訂網域。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 並要求切換至HTTP/2；這不會自動為您完成。
1. 在您的支援案例中提供下列資訊：

   * 主要連絡人姓名、電子郵件和電話號碼。
   * 所有要轉換為HTTP2的網域。 也就是說， `images.company.com` 或 `mycompany.scene7.com`.

      若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或多個帳戶。 然後導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**. 尋找標示為的欄位 **[!UICONTROL 已發佈的伺服器名稱]**.

   * 確認您使用安全HTTPS處理多媒體請求。
   * 確認您是透過Adobe使用CDN，且未透過直接關係管理。
   * 確認您使用專用網域。 也就是說， `images.company.com` 或 `mycompany.scene7.com`，不是一般Dynamic Media網域，例如 `s7d1.scene7.com`， `s7d2.scene7.com`， `s7d13.scene7.com`.

      若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或多個帳戶。 然後導覽至 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**. 尋找標示為的欄位 **[!UICONTROL 已發佈的伺服器名稱]**. 如果您目前使用一般Dynamic Media網域，您可以在此轉變中要求移至您自己的自訂網域。

1. Adobe客戶支援會根據提交請求的順序，將您新增至HTTP/2客戶輪候清單。
1. 當Adobe準備好處理您的請求時，「支援」會聯絡您以協調轉變並設定目標日期。
1. 完成後，您將會收到通知，並且可以驗證是否成功轉換到HTTP2。

## 我何時可以轉換為HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

系統會依照Adobe客戶支援收到請求的順序來處理請求。

>[!NOTE]
>
>由於轉換至HTTP/2的過程涉及清除快取，因此前置時間較長。 因此，一次只能處理幾個客戶轉換。

## 移至HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN上的快取，因為它牽涉到移至新的CDN設定。

非快取內容會直接點選Adobe的原始伺服器，直到再次重建快取為止。 由於此動作，Adobe計劃一次處理一些客戶轉換，以便在從Adobe來源提取請求時維持可接受的效能。

## 如何驗證URL或網站是否以HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下載可與網頁瀏覽器搭配使用的擴充功能。 Firefox和Chrome有一個擴充功能，稱為 **[!UICONTROL HTTP/2和SPDY指標]**. 瀏覽器僅安全地支援HTTP/2，因此有必要呼叫具有HTTPS的URL以進行驗證。 如果支援HTTP/2，則會以藍色Flash符號和標頭「X-Firefox-Spdy」的格式表示擴充功能：「h2」。
