---
title: 您的混合式應用程式是否已準備好使用AEM Mobile？
seo-title: Is your hybrid app ready for AEM Mobile?
description: 請依照此頁面瞭解雜湊應用程式。 AEM中的應用程式通常分為兩個部分。 「殼層」和「內容」及此頁面提供這些主題的更多深入分析。
seo-description: Follow this page to learn about hrybrid apps. An app in AEM is commonly divided into two parts. The 'shell' and 'content' and this page provides more insight on these topics.
uuid: cbcce3fa-9100-46ea-9f24-931b42666709
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b7fd7954-f2a5-402d-b259-e18b5a618be9
pagetitle: Is your hybrid app ready for AEM Mobile?
exl-id: 4625890c-2b76-4c78-88e8-23741bc09f5b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 您的混合式應用程式是否已準備好使用AEM Mobile？{#is-your-hybrid-app-ready-for-aem-mobile}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

您已將混合式PhoneGap或Cordova應用程式匯入AEM，現在該怎麼做？ 您可能會想要將可編寫的內容新增至應用程式。 若要完成此任務，您需要對AEM應用程式的結構有大致的瞭解。 AEM中的應用程式通常分為兩個部分。 「殼層」和「內容」。 「殼層」包含應用程式的靜態部分；例如PhoneGap設定檔案、應用程式架構和導覽控制項。 您匯入的歸檔內容會儲存為殼的一部分。 在此檔案的內容中，殼層是應用程式開發人員建置之混合PhoneGap應用程式的所有非AEM編寫內容。

內容是指由AEM開發人員建置的AEM中所編寫的元件、範本和編寫頁面。 內容會分類為開發人員內容或編寫內容。 元件、設計和頁面範本被視為開發內容，因為它們是由開發人員建置。 作者內容是使用元件和範本建立的頁面。 這些通常由設計人員或行銷人員完成。

將編寫的AEM頁面新增至您的混合式應用程式時，需要應用程式開發人員和AEM開發人員之間的協調。 應用程式中您想要新增編寫內容的任何地方，應用程式開發人員都必須採用可在AEM中重疊的結構來組織這些頁面。 應用程式開發人員必須能向AEM開發人員提供要新增AEM編寫內容的路徑，然後在混合應用程式中提供預留位置頁面，在AEM開發人員編寫頁面內容後取代預留位置頁面。

為了更方便理解，我們將使用AEMMarketing Cloud： AEM Mobile混合參考來說明概念。 混合式參考應用程式包含帶有側邊功能表的文摘頁面。

![chlimage_1-76](assets/chlimage_1-76.png)

在此範例中，我們將編寫應用程式的歡迎頁面。 檢視來源 [https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/hybrid-app/www/js/app.js#L75). 我們看到應用程式開發人員已定義歡迎頁面，並提供應用程式轉譯之頁面的範本。 這是應用程式開發人員和AEM開發人員需要協調的地方。 混合參考應用程式中歡迎頁面範本的路徑定義為「content/mobileapps/hybrid-reference-app/en/welcome.template.html」。 此路徑極為重要，因為AEM開發人員將使用相同的路徑，在AEM存放庫中編寫其歡迎頁面。

![chlimage_1-77](assets/chlimage_1-77.png)

混合式應用程式和AEM編寫內容使用相同路徑很重要，因為我們仰賴使用Content Sync覆蓋內容的功能，以將新頁面新增至混合式應用程式。 當混合式應用程式匯入到匯入程式的AEM中時，系統會設定Content Sync設定。

![chlimage_1-78](assets/chlimage_1-78.png)

當您從應用程式控制面板「下載來源」時，這些ContentSync指令碼會執行以組合混合式應用程式的封存。

![chlimage_1-79](assets/chlimage_1-79.png)

ContentSync會先提取應用程式的「殼層」（此為混合式應用程式所有開發內容的儲存位置），然後提取應用程式的「內容」。 現在，如果「shell」中有與「content」具有相同路徑的頁面，則「shell」下的頁面將（取代）為「content」下的頁面。 換言之，在混合參考應用程式範例中，如果我們在AEM中建立與「content/mobileapps/hybrid-reference-app/en/welcome.template.html」具有相同路徑的頁面，當ContentSync執行時，它將會以該位置的AEM中任何專案覆蓋作為混合參考應用程式一部分的頁面。 ContentSync會負責覆蓋，因此對於使用應用程式的人來說，使用AEM編寫內容更新應用程式看起來會很順暢，而且不需要重建應用程式。 因此，當您執行應用程式時，歡迎頁面會顯示如下：

![chlimage_1-80](assets/chlimage_1-80.png)
