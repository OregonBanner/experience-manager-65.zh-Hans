---
title: 在We.Retail中試用內容片段
seo-title: Trying out Content Fragments in We.Retail
description: 在We.Retail中試用內容片段
seo-description: null
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
exl-id: 1e5d8184-7164-4984-b43e-421015e8bf52
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 21%

---

# 在We.Retail中試用內容片段{#trying-out-content-fragments-in-we-retail}

内容片段允许您创建渠道中性内容，以及各种（特定于渠道的）变量。**We.Retail** (如在AEM的現成可用例項中可用)提供片段 **羅富登北極衝浪** 作為基本範例。 這說明：

* Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变体。

   * 另請參閱 [在We.Retail中何處可以找到內容片段資產](#where-to-find-content-fragments-in-we-retail)

* 然後，您可以 [在製作時使用這些片段及其變數](/help/sites-authoring/content-fragments.md) 您的內容頁面。

   * 另請參閱 [在We.Retail中使用內容片段的位置](#where-content-fragments-are-used-in-we-retail)

如需建立、管理、使用及開發內容片段的完整檔案：

* 另請參閱 [進一步資訊](#further-information)

>[!NOTE]
>
>**内容片段**&#x200B;和&#x200B;**[体验片段](/help/sites-authoring/experience-fragments.md)**&#x200B;是 AEM 中的两个不同功能：
>
>* **内容片段**&#x200B;是可编辑内容，主要为文本和相关图像。它們是純內容，沒有設計和版面。
>* **体验片段**&#x200B;是经过充分布局的内容；例如，网页的一个片段。
>
>体验片段可以包含内容片段形式的内容，反之则不行。

## 在We.Retail中尋找內容片段的位置 {#where-to-find-content-fragments-in-we-retail}

We.Retail中有數個範例內容片段；導覽至 **資產**， **檔案**， **We.Retail**， **英文**， **體驗**.

其中包括 **羅富登北極衝浪**，片段及相關視覺資產：

* 導覽： **資產**， **檔案**， **We.Retail**， **英文**， **體驗**， **洛富登荒蕪衝浪**：

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

您可以選取並編輯 **羅富登北極衝浪** 片段：

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

您可以 [編輯和管理](/help/assets/content-fragments/content-fragments.md) 使用標籤（左側面板）的片段：

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[變數](/help/assets/content-fragments/content-fragments-variations.md)** 包括 [Markdown](/help/assets/content-fragments/content-fragments-markdown.md)
* **[关联的内容](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[元数据](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## 在We.Retail中使用內容片段的位置 {#where-content-fragments-are-used-in-we-retail}

說明 [使用內容片段編寫頁面](/help/sites-authoring/content-fragments.md) 底下提供了幾個範例頁面，例如：

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

例如， **羅富登北極衝浪** 已參考Sites頁面中的內容片段：

* 導覽： **網站**， **We.Retail**， **語言主版**， **英文**， **體驗**. 然後開啟 **羅富登北極衝浪** 進行編輯：

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## 更多信息 {#further-information}

如需詳細資訊，請參閱：

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * 瞭解如何建立、編輯及管理您的內容片段資產。

* [使用內容片段編寫頁面](/help/sites-authoring/content-fragments.md)

   * 編寫頁面時使用您的內容片段。

* [開發AEM — 內容片段的元件](/help/sites-developing/components-content-fragments.md)

   * 內容片段元件的概觀。

* [開發和擴充內容片段](/help/sites-developing/customizing-content-fragments.md)

   * 協助您開發及擴充內容片段的資訊。
