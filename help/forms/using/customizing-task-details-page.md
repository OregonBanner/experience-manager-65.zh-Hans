---
title: 自定义任务详细信息页
seo-title: 自定义任务详细信息页
description: 如何在AEM Forms工作区中自定义任务详细信息页面以修改显示的任务默认信息。
seo-description: 如何在AEM Forms工作区中自定义任务详细信息页面以修改显示的任务默认信息。
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 自定义任务详细信息页面{#customizing-the-task-details-page}

任务详细信息页面包含有关任务及其进程的信息。 但是，您可以自定义任务详细信息页面以添加或删除信息。

您可以向任务详细信息页面添加以下信息：

* 任务的JSON对象中提供的信息([AEM Forms工作区JSON对象描述](/help/forms/using/html-workspace-json-object-description.md)中的任务部分)
* 进程实例的JSON对象中可用的信息([AEM Forms工作区JSON对象描述](/help/forms/using/html-workspace-json-object-description.md)中的进程实例部分)

要自定义任务详细信息页面，请执行以下操作：

1. 按照[AEM Forms工作区自定义的一般步骤操作。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要显示任何附加信息，请在`todo`块> `details`块> `app`块> [块`required`块]的`translation.json`文件中添加相应的键值对。

   [ `required`块]引用可用块，如任务信息的任务块、进程信息的进程块和待处理任务信息的当前处理任务块。

   例如，要在任务详细信息页面中添加“需要路由选择”的相关信息，可以在任务块中添加以下键值对：

   ```json
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

1. 将`/libs/ws/js/runtime/templates/taskdetails.html`复制到`/apps/ws/js/runtime/templates/taskdetails.html`。

   将新信息添加到`/apps/ws/js/runtime/templates/taskdetails.html`。 例如：

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

   搜索并将`text!/lc/libs/ws/js/runtime/templates/taskdetails.html`替换为`text!/lc/apps/ws/js/runtime/templates/taskdetails.html`。

>[!NOTE]
>
>要使用在AEM Forms工作区的&#x200B;**任务进程**&#x200B;选项卡中创建的任务自定义开始详细信息页面，请将新信息添加到`/apps/ws/js/runtime/templates/startprocess.html`。
>
>要为在详细信息页面中添加的信息添加新样式，请使用[工作区自定义](changing-locale-user-interface.md)中的&#x200B;*用户界面更改*&#x200B;部分修改CSS文件。
