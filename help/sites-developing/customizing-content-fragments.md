---
title: 自定义和扩展内容片段
seo-title: 自定义和扩展内容片段
description: 内容片段扩展标准资产。
seo-description: 内容片段扩展标准资产。
uuid: f72c3a23-9b0d-4fab-a960-bb1350f01175
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d0770bee-4be5-4a6a-8415-70fdfd75015c
docset: aem65
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '2749'
ht-degree: 1%

---


# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

内容片段扩展了标准资产； 请参阅：

* [有关内容片段的更多信息](/help/assets/content-fragments/content-fragments.md) ，请 [使用内容片段创建和管理内容片段](/help/sites-authoring/content-fragments.md) ，以及使用页面创作。

* [管理资产](/help/assets/managing-assets-touch-ui.md) 、 [自定义和扩展资产](/help/assets/extending-assets.md) ，以了解有关标准资产的更多信息。

## 架构 {#architecture}

内容片 [段的基](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 本组成部分包括：

* 内 *容片段，*
* 包含一个或多个 *内容*&#x200B;元素，
* 和可以具有一个或多个内 *容变*&#x200B;体。

根据片段类型，还会使用模型或模板：

>[!CAUTION]
>
>[现在建议使用](/help/assets/content-fragments/content-fragments-models.md) “内容片段模型”来创建您的所有片段。
>
>内容片段模型用于We.Retail中的所有示例。

* 内容片段模型:

   * 用于定义包含结构化内容的内容片段。
   * 内容片段模型定义内容片段在创建时的结构。
   * 片段引用模型； 因此，对模型所做的更改可能会／会影响任何从属片段。
   * 模型是数据类型的构建。
   * 添加新变量等的函数必须相应更新片段。
   >[!CAUTION]
   >
   >对现有内容片段模型的任何更改都可能影响相关片段； 这会导致这些片段中的孤立属性。

* 内容片段模板：

   * 用于定义简单内容片段。
   * 模板可定义内容片段在创建时的（基本的、纯文本的）结构。
   * 创建模板时，模板将复制到片段； 因此，对模板的进一步更改不会反映在现有片段中。
   * 添加新变量等的函数必须相应更新片段。
   * [内容片段模板](/help/sites-developing/content-fragment-templates.md) 以与AEM生态系统中其他模板机制（如页面模板等）不同的方式操作。 因此，应单独考虑这些问题。
   * 基于模板时，根据实际内容管理内容的MIME类型； 这意味着每个元素和变量都可以具有不同的MIME类型。

### 与资产集成 {#integration-with-assets}

内容片段管理(CFM)是以下AEM Assets的一部分：

* 内容片段是资产。
* 他们使用现有资产功能。
* 它们与资产（管理控制台等）完全集成。

#### 将结构化内容片段映射到资产 {#mapping-structured-content-fragments-to-assets}

![片段到资产结构化](assets/fragment-to-assets-structured.png)

具有结构化内容（即基于内容片段模型）的内容片段将映射到单个资产：

* 所有内容都存储在资 `jcr:content/data` 产的节点下：

   * 元素数据存储在主子节点下：
      `jcr:content/data/master`

   * 变体存储在子节点下，子节点带有变体的名称：
例如， `jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：
例如，元素的内容 `text` 作为属性存储在 `text` `jcr:content/data/master`

* 元数据和关联内容存储在 `jcr:content/metadata`下面，但标题和说明除外，它们不被视为传统元数据，并存储在 `jcr:content`

#### 将简单内容片段映射到资产 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

简单内容片段（基于模板）会映射到由主资产和（可选）子资产组成的组合：

* 片段的所有非内容信息（如标题、描述、元数据、结构）均专门在主资产上进行管理。
* 片段的第一个元素的内容将映射到主资产的原始演绎版。

   * 第一个元素的变量（如果有）会映射到主资产的其他演绎版。

* 其他元素（如果现有）会映射到主资产的子资产。

   * 这些附加元素的主要内容会映射到相应子资产的原始演绎版。
   * 任何其他元素的其他变体（如果适用）会映射到相应子资产的其他演绎版。

#### 资产位置 {#asset-location}

与标准资产一样，内容片段位于以下位置：

`/content/dam`

#### 资产权限 {#asset-permissions}

有关更多详细信息， [请参阅内容片段——删除注意事项](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能集成 {#feature-integration}

* 内容片段管理(CFM)功能构建于资产核心之上，但应尽可能独立于它。
* CFM为卡／列/列表视图中的项目提供其自己的实现； 这些插件可插入现有资产内容呈现实施。
* 已扩展多个资产组件，以满足内容片段的需要。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>现在 [建议使用内容片段](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) 核心组件。 有关更 [多详细信息](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) ，请参阅开发核心组件。

内容片段可以从AEM页面中引用，就像任何其他资产类型一样。 AEM提供内 [**容片段&#x200B;**核心组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)-一个[组件，允许您在页面中包含内容片段](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)。 您还可以扩展此内容片**&#x200B;段核心组&#x200B;**件。

* 组件使用属 `fragmentPath` 性引用实际内容片段。 该 `fragmentPath` 财产的处理方式与其他资产类型的类似财产相同； 例如，当内容片段被移动到其他位置时。

* 组件允许您选择要显示的变量。
* 此外，还可以选择一系列段落来限制输出； 例如，这可用于多列输出。
* 该组件允 [许中间内容](/help/sites-developing/components-content-fragments.md#in-between-content):

   * 在此组件中，您可以放置其他资产（图像等） 在引用片段的段落之间。
   * 对于中间内容，您需要：

      * 注意不稳定的参考资料的可能性； 中间内容（在创作页面时添加）与它位于旁边的段落没有固定关系，在中间内容的位置之前插入新段落（在内容片段编辑器中）可能会丢失相对位置
      * 考虑其他参数(如变化和段落过滤器)以避免搜索结果中出现误报

>[!NOTE]
>
>**内容片段模型:**
>
>当使用基于页面上的内容片段模型的内容片段时，将引用该模型。 这意味着，如果发布页面时尚未发布模型，则会标记该模型并将该模型添加到要随页面一起发布的资源。
>
>**内容片段模板：**
>
>在使用基于页面上的内容片段模板的内容片段时，没有引用，因为创建片段时复制了该模板。

#### 使用OSGi控制台进行配置 {#configuration-using-osgi-console}

例如，内容片段的后端实现负责使页面上使用的片段实例可搜索，或管理混合媒体内容。 此实现需要了解用于渲染片段的组件以及如何对渲染进行参数化。

Web控制台中可以为OSGi捆绑内 [容片段组](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)件配置配 **置配置此参数**。

* **资源类**&#x200B;型可以提 `sling:resourceTypes` 供列表来定义用于渲染内容片段的组件，以及应将后台处理应用到的组件。

* **引用属**&#x200B;性可以配置属性列表，以指定对片段的引用存储到相应组件的位置。

>[!NOTE]
>
>属性和组件类型之间没有直接映射。
>
>AEM只需获取可在段落上找到的第一个属性。 因此，您应当谨慎选择属性。

![screestop_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您仍必须遵循一些准则，以确保您的组件与内容片段后台处理兼容：

* 定义要呈现的元素的属性名称必须是或 `element` 者 `elementNames`。

* 定义要呈现的变体的属性名称必须是或 `variation` 者 `variationName`。

* 如果支持多个元素的输出(通过使用指 `elementNames` 定多个元素)，则实际显示模式由属性定义 `displayMode`:

   * 如果该值是 `singleText` （并且只配置了一个元素），则元素将呈现为具有中间内容、布局支持等的文本。 这是仅渲染一个元素的片段的默认值。
   * 否则，将使用一种更简单的方法(可称为“表单视图”)，其中不支持中间内容，并且片段内容将“按原样”呈现。

* 如果片段是为== `displayMode` (隐 `singleText` 式或显式)呈现的，则下列附加属性将起作用：

   * `paragraphScope` 定义是否应渲染所有段落或仅渲染一系列段落(值： `all` 与 `range`)

   * 如 `paragraphScope` 果= `range` ，则属性 `paragraphRange` 定义要渲染的段落范围

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可与以下内容集成：

* **翻译**

   内容片段与AEM翻译工作 [流完全集成](/help/sites-administering/tc-manage.md)。 在建筑层面，这意味着：

   * 内容片段的个别翻译实际上是单独的片段； 例如：

      * 它们位于不同的语言根下：

         `/content/dam/<path>/en/<to>/<fragment>`

         与

         `/content/dam/<path>/de/<to>/<fragment>`

      * 但是，它们在语言根下完全共享相对路径：

         `/content/dam/<path>/en/<to>/<fragment>`

         与

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有进一步的联系； 它们作为两个单独的片段处理，但UI提供了在语言变体之间导航的方法。
   >[!NOTE]
   >
   >AEM翻译工作流程可用于 `/content`:
   >
   >    * 由于内容片段模型位于 `/conf`其中，因此此类转换中不包含这些模型。 您可以 [将UI字符串国际化](/help/sites-developing/i18n-dev.md)。
      >
      >    
   * 模板将被复制以创建片段，因此这是隐式的。


* **元数据架构**

   * 内容片段（重新）使用元 [数据模式](/help/assets/metadata-schemas.md)，这些可以使用标准资产进行定义。
   * CFM提供其自己的特定模式:

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如果需要，可以扩展此功能。

   * 相应的模式表单与片段编辑器集成。

## 内容片段管理API —— 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问您的内容片段； 请参阅：

[com.adobe.cq.dam.cfm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>强烈建议使用服务器端API，而不是直接访问内容结构。

### 关键接口 {#key-interfaces}

以下三个接口可用作入口点：

* **片段模板** ([FragmentTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   用 `FragmentTemplate.createFragment()` 于创建新片段。

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   此接口表示：

   * 内容片段模型或内容片段模板，从中创建内容片段，
   * 和（创建后）该片段的结构信息
   此信息可包括：

   * 访问基本数据（标题、说明）
   * 访问片段元素的模板／模型：

      * 列表元素模板
      * 获取给定元素的结构信息
      * 访问元素模板(请参阅 `ElementTemplate`)
   * 访问片段变量的模板：

      * 列表变化模板
      * 获取给定变体的结构信息
      * 访问变体模板(请参阅 `VariationTemplate`)
   * 获取初始关联内容
   表示重要信息的接口：

   * `ElementTemplate`

      * 获取基本数据（名称、标题）
      * 获取初始元素内容
   * `VariationTemplate`

      * 获取基本数据（名称、标题、说明）






* **内容片段** ([ContentFragment](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此界面允许您以抽象方式处理内容片段。

   >[!CAUTION]
   >
   >强烈建议通过此接口访问片段。 应避免直接更改内容结构。

   该界面为您提供了以下方法：

   * 管理基本数据(例如，获取名称； get/set title/description)
   * 访问元数据
   * 访问元素：

      * 列表元素
      * 按名称获取元素
      * 创建新元素(请参阅 [警告](#caveats))

      * 访问元素数据(请参 `ContentElement`阅)
   * 为片段定义的列表变量
   * 全局创建新变量
   * 管理关联内容：

      * 列表集合
      * 添加集合
      * 删除集合
   * 访问片段的模型或模板
   表示片段主元素的接口包括：

   * **内容元素** ([ContentElement](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、说明）
      * 获取／设置内容
      * 访问元素的变体：

         * 列表变化
         * 按名称获取变体
         * 创建新变体(请参阅 [警告](#caveats))
         * 删除变体(请参 [阅警告](#caveats))
         * 访问变量数据(请参 `ContentVariation`阅)
      * 用于解析变量的快捷方式（如果指定的变量对元素不可用，则应用一些附加的特定于实施的回退逻辑）
   * **内容变化** ([ContentVariation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、说明）
      * 获取／设置内容
      * 简单同步，基于上次修改的信息
   所有三个界面( `ContentFragment`、 `ContentElement`、 `ContentVariation`)都扩展了界面，它添加了内容片段 `Versionable` 所需的版本控制功能：

   * 创建元素的新版本
   * 列表元素的版本
   * 获取版本化元素的特定版本的内容







### 改编——使用adaptTo() {#adapting-using-adaptto}

可以调整以下内容：

* `ContentFragment` 可适用于：

   * `Resource` -基础Sling资源； 请注意，直接更新 `Resource` 基础需要重建对 `ContentFragment` 象。

   * `Asset` -表示内 `Asset` 容片段的DAM抽象； 请注意，直接 `Asset` 更新需要重新构建对 `ContentFragment` 象。

* `ContentElement` 可适用于：

   * `ElementTemplate` -用于访问元素的结构信息。

* `FragmentTemplate` 可适用于：

   * `Resource` -确 `Resource` 定所复制的参照模型或原始模板；

      * 通过所做的更改 `Resource` 不会自动反映在 `FragmentTemplate`中。

* `Resource` 可适用于：

   * `ContentFragment`
   * `FragmentTemplate`

### 警告 {#caveats}

应当指出：

* 实现API以提供UI支持的功能。
* 整个API设计为不自 **动保留** 更改（除非在API JavaDoc中另有说明）。 因此，您始终必须提交相应请求的资源解析程序（或您实际使用的解析程序）。
* 可能需要付出额外努力的任务:

   * 创建／删除新元素不会更新简单片段（基于片段模板）的数据结构。
   * 从中创建新变 `ContentElement` 量不会更新数据结构(而是从将来全局 `ContentFragment` 创建)。

   * 删除现有变量不会更新数据结构。

## 内容片段管理API —— 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>对于AEM 6.5，客户端API是内部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

   内 `filter.xml` 容片段管理的配置使其不与资产核心内容包重叠。

## 编辑会话 {#edit-sessions}

当用户在一个编辑器页面中打开内容片段时，将启动编辑会话。 当用户通过选择“保存”或“取消”离开编辑器时，编 **辑会** 话即 **结束**。

### 要求 {#requirements}

控制编辑会话的要求有：

* 编辑可以跨多个视图（= HTML页）的内容片段应该是原子的。
* 编辑也应是事 *务性*; 在编辑会话结束时，必须提交（保存）或回滚（取消）更改。
* 边缘案件应妥善处理； 这些情况包括用户通过手动输入URL或使用全局导航离开页面的情况。
* 应定期自动保存（每x分钟），以防止数据丢失。
* 如果内容片段由两个用户同时编辑，则不应覆盖彼此的更改。

#### 进程 {#processes}

涉及的流程包括：

* 启动会话

   * 将创建内容片段的新版本。
   * 自动保存已启动。
   * Cookie已设置； 这些定义了当前编辑的片段，并且有一个编辑会话处于打开状态。

* 完成会话

   * 自动保存已停止。
   * 提交时：

      * 更新上次修改的信息。
      * Cookies被删除。
   * 回滚时：

      * 恢复在启动编辑会话时创建的内容片段的版本。
      * Cookies被删除。


* 编辑

   * 所有更改（包括自动保存）均在活动内容片段上完成——而不是在单独的受保护区域中。
   * 因此，这些更改会立即反映在引用相应内容片段的AEM页面上

#### 操作 {#actions}

可能的操作包括：

* 输入页面

   * 检查编辑会话是否已存在； 检查相应的cookie。

      * 如果存在，请验证当前正在编辑的内容片段的编辑会话是否已启动

         * 如果当前片段，则重新建立会话。
         * 否则，尝试取消对先前编辑的内容片段的编辑并删除cookie（之后不存在编辑会话）。
      * 如果不存在编辑会话，请等待用户所做的第一次更改（请参阅下文）。
   * 检查页面上是否已引用内容片段，如果引用，则显示相应的信息。



* 内容更改

   * 只要用户更改内容且不存在编辑会话，就会创建新的编辑会话(请参 [阅启动会话](#processes))。

* 离开页面

   * 如果存在编辑会话且更改尚未保留，则会显示一个模态确认对话框，通知用户可能丢失的内容并允许他们保留在页面上。

## 示例 {#examples}

### 示例： 访问现有内容片段 {#example-accessing-an-existing-content-fragment}

要实现此目标，您可以调整表示API的资源以：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 示例： 创建新内容片段 {#example-creating-a-new-content-fragment}

要以编程方式创建新内容片段，您需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例： 指定自动保存间隔 {#example-specifying-the-auto-save-interval}

可以使用配置管理器(ConfMgr)定义自动保存间隔（以秒为单位）:

* 节点： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型: `Long`

* 默认： `600` （10分钟）; 定义于 `/libs/settings/dam/cfm/jcr:content`

如果要设置5分钟的自动保存间隔，您需要定义节点上的属性； 例如：

* 节点： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型: `Long`

* 值： `300` （5分钟等于300秒）

## 内容片段模板 {#content-fragment-templates}

有关 [完整信息，请参](/help/sites-developing/content-fragment-templates.md) 阅内容片段模板。

## 用于创作页面的组件 {#components-for-page-authoring}

有关更多信息，请参阅

* [核心组件——内容片段组件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html) （推荐）
* [内容片段组件——用于页面创作的组件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
