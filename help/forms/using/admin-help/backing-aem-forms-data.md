---
title: 备份AEM表单数据
seo-title: 备份AEM表单数据
description: 本文档描述完成AEM表单数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。
seo-description: 本文档描述完成AEM表单数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 备份AEM表单数据 {#backing-up-the-aem-forms-data}

本节介绍完成AEM表单数据库、GDS和内容存储根目录的热备份或联机备份所需的步骤。

在将AEM表单安装并部署到生产区域后，数据库管理员应对数据库执行初始完整或冷备份。 此备份必须关闭数据库。 然后，应定期执行数据库的差异或增量（或热）备份。

要确保备份和恢复成功，系统映像备份必须始终可用。 然后，如果发生损失，您可以将整个环境恢复到一致的状态。

在备份GDS、AEM存储库和内容存储根目录的同时备份数据库有助于在需要恢复时保持这些系统的同步。

本节中介绍的备份过程要求您在备份AEM表单数据库、AEM存储库、GDS和内容存储根目录之前进入安全备份模式。 备份完成后，您必须退出安全备份模式。 安全备份模式用于标记驻留在GDS中的长期和永久文档。 此模式可确保自动文件清除机制（文件收集器）在释放安全备份模式之前不会删除过期的文件。 必须使GDS备份与数据库备份保持同步。

必须备份GDS位置的频率取决于AEM表单的使用方式和备份窗口的可用性。 备份窗口可能会受到长期进程的影响，因为它们可以运行数天。 如果您不断更改、添加和删除此目录中的文件，您应更频繁地备份GDS位置。

如果数据库以记录模式运行（如上一节所述），则数据库日志还必须经常备份，以便在介质出现故障时用于恢复数据库。

>[!NOTE]
>
>恢复过程后，未引用的文件可能会保留在GDS目录中。 这是目前已知的限制。

## 备份数据库、GDS、AEM存储库和内容存储根目录 {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

必须将AEM表单置于安全备份（快照）模式或滚动备份（连续覆盖）模式。 在将AEM表单设置为进入任一备份模式之前，请确保：

* 验证系统版本，并记录自上次完成系统映像备份后应用的修补程序或更新。
* 如果您使用滚动或快照模式备份，请确保您的数据库配置了正确的日志设置，以允许对数据库进行热备份。 (请参 [阅AEM表单数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)

除了这些，还要遵守以下备份／恢复过程准则。

* 使用可用的操作系统或第三方备份实用程序备份GDS目录。 (请参阅 [GDS位置](/help/forms/using/admin-help/files-back-recover.md#gds-location)。)
* （可选）使用可用的操作系统或第三方备份和实用程序备份内容存储根目录。 (请参 [阅内容存储根目录位置（独立环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) 或内 [容存储根目录位置（群集环境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)。)
* 备份创作和发布实例（crx -repository备份）。

   要备份Correponse Management Solution环境，请按照备份和还原中所述对创作和发布实例执行 [步骤](/help/sites-administering/backup-and-restore.md)。

   备份作者实例和发布实例时，请考虑以下几点：

   * 确保创作和发布实例的备份同步以同时启动。尽管在执行备份时可以继续使用作者实例和发布实例，但建议在备份过程中不要发布任何资产以避免任何未捕获的更改。 在发布新资产之前，请等待作者实例和发布实例的备份结束。
   * “作者”节点的完整备份包括Forms manager和AEM Forms Workspace数据的备份。
   * 工作台开发人员可以继续在本地处理其流程。 他们不应在备份阶段部署任何新进程。
   * 每个备份会话的长度（用于滚动备份模式）的决定应基于备份AEM表单（DB、GDS、AEM存储库和任何其他自定义数据）中所有数据所花费的总时间。

您应备份AEM表单数据库，包括任何事务日志。 (请参 [阅AEM表单数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)有关详细信息，请参阅数据库的相应知识库文章：

* [针对AEM表单的Oracle备份和恢复](https://www.adobe.com/go/kb403624)
* [针对AEM表单的MySQL备份和恢复](https://www.adobe.com/go/kb403625)
* [针对AEM表单的Microsoft SQL server备份和恢复](https://www.adobe.com/go/kb403623)
* [AEM表单的DB2备份和恢复](https://www.adobe.com/go/kb403626)

这些文章为备份和恢复数据提供了基本的数据库功能指导。 它们并非作为特定供应商的数据库备份和恢复功能的全包技术指南。 它们概述了为AEM表单应用程序数据创建可靠的数据库备份策略所需的命令。

>[!NOTE]
>
>在开始备份GDS之前，数据库备份必须完成。 如果数据库备份未完成，则您的数据将不同步。

### 进入备份模式 {#entering-the-backup-modes}

您可以使用管理控制台、LCBackupMode命令或AEM表单安装附带的API进入和退出备份模式。 请注意，对于滚动备份（连续覆盖），管理控制台选项不可用；您应使用命令行选项或API。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>如果在表单服务器上配置了SSL，则无法使用LCBackupMode.CMD脚本将表单服务器置于备份模式。

**使用管理控制台进入安全备份模式**

1. 登录到管理控制台。
1. 单击“设置”>“核心系统设置”>“备份实用程序”。
1. 选择“在安全备份模式下操作”，然后单击“确定”。

   此方法将AEM表单无限期地置于备份模式（不会超时），并进入快照模式而不是滚动备份模式。

**使用命令行选项进入安全备份模式**

您可以使用命令行界面脚 `LCBackupMode` 本将AEM表单置于安全备份模式。

1. 设置ADOBE_LIVECYCLE并启动应用程序服务器。
1. Go to the `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` folder.
1. 根据您的操作系统，编辑或 `LCBackupMode.cmd` 脚本以 `LCBackupMode.sh` 提供适合您的系统的默认值。
1. 在命令提示符下，在单行上运行以下命令：

   * (Windows)hostname `LCBackupMode.cmd enter [-Host=`*hostname *`] [-port=`*hostnameNumber用户名* 密码 `] [-user=`**`] [-password=`**`] [-label=`**`] [-timeout=`** LabelelName（秒） `]`
   * (Linux, UNIX)hostname `LCBackupMode.sh enter [-host=`*主机名&#x200B;*、`] [-port=`*机*`] [-user=`*名&#x200B;*用户名`] [-password=`*密码* passwordLabelname `] [-label=`**Unix`]`
   在以前的命令中，占位符的定义如下：

   `Host` 是运行AEM表单的主机的名称。

   `port` 是运行AEM表单的应用程序服务器的WebServices端口。

   `user` 是AEM表单管理员的用户名。

   `password` 是AEM表单管理员的口令。

   `label` 是此备份的文本标签，可以是任何字符串。

   `timeout` 是备份模式自动保留的秒数。 可以是0到10,080。 如果为0（这是默认值），则备份模式不会超时。

   有关备份模式的命令行界面的详细信息，请参阅BackupRestoreCommandline目录中的自述文件。

### 退出备份模式 {#leaving-backup-modes}

您可以使用管理控制台或命令行选项来保留备份模式。

**保持安全备份模式（快照模式）**

要使用Administration Console将AEM表单从安全备份模式（快照模式）转出，请执行以下任务。

1. 登录到管理控制台。
1. 单击“设置”>“核心系统设置”>“备份实用程序”。
1. 取消选择“在安全备份模式下操作”，然后单击“确定”。

**保留所有备份模式**

您可以使用命令行界面将AEM表单转出安全备份模式（快照模式）或结束当前备份模式会话（滚动模式）。 请注意，不能使用管理控制台退出滚动备份模式。 在滚动备份模式下，“管理”控制台上的“备份实用程序”控件被禁用。 必须使用API调用或使用LCBackupMode命令。

1. Go to the `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` folder.
1. 根据您的操作系统，编辑或 `LCBackupMode.cmd` 脚本以 `LCBackupMode.sh` 提供适合您的系统的默认值。

   >[!NOTE]
   >
   >必须按照准备安装AEM表单中应用程序服务器的相应章节中所述设置JAVA_HOME [目录](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)*。*

1. 在单行上运行以下命令：

   * (Windows)hostname `LCBackupMode.cmd leaveContinuousCoverage [-Host=`**hostname`] [-port=`** portnumber `] [-user=`**password`] [-password=`** username `]`
   * (Linux, UNIX)hostname `LCBackupMode.sh leaveContinuousCoverage [-Host=`**`] [-port=`*portnumber用户名*`] [-user=`*密码&#x200B;*`] [-password=`*(* password password) `]`

      在以前的命令中，占位符的定义如下：

      `Host` 是运行AEM表单的主机的名称。

      `port` 是AEM表单在应用程序服务器上运行时所在的端口。

      `user` 是AEM表单管理员的用户名。

      `password` 是AEM表单管理员的口令。

      `leaveContinuousCoverage` 使用此选项可完全禁用滚动备份模式。
   >[!NOTE]
   >
   >在关闭备份模式时，无法重新建立连续覆盖。 在此期间的任何更改都不受保护。

   >[!NOTE]
   >
   >如果在数据库中启用了文档存储，则快照备份模式和滚动备份模式不适用。

   有关备份模式的命令行界面的详细信息，请参阅BackupRestoreCommandline目录中的自述文件。

