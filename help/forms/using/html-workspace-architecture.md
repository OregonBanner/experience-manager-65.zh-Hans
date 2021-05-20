---
title: AEM Forms工作区架构
seo-title: AEM Forms工作区架构
description: LiveCycleAEM Forms工作区架构的概念信息和概述。
seo-description: LiveCycleAEM Forms工作区架构的概念信息和概述。
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# AEM Forms工作区架构{#aem-forms-workspace-architecture}

AEM Forms工作区是在CRX™上托管的Web应用程序。 在浏览器中打开工作区时，将访问CRX资源，并在浏览器中将应用程序呈现为HTML页面。

该应用程序在REST端点上访问AEM Forms服务器，以执行以下操作：

* 获取用户任务、进程起点、进程历史记录和用户信息
* 对任务执行操作
* 数据库中的查询任务
* 更新用户首选项等

AEM Forms服务器通过JDBC访问AEM Forms数据库。 数据库会保留任务、进程及其实例、用户和相关信息。

AEM Forms工作区设计为模块化JavaScript™组件，可单独自定义并在其他Web应用程序中重复使用。 这些组件基于BackBone，BackBone是一个JavaScript库，为Web应用程序提供了结构。 [此处](/help/forms/using/backbone-interaction.md)提供了描述组件与BackBone交互的详细文章。 [这篇](/help/forms/using/folder-structure.md)文章中对CRX文件夹结构中的组件组织进行了讨论。

为AEM Forms工作区提供的包：

* `adobe-lc-workspace-pkg-<version>.zip`:它是CRX包，也就是说，可以使用包管理器在CRX中部署它。
* `adobe-lc-workspace-<version>-src.zip`:它是一个存档，其中包含用于创建部署包（发运、调试和开发包）的AEM Forms工作区的完整代码和脚本。
