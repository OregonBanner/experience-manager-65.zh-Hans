---
title: 管理工作流实例
seo-title: Administering Workflow Instances
description: 了解如何管理工作流实例。
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 84%

---

# 管理工作流实例{#administering-workflow-instances}

工作流控制台提供了几种工具来管理工作流实例以确保它们按预期执行。

>[!NOTE]
>
>此 [JMX控制台](/help/sites-administering/jmx-console.md#workflow-maintenance) 提供了其他工作流维护操作。

提供了一系列控制台来管理您的工作流。使用[全局导航](/help/sites-authoring/basic-handling.md#global-navigation)以打开&#x200B;**工具**&#x200B;窗格，然后选择&#x200B;**工作流**：

* **模型**：管理工作流定义
* **实例**：查看和管理正在运行的工作流实例
* **启动器**：管理工作流的启动方式
* **存档**：查看已成功完成的工作流的历史记录
* **故障**：查看已完成但出现错误的工作流的历史记录
* **自动分配**：根据模板配置自动分配工作流

## 监控工作流实例状态 {#monitoring-the-status-of-workflow-instances}

1. 使用“导航”，依次选择&#x200B;**工具**&#x200B;和&#x200B;**工作流**。
1. 选择&#x200B;**实例**&#x200B;以显示当前正在进行的工作流实例的列表。

   ![wf-96](assets/wf-96.png)

<!--
## Search Workflow Instances {#search-workflow-instances}

1. Using Navigation select **Tools**, then **Workflow**.
1. Select **Instances** to display the list of workflow instances currently in progress. On the top rail, in the left corner, select **Filters**. Alternatively, you can use the keystrokes alt+1. The following dialog is displayed:

   ![wf-99-1](assets/wf-99-1.png)

1. In the Filter dialog, select the workflow search criteria. You can search based on these inputs:

   * Payload path: Select a specific path
   * Workflow model: Select a workflow model
   * Assignee: Select a workflow Assignee
   * Type: Task, Workflow item, or Workflow Failure
   * Task Status: Active, Complete, or Terminated
   * Where I Am: Owner AND Assignee, Owner only, Assignee only
   * Start Date: Start date before or after a specified date
   * End Date: End date before or after a specified date
   * Due Date: Due date before or after a specified date
   * Updated Date: Updated date before or after a specified date
-->

## 暂停、恢复和终止工作流实例 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用“导航”，依次选择&#x200B;**工具**&#x200B;和&#x200B;**工作流**。
1. 选择&#x200B;**实例**&#x200B;以显示当前正在进行的工作流实例的列表。

   ![wf-96-1](assets/wf-96-1.png)

1. 选择特定项目，然后相应地使用&#x200B;**终止**、**暂停**&#x200B;或&#x200B;**恢复**；需要确认和/或进一步的详细信息：

   ![wf-97-1](assets/wf-97-1.png)

## 查看存档的工作流 {#viewing-archived-workflows}

1. 使用“导航”，依次选择&#x200B;**工具**&#x200B;和&#x200B;**工作流**。
1. 选择&#x200B;**存档**&#x200B;以显示已成功完成的工作流实例的列表。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止状态被视为成功终止，因为它是用户操作的结果；例如：
   >
   >* 使用&#x200B;**终止**&#x200B;操作
   >* 当受工作流约束的页面被（强制）删除时，工作流将被终止

1. 选择特定项目，然后&#x200B;**打开历史记录**&#x200B;以查看更多详细信息：

   ![wf-99](assets/wf-99.png)

## 修复工作流实例故障 {#fixing-workflow-instance-failures}

当工作流失败时，AEM提供 **失败** 控制台让您进行调查，并在找到初始原因后执行适当的操作：

* **失败详细信息**
打开一个窗口以显示 **失败消息**， **步骤**、和 **失败栈栈**.

* **打开历史记录**
显示工作流历史记录的详细信息。

* **重试步骤**&#x200B;再次执行脚本步骤组件实例。修复导致原始错误的故障后，使用“重试步骤”命令。例如，在修复流程步骤执行的脚本中的错误后，重试该步骤。
* **终止**&#x200B;如果错误导致工作流出现不可调和的情况，则终止工作流。例如，工作流可以依赖于环境条件，例如存储库中对工作流实例不再有效的信息。
* **终止并重试**&#x200B;类似于&#x200B;**终止**，只不过使用原始有效负载、标题和描述来启动新的工作流实例。

要调查故障，然后恢复或终止工作流，请执行以下步骤：

1. 使用“导航”，依次选择&#x200B;**工具**&#x200B;和&#x200B;**工作流**。
1. 选择&#x200B;**故障**&#x200B;以显示未成功完成的工作流实例的列表。
1. 选择特定项目，然后选择适当的操作：

   ![wf-47](assets/wf-47.png)

## 定期清除工作流实例 {#regular-purging-of-workflow-instances}

最大限度地减少工作流实例的数量可以提高工作流引擎的性能，因此，您可以定期从存储库中清除已完成或正在运行的工作流实例。

配置 **Adobe Granite 工作流清除配置**&#x200B;以根据其时限和状态清除工作流实例。您还可以清除所有模型或特定模型的工作流实例。

您还可以创建多个服务配置以清除满足不同条件的工作流实例。例如，创建一个配置，以便在特定工作流模型的实例的运行时间显著超出预期时间时清除这些实例。创建另一个配置，以便在一定天数后清除所有已完成的工作流，从而最大限度地减小存储库。

要配置服务，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表描述了任一方法所需的属性。

>[!NOTE]
>
>对于将配置添加到存储库，服务 PID 为：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>由于服务是工厂服务，因此，`sling:OsgiConfig` 节点的名称需要标识符后缀，例如：
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>属性名称（Web 控制台）</th>
   <th>OSGi 属性名称</th>
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
   <td><p>要清除的工作流实例的状态。以下值有效：</p>
    <ul>
     <li>已完成：清除已完成的工作流实例。</li>
     <li>正在运行：清除正在运行的工作流实例。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要清除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流模型的 ID。ID是模型节点的路径，例如：<br /> /var/workflow/models/dam/update_asset<br /> </p> <p>要指定多个模型，请单击 Web 控制台中的 + 按钮。 </p> <p>请勿指定任何值以清除所有工作流模型的实例。</p> </td>
  </tr>
  <tr>
   <td>工作流时限</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流实例的时限（以天为单位）。</td>
  </tr>
 </tbody>
</table>

## 设置收件箱的最大大小 {#setting-the-maximum-size-of-the-inbox}

您可以通过配置 **AdobeGranite工作流服务**，使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表描述了为任一方法配置的属性。

>[!NOTE]
>
>对于将配置添加到存储库，服务 PID 为：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 属性名称（Web 控制台） | OSGi 属性名称 |
|---|---|
| 最大收件箱查询大小 | granite.workflow.inboxQuerySize |

## 对客户拥有的数据存储使用工作流变体 {#using-workflow-variables-customer-datastore}

工作流处理的数据存储在 Adobe 提供的存储 (JCR) 中。此类数据本质上可能是敏感的。您可能希望将所有用户定义的元数据/数据保存在您自己的托管存储中，而不是 Adobe 提供的存储中。这些部分描述了如何为外部存储设置这些变量。

### 设置模型以使用元数据的外部存储 {#set-model-for-external-storage}

在工作流模型级别，提供了一个标志来指示模型（及其运行时实例）具有元数据的外部存储。对于为外部存储标记的模型的工作流实例，工作流变量将不会保留在 JCR 中。

属性 *userMetadataPersistenceEnabled* 将存储在工作流模型的 *jcr:content 节点*&#x200B;上。此标志将作为 *cq:userMetaDataCustomPersistenceEnabled* 保留在工作流元数据中。

以下插图显示的是如何在工作流上设置标志。

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 外部存储中的元数据的 API {#apis-for-metadata-external-storage}

要在外部存储变量，您必须实施工作流公开的 API。

UserMetaDataPersistenceContext

以下示例说明如何使用 API。

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
