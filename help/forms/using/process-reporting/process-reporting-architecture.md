---
title: 流程报告的工作原理
seo-title: 流程报告的工作原理
description: 关于JEE流程报告的AEM Forms服务描述和流程报告UI介绍
seo-description: 关于JEE流程报告的AEM Forms服务描述和流程报告UI介绍
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 流程报告的工作原理{#how-process-reporting-works}

流程报告是AEM Forms在JEE上的报告模块。

流程报告允许您运行关于AEM Forms流程和任务的报告。

流程报告使用嵌入式流程报告库发布Forms数据。 然后，它使用该数据运行报告。

流程报告包括以下模块：

* [ProcessDataPublisher服务](#processdatapublisher-service-br-p)
* [ProcessDataStorage服务](#processdatastorageprovider-service-br-p)
* [OSGi服务](#osgi-service-br-p)
* [查询数据servlet](#querydataservlet-service-br-p)
* [进程报告用户界面](#process-reporting-user-interface-br-p)

## 进程报告架构{#process-reporting-architecture-br}

![处理报告架构](assets/processreportingarchitecture.png)

## 进程报告模块{#process-reporting-modules}

### ProcessDataPublisher服务{#processdatapublisher-service-br}

ProcessDataPublisher服务器定期在AEM Forms数据库上运行，并提取自上次运行服务后更改的数据。 然后，它将数据发布到“流程数据”存储服务。

有关配置服务的详细信息，请参阅[配置ProcessDataPublisher服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)。

### ProcessDataStorageProvider服务{#processdatastorageprovider-service-br}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收进程数据并将数据保存到进程报告库。

有关配置服务的详细信息，请参阅[配置ProcessDataStorageProvider服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)。

### OSGi服务{#osgi-service-br}

QueryDataServlet使用此服务从“进程报告”存储库获取报告数据。

### QueryDataServlet服务{#querydataservlet-service-br}

QueryDataServlet服务接受来自进程查询报告用户界面的数据。

然后，该服务使用OSGi服务来获取相关报告数据，处理该数据，并将该数据返回给该用户界面。

### 进程报告用户界面{#process-reporting-user-interface-br}

进程报告用户界面是基于Web浏览器的界面。 使用此接口视图从AEM Forms数据库发布的流程和任务信息。

有关“进程报告”用户界面的介绍，请参阅[“进程报告”用户界面](/help/forms/using/process-reporting/introduction-process-reporting.md)。

### QueryDataServlet服务{#querydataservlet-service-br-1}

QueryDataServlet服务接受来自进程查询报告用户界面的数据。

然后，该服务使用OSGi服务来获取相关报告数据，处理该数据，并将该数据返回给该用户界面。

### 自定义报告{#custom-reports-br}

您可以创建自己的自定义报告，并在“流程报告”用户界面的“自定义报告”选项卡中显示这些报告。

有关创建自定义报告的步骤，请参阅文章[在处理中自定义报告报告](/help/forms/using/process-reporting/process-reporting-custom-reports.md)中的创建自定义报告。
