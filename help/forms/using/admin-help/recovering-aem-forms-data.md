---
title: 恢复AEM表单数据
seo-title: 恢复AEM表单数据
description: 本文档介绍恢复AEM表单数据所需的步骤。
seo-description: 本文档介绍恢复AEM表单数据所需的步骤。
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 恢复AEM表单数据 {#recovering-the-aem-forms-data}

本节介绍恢复AEM表单数据所需的步骤。 另请参 [阅备份和恢复的特殊注意事项](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)。

>[!NOTE]
>
>必须将数据库、GDS、AEM存储库和内容存储根目录还原到与原始DNS名称相同的计算机。

AEM表单应可靠地从以下故障中恢复：

**磁盘故障：** 恢复数据库内容需要使用最新的备份介质。

**数据损坏：** 文件系统不会记录过去的事务，并且系统可能会意外覆盖所需的进程数据。

**用户错误：** 恢复仅限于数据库提供的数据。 如果数据已存储且可用，则恢复将得到简化。

**停电，系统崩溃：** 文件系统API通常不能以可靠的方式设计或使用，以防止意外的系统故障。 如果发生停电或系统崩溃，则存储在数据库中的文档内容比存储在文件系统中的内容更可能是最新的。

如果使用滚动备份模式，则恢复后仍处于备份模式。 如果您使用快照备份模式，则恢复后不处于备份模式。

从备份恢复到新系统时，以下配置可能不同。 此差异不应影响AEM表单应用程序的成功恢复：

* IP地址
* 物理系统配置（CPU、磁盘、内存）
* GDS位置

>[!NOTE]
>
>内容存储根目录的备份必须恢复到该目录在内容服务配置过程中设置的位置。

如果多节点群集的单个节点发生故障，且群集的其余节点正常运行，则执行群集单节点恢复过程。

## 恢复AEM表单数据 {#recover-the-aem-forms-data}

1. 如果运行，则停止AEM表单服务和应用程序服务器。
1. 如有必要，从系统映像重新创建物理系统。 例如，如果恢复的原因是有故障的数据库服务器，则可能不需要执行此步骤。
1. 将修补程序或更新应用到自创建图像以来应用的AEM表单。 此信息记录在备份过程中。 必须将AEM表单修补到与备份系统时相同的修补级别。
1. （WebSphere应用程序服务器）如果要恢复到WebSphere应用程序服务器的新实例，请运行restoreConfig.bat/sh命令。
1. 通过首先使用数据库备份文件运行数据库恢复操作，然后将事务重做日志应用到恢复的数据库，恢复AEM表单数据库。 (请参 [阅AEM表单数据库](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)。)有关详细信息，请参阅以下知识库文章之一：

   * [针对AEM表单的Oracle备份和恢复](https://www.adobe.com/go/kb403624)
   * [针对AEM表单的MySQL备份和恢复](https://www.adobe.com/go/kb403625)
   * [针对AEM表单的Microsoft SQL Server备份和恢复](https://www.adobe.com/go/kb403623)
   * [AEM表单的DB2备份和恢复](https://www.adobe.com/go/kb403626)

1. 恢复GDS目录，方法是先删除AEM表单现有安装中GDS目录的内容，然后从备份的GDS中复制GDS目录的内容。 如果更改了GDS目录位置，请参阅在恢 [复过程中更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。
1. 重命名要恢复的GDS备份目录，如下例所示：

   >[!NOTE]
   >
   >如果/restore目录已存在，请先备份它，然后删除它，然后再重命名包含最新数据的/backup目录。

   * (JBoss)重命名 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 为：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`.

   * (WebLogic)重命名 `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 为：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`.

   * (WebSphere)重命名 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 为：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`.

1. 恢复内容存储根目录，方法是先删除AEM表单现有安装上的内容存储根目录的内容，然后按照独立或群集环境的任务恢复内容：

   >[!NOTE]
   >
   >内容存储根目录的备份必须恢复到内容存储根目录的位置，就像在内容服务（已弃用）配置过程中设置的一样。

   **独立：** 在恢复过程中，恢复已备份的所有目录。 当恢复这些目录时，如果存在/backup-lucene-indexes目录，则将其重命名为/lucene-indexes。 否则，lucene-indexes目录应已存在，无需执行任何操作。

   **集群：** 在恢复过程中，恢复已备份的所有目录。 要恢复索引根目录，请对群集的每个节点执行以下步骤：

   * 删除“索引根目录”中的所有内容。
   * 如果存在/backup-lucene-indexes目录，请将 *Content存储根目录*/backup-lucene-indexes目录的内容复制到Index Root目录，并删除 *Content存储Root目录*/backup-lucene-indexes目录。
   * 如果存在/lucene-indexes目录，则将 *Content存储Root目录*/lucene-indexes目录的内容复制到Index Root目录。

1. 恢复／恢复CRX存储库。

   * **独立**

      *恢复创作和发布实例*:如果发生灾难，您可以通过执行备份和恢复中所述的步骤，将存储库恢复到上次 [备份状态。](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)

      “作者”节点的完全恢复还可确定Forms Manager和AEM Forms Workspace数据的恢复。

   * **已群集化**

      有关在群集环境中恢复的信息，请 [参阅群集环境中备份和恢复的策略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)。

1. 删除在java.io.temp目录或Adobe临时目录中创建的任何AEM表单临时文件。
1. 开始AEM表单(请参 [阅启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->。

## 在恢复过程中更改GDS位置 {#changing-the-gds-location-during-recovery}

如果GDS恢复到原来位置以外的位置，请运行LCSetGDS脚本将GDS设置为新位置。 该脚本在文件夹 `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` 中。 该脚本采用两个参数， `defaultGDS` 并且 `newGDS`。 有关如 `ReadMe.txt` 何运行脚本的说明，请参阅同一文件夹中的文件。

>[!NOTE]
>
>如果已在数据库中启用文档存储，则无需更改GDS位置。

>[!NOTE]
>
>这种情况是您唯一应使用此脚本更改GDS位置的情况。 要在AEM表单运行时更改GDS位置，请使用管理控制台。 (请参阅 [配置常规AEM表单设置](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。)

>[!NOTE]
>
>如果GDS目录位于驱动器根目录(例如，D:\)，则组件部署在Windows上将失败。 对于GDS，必须确保目录不位于驱动器的根目录中，而位于子目录中。 例如，目录应为D:\GDS and not simply D:\。

## 将GDS恢复到群集环境 {#recovering-the-gds-to-a-clustered-environment}

要更改群集环境中的GDS位置，请关闭整个群集，并在群集的单个节点上运行LCSetGDS脚本。 (请参 [阅在恢复过程中更改GDS位置](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。)仅开始该节点。 当该节点完全启动时，群集中的其他节点可能安全启动，并将正确指向新GDS。

>[!NOTE]
>
>如果无法确保在启动其他节点之前完全启动一个节点，则必须在开始群集之前在群集中的每个节点上运行LCSetGDS脚本。

