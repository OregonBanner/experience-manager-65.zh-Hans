---
title: 流程报告入门
seo-title: 流程报告入门
description: 开始使用AEM Forms on JEE Process Reporting时需要遵循的步骤
seo-description: 开始使用AEM Forms on JEE Process Reporting时需要遵循的步骤
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---

# 进程报告入门{#getting-started-with-process-reporting}

通过流程报表，AEM Forms用户能够查询有关AEM Forms实施中当前定义的AEM Forms流程的信息。 但是，“流程报表”不会直接从AEM Forms存储库访问数据。 数据首先按计划（*由ProcessDataPublisher &amp; ProcessDataStorage服务* s）发布到Process Reporting存储库。 然后，从发布到存储库的Process Reporting数据中生成Process Reporting中的报表和查询。 “流程报表”作为Forms Workflow模块的一部分安装。

本文详细介绍了将AEM Forms数据发布到Process Reporting存储库的步骤。 之后，您将能够使用“流程报表”来运行报表和查询。 本文还介绍了可用于配置Process Reporting服务的选项。

## 流程报告先决条件{#process-reporting-pre-requisites}

### 清除非必要流程{#purge-non-essential-processes}

如果您当前使用的是Forms Workflow,AEM Forms数据库可能包含大量数据

流程报表发布服务将发布数据库中当前可用的所有AEM Forms数据。 这意味着，如果数据库包含您不希望运行报告和查询的旧数据，则所有这些数据也将发布到存储库，即使报告不需要它。 建议您在运行服务之前清除此数据，以将数据发布到Process Reporting存储库。 这将提高发布者服务和查询数据以进行报告的服务的性能。

有关清除AEM Forms进程数据的详细信息，请参阅[清除进程数据](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)。

>[!NOTE]
>
>有关清除实用程序的提示和技巧，请参阅[清除流程和作业](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)上的Adobe Developer Connection文章。

## 配置Process Reporting服务{#configuring-process-reporting-services}

### 计划进程数据发布{#schedule-process-data-publishing}

Process Reporting服务按计划将数据从AEM Forms数据库发布到Process Reporting存储库。

此操作可能会占用大量资源，并且会影响AEM Forms服务器的性能。 建议您在AEM Forms服务器繁忙时段之外计划此时间。

默认情况下，数据发布计划每天凌晨2:00运行。

执行以下步骤以更改发布计划：

>[!NOTE]
>
>如果您在群集上运行AEM Forms实施，请对群集的每个节点执行以下步骤。

1. 停止AEM Forms服务器实例。
1. &#x200B;

   * （对于Windows）在编辑器中打开`[JBoss root]/bin/run.conf.bat`文件。
   * （对于Linux、AIX和Solaris）编辑器中的`[JBoss root]/bin/run.conf.sh`文件。

1. 添加JVM参数`-Dreporting.publisher.cron = <expression>.`

   示例：以下cron表达式会使流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 保存并关闭`run.conf.bat`文件。

1. 重新启动AEM Forms服务器实例。

1. 停止AEM Forms服务器实例。
1. 登录到WebSphere管理控制台。 在导航树中，单击&#x200B;**Servers** > **Application servers**，然后在右侧窗格中单击服务器名称。

1. 在“服务器基础架构”下，单击&#x200B;**Java和进程管理** > **进程定义**。

1. 在“其他属性”下，单击&#x200B;**Java虚拟机**。

   在通用JVM参数框中，添加参数`-Dreporting.publisher.cron = <expression>.`

   **示例**:以下cron表达式会使流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击&#x200B;**Apply**，单击“确定”，然后单击“直接保存到主控配置&#x200B;**”。**
1. 重新启动AEM Forms服务器实例。
1. 停止AEM Forms服务器实例。
1. 登录到WebLogic管理控制台。 WebLogic管理控制台的默认地址为`https://[hostname]:[port]/console`。
1. 在“更改中心”下，单击&#x200B;**锁定并编辑**。
1. 在“域结构”下，单击&#x200B;**环境** > **服务器**，然后在右窗格中单击受管服务器名称。
1. 在下一个屏幕上，单击&#x200B;**Configuration**&#x200B;选项卡> **Server Start**&#x200B;选项卡。
1. 在参数框中，添加JVM参数`-Dreporting.publisher.cron = <expression>`。

   **示例**:以下cron表达式会使流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击&#x200B;**Save**，然后单击&#x200B;**Activate Changes**。
1. 重新启动AEM Forms服务器实例。

![processdatabublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服务{#processdatastorage-service}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收进程数据，并将数据保存到Process Reporting存储库。

在每个发布周期，数据都会保存到预定义根文件夹的子文件夹中。

您可以使用管理控制台配置根(**default**):`/content/reporting/pm`位置和子文件夹(**default**):`/yyyy/mm/dd/hh/mi/ss`)将存储流程数据的层次结构格式。

#### 配置Process Reporting存储库位置{#to-configure-the-process-reporting-repository-locations}

1. 使用管理员凭据登录到&#x200B;**管理控制台**。 管理控制台的默认URL为`https://'[server]:[port]'/adminui`
1. 导航到&#x200B;**Home** > **Services** > **Applications and Services** >**Service Management**&#x200B;并打开&#x200B;**ProcessDataStorageProvider**&#x200B;服务。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **根文件夹**

   存储流程数据以进行报告的CRX位置。

   `Default`: `/content/reporting/pm`

   **文件夹层次结构**

   根据流程创建时间存储流程数据的文件夹层次结构。

   `Default`:  `/yyyy/mm/dd/hh/mi/ss`

1. 单击&#x200B;**保存**。

### ReportConfiguration服务{#reportconfiguration-service}

ReportConfiguration服务由Process Reporting用于配置Process Reporting查询服务。

#### 配置ReportingConfiguration服务{#to-configure-the-reportingconfiguration-service}

1. 使用CRX管理员凭据登录到&#x200B;**Configuration Manager**。 Configuration Manager的默认URL为`https://'[server]:[port]'/lc/system/console/configMgr`
1. 打开&#x200B;**ReportingConfiguration**&#x200B;服务。
1. **记录数**

   在存储库上运行查询时，结果可能包含大量记录。 如果结果集较大，则查询执行可能会占用服务器资源。

   要处理大的结果集， ReportConfiguration服务会将查询处理拆分为多个记录批次。 这可减少系统负载。

   `Default`:  `1000`

   **CRX存储路径**

   存储流程数据以进行报告的CRX位置。

   `Default`:  `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置与ProcessDataStorage配置选项&#x200B;**根文件夹**&#x200B;中指定的位置相同。
   >
   >
   >如果更新ProcessDataStorage配置中的根文件夹选项，则需要更新ReportConfiguration服务中的CRX存储路径位置。

1. 单击&#x200B;**Save**&#x200B;并关闭&#x200B;**CQ Configuration Manager**。

### ProcessDataPublisher服务{#processdatapublisher-service}

ProcessDataPublisher服务从AEM Forms数据库导入流程数据，并将该数据发布到ProcessDataStorageProvider服务以进行存储。

#### 配置ProcessDataPublisher服务   {#to-configure-processdatapublisher-service-nbsp}

1. 使用管理员凭据登录到&#x200B;**管理控制台**。

   默认URL为`https://'server':port]/adminui/`。

1. 导航到&#x200B;**Home** > **Services** > **Applications and Services** >**Service Management**&#x200B;并打开&#x200B;**ProcessDataPublisher**&#x200B;服务。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**发布数据**

启用此选项可开始发布流程数据。 默认情况下，选项处于禁用状态。

仅当与流程报表组件相关的所有配置均已正确设置时，才启用流程报表。

或者，如果流程数据不再需要，则使用此选项可禁用流程数据发布。

`Default`:  `Off`

**批处理间隔（秒）**

每次运行ProcessDataPublisher服务时，服务首先会按批处理间隔分配自上次运行服务以来的时间。 然后，该服务会单独处理AEM Forms数据的每个间隔。

这有助于控制发布者处理的数据在周期内每次运行（批处理）期间端到端的大小。

例如，如果发布者每天运行，则默认情况下，它会将处理分为24批，每批1小时，而不是在单次运行中处理一天的整个数据。

`Default`:  `3600`

`Unit`:  `Seconds`

**锁定超时（秒）**

发布者服务在开始处理数据时会获得锁定，这样发布者的多个实例就不会同时开始运行和处理数据。

如果已获得锁的发布者服务在“锁定超时”值定义的秒数内处于空闲状态，则其锁将被释放，以便其他发布者服务实例可以继续处理。

`Default`:  `3600`

`Unit`:  `Seconds`

**从发布数据**

AEM Forms环境包含环境设置后的数据。

默认情况下， ProcessDataPublisher服务会从AEM Forms数据库导入所有数据。

根据您的报表需求，如果您计划在特定日期和时间后对数据运行报表和查询，则建议您指定日期和时间。 然后，发布服务将从该时间开始发布日期。

`Default`:  `01-01-1970 00:00:00`

`Format`:  `dd-MM-yyyy HH:mm:ss`

## 访问Process Reporting用户界面{#accessing-the-process-reporting-user-interface}

流程报表的用户界面基于浏览器。

在设置Process Reporting后，您可以在AEM Forms安装中的以下位置开始使用Process Reporting :

`https://<server>:<port>/lc/pr`

### 登录以处理报告{#log-in-to-process-reporting}

导航到流程报表URL(https://&lt;server>:&lt;port>/lc/pr)时，会显示登录屏幕。

指定您的凭据以登录到“流程报告”模块。

>[!NOTE]
>
>要登录到Process Reporting用户界面，您需要以下AEM Forms权限：
>
>`PERM_PROCESS_REPORTING_USER`

![登录流程报表](assets/capture1_new.png)

登录Process Reporting后，将显示&#x200B;**[!UICONTROL Home]**&#x200B;屏幕。

### 进程报告主屏幕{#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**“流程报告”树视图：** “主页”屏幕左侧的树视图包含“流程报告”模块的项目。

树视图包含以下顶级项目：

**报表：** 此项目包含随“流程报表”一起提供的现成报表。

有关预定义报表的详细信息，请参阅[Pre-defined Reporting in Process Reporting](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**临时查询：** 此项目包含用于对流程和任务执行基于过滤器的搜索的选项。

有关临时查询的详细信息，请参阅[Ad-hoc Queries in Process Reporting](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**自定义：** 自定义节点显示您创建的自定义报表。

有关创建和显示自定义报表的过程，请参阅[Custom Reports in Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**“流程报表”标题栏：** “流程报表”标题栏包含一些在用户界面中工作时可以使用的通用选项。

**流程报表标题：** “流程报表”标题显示在标题栏的左角。

随时单击标题以返回主屏幕。

**上次更新时间：** 流程数据按计划从AEM Forms数据库发布到流程报表存储库。

“上次更新时间”显示将数据更新推送到流程报表存储库的上次日期和时间。

有关数据发布服务以及如何计划此服务的详细信息，请参阅流程报告快速入门文章中的[计划流程数据发布](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)。

**流程报表用户：** 登录用户名显示在“上次更新”时间的右侧。

**“流程报表”标题栏下拉列表：** “流程报表”标题栏右上角的下拉列表包含以下选项：

* **[!UICONTROL 同步]**:将嵌入的Process Reporting存储库与AEM Forms数据库同步。
* **[!UICONTROL 帮助]**:查看有关流程报告的帮助文档。
* **[!UICONTROL 注销]**:注销流程报表
