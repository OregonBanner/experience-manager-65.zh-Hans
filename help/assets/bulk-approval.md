---
title: 审核文件夹资产和收藏集
description: 为文件夹或集合中的资产设置审阅工作流，并与审阅者或创意合作伙伴共享该审阅，以寻求反馈。
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# 审核文件夹资产和收藏集 {#review-folder-assets-and-collections}

为文件夹或集合中的资产设置审阅工作流，并与审阅者或创意合作伙伴共享该审阅，以寻求反馈。

通过Adobe Experience Manager(AEM)资产，您可以为文件夹或集合中的资产设置临时审阅工作流，并与审阅人或创意合作伙伴共享该工作流以寻求反馈。

您可以将审核工作流与项目关联或创建独立的审核任务。

共享资产后，审阅者可以批准或拒绝资产。 通知在工作流的各个阶段发送，以通知预期收件人完成各种任务。 例如，当您共享文件夹或集合时，审阅人会收到一条通知，指示已共享文件夹／集合以供审阅。

审阅人完成审阅（批准或拒绝资产）后，您会收到审阅完成通知。

## 为文件夹创建审阅任务 {#creating-a-review-task-for-folders}

1. 从资产用户界面中，选择要为其创建审核任务的文件夹。
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （可选）从“项 **[!UICONTROL 目]** ”列表中，选择要将审核任务关联到的项目。 默认情况下，选 **[!UICONTROL 择“无]** ”选项。 如果不希望将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有“编辑者”级别权限（或更高）的项目才会显示在“项目 **[!UICONTROL ”列表中]** 。

1. 输入审核任务的名称，然后从分配到列表中选择 **[!UICONTROL 审批人]** 。

   >[!NOTE]
   >
   >选定项目的成员／组在“分配到”列表中可作 **[!UICONTROL 为批准者]** 。

1. 输入任务说明、审核任务的优先级和到期日。

   ![任务_详细信息](assets/task_details.png)

1. 在高级选项卡中，输入用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. 新任务的通知将发送给审批者。
1. 以批准者身份登录到AEM资产，然后导航到资产UI。 要批准资产，请单击 **[!UICONTROL 通知]** ，然后从列表中选择审核任务。

   ![资产通知](assets/aemAssetsNotification.png)

1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. In the **[!UICONTROL Review Task]** page, select assets, and click **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_任务](assets/review_task.png)

1. Click **[!UICONTROL Complete]** from the toolbar. 在对话框中，输入评论，然后单击“ **[!UICONTROL 完成]** ”进行确认。
1. 导航到资产用户界面并打开文件夹。 资产的批准状态图标显示在卡视图和列表视图中。

   **卡片视图**

   ![查看卡视图中的状态](assets/chlimage_1-404.png)

   **列表视图**

   ![查看状态(如列表视图中所示)](assets/review_status_listview.png)

## 为集合创建审阅任务 {#creating-a-review-task-for-collections}

1. 从“收藏集”页面中，选择要为其创建审阅任务的收藏集。
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （可选）从“项 **[!UICONTROL 目]** ”列表中，选择要将审核任务关联到的项目。 默认情况下，选 **[!UICONTROL 择“无]** ”选项。 如果不希望将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有“编辑者”级别权限（或更高）的项目才会显示在“项目 **[!UICONTROL ”列表中]** 。

1. 输入审核任务的名称，然后从分配到列表中选择 **[!UICONTROL 审批人]** 。

   >[!NOTE]
   >
   >选定项目的成员／组在“分配到”列表中可作 **[!UICONTROL 为批准者]** 。

1. 输入任务说明、审核任务的优先级和到期日。

   ![任务_details-collection](assets/task_details-collection.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. 新任务的通知将发送给审批者。
1. 以批准者身份登录到AEM资产，然后导航到资产控制台。 要批准资产，请单击 **[!UICONTROL 通知]** ，然后从列表中选择审核任务。
1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. 集合中的所有资产都显示在审核页面上。 Select the assets and click **[!UICONTROL Approve/Reject]** to approve or reject assets, as appropriate.

   ![review_任务_collection](assets/review_task_collection.png)

1. Click **[!UICONTROL Complete]** from the toolbar. 在对话框中，输入评论，然后单击“ **[!UICONTROL 完成]** ”进行确认。
1. 导航到收藏集控制台，然后打开收藏集。 资产的批准状态图标显示在卡片和列表视图中。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *图：卡视图*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *图：列表视图*
