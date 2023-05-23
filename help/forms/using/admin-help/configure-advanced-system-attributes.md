---
title: 設定進階系統屬性
seo-title: Configure advanced system attributes
description: 您可以在「設定進階系統屬性」頁面修改組態檔中的某些設定值，而不需要匯出、編輯和匯入檔案。
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# 設定進階系統屬性 {#configure-advanced-system-attributes}

您可以在「設定進階系統屬性」頁面修改組態檔中的某些設定值，而不需要匯出、編輯和匯入檔案。 (請參閱 [匯入和匯出組態檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. 在管理控制檯中，按一下 **[!UICONTROL 設定>使用者管理>設定>設定進階系統屬性]**.
1. （可選）變更下列任一工作階段屬性：

   **工作階段逾時限制（分鐘）：** 使用者自動從系統登出之前經過的時間長度，以分鐘為單位。 根據預設，AEM表單元件（例如Workbench）會在兩小時後逾時（無論活動或非活動狀態為何），使用者必須重新登入。 有效值為 `1` 至 `1440`. 預設值為 `120` （2小時）。 此設定會更新 `SAML/Producer/assertionValidityInMinutes` 專案金鑰。

   >[!NOTE]
   >
   >您不應該將工作階段逾時限制設定在10分鐘以下，因為系統可能無法正常運作。 建議值為10-120 （分鐘）。

   **判斷提示臨界值（秒）：** 因叢集中AEM表單應用程式伺服器之間的系統時間差異而抵消延遲的緩衝時間。 AEM forms會根據此屬性中指定的時間量（以秒為單位），將使用者的登入時間倒推。 有效值為 `0` 至 `3600`. 默认值为 `60`。此設定會更新 `SAML/Producer/assertionThresholdInSeconds` 專案金鑰。

   **宣告允許的最長續約時間：** 不需登入即可透明更新使用者工作階段的最大次數。 有效值為 `0` 至 `9999`. 值 `0` 表示宣告不會續約。 默认值为 10。此設定會更新 `SAML/Producer/maxAssertionRenewalCount` 專案金鑰。

1. （選擇性）變更下列任何目錄同步處理屬性：

   **同步統計資料記錄：** 指定「使用者管理」是否在同步處理期間記錄詳細的統計資料。 (請參閱 [在同步處理期間啟用或停用詳細記錄](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **同步完成器Cron運算式：** User Management重試同步失敗的時間間隔。 (請參閱 [設定目錄同步處理重試選項](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **叢集工作鎖定逾時（分鐘）：** 用於叢集環境。 如果一個節點上的同步化失敗，且叢集鎖定未釋放，此值會指定另一個節點在強製取得鎖定之前等待的分鐘數。 預設值為 `15` 分鐘。 有效值為 `1` 至 `1440` 分鐘。

1. （可選）變更下列屬性，然後按一下 **[!UICONTROL 確定]**：

   **使用者管理員事件稽核：** 選取此選項可啟用目錄同步化事件和驗證事件（例如成功、失敗和鎖定）的稽核。 依預設，除非您安裝需要稽核的元件(例如Rights Management)，否則不會選取此選項。 此設定會更新 `APSAuditService` 專案金鑰。

   **自動建立動態群組：** 啟用根據電子郵件網域自動建立動態群組。 (請參閱 [建立動態群組](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

您也可以按一下「重新載入」，回覆成原始的「使用者管理」設定。
