---
title: 流程报表的工作原理
seo-title: 流程报表的工作原理
description: JEE流程报表上的AEM Forms组成服务的说明以及流程报表UI的介绍
seo-description: JEE流程报表上的AEM Forms组成服务的说明以及流程报表UI的介绍
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 流程报表的工作原理{#how-process-reporting-works}

进程报告是JEE上AEM Forms的报告模块。

“流程报告”允许您对AEM Forms进程和任务运行报告。

Process Reporting使用嵌入的Process Reporting存储库发布Forms数据。 然后，它使用该数据运行报告。

Process Reporting由以下模块组成：

* [ProcessDataPublisher服务](#processdatapublisher-service-br-p)
* [ProcessDataStorage服务](#processdatastorageprovider-service-br-p)
* [OSGi服务](#osgi-service-br-p)
* [查询数据Servlet](#querydataservlet-service-br-p)
* [进程报告用户界面](#process-reporting-user-interface-br-p)

## 流程报告架构 {#process-reporting-architecture-br}

![处理报告架构](assets/processreportingarchitecture.png)

## 流程报告模块 {#process-reporting-modules}

### ProcessDataPublisher服务 {#processdatapublisher-service-br}

ProcessDataPublisher服务器定期在AEM Forms数据库上运行，并提取自上次运行服务以来已更改的数据。 然后，它将数据发布到进程数据存储服务。

有关配置服务的详细信息，请参 [阅配置ProcessDataPublisher服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProvider服务 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收进程数据，并将数据保存到Process Reporting存储库。

有关配置服务的详细信息，请参 [阅配置ProcessDataStorageProvider服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)。

### OSGi服务 {#osgi-service-br}

QueryDataServlet使用此服务从Process Reporting存储库获取报表数据。

### QueryDataServlet服务 {#querydataservlet-service-br}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获得相关的报告数据，处理该数据，并将该数据返回到用户界面。

### 进程报告用户界面 {#process-reporting-user-interface-br}

Process Reporting用户界面是基于Web浏览器的界面。 使用此界面可以查看从AEM Forms数据库发布的进程和任务信息。

有关Process Reporting用户界面的介绍，请参阅 [Process Reporting用户界面](/help/forms/using/process-reporting/introduction-process-reporting.md)。

### QueryDataServlet服务 {#querydataservlet-service-br-1}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获得相关的报告数据，处理该数据，并将该数据返回到用户界面。

### 自定义报告 {#custom-reports-br}

您可以创建自己的自定义报告，并在Process Reporting用户界面的“自定义报告”选项卡中显示这些报告。

有关创建自定义报告的步骤，请参阅Custom Reports in Process Reporting（流程中的自定义报告） [文章中的创建自定义报告](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
