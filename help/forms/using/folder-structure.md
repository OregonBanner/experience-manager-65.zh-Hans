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
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 了解文件夹结构 {#understanding-the-folder-structure}

AEM Forms工作区组件是使用Backbone在MVC架构上设计的。 每个组件都有一个文件，用于：

* 模型，它包含业务逻辑。
* 模板，即包含界面控件的HTML文件。
* 视图，它充当Template的Controller类。

所有组件的资产都放置在下面描述的文件夹结构中。 要访问资产，请登录CRXDE Lite并浏览至 `/libs/ws/js/runtime/`。

**型号** ，包含骨干型号。

**视图** ，包含骨干视图。

**模板** 仅包含组件的HTML模板。

**路由** Contains universal routes. 路由中的模板文件夹包含HTML代码和对组件的引用。

**服务** 包含用于在REST端点上调用Adobe Experience Manager服务器API的服务界面。

**util** 包含可由多个组件使用的通用实用程序。
