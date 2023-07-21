---
title: 在一台服务器上托管两个AEM Forms工作区实例
description: LC管理员如何自定义HTMLWS，以便在可通过不同URL访问的单个服务器上托管两个实例。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 在一台服务器上托管两个AEM Forms工作区实例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的默认安装和设置只允许一个AEM Forms工作区在服务器上可用。 但是，您可能需要在一台AEM Forms服务器上托管两个不同的AEM Forms工作区实例。 这两个实例可通过不同的URL访问。

AEM Forms管理员自定义工作区，以创建两个不同的URL，并使两个工作区在同一服务器上可用。 在本自定义文章中，您可以假设可以在以下位置访问这两个工作区： `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`.

按照以下步骤配置AEM Forms工作区。

1. 在服务器上安装AEM Forms工作区的开发包。 参见 [开发包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以获取有关创建它的说明。
1. 以管理员身份登录CRXDE Lite，方法是访问 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 在/content处复制节点，并在/content处粘贴。 将节点重命名为ws2。 单击 **[!UICONTROL 全部保存]**. 在此节点的属性中，更改值 `sling:resourceType` 到ws2。 单击 **[!UICONTROL 全部保存]**.

1. 从/libs复制文件夹ws并将其粘贴到/apps。 将文件夹重命名为ws2。 单击 **[!UICONTROL 全部保存]**.
1. In `GET.jsp` 在 `/apps/ws2`，对代码进行以下更改。 替换以下内容

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

   ，代码为

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. In `registry.js` 在 `/apps/ws2/js`，更改模板的路径以引用位于的模板 `/apps/ws2/js/runtime/templates`. 替换以下代码

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

   ，代码为

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

1. In `userinfo.js` 在 `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，更改字符串 `/lc/content/ws` 到 `lc/content/ws2`.

1. In `/apps/ws2/js/runtime/services/service.js`，更改中的路径 `getLocalizationData` 函数指向 `/lc/apps/ws2/Locale.html`.

1. 请参阅 `pdf.html` 的路径，更改 `pdf.html` 在 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 请参阅 `pdf.html` 的路径，更改路径 `pdf.html` 和 `WsNextAdapter.swf` 在 `startprocess.html`， `taskdetails.html`、和 `processinstancehistory.html` 在 `/apps/ws2/js/runtime/templates`.

1. 复制 `/etc/map/ws` 文件夹并粘贴于 `/etc/map`. 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在的属性中 `ws2`，更改值 `sling:redirect` 到 `content/ws2`.

1. 更改值 `sling:match` 到 `^[^/\||]/[^/\||]/ws2$`.
