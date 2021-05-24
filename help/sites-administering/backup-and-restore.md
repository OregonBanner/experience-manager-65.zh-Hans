---
title: 备份和恢复
seo-title: 备份和恢复
description: 了解如何备份和恢复AEM内容。
seo-description: 了解如何备份和恢复AEM内容。
uuid: 446a466f-f508-4430-9e50-42cd4463760e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: eb8bbb85-ca2f-4877-8ee0-bb1ee8b7d8de
exl-id: dd26dade-b769-483e-bc11-dcfa5ed1f87e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 0%

---

# 备份和恢复{#backup-and-restore}

在AEM中，有两种方法可备份和恢复存储库内容：

* 您可以创建存储库的外部备份并将其存储在安全位置。 如果存储库发生故障，您可以将其恢复到之前的状态。
* 您可以创建存储库内容的内部版本。 这些版本与内容一起存储在存储库中，因此您可以快速恢复已更改或删除的节点和树。

## 常规 {#general}

此处介绍的方法适用于系统备份和恢复。

如果您需要备份和/或恢复丢失的少量内容，则不一定需要恢复系统：

* 您可以通过包从其他系统获取数据
* 或者，在临时系统上恢复备份，创建一个内容包并将其部署在缺少此内容的系统上。

有关详细信息，请参阅下面的[包备份](/help/sites-administering/backup-and-restore.md#package-backup)。

## 计时 {#timing}

请勿与数据存储垃圾收集并行运行备份，因为这可能会损害两个进程的结果。

## 脱机备份{#offline-backup}

您始终可以执行离线备份。 这需要AEM停机，但与在线备份相比，在所需时间方面会非常高效。

在大多数情况下，您将使用文件系统快照来创建当时存储的只读副本。 要创建脱机备份，请执行以下步骤：

* 停止应用程序
* 生成快照备份
* 启动应用程序

由于快照备份通常只需要几秒钟，因此整个停机时间不到几分钟。

## 联机备份{#online-backup}

此备份方法可创建整个存储库的备份，包括其下部署的任何应用程序，如AEM。 备份包括内容、版本历史记录、配置、软件、修补程序、自定义应用程序、日志文件、搜索索引等。 如果您使用群集，并且共享文件夹是`crx-quickstart`的子目录（物理上或使用软链接），则也会备份共享目录。

您可以稍后恢复整个存储库（以及任何应用程序）。

此方法作为“热”或“联机”备份运行，因此可在存储库运行时执行此方法。 因此，在备份运行时，该存储库可用。 此方法适用于默认的基于Tar存储的存储库实例。

创建备份时，您可以使用以下选项：

* 使用AEM集成备份工具备份到目录。
* 使用文件系统快照备份到目录

无论如何，备份都会创建存储库的映像（或快照）。 然后，系统备份代理应当注意将此映像实际传输到专用备份系统（磁带机）。

>[!NOTE]
>
>如果在具有自定义Blobstore配置的AEM实例上使用了AEM联机备份功能，则建议将数据存储的路径配置为位于“ `crx-quickstart`”目录之外，并单独备份数据存储。

>[!CAUTION]
>
>联机备份仅备份文件系统。 如果将存储库内容和/或存储库文件存储在数据库中，则需要单独备份该数据库。 如果您正在将AEM与MongoDB结合使用，请参阅关于如何使用[MongoDB本机备份工具](https://docs.mongodb.org/manual/tutorial/backup-with-mongodump/)的文档。

### AEM联机备份{#aem-online-backup}

通过在线备份存储库，您可以创建、下载和删除备份文件。 它是“热”或“联机”备份功能，因此在读写模式下正常使用存储库时，可以执行该功能。

>[!CAUTION]
>
>请勿与[数据存储垃圾收集](/help/sites-administering/data-store-garbage-collection.md)或[修订清理](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)同时运行AEM联机备份。 它将对系统性能产生负面影响。

启动备份时，可以指定&#x200B;**目标路径**&#x200B;和/或&#x200B;**延迟**。

**目** 标路径备份文件通常保存在存放快速入门Jar文件(.jar)的文件夹的父文件夹中。例如，如果您在/InstallationKits/AEM下有AEM jar文件，则备份将在/InstallationKits下生成。 您还可以将目标指定到您选择的位置。

如果&#x200B;**TargetPath**&#x200B;是目录，则将在此目录中创建存储库的映像。 如果同一目录被多次（或始终）用于存储备份，

* 在TargetPath中相应地修改了存储库中的已修改文件
* 已删除的存储库文件将在TargetPath中删除
* 在存储库中创建的文件是在TargetPath中创建的

>[!NOTE]
>
>如果将&#x200B;**TargetPath**&#x200B;设置为扩展名为&#x200B;**.zip**&#x200B;的文件名，则存储库将备份到临时目录，然后压缩此临时目录的内容并将其存储在ZIP文件中。
>
>这种方法是不鼓励的，因为
>
>* 在备份过程中，它需要额外的磁盘存储（临时目录和zip文件）
>* 压缩过程由存储库完成，可能会影响其性能。
>* 会延迟备份过程。
>* 最高配置Java 1.6 Java只能创建大小为4 GB的ZIP文件。

>
>
如果需要创建ZIP作为备份格式，则应该备份到目录，然后使用压缩程序创建ZIP文件。

**** DelayDelay指示时间延迟（以毫秒为单位），以便不影响存储库性能。默认情况下，存储库备份以全速运行。 您可以减慢创建在线备份的速度，以便不会减慢其他任务的速度。

使用非常大的延迟时，请确保在线备份不会超过24小时。 如果是，请放弃此备份，因为它可能不包含所有二进制文件。
1毫秒的延迟通常导致CPU使用率达到10%，而10毫秒的延迟通常导致CPU使用率低于3%。 总延迟（以秒为单位）的估计如下：存储库大小(MB)、延迟（以毫秒为单位）、 2（如果使用zip选项）或4（备份到目录时）。 这意味着，备份到200 MB存储库的目录（延迟为1毫秒）会将备份时间增加大约50秒。

>[!NOTE]
>
>有关该过程的内部详细信息，请参阅[AEM联机备份的工作方式](#how-aem-online-backup-works)。

要创建备份，请执行以下操作：

1. 以管理员身份登录AEM。

1. 转到&#x200B;**工具 — 操作 — 备份。**
1. 单击&#x200B;**创建**。将打开备份控制台。

   ![chlimage_1-1](assets/chlimage_1-1a.png)

1. 在备份控制台中，指定&#x200B;**[目标路径](#aem-online-backup)**&#x200B;和&#x200B;**[延迟](#aem-online-backup)**。

   ![chlimage_1-2](assets/chlimage_1-2a.png)

   >[!NOTE]
   >
   >备份控制台也可使用：
   >
   >
   >` https://<*hostname*>:<*port-number*>/libs/granite/backup/content/admin.html`

1. 单击&#x200B;**Save**，进度栏将指示备份进度。

   >[!NOTE]
   >
   >您可以随时取消正在运行的备份。****

1. 备份完成后，备份窗口中会列出zip文件。

   ![chlimage_1-3](assets/chlimage_1-3a.png)

   >[!NOTE]
   >
   >可以使用控制台删除不再需要的备份文件。 在左窗格中选择备份文件，然后单击&#x200B;**删除**。

   >[!NOTE]
   >
   >如果已备份到目录：备份过程完成后，AEM将不会写入目标目录。

### 自动化AEM在线备份{#automating-aem-online-backup}

如果可能，应当在系统负载很小时（例如在上午）运行联机备份。

可以使用`wget`或`curl` HTTP客户端自动执行备份。 下面显示了如何使用curl自动备份的示例。

#### 备份到默认目标目录{#backing-up-to-the-default-target-directory}

>[!CAUTION]
>
>在以下示例中，可能需要为实例配置`curl`命令中的各种参数；例如，主机名(`localhost`)、端口(`4502`)、管理员密码(`xyz`)和文件名(`backup.zip`)。

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=backup.zip
```

备份文件/目录在服务器上的父文件夹中创建，该文件夹包含`crx-quickstart`文件夹（与使用浏览器创建备份时相同）。 例如，如果在`/InstallationKits/crx-quickstart/`目录中安装了AEM，则会在`/InstallationKits`目录中创建备份。

curl命令会立即返回，因此您必须监视此目录以查看zip文件准备就绪的时间。 在创建备份时，可以看到临时目录（其名称基于最终zip文件的名称），最后将压缩该目录。 例如：

* 生成的zip文件的名称：`backup.zip`
* 临时目录的名称：`backup.f4d5.temp`

#### 备份到非默认目标目录{#backing-up-to-a-non-default-target-directory}

备份文件/目录通常在服务器上的包含`crx-quickstart`文件夹的文件夹的父文件夹中创建。

如果要将备份（按任一顺序）保存到其他位置，可以在`curl`命令中将绝对路径“设置为`target`参数。

例如，要在`/Backups/2012`目录中生成`backupJune.zip`，请执行以下操作：

```shell
curl -u admin:admin -X POST http://localhost:4502/system/console/jmx/com.adobe.granite:type=Repository/op/startBackup/java.lang.String?target=/Backups/2012/backupJune.zip"
```

>[!CAUTION]
>
>使用其他应用程序服务器（如JBoss）时，联机备份可能无法按预期工作，因为目标目录不可写。 在这种情况下，请联系支持。

>[!NOTE]
>
>也可以使用AEM](/help/sites-administering/jmx-console.md)提供的MBean触发[备份。

### 文件系统快照备份{#filesystem-snapshot-backup}

此处描述的流程特别适用于大型存储库。

>[!NOTE]
>
>如果要使用此备份方法，则系统必须支持文件系统快照。 例如，对于Linux，这意味着您的文件系统应放置在逻辑卷上。

1. 为部署的文件系统AEM创建快照。

1. 装载文件系统快照。
1. 执行备份并卸载快照。

### AEM联机备份的工作原理{#how-aem-online-backup-works}

AEM Online Backup由一系列内部操作组成，这些操作可确保正在备份的数据和正在创建的备份文件的完整性。 下面列出了感兴趣的用户。

联机备份使用以下算法：

1. 创建zip文件时，第一步是创建或查找目标目录。

   * 如果备份到zip文件，则会创建一个临时目录。 目录名称以`backup.`开头，以`.temp`结尾；例如`backup.f4d3.temp`。
   * 如果备份到目录，则使用目标路径中指定的名称。 可以使用现有目录，否则将创建新目录。

      启动备份时，将在目标目录中创建名为`backupInProgress.txt`的空文件。 备份完成后，将删除此文件。

1. 文件将从源目录复制到目标目录（或创建zip文件时的临时目录）。 在数据存储之前复制segmentstore以避免存储库损坏。 创建备份时，将忽略索引和缓存数据。 因此，备份中不包含来自`crx-quickstart/repository/cache`和`crx-quickstart/repository/index`的数据。 创建zip文件时，该过程的进度条指示器介于0% - 70%之间；如果未创建zip文件，则进度条指示器为0% - 100%。

1. 如果备份到预先存在的目录，则目标目录中的“旧”文件会被删除。 旧文件是源目录中不存在的文件。

这些文件将分四个阶段复制到目标目录：

1. 在第一个复制阶段（创建zip文件时的进度指示器0% - 63%或未创建zip文件时的进度指示器0% - 90%），在存储库正常运行时复制所有文件。 该过程分为两个阶段：

   * 阶段A — 复制除数据存储（具有延迟）之外的所有内容。
   * 阶段B — 仅复制数据存储（具有延迟）。

1. 在第二个复制阶段（创建zip文件时进度指示器为63% - 65.8%，如果没有创建zip文件，则为90% - 94%），只复制自第一个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，这可能范围从根本没有文件到大量文件（因为第一个文件复制阶段通常需要很长时间）。 复制过程类似于第一阶段（具有延迟的阶段A和阶段B）。
1. 在第三个复制阶段（创建zip文件时进度指示器为65.8% - 68.6%，如果未创建zip文件则为94% - 98%），只复制自第二个复制阶段启动以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者只有非常少的文件（因为第二个文件复制阶段通常是快速的）。 复制过程类似于第二阶段 — 阶段A和阶段B ，但没有延迟。
1. 文件复制阶段1到3在存储库运行时都同时完成。 只复制自启动第三个复制阶段以来在源目录中创建或修改的文件。 根据存储库的活动，可能没有要复制的文件，或者文件的数量非常非常少（因为第二个文件复制阶段通常非常快）。 创建zip文件时，进度指示器为68.6% - 70%；如果未创建zip文件，进度指示器为98% - 100%。 复制过程与第三阶段类似。
1. 根据目标：

   * 如果指定了zip文件，则现在从临时目录创建该文件。 进度指标70% - 100%。 然后，将删除临时目录。
   * 如果目标是目录，则会删除名为`backupInProgress.txt`的空文件，以指示备份已完成。

## 恢复备份{#restoring-the-backup}

可以按如下方式恢复备份：

* 如果您执行了文件系统快照备份，则只需恢复系统映像即可。
* 如果您将备份创建为zip文件，则只需将内容解压缩到新文件夹中，然后从该位置启动AEM即可。

## 包备份{#package-backup}

要备份和恢复内容，您可以使用包管理器中的一个，该管理器使用内容包格式来备份和恢复内容。 包管理器在定义和管理包方面提供了更大的灵活性。

有关这些单独的内容包格式的功能和权衡的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。

### 备份范围{#scope-of-backup}

当您使用包管理器或内容拉链备份节点时，CRX会保存以下信息：

* 所选树下的存储库内容。
* 用于您备份的内容的节点类型定义。
* 用于您备份的内容的命名空间定义。

备份时，AEM会丢失以下信息：

* 版本历史记录。
