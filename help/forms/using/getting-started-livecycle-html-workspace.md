---
title: AEM Forms工作区入门
seo-title: AEM Forms工作区入门
description: 如何开始使用LiveCycleAEM Forms工作区管理业务自动化流程。
seo-description: 如何开始使用LiveCycleAEM Forms工作区管理业务自动化流程。
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---


# AEM Forms工作区{#getting-started-with-aem-forms-workspace}快速入门

您可以使用AEM Forms工作区执行以下任务:

* 开始业务流程
* 视图并对分配给您或您有权访问的其他待办列表的任务采取行动
* 跟踪属于您启动或参与的流程的任务

## 导航AEM Forms工作区{#navigating-html-workspace}

AEM Forms工作区用户界面中显示的不同项目取决于您正在处理的过程和任务。 您始终可能看不到“摘要”、“Forms”、“详细信息”、“历史记录”、“附件”或“备注”选项卡，或者看不到本“帮助”中描述的所有按钮。

您可以使用以下任意方法导航主AEM Forms工作区用户界面：

* 单击顶部导航栏中的项目以访问开始进程、待办列表、首选项、跟踪、帮助和注销选项。
* 单击“开始进程”、“待办事项”或“跟踪”选项卡以访问三个主要工作区域。
* 在“开始流程”、“待办事项”和“跟踪”选项卡上，单击左侧面板列表上的项目以访问收藏夹、处理类别、搜索模板、草稿或分配的任务。 使用滚动条在列表中查看其他项目。
* 所有操作按钮（批准、拒绝、转发、咨询、锁定和共享）都显示在文档和所有权中。
* 单击页面底部导航栏中的“所有选项”图标，将任务转发给其他用户，与其他用户共享任务，与其他用户协商任务，或锁定任务。
* 在“历史记录”选项卡上，选择一个任务以显示该任务的“附件”和“分配”选项卡。
* 使用Tab键、箭头键和空格键在AEM Forms工作区中导航，无需使用鼠标。

## 将AEM Forms工作区与屏幕阅读器{#using-html-workspace-with-screen-readers}一起使用

AEM Forms工作区是一个基于Web的HTML应用程序，与屏幕阅读器兼容。 您可以使用键盘在AEM Forms工作区界面中导航。

要将AEM Forms工作区与屏幕阅读器结合使用，请记住以下几点：

* AEM Forms工作区是符合任何标准屏幕阅读器工具的标准HTML应用程序。 运行屏幕阅读器工具不需要任何特定脚本。
* AEM Forms工作区中的所有导航都通过锚点标签进行，锚点标签可以通过选项卡轻松访问。
* Forms需要几秒钟才能加载。 屏幕阅读器不会有声地通知您正在加载表单，您必须等待。

## 使用键盘{#navigating-html-workspace-using-a-keyboard}导航AEM Forms工作区

当您使用键盘导航AEM Forms工作区时，导航符合HTML辅助工具惯例。 在某些情况下，跳位顺序不遵循典型的常规顺序。 以下提示可帮助您导航界面：

* 如果在浏览器顶部的工具栏外切换时遇到问题，请按Ctrl+Tab键以跳入浏览器窗口的内容。
* AEM Forms工作区帮助在单独的浏览器窗口中打开。 视图帮助后，焦点将返回到包含AEM Forms工作区的浏览器窗口。 当焦点返回时，“帮助”菜单仍保持焦点。
* 打开表单以开始流程或完成任务时，焦点将保留在现有元素中，而不会更改为表单。 使用选项卡将焦点移到表单并浏览表单。 在表单中按下Tab键顺序取决于表单的类型和设计。

   对于PDF forms，当您跳转到表单结尾或提交表单时，光标焦点将跳转到浏览器地址栏。 您必须再次在菜单（而非整个表单）间切换，才能转到表单操作按钮，如“另存为草稿”和“完成”。 如果表单仍处于打开状态，您还可以跳过按钮跳回表单。

## 管理首选项{#managing-preferences}

您可以在以下类别中设置各种AEM Forms工作区首选项：

**外出：设** 置首选项，以控制任务在外出时如何分配给其他人。请参阅[设置办公室外首选项](todo-lists.md#setting-out-of-office-preferences)。

**队列：** 设置用于与其他用户共享待办列表或请求访问其他用户列表的首选项。请参阅[使用组和共享队列中的任务](todo-lists.md#working-with-tasks-from-group-and-shared-queues)。

**UI设置：设** 置与AEM Forms工作区交互的首选项。请参阅[设置用户界面首选项](#set-user-interface-preferences)。

### 设置用户界面首选项{#set-user-interface-preferences}

在“首选项”>“UI设置”选项卡中设置用户界面首选项。 提供以下首选项。

* **开始位** 置：指定登录AEM Forms工作区时显示的页面。四个可用选项是“开始流程”、“操作”、“跟踪”和“收藏夹”。
* **注销提示：** 指定在单击“注销”后是否提示您确认要注销。
* **日期格式：指** 定在AEM Forms工作区中使用的日期显示格式。
* **时间格式**:指定在AEM Forms工作区中使用的时间显示格式。
* **通过电子邮件通知任务事件:** 指定您是否收到任务事件的电子邮件通知，包括待办列表和您所属的组待办列表中任务的任务分配、提醒和截止日期。
* **在电子邮件中附加Forms** ：指定表单的副本是否附加到电子邮件通知消息中。附件仅支持PDF和XDP表单。
* **定期保存草稿：** 指定是否定期自动保存表单草稿。要定期保存草稿，请启用此选项，并将自动保存的持续时间从1分钟设置为30分钟。 启用自动保存功能且用户正在处理草稿时，草稿将在指定的分钟数后定期保存。 仅当自上次保存或自动保存后草图发生更改时，草图才自动保存。 保存草稿后，屏幕上将显示一条警报消息。
