---
title: AEM Forms工作区中使用的API
seo-title: APIs used in AEM Forms workspace
description: 公共Java和JavaScript API以及LiveCycleAEM Forms工作区的方法，公开用于自定义和自动化。
seo-description: Public Java and JavaScript APIs and methods of LiveCycle AEM Forms workspace, exposed for customization and automation.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# AEM Forms工作区中使用的API {#apis-used-in-aem-forms-workspace}

AEM Forms工作区中使用以下API。

<table>
 <tbody>
  <tr>
   <td><strong>JavaScript方法</strong></td>
   <td><strong>服务名称</strong></td>
   <td><strong>API 名称</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>进程管理用户代理服务</td>
   <td>getGroups</td>
   <td>搜索组。 如果未指定任何内容，则返回所有组的列表，否则返回具有指定名称的组。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>进程管理用户代理服务</td>
   <td>getUsersAndGroups</td>
   <td>搜索用户和组。 如果未指定任何内容，则返回所有用户和组的列表，否则返回具有指定名称的用户和组。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>在通过DocumentSubmitServlet提交表单之前调用它。 它会在会话变量中设置任务ID（以及过期时间），该变量在实际提交期间进行检索。</td>
  </tr>
  <tr>
   <td>submittask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>提交</td>
   <td>它会提交与任务关联的文档对象（并依次提交流程）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>它会获取服务器上存在的所有根类别。</td>
  </tr>
  <tr>
   <td>getDirectChildCategory</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>它会获取某个类别的所有直接子项。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>它会获取服务器上所有类别下的所有起点。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>这将调用一个起点并创建一个对应于起点的新任务</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>它会获取为登录用户创建和转发或咨询、保存、分配、分配和保存的所有任务。</td>
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
   <td>渲染</td>
   <td>它渲染任务并返回渲染表单所需的信息，如表单URL、表单类型、数据URL（如果需要）等。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>它会使用结果密钥返回TaskManager的提交API的结果。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>它使用TaskManager的提交API提交与任务关联的表单数据（以字符串形式传递）。 它用于不调用TaskManager的提交API的Flex表单。</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>ProcessManagementTaskService</td>
   <td>保存</td>
   <td>它将任务保存在服务器上。</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>它完成一项任务，并根据流程设计将任务传递到下一步。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>它会返回可用附件的附件URL。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>它会获取任务的所有附件和注释。</td>
  </tr>
  <tr>
   <td>共享</td>
   <td>ProcessManagementTaskService</td>
   <td>共享</td>
   <td>它与其他用户共享任务。 另一个用户可以声明该任务并成为该任务的所有者。</td>
  </tr>
  <tr>
   <td>转发</td>
   <td>ProcessManagementTaskService</td>
   <td>转发</td>
   <td>它将任务转发给另一个用户。</td>
  </tr>
  <tr>
   <td>咨询</td>
   <td>ProcessManagementTaskService</td>
   <td>咨询</td>
   <td>它会咨询另一个用户的任务。</td>
  </tr>
  <tr>
   <td>声明</td>
   <td>ProcessManagementTaskService</td>
   <td>声明</td>
   <td>它声明任务在共享队列中可用。</td>
  </tr>
  <tr>
   <td>解锁</td>
   <td>ProcessManagementTaskService</td>
   <td>解锁</td>
   <td>它解锁一项任务。</td>
  </tr>
  <tr>
   <td>锁定</td>
   <td>ProcessManagementTaskService</td>
   <td>锁定</td>
   <td>它锁定一个任务，如果共享，则另一个用户不能声明该任务。</td>
  </tr>
  <tr>
   <td>拒绝</td>
   <td>ProcessManagementTaskService</td>
   <td>拒绝</td>
   <td>它将任务返回到任务的先前所有者。</td>
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
   <td>它设置任务的可见性。 如果可见性设置为false ，则以后任务对用户不可见。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>进程管理用户代理服务</td>
   <td>getUsers</td>
   <td>用于搜索用户。 如果未指定名称，则返回所有用户，否则返回具有指定名称的用户。</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>进程管理用户代理服务</td>
   <td>getUsersInGroupByName</td>
   <td>它会返回一个组中的所有用户。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>它向指定用户授予登录用户队列的访问权限。 它基本上是与其他用户共享自己的队列。</td>
  </tr>
  <tr>
   <td>requestQueueCess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueCess</td>
   <td>它向登录用户发出访问指定用户队列的请求。 如果用户批准该请求，则用户的队列将与已登录的用户共享。</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>它会返回对登录用户队列具有访问权限的所有用户。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>它会返回其队列可供用户访问的所有用户。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>它会从有权访问登录用户队列的用户列表中删除用户。</td>
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
   <td>它获取登录用户可访问的所有队列（自己的、共享和组队列）。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>它获取用户的办公外设置。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>它保存用户的办公外设置。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>它会返回所有进程的列表。</td>
  </tr>
  <tr>
   <td>getActividedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getActividedProcesses</td>
   <td>它会返回由登录用户参与的所有进程名称的列表。</td>
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
   <td>它会获取进程的所有进程实例。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>它获取进程实例的待处理任务。</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>它获取一个进程实例的所有任务。</td>
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
   <td>它会返回搜索模板的内容。</td>
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
   <td>它获取一个任务的所有工作分配。 例如， ： — 如果用户与其他用户转发或咨询任务，则它是任务的指派。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>任务管理器服务</td>
   <td>deleteAttachment</td>
   <td>它删除附件。</td>
  </tr>
  <tr>
   <td>初始化</td>
   <td>ProcessManagementClientSessionService</td>
   <td>初始化</td>
   <td>如有必要，它会重申断言。 对用户进行身份验证。 设置服务器/客户端信息的会话参数。 返回用户信息和轮询间隔。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>它会返回登录经理的直接下属的所有任务。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>返回登录管理器的指定直接下属的任务。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>它将直接报告的任务转发给另一个用户。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>它将直接下属的任务返回给前一个用户。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>工作区属性服务</td>
   <td>getProperty</td>
   <td>它获取用户的Workspace属性。</td>
  </tr>
  <tr>
   <td>removeproperty</td>
   <td>工作区属性服务</td>
   <td>删除</td>
   <td>它删除用户的Workspace属性。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>工作区属性服务</td>
   <td>getPropertiesAsMap</td>
   <td>它会返回用户的所有Workspace属性。</td>
  </tr>
  <tr>
   <td>setproperty</td>
   <td>工作区属性服务</td>
   <td>setproperty</td>
   <td>它为用户设置工作区属性。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>它获取登录用户的图像URL。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>它获取指定用户的图像url。</td>
  </tr>
  <tr>
   <td>uploadnote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadnote</td>
   <td>它在服务器上为任务上传注释。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（也可以直接从html模板调用）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>上传附件</td>
   <td>它将为任务在服务器上上传附件。</td>
  </tr>
  <tr>
   <td>getImageURL（也可以直接从html模板调用）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>它获取进程的图像。</td>
  </tr>
 </tbody>
</table>
