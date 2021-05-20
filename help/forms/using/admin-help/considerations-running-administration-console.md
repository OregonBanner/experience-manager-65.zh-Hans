---
title: 运行AdministrationConsole时的注意事项
seo-title: 运行AdministrationConsole时的注意事项
description: 本文档列出了运行管理控制台时要考虑的几点。
seo-description: 本文档列出了运行管理控制台时要考虑的几点。
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 运行管理控制台{#considerations-when-running-administrationconsole}时的注意事项

运行管理控制台时，需考虑以下事项：

* 如果使用URL `https://[hostname]:'port'/adminui`访问管理控制台，则指定的主机名不能包含下划线字符。 否则，指向管理控制台某些区域的链接可能无法正常工作。
* 如果在日语版操作系统的Windows资源管理器中运行管理控制台，则可能会遇到以下问题：

   * 单击链接会返回到登录页面，而不是预期链接。
   * 单击链接会显示权限错误。

   最佳做法是从其他浏览器（如Mozilla Firefox）运行管理控制台，以确保无链接失败。

* 在管理控制台中执行搜索时，请勿使用反斜线字符()。
