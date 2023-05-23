---
title: 内容分析
seo-title: Content Insight
description: 內容深入分析會使用網頁分析和SEO建議來提供頁面效能的相關資訊
seo-description: Content Insight provides information about page performance using web analytics and SEO recommendation
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 内容分析{#content-insight}

「內容分析」會使用網頁分析和SEO建議來提供頁面效能的相關資訊。 使用「內容分析」來決定如何修改頁面，或瞭解先前的變更如何改變效能。 對於您編寫的每個頁面，您可以開啟「內容分析」來分析頁面。

![chlimage_1-311](assets/chlimage_1-311.png)

「內容分析」頁面的版面會隨著您使用之裝置的熒幕維度和方向而改變。

## 報表資料

「內容分析」頁面包含使用Adobe SiteCatalyst、Adobe Target、Adobe Social和BrightEdge資料的報表：

* SiteCatalyst：提供下列量度的報表：

   * 頁面檢視
   * 頁面平均逗留時間
   * 源

* Target：您的頁面包含選件的促銷活動報表。
* BrightEdge：報告可改善搜尋引擎對頁面可見度的頁面功能，並建議應實作的功能。

另請參閱 [開啟頁面的Analytics和Recommendations](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## 報告期間

報表會顯示您所控制的一段時間的資料。 當您調整報告時段時，報表會自動重新整理該時段的資料。 視覺提示會指出頁面版本變更的時間，讓您能夠比較每個版本的效能。

您也可以指定報告資料的詳細程度，例如，您可以檢視每日、每週、每月或每年的資料。

另請參閱 [變更報告期間](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>內容深入分析報表要求您的管理員已將AEM與SiteCatalyst、Target和BrightEdge整合。 另請參閱 [與SightCatalyst整合](/help/sites-administering/adobeanalytics.md)， [與Adobe Target整合](/help/sites-administering/target.md)、和 [與BrightEdge整合](/help/sites-administering/brightedge.md).

## 檢視報告 {#the-views-report}

「檢視」報表包含下列評估頁面流量的功能：

* 報告期間頁面檢視的總數。
* 報告期間檢視次數的圖表：

   * 檢視總數。
   * 不重複訪客。

![chlimage_1-312](assets/chlimage_1-312.png)

## 頁面平均參與報表 {#the-page-average-engaged-report}

「頁面平均參與」報表包含下列功能，可用來評估頁面成效：

* 整個報告期間保持頁面開啟的平均時間。
* 整個報告期間頁面檢視的平均長度圖表。

![chlimage_1-313](assets/chlimage_1-313.png)

## 來源報表 {#the-sources-report}

「來源」報表指出使用者如何導覽至頁面，例如從搜尋引擎結果或使用已知URL。

![chlimage_1-314](assets/chlimage_1-314.png)

## 彈回報表 {#the-bounces-report}

「跳出數」報表包含圖形，顯示所選報告期間某個頁面發生的跳出數。

![chlimage_1-315](assets/chlimage_1-315.png)

## 行銷活動報表 {#the-campaign-activity-report}

對於頁面有效的每個行銷活動，都會顯示一個報表，並命名為 *行銷活動名稱* 活動。 報表會顯示提供選件的每個區段的頁面曝光次數和轉換次數。

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO Recommendations報表 {#the-seo-recommendations-report}

SEO Recommendations報表包含頁面BrightEdge分析的結果。 該報告是頁面功能的檢查清單，指出頁面包含和不包含哪些功能，以使用搜尋引擎最大化發現能力。

報表可讓您建立任務，以便進行改善以改善頁面可發現性。 Recommendations會指出已建立實施建議的工作。 另請參閱 [指派SEO Recommendations的任務](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
