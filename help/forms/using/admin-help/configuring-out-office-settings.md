---
title: 配置外出设置
seo-title: 配置外出设置
description: 使用“办公室外”功能，您可以指定用户何时离开办公室，并且无法完成AEM表单分配的任务。
seo-description: 使用“办公室外”功能，您可以指定用户何时离开办公室，并且无法完成AEM表单分配的任务。
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---


# 配置办公室外设置{#configuring-out-of-office-settings}

使用“办公室外”功能，用户或管理员可以指定用户何时离开办公室，并且无法完成AEM表单分配的任务。 当用户设置为“外出”时，其任务将分配给一个或多个指定用户。 用户可以在Workspace中更改其“办公室外”设置，管理员也可以在表单工作流中代表用户更改设置。

创建流程时，Workbench用户可以指定任务是否可由于“办公室外”设置而被重定向。

## 视图用户的办公室外信息{#view-a-user-s-out-of-office-information}

1. 在管理控制台中，单击“服务”>“表单工作流”>“办公室外”。
1. 在“办公室外”页面顶部附近的框中，您可以执行下列操作之一：

   **按名称搜索**

   选择“按名称搜索”选项。 键入全部或部分用户名，然后单击“查找”。 如果将字段留空，Forms工作流将返回所有用户的列表

   **按日期范围搜索**

   选择按日期范围搜索选项。 指定起始和终止日期以及所需的时间戳，以缩小搜索结果。 单击“查找”。

1. 单击用户名可在用户列表下显示用户的“办公室外”信息。

## 更改用户的办公室外状态{#change-a-user-s-out-of-office-status}

1. 查找用户，如[视图用户的Out of Office信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
1. 单击要更改的用户的名称。
1. 从&#x200B;*用户名*&#x200B;当前为列表，选择“在办公室中”或“在办公室之外”。
1. 单击保存。

## 为用户{#add-an-out-of-office-date-range-for-a-user}添加“Out of Office”日期范围

1. 查找用户，如[视图用户的Out of Office信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
1. 单击要更改的用户的名称。
1. 单击“添加日期范围”。
1. 输入开始时间和结束时间。 您可以单击日历图标以选择日期。 如果不指定结束时间，则用户将被无限期地设置为不在办公室。
1. 单击保存。

## 为“办公室外”任务分配用户{#assign-a-user-for-out-of-office-tasks}

当用户不在办公室时，您可以指派一个或多个用户为用户执行任何新任务。 您可以设置以下配置：

* 将所有新任务分配给指定的默认用户。
* 请勿重新分配任何任务。 新任务仍分配给不在办公室的用户。
* 指定将接收大多数用户任务的默认用户，但指定将特定进程的任务重新分配给其他用户，或仍分配给不在办公室的用户。
* 不要分配默认用户，而是将特定进程中的特定任务分配给特定用户。

   1. 查找用户，如[视图用户的Out of Office信息](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)中所述。
   1. 单击要更改的用户的名称。
   1. 在“Default User For Out Office”任务列表中，从列表中选择一个用户。 如果不想指定默认用户接收重新分配的项目，请选择“不分配”。

      如果相应的用户名未出现在列表中，请单击“查找用户”，然后使用“查找用户”对话框搜索用户。 从列表中选择相应的用户，然后单击“选择用户”。 您还可以在“查找用户”对话框中单击视图用户的计划，以查看选定用户的办公室外计划。

   1. 如果有任何进程不应发送给默认用户，请单击“添加异常”，然后选择该进程并从列表中选择其他用户。 您也可以选择“不分配”，将任务分配给不在办公室的用户。
   1. 单击保存。

