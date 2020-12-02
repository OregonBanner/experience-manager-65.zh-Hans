---
title: 将AEM Forms工作区组件集成到Web应用程序中
seo-title: 将AEM Forms工作区组件集成到Web应用程序中
description: 如何在您自己的Web应用程序中重复使用AEM Forms工作区组件，以利用功能并提供紧密集成。
seo-description: 如何在您自己的Web应用程序中重复使用AEM Forms工作区组件，以利用功能并提供紧密集成。
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# 将AEM Forms工作区组件集成到Web应用程序{#integrating-aem-forms-workspace-components-in-web-applications}

您可以在自己的Web应用程序中使用AEM Forms工作区[组件](/help/forms/using/description-reusable-components.md)。 以下示例实现使用安装在CRX™实例上的AEM Forms工作区开发包中的组件创建Web应用程序。 自定义以下解决方案以满足您的特定需求。 示例实现在Web门户中重用`UserInfo`、`FilterList`和`TaskList`组件。

1. 登录`https://'[server]:[port]'/lc/crx/de/`的CRXDE Lite环境。 确保您安装了AEM FormsWorkpace Dev软件包。
1. 创建路径`/apps/sampleApplication/wscomponents`。
1. 复制css、图像、js/libs、js/runtime和js/registry.js

   * 从 `/libs/ws`
   * 到 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js文件夹中创建demomain.js文件。 将代码从/libs/ws/js/main.js复制到demomain.js。
1. 在demomain.js中，删除用于初始化路由器的代码并添加以下代码：

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. 在/content下按名称`sampleApplication`创建一个节点，然后键入`nt:unstructured`。 在此节点的属性中，添加“字符串”类型的`sling:resourceType`和值`sampleApplication`。 在此节点的访问控制列表中，为`PERM_WORKSPACE_USER`添加一个允许jcr:read权限的条目。 此外，在`/apps/sampleApplication`的访问控制列表中，为`PERM_WORKSPACE_USER`添加允许jcr:read权限的条目。
1. 在`/apps/sampleApplication/wscomponents/js/registry.js`中，将模板值从`/lc/libs/ws/`更新到`/lc/apps/sampleApplication/wscomponents/`的路径。
1. 在位于`/apps/sampleApplication/GET.jsp`的门户主页JSP文件中，添加以下代码，将所需的组件包含在门户中。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   还包括AEM Forms工作区组件所需的CSS文件。

   >[!NOTE]
   >
   >呈现时，每个组件都会添加到组件标签（具有类组件）。 确保您的主页包含这些标记。 请参阅AEM Forms工作区的`html.jsp`文件，进一步了解这些基本控件标签。

1. 要自定义组件，您可以按如下方式扩展所需组件的现有视图:

   ```javascript
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. 修改门户CSS，在门户上配置所需组件的布局、位置和样式。 例如，您希望将此门户的背景颜色保持为黑色，以便视图userInfo组件。 可通过在`/apps/sampleApplication/wscomponents/css/style.css`中更改背景颜色来实现此目的，如下所示：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
