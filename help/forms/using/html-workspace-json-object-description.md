---
title: AEM Forms工作区JSON对象描述
seo-title: AEM Forms工作区JSON对象描述
description: 有关LiveCycleAEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念信息。
seo-description: 有关LiveCycleAEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念信息。
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 4%

---

# AEM Forms工作区JSON对象描述{#aem-forms-workspace-json-object-description}

AEM Forms工作区中使用的JSON对象如下所述。

1. 类别

   工作区的开始流程选项卡中存在类别。 这些类别用于对起点进行分类。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>类别名称</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>类别ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>F</td>
   <td>类别描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>包含父类别<br type="_moz" />的oid </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>包含类别中存在的所有起点的列表</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>包含类别<br type="_moz" />的直接子类别列表 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有“起点”和“收藏夹”都是在客户端定义的类别。 收藏夹类别包含用户标记为收藏的所有起点。 所有起点类别包含所有起点。

1. 起点

   调用时，起点用于从工作区启动进程。

   | **属性** | **仅限客户端** | **评论** |
   |---|---|---|
   | categoryId | F | 它包含起点所属类别的ID。 |
   | 描述 | F | 它包含起点的描述。 |
   | name | F | 它包含起点的名称。 |
   | serializedImageTicket | F | 它包含与起始点对应的图像票证。 此图像票证用于起始点的imageUrl字段，以从服务器获取起始点的图像。 |
   | serviceName | F | 它包含起点的服务名称。 |
   | startpointId | F | 它包含起始点的ID。 |
   | isFavorite | T | 表示起点是否为收藏。 如果起点是收藏，则为True；否则为False。 |
   | isDefaultImage | T | 指示是否指定了处理映像。 如果没有与进程else关联的图像，则为true。 |
   | 任务 | T | 它包含在调用起始点时创建的任务。 |
   | imageUrl | T | 它包含与起始点对应的图像的URL。 |

1. 任务

   任务被分配给用户/组，并包括可填充数据的用户界面(表单或指南（已弃用）)。 为用户分配任务后，他们将获得填写和提交的表单或指南。

<table>
 <tbody>
  <tr>
   <td>属性<br /> </td>
   <td>仅客户端<br /> </td>
   <td>评论<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>任务类为“LC8”，任务为lc8任务，而任务为“标准”。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>任务完成时包含时间戳。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可咨询任务的组的ID。 在过程设计期间设置。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>它包含创建任务时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>该ID包含创建任务的用户ID。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>它包含有关当前任务分配的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>deadline<br /> </td>
   <td>F</td>
   <td>它包含任务达到其截止时间的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>描述<br /> </td>
   <td>F</td>
   <td>它包含任务的描述。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>它包含任务的显示名称。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>它包含可将任务转发到的组的ID。 在过程设计期间设置。<br /> </td>
  </tr>
  <tr>
   <td>说明<br /> </td>
   <td>F</td>
   <td>它包含任务的说明。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>如果任务已锁定，则为True。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必须打开任务表单才能完成任务，则为true。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果为true，则在打开任务时，表单将首次显示完整屏幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果为true，则必须选择路由以完成任务。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>如果为true，则会显示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果为true，则从起始点创建任务。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>如果任务在工作区中可见，则为True。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>下次提醒的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>优先级<br /> </td>
   <td>F</td>
   <td>它包含任务的优先级。<br /> 1 =最高优先级<br /> 2 =高优先级<br /> 3 =正常优先级<br /> 4 =低优先级<br /> 5 =最低优先级<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>任务所属的进程实例的ID。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>任务的进程实例的状态。<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>它包含任务的提醒计数。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>它包含与任务关联的路由列表。 用户可以通过从路由列表中选择路由中的任意一条来完成任务。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含任务完成时所选路由的名称。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含与任务对应的图像票证。 此图像票证用于任务的imageUrl字段，用于从服务器获取任务的图像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>它包含任务的服务名称。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>它包含任务服务的标题。<br /> </td>
  </tr>
  <tr>
   <td>状态<br /> </td>
   <td>F</td>
   <td>1 =已创建（任务从起始点创建。）<br /> 2 =已创建并保存（任务从起始点创建并保存。）<br /> 3 =已分配（进程启动后，会将任务分配给用户。）<br /> 4 =已分配并保存（任务已分配并保存。）<br /> 100 =已完成（任务已完成。）<br /> 101 =无效（任务已到期。）<br /> 102 =终止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>它包含在流程设计期间的任务集的名称。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>它包含任务摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>它是任务的访问控制列表。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>任务的ID。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>上次更新任务时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>它包含任务的表单URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任务表单类型。 使用此字段，任务在客户端上以pdf格式呈现，如swf表单等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果为true，则在工作区中可看到路由操作。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>如果为true，则在工作区中会显示诸如转发、查阅、共享等操作。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>如果为true，则表单可脱机。 这仅适用于pdf表单。<br /> </td>
  </tr>
  <tr>
   <td>支持Save<br /> </td>
   <td>T</td>
   <td>如果为true，则用户可以保存任务。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此对象包含用于在pdf表单不包含提交按钮时通过阅读器提交pdf表单的选项。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>指示是否指定了处理映像。 如果没有与进程else关联的图像，则为true。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含任务详细信息历史记录选项卡中使用的任务列表。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>如果已登录的用户是任务的所有者，则为True。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>它包含可对任务执行的所有操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>它包含可用于任务的所有路由操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>它包含转发、共享和查询等命令（如果可用于任务）。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含锁定、解锁、放弃、返回、声明等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>它包含有关任务的进程实例的信息。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含进程变量对象数组（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>它包含任务进程实例的挂起任务列表。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是对象数组。 每个对象都包含有关路由及其相应确认消息的详细信息（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>它是任务形式数据的url。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>这是第三方应用程序表单的配置。<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>如果提交了任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>T</td>
   <td>任务的附件列表。<br /> </td>
  </tr>
  <tr>
   <td>个指定任务<br /> </td>
   <td>T</td>
   <td>任务的分配列表。<br /> </td>
  </tr>
 </tbody>
</table>

1. 筛选器

   过滤器基本上是用户或组的队列。 将任务分配给用户/组后，该任务会添加到相应的队列中。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>如果队列是已登录用户的默认队列，则为true；否则为false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>队列所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>队列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型</td>
   <td>F</td>
   <td>它包含队列的类型。<br /> 0 — 用户队列。<br /> 1. 共享队列。<br /> 2.组队列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查询</td>
   <td>T</td>
   <td>此变量包含与过滤器关联的查询。 此查询用于从完成的任务列表中搜索任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务</td>
   <td>T</td>
   <td>它包含属于某个过滤器的所有任务的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 不在办公室

   您可以管理您的离职计划，并控制在您缺勤时分配给您的任务流。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong><br type="_moz" /> </td>
   <td><strong>仅限客户端</strong><br type="_moz" /> </td>
   <td><strong>评论</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含用户不在办公室的计划的数组对象。 在每个计划对象中， startDate字段包含计划的开始日期，dendDate字段包含计划的结束日期。 如果计划中的endDate为null，则意味着用户尚未计划离职计划的结束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则没有主要指定项，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含被用户指定为主要指定的用户的详细信息。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDisigns<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含特定于进程的“不在办公室”指定对象的数组。 在每个特定于进程的指定对象中，processName包含进程的名称；如果没有为相应进程分配用户，则isNotDesignated为true；如果没有为相应进程分配用户的详细信息，则userDesignated为null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>进程<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用户可用的所有进程的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初获取的用户的初始不在办公室设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含已修改的“不在办公室”设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含登录用户在日期之前搜索的用户列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程实例

   通过工作区或工作台调用进程时，会创建进程实例。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>F</td>
   <td>进程实例的描述<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>发起者</td>
   <td>F</td>
   <td>进程实例的启动器名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>进程实例的启动器ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>进程完成时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>进程实例的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =已启动<br /> 1 =运行<br /> 2 =完成<br /> 3 =完成<br /> 4 =终止<br /> 5 =终止<br /> 6 =暂停<br /> 7 =暂停<br /> 8 =取消暂停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>进程启动时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>进程变量对象数组。 每个进程变量对象都包含进程变量名称、进程变量值和进程变量类型的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务列表<br type="_moz" /> </td>
   <td>T</td>
   <td>此进程实例生成的任务。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程名称

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的主版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的次版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的标题。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>此进程的进程实例列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务分配对象

   任务分配对象包含有关任务分配的信息。 以下是任务分配的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>创建此任务分配时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初始分配<br /> 1 =转发（任务已转发给任务的当前所有者。）<br /> 2 =已返回（任务的先前所有者已将任务返回给当前任务所有者。）<br /> 3 =已声明（任务的当前所有者已声明任务。）<br /> 4 =呈报（呈报后已将任务分配给当前任务所有者。）<br /> 5 =已分配管理员（管理员已将任务分配给当前任务所有者。）<br /> 6 =已咨询（已咨询任务的当前所有者。）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新任务分配的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>任务当前所有者的队列的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>任务的当前所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>任务当前所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务ACL对象

   任务ACL对象包含有关权限（如转发、共享、查阅等）的信息。 任务的一部分。 以下是任务ACL的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可以将附件添加到任务中。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可向任务添加注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可声明任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可以查阅任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可以转发任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可以共享任务。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务附件

   可以将附件添加到任务中。 附件可以是附件和注释类型。 以下是附件对象的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>创建附件时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的用户ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>添加附件的用户的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的说明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>上次修改附件时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则注释为扩展（长）注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>权限<br type="_moz" /> </td>
   <td>F</td>
   <td>与附件关联的权限。 allowRead字段用于读取权限，allowWrite用于写入权限，allowDelete用于删除权限。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>大小<br type="_moz" /> </td>
   <td>F</td>
   <td>附件的大小（以字节为单位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>添加了附件的任务的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型<br type="_moz" /> </td>
   <td>F</td>
   <td>类型是文件的附件，类型是注释的注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含根据用户UI设置创建附件的日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>带格式的附件描述。 用于在AEM Forms工作区中显示附件描述中存在的特殊字符。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>带格式的附件名称。 用于在AEM Forms工作区中显示附件名称中存在的特殊字符。 仅供注释使用。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 用户

   以下是用户对象的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>地址<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的通用名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>描述<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的描述。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>用户组的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的显示名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的电子邮件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的名字。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的组织名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的邮政地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电话<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的联系电话。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电话号码<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的联系电话。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>登录用户的id。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
