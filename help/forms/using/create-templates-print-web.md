---
title: 教學課程：建立範本
seo-title: Create Print and Web templates for Interactive Communication
description: 建立互動式通訊的列印和Web範本
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 0%

---

# 教學課程：建立範本{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 數列。 建議您依照時間順序觀看本系列，以瞭解、執行和示範完整的教學課程使用案例。

若要建立互動式通訊，您必須在AEM伺服器上擁有可供列印和Web Channels使用的範本。

列印頻道的範本是在AdobeForms Designer中建立並上傳至AEM伺服器。 建立互動式通訊時，即可使用這些範本。

Web channel的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用網頁範本。 建立並啟用後，這些範本便可在建立互動式通訊時使用。

本教學課程將逐步帶您瞭解為列印和Web管道建立範本的步驟，以便在建立互動式通訊時使用這些範本。 在本教學課程結束時，您將能夠：

* 使用AdobeForms Designer為列印頻道建立XDP範本
* 將XDP範本上傳至AEM Forms伺服器
* 建立和啟用網頁頻道的範本

## 建立列印管道的範本 {#create-template-for-print-channel}

使用下列工作建立和管理互動式通訊列印頻道的範本：

* [使用Forms Designer建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [將XDP範本上傳至AEM Forms伺服器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [為佈局片段建立XDP範本](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer建立XDP範本 {#create-xdp-template-using-forms-designer}

根據 [使用案例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖學](/help/forms/using/planning-interactive-communications.md)，在XDP範本中建立下列子表單：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資料：包含檔案片段
* 帳單摘要：包含檔案片段
* 摘要：包含檔案片段（費用子表單）和圖表（圖表子表單）
* 分項呼叫：包含表格（佈局片段）
* 立即付款：包含影像
* 增值服務：包含影像

![create_print_template](assets/create_print_template.gif)

將XDP檔案上傳至Forms伺服器後，這些子表單會在列印範本中顯示為目標區域。 建立互動式通訊時，所有實體（例如檔案片段、圖表、版面片段和影像）都會新增至目標區域。

執行以下步驟，為列印管道建立XDP範本：

1. 開啟Forms Designer，選取 **檔案** > **新增** > **使用空白表單，** 點選 **下一個**，然後點選 **完成** 以開啟表單以建立範本。

   確保 **物件庫** 和 **物件** 選項是從 **視窗** 功能表。

1. 拖放 **子表單** 元件來自 **物件庫** 至表單。
1. 選取子表單，以在下列位置顯示子表單的選項： **物件** 視窗中。
1. 選取 **子表單** 標籤並選取 **已流動** 從 **內容** 下拉式清單。 拖曳子表單的左側端點以調整長度。
1. 在 **繫結** 標籤：

   1. 指定 **帳單詳細資訊** 在 **名稱** 欄位。

   1. 選取 **無資料繫結** 從 **資料繫結** 下拉式清單。

   ![Designer子表單](assets/forms_designer_subform_new.png)

1. 同樣地，選取根子表單，然後選取 **子表單** 標籤，然後選取 **已流動** 從 **內容** 下拉式清單。 在 **繫結** 標籤：

   1. 指定 **TelecaBill** 在 **名稱** 欄位。

   1. 選取 **無資料繫結** 從 **資料繫結** 下拉式清單。

   ![列印範本的子表單](assets/root_subform_print_template_new.png)

1. 重複步驟2 - 5以建立下列子表單：

   * 帳單詳細資訊
   * Customerdetails
   * 帳單摘要
   * 摘要 — 選取 **子表單** 標籤並選取 **已定位** 從 **內容** 此子表單的下拉式清單。 將下列子表單插入 **摘要** 子表單。

      * 費用
      * 圖表
   * ItemisedCalls
   * Paynow
   * ValueAddedServices

   為了節省時間，您也可以複製並貼上現有的子表單以建立新的子表單。

   若要移動 **圖表** 子表單在「費用」子表單的右側，選取 **圖表** 從左窗格中選取子表單 **版面** 標籤，並指定值 **錨點X** 欄位。 值必須大於 **寬度** 的欄位 **費用** 子表單。 選取 **費用** 子表單並選取 **版面** 標籤以檢視 **寬度** 欄位。

1. 拖放 **文字** 物件 **物件庫** 至表單並輸入 **撥打XXXX進行訂閱** 方塊中的文字。
1. 在左窗格中的文字物件上按一下滑鼠右鍵，然後選取 **重新命名物件**，然後輸入文字物件的名稱作為 **訂閱**.

   ![XDP範本](assets/print_xdp_template_subform_new.png)

1. 選取 **檔案** > **另存為** 若要將檔案儲存在本機檔案系統上：

   1. 導覽至儲存檔案的位置，並將名稱指定為 **create_first_ic_print_template**.
   1. 選取 **.xdp** 從 **另存為型別** 下拉式清單。

   1. 點選 **儲存**.

### 將XDP範本上傳至AEM Forms伺服器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer建立XDP範本後，您必須將其上傳到AEM Forms伺服器，以便在建立互動式通訊時使用該範本。

1. 選取 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **建立** > **檔案上傳**.

   瀏覽並選取 **create_first_ic_print_template** 範本(XDP)並點選 **開啟** 將XDP範本匯入AEM Forms伺服器。

### 為佈局片段建立XDP範本 {#create-xdp-template-for-layout-fragments}

若要為互動式通訊的列印頻道建立佈局片段，請使用Forms Designer建立XDP並將其上傳到AEM Forms伺服器。

1. 開啟Forms Designer，選取 **檔案** > **新增** > **使用空白表單，** 點選 **下一個**，然後點選 **完成** 以開啟表單以建立範本。

   確保 **物件庫** 和 **物件** 選項是從 **視窗** 功能表。

1. 拖放 **表格** 元件來自 **物件庫** 至表單。
1. 在「插入表格」對話方塊中：

   1. 指定欄數為 **5**.
   1. 指定內文列數為 **1**.
   1. 選取 **在表格中包含標題列** 核取方塊。
   1. 標籤 **確定**.

1. 點選 **+** 在左窗格旁邊 **表格** 1並按一下右鍵 **儲存格1** 並選取 **重新命名物件** 至 **日期**.

   同樣地，重新命名 **儲存格2**， **儲存格3**， **儲存格4**、和 **儲存格5** 至 **時間**， **數字**， **持續時間**、和 **費用** （分別）。

1. 按一下「 」中的「標頭」文字欄位 **設計工具檢視** 並將它們重新命名為 **時間**， **數字**， **持續時間**、和 **費用**.

   ![佈局片段](assets/layout_fragment_print_new.png)

1. 選取 **第1列** 從左窗格中選取 **物件** > **繫結** > **對每個資料專案重複列**.

   ![重複佈局片段的屬性](assets/layout_fragment_print_repeat_new.png)

1. 拖放 **文字欄位** 元件來自 **物件庫** 至 **設計工具檢視**.

   ![佈局片段的文字欄位](assets/layout_fragment_print_text_field_new.png)

   同樣地，拖放 **文字欄位** 元件至 **時間**， **數字**， **持續時間**、和 **費用** 列。

1. 選取 **檔案** > **另存為** 若要將檔案儲存在本機檔案系統上：

   1. 導覽至儲存檔案的位置，並將名稱指定為 **table_lf**.
   1. 選取 **.xdp** 從 **另存為型別** 下拉式清單。

   1. 點選 **儲存**.
   使用Forms Designer建立版面片段的XDP範本後，您必須 [上傳](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 將其傳送至AEM Forms伺服器，以便建立版面片段時可以使用範本。

## 建立Web channel範本 {#create-template-for-web-channel}

使用下列工作建立和管理互動式通訊Web channel的範本：

* [建立範本資料夾](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [建立範本](../../forms/using/create-templates-print-web.md#create-the-template)
* [啟用範本](../../forms/using/create-templates-print-web.md#enable-the-template)
* [啟用互動式通訊中的按鈕](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 建立範本資料夾 {#create-folder-for-templates}

若要建立Web channel範本，請定義一個資料夾，您可以在其中儲存建立的範本。 在該資料夾中建立範本後，請啟用範本以允許表單使用者根據該範本建立互動式通訊的Web channel。

執行以下步驟，為可編輯的範本建立資料夾：

1. 點選 **工具** ![槌子圖示](assets/hammer-icon.svg) > **設定瀏覽器**.
   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
1. 在「設定瀏覽器」頁面中，點選 **建立**.
1. 在 **建立設定** 對話方塊，指定 **Create_First_IC_templates** 若為資料夾的標題，請核取 **可編輯的範本**，然後點選 **建立**.

   ![設定網頁範本](assets/create_first_ic_web_template_new.png)

   此 **Create_First_IC_templates** 資料夾建立並列於 **設定瀏覽器** 頁面。

### 建立範本 {#create-the-template}

根據 [使用案例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖學](/help/forms/using/planning-interactive-communications.md)中，在Web範本中建立下列面板：

* 帳單詳細資訊：包含檔案片段
* 客戶詳細資料：包含檔案片段
* 帳單摘要：包含檔案片段
* 費用摘要：包含檔案片段和圖表（兩欄式配置）
* 分項呼叫：包含表格
* 立即付款：包含 **立即付款** 按鈕和影像
* 增值服務：包含影像和 **訂閱** 按鈕。

![create_web_template](assets/create_web_template.gif)

建立互動式通訊時，會新增所有實體，例如檔案片段、圖表、表格、影像和按鈕。

執行以下步驟，在中建立Web通道的範本 **Create_First_IC_templates** 資料夾：

1. 選取「 」，導覽至適當的範本資料夾 **工具** > **範本** > **Create_First_IC_templates** 資料夾。
1. 點選 **建立**.
1. 於 **挑選範本型別** 設定精靈，選取 **互動式通訊 — Web Channel** 並點選 **下一個**.
1. 於 **範本詳細資訊** 設定精靈，指定 **Create_First_IC_Web_Template** 作為範本標題。 指定選擇性說明並點選 **建立**.

   確認訊息，指明 **Create_First_IC_Web_Template** 隨即顯示。

1. 點選 **開啟** 以在範本編輯器中開啟範本。
1. 選取 **初始內容** 從「 」旁邊的「 」下拉式清單 **預覽** 選項。

   ![模板编辑器](assets/template_editor_initial_content_new.png)

1. 點選 **根面板** 然後點選 **+** 以檢視可新增至範本的元件清單。
1. 選取 **面板** 從清單中新增面板 **根面板**.
1. 選取 **內容** 索引標籤進行編輯。 在步驟8中新增的新面板會顯示在 **根面板** 在內容樹狀結構中。

   ![内容树](assets/content_tree_root_panel_new.png)

1. 選取面板並點選 ![configure_icon](assets/configure_icon.png) （設定）。
1. 在「屬性」窗格中：

   1. 指定 **帳單詳細資訊** 名稱欄位中。
   1. 指定 **帳單詳細資訊** 標題欄位中。
   1. 選取 **1** 從 **欄數** 下拉式清單。

   1. 點選 ![](/help/forms/using/assets/done_icon.png) 以儲存屬性。

   面板名稱會更新為 **帳單詳細資訊** 在內容樹狀結構中。

1. 重複步驟7 - 11，將具有以下屬性的面板新增至範本：

   | 名称 | 标题 | 列数 |
   |---|---|---|
   | customerdetails | 客戶詳細資料 | 1 |
   | 帳單摘要 | 帳單摘要 | 1 |
   | 彙總費用 | 費用摘要 | 2 |
   | itemisedcalls | 逐項列出的呼叫 | 1 |
   | paynow | 立即付款 | 2 |
   | vas | 增值服務 | 1 |

   以下影像說明將所有面板新增至範本後的內容樹狀結構：

   ![所有面板的內容樹](assets/content_tree_all_panels_new.png)

### 啟用範本 {#enable-the-template}

建立Web範本後，您必須將其啟用，才能在建立互動式通訊時使用範本。

執行以下步驟以啟用Web範本：

1. 點選 **工具** ![槌子圖示](assets/hammer-icon.svg) > **範本**.
1. 導覽至 **Create_First_IC_Web_Template** 範本，選取並點選 **啟用**.
1. 標籤 **啟用** 再次確認。

   範本已啟用，其狀態會顯示為「已啟用」。 建立Web通道的互動式通訊時，您可以使用此範本。

### 啟用互動式通訊中的按鈕 {#enabling-buttons-in-interactive-communications}

根據使用案例，您必須包含 **立即付款** 和 **訂閱** 互動式通訊中的按鈕（最適化表單元件）。 若要在互動式通訊中啟用這些按鈕，請執行下列步驟：

1. 選取 **結構** 從「 」旁邊的「 」下拉式清單 **預覽** 選項。
1. 選取 **檔案容器** 使用內容樹並點選根面板 **原則** 以選取可在互動式通訊中使用的元件。

   ![設定原則](assets/structure_configure_policy_new.png)

1. 在 **允許的元件** 索引標籤/ **屬性** 區段，選取 **按鈕** 從 **最適化表單** 元件。

   ![允許的元件](assets/allowed_components_af_new.png)

1. 點選 ![done_icon](assets/done_icon.png) 以儲存屬性。
