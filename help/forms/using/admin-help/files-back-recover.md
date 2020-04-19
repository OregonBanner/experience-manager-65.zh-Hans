---
title: 要备份和恢复的文件
seo-title: 要备份和恢复的文件
description: 本文档描述了必须备份的应用程序和数据文件。
seo-description: 本文档描述了必须备份的应用程序和数据文件。
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# 要备份和恢复的文件 {#files-to-back-up-and-recover}

以下各节将更详细地介绍必须备份的应用程序和数据文件。

请考虑以下有关备份和恢复的要点：

* 应在GDS和AEM存储库之前备份数据库。
* 如果需要关闭群集环境中的节点进行备份，请确保在主节点之前关闭从节点。 否则，可能导致群集或服务器中的不一致。 此外，主节点应在任何从节点之前变为活动节点。
* 对于群集的恢复操作，应停止群集中每个节点的应用程序服务器。

## 全局文档存储目录 {#global-document-storage-directory}

GDS是一个目录，用于存储进程中使用的长期文件。 长期文件的生命周期旨在跨AEM表单系统的一个或多个启动项，并且可能跨日期甚至年。 这些长期使用的文件可以包括PDF、策略和表单模板。 长期使用的文件是许多AEM表单部署的整体状态的关键部分。 如果某些或所有长期文档丢失或损坏，表单服务器可能会变得不稳定。

异步作业调用的输入文档也存储在GDS中，并且必须可用于处理请求。 因此，务必考虑承载GDS并采用独立磁盘冗余阵列(RAID)或其他技术的文件系统的可靠性，以满足您的质量和服务级别要求。

GDS的位置是在AEM表单安装过程中或更高版本中使用管理控制台确定的。 除了为GDS保留高可用性位置，您还可以为文档启用数据库存储。 请参 [阅使用数据库进行文档存储时的备份选项](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。

### GDS位置 {#gds-location}

如果在安装过程中将位置设置留空，则位置默认为应用程序服务器安装下的目录。 必须备份应用程序服务器的以下目录：

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果将GDS位置更改为非默认位置，则可以按如下方式确定它：

* 登录到管理控制台，然后单击设置>核心系统设置>配置。
* 记录在“全局文档存储目录”框中指定的位置。

在群集环境中，GDS通常指向网络上共享的目录，并且每个群集节点都可读／写访问该目录。

如果原始位置不再可用，则GDS的位置可以在恢复期间被更改。 (请参 [阅在恢复过程中更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。)

### 数据库用于文档存储时的备份选项 {#backup-options-when-database-is-used-for-document-storage}

您可以使用管理控制台在AEM表单数据库中启用AEM表单文档存储。 即使此选项将所有永久文档保留在数据库中，AEM表单仍需要基于文件系统的GDS目录，因为它用于存储与AEM表单的会话和调用相关的永久和临时文件和资源。

在管理控制台的核心系统设置中或通过使用配置管理器选择“在数据库中启用文档存储”选项时，AEM表单不允许快照备份模式和滚动备份模式。 因此，您无需使用AEM表单管理备份模式。 如果您使用此选项，则在启用该选项后只备份一次GDS。 从备份中恢复AEM表单时，无需为GDS重命名备份目录或恢复GDS。

## AEM存储库 {#aem-repository}

如果在安装AEM表单时配置了crx-repository，则会创建AEM存储库(crx-repository)。 crx-repository目录的位置在AEM表单安装过程中确定。 需要AEM存储库备份和恢复以及数据库和GDS，才能在AEM表单中实现一致的AEM表单数据。 AEM存储库包含Correponce Management Solution、Forms Manager和AEM Forms Workspace的数据。

### 通信管理解决方案 {#correspondence-management-solution}

通信管理解决方案集中管理安全、个性化和交互式通信的创建、汇编和投放。 它使您能够通过从创建到存档的简化流程，从预先批准的内容到自定义创作的内容，快速组合对应内容。 因此，您的客户可以获得及时、准确、便捷、安全和相关的通信。 您的企业通过简化的流程轻松、快速、高效，从而最大化客户互动的价值并最大限度地降低成本和风险。

简单的“对应管理解决方案”设置包括同一台计算机或不同计算机上的作者实例和发布实例

### forms manager {#forms-manager}

表单管理器简化了更新、管理和退出表单的过程。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace与（JEE上的AEM表单已弃用）Flex Workspace的功能相匹配，并添加了扩展和集成Workspace的新功能，使其更易用。

>[!NOTE]
>
>AEM表单发行版中已弃用Flex工作空间。

它允许在没有Flash Player和Adobe Reader的客户端上进行任务管理。 除PDF表单和Flex表单外，它还便于HTML表单的再现。

## AEM表单数据库 {#aem-forms-database}

AEM表单数据库存储对GDS和内容存储根目录（针对内容服务）中文件的内容，如表单对象、服务配置、进程状态和数据库引用。 数据库备份可以实时执行而不中断服务，恢复可以是到特定时间点或特定更改。 本节介绍如何配置数据库，以便实时备份它。

在正确配置的AEM表单系统上，系统管理员和数据库管理员可以轻松协作，将系统恢复到一致的已知状态。

要实时备份数据库，您必须使用快照模式或将数据库配置为在指定的日志模式下运行。 这允许在数据库打开并可供使用时备份数据库文件。 此外，当数据库在这些模式下运行时，它会保留其回滚和事务日志。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES（已弃用）是与LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持将于2014年12月31日结束。 请参 [阅Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 要了解有关配置Content Services（已弃用）的信息，请参阅 [管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

### DB2 {#db2}

将DB2数据库配置为在存档日志模式下运行。

>[!NOTE]
>
>如果您的AEM表单环境是从AEM表单的先前版本升级的，并且使用DB2，则不支持联机备份。 在这种情况下，您必须关闭AEM表单并执行脱机备份。 未来版本的AEM表单将支持升级客户的在线备份。

IBM拥有一套工具和帮助系统来帮助数据库管理员管理其备份和恢复任务:

* IBM DB2 Archive Log Accelerator(请参阅 [IBM DB2 Archive Log Accelerator for z/OS用户指南](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true)。)
* IBM DB2数据存档专家(请参阅 [IBM DB2数据存档专家用户指南和参考](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)。)

DB2具有将数据库备份到Tivoli存储管理器的内置功能。 通过使用Tivoli存储管理器，DB2备份可以存储在其他介质或本地硬盘上。

有关DB2数据库备份和恢复的详细信息，请参 [阅为DB2开发备份和恢复策略](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm)。

### Oracle {#oracle}

使用快照备份或将Oracle数据库配置为以存档日志模式运行。 (请参 [阅Oracle备份：简介](https://www.databasedesign-resource.com/oracle-backup.md)。)有关备份和恢复Oracle数据库的详细信息，请转到以下站点：

[Oracle备份和恢复：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 更详细地介绍备份和恢复的概念以及使用Recovery Manager(RMAN)进行备份、恢复和报告的最常用技术，并提供有关如何规划备份和恢复战略的更多信息。

[Oracle Database Backup and Recovery User&#39;s Guide:](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供有关RMAN体系结构、备份和恢复概念和机制、高级恢复技术（如时间点恢复和数据库闪回功能）以及备份和恢复性能调整的详细信息。 它还包括使用主机操作系统设备而不是RMAN进行用户管理的备份和恢复。 此卷对于备份和恢复更复杂的数据库部署以及高级恢复场景至关重要。

[Oracle数据库备份和恢复参考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供有关所有RMAN命令的语法和语义的完整信息，并描述可用于报告备份和恢复活动的数据库视图。

### SQL Server {#sql-server}

使用快照备份或将SQL Server数据库配置为以事务日志模式运行。

SQL Server还提供两种备份和恢复工具：

* SQL Server Management Studio(GUI)
* T-SQL（命令行）

请参 [阅备](https://articles.techrepublic.com.com/5100-1035_61-1043671.md)份战 [略和备份和还原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)。

### MySQL {#mysql}

使用MySQLAdmin或在Windows中修改INI文件，将MySQL数据库配置为以二进制日志模式运行。 (请参阅 [MySQL二进制日志](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)。)InnoBase软件中也提供了MySQL的热备份工具。 (请参 [阅Innobase热备份](https://www.innodb.com/hot-backup/features.md)。)

>[!NOTE]
>
>MySQL的默认二进制记录模式是“语句”，它与Content Services使用的表（已弃用）不兼容。 在此默认模式下使用二进制日志记录会导致Content Services（已弃用）失败。 如果您的系统包含Content Services（已弃用），请使用“混合”日志记录模式。 要启用“混合”日志记录，请将以下参数添加到my.ini file:*`binlog_format=mixed log-bin=logname`

您可以使用mysqldump实用程序获取完整的数据库备份。 完全备份是必需的，但并不总是方便的。 它们生成大型备份文件并需要时间生成。 要执行增量备份，请确保使用——选项开始服 `log-bin` 务器，如上一节所述。 每次MySQL服务器重新启动时，它都停止写入当前的二进制日志，创建一个新的二进制日志，然后从此开始，新的二进制日志变成当前的二进制日志。 您可以使用命令手动强制切换 `FLUSH LOGS SQL` 器。 第一次完全备份后，将使用mysqladmin实用程序和命令（该命令创建下一个日志文件）执 `flush-logs` 行后续增量备份。

请参 [阅备份战略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)。

```as3
binlog_format=mixed
log-bin=logname
```

## 内容存储根目录（仅限Content Services） {#content-storage-root-directory-content-services-only}

内容存储根目录包含Content Services（已弃用）存储库，其中存储了所有文档、对象和索引。 必须备份内容存储根目录树。 本节介绍如何确定独立和群集环境的内容存储根目录的位置。

### 内容存储根位置(独立环境) {#content-storage-root-location-stand-alone-environment}

内容存储根目录是在安装Content Services（已弃用）时创建的。 内容存储根目录的位置在AEM表单安装过程中确定。

内容存储根目录的默认位置为 `[aem-forms root]/lccs_data`。

备份位于内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果存在/backup-lucene-indexes目录，请不要备份/lucene-indexes目录，因为它可能导致错误。

### 内容存储根位置(群集环境) {#content-storage-root-location-clustered-environment}

在群集环境中安装Content Services（已弃用）时，内容存储根目录将拆分为两个单独的目录：

**内容存储根目录：** 通常，共享网络目录对于群集中的所有节点都可读／写访问

**索引根目录：** 在群集中每个节点上创建的目录，始终具有相同的路径和目录名

内容存储根目录的默认位置是 `[GDS root]/lccs_data`GDS位 `[GDS root]` 置中描述的 [位置](files-back-recover.md#gds-location)。 备份位于内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果存在/backup-lucene-indexes目录，请不要备份/lucene-indexes目录，因为它可能导致错误。

索引根目录的默认位置位于每 `[aem-forms root]/lucene-indexes` 个节点上。

## 客户安装的字体 {#customer-installed-fonts}

如果您在AEM表单环境中安装了其他字体，则必须单独备份这些字体。 备份在管理控制台中“设置”>“核心系统”>“配置”下指定的所有Adobe和客户字体目录。 确保备份整个字体目录。

>[!NOTE]
>
>默认情况下，随AEM表单一起安装的Adobe字体位于该目 `[aem-forms root]/fonts` 录中。

如果要重新初始化主机上的操作系统，并且希望使用先前操作系统中的字体，则还应备份系统字体目录的内容。 （有关具体说明，请参阅操作系统的文档）。
