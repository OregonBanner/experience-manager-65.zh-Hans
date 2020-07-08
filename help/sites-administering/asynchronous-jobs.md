---
title: 异步作业
description: Adobe Experience Manager通过异步完成某些资源密集型任务来优化性能。
translation-type: tm+mt
source-git-commit: 198593fa456780816216a63790fea8cca469f8c7
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 3%

---


# 异步操作 {#asynchronous-operations}

为了减少对性能的负面影响，Adobe Experience Manager异步处理某些长时间运行且资源密集型操作。 异步处理包括入队多个作业并以串行方式运行它们，但需考虑系统资源的可用性。

这些操作包括：

* 删除许多资产
* 移动包含许多引用的许多资产或资产
* 批量导出／导入资产元数据
* 从远程Experience Manager部署获取超过阈值限制设置的资产
* 移动页面
* 转出Live Copy

您可以从Async Job Status **** 仪表板的Global Navigation **->** Tools **-> Operations** ********&#x200B;中视图异步作业的状态。

>[!NOTE]
>
>默认情况下，异步作业并行运行。 如 *`n`* 果是CPU核心的数量，则 *`n/2`* 默认情况下，作业可以并行运行。 要对作业队列使用自定义设置，请从 **[!UICONTROL Web控制台修改Async Operation]** Default Queue **Config和Async Operation Page Move and Rollout Config** 。
>
>有关详细信息，请参阅 [队列配置](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 监视异步操作的状态 {#monitor-the-status-of-asynchronous-operations}

每当AEM异步处理操作时，您都会在收件箱中和通过电子邮件 [(如](/help/sites-authoring/inbox.md) 果已启用)收到通知。

要详细视图异步操作的状态，请导航到“异步作 **[!UICONTROL 业状态”页]** 。

1. 在Experience Manager界面中，单击 **[!UICONTROL 操作]** > **[!UICONTROL 作业]**。

1. 在“异 **[!UICONTROL 步作业状态]** ”页中，查看操作的详细信息。

   ![异步操作的状态和详细信息](assets/async-operation-status.png)

   要确定特定操作的进度，请参阅“状态”列 **[!UICONTROL 中的]** 值。 根据进度，将显示以下状态之一：

   * **[!UICONTROL 活动]**: 正在处理操作

   * **[!UICONTROL 成功]**: 操作已完成

   * **[!UICONTROL 失败]**&#x200B;或&#x200B;**[!UICONTROL 错误]**：无法处理该操作

   * **[!UICONTROL 计划]**: 该操作计划稍后处理

1. 要停止活动操作，请从列表中选择它，然后单 **[!UICONTROL 击工]** 具栏中的停止。

   ![stop_icon](assets/async-stop-icon.png)

1. 要视图其他详细信息（例如说明和日志），请选择操作，然后单 **[!UICONTROL 击工]** 具栏中的打开。

   ![open_icon](assets/async-open-icon.png)

   此时会显示作业详细信息页面。

   ![job_details](assets/async-job-details.png)

1. 要从列表中删除该操作，请从工 **[!UICONTROL 具栏]** 中选择删除。 要以CSV文件下载详细信息，请单击“下 **[!UICONTROL 载”]**。

   >[!NOTE]
   >
   >如果作业的状态为“活动”或“已排队”，则 **不能** 删除 **该作业**。

## 清除已完成的作业 {#purging-completed-jobs}

AEM每天01:00运行清除作业，以删除已完成的已超过一天的异步作业。

您可以修改清除作业的计划以及删除之前保留已完成作业详细信息的持续时间。 您还可以配置在任何时间点保留详细信息的已完成作业的最大数量。

1. 在全局导航中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 打开Adobe **[!UICONTROL Granite异步作业清除计划作业]** 。
1. 指定：
   * 删除完成作业后的阈值天数。
   * 历史记录中保留详细信息的最大作业数。
   * 应运行清除时的cron表达式。

   ![配置以计划异步作业的清除](assets/async-purge-job.png)

1. 保存更改。

## 配置异步处理 {#configuring-asynchronous-processing}

您可以为AEM配置资产、页面或引用的阈值数，以异步处理特定操作，以及切换处理作业时的电子邮件通知。

### 配置异步资产删除操作 {#configuring-synchronous-delete-operations}

如果要删除的资产或文件夹数超过阈值数，将异步执行删除操作。

1. 在全局导航中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 从Web控制台中，打开异步进 **[!UICONTROL 程默认队列配置。]**
1. 在“资 **[!UICONTROL 产的阈值数]** ”框中，指定用于异步处理删除操作的资产／文件夹的阈值数。

   ![资产删除阈值](assets/async-delete-threshold.png)

1. 选中“启用电 **子邮件通知** ，以接收此作业状态的电子邮件通知”选项。 例如，成功，失败。
1. 保存更改。

### 配置异步资产移动操作 {#configuring-asynchronous-move-operations}

如果要移动的资产／文件夹或引用数超过阈值数，则异步执行移动操作。

1. 在全局导航中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 从Web控制台中，打开异 **[!UICONTROL 步移动操作作业处理配置。]**
1. 在“资 **[!UICONTROL 产／引用的阈值数]** ”框中，指定用于异步处理移动操作的资产／文件夹或引用的阈值数。

   ![资产移动阈值](assets/async-move-threshold.png)

1. 选中“启用电 **子邮件通知** ，以接收此作业状态的电子邮件通知”选项。 例如，成功，失败。
1. 保存更改。

### 配置异步页面移动操作 {#configuring-asynchronous-page-move-operations}

如果对要移动的页面的引用数超过阈值数，则异步执行移动操作。

1. 在全局导航中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 从Web控制台中，打开异 **[!UICONTROL 步页面移动操作作业处理配置。]**
1. 在“引 **[!UICONTROL 用的阈值数]** ”字段中，指定用于异步处理页面移动操作的引用的阈值数。

   ![页面移动阈值](assets/async-page-move.png)

1. 选中“启用电 **子邮件通知** ，以接收此作业状态的电子邮件通知”选项。 例如，成功，失败。
1. 保存更改。

### 配置异步MSM操作 {#configuring-asynchronous-msm-operations}

1. 在全局导航中，单 **[!UICONTROL 击工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控]**&#x200B;制台。
1. 从Web控制台中，打开异 **[!UICONTROL 步页面移动操作作业处理配置。]**
1. 选中“启用电 **子邮件通知** ，以接收此作业状态的电子邮件通知”选项。 例如，成功，失败。

   ![MSM配置](assets/async-msm.png)

1. 保存更改。

>[!MORELIKETHIS]
>
>* [创建和组织页面](/help/sites-authoring/managing-pages.md)
>* [创建和同步Live Copy](/help/sites-administering/msm-livecopy.md)
>* [在Experience Manager中配置电子邮件](/help/sites-administering/notification.md)。
>* [批量导入和导出资产元数据](/help/assets/metadata-import-export.md)。
>* [使用连接资产共享远程部署中的DAM资产](/help/assets/use-assets-across-connected-assets-instances.md)。

