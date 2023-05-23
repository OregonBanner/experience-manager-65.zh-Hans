---
title: 連線到Adobe Analytics和建立框架
seo-title: Connecting to Adobe Analytics and Creating Frameworks
description: 瞭解如何將AEM連線至SiteCatalyst和建立架構。
seo-description: Learn about connecting AEM to SiteCatalyst and creating frameworks.
uuid: 3820dd24-4193-42ea-aef2-4669ebfeaa9d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6b545a51-3677-4ea1-ac7e-2d01ba19283e
docset: aem65
exl-id: 8262bbf9-a982-479b-a2b5-f8782dd4182d
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 6%

---

# 連線到Adobe Analytics和建立框架 {#connecting-to-adobe-analytics-and-creating-frameworks}

若要從Adobe Analytics中的AEM頁面追蹤網頁資料，請建立Adobe Analytics Cloud Services設定和Adobe Analytics架構：

* **Adobe Analytics設定：** 有關您的Adobe Analytics帳戶的資訊。 Adobe Analytics設定可讓AEM連線至Adobe Analytics。 為您使用的每個帳戶建立Adobe Analytics設定。
* **Adobe Analytics架構：** Adobe Analytics報表套裝屬性和CQ變數之間的一組對應。 使用架構來設定網站資料如何填入Adobe Analytics報表。 架構與Adobe Analytics設定相關聯。 您可以為每個設定建立多個架構。

將網頁與框架建立關聯時，框架會對該頁面以及該頁面的子系執行追蹤。 然後可以從Adobe Analytics擷取頁面檢視，並顯示在Sites主控台中。

## 前提条件 {#prerequisites}

### Adobe Analytics帳戶 {#adobe-analytics-account}

若要在Adobe Analytics中追蹤AEM資料，您必須具備有效的Adobe Experience Cloud Adobe Analytics帳戶。

Adobe Analytics帳戶必須：

* 具有 **管理員** 許可權
* 指派給 **Web服務存取** 使用者群組。

>[!CAUTION]
>
>提供 **管理員** 許可權(在Adobe Analytics內)不足以讓使用者從AEM連線至Adobe Analytics。 帳戶還必須具有 **Web服務存取** 許可權。

![chlimage_1-67](assets/chlimage_1-67.png)

繼續之前，請確定您的憑證可讓您登入Adobe Analytics。 藉由下列其中一種方式：

* [Adobe Experience Cloud登入](https://experience.adobe.com/#/@login/home)

* [Adobe Analytics登入](https://sc.omniture.com/login/)

### 設定AEM以使用您的Adobe Analytics資料中心 {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Adobe Analytics [資料中心](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html?lang=en) 收集、處理和儲存與您的Adobe Analytics報表套裝相關聯的資料。 設定AEM以使用託管Adobe Analytics報表套裝的資料中心。 您的合約中提到了資料中心。 如需此資訊，請聯絡貴組織的管理員。

如有必要，請使用下列專案來路由至正確的資料中心： `https://api.omniture.com/`.

如果您的組織需要從特定資料中心收集或擷取資料，請使用下列專案：

| 数据中心 | URL |
|---|---|
| 伦敦 | `https://api3.omniture.com/` |
| 新加坡 | `https://api4.omniture.com/` |
| 俄勒冈州 | `https://api5.omniture.com/` |

使用 [設定OSGi套件組合的Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **AdobeAEM Analytics HTTP使用者端**. 新增 **資料中心URL** 適用於託管報表套裝(您的AEM頁面會收集該套裝的資料)的資料中心。

![aa-07](assets/aa-07.png)

1. 在網頁瀏覽器中開啟Web主控台。 ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. 若要存取主控台，請輸入您的認證。

   >[!NOTE]
   >
   >若要瞭解您是否有此主控台的存取權，請連絡您的網站管理員。

1. 選取名為的組態專案 **AdobeAEM Analytics HTTP使用者端**.
1. 若要新增資料中心的URL，請按資料中心旁的+按鈕。 **資料中心URL** 清單，並在方塊中輸入URL。

1. 若要從清單中移除URL，請按一下URL旁邊的 — 按鈕。
1. 单击“保存”。

## 設定與Adobe Analytics的連線 {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>此 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。

## 為Activity Map設定 {#configuring-for-the-activity-map}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>此 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。

## 建立Adobe Analytics架構 {#creating-a-adobe-analytics-framework}

對於您正在使用的報表套裝ID (RSID)，您可以控制哪些伺服器執行個體（製作、發佈或兩者）會將資料貢獻至報表套裝：

* **全部**：來自作者和發佈執行個體的資訊會填入報表套裝。
* **作者**：只有來自作者執行個體的資訊會填入報表套裝。
* **發佈**：只有發佈執行個體的資訊會填入報表套裝。

>[!NOTE]
>
>選取伺服器執行個體的型別不會限制對Adobe Analytics的呼叫，它只會控制哪些呼叫包含RSID。
>
>例如，某個框架設定為使用 *diiweretail* 報表套裝和作者是選取的伺服器執行個體。 當頁面與框架一起發佈時，仍會對Adobe Analytics發出呼叫，但這些呼叫不包含RSID。 只有來自作者執行個體的呼叫包含RSID。

1. 使用 **導覽**，選取 **工具**， **Cloud Services**，則 **舊版Cloud Services**.
1. 捲動至 **Adobe Analytics** 並選取 **顯示設定**.
1. 按一下 **[+]** Adobe Analytics設定旁的連結。

1. 在 **建立框架** 對話方塊：

   * 指定&#x200B;**标题**。
   * 您可選擇指定 **名稱**，適用於將架構詳細資料儲存在存放庫中的節點。
   * 選取 **Adobe Analytics框架**

   然後按一下 **建立**.

   框架隨即開啟以進行編輯。

1. 在 **報表套裝** 側Pod的區段（主面板的右側），按一下 **新增專案**. 然後使用下拉式清單來選取報表套裝ID (例如 `geometrixxauth`)進行互動。

   >[!NOTE]
   >
   >當您選取報表套裝ID時，左側的「內容尋找器」會填入Adobe Analytics變數(SiteCatalyst變數)。

1. 若要選取您要傳送資訊至報表套裝的伺服器執行個體，請使用 **執行模式** 下拉式清單（位於報表套裝ID旁）。

   ![aa-framework-01](assets/aa-framework-01.png)

1. 若要讓架構可用於網站的發佈執行個體，請前往 **頁面** 索引標籤，按一下 **啟動框架。**

### 正在設定Adobe Analytics的伺服器設定 {#configuring-server-settings-for-adobe-analytics}

框架系統可讓您變更每個Adobe Analytics框架中的伺服器設定。

>[!CAUTION]
>
>這些設定會決定傳送資料的位置和方式，因此您必須執行下列動作 *請勿竄改這些設定* 並讓Adobe Analytics代表自行設定。

從開啟面板開始。 按下旁邊的向下箭頭 **伺服器**：

![server_001](assets/server_001.png)

* **跟踪服务器**

   * 包含用來傳送Adobe Analytics呼叫的URL

      * `cname`  — 預設為Adobe Analytics帳戶的 *公司名稱*
      * `d1`  — 對應至傳送資訊的資料中心（以下任一項之一） `d1`， `d2`，或 `d3`)
      * `sc.omtrdc.net`  — 網域名稱

* **安全跟踪服务器**

   * 具有與追蹤伺服器相同的區段
   * 用於從安全頁面傳送資料(`https://`)

* **访客命名空间**

   * 名稱空間會決定追蹤URL的第一部分。
   * 例如，將名稱空間變更為 **CNAME** 導致向Adobe Analytics發出的呼叫看起來像 **CNAME.d1.omtrdc.net** 而不是預設值。

## 將頁面與Adobe Analytics架構建立關聯 {#associating-a-page-with-a-adobe-analytics-framework}

當頁面與Adobe Analytics框架相關聯時，頁面會在載入時傳送資料至Adobe Analytics。 頁面填入的變數會從框架中的Adobe Analytics變數對應及擷取。 例如，頁面檢視是從Adobe Analytics中擷取。

頁面的下階會繼承與架構的關聯。 例如，將網站的根頁面與框架建立關聯時，網站的所有頁面都會與框架建立關聯。

1. 從 **網站** 主控台，選取您要設定追蹤的頁面。
1. 開啟 **[頁面屬性](/help/sites-authoring/editing-page-properties.md)**，直接來自主控台或頁面編輯器。
1. 開啟**Cloud Services**標籤。

1. 使用 **新增設定** 下拉式清單以選取 **Adobe Analytics** 從可用選項中選取。 如果已設定繼承，請在選取器可供使用之前停用繼承。

1. 的下拉式選取器 **Adobe Analytics** 會附加至可用的選項。 選取所需的架構設定。

1. 選取 **儲存並關閉**.
1. 若要啟動頁面及任何連線的組態/檔案， **[發佈](/help/sites-authoring/publishing-pages.md)** 頁面。
1. 最後一個步驟是造訪發佈執行個體上的頁面，並使用搜尋關鍵字（例如eggplant） **搜尋** 元件。
1. 您可以使用適當的工具來檢查對Adobe Analytics發出的呼叫；例如， [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. 根據提供的範例，呼叫應包含在eVar7中輸入的值（即eggplant），而事件清單應包含event3。

### 页面视图 {#page-views}

當頁面與Adobe Analytics架構相關聯時，頁面檢視次數會顯示在Sites主控台的「清單」檢視中。

另請參閱 [檢視頁面分析資料](/help/sites-authoring/page-analytics-using.md) 以取得更多詳細資料。

### 設定匯入間隔 {#configuring-the-import-interval}

設定適當的執行個體 **AdobeAEM Managed Polling設定** 服務：

* **輪詢間隔**：服務從Adobe Analytics擷取頁面檢視資料的間隔，以秒為單位。
預設間隔為43200000毫秒（12小時）。

* **啟用**：啟用或停用服務。 依預設，服務已啟用。

若要設定此OSGi服務，您可以使用 [網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存放庫中的osgiConfig節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (服務PID為 `com.day.cq.polling.importer.impl.ManagedPollConfigImpl`)。

## 編輯Adobe Analytics設定和/或架構 {#editing-adobe-analytics-configurations-and-or-frameworks}

建立Adobe Analytics設定或框架時，請導覽至（舊版） **Cloud Services** 畫面。 選取 **顯示設定**，然後按一下您要更新之特定設定的連結。

編輯Adobe Analytics設定時，按下 **編輯** 在設定頁面上時，開啟 **編輯元件** 對話方塊。

## 刪除Adobe Analytics框架 {#deleting-adobe-analytics-frameworks}

若要刪除Adobe Analytics架構，請先 [開啟以進行編輯](#editing-adobe-analytics-configurations-and-or-frameworks).

然後選取 **刪除框架** 從 **頁面** 索引標籤。
