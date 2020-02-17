---
title: 模板
seo-title: 模板
description: 在创建将用作新页面基础的页面时，会使用模板
seo-description: 在创建将用作新页面基础的页面时，会使用模板
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 模板{#templates}

模板在AEM中的不同点使用：

* When [creating a page you need to select a template](#templates-pages); this will be used as the base for the new page. The template defines the structure of the resultant page, any initial content and the [components](/help/sites-authoring/default-components.md) that can be used (design properties).

* 创建 [内容片段时，您还需要选择模板](#templates-content-fragments)。 此模板定义结构、初始元素和变量。

详细介绍了以下模板：

* [页面模板——可编辑](/help/sites-developing/page-templates-editable.md)
* [页面模板——静态](/help/sites-developing/page-templates-static.md)
* [内容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自适应模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板——页面 {#templates-pages}

AEM现在提供两种用于创建页面的基本模板类型：

>[!NOTE]
>
>使用模板创建新 [页面时](/help/sites-authoring/managing-pages.md#creating-a-new-page) ,（对于页面作者）没有明显区别，也没有指示所使用的模板类型。

### 可编辑的模板 {#editable-templates}

现在，可编辑的模板被视为使用AEM进行开发的最佳实践。

可编辑模板的优势：

* 作者可 [以创](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 建和编 [辑](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 。

* 已引入此模板，允许您为使用模板创建的任何页面定义以下内容：

   * 结构
   * 初始内容
   * 内容策略

* 创建新页面后，页面与模板之间会保持动态连接；这意味着对模板结构的更改将反映在使用该模板创建的任何页面上（不会反映对初始内容的更改）。
* 使用内容策略（从模板编辑器中编辑）来保留设计属性（不在页面编辑器中使用设计模式）。
* 存储在 `/conf`
* 有关更 [多信息，请参阅](/help/sites-developing/page-templates-editable.md) “可编辑的模板”。

>[!NOTE]
>
>AEM社区文章将介绍如何使用可编辑模板开发Experience Manager站点，请参阅使 [用可编辑模板创建Adobe Experience Manager 6.5网站](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)。

### 静态模板 {#static-templates}

静态模板:

* 必须由开发人员定义和配置。
* 这是AEM的原始模板系统，已在许多版本中提供。
* 静态模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。
* 复制以创建新页面，之后不存在动态连接。
* Uses [Design Mode](/help/sites-authoring/default-components-designmode.md) to persist design properties.
* 存储在 `/apps`
* 有关更 [多信息，请参阅](/help/sites-developing/page-templates-static.md) “静态模板”。

>[!NOTE]
>
>自AEM 6.5起，使用静态模板不被视为最佳实践。 请改用可编辑的模板。
>
>[AEM Moderization](modernization-tools.md) 工具可以帮助您从静态模板迁移到可编辑模板。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供多个属性以控制站点下允许的 **模板**。 但是，将这些规则组合在一起可能会导致非常复杂的规则难以跟踪和管理。
>
>因此，Adobe建议您通过定义以下内容，从简单开始：
>
>* 只有属 `cq:allowedTemplates` 性
   >
   >
* 仅在站点根目录上
>
>
有关示例，请参阅We.Retail: `/content/we-retail/jcr:content`
>
>属性 `allowedPaths`、 `allowedParents`和 `allowedChildren` 也可放置在模板上以定义更复杂的规则。 但是，如果需要进一 *步限制*`cq:allowedTemplates` ，则在站点的子部分上定义更多属性要简单得多。
>
>另一个优势是，作 `cq:allowedTemplates` 者可以在页面属性的高级选项卡中 **更新****属性**。 其他模板属性无法使用（标准）UI进行更新，因此需要开发人员为每次更改维护规则和代码部署。

在站点管理界面中创建新页面时，可用模板列表取决于新页面的位置以及在每个模板中指定的位置限制。

以下属性确定是否允 `T` 许将模板用于要作为页面子项放置的新页面 `P`。 这些属性中的每个都是一个包含零个或多个正则表达式的多值字符串，这些正则表达式用于与路径匹配：

* 子 `cq:allowedTemplates` 节点或 `jcr:content` 的祖 `P` 代的属性 `P`。

* 属 `allowedPaths` 性 `T`。

* 属 `allowedParents` 性 `T`。

* 模 `allowedChildren` 板的属性 `P`。

评价工作如下：

* 在以开始的页 `cq:allowedTemplates` 面层次结构的升序时找到的第一个非空属 `P` 性将与路径匹配 `T`。 如果所有值均不匹配，则 `T` 拒绝。

* 如果 `T` 有非空属性，但 `allowedPaths` 没有任何值与路径匹配 `P`，则 `T` 将拒绝。

* 如果上述两个属性为空或不存在，则拒绝， `T` 除非它属于与相同的应用程序 `P`。 `T` 属于同一应用程序， `P` 并且仅当路径的第二级名称与路径的第二级名称相同 `T` 时，才属于该应用程序 `P`。 例如，模板属 `/apps/geometrixx/templates/foo` 于与页面相同的应用程序 `/content/geometrixx`。

* 如果 `T` 有非空属性，但 `allowedParents` 没有任何值与路径匹配 `P`，则 `T` 将拒绝。

* 如果模板的 `P` 属性为非空，但 `allowedChildren` 没有任何值与路径匹配 `T`，则 `T` 将拒绝。

* 在所有其他情况下， `T` 都允许。

下图描述了模板评估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子页面中使用的模板 {#limiting-templates-used-in-child-pages}

要限制可用于在给定页面下创建子页面的模板，请使用页面节点的 `cq:allowedTemplates` 属性 `jcr:content` 指定允许作为子页面的模板列表。 例如，列表中的每个值必须是允许的子页面的模板的绝对路径 `/apps/geometrixx/templates/contentpage`。

您可以使用模 `cq:allowedTemplates` 板节点上的属性，将 `jcr:content` 此配置应用到使用此模板的所有新创建的页面。

如果要添加更多约束（例如，关于模板层次结构），则可以使用模 `allowedParents/allowedChildren` 板上的属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父项／子项。

## 模板——内容片段 {#templates-content-fragments}

有关完 [整信息，请参阅内容片段模板](/help/sites-developing/content-fragment-templates.md) 。
