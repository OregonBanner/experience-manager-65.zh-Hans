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


# 在一台服务器{#hosting-two-aem-forms-workspace-instances-on-one-server}上承载两个AEM Forms工作区实例

AEM Forms的默认安装和设置只允许在服务器上提供一个AEM Forms工作区。 但是，您可能需要在单台AEM Forms服务器上承载两个不同的AEM Forms工作区实例。 两个实例可通过不同的URL访问。

AEM Forms管理员可以自定义工作区，以创建两个不同的URL，并在同一服务器上提供两个工作区。 在此自定义文章中，我们假定两个工作区可在`https://'[server]:[port]'/lc/ws`和`https://'[server]:[port]':/lc/ws2`访问。

按照以下步骤配置AEM Forms工作区。

1. 在您的服务器上安装AEM Forms工作区的开发包。 请参见[dev package](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以获得创建它的说明。
1. 以管理员身份登录CRXDE Lite，访问`https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 复制节点在/content处，粘贴在/content处。 将节点重命名为ws2。 单击&#x200B;**[!UICONTROL 保存全部]**。 在此节点的属性中，将`sling:resourceType`的值更改为ws2。 单击&#x200B;**[!UICONTROL 保存全部]**。

1. 从/libs复制文件夹ws并粘贴到/apps。 将文件夹重命名为ws2。 单击&#x200B;**[!UICONTROL 保存全部]**。
1. 在`GET.jsp`的`/apps/ws2`中，进行以下代码更改。 替换以下内容

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

1. 在`/apps/ws2/js`的`registry.js`中，更改模板路径以引用位于`/apps/ws2/js/runtime/templates`的模板。 替换以下代码

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

1. 在`/apps/ws2/js/runtime/models`和`/apps/ws2/js/runtime/views`的`userinfo.js`中，将字符串`/lc/content/ws`更改为`lc/content/ws2`。

1. 在`/apps/ws2/js/runtime/services/service.js`中，将`getLocalizationData`函数中的路径更改为指向`/lc/apps/ws2/Locale.html`。

1. 要引用新Workspace的`pdf.html`，请更改`/apps/ws2/js/runtime/views/forms/pdftaskform.js`中`pdf.html`的路径。

1. 要引用新Workspace的`pdf.html`，请更改`startprocess.html`、`taskdetails.html`和`processinstancehistory.html`中`pdf.html`和`WsNextAdapter.swf`的路径（位于`/apps/ws2/js/runtime/templates`）。

1. 复制`/etc/map/ws`文件夹并粘贴到`/etc/map`。 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在`ws2`的属性中，将`sling:redirect`的值更改为`content/ws2`。

1. 将值`sling:match`更改为`^[^/\||]/[^/\||]/ws2$`。
