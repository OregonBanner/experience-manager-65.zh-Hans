---
title: 自定义和扩展内容片段
seo-title: Customizing and Extending Content Fragments
description: 内容片段扩展了标准资产。 了解如何对其进行自定义。
seo-description: A content fragment extends a standard asset. Learn how you can customize them.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2793'
ht-degree: 2%

---


# 自定义和扩展内容片段{#customizing-and-extending-content-fragments}

内容片段扩展了标准资产；请参阅：

* [创建和管理内容片段](/help/assets/content-fragments/content-fragments.md) 和 [使用内容片段进行页面创作](/help/sites-authoring/content-fragments.md) 以了解有关内容片段的更多信息。

* [管理资源](/help/assets/manage-assets.md) 和 [自定义和扩展资产](/help/assets/extending-assets.md) 以了解有关标准资产的更多信息。

## 架构 {#architecture}

基本 [组成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 的内容片段包括：

* A *内容片段，*
* 由一个或多个组成 *内容元素* s，
* 可以有一个或多个 *内容变量* s.

根据片段类型，还会使用模型或模板：

>[!CAUTION]
>
>[内容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建议用于创建所有新片段。
>
>内容片段模型用于WKND中的所有示例。

>[!NOTE]
>
>在AEM 6.3之前，内容片段是基于模板而不是模型创建的。
>
>现已弃用内容片段模板。 它们仍可用于创建片段，但建议改用内容片段模型。 不会向片段模板中添加任何新功能，并且会在未来版本中删除这些功能。

* 内容片段模型:

   * 用于定义包含结构化内容的内容片段。
   * 内容片段模型在创建内容片段时定义其结构。
   * 片段引用模型；因此，对模型的更改可能/将影响任何依赖的片段。
   * 模型由数据类型构建。
   * 用于添加新变体的函数等，必须相应地更新片段。

  >[!CAUTION]
  >
  >对现有内容片段模型所做的任何更改都会影响从属片段；这可能会导致这些片段中的属性孤立。

* 内容片段模板：

   * 用于定义简单内容片段。
   * 模板在创建内容片段时定义内容片段的（基本、纯文本）结构。
   * 模板在创建时复制到片段；因此对模板的进一步更改将不会反映在现有片段中。
   * 用于添加新变体的函数等，必须相应地更新片段。
   * [内容片段模板](/help/sites-developing/content-fragment-templates.md) 其操作方式与AEM生态系统内的其他模板机制（例如，页面模板等）不同。 因此，应单独审议这些问题。
   * 当基于模板时，内容的MIME类型根据实际内容进行管理；这意味着每个元素和变体可以具有不同的MIME类型。

### 与Assets集成 {#integration-with-assets}

内容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 内容片段是资产。
* 它们使用现有的资产功能。
* 它们与Assets（Admin Console等）完全集成。

#### 将结构化内容片段映射到资产 {#mapping-structured-content-fragments-to-assets}

![片段到资产结构化](assets/fragment-to-assets-structured.png)

包含结构化内容（即基于内容片段模型）的内容片段映射到单个资产：

* 所有内容都存储在 `jcr:content/data` 资源的节点：

   * 元素数据存储在主子节点下：
     `jcr:content/data/master`

   * 变体存储在子节点下，该子节点带有变体的名称：例如， `jcr:content/data/myvariation`

   * 每个元素的数据作为具有元素名称的属性存储在相应的子节点中：例如，元素的内容 `text` 存储为属性 `text` 日期 `jcr:content/data/master`

* 元数据和关联内容存储在下方 `jcr:content/metadata`
除了标题和描述，它们不被视为传统元数据并存储在上 `jcr:content`

#### 将简单内容片段映射到资产 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

简单内容片段（基于模板）将映射到由主资产和（可选）子资产组成的组合：

* 片段的所有非内容信息（例如标题、描述、元数据、结构）在主资产上专门进行管理。
* 片段第一个元素的内容映射到主资源的原始演绎版。

   * 第一个元素的变体（如果有）映射到主资源的其他演绎版。

* 其他元素（如果存在）将映射到主资产的子资产。

   * 这些附加元素的主要内容映射到相应子资产的原始演绎版。
   * 任何其他元素的其他变体（如果适用）映射到相应子资产的其他演绎版。

#### 资产位置 {#asset-location}

与标准资产一样，内容片段位于下：

`/content/dam`

#### 资源权限 {#asset-permissions}

有关更多详细信息，请参阅 [内容片段 — 删除注意事项](/help/assets/content-fragments/content-fragments-delete.md).

#### 功能集成 {#feature-integration}

* 内容片段管理(CFM)功能以Assets核心为基础，但应尽可能独立于此核心。
* CFM为卡片/列/列表视图中的项目提供自己的实施；这些实施可以插入现有Assets内容呈现实施。
* 扩展了多个Assets组件以满足内容片段的需求。

### 在页面中使用内容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) 现在推荐。 请参阅 [开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html) 以了解更多详细信息。

可以从AEM页面引用内容片段，就像任何其他资源类型一样。 AEM提供 [**内容片段** 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) - a [允许您在页面上包含内容片段的组件](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). 您还可以扩展 **内容片段** 核心组件。

* 组件使用 `fragmentPath` 属性以引用实际内容片段。 此 `fragmentPath` 资产的处理方式与其他资产类型的类似资产相同；例如，当内容片段移动到其他位置时。

* 利用组件，可选择要显示的变体。
* 此外，可以选择一定范围的段落以限制输出；例如，这可用于多列输出。
* 组件允许 [中间内容](/help/sites-developing/components-content-fragments.md#in-between-content)：

   * 在这里，利用组件可以在引用片段的段落之间放置其他资产（图像等）。
   * 对于中间内容，您需要：

      * 请注意，可能存在不稳定的引用；中间内容（在创作页面时添加）与其旁边的段落没有固定关系，在中间内容的位置可能丢失相对位置之前插入新段落（在内容片段编辑器中）
      * 请考虑使用其他参数（如变体和段落过滤器）以避免搜索结果中出现误报

>[!NOTE]
>
>**内容片段模型:**
>
>使用基于页面上的内容片段模型的内容片段时，会引用模型。 这意味着，如果在您发布页面时模型尚未发布，则会标记该模型，并将模型添加到要与页面一起发布的资源。
>
>**内容片段模板：**
>
>使用基于页面上的内容片段模板的内容片段时，没有引用，因为创建片段时复制了模板。

#### 使用OSGi控制台进行配置 {#configuration-using-osgi-console}

例如，内容片段的后端实施负责使页面上使用的片段实例可搜索，或管理混合媒体内容。 此实施需要知道哪些组件用于呈现片段以及如何对呈现进行参数化。

此操作的参数可在 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，用于OSGi捆绑包 **内容片段组件配置**.

* **资源类型**
列表 `sling:resourceTypes` 可用于定义用于呈现内容片段的组件以及应应用后台处理的位置。

* **引用属性**
可以配置属性列表以指定在何处为各个组件存储对片段的引用。

>[!NOTE]
>
>属性和组件类型之间没有直接映射。
>
>AEM只采用可在段落上找到的第一个属性。 因此，您应该仔细选择属性。

![screenshot_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您还必须遵循以下一些准则，以确保组件与内容片段后台处理兼容：

* 定义要呈现的元素的属性的名称必须是 `element` 或 `elementNames`.

* 定义要呈现的变量的属性的名称满足以下任一条件 `variation` 或 `variationName`.

* 如果支持多个元素的输出(通过使用 `elementNames` 要指定多个元素)，实际显示模式由属性定义 `displayMode`：

   * 如果值为 `singleText` （并且只配置了一个元素），则该元素将呈现为具有中间内容、布局支持等的文本。 这是仅呈现一个元素的片段的默认设置。
   * 否则，将使用一种更简单的方法（可以称为“表单视图”），这种方法不支持中间内容，并且片段内容按“原样”渲染。

* 如果片段呈现为 `displayMode` == `singleText` （隐式或显式）以下附加属性发挥作用：

   * `paragraphScope` 定义是应呈现所有段落，还是只呈现某个范围的段落(值： `all` 对比 `range`)

   * 如果 `paragraphScope` == `range` 然后属性 `paragraphRange` 定义要呈现的段落范围

### 与其他框架集成 {#integration-with-other-frameworks}

内容片段可以与集成：

* **翻译**

  内容片段与完全集成 [AEM翻译工作流](/help/sites-administering/tc-manage.md). 在架构方面，这意味着：

   * 内容片段的各个翻译实际上是单独的片段；例如：

      * 它们位于不同的语言根下：

        `/content/dam/<path>/en/<to>/<fragment>`

        对比

        `/content/dam/<path>/de/<to>/<fragment>`

      * 但它们共享语言根目录下的完全相同的相对路径：

        `/content/dam/<path>/en/<to>/<fragment>`

        对比

        `/content/dam/<path>/de/<to>/<fragment>`

   * 除了基于规则的路径之外，内容片段的不同语言版本之间没有进一步的连接；它们作为两个单独的片段处理，尽管UI提供了在语言变体之间导航的方法。

  >[!NOTE]
  >
  >AEM翻译工作流可与配合使用 `/content`：
  >
  >* 由于内容片段模型驻留在 `/conf`，这些不会包含在此类翻译中。 您可以 [国际化UI字符串](/help/sites-developing/i18n-dev.md).
  >
  >* 将复制模板以创建片段，因此这是隐式的。

* **元数据架构**

   * 内容片段（重新）使用 [元数据架构](/help/assets/metadata-schemas.md)，这些资源可使用标准资源定义。
   * CFM提供了自己的特定架构：

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     如果需要，可以扩展此功能。

   * 相应的架构表单与片段编辑器集成。

## 内容片段管理API — 服务器端 {#the-content-fragment-management-api-server-side}

您可以使用服务器端API访问内容片段；请参阅：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>强烈建议使用服务器端API，而不是直接访问内容结构。

### 关键界面 {#key-interfaces}

以下三个接口可用作入口点：

* **片段模板** ([片段模板](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  使用 `FragmentTemplate.createFragment()` 用于创建片段。

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  此界面表示：

   * 从中创建内容片段的内容片段模型或内容片段模板，
   * 以及（创建后）该片段的结构信息

  此信息可以包括：

   * 访问基本数据（标题、描述）
   * 访问片段元素的模板/模型：

      * 列表元素模板
      * 获取给定元素的结构信息
      * 访问元素模板(请参阅 `ElementTemplate`)

   * 访问片段变体的模板：

      * 列出变体模板
      * 获取给定变体的结构信息
      * 访问变体模板(请参阅 `VariationTemplate`)

   * 获取初始关联内容

  表示重要信息的接口：

   * `ElementTemplate`

      * 获取基本数据（名称、标题）
      * 获取初始元素内容

   * `VariationTemplate`

      * 获取基本数据（名称、标题、描述）

* **内容片段** ([内容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  利用此界面，您可以以抽象方式处理内容片段。

  >[!CAUTION]
  >
  >强烈建议通过此界面访问片段。 应避免直接更改内容结构。

  该界面为您提供了以下方法：

   * 管理基本数据（例如，获取名称；获取/设置标题/描述）
   * 访问元数据
   * 访问元素：

      * 列出元素
      * 按名称获取元素
      * 创建新元素(请参阅 [注意事项](#caveats))

      * 访问元素数据(请参阅 `ContentElement`)

   * 为片段定义的列表变量
   * 全局创建新变体
   * 管理关联内容：

      * 列出收藏集
      * 添加收藏集
      * 删除收藏集

   * 访问片段的模型或模板

  表示片段的主元素的接口包括：

   * **内容元素** ([内容元素](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 访问元素的变体：

         * 列表变量
         * 按名称获取变体
         * 创建新变体(请参阅 [注意事项](#caveats))
         * 删除变体(请参阅 [注意事项](#caveats))
         * 访问变体数据(请参阅 `ContentVariation`)

      * 解决变体的快捷方式（如果指定的变体不适用于元素，则应用一些其他特定于实施的回退逻辑）

   * **内容变量** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 获取基本数据（名称、标题、描述）
      * 获取/设置内容
      * 简单同步，基于上次修改的信息

  所有三个接口( `ContentFragment`， `ContentElement`， `ContentVariation`)扩展 `Versionable` 界面，添加了内容片段所需的版本控制功能：

   * 创建新版本的元素
   * 列出元素的版本
   * 获取版本化元素的特定版本的内容

### 适应 — 使用adaptTo() {#adapting-using-adaptto}

可以调整以下内容：

* `ContentFragment` 可以适应：

   * `Resource`  — 基础Sling资源；请注意，更新基础 `Resource` 直接，需要重建 `ContentFragment` 对象。

   * `Asset` - DAM `Asset` 表示内容片段的抽象；请注意，更新 `Asset` 直接，需要重建 `ContentFragment` 对象。

* `ContentElement` 可以适应：

   * `ElementTemplate`  — 用于访问元素的结构信息。

* `FragmentTemplate` 可以适应：

   * `Resource` - `Resource` 确定所复制的参考模型或原始模板；

      * 通过进行的更改 `Resource` 不会自动反映在 `FragmentTemplate`.

* `Resource` 可以适应：

   * `ContentFragment`
   * `FragmentTemplate`

### 注意事项 {#caveats}

应当指出：

* 实施API是为了提供UI支持的功能。
* 整个API旨在 **非** 自动保留更改（除非在API JavaDoc中另有说明）。 因此，您将始终必须提交相应请求的资源解析程序（或您实际使用的解析程序）。
* 可能需要额外工作的任务：

   * 创建/删除新元素将不会更新简单片段的数据结构（基于片段模板）。
   * 从创建新变体 `ContentElement` 不会更新数据结构（但会从全局创建数据结构） `ContentFragment` 会)。

   * 删除现有变体将不会更新数据结构。

## 内容片段管理API — 客户端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>对于AEM 6.5，客户端API是内部的。

### 附加信息 {#additional-information}

请参阅以下内容：

* `filter.xml`

  此 `filter.xml` 对于内容片段管理，已配置为不与资产核心内容包重叠。

## 编辑会话 {#edit-sessions}

当用户在一个编辑器页面中打开内容片段时，会启动编辑会话。 当用户通过选择任一选项离开编辑器时，编辑会话即完成 **保存** 或 **取消**.

### 要求 {#requirements}

控制编辑会话的要求包括：

* 编辑的内容片段可以跨越多个视图(=HTML页面)，应为原子结构。
* 编辑也应 *事务性*；在编辑会话结束时，必须提交（保存）更改或回滚（取消）更改。
* 边缘案例应正确处理；这些案例包括用户通过手动输入URL或使用全局导航离开页面等情况。
* 应提供定期自动保存（每x分钟）以防止数据丢失。
* 如果两个用户同时编辑内容片段，则他们不应覆盖彼此的更改。

#### 进程 {#processes}

涉及的过程包括：

* 启动会话

   * 将创建内容片段的新版本。
   * 自动保存已启动。
   * 设置了Cookie；这些Cookie定义了当前编辑的片段，并打开了编辑会话。

* 完成会话

   * 自动保存已停止。
   * 提交时：

      * 上次修改的信息已更新。
      * Cookie将被删除。

   * 回滚时：

      * 恢复在编辑会话启动时创建的内容片段的版本。
      * Cookie将被删除。

* 编辑

   * 所有更改（包括自动保存）都是在活动内容片段上完成的，而不是在分隔的保护区中。
   * 因此，这些更改会立即反映在引用相应内容片段的AEM页面上

#### 操作 {#actions}

可能的操作包括：

* 输入页面

   * 检查编辑会话是否已存在；通过检查相应的Cookie。

      * 如果存在，请验证是否已为当前正在编辑的内容片段启动编辑会话

         * 如果是当前片段，请重新建立会话。
         * 如果没有，请尝试取消对以前编辑的内容片段的编辑并删除Cookie（之后不存在编辑会话）。

      * 如果不存在编辑会话，请等待用户进行第一次更改（请参阅下文）。

   * 检查页面上是否已引用内容片段，如果是，则显示相应的信息。

* 内容更改

   * 每当用户更改内容并且不存在编辑会话时，都会创建一个新的编辑会话(请参阅 [启动会话](#processes))。

* 离开页面

   * 如果存在编辑会话并且更改未保留，则会显示模式确认对话框，以通知用户内容可能丢失，并允许他们停留在页面上。

## 示例 {#examples}

### 示例：访问现有内容片段 {#example-accessing-an-existing-content-fragment}

要实现此目的，您可以使表示API的资源适应：

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

### 示例：创建内容片段 {#example-creating-a-new-content-fragment}

要以编程方式创建内容片段，您需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例：指定自动保存时间间隔 {#example-specifying-the-auto-save-interval}

可以使用配置管理器(ConfMgr)定义自动保存时间间隔（以秒为单位）：

* 节点： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`
* 类型：`Long`

* 默认： `600` （10分钟）；此时间定义于 `/libs/settings/dam/cfm/jcr:content`

如果要将自动保存间隔设置为5分钟，则需要在节点上定义属性；例如：

* 节点： `/conf/global/settings/dam/cfm/jcr:content`
* 属性名称: `autoSaveInterval`

* 类型：`Long`

* 值： `300` （5分钟等于300秒）

## 内容片段模板 {#content-fragment-templates}

请参阅 [内容片段模板](/help/sites-developing/content-fragment-templates.md) 获取完整信息。

## 用于页面创作的组件 {#components-for-page-authoring}

有关详细信息，请参阅

* [核心组件 — 内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans) （推荐）
* [内容片段组件 — 用于页面创作的组件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
