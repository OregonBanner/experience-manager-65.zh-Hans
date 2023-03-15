---
title: OSGi上以Forms为中心的工作流
seo-title: Rapidly build adaptive forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms Workflow自动并快速构建审阅和批准，以启动文档服务
seo-description: Use AEM Forms Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
source-git-commit: d9608d584e822accc0c198fcf1d1b706d065938e
workflow-type: tm+mt
source-wordcount: '3681'
ht-degree: 2%

---

# OSGi上以Forms为中心的工作流{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企业从成千上万个表单、各种后端系统以及在线或离线数据源中收集数据。 他们还拥有一组动态的用户，可就数据做出决策，这涉及反复的审查和批准流程。

除了内部和外部受众的审查和审批工作流之外，大型组织和企业还有重复的任务。 例如，将PDF文档转换为另一种格式。 手动完成这些任务会占用很多时间和资源。 企业还有法律要求，必须对文档进行数字签名，并将表单数据存档，以便以后以预定义格式使用。

## 关于OSGi的以Forms为中心的工作流简介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM Workflows快速构建基于自适应表单的工作流。 这些工作流可用于审阅和批准、业务流程流、启动文档服务、与Adobe Sign签名工作流集成以及类似操作。 例如，信用卡申请处理、员工休假审批工作流、将表单另存为PDF文档。 此外，这些工作流还可以在组织内或跨网络防火墙使用。

借助OSGi上以Forms为中心的工作流，您可以在OSGi栈栈上快速构建和部署各种任务的工作流，而无需在JEE栈栈上安装完整的流程管理功能。 工作流的开发和管理使用熟悉的AEM Workflow和AEM Inbox功能。 工作流构成了自动化跨多个软件系统、网络、部门甚至组织的真实业务流程的基础。

设置后，这些工作流可以手动触发以完成定义的流程，或在用户提交表单或页面时以编程方式运行 [通信管理](/help/forms/using/cm-overview.md) 书信。 通过这一增强的AEM Workflow功能，AEM Forms提供了两种截然不同但相似的功能。 作为部署策略的一部分，您需要确定适合您的部署策略。 查看 [比较](capabilities-osgi-jee-workflows.md) OSGi上以Forms为中心的AEM Workflow和JEE上的流程管理。 此外，对于部署拓扑，请参见 [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md).

OSGi上以Forms为中心的工作流扩展了 [AEM收件箱](/help/sites-authoring/inbox.md) 并为AEM Workflow编辑器提供额外的组件（步骤），以添加对以AEM Forms为中心的工作流的支持。 扩展的AEM收件箱具有类似于 [AEM Forms工作区](introduction-html-workspace.md). 除了管理以人为中心的工作流（批准、审核等）之外，您还可以使用AEM工作流实现自动化 [文档服务](/help/sites-developing/workflows-step-ref.md) — 相关操作(例如，生成PDF)和电子签名(Adobe Sign)文档。

所有AEM Forms工作流步骤都支持使用变量。 变量使工作流步骤能够在运行时跨步骤保留和传递元数据。 您可以创建不同类型的变量来存储不同类型的数据。 您还可以创建变量集合（数组），用于存储相关同类数据的多个实例。 通常，当您需要根据其持有的值做出决策时，或者需要存储稍后在流程中所需的信息时，可以使用变量或变量集合。 有关在这些以Forms为中心的工作流组件中使用变量的更多信息（步骤），请参阅 [OSGi上以Forms为中心的工作流 — 步骤参考](../../forms/using/aem-forms-workflow-step-reference.md). 有关创建和管理变量的信息，请参阅 [AEM工作流中的变量](../../forms/using/variable-in-aem-workflows.md).

下图描述了在OSGi上创建、运行和监控以Forms为中心的工作流的端到端过程。

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 开始之前 {#before-you-start}

* 工作流是真实业务过程的一种表现形式。 让您的实际业务流程和业务流程参与者的列表做好准备。 此外，在开始创建PDF之前，还要准备好宣传资料（自适应表单、工作流文档等）。
* 一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中，并帮助报告工作流的进度。 将业务流程划分为逻辑阶段。
* 您可以将AEM Workflows的分配任务步骤配置为向用户或受分配人发送电子邮件通知。 所以， [启用电子邮件通知](#configure-email-service).
* 工作流还可以使用Adobe签名进行数字签名。 如果您计划在工作流中使用Adobe Sign，则 [为AEM Forms配置Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 在工作流中使用它之前。

## 创建工作流模型 {#create-a-workflow-model}

工作流模型由业务流程的逻辑和流程组成。 它由一系列步骤组成。 这些步骤是AEM组件。 您可以使用参数和脚本扩展工作流步骤，以根据需要提供更多的功能和控制。 除了开箱即用的AEM步骤外，AEM Forms还提供了一些步骤。 有关AEM和AEM Forms步骤的详细列表，请参阅 [AEM工作流步骤参考](/help/sites-developing/workflows-step-ref.md) 和 [OSGi上以Forms为中心的工作流 — 步骤参考](../../forms/using/aem-forms-workflow.md).

AEM提供了一个直观的用户界面，用于使用提供的工作流步骤创建工作流模型。 有关创建工作流模型的分步说明，请参阅 [创建工作流模型](/help/sites-developing/workflows-models.md). 以下示例提供了为批准和审阅工作流创建工作流模型的分步说明：

>[!NOTE]
>
>您必须是工作流编辑器组的成员才能创建或编辑工作流模型。

### 为审批和审核工作流创建模型 {#create-a-model-for-an-approval-and-review-workflow}

审批和审核工作流适用于需要人工干预才能做出决定的任务。 以下示例为要由前台银行代理填写的抵押贷款申请创建工作流模型。 填写申请后，将发送该申请以供审批。 随后，已批准的申请将通过Adobe Sign发送给申请人以索取电子签名。

该示例以如下附加的包形式提供。 使用包管理器导入并安装示例。 您还可以执行以下步骤来手动创建应用程序的工作流模型：

该示例创建一个工作流模型，用于创建一个由前台银行代理填写的抵押贷款申请。 填写完毕后，将发送申请以供审批。 之后，将批准的申请发送给客户以使用Adobe Sign进行电子签名。 您可以使用包管理器导入和安装示例。

[获取文件](assets/example-mortgage-loan-application.zip)

1. 打开工作流模型控制台。 默认URL为 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 选择 **创建**，则 **创建模型**. 此时将显示“添加工作流模型”对话框。
1. 输入 **标题** 和 **名称** （可选）。 例如，抵押贷款申请。 点按&#x200B;**完成**。
1. 选择新创建的工作流模型并点按 **编辑**. 现在，您可以添加工作流步骤来构建业务逻辑。 首次创建工作流模型时，它包含：

   * 步骤：流程开始和流程结束。 这些步骤表示工作流的开始和结束。 这些步骤是必需的，无法编辑或删除。
   * 名为步骤1的参与者步骤示例。 此步骤配置为将工作项分配给管理员用户。 删除此步骤。

1. 启用电子邮件通知。 您可以在OSGi上配置以Forms为中心的工作流，向用户或受分配人发送电子邮件通知。 执行以下配置以启用电子邮件通知：

   1. 转到AEM配置管理器，网址为 `https://[server]:[port]/system/console/configMgr`.
   1. 打开 **[!UICONTROL Day CQ邮件服务]** 配置。 指定值 **[!UICONTROL SMTP服务器主机名]**， **[!UICONTROL SMTP服务器端口，]** 和 **[!UICONTROL “寄件者”地址]** 字段。 单击“**[!UICONTROL 保存]**”。
   1. 打开 **[!UICONTROL Day CQ链接外部化器]** 配置。 在 **[!UICONTROL 域]** 字段，为本地、创作和发布实例指定实际主机名/IP地址和端口号。 单击“**[!UICONTROL 保存]**”。

1. 创建工作流暂存。 一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中并报告工作流的进度。

   要定义舞台，请点按 ![信息圆](assets/info-circle.png) 图标打开工作流模型属性，打开 **暂存** 选项卡，为工作流模型添加暂存，然后点按 **保存并关闭**. 对于抵押贷款申请示例，创建阶段：贷款请求、贷款请求状态、要签名的文档和已签名的贷款文档。

1. 拖放 **分配任务** 步骤浏览器到工作流模型。 使其成为模型的第一步。

   分配任务组件将工作流创建的任务分配给用户或组。 在分配任务时，您可以使用组件为任务指定自适应表单或非交互式PDF。 自适应表单需要接受用户输入，非交互式PDF或使用只读自适应表单进行仅审核工作流。

   您还可以使用该步骤控制任务的行为。 例如，创建自动记录文档，将任务分配给特定用户或组，提交数据的路径，要预填充的数据路径以及默认操作。 有关分配任务步骤选项的详细信息，请参见 [OSGi上以Forms为中心的工作流 — 步骤参考](../../forms/using/aem-forms-workflow.md) 文档。

   ![workflow-editor](assets/workflow-editor.png)

   对于抵押贷款应用程序示例，将分配任务步骤配置为使用只读自适应表单并在任务完成后显示PDF文档。 此外，选择以允许批准贷款请求的用户组。 在 **操作** 选项卡，禁用 **提交** 选项。 创建 **actionTaked** 变量，并将变量指定为 **路由变量**. 例如，actionTuned。 此外，还添加“批准”和“拒绝”路由。 路由在AEM收件箱中显示为单独的操作（按钮）。 工作流会根据用户点击的操作（按钮）选择一个分支。

   您可以导入示例包，该示例包可在部分的开头下载，用于为分配任务步骤的所有字段的完整值集，这些字段配置有抵押应用程序。

1. 将OR拆分组件从步骤浏览器拖放到工作流模型中。 “OR拆分”会在工作流中创建拆分，之后只有一个分支处于活动状态。 通过此步骤，您可以将条件处理路径引入工作流。 您可以根据需要向每个分支添加工作流步骤。

   您可以使用规则定义、ECMA脚本或外部脚本来定义分支的路由表达式。

   使用表达式编辑器为Branch 1和Branch 2创建路由选择表达式。 这些路由表达式有助于根据AEM收件箱中的用户操作选择分支。

   **分支1的路由表达式**

   用户点按时 **批准** 在AEM收件箱中，分支1处于激活状态。

   ![OR拆分示例](assets/orsplit_branch1_active_new.png)

   **分支2的路由表达式**

   用户点按时 **拒绝** 在AEM收件箱中，分支2处于激活状态。

   ![OR拆分示例](assets/orsplit_branch2_active_new.png)

   有关使用变量创建路由表达式的信息，请参见 [AEM Forms工作流中的变量](../../forms/using/variable-in-aem-workflows.md).

1. 添加其他工作流步骤以构建业务逻辑。

   对于抵押示例，将生成记录文档、两个分配任务步骤和一个签名文档步骤添加到模型的分支1，如下图所示。 一个分配任务步骤是显示和发送 **将签署给申请人的贷款文件** 另一个分配任务组件是 **显示已签署文档**. 此外，还可将分配任务组件添加到分支2。 当用户点按AEM收件箱中的拒绝时，它会激活。

   对于配置的分配任务步骤、记录文档步骤和签名文档步骤的所有字段的完整值集，例如，抵押应用程序，导入示例包，该示例包可在本节开头下载。

   工作流模型已准备就绪。 您可以通过各种方法启动工作流。 有关详细信息，请参阅 [在OSGi上启动以Forms为中心的工作流](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## 创建以Forms为中心的工作流应用程序 {#create-a-forms-centric-workflow-application}

应用程序是与工作流关联的自适应表单。 通过“收件箱”提交应用程序时，它会启动关联的工作流。 要使Forms工作流可用作AEM收件箱和AEM Forms应用程序中的应用程序，请执行以下操作以创建工作流应用程序：

>[!NOTE]
>
>您必须是fd-administrator组的成员才能创建和管理工作流应用程序。

1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流应用程序]** 和点按 **[!UICONTROL 创建]**.
1. 在“创建工作流应用程序”窗口中，为以下字段提供输入，然后点按 **创建**. 随即会创建一个新应用程序，该应用程序将在Workflow Applications屏幕上列出。

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>标题显示在AEM收件箱中，可帮助用户选择应用程序。 保持描述性。 例如，储蓄帐户开户应用程序。<br /> </td>
  </tr>
  <tr>
   <td>名称 </td>
   <td>指定应用程序的名称。 除字母、数字、连字符和下划线之外的所有字符都将替换为连字符。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>该描述将显示在AEM收件箱中。 在描述字段中提供有关应用程序的详细信息。 例如，应用程序的用途。<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td><p>指定自适应表单的路径。 当用户启动应用程序时，将显示指定的自适应表单。</p> <p><strong>注释</strong>：工作流应用程序不支持长度超过一页或需要在Apple iPad上滚动的表单和PDF文档。 在Apple iPad上打开应用程序，并且自适应表单或PDF文档比页长时，第二页的表单字段和内容丢失。</p> </td>
  </tr>
  <tr>
   <td>访问组</td>
   <td><p>选择一个组。 该应用程序在AEM收件箱中仅对选定组的成员可见。 访问组选项使工作流用户组的所有组都可供选择。 </p> <br /> </td>
  </tr>
  <tr>
   <td>预填服务</td>
   <td>选择 <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">预填充服务</a> 用于自适应表单。<br /> </td>
  </tr>
  <tr>
   <td>工作流模型</td>
   <td>选择 <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">工作流模型</a> 应用程序的。 工作流模型由业务过程的逻辑和流程组成。 </td>
  </tr>
  <tr>
   <td>数据文件路径</td>
   <td>指定crx-repository中数据文件的路径。 路径相对于自适应表单有效负荷，并包含数据文件的名称。 始终包括文件的完整名称，包括扩展名（如果适用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路径</td>
   <td>指定crx-repository中附件文件夹的路径。 附件路径相对于有效负荷位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>记录文档路径</td>
   <td>指定crx-repository中记录文档文件的路径。 该路径相对于自适应表单有效负荷位置。 始终包括文件的完整名称，包括扩展名（如果适用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上启动以Forms为中心的工作流 {#launch}

您可以通过以下方式启动或触发以Forms为中心的工作流：

* [从AEM收件箱提交应用程序](#inbox)
* [从AEM Forms应用程序提交应用程序](#afa)

* [提交自适应表单](#af)
* [使用观察文件夹](#watched)

* [提交交互式通信或信件](#letter)

### 从AEM收件箱提交应用程序 {#inbox}

您创建的工作流应用程序可用作收件箱中的应用程序。 作为workflow-users组成员的用户可以填写并提交触发关联工作流的应用程序。 有关使用AEM收件箱提交应用程序和管理任务的信息，请参阅 [在AEM收件箱中管理Forms应用程序和任务](../../forms/using/manage-applications-inbox.md).

### 从AEM Forms应用程序提交应用程序 {#afa}

AEM Forms应用程序与AEM Forms服务器同步，并允许您更改帐户中的表单数据、任务、工作流应用程序和保存的信息（草稿/模板）。 有关更多信息，请参阅 [AEM Forms应用程序](/help/forms/using/aem-forms-app.md) 及相关文章。

### 提交自适应表单 {#af}

您可以配置自适应表单的提交操作，以在提交自适应表单时启动工作流。 自适应表单提供 **调用AEM Workflow** 提交操作可在提交自适应表单时启动工作流。 有关提交操作的详细信息，请参阅 [配置提交操作](../../forms/using/configuring-submit-actions.md). 要通过AEM Forms应用程序提交自适应表单，请在自适应表单属性中启用“与AEM Forms应用程序同步” 。

您可以配置自适应表单，以从AEM Forms应用程序同步、提交和触发工作流。 有关详细信息，请参阅 [使用表单](/help/forms/using/working-with-form.md).

### 使用观察文件夹 {#watched}

管理员（fd-administrators组的成员）可以配置网络文件夹，以便当用户在该文件夹中放置文件(例如PDF文件)时运行预配置的工作流。 工作流完成后，它可以将结果文件保存到指定的输出文件夹中。 此类文件夹称为 [观察文件夹](../../forms/using/watched-folder-in-aem-forms.md). 执行以下过程可配置watched文件夹以启动工作流：

1. 在您的AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 配置Watched文件夹]**. 将显示已配置的Watched文件夹的列表。
1. 点按 **[!UICONTROL 新]**. 此时将显示字段列表。 为以下字段指定值以配置工作流的Watched文件夹：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><span class="uicontrol">名称</code></td>
   <td>指定Watched文件夹的名称。 此字段仅支持字母数字。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">路径</code></td>
   <td>指定Watched文件夹的物理位置。 在群集环境中，使用可从AEM群集节点访问的共享网络文件夹。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">文件处理方法</code></td>
   <td>选择 <span class="uicontrol">工作流 </code>选项。 </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">工作流模型</code></td>
   <td>选择工作流模型。<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">输出文件模式</code></td>
   <td>指定输出文件和目录的目录结构。 您还可以指定 <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">输出文件和目录的模式</a>.</td>
  </tr>
 </tbody>
</table>

1. 点按 **高级**. 指定以下字段的值，然后点按 **创建**. Watched文件夹配置为启动工作流。 现在，每当将文件放入Watched Folder的输入目录时，就会触发指定的工作流。

   | 字段 | 描述 |
   |---|---|
   | 有效负荷映射器过滤器 | 创建watched文件夹时，会在crx-repository中创建文件夹结构。 文件夹结构可用作工作流的负载。 您可以编写脚本来映射AEM Workflow，以接受来自观察文件夹结构的输入。 现成的实施可用，并列在有效负载映射器过滤器中。 如果您没有自定义实施，请选择默认实施。 |

   “高级”选项卡包含更多字段。 这些字段中的大多数都包含默认值。 要了解所有字段，请参阅 [创建或配置观察文件夹](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 文章。

### 提交交互式通信或信件 {#letter}

您可以在提交交互式通信或信件时，在OSGi上关联并执行以Forms为中心的工作流。 在通信管理中，工作流用于后处理交互式通信和信件。 例如，通过电子邮件发送、打印、传真或存档最终信件。 有关详细步骤，请参阅 [交互式通信和信件的后处理](../../forms/using/submit-letter-topostprocess.md).

## 其他配置 {#additional-configurations}

### 配置电子邮件服务 {#configure-email-service}

您可以使用AEM Workflows的分配任务和发送电子邮件步骤来发送电子邮件。 执行以下步骤，指定发送电子邮件所需的电子邮件服务器和其他配置：

1. 转到AEM配置管理器，网址为 `https://[server]:[port]/system/console/configMgr`.
1. 打开 **[!UICONTROL Day CQ邮件服务]** 配置。 指定值 **[!UICONTROL SMTP服务器主机名]**， **[!UICONTROL SMTP服务器端口，]** 和 **[!UICONTROL “寄件者”地址]** 字段。 单击“**[!UICONTROL 保存]**”。
1. 打开 **[!UICONTROL Day CQ链接外部化器]** 配置。 在 **[!UICONTROL 域]** 字段，为本地、创作和发布实例指定实际主机名/IP地址和端口号。 单击“**[!UICONTROL 保存]**”。

### 清除工作流实例 {#purge-workflow-instances}

最大限度地减少工作流实例的数量可以提高工作流引擎的性能，因此，您可以定期从存储库中清除已完成或正在运行的工作流实例。有关详细信息，请参阅， [定期清除工作流实例](/help/sites-administering/workflows-administering.md#regular) 清除工作流实例。

## 将敏感数据参数化为工作流变量并存储在外部数据存储中 {#externalize-wf-variables}

从自适应表单提交到的任何数据 [!DNL Experience Manager] 工作流可以包含企业最终用户的PII（个人身份信息）或SPD（敏感个人数据）。 但是，并非强制要将您的数据存储在 [!DNL Adobe Experience Manager] [JCR存储库](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html). 您可以将最终用户数据存储外部化到托管数据存储中（例如Azure blob存储），方法是将信息参数化 [工作流变量](/help/forms/using/variable-in-aem-workflows.md).

在 [!DNL Adobe Experience Manager] 在Forms工作流中，通过工作流变量执行一系列工作流步骤来处理和传递数据。 这些变量是存储在工作流实例元数据节点中的命名属性或键值对；例如 `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. 这些工作流变量可以外部化到JCR以外的单独存储库中，然后由进行处理 [!DNL Adobe Experience Manager] 工作流。 [!DNL Adobe Experience Manager] 提供API `[!UICONTROL UserMetaDataPersistenceProvider]` 以将工作流变量存储在托管外部存储中。 详细了解在中将工作流变量用于客户拥有的数据存储 [!DNL Adobe Experience Manager]，请参见 [管理外部数据存储的工作流变量](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] 提供了以下内容 [示例](https://github.com/adobe/workflow-variable-externalizer) 使用API将变量从工作流元数据映射到Azure blob存储 [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). 在类似行中，您可以使用示例作为使用指南 [UserMetaDataPersistenceProvider] 用于将任何其他数据存储中的工作流变量外部化的API [!DNL Adobe Experience Manager] 并管理相同的内容。

>[!NOTE]
>
>将工作流变量存储到外部数据存储时，请参考 [工作流外部数据存储准则](#guidelines-workflows-external-data-storage).

### 安装工作流API示例实施

要在托管的Azure Blob存储中存储工作流变量，请执行以下操作：
1. 安装 [示例](https://github.com/adobe/workflow-variable-externalizer) 工作流API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) 如下所示：

   1. 在项目的根目录中运行 `mvn clean install` Maven 3的命令。

   1. 要将包和内容包部署到创作，请运行 `mvn clean install -PautoInstallPackage`.

   1. 要仅将捆绑包部署到作者，请运行 `mvn clean install -PautoInstallBundle`.

1. 在中初始化外部化器OSGi配置文件中的以下属性 `ui.config` 内容包：

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

以下是这些属性的用途（和示例）：

* **帐户密钥** 是授权访问的密钥。

* **帐户名称** 是必须存储数据的azure帐户。

* **endpointsuffix**&#x200B;例如 `core.windows.net`.

* **containername** 是帐户中需要存储数据的容器。 此示例假定容器存在。

* **协议**&#x200B;例如 `https` 或 `http`.

1. 在中配置工作流模型 [!DNL Adobe Experience Manager]. 要了解如何为外部存储配置工作流模型，请参阅 [配置工作流模型](#configure-aem-wf-model).

### 在中配置工作流模型 [!DNL Adobe Experience Manager] 用于外部数据存储 {#configure-aem-wf-model}

要为外部数据存储配置AEM Workflow模型：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**.

1. 选择模型名称并选择 **[!UICONTROL 编辑]**.

1. 选择“页面信息”图标并选择 **[!UICONTROL 打开属性]**.

1. 选择 **[!UICONTROL 将工作流数据存储外部化]**.

1. 选择 **[!UICONTROL 保存并关闭]** 以保存属性。

### 外部数据存储的AEM Workflow准则 {#guidelines-workflows-external-data-storage}

以下是使用时的准则 [!DNL Adobe Experience Manager] 工作流并将数据存储到外部数据存储(例如Microsoft Azure Storage Server)：

* 在工作流模型步骤中定义输入和输出数据文件及附件时，可使用变量来存储数据。 不选择 **[!UICONTROL 相对于有效负荷]** 和 **[!UICONTROL 在绝对路径上可用]** 选项。 此 **[!UICONTROL 相对于有效负荷]** 和 **[!UICONTROL 在绝对路径上可用]** 选项不会自动显示一次 [配置 [!DNL Adobe Experience Manager] 用于外部数据存储的工作流模型](#configure-aem-wf-model).

* 向AEM Workflow提交自适应表单时，使用变量存储数据文件和附件。 不选择 **[!UICONTROL 相对于有效负荷]** 将自适应表单提交到的选项 [!DNL Adobe Experience Manager] 工作流。 此 **[!UICONTROL 相对于有效负荷]** 选项不会在您选择后自动显示 [配置 [!DNL Adobe Experience Manager] 用于外部数据存储的工作流模型](#configure-aem-wf-model).

* 不使用自定义 [!DNL Adobe Experience Manager] 工作流模型中的工作流步骤，用于将数据存储在 [!UICONTROL CRX DE] 存储库。

* 当您 [配置 [!DNL Adobe Experience Manager] 用于外部数据存储的工作流模型](#configure-aem-wf-model)，不创建自定义列 [!DNL Adobe Experience Manager] [!UICONTROL 收件箱] 因为如果工作项位于 [!DNL Adobe Experience Manager] [!UICONTROL 收件箱] 属于标记为外部存储的工作流。
