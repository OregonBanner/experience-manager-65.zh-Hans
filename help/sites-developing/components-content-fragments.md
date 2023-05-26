---
title: 内容片段的组件
seo-title: Components for Content Fragments
description: AEM内容片段作为独立于页面的资产进行创建和管理
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 3%

---

# 内容片段的组件{#components-for-content-fragments}

## 用于片段创作的组件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建议扩展或更改片段编辑器中使用的实际组件，因为它们仍可能会发生更改。

请参阅 [内容片段管理API — 客户端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## 用于页面创作的组件 {#components-for-page-authoring}

>[!CAUTION]
>
>此 [内容片段核心组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 现在建议使用。 参见 [开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 了解更多详细信息。
>
>此部分详细介绍为与内容片段一起使用而交付的原始组件(**内容片段** 在 **常规** 组)。

>[!NOTE]
>
>另请参阅 [内容片段配置用于呈现的组件](/help/sites-developing/content-fragments-config-components-rendering.md) 以进一步了解。

Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变体。[然后，您可以在创作内容页面时使用这些片段及其变体](/help/sites-authoring/content-fragments.md). 您还可以通过以下方式使用现有内容片段资源 [将其从资源浏览器拖到页面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （对于其他基于资产的组件，例如基础组件图像）。 现成的内容片段组件仅显示一个 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 引用的内容片段的。 使用组件对话框，您可以定义 [元素、变量和片段段落范围](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 要显示在页面上的内容。

>[!NOTE]
>
>此内容片段组件作为Article组件的增强版本引入到AEM 6.2中，该版本已弃用。

>[!NOTE]
>
>经典UI中不支持内容片段。

### 定义 {#definition}

此 **内容片段** 组件用于保存对内容片段资产（有效增强的文本资产）的引用。 内容片段的资源类型为：

`dam/cfm/components/contentfragment/contentfragment`

引用在属性中定义：

`fileReference`

只有触屏UI的编辑器完全支持内容片段组件，其中包括客户端库：

`cq.authoring.editor.plugin.cfm`

此库将特定于内容片段的功能添加到编辑器。 例如，支持在页面上添加和配置内容片段的功能，支持在资产浏览器中搜索内容片段资产的功能，以及在侧面板中搜索关联内容的功能。

### 中间内容 {#in-between-content}

此 **内容片段** t组件允许您在显示的不同段落之间放置其他组件 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 基本上，显示的元素由不同的段落组成（每个段落都标有一个回车符）。 在每个段落之间，您可以使用其他组件插入内容。

从技术角度来看，所显示元素* *的每个段落都位于自己的parsys中，您在段落之间添加的每个组件都将（在标题下）插入parsys中。

换句话说，如果内容片段组件的实例由三个段落组成，则组件在存储库中将具有三个不同的parsys。 添加到内容片段的所有中间内容实际上将位于这些parsys中。

在存储库中，中间内容相对于其在整个段落结构中的位置进行存储，即，它未附加到实际的段落内容。

为了说明这一点，让我们考虑一下：

* 由三个段落组成的内容片段的实例
* 并且某些内容已经插入到第二段之后

   * 这意味着该内容将存储在第二个parsys中。

基本上，如果此实例的段落结构发生更改（通过更改显示的变体、元素或段落范围），它可能会影响在内容片段内容时显示的中间内容：

* 编辑，并在第二段之前添加另一段：

   * 中间内容将显示在新创建的段落之后（第二个parsys现在包含新创建的段落）。

* 编辑并删除第二段：

   * 中间内容将显示在之前是第三段的段落之后（第二个parsys现在包含前三个段落）。

* 进行了配置，以便仅显示第一段：

   * 将不会显示中间内容（由于新配置，第二个parsys不再呈现）。

### 自定义内容片段组件 {#customizing-the-content-fragment-component}

要使用现成的内容片段组件作为扩展的蓝图，您应遵守以下合同：

* 重用HTL渲染脚本及其关联的POJO以查看中间内容功能的实施方式。
* 重用内容片段节点： `cq:editConfig`

   * 此 `afterinsert`/ `afteredit`/ `afterdelete` 监听器用于触发JS事件。 这些事件将在中进行处理 `cq.authoring.editor.plugin.cfm` 客户端库，可在侧面板中显示关联内容。
   * 此 `cq:dropTargets` 配置为支持拖动内容片段资产。
   * `cq:inplaceEditing` 配置为支持在页面编辑器中创作内容片段。 片段就地编辑器在中定义 `cq.authoring.editor.plugin.cfm` 客户端库，并允许快速链接打开当前 [元素/变量](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 在 [片段编辑器](/help/assets/content-fragments/content-fragments-variations.md).

### 呈现前资源重写 {#asset-rewriting-before-rendering}

内容片段管理使用内部渲染过程为页面生成最终HTML输出。 这由内容片段组件在内部使用，也由后台进程使用，该进程更新引用页面上的引用片段。

在内部，Sling重写器用于该渲染。 相应的配置位于 `/libs/dam/config/rewriter/cfm` 并且可以根据需要进行调整。 请参阅 [Apache Sling重写器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 了解更多信息。

>[!CAUTION]
>
>如果您调整/叠加重写器的配置：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然后 `serializerType` **必须** 将更新为：
>
>* `serializerType="html5-serializer"`


开箱即用配置使用以下转换器：

* `transformer-cfm-payloadfilter`  — 用于检索 `body` 部件( `<body>...</body>`)的片段HTML

* `transformer-cfm-parfilter`  — 如果指定了段落范围，则过滤掉不需要的段落（使用内容片段组件可以这样做）
* `transformer-cfm-assetprocessor`  — 在内部用于检索片段中嵌入的资产列表

呈现过程将通过以下方式公开 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 如果需要，自定义组件可以使用（例如）和。
