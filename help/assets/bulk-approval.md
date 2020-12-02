---
title: 审核文件夹资产和收藏集
description: 为文件夹或集合中的资产设置审阅工作流，并与审阅者或创意合作伙伴共享它以寻求反馈。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 4%

---


# 审核文件夹资产和收藏集 {#review-folder-assets-and-collections}

为文件夹或集合中的资产设置审阅工作流，并与审阅者或创意合作伙伴共享它以寻求反馈。

[!DNL Adobe Experience Manager Assets] 允许您为文件夹或集合中的资产设置临时审阅工作流，并与审阅者或创意合作伙伴共享该工作流以寻求反馈。

您可以将审核工作流与项目关联，也可以创建独立的审核任务。

共享资产后，审阅者可以批准或拒绝资产。 通知在工作流的各个阶段发送，以通知预期收件人完成各种任务。 例如，当您共享文件夹或集合时，审阅者会收到一个通知，告知已共享文件夹／集合以供审阅。

审阅人完成审阅（批准或拒绝资产）后，您会收到审阅完成通知。

## 为文件夹{#creating-a-review-task-for-folders}创建审阅任务

1. 从[!DNL Assets]用户界面中，选择要为其创建审阅任务的文件夹。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 创建审阅任务]** ![创建审阅任务](assets/do-not-localize/create-review-task.png)以打开&#x200B;**[!UICONTROL 审阅任务]**&#x200B;页。 如果在工具栏中看不到该选项，请单击&#x200B;**[!UICONTROL 更多]**，然后选择该选项。

1. （可选）从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择要将审核任务关联到的项目。 默认情况下，选中&#x200B;**[!UICONTROL 无]**&#x200B;选项。 如果您不想将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑者级别权限（或更高）的项目才会显示在&#x200B;**[!UICONTROL 项目]**&#x200B;列表中。

1. 输入审核任务的名称，然后从&#x200B;**[!UICONTROL 分配给]**&#x200B;列表中选择审批者。

   >[!NOTE]
   >
   >在&#x200B;**[!UICONTROL “分配给]**”列表中，选定项目的成员／组可作为批准者。

1. 输入复查任务的说明、任务优先级和到期日。

   ![任务_详细信息](assets/task_details.png)

1. 在高级选项卡中，输入用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. 单击&#x200B;**[!UICONTROL 提交]**，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;以关闭确认消息。 新任务的通知将发送给审批者。
1. 以批准者身份登录到[!DNL Assets]，然后导航到[!DNL Assets] UI。 要批准资产，请单击&#x200B;**[!UICONTROL 通知]**，然后从列表中选择审核任务。

   ![资产通知](assets/aemAssetsNotification.png)

1. 在&#x200B;**[!UICONTROL 审阅任务]**&#x200B;页面中，检查审阅任务的详细信息，然后单击&#x200B;**[!UICONTROL 审阅]**。
1. 在&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面中，选择资产，然后根据需要单击&#x200B;**[!UICONTROL 批准／拒绝]**&#x200B;以批准或拒绝。

   ![review_任务](assets/review_task.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 完成]**。 在对话框中，输入注释，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;进行确认。
1. 导航到[!DNL Assets]用户界面并打开文件夹。 资产的批准状态图标以卡视图和列表视图显示。

   **卡片视图**

   ![查看卡视图](assets/chlimage_1-404.png)

   **列表视图**

   ![查看状态(如列表视图所示)](assets/review_status_listview.png)

## 为集合{#creating-a-review-task-for-collections}创建审核任务

1. 从收藏集页面中，选择要为其创建审阅任务的收藏集。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 创建审阅任务]** ![创建审阅任务](assets/do-not-localize/create-review-task.png)以打开&#x200B;**[!UICONTROL 审阅任务]**&#x200B;页。 如果工具栏上看不到该选项，请单击&#x200B;**[!UICONTROL 更多]**，然后选择该选项。

1. （可选）从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择要将审核任务关联到的项目。 默认情况下，选中&#x200B;**[!UICONTROL 无]**&#x200B;选项。 如果您不想将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑者级别权限（或更高）的项目才会显示在&#x200B;**[!UICONTROL 项目]**&#x200B;列表中。

1. 输入审核任务的名称，然后从&#x200B;**[!UICONTROL 分配给]**&#x200B;列表中选择审批者。

   >[!NOTE]
   >
   >在&#x200B;**[!UICONTROL “分配给]**”列表中，选定项目的成员／组可作为批准者。

1. 输入复查任务的说明、任务优先级和到期日。

   ![任务详细信息集合](assets/task_details-collection.png)

1. 单击&#x200B;**[!UICONTROL 提交]**，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;以关闭确认消息。 新任务的通知将发送给审批者。
1. 以批准者身份登录到[!DNL Assets]，然后导航到[!DNL Assets]控制台。 要批准资产，请单击&#x200B;**[!UICONTROL 通知]**，然后从列表中选择审核任务。
1. 在&#x200B;**[!UICONTROL 审阅任务]**&#x200B;页面中，检查审阅任务的详细信息，然后单击&#x200B;**[!UICONTROL 审阅]**。
1. 集合中的所有资产都会显示在审核页面上。 选择资产，然后根据需要单击&#x200B;**[!UICONTROL 批准／拒绝]**&#x200B;以批准或拒绝资产。

   ![review_任务_collection](assets/review_task_collection.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 完成]**。 在对话框中，输入注释，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;进行确认。
1. 导航到收藏集控制台并打开收藏集。 资产的批准状态图标会同时显示在卡和列表视图中。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *图：卡视图。*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *图：列表视图。*
