---
title: 要备份和恢复的文件
seo-title: 要备份和恢复的文件
description: 本文档介绍了必须备份的应用程序和数据文件。
seo-description: 本文档介绍了必须备份的应用程序和数据文件。
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---

# 要备份和恢复的文件{#files-to-back-up-and-recover}

以下各节对必须备份的应用程序和数据文件进行了更详细的描述。

请考虑以下有关备份和恢复的要点：

* 应在GDS和AEM存储库之前备份数据库。
* 如果需要关闭群集环境中的节点进行备份，请确保在主节点之前关闭辅助节点。 否则，可能会导致群集或服务器中出现不一致。 此外，主节点应该在任何辅助节点之前处于活动状态。
* 对于群集的还原操作，应停止群集中每个节点的应用程序服务器。

## 全局文档存储目录{#global-document-storage-directory}

GDS是用于存储进程内使用的长生命周期文件的目录。 长存留期文件的生命周期旨在跨越AEM表单系统的一次或多次启动，并且可能跨越数天甚至数年。 这些长期使用的文件可以包含PDF、策略和表单模板。 长期文件是许多AEM表单部署整体状态的关键部分。 如果某些或所有长期存在的文档丢失或损坏，则表单服务器可能会变得不稳定。

异步作业调用的输入文档也存储在GDS中，并且必须可用于处理请求。 因此，必须考虑托管GDS并采用独立磁盘冗余阵列(RAID)或其他技术的文件系统的可靠性，以满足您的质量和服务级别要求。

GDS的位置在AEM表单安装过程中或稍后使用管理控制台来确定。 除了为GDS保留高可用性位置外，您还可以为文档启用数据库存储。 请参见[将数据库用于文档存储时的备份选项](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。

### GDS位置{#gds-location}

如果在安装期间将位置设置留空，则该位置默认为应用程序服务器安装下的目录。 必须备份应用程序服务器的以下目录：

* (JBoss)`[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic)`[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere)`[appserver root]/installedApps/adobe/'server'/DocumentStorage`

如果将GDS位置更改为非默认位置，则可以按如下方式确定该位置：

* 登录到管理控制台，然后单击设置>核心系统设置>配置。
* 记录在“全局文档存储目录”框中指定的位置。

在群集环境中，GDS通常指向网络上共享的目录，该目录可供每个群集节点读/写访问。

如果原始位置不再可用，则在恢复期间，GDS的位置可能会发生更改。 （请参阅[在恢复期间更改GDS位置](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)。）

### 将数据库用于文档存储{#backup-options-when-database-is-used-for-document-storage}时的备份选项

您可以使用管理控制台在AEM Forms数据库中启用AEM Forms文档存储。 即使此选项会保留数据库中的所有永久性文档，AEM表单仍需要基于文件系统的GDS目录，因为它用于存储与AEM表单的会话和调用相关的永久性和临时文件及资源。

当您在管理控制台的核心系统设置中选择“在数据库中启用文档存储”选项或使用配置管理器时，AEM表单不允许快照备份模式和滚动备份模式。 因此，您无需使用AEM表单管理备份模式。 如果使用此选项，则在启用此选项后，只应备份一次GDS。 从备份中恢复AEM表单时，无需重命名GDS或恢复GDS的备份目录。

## AEM存储库{#aem-repository}

如果在安装AEM Forms时配置了crx-repository，则会创建AEM存储库(crx-repository)。 crx-repository目录的位置在AEM Forms安装过程中确定。 AEM存储库备份和还原需要与数据库和GDS一起使用，才能在AEM表单中实现一致的AEM表单数据。 AEM存储库包含通信管理解决方案、Forms manager和AEM Forms工作区的数据。

### 通信管理解决方案{#correspondence-management-solution}

通信管理解决方案可集中管理安全、个性化和交互式信函的创建、汇编和交付。 它使您能够通过从创建到存档的简化流程，从预先批准和自定义创作的内容快速组合通信。 这样，您的客户就能够及时、准确、方便、安全且相关地进行通信。 您的企业通过简化流程以轻松、快速和高效地实现客户交互的价值最大化，并最大限度地降低成本和风险。

简单的通信管理解决方案设置包括位于同一台计算机或不同计算机上的创作实例和发布实例

### 表单管理器{#forms-manager}

表单管理器可简化更新、管理和停用表单的过程。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace与(JEE上的AEM表单已弃用)Flex Workspace的功能相匹配，并添加了扩展和集成工作区以及使其更加用户友好的新功能。

>[!NOTE]
>
>AEM Forms版本已弃用Flex Workspace。

它允许在客户端上管理任务，而无需Flash Player和Adobe Reader。 除了PDF forms和Flex表单之外，它还方便了HTML Forms的呈现。

## AEM forms数据库{#aem-forms-database}

AEM Forms数据库存储对GDS和内容存储根目录（用于内容服务）中文件的表单对象、服务配置、进程状态和数据库引用等内容。 数据库备份可以在不中断服务的情况下实时执行，恢复可以是特定时间点或特定更改。 本节将介绍如何配置数据库以便能够实时备份它。

在正确配置的AEM表单系统上，系统管理员和数据库管理员可以轻松协作，将系统恢复到一致的已知状态。

要实时备份数据库，必须使用快照模式或配置数据库以指定的日志模式运行。 这样，在数据库打开并可供使用时，即可备份数据库文件。 此外，当数据库以这些模式运行时，它将保留其回滚和事务日志。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（已弃用）是随LiveCycle一起安装的内容管理系统。 它使用户能够设计、管理、监控和优化以人为中心的流程。 内容服务（已弃用）支持将于12/31/2014终止。 请参阅[Adobe产品生命周期文档](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 要了解有关配置Content Services的信息（已弃用），请参阅[管理Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

### DB2 {#db2}

配置DB2数据库以在存档日志模式下运行。

>[!NOTE]
>
>如果您的AEM表单环境是从以前版本的AEM表单升级而来的，并且使用的是DB2，则不支持联机备份。 在这种情况下，您必须关闭AEM表单并执行离线备份。 未来版本的AEM表单将支持升级客户的在线备份。

IBM有一套工具和帮助系统来帮助数据库管理员管理其备份和恢复任务：

* IBM DB2 Archive Log Accelerator（请参阅[IBM DB2 Archive Log Accelerator for z/OS User&#39;s Guide](https://publib.boulder.ibm.com/infocenter/dzichelp/v2r2/topic/com.ibm.db2tools.alc.doc.ug/alcugb20.pdf?noframes=true)。）
* IBM DB2 Data Archive专家（请参阅[IBM DB2 Data Archive Expert User&#39;s Guide and Reference](https://publib.boulder.ibm.com/infocenter/mptoolic/v1r0/topic/com.ibm.db2tools.aeu.doc.ug/ahxugb13.pdf?noframes=true)。）

DB2具有将数据库备份到Tivoli Storage Manager的内置功能。 使用Tivoli Storage Manager , DB2备份可以存储在其他介质或本地硬盘上。

有关DB2数据库备份和恢复的详细信息，请参阅[为DB2](https://publib.boulder.ibm.com/infocenter/db2luw/v9/index.jsp?topic=/com.ibm.db2.udb.admin.doc/doc/c0005945.htm)制定备份和恢复策略。

### Oracle {#oracle}

使用快照备份或配置Oracle数据库以在存档日志模式下运行。 (请参阅[Oracle备份：简介](https://www.databasedesign-resource.com/oracle-backup.md)。) 有关备份和恢复Oracle数据库的更多信息，请访问以下站点：

[Oracle备份和恢复：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) 更详细地说明备份和恢复的概念以及使用Recovery Manager(RMAN)进行备份、恢复和报告的最常用技术，并提供有关如何规划备份和恢复策略的更多信息。

[Oracle数据库备份和恢复用户指南：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) 提供有关RMAN体系结构、备份和恢复概念和机制、高级恢复技术（如时间点恢复和数据库闪回功能）以及备份和恢复性能调整的深入信息。它还包括使用主机操作系统设施而不是RMAN的用户管理的备份和恢复。 此卷对于备份和恢复更复杂的数据库部署以及高级恢复方案至关重要。

[Oracle数据库备份和恢复参考：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) 提供有关所有RMAN命令的语法和语义的完整信息，并描述可用于报告备份和恢复活动的数据库视图。

### SQL Server {#sql-server}

使用快照备份或配置SQL Server数据库以在事务日志模式下运行。

SQL Server还提供了两种备份和恢复工具：

* SQL Server Management Studio(GUI)
* T-SQL（命令行）

有关更多信息，请参阅[备份和还原](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)。

### MySQL {#mysql}

使用MySQLAdmin或在Windows中修改INI文件，以配置MySQL数据库以二进制日志模式运行。 （请参阅[MySQL二进制日志记录](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)。） InnoBase软件还提供了MySQL的热备份工具。 （请参阅[Innobase热备份](https://www.innodb.com/hot-backup/features.md)。）

>[!NOTE]
>
>MySQL的默认二进制日志记录模式为“语句”，该模式与Content Services使用的表（已弃用）不兼容。 在此默认模式下使用二进制日志记录会导致“内容服务”（已弃用）失败。 如果您的系统包含内容服务（已弃用），请使用“混合”日志记录模式。 要启用“混合”日志记录，请将以下参数添加到my.ini文件中：`binlog_format=mixed log-bin=logname`

您可以使用mysqldump实用程序获取完整的数据库备份。 需要完整备份，但并不总是方便。 它们会生成大型备份文件，并且需要一些时间才能生成。 要执行增量备份，请确保您使用 — `log-bin`选项启动服务器，如上一节中所述。 每次MySQL服务器重新启动时，它都会停止写入当前二进制日志，创建新日志，然后从此开始，新日志将变为当前日志。 可以使用`FLUSH LOGS SQL`命令手动强制交换机。 在第一次完全备份后，使用mysqladmin实用程序和`flush-logs`命令完成后续增量备份，该命令将创建下一个日志文件。

请参阅[备份策略摘要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)。

```text
binlog_format=mixed
log-bin=logname
```

## 内容存储根目录（仅限内容服务）{#content-storage-root-directory-content-services-only}

内容存储根目录包含存储所有文档、工件和索引的内容服务（已弃用）存储库。 必须备份内容存储根目录树。 本节介绍如何确定独立和群集环境的内容存储根目录的位置。

### 内容存储根位置（独立环境）{#content-storage-root-location-stand-alone-environment}

安装Content Services（已弃用）时，将创建Content Storage Root目录。 内容存储根目录的位置在AEM表单安装过程中确定。

内容存储根目录的默认位置为`[aem-forms root]/lccs_data`。

备份位于内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果/backup-lucene-indexes目录存在，请不要备份/lucene-indexes目录，因为它可能会导致错误。

### 内容存储根位置（群集环境）{#content-storage-root-location-clustered-environment}

在群集环境中安装Content Services（已弃用）时，Content Storage Root目录将拆分为两个单独的目录：

**内容存储根目录：** 通常是可供群集中所有节点读/写访问的共享网络目录

**索引根目录：** 在群集中每个节点上创建的目录，始终具有相同的路径和目录名称

内容存储根目录的默认位置为`[GDS root]/lccs_data`，其中`[GDS root]`是[GDS位置](files-back-recover.md#gds-location)中描述的位置。 备份位于内容存储根目录中的以下目录：

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

如果/backup-lucene-indexes目录不存在，请备份/lucene-indexes目录，该目录也位于内容存储根目录中。 如果/backup-lucene-indexes目录存在，请不要备份/lucene-indexes目录，因为它可能会导致错误。

索引根目录在每个节点上的默认位置为`[aem-forms root]/lucene-indexes`。

## 客户安装的字体{#customer-installed-fonts}

如果您在AEM表单环境中安装了其他字体，则必须单独对其进行备份。 备份在管理控制台中的设置>核心系统>配置下指定的所有Adobe和客户字体目录。 确保备份整个字体目录。

>[!NOTE]
>
>默认情况下，随AEM Forms一起安装的Adobe字体位于`[aem-forms root]/fonts`目录中。

如果要重新初始化主机上的操作系统，并且希望使用先前操作系统的字体，则还应备份系统字体目录的内容。 （有关具体说明，请参阅操作系统的文档）。
