---
title: 以Forms为中心的OSGi工作流 |处理用户数据
seo-title: 以Forms为中心的OSGi工作流 |处理用户数据
description: 以Forms为中心的OSGi工作流 |处理用户数据
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# 以Forms为中心的OSGi工作流 |处理用户数据 {#forms-centric-workflows-on-osgi-handling-user-data}

以Forms为中心的AEM工作流使您能够自动处理以Forms为中心的真实业务流程。 工作流由一系列步骤组成，这些步骤按关联工作流模型中指定的顺序执行。 每个步骤都执行特定操作，如向用户分配任务或发送电子邮件。 工作流可以与存储库中的资产、用户帐户和服务进行交互。 因此，工作流可以协调涉及任何Experience Manager方面的复杂活动。

可通过以下任意方法触发或启动以表单为中心的工作流：

* 从AEM收件箱提交应用程序
* 从AEM应用程序提交应 [!DNL Forms] 用程序
* 提交自适应表单
* 使用监视的文件夹
* 提交交互式通信或信件

有关以Forms为中心的AEM工作流和功能的更多信息，请参 [阅OSGi上以Forms为中心的工作流](/help/forms/using/aem-forms-workflow.md)。

## 用户数据和数据存储 {#user-data-and-data-stores}

触发工作流时，将自动为工作流实例生成有效负荷。 为每个工作流实例分配一个唯一的实例ID和一个关联的有效负荷ID。 有效负荷包含与工作流实例关联的用户和表单数据的存储库位置。 此外，工作流实例的草稿和历史数据也存储在AEM存储库中。

工作流实例的有效负荷、草稿和历史记录所在的默认存储库位置如下：

>[!NOTE]
>
>在创建工作流或应用程序时，您可以配置不同的位置来存储有效负荷、草稿和历史记录数据。 要确定工作流或应用程序存储数据的位置，请检查工作流。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNLForms]</b></td>
   <td><b>AEM 6.3 [!DNLForms]</b></td>
  </tr>
  <tr>
   <td><strong>工作流 <br /> 实例</strong></td>
   <td>/var/workflow/instances/[server id]/&lt;date&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>有效负荷</strong></td>
   <td>/var/fd/仪表板/payload/[server_id]/[date]/<br /> [payload-id]/</td>
   <td>/etc/fd/仪表板/payload/[server_id]/[date]/<br /> [payload-id]/</td>
  </tr>
  <tr>
   <td><strong>草稿</strong></td>
   <td>/var/fd/仪表板/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[工作项]/</td>
   <td>/etc/fd/仪表板/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[工作项]/</td>
  </tr>
  <tr>
   <td><strong>历史</strong></td>
   <td>/var/fd/仪表板/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
   <td>/etc/fd/仪表板/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td>
  </tr>
 </tbody>
</table>

## 访问和删除用户数据 {#access-and-delete-user-data}

您可以从存储库中的工作流实例访问和删除用户数据。 要实现此目的，您必须知道与用户关联的工作流实例的实例ID。 您可以使用启动工作流实例的用户的用户名或工作流实例的当前被分派人来查找工作流实例的实例ID。

但是，在以下情况下，当识别与启动器关联的工作流时，您无法识别或结果可能不明确：

* **通过监视文件夹触发的工作流**:如果工作流是由监视的文件夹触发的，则无法使用其启动器来标识工作流实例。 在这种情况下，用户信息被编码在所存储的数据中。
* **从发布AEM实例启动的工作流**:从AEM发布实例提交自适应表单、交互通信或字母时，所有工作流实例都使用服务用户创建。 在这些情况下，不会在工作流实例数据中捕获登录用户的用户名。

### 访问用户数据 {#access}

要标识和访问为工作流实例存储的用户数据，请执行以下步骤：

1. 在AEM创作实例上，转 `https://'[server]:[port]'/crx/de` 到工具> **[!UICONTROL 查询]**。

   从 **[!UICONTROL “类型]** ”下 **[!UICONTROL 拉框]** 中选择SQL2。

1. 根据可用信息，执行以下查询之一：

   * 如果工作流启动器已知，请执行以下操作：

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 如果您正在查找其数据的用户是当前工作流被分派人，请执行以下操作：

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   该查询返回指定工作流启动器或当前工作流被分派人的所有工作流实例的位置。

   例如，以下查询从其工作流启动器所在的节点返回 `/var/workflow/instances` 两个工作流实例路 `srose`径。

   ![工作流实例](assets/workflow-instance.png)

1. 转到由查询返回的工作流实例路径。 状态属性显示工作流实例的当前状态。

   ![状态](assets/status.png)

1. 在工作流实例节点中，导航到 `data/payload/`。 该属 `path` 性存储工作流实例的有效负荷的路径。 您可以导航到访问有效负荷中存储的数据的路径。

   ![payload-path](assets/payload-path.png)

1. 导航到工作流实例的草稿和历史记录的位置。

   例如：

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 对步骤2中查询返回的所有工作流实例重复步骤3 - 5。

   >[!NOTE]
   >
   >AEM应 [!DNL Forms] 用程序还在脱机模式下存储数据。 工作流实例的数据可能本地存储在单个设备上，并在应用程序与服务器同步 [!DNL Forms] 时提交到服务器。

### 删除用户数据 {#delete-user-data}

您必须是AEM管理员才能通过执行以下步骤从工作流实例中删除用户数据：

1. 按照访问用户 [数据中的说](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) 明操作，并注意以下事项：

   * 与用户关联的工作流实例的路径
   * 工作流实例的状态
   * 工作流实例的有效负荷路径
   * 工作流实例的草稿和历史记录路径

1. 对处于“正在运行”、“已 **挂起**”或“ **过时**”状态 **的工作流实** 例执行此步骤：

   1. 转到并 `https://'[server]:[port]'/aem/start.html` 使用管理员凭据登录。
   1. 导航到 **[!UICONTROL 工具>工作流>实例]**。
   1. 为用户选择相关的工作流实例，然后点 **[!UICONTROL 按终止]** ，以终止正在运行的实例。

      有关使用工作流实例的详细信息，请参阅管 [理工作流实例](/help/sites-administering/workflows-administering.md)。

1. 转到控 [!DNL CRXDE Lite] 制台，导航到工作流实例的有效负荷路径，然后删除该 `payload` 节点。
1. 导航到工作流实例的草稿路径，然后删除该 `draft` 节点。
1. 导航到工作流实例的历史记录路径，然后删除该 `history` 节点。
1. 导航到工作流实例的工作流实例路径，然后删 `[workflow-instance-ID]` 除工作流的节点。

   >[!NOTE]
   >
   >删除工作流实例节点将删除所有工作流参加者的工作流实例。

1. 对于为用户标识的所有工作流实例，重复步骤2 - 6。
1. 识别并删除来自AEM应用程序工作流参加者 [!DNL Forms] 的外框的脱机草稿和提交数据，以避免任何提交到服务器。

您还可以使用API访问和删除节点和属性。 有关详细信息，请参阅以下文档。

* [如何以编程方式访问AEM JCR](/help/sites-developing/access-jcr.md)
* [删除节点和属性](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API参考](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

