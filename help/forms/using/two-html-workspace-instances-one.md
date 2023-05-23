---
title: 在單一伺服器上託管兩個AEM Forms工作區執行個體
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC管理員如何自訂HTMLWS，以便在可透過不同URL存取的單一伺服器上託管兩個執行個體。
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 在單一伺服器上託管兩個AEM Forms工作區執行個體 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝與設定僅允許伺服器上使用一個AEM Forms工作區。 不過，您可能需要在一部AEM Forms伺服器上託管兩個不同的AEM Forms工作區例項。 這兩個例項可由不同的URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一部伺服器上使用。 在本自訂文章中，我們假設兩個工作區可在以下位置存取： `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`.

請依照下列步驟設定AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的開發套件。 另請參閱 [開發套件](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以取得建立它的指示。
1. 以管理員身分登入CRXDE Lite，方法是存取 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 在/content複製節點ws，然後在/content貼上。 將節點重新命名為ws2。 按一下 **[!UICONTROL 全部儲存]**. 在此節點的屬性中，變更值 `sling:resourceType` 至ws2。 按一下 **[!UICONTROL 全部儲存]**.

1. 從/libs複製資料夾ws並貼到/apps。 將資料夾重新命名為ws2。 按一下 **[!UICONTROL 全部儲存]**.
1. 在 `GET.jsp` 於 `/apps/ws2`，進行下列程式碼變更。 取代下列專案

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   包含下列程式碼

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 於 `/apps/ws2/js`，變更範本路徑以參照範本 `/apps/ws2/js/runtime/templates`. 取代下列程式碼

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   包含下列程式碼

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. 在 `userinfo.js` 於 `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，變更字串 `/lc/content/ws` 至 `lc/content/ws2`.

1. 在 `/apps/ws2/js/runtime/services/service.js`，變更中的路徑 `getLocalizationData` 指向的函式 `/lc/apps/ws2/Locale.html`.

1. 若要參閱 `pdf.html` 的路徑變更 `pdf.html` 在 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 若要參閱 `pdf.html` 變更新工作區的路徑 `pdf.html` 和 `WsNextAdapter.swf` 在 `startprocess.html`， `taskdetails.html`、和 `processinstancehistory.html` 於 `/apps/ws2/js/runtime/templates`.

1. 複製 `/etc/map/ws` 資料夾並貼到 `/etc/map`. 將新資料夾重新命名為ws2。 按一下「全部儲存」。

1. 在下列專案的屬性中： `ws2`，變更值 `sling:redirect` 至 `content/ws2`.

1. 變更值 `sling:match` 至 `^[^/\||]/[^/\||]/ws2$`.
