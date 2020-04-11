---
title: 骨干交互
seo-title: 骨干交互
description: 有关在AEM Forms工作区中使用Backbone JavaScript模型的概念性信息。
seo-description: 有关在AEM Forms工作区中使用Backbone JavaScript模型的概念性信息。
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 骨干交互{#backbone-interaction}

Backbone是一个库，它有助于在Web应用程序中创建和遵循MVC架构。 Backbone的基本思想是将您的界面组织到逻辑视图中，由模型支持，每个模型在模型更改时都可以单独更新，而无需重绘页面。 有关Backbone的详细信息，请参 [阅https://backbonejs.org](https://backbonejs.org/)。

主要概念如下：

**骨干模型** ，包含数据以及与这些数据相关的大多数逻辑。

**骨干视图** -用于表示相应模型的状态。 骨干视图实际上就像控制器一样，监听用户单击等用户界面事件，或者模型事件（如数据更改），并根据需要修改用户界面。

**HTML模板** ：包装器模板，其占位符由模型填充。

**AEM Forms工作区** ，包含多个单独的组件。 每个组件：

* 表示单个逻辑用户界面元素。
* 可以是类似组件的集合。
* 由Backbone模型、Backbone视图和HTML模板组成。
* 包含对服务的引用。
* 包含对必需实用程序的引用。

初始化组件时，会创建以下对象：

* 将为组件创建Backbone模型的新实例。 服务会注入模型中。
* 将创建Backbone视图的新实例。
* 相应模型、HTML模板和实用程序的实例将插入视图。

在骨干视图中，有一个事件映射，它映射由于用户界面与相应处理程序交互而可能产生的各种事件。 在初始化组件后将启动此映射。

当视图初始化时，视图调用其相应的模型从服务器获取数据。 视图所需的所有数据可用后，视图将以HTML模板指定的格式呈现数据。 多个视图可以共享同一模型进行通信。

![](do-not-localize/aem_forms_workflow.png)

示例：

1. 用户单击任务列表中的任务模板。
1. 任务视图监听单击，并调用任务模型上的渲染函数。
1. 任务模型随后调用服务，该服务是与AEM Forms服务器进行所有通信的公用点。
1. 服务类通过ajax调用AEM Forms REST端点以呈现方法。
1. 此Ajax调用的成功回调在任务模型中定义。
1. 任务模型将骨干事件作为渲染调用完成的通知。
1. 另一个视图,任务详细信息视图监听来自任务模型的此事件。
1. 任务详细信息视图会更改任务详细信息模板，以向用户显示渲染的任务（表单、详细信息、附件、附注等）。
