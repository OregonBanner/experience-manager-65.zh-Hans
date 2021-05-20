---
title: 备份AEM表单数据
seo-title: 备份AEM表单数据
description: 本文档介绍完成AEM Forms数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。
seo-description: 本文档介绍完成AEM Forms数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 备份AEM表单数据{#backing-up-the-aem-forms-data}

本节介绍完成AEM Forms数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。

在将AEM表单安装并部署到生产区域后，数据库管理员应对数据库执行初始完全或冷备份。 必须关闭数据库才能进行此备份。 然后，应定期执行数据库的差异或增量（或热）备份。

为确保成功的备份和恢复，系统映像备份必须始终可用。 然后，如果发生丢失，您可以将整个环境恢复到一致的状态。

在备份数据库的同时备份GDS、AEM存储库和内容存储根目录备份有助于在需要恢复时保持这些系统同步。

本节中介绍的备份过程要求您在备份AEM Forms数据库、AEM存储库、GDS和内容存储根目录之前进入安全备份模式。 备份完成后，必须退出安全备份模式。 安全备份模式用于标记GDS中存在的长期永久文档。 此模式可确保在释放安全备份模式之前，自动文件清理机制（文件收集器）不会删除过期的文件。 必须使GDS备份与数据库备份同步。

必须备份GDS位置的频率取决于AEM表单的使用方式和备份窗口的可用性。 备份窗口可能会受到长期进程的影响，因为它们可以运行数天。 如果您不断更改、添加和删除此目录中的文件，则应更频繁地备份GDS位置。

如前一节所述，如果数据库以日志记录模式运行，则还必须频繁备份数据库日志，以便在介质出现故障时使用它们还原数据库。

>[!NOTE]
>
>恢复过程后，未引用的文件可能会保留在GDS目录中。 这是当前已知的限制。

## 备份数据库、 GDS、AEM存储库和内容存储根目录{#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

必须将AEM表单置于安全备份（快照）模式或滚动备份（连续覆盖）模式。 在将AEM表单设置为进入任一备份模式之前，请确保：

* 验证系统版本并记录自上次执行完整系统映像备份以来应用的修补程序或更新。
* 如果您使用滚动或快照模式备份，请确保数据库配置了正确的日志设置，以允许对数据库进行热备份。 (请参阅[AEM Forms数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)

除了这些之外，还要遵守以下备份/恢复过程准则。

* 使用可用的操作系统或第三方备份实用程序备份GDS目录。 （请参阅[GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location)。）
* （可选）使用可用的操作系统或第三方备份和实用程序备份内容存储根目录。 (请参阅[内容存储根位置（独立环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment)或[内容存储根位置（群集环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)。)
* 备份   创作和发布实例（crx -repository备份）。

   要备份通信管理解决方案环境，请按照[Backup and Restore](/help/sites-administering/backup-and-restore.md)中所述，对创作实例和发布实例执行步骤。

   在备份创作和发布实例时，请考虑以下几点：

   * 确保创作实例和发布实例的备份同步以同时启动。虽然在执行备份时可以继续使用创作实例和发布实例，但建议在备份期间不发布任何资产以避免任何未捕获的更改。 在发布新资产之前，请等待创作实例和发布实例的备份结束。
   * 对“创作”节点的完整备份包括对Forms Manager和AEM Forms Workspace数据的备份。
   * Workbench开发人员可以继续在本地处理其流程。 在备份阶段，他们不应部署任何新进程。
   * 每个备份会话（用于滚动备份模式）的时长取决于备份AEM表单中所有数据(DB、GDS、AEM存储库和任何其他自定义数据)所花费的总时间。

您应备份AEM表单数据库，包括任何事务日志。 (请参阅[AEM Forms数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。) 有关详细信息，请参阅数据库的相应知识库文章：

* [OracleAEM表单的备份和恢复](https://www.adobe.com/go/kb403624)
* [AEM表单的MySQL备份和恢复](https://www.adobe.com/go/kb403625)
* [AEM表单的Microsoft SQL Server备份和恢复](https://www.adobe.com/go/kb403623)
* [AEM表单的DB2备份和恢复](https://www.adobe.com/go/kb403626)

这些文章为数据备份和恢复的基本数据库功能提供了指导。 它们不是作为特定供应商数据库备份和恢复功能的全包技术指南。 它们概述了为AEM表单应用程序数据创建可靠数据库备份策略所需的命令。

>[!NOTE]
>
>在开始备份GDS之前，必须完成数据库备份。 如果数据库备份未完成，则数据将不同步。

### 进入备份模式{#entering-the-backup-modes}

您可以使用管理控制台、LCBackupMode命令或AEM Forms安装中提供的API进入和退出备份模式。 请注意，对于滚动备份（连续覆盖），管理控制台选项不可用；您应使用命令行选项或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果在Forms服务器上配置了SSL，则无法使用LCBackupMode.CMD脚本将Forms服务器置于备份模式。

**使用管理控制台进入安全备份模式**

1. 登录到管理控制台。
1. 单击设置>核心系统设置>备份实用程序。
1. 选择在安全备份模式下操作，然后单击确定。

   此方法将AEM表单无限期地置于备份模式（无超时），并进入快照模式，而不是滚动备份模式。

**使用命令行选项进入安全备份模式**

您可以使用命令行界面`LCBackupMode`脚本将AEM表单置于安全备份模式。

1. 设置ADOBELIVECYCLE并启动应用程序服务器。
1. 转到`*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`文件夹。
1. 根据您的操作系统，编辑`LCBackupMode.cmd`或`LCBackupMode.sh`脚本以提供适合您的系统的默认值。
1. 在命令提示符下，在一行上运行以下命令：

   * (Windows)`LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*用户名* `] [-password=`*密码* `] [-label=`*标签名称* `] [-timeout=`*秒* `]`
   * (Linux， UNIX)`LCBackupMode.sh enter [-host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `] [-label=`*标签名* `]`

   在以前的命令中，占位符的定义如下所示：

   `Host` 是运行AEM表单的主机的名称。

   `port` 是运行AEM表单的应用程序服务器的WebServices端口。

   `user` 是AEM表单管理员的用户名。

   `password` 是AEM表单管理员的密码。

   `label` 是用于此备份的文本标签，可以是任何字符串。

   `timeout` 是自动保留备份模式后的秒数。可以是0到10,080。 如果为0（默认为0），则备份模式永远不会超时。

   有关备份模式的命令行界面的详细信息，请参阅BackupRestoreCommandline目录中的自述文件。

### 离开备份模式{#leaving-backup-modes}

您可以使用管理控制台或命令行选项来保留备份模式。

**保持安全备份模式（快照模式）**

要使用管理控制台将AEM表单从安全备份模式（快照模式）转出，请执行以下任务。

1. 登录到管理控制台。
1. 单击设置>核心系统设置>备份实用程序。
1. 取消选择在安全备份模式下操作，然后单击“确定”。

**保留所有备份模式**

您可以使用命令行界面将AEM表单从安全备份模式（快照模式）中取出，或结束当前备份模式会话（滚动模式）。 请注意，不能使用管理控制台退出滚动备份模式。 在滚动备份模式下，“管理控制台”上的“备份实用程序”控件处于禁用状态。 您必须使用API调用或使用LCBackupMode命令。

1. 转到`*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`文件夹。
1. 根据您的操作系统，编辑`LCBackupMode.cmd`或`LCBackupMode.sh`脚本以提供适合您的系统的默认值。

   >[!NOTE]
   >
   >必须按照[准备安装AEM表单](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*中应用程序服务器的相应章节中所述设置JAVA_HOME目录。*

1. 在一行中运行以下命令：

   * (Windows)`LCBackupMode.cmd leaveContinuousCoverage [-Host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `]`
   * (Linux， UNIX)`LCBackupMode.sh leaveContinuousCoverage [-Host=`*主机名* `] [-port=`*端口号* `] [-user=`*用户名* `] [-password=`*密码* `]`

      在以前的命令中，占位符的定义如下所示：

      `Host` 是运行AEM表单的主机的名称。

      `port` 是应用程序服务器上运行AEM表单的端口。

      `user` 是AEM表单管理员的用户名。

      `password` 是AEM表单管理员的密码。

      `leaveContinuousCoverage` 使用此选项可完全禁用滚动备份模式。
   >[!NOTE]
   >
   >在备份模式关闭时，无法重新建立连续覆盖。 在此期间的任何更改都不受保护。

   >[!NOTE]
   >
   >如果在数据库中启用了文档存储，则快照备份模式和滚动备份模式不适用。

   有关备份模式的命令行界面的详细信息，请参阅BackupRestoreCommandline目录中的自述文件。
