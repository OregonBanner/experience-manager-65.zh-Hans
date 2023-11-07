---
title: 在Web应用程序中集成AEM Forms工作区组件
description: 如何在您自己的Web应用程序中重用AEM Forms工作区组件以使用功能并提供紧密集成。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 在Web应用程序中集成AEM Forms工作区组件 {#integrating-aem-forms-workspace-components-in-web-applications}

您可以使用AEM Forms工作区 [组件](/help/forms/using/description-reusable-components.md) 在您自己的Web应用程序中。 以下实施示例使用安装在CRX™实例上的AEM Forms工作区开发包中的组件来创建Web应用程序。 自定义以下解决方案以满足您的特定需求。 实现重用示例 `UserInfo`， `FilterList`、和 `TaskList`Web门户中的组件。

1. 登录CRXDE Lite环境： `https://'[server]:[port]'/lc/crx/de/`. 确保您已安装AEM Forms Workspace开发包。
1. 创建路径 `/apps/sampleApplication/wscomponents`.
1. 复制css、图像、js/libs、js/runtime和js/registry.js

   * 从 `/libs/ws`
   * 到 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js文件夹内创建demomain.js文件。 将代码从/libs/ws/js/main.js复制到demomain.js中。
1. 在demomain.js中，删除用于初始化路由器的代码，然后添加以下代码：

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

1. 在/content下按名称创建节点 `sampleApplication` 和类型 `nt:unstructured`. 在此节点的属性中，添加 `sling:resourceType` 字符串和值的类型 `sampleApplication`. 在此节点的访问控制列表中，添加一个条目 `PERM_WORKSPACE_USER` 允许jcr：read权限。 此外，在的“访问控制”列表中 `/apps/sampleApplication` 添加条目 `PERM_WORKSPACE_USER` 允许jcr：read权限。
1. 在 `/apps/sampleApplication/wscomponents/js/registry.js` 更新路径 `/lc/libs/ws/` 到 `/lc/apps/sampleApplication/wscomponents/` （对于模板值）。
1. 在门户主页JSP文件中： `/apps/sampleApplication/GET.jsp`，添加以下代码以在门户中包含所需的组件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   还包括AEM Forms工作区组件所需的CSS文件。

   >[!NOTE]
   >
   >在渲染时，每个组件都会添加到组件标记（具有类组件）。 确保主页包含这些标记。 请参阅 `html.jsp` AEM Forms文件，以了解有关这些基本控件标记的更多信息。

1. 要自定义组件，您可以按如下方式扩展所需组件的现有视图：

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
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

1. 修改门户CSS以在您的门户上配置所需组件的布局、位置和样式。 例如，您希望将此门户的背景颜色保持为黑色以便更好地查看userInfo组件。 为此，您可以更改中的背景颜色 `/apps/sampleApplication/wscomponents/css/style.css` 如下所示：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
