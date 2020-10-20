---
title: OSGi上以Forms为中心的工作流程
seo-title: 快速构建基于表单的自适应流程，自动执行文档服务操作，并将Adobe Sign与AEM工作流结合使用
description: 使用AEM Forms工作流自动化并快速构建审阅和批准，以开始文档服务
seo-description: 使用AEM Forms工作流自动化并快速构建审阅和批准、开始文档服务(例如，将PDF文档转换为其他格式)、与Adobe Sign签名工作流集成等。
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
translation-type: tm+mt
source-git-commit: 149e505eb4dac0d9a56c53036ce1c6b8d16ad0f1
workflow-type: tm+mt
source-wordcount: '3065'
ht-degree: 1%

---


# OSGi上以Forms为中心的工作流程{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

企业从数以百计的表单、各种后端系统以及在线或离线数据源中收集数据。 他们还拥有一组动态的用户来对数据做出决策，这涉及到迭代式审阅和批准流程。

除了内部和外部受众的审核和批准工作流，大型组织和企业还具有重复的任务。 例如，将PDF文档转换为其他格式。 手动完成后，这些任务将占用大量时间和资源。 企业还有法律要求对文档进行数字签名并归档表单数据，以便以后以预定义格式使用。

## OSGi上以Forms为中心的工作流程介绍 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM工作流快速构建基于表单的自适应工作流。 这些工作流可用于审查和批准、业务流程流、开始文档服务、与Adobe Sign签名工作流集成以及类似操作。 例如，信用卡申请处理、员工离职审批工作流、将表单另存为PDF文档。 此外，这些工作流可以在组织内或通过网络防火墙使用。

借助OSGi上以Forms为中心的工作流程，您可以快速为OSGi堆栈上的各种任务构建和部署工作流，无需在JEE堆栈上安装成熟的流程管理功能。 工作流的开发和管理使用了熟悉的AEM工作流和AEM收件箱功能。 工作流构成了实际业务流程自动化的基础，这些业务流程跨越多个软件系统、网络、部门甚至组织。

设置完成后，可以手动触发这些工作流以完成定义的流程，或在用户提交表单或通信管理信函时以编 [程方式](/help/forms/using/cm-overview.md) 运行。 借助这一增强的AEM工作流功能，AEM Forms优惠了两个独特但相似的功能。 作为部署战略的一部分，您需要确定哪一项适合您。 查看以 [Forms](capabilities-osgi-jee-workflows.md) 为中心的AEM工作流在OSGi和JEE上的流程管理方面的比较。 此外，有关部署拓扑，请参见 [AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)。

OSGi上以Forms为中心的工作流 [程扩展了AEM](/help/sites-authoring/inbox.md) 收件箱，并为AEM工作流编辑器提供了额外的组件（步骤），以添加对以AEM Forms为中心的工作流的支持。 扩展的AEM收件箱具有类似于 [AEM FormsWorkspace的功能](introduction-html-workspace.md)。 除了管理以人为中心的工作流（批准、审阅等），您还可以使用AEM工作流自动执行与 [文档](/help/sites-developing/workflows-step-ref.md)服务相关的操作（例如，生成PDF）和电子签名(Adobe Sign)文档。

所有AEM Forms工作流程步骤都支持使用变量。 变量使工作流步骤能够在运行时跨步骤保存和传递元数据。 您可以创建不同类型的变量来存储不同类型的数据。 您还可以创建变量集合（数组），以存储相关的同类型数据的多个实例。 通常，当您需要根据变量所包含的值做出决策或在后续流程中存储您需要的信息时，您会使用变量或变量集合。 有关在这些以Forms为中心的工作流组件（步骤）中使用变量的更多信息，请参 [阅OSGi —— 步骤参考上以Forms为中心的工作流](../../forms/using/aem-forms-workflow-step-reference.md)。 有关创建和管理变量的信息，请参 [阅AEM工作流中的变量](../../forms/using/variable-in-aem-workflows.md)。

下图描述了在OSGi上创建、运行和监视以Forms为中心的工作流的端到端过程。

![简介-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Before you start {#before-you-start}

* 工作流是真实业务流程的代表。 让您的真实业务流程和业务流程参与者的列表准备就绪。 此外，在开始创建工作流程之前，请准备好宣传资料(自适应表单、PDF文档等)。
* 一个工作流可以具有多个阶段。 这些阶段显示在AEM收件箱中，并帮助报告工作流的进度。 将业务流程分为多个逻辑阶段。
* 您可以配置AEM任务的分配工作流步骤，以向用户或受分配者发送电子邮件通知。 因此，启 [用电子邮件通知](#configure-email-service)。
* 工作流程还可以使用Adobe签名进行数字签名。 如果您计划在工作流中使用Adobe Sign，请先 [为AEM Forms配置](../../forms/using/adobe-sign-integration-adaptive-forms.md) Adobe Sign，然后在工作流中使用它。

## Create a workflow model {#create-a-workflow-model}

工作流模型由业务流程的逻辑和流程组成。 它由一系列步骤组成。 这些步骤是AEM组件。 您可以根据需要使用参数和脚本扩展工作流步骤以提供更多功能和控制。 AEM Forms除了提供AEM开箱即用步骤外，还提供了几个步骤。 有关AEM和AEM Forms步骤的详细列表，请参 [阅AEM工作流步](/help/sites-developing/workflows-step-ref.md)[骤参考和以Forms为中心的OSGi —— 步骤参考](../../forms/using/aem-forms-workflow.md)。

AEM提供了直观的用户界面，以使用提供的工作流步骤创建工作流模型。 有关创建工作流模型的分步说明，请参阅创 [建工作流模型](/help/sites-developing/workflows-models.md)。 以下示例提供了为审批和复查工作流创建工作流模型的分步说明：

>[!NOTE]
>
>您必须是工作流编辑器组的成员才能创建或编辑工作流模型。

### 为审批和审阅工作流创建模型 {#create-a-model-for-an-approval-and-review-workflow}

审批和审核工作流面向需要人为干预才能做出决策的任务。 以下示例为要由前台银行代理填写的按揭贷款应用程序创建工作流模型。 填写申请后，即发送审批。 之后，将批准的申请书送交申请人，由Adobe Sign进行电子签名。

该示例以下附加的包的形式提供。 使用包管理器导入并安装示例。 您还可以执行以下步骤来手动创建应用程序的工作流模型：

该示例创建一个工作流模型，该工作流模型是由前台银行代理填写的抵押申请。 填写完毕后，将发送申请以供审批。 随后，批准的申请将发送给客户，由Adobe Sign进行电子签名。 您可以使用包管理器导入和安装示例。

[获取文件](assets/example-mortgage-loan-application.zip)

1. 打开工作流模型控制台。 默认URL为 `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Select **Create**, then **Create Model**. 此时会出现“添加工作流模型”对话框。
1. 输入 **标题** 和 **名称** （可选）。 例如，抵押申请。 点按&#x200B;**完成**。
1. 选择新创建的工作流模型并点按 **编辑**。 现在，您可以添加工作流步骤来构建业务逻辑。 首次创建工作流模型时，它包含：

   * 步骤：流开始和流结束。 这些步骤表示工作流的开始和结束。 这些步骤是必需的，无法编辑或删除。
   * 名为步骤1的参加者步骤示例。 此步骤配置为向管理员用户分配工作项。 删除此步骤。

1. 启用电子邮件通知。 您可以在OSGi上配置以Forms为中心的工作流，以向用户或受分配者发送电子邮件通知。 执行以下配置以启用电子邮件通知：

   1. 请转至AEM configuration manager `https://[server]:[port]/system/console/configMgr`。
   1. 打开Day **[!UICONTROL CQ邮件服务配置]** 。 为SMTP服务器主 **[!UICONTROL 机名、SMTP服]****[!UICONTROL 务器端口和]** “ **[!UICONTROL 发件人”地址字段指定值]** 。 单击&#x200B;**[!UICONTROL 保存]**。
   1. 打开Day **[!UICONTROL CQ Link Externalizer配置]** 。 在“域 **** ”字段中，为本地、作者和发布实例指定实际的主机名/IP地址和端口号。 单击&#x200B;**[!UICONTROL 保存]**。

1. 创建工作流阶段。 一个工作流可以具有多个阶段。 这些阶段显示在AEM收件箱中并报告工作流的进度。

   要定义舞台，请点按信 ![息圆图标](assets/info-circle.png) ，打开工作流模型属性，打开“ **舞台** ”选项卡，为工作流模型添加舞台，然后点 **按保存并关闭**。 对于按揭贷款应用程序示例，请创建阶段：贷款申请、贷款申请状态、待签署文档和已签署贷款文档。

1. 将“分配任务步 **骤”浏览器** 拖放到工作流模型。 将它作为模型的第一步。

   分配任务组件将工作流创建的任务分配给用户或用户组。 除了指定任务，您还可以使用组件为任务指定自适应表单或非交互式PDF。 自适应表单必须接受用户的输入，非交互式PDF或只读自适应表单仅用于审阅工作流。

   您还可以使用该步骤控制任务的行为。 例如，创建记录的自动文档，将任务分配给特定用户或用户组、提交数据的路径、要预填充的数据路径以及默认操作。 有关分配任务步骤选项的详细信息，请参阅OSGi - [步骤参考文档上以Forms为中心的工作流](../../forms/using/aem-forms-workflow.md) 。

   ![工作流编辑器](assets/workflow-editor.png)

   对于按揭任务应用程序示例，将分配文档步骤配置为使用只读自适应表单，并在任务完成后显示PDF。 此外，选择允许批准贷款请求的用户组。 在“操 **作** ”选项卡上，禁用 **“提交** ”选项。 创建String **数据** 类型的actionTaked变量，并将该变量指定为 **Route Variable**。 例如，actionTaked。 此外，添加“批准”和“拒绝”路由。 路由在AEM收件箱中显示为单独的操作（按钮）。 工作流会根据用户点击的操作（按钮）选择分支。

   您可以导入示例包，该示例包可在章节的开头下载，以获得为示例按揭贷款应用程序配置的分配任务步骤的所有字段的完整值集。

1. 将“或拆分”组件从步骤浏览器拖放到工作流模型。 “或拆分”(OR Split)在工作流中创建拆分，之后只有一个分支处于活动状态。 此步骤允许您将条件处理路径引入工作流。 您可以根据需要向每个分支添加工作流步骤。

   您可以使用规则定义、ECMA脚本或外部脚本为分支定义路由表达式。

   使用表达式编辑器为Branch 1和Branch 2创建路由表达式。 这些路由表达式可帮助根据AEM收件箱中的用户操作选择分支。

   **路由表达式第1分支**

   当用户在AEM收件 **箱中点** 击“批准”时，将激活Branch 1。

   ![OR拆分示例](assets/orsplit_branch1_active_new.png)

   **路由分支表达式2**

   当用户在AEM收件 **箱中** 点击“拒绝”时，Branch 2即被激活。

   ![OR拆分示例](assets/orsplit_branch2_active_new.png)

   有关使用变量创建路由表达式的信息，请参 [阅AEM Forms工作流中的变量](../../forms/using/variable-in-aem-workflows.md)。

1. 添加其他工作流步骤以构建业务逻辑。

   对于抵押示例，将生成记录文档、两个分配任务步骤和一个符号文档步骤添加到模型的分支1，如下图所示。 一个分配任务步骤是向申请人显 **示和发送要签名的贷款文档** ，另一个分配任务组件 **用于显示已签名文档**。 另外，向分支2添加分配任务组件。 当用户在AEM收件箱中点击“拒绝”时，此选项会激活。

   对于为按揭任务应用程序配置的分配文档步骤、记录步骤的和签名文档步骤的所有字段的完整值集，请导入示例包，该示例包可在本节的开头进行下载。

   工作流模型已准备就绪。 您可以通过各种方法启动工作流。 有关详细信息，请 [参阅在OSGi上启动以Forms为中心的工作流](#launch)。

   ![工作流——编辑器——按揭](assets/workflow-editor-mortgage.png)

## 创建以Forms为中心的工作流程应用程序 {#create-a-forms-centric-workflow-application}

应用程序是与工作流关联的自适应表单。 当应用程序通过收件箱提交时，它会启动关联的工作流。 要使Forms工作流作为AEM收件箱和AEM Forms应用程序中的应用程序可用，请执行以下操作以创建工作流应用程序：

>[!NOTE]
>
>您必须是fd-administrator组的成员才能创建和管理工作流应用程序。

1. 在AEM创作实例上，转到 ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Manage Workflow Application]** ，然 **[!UICONTROL 后点按Create]** Adobe。
1. 在“创建工作流应用程序”窗口中，为以下字段提供输入，然后点按 **创建**。 将创建新应用程序，并在“工作流应用程序”屏幕中列出。

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>标题显示在AEM收件箱中，可帮助用户选择应用程序。 保持描述性。 例如，开立储蓄帐户的应用程序。<br /> </td>
  </tr>
  <tr>
   <td>名称 </td>
   <td>指定应用程序的名称。 除字母、数字、连字符和下划线之外的所有字符都替换为连字符。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>说明显示在AEM收件箱中。 在说明字段中提供有关应用程序的详细信息。 例如，应用程序的用途。<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td><p>指定自适应表单的路径。 当用户开始应用程序时，将显示指定的自适应表单。</p> <p><strong>注意</strong>:工作流程应用程序不支持长于一页或需要在Apple iPad上滚动的表单和PDF文档。 当应用程序在Apple iPad上打开且自适应表单或PDF文档长于页面时，第二页中的表单字段和内容将丢失。</p> </td>
  </tr>
  <tr>
   <td>访问组</td>
   <td><p>选择用户组。 该应用程序仅对选定组的成员显示在AEM收件箱中。 “访问组”选项使工作流用户组的所有组都可供选择。 </p> <br /> </td>
  </tr>
  <tr>
   <td>预填服务</td>
   <td>为自适应 <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">表单</a> 选择预填服务。<br /> </td>
  </tr>
  <tr>
   <td>工作流模型</td>
   <td>为应用 <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">程序选择</a> 工作流模型。 工作流模型由业务流程的逻辑和流程组成。 </td>
  </tr>
  <tr>
   <td>数据文件路径</td>
   <td>在crx-repository中指定数据文件的路径。 该路径相对于自适应表单有效负荷，并包含数据文件的名称。 始终包含文件的完整名称（包括扩展名）（如果适用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路径</td>
   <td>在crx-repository中指定附件文件夹的路径。 附件路径相对于有效负荷位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>记录文档路径</td>
   <td>指定crx-repository中记录文件的文档路径。 路径相对于自适应表单有效负荷位置。 始终包含文件的完整名称（包括扩展名）（如果适用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上启动以Forms为中心的工作流程 {#launch}

您可以通过以下方式启动或触发以Forms为中心的工作流：

* [从AEM收件箱提交应用程序](#inbox)
* [从AEM Forms应用程序提交应用程序](#afa)

* [提交自适应表单](#af)
* [使用监视文件夹](#watched)

* [提交交互式通信或信件](#letter)

### 从AEM收件箱提交应用程序 {#inbox}

您创建的工作流应用程序在收件箱中可作为应用程序使用。 作为工作流用户组的成员的用户可以填写和提交触发关联工作流的应用程序。 有关使用AEM收件箱提交应用程序和管理任务的信息，请参 [阅管理AEM收件箱中的Forms应用程序和任务](../../forms/using/manage-applications-inbox.md)。

### 从AEM Forms应用程序提交应用程序 {#afa}

AEM Forms应用程序与AEM Forms服务器同步，允许您更改您帐户中的表单数据、任务、工作流应用程序和已保存的信息（草稿／模板）。 有关详细信息，请参阅 [AEM Forms应用](/help/forms/using/aem-forms-app.md) 程序和相关文章。

### 提交自适应表单 {#af}

您可以配置自适应表单的提交操作，以在提交自适应表单时开始工作流。 自适应表单提 **供调用AEM工作流** 提交操作，以在提交自适应表单时开始工作流。 有关提交操作的详细信息，请参 [阅配置提交操作](../../forms/using/configuring-submit-actions.md)。 要通过AEM Forms应用程序提交自适应表单，请在自适应表单属性中启用与AEM Forms应用程序同步。

您可以配置自适应表单以从AEM Forms应用程序同步、提交和触发工作流。 有关详细信息，请 [参阅使用表单](/help/forms/using/working-with-form.md)。

### 使用监视的文件夹 {#watched}

管理员（fd-administrators组的成员）可以将网络文件夹配置为在用户将文件（如PDF文件）放置到文件夹时运行预配置的工作流。 工作流完成后，它可以将结果文件保存到指定的输出文件夹。 这类文件夹称为“监视 [文件夹”](../../forms/using/watched-folder-in-aem-forms.md)。 请执行以下过程来配置监视的文件夹以启动工作流：

1. 在AEM作者实例中，转 ![到tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 配置监视文件夹]**。 将显示已配置的监视文件夹列表。
1. 点按 **[!UICONTROL 新建]**。 将显示一列表字段。 指定以下字段的值，为工作流配置监视文件夹：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td><span class="uicontrol">名称</code></td>
   <td>指定监视文件夹的名称。 此字段仅支持字母数字。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">路径</code></td>
   <td>指定监视文件夹的物理位置。 在群集环境中，使用可从AEM群集节点访问的共享网络文件夹。</td>
  </tr>
  <tr>
   <td><span class="uicontrol">文件处理方法</code></td>
   <td>选择工 <span class="uicontrol">作 </code>流选项。 </code></td>
  </tr>
  <tr>
   <td><span class="uicontrol">工作流模型</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">输出文件模式</code></td>
   <td>指定输出文件和目录的目录结构。 您还可以指定输 <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">出文件和目录的模式</a>。</td>
  </tr>
 </tbody>
</table>

1. 点按 **高级**。 为以下字段指定一个值，然后点按 **创建**。 已将监视文件夹配置为启动工作流。 现在，每当将文件放在监视文件夹的输入目录中时，都会触发指定的工作流。

   | 字段 | 描述 |
   |---|---|
   | 有效负荷映射器过滤器 | 创建监视文件夹时，会在crx-repository中创建文件夹结构。 文件夹结构可用作工作流的有效负荷。 您可以编写一个脚本来映射AEM Workflow以接受监视的文件夹结构中的输入。 现成的实施可用并列在“有效负荷映射器过滤器”中。 如果您没有自定义实现，请选择默认实现。 |

   高级选项卡包含更多字段。 这些字段中的大多数都包含默认值。 要了解所有字段，请参阅创 [建或配置监视的文件夹文章](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 。

### 提交交互式通信或信件 {#letter}

在提交交互式通信或信件时，您可以在OSGi上关联并执行以Forms为中心的工作流。 在通信管理中，工作流用于后处理交互通信和信件。 例如，通过电子邮件发送、打印、传真或归档最终信件。 有关详细步骤，请参 [阅交互式通信和信件的后处理](../../forms/using/submit-letter-topostprocess.md)。

## 其他配置 {#additional-configurations}

### 配置电子邮件服务 {#configure-email-service}

您可以使用AEM任务的分配工作流和发送电子邮件步骤发送电子邮件。 请执行以下步骤以指定电子邮件服务器和发送电子邮件所需的其他配置：

1. 请转至AEM configuration manager `https://[server]:[port]/system/console/configMgr`。
1. 打开Day **[!UICONTROL CQ邮件服务配置]** 。 为SMTP服务器主 **[!UICONTROL 机名、SMTP服]****[!UICONTROL 务器端口和]** “ **[!UICONTROL 发件人”地址字段指定值]** 。 单击&#x200B;**[!UICONTROL 保存]**。
1. 打开Day **[!UICONTROL CQ Link Externalizer配置]** 。 在“域 **** ”字段中，为本地、作者和发布实例指定实际的主机名/IP地址和端口号。 单击&#x200B;**[!UICONTROL 保存]**。

### 清除工作流实例 {#purge-workflow-instances}

最小化工作流实例数可提高工作流引擎的性能，因此您可以定期从存储库中清除已完成或正在运行的工作流实例。 有关详细信息，请参 [阅常规清除工作流实例](/help/sites-administering/workflows-administering.md#regular) ，清除工作流实例
