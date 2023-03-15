---
title: 备份和恢复
seo-title: Backup and Restore
description: 了解如何备份和恢复AEM内容。
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

在AEM中备份和还原存储库内容的方法有两种：

* 您可以创建存储库的外部备份，并将其存储在安全位置。 如果存储库出现故障，您可以将其恢复到以前的状态。
* 您可以创建存储库内容的内部版本。 这些版本与内容一起存储在存储库中，因此您可以快速恢复已更改或删除的节点和树。

## 常规 {#general}

这里介绍的方法适用于系统备份和恢复。

如果您需要备份和/或恢复少量丢失的内容，则不一定需要恢复系统：

* 您可以通过软件包从另一个系统获取数据
* 或者，在临时系统上恢复备份，创建一个内容包并将其部署到缺少此内容的系统上。

有关详细信息，请参阅 [包备份](/help/sites-administering/backup-and-restore.md#package-backup) 下面的。

## 计时 {#timing}

请勿与数据存储垃圾收集并行运行备份，因为这样可能会损害这两个过程的结果。

## 脱机备份 {#offline-backup}

您始终可以执行脱机备份。 这需要AEM的停机，但与在线备份相比，在所需时间方面可以非常高效。

在大多数情况下，您将使用文件系统快照来创建存储区的只读副本。 要创建脱机备份，请执行以下步骤：

* 停止应用程序
* 创建快照备份
* 启动应用程序

由于快照备份通常只需要几秒钟，因此整个停机时间少于几分钟。

## 在线备份 {#online-backup}

此备份方法创建整个存储库的备份，包括在其下部署的任何应用程序，如AEM。 备份包括内容、版本历史记录、配置、软件、修补程序、自定义应用程序、日志文件、搜索索引等。 如果您使用群集，并且共享文件夹是的子目录 `crx-quickstart` （物理目录或使用软链接），共享目录也会进行备份。

您可以在以后恢复整个存储库（以及任何应用程序）。

此方法作为“热”或“在线”备份运行，因此可在存储库运行时执行。 因此，在备份运行时，存储库可用。 此方法适用于默认的基于Tar存储的存储库实例。

创建备份时，您有以下选项：

* 使用AEM集成备份工具备份到目录。
* 使用文件系统快照备份到目录

无论如何，备份都会创建存储库的映像（或快照）。 然后，系统备份代理应该注意将此映像实际传输到专用备份系统（磁带机）。

>[!NOTE]
>
>如果在具有自定义Blobstore配置的AEM实例上使用AEM Online Backup功能，建议将数据存储的路径配置为在“ `crx-quickstart`”目录，并分别备份数据存储。

>[!CAUTION]
>
>联机备份仅备份文件系统。 如果将存储库内容和/或存储库文件存储在数据库中，则需要单独备份该数据库。 如果将AEM与MongoDB一起使用，请参阅有关如何使用 [MongoDB本机备份工具](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/).

### AEM联机备份 {#aem-online-backup}

存储库的在线备份允许您创建、下载和删除备份文件。 它是一种“热”或“在线”备份功能，因此可以在存储库以读写模式正常使用时执行。

>[!CAUTION]
>
>不要同时运行AEM联机备份 [数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md) 或 [修订版清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup). 这将对系统性能产生负面影响。

在启动备份时，您可以指定 **目标路径** 和/或 **延迟**.

**目标路径** 备份文件通常保存在包含快速入门jar文件(.jar)的文件夹的父文件夹中。 例如，如果AEM jar文件位于/InstallationKits/AEM下，则会在/InstallationKits下生成备份。 您还可以为所选位置指定目标。

如果 **目标路径** 是一个目录，在此目录中创建存储库的图像。 如果存储备份时多次使用同一个目录（或总是使用同一个目录），

* 存储库中已修改的文件将在TargetPath中相应地修改
* 存储库中已删除的文件将在TargetPath中删除
* 在存储库中创建的文件是在TargetPath中创建的

>[!NOTE]
>
>如果 **目标路径** 设置为带扩展名的文件名 **.zip**，存储库将备份到临时目录，然后压缩此临时目录的内容并将其存储在ZIP文件中。
>
>这种办法不令人鼓舞，因为
>
>* 在备份过程中需要额外的磁盘存储（临时目录加上zip文件）
>* 压缩过程由存储库完成，并且可能会影响其性能。
>* 这会延迟备份过程。
>* 在Java 1.6版本中，Java只能创建大小不超过4 GB的ZIP文件。
>
>如果需要创建ZIP作为备份格式，则应备份到目录，然后使用压缩程序创建zip文件。

**延迟** 指示时间延迟（以毫秒为单位），以使存储库性能不受影响。 默认情况下，存储库备份以全速运行。 您可以减慢创建联机备份的速度，这样就不会减慢其他任务的速度。

如果使用非常长的延迟，请确保在线备份不超过24小时。 如果是，则放弃此备份，因为它可能不包含所有二进制文件。
1毫秒的延迟通常导致10%的CPU使用率，10毫秒的延迟通常导致3%以下的CPU使用率。 总延迟时间（以秒为单位）的估计如下：存储库大小（以MB为单位），乘以延迟时间（以毫秒为单位），再除以2（如果使用zip选项），或者再除以4（备份到目录时）。 这意味着，如果备份到200 MB存储库的目录，延迟为1毫秒，备份时间将增加约50秒。

>[!NOTE]
>
>参见 [AEM Online Backup的工作原理](#how-aem-online-backup-works) 以了解该过程的内部详细信息。

要创建备份，请执行以下操作：

1. 以管理员身份登录AEM。

1. 转到 **工具 — 操作 — 备份。**
1. 单击&#x200B;**创建**。此时将打开备份控制台。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在备份控制台上，指定 **[目标路径](#aem-online-backup)** 和 **[延迟](#aem-online-backup)**.

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >备份控制台还可通过以下方式使用：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 单击 **保存**，进度条将指示备份进度。

   >[!NOTE]
   >
   >您可以 **取消** 随时运行备份。

1. 备份完成后，备份窗口中会列出zip文件。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >不再需要的备份文件可以使用控制台删除。 在左窗格中选择备份文件，然后单击 **删除**.

   >[!NOTE]
   >
   >如果已备份到目录：备份过程完成后，AEM将不会写入目标目录。

### 自动化AEM在线备份 {#automating-aem-online-backup}

如果可能，应在系统负荷很小时（例如，早上时）运行联机备份。

可以使用自动执行备份 `wget` 或 `curl` HTTP客户端。 下面显示了如何使用curl自动进行备份的示例。

#### 备份到默认目标目录 {#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在以下示例中，将使用 `curl` 可能需要为实例配置命令；例如，主机名( `localhost`)，端口( `4502`)，管理员密码( `xyz`)和文件名( `backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

备份文件/目录在服务器上创建，位于包含 `crx-quickstart` 文件夹（与使用浏览器创建备份时相同）。 例如，如果您在目录中安装了AEM `/InstallationKits/crx-quickstart/`，则会在中创建备份 `/InstallationKits` 目录。

curl命令会立即返回，因此您必须监视此目录以查看zip文件何时准备就绪。 在创建备份时，可以看到临时目录（其名称基于最终zip文件的名称），但最后会压缩该目录。 例如：

* 生成的zip文件的名称： `backup.zip`
* 临时目录的名称： `backup.f4d5.temp`

#### 备份到非默认目标目录 {#backing-up-to-a-non-default-target-directory}

通常，备份文件/目录是在服务器上在包含 `crx-quickstart` 文件夹。

如果要将备份（任何一种类型）保存到其他位置，可以设置一个绝对路径“到 `target` 中的参数 `curl` 命令。

例如，要生成 `backupJune.zip` 在目录中 `/Backups/2012`：

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用其他应用程序服务器（如JBoss）时，由于目标目录不可写，联机备份可能无法按预期工作。 在这种情况下，请联系支持人员。

>[!NOTE]
>
>也可以触发备份 [使用AEM提供的MBean](/help/sites-administering/jmx-console.md).

### 文件系统快照备份 {#filesystem-snapshot-backup}

这里描述的流程特别适用于大型存储库。

>[!NOTE]
>
>如果要使用此备份方法，您的系统必须支持文件系统快照。 例如，对于Linux ，这意味着文件系统应放置在逻辑卷上。

1. 对部署的文件系统AEM创建快照。

1. 装载文件系统快照。
1. 执行备份并卸载快照。

### AEM Online Backup的工作原理 {#how-aem-online-backup-works}

AEM Online Backup由一系列内部操作组成，这些操作可确保正在备份的数据和正在创建的备份文件的完整性。 有关人士可参阅下文所示的讲座。

联机备份使用以下算法：

1. 创建zip文件时，第一步是创建或定位目标目录。

   * 如果备份到zip文件，则会创建一个临时目录。 目录名开头为 `backup.` 结束于 `.temp`；例如 `backup.f4d3.temp`.
   * 如果备份到目录，则使用目标路径中指定的名称。 可以使用现有目录，否则将创建一个新目录。

      名为的空文件 `backupInProgress.txt` 备份启动时，在目标目录中创建。 备份完成后，此文件将被删除。

1. 文件将从源目录复制到目标目录（或在创建zip文件时复制到临时目录）。 区段存储会在数据存储之前复制，以避免存储库损坏。 创建备份时省略了索引和缓存数据。 因此，数据来自 `crx-quickstart/repository/cache` 和 `crx-quickstart/repository/index` 未包含在备份中。 创建zip文件时，进程的进度条指示符介于0% - 70%之间；如果未创建zip文件，则进度条指示符介于0% - 100%之间。

1. 如果备份到预先存在的目录，则将删除目标目录中的“旧”文件。 旧文件是源目录中不存在的文件。

文件将分四个阶段复制到目标目录：

1. 在第一个复制阶段（创建zip文件时进度指示器0% - 63%，如果未创建zip文件，则进度指示器0% - 90%），所有文件都将在存储库正常运行时复制。 该过程分为两个阶段：

   * 阶段A — 复制除数据存储之外的所有内容（延迟）。
   * 阶段B — 仅复制数据存储（延迟）。

1. 在第二个复制阶段（创建zip文件时进度指示器63% - 65.8%，如果未创建zip文件，则进度指示器90% - 94%），将仅复制自第一个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，文件数量可能会从完全没有文件到大量文件（因为第一个文件复制阶段通常需要大量时间）。 复制过程类似于第一阶段（阶段A和阶段B延迟）。
1. 在第三个复制阶段（创建zip文件时进度指示器65.8% - 68.6%，未创建zip文件时进度指示器94% - 98%），仅复制自第二个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者文件数量非常少（因为第二个文件复制阶段通常很快）。 复制过程与第二阶段（阶段A和阶段B）相似，但不会延迟。
1. 文件复制阶段1到3都是在存储库运行时同时完成的。 仅复制自第三个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者文件数量非常少（因为第二个文件复制阶段通常非常快）。 创建zip文件时进度指示器68.6% - 70%；如果未创建zip文件，进度指示器98% - 100%。 复制过程类似于第三阶段。
1. 根据目标：

   * 如果指定了zip文件，则现在将从临时目录创建该文件。 进度指标70%-100%。 然后删除临时目录。
   * 如果目标是目录，则空文件将命名为 `backupInProgress.txt` 将被删除，以指示备份已完成。

## 恢复备份 {#restoring-the-backup}

您可以按如下方式恢复备份：

* 如果执行了文件系统快照备份，则只需还原系统的映像即可。
* 如果已将备份创建为zip文件，只需解压缩新文件夹中的内容并从该位置启动AEM。

## 包备份 {#package-backup}

要备份和还原内容，您可以使用包管理器之一，它使用内容包格式来备份和还原内容。 包管理器在定义和管理包方面提供了更大的灵活性。

有关每种内容包格式的功能和权衡的详细信息，请参阅 [如何使用包](/help/sites-administering/package-manager.md).

### 备份范围 {#scope-of-backup}

使用包管理器或内容拉链备份节点时，CRX将保存以下信息：

* 所选树下的存储库内容。
* 用于备份内容的节点类型定义。
* 用于备份内容的命名空间定义。

备份时，AEM会丢失以下信息：

* 版本历史记录。
