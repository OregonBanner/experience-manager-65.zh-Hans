---
title: 异步操作
description: AEM资产通过异步完成某些资源密集型任务来优化性能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 异步操作 {#asynchronous-operations}

为了减少对性能的不利影响，Adobe Experience Manger(AEM)资产异步处理某些长时间运行且资源密集型资产操作。

这些操作包括：

* 删除许多资产
* 移动包含许多引用的许多资产或资产
* 批量导出／导入资产元数据。
* 从远程AEM部署获取超过阈值限制设置的资产。

异步处理涉及将多个作业入队，并最终在系统资源可用性的前提下以串行方式运行它们。

您可以从“异步作业状态”页视图异步 **[!UICONTROL 作业的状态]** 。

>[!NOTE]
>
>默认情况下，AEM资产中的作业并行运行。 如果N是CPU核心的数量，则默认情况下，N/2个作业可以并行运行。 要使用作业队列的自定义设置，请从Web控制台 **[!UICONTROL 修改异步操作默认队列配置]** 。 有关详细信息，请参阅 [队列配置](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 监视异步操作的状态 {#monitoring-the-status-of-asynchronous-operations}

每当AEM资产异步处理操作时，您都会在您的收件箱中和通过电子邮件收到通知。

要详细视图异步操作的状态，请导航到“异步作业状 **[!UICONTROL 态”页]** 。

1. 在Experience Manager界面中，单击“操 **[!UICONTROL 作]** ”>“ **[!UICONTROL 作业”]**。

1. 在“异 **[!UICONTROL 步作业状态]** ”页中，查看操作的详细信息。

   ![异步操作的状态和详细信息](assets/AsyncOperation-status.png)

   要确定特定操作的进度，请参阅“状态”列中 **[!UICONTROL 的值]** 。 根据进度，将显示以下状态之一：

   * **[!UICONTROL 活动]**:正在处理操作

   * **[!UICONTROL 成功]**:操作完成

   * **[!UICONTROL 失败]**&#x200B;或&#x200B;**[!UICONTROL 错误]**：无法处理该操作

   * **[!UICONTROL 计划]**:此操作计划稍后处理

1. 要停止活动操作，请从列表中选择它，然后单击工 **[!UICONTROL 具栏中]** 的停止。

   ![stop_icon](assets/stop_icon.png)

1. 要视图其他详细信息（例如说明和日志），请选择操作，然后单击工 **[!UICONTROL 具栏中]** 的打开。

   ![open_icon](assets/open_icon.png)

   此时将显示作业详细信息页面。

   ![job_details](assets/job_details.png)

1. 要从列表中删除操作，请从工具栏中 **[!UICONTROL 选择]** “删除”。 要下载CSV文件中的详细信息，请单击“下 **[!UICONTROL 载”]**。

   >[!NOTE]
   >
   >如果作业的状态为活动或已排队，则不能删除作业。

## 清除已完成的作业 {#purging-completed-jobs}

AEM资产每天凌晨1:00运行清除作业，以删除已完成且已超过一天的异步作业。

您可以修改清除作业的计划以及在删除之前保留已完成作业详细信息的持续时间。 您还可以配置在任何时间点保留详细信息的已完成作业的最大数量。

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]**。
1. 打开 **[!UICONTROL Adobe CQ DAM异步作业清除计划作业]** 。
1. 指定删除已完成作业的天数阈值，以及保留历史记录中详细信息的作业的最大天数。

   ![配置以计划异步作业的清除](assets/configmgr_purge_asyncjobs.png)

1. 保存更改。

## 为异步处理配置阈值 {#configuring-thresholds-for-asynchronous-processing}

您可以配置AEM资产的阈值资产数或引用，以异步处理特定操作。

### 为异步删除操作配置阈值 {#configuring-thresholds-for-asynchronous-delete-operations}

如果要删除的资产或文件夹数量超过阈值数，则异步执行删除操作。

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]**。
1. 从Web控制台中，打开异步删 **[!UICONTROL 除操作作业处理配置]** 。
1. 在“资 **[!UICONTROL 产阈值数”框中]** ，指定用于异步处理删除操作的资产／文件夹的阈值数。

   ![delete_threshold](assets/delete_threshold.png)

1. 保存更改。

### 为异步移动操作配置阈值 {#configuring-thresholds-for-asynchronous-move-operations}

如果要移动的资产／文件夹或引用数超过阈值数，则异步执行移动操作。

1. 在Experience Manager界面中，单击工 **[!UICONTROL 具]** >操 **[!UICONTROL 作]** > **[!UICONTROL Web控制台]**。
1. 从Web控制台中，打开异步移 **[!UICONTROL 动操作作业处理配置]** 。
1. 在“资 **[!UICONTROL 产／引用的阈值数”框中]** ，指定用于异步处理移动操作的资产／文件夹或引用的阈值数。

   ![move_threshold](assets/move_threshold.png)

1. 保存更改。
