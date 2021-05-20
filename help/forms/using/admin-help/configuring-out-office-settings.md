---
title: 配置“不在办公室”设置
seo-title: 配置“不在办公室”设置
description: “外出”功能允许您指定用户何时离开办公室，无法完成由AEM表单分配的任务。
seo-description: “外出”功能允许您指定用户何时离开办公室，无法完成由AEM表单分配的任务。
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 配置“不在办公室”设置{#configuring-out-of-office-settings}

“外出”功能使用户或管理员能够指定用户何时离开办公室，无法完成由AEM表单分配的任务。 当用户设置为“不在办公室”时，其任务会分配给一个或多个指定用户。 用户可以在工作区中更改其“不在办公室”设置，或者管理员可以在表单工作流中代表用户更改设置。

在创建流程时，Workbench用户可以指定是否因“不在办公室”设置而可以重定向任务。

## 查看用户的外出信息{#view-a-user-s-out-of-office-information}

1. 在管理控制台中，单击“服务”>“表单工作流”>“不在办公室”。
1. 在“Out of Office”（外出）页面顶部附近的框中，您可以执行以下操作之一：

   **按名称搜索**

   选择按名称搜索选项。 键入所有或部分用户名，然后单击“查找”。 如果将字段留空，则Forms工作流会返回所有用户的列表

   **按日期范围搜索**

   选择按日期范围搜索选项。 指定开始日期和结束日期以及所需的时间戳，以缩小搜索结果。 单击“查找”。

1. 单击用户名可在用户列表下方显示用户的“外出”信息。

## 更改用户的外出状态{#change-a-user-s-out-of-office-status}

1. 查找用户，如[查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
1. 单击要更改的用户的名称。
1. 从&#x200B;*用户名*&#x200B;当前列表中，选择“在办公室”或“不在办公室”。
1. 单击保存。

## 为用户{#add-an-out-of-office-date-range-for-a-user}添加“不在办公室”日期范围

1. 查找用户，如[查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
1. 单击要更改的用户的名称。
1. 单击添加日期范围。
1. 输入开始时间和结束时间。 您可以单击日历图标以选择日期。 如果您没有指定结束时间，则用户将被无限期地设置为不在办公室。
1. 单击保存。

## 为“外出”任务分配用户{#assign-a-user-for-out-of-office-tasks}

当用户不在办公室时，您可以指派一个或多个用户为用户执行任何新任务。 您可以设置以下配置：

* 将所有新任务分配给指定的默认用户。
* 请勿重新分配任何任务。 新任务仍分配给不在办公室的用户。
* 为将接收大多数用户任务的默认用户分配，但指定将某些进程中的任务重新分配给其他用户，或者保留分配给不在办公室的用户。
* 不要分配默认用户，而是将特定进程中的某些任务分配给特定用户。

   1. 查找用户，如[查看用户的外出信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
   1. 单击要更改的用户的名称。
   1. 在“Default User For Of Office Tasks”列表中，从列表中选择一个用户。 如果您不想指定默认用户来接收重新分配的项目，请选择“不分配”。

      如果列表中未显示相应的用户名，请单击“查找用户”，然后使用“查找用户”对话框搜索该用户。 从列表中选择相应的用户，然后单击“选择用户”。 您还可以单击“查找用户”对话框中的“查看用户的计划”，以查看所选用户的外出计划。

   1. 如果有任何进程不应发送给默认用户，请单击添加例外，然后选择该进程并从列表中选择其他用户。 您还可以选择“不分配”，以将任务保留分配给不在办公室的用户。
   1. 单击保存。
