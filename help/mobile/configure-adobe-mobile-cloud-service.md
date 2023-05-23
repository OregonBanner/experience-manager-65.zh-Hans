---
title: 設定您的Adobe行動服務Cloud Service
seo-title: Configure your Adobe Mobile Services Cloud Service
description: 請依照本頁面的說明設定您的Adobe Mobile ServicesCloud Service。
seo-description: Follow this page to configure your Adobe Mobile Services Cloud Service.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
exl-id: 209c36f9-1a4b-4eea-8dde-22e0fc9718c1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 設定您的Adobe行動服務Cloud Service {#configure-your-adobe-mobile-services-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

此 **行動量度動態磚** 位於命令中心，為您的行動應用程式提供即時分析。

此 [AdobeMobile Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK可透過PhoneGap外掛程式使用。 系統會在裝置上收集量度並加以快取，直到裝置連線為止，此時會將資料推送至AdobeMobile Services雲端，以進行報表和分析。

Adobe Mobile Analytics SDK提供下列功能：

1. **行動頻道的資料收集**  — 收集所有主要作業系統上行動網站和應用程式的完整資料。
1. **行動參與分析**  — 瞭解使用者在您的行動應用程式、網站或視訊中的參與度，包括消費者啟動管道的頻率、是否從中進行購買等等。
1. **行動應用程式控制面板和報表**  — 取得包含應用程式和應用程式商店量度之生命週期量度的使用情況報表 — 檢視使用者、啟動次數、平均工作階段長度、保留時間長度和當機次數趨勢。
1. **行動促銷活動分析**  — 量化行動裝置特定行銷活動的成效，例如SMS、行動搜尋廣告、行動顯示廣告和二維碼。
1. **地理位置分析**  — 透過GPS位置或地標，找出您的應用程式使用者在哪裡啟動以及與您的行動體驗互動。
1. **路徑分析**  — 瞭解使用者如何導覽您的應用程式，以判斷哪些畫面和UI元素吸引使用者，以及哪些造成使用者流失。

>[!CAUTION]
>
>此 **分析量度** 只有在您已設定雲端服務時，圖磚才會顯示在控制面板中。

![chlimage_1-22](assets/chlimage_1-22.png)

AEM Command Center量度圖磚

## 設定Cloud Service {#configuring-the-cloud-service}

為了妥善運用Adobe行動服務分析功能，您需要使用Adobe Analytics帳戶資訊設定AEM Mobile Analytics Cloud服務。

1. 按一下右上角的圖示，即可從新增或編輯Cloud Services **管理Cloud Services** 從應用程式儀表板動態磚。

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. 此 **新增或編輯Cloud Services** 熒幕顯示。 選取 **Adobe行動服務** 並按一下 **下一個**.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. 從中選擇現有設定 **行動服務** 或選擇 **建立設定** 以建立新檔案。

   若為新設定，請輸入 **行動服務屬性**&#x200B;並按一下&#x200B;**驗證。**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   如果認證已驗證， **驗證** 按鈕變更為 **已驗證**. 您可以從中選擇行動服務應用程式 **選取行動應用程式服務**.

   按一下 **提交** 以設定您的設定。

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 設定雲端設定後，您即可在控制面板中檢視相同的設定。

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >設定雲端設定後，您可以檢視 **分析量度** 在您應用程式儀表板中的動態磚。

   ![chlimage_1-28](assets/chlimage_1-28.png)
