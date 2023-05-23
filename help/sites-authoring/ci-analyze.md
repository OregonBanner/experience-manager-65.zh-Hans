---
title: 分析頁面效能
seo-title: Analyzing Page Performance
description: 您可以使用「內容分析」頁面來分析您編寫之頁面的效能
seo-description: Use the Content Insight page to analyze the performance of the page that you are authoring
uuid: 563d3e98-20d9-4cca-a174-bafd6e65c1bb
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 57cd61d5-78f2-4f8c-99ee-75e100c052ef
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 分析頁面效能{#analyzing-page-performance}

開啟 [內容分析](/help/sites-authoring/content-insights.md) 頁面，分析您正在編寫之頁面的效能。 設定報告期間，以集中進行分析。

## 開啟頁面的Analytics和Recommendations {#opening-analytics-and-recommendations-for-a-page}

請使用下列程式檢視頁面的Analytics和Recommendations：

1. 導覽至您要分析的頁面。
1. 在工具列中按一下或點選 **Analytics和Recommendations**.

   >[!NOTE]
   >
   >頁面的Analytics和Recommendations只有在您已將AEM設定為 [與Adobe Analytics整合](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### 變更報告期間 {#changing-the-reporting-period}

變更Analytics報表的下列時間相關面向：

* 要報告的時間段。
* 資料的詳細程度。

用於變更報表中與時間相關方面的工具會出現在「內容分析」頁面的頂端。 ![chlimage_1-126](assets/chlimage_1-126.png)

#### 變更報告期間 {#changing-the-reporting-period-1}

變更「內容分析」頁面的報告期間，以針對特定期間分析頁面活動。 當您變更報告時段時，報表會自動重新整理。 時間範圍上的陰影區域代表報告期間。 時間範圍上的日期從左到右增加。

![chlimage_1-127](assets/chlimage_1-127.png)

若要變更「內容分析」頁面的報告期間：

1. 如果時間範圍未出現在頁面頂端，請按一下或點選「切換時間範圍」圖示。

   ![](do-not-localize/chlimage_1-22.png)

1. 若要變更報告時段的開始日期，請將陰影區域左側的圓圈拖曳至所需的開始日期。

   如果您看不到著色區域的左側，請使用卷軸將其帶入檢視。

1. 若要變更報告時段的結束日期，請將陰影區域右邊的圓圈拖曳到所需的結束日期。

#### 變更報告時段的詳細程度 {#changing-the-granularity-of-the-reporting-period}

變更報表中每個資料點跨越的時間長度。 例如，選取「週」詳細程度時，「檢視」報表上的每個資料點代表一週的檢視次數。

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

詳細程度會影響根據時間繪製資料的報表，例如「檢視」和「頁面平均參與分鐘數」報表。 詳細程度也會影響時間範圍的比例。

1. 如果未顯示粒度控制項，請按一下或點選「切換粒度」圖示。

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. 按一下或點選所需的精細度。 選取後，報表會自動更新以反映粒度。

### 指派SEO Recommendations的任務 {#assigning-tasks-for-seo-recommendations}

使用SEO Recommendations報表來建立任務，以改善搜尋引擎的頁面可見度。 對於報表中沒有核取記號的每個建議，您可以建立指派給使用者的任務，以執行所需工作。

![chlimage_1-129](assets/chlimage_1-129.png)

SEO建議的狀態會指出工作已建立但尚未完成的時間。

![chlimage_1-130](assets/chlimage_1-130.png)

建立後，任務會出現在使用者的任務清單中。 如需工作的相關資訊，請參閱 [使用任務](/help/sites-authoring/task-content.md).

使用下列程式來建立SEO建議的工作。

1. 按一下或點選SEO建議的資訊圖示。

   ![](do-not-localize/chlimage_1-23.png)

1. 按一下資訊圖示旁邊顯示的環繞三角形圖示。

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. 填寫顯示的表單欄位，然後點選「建立」：

   * 專案：選取要在其中建立任務的專案。
   * 名稱：識別工作的名稱。 預設名稱是SEO建議的標題。
   * 指派給：選取要指派任務的使用者。 開始輸入使用者名稱以篩選清單。
   * 摘要：完成工作所需之活動的摘要。 預設說明是SEO建議隨附的資訊。
   * 工作優先順序：工作的優先順序。
   * 到期日：作業應完成的日期。

   **注意：** 建立的工作也包含SEO建議適用的頁面路徑。

1. 按一下或點選「完成」以關閉「任務已建立」訊息。
