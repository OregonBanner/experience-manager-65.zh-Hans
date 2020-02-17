---
title: 流程报告中的预定义报告
seo-title: 流程报告中的预定义报告
description: 查询JEE上的AEM Forms流程数据，以创建有关长时间运行进程、进程持续时间和工作流卷的报告
seo-description: 查询JEE上的AEM Forms流程数据，以创建有关长时间运行进程、进程持续时间和工作流卷的报告
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 流程报告中的预定义报告 {#pre-defined-reports-in-process-reporting}

## 在制作中预定义的报告 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting随附以 *下现成报表* :

* **[长时间运行的进程](#long-running-processes)**:一个报告，其中列出了完成所有AEM表单进程所花费的时间超过指定时间
* **[流程持续时间图表](#process-duration-report)**:按持续时间列出的指定AEM Forms流程报告
* **[工作流量](#workflow-volume-report)**:按日期列出指定进程正在运行和已完成实例的报告

## 长时间运行的进程 {#long-running-processes}

“长时间运行的进程”报告显示已花费超过指定时间完成的AEM表单进程。

### 执行长进程报告 {#to-execute-a-long-running-process-report}

1. 要查看“流程报表”中预定义的报表列表，请在“流程报 **表** ”树视图中单击“**报表”**节点。
1. 单击“长 **运行进程** ”报告节点。

   ![long_running_node](assets/long_running_node.png)

   选择报告时，树视 **图右侧将显示** “报告参数”面板。

   ![长时间运行进程报告参数面板](assets/report_parameters_panel.png)

   参数:

   * **持续时间**(*必需*):指定持续时间和时间单位。 显示运行时间超过指定持续时间的所有AEM Forms进程。
   * **开始时间** (*可选*):选择日期。 过滤报告以显示在指定日期之后开始的进程实例。
   * **开始时间** (*可选*):选择日期。 过滤报告以显示在指定日期之前开始的进程实例。

1. 单击 **开始** ，以执行报告。

   报告显示在“进程报告”窗口右侧的**报告* **面板中** 。

   ![long_running_processes](assets/long_running_processes.png)

   使用**报告**面板右上角的选项对报告执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报告
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将报告中的数据导出并下载到逗号分隔的文件

## “进程持续时间”报告 {#process-duration-report}

“进程持续时间”报告按每个实例运行的天数显示表单进程的实例数。

### 执行“进程持续时间”报告 {#to-execute-a-process-duration-report}

1. 要在“流程报表”中查看预定义的报表，请在“流程报 **表** ”树视图中单击“**报表”**节点。
1. 单击“进 **程持续时间** ”报告节点。

   ![process_duration_node](assets/process_duration_node.png)

   选择报告时，树视 **图右侧将显示** “报告参数”面板。

   ![长时间运行进程报告参数面板](assets/process_duration_params.png)

   参数:

   * **选择进程**(必&#x200B;*需*):选择一个AEM Forms进程。

1. 单击**转到**以执行报告。

   报告显示在“进程报告”窗口右侧的**报告**面板中。

   ![process_duration_report](assets/process_duration_report.png)

   使用**报告**面板右上角的选项对报告执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报告
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将报告中的数据导出并下载到逗号分隔的文件

## 工作流量报告 {#workflow-volume-report}

“工作流量”报告按日历日显示AEM Forms进程当前正在运行和已完成的实例数。

### 执行工作流卷报告 {#to-execute-a-workflow-volume-report}

1. 要在“流程报表”中查看预定义的报表，请在“**流程报表”**树视图上单击“**报表”**节点。
1. 单击“工 **作流卷** ”报告节点。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   选择报告时，树视 **图右侧将显示** “报告参数”面板。

   ![长时间运行进程报告参数面板](assets/workflow_volume_params.png)

   参数:

   * **选择进程**(必&#x200B;*需*):选择一个AEM Forms进程。

   * **开始时间** (*可选*):选择日期。 过滤报告以显示在指定日期之后开始的进程实例。

   * **开始时间** (*可选*):选择日期。 过滤报告以显示在指定日期之前开始的进程实例。

1. 单击**转到**以执行报告。

   报告显示在“进程报告”窗口右侧的**报告* **面板中** 。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用**报告**面板右上角的选项对报告执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报告
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将报告中的数据导出并下载到逗号分隔的文件

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
