---
title: AEM Forms簡介
seo-title: Introduction to AEM Forms
description: 透過Adobe Experience Manager Forms，商業使用者可以將吸引人、回應式且最適化表單整合至網站和行動網站，簡化數位註冊程式，並提高客戶轉換率。
seo-description: With Adobe Experience Manager Forms, business users can integrate engaging, responsive, and adaptive forms into web and mobile sites, simplifying the digital enrollment process and increasing customer conversion rates.
uuid: a6564997-4227-4d5d-b27d-47a55a386238
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: a20383f2-f86a-45bf-a39e-725ee764503b
docset: aem65
feature: Adaptive Forms
exl-id: e5533b4f-93b7-4ea9-a01d-fdf9528652c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 10%

---

# AEM Forms簡介{#introduction-to-aem-forms}

如需AEM Forms最新功能和增強功能的相關資訊，請參閱 [AEM Forms的新功能](../../forms/using/whats-new.md).

## 關於AEM Forms {#about-aem-forms}

Adobe Experience Manager (AEM)提供易用的解決方案，可建立、管理、發佈和更新複雜的數位表格，同時與後端流程、商業規則和資料整合。

AEM Forms結合表單編寫、管理和發佈，以及通訊管理功能、檔案安全性和整合式分析，以建立引人入勝的端對端體驗。 AEM Forms可跨網路和行動裝置管道運作，能有效整合至您的業務流程，減少紙張流程和錯誤，同時提升效率。

在大型企业中，通常只创建表单一次，之后通过将它复制到内容管理系统中来进行重用。讓大型的表單資料庫保持最新狀態，並讓這些表單可供探索，是一項相當艱鉅的挑戰。 AEM 提供了一个可自定义的 Forms Portal，确保客户能够通过 Web 和移动渠道找到并访问所需的表单。

AEM Forms提供的表單管理工具不僅可讓您管理最適化表單，還可管理XFA表單、PDF forms和相關資產。 如需詳細資訊，請參閱 [管理表單簡介](../../forms/using/introduction-managing-forms.md).

![](do-not-localize/4th-draft.gif)

### 重要功能 {#key-capabilities}

總而言之，AEM Forms提供如以下的強大表單管理功能，可減少手動程式並提高客戶滿意度。

* 集中式Forms入口網站，用於設計和部署動態表單，包括PDF、HTML5和調適型表單
* 簡單易用的圖形使用者介面，可讓業務使用者輕鬆匯入、管理、預覽和發佈表單
* 回應式表單目錄，具有使用關鍵字、標籤和中繼資料的強大搜尋功能
* 動態偵測使用者的裝置和位置，以適當地在網頁和行動裝置頻道上呈現表單
* 與Adobe Analytics整合，以有效測量表單使用量度
* 與Adobe Document Cloud eSign服務或Scribble整合，以電子方式簽署包含機密資訊的檔案
* 自動化表單發佈功能，以及透過多個管道提供及時、個人化且一致的溝通能力

## AEM表單型別 {#aem-form-types}

AEM Forms可讓您擴充新表單和現有表單，以建立：

* 完美的畫素、分頁HTML和看起來幾乎像紙張的PDF forms，或者
* 自動為使用者裝置和瀏覽器轉譯的最適化表單。

**PDF forms**

PDF forms可以離線填寫、儲存在本機，以及下次連線時傳送的表單資料。 您可以使用2D條碼來擷取表單資料，並使用數位簽名來驗證使用者的真實性。

**HTML表單**

HTML5瀏覽器型表單可在行動裝置和桌上型瀏覽器上檢視。 您可以使用Scribble或eSign服務，以電子方式簽署HTML表單。

**調適型表單**

調適型表單可依需要新增或移除欄位或區段，以動態調整以符合使用者回應。 AEM可讓您重複使用AdobeXML表單範本來建立調適型表單。

### 支援的功能 {#supported-features}

所有表單型別都支援下列功能：

* 動態配置
* 表單欄位驗證
* 內容相關說明
* 指令碼和XML資料處理
* 協助工具設計與檢查
* 可在伺服器端儲存表單
* 支援檔案附件
* 與HTML Workspace整合以進行資料擷取

## 離線資料收集 {#offline-data-collection}

提交表單資料後，Adobe Experience Manager會將表單資料與現有系統、商業規則和所需人員連結。

AEM Forms提供Forms Workspace，此行動應用程式可將您的數位業務流程延伸到行動裝置。 使用Forms工作區，您甚至可以在離線時收集並記錄資料。 Forms工作區可運用行動裝置的功能，讓您擷取像片、視訊，並收集時間戳記和其他資訊等資料。 下次連線到網路時，您可以同步收集的資料。

離線擷取資料並在下次回線時加以同步處理對現場人員特別有幫助。 它可提升生產力並減少錯誤。

**使用Forms Workspace進行離線資料收集的優點**

* 易於使用的HTML工作區應用程式，用於任務指派和追蹤
* 拖放式工作流程設計環境
* 企業內容管理聯結器(ECM)
* 開放式標準支援，包括XML和SOAP，可將表單資料與企業系統連線
* 現成可用的HTML報告可監控積壓、工作佇列和關鍵績效指標(KPI)
* 可自訂的儀表板，可即時深入分析業務營運
* 用於連線協力廠商報告工具的API

![](do-not-localize/3rd-draft.gif)

## 個人化通訊 {#personalized-communication}

高效自助服务数字体验的一个重要组成部分是，及时传达用户可以在任意位置通过任意设备访问的个性化信息。个性化和及时的通信可以提高转化率和用户满意度。

商業使用者可以使用AEM Forms自訂檔案範本、合併來自後端流程的資訊，並包含互動式元件，藉此建立引人入勝的個人化使用者體驗。 直覺式使用者介面可協助非技術使用者開發商業規則，以決定何時根據查詢產生通訊，或起始使用者產生的回應。

個人化檔案（例如，收據、歡迎套件和宣告）可以輕鬆地跨多個管道傳送。 组织可以将流量引入个性化的 Web 门户，从而让受众注册或购买额外的服务。

**关键功能**

* 通訊製作環境，支援範本、內容區塊、商業規則等
* 檔案轉換和組裝
* 支援透過多個管道（包括網路、電子郵件和紙張）隨選或批次檔案傳送
* 具有變更記錄的稽核軌跡
* 支援數位簽章，以驗證內容完整性和簽署者的身分
* AEM Forms的Document Security附加元件，包括加密、使用原則、追蹤和稽核

![](do-not-localize/layout-02.png)

簡化的個人化通訊工作流程
