---
title: 内容片段的组件
seo-title: Components for Content Fragments
description: AEM内容片段是作为独立于页面的资产创建和管理的
seo-description: AEM content fragments are created and managed as page-independent assets
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: de774bec7440805273928267ea6c09669720ea24
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 3%

---

# 内容片段的组件{#components-for-content-fragments}

## 用于片段创作的组件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建议扩展或更改片段编辑器中使用的实际组件，因为它们仍可能发生更改。

请参阅 [内容片段管理API — 客户端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## 用于创作页面的组件 {#components-for-page-authoring}

>[!CAUTION]
>
>的 [内容片段核心组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 现在建议。 请参阅 [开发核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) 以了解更多详细信息。
>
>本节详细介绍交付用于内容片段的原始组件(**内容片段** 在 **常规** 组)。

>[!NOTE]
>
>另请参阅 [内容片段配置用于渲染的组件](/help/sites-developing/content-fragments-config-components-rendering.md) 以了解更多信息。

Adobe Experience Manager (AEM) 内容片段[作为独立于页面的资产而创建和管理](/help/assets/content-fragments/content-fragments.md)。这允许您创建渠道中性内容，以及各种（特定于渠道的）变量。[然后，在创作内容页面时，您可以使用这些片段及其变体](/help/sites-authoring/content-fragments.md). 您还可以通过 [将其从资产浏览器拖到页面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （对于其他基于资产的组件，例如基础组件图像）。 现成的内容片段组件仅显示一个 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 引用内容片段的URL。 使用组件对话框，您可以定义 [元素、变体和片段段落范围](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 页面上显示的内容。

>[!NOTE]
>
>此内容片段组件作为文章组件的增强版本在AEM 6.2中引入，该组件已弃用。

>[!NOTE]
>
>经典UI中不支持内容片段。

### 定义 {#definition}

的 **内容片段** 组件用于保存对内容片段资产（有效地增强了文本资产）的引用。 内容片段的资源类型为：

`dam/cfm/components/contentfragment/contentfragment`

引用在属性中定义：

`fileReference`

只有触屏优化UI的编辑器完全支持内容片段组件，该组件包括客户端库：

`cq.authoring.editor.plugin.cfm`

此库会将特定于内容片段的功能添加到编辑器中。 例如，支持在页面上添加和配置内容片段的功能，在资产浏览器中搜索内容片段资产的功能，以及侧面板中的关联内容。

### 中间内容 {#in-between-content}

的 **内容片段** t组件允许您将其他组件放置在所显示的不同段落之间 [元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 显示的元素基本上由不同的段落组成（每个段落都标有回车符）。 在这些段落之间，您可以使用其他组件插入内容。

从技术角度来看，显示的元素* *的每个段落都位于其自己的Parsys中，并且您在段落之间添加的每个组件都将（在引擎盖下）插入到Parsys中。

换言之，如果内容片段组件的实例由三个段落组成，则组件在存储库中将具有三个不同的parsys。 添加到内容片段的所有中间内容实际上都将位于这些Parsys内。

在存储库中，中间内容相对于其在整体段落结构中的位置进行存储，即它未附加到实际段落内容。

为了说明这一点，让我们考虑一下：

* 由三个段落组成的内容片段的实例
* 第二段之后已经插入了一些内容

   * 这意味着内容将存储在第二个Parsys中。

基本上，如果此实例的段落结构发生更改（通过更改显示的变体、元素或段落范围），则可能影响内容片段内容时显示的中间内容：

* 编辑，并在第二段之前添加另一个段落：

   * 中间内容将在新创建的段落之后显示（第二个Parsys现在包含新创建的段落）。

* 编辑并删除第二个段落：

   * 中间内容将显示在之前为第三个段落的段落之后（第二个Parsys现在包含前一个第三个段落）。

* 已配置，以便仅显示第一个段落：

   * 将不显示中间内容（由于新配置，第二个Parsys不再呈现）。

### 自定义内容片段组件 {#customizing-the-content-fragment-component}

要将现成的内容片段组件用作扩展的蓝图，您应遵守以下合同：

* 重复使用HTL渲染脚本及其关联的POJO，以查看中间内容功能的实施方式。
* 重复使用内容片段节点： `cq:editConfig`

   * 的 `afterinsert`/ `afteredit`/ `afterdelete` 侦听器用于触发JS事件。 这些事件将在 `cq.authoring.editor.plugin.cfm` 客户端库，在侧面板中显示相关内容。
   * 的 `cq:dropTargets` 配置为支持拖动内容片段资产。
   * `cq:inplaceEditing` 配置为支持在页面编辑器中创作内容片段。 片段就地编辑器在 `cq.authoring.editor.plugin.cfm` 客户端库，并允许快速链接打开当前 [元素/变量](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 在 [片段编辑器](/help/assets/content-fragments/content-fragments-variations.md).

### 渲染前资产重写 {#asset-rewriting-before-rendering}

内容片段管理使用内部渲染过程为页面生成最终HTML输出。 内容片段组件可在内部使用，也可由在引用页面上更新引用片段的后台进程使用。

在内部，Sling重写程序用于进行渲染。 相关配置位于 `/libs/dam/config/rewriter/cfm` 和可根据需要进行调整。 请参阅 [Apache Sling重写程序](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 以了解更多信息。

>[!CAUTION]
>
>如果您确实调整/叠加重写器的配置：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然后 `serializerType` **必须** 更新为：
>
>* `serializerType="html5-serializer"`


开箱即用的配置使用以下变压器：

* `transformer-cfm-payloadfilter`  — 用于检索 `body` 部件( `<body>...</body>`)的HTML

* `transformer-cfm-parfilter`  — 如果指定了段落范围，则会过滤掉不需要的段落（与内容片段组件的操作一样）
* `transformer-cfm-assetprocessor`  — 在内部用于检索片段中嵌入的资产列表

渲染过程将通过 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 和（例如）可根据需要通过自定义组件来使用。
