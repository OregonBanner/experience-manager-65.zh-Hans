---
title: 运行状况监视器概述
description: 本文档提供了运行状况监视器的概述以及有关访问方式的详细信息。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 运行状况监视器概述 {#overview-of-health-monitor}

运行状况监视器提供有关AEM表单系统的重要信息，如服务器信息、内存使用情况和处理器使用情况。 还提供Work Manager统计数据，如队列中的工作项或作业数量及其状态。 您可以使用运行状况监视器执行以下任务：

* 验证系统是否正常运行
* 查看信息以帮助诊断发生的系统问题
* 对显示问题的工作项或作业执行操作
* 从Job Manager数据库中清除过时记录

管理控制台中的“运行状况监视器”页面有三个选项卡：

* “系统”选项卡显示资源监视图表和有关Forms Server（或群集环境中的节点）的信息。 (请参阅 [查看系统信息](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* “工作管理器”选项卡显示与“工作管理器”相关的数据，例如“工作管理器”队列中的工作项数。 您可以使用各种标准筛选信息，或使用操作工具管理单个工作项。 (请参阅 [查看与工作管理器相关的统计信息](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* 使用“作业清除计划程序”选项卡，您可以从Job Manager数据库中清除过时的记录。 (请参阅 [从作业管理器数据库中清除记录](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

“运行状况监视器”网页中填充了通过Gemfire API收集的统计数据。 此API会自动发现群集中的所有节点。 它还解决了从代理服务器或负载平衡器后面收集统计信息时出现的安全问题。 Java选项可用于微调运行状况监视器，从而减少对AEM表单环境性能的影响。 (请参阅 [微调运行状况监视器性能](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**访问运行状况监视器**

1. 在管理控制台中，单击页面右上角的运行状况监视器。
