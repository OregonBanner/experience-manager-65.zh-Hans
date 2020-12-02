---
title: SPA编辑器概述
seo-title: SPA编辑器概述
description: 本文全面概述SPA Editor及其工作方式，包括AEM Editor在SPA内的一工作流详细交互。
seo-description: 本文全面概述SPA Editor及其工作方式，包括AEM Editor在SPA内的一工作流详细交互。
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 0%

---


# SPA Editor概述{#spa-editor-overview}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，而作者希望无缝编辑AEM中的内容，以便使用此类框架构建站点。

SPA Editor优惠了在AEM内支持SPA的全面解决方案。 本页概述SPA支持在AEM中的结构化、SPA编辑器的工作方式以及SPA框架和AEM保持同步的方式。

>[!NOTE]
>
>SPA编辑器是需要SPA框架的客户端渲染（例如，React或Angular）的项目的推荐解决方案。

## 简介 {#introduction}

使用通用SPA框架（如React和Angular）构建的站点通过动态JSON加载其内容，并且不提供AEM页面编辑器必须的HTML结构才能放置编辑控件。

要在AEM中启用SPA的编辑，需要SPA的JSON输出与AEM存储库中的内容模型之间的映射才能保存对内容所做的更改。

SPA中的AEM支持引入了精简JS层，当在页面编辑器中加载时，该层会与SPA JS代码交互，通过该层可以发送事件，并激活编辑控件的位置以允许上下文编辑。 此功能基于Content Services API端点概念，因为SPA中的内容需要通过Content Services加载。

有关AEM中SPA的更多详细信息，请参阅以下文档:

* [SPA ](/help/sites-developing/spa-blueprint.md) Blueprint了解SPA的技术要求
* [在AEM中快速](/help/sites-developing/spa-getting-started-react.md) 入门SPA以快速浏览简单的SPA

## 设计 {#design}

SPA的页面组件不通过JSP或HTL文件提供其子组件的HTML元素。 此操作委托给SPA框架。 子组件或模型的表示形式从JCR中作为JSON数据结构获取。 然后，SPA组件会根据该结构添加到页面。 此行为将页面组件的初始主体组合与非SPA组件的相对应部分区分开。

### 页面模型管理{#page-model-management}

页面模型的解析和管理委托给提供的`PageModel`库。 SPA必须使用页面模型库才能进行初始化，并由SPA编辑器进行创作。 页面模型库通过`aem-react-editable-components` npm间接提供给AEM页面组件。 页面模型是AEM和SPA之间的解释器，因此始终必须存在。 创作页面时，必须添加一个额外的库`cq.authoring.pagemodel.messaging`，以启用与页面编辑器的通信。

如果SPA页面组件从页面核心组件继承内容，则有两个选项可以使`cq.authoring.pagemodel.messaging`客户端库类别可用：

* 如果模板是可编辑的，则将其添加到页面策略。
* 或者使用`customfooterlibs.html`添加类别。

对于导出模型中的每个资源，SPA将映射一个实际组件，以执行
呈现。 该模型表示为JSON，然后使用容器中的组件映射进行呈现。
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>`cq.authoring.pagemodel.messaging`类别的包含应限于SPA编辑器的上下文。

### 通信数据类型{#communication-data-type}

将`cq.authoring.pagemodel.messaging`类别添加到页面时，它将向页面编辑器发送一条消息，以建立JSON通信数据类型。 当通信数据类型设置为JSON时，GET请求将与组件的Sling Model端点进行通信。 在页面编辑器中进行更新后，已更新组件的JSON表示形式将发送到页面模型库。 页面模型库随后会通知SPA更新。

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## 工作流 {#workflow}

您可以理解SPA和AEM之间的交互流程，将SPA编辑看作是和之间的调解人。

* 页面编辑器与SPA之间的通信是使用JSON而不是HTML进行的。
* 页面编辑器通过iframe和消息API向SPA提供最新版本的页面模型。
* 页面模型管理器会通知编辑者已准备好进行编辑，并将页面模型作为JSON结构传递。
* 编辑者不会更改或甚至访问所创作页面的DOM结构，而是提供最新的页面模型。

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### 基本SPA编辑器工作流{#basic-spa-editor-workflow}

请注意SPA Editor的关键元素，在AEM内编辑SPA的高级工作流程对作者如下所示。

![无标题1](assets/untitled1.gif)

1. SPA Editor加载。
1. SPA加载到单独的帧中。
1. SPA在客户端请求JSON内容并呈现组件。
1. SPA Editor检测渲染的组件并生成叠加。
1. 创作单击叠加，显示组件的编辑工具栏。
1. SPA Editor会持续进行编辑，并向服务器发出POST请求。
1. SPA Editor向SPA Editor请求更新的JSON，该编辑器将使用DOM事件发送到SPA。
1. SPA重新渲染相关组件，更新其DOM。

>[!NOTE]
>
>记住：
>
>* SPA总是负责显示。
>* SPA编辑器与SPA本身相分离。
>* 在生产（发布）中，不会加载SPA编辑器。

>



### 客户端——服务器页面编辑工作流{#client-server-page-editing-workflow}

这是编辑SPA时客户端与服务器交互的更详细概述。

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA将自行初始化，并从Sling Model Exporter请求页面模型。
1. Sling Model Exporter从存储库请求组成页面的资源。
1. 存储库返回资源。
1. Sling Model Exporter返回页面的模型。
1. SPA根据页面模型实例化其组件。
1. **6** a内容会通知编辑者已准备好进行创作。

   **6b** 页面编辑器请求组件创作配置。

   **6** 页面编辑器接收组件配置。
1. 当作者编辑组件时，页面编辑器会将修改请求发布到默认POSTservlet。
1. 资源会在存储库中更新。
1. 更新的资源被提供给POSTservlet。
1. 默认POSTservlet通知页面编辑器资源已更新。
1. 页面编辑器请求新的页面模型。
1. 从存储库请求构成页面的资源。
1. 组成页面的资源由存储库提供给Sling Model Exporter。
1. 更新的页面模型将返回到编辑器。
1. 页面编辑器更新SPA的页面模型参考。
1. SPA会根据新的页面模型参考更新其组件。
1. 页面编辑器的组件配置将更新。

   **17**  aSPA向页面编辑器发出指示，内容已准备就绪。

   **17** b页面编辑器为SPA提供组件配置。

   **17** SPA提供更新的组件配置。

### 创作工作流{#authoring-workflow}

这是更详细的概述，重点介绍创作体验。

![spa_content_authoring模型](assets/spa_content_authoringmodel.png)

1. SPA获取页面模型。
1. **2** a页面模型为编辑者提供创作所需的数据。

   **2b** 当收到通知时，component orchestrator会更新页面的内容结构。
1. 组件查询器将映射到AEM资源类型和SPA组件。
1. component orchestrator根据页面模型和组件映射动态实例化SPA组件。
1. 页面编辑器会更新页面模型。
1. **6a** 页面模型为页面编辑器提供更新的创作数据。

   **6b** 页面模型将更改调度到component orchestrator。
1. 组件Orchestrator获取组件映射。
1. component orchestrator更新页面内容。
1. 当SPA完成更新页面内容时，页面编辑器将加载创作环境。

## 要求和限制{#requirements-limitations}

要使作者能够使用页面编辑器编辑SPA的内容，必须实现SPA应用程序以与SPA AEM编辑器SDK进行交互。 请参阅AEM中的[SPA快速入门文档，了解使您的产品运行所需的最低要求。](/help/sites-developing/spa-getting-started-react.md)

### 支持的框架{#supported-frameworks}

SPA Editor SDK支持以下最低版本：

* 响应16.x及更高
* 角度6.x和向上

这些框架的先前版本可能与AEM SPA Editor SDK一起使用，但不支持。

### 其他框架{#additional-frameworks}

可实施其他SPA框架以与AEM SPA Editor SDK配合使用。 请参见[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文档，了解框架为创建框架特定层以与SPA AEM Editor一起使用而必须满足的要求。

### 使用多个选择器{#multiple-selectors}

可以定义其他自定义选择器并将其用作为AEM SPA SDK开发的SPA的一部分。 但是，此支持要求`model`选择器是第一个选择器，扩展名为`.json`，作为JSON导出器所需的[。](json-exporter-components.md#multiple-selectors)

### 文本编辑器要求{#text-editor-requirements}

如果要使用在SPA中创建的文本组件的就地编辑器，则需要其他配置。

1. 在包含文本HTML的容器包装器元素上设置属性（它可以是任何属性）。 对于WKND日志示例内容，它是`<div>`元素，使用的选择器是`data-rte-editelement`。
1. 在相应的AEM文本组件`cq:InplaceEditingConfig`上设置指向该选择器的配置`editElementQuery`，例如`data-rte-editelement`。 这样，编辑者就知道哪些HTML元素会包裹HTML文本。

有关如何实现此操作的示例，请参阅[WKND日志示例内容。](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

有关`editElementQuery`属性和富文本编辑器配置的详细信息，请参阅[配置富文本编辑器。](/help/sites-administering/rich-text-editor.md)

### 限制 {#limitations}

AEM SPA Editor SDK随AEM 6.4 service pack 2引入。 它完全受Adobe支持，并且作为一项新功能，它将继续得到增强和扩展。 SPA编辑器尚不支持以下AEM功能：

* 目标模式
* ContextHub
* 内联图像编辑
* 编辑配置(例如 监听器)
* 样式系统
* 撤消／重做
* 页面差异和时间扭曲
* 执行HTML重写服务器端功能，如链接检查器、CDN重写器服务、URL缩短等。
* 开发人员模式
* AEM启动项
