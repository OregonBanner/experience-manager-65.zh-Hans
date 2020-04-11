---
title: 使用AEM Forms工作区
seo-title: 使用AEM Forms工作区
description: 通过此流程工作流的快速概述，开始使用AEM Forms工作区。
seo-description: 通过此流程工作流的快速概述，开始使用AEM Forms工作区。
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Working with AEM Forms workspace{#working-with-aem-forms-workspace}

## 简介 {#introduction}

AEM Forms工作区是AEM Forms的一部分。 Workspace除了便于再现PDF表单外，还便于再现HTML表单。 现在，您可以从移动界面和Web应用程序中参与业务流程。

此外，AEM Forms工作区可使用标准HTML和JavaScript™开发方法进行高度自定义。 它是基于组件的软件，可轻松与您的其他Web应用程序集成。

有关详细信息，请参 [阅AEM Forms工作区简介](/help/forms/using/introduction-html-workspace.md)。

## 熟悉 {#getting-familiar}

要熟悉创建表单应用程序以实现业务流程自动化的端到端流程，请遵循演练。 完成演练后，您可以使用Workbench、Designer和AEM Forms工作区创建、管理和测试应用程序。 有关实施详细信息，请 [参阅创建您的第一个AEM Forms应用程序](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概述 {#functional-overview}

您可以使用AEM Forms工作区执行以下任务:

**开始业务流程：** AEM Forms工作区按照您的组织设计和设置的流程进行类别。 您可以喜欢常用的类别以快速访问类别。 在开始流程时，通常需要填写表单以开始表单工作流程控制的业务流程。 有关详细信息，请参阅 [启动进程](/help/forms/using/starting-processes.md)。

**视图并依据任务:** 视图待办事项列表时，您会看到业务流程中分配给您的任务，或分配给您所属的任何组，或者您是其他用户的共享任务。 您可以根据需要打开、处理和完成任务。 通常，完成任务涉及提供信息、批准表单或拒绝表单。 有关详细信息，请 [参阅使用待办事项列表](/help/forms/using/todo-lists.md)。

**跟踪任务**:要跟踪任务，请使用AEM Forms工作区的“跟踪”选项卡。 您可以搜索已启动或参与的活动或已完成进程。 您可以视图属于流程的任务、任务和表单。 您还可以使用先前启动的进程中的表单数据开始新进程。 有关详细信息，请参阅 [跟踪进程](/help/forms/using/tracking-processes.md)。

## AEM Forms工作区的新增功能 {#new-offering-of-aem-forms-workspace}

**支持批量批准任务**:

您可以批准同一类型的多个任务。 选择一个任务进行批准后，将仅启用具有相同流程、相同任务名和相同路由选项的任务。 有关 [实施详细信息，请参阅使用待办列表](/help/forms/using/todo-lists.md) 。

## 从Flex Workspace迁移到AEM Forms工作区 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms客户不支持Flex Workspace。 所有使用Flex Workspace的客户都应转到AEM Forms Workspace。

在AEM Forms工作区中，与XDP表单关联的默认渲染和提交服务在默认操作用户档案中已更改，并且已引入新服务。 有关详细信息，请参 [阅新建渲染和提交服务](/help/forms/using/new-render-submit-service.md)。 要迁移使用XDP表单的现有流程，以利用这些服务，您可以执行以 [下步骤](/help/forms/using/new-render-submit-service.md#main-pars-faq)。

**将Flex Workspace自定义与AEM Forms Workspace映射**

两个工作区中各种类型的自定义之间的映射如下所示。

<table>
 <tbody>
  <tr>
   <td><strong>自定义类型 </strong></td>
   <td><strong>涵盖的自定义 </strong></td>
   <td><strong>相应的AEM Forms工作区自定义方案</strong></td>
  </tr>
  <tr>
   <td>本地化自定义</td>
   <td>
    <ol>
     <li>更改工作区区域设置</li>
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
     <li>创建新登录屏幕</li>
     <li>创建自定义批准容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重用组件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">创建新的登录屏幕</a></li>
     <li>已弃用批准容器。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Flex Workspace的某些功能在AEM Forms工作区中不可用，包括：消息和通知、欢迎页面、批准容器以及用于管理列标题的选项。 有关完整的列表，请参 [阅Flex Workspace的功能（AEM Forms工作区中不提供）](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作区进行开发 {#developing-with-aem-forms-workspace}

### 架构 {#architecture}

AEM Forms工作区是基于HTML和JavaScript™的Web应用程序，托管在CRX™上。 在浏览器中打开Workspace URL时，将访问CRX™资源，并在浏览器中将应用程序呈现为HTML页。 JavaScript库和自定义JavaScript代码管理应用程序的内部和外部行为，如用户界面、用户交互以及与AEM Forms服务器的通信。 有关详细信息，请参阅AEM Forms工作区架 [构](/help/forms/using/html-workspace-architecture.md)。

### AEM Forms工作区自定义 {#aem-forms-workspace-customization}

AEM Forms工作区支持各种自定义，以更新用户界面的布局、其外观和功能等。 这些自定义包括更新以下一项或多项内容：

* 用户界面的外观
* 使用语义自定义的功能
* 在其他Web应用程序中重用HTML组件

自定 [义文章](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-0) 介绍了此类自定义的类型。

### Set up the developer environment {#set-up-the-developer-environment}

AEM Forms工作区交付内容包括部署在CRX上的CRX包、包含完整源代码的SDK存档、第三方JavaScript库以及AEM Forms工作区的构建脚本。 使用这些设置设置开发人员环境以执行上述自定义。 有关详细信息，请参 [阅构建AEM Forms工作区代码](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)。

您可以自定义界面和核心功能的主要部分，如字体、颜色方案、徽标、登录屏幕、错误对话框、与第三方应用程序的集成以及第三方应用程序中组件的重用。 您还可以增强“任务摘要”页面上显示的内容，显示用于任务路由操作的图像，甚至可以修改创建AEM Forms工作区应用程序的低级骨干模型和视图。

### XDP表单的HTML渲染 {#html-rendering-of-xdp-forms}

默认情况下，对于新流程，XDP表单在桌面上以PDF格式呈现，在平板电脑上以HTML格式呈现。 始终可以以HTML格式呈现XDP表单。 有关详细信息，请参 [阅新的渲染和提交服务](/help/forms/using/new-render-submit-service.md)。

[可与用户档案一起使用的移](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 动表单 [](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)，该功能支持XDP表单的HTML再现。 默认情况下，“渲染新HTML表单”使用 `default.html` 用户档案，您可以更改它。 您还可以添加在以HTML格式呈现XDP表单之前发生的自定义更改。

## AEM Forms工作区应用程序 {#aem-forms-workspace-app}

要在移动设备上处理业务流程，您可以使用AEM Forms的AEM Forms工作区应用程序产品。 有关详细信息，请参阅 [AEM Forms工作区应用程序概述](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)。
