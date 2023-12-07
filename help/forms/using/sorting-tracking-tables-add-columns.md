---
title: 自定义跟踪表
description: 如何自定义任务表中用户进程详细信息的显示，该表显示在AEM Forms工作区的“跟踪”选项卡中。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9ab657cc-fa8e-4168-8a68-e38ac5c51b29
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# 自定义跟踪表{#customize-tracking-tables}

AEM Forms工作区中的“跟踪”选项卡用于显示与登录用户有关的进程实例的详细信息。 要查看跟踪表，请先在左窗格中选择进程名称，然后在中间窗格中查看其实例列表。 选择一个进程实例，以在右侧窗格中查看由此实例生成的任务表。 默认情况下，表列显示以下任务属性（任务模型中的相应属性在括号中给出）：

* ID ( `taskId`)
* 名称( `stepName`)
* 说明( `instructions`)
* 选定的操作( `selectedRoute`)
* 创建时间( `createTime`)
* 完成时间( `completeTime`)
* 所有者( `currentAssignment.queueOwner`)

任务模型中可在任务表中显示的其余属性包括：

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>提醒计数</p> </td>
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
   <td><p>内容类型</p> </td>
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
   <td><p>服务标题</p> </td>
  </tr>
  <tr>
   <td><p>当前工作</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>截止日期</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>说明</p> </td>
   <td><p>numformsToBeSaved</p> </td>
   <td><p>状态</p> </td>
  </tr>
  <tr>
   <td><p>显示名称</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportssave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>优先级</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>任务表单类型</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserinfo</p> </td>
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

对于任务表中的以下自定义，您需要在源代码中进行语义更改。 请参阅 [自定义AEM Forms工作区简介](/help/forms/using/introduction-customizing-html-workspace.md) 有关如何使用Workspace SDK进行语义更改以及如何从更改的源构建缩小的包。

## 更改表列及其顺序 {#changing-table-columns-and-their-order}

1. 要修改表中显示的任务属性及其顺序，请配置文件/ws/js/runtime/templates/processinstancehistory.html ：

   ```html
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

   ```html
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example, -->
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

1. 注册点击处理程序 `.fixedTaskTableHeader th` 在文件中 `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   在处理程序中，调用 `onTaskTableHeaderClick` 功能 `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. 公开 `TaskTableHeaderClick` 中的方法 `js/runtime/util/history.js`.

   该方法从单击事件中查找任务属性，对该属性上的任务列表进行排序，然后使用排序的任务列表呈现任务表。

   通过提供比较器函数，使用任务列表集合上的主干排序函数完成排序。

   ```javascript
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```javascript
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
