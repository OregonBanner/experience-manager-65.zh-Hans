---
title: 流程报表简介
seo-title: 流程报表简介
description: JEE Process Reporting上的AEM Forms的简介和主要功能
seo-description: JEE Process Reporting上的AEM Forms的简介和主要功能
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 流程报表简介{#introduction-to-process-reporting}

![进程报告](assets/process-reporting.png)

流程报告是一个基于浏览器的工具，用于创建和查看有关AEM Forms流程和任务的报告。

“流程报告”提供一组现成报告，允许您过滤、查看有关长期运行的进程、进程持续时间和工作流卷的信息。

此外，Process Reporting还提供一个界面，用于运行专门查询并将自定义报表视图集成到Process Reporting用户界面中。

有关支持的浏览器列表，请参阅 [AEM Forms支持的平台](/help/forms/using/aem-forms-jee-supported-platforms.md)。

流程报告基于以下模块构建：

* 从AEM Forms数据库读取进程数据
* 将流程数据发布到嵌入的Process Reporting存储库
* 提供基于浏览器的用户界面以查看报告

## 关键功能 {#key-capabilities}

### 始终在线报告 {#always-on-reporting}

![站点管理](assets/site-management.png)

查看长进程列表、进程持续时间图表以及使用过滤器运行自定义查询。

“流程报告”还提供以CSV格式导出报告和查询数据的选项。

### 临时报告 {#adhoc-reports}

![打印和颜色](assets/print-&-colour.png)

使用过滤器获取特定的数据视图。

您可以按ID、持续时间、开始和结束日期、进程启动器等搜索进程或任务。

您可以组合多个过滤器以创建特定报告。

然后，可保存报告过滤器，以在以后的日期或时间运行。

### 进程／任务历史记录 {#process-task-history}

![文件管理](assets/file-management.png)

AEM Forms服务器并行运行多个进程。 这些进程继续从一种状态过渡到另一种状态。 通过定期将Forms数据发布到Process Reporting存储库，Process Reporting会保留有关在AEM Forms中运行的进程的转换信息。

### 访问控制 {#access-control-br}

![未标题](assets/untitled.png)

进程报告提供对用户界面的基于权限的访问。

这意味着只有具有报告权限的用户才有权访问“进程报告”用户界面。

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
