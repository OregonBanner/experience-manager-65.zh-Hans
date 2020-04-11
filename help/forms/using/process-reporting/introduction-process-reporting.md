---
title: 流程报告简介
seo-title: 流程报告简介
description: JEE流程报告上AEM Forms的简介和主要功能
seo-description: JEE流程报告上AEM Forms的简介和主要功能
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 流程报告简介{#introduction-to-process-reporting}

![过程报告](assets/process-reporting.png)

流程报告是一个基于浏览器的工具，用于创建和视图AEM Forms流程和任务的报表。

流程报告提供一组现成报告，允许您过滤、视图有关长期运行流程、流程持续时间和工作流量的信息。

此外，“进程报告”还提供一个界面，用于运行临时查询并将自定义报告视图集成到“进程报告”用户界面中。

有关受支持浏览器的列表，请参阅 [AEM Forms支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)。

流程报告建立在以下模块上：

* 从AEM Forms数据库读取进程数据
* 将流程数据发布到嵌入式流程报告存储库
* 为视图报告提供基于浏览器的用户界面

## 关键功能 {#key-capabilities}

### 始终保持报告 {#always-on-reporting}

![站点管理](assets/site-management.png)

视图长时间运行的进程的列表、进程持续时间图表以及使用过滤器运行自定义查询。

流程报告还提供了以CSV格式导出报告和查询数据的选项。

### 临时报告 {#adhoc-reports}

![打印和颜色](assets/print-&-colour.png)

使用过滤器获取数据的特定视图。

您可以按ID、持续时间、开始和结束日期、进程启动器等搜索进程或任务。

您可以合并多个过滤器以创建特定报告。

然后，您可以保存要在以后的日期或时间运行的报表过滤器。

### 进程/任务历史 {#process-task-history}

![文件管理](assets/file-management.png)

AEM Forms服务器并行运行多个进程。 这些进程继续从一种状态过渡到另一种状态。 通过定期将Forms数据发布到“流程报告”存储库，“流程报告”会保留有关在AEM Forms中运行的流程的过渡信息。

### 访问控制 {#access-control-br}

![未标题](assets/untitled.png)

进程报告提供对用户界面的基于权限的访问。

这意味着只有具有报告权限的用户才有权访问进程报告用户界面。
