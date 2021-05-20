---
title: 了解文件夹结构
seo-title: 了解文件夹结构
description: 如何了解要自定义的AEM Forms工作区源代码的文件夹结构。
seo-description: 如何了解要自定义的AEM Forms工作区源代码的文件夹结构。
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 了解文件夹结构{#understanding-the-folder-structure}

AEM Forms工作区组件是使用Backbone在MVC架构上设计的。 每个组件都有一个用于：

* 模型，其中包含业务逻辑。
* 模板，即包含界面控件的HTML文件。
* 视图，它充当模板的Controller类。

所有组件的资产都放置在下面描述的文件夹结构中。 要访问资产，请登录CRXDE Lite并浏览至`/libs/ws/js/runtime/`。

**** 模型包含骨干模型。

**** 视图包含骨干视图。

**** 模板仅包含组件的HTML模板。

**** routes包含通用路由。路由内的“模板”文件夹包含HTML代码和对组件的引用。

**** services包含用于在REST端点上调用Adobe Experience Manager服务器API的服务接口。

**** utilContains通用实用程序（可由多个组件使用）。
