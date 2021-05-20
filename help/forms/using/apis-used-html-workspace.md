---
title: 在AEM Forms工作区中使用的API
seo-title: 在AEM Forms工作区中使用的API
description: 公共Java和JavaScript API以及LiveCycleAEM Forms工作区的方法，已公开以进行自定义和自动化。
seo-description: 公共Java和JavaScript API以及LiveCycleAEM Forms工作区的方法，已公开以进行自定义和自动化。
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
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
   <td><strong>API 名称</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>搜索组。 如果未指定任何内容，则返回所有组的列表，否则返回具有指定名称的组。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>搜索用户和组。 如果未指定任何内容，则返回所有用户和组的列表，否则返回具有指定名称的用户和组。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>在通过DocumentSubmitServlet提交表单之前，会调用该函数。 它会在会话变量（以及到期时间）中设置任务ID，该变量在实际提交期间进行检索。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它提交与任务关联的文档对象（并依次提交流程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它会获取服务器上存在的所有根类别。</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>它为某个类别提取所有直接子项。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它会获取所有类别下服务器上存在的所有起点。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>这会调用起始点并创建与起始点对应的新任务</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllPolabeTasks</td>
   <td>它会获取为登录用户创建、转发或查看、保存、分配、分配和保存的所有任务。</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>它会获取特定任务。</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>render</td>
   <td>它会渲染任务并返回渲染表单所需的信息，如表单url、表单类型、数据url（如果需要）等。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>它使用结果密钥返回TaskManager提交API的结果。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>它使用TaskManager的提交API提交与任务关联的表单数据（作为字符串传递）。 它用于不调用TaskManager提交API的Flex表单。</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>ProcessManagementTaskService</td>
   <td>保存</td>
   <td>它会在服务器上保存任务。</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>它按照流程设计完成任务，并传递到下一步。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>它会返回可使用附件的附件的URL。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllPolaceAttachments</td>
   <td>它会为任务提取所有附件和注释。</td>
  </tr>
  <tr>
   <td>共享</td>
   <td>ProcessManagementTaskService</td>
   <td>共享</td>
   <td>它与另一个用户共享任务。 另一用户可以声明该任务并成为该任务的所有者。</td>
  </tr>
  <tr>
   <td>转发</td>
   <td>ProcessManagementTaskService</td>
   <td>转发</td>
   <td>它会将任务转发给其他用户。</td>
  </tr>
  <tr>
   <td>咨询</td>
   <td>ProcessManagementTaskService</td>
   <td>咨询</td>
   <td>它会咨询其他用户的任务。</td>
  </tr>
  <tr>
   <td>索赔</td>
   <td>ProcessManagementTaskService</td>
   <td>索赔</td>
   <td>它声明共享队列中可用的任务。</td>
  </tr>
  <tr>
   <td>解锁</td>
   <td>ProcessManagementTaskService</td>
   <td>解锁</td>
   <td>它会解锁任务。</td>
  </tr>
  <tr>
   <td>锁</td>
   <td>ProcessManagementTaskService</td>
   <td>锁</td>
   <td>它会锁定任务，如果共享，则其他用户无法声明该任务。</td>
  </tr>
  <tr>
   <td>拒绝</td>
   <td>ProcessManagementTaskService</td>
   <td>拒绝</td>
   <td>它会将任务返回给任务的先前所有者。</td>
  </tr>
  <tr>
   <td>放弃</td>
   <td>ProcessManagementTaskService</td>
   <td>放弃</td>
   <td>它会删除任务。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>它设置任务的可见性。 如果可见性设置为false，则以后用户将看不到任务。</td>
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
   <td>它会返回组中的所有用户。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>它授予指定用户对已登录用户队列的访问权限。 它基本上是与其他用户共享自己的队列。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>它对登录用户的指定用户队列发出访问请求。 如果用户批准了该请求，则会与已登录的用户共享用户的队列。</td>
  </tr>
  <tr>
   <td>getGrandedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrandedUsers</td>
   <td>它将返回有权访问已登录用户队列的所有用户。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它会返回用户可以访问其队列的所有用户。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它会从有权访问已登录用户队列的用户列表中删除用户。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>它会从登录用户可访问其队列的用户列表中删除用户。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>它获得登录用户可访问的所有队列（自有、共享和组队列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>它会从用户的办公室设置中删除。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>它可以省去用户的办公室设置。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它返回所有进程的列表。</td>
  </tr>
  <tr>
   <td>getTerpotedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getTerpotedProcesses</td>
   <td>它会返回已登录用户参与的所有进程名称的列表。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>它会获取进程实例的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>它会获取某个进程的所有进程实例。</td>
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
   <td>它会返回所有搜索模板的列表。</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>返回搜索模板的内容。</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>它会搜索并返回满足搜索模板所有条件的所有任务。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>它获取任务的所有分配。 例如： — 如果用户转发任务或与其他用户协商任务，则它是任务的分配。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>它会删除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如果必要的话，它会重新提出主张。 验证用户。 设置服务器/客户端信息的会话参数。 返回用户信息和轮询间隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>它返回已登录管理器的直接报告的所有任务。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>它返回登录管理器的指定直接报告的任务。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它会将直接报告的任务转发给其他用户。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它会将直接报告的任务返回给前一个用户。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>它为用户获取工作区属性。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>删除</td>
   <td>它会删除用户的工作区属性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>它会返回用户的所有工作区属性。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>它会为用户设置工作区属性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它获取登录用户的用户图像URL。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它获取指定用户的图像URL。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>它会在服务器上上传任务的注释。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也直接从html模板调用）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>它会在服务器上上传任务的附件。</td>
  </tr>
  <tr>
   <td>getImageURL（也直接从html模板调用）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它得到一个过程的图像。</td>
  </tr>
 </tbody>
</table>
