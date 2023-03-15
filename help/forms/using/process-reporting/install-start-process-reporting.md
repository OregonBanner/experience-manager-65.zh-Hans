---
title: 开始使用流程报告
seo-title: Getting Started with Process Reporting
description: 开始使用AEM Forms on JEE流程报告时需要遵循的步骤
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# 开始使用流程报告{#getting-started-with-process-reporting}

利用Process Reporting，AEM Forms用户可以查询有关当前在AEM Forms实施中定义的AEM Forms流程的信息。 但是，流程报表不会直接从AEM Forms存储库访问数据。 数据首先会按计划发布到Process Reporting存储库(*通过ProcessDataPublisher和ProcessDataStorage服务* s)。 然后，使用发布到存储库的“流程报告”数据生成“流程报告”中的报告和查询。 Process Reporting作为Forms Workflow模块的一部分安装。

本文详细介绍了将AEM Forms数据发布到Process Reporting存储库的步骤。 之后，您将能够使用“进程报告”来运行报告和查询。 本文还介绍了可用于配置Process Reporting服务的选项。

## 流程报告先决条件 {#process-reporting-pre-requisites}

### 清除非必需流程 {#purge-non-essential-processes}

如果您当前使用的是Forms Workflow，则AEM Forms数据库可能包含大量数据

Process Reporting发布服务将发布数据库中当前可用的所有AEM Forms数据。 这意味着，如果数据库包含您不想对其运行报告和查询的旧数据，则所有此类数据也将发布到存储库，即使报表不需要这些数据也是如此。 建议您在运行服务以将数据发布到Process Reporting存储库之前清除此数据。 这将提高发布者服务和查询报告数据的服务的性能。

有关清除AEM Forms流程数据的详细信息，请参阅 [清除流程数据](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>有关清除实用程序的提示和技巧，请参阅Adobe Developer Connection文章，网址为 [清除流程和作业](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## 配置进程Reporting Services {#configuring-process-reporting-services}

### 计划流程数据发布 {#schedule-process-data-publishing}

Process Reporting Services会按计划将数据从AEM Forms数据库发布到Process Reporting存储库。

此操作可能会占用大量资源，并且可能会影响AEM Forms服务器的性能。 建议在AEM Forms服务器忙碌时段之外计划此项。

默认情况下，数据发布安排在每天凌晨2:00运行。

执行以下步骤以更改发布计划：

>[!NOTE]
>
>如果您在群集上运行AEM Forms实施，请在群集的每个节点上执行以下步骤。

1. 停止AEM Forms服务器实例。
1. &#x200B;

   * （对于Windows）打开 `[JBoss root]/bin/run.conf.bat` 文件中的文件。
   * （对于Linux、AIX和Solaris） `[JBoss root]/bin/run.conf.sh` 文件中的文件。

1. 添加JVM参数 `-Dreporting.publisher.cron = <expression>.`

   示例：以下cron表达式导致Process Reporting每5小时将AEM Forms数据发布到Process Reporting存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 保存并关闭 `run.conf.bat` 文件。

1. 重新启动AEM Forms服务器实例。

1. 停止AEM Forms服务器实例。
1. 登录到WebSphere管理控制台。 在导航树中，单击 **服务器** > **应用程序服务器** 然后，在右窗格中，单击服务器名称。

1. 在服务器基础结构下，单击 **Java和进程管理** > **流程定义**.

1. 在“其他属性”下，单击 **Java虚拟机**.

   在“通用JVM参数”框中，添加参数 `-Dreporting.publisher.cron = <expression>.`

   **示例**：以下cron表达式导致Process Reporting每5小时将AEM Forms数据发布到Process Reporting存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击 **应用**，单击“确定” ，然后单击 **直接保存到主控配置**.
1. 重新启动AEM Forms服务器实例。
1. 停止AEM Forms服务器实例。
1. 登录到WebLogic管理控制台。 WebLogic管理控制台的默认地址为 `https://[hostname]:[port]/console`.
1. 在更改中心下，单击 **锁定和编辑**.
1. 在“域结构”下，单击 **环境** > **服务器** 然后，在右窗格中，单击受控服务器名称。
1. 在下一个屏幕上，单击 **配置** 选项卡> **服务器启动** 选项卡。
1. 在参数框中，添加JVM参数 `-Dreporting.publisher.cron = <expression>`.

   **示例**：以下cron表达式导致Process Reporting每5小时将AEM Forms数据发布到Process Reporting存储库：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击 **保存** 然后单击 **激活更改**.
1. 重新启动AEM Forms服务器实例。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage服务 {#processdatastorage-service}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收流程数据，并将该数据保存到Process Reporting存储库。

在每个发布周期，数据都会保存到预定义根文件夹的子文件夹中。

您可以使用管理控制台来配置根(**默认**： `/content/reporting/pm`)位置和子文件夹(**默认**： `/yyyy/mm/dd/hh/mi/ss`)存储流程数据的层次结构格式。

#### 配置“进程报告”存储库位置 {#to-configure-the-process-reporting-repository-locations}

1. 登录 **管理控制台** 使用管理员凭据。 管理控制台的默认URL为 `https://'[server]:[port]'/adminui`
1. 导航到 **主页** > **服务** > **应用程序和服务** >**服务管理** 然后打开 **ProcessDataStorageProvider** 服务。

   ![process-data-store-service](assets/process-data-storage-service.png)

   **根文件夹**

   存储流程数据以用于报表的CRX位置。

   `Default`： `/content/reporting/pm`

   **文件夹层次结构**

   根据流程创建时间将存储流程数据的文件夹层次结构。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 单击“**保存**”。

### ReportConfiguration服务 {#reportconfiguration-service}

ReportConfiguration服务由Process Reporting用于配置进程报告查询服务。

#### 配置ReportingConfiguration服务 {#to-configure-the-reportingconfiguration-service}

1. 登录 **配置管理器** 具有CRX管理员凭据。 Configuration Manager的默认URL为 `https://'[server]:[port]'/lc/system/console/configMgr`
1. 打开 **报告配置** 服务。
1. **记录数**

   在存储库上运行查询时，结果可能包含大量记录。 如果结果集很大，则查询执行可能会占用服务器资源。

   为了处理大型结果集，ReportConfiguration服务将查询处理拆分为多批记录。 这减少了系统负载。

   `Default`: `1000`

   **CRX存储路径**

   存储流程数据以用于报表的CRX位置。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >此位置与ProcessDataStorage配置选项中指定的位置相同 **根文件夹**.
   >
   >
   >如果更新ProcessDataStorage配置中的Root Folder选项，则需要更新ReportConfiguration服务中的CRX存储路径位置。

1. 单击 **保存** 并关闭 **CQ配置管理器**.

### ProcessDataPublisher服务 {#processdatapublisher-service}

ProcessDataPublisher服务从AEM Forms数据库导入进程数据，并将该数据发布到ProcessDataStorageProvider服务进行存储。

#### 配置ProcessDataPublisher服务的步骤   {#to-configure-processdatapublisher-service-nbsp}

1. 登录 **管理控制台** 使用管理员凭据。

   默认URL为 `https://'server':port]/adminui/`.

1. 导航到 **主页** > **服务** > **应用程序和服务** >**服务管理** 然后打开 **ProcessDataPublish** 服务。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**发布数据**

启用此选项以开始发布流程数据。 默认情况下，该选项处于禁用状态。

只有在正确设置了与Process Reporting组件相关的所有配置时，才启用Process Reporting。

或者，使用此选项可在不再需要流程数据发布时禁用它。

`Default`: `Off`

**批次间隔（秒）**

每次ProcessDataPublisher服务运行时，该服务都会按批处理间隔第一次分割自上次运行该服务以来的时间。 然后，该服务将分别处理每个AEM Forms数据间隔。

这有助于控制发布器流程在一个周期内的每次运行（批处理）期间端到端的数据大小。

例如，如果发布器每天运行，则默认情况下，它会将处理过程拆分为24批处理，每批处理1小时，而不是在单个运行中处理一天的所有数据。

`Default`: `3600`

`Unit`: `Seconds`

**锁定超时（秒）**

发布器服务在开始处理数据时获得锁定，以便发布器的多个实例不会同时开始运行和处理数据。

如果获得锁的发布服务器服务在“锁定超时”值定义的秒数内处于空闲状态，则会释放其锁，以便其他发布服务器服务实例可以继续处理。

`Default`: `3600`

`Unit`: `Seconds`

**发布数据来源**

AEM Forms环境包含从设置环境时开始的数据。

默认情况下，ProcessDataPublisher服务从AEM Forms数据库导入所有数据。

根据您的报告需求，如果您计划在特定日期和时间后运行关于数据的报告和查询，建议您指定日期和时间。 发布服务随后将发布该时间之后的日期。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## 访问“进程报告”用户界面 {#accessing-the-process-reporting-user-interface}

“流程报表”的用户界面基于浏览器。

设置Process Reporting后，您可以在AEM Forms安装中的以下位置开始使用Process Reporting：

`https://<server>:<port>/lc/pr`

### 登录到流程报告 {#log-in-to-process-reporting}

导航到流程报表URL时(https://)&lt;server>：&lt;port>/lc/pr)，将显示登录屏幕。

指定用于登录到“进程报告”模块的凭据。

>[!NOTE]
>
>要登录“流程报表”用户界面，您需要具有以下AEM Forms权限：
>
>`PERM_PROCESS_REPORTING_USER`

![登录流程报告](assets/capture1_new.png)

当您登录Process Reporting时， **[!UICONTROL 主页]** 屏幕显示。

### 流程报告主屏幕 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**进程报告树视图：** 主屏幕左侧的树视图包含流程报告模块的项目。

树视图由以下顶级项目组成：

**报告：** 此项目包含随Process Reporting一起提供的现成报告。

有关预定义报表的详细信息，请参阅 [预定义的报告正在处理报告](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**临时查询：** 此项目包含对进程和任务执行基于过滤器的搜索的选项。

有关临时查询的详细信息，请参阅 [进程报告中的临时查询](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**自定义：** “自定义”节点显示您创建的自定义报表。

有关创建和显示自定义报表的过程，请参阅 [正在报告中的自定义报表](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**进程报告标题栏：** 进程报表标题栏包含一些可在用户界面中使用的通用选项。

**进程报告标题：** 标题栏的左角显示流程报告标题。

随时单击标题以返回主屏幕。

**上次更新时间：** 流程数据会按计划从AEM Forms数据库发布到Process Reporting存储库。

“上次更新时间”显示数据更新被推送到Process Reporting存储库的最后日期和时间。

有关数据发布服务以及如何计划此服务的详细信息，请参阅 [计划流程数据发布](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) 在进程报告快速入门一文中。

**进程报告用户：** 登录用户名显示在上次更新时间的右侧。

**“流程报表”标题栏下拉列表：** Process Reporting标题栏右角的下拉列表包含以下选项：

* **[!UICONTROL 同步]**：将嵌入式进程报表存储库与AEM Forms数据库同步。
* **[!UICONTROL 帮助]**：查看有关流程报告的帮助文档。
* **[!UICONTROL 注销]**：注销流程报表
