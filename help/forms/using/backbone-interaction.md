---
title: 骨干互动
seo-title: 骨干互动
description: 有关在AEM Forms工作区中使用骨干JavaScript模型的概念信息。
seo-description: 有关在AEM Forms工作区中使用骨干JavaScript模型的概念信息。
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 骨干互动{#backbone-interaction}

Backbone是一个库，可帮助在Web应用程序中创建和遵循MVC架构。 Backbone的基本思想是将您的界面组织成逻辑视图，并由模型支持，每个模型在模型更改时都可以独立更新，而无需重绘页面。 有关Backbone的详细信息，请参阅[https://backbonejs.org](https://backbonejs.org/)。

一些关键概念如下：

**骨干** 模型包含数据，以及与此数据相关的大多数逻辑。

**骨干** 视图用于表示相应模型的状态。骨干视图实际上像控制器一样，监听用户点击等用户界面事件，或模拟事件（如数据更改），并根据需要修改用户界面。

**HTML模** 板（HTML模板）包装模板，其占位符由模型填充。

**AEM Forms工** 作区包含多个单独的组件。每个组件：

* 表示单个逻辑用户界面元素。
* 可以是类似组件的集合。
* 由骨干模型、骨干视图和HTML模板组成。
* 包含对服务的引用。
* 包含对所需实用工具的引用。

初始化组件时，会创建以下对象：

* 将创建组件的骨干模型的新实例。 服务将插入模型中。
* 将创建Backbone视图的新实例。
* 相应模型、HTML模板和实用程序的实例将插入到视图中。

在骨干视图中，有一个事件映射，它映射由于用户界面与相应处理程序的交互而可能出现的各种事件。 初始化组件后，将启动此映射。

初始化视图时，视图会调用其相应的模型以从服务器获取数据。 视图所需的所有数据都可用后，视图会以HTML模板指定的格式呈现数据。 多个视图可以共享同一模型进行通信。

![](do-not-localize/aem_forms_workflow.png)

示例：

1. 用户单击任务列表中的任务模板。
1. 任务视图侦听点击，并在任务模型上调用呈现函数。
1. 任务模型随后调用服务，该服务是与AEM Forms服务器进行所有通信的公共点。
1. 服务类通过ajax为呈现方法调用AEM Forms REST端点。
1. 此Ajax调用的成功回调在任务模型中定义。
1. 任务模型在呈现调用完成的通知中引发骨干事件。
1. 另一个视图，任务详细信息视图从任务模型侦听此事件。
1. 然后，“任务详细信息”视图会更改任务详细信息模板，以向用户显示已呈现的任务（表单、详细信息、附件、注释等）。
