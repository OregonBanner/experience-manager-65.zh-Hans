---
title: AEM Forms工作区快速入门
seo-title: Getting started with AEM Forms workspace
description: 如何开始使用LiveCycleAEM Forms工作区来管理您的业务自动化流程。
seo-description: How to get started with using the LiveCycle AEM Forms workspace to manage your business automation processes.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# AEM Forms工作区快速入门 {#getting-started-with-aem-forms-workspace}

您可以使用AEM Forms工作区执行以下任务：

* 启动业务流程
* 查看分配给您或您有权访问的其他待办事项列表的任务并对其执行操作
* 跟踪属于您启动或参与的流程的任务

## 在AEM Forms工作区中导航 {#navigating-html-workspace}

根据您正在处理的流程和任务，AEM Forms工作区用户界面中会显示不同的项目。 您可能会看到，也可能不会看到“摘要”、“Forms”、“详细信息”、“历史记录”、“附件”或“注释”选项卡，或本帮助中介绍的所有按钮。

您可以使用以下任一方法在AEM Forms工作区主用户界面中导航：

* 单击顶部导航栏中的项目可访问“启动流程”、“待办事项列表”、“首选项”、“跟踪”、“帮助”和“注销”选项。
* 单击“启动流程”、“待办事项”或“跟踪”选项卡以访问三个主要工作区。
* 在“启动流程”、“待办事项”和“跟踪”选项卡中，单击左侧面板中列表上的项目以访问收藏夹、流程类别、搜索模板、草稿或已分配任务。 使用滚动条查看列表中的其他项目。
* 所有操作按钮（“批准”、“拒绝”、“转发”、“咨询”、“锁定”和“共享”）都显示在文档和所有权中。
* 单击页面底部导航栏中的“所有选项”图标，将任务转发给另一个用户，与另一个用户共享任务，与另一个用户协商任务或锁定任务。
* 在“历史记录”选项卡上，选择一个任务以显示该任务的“附件”和“工作总揽”选项卡。
* 使用Tab键、箭头键和空格键可在AEM Forms工作区中导航，而无需使用鼠标。

## 将AEM Forms工作区与屏幕阅读器结合使用 {#using-html-workspace-with-screen-readers}

AEM Forms workspace是基于Web的HTML应用程序，与屏幕阅读器兼容。 您可以使用键盘在AEM Forms工作区界面中导航。

要将AEM Forms工作区与屏幕阅读器结合使用，请记住以下几点：

* AEM Forms工作区是一个符合任何标准屏幕阅读器工具的标准HTML应用程序。 无需任何特定脚本即可运行屏幕阅读器工具。
* AEM Forms工作区中的所有导航都通过锚点标记进行，通过选项卡可轻松访问这些标记。
* 加载Forms可能需要几秒钟的时间。 屏幕阅读器不会通过声音通知您表单正在加载且您必须等待。

## 使用键盘导航AEM Forms工作区 {#navigating-html-workspace-using-a-keyboard}

使用键盘导航AEM Forms工作区时，导航遵循HTML辅助功能惯例。 在某些情况下，Tab键顺序不遵循典型的常规顺序。 以下提示可帮助您导航界面：

* 如果在浏览器顶部的工具栏上执行Tab键时出现问题，请按Ctrl+Tab键以进入浏览器窗口的内容。
* AEM Forms工作区帮助会在单独的浏览器窗口中打开。 查看帮助后，焦点将返回到包含AEM Forms工作区的浏览器窗口。 当焦点返回时，“帮助”菜单将保持焦点。
* 打开表单以启动流程或完成任务时，焦点仍然位于现有元素中，并且不会更改为表单。 使用选项卡将焦点移动到表单并在表单中浏览。 在表单中Tab键顺序取决于表单的类型和设计。

  对于PDF forms，当您通过选项卡进入表单的结尾或提交表单时，光标焦点会跳转到浏览器的地址栏。 再次通过菜单（而不是整个表单）按Tab键转到表单操作按钮，如“另存为草稿”和“完成”。 如果表单仍处于打开状态，您还可以通过按钮跳转到表单中。

## 管理首选项 {#managing-preferences}

您可以在以下类别中设置各种AEM Forms工作区首选项：

**外出：** 设置首选项以控制在您外出时如何将任务分配给其他人。 请参阅 [设置外出首选项](todo-lists.md#setting-out-of-office-preferences).

**队列：** 设置首选项以与其他用户共享您的待办事项列表或请求访问其他用户的列表。 请参阅 [处理组和共享队列中的任务](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**UI设置：** 设置首选项，了解如何与AEM Forms工作区交互。 请参阅 [设置用户界面首选项](#set-user-interface-preferences).

### 设置用户界面首选项 {#set-user-interface-preferences}

在“首选项”>“UI设置”选项卡中设置用户界面首选项。 以下首选项可用。

* **起始位置：** 指定登录到AEM Forms工作区时显示的页面。 四个可用选项为“启动进程”、“待办事项”、“跟踪”和“收藏夹”。
* **注销提示：** 指定在单击“注销”后，是否提示您确认要注销。
* **日期格式：** 指定在AEM Forms工作区中使用的日期显示格式。
* **时间格式**：指定在AEM Forms工作区中使用的时间显示格式。
* **通过电子邮件通知任务事件：** 指定您是否收到任务事件的电子邮件通知，包括任务分配、提醒以及任务在待办事项列表和您所属的待办事项组中的截止日期。
* **在电子邮件中附加Forms：** 指定是否将表单副本附加到电子邮件通知消息。 仅支持PDF和XDP表单的附件。
* **定期保存草稿：** 指定是否定期自动保存表单草稿。 要定期保存草稿，请启用此选项，并将自动保存持续时间设置为1到30分钟。 当启用了自动保存并且用户正在处理草稿时，将在指定的分钟数后定期保存草稿。 仅当自上次保存或自动保存以来草稿中有更改时，才会自动保存草稿。 保存草稿后，屏幕上将显示一条警告消息。
