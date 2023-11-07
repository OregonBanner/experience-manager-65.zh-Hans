---
title: 日志文件
seo-title: Log files
description: 诸如运行时错误或启动错误等事件将记录到应用程序服务器日志文件中，这些文件可以使用任何文本编辑器打开。
seo-description: Events such as run-time or startup errors are recorded to the application server log files, which can be  opened using any text editor.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 日志文件 {#log-files}

诸如运行时错误或启动错误等事件将记录到应用程序服务器日志文件中。 如果在部署到应用程序服务器时遇到任何问题，可以使用日志文件来帮助您查找问题。 您可以使用任何文本编辑器打开日志文件。

(JBoss)以下日志文件位于 `[appserver root]/server/'server'/log` 目录：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)域日志文件位于 `[appserverdomain]` 目录和服务器日志文件位于 `[appserverdomain]/servers/[appserver name]/logs` 目录：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)以下日志文件位于 `[appserver root]/profiles/default/logs/[appserver name]` 目录：

* SystemErr.log
* SystemOut.log
* StartServer.log
