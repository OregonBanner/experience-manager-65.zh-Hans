---
title: 自定义任务详细信息页面
seo-title: 自定义任务详细信息页面
description: 如何在AEM Forms工作区中自定义任务详细信息页面，以修改显示的关于任务的默认信息。
seo-description: 如何在AEM Forms工作区中自定义任务详细信息页面，以修改显示的关于任务的默认信息。
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# 自定义任务详细信息页面 {#customizing-the-task-details-page}

任务详细信息页面包含有关任务及其进程的信息。 但是，您可以自定义任务详细信息页面以添加或删除信息。

您可以向任务详细信息页面添加以下信息：

* 任务的JSON对象中提供的信息( [AEM Forms工作区中的任务部分JSON对象描述](/help/forms/using/html-workspace-json-object-description.md))
* 进程实例的JSON对象中提供的信息( [AEM Forms工作区中的进程实例部分JSON对象描述](/help/forms/using/html-workspace-json-object-description.md))

要自定义任务详细信息页面，请执行以下操作：

1. 按照 [常规步骤自定义AEM Forms工作区。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要显示任何其他信息，请在“块>块>块>块” `translation.json` >块处向文 `todo`件添加相 `details`应的键值 `app`对 [`required`]。

   该 [ 块 `required`引用可用块] ，例如任务信息的任务块、处理信息的处理块和待处理任务信息的当前处理任务块。

   例如，要在任务详细信息页面中添加“需要路由选择”的相关信息，可以在任务块中添加以下键值对：

   ```
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >为所有支持的语言添加相应的键值对。

1. 复制 `/libs/ws/js/runtime/templates/taskdetails.html` 到 `/apps/ws/js/runtime/templates/taskdetails.html`。

   将新信息添加到 `/apps/ws/js/runtime/templates/taskdetails.html`。 例如：

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. 打开/apps/ws/js/registry.js进行编辑。

   搜索并替换 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 为 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>要使用在AEM Forms工作区的任务流程选项卡中创建的任务自定义开始详细信息页面 **，请向其中添加新信息**`/apps/ws/js/runtime/templates/startprocess.html`。
>
>要为在详细信息页面中添加的信息添加新样式，请使用工作区自定义中的“用户界面 *更改* ”部分修改 [CSS文件](changing-locale-user-interface.md)。
