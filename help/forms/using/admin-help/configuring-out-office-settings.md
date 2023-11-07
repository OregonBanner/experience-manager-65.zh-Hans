---
title: 配置“外出”设置
description: “外出”功能允许您指定用户何时外出且无法完成AEM表单分配的任务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 配置“外出”设置 {#configuring-out-of-office-settings}

“外出”功能使用户或管理员可以指定用户何时外出且无法完成AEM表单分配的任务。 当用户设置为“外出”时，其任务将分配给一个或多个指定用户。 用户可以在Workspace中更改其“外出”设置，或者管理员可以代表用户在表单工作流中更改设置。

创建进程时，Workbench用户可以指定任务是否可以因“外出”设置而被重定向。

## 查看用户的外出信息 {#view-a-user-s-out-of-office-information}

1. 在管理控制台中，单击服务>表单工作流>外出。
1. 在“外出”页面顶部附近的框中，您可以执行以下操作之一：

   **按名称搜索**

   选择按名称搜索选项。 键入全部或部分用户名，然后单击查找。 如果将该字段留空，Forms工作流将返回所有用户的列表。

   **按日期范围搜索**

   选择按日期范围搜索选项。 指定开始日期和结束日期以及所需的时间戳以缩小搜索结果。 单击“查找”。

1. 单击用户名可在用户列表下方显示用户的“外出”信息。

## 更改用户的外出状态 {#change-a-user-s-out-of-office-status}

1. 查找用户，如中所述 [查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 单击要更改的用户名。
1. 从 *用户名* 位于当前列表中，选择在办公室中或外出办公室。
1. 单击保存。

## 为用户添加外出日期范围 {#add-an-out-of-office-date-range-for-a-user}

1. 查找用户，如中所述 [查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 单击要更改的用户名。
1. 单击添加日期范围。
1. 输入开始时间和结束时间。 您可以单击日历图标以选择日期。 如果不指定结束时间，则会将用户无限期地设置为不在办公室。
1. 单击保存。

## 为外出任务分配用户 {#assign-a-user-for-out-of-office-tasks}

当用户不在办公室时，您可以分配一个或多个用户为该用户执行任何新任务。 您可以设置以下配置：

* 将所有新任务分配给指定的默认用户。
* 请勿重新分配任何任务。 新任务仍被分配给不在办公室的用户。
* 分配一个默认用户，该用户将接收该用户的大部分任务，但指定将某些流程中的任务重新分配给其他用户或保留分配给不在办公室的用户。
* 不要分配默认用户，而是将某些进程中的某些任务分配给特定用户。

   1. 查找用户，如中所述 [查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. 单击要更改的用户名。
   1. 在“Default User For Out Office Tasks（外出任务的默认用户）”列表中，选择一个用户。 如果不想指定默认用户接收重新分配的物料，请选择“不分配”。

      如果列表中未显示相应的用户名，请单击“查找用户”，然后使用“查找用户”对话框搜索该用户。 从列表中选择适当的用户，然后单击“选择用户”。 您还可以单击“查找用户”对话框中的“查看用户计划”来查看选定用户的外出计划。

   1. 如果有任何不应发送给默认用户的进程，请单击添加例外，然后选择该进程并从列表中选择另一个用户。 您还可以选择“不分配”，以将任务保持分配给不在办公室的用户。
   1. 单击保存。
