---
title: 进程报告中的预定义报告
description: 查询AEM Forms on JEE流程数据以创建长时间运行的流程、流程持续时间和工作流量的报告
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 进程报告中的预定义报告 {#pre-defined-reports-in-process-reporting}

## 正在报告的预定义报告 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting附带以下功能 *开箱即用* 报告：

* **[长时间运行的进程](#long-running-processes)**：包含所有完成时间超过指定时间的AEM Forms进程的报告
* **[进程持续时间图表](#process-duration-report)**：按持续时间列出的指定AEM Forms进程报表
* **[工作流量](#workflow-volume-report)**：按日期显示指定进程的正在运行和已完成的实例的报告

## 长时间运行的进程 {#long-running-processes}

“长时间运行的进程”报表显示已花费超过指定时间完成的AEM Forms进程。

### 执行长时间运行的进程报告 {#to-execute-a-long-running-process-report}

1. 要查看流程报告中的预定义报告列表，请在 **进程报告** 树视图，单击 **报表** 节点。
1. 单击 **长时间运行的进程** 报表节点。

   ![long_run_node](assets/long_running_node.png)

   当您选择报告时， **报表参数** 面板将显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/report_parameters_panel.png)

   参数：

   * **持续时间** (*必需*)：指定持续时间和时间单位。 显示已运行超过指定持续时间的所有AEM Forms进程。
   * **开始晚于** (*可选*)：选择日期。 筛选报告以显示在指定日期之后开始的进程实例。
   * **开始于以下日期之前** (*可选*)：选择日期。 筛选报告以显示在指定日期之前开始的进程实例。

1. 单击 **开始** 以执行报告。

   报告显示在 **报表** 右侧面板 **进程报告** 窗口。

   ![long_running_processes](assets/long_running_processes.png)

   使用右上角的选项 **报表** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：导出数据并将该数据从报表下载到以逗号分隔的文件中

## 进程持续时间报表  {#process-duration-report}

进程持续时间报表按每个实例已运行的天数显示Forms进程的实例数。

### 执行进程持续时间报告 {#to-execute-a-process-duration-report}

1. 要查看流程报告中的预定义报表，请在 **进程报告** 树视图，单击 **报表** 节点。
1. 单击 **进程持续时间** 报表节点。

   ![process_duration_node](assets/process_duration_node.png)

   当您选择报告时， **报表参数** 面板将显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/process_duration_params.png)

   参数：

   * **选择进程** (*必需*)：选择AEM Forms进程。

1. 单击 **开始** 以执行报告。

   报告显示在 **报表** 面板中，该面板位于“流程报告”窗口的右侧。

   ![process_duration_report](assets/process_duration_report.png)

   使用右上角的选项 **报表** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：导出数据并将该数据从报表下载到以逗号分隔的文件中

## “Workflow Volume”报告 {#workflow-volume-report}

“工作流量”报表按日历日显示当前运行和已完成的AEM Forms进程实例数。

### 执行工作流卷报告 {#to-execute-a-workflow-volume-report}

1. 要查看流程报告中的预定义报表，请在 **进程报告** 树视图，单击 **报表** 节点。
1. 单击 **工作流量** 报表节点。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   当您选择报告时， **报表参数** 面板将显示在树视图的右侧。

   ![长时间运行的进程报告参数面板](assets/workflow_volume_params.png)

   参数：

   * **选择进程** (*必需*)：选择AEM Forms进程。

   * **开始晚于** (*可选*)：选择日期。 筛选报告以显示在指定日期之后开始的进程实例。

   * **开始于以下日期之前** (*可选*)：选择日期。 筛选报告以显示在指定日期之前开始的进程实例。

1. 单击 **开始** 以执行报告。

   报告显示在 **报表** 右侧面板 **进程报告** 窗口。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用右上角的选项 **报表** 面板来对报告执行以下操作。

   * **刷新**：使用存储中的最新数据刷新报表
   * **更改图例颜色**：选择并更改报表图例的颜色
   * **导出到CSV**：导出数据并将该数据从报表下载到以逗号分隔的文件中
