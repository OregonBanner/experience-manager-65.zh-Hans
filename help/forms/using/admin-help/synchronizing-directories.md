---
title: 同步目錄
seo-title: Synchronizing directories
description: 瞭解如何使用手動或排程同步處理，將使用者管理資料庫與來源目錄伺服器的變更同步。
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# 同步目錄 {#synchronizing-directories}

若要同步化網域，您可以選擇執行手動或排程的同步化。 A *手動同步* 同步任何選取的網域。 A *排定的同步* 同步所有網域。

目錄同步處理用於將您在目錄設定中指定的目錄伺服器詳細資料提取到「使用者管理」資料庫中。 稍後，如果目錄伺服器上發生變更或更新，您也可以執行手動同步處理。 例如，如果新增使用者和群組或變更使用者帳戶，您可以執行手動同步。

您也可以設定每日同步化排程，以自動將「使用者管理」資料庫與來源目錄伺服器的變更或更新同步。 但是，請注意，此程式會使用網路和伺服器資源。 選擇低使用率時段，並避免排程不必要的同步作業，以免繫結系統與網路資源。 若要將不必要的同步化最小化，請改用立即同步化選項。

您也可以指定在同步網域時，是否將使用者和群組資訊推送到AdobeLiveCycle內容服務9 （已棄用）。

>[!NOTE]
>
>請勿在LDAP目錄同步處理進行時建立多個本機使用者和群組。 嘗試此程式可能會導致錯誤。

>[!NOTE]
>
>如果網域同步處理作業中斷（例如，應用程式伺服器會在處理作業期間關閉），請稍候片刻，再嘗試同步處理網域。 若要評估同步化的狀態，請檢視狀態。 如果User Management在關機前取得鎖定，請等待10分鐘讓鎖定在伺服器重新啟動後釋放。 如果同步化狀態為「進行中」，但同步化中斷或停止，「使用者管理」會在3分鐘後重試同步化。 3次嘗試失敗後，「使用者管理」會宣告同步處理失敗，並解除鎖定。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES （已棄用）是隨LiveCycle安裝的內容管理系統。 它可讓使用者設計、管理、監控及最佳化以人為中心的流程。 內容服務（已棄用）支援將於2014年12月31日終止。 另請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## 啟用差異目錄同步處理 {#enable-delta-directory-synchronization}

差異目錄同步處理可改善目錄同步處理的效率。 啟用差異目錄同步化時，「使用者管理」只會同步化自上次同步化以來新增或更新過的使用者和群組。

啟用差異目錄同步化時，「使用者管理」會執行下列步驟：

* 從目錄伺服器擷取所有使用者，但只使用時間戳記已變更的使用者來更新「使用者管理」資料庫。
* 擷取所有群組，但只使用時間戳記已變更的群組來更新「使用者管理」資料庫。
* 僅擷取時間戳記已變更之群組的群組成員，並使用該資訊更新「使用者管理」資料庫。

>[!NOTE]
>
>在您執行完整的目錄同步處理之前，不會從「使用者管理」資料庫刪除從目錄移除的使用者和群組。

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 在「差異同步」下，選取核取方塊並按一下「儲存」。
1. 編輯將使用差異目錄同步化功能的每個企業網域的目錄設定值。 在「使用者設定」和「群組設定」頁面上，找到「修改時間戳記」設定並輸入 `modify TimeStamp` 做為值。 如需有關編輯企業網域的詳細資訊，請參閱 [編輯和轉換現有網域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## 在同步處理期間啟用或停用詳細記錄 {#enable-or-disable-detailed-logging-during-synchronization}

依照預設，「使用者管理」會在同步處理期間記錄詳細的統計資料。

1. 在管理控制檯中，按一下「設定>使用者管理>設定>設定進階系統屬性」。
1. 在同步統計記錄下，取消選取核取方塊以停用詳細記錄，或選取它以啟用記錄，然後按一下儲存。

## 設定目錄同步處理重試選項 {#configure-the-directory-synchronization-retry-option}

您可以設定「使用者管理」定期檢查是否有任何失敗的目錄同步處理嘗試。 然後User Management會嘗試完成失敗的同步。

1. 在管理控制檯中，按一下「設定>使用者管理>設定>設定進階系統屬性」。
1. 在Synch Finisher Cron運算式下，輸入cron運算式，代表「使用者管理」重試同步失敗的時間間隔。 cron運算式使用方式是根據Quartz開放原始碼作業排程系統1.4.0版。

   預設值為0 0/13 &amp;ast； ？ &amp;ast； ，這表示每13分鐘進行一次檢查。

## 手動同步目錄 {#manually-synchronize-directories}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. （可選）若要將使用者和群組資訊推送至內容服務（已棄用），請選取此選項，將使用者和群組推送至已註冊的外部主要儲存提供者選項。 透過「使用者和群組」頁面新增使用者和群組時，此選項也適用。
1. 選取每個要同步的企業網域的核取方塊，然後按一下立即同步。

   如果您選取多個網域，則可以同時執行所有網域的網域同步處理。 但是，如果您單獨選取網域，一次只能執行一個網域同步處理。

## 排程目錄同步處理 {#schedule-directory-synchronization}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 排程同步處理：

   * 若要啟用每日自動同步處理，請在[排程器]下選取[發生]。 從清單中選取每日，並在對應的方塊中以24小時格式輸入時間。 儲存設定時，此值會轉換為cron運算式，顯示在cron運算式方塊中。
   * 若要排程在一週或一個月中的某一天或某一特定月份進行同步處理，請選取Cron運算式，並在方塊中輸入適當的運算式。 例如，在每月最後一個星期五的凌晨1:30進行同步。

cron運算式使用方式是根據Quartz開放原始碼作業排程系統1.4.0版。

* 若要關閉自動同步化，請選取[Occurs]，然後從清單中選取[Never]。
* （可選）若要將使用者和群組資訊推送至內容服務（已棄用），請選取此選項，將使用者和群組推送至已註冊的外部主要儲存提供者選項。 透過「使用者和群組」頁面新增使用者和群組時，此選項也適用。
* 单击“保存”。

## 停止目前進行中的所有目錄同步 {#stop-all-directory-synchronizations-currently-in-progress}

1. 在管理控制檯中，按一下「設定>使用者管理>網域管理」。
1. 按一下「中止」。 此按鈕僅在目錄同步處理進行中時顯示。
