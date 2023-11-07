---
title: 模板
description: 创建用作新页面基础的页面时，将使用模板。
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# 模板{#templates}

模板在AEM中的各个时间点使用：

* [创建页面时，您可以选择模板](#templates-pages). 此模板用作新页面的基础。 模板定义页面的结构、任何初始内容以及 [组件](/help/sites-authoring/default-components.md) 可以使用的属性（设计属性）。

* [在创建内容片段时，您还可以选择模板](#templates-content-fragments). 此模板定义结构、初始元素和变体。

以下模板将详细介绍：

* [页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)
* [页面模板 — 静态](/help/sites-developing/page-templates-static.md)
* [内容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自适应模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板 — 页面 {#templates-pages}

AEM现在提供了两种用于创建页面的基本模板类型：

>[!NOTE]
>
>将模板用于 [创建页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)，则没有可见差异（对于页面作者），也未指示所使用的模板类型。

### 可编辑模板 {#editable-templates}

可编辑模板现在被视为使用AEM进行开发的最佳实践。

可编辑模板的优势：

* 可以是 [已创建](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 和 [已编辑](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 你的作者写的。

* 引入后，您可以为使用该模板创建的任何页面定义以下内容：

   * 结构
   * 初始内容
   * 内容策略

* 创建新页面后，页面和模板之间会保持动态连接。 此连接意味着对模板结构的更改会反映在使用该模板创建的任何页面上；对初始内容的更改不会反映在页面上。
* 使用内容策略（从模板编辑器编辑）来保留设计属性（不使用页面编辑器中的设计模式）。
* 存储在 `/conf`
* 请参阅 [可编辑的模板](/help/sites-developing/page-templates-editable.md) 以了解详细信息。

>[!NOTE]
>
>请参阅 [使用可编辑页面模板开发Experience Manager站点](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### 静态模板 {#static-templates}

静态模板:

* 必须由开发人员定义和配置。
* AEM的原始模板系统已经有许多版本可用。
* 静态模板是指与要创建页面具有相同结构，但没有任何实际内容的节点的层次结构。
* 创建页面时复制了此变量，此后不存在动态连接。
* 用途 [设计模式](/help/sites-authoring/default-components-designmode.md) 以保留设计属性。
* 存储在 `/apps`
* 请参阅 [静态模板](/help/sites-developing/page-templates-static.md) 以了解详细信息。

>[!NOTE]
>
>从AEM 6.5开始，使用静态模板不被视为最佳实践。 请改用可编辑的模板。
>
>[AEM现代化](modernization-tools.md) 工具可以帮助您从静态模板迁移到可编辑模板。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供了多个属性来控制下允许的模板 **站点**. 但是，将它们组合在一起可能会导致难以跟踪和管理的复杂规则。
>
>因此，Adobe建议您从定义以下内容开始：
>
>* 仅 `cq:allowedTemplates` 属性
>
>* 仅在站点根目录上
>
>有关示例，请参阅We.Retail： `/content/we-retail/jcr:content`
>
>属性 `allowedPaths`， `allowedParents`、和 `allowedChildren` 还可以放置在模板上以定义更复杂的规则。 但是，如果可能，它是 *很多* 更简单以进一步定义 `cq:allowedTemplates` 属性。
>
>另一个优势是 `cq:allowedTemplates` 作者可以在以下位置更新属性 **高级** 选项卡 **页面属性**. 无法使用（标准）UI更新其他模板属性，因此需要开发人员维护规则和每次更改的代码部署。

在站点管理界面中创建页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的版面限制。

以下属性确定模板是否 `T` 用于作为页面的子项放置的新页面 `P`. 以下每个属性都是一个多值字符串，其中包含零个或多个用于与路径匹配的正则表达式：

* 此 `cq:allowedTemplates` 的属性 `jcr:content` 子节点 `P` 或祖先 `P`.

* 此 `allowedPaths` 属性 `T`.

* 此 `allowedParents` 属性 `T`.

* 此 `allowedChildren` 模板的属性 `P`.

评估工作如下：

* 第一个非空 `cq:allowedTemplates` 在页面层次结构中以开始升序时发现属性 `P` 的路径匹配 `T`. 如果没有任何值匹配， `T` 被拒绝。

* 如果 `T` 具有非空 `allowedPaths` 属性，但没有值匹配路径 `P`， `T` 被拒绝。

* 如果以上属性为空或不存在， `T` 被拒绝，除非它属于与相同的应用程序 `P`. `T` 属于与相同的应用程序 `P` 当且仅当第二级路径的名称 `T` 与的路径的第二级名称相同 `P`. 例如，模板 `/apps/geometrixx/templates/foo` 属于与页面相同的应用程序 `/content/geometrixx`.

* 如果 `T` 具有非空 `allowedParents` 属性，但没有值匹配路径 `P`， `T` 被拒绝。

* 如果模板 `P` 具有非空 `allowedChildren` 属性，但没有值匹配路径 `T`， `T` 被拒绝。

* 在所有其他情况下， `T` 允许。

下图描述了模板评估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子页面中使用的模板 {#limiting-templates-used-in-child-pages}

要限制哪些模板可用于在给定页面下创建子页面，请使用 `cq:allowedTemplates` 属性 `jcr:content` 页面的节点，用于指定允许作为子页面的模板列表。 列表中的每个值都必须是允许的子页面模板的绝对路径，例如， `/apps/geometrixx/templates/contentpage`.

您可以使用 `cq:allowedTemplates` 模板的属性  `jcr:content` 节点，用于将此配置应用于使用此模板的所有新创建的页面。

例如，如果要添加更多关于模板层次结构的约束，可以使用 `allowedParents/allowedChildren` 属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父项/子项。

## 模板 — 内容片段 {#templates-content-fragments}

请参阅 [内容片段模板](/help/sites-developing/content-fragment-templates.md).
