---
title: AEM表單的備份與回覆策略
seo-title: Backup and recovery strategy for AEM forms
description: 瞭解如何實作策略以備份資料，並確保資料與AEM表單資料保持同步。
seo-description: Learn how to implement a strategy to back up data and ensuring that it remains in sync with the AEM forms data.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# AEM表單的備份與回覆策略{#backup-and-recovery-strategy-for-aem-forms}

如果您的AEM表單實作將其他自訂資料儲存在不同的資料庫中，您有責任實作策略來備份此資料，並確保其與AEM表單資料保持同步。 此外，應用程式的設計必須使其足夠健全，能夠處理其他資料庫不同步的情況。 強烈建議您在交易內容中執行任何資料庫作業，以協助維持一致狀態。

在您識別AEM表單的使用方式後，請確定必須備份哪些檔案、備份頻率以及備份視窗是否可以使用。

>[!NOTE]
>
>與AEM Forms實作的其他任何方面一樣，您的備份與復原策略必須在開發或中繼環境中開發及測試，之後才用於生產環境，以確保整個解決方案如預期般運作且不會遺失資料。

Adobe Experience Manager (AEM)是AEM表單不可或缺的一部分。 因此，您需要備份AEM以及與AEM Forms備份同步，因為Correspondence Management解決方案和服務（例如Forms Manager）是以AEM Forms的AEM部分中所儲存的資料為基礎。為了防止任何資料遺失，必須備份AEM Forms特定資料，以確保GDS和AEM （儲存庫）與資料庫參考關聯。資料庫、GDS、AEM和內容儲存根目錄必須還原到與原始資料具有相同DNS名稱的電腦。

## 備份型別 {#types-of-backups}

AEM Forms備份策略包含兩種型別的備份：

**系統影像：** 完整的系統備份，可在硬碟或整部電腦停止運作時，用來還原電腦內容。 系統映像備份只有在AEM表單的生產部署之前是必要的。 然後，內部公司政策會規定系統影像備份的頻率。

**AEM表單特定資料：** 應用程式資料存在於資料庫、全域檔案儲存(GDS)和AEM儲存庫中，且必須即時備份。 GDS是用來儲存處理序中使用的長期檔案的目錄。 這些檔案可能包括PDF、原則或表單範本。

>[!NOTE]
>
>如果已安裝Content Services （已棄用），請一併備份內容儲存根目錄。 另請參閱 [內容儲存根目錄（僅限內容服務）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

資料庫用來儲存表單成品、服務設定、處理狀態以及GDS檔案的資料庫參考。 如果您在資料庫中啟用了檔案儲存，則GDS中的永久資料和檔案也會儲存在資料庫中。 您可以使用下列方法來備份及復原資料庫：

* **快照備份** 模式表示AEM forms系統處於備份模式，可為無限期或在指定的分鐘數內，之後便不再啟用備份模式。 若要進入或離開快照備份模式，您可以使用下列其中一個選項。 在復原情況之後，不應啟用快照備份模式。

   * 使用「管理主控台」中的「備份設定值」頁面。 若要進入快照模式，請選取「在安全備份模式下操作」核取方塊。 取消選取核取方塊以結束快照模式。
   * 使用LCBackupMode指令碼(請參閱 [備份資料庫、GDS和內容儲存根目錄](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories))。 若要結束快照備份模式，請在指令碼引數中，設定 `continuousCoverage` 引數至 `false` 或使用 `leaveContinuousCoverage` 選項。
   * 使用提供的備份/復原API。 <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **正在復原備份** 模式表示系統始終處於備份模式，一旦釋放上一個工作階段，就會啟動新的備份模式工作階段。 無逾時與正在復原的備份模式相關聯。 當呼叫LCBackupMode指令碼或API以離開滾動備份模式時，新的滾動備份模式工作階段開始。 此模式在支援連續備份時非常有用，但仍允許從GDS目錄中清除舊的和不需要的檔案。 不支援透過「備份與復原」頁面來捲動備份模式。 復原案例後，捲動備份模式仍會啟用。 您可以使用LCBackupMode指令碼搭配 `leaveContinuousCoverage` 選項。

>[!NOTE]
>
>離開捲動備份模式會立即開始新的備份模式工作階段。 若要完全停用滾動備份模式，請使用 `leaveContinuousCoverage` 指令碼中的選項，可覆寫現有的滾動式備份工作階段。 當處於快照備份模式時，您可以像往常一樣離開備份模式。

為了防止資料遺失，AEM表單特定資料的備份方式必須確保GDS和內容儲存根目錄檔案與資料庫參照相互關聯。

>[!NOTE]
>
>當GDS儲存在檔案系統而非資料庫中時，請在GDS備份之前執行資料庫備份。

## 備份與復原的特殊考量 {#special-considerations-for-backup-and-recovery}

如果您因為下列變更而必須將AEM表單復原到其他環境，請遵循下列准則：

* 變更AEM表單伺服器的IP位址、主機名稱或連線埠
* 變更磁碟機代號或目錄路徑
* 變更為不同的資料庫主機、連線埠或名稱

一般而言，這類復原情況是由裝載應用程式伺服器、資料庫伺服器或表單伺服器的伺服器硬體故障所造成。 除了本節所述的AEM表單特定設定外，如果AEM表單伺服器的主機名稱或IP位址變更，您也應該對AEM表單部署的其他部分（例如負載平衡器和防火牆）進行必要的變更。

### 無法變更的專案 {#what-cannot-be-changed}

即使您可以變更資料庫伺服器和許多其他引數，當您從備份復原AEM表單時，也無法變更應用程式伺服器型別或資料庫型別。 例如，如果您正在復原AEM表單備份，則無法將應用程式伺服器從JBoss變更為WebLogic，或將資料庫從Oracle變更為DB2。 此外，復原的AEM表單必須使用相同的檔案系統路徑，例如fonts目錄。

### 復原後重新啟動 {#restarting-after-a-recovery}

在復原後重新啟動表單伺服器之前，請執行下列動作：

1. 以維護模式啟動系統。
1. 請務必在維護模式下將表單管理員與AEM表單同步：

   1. 前往https://&lt;*伺服器*>：&lt;*連線埠*>/lc/fm並使用管理員/密碼憑證登入。
   1. 按一下右上角的使用者名稱（在此案例中為「超級管理員」）。
   1. 按一下 **管理選項**.
   1. 按一下 **開始** 以從存放庫同步資產。

1. 在叢集環境中，主要節點(相對於AEM)應在次要節點之前。
1. 在驗證系統的正常作業之前，請確定沒有從內部或外部來源（例如Web、SOAP或EJB處理啟動器）啟動處理。

如果移動或變更主要AEM表單資料庫，請檢閱與您的應用程式伺服器相關的安裝指南，以取得更新AEM表單資料來源IDP_DS和EDC_DS的資料庫連線資訊的相關資訊。

### 變更AEM表單主機名稱或IP位址 {#changing-the-aem-forms-hostname-or-ip-address}

在叢集中，如果您使用TCP快取而非UDP，則必須更新快取定位器組態。 請參閱與應用程式伺服器相關的設定指南中的「設定快取位置（僅使用TCP快取）」。

### 變更AEM表單節點檔案系統路徑 {#changing-the-aem-forms-node-file-system-paths}

如果您變更獨立節點的檔案系統路徑，則必須更新偏好設定、其他系統組態、自訂應用程式和已部署的AEM表單應用程式中的適當參照。 另一方面，叢集的所有節點都必須使用相同的檔案系統路徑設定。 您必須設定Global Document Storage (GDS)根目錄，並確保它指向復原的GDS復本，該復本與復原的資料庫同步。 設定GDS路徑很重要，因為GDS可以包含要在應用程式伺服器重新啟動時持續存在的資料。

在叢集環境中，所有叢集節點在備份之前和復原之後的存放庫檔案系統路徑設定應該相同。

使用 `LCSetGDS`中的指令碼 `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` 資料夾，以便在變更檔案系統路徑後設定GDS路徑。 請參閱 `ReadMe.txt` 檔案來取得詳細資訊。 如果無法使用舊的GDS目錄路徑， `LCSetGDS` 啟動AEM表單之前，必須使用指令碼來設定GDS的新路徑。

>[!NOTE]
>
>只有在這種情況下，您才應該使用此指令碼來變更GDS位置。 若要在AEM表單執行時變更GDS位置，請使用Administration Console。 (請參閱 [設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

設定GDS路徑之後，以維護模式啟動Forms伺服器，然後使用管理主控台更新新節點的剩餘檔案系統路徑。 確認所有必要的設定均已更新後，請重新啟動並測試AEM表單。
