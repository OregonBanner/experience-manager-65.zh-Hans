---
title: 要备份和恢复的文件
description: 本文档介绍了必须备份的应用程序和数据文件。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2065'
ht-degree: 0%

---

# 要备份和恢复的文件 {#files-to-back-up-and-recover}

以下各节将更详细地介绍必须备份的应用程序和数据文件。

关于备份和恢复，请考虑以下几点：

* 数据库应在GDS和AEM资料档案库之前进行备份。
* 如果需要关闭群集环境中的节点以进行备份，请确保在主节点之前关闭辅助节点。 否则，可能会导致群集或服务器中的不一致。 此外，主节点应在任何辅助节点之前处于活动状态。
* 对于群集的还原操作，应该为群集中的每个节点停止应用程序服务器。

## 全局文档存储目录 {#global-document-storage-directory}

GDS是用于存储进程中使用的长期文件的目录。 长生命周期文件的生命周期旨在跨越AEM表单系统的一个或多个启动项，并且可能跨越天甚至年。 这些长期文件可以包括PDF、策略和表单模板。 长生命周期文件是许多AEM forms部署总体状态的重要组成部分。 如果某些或所有长期文档丢失或损坏，表单服务器可能会变得不稳定。

异步作业调用的输入文档也存储在GDS中，并且必须可用于处理请求。 因此，一定要考虑承载GDS的文件系统的可靠性，并采用独立磁盘冗余阵列(RAID)或其他适合您的质量和服务级别要求的技术。

GDS的位置是在AEM Forms安装过程中或以后使用管理控制台确定的。 除了为GDS保留一个高可用性位置之外，您还可以为文档启用数据库存储。 请参阅 [当数据库用于文档存储时的备份选项](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS位置 {#gds-location}

如果在安装期间将位置设置保留为空，则该位置将默认为应用程序服务器安装下的目录。 您必须为应用程序服务器备份以下目录：

* (JBos) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果将GDS位置更改为非默认位置，可按如下方式确定：

* 登录到管理控制台并单击设置>核心系统设置>配置。
* 记录在“全局文档存储目录”框中指定的位置。

在群集环境中，GDS通常指向网络上共享的目录，并且每个群集节点都可以读/写访问。

如果原始位置不再可用，则在恢复期间可以更改GDS的位置。 (请参阅 [在恢复过程中更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### 当数据库用于文档存储时的备份选项 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理控制台在AEM forms数据库中启用AEM forms文档存储。 即使此选项保留数据库中的所有持久性文档，AEM表单仍需要基于文件系统的GDS目录，因为它用于存储与AEM表单的会话和调用相关的永久和临时文件及资源。

当您在管理控制台的“核心系统设置”中选择“在数据库中启用文档存储”选项或使用Configuration Manager时，AEM Forms不允许快照备份模式和滚动备份模式。 因此，您不需要使用AEM表单管理备份模式。 如果使用此选项，则启用该选项后，应仅备份GDS一次。 从备份中恢复AEM表单时，不需要重命名GDS的备份目录或恢复GDS。

## AEM存储库 {#aem-repository}

如果在安装AEM表单时配置了crx-repository，则会创建AEM存储库(crx-repository)。 crx-repository目录的位置是在AEM Forms安装过程中确定的。 在AEM表单中要获得一致的AEM表单数据，需要进行AEM存储库备份和还原以及数据库和GDS。 AEM存储库包含用于通信管理解决方案、Forms Manager和AEM Forms Workspace的数据。

### 通信管理解决方案 {#correspondence-management-solution}

通信管理解决方案可集中管理安全、个性化的交互式通信的创建、编排和交付。 它使您能够通过从创建到存档的简化流程，快速汇编预批准和自定义创作内容的通信。 这样，您的客户就可以获得及时、准确、方便、安全且相关的通信。 您的企业通过简化流程实现客户交互的最大价值，并最大程度地降低成本和风险，以实现轻松、快速和生产效率。

简单的通信管理解决方案设置包括在同一台计算机上或不同计算机上的创作实例和发布实例

### 表单管理器 {#forms-manager}

forms manager简化了更新、管理和报废表单的过程。

### AEM Forms工作区 {#html-workspace}

AEM Forms工作区与(已弃用JEE上的AEM表单)Flex工作区的功能相匹配，并添加了扩展和集成工作区的新功能，使其更加用户友好。

>[!NOTE]
>
>AEM Forms版本弃用Flex工作区。

它允许在没有Flash Player和Adobe Reader的客户端上进行任务管理。 它有助于呈现除PDF forms和Flex表单之外的HTMLForms。

## AEM forms数据库 {#aem-forms-database}

AEM Forms数据库将表单对象、服务配置、进程状态以及对GDS和内容存储根目录（用于Content Services）中文件的数据库引用等内容存储起来。 数据库备份可以在不中断服务的情况下实时执行，并且可以恢复到特定时间点或特定更改。 本节介绍如何配置数据库以便对其进行实时备份。

在正确配置的AEM Forms系统上，系统管理员和数据库管理员可以轻松地协作以将系统恢复到一致的已知状态。

要实时备份数据库，必须使用快照模式或将数据库配置为以指定的日志模式运行。 这允许在数据库打开且可用时备份数据库文件。 此外，当数据库在这些模式下运行时，它保留回滚和事务日志。

>[!NOTE]
>
>Adobe®LiveCycle®内容服务ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 Content Services（已弃用）支持于2014年12月31日终止。 请参阅 [Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

### DB2 {#db2}

将DB2数据库配置为在归档日志模式下运行。

>[!NOTE]
>
如果您的AEM表单环境是从以前版本的AEM表单升级的，并且使用的是DB2，则不支持联机备份。 在这种情况下，必须关闭AEM表单并执行脱机备份。 AEM表单的未来版本将支持升级客户的在线备份。

IBM提供了一套工具和帮助系统，可帮助数据库管理员管理其备份和恢复任务：

* IBM DB2归档日志加速器
* IBM DB2数据存档专家

DB2具有将数据库备份到Tivoli Storage Manager的内置功能。 通过使用Tivoli Storage Manager，DB2备份可以存储在其他介质或本地硬盘上。

### oracle {#oracle}

使用快照备份或将Oracle数据库配置为在归档日志模式下运行。 (请参阅 [oracle备份：简介](https://www.databasedesign-resource.com/oracle-backup.md).) 有关备份和恢复Oracle数据库的详细信息，请转到以下站点：

[oracle备份和恢复：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 更详细地说明了备份和恢复的概念以及使用Recovery Manager (RMAN)进行备份、恢复和报告的最常用技术，并提供了有关如何规划备份和恢复策略的更多信息。

[《Oracle数据库备份和恢复用户指南》 ：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供有关RMAN体系结构、备份和恢复概念和机制、高级恢复技术（如时间点恢复和数据库闪回功能）以及备份和恢复性能调整的深入信息。 它还涵盖了用户管理的备份和恢复，使用主机操作系统功能而不是RMAN。 此卷对于备份和恢复更复杂的数据库部署以及高级恢复方案至关重要。

[oracle数据库备份和恢复参考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供了有关所有RMAN命令的语法和语义的完整信息，并描述了可用于报告备份和恢复活动的数据库视图。

### SQL Server {#sql-server}

使用快照备份或将SQL Server数据库配置为在事务日志模式下运行。

SQL Server还提供了两种备份和恢复工具：

* SQL Server Management Studio (GUI)
* T-SQL（命令行）

有关更多信息，请参阅 [备份和恢复](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx).

### MySQL {#mysql}

在Windows中使用MySQLAdmin或修改INI文件，将MySQL数据库配置为以二进制日志模式运行。 (请参阅 [MySQL二进制日志记录](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) InnoBase软件也提供了用于MySQL的热备份工具。 (请参阅 [Innobase热备份](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
MySQL的默认二进制日志记录模式是“语句”，它与Content Services使用的表不兼容（已弃用）。 在此默认模式下使用二进制日志记录会导致Content Services（已弃用）失败。 如果您的系统包含内容服务（已弃用），请使用“混合”日志记录模式。 要启用“混合”日志记录，请将以下参数添加到my.ini文件中： `binlog_format=mixed log-bin=logname`

您可以使用mysqldump实用程序获取完整的数据库备份。 需要完全备份，但并不总是方便的。 它们会生成大型备份文件，并且需要时间才能生成。 要执行增量备份，请确保使用 —  `log-bin` 选项，如上一节所述。 每次MySQL服务器重新启动时，它都会停止写入当前二进制日志，并创建一个新日志，从那时起，新日志将成为当前二进制日志。 您可以使用手动强制切换 `FLUSH LOGS SQL` 命令。 在第一次完全备份后，后续增量备份将使用mysqladmin实用程序和 `flush-logs` 命令，用于创建下一个日志文件。

请参阅 [备份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## 内容存储根目录（仅限Content Services） {#content-storage-root-directory-content-services-only}

内容存储根目录包含Content Services（已弃用）存储库，其中存储了所有文档、对象和索引。 必须备份内容存储根目录树。 本节介绍如何为独立环境和群集环境确定内容存储根目录的位置。

### 内容存储根目录位置（独立环境） {#content-storage-root-location-stand-alone-environment}

内容存储根目录是在安装Content Services（已弃用）时创建的。 内容存储根目录的位置是在AEM Forms安装过程中确定的。

内容存储根目录的默认位置为 `[aem-forms root]/lccs_data`.

备份内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果/backup-lucene-indexes目录存在，请勿备份/lucene-indexes目录，因为它可能会导致错误。

### 内容存储根位置（群集环境） {#content-storage-root-location-clustered-environment}

在群集环境中安装Content Services（已弃用）时，内容存储根目录将拆分为两个单独的目录：

**内容存储根目录：** 通常，群集中的所有节点均可读/写访问的共享网络目录

**索引根目录：** 在群集中的每个节点上创建的目录，其路径和目录名称始终相同

内容存储根目录的默认位置为 `[GDS root]/lccs_data`，其中 `[GDS root]` 是中描述的位置 [GDS位置](files-back-recover.md#gds-location). 备份内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果/backup-lucene-indexes目录存在，请勿备份/lucene-indexes目录，因为它可能会导致错误。

“索引根目录”的默认位置为 `[aem-forms root]/lucene-indexes` 在每个节点上。

## 客户安装的字体 {#customer-installed-fonts}

如果您在AEM表单环境中安装了其他字体，则必须单独对其进行备份。 备份在管理控制台中的“设置”>“核心系统”>“配置”下指定的所有Adobe和客户字体目录。 确保备份整个字体目录。

>[!NOTE]
>
默认情况下，随AEM表单一起安装的Adobe字体位于 `[aem-forms root]/fonts` 目录。

如果您正在重新初始化主机计算机上的操作系统，并且希望使用上一个操作系统的字体，则系统字体目录的内容也应进行备份。 （有关具体说明，请参阅适用于您的操作系统的文档）。
