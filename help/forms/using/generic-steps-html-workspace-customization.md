---
title: AEM Forms工作区自定义的一般步骤
seo-title: Generic steps for AEM Forms workspace customization
description: 如何开始自定义AEM Forms工作区用户界面。
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# AEM Forms工作区自定义的一般步骤 {#generic-steps-for-aem-forms-workspace-customization}

执行任何自定义的一般步骤包括：

1. 通过访问以登录CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 创建 `sling:Folder` 文件夹已命名 `ws` at `/apps`，如果不存在。 创建 `sling:Folder` 文件夹，右键单击 `apps` 文件夹，选择 **[!UICONTROL 创建]** > **[!UICONTROL 创建节点]**. 将名称指定为 `ws`选择类型 `sling:Folder` 单击 **[!UICONTROL 确定]**. 单击 **[!UICONTROL 全部保存]**.
1. 浏览到 `/apps/ws`，然后导航到 **[!UICONTROL 访问控制]** 选项卡。
1. 选择 **[!UICONTROL 存储库]** 选项。 在 **[!UICONTROL 访问控制]** 列表，单击 **[!UICONTROL +]** 添加新条目。 单击 **[!UICONTROL +]** 再次。
1. 搜索并选择 **PERM_WORKSPACE_USER** 校长。

   ![选择PERM_WORKSPACE_USER主体作为自定义HTML工作区的常规步骤的一部分](assets/perm_workspace_user.png)

1. 给 `jcr:read` 权限。
1. 单击 **[!UICONTROL 全部保存]**.
1. 复制 `GET.jsp`, `index`和 `html.jsp` 文件 `/libs/ws` 文件夹 `/apps/ws` 文件夹。
1. 复制 `/libs/ws/locales` 文件夹 `/apps/ws` 文件夹。 单击 **[!UICONTROL 全部保存]**.
1. 更新 `GET.jsp` 文件，如下所示，然后单击 **[!UICONTROL 全部保存]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 对CSS自定义项执行以下操作：

   1. 导航到 `/apps/ws` 文件夹，并创建名为 `css`.

   1. 在 `css` 文件夹，创建名为 `newStyle.css`.

   1. 打开 `/apps/ws/html`.jsp，从

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   到

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >将用户定义的CSS文件的条目放在style.css条目之后，如上所示。

1. 在/apps/ws/html.jsp文件中，从

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   到

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 执行以下操作：

   1. 创建名为的文件夹 `js` at `/apps/ws`. 单击 **[!UICONTROL 全部保存]**.

   1. 创建名为的文件夹 `libs` at `/apps/ws/js`. 单击 **[!UICONTROL 全部保存]**.

   1. 复制 `/libs/ws/js/libs/jqueryui` 文件夹 `/apps/ws/js/libs`. 单击 **[!UICONTROL 全部保存]**.

1. 对HTML自定义执行以下操作：

   1. 在 `/apps/ws/js`，创建名为的文件夹 `runtime`. 单击 **[!UICONTROL 全部保存]**.

   1. 在 `/apps/ws/js/runtime`，创建名为的文件夹 `templates`. 单击 **[!UICONTROL 全部保存]**.

   1. 复制 `/libs/ws/js/main.js` to `/apps/ws/js/main.js`.

   1. 将/libs/ws/js/registry.js复制到 `/apps/ws/js/registry.js`.

1. 单击 **[!UICONTROL 全部保存]**、清除缓存并刷新AEM Forms工作区。

   访问URL `https://'[server]:[port]'/lc/ws` 和使用管理员/密码凭据登录。 浏览器重定向到 `https://'[server]:[port]'/lc/apps/ws/index.html`.
