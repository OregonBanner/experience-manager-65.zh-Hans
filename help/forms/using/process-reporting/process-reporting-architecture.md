---
title: 流程报告的工作方式
description: 组成AEM Forms on JEE流程报表的服务描述以及流程报表UI简介
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 流程报告的工作方式{#how-process-reporting-works}

流程报表是JEE上的AEM Forms的报表模块。

通过进程报告，可运行AEM Forms进程和任务报告。

进程报表使用嵌入的进程报表存储库发布Forms数据。 然后，它使用该数据来运行报表。

“进程报告”包含以下模块：

* [ProcessDataPublisher服务](#processdatapublisher-service-br-p)
* [ProcessDataStorage服务](#processdatastorageprovider-service-br-p)
* [OSGi服务](#osgi-service-br-p)
* [查询数据servlet](#querydataservlet-service-br-p)
* [Process Reporting用户界面](#process-reporting-user-interface-br-p)

## 流程报告体系结构 {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## 流程报告模块 {#process-reporting-modules}

### ProcessDataPublisher服务 {#processdatapublisher-service-br}

ProcessDataPublisher服务器定期在AEM Forms数据库上运行，并提取自上次运行服务以来更改的数据。 然后，它将数据发布到Process Data Storage服务。

有关配置服务的详细信息，请参阅 [配置ProcessDataPublisher服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### ProcessDataStorageProvider服务 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收流程数据，并将该数据保存到Process Reporting存储库。

有关配置服务的详细信息，请参阅 [配置ProcessDataStorageProvider服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### OSGi服务 {#osgi-service-br}

QueryDataServlet使用此服务从Process Reporting存储库获取报表数据。

### QueryDataServlet服务 {#querydataservlet-service-br}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获取相关报表数据，处理该数据，并将该数据返回到用户界面。

### Process Reporting用户界面 {#process-reporting-user-interface-br}

进程报表用户界面是一个基于Web浏览器的界面。 您可以使用此界面查看从AEM Forms数据库发布的进程和任务信息。

有关Process Reporting用户界面的介绍，请参见 [Process Reporting用户界面](/help/forms/using/process-reporting/introduction-process-reporting.md).

### QueryDataServlet服务 {#querydataservlet-service-br-1}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获取相关报表数据，处理该数据，并将该数据返回到用户界面。

### 自定义报表 {#custom-reports-br}

您可以创建自己的自定义报表，并在“流程报表”用户界面的“自定义报表”选项卡中显示这些报表。

有关创建自定义报表的步骤，请参阅文章中的创建自定义报表 [正在报告中的自定义报表](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
