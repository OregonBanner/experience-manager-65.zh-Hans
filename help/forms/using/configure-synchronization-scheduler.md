---
title: 設定同步化排程器
seo-title: Configuring the synchronization scheduler
description: 瞭解如何移轉和同步資產、設定同步排程器，以及使用資料夾來排列資產。
seo-description: Learn how to migrate and sync assets, configure sync scheduler, and use folders to arrange assets.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 設定同步化排程器 {#configuring-the-synchronization-scheduler}

根據預設，同步排程器每3分鐘會執行一次，以同步化透過LiveCycleWorkbench 11在存放庫中修改和更新的所有資產。 同步程式完成後，AEM Forms使用者介面中會顯示包含表單和資源的應用程式。

## 變更同步化排程器的間隔 {#change-interval-of-the-synchronization-scheduler}

執行以下步驟來變更同步化排程器的間隔：

1. 登入AEM組態管理員。 Configuration Manager的網址是 `https://'[server]:[port]'/lc/system/console/configMgr`

1. 找到並開啟 **FormsManagerConfiguration** 套件組合。

1. 為以下專案指定新值 **同步化排程器頻率** 選項。

   頻率單位為分鐘。 例如，若要設定排程器每60分鐘執行，請指定60。

## 同步資產 {#synchronizing-assets}

您可以使用 **從存放庫同步資產** 手動同步資產的選項。 執行以下步驟以手動同步資產：

1. 登入AEM Forms。 預設URL為 `https://'[server]:[port]'/lc/aem/forms/`.

   ![AEM Forms使用者介面](assets/aem_forms_ui.png)

   **圖：** *AEM Forms使用者介面*

1. 按一下 ![aem6forms_sync](assets/aem6forms_sync.png) 圖示加以檢視。 如果您在最後設定的路徑沒有任何資產，則對話方塊如下所示。 按一下 **開始** 以啟動同步化。

   ![同步化對話方塊](assets/migrate-and-syncronize.png)

   **圖：** *同步化對話方塊*

## 疑難排解同步處理錯誤 {#troubleshooting-synchronization-error}

您可以在工作流程設計工具(LiveCycle維護作業)中建立新的應用程式。

如果新建立的應用程式和位於/content/dam/formsanddocuments的資料夾具有相同的名稱，則會出現錯誤»*根層級已存在與此應用程式同名的資產。*「 」已記錄。

若要解決衝突，請重新命名應用程式，然後手動同步資產。

![資產同步化對話方塊中的衝突](assets/sync-conflict.png)

**圖：** *資產同步化對話方塊中的衝突*
