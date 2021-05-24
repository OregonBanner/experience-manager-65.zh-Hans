---
title: 开发AEM组件
seo-title: 开发AEM组件
description: AEM组件用于保存、格式化和渲染网页上提供的内容。
seo-description: AEM组件用于保存、格式化和渲染网页上提供的内容。
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 1%

---

# 开发AEM组件{#developing-aem-components}

AEM组件用于保存、格式化和渲染网页上提供的内容。

* 在[创作页面](/help/sites-authoring/default-components.md)时，组件允许作者编辑和配置内容。

   * 例如，在构建[Commerce](/help/commerce/cif-classic/administering/ecommerce.md)站点时，组件可以从目录中收集和渲染信息。
有关更多信息，请参阅[开发电子商务](/help/commerce/cif-classic/developing/ecommerce.md)。

   * 在构建[Communities](/help/communities/author-communities.md)站点时，组件可以向访客提供信息并从访客那里收集信息。
有关更多信息，请参阅[开发社区](/help/communities/communities.md)。

* 在发布实例中，组件会渲染您的内容，并根据您的要求向网站访客显示内容。

>[!NOTE]
>
>本页是文档[AEM组件 — 基础知识](/help/sites-developing/components-basics.md)的继续。

>[!CAUTION]
>
>`/libs/cq/gui/components/authoring/dialog`下的组件仅用于编辑器（创作中的组件对话框）中。 如果在其他位置（例如在向导对话框中）使用它们，则它们可能无法按预期运行。

## 代码样本 {#code-samples}

本页提供了为AEM开发新组件所需的参考文档（或引用文档的链接）。 有关一些实用示例，请参阅[开发AEM组件 — 代码示例](/help/sites-developing/developing-components-samples.md)。

## 结构 {#structure}

[AEM组件 — 基础知识](/help/sites-developing/components-basics.md#structure)页面上介绍了组件的基本结构。 该文档涵盖触屏UI和经典UI。 即使您不需要在新组件中使用经典设置，在继承现有组件时，也需要注意这些设置。

## 扩展现有组件和对话框{#extending-existing-components-and-dialogs}

根据要实施的组件，可以扩展或自定义现有实例，而不是从头开始定义和开发整个[结构](#structure)。

扩展或自定义现有组件或对话框时，您可以在进行更改之前复制或复制对话框所需的整个结构或结构。

### 扩展现有组件{#extending-an-existing-component}

使用[资源类型层次结构](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance)和相关继承机制可以扩展现有组件。

>[!NOTE]
>
>元件还可以使用基于搜索路径逻辑的叠加来重新定义。 但是，在这种情况下，将不会触发[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)，并且`/apps`必须定义整个叠加。

>[!NOTE]
>
>也可以自定义和扩展[内容片段组件](/help/sites-developing/customizing-content-fragments.md)，但必须考虑资产的完整结构和关系。

### 自定义现有组件对话框{#customizing-a-existing-component-dialog}

还可以使用[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)来覆盖&#x200B;*组件对话框*，并定义属性`sling:resourceSuperType`。

这表示您只需重定义所需的差异，而不是重定义整个对话框（使用`sling:resourceSuperType`）。 现在建议使用此方法来扩展组件对话框

有关更多详细信息，请参阅[Sling资源合并器](/help/sites-developing/sling-resource-merger.md)。

## 定义标记{#defining-the-markup}

组件将以[HTML](https://www.w3schools.com/htmL/html_intro.asp)呈现。 您的组件需要定义获取所需内容所需的HTML，然后在创作和发布环境中根据需要渲染该内容。

### 使用HTML模板语言{#using-the-html-template-language}

随AEM 6.0引入的[HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)取代了JSP(JavaServer Pages)，成为HTML的首选和推荐的服务器端模板系统。 对于需要构建强大企业网站的Web开发人员，HTL有助于提高安全性和开发效率。

>[!NOTE]
>
>尽管HTL和JSP都可用于开发组件，但我们将在本页上使用HTL来说明开发，因为它是AEM的推荐脚本语言。

## 开发内容逻辑{#developing-the-content-logic}

此可选逻辑选择和/或计算要渲染的内容。 它可通过相应的Use-API模式从HTL表达式中调用。

将逻辑与外观分离的机制有助于阐明对给定视图所调用的内容。 它还允许对同一资源的不同视图使用不同的逻辑。

### 使用Java {#using-java}

[HTL Java Use-API允许HTL文件访问自定义Java类中的Helper方法](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)。这允许您使用Java代码实施用于选择和配置组件内容的逻辑。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API允许HTL文件访问使用JavaScript编写的帮助程序代码](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html)。这允许您使用JavaScript代码实施用于选择和配置组件内容的逻辑。

### 使用客户端HTML库{#using-client-side-html-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了&#x200B;**客户端库文件夹**，这允许您将客户端代码存储在存储库中，将其组织到各个类别中，并定义何时以及如何将每个类别的代码提供给客户端。 然后，客户端库系统会负责在最终网页中生成正确的链接，以加载正确的代码。

请阅读[使用客户端HTML库](/help/sites-developing/clientlibs.md)以了解更多信息。

## 配置编辑行为{#configuring-the-edit-behavior}

您可以配置组件的编辑行为，包括组件可用的操作等属性、就地编辑器的特性以及与组件上的事件相关的侦听器。 触屏UI和经典UI都使用此配置，尽管这两种配置存在某些特定差异。

组件的[编辑行为配置为](/help/sites-developing/components-basics.md#edit-behavior)，具体方法是：在组件节点（`cq:Component`类型）下添加`cq:editConfig`类型的`cq:EditConfig`节点，并添加特定属性和子节点。

## 配置预览行为{#configuring-the-preview-behavior}

切换到&#x200B;**预览**&#x200B;模式时，即使页面未刷新，也会设置[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

对于呈现的对WCM模式敏感的组件，需要定义它们以专门刷新它们，然后依赖Cookie的值。

>[!NOTE]
>
>在触屏启用UI中，仅`EDIT`和`PREVIEW`值用于[ WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

## 创建和配置对话框{#creating-and-configuring-a-dialog}

对话框用于允许作者与组件进行交互。 使用对话框，作者和/或管理员可以编辑内容、配置组件或定义设计参数（使用[设计对话框](#creating-and-configuring-a-design-dialog)）

### Coral UI和Granite UI {#coral-ui-and-granite-ui}

[Coral ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) UI [和](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite UI定义了AEM的现代外观。

[Granite UI提供了在创作环境中创建对话框所需的大量基本组件（小组件）](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 。如有必要，您可以扩展此选择并[创建您自己的小组件](#creatinganewwidget)。

有关使用Coral和Granite资源类型开发组件的更多信息，请参阅：[使用Coral/Granite资源类型构建Experience Manager组件](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)。

有关完整详细信息，请参阅：

* Coral用户界面

   * 在所有云解决方案中提供一致的UI
   * [AEM触屏优化UI的概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite用户界面

   * 提供封装在Sling组件中的Coral UI标记，以用于构建UI控制台和对话框
   * [AEM触屏优化UI的概念 — Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite用户界面文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>由于Granite UI组件的性质（以及与ExtJS小组件的不同），组件与触屏优化UI和[经典UI](/help/sites-developing/developing-components-classic.md)的交互方式存在一些差异。

### 创建新对话框{#creating-a-new-dialog}

触屏UI的对话框：

* 名为`cq:dialog`。
* 定义为设置了`sling:resourceType`属性的`nt:unstructured`节点。

* 位于其`cq:Component`节点下，且位于其组件定义旁边。
* 基于组件的内容结构和`sling:resourceType`属性，在服务器端呈现（作为Sling组件）。
* 使用Granite UI框架。
* 包含描述对话框中字段的节点结构。

   * 这些节点是具有所需`sling:resourceType`属性的`nt:unstructured`。

示例节点结构可能为：

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

自定义对话框与开发组件类似，因为对话框本身是组件（即组件脚本渲染的标记以及客户端库提供的行为/样式）。

有关示例，请参阅：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果组件没有为触屏优化UI定义对话框，则经典UI对话框将用作兼容性层内的回退。 要自定义此类对话框，您需要自定义经典UI对话框。 请参阅[AEM Components for the Classic UI](/help/sites-developing/developing-components-classic.md)。

### 自定义对话框字段{#customizing-dialog-fields}

>[!NOTE]
>
>请参阅：
>
>* [自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的AEM Gems会话。
>* [代码示例 — 如何自定义对话框字段](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)下涵盖的相关示例代码。

>



#### 创建新字段{#creating-a-new-field}

触屏UI的小组件作为Granite UI组件实施。

要创建新小组件以在触屏UI的组件对话框中使用，需要[创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)。

>[!NOTE]
>
>有关Granite UI的完整详细信息，请参阅[Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

如果将对话框视为表单元素的简单容器，则还可以将对话框内容的主要内容视为表单字段。 创建新表单字段需要创建资源类型；这等同于创建新组件。 为了帮助您完成该任务，Granite UI提供了一个要从中继承的通用字段组件（使用`sling:resourceSuperType`）：

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列字段组件，这些组件适合在对话框（或更一般地，在[forms](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)中）中使用。

>[!NOTE]
>
>这与经典UI不同，在经典UI中，小组件由`cq:Widgets`节点表示，每个节点具有特定的`xtype`，以便与相应的ExtJS小组件建立关系。 从实施角度来看，这些小组件是通过ExtJS框架在客户端渲染的。

创建资源类型后，您可以通过在对话框中添加新节点来实例化字段，该节点的属性`sling:resourceType`引用了您刚才引入的资源类型。

#### 为样式和行为创建客户端库{#creating-a-client-library-for-style-and-behavior}

如果要为组件定义样式和行为，可以创建专用的[客户端库](/help/sites-developing/clientlibs.md)来定义自定义CSS/LESS和JS。

要仅为组件对话框加载客户端库（即不会为其他组件加载），您需要将对话框的属性`extraClientlibs`** **设置为刚刚创建的客户端库的类别名称。 如果您的客户端库非常大，并且/或您的字段特定于该对话框，而在其他对话框中不需要，则建议使用此方法。

要为所有对话框加载客户端库，请将客户端库的category属性设置为`cq.authoring.dialog`。 这是客户端库的类别名称，默认情况下，在渲染所有对话框时会包含此名称。 如果客户端库很小，并且/或您的字段是通用的，并且可以在其他对话框中重复使用，则需要执行此操作。

有关示例，请参阅：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

#### 扩展（继承）字段{#extending-inheriting-from-a-field}

根据您的要求，您可以：

* 通过组件继承扩展给定的Granite UI字段(`sling:resourceSuperType`)
* 通过遵循小组件库API（JS/CSS继承），从基础小组件库扩展给定小组件（对于Granite UI，即Coral UI）

#### 对对话框字段{#access-to-dialog-fields}的访问权限

您还可以使用渲染条件(`rendercondition`)来控制谁有权访问对话框中的特定选项卡/字段；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 处理字段事件{#handling-field-events}

现在，处理对话框字段中事件的方法已通过自定义客户端库](#listeners-in-a-custom-client-library)中的[侦听器完成。 这与在内容结构](#listenersinthecontentstructureclassicui)中具有[侦听器的旧方法相比有所变化。

#### 自定义客户端库{#listeners-in-a-custom-client-library}中的侦听器

要在字段中插入逻辑，您应：

1. 使用给定的CSS类标记字段(*hook*)。
1. 在客户端库中定义一个挂接到该CSS类名称的JS侦听器（这可确保自定义逻辑的范围仅限您的字段，并且不会影响其他相同类型的字段）。

要实现此目的，您需要了解要与之交互的底层小组件库。 请参阅[Coral UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)以确定要对哪个事件做出响应。 这与您过去使用ExtJS执行的过程非常相似：找到给定小组件的文档页面，然后查看其事件API的详细信息。

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

#### 内容结构{#listeners-in-the-content-structure}中的侦听器

在使用ExtJS的经典UI中，通常会在内容结构中为给定小组件设置侦听器。 由于JS侦听器代码（或根本不是任何代码）不再在内容中定义，因此在触屏UI中实现相同的方式有所不同。

内容结构描述语义结构；它不应（必须）暗示基础小组件的性质。 通过在内容结构中不包含JS代码，您可以更改实施详细信息，而无需更改内容结构。 换言之，您无需触摸内容结构即可更改小组件库。

#### 检测对话框{#dialog-ready}的可用性

如果您有一个自定义JavaScript，该JavaScript需要仅在对话框可用且准备就绪时才执行，则应该侦听`dialog-ready`事件。

当对话框加载（或重新加载）并准备就绪以供使用时，将触发此事件，这意味着每当对话框的DOM中发生更改（创建/更新）时。

`dialog-ready` 可用于挂接JavaScript自定义代码，该代码可对对话框或类似任务中的字段执行自定义。

### 字段验证{#field-validation}

#### 必填字段{#mandatory-field}

要将给定字段标记为必填字段，请在字段的内容节点上设置以下属性：

* 名称: `required`
* 类型: `Boolean`

有关示例，请参阅：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 字段验证(Granite UI){#field-validation-granite-ui}

使用`foundation-validation` API完成了Granite UI和Granite UI组件（等同于小组件）中的字段验证。 [有关详细 `foundation-valdiation` 信息，请参阅Granite文档。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * [代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 创建和配置设计对话框{#creating-and-configuring-a-design-dialog}

当组件具有可在[设计模式](/help/sites-authoring/default-components-designmode.md)中编辑的设计详细信息时，将提供“设计”对话框。

定义与用于编辑内容](#creating-a-new-dialog)的[对话框的定义非常相似，不同之处在于它被定义为节点：

* 节点名称：`cq:design_dialog`
* 类型: `nt:unstructured`

## 创建和配置就地编辑器{#creating-and-configuring-an-inplace-editor}

就地编辑器允许用户直接在段落流中编辑内容，而无需打开对话框。 例如，标准的文本组件和标题组件都具有就地编辑器。

并非每个组件类型都需要/有意义的就地编辑器。

有关更多信息，请参阅[扩展页面创作 — 添加新的就地编辑器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

## 自定义组件工具栏{#customizing-the-component-toolbar}

[组件工具栏](/help/sites-developing/touch-ui-structure.md#component-toolbar)允许用户访问组件的一系列操作，如编辑、配置、复制和删除。

有关更多信息，请参阅[扩展页面创作 — 向组件工具栏添加新操作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 。

## 为引用边栏（借入/借出）{#configuring-a-component-for-the-references-rail-borrowed-lent}配置组件

如果新组件引用了来自其他页面的内容，则您可以考虑是否希望它影响&#x200B;[**引用**](/help/sites-authoring/basic-handling.md#references)&#x200B;边栏的&#x200B;**借入内容**&#x200B;和&#x200B;**借出内容**&#x200B;部分。

现成的AEM仅检查引用组件。 要添加组件，您需要配置OSGi包&#x200B;**WCM创作内容引用配置**。

在定义中创建新条目，指定组件以及要检查的属性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用AEM时，可通过多种方法来管理此类服务的配置设置。有关更多详细信息和建议的实践，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md) 。

## 启用组件并将其添加到段落系统{#enabling-and-adding-your-component-to-the-paragraph-system}

开发组件后，需要启用该组件以在相应的段落系统中使用，以便在所需的页面上使用。

这可以通过以下任一方式完成：

* 在编辑特定页面时使用[设计模式](/help/sites-authoring/default-components-designmode.md)。
* [在模 `components` 板的段落系统中定义属性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## 配置段落系统以便拖动资产会创建组件实例{#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM提供了在页面上配置段落系统的功能，以便当用户将（相应的）资产拖动到该页面的实例](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui)时，自动创建新组件的[实例（而不必始终将空组件拖动到页面）。

可以配置此行为和所需的资产到组件关系：

1. 在页面设计的段落定义下。 例如：

   * `/etc/designs/<myApp>/page/par`

   创建新节点：

   * 名称: `cq:authoring`
   * 类型: `nt:unstructured`


1. 在此下，创建一个新节点以保存所有资产到组件映射：

   * 名称: `assetToComponentMapping`
   * 类型: `nt:unstructured`

1. 对于每个资产到组件映射，创建一个节点：

   * 名称：文本；建议名称指示资产及相关组件类型；例如，图像
   * 类型: `nt:unstructured`

   每个资产均具有以下属性：

   * `assetGroup`:

      * 类型: `String`
      * 值：相关资产所属之组别；例如，`media`
   * `assetMimetype`:

      * 类型: `String`
      * 值：相关资产的mime类型；例如`image/*`
   * `droptarget`:

      * 类型: `String`
      * 值：落靶；例如，`image`
   * `resourceType`:

      * 类型: `String`
      * 值：相关组件资源；例如，`foundation/components/image`
   * `type`:

      * 类型: `String`
      * 值：类型，例如`Images`






有关示例，请参阅：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-project-archetype项目](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* 将项目下载为[a ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>现在，使用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)和可编辑的模板时，可以轻松地在UI中配置组件实例的自动创建。 请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) ，以了解有关定义与给定媒体类型自动关联的组件的详细信息。

## 使用AEM Brackets扩展{#using-the-aem-brackets-extension}

[AEM Brackets扩展](/help/sites-developing/aem-brackets.md)提供了一个编辑AEM组件和客户端库的顺畅工作流。 它基于[Brackets](https://brackets.io/)代码编辑器。

扩展：

* 简化了同步（不需要Maven或File Vault），以帮助提高开发人员效率，并帮助知识有限的前端开发人员参与项目。
* 提供一些[HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)支持，该模板语言旨在简化组件开发并提高安全性。

>[!NOTE]
>
>建议使用括号来创建组件。 它取代了专为经典UI设计的CRXDE Lite — 创建组件功能。

## 从经典组件{#migrating-from-a-classic-component}迁移

将专为与经典UI一起使用而设计的组件迁移到可与触屏UI一起使用的组件（单独或联合使用）时，应考虑以下问题：

* HTL

   * 不强制使用[HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)，但如果组件需要更新，则最好考虑从JSP迁移到HTL](/help/sites-developing/components-basics.md#htl-vs-jsp)。[

* 组件

   * 迁移使用经典UI特定函数的[ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code)代码
   * RTE插件，以了解更多信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。
   * [迁移 `cq:listener` ](#migrating-cq-listener-code) 代码时使用特定于经典UI的函数

* 对话框

   * 您需要创建一个新对话框以在触屏UI中使用。 但是，出于兼容目的，当未为触屏UI定义任何对话框时，触屏UI可以使用经典UI对话框的定义。
   * 提供[AEM现代化工具](/help/sites-developing/modernization-tools.md)以帮助扩展现有组件。
   * [将ExtJS映射到Granite UI组](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 件可方便地概述ExtJS xtypes和节点类型及其等效的Granite UI资源类型。
   * 自定义字段，有关更多信息，请参阅[自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的AEM Gems会话。
   * 从类型迁移到[Granite UI验证](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS侦听器，有关更多信息，请参阅[自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的[处理字段事件](#handling-field-events)和AEM Gems会话。

### 迁移cq:listener代码{#migrating-cq-listener-code}

如果您迁移的项目是为经典UI设计的，则`cq:listener`代码（以及与组件相关的clientlib）可能使用特定于经典UI的函数（如`CQ.wcm.*`）。 对于迁移，必须使用触屏UI中的对等对象/函数来更新此类代码。

如果您的项目完全迁移到触屏优化UI，您需要替换此类代码以使用与触屏优化UI相关的对象和函数。

但是，如果您的项目在迁移期间（通常情况下）必须同时满足经典UI和触屏优化UI的需求，则您需要实施一个开关以区分引用相应对象的单独代码。

此切换机制可实现为：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 记录组件{#documenting-your-component}

作为开发人员，您希望轻松访问组件文档，以便快速了解：

* 描述
* 预期用途
* 内容结构和属性
* 公开的API和扩展点
* 等等

因此，很容易就会在组件中使用您现有的任何文档标记。

您只需在组件结构中放置一个`README.md`文件即可。 然后，此标记将显示在[组件控制台](/help/sites-authoring/default-components-console.md)中。

![chlimage_1-7](assets/chlimage_1-7.png)

支持的标记与[内容片段](/help/assets/content-fragments/content-fragments-markdown.md)的标记相同。
