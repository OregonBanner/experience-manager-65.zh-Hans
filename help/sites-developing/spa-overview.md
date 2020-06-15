---
title: SPA编辑器概述
seo-title: SPA编辑器概述
description: 本文全面概述了SPA编辑器及其工作方式，包括AEM中SPA编辑器交互的详细工作流。
seo-description: 本文全面概述了SPA编辑器及其工作方式，包括AEM中SPA编辑器交互的详细工作流。
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: fe81a72a6269060a7ec1283f817920618ba715ef
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 0%

---


# SPA编辑器概述{#spa-editor-overview}

单页应用程序(SPA)可以为网站用户优惠引人入胜的体验。 开发人员希望能够使用SPA框架构建站点，作者希望在AEM中为使用此类框架构建的站点无缝编辑内容。

SPA编辑器为在AEM中支持SPA提供了全面的解决方案。 本页概述了SPA支持在AEM中的结构、SPA编辑器的工作方式以及SPA框架和AEM保持同步的方式。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（如“反应”或“角度”）的项目，建议使用SPA编辑器。

## 简介 {#introduction}

使用常见SPA框架（如React和Angular）构建的站点通过动态JSON加载其内容，并且不提供AEM页面编辑器必须的HTML结构才能放置编辑控件。

要在AEM中启用SPA编辑，需要SPA的JSON输出与AEM存储库中的内容模型之间的映射才能保存对内容所做的更改。

AEM中的SPA支持引入了一个精简JS层，当在页面编辑器中加载时，该层会与SPA JS代码交互，事件可通过该层发送，编辑控件的位置也可以激活，以便进行上下文编辑。 此功能基于Content Services API端点概念，因为SPA中的内容需要通过Content Services加载。

有关AEM中SPA的更多详细信息，请参阅以下文档:

* [SPA Blueprint](/help/sites-developing/spa-blueprint.md) （SPA技术要求）
* [AEM中的SPA入门](/help/sites-developing/spa-getting-started-react.md) ，快速浏览简单的SPA

## 设计 {#design}

SPA的页面组件不会通过JSP或HTL文件提供其子组件的HTML元素。 此操作被委派到SPA框架。 子组件或模型的表示形式从JCR中作为JSON数据结构获取。 SPA组件随后会根据该结构添加到页面。 此行为使页面组件的初始主体构成与非SPA组件的相对应部分区别开来。

### 页面模型管理 {#page-model-management}

页面模型的解析和管理被委托给提供的 `PageModel` 库。 SPA必须使用页面模型库才能进行初始化并由SPA编辑器创作。 页面模型库通过npm间接提供给AEM页面组 `cq-react-editable-components` 件。 页面模型是AEM和SPA之间的解释器，因此始终必须存在。 创作页面时，必须添加其 `cq.authoring.pagemodel.messaging` 他库才能启用与页面编辑器的通信。

如果SPA页面组件从页面核心组件继承内容，则有两个选项可使客户端库 `cq.authoring.pagemodel.messaging` 类别可用：

* 如果模板是可编辑的，则将其添加到页面策略。
* 或者使用添加类别 `customfooterlibs.html`。

对于导出模型中的每个资源，SPA将映射一个将进行渲染的实际组件。 该模型表示为JSON，然后使用容器中的组件映射进行呈现。
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>包含类别 `cq.authoring.pagemodel.messaging` 应限于SPA编辑器的上下文。

### 通信数据类型 {#communication-data-type}

将类别 `cq.authoring.pagemodel.messaging` 添加到页面时，它将向页面编辑器发送消息，以建立JSON通信数据类型。 当通信数据类型设置为JSON时，GET请求将与组件的Sling Model端点进行通信。 在页面编辑器中进行更新后，已更新组件的JSON表示形式将发送到页面模型库。 页面模型库随后会通知SPA更新。

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## 工作流 {#workflow}

您可以将SPA编辑器视为SPA和AEM之间的调解者，从而了解SPA与AEM之间的交互流程。

* 页面编辑器与SPA之间的通信是使用JSON而不是HTML进行的。
* 页面编辑器通过iframe和消息传递API向SPA提供最新版本的页面模型。
* 页面模型管理器会通知编辑者已准备好进行编辑，并将页面模型作为JSON结构传递。
* 编辑者不会更改或甚至访问所创作页面的DOM结构，而是提供最新的页面模型。

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### 基本SPA编辑器工作流程 {#basic-spa-editor-workflow}

请注意SPA编辑器的关键元素，创作者可以按如下方式了解在AEM中编辑SPA的高级工作流程。

![untitled1](assets/untitled1.gif)

1. 加载SPA编辑器。
1. SPA加载在单独的框架中。
1. SPA请求JSON内容并在客户端呈现组件。
1. SPA编辑器检测渲染的组件并生成叠加。
1. 创作单击叠加，显示组件的编辑工具栏。
1. SPA编辑器会持续对服务器进行编辑，并向服务器发出POST请求。
1. SPA编辑器向SPA编辑器请求更新的JSON,SPA编辑器会通过DOM事件发送到SPA。
1. SPA重新呈现相关组件，更新其DOM。

>[!NOTE]
>
>记住：
>
>* SPA总是负责其展示。
>* SPA编辑器与SPA本身隔离。
>* 在生产（发布）中，从不加载SPA编辑器。

>



### 客户端——服务器页面编辑工作流 {#client-server-page-editing-workflow}

这是编辑SPA时客户端与服务器交互的更详细概述。

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA将自行初始化，并从Sling Model Exporter请求页面模型。
1. Sling Model Exporter从存储库请求组成页面的资源。
1. 存储库返回资源。
1. Sling Model Exporter返回页面的模型。
1. SPA根据页面模型实例化其组件。
1. **6a内容** 会通知编辑者已准备好进行创作。

   **6b页面编辑器** 请求组件创作配置。

   **6c页面** 编辑器接收组件配置。
1. 作者编辑组件时，页面编辑器会将修改请求发布到默认的POST servlet。
1. 资源会在存储库中更新。
1. 更新的资源被提供给POST servlet。
1. 默认的POST servlet通知页面编辑器资源已更新。
1. 页面编辑器请求新的页面模型。
1. 从存储库请求构成页面的资源。
1. 组成页面的资源由存储库提供给Sling Model Exporter。
1. 更新的页面模型将返回到编辑器。
1. 页面编辑器更新SPA的页面模型参考。
1. SPA会根据新的页面模型参考更新其组件。
1. 页面编辑器的组件配置将更新。

   **17a SPA** 向页面编辑器发出指示，内容已准备就绪。

   **17b页面编辑器** 为SPA提供组件配置。

   **17c SPA** 提供更新的组件配置。

### 创作工作流 {#authoring-workflow}

这是更详细的概述，重点介绍创作体验。

![spa_content_authoring模型](assets/spa_content_authoringmodel.png)

1. SPA获取页面模型。
1. **2a页面** 模型为编辑者提供创作所需的数据。

   **2b通知** ,component orchestrator会更新页面的内容结构。
1. 组件查询器可以管理AEM资源类型与SPA组件之间的映射。
1. 组件管理器根据页面模型和组件映射动态地实例化SPA组件。
1. 页面编辑器会更新页面模型。
1. **6a页面模型** 为页面编辑器提供了更新的创作数据。

   **6b** page model将更改调度给component orchestrator。
1. 组件Orchestrator获取组件映射。
1. component orchestrator更新页面内容。
1. 当SPA完成更新页面内容时，页面编辑器将加载创作环境。

## 要求和限制 {#requirements-limitations}

要使作者能够使用页面编辑器编辑SPA的内容，必须实施您的SPA应用程序才能与AEM SPA Editor SDK进行交互。 请参阅AEM [文档中的SPA快速入门](/help/sites-developing/spa-getting-started-react.md) ，了解让您的SPA投入运行所需的最低要求。

### 支持的框架 {#supported-frameworks}

SPA编辑器SDK支持以下最低版本：

* 响应16.x及更高
* 角度6.x和向上

这些框架的先前版本可能与AEM SPA Editor SDK一起使用，但不支持。

### 其他框架 {#additional-frameworks}

可以实施其他SPA框架以与AEM SPA Editor SDK配合使用。 请参阅 [SPA Blueprint文档](/help/sites-developing/spa-blueprint.md) ，了解框架创建框架特定层时必须满足的要求，该层由模块、组件和服务组成，以与AEM SPA Editor结合使用。

### 使用多个选择器 {#multiple-selectors}

可以定义其他自定义选择器并将其用作为为AEM SPA SDK开发的SPA的一部分。 但是，此支持要求选 `model` 择器是第一个选择器，而扩展是 `.json` JSON导 [出器所需的。](json-exporter-components.md#multiple-selectors)

### 文本编辑器要求 {#text-editor-requirements}

如果要使用在SPA中创建的文本组件的就地编辑器，则需要其他配置。

1. 在包含文本HTML的容器包装器元素上设置属性（它可以是任何属性）。 对于WKND日志范例内容，它是一 `<div>` 个元素，已使用的选择器 `data-rte-editelement`。
1. 在相应的 `editElementQuery` AEM文本组件上设置指向该选 `cq:InplaceEditingConfig` 择器的配置，例如， `data-rte-editelement`. 这样，编辑者就知道哪些HTML元素会包裹HTML文本。

有关如何实现此操作的示例，请参阅 [WKND日志范例内容。](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

有关富文本编 `editElementQuery` 辑器属性和配置的其他信息，请参 [阅配置富文本编辑器。](/help/sites-administering/rich-text-editor.md)

### 限制 {#limitations}

AEM 6.4 service pack 2引入了AEM SPA Editor SDK。 它得到Adobe的全面支持，并且作为一项新功能，它将继续得到增强和扩展。 SPA编辑器尚不支持以下AEM功能：

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
