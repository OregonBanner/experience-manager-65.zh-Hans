---
title: AEM Forms工作區自訂的一般步驟
seo-title: Generic steps for AEM Forms workspace customization
description: 如何開始自訂AEM Forms工作區使用者介面。
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

# AEM Forms工作區自訂的一般步驟 {#generic-steps-for-aem-forms-workspace-customization}

執行任何自訂的一般步驟如下：

1. 透過存取登入CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 建立 `sling:Folder` 資料夾已命名 `ws` 於 `/apps`，如果它不存在。 若要建立 `sling:Folder` 資料夾，用滑鼠右鍵按一下 `apps` 資料夾並選取 **[!UICONTROL 建立]** > **[!UICONTROL 建立節點]**. 將名稱指定為 `ws`，選取型別為 `sling:Folder` 並按一下 **[!UICONTROL 確定]**. 按一下 **[!UICONTROL 全部儲存]**.
1. 瀏覽至 `/apps/ws`，並導覽至 **[!UICONTROL 存取控制]** 標籤。
1. 選取 **[!UICONTROL 存放庫]** 選項。 在 **[!UICONTROL 存取控制]** 清單，按一下 **[!UICONTROL +]** 以新增專案。 按一下 **[!UICONTROL +]** 再來一次。
1. 搜尋並選取 **PERM_WORKSPACE_USER** 主體。

   ![選取PERM_WORKSPACE_USER主體作為自訂HTML工作區的一般步驟的一部分](assets/perm_workspace_user.png)

1. 授予 `jcr:read` 主體許可權。
1. 按一下 **[!UICONTROL 全部儲存]**.
1. 複製 `GET.jsp`， `index`、和 `html.jsp` 檔案來自 `/libs/ws` 資料夾至 `/apps/ws` 資料夾。
1. 複製 `/libs/ws/locales` 中的資料夾 `/apps/ws` 資料夾。 按一下 **[!UICONTROL 全部儲存]**.
1. 更新中的參照和相對路徑 `GET.jsp` 檔案，如下所示，然後按一下 **[!UICONTROL 全部儲存]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. 請針對CSS自訂執行下列動作：

   1. 導覽至 `/apps/ws` 資料夾並建立名為的新資料夾 `css`.

   1. 在 `css` 資料夾，建立名為的新檔案 `newStyle.css`.

   1. 開啟 `/apps/ws/html`.jsp和變更自

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
   >將使用者定義的CSS檔案專案放在style.css專案之後，如上所示。

1. 在/apps/ws/html.jsp檔案中，從

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   到

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. 执行以下操作：

   1. 建立名為的資料夾 `js` 於 `/apps/ws`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 建立名為的資料夾 `libs` 於 `/apps/ws/js`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 複製 `/libs/ws/js/libs/jqueryui` 資料夾至 `/apps/ws/js/libs`. 按一下 **[!UICONTROL 全部儲存]**.

1. 請針對HTML自訂執行下列動作：

   1. 下 `/apps/ws/js`，建立名為的資料夾 `runtime`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 下 `/apps/ws/js/runtime`，建立名為的資料夾 `templates`. 按一下 **[!UICONTROL 全部儲存]**.

   1. 複製 `/libs/ws/js/main.js` 至 `/apps/ws/js/main.js`.

   1. 將/libs/ws/js/registry.js複製到 `/apps/ws/js/registry.js`.

1. 按一下 **[!UICONTROL 全部儲存]**，清除快取，然後重新整理AEM Forms工作區。

   存取URL `https://'[server]:[port]'/lc/ws` 並使用管理員/密碼認證登入。 瀏覽器重新導向至 `https://'[server]:[port]'/lc/apps/ws/index.html`.
