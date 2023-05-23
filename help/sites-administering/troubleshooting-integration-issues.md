---
title: 疑難排解整合問題
seo-title: Troubleshooting Integration Issues
description: 瞭解如何疑難排解整合問題。
seo-description: Learn how to troubleshoot integration issues.
uuid: fe080e58-a855-4308-a611-f72eb47ba82d
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 422ee332-23ae-46bd-8394-a4e0915beaa2
exl-id: 11b0023e-34bd-4dfe-8173-5466db9fbe34
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# 疑難排解整合問題{#troubleshooting-integration-issues}

## 一般疑難排解提示 {#general-troubleshooting-tips}

### 確定沒有JavaScript錯誤 {#ensure-there-are-no-javascript-errors}

檢查瀏覽器的JavaScript主控台是否顯示任何錯誤。 未處理的錯誤可能會妨礙後續程式碼正確執行。 如果出現錯誤，請檢查導致錯誤的指令碼以及在哪個區域。 指令碼的路徑可能會指出指令碼所屬的功能。

### 在元件層級登入 {#logging-on-component-level}

在某些情況下，在元件層級新增其他陳述式可能會有幫助。 由於元件已呈現，您可以新增暫時標籤以顯示可能有助於您識別潛在問題的變數值。 例如：

```
<%
log.info("myVariable={}", myVariable);
%>

<!--
<%= myJspVariable %>
-->

<!--
${ myHtlVariable }
-->
```

如需有關記錄的其他詳細資訊，請參閱 [記錄](/help/sites-deploying/configure-logging.md) 和 [使用稽核記錄和記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files) 頁面。

## Analytics整合問題 {#analytics-integration-issues}

### Report Importer導致CPU/記憶體使用量高 {#the-report-importer-causes-high-cpu-memory-usage}

Report Importer導致CPU/記憶體使用率高或導致 `OutOfMemoryError` 例外。

#### 解决方案 {#solution}

若要修正此問題，請嘗試下列步驟：

* 請確定並未註冊大量PollingImporters （請參閱以下的「由於PollingImporter關機需要很長時間」一節）。
* 對以下專案使用CRON運算式，在一天中的特定時間執行報表匯入程式： `ManagedPollingImporter` 中的設定 [OSGi控制檯](/help/sites-deploying/configuring-osgi.md).

如需有關在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

### 由於PollingImporter，關機需要很長的時間 {#shutdown-takes-a-long-time-due-to-the-pollingimporter}

Analytics在設計時已考慮繼承機制。 通常，您會透過在頁面屬性中新增Analytics設定的參照來啟用網站的Analytics [Cloud Services](/help/sites-developing/extending-cloud-config.md) 標籤。 然後，設定會自動繼承到所有子頁面，無需再次參考，除非頁面需要不同的設定。 新增對網站的參照也會自動建立多個型別的節點(12個適用於AEM 6.3及舊版，或6個適用於AEM 6.4及更新版) `cq;PollConfig` 這會具現化用來將Analytics資料匯入AEM的PollingImporters。 因此：

* 有大量頁面參考Analytics會導致大量的PollingImporters。
* 此外，複製和貼上參照Analytics設定的頁面會導致其PollingImporters重複。

#### 解决方案 {#solution-1}

首先，分析 [error.log](/help/sites-deploying/configure-logging.md) 可讓您深入瞭解作用中或註冊的PollingImporters數量。 例如：

```
# Count PollingImporter entries
$ sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\),interval.*/\1/p" error.log | wc -l
86415
# Count PollingImporter entries for last30days
$ sed -n "s/.*(aem-analytics-integration-last30Days).*target=\(.*\),interval.*/\1/p" error.log | wc -l
14531
# Count unique paths of PollingImporter registrations
sed -n "s/.*(aem-analytics-integration-.*).*target=\(.*\)\/jcr:content.*/\1/p" error.log | sort | uniq -c
28115
```

其次，請確定只有最上層頁面（在階層中位於頂端）有參照的Analytics設定。

如需有關在AEM中建立自訂資料匯入工具服務的其他詳細資訊，請參閱以下文章 [https://helpx.adobe.com/experience-manager/using/polling.html](https://helpx.adobe.com/experience-manager/using/polling.html).

## DTM（舊版）問題 {#dtm-legacy-issues}

### DTM指令碼標籤未呈現在頁面來源中 {#the-dtm-script-tag-is-not-rendered-in-the-page-source}

此 [DTM](/help/sites-administering/dtm.md) 指令碼標籤未正確包含在頁面中，即使已在頁面屬性中參考設定 [Cloud Services](/help/sites-developing/extending-cloud-config.md) 標籤。

#### 解决方案 {#solution-2}

若要修正此問題，請嘗試下列步驟：

* 請確定加密的屬性可以解密(請注意，加密可能在每個AEM執行個體上使用不同的自動產生金鑰)。 如需其他詳細資訊，請閱讀 [設定屬性的加密支援](/help/sites-administering/encryption-support-for-configuration-properties.md).
* 重新發佈在中找到的設定 `/etc/cloudservices/dynamictagmanagement`
* 檢查ACL `/etc/cloudservices`. ACL應為：

   * 允許； jcr：read； webservice-support-servicelibfinder
   * 允許； jcr：read；每個人； rep:glob:&amp;ast；/defaults/&amp;ast；
   * 允許； jcr：read；每個人； rep:glob:&amp;ast；/defaults
   * 允許； jcr：read；每個人； rep:glob:&amp;ast；/public/&amp;ast；
   * 允許； jcr：read；每個人； rep:glob:&amp;ast；/public

如需有關管理ACL的詳細資訊，請閱讀 [使用者管理與安全性](/help/sites-administering/security.md#permissions-in-aem) 頁面。

## Target整合問題 {#target-integration-issues}

### 使用自訂頁面元件時，目標內容在預覽模式中不可見 {#targeted-content-not-visible-in-preview-mode-when-using-custom-page-components}

發生此問題的原因是因為自訂頁面元件未包含處理Target DTM整合的正確JSP或使用者端資料庫。

#### 解决方案 {#solution-3}

您可以嘗試下列解決方案：

* 確定自訂 `headlibs.jsp` （如有） `/apps/<CUSTOM-COMPONENTS-PATH>/headlibs.jsp`)包含下列專案：

```
<%@include file="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" %>
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

* 確定自訂 `head.html` （如有） `/apps/<CUSTOM-COMPONENTS-PATH>/head.html`) **不會** 選擇性地包含特定的整合標題庫，例如下列範例：

```
<!-- DO NOT MANUALLY INCLUDE SPECIFIC CLOUD SERVICE HEADLIBS LIKE THIS -->
<meta data-sly-include="/libs/cq/dtm/components/dynamictagmanagement/headlibs.jsp" data-sly-unwrap/>
```

此 `servicelibs.jsp` 新增必要的Analytics JavaScript物件，並載入與網站相關聯的雲端服務程式庫。 若為Target服務，程式庫是透過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的程式庫組取決於目標使用者端程式庫的型別( `mbox.js` 或 `at.js`)用於Target設定。

使用DTM進行遞送時 `mbox.js` 或 `at.js` 請確定在轉譯內容之前載入程式庫。 使用以非同步方式載入這些程式庫的Tag Management系統，可能會導致執行目標特定JavaScript程式碼時發生問題。

如需詳細資訊，請閱讀 [針對目標內容開發](/help/sites-developing/target.md#understanding-the-target-component) 頁面。

### 瀏覽器主控台中會顯示「AppMeasurement初始化中缺少報表套裝ID」錯誤 {#the-error-missing-report-suite-id-in-appmeasurement-initialization-is-displayed-in-the-browser-console}

使用DTM在網站上實作Adobe Analytics並使用自訂程式碼時，可能會出現此問題。 原因是使用 `s = new AppMeasurement()` 例項化 `s` 物件。

#### 解决方案 {#solution-4}

使用 `s_gi` 而非 `new AppMeasurement` 具現化方法。 例如：

```
var s_account="INSERT-RSID-HERE"
var s=s_gi(s_account)
```

### 預設選件會隨機顯示，而不是正確選件 {#a-default-offer-is-randomly-displayed-instead-of-the-correct-offer}

此問題可能有多個原因：

* 正在載入Target使用者端程式庫( `mbox.js` 或 `at.js`)非同步使用第三方Tag Management系統可能會隨機中斷鎖定目標。 Target程式庫應在頁面標頭中同步載入。 從AEM傳遞程式庫時，一律如此。

* 正在載入兩個Target使用者端資料庫( `at.js`)同時(例如，一個使用DTM，另一個使用AEM中的Target設定)。 這可能會導致 `adobe.target` 定義： `at.js` 版本不同。

#### 解决方案 {#solution-5}

您可以嘗試下列解決方案：

* 確保在中同步執行載入類似DTM程式庫的客戶程式碼（進而載入Target程式庫） [頁首](/help/sites-developing/target.md#enabling-targeting-with-adobe-target-on-your-pages).
* 如果網站設定為使用DTM來傳遞Target程式庫，請確保 **DTM提供的Clientlib** 選項已核取 [Target設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/target-configuring.html) 用於網站。

### 使用AT.js 1.3+時，一律會顯示預設選件，而非正確選件 {#a-default-offer-is-always-displayed-instead-of-correct-offer-when-using-at-js}

現成的AEM 6.2和6.3與AT.js版本1.3.0+不相容。 AT.js版本1.3.0為其API引入引數驗證， `adobe.target.applyOffer()` 需要「mbox」引數，但並未由 `atjs-itegration.js` 程式碼。

#### 解决方案 {#solution-6}

若要解決此問題，請編輯 `atjs-itegration.js` 並新增 `"mbox": mboxName` 引數物件中的欄位 `adobe.target.applyOffer()` 如下所示：

```
adobe.target.getOffer({
    "mbox": mboxName,
    "params": params,
    "success": function (response) {
        adobe.target.applyOffer({
            "mbox": mboxName, //<--- ADDED PARAM
            "selector": "#" + mboxName,
            "offer": response
        })
    },
```

### 「目標與設定」頁面未顯示「報表來源」區段 {#the-goals-settings-page-does-not-show-the-reporting-sources-section}

此問題很可能是 [A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md) 布建問題。

#### 解决方案 {#solution-7}

您必須藉由向AEM發出下列驗證要求，驗證您的Target帳戶是否已正確啟用A4T：

```
http://localhost:4502/etc/cloudservices/testandtarget/<YOUR-CONFIG>/jcr:content.a4t.json

{
    "a4tEnabled": true,
    "sharedsecret": "SECRET",
    "proxyUrl": "/libs/cq/contentinsight/content/proxy.reportingservices.json",
    "active": "true",
    "pageName": "",
    "url": "https://api5.omniture.com/rs/0.5/",
    "username": "USER@DOMAIN"
}
```

如果回應包含行 `a4tEnabled:false`，連結 [Adobe客戶服務](https://helpx.adobe.com/contact.html) 以正確布建您的帳戶。

### 實用的Target API {#helpful-target-apis}

以下是兩個Target API，它們在疑難排解Target問題時可能會很實用：

* 擷取指定clientcode的Target端點

```
https://admin.testandtarget.omniture.com/rest/v1/endpoint/<CLIENTCODE>.json

{"api":"https://admin<N>.testandtarget.omniture.com/admin/rest/v1"}
```

* 擷取使用者端的設定檔

```
https://admin<N>.testandtarget.omniture.com/admin/rest/v1/clients/<CLIENT>?email=<EMAIL>&password=<PASSWORD>

Response for N=4, CLIENT-dayintegrationintern
{
    "clientCode": "dayintegrationintern",
    "companyName": "Day Integration - Internal",
    "omnitureCompanyId": "Day Integration Internal",
    "softTraxId": -1,
    "address1": "XYZ",
    "city": "San Francisco",
    "state": "ca",
    "zip": "94107",
    "country": "UNITED STATES",
    "locale": "de_DE",
    "timeZone": "Europe/Berlin",
    "phone": "XX-XX-XXXX",
    "serviceLevel": "Up to 100,000",
    "privileges": [
        "a4t",
        "hosts",
        "TnT-SC-integration",
        "mvt",
        "steps",
        "testing-campaigns",
        "view-snapshot",
        "on-site-editor",
        "optimizing-campaign",
        "third-party-id-support",
        "landing-page-campaigns",
        "segment",
        "rest-create-user",
        "advanced-targeting",
        "mobile-device-targeting",
        "beta",
        "geolocation"
    ]
}
```
