---
title: AEM Forms的架构和部署拓扑
seo-title: Architecture and deployment topologies for AEM Forms
description: AEM Forms的架构详细信息，以及面向新客户和现有AEM客户以及从LiveCycleES4升级到AEM Forms的客户推荐的拓扑。
seo-description: Architecture details for AEM Forms and recommended topologies for new and existing AEM customers and customers upgrading from LiveCycle ES4 to AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '2478'
ht-degree: 0%

---

# AEM Forms的架构和部署拓扑 {#architecture-and-deployment-topologies-for-aem-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html) |
| AEM 6.5 | 本文 |

## 架构 {#architecture}

AEM Forms是作为AEM包部署到AEM中的应用程序。 此包称为AEM Forms附加组件包。 AEM Forms附加组件包包含部署到AEM OSGi容器中的服务（API提供程序）和由AEM Sling框架管理的servlet或JSP（提供前端和REST API功能）。 下图描述了此设置：

![架构](assets/architecture.png)

AEM Forms的架构包含以下组件：

* **核心AEM服务：** AEM为已部署的应用程序提供的基本服务。 这些服务包括符合JCR的内容存储库、OSGI服务容器、工作流引擎、信任存储、密钥存储等。 AEM Forms应用程序可以使用这些服务，但AEM Forms包不提供这些服务。 这些服务是整个AEM栈栈的组成部分，各种AEM Forms组件都使用这些服务。
* **Forms服务：** 提供与表单相关的功能，如创建、汇编、分发和存档PDF文档，添加数字签名以限制对文档的访问，以及对条形码表单进行解码。 这些服务可公开供在AEM中联合部署的自定义代码使用。
* **Web层：** JSP或servlet，基于常用服务和表单服务构建，可提供以下功能：

   * **创作前端**：用于创作和管理表单的表单创作和表单管理用户界面。
   * **表单呈现和提交前端**：面向最终用户的界面，供AEM Forms的最终用户（例如，访问政府网站的公民）使用。 这提供了表单呈现（在Web浏览器中显示表单）和提交功能。
   * **REST API**：JSP和servlet导出表单服务的子集，以供基于HTTP的客户端（例如forms移动SDK）远程使用。

**OSGi上的AEM Forms：** OSGi环境上的AEM Forms是标准的AEM Author或AEM Publish ，并在其上部署了AEM Forms包。 您可以在OSGi上运行AEM Forms [单服务器环境、群组和群集设置](/help/sites-deploying/recommended-deploys.md). 集群设置仅可用于AEM Author实例。

**AEM Forms在JEE：** JEE上的AEM Forms是在JEE栈栈上运行的AEM Forms服务器。 它在应用程序服务器中运行的单个JEE栈栈上联合部署了AEM Author和AEM Forms附加组件包及其他AEM Forms JEE功能。 您可以在单服务器和群集设置中在JEE上运行AEM Forms。 只有运行Document Security、流程管理以及升级到AEM Forms的LiveCycle客户，才需要JEE上的AEM Forms。 以下是一些在JEE上使用AEM Forms的其他方案：

* **HTML工作区支持(适用于使用HTML工作区的客户)：** JEE上的AEM Forms支持通过处理实例进行单点登录，为处理实例上渲染的特定资源提供服务，并处理在HTML工作区中渲染的表单提交。
* **高级附加表单/交互式通信数据处理**：在需要高级流程管理功能的复杂用例中，可以使用JEE上的AEM Forms另外处理表单/交互式通信数据（并将结果保存到适当的数据存储中）。

JEE上的AEM Forms还向AEM组件提供以下支持服务：

* **集成的用户管理：** 允许将JEE上的AEM Forms用户识别为OSGi用户上的AEM表单，并帮助为OSGi和JEE用户启用SSO。 当需要在OSGi上的AEM表单与JEE上的AEM Forms之间进行单点登录(例如，HTML工作区)时，需要此项。
* **资产托管：** JEE上的AEM Forms可以在OSGi上提供在AEM Forms上渲染的资源(例如，HTML5表单)。

AEM Forms创作用户界面不支持创建记录文档(DOR)、PDF forms和HTML5 Forms。 此类资源是使用独立的Forms Designer应用程序设计的，并分别上传到AEM Forms Manager。 或者，对于JEE上的AEM Forms，可以将表单设计为(在AEM Forms Workbench中)应用程序资产，并部署到JEE服务器上的AEM Forms中。

OSGi上的AEM Forms和JEE上的AEM Forms都具有工作流功能。 您可以在OSGi上的AEM Forms上快速构建和部署用于各种任务的基本工作流，而无需在JEE上安装AEM Forms的全套流程管理功能。 以下内容有一些区别 [OSGi上AEM Forms的表单中心工作流功能和JEE上AEM Forms的流程管理功能](capabilities-osgi-jee-workflows.md). 在OSGi上的AEM Forms上开发和管理以表单为中心的工作流，使用的是熟悉的AEM Workflow和AEM Inbox功能。

## 术语 {#terminologies}

下图显示了典型AEM Forms部署中使用的各种AEM表单服务器配置及其组件：

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**作者：** 创作实例是在标准创作运行模式下运行的AEM Forms服务器。 它可以是JEE上的AEM Forms或OSGi环境上的AEM Forms。 它面向内部用户、表单和交互式通信设计人员以及开发人员。 它支持以下功能：

* **创作和管理表单和交互式通信：** 设计人员和开发人员可以创建和编辑自适应表单和交互式通信，上传外部创建的其他类型的表单，例如在AdobeForms Designer中创建的表单，并使用Forms Manager控制台管理这些资源。
* **表单和交互式通信发布：** 可以将在创作实例上托管的资产发布到发布实例以执行运行时操作。 资产发布使用AEM复制功能。 Adobe建议在所有创作实例上配置复制代理，以手动将发布的表单推送到处理实例，并在使用处理实例时配置另一个复制代理。 *接收时* 触发器已启用，可自动将收到的表单复制到发布实例。

**发布：** 发布实例是在标准发布运行模式下运行的AEM Forms服务器。 发布实例面向基于表单的应用程序的最终用户，例如访问公共网站和提交表单的用户。 它支持以下功能：

* 呈现和提交最终用户的Forms。
* 将原始提交的表单数据传输到处理实例，以供进一步处理并存储在最终记录系统中。 AEM Forms中提供的默认实施是使用AEM的反向复制功能来实现这一点的。 此外，还可以使用替代实施将表单数据直接推送到处理服务器，而不是先在本地保存（后者是激活反向复制的先决条件）。 担心发布实例上存储潜在敏感数据的客户可以加入讨论 [替代实施](/help/forms/using/configuring-draft-submission-storage.md)，因为处理实例通常位于更安全的区域中。
* 呈现和提交交互式通信和信件：在发布实例上呈现交互式通信和信件，并将相应数据提交到处理实例以供存储和后处理。 数据可以在发布实例上本地保存并在以后反向复制到处理实例（默认选项），也可以直接推送到处理实例而不保存在发布实例上。 后一种实施对于注重安全的客户非常有用。

**正在处理：** AEM Forms实例在创作运行模式下运行，未将任何用户分配给forms-manager组。 您可以在JEE上部署AEM Forms，或在OSGi上部署AEM Forms作为处理实例。 未分配用户以确保表单创作和管理活动不在处理实例上执行，并且仅在创作实例上发生。 处理实例可启用以下功能：

* **处理从发布实例到达的原始表单数据：** 这主要在通过AEM工作流处理的实例上实现，当数据到达时，将触发该工作流。 工作流可以使用现成的表单数据模型步骤将数据或文档存档到适当的数据存储。
* **安全存储表单数据**：处理过程为与用户隔离的原始表单数据提供了一个防火墙后的存储库。 创作实例上的表单设计人员和发布实例上的最终用户均无法访问此存储库。

  >[!NOTE]
  >
  >Adobe建议使用第三方数据存储来保存最终处理数据，而不是使用AEM存储库。

* **对从Publish实例到达的通信数据的存储和后处理：** AEM工作流可对相应的信件定义执行可选的后处理。 这些工作流可以将最终处理的数据保存到合适的外部数据存储中。

* **HTML工作区托管**：处理实例托管HTML工作区的前端。 HTML工作区为审阅和批准流程提供了相关任务/组分配的UI。

处理实例配置为在创作运行模式下运行，因为：

* 它允许从发布实例反向复制原始表单数据。 默认数据存储处理程序需要反向复制功能。
* 建议在创作样式系统上运行AEM工作流，这是处理从发布实例到达的原始表单数据的主要方式。

## JEE上AEM Forms的物理拓扑示例 {#sample-physical-topologies-for-aem-forms-on-jee}

下面推荐的AEM Forms on JEE拓扑主要适用于从JEE上的LiveCycle或以前版本的AEM Forms进行升级的客户。 Adobe建议在OSGi上使用AEM Forms进行全新安装。 建议在JEE上重新安装AEM Forms ，但只是为了使用Document Security和Process Management功能。

### 用于使用Document Services或Document Security功能的拓扑 {#topology-for-using-document-services-or-document-security-capabilities}

计划仅使用document services或document security功能的AEM Forms客户可以具有与下面显示的拓扑类似的拓扑。 此拓扑建议使用单个AEM Forms实例。 如有必要，您还可以创建AEM Forms服务器的群集或场。 当大多数用户以编程方式访问AEM Forms服务器的功能且通过用户界面进行干预最小时，建议使用此拓扑。 该拓扑有助于文档服务的批处理操作。 例如，使用输出服务每天创建数百个不可编辑的PDF文档。

虽然AEM Forms允许您从一台服务器设置和运行所有功能，但您应该进行容量规划、负载平衡，并为生产环境中的特定功能设置专用服务器。 例如，对于使用PDF Generator服务每天转换数千页并添加数字签名以限制访问文档的环境，请为PDF Generator服务和数字签名功能设置单独的AEM Forms服务器。 它有助于提供最佳性能并扩展相互独立的服务器。

![基本功能](assets/basic-features.png)

### 使用AEM Forms进程管理的拓扑 {#topology-for-using-aem-forms-process-management}

例如，计划使用AEM Forms流程管理功能的AEM Forms客户，HTML工作区可以具有与下面显示的拓扑类似的拓扑。 JEE服务器上的AEM Forms可以在单个服务器或群集配置中。

如果您从LiveCycleES4进行升级，此拓扑会与LiveCycle中已有的内容紧密镜像，但AEM Author内置到AEM Forms on JEE中的内容除外。 此外，对于执行升级的客户，群集要求没有变化。 如果您在群集环境中使用AEM Forms，则可以在AEM 6.5 Forms中继续使用相同功能。 要重新安装JEE的AEM Forms以使用HTML工作区，还需要运行内置于JEE环境中的AEM创作实例。

表单数据存储是第三方数据存储器，用于存储表单和交互式通信的最终处理数据。 这是拓扑中的可选元素。 您还可以根据需要选择设置处理实例，并将其存储库用作最终记录系统。

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

建议此拓扑图面向计划使用AEM Forms on JEE Server实现流程管理功能(HTML工作区)的客户，而不使用任何后处理、自适应表单、HTML5表单和交互式通信功能。

### 用于使用自适应表单、HTML5表单和交互式通信功能的拓扑 {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

计划使用AEM Forms数据捕获功能(例如自适应表单、HTML5 Forms、PDF forms)的AEM Forms客户可以具有与下面显示的拓扑类似的拓扑。 此外，还建议使用此拓扑来使用AEM Forms的交互式通信功能。

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

您可以对上述建议的拓扑进行以下更改/定制：

* 使用HTML工作区和AEM Forms应用程序需要AEM创作或处理实例。 您可以使用内置到JEE服务器上AEM Forms的AEM创作实例，而不是设置额外的外部AEM创作服务器。
* 只有在OSGi、自适应表单、表单门户和交互式通信上以Forms为中心的工作流，才需要AEM创作或处理实例。
* 交互式通信代理UI通常在组织内运行。 因此，您可以在专用网络中为Agent UI保留发布服务器。
* JEE服务器上内置到AEM Forms的OSGi实例上的AEM表单也可以在OSGi和Watched文件夹上运行以Forms为中心的工作流。

## 在OSGi上使用AEM Forms的物理拓扑示例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### OSGi功能上的数据捕获、交互式通信、以表单为中心的工作流的拓扑 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

计划使用AEM Forms数据捕获功能(例如自适应表单、HTML5 Forms、PDF forms)的AEM Forms客户可以具有与下面显示的拓扑类似的拓扑。 此外，还建议将此拓扑用于在OSGi功能上使用交互式通信和Forms为中心的工作流，例如，将AEM收件箱和AEM Forms应用程序用于业务流程工作流。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 用于使用watched文件夹功能进行脱机批处理的拓扑 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

计划使用Watched文件夹进行批处理的AEM Forms客户可以具有与下面显示的拓扑相似的拓扑。 拓扑显示一个群集环境，但您决定根据负载使用单个实例或AEM Forms服务器场。 第三方数据源是您自己的记录系统。 它用作Watched文件夹的输入源。 拓扑还会以打印文件的形式显示输出。 您还可以将输出内容存储到文件系统，通过电子邮件发送，并使用其他自定义方法来使用输出。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### 使用文档服务功能进行基于API的离线处理的拓扑 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

计划仅使用document services功能的AEM Forms客户可以具有与下面显示的拓扑类似的拓扑。 此拓扑建议在OSGi服务器上使用AEM Forms群集。 当大多数用户以编程方式（使用API）访问AEM Forms服务器的功能且通过用户界面进行干预最小时，建议使用此拓扑。 该拓扑在多个软件客户端场景中非常有用。 例如，多个客户端使用PDF Generator服务按需创建PDF文档。

虽然AEM Forms允许您从一台服务器设置和运行所有功能，但您应该进行容量规划、负载平衡，并为生产环境中的特定功能设置专用服务器。 例如，对于使用PDF Generator服务每天转换数千页以及使用多个自适应表单捕获数据的环境，请为PDF Generator服务和自适应表单功能设置单独的AEM Forms服务器。 它有助于提供最佳性能并扩展相互独立的服务器。

![基于离线api的处理](assets/offline-api-based-processing.png)
