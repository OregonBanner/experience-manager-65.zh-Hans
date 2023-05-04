---
title: 恢复AEM表单数据
seo-title: Recovering the AEM forms data
description: 本文档介绍了恢复AEM表单数据所需的步骤。
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

# 恢复AEM表单数据 {#recovering-the-aem-forms-data}

本节介绍恢复AEM表单数据所需的步骤。 另请参阅 [备份和恢复的特殊注意事项](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>必须将数据库、 GDS、AEM存储库和内容存储根目录还原到与原始DNS名称相同的计算机。

AEM表单应可靠地从以下故障中恢复：

**磁盘故障：** 恢复数据库内容需要最新的备份介质。

**数据损坏：** 文件系统不会记录过去的事务，并且系统可能会意外覆盖所需的进程数据。

**用户错误：** 恢复仅限于数据库提供的数据。 如果数据已存储且可用，则恢复过程会得到简化。

**断电，系统崩溃：** 文件系统API的设计或使用通常不是以一种可靠的方式来防止意外的系统故障。 如果发生断电或系统崩溃，则存储在数据库中的文档内容比存储在文件系统中的内容更有可能是最新的。

如果您使用滚动备份模式，则恢复后仍处于备份模式。 如果您使用快照备份模式，则恢复后不处于备份模式。

从备份还原到新系统时，以下配置可能有所不同。 此差异不应影响AEM表单应用程序的成功恢复：

* IP地址
* 物理系统配置（CPU、磁盘、内存）
* GDS位置

>[!NOTE]
>
>必须将内容存储根目录的备份还原到该目录的位置，因为该目录是在内容服务配置期间设置的。

如果多节点群集的单个节点出现故障，且该群集的其余节点运行正常，则执行群集单节点恢复过程。

## 恢复AEM表单数据 {#recover-the-aem-forms-data}

1. 如果运行，请停止AEM Forms服务和应用程序服务器。
1. 如有必要，从系统映像重新创建物理系统。 例如，如果恢复原因是数据库服务器故障，则可能不需要此步骤。
1. 将补丁或更新应用于自创建图像以来应用的AEM表单。 此信息已记录在备份过程中。 必须将AEM表单打补丁到与备份系统时相同的补丁程序级别。
1. (WebSphere®应用程序服务器)如果要恢复到WebSphere®应用程序服务器的新实例，请运行restoreConfig.bat/sh命令。
1. 恢复AEM表单数据库的方法是：首先使用数据库备份文件运行数据库还原操作，然后将事务重做日志应用到恢复的数据库。 (请参阅 [AEM forms数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 有关更多信息，请参阅以下知识库文章之一：

   * [DB2](/help/forms/using/admin-help/files-back-recover.md#db2)
   * [OracleAEM表单的备份和恢复](/help/forms/using/admin-help/files-back-recover.md#oracle)
   * [Microsoft](/help/forms/using/admin-help/files-back-recover.md#sql-server)
   * [AEM表单的MySQL备份和恢复](/help/forms/using/admin-help/files-back-recover.md#mysql)

1. 恢复GDS目录，方法是先删除现有AEM表单安装上GDS目录的内容，然后从备份的GDS中复制GDS目录的内容。 如果更改了GDS目录位置，请参阅 [在恢复期间更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. 重命名要还原的GDS备份目录，如以下示例所示：

   >[!NOTE]
   >
   >如果/restore目录已存在，请先将其备份，然后将其删除，然后再重命名包含最新数据的/backup目录。

   * (JBoss®)重命名 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 至：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`。

   * (WebLogic)重命名 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 至：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`。

   * (WebSphere®)重命名 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 至：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`。

1. 恢复内容存储根目录，方法是先删除现有AEM表单安装上的内容存储根目录的内容，然后按照独立或群集环境的任务恢复内容：

   >[!NOTE]
   >
   >必须将内容存储根目录的备份还原到内容存储根目录的位置，因为该目录是在内容服务（已弃用）配置期间设置的。

   **独立：** 在恢复过程中，恢复所有备份的目录。 在恢复这些目录时，如果存在/backup-lucene-indexes目录，请将其重命名为/lucene-indexes。 否则，lucene-indexes目录应已存在，无需执行任何操作。

   **群集：** 在恢复过程中，恢复所有备份的目录。 要恢复索引根目录，请对群集的每个节点执行以下步骤：

   * 删除“索引根”目录中的所有内容。
   * 如果/backup-lucene-indexes目录存在，请复制 *内容存储根目录*/backup-lucene-indexes目录到索引根目录，并删除 *内容存储根目录*/backup-lucene-indexes目录。
   * 如果/lucene-indexes目录存在，请复制 *内容存储根目录*/lucene-indexes目录到索引根目录。

1. 恢复/恢复CRX存储库。

   * **独立**

      *恢复创作和发布实例*:如果发生灾难，您可以通过执行 [备份和恢复。](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)

      完全恢复“创作”节点也可确定恢复Forms Manager和AEM Forms Workspace数据。

   * **群集**

      有关在群集环境中恢复的信息，请参阅 [在群集环境中备份和恢复的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. 删除之前在java.io.temp目录或AEM临时目录中创建的任何Adobe表单临时文件。
1. 启动AEM表单(请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->.

## 在恢复期间更改GDS位置 {#changing-the-gds-location-during-recovery}

如果您的GDS被恢复到原来位置以外的位置，请运行LCSetGDS脚本以将GDS设置为新位置。 脚本位于 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 文件夹。 脚本包含两个参数， `defaultGDS` 和 `newGDS`. 请参阅 `ReadMe.txt` 文件，以获取有关如何运行脚本的说明。

>[!NOTE]
>
>如果已在数据库中启用文档存储，则无需更改GDS位置。

>[!NOTE]
>
>这种情况是您唯一应使用此脚本更改GDS位置的情况。 要在AEM表单运行时更改GDS位置，请使用管理控制台。 (请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).)

>[!NOTE]
>
>如果GDS目录位于驱动器根目录(例如D:\)，则Windows上的组件部署将失败。 对于GDS，必须确保目录不位于驱动器的根目录，而位于子目录中。 例如，目录应为D:\GDS and not simply D:\。

## 将GDS恢复到群集环境 {#recovering-the-gds-to-a-clustered-environment}

要在群集环境中更改GDS位置，请关闭整个群集并在群集的单个节点上运行LCSetGDS脚本。 (请参阅 [在恢复期间更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) 仅启动该节点。 当该节点完全启动时，群集中的其他节点可能会安全启动，并将正确指向新的GDS。

>[!NOTE]
>
>如果无法确保在启动其他节点之前完全启动一个节点，则必须在启动群集之前对群集中的每个节点运行LCSetGDS脚本。
