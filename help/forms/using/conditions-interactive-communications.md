---
title: 互動式通訊的條件
seo-title: Conditions in Interactive Communications
description: 建立和編輯用於互動式通訊的條件片段 — 條件是用於建立互動式通訊的四種檔案片段型別之一。 其他三個是文字、清單和佈局片段。
seo-description: Creating and editing conditions to be used in Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# 互動式通訊的條件{#conditions-in-interactive-communications}

建立和編輯用於互動式通訊的條件片段 — 條件是用於建立互動式通訊的四種檔案片段型別之一。 其他三個是文字、清單和佈局片段。

## 概述 {#overview}

條件是可包含在互動式通訊中的檔案片段。 其他檔案片段包括 [文字](../../forms/using/texts-interactive-communications.md)、清單和佈局片段。 條件可讓您根據提供的資料和規則定義一或多個內容相關資產，這些資產會包含在互動式通訊中。

示例：

* 在信用卡對帳單中，根據客戶的信用卡型別，顯示信用卡年費和信用卡影像。
* 在保險費到期提醒中，顯示根據客戶所在州的稅捐所計算的稅捐。

條件中的資產，會根據套用的規則和傳遞至規則的值轉譯。 條件中的規則可以檢查下列資料型別中的值：

* 關聯的表單資料模型屬性
* 您在條件中建立的任何變數
* 字符串
* 数字
* 數學運算式
* 日期

## 创建条件 {#createcondition}

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 選取 **[!UICONTROL 建立]** > **[!UICONTROL 條件]**.
1. 指定下列資訊：

   * **[!UICONTROL 標題]**：（選用）輸入條件的標題。 標題不一定是唯一的，而且可以有特殊字元和非英文字元。 條件會以其標題（可用時）參照，例如在縮圖和屬性中。
   * **[!UICONTROL 名稱]**：資料夾中條件的唯一名稱。 資料夾中不能存在任何狀態下具有相同名稱的兩個檔案片段（文字、條件或清單）。 在「名稱」欄位中，您只能輸入英文字元、數字和連字型大小。 「名稱」欄位會根據「標題」欄位自動填入。 在「標題」欄位中輸入的特殊字元、空格、數字和非英文字元，會由「名稱」欄位中的連字型大小取代。 雖然「標題」欄位中的值會自動複製到「名稱」，但您可以編輯該值。

   * **[!UICONTROL 說明]**：輸入檔案片段的說明。
   * **[!UICONTROL 表單資料模型]**：選擇性地選取「表單資料模型」選項按鈕，以根據表單資料模型建立條件。 當您選取表單資料模型選項按鈕時， **[!UICONTROL 表單資料模型]** 欄位隨即顯示。 瀏覽並選取表單資料模型。 建立互動式通訊的條件時，請確定您使用與互動式通訊相同的資料模型。 如需表單資料模型的詳細資訊，請參閱 [資料整合](../../forms/using/data-integration.md).

   * **[!UICONTROL 標籤]**：若要建立自訂標籤，請在文字欄位中輸入值，然後點選Enter 。 儲存此條件時，會建立新新增的標籤。

1. 點選 **[!UICONTROL 下一個]**.

   便會顯示「建立條件」頁面。

   ![createcondition](assets/createcondition.png)

1. 點選 **[!UICONTROL 新增資產]**.

   「選取資產」頁面即會出現，並顯示可在條件中新增的可用文字、清單、條件和影像。

   >[!NOTE]
   >
   >「選取資產」頁面中只會顯示無型、新建立的資產和FDM型資產（使用與正在建立的條件相同的FDM建立）。

1. 點選適當的資產以選取要包含在條件中，然後點選 **[!UICONTROL 完成]**.

   「建立條件」頁面便會出現，並列出新增的資產。

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   您可以使用以下選項管理條件中的資產：

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] 拒絕變更。** 點選此圖示可拒絕您可能對資產和條件中的規則所做的變更。
   **[B] 接受變更。** 點選此圖示以接受您在資產和條件中的規則中所做的變更。
   **[C] 複製資產。** 點選此圖示可建立資產副本以及在條件中套用的規則（如有）。 然後，您可以繼續編輯重複資產的規則和資產。 複製資產有助於建立類似規則，以根據特定內容顯示替代資產。
   **[D] 顯示預覽。** 點選此圖示，即可在「建立\編輯條件」頁面中顯示資產的預覽。
   **&#39;server&#39;重新排序。** 點選並按住此圖示，以拖放資產在條件中重新排序。

   您可以選取下列選項來指定條件在執行階段的行為：

   * **已停用多個結果評估\已啟用多個結果評估**：啟用此選項時（顯示為「啟用多項結果評估」），會評估所有規則，結果會是所有真正規則的總和。 如果停用此選項（顯示為「已停用多個結果評估」），則只會評估第一個被發現為true的規則，並成為條件的輸出。

   * **分頁符號**：選取此選項( ![中斷](assets/break.png))，在條件的資產之間新增分頁符號。 未選取此選項時( ![nobreak](assets/nobreak.png))，如果條件溢位到列印輸出的下一頁，則整個條件會移至下一頁，而不是在條件中資產之間的頁面中中斷。

1. 點選 **[!UICONTROL 建立規則]** 以視需要新增顯示或隱藏資產的規則。 若要在規則中使用變數，請參閱 [建立變數](#variables). 如需詳細資訊，請參閱 [將規則新增至條件](#ruleeditor).

   建立的規則會顯示在「建立條件」畫面的「規則」欄中。

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >您可以在已套用規則或重複專案的條件中插入資產。

1. 點選 **[!UICONTROL 儲存]**.

   條件已建立。 現在當您建立互動式通訊時，可以繼續使用條件作為建置區塊。

   >[!NOTE]
   >
   >若要儲存新的或編輯的條件，條件中新增的每個資產都必須至少有一個規則。

## 編輯條件 {#edit-a-condition}

您可以使用下列步驟編輯條件。 您也可以選取躍現式選單中的「編輯片段」，從互動式通訊中編輯條件。

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL 檔案片段]**.
1. 導覽至條件並加以選取。
1. 點選 **[!UICONTROL 編輯]**.
1. 在條件中進行所需的變更。 如需可在條件中變更之資訊的詳細資訊，請參閱 [建立條件](#createcondition).
1. 點選 **[!UICONTROL 儲存]** 然後點選 **[!UICONTROL 關閉]**.

## 在條件中建立規則 {#ruleeditor}

在條件中使用規則編輯器，您可以建立規則來根據以下條件顯示或隱藏資產 **預設集條件**. 這些條件可建構於：

* 字符串
* 数字
* 數學運算式
* 日期
* 關聯的表單資料模型屬性
* 任何 [變數](#variables) 您可能已建立的

### 在條件中建立規則 {#create-rule-in-condition}

1. 在建立或編輯條件時，點選 ![ruleeditoricon](assets/ruleeditoricon.png) 相關資產的（規則編輯器）圖示。

   「建立規則」對話方塊隨即顯示。 除了字串、數字、數學運算式和日期之外，規則編輯器中也提供下列專案來建立規則的陳述式：

   * 關聯的表單資料模型屬性
   * 任何 [變數](#variables) 您已建立的URL。

   ![createruledialog](assets/createruledialog.png)

   選取要評估的適當選項。

   >[!NOTE]
   >
   >集合屬性不支援建立顯示資產的規則。

1. 選取要評估規則的適當運運算元，例如「等於」、「包含」和「開頭為」。
1. 插入評估運算式、字串、資料模型屬性、變數或日期。

   ![原則型別為標準時顯示資產的規則](assets/ruleincondition.png)

   原則型別為標準時顯示資產的規則

   * 在建立或編輯規則時，您也可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則/編輯規則」對話方塊。 展開的完整視窗對話方塊可讓您建立 [變數](#variables) 以建構規則。 再次點選「調整大小」可返回一般「建立規則」對話方塊。

   * 您也可以在規則中建立多個條件。

1. 點選 **[!UICONTROL 完成]**.

   此規則會套用至資產。

## 在條件中建立和使用變數 {#variables}

在條件中建立或編輯規則時，您可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話方塊。 展開的完整視窗對話方塊可讓您：

* 在規則中建立和使用變數
* 在規則中拖放表單資料模型的屬性和變數

再次點選「調整大小」以返回「建立規則\編輯規則」對話方塊。

### 建立變數 {#create-variables}

1. 在條件中建立或編輯規則時，您可以點選 ![icon_resize](assets/icon_resize.png) （調整大小）以展開「建立規則\編輯規則」對話方塊。

   「已展開，全視窗」對話方塊隨即顯示。

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. 在左窗格中，點選 **[!UICONTROL 變數]**.

   「變數」窗格隨即顯示。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 點選 **[!UICONTROL 建立]**.

   「建立變數」窗格隨即顯示。

1. 輸入下列資訊並點選 **[!UICONTROL 建立]**：

   * **[!UICONTROL 名稱]**：變數的名稱。
   * **[!UICONTROL 說明]**：選擇性地輸入變數的說明。
   * **[!UICONTROL 型別]**：選取變數型別：字串、數字、布林值或日期。
   * **[!UICONTROL 僅允許特定值]**：針對字串和數字變數，您可以確保代理程式會從代理程式UI中預留位置的一組特定值中進行選擇。 若要指定一組值，請選取此選項，然後指定允許在 **[!UICONTROL 值]** 欄位。

1. 點選 **[!UICONTROL 建立]**.

   變數隨即建立並列於「變數」窗格中。

1. 若要在規則中插入變數，請將變數拖放至規則中某個選項的預留位置。
1. 在您建構有效規則後，點選 **[!UICONTROL 完成]**.

   繼續視需要在條件中進行進一步變更並儲存。
