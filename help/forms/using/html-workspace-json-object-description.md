---
title: AEM Forms工作区JSON对象说明
seo-title: AEM Forms工作区JSON对象说明
description: 有关LiveCycle AEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念性信息。
seo-description: 有关LiveCycle AEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念性信息。
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms工作区JSON对象说明 {#aem-forms-workspace-json-object-description}

在AEM Forms工作区中使用的JSON对象如下所述。

1. 类别

   类别显示在工作区的开始进程选项卡中。 这些类别用于对起点进行分类。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>名称</td>
   <td>F</td>
   <td>类别名称</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>类别ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>类别说明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>包含父类别的oid<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>包含列表类别中存在的所有起始点</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>包含列表类别的直接子类别<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>所有起点和收藏夹都是在客户端定义的类别。 “收藏夹”类别包含用户标记为“收藏夹”的所有起点。 所有起点类别包含所有起点。

1. 起点

   起点用于在调用时从工作区开始进程。

   | **属性** | **仅限客户端** | **评论** |
   |---|---|---|
   | categoryId | F | 它包含起始点所属类别的id。 |
   | 描述 | F | 它包含起点的描述。 |
   | 名称 | F | 它包含起始点的名称。 |
   | serializedImageTicket | F | 它包含与起始点对应的图像票证。 此图像票证用于从服务器获取起始点的图像。 |
   | serviceName | F | 它包含起始点服务的名称。 |
   | startpointId | F | 它包含起始点的id。 |
   | isFavorite | T | 指示起始点是否为收藏点。 如果起始点是最喜欢的，则返回true；否则返回false。 |
   | isDefaultImage | T | 指示是否有为进程指定的图像。 如果没有与进程else false关联的图像，则返回true。 |
   | 任务 | T | 它包含调用起始点时创建的任务。 |
   | imageUrl | T | 它包含与起始点对应的图像的url。 |

1. 任务

   任务分配给用户／用户组，并包含可填充数据的用户界面(表单或指南（已弃用）)。 为用户分配任务后，会向他们提供表单或指南以完成和提交。

<table>
 <tbody>
  <tr>
   <td>属性<br /> </td>
   <td>仅限客户端<br /> </td>
   <td>评论<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>当任务为lc8任务时，任务类为“LC8”，否则为“标准”。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>它包含任务完成时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>它包含可咨询任务的组的ID。 在设计过程中设置。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>它包含创建任务时的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>它包含创建任务的用户的id。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>它包含有关当前任务分配的详细信息。<br /> </td>
  </tr>
  <tr>
   <td>截止期限<br /> </td>
   <td>F</td>
   <td>它包含任务到期的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>说明<br /> </td>
   <td>F</td>
   <td>它包含对任务的描述。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>它包含任务的显示名称。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>它包含可转发任务的组的ID。 在设计过程中设置。<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>它包含任务的说明。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>如果任务已锁定，则为true。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>如果必须打开任务表单才能完成任务，则为true。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果为true，则打开任务时，表单将首次显示完整屏幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果为true，则必须选择路由才能完成任务。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>如果属于，则显示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果为true，则从任务点创建开始。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>如果任务在工作区中可见，则为true。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>下次提醒的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>优先级<br /> </td>
   <td>F</td>
   <td>它包含任务优先级。<br /> 1 =最高优先级<br /> 2 =高优先级<br /> 3 =正常优先级<br /> 4 =低优先级<br /> 5 =最低优先级<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>其任务所属的进程实例的ID。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>任务进程实例的状态。<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>它包含任务的提醒计数。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>它包含与列表相关的路由任务。 用户可以通过从路由任务中选择任一路由来完成列表。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含完成任务时所选路由的名称。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含与任务相对应的图像票证。 此图像票证用于任务的imageUrl字段，以从服务器获取要任务的图像。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>它包含任务服务的名称。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>它包含任务服务的标题。<br /> </td>
  </tr>
  <tr>
   <td>状态<br /> </td>
   <td>F</td>
   <td>1 =创建任务(从开始点创建。)<br /> 2 =创建并保存(任务是从开始点创建并保存的。)<br /> 3 =已分配(在进程启动后，任务将分配给用户。)<br /> 4 =已分配并保存(已分配并保存任务。)<br /> 100 =已完成(任务已完成。)<br /> 101 =死期(任务已到期)。<br /> 102 =终止<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>它包含在流程设计过程中任务集的名称。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>它包含任务摘要url。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>这是访问控制的列表,任务。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>任务的ID。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>上次更新任务的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>它包含任务的表单URL。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任务表单类型。 使用此字段，任务在客户端上呈现为pdf for、swf表单等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果为true，则路由操作在工作区中可见。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>如果为true，则向前、查阅、共享等操作在工作区中可见。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>如果为true，则表单可脱机。 这仅适用于pdf表单。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>如果为true，则用户可以保存任务。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>此对象包含用于通过Reader提交PDF表单的选项，以防PDF表单不包含提交按钮。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>指示是否有为进程指定的图像。 如果没有与进程else false关联的图像，则返回true。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含列表,任务在任务详细信息的历史记录选项卡中使用。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>如果已登录用户是任务的所有者，则为true。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>它包含可对任务执行的操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>它包含可用于任务的所有路由操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>它包含向前、共享和查阅等命令(如果任务可用)。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含锁定、解锁、放弃、返回、声明等可用命令。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>它包含有关任务进程实例的信息。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>它包含进程变量的对象数组（如果存在）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>它包含任务进程实例的待定任务的列表。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是对象的数组。 每个对象都包含有关路由的详细信息，如果存在，还包含相应的确认消息。<br /> </td>
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
   <td>如果提交了任务，则返回true。<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>列表任务。<br /> </td>
  </tr>
  <tr>
   <td>个指定任务<br /> </td>
   <td>T</td>
   <td>列表任务的分配。<br /> </td>
  </tr>
 </tbody>
</table>

1. 筛选器

   过滤器基本上是用户或用户组的队列。 将任务分配给用户／用户组后，任务会添加到相应的队列中。

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
   <td>如果队列是登录用户的默认队列，则为true；否则为false。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名称<br type="_moz" /> </td>
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
   <td>它包含队列的类型。<br /> 0 —— 用户队列。<br /> 1. 共享队列。<br /> 2. 组队列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查询</td>
   <td>T</td>
   <td>它包含与过滤器关联的查询。 此查询用于从完整任务列表中搜索任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务</td>
   <td>T</td>
   <td>它包含属于过滤器的所有任务的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 办公室外

   您可以管理离职计划，并控制在您缺席时分配给您的任务流。

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
   <td>它包含用户的办公外计划的数组对象。 在每个计划对象中，startDate字段包含计划的开始日期，dendDate字段包含计划的结束日期。 如果endDate在计划中为null，则表示用户尚未预定离职计划的结束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则没有主要指定项，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含用户被分配为主要指定用户的详细信息。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDistans<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含特定于进程的指定办公室外对象的数组。 在每个进程特定的指定对象中，processName包含进程的名称；如果没有为相应进程分配用户，则isNotDesignated为true；如果没有为相应进程分配用户的其他详细信息，则userDesignated为null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用户可用的所有进程的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初获取的用户的初始离职设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含修改的离职设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用户列表，用户在日期之前会按登录用户进行搜索。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程实例

   当通过工作区或工作台调用进程时，将创建进程实例。

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>仅限客户端</strong></td>
   <td><strong>评论</strong></td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>进程实例说明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>启动器</td>
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
   <td>0 =启动<br /> 1 =运行<br /> 2 =完成3 =完成<br /> 4 =终止<br /> 5 =终止<br /> 6 =暂停7 =暂停<br /><br /><br /> 8 =取消暂停<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>进程开始时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>进程变量对象的数组。 每个进程变量对象包含进程变量名、进程变量值和进程变量类型。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务列表<br type="_moz" /> </td>
   <td>T</td>
   <td>由此进程实例生成的任务。<br type="_moz" /> </td>
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
   <td>流程的主要版本。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>进程的次要版本。<br type="_moz" /> </td>
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
   <td>列表此进程的进程实例。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务分配对象

   任务赋值对象包含有关任务赋值的信息。 以下是任务赋值的属性。

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
   <td>0 =初始分配<br /> 1 =转发(任务已转发给当前任务所有者。)<br /> 2 =已退回(任务已由先前的任务所有者返回给当前任务所有者。)<br /> 3 =已申请(任务的当前所有者已申请任务。)<br /> 4 =升级(升级后，任务已分配给当前任务所有者。)<br /> 5 =已分配管理员(管理员已将任务分配给当前任务所有者。)<br /> 6 =咨询了任务(已咨询了任务的当前所有者。)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新任务的此分配时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>当前任务所有者的队列ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>任务的当前所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>当前任务所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务ACL对象

   任务ACL对象包含有关转发、共享、查阅等权限的信息。 任务。 以下是任务ACL的属性。

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
   <td>如果为true，则可将附件添加到任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可向任务添加注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为真，则可声明任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果是真的，可以咨询任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为真，则可转发任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为True，则可以共享任务。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务附件

   附件可添加到任务。 附件的类型可以是附件和附注。 以下是attachment对象的属性。

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
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>附件说明。<br type="_moz" /> </td>
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
   <td>如果为true，则备注为扩展（长）备注。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissions<br type="_moz" /> </td>
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
   <td>向其添加附件的任务的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型<br type="_moz" /> </td>
   <td>F</td>
   <td>“类型”(Type)是文件的附件，“类型”(Type)是注释的注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>它根据用户的UI设置包含附件创建日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化的附件说明。 用于显示AEM Forms工作区中附件说明中的特殊字符。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化的附件名称。 用于显示AEM Forms工作区中附件名称中存在的特殊字符。 这仅用于备注。<br type="_moz" /> </td>
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
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的通用名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的说明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>F</td>
   <td>列表用户组。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>显示用户的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的电子邮件ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOffice<br type="_moz" /> </td>
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
   <td>邮政地址<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的邮政地址。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的联系号码。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的联系号码。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的登录ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
