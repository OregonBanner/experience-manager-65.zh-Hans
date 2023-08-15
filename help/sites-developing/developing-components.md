---
title: 开发AEM组件
seo-title: Developing AEM Components
description: AEM组件用于保留、格式化和呈现网页上可用的内容。
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 2%

---

# 开发AEM组件{#developing-aem-components}

AEM组件用于保留、格式化和呈现网页上可用的内容。

* 时间 [创作页面](/help/sites-authoring/default-components.md)中，作者可以使用组件编辑和配置内容。

   * 构建 [商务](/help/commerce/cif-classic/administering/ecommerce.md) 例如，组件可以从目录中收集和呈现信息的站点。
请参阅 [发展电子商务](/help/commerce/cif-classic/developing/ecommerce.md) 以了解更多信息。

   * 构建 [Communities](/help/communities/author-communities.md) 网站组件可以为访客提供信息并从访客那里收集信息。
请参阅 [发展中的社区](/help/communities/communities.md) 以了解更多信息。

* 在发布实例上，组件渲染您的内容，根据需要向网站访客呈现内容。

>[!NOTE]
>
>本页是文档的延续 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>以下组件 `/libs/cq/gui/components/authoring/dialog` 仅可在编辑器（创作中的组件对话框）中使用。 如果在其他位置（例如，在向导对话框中）使用它们，它们可能无法按预期运行。

## 代码示例 {#code-samples}

本页提供了为AEM开发新组件所需的参考文档（或参考文档的链接）。 请参阅 [开发AEM组件 — 代码示例](/help/sites-developing/developing-components-samples.md) 举几个实际例子。

## 结构 {#structure}

页面上介绍了组件的基本结构 [AEM组件 — 基础知识](/help/sites-developing/components-basics.md#structure). 该文档涵盖了触屏界面和经典UI。 即使您不需要在新组件中使用经典设置，也可以在继承现有组件时了解这些设置。

## 扩展现有组件和对话框 {#extending-existing-components-and-dialogs}

根据要实施的组件，可能会扩展或自定义现有实例，而不是定义和开发整个实例 [结构](#structure) 从头开始。

扩展或自定义现有组件或对话框时，您可以在进行更改之前复制或复制整个结构或对话框所需的结构。

### 扩展现有组件 {#extending-an-existing-component}

可通过以下方式扩展现有组件 [资源类型层次结构](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 以及相关的继承机制。

>[!NOTE]
>
>组件还可以通过基于搜索路径逻辑的覆盖来重新定义。 然而，在此情况下， [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 未触发并且 `/apps` 必须定义整个叠加。

>[!NOTE]
>
>此 [内容片段组件](/help/sites-developing/customizing-content-fragments.md) 也可以自定义和扩展，但必须考虑完整结构和与Assets的关系。

### 自定义现有组件对话框 {#customizing-a-existing-component-dialog}

也可以覆盖 *组件对话框* 使用 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 并定义属性 `sling:resourceSuperType`.

这意味着您只需要重新定义所需的差异，而不是重新定义整个对话框(使用 `sling:resourceSuperType`)。 现在，推荐使用此方法来扩展组件对话框

请参阅 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md) 以了解更多详细信息。

## 定义标记 {#defining-the-markup}

您的组件将渲染为 [HTML](https://www.w3schools.com/htmL/html_intro.asp). 您的组件需要定义所需的HTML，以便在创作和发布环境中获取所需的内容，然后根据需要进行渲染。

### 使用HTML模板语言 {#using-the-html-template-language}

此 [HTML模板语言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)随AEM 6.0引入，它取代了JSP (JavaServer Pages)，成为适用于HTML的首选和推荐的服务器端模板系统。 对于需要构建强大企业网站的Web开发人员，HTL有助于提高安全性和开发效率。

>[!NOTE]
>
>尽管HTL和JSP都可以用于开发组件，但我们在此页面上将演示使用HTL进行开发，因为它是适用于AEM的推荐脚本语言。

## 开发内容逻辑 {#developing-the-content-logic}

此可选逻辑选择和/或计算要呈现的内容。 它通过适当的Use-API模式从HTL表达式调用。

从外观中分离逻辑的机制有助于阐明对给定视图的调用。 它还允许对同一资源的不同视图使用不同的逻辑。

### 使用Java {#using-java}

[HTL Java Use-API让HTL文件可以访问自定义Java类中的Helper方法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). 这使您能够使用Java代码实施用于选择和配置组件内容的逻辑。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API让HTL文件可以访问使用JavaScript编写的帮助程序代码](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en). 这使您能够使用JavaScript代码实施用于选择和配置组件内容的逻辑。

### 使用客户端HTML库 {#using-client-side-html-libraries}

现代网站在很大程度上依赖于由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了 **客户端库文件夹**，可将您的客户端代码存储在存储库中，将其组织成不同的类别，并定义何时以及如何向客户端提供每种类别的代码。 然后，客户端库系统负责在最终网页中产生正确的链接，以加载正确的代码。

读取 [使用客户端HTML库](/help/sites-developing/clientlibs.md) 以了解更多信息。

## 配置编辑行为 {#configuring-the-edit-behavior}

您可以配置组件的编辑行为，包括组件可用的操作、就地编辑器的特征以及与组件上的事件相关的侦听器等属性。 尽管存在某些特定差异，但配置对于触屏优化UI和经典UI都是通用的。

此 [组件的编辑行为已配置](/help/sites-developing/components-basics.md#edit-behavior) 通过添加 `cq:editConfig` 类型节点 `cq:EditConfig` 在组件节点下(类型为 `cq:Component`)，并添加特定属性和子节点。

## 配置预览行为 {#configuring-the-preview-behavior}

此 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 切换为时设置Cookie **预览** 模式，即使页面未刷新。

对于呈现时对WCM模式敏感的组件，需要定义它们以专门刷新自身，然后依赖Cookie的值。

>[!NOTE]
>
>在启用了触屏操作的UI中 `EDIT` 和 `PREVIEW` 用于 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

## 创建和配置对话框 {#creating-and-configuring-a-dialog}

对话框用于允许作者与组件交互。 通过对话框，作者和/或管理员可以编辑内容、配置组件或定义设计参数(使用 [“设计”对话框](#creating-and-configuring-a-design-dialog))

### Coral用户界面和Granite用户界面 {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 和 [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 定义AEM的现代外观。

[Granite UI提供了一系列基本组件（构件）](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 需要在创作环境中创建对话框。 必要时，您可以扩展此选择并 [创建自己的构件](#creatinganewwidget).

有关完整的详细信息，请参阅：

* Coral UI

   * 在所有云解决方案中提供一致的UI
   * [AEM触屏优化UI的概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite UI

   * 提供封装在Sling组件中的Coral UI标记，用于构建UI控制台和对话框
   * [AEM触屏优化UI的概念 — Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>由于Granite UI组件的性质（以及ExtJS小部件的差异），组件与启用了触屏的UI的交互方式与 [经典UI](/help/sites-developing/developing-components-classic.md).

### 创建新对话框 {#creating-a-new-dialog}

触屏优化UI的对话框：

* 已命名 `cq:dialog`.
* 定义为 `nt:unstructured` 节点具有 `sling:resourceType` 属性集。

* 位于他们的 `cq:Component` 节点及其组件定义旁边。
* 在服务器端（作为Sling组件）根据其内容结构和 `sling:resourceType` 属性。
* 使用Granite UI框架。
* 包含描述对话框中的字段的节点结构。

   * 这些节点包括 `nt:unstructured` 具有所需的 `sling:resourceType` 属性。

示例节点结构可能是：

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

自定义对话框与开发组件类似，因为对话框本身是一个组件（即组件脚本渲染的标记以及客户端库提供的行为/样式）。

有关示例，请参阅：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果组件没有为触控式UI定义对话框，则经典UI对话框会用作兼容性层中的回退。 要自定义此类对话框，您需要自定义经典UI对话框。 请参阅 [经典UI的AEM组件](/help/sites-developing/developing-components-classic.md).

### 自定义对话框字段 {#customizing-dialog-fields}

>[!NOTE]
>
>请参阅：
>
>* 上的AEM Gems讲座 [自定义对话框字段](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
>* 下包含的相关示例代码 [代码示例 — 如何自定义对话框字段](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### 创建新字段 {#creating-a-new-field}

触屏UI的构件实施为Granite UI组件。

要创建新构件以便在启用了触屏操作的UI的组件对话框中使用，需要您 [创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>有关Granite UI的完整详细信息，请参阅 [Granite UI文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

如果将对话框视为表单元素的简单容器，则还可以将对话框内容的主要内容视为表单字段。 创建新表单字段要求您创建资源类型；这等同于创建新组件。 为了帮助您完成该任务，Granite UI提供了一个通用字段组件来继承(使用 `sling:resourceSuperType`)：

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列适合在对话框中使用的字段组件(或者，更一般地说，在 [表单](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))。

>[!NOTE]
>
>这与经典UI不同，在经典UI中，小部件的表示方式为 `cq:Widgets` 节点，每个节点具有特定 `xtype` 以建立与其相应ExtJS小部件的关系。 从实施角度来看，这些构件通过ExtJS框架在客户端呈现。

创建资源类型后，可通过在对话框中添加新节点和属性来实例化字段 `sling:resourceType` 请参阅您刚刚引入的资源类型。

#### 创建用于样式和行为的客户端库 {#creating-a-client-library-for-style-and-behavior}

如果要为组件定义样式和行为，可以创建专用的 [客户端库](/help/sites-developing/clientlibs.md) 定义您的自定义CSS/LESS和JS。

要仅为组件对话框加载客户端库（即它不会为其他组件加载），您需要设置属性 `extraClientlibs`**对话框中的**添加到刚刚创建的客户端库的类别名称。 如果您的客户端库很大和/或您的字段特定于此对话框，并且其他对话框不需要执行此操作，则建议您执行此操作。

要为所有对话框加载客户端库，请将客户端库的类别属性设置为 `cq.authoring.dialog`. 这是渲染所有对话框时默认包括的客户端库的类别名称。 如果客户端库较小和/或字段是通用的，并且可在其他对话框中重复使用，则需要执行此操作。

有关示例，请参阅：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由 [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 扩展（继承）字段 {#extending-inheriting-from-a-field}

根据您的要求，您可以：

* 通过组件继承扩展给定的Granite UI字段( `sling:resourceSuperType`)
* 通过遵循构件库API（JS/CSS继承），从基础构件库（对于Granite UI，则为Coral UI）扩展给定的构件

#### 对对话框字段的访问权限 {#access-to-dialog-fields}

您还可以使用渲染条件( `rendercondition`)，以控制有权访问对话框中特定选项卡/字段的用户；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 处理字段事件 {#handling-field-events}

处理对话框字段上的事件方法现在已完成 [自定义客户端库中的侦听器](#listeners-in-a-custom-client-library). 这与以前的方法有所不同，以前的方法是 [内容结构中的侦听器](#listenersinthecontentstructureclassicui).

#### 自定义客户端库中的监听器 {#listeners-in-a-custom-client-library}

要将逻辑注入到字段中，您应：

1. 让您的字段标记给定CSS类( *挂钩*)。
1. 在客户端库中定义一个挂接在该CSS类名称上的JS侦听器（这可确保您的自定义逻辑仅限定在字段的范围内，而不影响同一类型的其他字段）。

要实现此目的，您需要了解要与之交互的底层构件库。 请参阅 [Coral用户界面文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 以识别您要对哪个事件做出反应。 这非常类似于过去使用ExtJS执行的流程：查找给定小部件的文档页面，然后检查其事件API的详细信息。

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由 [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 内容结构中的侦听器 {#listeners-in-the-content-structure}

在使用ExtJS的经典UI中，通常内容结构中给定小组件具有侦听器。 在触屏UI中实现相同操作与内容中不再定义JS侦听器代码（或根本没有任何代码）不同。

内容结构描述了语义结构；它应该（必须）不暗示底层构件的性质。 通过在内容结构中不具有JS代码，您可以更改实施详细信息，而不必更改内容结构。 换言之，无需接触内容结构即可更改构件库。

#### 检测对话框的可用性 {#dialog-ready}

如果您有一个自定义JavaScript，只有在对话框可用并准备就绪时才需要执行，则应监听 `dialog-ready` 事件。

只要对话框加载（或重新加载）并准备就绪，即表示只要对话框的DOM中存在更改（创建/更新），就会触发此事件。

`dialog-ready` 可用于挂接JavaScript自定义代码，以对对话框或类似任务中的字段执行自定义。

### 字段验证 {#field-validation}

#### 必填字段 {#mandatory-field}

要将给定字段标记为必填字段，请在字段的内容节点上设置以下属性：

* 名称: `required`
* 类型: `Boolean`

有关示例，请参阅：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 字段验证(Granite UI) {#field-validation-granite-ui}

在Granite UI和Granite UI组件（等效于构件）中，使用进行字段验证 `foundation-validation` API。 [请参阅 `foundation-valdiation` 有关详细信息，请参阅Granite文档。](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由 [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 创建和配置设计对话框 {#creating-and-configuring-a-design-dialog}

当组件具有可在其中编辑的设计详细信息时，会提供“设计”对话框 [设计模式](/help/sites-authoring/default-components-designmode.md).

其定义与a的定义非常相似 [用于编辑内容的对话框](#creating-a-new-dialog)，不同之处在于它被定义为节点：

* 节点名称： `cq:design_dialog`
* 类型: `nt:unstructured`

## 创建和配置就地编辑器 {#creating-and-configuring-an-inplace-editor}

就地编辑器允许用户直接在段落流中编辑内容，而无需打开对话框。 例如，标准的“文本”和“标题”组件都有一个就地编辑器。

并非每个组件类型都需要/有意义的就地编辑器。

请参阅 [扩展页面创作 — 添加新的就地编辑器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 以了解更多信息。

## 自定义组件工具栏 {#customizing-the-component-toolbar}

此 [组件工具栏](/help/sites-developing/touch-ui-structure.md#component-toolbar) 允许用户访问组件的各种操作，如编辑、配置、复制和删除。

请参阅 [扩展页面创作 — 向组件工具栏添加新操作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 以了解更多信息。

## 为引用边栏配置组件（借入/借出） {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果新组件引用其他页面中的内容，则可以考虑是否希望它影响 **借用的内容** 和 **借出内容** 的部分 [**引用**](/help/sites-authoring/basic-handling.md#references) 边栏。

现成的AEM仅检查“参照”组件。 要添加组件，您需要配置OSGi捆绑包 **WCM创作内容引用配置**.

在定义中创建一个新条目，指定组件以及要检查的属性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用 AEM 时，可通过多种方法管理此类服务的配置设置。请参阅[配置 OSGi](/help/sites-deploying/configuring-osgi.md)，以了解更多详细信息和建议的做法。

## 启用组件并将组件添加到段落系统 {#enabling-and-adding-your-component-to-the-paragraph-system}

开发组件后，需要启用该组件，以便在适当的段落系统中使用，以便在所需的页面上使用。

可以通过以下任一方式完成此操作：

* 使用 [设计模式](/help/sites-authoring/default-components-designmode.md) 编辑特定页面时。
* [定义 `components` 模板的段落系统上的属性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## 配置段落系统以便拖动资产可创建组件实例 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

利用AEM，可以在您的页面上配置段落系统，以便 [当用户将资产（相应的）拖放到页面的实例上时，会自动创建新组件的实例](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （无需始终将空组件拖动到页面）。

此行为以及所需的资产到组件关系可以配置：

1. 在页面设计的段落定义下。 例如：

   * `/etc/designs/<myApp>/page/par`

   创建新节点：

   * 名称: `cq:authoring`
   * 类型: `nt:unstructured`

1. 在此下，创建一个新节点来保存所有资产到组件映射：

   * 名称: `assetToComponentMapping`
   * 类型: `nt:unstructured`

1. 对于每个资产到组件的映射，请创建一个节点：

   * 名称：文本；建议名称指示资产和相关组件类型；例如，图像
   * 类型: `nt:unstructured`

   每个配置文件均具有以下属性：

   * `assetGroup`：

      * 类型: `String`
      * 值：相关资产所属的组；例如， `media`

   * `assetMimetype`:

      * 类型: `String`
      * 值：相关资产的mime类型；例如 `image/*`

   * `droptarget`:

      * 类型: `String`
      * 值：放置目标；例如， `image`

   * `resourceType`:

      * 类型: `String`
      * 值：相关的组件资源；例如， `foundation/components/image`

   * `type`:

      * 类型: `String`
      * 值：类型，例如， `Images`

有关示例，请参阅：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-project-archetype项目](https://github.com/adobe/aem-project-archetype)
* 将项目下载为 [ZIP文件](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>使用时，现在可以在UI中轻松配置组件实例的自动创建 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和可编辑的模板。 请参阅 [创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 有关定义哪些组件自动与给定介质类型关联的更多信息。

## 使用AEM Brackets扩展 {#using-the-aem-brackets-extension}

此 [AEM Brackets扩展](/help/sites-developing/aem-brackets.md) 提供了流畅的工作流来编辑AEM组件和客户端库。 它基于 [括号](https://brackets.io/) 代码编辑器。

扩展：

* 简化同步（不需要Maven或File Vault）以帮助提高开发人员效率，并帮助具有有限AEM知识的前端开发人员参与项目。
* 提供一些 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 支持，这种模板语言旨在简化组件开发并提高安全性。

>[!NOTE]
>
>建议使用托架来创建元件。 它取代了为经典UI设计的“CRXDE Lite — 创建组件”功能。

## 从经典组件迁移 {#migrating-from-a-classic-component}

将设计为与经典UI一起使用的组件迁移到可与触屏UI一起使用的组件时（单独或联合），应考虑以下问题：

* HTL

   * 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 不是强制性的，但如果您的组件需要更新，则最好考虑更新 [从JSP迁移到HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* 组件

   * 迁移 [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 使用经典UI特定函数的代码
   * RTE插件，有关更多信息，请参阅 [配置富文本编辑器](/help/sites-administering/rich-text-editor.md).
   * [迁移 `cq:listener` 代码](#migrating-cq-listener-code) 使用特定于经典UI的函数

* 对话框

   * 创建要在触屏UI中使用的对话框。 但是，出于兼容性目的，如果没有为触控式UI定义对话框，则触控式UI可以使用经典UI对话框的定义。
   * 此 [AEM现代化工具](/help/sites-developing/modernization-tools.md) 是为了帮助您扩展现有组件而提供的。
   * [将ExtJS映射到Granite UI组件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 为ExtJS xtype和节点类型及其等效的Granite UI资源类型提供了方便的概述。
   * 自定义字段，有关更多信息，请参阅AEM Gems会话，地址为 [自定义对话框字段](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).
   * 从vtype迁移到 [Granite UI验证](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS监听器，有关更多信息，请参阅 [处理字段事件](#handling-field-events) 和AEM Gems讲座 [自定义对话框字段](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en).

### 迁移cq：listener代码 {#migrating-cq-listener-code}

如果您要迁移专为经典UI设计的项目，则 `cq:listener` 代码（和组件相关的clientlibs）可以使用特定于经典UI的函数(例如 `CQ.wcm.*`)。 对于迁移，您必须使用触屏UI中的等效对象/函数更新此类代码。

如果您的项目完全迁移到触屏UI，则需要替换此类代码，才能使用与触屏UI相关的对象和函数。

但是，如果您的项目必须在迁移期间（通常情况下）同时满足经典UI和触屏UI要求，则必须实施切换以区分引用相应对象的单独代码。

此切换机制可以按如下方式实现：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 记录组件 {#documenting-your-component}

作为开发人员，您希望能够轻松访问组件文档，以便快速了解：

* 描述
* 预期用途
* 内容结构和属性
* 公开的API和扩展点
* 等等

因此，您可以轻松地在组件本身中使用任何现有的文档标记。

放置 `README.md` 文件。 此Markdown显示在 [组件控制台](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

受支持的Markdown与 [内容片段](/help/assets/content-fragments/content-fragments-markdown.md).
