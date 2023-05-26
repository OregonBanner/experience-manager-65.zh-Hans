---
title: 自定义任务详细信息页面
seo-title: Customizing the task details page
description: 如何在AEM Forms工作区中自定义“任务详细信息”页面，以修改显示的关于任务的默认信息。
seo-description: How-to customize the task details page in AEM Forms workspace to modify the default information displayed about a task.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 自定义任务详细信息页面 {#customizing-the-task-details-page}

任务详细信息页面包含有关任务及其流程的信息。 但是，您可以自定义任务详细信息页面以添加或删除信息。

可以将以下信息添加到任务详细信息页面：

* 任务的JSON对象中可用的信息（中的“任务”部分） [AEM Forms工作区JSON对象说明](/help/forms/using/html-workspace-json-object-description.md))
* 进程实例的JSON对象中可用的信息（中的“进程实例”部分） [AEM Forms工作区JSON对象说明](/help/forms/using/html-workspace-json-object-description.md))

要自定义任务详细信息页面，请执行以下操作：

1. 关注 [AEM Forms工作区自定义的一般步骤。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 要显示任何其他信息，请将相应的键值对添加到 `translation.json` 文件位置 `todo`块> `details`块> `app`块> [ `required`块].

   此 [ `required`块] 指可用的块，例如任务信息的任务块、流程信息的处理块和待定任务信息的当前待定任务块。

   例如，要在任务详细信息页面中添加有关“需要路由选择”的信息，您可以在任务块中添加以下键值对：

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

1. 复制 `/libs/ws/js/runtime/templates/taskdetails.html` 到 `/apps/ws/js/runtime/templates/taskdetails.html`.

   将新信息添加到 `/apps/ws/js/runtime/templates/taskdetails.html`. 例如：

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

   搜索和替换 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` 替换为 `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>要使用在中创建的任务来自定义任务详细信息页面 **启动进程** AEM Forms选项卡，将新信息添加到 `/apps/ws/js/runtime/templates/startprocess.html`.
>
>要为详细信息页面中添加的信息添加新样式，请使用修改CSS文件 *用户界面更改* 中的部分 [工作区自定义](changing-locale-user-interface.md).
