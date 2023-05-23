---
title: 在AEM中開發行動應用程式
seo-title: Developing Mobile Applications in AEM
description: 請依照此頁面，開始使用Adobe PhoneGap Enterprise在AEM中開發行動應用程式。
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

AEM運用Adobe PhoneGap和Adobe Publishing Solutions，可讓您建立和管理內容豐富且以公用程式為基礎的跨平台行動應用程式：

* 在一個位置管理所有公司的行動應用程式。
* 檢閱開發和測試環境中的應用程式，免除布建設定檔的複雜性，以及額外費力建置和上傳應用程式以進行共用。
* 使用AEM編寫環境為您的應用程式建立和管理豐富的內容。
* 將HTML5與Adobe PhoneGap搭配使用，以裝置原生功能建立豐富的體驗。
* 將HTML5網頁檢視介紹給新的或預先存在的 **原生** Cordova WebViews的應用程式。
* 跨所有傳遞管道（包括網頁、行動網頁、行動應用程式和印刷）建立、組織和分享豐富的多媒體內容。

AEM與Adobe整合 **[PhoneGap Build服務](https://build.phonegap.com/)** 以簡化應用程式的建置和部署程式。

**AdobeContentSync** 可讓使用者輕鬆將Over-The-Air (OTA)頁面和內容更新下載至其裝置，而不需重新安裝應用程式，或從appStore、Google Play或其他應用程式來源下載。

**Adobe Analytics** 已完全整合至AEM應用程式，可詳細追蹤分佈、地理位置、作業系統、裝置、點選串流、iBeacon追蹤等。

## 建立應用程式 {#creating-apps}

開發人員可使用 [AEM PhoneGap入門套件](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) 以及中找到的其他資源 [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) 使用PhoneGap啟動AEM應用程式，包括執行Cordova Webviews的參考原生應用程式。

Starter Kit Git存放庫的Readme包含使用Starter Kit的教學課程：

* 自訂品牌
* Maven範例建置和部署目標
* 原始檔控制存放庫設定
* 安裝並部署至本機或遠端AEM執行個體
* 從AEM解除安裝

>[!NOTE]
>
>您可在GitHub上找到其他參考實作來源，包括Labs [此處](https://github.com/adobe-marketing-cloud-apps) 以及「廚房水槽」來源 [此處](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## 針對IOS 9和HTTP主機開發 {#developing-for-ios-and-http-hosts}

iOS開發人員應注意iOS 9上執行的Cordova應用程式的一個未完成問題。 此問題會導致系統無法向不安全的主機提出要求(例如 *http://localhost:4502*)。 此問題將通過即將發行的cordova-ios （由Cordova CLI使用）解決，但與此同時，有兩種可用的解決方法：

1. 作為立即的因應措施，您仍然可以使用任何iOS 8模擬器，而不會出現問題。
1. 如果您必須使用iOS 9，您的應用程式 — Info.plist （在執行後找到） `cordova platform add ios` 在&quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>-Info.plist&quot;)檔案可以手動編輯以包含以下屬性：

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>如需「App Transport Security」的詳細資訊，請參閱以下章節 [Apple的iOS9發行前檔案](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) 以及這個 [棧疊溢位討論](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## 在AEM中開發行動應用程式 {#developing-mobile-applications-in-aem-1}

* [啟動AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [建立行動應用程式](/help/mobile/building-app-mobile-phonegap.md)
* [建構應用程式](/help/mobile/phonegap-structure-an-app.md)
* [使用Apps Console建立和編輯應用程式](/help/mobile/phonegap-apps-console.md)
* [单页面应用程序](/help/mobile/phonegap-single-page-applications.md)
* [使用PhoneGap CLI開發應用程式](/help/mobile/phonegap-apps-pg-cli.md)
* [存取裝置功能](/help/mobile/phonegap-access-device-features.md)
* [透過AdobeMobile Analytics追蹤應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
* [將Adobe Analytics新增至您的行動應用程式](/help/mobile/phonegap-add-analytics-to-apps.md)
* [推送通知](/help/mobile/phonegap-push-notifications.md)
* [AEM Mobile內容個人化](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [應用程式的剖析](/help/mobile/phonegap-apps-arch.md)
* [您的混合式應用程式是否已準備好使用AEM Mobile？](/help/mobile/phonegap-adding-content-to-imported-app.md)

### 其他资源 {#additional-resources}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise編寫](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
