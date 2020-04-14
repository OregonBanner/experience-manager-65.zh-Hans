---
title: 自定义路由操作中使用的图像
seo-title: 自定义路由操作中使用的图像
description: 如何自定义在LiveCycle AEM Forms工作区中路由操作中使用的图像。
seo-description: 如何自定义在LiveCycle AEM Forms工作区中路由操作中使用的图像。
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# 自定义路由操作中使用的图像 {#customize-images-used-in-route-actions}

要自定义路由操作中使用的图像，请执行自定义的常规步骤中所述的步骤 [](/help/forms/using/generic-steps-html-workspace-customization.md) ，然后执行本文中描述的步骤。

## 用于路由操作的图像 {#images-for-route-actions}

1. 在CSS中为新路由操作添加定义图像的样式，位置如下：

   `/apps/ws/css/newStyle.css`

   例如：添加一个新样式， `myStyle1`如下所示，并使用WebDAV客户端将图像 `myStyleIcon1.png` 文件上 `/apps/ws/image`传到s文件夹。

   >[!NOTE]
   >
   >有关WebDAV访问的详细信息，请参 [阅https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

   >[!NOTE]
   >
   >希望使用样式名称与路由操作名称相同。

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## 任务列表任务操作弹出窗口 {#task-list-task-action-popup}

1. 创建任务列表操作弹出窗口，请参 [阅构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code)。 它需要使用开发包。

1. 复制 `/libs/ws/js/runtime/templates/task.html` 到 `/apps/ws/js/runtime/templates/task.html`。

1. 如果CSS样式的名称与来自服务器的路由操作名称相同，请在中修改以下代码 `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. 如果CSS样式的名称与来自服务器的路由操作名称不同，请在中修改以下代码 `/apps/ws/js/runtime/templates/task.html`。 它会添加一堆Servlet条 `if-else` 件，以将样式与路由操作名称映射。

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## 任务详细信息任务操作弹出窗口 {#task-details-task-action-popup}

1. 复制 `/libs/ws/js/runtime/templates/taskdetails.html` 到 `/apps/ws/js/runtime/templates/taskdetails.html`。

1. 如果CSS样式的名称与来自服务器的路由操作名称相同，请在中修改以下代码 `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. 如果CSS样式的名称与来自服务器的路由操作名称不同，请在中修改以下代码 `/apps/ws/js/runtime/templates/taskdetails.html`。 它会添加一堆Servlet条 `if-else` 件，以将样式与路由操作名称进行映射。

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. 打开 `/apps/ws/js/registry.js` 进行编辑并查找以下文本：
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. 将文本替换为：
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
