---
title: 檢視頁面分析資料以評估頁面內容的成效
description: 使用頁面分析資料來評估其頁面內容的成效
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# 檢視頁面分析資料{#seeing-page-analytics-data}

使用頁面分析資料來評估頁面內容的成效。

## 控制檯中的Analytics可見專案 {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

頁面分析資料顯示於 [清單檢視](/help/sites-authoring/basic-handling.md#list-view) Sites主控台的。 當頁面以清單格式顯示時，預設可使用下列欄：

* 页面视图
* 独特访客
* 页面停留时间

每欄會顯示目前報告期間的值，也會指出值自上一個報告期間以來是增加還是減少。 您看到的資料每12小時會更新一次。

>[!NOTE]
>
>若要變更更新週期， [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. 開啟 **網站** 主控台；例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. 在工具列的最右側（右上角），按一下或點選圖示以選取 **清單檢視** (顯示的圖示取決於 [目前檢視](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources))。

1. 再次強調，在工具列的最右側（右上角），按一下或點選圖示，然後選取 **檢視設定**. 此 **設定欄** 對話方塊將會開啟。 進行任何必要的變更，並確認： **更新**.

   ![aa-04](assets/aa-04.png)

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

   ![aa-15](assets/aa-15.png)

1. 選取您要在Sites主控台中向作者公開的量度，然後按一下 **新增**.

   顯示的欄是從Adobe Analytics中擷取。

   ![aa-16](assets/aa-16.png)

### 從Sites開啟內容分析 {#opening-content-insights-from-sites}

開啟 [內容分析](/help/sites-authoring/content-insights.md) 從Sites主控台，以進一步調查頁面有效性。

1. 在Sites主控台中，選取您要檢視其內容深入分析的頁面。
1. 在工具列上，按一下Analytics和Recommendations圖示。

   ![](do-not-localize/chlimage_1-16a.png)

## 頁面編輯器中的Analytics (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>這將會顯示如果 [已設定Activity Map](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) （適用於您的網站）。

>[!NOTE]
>
>Activity Map的資料擷取自Adobe Analytics。

當您的網站已 [已針對Adobe Analytics設定](/help/sites-administering/adobeanalytics-connect.md)，您可以使用 [模式Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 以檢視相關資料。 例如：

![aa-07](assets/aa-07.png)

### 存取Activity Map {#accessing-the-activity-map}

選取 [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) 模式，系統會要求您輸入Adobe Analytics認證。

![aa-03](assets/aa-03.png)

此 **分析** 浮動工具列隨即顯示；您可以：

* 使用雙箭頭(**>>**)
* 切換頁面詳細資料（眼睛圖示）
* 設定Activity Map設定（cog圖示）
* 選取要顯示的分析（各種下拉式選取器）
* 結束Activity Map並關閉工具列(x)

![aa-09](assets/aa-09.png)

### 選取要顯示的Analytics {#selecting-the-analytics-to-show}

您可以使用各種條件來選取要顯示的分析資料及其顯示方式：

* **標準**/**即時**

* 事件型別
* 使用者群組
* **泡泡**/**漸層**/**獲益者和損失者**/**關閉**

* 要顯示的期間

![aa-13](assets/aa-13.png)

### 設定Activity Map {#configuring-the-activity-map}

使用 **顯示設定** 圖示以開啟 **Activity Map設定** 對話方塊。

![aa-04-1](assets/aa-04-1.png)

此 **Activity Map設定** 對話方塊在三個索引標籤上提供一系列選項：

![aa-06](assets/aa-06.png)

* 常规

   * 报表包
   * 页面名称
   * 语言
   * 標籤覆蓋圖表示方式
   * 標簽字型大小
   * 漸層顏色
   * 泡泡顏色
   * 顏色漸層依據
   * 漸層透明度

* 标准

   * 顯示（連結型別和數目）
   * 隱藏未收到點選之連結的覆蓋圖

* 实时版

   * 顯示排名最前的（獲益者或損失者）
   * 排除最後%
   * 自動更新（資料和期間）
