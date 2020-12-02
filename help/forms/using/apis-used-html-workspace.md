---
title: AEM Forms工作区中使用的API
seo-title: AEM Forms工作区中使用的API
description: 公开的Java和JavaScript API和LiveCycleAEM Forms工作区的方法，用于自定义和自动化。
seo-description: 公开的Java和JavaScript API和LiveCycleAEM Forms工作区的方法，用于自定义和自动化。
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---


# AEM Forms工作区{#apis-used-in-aem-forms-workspace}中使用的API

以下API在AEM Forms工作区中使用。

<table>
 <tbody>
  <tr>
   <td><strong>Javascript方法</strong></td>
   <td><strong>服务名称</strong></td>
   <td><strong>API名称</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>搜索组。 如果未指定，则返回所有组的列表，否则返回具有指定名称的组。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>搜索用户和组。 它返回所有用户和用户组的列表符（如果未指定），否则返回具有指定名称的用户和用户组。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>在通过DocumentSubmitServlet提交表单之前，会调用它。 它在实际提交期间检索的会话变量（以及到期时间）中设置任务ID。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它提交与文档关联的任务对象（然后依次提交进程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它获取服务器上存在的所有根类别。</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>它为类别获取所有直接子项。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它获取服务器上所有类别下的所有起始点。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>这将调用起始点并创建与起始点对应的新任务</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllCopacleTasks</td>
   <td>它会获取为登录用户创建、转发或咨询、保存、分配、分配和保存的所有任务。</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>它获取特定任务。</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>渲染</td>
   <td>它会呈现一个任务，并根据需要返回呈现表单所需的信息，如表单url、表单类型、数据url等。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>它使用结果密钥返回TaskManager的提交API的结果。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>它使用TaskManager的提交API提交与任务关联的表单数据（作为字符串传递）。 它用于不调用TaskManager的提交API的flex表单。</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>ProcessManagementTaskService</td>
   <td>保存</td>
   <td>它在服务器上保存任务。</td>
  </tr>
  <tr>
   <td>完整</td>
   <td>ProcessManagementTaskService</td>
   <td>完整</td>
   <td>它完成任务，并按照流程设计将任务传递到下一步。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>它返回附件可用的URL。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllCopactedAttachments</td>
   <td>它获取任务的所有附件和备注。</td>
  </tr>
  <tr>
   <td>股份</td>
   <td>ProcessManagementTaskService</td>
   <td>股份</td>
   <td>它与其他用户共享任务。 另一个用户可以声明任务并成为任务的所有者。</td>
  </tr>
  <tr>
   <td>转发</td>
   <td>ProcessManagementTaskService</td>
   <td>转发</td>
   <td>它将任务转发给其他用户。</td>
  </tr>
  <tr>
   <td>咨询</td>
   <td>ProcessManagementTaskService</td>
   <td>咨询</td>
   <td>它咨询另一个用户的任务。</td>
  </tr>
  <tr>
   <td>索赔</td>
   <td>ProcessManagementTaskService</td>
   <td>索赔</td>
   <td>它声明共享队列中有可用的任务。</td>
  </tr>
  <tr>
   <td>解锁</td>
   <td>ProcessManagementTaskService</td>
   <td>解锁</td>
   <td>它解锁任务。</td>
  </tr>
  <tr>
   <td>锁</td>
   <td>ProcessManagementTaskService</td>
   <td>锁</td>
   <td>它锁定任务，如果共享，则其他用户无法声明任务。</td>
  </tr>
  <tr>
   <td>拒绝</td>
   <td>ProcessManagementTaskService</td>
   <td>拒绝</td>
   <td>它将任务返回给任务的前所有者。</td>
  </tr>
  <tr>
   <td>放弃</td>
   <td>ProcessManagementTaskService</td>
   <td>放弃</td>
   <td>它删除任务。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>它设置任务的可见性。 如果可见性设置为false，则用户随后将看不到任务。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>用于搜索用户。 如果未指定名称，则返回所有用户；否则返回具有指定名称的用户。</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>它返回组中的所有用户。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>它向指定用户授予对已登录用户队列的访问权限。 它基本上与另一个用户共享自己的队列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它对登录用户的指定用户的队列发出访问请求。 如果用户批准了该请求，则用户的队列将与登录用户共享。</td>
  </tr>
  <tr>
   <td>getGragnedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGragnedUsers</td>
   <td>它返回有权访问已登录用户队列的所有用户。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它返回用户可以访问其队列的所有用户。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它将用户从有权访问已登录用户队列的用户列表中删除。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>它从登录用户可访问其队列的用户列表中删除用户。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>它获取登录用户可以访问的所有队列（自己的、共享的和组队列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>它会从用户的办公室设置中移出。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>它省去了用户的办公室设置。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它返回所有进程的列表。</td>
  </tr>
  <tr>
   <td>getEptortedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getEptortedProcesses</td>
   <td>它返回已登录用户参与的所有进程名称的列表。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>它获取进程实例的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>它获取某个进程的所有进程实例。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>它获取进程实例的挂起任务。</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>它获取进程实例的所有任务。</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>它返回所有搜索模板的列表。</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>它返回搜索模板的内容。</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>它搜索并返回满足搜索模板所有条件的所有任务。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>它获取任务的所有任务。 例如：-如果用户转发或咨询任务给其他用户，则它是任务的分配。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>它删除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如果必要，它会重新声明。 验证用户。 设置服务器／客户端信息的会话参数。 返回用户信息和轮询间隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>它返回已登录管理器的所有任务直接报告。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>它返回已登录管理器的指定直接报告的任务。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它将直接报告的任务转发给其他用户。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它将直接报告的任务返回给前一个用户。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>它为用户获取一个Workspace属性。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>删除</td>
   <td>它删除用户的Workspace属性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>它返回用户的所有Workspace属性。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>它为用户设置Workspace属性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它获取登录用户的用户图像url。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它获取指定用户的用户图像url。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>它在服务器上上传注释以供任务。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也直接从html模板调用）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>它上传服务器上的附件以供任务。</td>
  </tr>
  <tr>
   <td>getImageURL（也直接从html模板调用）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它获得一个过程的图像。</td>
  </tr>
 </tbody>
</table>
