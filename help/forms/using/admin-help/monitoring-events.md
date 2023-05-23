---
title: 監視事件
seo-title: Monitoring events
description: 啟用稽核功能後，Document Security可讓您監視特定型別的事件。 您可以使用Document Security輕鬆搜尋和排序事件清單。
seo-description: When the auditing capability is enabled, document security enables you to monitor certain types of events. You can easily search and sort the events list using the document security.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 監視事件 {#monitoring-events}

啟用稽核功能後，Document Security可讓您監視特定型別的事件。 您可以看到的事件取決於您的角色：

**使用者：** 可以檢視其受原則保護檔案及其收到和使用的任何受保護檔案的已稽核事件。

**原則集協調員：** 可以檢視受原則保護，不受其原則集保護之檔案的已稽核事件，包括檔案和原則事件。

**管理員：** 可以檢視與所有受原則保護檔案和使用者相關的已稽核事件。 管理員也可以追蹤其他型別的事件，包括使用者、檔案、原則和系統事件。

>[!NOTE]
>
>在受原則保護檔案的副本上執行的事件，也會作為原始受保護檔案上的事件進行追蹤。

(請參閱 [事件稽核選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

如果未經授權的使用者嘗試檢視檔案或嘗試使用錯誤的使用者名稱或密碼登入，則會記錄失敗事件。

>[!NOTE]
>
>如果編輯原則以移除匿名存取，可能會記錄檔案的匿名存取事件失敗。 當授權收件者嘗試存取已編輯原則保護的檔案時，仍嘗試匿名存取，但將失敗。

如果原則允許匿名使用者存取，但管理員稍後關閉匿名存取Document Security，則匿名存取受原則保護的檔案將會失敗，並且不會記錄事件。

## 啟用事件稽核 {#enable-event-auditing}

必須符合下列設定要求，才能進行事件稽核：

* 系統或管理員必須啟用伺服器的稽核權能。

   (請參閱 [設定事件稽核和隱私設定](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* 您用來保護檔案的原則必須啟用稽核。 (請參閱 [建立和編輯原則](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## 搜尋事件 {#search-for-an-event}

您可以搜尋事件清單，並檢視有關事件的更詳細說明。 詳細說明包含事件ID、說明、IP位址、組織、使用者受影響、事件發生日期和時間、被拒絕活動以及離線事件（當使用者嘗試在未連線至Document Security時使用檔案時）等資訊。

您可以使用事件搜尋條件與事件發生日期的組合，在「事件」頁面上搜尋事件。 您可以搜尋的事件取決於您的角色：

**使用者：** 可以檢視其受原則保護檔案及其收到和使用的任何受保護檔案的已稽核事件。 提供下列搜尋選項：

**與我相關的事件：** 使用者可以為其建立或接收的任何受原則保護檔案尋找事件。 例如，如果使用者開啟、檢視或列印另一個人保護的檔案，則使用者只會看到該檔案的這些事件。

**與我的檔案相關的事件：** 使用者可以找到與自己受原則保護檔案相關的所有事件。 使用者會看到處理其檔案的每個人員產生的事件。

**原則集協調員：** 可以檢視受原則保護，不受其原則集保護之檔案的已稽核事件，包括檔案和原則事件。 這些選項可供使用：

**記錄我是原則集協調者的事件：** 具有檢視事件許可權的原則集專員可以尋找與原則保護其原則集之檔案相關的事件。

**我擔任原則集協調器的原則事件：** 具有檢視事件許可權的原則集專員可以從其原則集中找到與原則相關的事件。

**管理員：** 可以檢視與所有受原則保護檔案和使用者相關的已稽核事件。 管理員也可以追蹤其他型別。 此外，管理員還可以根據使用者型別進一步細分事件搜尋：

**已知使用者：** 使用者位於來源目錄中，或註冊為外部使用者。

**匿名使用者：** 未知的使用者存取受允許匿名存取之原則保護的檔案。

**系統使用者：** 伺服器啟動的事件，例如目錄同步處理。

1. 在Document Security頁面上，按一下「事件」。
1. 在「尋找」清單中，選取您要使用的搜尋條件。 視您在「尋找」清單中的選取專案而定，會顯示第二個提供額外搜尋條件的清單。 如果適用，請在文字方塊中輸入搜尋條件。

   如需特定事件型別的詳細資訊，請參閱 [事件稽核選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. 在「使用者」清單中，選取執行事件的使用者型別：

   * 如果您選取「已知使用者」，則會顯示第二個搜尋方塊，您必須在此輸入使用者的使用者名稱或電子郵件地址。
   * 如果您不知道這些值，請按一下通訊錄搜尋圖示，依使用者名稱或電子郵件地址來搜尋使用者。

1. 在日期清單中，選取日期範圍選項。 如果您選取「自訂日期」 ，畫面會顯示方塊，您可在其中以yyyy/mm/dd格式輸入日期，或者您也可以使用「日期選擇器」來指定日期範圍：

   * 按一下行事曆以開啟日期選擇器。
   * 使用箭頭來尋找年份和月份。
   * 在行事曆上按一下當月某日。
   * 按一下「確定」以關閉「日期選擇器」。

1. 在「顯示」清單中，選取每頁要顯示的搜尋結果數目。
1. 按一下「尋找」。

   任何失敗事件都會在清單中反白顯示，並出現拒絕圖示。

1. 若要檢視事件的詳細資訊，請按一下清單中事件的說明。

## 排序事件清單 {#sort-the-event-list}

您可以依欄標題排序事件清單，更輕鬆地尋找事件。 欄標題旁的三角形圖示表示目前使用哪一欄來排序。 向上指向三角形表示遞增順序，向下指向三角形表示遞減順序。

1. 按一下適當的欄標題。
1. 若要變更排序順序，請再次按一下欄標題。
