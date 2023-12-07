---
title: 了解文件夹结构
description: 如何了解要自定义的AEM Forms工作区源代码的文件夹结构。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 了解文件夹结构 {#understanding-the-folder-structure}

AEM Forms工作区组件使用骨干在MVC架构上设计。 每个组件都有一个文件，用于：

* 模型，其中包含业务逻辑。
* 模板，即包含接口控件的HTML文件。
* 视图，充当模板的Controller类。

所有组件的资产都放置在如下所述的文件夹结构中。 要访问资源，请登录CRXDE Lite并浏览 `/libs/ws/js/runtime/`.

**模型** 包含主干模型。

**查看次数** 包含主干视图。

**模板** 仅包含组件的HTML模板。

**路由** 包含通用路由。 路由中的Templates文件夹包含HTML代码和对组件的引用。

**服务** 包含用于在REST端点上调用Adobe Experience Manager服务器API的服务接口。

**直到** 包含可供多个组件使用的通用实用程序。
