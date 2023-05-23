---
title: 透過AdobeMobile Analytics追蹤應用程式效能
seo-title: Track App Performance with Adobe Mobile Analytics
description: 透過AdobeMobile Services，您可以追蹤使用狀況、應用程式當機、裝置詳細資訊，以及其他許多行動應用程式的關鍵量度，深入瞭解使用者如何使用行動應用程式。 請詳閱本頁以瞭解更多資訊。
seo-description: With Adobe Mobile Services you can gain insight on how your users are using your mobile apps by tracking usage, app crashes, device details and so many other critical metrics for your mobile apps. Follow this page to learn more.
uuid: 139858c7-66a1-4fea-9f7e-4671b86f67e6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 377548fa-987a-4a59-84a3-067a3541b6b2
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# 透過AdobeMobile Analytics追蹤應用程式效能{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

您想要提高客戶轉換率和忠誠度。

您想要為客戶提供相關且吸引人的體驗。

您的AEM Mobile應用程式對行銷活動有何影響？

如何微調行動應用程式以提供使用者最佳體驗？

透過AdobeMobile Services，您可以追蹤使用狀況、應用程式當機、裝置詳細資訊，以及其他許多行動應用程式的關鍵量度，深入瞭解使用者如何使用行動應用程式。

Adobe Experience Manager Mobile可讓您直接從AEM Mobile應用程式控制面板，快速一覽行動分析的詳細資訊。 此 **行動量度動態磚** 儀表板中的可為您的行動應用程式提供即時分析，好讓開發人員、作者和管理員快速瞭解您的行動應用程式的運作狀況。 在封面底下支援分析的是 [AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK. AdobeMobile Analytics SDK可以原生或透過PhoneGap Bridge外掛程式插入您的應用程式以進行網頁檢視。 系統會在裝置上收集量度並加以快取，直到裝置連線為止，接著資料會推送至AdobeMobile Services雲端，以便進行報表和分析。

Adobe Mobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集所有主要作業系統上行動網站和應用程式的完整資料。
1. **行動參與分析**  — 瞭解使用者在您的行動應用程式、網站或視訊中的參與度，包括消費者啟動管道的頻率、是否從中進行購買等等。
1. **行動應用程式控制面板和報表**  — 取得包含應用程式和應用程式商店量度之生命週期量度的使用情況報表 — 檢視使用者、啟動次數、平均工作階段長度、保留時間長度和當機次數趨勢。
1. **行動促銷活動分析**  — 量化行動裝置特定行銷活動的成效，例如SMS、行動搜尋廣告、行動顯示廣告和二維碼。
1. **地理位置分析**  — 透過GPS位置或地標，找出您的應用程式使用者在哪裡啟動以及與您的行動體驗互動。
1. **路徑分析**  — 瞭解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，以及哪些造成使用者流失。

本節說明如何進行 [AEM開發人員](#developers) 然後可以瞭解如何透過analytics追蹤來檢測AEM Mobile應用程式。

最後， [AEM管理員](#administrators) 瞭解：

* 建立雲端服務以Adobe行動服務
* 建立行動服務設定並關聯報表套裝
* 將行動服務設定與行動應用程式建立關聯
* 透過AEM應用程式命令中心檢視量度
* 將AMS SDK設定指派至您的行動應用程式

## 適用於開發人員 — 將Analytics整合至您的應用程式 {#for-developers-integrate-analytics-into-your-app}

**先決條件：** AEM管理員需要設定AdobeMobile Services雲端設定， [如下所述](#amscloudserviceconfig).

開發人員需負責 [將analytics新增至AEM Mobile應用程式](/help/mobile/phonegap-add-analytics-to-apps.md) 追蹤、報告及瞭解您的使用者如何參與行動應用程式內容，以及測量啟動、應用程式逗留時間和當機率等關鍵生命週期量度的必要專案。

## 適用於管理員 — 設定AdobeMobile ServicesCloud Service {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

為了妥善運用Adobe Mobile Services的優勢，您需要使用Adobe Analytics帳戶資訊設定AEM Adobe Mobile ServicesCloud Service。 應用程式命令中心提供 **分析量度** 圖磚，您可在此處建立雲端服務並將其與行動應用程式建立關聯。

若要開始設定行動應用程式的雲端服務，請按一下「分析量度」圖磚上的齒輪圖示。

![chlimage_1-125](assets/chlimage_1-125.png)

按一下「分析量度」表徵圖中的齒輪圖示，將會開啟「設定Mobile Services Analytics」強制回應對話方塊。 從「選取行動服務設定」下拉式清單中選取您的設定。 如果您需要建立新組態，請按一下扳手按鈕。

若要建立Adobe Mobile Service雲端服務，需要兩個步驟：連線至服務並選取要指派給設定的報表套裝。

若要開始，請按一下控制面板中「管理Cloud Services」表徵圖上的「+」按鈕。

![chlimage_1-126](assets/chlimage_1-126.png)

按一下「**+**&#39;按鈕， **新增Cloud Service** 精靈將會顯示。

![chlimage_1-127](assets/chlimage_1-127.png)

填寫下列必填欄位，以選取或建立新的行動服務設定。 您的AEM管理員需要此資訊才能成功建立與AdobeMobile Services的連線。

![chlimage_1-128](assets/chlimage_1-128.png)

完成Mobile Services帳戶設定後，系統會提示您選取應用程式。 這麼做會將Adobe Mobile Service分析報表連線至該應用程式。

選取所需的行動服務，然後按一下「更新」以指派行動服務設定，並關閉對話方塊。

現在您已將Mobile Service設定與AEM Mobile應用程式建立關聯，圖磚就會開始擷取量度資料並開始製作報表。

![chlimage_1-129](assets/chlimage_1-129.png)

### AdobeMobile Services SDK設定檔案 {#adobe-mobile-services-sdk-config-file}

此時，您的行動應用程式已與雲端服務建立關聯，但行動應用程式還不知道如何將收集到的行動量度傳回Adobe Analytics。 若要將行動應用程式連線至Adobe Analytics，需要將AdobeMobile Services SDK設定檔案新增至Adobe Experience Manager。

在分析量度圖磚中，按一下箭頭圖示，即可顯示「下載/上傳AMS SDK設定」功能表專案。

![chlimage_1-130](assets/chlimage_1-130.png)

第一步是從Adobe Mobile Services取得SDK設定，按一下「下載AMS SDK設定」會將您重新導向至AdobeMobile Services網站，您可在其中下載設定檔案。 取得ADBMobileConfig.json檔案後，按一下「上傳AMS SDK設定」即可將設定檔案上傳至AEM。

![chlimage_1-131](assets/chlimage_1-131.png)

按一下「上傳AdobeMobile Services應用程式設定」按鈕，並瀏覽ADBMobileConfig.json檔案，然後按一下「上傳」。

行動應用程式現在已可存取ADBMobileConfig.json檔案，並已瞭解如何傳回Adobe Analytics並開始報告有助於推動應用程式成功的重要量度值。

## 后续内容? {#what-s-next}

1. [開始我的AEM Mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用程式內容](/help/mobile/phonegap-manage-app-content.md)
1. [建置我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [透過AdobeMobile Analytics追蹤我的應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化的應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
