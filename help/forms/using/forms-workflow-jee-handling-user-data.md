---
title: 表单JEE工作流程|处理用户数据
seo-title: 表单JEE工作流程|处理用户数据
description: 'null'
seo-description: 'null'
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 表单JEE工作流程|处理用户数据 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE工作流程提供了用于设计、创建和管理业务流程的工具。 工作流进程由一系列按指定顺序执行的步骤组成。 每个步骤都会执行特定操作，如向用户分配任务或发送电子邮件。 流程可以与资产、用户帐户和服务交互，并可以使用以下任一方法触发：

* 从AEM Forms Workspace启动流程
* 使用SOAP或RESTful服务
* 提交自适应表单
* 使用监视文件夹
* 使用电子邮件

有关创建AEM Forms JEE工作流程的详细信息，请参阅工作 [台帮助](http://www.adobe.com/go/learn_aemforms_workbench_65)。

## 用户数据和数据存储 {#user-data-and-data-stores}

当进程被触发并进行时，它会捕获有关进程参加者的数据、参加者在与进程关联的表单中输入的数据以及添加到表单的附件。 数据存储在AEM Forms JEE服务器数据库中，如果配置了此类数据，某些数据（如附件）会存储在全局文档存储(GDS)目录中。 可以在共享文件系统或数据库上配置GDS目录。

## 访问和删除用户数据 {#access-and-delete-user-data}

当进程被触发时，将生成唯一的进程实例ID和长期调用ID并与进程实例相关联。 您可以基于长期调用ID访问和删除进程实例的数据。 您可以使用已提交任务的进程启动器或进程参加者的用户名推断进程实例的长期调用ID。

但是，在以下情况下，您无法标识启动器的进程实例ID:

* **通过监视的文件夹触发的进程**:如果进程是由监视的文件夹触发的，则无法使用进程实例的启动器进行标识。 在这种情况下，用户信息被编码在所存储的数据中。
* **从发布AEM实例启动的进程**:从AEM发布实例触发的所有进程实例不会捕获有关启动器的信息。 但是，用户数据可以以与进程相关联的形式被捕获，该形式被存储在工作流变量中。
* **通过电子邮件发起的流程**:发送者的电子邮件ID将捕获为数据库表的不透明blob列中的一个属性， `tb_job_instance` 不能直接查询该属性。

### 在工作流发起者或参加者已知时识别进程实例ID {#initiator-participant}

执行以下步骤以标识工作流启动器或参加者的进程实例ID:

1. 在AEM Forms服务器数据库中执行以下命令，从数据库表中检索工作流启动器或参加者的主 `edcprincipalentity` 体ID。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   查询将返回指定的主体ID `user_ID`。

1. (对&#x200B;**于工作流启动器**)执行以下命令，从数据库表中检索与启动器的主ID关联的所 `tb_task` 有任务。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   查询将返回由指定的 `initiator`_启动的任务 `principal_id`。 任务分为两种类型：

   * **已完成的任务**:这些任务已提交，并在字段中显示一个字母数字 `process_instance_id` 值。 注意已提交任务的所有进程实例ID，并继续执行这些步骤。
   * **已启动但未完成的任务**:这些任务已启动但尚未提交。 这些任务的字 `process_instance_id` 段中的值为 **0** （零）。 在这种情况下，请注意相应的任务ID，并参阅 [处理孤立任务](#orphan)。

1. (对&#x200B;**于工作流参加者**)执行以下命令，从数据库表中检索与启动者的进程参加者的主体ID关联的进程实例 `tb_assignment` ID。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   查询返回与参加者关联的所有进程的实例ID，包括参加者尚未提交任何任务的进程。

   注意已提交任务的所有进程实例ID，并继续执行这些步骤。

   对于孤立任务或其为0( `process_instance_id` 零)的任务，请注意相应的任务ID，并参阅 [处理孤立任务](#orphan)。

1. 按照基于进程实 [例ID的工作流实例中的清除用户数据部分中的说明](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) ，删除标识的进程实例ID的用户数据。

### 识别将用户数据存储在基本变量中的进程实例ID {#primitive}

可以设计一个工作流，以便将数据捕获到变量中，该变量作为blob存储在数据库中。 在这种情况下，仅当用户数据存储在以下简单类型变量之一时，才能查询用户数据：

* **字符串**:直接包含用户ID或作为子字符串包含，并可以使用SQL进行查询。
* **数字**:直接包含用户ID。
* **XML**:将用户ID作为子字符串包含在作为文本列存储在数据库中的文本中，并可以像字符串一样进行查询。

执行以下步骤以确定以简单类型变量存储数据的工作流是否包含用户的数据：

1. 执行以下数据库命令：

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   查询返回指定应用程 `tb_<number>` 序()和工作流()格 `app_name`式的表名 `workflow_name`称。

   >[!NOTE]
   >
   >如果工作流嵌套 `name` 在应用程序内的子文件夹中，则属性的值可能很复杂。 确保指定工作流的精确完整路径，您可以从数据库表中获 `omd_object_type` 取该路径。

1. 查看表 `tb_<number>` 架构。 该表包含存储指定工作流的用户数据的变量。 表中的变量与工作流中的变量相对应。

   识别并记下与包含用户ID的工作流变量相对应的变量。 如果标识的变量为简单类型，则可以运行查询以确定与用户ID关联的工作流实例。

1. 执行以下数据库命令。 在此命令中， `user_var` 是包含用户ID的简单类型变量。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   查询将返回与指定的进程实例ID关联的所有进程实例ID `user_ID`。

1. 按照基于进程实 [例ID的工作流实例中的清除用户数据部分中的说明](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) ，删除标识的进程实例ID的用户数据。

### 根据流程实例ID从工作流实例中清除用户数据 {#purge}

既然您已经识别了与用户关联的进程实例ID，请执行以下操作以从相应的进程实例中删除用户数据。

1. 执行以下命令，从表中检索进程实例的长期调用ID和状 `tb_process_instance` 态。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   查询将返回指定的长期调用ID和状态 `process_instance_id`。

1. 使用具有正确连接设 `ProcessManager` 置的实例创 `com.adobe.idp.workflow.client.ProcessManager`建公共客 `ServiceClientFactory` 户端()的实例。

   有关详细信息，请参阅Class ProcessManager的Java API [参考](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)。

1. 检查工作流实例的状态。 如果状态不是2(COMPLETE)或4(TERMINATED)，则首先调用以下方法终止实例：

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. 通过调用以下方法清除工作流实例：

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   如果 `purgeProcessInstance` 配置了此方法，则从AEM Forms服务器数据库和GDS中完全删除指定调用ID的所有数据。

### 处理孤立任务 {#orphan}

孤立任务是指其包含进程已启动但尚未提交的任务。 在这种情况下， `process_instance_id` 为 **0** （零）。 因此，您无法使用进程实例ID跟踪为孤立任务存储的用户数据。 但是，您可以使用孤立任务的任务ID跟踪该任务。 您可以从表中为用户标识任务ID, `tb_task` 如识别工作流发起者或参 [加者已知时的进程实例ID中所述](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)。

获得任务ID后，请执行以下操作，以从GDS和数据库中清除具有孤立任务的关联文件和数据。

1. 对AEM Forms服务器数据库执行以下命令，以检索所标识任务ID的ID。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   查询返回ID列表。 对于结果中返回 `fd_id`的每个ID()，创建一个会话ID字符串列表，如下所示：

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. 根据GDS是指向文件系统还是数据库，执行以下步骤之一：

   1. **文件系统中的GDS**

      在GDS文件系统中：

      1. 搜索具有以下会话ID字符串的文件作为其扩展名：
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`
      具有这些扩展名的文件是标记文件。 这些文件名采用以下格式存储：

      `<file_name_guid>.session<session_id_string>`

      1. 从文件系统中删除文件名与其相同的所有标记 `<file_name_guid>` 文件和其他文件。
   1. **数据库中的GDS**

      对每个会话ID执行以下命令：

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 执行以下命令以从AEM Forms服务器数据库中删除任务ID的数据：

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

