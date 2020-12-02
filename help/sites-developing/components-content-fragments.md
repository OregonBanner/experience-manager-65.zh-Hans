---
title: 内容片段的组件
seo-title: 内容片段的组件
description: AEM内容片段是作为独立于页面的资产创建和管理的
seo-description: AEM内容片段是作为独立于页面的资产创建和管理的
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 3%

---


# 内容片段的组件{#components-for-content-fragments}

## 片段创作组件{#components-for-fragment-authoring}

>[!CAUTION]
>
>不建议扩展或更改片段编辑器中使用的实际组件，因为它们仍可能更改。

请参阅[内容片段管理API —— 客户端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 用于创作页面的组件 {#components-for-page-authoring}

>[!CAUTION]
>
>现在建议使用[内容片段核心组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)。 有关详细信息，请参阅[开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)。
>
>本节详细介绍了交付用于内容片段的原始组件（**常规**&#x200B;组中的&#x200B;**内容片段**）。

>[!NOTE]
>
>另请参阅[内容片段配置要渲染的组件](/help/sites-developing/content-fragments-config-components-rendering.md)以了解详细信息。

Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变量。[然后，在创作内容页面时，您可以使用这些片段及其变体](/help/sites-authoring/content-fragments.md)。您还可以通过[将现有内容片段资产从资产浏览器拖动到页面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)来使用该资产（对于其他基于资产的组件，如基础组件图像）。 现成的内容片段组件仅显示引用的内容片段的一个[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。 使用组件对话框，您可以定义要在页面上显示的[元素、变体和片段段落范围](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

>[!NOTE]
>
>AEM 6.2中引入了此内容片段组件，作为文章组件的增强版本，该组件已弃用。

>[!NOTE]
>
>经典UI中不支持内容片段。

### 定义 {#definition}

**内容片段**&#x200B;组件用于保存对内容片段资产（有效增强的文本资产）的引用。 内容片段的资源类型为：

`dam/cfm/components/contentfragment/contentfragment`

引用在属性中定义：

`fileReference`

只有触屏优化UI的编辑器完全支持内容片段组件，其中包括客户端库：

`cq.authoring.editor.plugin.cfm`

此库向编辑器添加特定于内容片段的功能。 例如，支持在页面上添加和配置内容片段的功能、在资产浏览器中搜索内容片段资产以及侧面板中的关联内容。

### 中间内容{#in-between-content}

**内容片段** t组件允许您在显示的[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)的不同段落之间放置其他组件。 显示的元素基本上由不同段落组成（每个段落都标有回车符）。 在这些段落之间，您可以使用其他组件插入内容。

从技术角度看，显示的元素* *的每个段落都位于其自己的parsys中，您在段落之间添加的每个组件都将（在外罩下）插入parsys中。

换言之，如果内容片段组件的实例由三个段落组成，则该组件在存储库中将具有三个不同的parsys。 添加到内容片段的所有中间内容实际上将位于这些parsys中。

在存储库中，中间内容会相对于其在整个段落结构中的位置进行存储，即它不会附加到实际的段落内容。

为了说明这一点，我们考虑一下：

* 由三个段落组成的内容片段的实例
* 而且，某些内容已在第二段之后插入

   * 这意味着内容将存储在第二个parsys中。

基本上，如果此实例的段落结构发生更改（通过更改显示的变体、元素或段落范围），则可能影响内容片段内容时显示的中间内容：

* 编辑，并在第二段前添加另一个段落：

   * 中间内容将在新创建的段落后显示（第二个段落现在包含新创建的段落）。

* 已编辑并删除第二个段落：

   * 中间内容将显示在之前是第三个段落的段落之后（第二个段落现在包含前一个第三个段落）。

* 已进行配置，以便仅显示第一个段落：

   * 将不显示中间内容（由于新配置，第二个parsys不再呈现）。

### 自定义内容片段组件{#customizing-the-content-fragment-component}

要将现成内容片段组件用作扩展蓝图，您应遵守以下合同：

* 重用HTL渲染脚本及其关联的POJO，查看如何实现中间内容功能。
* 重用内容片段节点：`cq:editConfig`

   * `afterinsert`/ `afteredit`/ `afterdelete`监听器用于触发JS事件。 这些事件将在`cq.authoring.editor.plugin.cfm`客户端库中处理，以在侧面板中显示相关内容。
   * `cq:dropTargets`配置为支持拖动内容片段资产。
   * `cq:inplaceEditing` 配置为支持在页面编辑器中创作内容片段。片段就地编辑器在`cq.authoring.editor.plugin.cfm`客户端库中定义，并允许快速链接在[片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)中打开当前的[元素／变量](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

### 渲染{#asset-rewriting-before-rendering}前资源重写

内容片段管理使用内部渲染过程为页面生成最终HTML输出。 这由内容片段组件在内部使用，也由在引用页面上更新引用片段的后台进程使用。

在内部，Sling Rewriter用于该渲染。 各个配置位于`/libs/dam/config/rewriter/cfm`，可根据需要进行调整。 有关详细信息，请参阅[Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)。

现成配置使用以下变压器：

* `transformer-cfm-payloadfilter` -仅用于 `body` 检索片 `<body>...</body>`段的HTML的部件()

* `transformer-cfm-parfilter` -如果指定了段落范围，则过滤器掉不需要的段落（如使用内容片段组件所做）
* `transformer-cfm-assetprocessor` -在内部用于检索嵌入在片段中的资产列表

渲染过程通过[`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)公开，如果需要，可由自定义组件利用（例如）。
