---
title: 備份和復原EMC Documentum存放庫
seo-title: Backing up and recovering the EMC Documentum repository
description: 本檔案說明備份和復原為您的AEM表單環境設定的EMC Documentum存放庫所需的工作。
seo-description: This document describes the tasks required to back up and recover the EMC Documentum repository configured for your AEM forms environment.
uuid: ab3b1fb1-25b3-4c95-801f-82d4b58f05ff
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f146202f-25f1-46a0-9943-c483f5f09f9f
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 備份和復原EMC Documentum存放庫 {#backing-up-and-recovering-the-emc-documentum-repository}

本節說明備份和復原為您的AEM Forms環境設定的EMC Documentum存放庫所需的工作。

>[!NOTE]
>
>這些指示假設已視需要安裝並設定AEM forms with Connectors for ECM和EMC Documentum Content Server。

對於備份和還原程式，有兩個主要工作：

* 備份（或還原） AEM表單環境。
* 備份（或還原） EMC Documentum Content Server。

>[!NOTE]
>
>在備份EMC Documentum系統之前，請先備份AEM表單資料，接著在還原AEM表單環境之前還原EMC Documentum系統。

## 軟體需求 {#software-requirements}

若要在EMC Documentum Content Server上執行必要的備份工作，請從EMC購買適當的第三方公用程式，例如EMC NetWorker，或從CYA購買適用於EMC Documentum的CYA SmartRecovery。 下列指示說明使用EMC NetWorker Module 7.2.2版的步驟。

您需要下列EMC NetWorker模組：

* NetWorker模組
* NetWorker設定精靈
* NetWorker裝置設定精靈
* NetWorker Module，適用於您的Content Server使用的資料庫型別
* Networker Module for Documentum

## 準備EMC Document Content Server以進行備份和復原 {#preparing-the-emc-document-content-server-for-backup-and-recovery}

本節說明如何在Content Server上安裝和設定EMC NetWorker軟體。

**準備EMC Documentum伺服器以進行備份**

1. 在EMC Documentum Content Server上，安裝EMC NetWorker模組，接受所有預設值。

   在安裝過程中，系統會提示您輸入Content Server電腦的伺服器名稱作為 *NetWorker伺服器名稱*. 為資料庫安裝EMC NetWorker Module時，請選擇「完整」安裝。

1. 使用以下範例內容，建立名為的設定檔 *nsrnmd_win.cfg* 並儲存至Content Server上可存取的位置。 備份與還原命令會呼叫此檔案。

   下列文字包含分行符號的格式字元。 如果您將此文字複製到此檔案以外的位置，請一次複製一個部分，並在您將文字貼到新位置時移除格式設定字元。

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # Please refer to the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   保留設定檔密碼欄位 `NMDDE_DM_PASSWD` 空白。 您將在下一個步驟中設定密碼。

1. 設定組態檔密碼，如下所示：

   * 開啟命令提示字元並變更為 `[NetWorker_root]\Legato\nsr\bin`.
   * 執行以下命令： `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. 建立用來備份資料庫的可執行批次(.bat)檔案。 （請參閱NetWorker檔案）。 根據您的安裝設定批次檔案中的詳細資訊。

   * 完整資料庫備份(nsrnmddbf.bat)：

      `NetWorker_database_module_root` `-s`*&lt;networker_server_name>* `-U``[username]` `-P`*[密碼&#x200B;]*`-l full`*&lt;database_name>*

   * 增量資料庫備份(nsrnmddbi.bat)：

      `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * 資料庫記錄備份(nsrnmddbl.bat)：

      `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

      其中：

      `[NetWorker_database_module_root]` 是NetWorker模組的安裝目錄。 例如，NetWorker Module for SQL Server的預設安裝目錄為C:\Program Files\Legato\nsr\bin\nsrsqlsv。

      `NetWorker_Server_Name` 是安裝NetWorker的伺服器。

      `username` 和 `password` 是資料庫管理員使用者的使用者名稱和密碼。

      `database_name` 是要備份的資料庫名稱。

**建立備份裝置**

1. 在EMC Documentum伺服器上建立新目錄，並透過授予所有使用者完整許可權來共用資料夾。
1. 啟動「EMC NetWorker管理員」，然後按一下「媒體管理>裝置」。
1. 以滑鼠右鍵按一下裝置，然後選取建立。
1. 輸入下列值，然後按一下「確定」：

   **名稱：** 共用目錄的完整路徑

   **媒體型別：** `File`

1. 在新裝置上按一下滑鼠右鍵，然後選取操作。
1. 按一下「標籤」，輸入名稱，按一下「確定」，然後按一下「掛載」。

新增要儲存已備份檔案的裝置。 您可以新增多種不同格式的裝置。

## 備份EMC Documentum Content Server {#back-up-the-emc-documentum-content-server}

完成AEM表單資料的完整備份後，請執行以下工作。 (請參閱 [備份AEM表單資料](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data).)

>[!NOTE]
>
>命令指令碼需要您在中建立的nsrnmd_win.cfg檔案的完整路徑 [準備EMC Document Content Server以進行備份和復原](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. 開啟命令提示字元並變更為 `[NetWorker_root]\Legato\nsr\bin`.
1. 執行以下命令：

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## 還原EMC Documentum Content Server {#restore-the-emc-documentum-content-server}

還原AEM表單資料之前，請執行以下工作。 (請參閱 [復原AEM表單資料](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data).)

>[!NOTE]
>
>命令指令碼需要您在中建立的nsrnmd_win.cfg檔案的完整路徑 [準備EMC Document Content Server以進行備份和復原](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery).

1. 停止正在還原的Docbase服務。
1. 啟動資料庫模組的NetWorker使用者公用程式(例如， *NetWorker User for SQL Server*)。
1. 按一下「還原」工具，然後選取「一般」。
1. 在畫面左側，選取檔案庫的資料庫，然後按一下工具列上的「開始」按鈕。
1. 還原資料庫時，請重新啟動Docbase服務。
1. 開啟命令提示字元並變更為 *[NetWorker_root]*\Legato\nsr\bin
1. 執行以下命令：

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
