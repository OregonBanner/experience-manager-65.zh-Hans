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
source-git-commit: 8b4459c69b73159ce5afd819dfb772df5c51cd16
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 0%

---

# 管理工作流实例{#administering-workflow-instances}

工作流控制台提供了多种用于管理工作流实例的工具，以确保它们按预期执行。

>[!NOTE]
>
>的 [JMX控制台](/help/sites-administering/jmx-console.md#workflow-maintenance) 提供了其他工作流维护操作。

一系列控制台可用于管理您的工作流。 使用 [全局导航](/help/sites-authoring/basic-handling.md#global-navigation) 打开 **工具** 窗格，然后选择 **工作流**:

* **模型**:管理工作流定义
* **实例**:查看和管理正在运行的工作流实例
* **启动器**:管理工作流的启动方式
* **存档**:查看成功完成的工作流的历史记录
* **失败**:查看已完成但出现错误的工作流的历史记录
* **自动分配**:配置向模板自动分配工作流

## 监控工作流实例的状态 {#monitoring-the-status-of-workflow-instances}

1. 使用导航选择 **工具**，则 **工作流**.
1. 选择 **实例** 以显示当前正在进行的工作流实例列表。

   ![wf-96](assets/wf-96.png)


## 搜索工作流实例 {#search-workflow-instances}

1. 使用导航选择 **工具**，则 **工作流**.
1. 选择 **实例** 以显示当前正在进行的工作流实例列表。 在左角的上边栏中，选择 **过滤器**. 或者，您也可以使用alt+1键击。 将显示以下对话框：

   ![wf-99-1](assets/wf-99-1.png)

1. 在过滤器对话框中，选择工作流搜索条件。 您可以根据以下输入进行搜索：

   * 负载路径：选择特定路径
   * 工作流模型：选择工作流模型
   * 被分派人：选择工作流被分派人
   * 类型：任务、工作流项或工作流失败
   * 任务状态：活动、完成或终止
   * 我的位置：责任人AND Assignee，仅限责任人，仅限受分配人
   * 开始日期：指定日期之前或之后的开始日期
   * 结束日期：指定日期之前或之后的结束日期
   * 到期日期：指定日期之前或之后的到期日期
   * 更新日期：在指定日期之前或之后更新的日期

## 暂停、恢复和终止工作流实例 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用导航选择 **工具**，则 **工作流**.
1. 选择 **实例** 以显示当前正在进行的工作流实例列表。

   ![wf-96-1](assets/wf-96-1.png)

1. 选择特定项目，然后使用 **终止**, **暂停**&#x200B;或 **恢复**，酌情；确认，和/或需要提供更多详细信息：

   ![wf-97-1](assets/wf-97-1.png)

## 查看存档的工作流 {#viewing-archived-workflows}

1. 使用导航选择 **工具**，则 **工作流**.
1. 选择 **存档** 以显示成功完成的工作流实例列表。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止状态被视为由于用户操作而发生的成功终止；例如：
   >
   >* 使用 **终止** 操作
   >* 当受工作流约束的页面被（强制）删除时，工作流将被终止


1. 选择特定项目，然后 **打开历史记录** 要查看更多详细信息，请执行以下操作：

   ![wf-99](assets/wf-99.png)

## 修复工作流实例失败 {#fixing-workflow-instance-failures}

当工作流失败时，AEM会提供 **失败** 控制台允许您在处理原始原因后进行调查并采取适当措施：

* **失败详细信息**
打开一个窗口以显示 
**失败消息**, **步骤** 和 **失败堆栈**.

* **打开历史记录**
显示工作流历史记录的详细信息。

* **重试步骤** 再次执行脚本步骤组件实例。 修复了原始错误的原因后，请使用“重试步骤”命令。 例如，在修复了脚本中执行流程步骤的错误后，请重试该步骤。
* **终止** 如果错误导致了工作流的不可考虑情况，则终止工作流。 例如，工作流可以依赖于环境条件，例如存储库中对工作流实例不再有效的信息。
* **终止并重试** 类似于 **终止** 除了使用原始有效负载、标题和描述启动新的工作流实例之外。

要调查失败，然后恢复或终止工作流，请执行以下步骤：

1. 使用导航选择 **工具**，则 **工作流**.
1. 选择 **失败** 以显示未成功完成的工作流实例列表。
1. 选择特定项目，然后执行相应的操作：

   ![wf-47](assets/wf-47.png)

## 定期清除工作流实例 {#regular-purging-of-workflow-instances}

最大限度地减少工作流实例数会提高工作流引擎的性能，因此您可以定期从存储库中清除已完成或正在运行的工作流实例。

配置 **AdobeGranite工作流清除配置** 根据工作流实例的年龄和状态清除工作流实例。 您还可以清除所有模型或特定模型的工作流实例。

您还可以创建服务的多个配置，以清除满足不同标准的工作流实例。 例如，创建一个配置，在特定工作流模型的实例运行时间比预期时间长得多时清除这些实例。 创建另一个配置，该配置会在特定天数后清除所有已完成的工作流，以最大限度地减少存储库的大小。

要配置服务，您可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表介绍了任一方法所需的属性。

>[!NOTE]
>
>要将配置添加到存储库，服务PID为：
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>由于服务是工厂服务，因此 `sling:OsgiConfig` 节点需要使用标识符后缀，例如：
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
   <td><p>要清除的工作流模型的ID。 ID是模型节点的路径，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 指定不值以清除所有工作流模型的实例。</p> <p>要指定多个模型，请单击Web控制台中的+按钮。 </p> </td>
  </tr>
  <tr>
   <td>工作流年龄</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流实例的年龄（以天为单位）。</td>
  </tr>
 </tbody>
</table>

## 设置收件箱的最大大小 {#setting-the-maximum-size-of-the-inbox}

您可以通过配置 **AdobeGranite工作流服务**，使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [将OSGi配置添加到存储库](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository). 下表介绍了为任一方法配置的属性。

>[!NOTE]
>
>要将配置添加到存储库，服务PID为：
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 属性名称（Web控制台） | OSGi属性名称 |
|---|---|
| 最大收件箱查询大小 | granite.workflow.inboxQuerySize |

## 为客户拥有的数据存储使用工作流变量 {#using-workflow-variables-customer-datastore}

由工作流处理的数据存储在Adobe提供的存储(JCR)中。 此数据在性质上可能是敏感的。 您可能希望将所有用户定义的元数据/数据保存在您自己的托管存储中，而不是Adobe提供的存储中。 以下部分介绍如何为外部存储设置这些变量。

### 设置模型以使用元数据的外部存储 {#set-model-for-external-storage}

在工作流模型的级别，提供一个标记来指示模型（及其运行时实例）具有元数据的外部存储。 对于标记为外部存储的模型的工作流实例，不会在JCR中保留工作流变量。

资产 *userMetadataPersistenceEnabled* 将存储在 *jcr:content节点* 工作流模型的子目录访问。 此标记将作为 *cq:userMetaDataCustomPersistenceEnabled*.

下图显示了必须在工作流中设置标记。

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 外部存储中元数据的API {#apis-for-metadata-external-storage}

要在外部存储变量，您必须实施工作流公开的API。

UserMetaDataPersistenceContext

以下示例向您展示了如何使用API。

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
