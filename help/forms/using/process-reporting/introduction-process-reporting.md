---
title: 流程报告简介
seo-title: 流程报告简介
description: AEM Forms在JEE流程报告中的简介和关键功能
seo-description: AEM Forms在JEE流程报告中的简介和关键功能
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 流程报告简介{#introduction-to-process-reporting}

![进程报告](assets/process-reporting.png)

“流程报表”是一个基于浏览器的工具，可用于创建和查看有关AEM Forms流程和任务的报表。

“流程报表”提供一组现成的报表，用于筛选、查看有关长时间运行的流程、流程持续时间和工作流量的信息。

此外，“流程报表”还提供了一个界面来运行临时查询，并将自定义报表视图集成到“流程报表”用户界面中。

有关支持的浏览器列表，请参阅[AEM Forms支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)。

流程报告基于以下模块：

* 从AEM Forms数据库读取进程数据
* 将流程数据发布到嵌入的流程报表存储库
* 提供基于浏览器的用户界面以查看报表

## 关键功能{#key-capabilities}

### 始终运行报表{#always-on-reporting}

![站点管理](assets/site-management.png)

查看长时间运行的进程列表、进程持续时间图，并使用过滤器运行自定义查询。

“流程报表”还提供了以CSV格式导出报表和查询数据的选项。

### 临时报表{#adhoc-reports}

![打印和颜色](assets/print-&-colour.png)

使用过滤器获取数据的特定视图。

您可以按ID、持续时间、开始和结束日期、进程启动器等搜索进程或任务。

您可以合并多个过滤器以创建特定报表。

然后，您可以保存报表过滤器，以便在以后的日期或时间运行。

### 进程/任务历史记录{#process-task-history}

![文件管理](assets/file-management.png)

AEM Forms服务器并行运行多个进程。 这些过程会持续从一种状态转换到另一种状态。 通过定期将Forms数据发布到Process Reporting存储库，Process Reporting可保留有关在AEM Forms中运行的流程的转换信息。

### 访问控制 {#access-control-br}

![未命名](assets/untitled.png)

流程报表提供对用户界面的基于权限的访问。

这意味着只有具有报表权限的用户才有权访问Process Reporting用户界面。
