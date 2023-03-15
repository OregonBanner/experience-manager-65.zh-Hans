---
title: 审核文件夹资源和收藏集
description: 为文件夹或收藏集中的资产设置审阅工作流，并与审阅人或创意合作伙伴共享该工作流以寻求反馈。
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 5%

---

# 审核文件夹资源和收藏集 {#review-folder-assets-and-collections}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/bulk-approval.html?lang=en) |

为文件夹或收藏集中的资产设置审阅工作流，并与审阅人或创意合作伙伴共享该工作流以寻求反馈。

[!DNL Adobe Experience Manager Assets] 允许您为文件夹或收藏集中的资产设置临时审阅工作流，并与审阅人或创意合作伙伴共享该工作流以寻求反馈。

您可以将审阅工作流与项目关联，也可以创建独立的审阅任务。

共享资产后，审核者可以批准或拒绝资产。 通知会在工作流的各个阶段发送，以通知目标收件人有关各种任务的完成。 例如，当您共享文件夹或收藏集时，审阅人会收到一则通知，指出已共享文件夹/收藏集以供审阅。

在审核者完成审核（批准或拒绝资产）后，您将收到审核完成通知。

## 为文件夹创建审核任务 {#creating-a-review-task-for-folders}

1. 从 [!DNL Assets] 用户界面中，选择要为其创建审阅任务的文件夹。
1. 在工具栏中，单击 **[!UICONTROL 创建审阅任务]** ![创建审阅任务](assets/do-not-localize/create-review-task.png) 以打开 **[!UICONTROL 审核任务]** 页面。 如果在工具栏中看不到该选项，请单击 **[!UICONTROL 更多]** 然后选择选项。

1. （可选）从 **[!UICONTROL 项目]** 列表中，选择要与审阅任务关联的项目。 默认情况下， **[!UICONTROL 无]** 选项。 如果不想将任何项目与审阅任务相关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高版本）的项目才会在中显示 **[!UICONTROL 项目]** 列表。

1. 输入审核任务的名称，然后从中选择一个批准者 **[!UICONTROL 分配给]** 列表。

   >[!NOTE]
   >
   >所选项目的成员/组可作为批准者出现在 **[!UICONTROL 分配给]** 列表。

1. 输入审阅任务的描述、任务优先级和到期日。

   ![task_details](assets/task_details.png)

1. 在高级选项卡中，输入要用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. 单击 **[!UICONTROL 提交]**，然后单击 **[!UICONTROL 完成]** 以关闭确认消息。 新任务的通知将发送给审批者。
1. 登录 [!DNL Assets] 以审批者身份导航至 [!DNL Assets] UI。 要批准资源，请单击 **[!UICONTROL 通知]** 然后从列表中选择审阅任务。

   ![资产通知](assets/aemAssetsNotification.png)

1. 在 **[!UICONTROL 审核任务]** 页，检查复查任务的详细资料，然后单击 **[!UICONTROL 审核]**.
1. 在 **[!UICONTROL 审核任务]** 页面，选择资源，然后单击 **[!UICONTROL 批准/拒绝]** 以批准或拒绝（根据需要）。

   ![review_task](assets/review_task.png)

1. 单击 **[!UICONTROL 完成]** 工具栏中。 在对话框中，输入注释并单击  **[!UICONTROL 完成]** 以确认。
1. 导航到 [!DNL Assets] 用户界面并打开文件夹。 资产的审批状态图标会显示在卡片视图和列表视图中。

   **信息卡视图**

   ![查看卡片视图中的状态](assets/chlimage_1-404.png)

   **列表视图**

   ![查看列表视图中的状态](assets/review_status_listview.png)

## 为收藏集创建审核任务 {#creating-a-review-task-for-collections}

1. 从“收藏集”页面中，选择要为其创建审阅任务的收藏集。
1. 在工具栏中，单击 **[!UICONTROL 创建审阅任务]** ![创建审阅任务](assets/do-not-localize/create-review-task.png) 以打开 **[!UICONTROL 审核任务]** 页面。 如果在工具栏上看不到该选项，请单击 **[!UICONTROL 更多]** 然后选择选项。

1. （可选）从 **[!UICONTROL 项目]** 列表中，选择要与审阅任务关联的项目。 默认情况下， **[!UICONTROL 无]** 选项。 如果不想将任何项目与审阅任务相关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高版本）的项目才会在中显示 **[!UICONTROL 项目]** 列表。

1. 输入审核任务的名称，然后从中选择一个批准者 **[!UICONTROL 分配给]** 列表。

   >[!NOTE]
   >
   >所选项目的成员/组可作为批准者出现在 **[!UICONTROL 分配给]** 列表。

1. 输入审阅任务的描述、任务优先级和到期日。

   ![task_details — 收藏集](assets/task_details-collection.png)

1. 单击 **[!UICONTROL 提交]**，然后单击 **[!UICONTROL 完成]** 以关闭确认消息。 新任务的通知将发送给审批者。
1. 登录 [!DNL Assets] 以审批者身份导航至 [!DNL Assets] 控制台。 要批准资源，请单击 **[!UICONTROL 通知]** 然后从列表中选择审阅任务。
1. 在 **[!UICONTROL 审核任务]** 页，检查复查任务的详细资料，然后单击 **[!UICONTROL 审核]**.
1. 收藏集中的所有资产均显示在审核页面上。 选择资源并单击 **[!UICONTROL 批准/拒绝]** 批准或拒绝资产（根据需要）。

   ![review_task_collection](assets/review_task_collection.png)

1. 单击 **[!UICONTROL 完成]** 工具栏中。 在对话框中，输入注释并单击 **[!UICONTROL 完成]** 以确认。
1. 导航到收藏集控制台并打开收藏集。 资产的审批状态图标会同时显示在“信息卡”和“列表”视图中。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *图：卡片视图。*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *图：列表视图。*
