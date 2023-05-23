---
title: 程式報表中的臨時查詢
seo-title: Ad-hoc Queries in Process Reporting
description: 建立自訂查詢，以搜尋Process Reporting中JEE流程的AEM Forms和任務詳細資訊
seo-description: Create custom queries to search for AEM Forms on JEE  process and task details in Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# 程式報表中的臨時查詢{#ad-hoc-queries-in-process-reporting}

## 程式報告中的臨時查詢 {#ad-hoc-queries-in-process-reporting-1}

程式報告中的臨時查詢可讓您建立自訂查詢，以便用於搜尋在您的AEM Forms環境中定義的AEM Forms程式執行個體的程式和任務詳細資訊。

此外，可以使用流程和任務屬性篩選器來定義臨時查詢。 然後可以儲存這些篩選器，並用於稍後執行報表。

[**程式搜尋**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)：使用使用者定義的搜尋篩選器，根據流程屬性來搜尋流程例項。

[**程式詳細資料**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)：指定程式ID以檢視程式執行個體的詳細資訊。

**任務搜尋**：使用使用者定義的搜尋篩選器，根據任務屬性來搜尋任務執行個體。

**任務詳細資訊**：指定任務ID以檢視任務執行個體的詳細資訊。

### 流程和任務 {#processes-and-tasks}

建立篩選和執行查詢流程詳細資訊的步驟與工作相同。

這表示「程式搜尋」和「工作搜尋」的使用者介面僅在您可搜尋的欄位和搜尋結果中傳回的欄位中有所不同。 這只是因為，雖然許多欄位相同，但某些欄位是流程專屬的，而某些欄位是任務專屬的。

本文詳細說明「程式/任務搜尋」和「程式/任務詳細資訊」章節的說明。 在適當的位置，會特別指出任何特定的差異。

## 程式/任務搜尋 {#process-task-search}

您可以使用「程式/任務搜尋」來定義查詢程式/任務執行個體的篩選器。

### 若要建立處理/作業搜尋查詢 {#to-create-a-process-task-search-query}

1. 若要檢視已儲存的「處理/任務搜尋」查詢或建立查詢，請按一下 **臨機查詢** 然後按一下 **程式/任務搜尋**.

   ![search_nodes](assets/search_nodes.png)

   此 **我的篩選器** 面板會顯示在樹狀檢視的右側。

   在 **我的篩選器** 面板中，您可以建立新的臨時查詢，然後按一下以執行先前儲存的查詢。

   ![my_filters_panel](assets/my_filters_panel.png)

1. 若要執行現有查詢，只需按一下 **我的篩選器** 面板。
1. 若要建立查詢，請按一下 **新增** (+)。

   此 **建立篩選器** 面板顯示。

   ![create_filter_panel](assets/create_filter_panel.png)

   查詢包含一或多個查詢篩選器。 若要建立篩選器，請新增篩選器列至查詢。 依預設，會新增一個篩選器列至查詢。

   **定義篩選器的方式**

   1. 選取欄位。

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >欄位清單包含AEM Forms程式/任務的特定欄位。

   1. 選取條件。

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >列出的條件取決於選取進行篩選的屬性。

   1. 輸入值。

      ![filter_值](assets/filter_value.png)

   1. 若要新增其他篩選器至查詢，請按一下 **新增(+)** 篩選列的右側。

      若要從查詢中移除篩選器，請按一下 **刪除(-)** 篩選列的右側。

      ![filter_add_del](assets/filter_add_del.png)

建立查詢後，請使用 **建立篩選器** 面板至：

* **取消**：取消變更並返回 **我的篩選器** 面板。
* **執行**：執行目前的查詢以檢視和/或驗證結果。 在這種情況下，您不需要在執行查詢之前儲存查詢。 您可以驗證結果、進行必要的變更，然後在您滿意輸出時儲存查詢。
* **儲存**：儲存篩選。 然後，您便可以從以下位置檢視及執行篩選器： **我的篩選器** 面板。

### 「我的篩選器」面板中的選項 {#options-in-my-filters-panel}

使用中的選項 **我的篩選器** 面板至 **新增** ![lc_pr_add_filter](assets/lc_pr_add_filter.png)， **編輯** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)，或 **刪除** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)臨時查詢。

![my_filters_options](assets/my_filters_options.png)

### 執行搜尋查詢 {#to-execute-a-search-query}

1. 若要執行查詢，請按一下 **我的篩選器** 面板或按一下 **執行** 按鈕。
1. 查詢結果會顯示在 **報告** 的面板 **程式報告** 視窗。

   ![process_search_result](assets/process_search_result.png)

   您可以在報表底部顯示的分頁面板的協助下，將搜尋結果分頁。

   ![process_result_pgn](assets/process_result_pgn.png)

   在 **顯示** 從下拉式清單中，選擇每頁顯示的結果數目。

   在 **頁面** 文字方塊中，輸入頁碼以直接前往該頁面。

1. 「程式搜尋」結果中會顯示下列欄位：

   * **程式ID**：程式的ID。 欄位會建立超連結。 如果您按一下此欄位中的程式ID，則會將您重新導向至 **[!UICONTROL 程式詳細資料]** 程式面板。
   * **發起人**：啟動程式例項的AEM Forms使用者
   * **建立時間**：程式執行個體開始的日期和時間
   * **完成時間**：程式執行個體完成的日期和時間
   * **持續時間**：流程例項從開始到完成的持續時間
   * **狀態**：程式執行個體的目前狀態。

   依預設，結果會依程式ID排序。 不過，若要依任何欄位排序結果，請按一下欄位標題。

   由於排序是切換作業，按一下欄標題可將結果遞增排序，再按一下欄標題可將結果遞減排序。

   同樣地，「任務搜尋」結果中會顯示下列欄位：

   * **任務ID**：任務的ID。 欄位會建立超連結。 如果您按一下此欄位中的任務ID，則會將您重新導向至 **[!UICONTROL 任務詳細資訊]** 任務面板。
   * **發起人**：啟動程式例項的AEM Forms使用者
   * **建立時間**：程式執行個體開始的日期和時間
   * **完成時間**：程式執行個體完成的日期和時間
   * **持續時間**：流程例項從開始到完成的持續時間
   * **狀態**：程式執行個體的目前狀態。

   依預設，結果會依任務ID排序。 不過，若要依任何欄位排序結果，請按一下欄位標題。 結果會依欄排序，欄標題旁的深色箭頭會指出該欄。

   由於排序是切換操作，按一下欄位標題可將結果遞增排序，再按一下它可遞減排序。 目前的排序順序（升序/降序）是由欄標題旁的變暗箭頭方向所指示。

   ![task_search_result](assets/task_search_result.png)

1. 按一下邊欄按鈕 ![lc_pr_rail_button](assets/lc_pr_rail_button.png) 左上角以摺疊 **我的篩選器** 窗格並展開 **報告** 面板。
1. 使用**報表**面板右上角的選項，對查詢結果執行操作。

   * **重新整理**：以存放區中的最新資料重新整理報表

   * **匯出至CSV**：將報表資料匯出至逗號分隔的檔案。
   >[!NOTE]
   >
   >匯出報表時，搜尋的整個結果會匯出為CSV檔案，而不只是目前的頁面

## 程式/任務詳細資訊 {#process-task-details}

您使用 **程式詳細資料** 面板，以檢視特定程式的詳細資訊。

同樣地，您使用 **任務詳細資訊** 面板以檢視特定任務的詳細資訊。

### 若要檢視處理/作業詳細資訊 {#to-view-process-task-details}

您可以檢視特定AEM Forms程式/任務的詳細資訊：

* **從程式/任務搜尋結果**
* **在「程式/任務詳細資訊」面板中輸入程式/任務ID**

#### 從程式/任務搜尋結果 {#from-a-process-task-search-result}

1. 執行程式/工作搜尋。 如需詳細資訊，請參閱 [執行程式搜尋查詢](#to-execute-a-search-query).

   請注意，顯示在結果中傳回的程式ID會建立超連結。

   ![process_id_list](assets/process_id_list.png)

1. 按一下清單中的程式ID，即可在以下位置檢視此程式的詳細資訊： **程式詳細資料** 面板。

   此 **程式/任務詳細資訊** 查詢結果會顯示流程/任務中所包含任務/表單的詳細資訊。

   依預設，結果會依任務/表單ID排序。 不過，若要依任何欄位排序結果，請按一下欄位標題。 排序結果所依據的欄由欄標題旁邊的深色箭頭指示。

   由於排序是切換操作，按一下欄位標題可將結果遞增排序，再按一下它可遞減排序。 目前的排序順序（升序/降序）是由欄標題旁的變暗箭頭方向所指示。

   **處理詳細資訊結果**

   ![process_details](assets/process_details.png)

   **左側面板：** 顯示所選流程的下列詳細資訊：

   * 處理序名稱
   * 程式建立日期時間
   * 處理完成日期時間
   * 處理持續時間
   * 處理狀態
   * 程式發起人

   **右上面板：** 顯示構成所選程式之工作的下列詳細資訊：

   * 任務ID
   * 任務名稱
   * 任務擁有者
   * 任務建立日期時間
   * 任務更新日期時間
   * 任務完成日期時間
   * 任務工期
   * 任務狀態

   **右下方面板：** 顯示所選處理作業的處理作業歷史記錄的下列詳細資訊：

   * 程式名稱
   * 程式發起人
   * 處理更新日期時間
   * 處理完成日期時間
   * 處理狀態

   **任務詳細資訊結果**

   ![task_details](assets/task_details.png)

   **左側面板：** 顯示所選工作的下列詳細資訊：

   * 任務名稱
   * 此任務所屬的處理序識別碼
   * 任務說明
   * 任務建立日期時間
   * 任務完成日期時間
   * 任務工期
   * 任務狀態
   * 選取的任務路由

   **右上面板：** 顯示構成所選任務的表單的下列詳細資訊：

   * 資料夾ID
   * 表單建立日期時間
   * 表單更新日期時間
   * 表單範本URL

   **右下方面板：** 顯示所選工作的處理作業歷史記錄的下列詳細資訊：

   * 任務指派型別
   * 任務擁有者
   * 任務指派建立日期時間
   * 任務更新日期時間






1. 按一下 **返回流程/任務搜尋** 返回搜尋結果，系統會從該結果向下鑽研流&#39;b5&#39;7b/任務詳細資訊。

   ![back_to_search](assets/back_to_search.png)

   但是，如果透過輸入特定程式/任務ID找到程式/任務詳細資訊，則按一下「返回程式/任務搜尋」可帶您返回 **程式/任務搜尋**，不會顯示任何搜尋結果。

#### 在「程式/任務詳細資訊」面板中輸入程式/任務ID {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. 前往 **程式/任務詳細資訊** 面板。

   ![details_nodes](assets/details_nodes.png)

1. 在「程式/工作識別碼」文字方塊中，輸入程式/工作識別碼。

   ![process_details-1](assets/process_details-1.png)

   中的欄位 **程式/任務詳細資訊** 查詢結果是AEM Forms程式/任務的特定欄位。

   對於處理序，查詢結果會顯示處理序中包含之任務的詳細資訊。

   對於任務，查詢結果會顯示任務中包含的表單的詳細資訊。
