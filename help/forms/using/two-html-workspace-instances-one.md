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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 在一台服务器上承载两个AEM Forms工作区实例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的默认安装和设置只允许在服务器上提供一个AEM Forms工作区。 但是，您可能需要在一个AEM Forms服务器上承载两个不同的AEM Forms工作区实例。 两个实例可通过不同的URL访问。

AEM Forms管理员可以自定义工作区，以创建两个不同的URL并使两个工作区在同一服务器上可用。 在此自定义文章中，我们假定两个工作区可在 `https://'[server]:[port]'/lc/ws` 和访 `https://'[server]:[port]':/lc/ws2`问。

按照以下步骤配置AEM Forms工作区。

1. 在您的服务器上安装AEM Forms工作区的开发包。 有关 [创建开发包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，请参阅开发包。
1. 通过访问以管理员身份登录CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 复制节点在/content处，粘贴在/content处。 将节点重命名为ws2。 单击“ **[!UICONTROL 全部保存]**”。 在此节点的属性中，将值 `sling:resourceType` 更改为ws2。 单击“ **[!UICONTROL 全部保存]**”。

1. 从/libs复制文件夹ws并粘贴到/apps。 将文件夹重命名为ws2。 单击“ **[!UICONTROL 全部保存]**”。
1. 在 `GET.jsp` 中， `/apps/ws2`进行以下代码更改。 替换以下内容

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

   代码

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 的 `/apps/ws2/js`中，更改模板的路径以引用模板 `/apps/ws2/js/runtime/templates`。 替换以下代码

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

1. 在 `userinfo.js` at `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`中，将字符串 `/lc/content/ws` 更改为 `lc/content/ws2`。

1. 在 `/apps/ws2/js/runtime/services/service.js`中，将函数中的 `getLocalizationData` 路径更改为指向 `/lc/apps/ws2/Locale.html`。

1. 要引用 `pdf.html` 新工作区的路径，请更改 `pdf.html` 中的路 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`径。

1. 要引用 `pdf.html` 新的Workspace，请更改 `pdf.html` 、中、 `WsNextAdapter.swf` 和的路 `startprocess.html`径 `taskdetails.html``processinstancehistory.html``/apps/ws2/js/runtime/templates`。

1. 复制文 `/etc/map/ws` 件夹并粘贴到 `/etc/map`。 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在的属性 `ws2`中，将值 `sling:redirect` 更改为 `content/ws2`。

1. 将值更 `sling:match` 改为 `^[^/\||]/[^/\||]/ws2$`。
