---
title: 將Adobe Analytics新增至您的行動應用程式
seo-title: Add Adobe Analytics to your Mobile Application
description: 請詳閱本頁面，瞭解如何透過與Analytics Mobile Services整合，在AEM應用程式中使用行動應用程式Adobe。
seo-description: Follow this page to learn about how you can use Mobile App Analytics in your AEM Apps by integrating with Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# 將Adobe Analytics新增至您的行動應用程式{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

想要為您的行動應用程式使用者建立吸引人且相關的體驗嗎？ 如果您沒有使用AdobeMobile Services SDK來監控和測量應用程式的生命週期和使用量，那麼您的決策依據是什麼？ 您最忠實的客戶在何處？ 如何確保您保持相關度並最佳化轉換？

您的使用者是否存取所有內容？ 他們是否正在放棄應用程式？如果是，在哪裡放棄？ 他們會在應用程式中停留多久，以及回訪使用應用程式的頻率？ 您可以引入哪些變更，然後測量增加保留率的程度？ 當機率怎麼樣，您的應用程式對使用者而言是否當機？

充分利用 [行動應用程式分析](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) 在您的AEM應用程式中，透過與整合 [Adobe行動服務](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

檢測您的AEM應用程式，以追蹤、報告並瞭解您的使用者如何與您的行動應用程式和內容互動，並測量關鍵生命週期量度，例如啟動次數、應用程式使用時間和當機率。

本節說明AEM如何運作 *開發人員* 可以：

* 將行動分析整合至您的行動應用程式
* 使用Bloodhound測試您的分析追蹤

## 先決條件 {#prerequisties}

AEM Mobile需要Adobe Analytics帳戶，才能在您的應用程式中收集和報告追蹤資料。 在設定中， AEM *管理員* 將首先需要：

* 設定Adobe Analytics帳戶，並在Mobile Services中為您的應用程式建立報表套裝。
* 在Adobe Experience Manager (AEM)中設定AMSCloud Service。

## 適用於開發人員 — 將Mobile Analytics整合至您的應用程式 {#for-developers-integrate-mobile-analytics-into-your-app}

### 設定ContentSync以提取設定檔案 {#configure-contentsync-to-pull-in-configuration-file}

設定Analytics帳戶後，您需要建立Content Sync設定，以將內容拉入您的行動應用程式。

如需其他詳細資訊，請參閱設定內容同步內容。 設定需要指示Content Sync將ADBMobileConfig放入/www目錄。 例如，在Geometrixx Outdoors應用程式中， Content Sync設定位於： */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-config/ams-ADBMobileConfig*. 也有可供開發的設定；但是，在Geometrixx Outdoors的情況下它與非開發設定相同。

如需進一步瞭解如何從行動應用程式AEM應用程式儀表板下載ADBMobileConfig，請參閱Analytics - Mobile Services -AdobeMobile Services SDK設定檔案。

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

每個平台都需要將ADBMobileConfig複製到特定位置。

如果使用PhoneGap CLI建置，則可使用cordova建置掛接指令碼來完成。 您可在Geometrixx Outdoors應用程式中檢視以下資訊：*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

若為iOS，檔案需要複製到Xcode專案的 **資源** 目錄(例如 &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;)。 如果應用程式目標為Android，則複製的目的地路徑為「platforms/android/assets/ADBMobileConfig.json」。 有關在PhoneGap CLI建置期間使用鉤點的更多詳細資訊，請參閱 [勾選您的Cordova/PhoneGap專案需求](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### 在應用程式中新增AMS外掛程式 {#add-the-ams-plugin-in-the-app}

應用程式若要收集資料，必須將AdobeMobile Services (AMS)外掛程式納入應用程式中。 將外掛程式加入為應用程式的config.xml中的功能，就能在PhoneGap Build程式期間，使用另一個Cordova鉤點來自動新增外掛程式。

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors App config.xml位於 */content/phonegap/geometrixx-outdoors/shell/jcr：content/pge-app/app-content/phonegap/www/config.xml*. 上述範例要求使用特定版本的外掛程式，方法是先新增「#」，接著在外掛程式URL後面加上標籤值。 這是一個良好的做法，可確保在建置期間新增未經測試的外掛程式時，不會出現未預期的問題。

執行這些步驟後，您的應用程式將可報告Adobe Analytics提供的所有生命週期量度。 這包括啟動、當機和安裝等資料。 如果這是您唯一在意的資料，則表示您已完成。 如果您想要收集自訂資料，則需要檢測您的程式碼。

### 檢測您的程式碼以進行完整應用程式追蹤 {#instrument-your-code-for-full-app-tracking}

中提供數個追蹤API [AMS Phonegap外掛程式API。](https://experienceleague.adobe.com/docs/mobile-services/ios/phonegap-ios/phonegap-methods.html)

這些功能可讓您追蹤狀態和動作，例如使用者在應用程式中導覽至的頁面、最常使用哪些控制項。 要偵測應用程式以進行追蹤，最簡單的方式是使用AMS外掛程式提供的Analytics API。

* ADB.trackState()
* ADB.trackAction()

如需參考資訊，您可以在Geometrixx Outdoors應用程式中檢視程式碼。 在Geometrixx Outdoors應用程式中，所有頁面導覽都使用ADB.trackState()方法進行追蹤。 如需詳細資訊，請檢視/libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js的原始程式碼

透過使用這些方法呼叫來檢測您的原始程式碼，您就可以收集應用程式的完整量度。

#### 連線至AMS的屬性 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l會公開下列屬性以連線至AMS：

| **标签** | **描述** | **默认** |
|---|---|---|
| API端點 | AdobeMobile Services HTTP API的基本URL | https://api.omniture.com |
| 設定端點 | 用於擷取給定報表套裝ID的ADB行動設定的URL | /ams/1.0/app/config/ |
| 行動服務應用程式 | 取得使用者公司內的應用程式清單 | /ams/1.0/apps |
