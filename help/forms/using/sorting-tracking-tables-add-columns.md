---
title: 自定义跟踪表
seo-title: 自定义跟踪表
description: 如何自定义在AEM Forms工作区的跟踪选项卡中显示的任务表中显示用户进程详细信息。
seo-description: 如何自定义在AEM Forms工作区的跟踪选项卡中显示的任务表中显示用户进程详细信息。
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 自定义跟踪表{#customize-tracking-tables}

AEM Forms工作区中的跟踪选项卡用于显示涉及登录用户的进程实例的详细信息。 要视图跟踪表，请首先在左窗格中选择进程名称，以便在中间窗格中查看其实例的列表。 选择一个进程实例，以在右侧窗格中查看由此实例生成的任务表。 默认情况下，表列显示以下任务属性(任务模型中的相应属性在括号中给出):

* ID ( `taskId`)
* 名称 ( `stepName`)
* 说明 ( `instructions`)
* 选择的操作 ( `selectedRoute`)
* 创建时间( `createTime`)
* 完成时间( `completeTime`)
* 所有者 ( `currentAssignment.queueOwner`)

任务模型中剩余的可在任务表中显示的属性有：

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLAactions</p> </td>
  </tr>
  <tr>
   <td><p>截止期限</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>描述</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>状态</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfficeUserName</p> </td>
   <td><p>supportsSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>优先级</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

对于任务表中的以下自定义，您需要在源代码中进行语义更改。 请参 [阅自定义AEM Forms工作区简介](/help/forms/using/introduction-customizing-html-workspace.md) ，了解如何使用工作区SDK进行语义更改并从更改的源中构建简化的包。

## 更改表列及其顺序 {#changing-table-columns-and-their-order}

1. 要修改表中显示的任务属性及其顺序，请配置文件/ws/js/runtime/templates/processinstancehistory.html:

   ```as3
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## 对跟踪表进行排序 {#sorting-a-tracking-table}

要在单击列标题时对任务列表表进行排序，请执行以下操作：

1. 在文件中注册一个 `.fixedTaskTableHeader th` 单击处理程序 `js/runtime/views/processinstancehistory.js`。

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   在处理函数中，调用 `onTaskTableHeaderClick` 的函数 `js/runtime/util/history.js`。

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 在中公 `TaskTableHeaderClick` 开该方法 `js/runtime/util/history.js`。

   该方法从单击任务中查找事件属性，对该属性的任务列表进行排序，并使用排序的任务列表呈现任务表。

   通过提供比较器函数，使用任务列表集合上的骨干排序函数来进行排序。

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
