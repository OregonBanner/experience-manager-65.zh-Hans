---
title: 測試行動應用程式
seo-title: Testing Mobile Apps
description: 測試行動應用程式
seo-description: null
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# 測試行動應用程式{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）專案使用SPA編輯器。 [了解详情](/help/sites-developing/spa-overview.md).

鑑於市面上各種裝置和即將發行的裝置，測試您的應用程式已變得極為重要。 這是功能和可用性在應用程式商店中可能獲得低評價的地方，但單一缺陷可能會導致您的應用程式解除安裝。 測試計畫和品質保證必須謹慎處理。 以下連結涵蓋許多需要一般處理的主題，例如，識別您的環境、定義測試案例、測試型別、假設、客戶參與等。 另外還討論了有助於測試工作的工具。 內部工具，例如 [Hobbes](/help/sites-developing/hobbes.md)，可協助您進行網頁式UI測試。 [艱難的一天](/help/sites-developing/tough-day.md) 會以模擬的負載來強調例證。 如果您的測試環境已有使用協力廠商工具（例如Selenium）的經驗，也可以使用這些工具。

在開發行動應用程式時，許多特定於裝置的新問題必須與傳統測試一起解決。

* 功能 — 您的應用程式是否符合所有需求？
* 可用性 — 您的客戶是否可輕鬆使用和瞭解應用程式？
* 效能 — 使用量尖峰期間會發生什麼事？ 應用程式元素（例如撥動和輪播）是否能快速且不會偏離體驗？
* 失敗或中斷 — 當您的應用程式在執行時，有來電或通知時會發生什麼情況？ 如果網路中斷或關機會發生什麼情況？
* 安裝與更新 — 安裝體驗如何？ 如何推送更新？
* 技術性 — 您的應用程式是否消耗裝置過多的電力？
* 本地化 — 應用程式中的所有區域都經過翻譯嗎？
* 認證 — 您的應用程式是否已通過認證？ 客戶是否可相信其遵循所有資料隱私權法律規定？

這些問題應在您的自動化和手動測試期間獲得解答。

## 自動化測試 {#automated-testing}

應執行一定程度的自動化測試，以涵蓋各種熒幕大小、記憶體限制、輸入方法和作業系統。 它不僅涵蓋許多測試案例，而且可在引入新功能或裝置時加快回歸測試。 理想情況下，您的自動化工具應該減少或限制重複工作。 使用工具或架構，讓您的測試工作可套用在所有平台。 下圖顯示用於網頁式UI測試和行動應用程式測試的測試環境的簡化結構。 圖表左側顯示一系列使用瀏覽器的Selenium節點。 SeleniumGrid可以將常見的Web型UI測試陣列化到這些節點中的任一個。 Selenium中心也可以連線至Appium，以進行跨平台應用程式測試。 只顯示模擬器，但您可以納入adb （適用於Android）和Xcode (適用於iOS裝置)公用程式。 本檔案稍後會提供連結，您可以在其中找到提及之工具的特定詳細資料。

![chlimage_1](assets/chlimage_1.jpeg)

## 手動測試 {#manual-testing}

除了自動化測試之外，您的應用程式還應進行一系列手動測試。 指令碼無法複製在真實裝置上執行應用程式的客戶。 在這裡，您也有許多選項。 您可以使用HockeyApp等平台來定義誰有權存取及收集意見回饋。 或者，您可以將整個程式外包給UTest、ElusiveStars或Testn等服務。 如果您有一組內部測試者，但缺少裝置的變化，則可使用雲端服務在其裝置集區上執行手動測試。 其中一項服務提供的是SauceLabs。 您也可以從遠端建立應用程式至PhoneGap Enterprise，並安裝在本機裝置上，作為驗收測試或降級等級。 請參閱 [PhoneGap](https://phonegap.com/) 網站以取得其最新功能和檔案。 無論採用何種方法，手動測試都應如此；

* 撞上了一大群測試者，
* 針對大型裝置集區進行測試（最好是真實的裝置，但如果沒有真正的裝置，則為模擬器/模擬器），
* 提供資訊性意見反應：

   * 當機報告，
   * 分析/追蹤，
   * 可用性，
   * 需要注意的領域，
   * 效能，
   * 資料/耗電量等

## 工具 {#tools}

測試行動應用程式時可使用多種工具。 選擇使用的選項將視您的特定情況而定：功能、價格、支援、涵蓋範圍等。 以下只是一些可用工具與服務的簡短說明。

**Selenium**

* 此架構包含用於測試指令碼的API，以提供WebDriver並控制各種瀏覽器。
* 您可以將其與Appium搭配使用，以便在實際裝置上進行測試。
* SeleniumGrid會跨節點指引測試，以進行平行測試。
* Selenium IDE有助於減少測試案例的寫入。

如需詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* 雲端型測試服務，提供持續整合掛接和真實裝置測試。
* 包含應用程式編目程式，可檢查裝置相容性、分析記錄、瀏覽檢視、擷取熒幕擷取畫面及監控效能。

如需詳細資訊，請參閱 [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium是自動化行動測試的熱門跨平台架構。
* 此外，檢查器還隨附記錄功能，以協助程式碼測試案例。

如需詳細資訊，請參閱 [https://appium.io/](https://appium.io/).

**醬汁實驗室**

* SauceLabs提供雲端型測試，並與持續整合整合。
* 測試會在他們的雲端環境中自動執行，或者您可以啟動特定裝置或平台，並執行手動測試以幫助偵錯問題。

如需詳細資訊，請參閱 [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* 將測試您的行動應用程式的外包服務。
* 包含大量裝置，並提供多種型別的測試：效能、品質、功能、認證、本地化、資料使用量等。

如需詳細資訊，請參閱 [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp屬於手動測試，其中行動應用程式會推送至個人應用程式商店，以供測試人員下載及試用。

如需詳細資訊，請參閱 [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* 雖然Jenkins不是測試工具，但它是持續整合架構，提供自動化測試的主幹。 有許多協力廠商外掛程式可用來擴充功能。 例如，SeleniumGrid外掛程式提供UI來協助管理Selenium中心和節點。

如需詳細資訊，請參閱 [https://jenkins-ci.org/](https://jenkins-ci.org/) 和 [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
