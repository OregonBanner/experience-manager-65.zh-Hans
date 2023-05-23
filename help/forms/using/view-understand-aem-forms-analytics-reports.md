---
title: 檢視和瞭解AEM Forms analytics報表
seo-title: View and understand AEM Forms analytics reports
description: AEM Forms會與Adobe Analytics整合，並為您提供有關已發佈的最適化表單的摘要和詳細分析。
seo-description: AEM Forms integrates with Adobe Analytics and provides you summary and detailed analytics about your published adaptive forms.
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 2%

---

# 檢視和瞭解AEM Forms analytics報表 {#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms與Adobe Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的績效量度。 分析这些指标的目的在于，根据有关使表单或文档更有用所需的更改的数据做出明智的决策。

## 設定分析 {#setting-up-analytics}

AEM Forms中的分析功能屬於AEM Forms附加元件套件的一部分。 如需有關安裝附加元件套件的資訊，請參閱 [安裝和設定AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

除了附加元件套件之外，您還需要Adobe Analytics帳戶。 如需解決方案的相關資訊，請參閱 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

取得AEM Forms附加元件套件和Adobe Analytics帳戶後，請將Adobe Analytics帳戶與AEM Forms整合，並對您的表單或檔案啟用追蹤，如中所述 [設定分析和報表](../../forms/using/configure-analytics-forms-documents.md).

### 如何記錄使用者互動資訊 {#how-user-interaction-information-is-recorded}

當使用者與表單互動時，將會記錄互動並傳送至Analytics伺服器。 下列清單指示各種使用者活動的伺服器呼叫：

* 每次造訪每個欄位2次呼叫
* 1代表面板造訪
* 1表示儲存
* 2用於提交
* 儲存2
* 1以取得說明
* 每個驗證錯誤為1
* 1代表表單轉譯+ 1代表預設面板造訪+ 1代表預設第1個欄位造訪
* 2表示表單放棄

>[!NOTE]
>
>此清單並非詳盡無遺。

### 檢視Analytics報表 {#summary-report}

執行以下步驟來檢視Analytics報表：

1. 登入AEM入口網站： `https://[hostname]:'port'`
1. 按一下 **Forms > Forms與檔案**.
1. 選取您要檢視其分析報表的表單。
1. 選取 **更多> Analytics報表**.

![分析報告](assets/analyticsreport.png)

**答：** Analytics報表命令

AEM Forms會顯示表單的analytics報表，以及表單中每個面板的報表，如下所示。

![最適化表單的摘要報表](assets/analyticsdashboard_callout.png)

**答：** 轉換 **B.** 表單層級摘要 **C.** 面板層級摘要 **D.** 訪客瀏覽器 — 篩選器 **E.** 訪客的作業系統 — 篩選器 **F.** 訪客語言 — 篩選器

依預設，會顯示過去七天的分析報表。 您可以檢視過去15天、一個月等的報告，或指定日期範圍。

>[!NOTE]
>
>「最近7天」和「最近15天」等選項不包含您產生分析報表的當天資料。 若要包含當天的資料，您必須指定包含當天的日期範圍，然後執行報表。

![date-range](assets/date-range.png)

### 最適化和HTML5表單的轉換圖 {#conversions-graph-for-adaptive-and-html-forms}

表單層級轉換圖表可讓您深入瞭解表單在下列關鍵績效指標(KPI)上的執行情形：

* **轉譯**：表單開啟的次數
* **訪客**：表單的訪客數量
* **提交內容**：提交表單的次數

![轉換圖](assets/conversion-graph.png)

### 最適化和HTML5表單的Analytics報表 {#analytics-report-for-adaptive-and-html-forms}

表單層級摘要區段可讓您深入瞭解表單在下列關鍵績效指標(KPI)上的執行情形：

* **平均填滿時間**：填寫表單所花的平均時間。 當使用者在表單上花費時間但未提交時，該時間未包含在此計算中。
* **轉譯**：表單已轉譯或開啟的次數
* **草稿**：表單儲存為草稿的次數
* **提交內容**：表單提交次數
* **中止**：使用者開始填寫表單然後離開而未完成表單的次數
* **不重複訪客**：表單由不重複訪客轉譯的次數。 如需不重複訪客的詳細資訊，請參閱 [不重複訪客、造訪和客戶行為](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html).

![展開的表單層級摘要分析報表](assets/analytics-report.png)

### 面板報告 {#bottom-summary-report}

面板層級摘要區段提供有關表單中每個面板的下列資訊：

* **平均填滿時間**：面板平均逗留時間，無論表單是否提交
* **已遇到錯誤**：使用者在面板中的欄位上遇到的平均錯誤數。 遇到的錯誤是以欄位中的錯誤總數除以表單轉譯數得出。
* **已存取說明**：使用者存取面板中欄位內容說明的平均次數。 「已存取說明」的取得方式是將欄位的「已存取說明」總次數除以表單轉譯次數。

#### 詳細面板報告 {#detailed-panel-report}

您也可以按一下「面板報告」中面板的名稱，以檢視每個面板的詳細資訊。

![詳細面板報告](assets/panel-report-detailed.png)

詳細報告會顯示面板中所有欄位的值。

面板報告有三個索引標籤：

* **時間報表**（預設）：顯示填入面板中每個欄位所花費的時間（以秒為單位）
* **錯誤報告**：顯示使用者在填寫欄位時遇到的錯誤數量
* **說明報告**：存取特定欄位的說明次數

如果有多個面板可用，您可以在面板之間導覽。

### 篩選器：瀏覽器、作業系統和語言 {#filters-browser-os-and-language}

「瀏覽器分送」、「OS分送」和「語言分送」表格會依表單使用者的瀏覽器、作業系統和語言來顯示轉譯、訪客和提交專案。 預設情況下，這些表格最多會顯示五個專案。 您可以按一下「顯示更多」來顯示更多專案，並按一下「顯示更少」來返回一般五個或更少專案。

若要進一步篩選分析資料，您可以按一下任何表格中的專案。 例如，如果您按一下「瀏覽器分送」表格中的「Google Chrome」，報表會再次轉譯為包含與Google Chrome瀏覽器相關的資料，如下所示：

![套用至Analytics報表的篩選器 — Google Chrome ](assets/filter-1.png)

如果您在套用篩選條件後檢視面板報表，面板報表資料也會根據套用的篩選條件顯示。

套用篩選器後：

* 發佈表格會變成唯讀，因為一次只能套用一個篩選器。
* 套用的篩選器表格會消失。
* 您可以按一下「關閉」按鈕（在下方反白顯示）以移除套用的篩選器。

![關閉按鈕以移除套用的篩選器](assets/close-filter.png)

### A/B測試 {#a-b-testing}

如果您已啟用並設定表單的A/B測試，報表頁面會有一個下拉式清單，可用來顯示A/B測試報表。 A/B測試報告會在您設定後，顯示兩個版本表單的比較效能。

如需A/B測試的詳細資訊，請參閱 [建立和管理最適化表單的A/B測試](../../forms/using/ab-testing-adaptive-forms.md).
