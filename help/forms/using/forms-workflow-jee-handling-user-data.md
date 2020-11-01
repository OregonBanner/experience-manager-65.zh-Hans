---
title: Forms·吉工作流 |处理用户数据
seo-title: Forms·吉工作流 |处理用户数据
description: Forms·吉工作流 |处理用户数据
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---


# Forms·吉工作流 |处理用户数据 {#forms-jee-workflows-handling-user-data}

AEM FormsJEE工作流提供设计、创建和管理业务流程的工具。 工作流进程由一系列按指定顺序执行的步骤组成。 每个步骤都执行特定操作，如向用户分配任务或发送电子邮件。 流程可以与资产、用户帐户和服务交互，并可以使用以下任一方法触发：

* 从AEM Forms工作区启动流程
* 使用SOAP或RESTful服务
* 提交自适应表单
* 使用监视文件夹
* 使用电子邮件

有关创建AEM FormsJEE工作流流程的详细信息，请参阅工 [作台帮助](http://www.adobe.com/go/learn_aemforms_workbench_65)。

## 用户数据和数据存储 {#user-data-and-data-stores}

当进程被触发并在进行时，它会捕获有关进程参加者的数据、参加者在与进程关联的表单中输入的数据以及添加到表单的附件。 数据存储在AEM FormsJEE服务器存储库中，如果配置了，某些数据（如附件）会存储在全局文档(GDS)目录中。 可以在共享文件系统或数据库上配置GDS目录。

## 访问和删除用户数据 {#access-and-delete-user-data}

当触发进程时，将生成唯一的进程实例ID和长寿命调用ID并与该进程实例相关联。 您可以基于长期调用ID访问和删除进程实例的数据。 您可以使用已提交其任务的进程发起者或进程参与者的用户名推断进程实例的长期调用ID。

但是，在以下情况下，您无法标识启动器的进程实例ID:

* **通过监视的文件夹触发的进程**:如果进程由监视的文件夹触发，则无法使用其启动器来标识该进程实例。 在这种情况下，用户信息被编码在所存储的数据中。
* **从发布AEM实例启动的进程**:从AEM发布实例触发的所有进程实例不会捕获有关启动器的信息。 但是，用户数据可以以与进程相关联的形式捕获，该形式存储在工作流变量中。
* **通过电子邮件启动的流程**:发送者的电子邮件ID被捕获为数据库表的不透明blob列中的 `tb_job_instance` 一个属性，无法直接查询。

### 在已知工作流发起者或参与者时标识进程实例ID {#initiator-participant}

执行以下步骤以标识工作流发起者或参与者的流程实例ID:

1. 在AEM Forms服务器数据库中执行以下命令，从数据库表中检索工作流发起者或参与者的主 `edcprincipalentity` 体ID。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查询返回指定的主体ID `user_ID`。

1. (对&#x200B;**于工作流启动器**)执行以下命令，从数据库表中检索与启动器的主体ID关联的 `tb_task` 所有任务。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查询返回由指定的_启动的 `initiator`任务 `principal_id`。 任务有两种类型：

   * **已完成任务**:这些任务已提交，并在字段中显示一个字母数字 `process_instance_id` 值。 记下已提交任务的所有进程实例ID，并继续执行这些步骤。
   * **任务已启动但未完成**:这些任务已经启动，但尚未提交。 这些任务 `process_instance_id` 的字段值 **为** 0（零）。 在这种情况下，请注意相应的任务ID，并参 [阅使用孤立任务](#orphan)。

1. (对&#x200B;**于工作流参加者**)执行以下命令，从数据库表中检索与启动器的进程参与者的主体ID关联的进程实例 `tb_assignment` ID。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查询返回与参加者关联的所有进程的实例ID，包括参加者尚未提交任何任务的进程。

   记下已提交任务的所有进程实例ID，并继续执行这些步骤。

   对于孤立任务或， `process_instance_id` 如果任务为0（零），请记下相应的任务ID，并参阅 [使用孤立任务](#orphan)。

1. 按照基于流程实 [例ID的工作流实例中清除用户数据部分中的说明](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) ，删除已标识的流程实例ID的用户数据。

### 当用户数据存储在基元变量中时标识进程实例ID {#primitive}

可以设计一个工作流，以便用户数据被捕获到变量中，该变量被存储为数据库中的Blob。 在这种情况下，仅当用户数据存储在以下简单类型变量之一时，您才可以查询用户数据：

* **字符串**:直接包含用户ID或作为子字符串包含，并可使用SQL进行查询。
* **数字**:直接包含用户ID。
* **XML**:包含用户ID作为子字符串，在数据库中存储为文本列的文本中，可以像字符串一样查询。

执行以下步骤以确定以简单类型变量存储数据的工作流是否包含用户数据：

1. 执行以下数据库命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查询返回指定应用程 `tb_<number>` 序()和工作流() `app_name`格式的表 `workflow_name`名称。

   >[!NOTE]
   >
   >如果工作流嵌套 `name` 在应用程序内的子文件夹中，则属性的值可能很复杂。 请确保指定工作流的确切完整路径，您可以从数据库表 `omd_object_type` 获取该路径。

1. 查看表 `tb_<number>` 模式。 该表包含存储指定工作流的用户数据的变量。 表中的变量与工作流中的变量相对应。

   识别并记下与包含用户ID的工作流变量对应的变量。 如果标识的变量为基元类型，则可以运行查询来确定与用户ID关联的工作流实例。

1. 执行以下数据库命令。 在此命令中， `user_var` 是包含用户ID的基元类型变量。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   该查询返回与指定的进程实例ID关联的所有进程实例 `user_ID`。

1. 按照基于流程实 [例ID的工作流实例中清除用户数据部分中的说明](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) ，删除已标识的流程实例ID的用户数据。

### 根据流程实例ID从工作流实例中清除用户数据 {#purge}

现在，您已识别与用户关联的进程实例ID，请执行以下操作以从相应的进程实例中删除用户数据。

1. 执行以下命令，从表中检索进程实例的长期调用ID和 `tb_process_instance` 状态。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查询返回指定的长期调用ID和状态 `process_instance_id`。

1. 使用具有正确连接设 `ProcessManager` 置的实 `com.adobe.idp.workflow.client.ProcessManager`例创建公 `ServiceClientFactory` 共客户端()的实例。

   有关详细信息，请参阅类ProcessManager的Java [API参考](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)。

1. 检查工作流实例的状态。 如果状态不是2(COMPLETE)或4(TERMINATED)，请首先调用以下方法终止实例：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 通过调用以下方法清除工作流实例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   如果 `purgeProcessInstance` 配置了该方法，则从AEM Forms服务器数据库和GDS中完全删除指定调用ID的所有数据。

### 使用孤立任务 {#orphan}

孤立任务是已启动但尚未提交其包含过程的任务。 在这种情况下， `process_instance_id` 为 **0** （零）。 因此，您无法使用进程实例ID跟踪为孤立任务存储的用户数据。 但是，您可以使用孤立任务的任务ID跟踪它。 如识别流程实例ID中所述，当 `tb_task` 工作流发起者或参加者 [被知时，您可以从表中识别用户的任务ID](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)。

获得任务ID后，请执行以下操作，以从GDS和任务库中清除孤立的关联文件和数据。

1. 在AEM Forms服务器任务库上执行以下命令以检索标识的数据ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查询返回ID列表。 对于结果中返 `fd_id`回的每个ID()，创建会话ID字符串的列表，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根据GDS是指向文件系统还是数据库，执行以下步骤之一：

   1. **文件系统中的GDS**

      在GDS文件系统中：

      1. 搜索扩展名为以下会话ID字符串的文件：
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      具有这些扩展名的文件是标记文件。 文件名采用以下格式进行存储：

      `<file_name_guid>.session<session_id_string>`

      1. 从文件系统中删除文件名完全相同的所有标记 `<file_name_guid>` 文件和其他文件。
   1. **数据库中的GDS**

      对每个会话ID执行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 执行以下命令，从AEM Forms服务器任务库删除ID的数据：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

