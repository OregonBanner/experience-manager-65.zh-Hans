---
title: 在網頁應用程式中整合AEM Forms工作區元件
seo-title: Integrating AEM Forms workspace components in web applications
description: 如何在您自己的網頁應用程式中重複使用AEM Forms工作區元件，以運用功能並提供緊密整合。
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 在網頁應用程式中整合AEM Forms工作區元件 {#integrating-aem-forms-workspace-components-in-web-applications}

您可以使用AEM Forms工作區 [元件](/help/forms/using/description-reusable-components.md) 在您自己的網頁應用程式中。 以下實作範例使用安裝在CRX™執行個體上的AEM Forms Workspace Dev套件中的元件來建立網頁應用程式。 根據您的特定需求，自訂以下的解決方案。 實作重複使用範例 `UserInfo`， `FilterList`、和 `TaskList`網站入口網站內的元件。

1. 登入CRXDE Lite環境於 `https://'[server]:[port]'/lc/crx/de/`. 確保您已安裝AEM Forms workspace dev套件。
1. 建立路徑 `/apps/sampleApplication/wscomponents`.
1. 複製css、影像、js/libs、js/runtime和js/registry.js

   * 从 `/libs/ws`
   * 到 `/apps/sampleApplication/wscomponents`.

1. 在/apps/sampleApplication/wscomponents/js資料夾中建立demomain.js檔案。 將程式碼從/libs/ws/js/main.js複製到demomain.js中。
1. 在demomain.js中，移除程式碼以初始化Router並新增下列程式碼：

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

1. 在/content下依名稱建立節點 `sampleApplication` 和型別 `nt:unstructured`. 在此節點的屬性中新增 `sling:resourceType` 字串和值的型別 `sampleApplication`. 在此節點的「存取控制清單」中新增專案 `PERM_WORKSPACE_USER` 允許jcr：read許可權。 此外，在的「存取控制」清單中 `/apps/sampleApplication` 新增專案 `PERM_WORKSPACE_USER` 允許jcr：read許可權。
1. 在 `/apps/sampleApplication/wscomponents/js/registry.js` 更新路徑 `/lc/libs/ws/` 至 `/lc/apps/sampleApplication/wscomponents/` 範本值。
1. 在您的入口網站首頁，JSP檔案位於 `/apps/sampleApplication/GET.jsp`，新增下列程式碼，在入口網站中包含必要元件。

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   也包含AEM Forms工作區元件所需的CSS檔案。

   >[!NOTE]
   >
   >呈現時，每個元件都會新增至元件標籤（具有類別元件）。 確定您的首頁包含這些標籤。 請參閱 `html.jsp` AEM Forms工作區檔案，以進一步瞭解這些基本控制項標籤。

1. 若要自訂元件，您可以延伸所需元件的現有檢視，如下所示：

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

1. 修改入口網站CSS以設定入口網站上所需元件的版面、位置和樣式。 例如，您想要讓此入口網站的背景顏色保持為黑色，以便順利檢視userInfo元件。 您可以變更下列專案的背景顏色來完成此操作： `/apps/sampleApplication/wscomponents/css/style.css` 如下所示：

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
