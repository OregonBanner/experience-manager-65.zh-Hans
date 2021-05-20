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
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# 使用AEM Forms工作区{#working-with-aem-forms-workspace}

## 简介 {#introduction}

AEM Forms工作区是AEM Forms的一部分。 工作区可帮助呈现HTML Forms和PDF forms。 现在，您可以通过移动界面和Web应用程序参与业务流程。

此外，AEM Forms工作区可使用标准HTML和JavaScript™开发方法进行高度自定义。 它是一个基于组件的软件，可轻松与您的其他Web应用程序集成。

有关更多信息，请参阅[AEM Forms工作区简介](/help/forms/using/introduction-html-workspace.md)。

## 熟悉{#getting-familiar}

要熟悉创建表单应用程序以实现业务流程自动化的端到端过程，请遵循演练。 在完成演练后，您可以使用Workbench、Designer和AEM Forms工作区创建、管理和测试应用程序。 有关实施详细信息，请参阅[创建您的第一个AEM Forms应用程序](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概述{#functional-overview}

您可以使用AEM Forms工作区执行以下任务：

**启动业务流程：** AEM Forms工作区按照您的组织设计和设置的流程类别。您可以收藏常用的类别，以便快速访问这些类别。 在开始某个流程时，您通常会填写表格，以启动表单工作流控制的业务流程。 有关更多信息，请参阅[启动进程](/help/forms/using/starting-processes.md)。

**查看任务并执行相应操作：** 在查看待办事项列表时，您会看到业务流程中分配给您或您所属的任何组的任务，或者是其他用户的共享任务。您可以根据需要打开、处理和完成任务。 通常，完成任务包括提供信息、批准表单或拒绝表单。 有关更多信息，请参阅[使用待办事项列表](/help/forms/using/todo-lists.md)。

**跟踪任务**:要跟踪任务，请使用AEM Forms工作区的“跟踪”选项卡。您可以搜索已启动或参与的活动或已完成进程。 您可以查看流程中包含的任务、分配和表单。 您还可以使用之前启动的流程中的表单数据启动新流程。 有关更多信息，请参阅[跟踪进程](/help/forms/using/tracking-processes.md)。

## AEM Forms工作区的新产品{#new-offering-of-aem-forms-workspace}

**支持批量批准任务**:

您可以批准同一类型的多个任务。 选择一项任务进行审批后，将只启用具有相同进程、具有相同任务名称和相同路由选项的任务。 有关实施详细信息，请参阅[使用待办事项列表](/help/forms/using/todo-lists.md)。

## 从Flex Workspace迁移到AEM Forms工作区{#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex客户不支持AEM Forms工作区。 所有使用Flex工作区的客户都应转到AEM Forms工作区。

在AEM Forms工作区中，与XDP表单关联的默认呈现和提交服务（位于默认操作配置文件中）已发生更改，并且已引入新服务。 有关详细信息，请参阅[新建渲染和提交服务](/help/forms/using/new-render-submit-service.md)。 要迁移与XDP表单一起使用的现有流程，以便利用这些服务，您可以按照[这些步骤](new-render-submit-service.md)执行。

**将Flex工作区自定义设置映射到AEM Forms工作区**

两个工作区中各种类型自定义之间的映射如下所示。

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
     <li>创建自定义批准容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重用组件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">创建新的“登录”屏幕</a></li>
     <li>批准容器已弃用。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Flex工作区中某些未在AEM Forms工作区中提供的功能包括：消息和通知、欢迎页面、批准容器以及用于管理列标题的选项。 有关完整列表，请参阅[Flex Workspace的功能在AEM Forms工作区中不可用](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作区{#developing-with-aem-forms-workspace}进行开发

### 架构 {#architecture}

AEM Forms工作区是在CRX™上托管的基于HTML和JavaScript™的Web应用程序。 在浏览器中打开工作区URL时，将访问CRX™资源，并且该应用程序会在浏览器中以HTML页面的形式呈现。 JavaScript库和自定义JavaScript代码可管理应用程序的内部和外部行为，如用户界面、用户交互以及与AEM Forms服务器的通信。 有关更多详细信息，请参阅AEM Forms工作区[架构](/help/forms/using/html-workspace-architecture.md)。

### AEM Forms工作区自定义{#aem-forms-workspace-customization}

AEM Forms工作区支持各种自定义，以更新用户界面的布局、外观、功能等。 这些自定义涉及更新以下一项或多项：

* 用户界面的外观
* 使用语义自定义的功能
* 在其他Web应用程序中重用HTML组件

[customization](introduction-customizing-html-workspace.md#types-of-customizations)一文介绍了此类自定义的类型。

### 设置开发人员环境{#set-up-the-developer-environment}

AEM Forms工作区的交付项包括：在CRX上部署的CRX包、包含完整源代码的SDK存档、第三方JavaScript库，以及AEM Forms工作区的构建脚本。 使用这些组件设置开发人员环境以执行上述自定义设置。 有关更多详细信息，请参阅[构建AEM Forms工作区代码](introduction-customizing-html-workspace.md#building-html-workspace-code)。

您可以自定义界面和核心功能的主要部分，如字体、颜色方案、徽标、登录屏幕、错误对话框、与第三方应用程序集成，以及在第三方应用程序中重复使用组件。 您还可以增强“任务摘要”页面上显示的内容，显示任务路由操作的图像，甚至修改创建AEM Forms工作区应用程序的低级骨干模型和视图。

### XDP Forms {#html-rendering-of-xdp-forms}的HTML渲染

默认情况下，对于新流程，XDP表单在桌面上以PDF格式呈现，在平板电脑上以HTML格式呈现。 可以始终以HTML格式渲染XDP表单。 有关详细信息，请参阅[New Render and Submit Services](/help/forms/using/new-render-submit-service.md)。

[移动设](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 备表单功能(可用于配 [置文件](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html))允许XDP表单的HTML呈现。默认情况下，“渲染新HTML表单”使用`default.html`配置文件，您可以更改该配置文件。 您还可以添加在以HTML格式呈现XDP表单之前发生的自定义更改。

## AEM Forms工作区应用程序{#aem-forms-workspace-app}

要在移动设备上处理您的业务流程，您可以使用AEM Forms工作区应用程序产品AEM Forms。 有关更多信息，请参阅[AEM Forms工作区应用程序概述](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)。
