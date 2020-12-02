---
title: AEM Forms工作区JSON对象描述
seo-title: AEM Forms工作区JSON对象描述
description: 有关在LiveCycleAEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念信息。
seo-description: 有关在LiveCycleAEM Forms工作区中用于自定义、扩展、修改和重用的JSON JavaScript对象的概念信息。
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 4%

---


# AEM Forms工作区JSON对象描述{#aem-forms-workspace-json-object-description}

在AEM Forms工作区中使用的JSON对象如下所述。

1. 类别

   类别显示在工作区的“开始”进程选项卡中。 这些类别用于对起始点进行分类。

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
   <td>类别名</td>
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
   <td>包含父类别<br type="_moz" />的oid </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>包含列表类别中存在的所有起点</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>包含类别的直接子类别的列表<br type="_moz" /> </td>
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
   | 名称 | F | 它包含起点的名称。 |
   | serializedImageTicket | F | 它包含与起始点对应的图像票证。 此图像票证用于起始点的imageUrl字段，以从服务器获取起始点的图像。 |
   | serviceName | F | 它包含起始点服务的名称。 |
   | startpointId | F | 它包含起始点的id。 |
   | isFavorite | T | 表示起点是否为收藏点。 如果起始点是最喜爱的，则返回true；如果返回，则返回false。 |
   | isDefaultImage | T | 指示是否有为处理指定的图像。 如果没有与进程关联的图像，则返回True；否则返回False。 |
   | 任务 | T | 它包含调用起始点时创建的任务。 |
   | imageUrl | T | 它包含与起始点对应的图像的url。 |

1. 任务

   任务分配给用户／用户组，并包含一个可以填充数据的用户界面(表单或指南（已弃用）)。 为用户分配任务后，会向他们提供填写和提交的表单或指南。

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
   <td>deadline<br /> </td>
   <td>F</td>
   <td>它包含任务到达其截止日期的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>说明<br /> </td>
   <td>F</td>
   <td>它包含任务的说明。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>它包含任务的显示名称。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>它包含可将任务转发到的组的ID。 在设计过程中设置。<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
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
   <td>如果必须打开任务表单才能完成任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>如果为true，则打开任务时，表单将首次显示完整屏幕。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>如果为true，则必须选择路由以完成任务。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>如果为true，则显示附件。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>如果为true，则从任务点创建开始。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>如果工作区中显示任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>下次提醒的时间戳。<br /> </td>
  </tr>
  <tr>
   <td>优先级<br /> </td>
   <td>F</td>
   <td>它包含任务优先级。<br /> 1 =最高优先级<br /> 2 =高优先<br /> 级3 =正常优先级<br /> 4 =低优先级<br /> 5 =最低优先级<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>其任务是其一部分的进程实例的ID。<br /> </td>
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
   <td>它包含与列表相关的路由任务。 用户可以通过从路由任务中选择任何一条路由来完成列表。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>它包含完成任务时所选路由的名称。<br /> </td>
  </tr>
  <tr>
   <td>seriadedImageTicket<br /> </td>
   <td>F</td>
   <td>它包含与任务对应的图像票证。 此图像票证用于任务的imageUrl字段，以从服务器获取任务映像。<br /> <br /> </td>
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
   <td>1 =已创建(任务是从开始点创建的。)<br /> 2 =创建并保存(任务是从开始点创建并保存的。)<br /> 3 =已分配(进程启动后，任务将分配给用户。)<br /> 4 =已分配并保存(已分配并保存任务。)<br /> 100 =已完成(任务已完成。)<br /> 101 =死期(任务已到期)<br /> 102 =终止<br /> </td>
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
   <td>它是访问控制列表任务。<br /> </td>
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
   <td>它包含任务的表单url。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>它包含任务表单类型。 使用此字段，任务在客户端上呈现为pdf形式、swf表单等。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>如果为true，则在工作区中可以看到路由操作。<br /> </td>
  </tr>
  <tr>
   <td>showACLAactions<br /> </td>
   <td>T</td>
   <td>如果为true，则在工作区中可看到向前、查阅、共享等操作。<br /> </td>
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
   <td>此对象包含用于在pdf表单不包含提交按钮时通过reader提交pdf表单的选项。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>指示是否有为处理指定的图像。 如果没有与进程关联的图像，则为True。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>它包含列表任务，这些任务在详细信息的历史记录选项卡中使用。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>如果登录用户是任务的所有者，则为True。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>它包含可对任务执行的所有操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>它包含任务可用的所有路由操作。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>它包含向前、共享和查询等命令(如果任务可用)。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>它包含诸如锁定、解锁、放弃、返回、声明等可用命令。<br /> </td>
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
   <td>它包含任务进程实例的挂起列表。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>它是对象的数组。 每个对象都包含路由及其相应确认消息的详细信息（如果存在）。<br /> </td>
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
   <td>已提交<br /> </td>
   <td>T</td>
   <td>如果提交了任务，则为True。<br /> </td>
  </tr>
  <tr>
   <td>附件<br /> </td>
   <td>T</td>
   <td>列表的附件。<br /> </td>
  </tr>
  <tr>
   <td>个指定任务<br /> </td>
   <td>T</td>
   <td>列表任务的分配。<br /> </td>
  </tr>
 </tbody>
</table>

1. 筛选器

   过滤器基本上是用户或组的队列。 当任务被分配给用户／组时，任务会添加到相应队列中。

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
   <td>如果队列是登录用户的默认队列，则为True，否则为False。<br type="_moz" /> </td>
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
   <td>它包含队列的类型。<br /> 0 —— 用户队列。<br /> 1. 共享队列。<br /> 2.组队列。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>查询</td>
   <td>T</td>
   <td>它包含与筛选器关联的查询。 此查询用于从完整任务列表中搜索任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务</td>
   <td>T</td>
   <td>它包含属于过滤器的所有任务的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 办公室外

   您可以管理办公室外计划，并控制在您缺席时分配给您的任务流。

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
   <td>它包含用户的办公室外计划的数组对象。 在每个计划对象中，startDate字段包含计划的开始日期，而dendDate字段包含计划的结束日期。 如果endDate在计划中为null，则表示用户尚未计划离职计划的结束日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则没有主要指定项，则为true。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则为True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含被用户指定为主指定用户的详细信息。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDistans<br type="_moz" /> </td>
   <td>F</td>
   <td>它包含特定于流程的指定对象数组。 在每个特定于进程的指定对象中，processName包含进程的名称；如果没有为相应进程分配用户，则isNotDesignated为true；如果没有为相应进程分配用户的其他详细信息，则userDesignated为null。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>进程<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含用户可用的所有进程的列表。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含最初获取的用户的初始办公室外设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含已修改的办公室外设置。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>它包含登录用户搜索到日期的用户的列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 进程实例

   当通过工作区或工作台调用进程时，会创建进程实例。

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
   <td>进程实例的说明<br type="_moz" /> </td>
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
   <td>0 =启动<br /> 1 =运行<br /> 2 =完成<br /> 3 =完成<br /> 4 =终止<br /> 5 =终止<br /> 6 =暂停<br /> 7 =暂停<br /> 8 =取消暂停<br type="_moz" /> </td>
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
   <td>进程变量对象的数组。 每个进程变量对象都包含进程变量名称、进程变量值和进程变量类型。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>任务列表<br type="_moz" /> </td>
   <td>T</td>
   <td>任务由此进程实例生成。<br type="_moz" /> </td>
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
   <td>进程的主要版本。<br type="_moz" /> </td>
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
   <td>此进程的进程实例列表。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务分配对象

   任务赋值对象包含有关任务赋值的信息。 以下是任务分配的属性。

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
   <td>0 =初始分配<br /> 1 =转发(任务已转发给当前任务所有者。)<br /> 2 =已退回(任务已由先前的任务所有者返回给当前任务所有者。)<br /> 3 =已申请(任务的当前所有者已申请任务。)<br /> 4 =升级(任务在升级后已分配给任务的当前所有者。)<br /> 5 =管理员已分配任务(管理员已将任务分配给当前所有者。)<br /> 6 =已咨询任务(已咨询任务的当前所有者。)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>更新任务的此分配时的时间戳。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>任务当前所有者的队列ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>任务的当前所有者的名称。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>任务的当前所有者的ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务ACL对象

   任务ACL对象包含有关权限的信息，如转发、共享、查阅等。 任务。 以下是任务ACL的属性。

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
   <td>如果为true，则可声明任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可咨询任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可转发任务。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>如果为true，则可共享任务。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 任务附件

   附件可以添加到任务。 附件的类型可以是附件和附注。 以下是attachment对象的属性。

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
   <td>添加附件的任务的ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>类型<br type="_moz" /> </td>
   <td>F</td>
   <td>“类型”是文件的附件，“类型”是注释。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>它根据用户的UI设置包含附件创建日期。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化附件说明。 用于在AEM Forms工作区中显示附件说明中显示的特殊字符。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>格式化的附件名称。 用于在AEM Forms工作区中显示附件名称中存在的特殊字符。 仅用于注释。<br type="_moz" /> </td>
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
   <td>说明<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的说明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>用户组的列表。<br type="_moz" /> </td>
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
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>如果用户不在办公室，则为True。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的姓氏。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>用户的名。<br type="_moz" /> </td>
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
   <td>用户的联系号码。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>电话号码<br type="_moz" /> </td>
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
