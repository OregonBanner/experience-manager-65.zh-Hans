---
title: AEM Forms工作区架构
seo-title: AEM Forms工作区架构
description: 概念信息和LiveCycleAEM Forms工作区体系结构概述。
seo-description: 概念信息和LiveCycleAEM Forms工作区体系结构概述。
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# AEM Forms工作区体系结构{#aem-forms-workspace-architecture}

AEM Forms工作区是在CRX™上托管的Web应用程序。 在浏览器中打开工作区时，将访问CRX资源，并在浏览器中将应用程序呈现为HTML页。

应用程序访问REST端点上的AEM Forms服务器以执行以下操作：

* 获取用户任务、进程起点、进程历史记录和用户信息
* 对任务执行操作
* 查询任务
* 更新用户首选项等

AEM Forms服务器通过JDBC访问AEM Forms数据库。 数据库保留任务、进程及其实例、用户和相关信息。

AEM Forms工作区设计为模块化的JavaScript™组件，可单独自定义并在其他Web应用程序中重用。 这些组件基于BackBone,BackBone是一个JavaScript库，它为Web应用程序提供结构。 描述组件与BackBone交互的详细文章为[此处](/help/forms/using/backbone-interaction.md)。 在[此](/help/forms/using/folder-structure.md)文章中，将讨论CRX文件夹结构中组件的组织。

为AEM Forms工作区提供的包：

* `adobe-lc-workspace-pkg-<version>.zip`:它是CRX包，即，可以使用包管理器在CRX中部署它。
* `adobe-lc-workspace-<version>-src.zip`:它是一个存档，包含AEM Forms工作区的完整代码和用于创建部署包的脚本——发运、调试和开发包。
