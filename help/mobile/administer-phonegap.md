---
title: 使用AEM管理Adobe PhoneGap Enterprise的內容
seo-title: Administering Content for Adobe PhoneGap Enterprise with AEM
description: 此頁面可作為管理Adobe PhoneGap Enterprise的登陸頁面。
seo-description: This page serves as landing page for administering Adobe PhoneGap Enterprise.
uuid: 31bda96a-bc35-4f04-9107-7d575c04d761
contentOwner: msm-service
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: cd080122-7ae5-4e6e-a8f6-b95dfbb0b511
exl-id: 5a98eb3c-5c12-4a6c-8d76-eed44c7c3df5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# 使用AEM管理Adobe PhoneGap Enterprise的內容 {#administering-content-for-adobe-phonegap-enterprise-with-aem}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

一個 ***AEM管理員*** 負責透過使用建立精靈建立新應用程式，或匯入現有應用程式，將新應用程式新增至AEM Mobile目錄。 使用AEM Mobile建立新應用程式的AEM管理員 *建立精靈* 通常會從我們現成的參考範例或（大多數情況下）建立的自訂應用程式範本中，選取其中一個所需的應用程式範本 *AEM開發人員。*

使用HTML5和PhoneGap建立行動應用程式後，您就可以在指揮中心管理該應用程式。 當然，您也可以使用Cordova網頁檢視，在命令中心管理原生應用程式的HTML5內容（以允許PhoneGap外掛程式存取原生功能）。

AEM Apps控制中心可讓您建置和部署行動應用程式、在發佈行動應用程式之前建立及編輯應用程式中繼資料、共同組織並經常發佈全新和相對的內容，而不需要重新造訪應用程式商店提交流程，以及分析應用程式生命週期和使用量度，以改善客戶轉換率和品牌忠誠度。

若要建置AEM Mobile應用程式，請參閱 [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md) 頁面，在開發人員區段中。

若要設定您的環境並開始使用控制中心，

1. [設定使用者和群組](/help/mobile/configure-users-groups.md)
1. [設定您的反向連結篩選器以允許空白](/help/mobile/setting-referrer-filter-empty.md)
1. [設定您的Adobe PhoneGap BuildCloud Service](/help/mobile/configure-phonegap-build-cloud.md)
1. [設定您的Adobe Analytics Cloud服務](/help/mobile/configure-adobe-mobile-cloud-service.md)

若要瞭解內容服務Content Services，請參閱 [管理內容服務](/help/mobile/developing-content-services.md).

>[!NOTE]
>
>此 *AEM驗證* 是在任何iOS或Android行動裝置上執行AEM行動應用程式的快速且簡單的方法。 此 *AEM驗證* 是行動應用程式，在您裝置上，然後將其連線到執行「快速入門」的伺服器，以取得要檢視的應用程式清單。 按一下 [此處](/help/mobile/phonegap-mobile-quickstart.md) 以檢視詳細資訊。

## 其他资源 {#additional-resources}

若要瞭解作者和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [在AEM中為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
