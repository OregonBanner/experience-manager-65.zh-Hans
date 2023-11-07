---
title: 备份Adobe Experience Manager Forms数据
description: 本文档介绍了对Adobe Experience Manager (AEM)表单数据库、GDS和内容存储根目录进行热备份或联机备份所需的步骤。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 0%

---

# 备份Adobe Experience Manager (AEM) Forms数据 {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

本节介绍完成AEM Forms数据库、GDS和Content Storage Root目录的热备份或联机备份所需的步骤。

安装AEM Forms并将其部署到生产区域后，数据库管理员应该对数据库执行初始完全备份或冷备份。 必须关闭数据库才能进行此备份。 然后，应该定期对数据库进行差异或增量（或热）备份。

为确保成功备份和恢复，系统映像备份必须始终可用。 然后，如果发生丢失，您可以将整个环境恢复到一致状态。

在备份GDS 、 AEM资料档案库和Content Storage Root目录的同时备份数据库有助于在需要恢复时使这些系统保持同步。

本节中介绍的备份过程要求您在备份AEM Forms数据库、AEM资料档案库、GDS和内容存储根目录之前进入安全备份模式。 备份完成后，必须退出安全备份模式。 安全备份模式用于标记驻留在GDS中的长期和永久文档。 此模式可确保自动文件清理机制（文件收集器）在释放安全备份模式之前不会删除过期文件。 必须使GDS备份与数据库备份保持同步。

GDS位置必须备份的频率取决于AEM Forms的使用方式以及可用的备份窗口。 备份窗口可能会受到长期进程的影响，因为这些进程可以运行几天。 如果不断更改、添加和删除此目录中的文件，则应更频繁地备份GDS位置。

如果数据库以日志记录模式运行（如上一节所述），则还必须经常备份数据库日志，以便在发生介质故障时使用这些日志来恢复数据库。

>[!NOTE]
>
>恢复过程完成后，未引用的文件可能会保留在GDS目录中。 这是当前已知的限制。

## 备份数据库、 GDS 、 AEM存储库和内容存储根目录 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

必须将AEM Forms置于安全备份（快照）模式或滚动备份（连续覆盖）模式。 在将AEM Forms设置为进入任一备份模式之前，请确保满足以下条件：

* 验证系统版本并记录自上次执行完整系统映像备份以来应用的修补程序或更新。
* 如果使用的是滚动模式或快照模式备份，请确保为数据库配置了正确的日志设置，以允许对数据库进行热备份。 (请参阅 [AEM Forms数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

除此之外，请遵循以下备份/恢复过程指南。

* 使用可用的操作系统或第三方备份实用程序备份GDS目录。 (请参阅 [GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* （可选）使用可用的操作系统或第三方备份和实用程序备份内容存储根目录。 (请参阅 [内容存储根目录位置（独立环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 或 [内容存储根位置（群集环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* 备份创作实例和发布实例（ crx -repository备份）。

  要备份Correspondence Management Solution环境，请对创作和发布实例执行相关步骤，如中所述 [备份和恢复](/help/sites-administering/backup-and-restore.md).

  备份创作实例和发布实例时，请考虑以下几点：

   * 请确保同步创作实例和发布实例的备份，以便同时启动。 虽然在执行备份时您可以继续使用创作和发布实例，但建议不要在备份期间发布任何资产，以避免任何未捕获的更改。 等待创作实例和发布实例的备份结束，然后再发布新资产。
   * “创作”节点的完整备份包括Forms Manager和AEM Forms Workspace数据的备份。
   * Workbench开发人员可以继续在本地处理其流程。 他们不应在备份阶段部署任何新流程。
   * 应根据AEM Forms中所有数据(DB、GDS、AEM存储库和任何其他自定义数据)的备份总耗时来确定每个备份会话的长度（用于滚动备份模式）。

备份AEM Forms数据库，包括任何事务日志。 请参阅 [AEM Forms数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

有关详细信息，请参阅适用于您的数据库的知识库文章：
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [适用于AEM Forms的Oracle备份和恢复](https://www.adobe.com/go/kb403624)
* [适用于AEM Forms的MySQL备份和恢复](https://www.adobe.com/go/kb403625)
* [适用于AEM Forms的Microsoft® SQL Server备份和恢复](https://www.adobe.com/go/kb403623)
* [针对AEM Forms的DB2®备份和恢复](https://www.adobe.com/go/kb403626)

这些文章为数据的备份和恢复提供了基本的数据库功能指导。 它们并非旨在作为特定供应商的数据库备份和恢复功能的全面技术指南。 它们概述了为AEM Forms应用程序数据创建可靠的数据库备份策略所需的命令。

>[!NOTE]
>
>必须先完成数据库备份，然后才能开始备份GDS。 如果数据库备份未完成，则表示您的数据不同步。

### 进入备份模式 {#entering-the-backup-modes}

可以使用管理控制台、LCBackupMode命令或AEM Forms安装提供的API进入和退出备份模式。 对于滚动备份（连续覆盖），管理控制台选项不可用；您应使用命令行选项或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果在Forms服务器上配置了SSL，则无法使用LCBackupMode.CMD脚本将Forms服务器置于备份模式。

**使用管理控制台进入安全备份模式**

1. 登录到管理控制台。
1. 单击“设置”>“核心系统设置”>“备份实用程序”。
1. 选择“在安全备份模式下操作” ，然后单击“确定”。

   此方法会无限期地将AEM Forms置于备份模式（无超时），并且它会进入快照模式而不是滚动备份模式。

**使用命令行选项进入安全备份模式**

您可以使用命令行界面 `LCBackupMode` 用于将AEM Forms置于安全备份模式的脚本。

1. 设置ADOBELIVECYCLE并启动应用程序服务器。
1. 转到 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 文件夹。
1. 根据您的操作系统，编辑 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 脚本以提供适用于您的系统的默认值。
1. 在命令提示符下，在一行上运行以下命令：

   * (Windows) `LCBackupMode.cmd enter [-Host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `] [-label=`*标签名称* `] [-timeout=`*秒* `]`
   * (Linux®和UNIX®) `LCBackupMode.sh enter [-host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `] [-label=`*标签名称* `]`

   在前面的命令中，占位符定义如下：

   `Host` 是运行AEM Forms的主机的名称。

   `port` 是运行AEM Forms的应用程序服务器的WebServices端口。

   `user` 是AEM Forms管理员的用户名。

   `password` 是AEM Forms管理员的密码。

   `label` 是此备份的文本标签，可以是任何字符串。

   `timeout` 是自动保留备份模式的秒数。 它可以是0-10,080。 如果它为0（默认值），则备份模式不会超时。

   有关进入备份模式的命令行界面的详细信息，请参见BackupRestoreCommandline目录中的Readme文件。

### 退出备份模式 {#leaving-backup-modes}

可以使用管理控制台或命令行选项离开备份模式。

**离开安全备份模式（快照模式）**

要使用Administration Console使AEM Forms退出安全备份模式（快照模式），请执行以下任务。

1. 登录到Administration Console。
1. 单击“设置”>“核心系统设置”>“备份实用程序”。
1. 取消选择“在安全备份模式下操作” ，然后单击“确定”。

**保留所有备份模式**

您可以使用命令行界面将AEM Forms退出安全备份模式（快照模式）或结束当前备份模式会话（滚动模式）。 您不能使用管理控制台退出滚动备份模式。 在滚动备份模式中，管理控制台上的“备份实用程序”控件处于禁用状态。 使用API调用或使用LCBackupMode命令。

1. 转到 `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` 文件夹。
1. 根据您的操作系统，编辑 `LCBackupMode.cmd` 或 `LCBackupMode.sh` 脚本以提供适用于您的系统的默认值。

   >[!NOTE]
   >
   >按照以下位置中应用程序服务器的相应章节所述设置JAVA_HOME目录： [准备安装AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*.*

1. 在一行上运行以下命令：

   * (Windows) `LCBackupMode.cmd leaveContinuousCoverage [-Host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `]`
   * (Linux®和UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `]`

     在前面的命令中，占位符定义如下：

     `Host` 是运行AEM Forms的主机的名称。

     `port` 是应用程序服务器上运行AEM Forms的端口。

     `user` 是AEM Forms管理员的用户名。

     `password` 是AEM Forms管理员的密码。

     `leaveContinuousCoverage` 使用此选项可完全禁用滚动备份模式。

   >[!NOTE]
   >
   >在备份模式关闭时，不能重新建立连续覆盖。 在此期间所做的任何更改都不会受到保护。

   >[!NOTE]
   >
   >如果在数据库中启用了文档存储，则快照备份模式和滚动备份模式不适用。

   有关进入备份模式的命令行界面的详细信息，请参见BackupRestoreCommandline目录中的自述文件。
