---
title: 备份和恢复
seo-title: Backup and Restore
description: 瞭解如何備份及還原您的AEM內容。
seo-description: Learn how to backup and restore your AEM content.
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2283'
ht-degree: 0%

---

# 备份和恢复{#backup-and-restore}

在AEM中有兩種方式可備份和還原存放庫內容：

* 您可以建立存放庫的外部備份，並將其儲存在安全的位置。 如果存放庫損毀，您可以將其還原成先前的狀態。
* 您可以建立存放庫內容的內部版本。 這些版本與內容一起儲存在存放庫中，因此您可以快速還原已變更或刪除的節點和樹狀結構。

## 常规 {#general}

這裡說明的方法適用於系統備份與復原。

如果您需要備份和/或復原少量遺失的內容，則系統不一定需要復原：

* 您可以透過套件從其他系統擷取資料
* 或者，您也可以在暫存系統上還原備份，建立內容套件並將其部署在缺少此內容的系統上。

如需詳細資訊，請參閱 [封裝備份](/help/sites-administering/backup-and-restore.md#package-backup) 下方的。

## 計時 {#timing}

請勿與資料存放區垃圾收集同時執行備份，因為這樣可能會損害兩個流程的結果。

## 離線備份 {#offline-backup}

您可以隨時進行離線備份。 這需要AEM的停機時間，但相較於線上備份，此備份所需的時間會相當有效率。

在大多數情況下，您會使用檔案系統快照，在當時建立儲存裝置的唯讀復本。 若要建立離線備份，請執行下列步驟：

* 停止應用程式
* 建立快照集備份
* 啟動應用程式

由於快照備份通常只需要幾秒鐘，因此整個停機時間少於幾分鐘。

## 線上備份 {#online-backup}

此備份方法會建立整個存放庫的備份，包括部署在其下的任何應用程式，例如AEM。 備份包括內容、版本記錄、設定、軟體、Hotfix、自訂應用程式、記錄檔、搜尋索引等。 如果您使用叢集，且共用資料夾是的子目錄 `crx-quickstart` （實體上或使用軟連結），也會備份共用目錄。

您可以在稍後還原整個存放庫（以及任何應用程式）。

此方法會當作「熱備份」或「線上」備份運作，因此可在存放庫執行時執行。 因此，在執行備份時可以使用存放庫。 此方法適用於預設的Tar儲存基礎存放庫執行個體。

建立備份時，您有以下選項：

* 使用AEM整合式備份工具備份到目錄。
* 使用檔案系統快照備份至目錄

無論如何，備份都會建立存放庫的影像（或快照）。 然後系統備份代理程式應該會小心將這個映像實際傳輸到專用的備份系統（磁帶機）。

>[!NOTE]
>
>如果AEM Online Backup功能用於具有自訂Blobstore設定的AEM執行個體，建議將資料存放區的路徑設定為「 `crx-quickstart`」目錄並分別備份資料存放區。

>[!CAUTION]
>
>線上備份只會備份檔案系統。 如果您將儲存庫內容和/或儲存庫檔案儲存在資料庫中，則需要分別備份該資料庫。 如果您正在搭配使用AEM與MongoDB，請參閱有關如何使用 [MongoDB原生備份工具](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### AEM線上備份 {#aem-online-backup}

存放庫的線上備份可讓您建立、下載和刪除備份檔案。 它是「熱備份」或「線上」備份功能，因此可在存放庫正常使用於讀寫模式時執行。

>[!CAUTION]
>
>請勿同時執行AEM Online Backup和 [資料存放區垃圾收集](/help/sites-administering/data-store-garbage-collection.md) 或 [修訂清除](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). 這會對系統效能產生負面影響。

開始備份時，您可以指定 **目標路徑** 和/或 **延遲**.

**目標路徑** 備份檔案通常儲存在含有quickstart jar檔案(.jar)的資料夾的父資料夾中。 例如，如果您的AEM jar檔案位於/InstallationKits/AEM下，則會在/InstallationKits下產生備份。 您也可以指定目標至您選擇的位置。

如果 **目標路徑** 是一個目錄，在此目錄中建立存放庫的影像。 如果同一目錄被多次（或一律使用）用來儲存備份，

* 存放庫中已修改的檔案會在TargetPath中相應修改
* 存放庫中刪除的檔案會在TargetPath中刪除
* 在存放庫中建立的檔案會在TargetPath中建立

>[!NOTE]
>
>若 **目標路徑** 設為副檔名為的檔案名稱 **.zip**&#x200B;時，會將存放庫備份至暫存目錄，然後壓縮此暫存目錄的內容並儲存在ZIP檔案中。
>
>不建議使用此方法，因為
>
>* 在備份過程中需要額外的磁碟儲存空間（暫存目錄加上zip檔案）
>* 壓縮程式由存放庫完成，可能會影響其效能。
>* 這會延遲備份程式。
>* Java 1.6 Java最多只能建立4 GB大小的ZIP檔案。
>
>如果您需要建立ZIP作為備份格式，您應該備份至目錄，然後使用壓縮程式來建立zip檔案。

**延遲** 表示時間延遲（以毫秒為單位），因此存放庫效能不受影響。 依預設，存放庫備份會以全速執行。 您可以減慢建立線上備份的速度，以免減慢其他工作的速度。

若使用非常長的延遲，請確保線上備份所需時間不超過24小時。 如果是，請捨棄此備份，因為它可能不包含所有二進位檔。
1毫秒的延遲通常會導致10%的CPU使用率，而10毫秒的延遲通常會導致3%以下的CPU使用率。 總延遲秒數（以秒為單位）的估計如下：存放庫大小（以MB為單位），乘以延遲（以毫秒為單位），再除以2 （如果使用zip選項），或再除以4 （備份至目錄時）。 這表示備份至200 MB存放庫的目錄並延遲1毫秒，會將備份時間增加約50秒。

>[!NOTE]
>
>另請參閱 [AEM Online Backup如何運作](#how-aem-online-backup-works) 以取得流程的內部詳細資訊。

若要建立備份：

1. 以管理員身分登入AEM。

1. 前往 **工具 — 作業 — 備份。**
1. 单击&#x200B;**创建**。備份主控台將會開啟。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在備份主控台上，指定 **[目標路徑](#aem-online-backup)** 和 **[延遲](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >備份主控台也可透過以下方式使用：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 按一下 **儲存**，進度列會指出備份進度。

   >[!NOTE]
   >
   >您可以 **取消** 隨時執行備份。

1. 備份完成後，壓縮檔會列在備份視窗中。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >您可使用主控台移除不再需要的備份檔案。 在左窗格中選取備份檔案，然後按一下 **刪除**.

   >[!NOTE]
   >
   >如果您已備份到目錄：備份程式完成後，AEM將不會寫入目標目錄。

### 自動化AEM線上備份 {#automating-aem-online-backup}

如果可能的話，應該在系統負載很少時執行線上備份，例如在早上。

備份可透過以下方式自動化： `wget` 或 `curl` http使用者端。 以下範例說明如何使用curl自動化備份。

#### 備份至預設目標目錄 {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在下列範例中， `curl` 命令可能需要為您的執行個體進行設定；例如，主機名稱( `localhost`)，連線埠( `4502`)，管理員密碼( `xyz`)和檔案名稱( `backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

備份檔案/目錄是在伺服器上所包含的資料夾的父資料夾中建立的。 `crx-quickstart` 資料夾（與使用瀏覽器建立備份時相同）。 例如，如果您在目錄中安裝了AEM `/InstallationKits/crx-quickstart/`，則會在中建立備份 `/InstallationKits` 目錄。

curl命令會立即傳回，因此您必須監視此目錄以檢視zip檔案何時準備就緒。 建立備份時，可以看到暫存目錄（其名稱以最終zip檔案的名稱為基礎），但最後會壓縮此目錄。 例如：

* 產生的zip檔案名稱： `backup.zip`
* 暫存目錄的名稱： `backup.f4d5.temp`

#### 備份至非預設的目標目錄 {#backing-up-to-a-non-default-target-directory}

通常，備份檔案/目錄會建立於伺服器上包含 `crx-quickstart` 資料夾。

如果要將備份（任何一種排序）儲存到其他位置，您可以將「至」的絕對路徑設定為 `target` 中的引數 `curl` 命令。

例如，若要產生 `backupJune.zip` 在目錄中 `/Backups/2012`：

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用不同的應用程式伺服器（例如JBoss）時，線上備份可能無法如預期運作，因為目標目錄不可寫入。 在此情況下，請聯絡支援人員。

>[!NOTE]
>
>也可以觸發備份 [使用AEM提供的MBean](/help/sites-administering/jmx-console.md).

### 檔案系統快照備份 {#filesystem-snapshot-backup}

這裡所述的程式特別適用於大型存放庫。

>[!NOTE]
>
>如果要使用此備份方法，您的系統必須支援檔案系統快照。 例如，對於Linux，這表示您的檔案系統應該放在邏輯磁碟區上。

1. 對部署了AEM的檔案系統進行快照。

1. 掛載檔案系統快照。
1. 執行備份並解除安裝快照。

### AEM Online Backup如何運作 {#how-aem-online-backup-works}

AEM Online Backup包含一系列內部動作，以確保要備份的資料和要建立的備份檔案的完整性。 以下列出感興趣的訪客名單。

線上備份會使用下列演演算法：

1. 建立zip檔案時，第一步是建立或尋找目標目錄。

   * 如果備份至zip檔案，則會建立暫存目錄。 目錄名稱開頭為 `backup.` 結束於 `.temp`；例如 `backup.f4d3.temp`.
   * 如果備份到目錄，則會使用目標路徑中指定的名稱。 可以使用現有的目錄，否則將會建立新目錄。

      名為的空白檔案 `backupInProgress.txt` 會在備份開始時，在目標目錄中建立。 備份完成時會刪除此檔案。

1. 檔案會從來源目錄複製到目標目錄（或建立zip檔案時的暫存目錄）。 區段存放區會在資料存放區之前複製，以避免存放庫損毀。 建立備份時省略索引和快取資料。 因此，資料來自 `crx-quickstart/repository/cache` 和 `crx-quickstart/repository/index` 未包含在備份中。 建立zip檔案時，流程的進度列指標介於0% - 70%之間，如果未建立zip檔案，則為0% - 100%。

1. 如果備份是在預先存在的目錄中進行，則會刪除目標目錄中的「舊」檔案。 舊檔案是指不存在於來源目錄中的檔案。

檔案會分四個階段複製到目標目錄：

1. 在第一個複製階段（建立zip檔案時進度指示器0% - 63%，如果未建立zip檔案，則進度指示器0% - 90%），所有檔案都會在存放庫正常執行時複製。 此程式有兩個階段：

   * 階段A — 除了資料存放區以外的所有專案都會複製（延遲）。
   * 階段B — 僅複製資料存放區（延遲）。

1. 在第二個複製階段中（建立zip檔案時進度指示器為63% - 65.8%，或是未建立zip檔案時進度指示器為90% - 94%），只會複製自第一個複製階段開始以來在來源目錄中建立或修改的檔案。 根據存放庫的活動，這可能從完全沒有檔案到大量檔案（因為第一個檔案複製階段通常需要大量時間）。 復製程式類似於第一個階段（階段A和階段B有延遲）。
1. 在第三個複製階段中（建立zip檔案時進度指示器是65.8% - 68.6%，未建立zip檔案時進度指示器是94% - 98%），只會複製第二個複製階段開始後在來源目錄中建立或修改的檔案。 根據存放庫的活動，可能沒有要複製的檔案或檔案數量非常少（因為第二個檔案複製階段通常很快）。 復製程式類似於第二個階段 — 階段A和階段B，但不會延遲。
1. 檔案複製階段一到三都會在存放庫執行時同時完成。 只會複製自第三個複製階段啟動後在來源目錄中建立或修改的檔案。 根據存放庫的活動，可能沒有要複製的檔案，或者檔案數量非常少（因為第二個檔案複製階段通常非常快）。 進度指示器68.6% - 70% （建立zip檔案時）或98% - 100% （未建立zip檔案時）。 復製程式類似於第三個階段。
1. 視目標而定：

   * 如果已指定zip檔案，現在會從暫存目錄建立它。 進度指示器70% - 100%。 然後刪除暫存目錄。
   * 如果目標是目錄，則空白檔案命名為 `backupInProgress.txt` 會刪除，表示備份已完成。

## 還原備份 {#restoring-the-backup}

您可以還原備份，如下所示：

* 如果您執行了「檔案系統快照備份」，您只需還原系統映像即可。
* 如果您將備份建立為zip檔案，只需將內容解壓縮到新資料夾中，然後從該位置啟動AEM。

## 封裝備份 {#package-backup}

若要備份和還原內容，您可以使用其中一個「封裝管理員」，它會使用「內容封裝」格式來備份和還原內容。 封裝管理程式在定義和管理封裝方面提供更大的彈性。

如需各個內容套件格式的功能和權衡的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md).

### 備份範圍 {#scope-of-backup}

當您使用封裝管理員或內容拉鍊備份節點時，CRX會儲存下列資訊：

* 您選取的樹狀結構下方的存放庫內容。
* 用於備份內容的節點型別定義。
* 用於備份內容的名稱空間定義。

備份時，AEM會遺失下列資訊：

* 版本記錄。
