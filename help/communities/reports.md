---
title: 報表主控台
seo-title: Reports Console
description: 瞭解如何存取報告
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# 報表主控台 {#reports-console}

## 概述 {#overview}

對於AEM Communities，有多種報表可從作者環境以數種方式存取。

一般而言，各種報表包括：

* [查看次数报表](#views-report)

   提供社群成員和網站訪客檢視任何社群網站內容的圖表。

* [发布报表](#posts-report)

   提供社群成員在任何社群網站的各種型別貼文的圖表。

表格報表可匯出為.csv格式，以供後續處理。

## 報告主控台 {#reporting-consoles}

### 社群網站報表 {#reports-for-community-sites}

* 從全域導覽： **[!UICONTROL 導覽]** > **[!UICONTROL Communities]** >  **[!UICONTROL 報表]**

* 選擇自：

   * **[!UICONTROL 指定报表]**

      * 為選取的社群網站、使用者或群組以及指派專案產生報告。
   * **[!UICONTROL 发布报表]**

      * 為選取的社群網站、內容型別和時段產生報表。
   * **[!UICONTROL 查看次数报表]**

      * 針對選取的社群網站、內容型別和時段產生報表。



![報告](assets/reports1.png)

## 查看次数报表 {#views-report}

「檢視」主控台可讓社群功能在指定時段內針對頁面檢視產生報表。

![檢視報告](assets/view-report.png)

選取報告的條件：

* **[!UICONTROL 站点]**

   選取社群網站。

* **[!UICONTROL 内容类型]**

   可以選擇「所有內容」或選取網站上提供的其中一項功能。

* **[!UICONTROL 時間範圍]**

   選取下列其中一項：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

選取 **[!UICONTROL 產生]** 以建立報表。

![generate-view](assets/generate-views.png)

## 发布报表 {#posts-report}

「貼文」主控台可讓您針對指定時段內社群功能的貼文數量產生報表。

![posts-report](assets/posts-report.png)

選取報告的條件：

* **[!UICONTROL 站点]**

   選取社群網站。

* **[!UICONTROL 内容类型]**

   可以選擇「所有內容」或選取網站上提供的其中一項功能。

* **[!UICONTROL 時間範圍]**

   選取下列其中一項：

   * 过去 7 天
   * 过去 30 天
   * 过去 90 天
   * 去年

選取 **[!UICONTROL 產生]** 以建立報表。

![generate-report](assets/generate-posts-report.png)

## 疑难解答 {#troubleshooting}

### 未列出任何社群網站 {#no-community-sites-listed}

如果未列出任何社群網站，請確認已為網站啟用Adobe Analytics。 如果選擇工作分派的報告，請確保工作分派功能在社群網站的結構中。

### 報告未顯示在AEM作者執行個體中 {#reports-do-not-show-in-aem-author-instance}

如果報表未顯示在AEM編寫執行個體中，請檢查是否有自訂，例如發佈執行個體上的URL對應。 如果URL對應僅在Communities網站的AEM Publish執行個體上完成，請確定已在AEM Author執行個體中設定相同的 **網站趨勢報表社交元件工廠** 設定。

![AEM作者上的URL對應](assets/sitetrend.png)
