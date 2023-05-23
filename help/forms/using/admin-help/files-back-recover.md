---
title: 要備份和復原的檔案
seo-title: Files to back up and recover
description: 本檔案說明必須備份的應用程式和資料檔案。
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---

# 要備份和復原的檔案 {#files-to-back-up-and-recover}

以下各節將更詳細地說明必須備份的應用程式和資料檔案。

請考量下列有關備份與回覆的要點：

* 資料庫應在GDS和AEM儲存庫之前進行備份。
* 如果您需要關閉叢集叢集環境中的節點以進行備份，請確定次要節點在主要節點之前關閉。 否則，可能會導致叢集或伺服器中的不一致。 此外，主要節點應在任何次要節點之前上線。
* 若要執行叢集的還原作業，叢集中的每個節點都應該停止應用程式伺服器。

## 全域檔案儲存目錄 {#global-document-storage-directory}

GDS是用來儲存處理序中使用的長期檔案的目錄。 長效檔案的存留期旨在橫跨一或多個AEM表單系統的啟動，並可橫跨數天甚至數年。 這些長效檔案可包含PDF、原則和表單範本。 長效檔案是許多AEM表單部署整體狀態的關鍵部分。 如果部分或所有長期檔案遺失或損毀，表單伺服器可能會變得不穩定。

非同步作業引動的輸入檔案也會儲存在GDS中，而且必須可用於處理請求。 因此，請務必考量裝載GDS的檔案系統的可靠性，並採用獨立磁碟備援陣列(RAID)或其他適合您品質和服務等級要求的技術。

GDS的位置是在AEM Forms安裝過程中或之後使用管理主控台確定的。 除了保留GDS的高可用性位置之外，您還可以啟用檔案的資料庫儲存。 另請參閱 [當資料庫用於檔案儲存時的備份選項](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS位置 {#gds-location}

如果您在安裝期間將位置設定保留為空白，則該位置會預設為應用程式伺服器安裝下的目錄。 您必須為應用程式伺服器備份下列目錄：

* (JBos) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果您將GDS位置變更為非預設位置，您可以依照以下方式加以確定：

* 登入管理主控台，然後按一下「設定>核心系統設定>設定」。
* 記錄在「全域檔案儲存目錄」方塊中指定的位置。

在叢集環境中，GDS通常會指向網路上共用的目錄，而且每個叢集節點都可以讀取/寫入存取該目錄。

如果原始位置不再可用，則在復原期間可能會變更GDS的位置。 (請參閱 [在復原期間變更GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### 當資料庫用於檔案儲存時的備份選項 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理主控台在AEM表單資料庫中啟用AEM表單檔案儲存。 即使此選項會保留資料庫中的所有永久檔案，AEM表單仍需要檔案系統型GDS目錄，因為它可用來儲存與工作階段和AEM表單呼叫相關的永久和暫存檔及資源。

當您在管理主控台的「核心系統設定」中選取「啟用資料庫中的檔案儲存」選項，或使用Configuration Manager時，AEM Forms不允許快照備份模式和復原備份模式。 因此，您不需要使用AEM表單管理備份模式。 如果您使用此選項，您應在啟用選項後，只備份一次GDS。 當您從備份復原AEM表單時，不需要重新命名GDS的備份目錄或還原GDS。

## AEM存放庫 {#aem-repository}

如果在安裝AEM表單時配置了crx-repository，則會建立AEM存放庫(crx-repository)。 crx-repository目錄的位置是在AEM表單安裝過程中確定的。 AEM儲存庫需要備份與還原，以及資料庫和GDS，以在AEM表單中保持一致AEM表單資料。 AEM存放庫包含Correspondence Management Solution、Forms Manager和AEM Forms Workspace的資料。

### 通訊管理解決方案 {#correspondence-management-solution}

Correspondence Management Solution可集中管理安全、個人化及互動式通訊的建立、集合及傳遞。 它可讓您以從建立到封存的簡化流程，快速組合來自預先核准和自訂編寫內容的通訊。 因此，您的客戶可獲得及時、準確、方便、安全且相關的通訊。 您的企業透過簡化流程以輕鬆、快速和生產力，將客戶互動的價值最大化，並將成本和風險降至最低。

簡單的Correspondence Management Solution設定包含相同電腦或不同電腦上的作者執行個體和發佈執行個體

### 表單管理員 {#forms-manager}

forms manager可簡化更新、管理和淘汰表單的程式。

### AEM Forms工作區 {#html-workspace}

AEM Forms Workspace符合(JEE已針對AEM Forms棄用) Flex Workspace的功能，並新增新功能以擴充和整合Workspace，並使其更人性化。

>[!NOTE]
>
>AEM Forms版本已棄用Flex Workspace。

它允許在沒有Flash Player和Adobe Reader的使用者端上進行任務管理。 除了PDF forms和Flex表單外，它還有助於轉譯HTMLForms。

## AEM forms資料庫 {#aem-forms-database}

AEM Forms資料庫會儲存內容，例如表單人工因素、服務設定、程式狀態，以及對GDS和內容儲存根目錄（適用於內容服務）中檔案的資料庫參考。 資料庫備份可以在不中斷服務的情況下即時執行，並且復原可以到特定時間點或特定變更。 本節說明如何設定資料庫，以便可以即時備份。

在正確設定的AEM表單系統上，系統管理員和資料庫管理員可以輕鬆地共同作業，將系統復原到一致的已知狀態。

若要即時備份資料庫，您必須使用快照模式，或設定資料庫以指定的記錄模式執行。 這可在資料庫開啟且可供使用時，備份您的資料庫檔案。 此外，當資料庫在這些模式中執行時，會保留其倒回和異動記錄。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES （已棄用）是隨LiveCycle安裝的內容管理系統。 它可讓使用者設計、管理、監控及最佳化以人為中心的流程。 內容服務（已棄用）支援將於2014年12月31日終止。 另請參閱 [Adobe產品生命週期檔案](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

設定DB2資料庫以存檔記錄模式執行。

>[!NOTE]
>
>如果您的AEM表單環境是從舊版AEM表單升級而來，並使用DB2，則不支援線上備份。 在這種情況下，您必須關閉AEM表單並執行離線備份。 未來版本的AEM Forms將支援升級客戶的線上備份。

IBM有一套工具和說明系統，可協助資料庫管理員管理其備份與復原工作：

* IBM DB2封存日誌加速器
* IBM DB2資料封存專家

DB2具有將資料庫備份至Tivoli Storage Manager的內建功能。 使用Tivoli Storage Manager，DB2備份可以儲存在其他媒體或本機硬碟上。

### oracle {#oracle}

使用快照備份或設定Oracle資料庫以存檔日誌模式執行。 (請參閱 [oracle備份：簡介](https://www.databasedesign-resource.com/oracle-backup.md).) 如需有關備份和復原Oracle資料庫的詳細資訊，請前往下列網站：

[oracle備份與復原：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 詳細說明備份與復原的概念，以及使用Recovery Manager (RMAN)進行備份、復原與報告的最常見技術，並提供有關如何規劃備份與復原策略的詳細資訊。

[oracle Database Backup and Recovery使用手冊：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供有關RMAN架構、備份與復原概念與機制、進階復原技術（例如時間點復原與資料庫倒溯功能）以及備份與復原效能調校的深入資訊。 此外，也涵蓋使用者管理的備份與復原，使用主機作業系統設施，而非RMAN。 此磁碟區對於更複雜的資料庫部署以及進階復原情況的備份與復原是必要的。

[oracle資料庫備份與復原參考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供所有RMAN指令的語法和語意的完整資訊，並說明可用於報告備份與復原活動的資料庫檢視。

### SQL Server {#sql-server}

使用快照備份或設定SQL Server資料庫以交易記錄模式執行。

SQL Server還提供兩種備份與復原工具：

* SQL Server Management Studio (GUI)
* T-SQL （命令列）

如需詳細資訊，請參閱 [備份與還原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

使用MySQLAdmin或修改Windows中的INI檔案，將MySQL資料庫設定為以二進位記錄模式執行。 (請參閱 [MySQL二進位記錄](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) InnoBase軟體也提供MySQL的熱備份工具。 (請參閱 [Innobase熱備份](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
>MySQL的預設二進位記錄模式是「陳述式」，與Content Services使用的表格不相容（已棄用）。 在此預設模式下使用二進位記錄會導致Content Services (Deprecated)失敗。 如果您的系統包含Content Services （已棄用），請使用「混合」記錄模式。 若要啟用「混合」記錄，請將下列引數新增至my.ini檔案： `binlog_format=mixed log-bin=logname`

您可以使用mysqldump公用程式來取得完整的資料庫備份。 需要完整備份，但並不總是很方便。 它們會產生大型備份檔案，並需要時間才能產生。 若要執行增量備份，請確定您啟動伺服器的方式為 —  `log-bin` 選項，如上一節所述。 每當MySQL伺服器重新啟動時，就會停止寫入目前的二進位記錄檔，建立新的記錄檔，從那時起，新的記錄檔就會變成目前的記錄檔。 您可以使用手動強制切換 `FLUSH LOGS SQL` 命令。 第一次完整備份後，後續的增量備份會使用mysqladmin公用程式搭配 `flush-logs` 指令，建立下一個記錄檔。

另請參閱 [備份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## 內容儲存根目錄（僅限內容服務） {#content-storage-root-directory-content-services-only}

「內容儲存根目錄」包含Content Services (Deprecated)存放庫，其中儲存所有檔案、成品和索引。 必須備份內容儲存根目錄樹狀結構。 本節說明如何為獨立和叢集環境決定內容儲存根目錄的位置。

### 內容儲存根目錄位置（獨立環境） {#content-storage-root-location-stand-alone-environment}

內容儲存根目錄是在安裝Content Services (Deprecated)時建立。 內容儲存根目錄的位置是在AEM Forms安裝過程中確定的。

內容儲存根目錄的預設位置為 `[aem-forms root]/lccs_data`.

備份下列位於內容儲存根目錄的目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-index

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，請勿備份/lucene-indexes目錄，因為它可能會導致錯誤。

### 內容儲存根目錄位置（叢集環境） {#content-storage-root-location-clustered-environment}

當您在叢集環境中安裝Content Services （已棄用）時，內容儲存根目錄會分割成兩個不同的目錄：

**內容儲存根目錄：** 一般而言，叢集中所有節點都可以讀取/寫入存取的共用網路目錄

**索引根目錄：** 在叢集中的每個節點上建立的目錄，一律有相同的路徑和目錄名稱

內容儲存根目錄的預設位置為 `[GDS root]/lccs_data`，其中 `[GDS root]` 是中說明的位置 [GDS位置](files-back-recover.md#gds-location). 備份下列位於內容儲存根目錄的目錄：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-index

如果/backup-lucene-indexes目錄不存在，請備份/lucene-indexes目錄，該目錄也位於內容儲存根目錄中。 如果/backup-lucene-indexes目錄存在，請勿備份/lucene-indexes目錄，因為它可能會導致錯誤。

「索引根目錄」的預設位置為 `[aem-forms root]/lucene-indexes` 在每個節點上。

## 客戶安裝的字型 {#customer-installed-fonts}

如果您在AEM表單環境中安裝了其他字型，則必須個別進行備份。 備份Administration Console中「設定>核心系統>設定」下指定的所有Adobe和客戶字型目錄。 請確定您備份了整個字型目錄。

>[!NOTE]
>
>依預設，隨AEM表單安裝的Adobe字型位於 `[aem-forms root]/fonts` 目錄。

如果您正在重新初始化主機電腦上的作業系統，並且想要使用上一個作業系統的字型，則系統字型目錄的內容也應備份。 （如需特定指示，請參閱作業系統的檔案）。
