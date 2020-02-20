---
title: 流程报表入门
seo-title: 流程报表入门
description: 开始使用JEE Process Reporting中的AEM Forms时需要遵循的步骤
seo-description: 开始使用JEE Process Reporting中的AEM Forms时需要遵循的步骤
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# 流程报表入门{#getting-started-with-process-reporting}

通过流程报告，AEM Forms用户可以查询有关AEM Forms进程的信息，这些信息当前在AEM Forms实施中定义。 但是，进程报告不直接从AEM Forms存储库访问数据。 数据首先按计划发布到Process Reporting存储库(由ProcessDataPublisher和ProcessDataStorage *服务发*&#x200B;布)。 然后，进程报告中的报告和查询会从发布到存储库的进程报告数据中生成。 Process Reporting作为Forms Workflow模块的一部分安装。

本文详细介绍了启用将AEM Forms数据发布到Process Reporting存储库的步骤。 之后，您将能够使用进程报告来运行报告和查询。 本文还介绍了用于配置Process Reporting服务的选项。

## 流程报告先决条件 {#process-reporting-pre-requisites}

### 清除非必要流程 {#purge-non-essential-processes}

如果您当前使用的是表单工作流，则AEM表单数据库可能包含大量数据

Process Reporting发布服务将发布数据库中当前可用的所有AEM Forms数据。 这意味着，如果数据库包含您不想运行报告和查询的旧版数据，则所有这些数据也将发布到存储库，即使报告不需要这些数据。 建议您在运行服务之前清除此数据，以将数据发布到Process Reporting存储库。 这将改善发布者服务和查询数据以进行报告的服务的性能。

有关清除AEM Forms流程数据的详细信息，请参阅 [清除流程数据](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)。

>[!NOTE]
>
>有关清除实用程序的提示与技巧，请参阅Adobe开发人员连接文章中的清 [除进程和作业](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)。

## 配置Process Reporting服务 {#configuring-process-reporting-services}

### 计划流程数据发布 {#schedule-process-data-publishing}

Process Reporting服务按计划将数据从AEM Forms数据库发布到Process Reporting存储库。

此操作可能会占用大量资源，并会影响AEM Forms服务器的性能。 建议您在AEM Forms服务器繁忙时段之外计划此设置。

默认情况下，数据发布计划每天凌晨2:00运行。

执行以下步骤以更改发布计划：

>[!NOTE]
>
>如果您正在群集上运行AEM Forms实施，请对群集的每个节点执行以下步骤。

1. 停止AEM Forms服务器实例。
1.

    * （对于Windows）在编辑 `[JBoss root]/bin/run.conf.bat` 器中打开文件。
    * （对于Linux、AIX和Solaris） `[JBoss root]/bin/run.conf.sh` 文件。

1. 添加JVM参数 `-Dreporting.publisher.cron = <expression>.`

   示例：以下cron表达式导致流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 保存并关闭 `run.conf.bat` 文件。

1. 重新启动AEM Forms服务器实例。

1. 停止AEM Forms服务器实例。
1. 登录到WebSphere管理控制台。 在导航树中，单击“服 **务器** ” > “应 **用程序服务器** ” ，然后在右窗格中单击服务器名称。

1. 在“服务器基础结构”下，单 **击“Java”并单击“进程管理** ”>“ **进程定义”**。

1. 在“其他属性”下，单 **击“Java虚拟机”**。

   在通用JVM参数框中，添加参数 `-Dreporting.publisher.cron = <expression>.`

   **示例**:以下cron表达式导致流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击 **应用**，单击确定，然后单击 **直接保存到主配置**。
1. 重新启动AEM Forms服务器实例。
1. 停止AEM Forms服务器实例。
1. 登录到WebLogic管理控制台。 WebLogic管理控制台的默认地址为 `https://[hostname]:[port]/console`。
1. 在“更改中心”下，单击“ **锁定并编辑”**。
1. 在“域结构”下，单 **击“环境** ” > “ **服务器** ” ，然后在右侧窗格中单击受控服务器名称。
1. 在下一个屏幕上，单击“配置”选 **项卡** >“服 **务器开始** ”选项卡。
1. 在“参数”框中，添加JVM参数 `-Dreporting.publisher.cron = <expression>`。

   **示例**:以下cron表达式导致流程报表每5小时将AEM Forms数据发布到流程报表存储库：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击“ **保存** ”，然后单击“ **激活更改”**。
1. 重新启动AEM Forms服务器实例。

![processdapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服务 {#processdatastorage-service}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收进程数据，并将数据保存到Process Reporting存储库。

在每个发布周期中，数据都会保存到预定义根文件夹的子文件夹中。

您可以使用“管理”控制台配置根(默&#x200B;**认**: `/content/reporting/pm`)位置和子文件夹(**默认**:( `/yyyy/mm/dd/hh/mi/ss`)存储流程数据的层次结构格式。

#### 配置Process Reporting存储库位置 {#to-configure-the-process-reporting-repository-locations}

1. 使用管理员凭 **据登录到Administration Console** 。 管理控制台的默认URL是 `https://[server]:[port]/adminui`
1. 导航到 **Home** > Services **> Applications** and Services > ************ Service Management进程和Home Management DataStorageProviderServiceServiceServicesServiceServicesService。

   ![过程数据存储服务](assets/process-data-storage-service.png)

   **RootFolder**

   存储进程数据以用于报告的CRX位置。

   `Default`: `/content/reporting/pm`

   **文件夹层次结构**

   根据进程创建时间存储进程数据的文件夹层次结构。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 单击&#x200B;**保存**。

### ReportConfiguration服务 {#reportconfiguration-service}

ReportConfiguration服务由Process Reporting用于配置进程报表查询服务。

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. 使用CRX管理员 **凭据登录到Configuration Manager** 。 配置管理器的默认URL是 `https://[server]:[port]/lc/system/console/configMgr`
1. 打开 **ReportingConfiguration** 服务。
1. **记录数**

   在存储库上运行查询时，结果可能包含大量记录。 如果结果集较大，则查询执行可能会占用服务器资源。

   要处理大的结果集，ReportConfiguration服务会将查询处理拆分为多批记录。 这样可减轻系统负载。

   `Default`: `1000`

   **CRX存储路径**

   存储进程数据以用于报告的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >这与在ProcessDataStorage配置选项根文件夹中指定的位 **置相同**。
   >
   >
   >如果更新ProcessDataStorage配置中的“根文件夹”选项，则需要更新ReportConfiguration服务中的“CRX存储路径”位置。

1. 单击 **保存** ，然后关 **闭CQ配置管理器**。

### ProcessDataPublisher服务 {#processdatapublisher-service}

ProcessDataPublisher服务从AEM Forms数据库导入进程数据，并将数据发布到ProcessDataStorageProvider服务进行存储。

#### 配置ProcessDataPublisher服务 {#to-configure-processdatapublisher-service-nbsp}

1. 使用管理员凭 **据登录到Administration Console** 。

   默认URL为 `https://[server]:port]/adminui/`。

1. 导航到“ **主页** ”>“服务 **”** >“应用程序和服务” ************ >“应用程序和服务”>“开放管理和Publisher Service service数据”。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**发布数据**

启用此选项可开始发布流程数据。 默认情况下，此选项处于禁用状态。

仅当与Process Reporting组件相关的所有配置都设置得当时，才可启用Process Reporting。

或者，当流程数据不再需要时，使用此选项可以禁用流程数据发布。

`Default`: `Off`

**批处理间隔（秒）**

每次运行ProcessDataPublisher服务时，服务首先按“批处理间隔”拆分自上次运行服务以来的时间。 然后，该服务将分别处理AEM Forms数据的每个间隔。

这有助于控制发布者处理的数据在周期内的每次运行（批处理）期间端到端的大小。

例如，如果发布者每天运行，而不是在单次运行中处理一天的整个数据，默认情况下，它会将处理分为24批，每批1小时。

`Default`: `3600`

`Unit`: `Seconds`

**锁定超时（秒）**

发布者服务在开始处理数据时获得锁，使得发布者的多个实例不同时开始运行和处理数据。

如果已获取锁的发布者服务在“锁定超时”值定义的秒数内处于空闲状态，则释放其锁，以便其他发布者服务实例可以继续处理。

`Default`: `3600`

`Unit`: `Seconds`

**发布数据自**

AEM Forms环境包含设置该环境时的数据。

默认情况下，ProcessDataPublisher服务从AEM Forms数据库导入所有数据。

根据您的报告需求，如果您计划在特定日期和时间后对数据运行报告和查询，建议您指定日期和时间。 然后，发布服务将从该时间开始发布日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 访问Process Reporting用户界面 {#accessing-the-process-reporting-user-interface}

进程报表的用户界面基于浏览器。

在设置Process Reporting后，您可以在AEM Forms安装中的以下位置开始使用Process Reporting:

`https://<server>:<port>/lc/pr`

### 登录到进程报告 {#log-in-to-process-reporting}

当您导航到Process Reporting URL(https://&lt;server>:&lt;port>/lc/pr)时，将显示登录屏幕。

指定凭据以登录到Process Reporting模块。

>[!NOTE]
>
>要登录到Process Reporting用户界面，您需要以下AEM Forms权限：
>
>`PERM_PROCESS_REPORTING_USER`

![登录进程报告](assets/capture1_new.png)

登录到Process Reporting时，将显示“ **[!UICONTROL 主页]** ”屏幕。

### 进程报告主屏幕 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**** “流程报表”树视图：“主页”屏幕左侧的树视图包含“进程报告”模块的项。

树视图由以下顶级项目组成：

**** 报告：此项目包含随“流程报表”一起提供的现成报表。

有关预定义报表的详细信息，请参 [阅Pre-defined Reporting in Process](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**** 临时查询：此项目包含对进程和任务执行基于筛选器的搜索的选项。

有关专门查询的详细信息，请参 [阅进程报告中的专门查询](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**** 自定义：“自定义”节点显示您创建的自定义报告。

有关创建和显示自定义报告的过程，请参阅“在进 [程中自定义报告”](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**** 流程报表标题栏：“进程报表”标题栏包含一些通用选项，在用户界面中工作时可以使用这些选项。

**** 流程报告标题：“流程报表”标题显示在标题栏的左角。

随时单击标题以返回主屏幕。

**** 上次更新时间：进程数据将按计划从AEM Forms数据库发布到Process Reporting存储库。

“上次更新时间”显示将数据更新推送到Process Reporting存储库的上次日期和时间。

有关数据发布服务以及如何计划此服务的详细信息，请参阅 [Process Reporting快速入门文章中的](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) Schedule process data publishing（计划流程数据发布）。

**** Process Reporting用户：登录的用户名显示在上次更新时间的右侧。

**** 流程报表标题栏下拉列表：Process Reporting标题栏右角的下拉列表包含以下选项：

* **[!UICONTROL 同步]**:将嵌入的Process Reporting存储库与AEM Forms数据库同步。
* **[!UICONTROL 帮助]**:查看有关流程报告的帮助文档。
* **[!UICONTROL 注销]**:注销进程报告

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
