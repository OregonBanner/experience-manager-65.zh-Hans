---
title: 模板
seo-title: 模板
description: 创建将用作新页面基础的页面时，会使用模板
seo-description: 创建将用作新页面基础的页面时，会使用模板
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---

# 模板{#templates}

模板在AEM的不同位置使用：

* 在[创建页面时，您需要选择模板](#templates-pages);这将用作新页面的基础。 模板可定义生成页面的结构、任何初始内容以及可使用的[组件](/help/sites-authoring/default-components.md)（设计属性）。

* 在[创建内容片段时，您还需要选择模板](#templates-content-fragments)。 此模板可定义结构、初始元素和变量。

详细介绍了以下模板：

* [页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)
* [页面模板 — 静态](/help/sites-developing/page-templates-static.md)
* [内容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自适应模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板 — 页面{#templates-pages}

AEM现在提供两种用于创建页面的基本模板类型：

>[!NOTE]
>
>使用模板创建新页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)时，没有明显差异（对页面作者），也没有显示正在使用的模板类型。[

### 可编辑的模板 {#editable-templates}

可编辑的模板现在被视为使用AEM进行开发的最佳实践。

可编辑模板的优势：

* 可以是作者创建的[](/help/sites-authoring/templates.md#creating-a-new-template-template-author)和[编辑的](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

* 引入此模板后，您可以为使用该模板创建的任何页面定义以下内容：

   * 结构
   * 初始内容
   * 内容策略

* 创建新页面后，页面与模板之间会保持动态连接；这意味着对模板结构所做的更改将反映在使用该模板创建的任何页面上（不会反映对初始内容所做的更改）。
* 使用内容策略（从模板编辑器中编辑）来保留设计属性（在页面编辑器中不使用设计模式）。
* 存储在`/conf`下
* 有关更多信息，请参阅[可编辑的模板](/help/sites-developing/page-templates-editable.md)。

>[!NOTE]
>
>有关AEM社区文章，请参阅如何使用可编辑模板开发Experience Manager网站，请参阅[使用可编辑模板创建Adobe Experience Manager 6.5网站](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)。

### 静态模板 {#static-templates}

静态模板:

* 必须由您的开发人员定义和配置。
* 这是AEM的原始模板系统，已推出多个版本。
* 静态模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。
* 复制以创建新页面，此后不存在动态连接。
* 使用[设计模式](/help/sites-authoring/default-components-designmode.md)保留设计属性。
* 存储在`/apps`下
* 有关更多信息，请参阅[静态模板](/help/sites-developing/page-templates-static.md)。

>[!NOTE]
>
>自AEM 6.5起，使用静态模板不被视为最佳实践。 请改用可编辑的模板。
>
>[AEM ](modernization-tools.md) Modernizationtools可以帮助您从静态模板迁移到可编辑的模板。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供了多个属性来控制&#x200B;**Sites**&#x200B;下允许的模板。 但是，将它们组合在一起可能会导致非常复杂的规则，从而难以跟踪和管理。
>
>因此，Adobe建议您首先通过定义以下内容来简单操作：
>
>* 仅`cq:allowedTemplates`属性
   >
   >
* 仅在站点根目录上
>
>
有关示例，请参阅We.Retail:`/content/we-retail/jcr:content`
>
>属性`allowedPaths`、`allowedParents`和`allowedChildren`也可以放在模板上，以定义更复杂的规则。 但是，如果可能，如果需要进一步限制允许的模板，则在站点的子区域上进一步定义`cq:allowedTemplates`属性会更简单。**
>
>另一个好处是，作者可以在&#x200B;**页面属性**&#x200B;的&#x200B;**Advanced**&#x200B;选项卡中更新`cq:allowedTemplates`属性。 无法使用（标准）UI更新其他模板属性，因此需要开发人员为每次更改维护规则和代码部署。

在站点管理界面中创建新页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的放置限制。

以下属性确定是否允许将模板`T`用于要作为页面`P`的子项放置的新页面。 以下每个属性都是一个包含零个或多个正则表达式的多值字符串，用于与路径匹配：

* `P`的`jcr:content`子节点或`P`的上级的`cq:allowedTemplates`属性。

* `T`的`allowedPaths`属性。

* `T`的`allowedParents`属性。

* `P`模板的`allowedChildren`属性。

评价工作如下：

* 在对以`P`开头的页面层次结构进行升序时找到的第一个非空`cq:allowedTemplates`属性与`T`的路径相匹配。 如果没有值匹配，则拒绝`T`。

* 如果`T`具有非空的`allowedPaths`属性，但没有任何值与`P`的路径匹配，则`T`将被拒绝。

* 如果上述两个属性为空或不存在，则拒绝`T`，除非它属于与`P`相同的应用程序。 `T` 属于与if相同的应 `P` 用程序，并且仅当路径的第二级名称与 `T` 路径的第二级名称相同时 `P`。例如，模板`/apps/geometrixx/templates/foo`属于与页面`/content/geometrixx`相同的应用程序。

* 如果`T`具有非空的`allowedParents`属性，但没有任何值与`P`的路径匹配，则`T`将被拒绝。

* 如果`P`的模板具有非空的`allowedChildren`属性，但没有任何值与`T`的路径匹配，则`T`将被拒绝。

* 在所有其他情况下，允许使用`T`。

下图描述了模板评估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子页面{#limiting-templates-used-in-child-pages}中使用的限制模板

要限制可用于在给定页面下创建子页面的模板，请使用页面`jcr:content`节点的`cq:allowedTemplates`属性指定允许作为子页面的模板列表。 列表中的每个值都必须是允许的子页面（例如`/apps/geometrixx/templates/contentpage`）的模板的绝对路径。

可以使用模板`jcr:content`节点上的`cq:allowedTemplates`属性将此配置应用于使用此模板的所有新创建页面。

如果要添加更多约束（例如与模板层次结构有关的约束），可以使用模板上的`allowedParents/allowedChildren`属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父/子页面。

## 模板 — 内容片段{#templates-content-fragments}

有关完整信息，请参阅[内容片段模板](/help/sites-developing/content-fragment-templates.md)。
