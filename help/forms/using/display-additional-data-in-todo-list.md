---
title: 在待办事项列表中显示附加数据
seo-title: Displaying additional data in ToDo list
description: 如何自定义LiveCycleAEM Forms工作区待办事项列表的显示，以显示默认列表以外的更多信息。
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# 在待办事项列表中显示附加数据{#displaying-additional-data-in-todo-list}

默认情况下，AEM Forms工作区的待办事项列表会显示任务显示名称和描述。 但是，您可以添加其他信息，如创建日期、截止日期等。 您还可以添加图标和更改显示样式。

![查看显示默认配置的HTML工作区待办事项选项卡](assets/html-todo-list.png)

本文详细介绍了为“待办事项”列表中的每个任务添加要显示信息的步骤。

## 可添加内容 {#what-can-be-added}

您可以添加以下位置提供的信息 `task.json` 由服务器发送。 信息可以纯文本形式添加，也可以使用样式设置信息的格式。

有关JSON对象描述的详细信息，请参见 [此](/help/forms/using/html-workspace-json-object-description.md) 文章。

## 显示任务信息 {#displaying-information-on-a-task}

1. 请遵循 [AEM Forms工作区自定义的一般步骤](../../forms/using/generic-steps-html-workspace-customization.md).
1. 要显示任务的附加信息，必须在的任务块中添加相应的键值对 `translation.json`.

   例如，更改 `/apps/ws/locales/en-US/translation.json` 对于英语：

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。

1. 例如，在任务块中添加信息：

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 为新属性定义CSS {#defining-css-for-the-new-property}

1. 您可以将样式应用于添加到任务的信息（属性）。 为此，您需要为添加到的新属性添加样式信息 `/apps/ws/css/newStyle.css`.

   例如，添加：

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## 在HTML模板中添加条目 {#adding-entry-in-the-html-template}

最后，您需要在开发包中为要添加到任务的每个属性包含一个条目。 要创建工作区代码，请参阅构建AEM Forms工作区代码。

1. 复制`task.html`：

   * 从: `/libs/ws/js/runtime/templates/`
   * 到: `/apps/ws/js/runtime/templates/`

1. 将新信息添加到 `/apps/ws/js/runtime/templates/task.html`.

   例如，添加在 `div class="taskProperties"`：

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
