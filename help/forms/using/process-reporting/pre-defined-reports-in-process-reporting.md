---
title: 进程报表中的预定义报表
seo-title: Pre-defined reports in Process Reporting
description: 查询AEM Forms on JEE流程数据，以创建有关长时间运行的流程、流程持续时间和工作流量的报告
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 进程报表中的预定义报表 {#pre-defined-reports-in-process-reporting}

## 预定义的报告正在处理报告 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting附带以下功能 *开箱即用* 报告：

* **[长时间运行的进程](#long-running-processes)**：有关完成所用时间超过指定时间的所有AEM Forms进程的报告
* **[进程持续时间图表](#process-duration-report)**：按持续时间列出的指定AEM Forms进程报表
* **[工作流数量](#workflow-volume-report)**：按日期显示指定进程的正在运行和已完成的实例的报告

## 长时间运行的进程 {#long-running-processes}

“长时间运行的进程”报告显示已花费超过指定时间完成的AEM Forms进程。

### 执行长时间运行的进程报告 {#to-execute-a-long-running-process-report}

1. 要在“流程报告”中查看预定义报表的列表，请在 **进程报告** 树视图，单击 **报告** 节点。
1. 单击 **长时间运行的进程** 报告节点。

   ![long_running_node](assets/long_running_node.png)

   当您选择报告时， **报表参数** 面板显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/report_parameters_panel.png)

   参数:

   * **持续时间** (*必需*)：指定持续时间和时间单位。 显示运行时间超过指定持续时间的所有AEM Forms进程。
   * **开始晚于** (*可选*)：选择日期。 筛选报告以显示在指定日期之后开始的进程实例。
   * **开始于以下日期之前** (*可选*)：选择日期。 筛选报告以显示在指定日期之前开始的进程实例。

1. 单击 **开始** 以执行报告。

   报告显示在 **报告** 右侧面板 **进程报告** 窗口。

   ![long_running_processes](assets/long_running_processes.png)

   使用右上角的选项 **报告** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：将数据从报表导出并下载到以逗号分隔的文件

## 进程持续时间报告  {#process-duration-report}

“进程持续时间”报告按每个实例已运行的天数显示Forms进程的实例数。

### 执行进程持续时间报告 {#to-execute-a-process-duration-report}

1. 要查看流程报告中的预定义报告，请在 **进程报告** 树视图，单击 **报告** 节点。
1. 单击 **进程持续时间** 报告节点。

   ![process_duration_node](assets/process_duration_node.png)

   当您选择报告时， **报表参数** 面板显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/process_duration_params.png)

   参数:

   * **选择进程** (*必需*)：选择AEM Forms进程。

1. 单击 **开始** 以执行报告。

   报告显示在 **报告** “进程报告”窗口右侧的面板。

   ![process_duration_report](assets/process_duration_report.png)

   使用右上角的选项 **报告** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：将数据从报表导出并下载到以逗号分隔的文件

## “工作流量”报告 {#workflow-volume-report}

“工作流量”报告按日历日显示当前正在运行和已完成的AEM Forms进程实例数。

### 执行工作流卷报告 {#to-execute-a-workflow-volume-report}

1. 要查看流程报告中的预定义报告，请在 **进程报告** 树视图，单击 **报告** 节点。
1. 单击 **工作流数量** 报告节点。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   当您选择报告时， **报表参数** 面板显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/workflow_volume_params.png)

   参数:

   * **选择进程** (*必需*)：选择AEM Forms进程。

   * **开始晚于** (*可选*)：选择日期。 筛选报告以显示在指定日期之后开始的进程实例。

   * **开始于以下日期之前** (*可选*)：选择日期。 筛选报告以显示在指定日期之前开始的进程实例。

1. 单击 **开始** 以执行报告。

   报告显示在 **报告** 右侧面板 **进程报告** 窗口。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用右上角的选项 **报告** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：将数据从报表导出并下载到以逗号分隔的文件
