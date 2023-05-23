---
title: 「教學課程：建立互動式通訊」
seo-title: Create an Interactive Communication for Print and Web
description: 使用所有建置區塊建立互動式通訊
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# 教學課程：建立互動式通訊 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

建立完表單資料模型、檔案片段、範本和Web版本的主題等所有建置區塊後，您就可以開始建立互動式通訊。

互動式通訊可透過兩種管道提供：列印和網路。 您也可以建立以Print channel為主體的互動式通訊。 Web channel的Print as master選項可確保Web channel的內容、繼承和資料繫結衍生自Print channel。 它也能確保在Print channel中所做的變更在Web channel中同步。 不過，互動式通訊作者可以中斷Web channel中特定元件的繼承。

本教學課程將逐步引導您完成為列印和Web頻道建立互動式通訊的步驟。 在本教學課程結束時，您將能夠：

* 為列印頻道建立互動式通訊
* 建立Web channel的互動式通訊
* 以「列印為主版」建立列印與Web互動式通訊

## 建立無同步處理的列印與網頁互動式通訊 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 為列印頻道建立互動式通訊 {#create-interactive-communication-for-print-channel}

以下是已在本教學課程中建立且在為列印頻道建立互動式通訊時所需的資源清單：

**列印範本：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**檔案片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**佈局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**影像：** PayNow和ValueAddedServices

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 並選取 **互動式通訊**. 此 **建立互動式通訊** 精靈隨即顯示。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選取 **FDM_Create_First_IC** 以表單資料模型形式使用，然後點選 **下一個**.
1. 在 **頻道** 精靈：

   1. 指定 **create_first_ic_print_template** 作為「列印」範本，然後點選 **選取**. 確保 **針對Web Channel使用列印為主版** 未選取核取方塊。

   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 做為Web範本並點選 **選取**.

   1. 點選 **建立**.

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 點選 **編輯** 以開啟右窗格中的互動式通訊。
1. 前往 **資產** 標籤並套用篩選器，以在左窗格中僅顯示檔案片段。
1. 將下列檔案片段拖放至互動式通訊中的目標區域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | Customerdetails |
   | bill_summary_first_ic | 帳單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

   ![互動式通訊的檔案片段](assets/create_first_ic_doc_fragments_new.png)

1. 點選 **圖表** 目標區域，然後點選 **+** 新增 **圖表** 元件。
1. 點選「圖表」元件並選取 ![configure_icon](assets/configure_icon.png) （設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選取 **圓形圖** 從 **圖表型別** 下拉式清單。
   1. 選取 **calltype** 屬性來自 **呼叫** 中的資料模型物件型別 **X軸** 區段。 點選 ![done_icon](assets/done_icon.png).
   1. 選取 **頻率** 從 **函式** 下拉式清單。
   1. 選取 **calltype** 屬性來自 **呼叫** 中的資料模型物件型別 **Y軸** 區段。 點選 ![done_icon](assets/done_icon.png).
   1. 點選 ![done_icon](assets/done_icon.png) 以儲存圖表屬性。

1. 前往 **資產** 標籤並套用篩選器，以在左窗格中僅顯示佈局片段。 拖放 **table_lf** 佈局片段到 **逐項列出的呼叫** 目標區域。
1. 選取中的文字欄位 **日期** 欄並點選 ![configure_icon](assets/configure_icon.png) （設定）。
1. 選取 **資料模型物件** 從 **繫結型別** 下拉式清單並選取 **呼叫** > **calldate**. 點選 ![done_icon](assets/done_icon.png) 儲存屬性兩次。

   同樣地，建立繫結 **calltime**， **callnumber**， **callduration**、和 **callcharges** 中的文字欄位 **時間**， **數字**， **持續時間**、和 **費用** 欄。

1. 點選 **Paynow** 目標區域，然後點選 **+** 新增 **影像** 元件。
1. 點選影像元件並選取 ![configure_icon](assets/configure_icon.png) （設定）。 影像屬性會顯示在左窗格中：

   1. 指定 **Paynow** 作為中影像的名稱 **名稱** 欄位。
   1. 點選 **上傳**，選取儲存在本機檔案系統上的影像，然後點選 **開啟**.
   1. 點選 ![done_icon](assets/done_icon.png) 以儲存影像屬性。

1. 重複步驟13和14以新增 **ValueAddedServices** 影像至 **ValueAddedServices** 目標區域。

### 建立Web channel的互動式通訊 {#create-interactive-communication-for-web-channel}

以下是已在本教學課程中建立且在建立Web頻道的互動式通訊時所需的資源清單：

**網頁範本：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表單資料模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**檔案片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**影像：** PayNowWeb和ValueAddedServicesWeb

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 並選取 **互動式通訊**. 此 **建立互動式通訊** 精靈隨即顯示。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選取 **FDM_Create_First_IC** 以表單資料模型形式使用，然後點選 **下一個**.
1. 在 **頻道** 精靈：

   1. 指定 **create_first_ic_print_template** 作為「列印」範本，然後點選 **選取**. 確保 **針對Web Channel使用列印為主版** 未選取核取方塊。

   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 做為Web範本並點選 **選取**.

   1. 點選 **建立**.

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 點選 **編輯** 以開啟右窗格中的互動式通訊。
1. 點選 **頻道** 從左窗格按Tab鍵並點選 **Web**.
1. 前往 **資產** 標籤並套用篩選器，以在左窗格中僅顯示檔案片段。
1. 將下列檔案片段拖放至互動式通訊中的目標區域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 帳單詳細資訊 |
   | customer_details_first_ic | Customerdetails |
   | bill_summary_first_ic | 帳單摘要 |
   | summary_charges_first_interactive_communication | 費用 |

1. 點選 **費用摘要** 目標區域，然後點選 **+** 新增 **圖表** 元件。
1. 點選「圖表」元件並選取 ![configure_icon](assets/configure_icon.png) （設定）。 圖表屬性會顯示在左窗格中：

   1. 指定圖表的名稱。
   1. 選取 **圓形圖** 從 **圖表型別** 下拉式清單。

   1. 選取 **calltype** 屬性來自 **呼叫** 中的資料模型物件型別 **X軸** 區段。 點選 ![done_icon](assets/done_icon.png).

   1. 選取 **頻率** 從 **函式** 下拉式清單。

   1. 選取 **calltype** 屬性來自 **呼叫** 中的資料模型物件型別 **Y軸** 區段。 點選 ![done_icon](assets/done_icon.png).

   1. 點選 ![done_icon](assets/done_icon.png) 以儲存圖表屬性。

1. 選取 **資料來源** 標籤並拖放 **呼叫** 資料模型物件至 **逐項列出的呼叫** 目標區域。 中的所有屬性 **呼叫** 資料模型物件會顯示為 **逐項列出的呼叫** 右窗格中的目標區域。

   根據使用案例，您在表格中需要「通話日期」、「通話時間」、「通話號碼」、「通話持續時間」和「通話費用」欄。

   ![互動式通訊的表格](assets/table_ic_web_new.png)

1. 選取 **Mobilenum** 表格欄標題並選取 **更多選項** > **刪除欄**. 同樣地，刪除 **Calltype** 欄。
1. 選取 **Calldate** 表格欄標題並點選 ![編輯](assets/edit.png) （編輯）將文字重新命名為 **通話日期**. 同樣地，重新命名表格中的其他欄標題。
1. 根據使用案例，插入 **立即付款** 互動式通訊中的按鈕，提供使用者按一下按鈕以進行付款的選項。 執行以下步驟來插入按鈕：

   1. 點選 **立即付款** 目標區域，然後點選 **+** 新增 **文字** 元件。

   1. 點選文字元件並點選 ![編輯](assets/edit.png) （編輯）。
   1. 將文字重新命名為 **立即付款**.
   1. 選取文字並點選「超連結」圖示。
   1. 在中指定付款URL **路徑** 欄位。
   1. 選取 **新標籤** 從 **Target** 下拉式清單。

   1. 點選 ![done_icon](assets/done_icon.png) 以儲存超連結屬性。

1. 選取 **樣式** 從「 」旁邊的「 」下拉式清單 **預覽** 選項。

   ![選取互動式通訊的樣式模式](assets/select_style_ic_web_new.png)

1. 使用下列步驟，設定超連結文字的樣式，使其顯示為互動式通訊中的按鈕：

   1. 點選文字元件並選取 ![編輯](assets/edit.png) （編輯）。
   1. 在 **邊框** 區段，指定 **1.5畫素** 作為 **邊框寬度**，選取 **實線** 作為 **邊框樣式**，並指定 **46畫素** 作為 **邊框半徑**.

   1. 選取「紅色」作為按鈕的背景顏色，該按鈕位於 **背景** 區段。
   1. 在 **利潤** 欄位 **Dimension與位置** 區段，點選 **同時編輯** 圖示，並設定 **右** 邊界為 **450畫素**. 「上」、「下」和「左」欄位會設定為空白。

   ![在互動式通訊中插入超連結](assets/ic_web_hyperlink_new.png)

1. 點選 **立即付款** 目標區域，然後點選 **+** 新增 **影像** 元件。
1. 點選影像元件並選取 ![configure_icon](assets/configure_icon.png) （設定）。 影像屬性會顯示在左窗格中：

   1. 指定 **Paynow** 作為中影像的名稱 **名稱** 欄位。

   1. 點選 **上傳**，選取 **PayNowWeb** 影像儲存在本機檔案系統上，然後點選 **開啟**.

   1. 點選 ![done_icon](assets/done_icon.png) 以儲存影像屬性。

1. 根據使用案例，插入 **訂閱** 互動式通訊中的按鈕，可讓使用者透過按一下按鈕來訂閱增值服務。

   重複步驟13到17以新增 **訂閱** 按鈕至 **增值服務** 目標區域並新增 **ValueAddedServicesWeb** 影像。

## 使用自動同步建立列印與網頁的互動式通訊 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您也可以透過啟用列印和Web頻道之間的自動同步來建立互動式通訊。 若要啟用自動同步化，請在建立互動式通訊時選取「列印為主版」選項。 選取「列印為主版」選項，可確保Web channel的內容、繼承和資料繫結衍生自Print channel。 它也能確保在列印管道中所做的變更反映在網頁管道中。

執行以下步驟，衍生使用Print channel的Web channel內容：

1. 登入AEM編寫執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** 並選取 **互動式通訊**. 此 **建立互動式通訊** 精靈隨即顯示。
1. 指定 **create_first_ic** 在 **標題** 和 **名稱** 欄位。 選取 **FDM_Create_First_IC** 以表單資料模型形式使用，然後點選 **下一個**.
1. 在 **頻道** 精靈：

   1. 指定 **create_first_ic_print_template** 作為「列印」範本，然後點選 **選取**.

   1. 選取 **針對Web Channel使用列印為主版** 核取方塊。
   1. 指定 **Create_First_IC_templates** 資料夾> **Create_First_IC_Web_Template** 做為Web範本並點選 **選取**.

   1. 點選 **建立**.

   系統會顯示確認訊息，指出已成功建立互動式通訊。

1. 點選 **編輯** 以開啟右窗格中的互動式通訊。
1. 執行步驟6 - 15 / [為列印頻道建立互動式通訊](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 區段。
1. 點選 **頻道** 從左窗格按Tab鍵並點選 **Web** 從Print channel自動產生Web channel的內容。
1. 作為 **針對Web Channel使用列印為主版** 在步驟4中選取核取方塊，則會從Print channel自動為Web channel產生內容和繫結。

   列印管道內容會插入Web channel範本內容下方。 若要修改從Print channel自動產生的Web channel內容，您可以取消任何目標區域的繼承。

   將滑鼠游標停留在Web Channel中的相關目標區域上，然後選取 ![取消繼承](assets/cancelinheritance.png) （取消繼承），然後在 **取消繼承** 對話方塊，點選 **是**.

   ![取消继承](assets/cancel_inheritance_web_channel_new.png)

   如果您已取消元件的繼承，則可重新啟用它。 若要重新啟用繼承，請將游標停留在相關目標區域的邊界上（包括元件），然後點選 ![reenableinheritance](assets/reenableinheritance.png).

1. 選取 **內容** 索引標籤進行編輯。
1. 使用內容樹將自動產生的Web頻道內容拖放至Web範本中的現有面板。 以下是需要重新排列的元件清單：

   * 「用料表詳細資訊」面板的「用料表詳細資訊」元件
   * 「客戶詳細資料」面板的「客戶詳細資料」元件
   * 「用料表彙總」元件至「用料表彙總」面板
   * 「費用彙總」面板的「費用彙總」元件
   * 分項呼叫面板的佈局片段（表格）

   ![網頁內容樹狀結構](assets/ic_web_content_tree_new.png)

1. 重複步驟13 - 18 / [建立Web channel的互動式通訊](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 以插入 **立即付款** 和 **訂閱** 互動式通訊的Web channel中的超連結。
