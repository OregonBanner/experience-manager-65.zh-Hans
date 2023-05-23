---
title: 檢視頁面分析資料以評估頁面內容的有效性
seo-title: Seeing Page Analytics Data
description: 使用頁面分析資料來評估其頁面內容的成效
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 11%

---

# 檢視頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的成效。

## 控制檯中的Analytics可見專案 {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

頁面分析資料顯示於 [清單檢視](/help/sites-authoring/basic-handling.md#list-view) Sites主控台的。 當頁面以清單格式顯示時，預設可使用下列欄：

* 页面视图
* 独特访客
* 页面停留时间

每欄會顯示目前報告期間的值，也會指出值自上一個報告期間以來是增加還是減少。 您看到的資料每12小時會更新一次。

>[!NOTE]
>
>若要變更更新週期， [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 開啟 **網站** 主控台；例如 [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下或點選圖示以選取 **清單檢視** (顯示的圖示取決於 [目前檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 再次強調，在工具列的最右側（右上角），按一下或點選圖示，然後選取 **檢視設定**. 此 **設定欄** 對話方塊將會開啟。 進行任何必要的變更，並確認： **更新**.

   ![spad-02](assets/spad-02.png)

### 選取報告期間 {#selecting-the-reporting-period}

選取Analytics資料出現在Sites主控台上的報告期間：

* 过去 30 天的数据
* 过去 90 天的数据
* 本年度的数据

目前的報告期間會顯示在Sites控制檯的工具列上（在頂端工具列的右側）。 使用下拉式清單來選取所需的報告期間。

![aa-05](assets/aa-05.png)

### 設定可用的資料欄 {#configuring-available-data-columns}

analytics-administrators使用者群組的成員可以設定Sites主控台，讓作者檢視額外的Analytics欄。

>[!NOTE]
>
>當頁面的樹狀結構包含與不同Adobe Analytics雲端設定相關聯的子項時，您無法設定頁面的可用資料欄。

1. 在清單檢視中，使用檢視選取器（工具列右側），選取 **檢視設定** 然後 **新增自訂Analytics資料**.

   ![spad-03](assets/spad-03.png)

1. 選取您要在Sites主控台中向作者公開的量度，然後按一下 **新增**.

   顯示的欄是從Adobe Analytics中擷取。

   ![aa-16](assets/aa-16.png)

### 從Sites開啟內容分析 {#opening-content-insights-from-sites}

開啟 [內容分析](/help/sites-authoring/content-insights.md) 從Sites主控台，以進一步調查頁面有效性。

1. 在Sites主控台中，選取您要檢視其內容深入分析的頁面。
1. 在工具列上，按一下Analytics和Recommendations圖示。

   ![](do-not-localize/chlimage_1-14.png)

## 頁面編輯器中的Analytics (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>由于 Adobe Analytics API 中的安全性更改，无法再使用 AEM 中包含的 Activity Map 版本。
>
>此 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) 現在應該使用。
