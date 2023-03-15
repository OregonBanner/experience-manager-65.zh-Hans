---
title: 骨干交互
seo-title: Backbone interaction
description: 有关在AEM Forms工作区中使用骨干JavaScript模型的概念信息。
seo-description: Conceptual information about use of Backbone JavaScript models in AEM Forms workspace.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 骨干交互{#backbone-interaction}

Backbone是一个库，有助于在Web应用程序中创建和遵循MVC架构。 Backbone的基本思想是将界面组织成逻辑视图，由模型支持，每个视图都可以在模型更改时独立更新，而无需重绘页面。 有关主干的详细信息，请参见 [https://backbonejs.org](https://backbonejs.org/).

一些关键概念如下：

**骨干模型** 包含数据以及与此数据相关的大多数逻辑。

**主干视图** 用于表示相应模型的状态。 骨干视图实际上像控制器一样运行，侦听用户界面事件（如用户点击）或为事件建模（如数据更改），并根据需要修改用户界面。

**HTML模板** 具有由模型填充的占位符的包装器模板。

**AEM Forms工作区** 包含多个单独的组件。 每个组件：

* 表示单个逻辑用户界面元素。
* 可以是类似组件的集合。
* 由骨干模型、骨干视图和HTML模板组成。
* 包含对服务的引用。
* 包含对所需实用程序的引用。

初始化组件时，将创建以下对象：

* 为组件创建了骨干模型的新实例。 服务被插入到模型中。
* 已创建新的骨干视图实例。
* 相应模型、HTML模板和实用程序的实例将插入视图中。

在骨干视图中，有一个事件映射，用于映射由于用户界面与相应处理程序的交互而可能产生的各种事件。 初始化组件后，将启动此映射。

初始化视图后，该视图会调用其相应模型以从服务器获取数据。 视图所需的所有数据都可用后，视图将按照HTML模板指定的格式呈现数据。 多个视图可以共享相同的通信模型。

![](do-not-localize/aem_forms_workflow.png)

示例：

1. 用户单击任务列表中的任务模板。
1. 任务视图侦听单击，并调用任务模型上的渲染函数。
1. 任务模型随后调用该服务，该服务是与AEM Forms服务器进行所有通信的共同点。
1. 服务类通过ajax为渲染方法调用AEM Forms REST端点。
1. 此Ajax调用的成功回调在任务模型中定义。
1. 任务模型会引发骨干事件，作为渲染调用完成的通知。
1. 另一个视图，任务详细信息视图从任务模型侦听此事件。
1. 然后，任务详细信息视图会更改任务详细信息模板，以便向用户显示呈现的任务（表单、详细信息、附件、注释等）。
