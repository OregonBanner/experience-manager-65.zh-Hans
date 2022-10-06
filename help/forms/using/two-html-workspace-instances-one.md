---
title: 在一个服务器上托管两个AEM Forms工作区实例
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC管理员如何可以自定义HTMLWS，以在可通过不同URL访问的单个服务器上托管两个实例。
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

# 在一个服务器上托管两个AEM Forms工作区实例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的默认安装和设置只允许在服务器上提供一个AEM Forms工作区。 但是，您可能需要在单个AEM Forms服务器上托管两个不同的AEM Forms工作区实例。 两个实例可通过不同的URL访问。

AEM Forms管理员可自定义工作区以创建两个不同的URL，并在同一服务器上提供两个工作区。 在此自定义文章中，我们假定两个工作区可在 `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`.

按照以下步骤配置AEM Forms工作区。

1. 在您的服务器上安装AEM Forms工作区的开发包。 请参阅 [开发包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以获取创建该报表包的说明。
1. 以管理员身份登录CRXDE Lite，访问 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 在/content处复制节点，然后在/content处粘贴。 将节点重命名为ws2。 单击 **[!UICONTROL 全部保存]**. 在此节点的属性中，更改 `sling:resourceType` 到ws2。 单击 **[!UICONTROL 全部保存]**.

1. 从/libs复制文件夹，然后粘贴到/apps。 将文件夹重命名为ws2。 单击 **[!UICONTROL 全部保存]**.
1. 在 `GET.jsp` at `/apps/ws2`，请更改以下代码。 替换以下内容

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

   使用以下代码

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` at `/apps/ws2/js`，请更改模板路径以在 `/apps/ws2/js/runtime/templates`. 替换以下代码

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

   使用以下代码

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

1. 在 `userinfo.js` at `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，更改字符串 `/lc/content/ws` to `lc/content/ws2`.

1. 在 `/apps/ws2/js/runtime/services/service.js`，请在 `getLocalizationData` 函数指向 `/lc/apps/ws2/Locale.html`.

1. 请参阅 `pdf.html` ，请更改 `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 请参阅 `pdf.html` ，请更改 `pdf.html` 和 `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`和 `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`.

1. 复制 `/etc/map/ws` 文件夹和粘贴位置 `/etc/map`. 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在的属性中 `ws2`，更改值 `sling:redirect` to `content/ws2`.

1. 更改值 `sling:match` to `^[^/\||]/[^/\||]/ws2$`.
