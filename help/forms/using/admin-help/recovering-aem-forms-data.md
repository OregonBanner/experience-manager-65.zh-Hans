---
title: 復原AEM表單資料
seo-title: Recovering the AEM forms data
description: 本檔案說明復原AEM表單資料所需的步驟。
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---

# 復原AEM表單資料 {#recovering-the-aem-forms-data}

本節說明復原AEM表單資料所需的步驟。 另請參閱 [備份與復原的特殊考量](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>資料庫、GDS、AEM儲存庫和內容儲存根目錄必須還原至與原始檔案具有相同DNS名稱的電腦。

AEM forms應該能從下列故障中可靠地復原：

**磁碟故障：** 需要最新的備份媒體來復原資料庫內容。

**資料損毀：** 檔案系統不會記錄過去的交易記錄，而且系統可能會意外覆寫必要的程式資料。

**使用者錯誤：** 復原僅限於資料庫提供的資料。 如果資料已儲存且可供使用，回覆程式就會簡化。

**停電、系統當機：** 檔案系統API的設計或使用方式通常不夠健全，無法防範非預期的系統故障。 如果發生電源中斷或系統當機，儲存在資料庫中的檔案內容比儲存在檔案系統中的內容更可能是最新的。

如果您使用滾動備份模式，復原後您仍會處於備份模式。 如果您使用快照備份模式，則在復原後不會處於備份模式。

從備份還原至新系統時，下列設定可能會不同。 此差異不應影響AEM表單應用程式的成功復原：

* ip位址
* 實體系統組態（CPU、磁碟、記憶體）
* GDS位置

>[!NOTE]
>
>內容儲存根目錄的備份必須還原到該目錄的位置，如同在內容服務設定期間所設定的那樣。

如果多節點叢集的單一節點失敗，且叢集的其餘節點運作正常，請執行叢集單一節點復原程式。

## 復原AEM表單資料 {#recover-the-aem-forms-data}

1. 停止AEM表單服務及應用程式伺服器（如果執行）。
1. 如有必要，請從系統映像重新建立實體系統。 例如，如果復原的原因是錯誤的資料庫伺服器，則可能不需要執行此步驟。
1. 將修補程式或更新套用至建立影像後套用的AEM表單。 此資訊會記錄在備份程式中。 AEM表單必須修補至與系統備份時相同的修補程式層級。
1. (WebSphere® Application Server)如果您要復原到新的WebSphere® Application Server執行個體，請執行restoreConfig.bat/sh命令。
1. 先使用資料庫備份檔案執行資料庫還原作業，然後將交易重做日誌套用至復原的資料庫，以復原AEM表單資料庫。 (請參閱 [AEM forms資料庫](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 如需詳細資訊，請參閱下列其中一篇知識庫文章：

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [AEM表單的Oracle備份與復原](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [適用於AEM表單的MySQL備份與復原](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 請先刪除現有AEM Forms安裝上的GDS目錄內容，然後從備份的GDS複製GDS目錄內容，以復原GDS目錄。 如果您變更了GDS目錄位置，請參閱 [在復原期間變更GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. 重新命名要還原的GDS備份目錄，如下列範例所示：

   >[!NOTE]
   >
   >如果/restore目錄已經存在，請先備份該目錄，然後刪除它，然後再重新命名包含最新資料的/backup目錄。

   * (JBoss®)重新命名 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 至：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`。

   * (WebLogic)重新命名 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 至：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`。

   * (WebSphere®)重新命名 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 至：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`。

1. 請先刪除現有AEM Forms安裝上的「內容儲存根目錄」內容，然後遵循獨立或叢集環境的工作來復原內容，以復原「內容儲存根目錄」：

   >[!NOTE]
   >
   >內容儲存根目錄的備份必須還原至內容儲存根目錄的位置，因為它是在內容服務（已棄用）設定期間所設定。

   **獨立：** 在復原程式中，還原所有已備份的目錄。 還原這些目錄時，如果存在/backup-lucene-indexes目錄，請將其重新命名為/lucene-indexes。 否則，lucene-indexes目錄應該已經存在，並且不需要採取任何動作。

   **叢集：** 在復原程式中，還原所有已備份的目錄。 若要還原「索引根目錄」，請在叢集的每個節點上執行下列步驟：

   * 刪除索引根目錄中的所有內容。
   * 如果/backup-lucene-indexes目錄存在，請複製 *內容儲存根目錄*/backup-lucene-indexes目錄至索引根目錄並刪除 *內容儲存根目錄*/backup-lucene-index目錄。
   * 如果/lucene-indexes目錄存在，請複製 *內容儲存根目錄*/lucene-indexes目錄至索引根目錄。

1. 還原/復原CRX-repository。

   * **獨立**

      *還原作者和發佈執行個體*：如果發生災難，您可以執行中所述的步驟，將存放庫還原至上次備份狀態 [備份與還原。](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      「作者」節點的完整還原作業也會確定Forms Manager和AEM Forms Workspace資料的還原作業。

   * **叢集**

      若要在叢集環境中還原，請參閱 [在叢集環境中進行備份與還原的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. 刪除在java.io.temp目錄或Adobe臨時目錄中建立的任何AEM表單暫存檔。
1. 啟動AEM表單(請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 在復原期間變更GDS位置 {#changing-the-gds-location-during-recovery}

如果您的GDS還原至原本位置以外的位置，請執行LCSetGDS指令碼，將GDS設定至新位置。 指令碼位於 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 資料夾。 指令碼會採用兩個引數， `defaultGDS` 和 `newGDS`. 請參閱 `ReadMe.txt` 檔案來取得如何執行指令碼的指示。

>[!NOTE]
>
>如果您已在資料庫中啟用檔案儲存，則不需要變更GDS位置。

>[!NOTE]
>
>只有在這種情況下，您才應該使用此指令碼來變更GDS位置。 若要在AEM表單執行時變更GDS位置，請使用Administration Console。 (請參閱 [設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>如果GDS目錄位於磁碟機根目錄(例如D:\)，則在Windows上部署元件將會失敗。 對於GDS，您必須確定目錄不是位於磁碟機的根目錄，而是位於子目錄中。 例如，目錄應該是D:\GDS，而不是簡單的D:\。

## 將GDS復原至叢集環境 {#recovering-the-gds-to-a-clustered-environment}

若要變更叢集環境中的GDS位置，請關閉整個叢集，並在叢集的單一節點上執行LCSetGDS指令碼。 (請參閱 [在復原期間變更GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) 僅啟動該節點。 當該節點完全啟動時，叢集中的其他節點可以安全地啟動，並正確地指向新的GDS。

>[!NOTE]
>
>如果您無法確保在啟動其他節點之前完全啟動一個節點，則必須在啟動叢集之前，在叢集中的每個節點上執行LCSetGDS指令碼。
