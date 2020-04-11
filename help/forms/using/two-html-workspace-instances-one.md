---
title: 在一台服务器上承载两个AEM Forms工作区实例
seo-title: 在一台服务器上承载两个AEM Forms工作区实例
description: LC管理员如何自定义HTML WS以在可通过不同URL访问的单台服务器上承载两个实例。
seo-description: LC管理员如何自定义HTML WS以在可通过不同URL访问的单台服务器上承载两个实例。
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在一台服务器上承载两个AEM Forms工作区实例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的默认安装和设置只允许在服务器上提供一个AEM Forms工作区。 但是，您可能需要在单台AEM Forms服务器上承载两个不同的AEM Forms工作区实例。 两个实例可通过不同的URL访问。

AEM Forms管理员可自定义工作区以创建两个不同的URL，并使两个工作区在同一服务器上可用。 在此自定义文章中，我们假定两个工作区可在 `https://'[server]:[port]'/lc/ws` 和访问 `https://'[server]:[port]':/lc/ws2`。

请按照以下步骤配置AEM Forms工作区。

1. 在服务器上安装AEM Forms Workspace的开发包。 有关 [创建开发包的说明](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，请参阅开发包。
1. 通过访问，以管理员身份登录到CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 复制节点位于/content，粘贴于/content。 将节点重命名为ws2。 单击“ **[!UICONTROL 全部保存]**”。 在此节点的属性中，将值更 `sling:resourceType` 改为ws2。 单击“ **[!UICONTROL 全部保存]**”。

1. 从/libs复制文件夹，然后粘贴到/apps。 将文件夹重命名为ws2。 单击“ **[!UICONTROL 全部保存]**”。
1. 在 `GET.jsp` 中， `/apps/ws2`进行以下代码更改。 替换以下内容

   ```
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

   代码

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 中， `/apps/ws2/js`更改模板路径以引用位于的模板 `/apps/ws2/js/runtime/templates`。 替换以下代码

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

   代码

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

1. 在 `userinfo.js` at和 `/apps/ws2/js/runtime/models` 中，将字 `/apps/ws2/js/runtime/views`符串更改为 `/lc/content/ws``lc/content/ws2`。

1. 在中， `/apps/ws2/js/runtime/services/service.js`将函数中的路径 `getLocalizationData` 更改为指向 `/lc/apps/ws2/Locale.html`。

1. 要引用新 `pdf.html` 的Workspace，请更改中的路 `pdf.html` 径 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`。

1. 要引用新 `pdf.html` 的工作区，请更改路径、中、中和中的路径，以及 `pdf.html` 在中的路 `WsNextAdapter.swf` 径 `startprocess.html``taskdetails.html``processinstancehistory.html``/apps/ws2/js/runtime/templates`。

1. 复制文 `/etc/map/ws` 件夹并粘贴到 `/etc/map`。 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在的属 `ws2`性中，将值更 `sling:redirect` 改为 `content/ws2`。

1. 将值更 `sling:match` 改为 `^[^/\||]/[^/\||]/ws2$`。
