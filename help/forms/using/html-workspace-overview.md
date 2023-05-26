---
title: 使用AEM Forms工作区
seo-title: Working with AEM Forms workspace
description: 通过此流程工作流的快速概述开始使用AEM Forms工作区。
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 使用AEM Forms工作区{#working-with-aem-forms-workspace}

## 简介 {#introduction}

AEM Forms工作区是AEM Forms的一部分。 除了PDF forms之外，工作区还方便了HTMLForms的演绎版。 现在，您可以从移动界面和Web应用程序参与业务流程。

此外，AEM Forms工作区可使用标准HTML和JavaScript™开发方法高度自定义。 它是一个基于组件的软件，可以轻松与其他Web应用程序集成。

有关更多信息，请参阅 [AEM Forms工作区简介](/help/forms/using/introduction-html-workspace.md).

## 熟悉 {#getting-familiar}

要熟悉创建表单应用程序以自动化业务流程的端到端过程，请按照以下步骤进行操作。 在逐步演示之后，您可以使用Workbench、Designer和AEM Forms Workspace创建、管理和测试应用程序。 有关实施详细信息，请参阅 [创建您的第一个AEM Forms应用程序](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## 功能概述 {#functional-overview}

您可以使用AEM Forms工作区执行以下任务：

**启动业务流程：** AEM Forms工作区根据贵组织设计和设置对您的流程进行分类。 您可以收藏常用类别以快速访问类别。 启动流程时，通常会填写表单以启动构成工作流控制的业务流程。 有关更多信息，请参阅 [启动进程](/help/forms/using/starting-processes.md).

**查看任务并执行任务：** 在查看待办事项列表时，您会看到业务流程中分配给您、您所属的任何组或其他用户的共享任务的任务。 您可以根据需要打开、处理和完成任务。 通常，完成任务需要提供信息、批准表单或拒绝表单。 有关更多信息，请参阅 [使用待办事项列表](/help/forms/using/todo-lists.md).

**跟踪任务**：要跟踪您的任务，请使用AEM Forms工作区的“跟踪”选项卡。 您可以搜索已启动或参与的活动或已完成的流程。 您可以查看属于该流程一部分的任务、分配和表单。 您还可以使用之前启动的流程的表单数据启动新流程。 有关更多信息，请参阅 [跟踪流程](/help/forms/using/tracking-processes.md).

## AEM Forms工作区的新增功能 {#new-offering-of-aem-forms-workspace}

**支持批量审批任务**：

您可以批准同一类型的多个任务。 选择一个任务进行审批后，将只启用具有相同流程、相同任务名称和相同路由选项的任务。 参见 [使用待办事项列表](/help/forms/using/todo-lists.md) 以了解实施详细信息。

## 从Flex工作区迁移到AEM Forms工作区 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms客户不支持Flex Workspace。 所有使用Flex工作区的客户都应迁移到AEM Forms工作区。

在AEM Forms工作区中，与XDP表单关联的默认操作配置文件中的默认渲染和提交服务已更改，并且引入了新服务。 有关详细信息，请参阅 [新渲染和提交服务](/help/forms/using/new-render-submit-service.md). 要迁移使用XDP表单的现有流程，并充分利用这些服务，您可以遵循 [这些步骤](new-render-submit-service.md).

**将Flex工作区自定义项与AEM Forms工作区映射**

两个工作区中各种自定义项之间的映射如下所示。

<table>
 <tbody>
  <tr>
   <td><strong>自定义类型 </strong></td>
   <td><strong>自定义项已覆盖 </strong></td>
   <td><strong>相应的AEM Forms工作区自定义方案</strong></td>
  </tr>
  <tr>
   <td>本地化自定义</td>
   <td>
    <ol>
     <li>更改工作区的区域设置</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">更改AEM Forms工作区区域设置</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>主题自定义</td>
   <td>
    <ol>
     <li>替换图像</li>
     <li>修改颜色</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">更改组织徽标</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">更改颜色方案</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>布局自定义</td>
   <td>
    <ol>
     <li>简化工作区用户界面<br /> </li>
     <li>创建新的登录屏幕</li>
     <li>创建自定义审批容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重用组件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">创建新的登录屏幕</a></li>
     <li>审批容器已弃用。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Flex Workspace中提供的AEM Forms Workspace的一些功能包括：消息和通知、欢迎页面、审批容器以及管理列标题的选项。 有关完整列表，请参阅 [Flex工作区中的功能在AEM Forms工作区中不可用](/help/forms/using/features-flex-workspace-available-html.md).

## 使用AEM Forms工作区进行开发 {#developing-with-aem-forms-workspace}

### 架构 {#architecture}

AEM Forms工作区是托管在CRX™上的基于HTML和JavaScript™的Web应用程序。 在浏览器中打开Workspace URL时，将访问CRX™资源，并且应用程序将在浏览器中呈现为HTML页。 JavaScript库和自定义JavaScript代码管理应用程序的内部和外部行为，例如用户界面、用户交互和与AEM Forms服务器的通信。 有关更多详细信息，请参阅AEM Forms工作区 [体系结构](/help/forms/using/html-workspace-architecture.md).

### AEM Forms工作区自定义 {#aem-forms-workspace-customization}

AEM Forms工作区支持各种自定义设置，以更新用户界面的布局、外观、功能等。 自定义项涉及更新以下一项或多项内容：

* 用户界面的外观
* 使用语义自定义的功能
* 在其他Web应用程序中重用HTML组件

此 [自定义](introduction-customizing-html-workspace.md#types-of-customizations) 文章说明了此类自定义的类型。

### 设置开发人员环境 {#set-up-the-developer-environment}

AEM Forms工作区交付件包括部署在CRX上的CRX包、包含完整源代码的SDK档案、第三方JavaScript库和AEM Forms工作区的构建脚本。 使用这些选项设置开发人员环境以执行上述自定义设置。 有关更多详细信息，请参阅 [构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code).

您可以自定义界面和核心功能的主要部分，如字体、颜色方案、徽标、登录屏幕、错误对话框、与第三方应用程序的集成以及第三方应用程序中组件的重用。 您还可以增强“任务摘要”页面上显示的内容，显示任务路由操作的图像，甚至修改用于创建AEM Forms工作区应用程序的低级骨干模型和视图。

### XDP Forms的HTML渲染 {#html-rendering-of-xdp-forms}

默认情况下，对于新流程，XDP表单在桌面上以PDF格式呈现，在平板电脑上以HTML格式呈现。 可以始终以HTML格式渲染XDP表单。 有关详细信息，请参阅 [新的渲染和提交服务](/help/forms/using/new-render-submit-service.md).

[移动设备Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 功能，适用于 [用户档案](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)，支持XDP表单的HTML演绎版。 默认情况下，“渲染新HTML表单”使用 `default.html` 个人资料，您可以对其进行更改。 您还可以添加在以HTML格式呈现XDP表单之前发生的自定义更改。

## AEM Forms工作区应用程序 {#aem-forms-workspace-app}

要在移动设备上处理业务流程，您可以使用AEM Forms的AEM Forms工作区应用程序产品。 欲了解更多信息，请参见 [AEM Forms工作区应用程序概述](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
