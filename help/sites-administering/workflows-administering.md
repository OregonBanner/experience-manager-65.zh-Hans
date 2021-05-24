---
title: 管理工作流实例
seo-title: 管理工作流实例
description: 了解如何管理工作流实例。
seo-description: 了解如何管理工作流实例。
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# 管理工作流实例{#administering-workflow-instances}

工作流控制台提供了多种用于管理工作流实例的工具，以确保它们按预期执行。

>[!NOTE]
>
>[JMX控制台](/help/sites-administering/jmx-console.md#workflow-maintenance)提供其他工作流维护操作。

一系列控制台可用于管理您的工作流。 使用[全局导航](/help/sites-authoring/basic-handling.md#global-navigation)打开&#x200B;**工具**&#x200B;窗格，然后选择&#x200B;**工作流**:

* **模型**:管理工作流定义
* **实例**:查看和管理正在运行的工作流实例
* **启动器**:管理工作流的启动方式
* **存档**:查看成功完成的工作流的历史记录
* **失败**:查看已完成但出现错误的工作流的历史记录

## 监控工作流实例的状态{#monitoring-the-status-of-workflow-instances}

1. 使用导航选择&#x200B;**工具**，然后选择&#x200B;**工作流**。
1. 选择&#x200B;**实例**&#x200B;以显示当前正在进行的工作流实例列表。

   ![wf-96](assets/wf-96.png)

1. 选择特定项目，然后选择&#x200B;**打开历史记录**&#x200B;以查看更多详细信息：

   ![wf-97](assets/wf-97.png)

## 暂停、恢复和终止工作流实例{#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用导航选择&#x200B;**工具**，然后选择&#x200B;**工作流**。
1. 选择&#x200B;**实例**&#x200B;以显示当前正在进行的工作流实例列表。

   ![wf-96-1](assets/wf-96-1.png)

1. 选择特定项目，然后根据需要使用&#x200B;**终止**、**暂停**&#x200B;或&#x200B;**恢复**;确认，和/或需要提供更多详细信息：

   ![wf-97-1](assets/wf-97-1.png)

## 查看存档的工作流{#viewing-archived-workflows}

1. 使用导航选择&#x200B;**工具**，然后选择&#x200B;**工作流**。
1. 选择&#x200B;**Archive**&#x200B;以显示成功完成的工作流实例列表。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止状态被视为由于用户操作而发生的成功终止；例如：
   >
   >* 使用&#x200B;**Terminate**&#x200B;操作
   >* 当受工作流约束的页面被（强制）删除时，工作流将被终止


1. 选择特定项目，然后选择&#x200B;**打开历史记录**&#x200B;以查看更多详细信息：

   ![wf-99](assets/wf-99.png)

## 修复工作流实例失败{#fixing-workflow-instance-failures}

当工作流失败时，AEM会提供&#x200B;**Failures**&#x200B;控制台，以便您在处理原始原因后调查并采取适当的操作：

* **失败详**
细信息打开一个窗口以显示 
**失败消息**、 **** 步骤 **和失败堆栈**。

* **打开**
历史记录显示工作流历史记录的详细信息。

* **重试** 步骤再次执行脚本步骤组件实例。修复了原始错误的原因后，请使用“重试步骤”命令。 例如，在修复了脚本中执行流程步骤的错误后，请重试该步骤。
* **** 终止如果错误导致工作流出现不可考虑的情况，则终止工作流。例如，工作流可以依赖于环境条件，例如存储库中对工作流实例不再有效的信息。
* **终止和重** 试与 **** 终止类似，不同之处在于新的工作流实例是使用原始有效负载、标题和描述启动的。

要调查失败，然后恢复或终止工作流，请执行以下步骤：

1. 使用导航选择&#x200B;**工具**，然后选择&#x200B;**工作流**。
1. 选择&#x200B;**失败**&#x200B;以显示未成功完成的工作流实例列表。
1. 选择特定项目，然后执行相应的操作：

   ![wf-47](assets/wf-47.png)

## 定期清除工作流实例{#regular-purging-of-workflow-instances}

最大限度地减少工作流实例数会提高工作流引擎的性能，因此您可以定期从存储库中清除已完成或正在运行的工作流实例。

配置&#x200B;**AdobeGranite工作流清除配置** ，以根据工作流实例的年龄和状态清除其实例。 您还可以清除所有模型或特定模型的工作流实例。

您还可以创建服务的多个配置，以清除满足不同标准的工作流实例。 例如，创建一个配置，在特定工作流模型的实例运行时间比预期时间长得多时清除这些实例。 创建另一个配置，该配置会在特定天数后清除所有已完成的工作流，以最大限度地减少存储库的大小。

要配置服务，可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。 下表介绍了任一方法所需的属性。

>[!NOTE]
>
>要将配置添加到存储库，服务PID为：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>由于服务是工厂服务，因此`sling:OsgiConfig`节点的名称需要一个标识符后缀，例如：
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>属性名称（Web控制台）</th>
   <th>OSGi属性名称</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>作业名称</td>
   <td>scheduledpurge.name</td>
   <td>计划清除的描述性名称。</td>
  </tr>
  <tr>
   <td>工作流状态</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>要清除的工作流实例的状态。 以下值有效：</p>
    <ul>
     <li>已完成：已完成的工作流实例已清除。</li>
     <li>正在运行：已清除运行的工作流实例。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要清除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流模型的ID。 ID是模型节点的路径，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br />指定不值以清除所有工作流模型的实例。</p> <p>要指定多个模型，请单击Web控制台中的+按钮。 </p> </td>
  </tr>
  <tr>
   <td>工作流年龄</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流实例的年龄（以天为单位）。</td>
  </tr>
 </tbody>
</table>

## 设置收件箱的最大大小{#setting-the-maximum-size-of-the-inbox}

您可以通过使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)来配置&#x200B;**AdobeGranite工作流服务**，从而设置收件箱的最大大小。 下表介绍了为任一方法配置的属性。

>[!NOTE]
>
>要将配置添加到存储库，服务PID为：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 属性名称（Web控制台） | OSGi属性名称 |
|---|---|
| 最大收件箱查询大小 | granite.workflow.inboxQuerySize |
