---
title: AEM Forms工作区自定义的一般步骤
seo-title: AEM Forms工作区自定义的一般步骤
description: 如何开始自定义AEM Forms工作区用户界面。
seo-description: 如何开始自定义AEM Forms工作区用户界面。
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---


# AEM Forms工作区自定义的一般步骤{#generic-steps-for-aem-forms-workspace-customization}

执行任何自定义的一般步骤包括：

1. 通过访问登录到CRXDE `https://'[server]:[port]'/lc/crx/de/index.jsp`Lite。
1. 如果文件夹不 `ws`存 `/apps`在，请创建名为的文件夹。 单击“ **[!UICONTROL 全部保存]**”。
1. 浏览至 `/apps/ws`访问控制，然后导航到 **** 选项卡。
1. 在 **[!UICONTROL 访问控制]** 列表 **[!UICONTROL 中]** ，单击+以添加新条目。 再次 **[!UICONTROL 单击]** +。
1. 搜索并选 **择PERM_WORKSPACE_USER** Principal。

   ![选择PERM_WORKSPACE_USER主体作为自定义HTML工作区的通用步骤的一部分](assets/perm_workspace_user.png)

1. 授予 `jcr:read` 主体权限。
1. 单击“ **[!UICONTROL 全部保存]**”。
1. 将文件夹 `GET.jsp` 中的 `html.jsp`和文件 `/libs/ws`复制到文 `/apps/ws` 件夹。
1. 复制文 `/libs/ws/locales` 件夹中的文 `/apps/ws` 件夹。 单击“ **[!UICONTROL 全部保存]**”。
1. 如下所示，更新文件中的引用 `GET.jsp` 和相对路径，然后单击“全 **[!UICONTROL 部保存”]**。

   ```jsp
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 对CSS自定义执行以下操作：

   1. 导览至该文 `/apps/ws` 件夹，然后创建一个名为的新文 `css`件夹。

   1. 在文件夹 `css`文件夹中，创建一个名为的新文 `newStyle.css`件。

   1. 打开 `/apps/ws/html`.jsp并从

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   到

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >将用户定义CSS文件的条目放在newStyle.css条目之后，如上所示。

1. 在/apps/ws/html.jsp文件中，更改

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   到

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 执行以下操作：

   1. 创建名为的文 `js`件夹 `/apps/ws`。 单击“ **[!UICONTROL 全部保存]**”。

   1. 创建名为的文 `libs`件夹 `/apps/ws/js`。 单击“ **[!UICONTROL 全部保存]**”。

   1. 创建名为的文 `jqueryui`件夹 `/apps/ws/js/libs`。 单击“ **[!UICONTROL 全部保存]**”。

   1. 复制 `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` 到 `/apps/ws/js/libs/jqueryui`。 单击“ **[!UICONTROL 全部保存]**”。

1. 对HTML自定义执行以下操作：

   1. 在下 `/apps/ws/js`面，创建一个名为的文 `runtime`件夹。 单击“ **[!UICONTROL 全部保存]**”。

   1. 在下 `/apps/ws/js/runtime`面，创建一个名为的文 `templates`件夹。 单击“ **[!UICONTROL 全部保存]**”。

   1. 复制 `/libs/ws/js/main.js` 到 `/apps/ws/js/main.js`。

   1. 将/libs/ws/js/registry.js复制到 `/apps/ws/js/registry.js`。

1. 单击 **[!UICONTROL 全部保存]**、清除缓存并刷新AEM Forms工作区。

   访问URL `https://'[server]:[port]'/lc/ws` 并使用管理员／密码凭据登录。 浏览器将重定向到 `https://'[server]:[port]'/lc/apps/ws/index.html`。
