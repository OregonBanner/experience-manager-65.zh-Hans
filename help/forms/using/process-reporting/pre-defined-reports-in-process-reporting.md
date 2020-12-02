---
title: 流程中的预定义报告报告
seo-title: 流程中的预定义报告报告
description: 查询AEM Forms的JEE流程数据，以创建有关长期运行流程、流程持续时间和工作流量的报告
seo-description: 查询AEM Forms的JEE流程数据，以创建有关长期运行流程、流程持续时间和工作流量的报告
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# 流程报告{#pre-defined-reports-in-process-reporting}中的预定义报告

## 流程中预定义的报告报告{#pre-defined-reports-in-process-reporting-1}

AEM Forms流程报告随附以下&#x200B;*现成报告*:

* **[长时间运行的进程](#long-running-processes)**:AEM Forms所有用超过指定时间完成的进程的报告
* **[流程持续时间图表](#process-duration-report)**:按期分列的AEM Forms具体进程的报告
* **[工作流卷](#workflow-volume-report)**:按日期列出指定进程正在运行和已完成实例的报告

## 长运行进程{#long-running-processes}

“ Long Running Processes”报告显示完成AEM Forms进程所花费的时间超过指定时间。

### 执行长进程运行报告{#to-execute-a-long-running-process-report}

1. 要在“流程报告”中视图预定义报表的列表，请在&#x200B;**“流程报告”**&#x200B;树视图中，单击&#x200B;**“报表”**&#x200B;节点。
1. 单击&#x200B;**长运行进程**&#x200B;报告节点。

   ![long_running_node](assets/long_running_node.png)

   选择报告时，**报告参数**&#x200B;面板显示在树视图的右侧。

   ![长运行进程报告参数面板](assets/report_parameters_panel.png)

   参数:

   * **持续时间** (*必填*):指定持续时间和时间单位。显示运行时间超过指定持续时间的所有AEM Forms进程。
   * **开始时间** (*可选*):选择日期。过滤报告以显示在指定日期之后开始的流程实例。
   * **开始时间** (*可选*):选择日期。过滤报告以显示在指定日期之前开始的流程实例。

1. 单击&#x200B;**转至**&#x200B;以执行报告。

   报告显示在&#x200B;**处理报告**&#x200B;窗口右侧的&#x200B;**报告**&#x200B;面板中。

   ![long_running_processes](assets/long_running_processes.png)

   使用&#x200B;**Report**&#x200B;面板右上角的选项对报表执行以下操作。

   * **刷新**:刷新报表时，存储中会显示最新数据
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报告导出并下载到以逗号分隔的文件

## 进程持续时间报告{#process-duration-report}

“进程持续时间”报告按每个实例运行的天数显示Forms进程的实例数。

### 执行进程持续时间报告{#to-execute-a-process-duration-report}

1. 要在“流程报告”中视图预定义的报表，请在&#x200B;**“流程报告”**&#x200B;树视图中，单击“**报表”**&#x200B;节点。
1. 单击&#x200B;**进程持续时间**&#x200B;报告节点。

   ![process_duration_node](assets/process_duration_node.png)

   选择报告时，**报告参数**&#x200B;面板显示在树视图的右侧。

   ![长运行进程报告参数面板](assets/process_duration_params.png)

   参数:

   * **选择进程** (*必填*):选择一个AEM Forms进程。

1. 单击&#x200B;**转至**&#x200B;以执行报告。

   此报告显示在“进程报告”窗口右侧的&#x200B;**Report**&#x200B;面板中。

   ![process_duration_report](assets/process_duration_report.png)

   使用&#x200B;**Report**&#x200B;面板右上角的选项对报表执行以下操作。

   * **刷新**:刷新报表时，存储中会显示最新数据
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报告导出并下载到以逗号分隔的文件

## 工作流卷报告{#workflow-volume-report}

“工作流量”报告按日历日显示AEM Forms进程当前正在运行和已完成的实例数。

### 执行工作流卷报告{#to-execute-a-workflow-volume-report}

1. 要在“流程报告”中视图预定义的报表，请在&#x200B;**“流程报告”**&#x200B;树视图中，单击“**报表”**&#x200B;节点。
1. 单击&#x200B;**工作流卷**&#x200B;报告节点。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   选择报告时，**报告参数**&#x200B;面板显示在树视图的右侧。

   ![长运行进程报告参数面板](assets/workflow_volume_params.png)

   参数:

   * **选择进程** (*必填*):选择一个AEM Forms进程。

   * **开始时间** (*可选*):选择日期。过滤器报表以显示在指定日期之后开始的流程实例。

   * **开始时间** (*可选*):选择日期。过滤器报表以显示在指定日期之前开始的流程实例。

1. 单击&#x200B;**转至**&#x200B;以执行报告。

   报告显示在&#x200B;**处理报告**&#x200B;窗口右侧的&#x200B;**报告**&#x200B;面板中。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用&#x200B;**Report**&#x200B;面板右上角的选项对报表执行以下操作。

   * **刷新**:刷新报表时，存储中会显示最新数据
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报告导出并下载到以逗号分隔的文件
