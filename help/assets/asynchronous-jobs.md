---
title: 异步操作
description: Experience Manager资产通过异步完成一些资源密集型任务来优化性能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 2%

---


# 异步操作 {#asynchronous-operations}

为了减少对性能的不利影响，Adobe Experience Manager资产异步处理某些长时间运行且资源密集型资产操作。

这些操作包括：

* 删除许多资产
* 移动包含许多引用的许多资产或资产
* 批量导出／导入资产元数据。
* 从远程Experience Manager部署获取超过阈值限制设置的资产。

异步处理涉及入队多个作业，并最终根据系统资源的可用性以串行方式运行它们。

您可以从“异步作业状态”页视图异 **[!UICONTROL 步作业的状态]** 。

>[!NOTE]
>
>默认情况下，资产中的作业并行运行。 如果N是CPU核心的数量，则默认情况下，N/2作业可以并行运行。 要对作业队列使用自定义设置，请从Web控 **[!UICONTROL 制台修改“异步操作默认队列]** ”配置。 有关详细信息，请参阅 [队列配置](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 监视异步操作的状态 {#monitoring-the-status-of-asynchronous-operations}

每当资产异步处理操作时，您都会在您的收件箱和电子邮件中收到通知。

要详细视图异步操作的状态，请导航到“异步作 **[!UICONTROL 业状态”页]** 。

1. 在Experience Manager界面中，单击“操 **[!UICONTROL 作]** ”> **[!UICONTROL “作业]**”。

1. 在“异 **[!UICONTROL 步作业状态]** ”页中，查看操作的详细信息。

   ![异步操作的状态和详细信息](assets/AsyncOperation-status.png)

   要确定特定操作的进度，请参阅“状态”列 **[!UICONTROL 中的]** 值。 根据进度，将显示以下状态之一：

   * **[!UICONTROL 活动]**: 正在处理操作

   * **[!UICONTROL 成功]**: 操作已完成

   * **[!UICONTROL 失败]**&#x200B;或&#x200B;**[!UICONTROL 错误]**：无法处理该操作

   * **[!UICONTROL 计划]**: 该操作计划稍后处理

1. 要停止活动操作，请从列表中选择它，然后单 **[!UICONTROL 击工]** 具栏中的停止。

   ![stop_icon](assets/stop_icon.png)

1. 要视图其他详细信息（例如说明和日志），请选择操作，然后单 **[!UICONTROL 击工]** 具栏中的打开。

   ![open_icon](assets/open_icon.png)

   此时会显示作业详细信息页面。

   ![job_details](assets/job_details.png)

1. 要从列表中删除该操作，请从工 **[!UICONTROL 具栏]** 中选择删除。 要以CSV文件下载详细信息，请单击“下 **[!UICONTROL 载”]**。

   >[!NOTE]
   >
   >如果作业的状态为活动或排队，则无法删除该作业。

## 清除已完成的作业 {#purging-completed-jobs}

Experience Manager资产每天凌晨1:00运行清除作业，以删除已完成且已使用一天以上的异步作业。

您可以修改清除作业的计划以及删除之前保留已完成作业详细信息的持续时间。 您还可以配置在任何时间点保留详细信息的已完成作业的最大数量。

1. 在Experience Manager界面中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 打开Adobe **[!UICONTROL CQ DAM异步作业清除计划作业]** 。
1. 指定删除已完成作业的天数阈值以及保留历史记录详细信息的作业的最大天数。

   ![配置以计划异步作业的清除](assets/configmgr_purge_asyncjobs.png)

1. 保存更改。

## 为异步处理配置阈值 {#configuring-thresholds-for-asynchronous-processing}

您可以配置资产的阈值数量或引用，以异步处理特定操作。

### 为异步删除操作配置阈值 {#configuring-thresholds-for-asynchronous-delete-operations}

如果要删除的资产或文件夹数超过阈值数，将异步执行删除操作。

1. 在Experience Manager界面中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 从Web控制台中，打开“异步 **[!UICONTROL 删除操作作业处理配置]** ”。
1. 在“资 **[!UICONTROL 产的阈值数]** ”框中，指定用于异步处理删除操作的资产／文件夹的阈值数。

   ![delete_threshold](assets/delete_threshold.png)

1. 保存更改。

### 为异步移动操作配置阈值 {#configuring-thresholds-for-asynchronous-move-operations}

如果要移动的资产／文件夹或引用的数量超过阈值数，则异步执行移动操作。

1. 在Experience Manager界面中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 从Web控制台中，打开异 **[!UICONTROL 步移动操作作业处理配置]** 。
1. 在“资 **[!UICONTROL 产／引用的阈值数]** ”框中，指定用于异步处理移动操作的资产／文件夹或引用的阈值数。

   ![move_threshold](assets/move_threshold.png)

1. 保存更改。
