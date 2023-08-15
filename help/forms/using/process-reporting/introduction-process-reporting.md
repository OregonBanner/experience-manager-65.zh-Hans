---
title: 进程报告简介
seo-title: Introduction to Process Reporting
description: AEM Forms on JEE Process Reporting的简介和主要功能
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 进程报告简介{#introduction-to-process-reporting}

![进程报告](assets/process-reporting.png)

进程报告是一种基于浏览器的工具，可用于创建和查看有关AEM Forms进程和任务的报告。

Process Reporting提供了一组现成的报告，可让您筛选、查看有关长时间运行的进程、进程持续时间以及工作流量的信息。

此外，“流程报表”提供了一个界面，用于运行临时查询并将自定义报表视图集成到“流程报表”用户界面中。

有关支持的浏览器的列表，请参阅 [AEM Forms支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md).

进程报告基于以下模块构建：

* 从AEM Forms数据库读取流程数据
* 将流程数据发布到嵌入式流程报表存储库
* 提供用于查看报告的基于浏览器的用户界面

## 主要功能 {#key-capabilities}

### 始终运行的报告 {#always-on-reporting}

![站点管理](assets/site-management.png)

查看长时间运行的进程的列表、进程持续时间图表，并使用过滤器运行自定义查询。

流程报表还提供了以CSV格式导出报表和查询数据的选项。

### 临时报表 {#adhoc-reports}

![打印与彩色](assets/print-&-colour.png)

使用筛选器获取数据的特定视图。

您可以按ID、持续时间、开始和结束日期、进程发起者等搜索进程或任务。

您可以组合多个过滤器以创建特定报告。

然后，您可以保存报表过滤器，以供在以后的日期或时间运行。

### 进程/任务历史记录 {#process-task-history}

![文件管理](assets/file-management.png)

AEM Forms服务器并行运行多个进程。 这些进程会不断从一个状态转换到另一个状态。 通过定期将Forms数据发布到Process Reporting存储库，Process Reporting保留有关在AEM Forms中运行的进程过渡信息。

### 访问控制 {#access-control-br}

![无标题](assets/untitled.png)

进程报告提供对用户界面的基于权限的访问。

这意味着只有具有报表权限的用户才能访问“流程报表”用户界面。
