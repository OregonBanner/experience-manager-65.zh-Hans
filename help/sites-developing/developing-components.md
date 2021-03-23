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
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 1%

---


# 开发AEM组件{#developing-aem-components}

AEM组件用于保存、格式化和渲染网页上提供的内容。

* 创作页面[时，组件允许作者编辑和配置内容。](/help/sites-authoring/default-components.md)

   * 例如，在构建[Commerce](/help/sites-administering/ecommerce.md)站点时，组件可以从目录中收集和呈现信息。
有关详细信息，请参阅[开发电子商务](/help/sites-developing/ecommerce.md)。

   * 在构建[Communities](/help/communities/author-communities.md)站点时，组件可以向访客提供信息并从其中收集信息。
有关详细信息，请参阅[开发社区](/help/communities/communities.md)。

* 在发布实例中，组件会呈现您的内容，并根据您的需要将其呈现给网站访客。

>[!NOTE]
>
>本页是文档[AEM组件 — 基础](/help/sites-developing/components-basics.md)的继续。

>[!CAUTION]
>
>`/libs/cq/gui/components/authoring/dialog`下的组件只能在编辑器中使用（“创作”中的组件对话框）。 如果在其他位置（例如在向导对话框中）使用它们，则它们的行为可能不会按预期方式。

## 代码样本 {#code-samples}

本页提供为AEM开发新组件所需的参考文档（或参考文档的链接）。 有关一些实际示例，请参阅[开发AEM组件 — 代码示例](/help/sites-developing/developing-components-samples.md)。

## 结构 {#structure}

[AEM组件 — 基础知识](/help/sites-developing/components-basics.md#structure)页上介绍了组件的基本结构。 该文档涵盖触屏优化UI和经典UI。 即使您不需要在新组件中使用经典设置，在从现有组件继承时也可以了解这些设置。

## 扩展现有组件和对话框{#extending-existing-components-and-dialogs}

根据要实现的组件，可能可以扩展或自定义现有实例，而不是从头定义和开发整个[结构](#structure)。

在扩展或自定义现有组件或对话框时，您可以复制或复制对话框所需的整个结构或结构，然后再进行更改。

### 扩展现有组件{#extending-an-existing-component}

可以使用[资源类型层次结构](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance)和相关继承机制扩展现有组件。

>[!NOTE]
>
>还可以使用基于搜索路径逻辑的叠加来重新定义元件。 但是，在这种情况下，将不会触发[Sling资源合并](/help/sites-developing/sling-resource-merger.md)，并且`/apps`必须定义整个叠加。

>[!NOTE]
>
>[内容片段组件](/help/sites-developing/customizing-content-fragments.md)也可以进行自定义和扩展，但必须考虑完整结构和与资产的关系。

### 自定义现有组件对话框{#customizing-a-existing-component-dialog}

还可以使用[Sling资源合并](/help/sites-developing/sling-resource-merger.md)覆盖&#x200B;*组件对话框*&#x200B;并定义属性`sling:resourceSuperType`。

这意味着您只需重定义所需的差异，而不是重定义整个对话框（使用`sling:resourceSuperType`）。 现在建议使用此方法来扩展组件对话框

有关更多详细信息，请参阅[Sling Resource Merabure](/help/sites-developing/sling-resource-merger.md)。

## 定义标记{#defining-the-markup}

组件将使用[HTML](https://www.w3schools.com/htmL/html_intro.asp)进行呈现。 您的组件需要定义需要的HTML，以便获取所需的内容，然后根据需要在创作和发布环境上呈现它。

### 使用HTML模板语言{#using-the-html-template-language}

随AEM 6.0引入的[HTML模板语言(HTL)](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)代替JSP(JavaServer Pages)作为HTML的首选和推荐的服务器端模板系统。 对于需要构建强大企业网站的Web开发人员，HTL有助于提高安全性和开发效率。

>[!NOTE]
>
>虽然HTL和JSP都可用于开发组件，但我们将在本页用HTL来说明开发，因为它是AEM的推荐脚本语言。

## 开发内容逻辑{#developing-the-content-logic}

此可选逻辑选择和/或计算要呈现的内容。 它从具有相应Use-API模式的HTL表达式中调用。

将逻辑与外观分离的机制有助于阐明对给定视图所调用的内容。 它还允许同一资源的不同视图有不同的逻辑。

### 使用Java {#using-java}

[HTL Java Use-API使HTL文件能够访问自定义Java类中的帮助程序方法](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)。这允许您使用Java代码实现用于选择和配置组件内容的逻辑。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API使HTL文件能够访问用JavaScript编写的帮助代码](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html)。这允许您使用JavaScript代码实现用于选择和配置组件内容的逻辑。

### 使用客户端HTML库{#using-client-side-html-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供&#x200B;**客户端库文件夹**，允许您将客户端代码存储在存储库中，将其组织到类别中，并定义将每个代码类别提供给客户端的时间和方式。 然后，客户端库系统将负责在最终网页中生成正确的链接，以加载正确的代码。

有关详细信息，请阅读[使用客户端HTML库](/help/sites-developing/clientlibs.md)。

## 配置编辑行为{#configuring-the-edit-behavior}

您可以配置组件的编辑行为，这些属性包括可用于组件的操作、就地编辑器的特性以及与组件上的事件相关的侦听器等。 该配置对触屏优化UI和经典UI都是通用的，尽管有某些特定的差异。

通过在组件节点（`cq:Component`类型）下添加`cq:EditConfig`类型的`cq:editConfig`节点，并添加特定属性和子节点，配置组件的[编辑行为。](/help/sites-developing/components-basics.md#edit-behavior)

## 配置预览行为{#configuring-the-preview-behavior}

在切换到&#x200B;**预览**&#x200B;模式时，即使页面未刷新，也会设置[WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

对于呈现对WCM模式敏感的组件，需要定义这些组件以具体刷新它们，然后依赖Cookie的值。

>[!NOTE]
>
>在触屏优化UI中，仅`EDIT`和`PREVIEW`值用于[ WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie。

## 创建和配置对话框{#creating-and-configuring-a-dialog}

对话框用于允许作者与组件进行交互。 使用对话框允许作者和/或管理员编辑内容、配置组件或定义设计参数（使用[设计对话框](#creating-and-configuring-a-design-dialog)）

### Coral UI和Granite UI {#coral-ui-and-granite-ui}

[Coral ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) UI和 [Granite ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) UI定义AEM的现代外观。

[Granite UI提供了在创作环境上创建对](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 话框所需的大量基本组件（构件）。必要时，您可以扩展此选择并[创建您自己的Widget](#creatinganewwidget)。

有关使用Coral和Granite资源类型开发组件的更多信息，请参阅：[使用Coral/Granite资源类型](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)构建Experience Manager组件。

有关完整的详细信息，请参阅：

* Coral UI

   * 在所有云解决方案中提供一致的UI
   * [AEM触屏优化UI的概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite UI

   * 提供打包到Sling组件中的Coral UI标记，用于构建UI控制台和对话框
   * [AEM触屏优化UI的概念 — Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>由于Granite UI组件的性质（以及与ExtJS窗口组件的不同），组件与触屏优化UI和[经典UI](/help/sites-developing/developing-components-classic.md)的交互方式之间存在一些差异。

### 创建新对话框{#creating-a-new-dialog}

触屏优化UI的对话框：

* 名为`cq:dialog`。
* 定义为`sling:resourceType`属性集的`nt:unstructured`节点。

* 位于其`cq:Component`节点下，并位于其组件定义旁。
* 基于其内容结构和`sling:resourceType`属性在服务器端呈现（作为Sling组件）。
* 使用Granite UI框架。
* 包含描述对话框中字段的节点结构。

   * 这些节点是`nt:unstructured`，具有所需的`sling:resourceType`属性。

节点结构的示例可以是：

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

自定义对话框与开发组件类似，因为对话框本身是组件（即组件脚本呈现的标记以及客户端库提供的行为/样式）。

有关示例，请参阅：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果组件没有为触屏优化UI定义对话框，则经典UI对话框将用作兼容性层内的回退。 要自定义此类对话框，您需要自定义经典UI对话框。 请参阅[用于经典UI的AEM组件](/help/sites-developing/developing-components-classic.md)。

### 自定义对话框字段{#customizing-dialog-fields}

>[!NOTE]
>
>请参阅：
>
>* [自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的AEM Gems会话。
>* [代码示例 — 如何自定义对话框字段](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)中介绍的相关示例代码。

>



#### 创建新字段{#creating-a-new-field}

触屏优化UI的构件作为Granite UI组件实现。

要为触屏优化UI创建新Widget以在组件对话框中使用，需要[创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)。

>[!NOTE]
>
>有关Granite UI的完整详细信息，请参阅[Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

如果您将对话框视为表单元素的简单容器，则还可以将对话框内容的主要内容作为表单域查看。 创建新表单字段需要创建资源类型；这等同于创建新组件。 为了帮助您在该任务中完成工作，Granite UI将优惠一个要继承的通用字段组件（使用`sling:resourceSuperType`）：

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列适用于对话框（或更一般地，以[形式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)）的字段组件。

>[!NOTE]
>
>这与经典UI不同，在经典UI中，构件由`cq:Widgets`节点表示，每个节点具有特定的`xtype`，以建立与相应ExtJS构件的关系。 从实施角度来看，这些构件是通过ExtJS框架在客户端呈现的。

创建资源类型后，可以通过在对话框中添加新节点来实例化字段，属性`sling:resourceType`引用您刚引入的资源类型。

#### 为样式和行为创建客户端库{#creating-a-client-library-for-style-and-behavior}

如果要为组件定义样式和行为，可创建专用的[客户端库](/help/sites-developing/clientlibs.md)，用于定义自定义CSS/LESS和JS。

要仅为您的组件对话框加载您的客户端库（即不会为其他组件加载它），您需要将对话框的属性`extraClientlibs`** **设置为您刚刚创建的客户端库的类别名。 如果您的客户端库很大，并且/或您的字段特定于该对话框，而在其他对话中不需要您，则建议这样做。

要加载所有对话框的客户端库，请将客户端库的类别属性设置为`cq.authoring.dialog`。 这是显示所有对话框时默认包含的客户端库的类别名称。 如果客户端库很小，且/或字段是通用的，并且可能在其他对话框中重用，则您希望这样做。

有关示例，请参阅：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由[代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

#### 扩展（继承自）字段{#extending-inheriting-from-a-field}

根据您的要求，您可以：

* 通过组件继承扩展给定的Granite UI字段(`sling:resourceSuperType`)
* 通过遵循构件库API（JS/CSS继承），从基础构件库扩展给定构件（对于Granite UI，这是Coral UI）

#### 访问对话框字段{#access-to-dialog-fields}

您还可以使用渲染条件(`rendercondition`)来控制谁有权访问对话框中的特定选项卡/字段；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 处理字段事件{#handling-field-events}

现在，对对话框字段的事件处理方法在自定义客户端库](#listeners-in-a-custom-client-library)中的[侦听器中完成。 这与在内容结构](#listenersinthecontentstructureclassicui)中具有[侦听器的旧方法相比有所变化。

#### 自定义客户端库{#listeners-in-a-custom-client-library}中的侦听器

要将逻辑插入字段，您应：

1. 将您的字段标记为给定的CSS类(*hook*)。
1. 在客户端库中定义一个挂接到该CSS类名的JS侦听器（这可确保您的自定义逻辑仅作用于您的字段，且不影响同一类型的其他字段）。

要实现此目的，您需要了解要与之交互的基础Widget库。 请参阅[Coral UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)以确定要对哪个事件做出响应。 这与您过去使用ExtJS执行的过程非常相似：查找给定构件的文档页面，然后检查其事件 API的详细信息。

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由[代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

#### 内容结构{#listeners-in-the-content-structure}中的侦听器

在具有ExtJS的经典UI中，通常在内容结构中具有给定Widget的侦听器。 在触屏优化UI中实现相同功能是不同的，因为JS侦听器代码（或任何代码）在内容中已不再定义。

内容结构描述了语义结构；它不应（必须）暗示基础构件的性质。 如果内容结构中没有JS代码，则无需更改内容结构即可更改实施详细信息。 换句话说，您无需触摸内容结构即可更改构件库。

#### 检测对话框{#dialog-ready}的可用性

如果您有自定义JavaScript，只有在对话框可用且准备就绪时才需要执行，则应侦听`dialog-ready`事件。

当对话框加载（或重新加载）并准备使用时，将触发此事件，这意味着当对话框的DOM中发生更改（创建/更新）时。

`dialog-ready` 可用于在JavaScript自定义代码中挂接，该代码对对话框或类似任务中的字段执行自定义。

### 字段验证{#field-validation}

#### 必填字段{#mandatory-field}

要将给定字段标记为必填，请在字段的内容节点上设置以下属性：

* 名称: `required`
* 类型: `Boolean`

有关示例，请参阅：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 字段验证(Granite UI){#field-validation-granite-ui}

Granite UI和Granite UI组件（等效于构件）中的字段验证是使用`foundation-validation` API完成的。 [有关详细信息， `foundation-valdiation` 请参阅Granite文档。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由[代码示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)提供

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 创建和配置设计对话框{#creating-and-configuring-a-design-dialog}

当组件具有可在[设计模式](/help/sites-authoring/default-components-designmode.md)中编辑的设计详细信息时，将提供“设计”对话框。

该定义与用于编辑内容](#creating-a-new-dialog)的[对话框的定义非常相似，其区别在于它被定义为节点：

* 节点名称：`cq:design_dialog`
* 类型: `nt:unstructured`

## 创建和配置就地编辑器{#creating-and-configuring-an-inplace-editor}

就地编辑器允许用户直接编辑段落流中的内容，无需打开对话框。 例如，标准文本组件和标题组件都具有就地编辑器。

对于每个组件类型，就地编辑器并非必需/有意义。

有关详细信息，请参阅[扩展页面创作 — 添加新就地编辑器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

## 自定义组件工具栏{#customizing-the-component-toolbar}

[组件工具栏](/help/sites-developing/touch-ui-structure.md#component-toolbar)允许用户访问组件的一系列操作，如编辑、配置、复制和删除。

有关详细信息，请参阅[扩展页面创作 — 向组件工具栏添加新操作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar)。

## 为引用边栏配置组件（借入/借出）{#configuring-a-component-for-the-references-rail-borrowed-lent}

如果您的新组件引用了其他页面的内容，则您可以考虑是否希望它影响&#x200B;[**引用**](/help/sites-authoring/basic-handling.md#references)&#x200B;边栏的&#x200B;**借入内容**&#x200B;和&#x200B;**借出内容**&#x200B;部分。

现成的AEM只检查引用组件。 要添加组件，您需要配置OSGi bundle **WCM创作内容引用配置**。

在定义中创建新条目，指定您的组件以及要检查的属性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用AEM时，有多种方法可管理此类服务的配置设置。有关更多详细信息和建议的做法，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。

## 启用组件并将其添加到段落系统{#enabling-and-adding-your-component-to-the-paragraph-system}

开发组件后，需要启用该组件以在相应的段落系统中使用，以便在所需的页面上使用。

可通过以下任一方式执行此操作：

* 编辑特定页面时使用[设计模式](/help/sites-authoring/default-components-designmode.md)。
* [在模 `components` 板的段落系统中定义属性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## 配置段落系统以便拖动资产可创建组件实例{#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM优惠在您的页面上配置段落系统，以便当用户将（适当）资产拖动到该页面](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui)的实例时，会自动创建新组件的[实例（而不是总是将空组件拖动到页面）。

可以配置此行为以及所需的资产与组件关系：

1. 在页面设计的段落定义下。 例如：

   * `/etc/designs/<myApp>/page/par`

   创建新节点：

   * 名称: `cq:authoring`
   * 类型: `nt:unstructured`


1. 在此下，创建一个新节点以保存所有资产到组件映射：

   * 名称: `assetToComponentMapping`
   * 类型: `nt:unstructured`

1. 对于每个资产到组件映射，请创建一个节点：

   * 名称：文本；建议名称指示资产及相关组件类型；例如，图像
   * 类型: `nt:unstructured`

   每个都具有以下属性：

   * `assetGroup`:

      * 类型: `String`
      * 值：相关资产所属的组；例如，`media`
   * `assetMimetype`:

      * 类型: `String`
      * 值：相关资产的mime类型；例如`image/*`
   * `droptarget`:

      * 类型: `String`
      * 值：投掷目标;例如，`image`
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
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>现在，使用[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)和可编辑模板时，可以在UI中轻松配置组件实例的自动创建。 有关定义与给定媒体类型自动关联的组件的详细信息，请参阅[创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

## 使用AEM Brackets扩展{#using-the-aem-brackets-extension}

[AEM Brackets Extension](/help/sites-developing/aem-brackets.md)提供了编辑AEM组件和客户端库的流畅工作流。 它基于[Brackets](https://brackets.io/)代码编辑器。

扩展：

* 简化同步（不需要Maven或File Vault），以帮助提高开发人员效率，并帮助具有有限AEM知识的前端开发人员参与项目。
* 提供某些[HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)支持，该模板语言旨在简化组件开发并提高安全性。

>[!NOTE]
>
>建议使用Brackets来创建组件。 它替换了专为经典UI设计的CRXDE Lite — 创建组件功能。

## 从经典组件{#migrating-from-a-classic-component}迁移

将设计用于经典UI的组件迁移到可与触屏优化UI一起使用的组件（单独或联合使用）时，应考虑以下问题：

* HTL

   * 使用[HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)并非强制性的，但如果您的组件需要更新，则最好考虑从JSP迁移到HTL](/help/sites-developing/components-basics.md#htl-vs-jsp)。[

* 组件

   * 迁移使用经典UI特定函数的[ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code)代码
   * RTE插件，有关详细信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。
   * [迁 `cq:listener` ](#migrating-cq-listener-code) 移使用经典UI特定函数的代码

* 对话框

   * 您需要创建新对话框才能在触屏优化UI中使用。 但是，出于兼容性考虑，当未为触屏优化UI定义对话框时，触屏优化UI可以使用经典UI对话框的定义。
   * 提供[AEM现代化工具](/help/sites-developing/modernization-tools.md)以帮助您扩展现有组件。
   * [将ExtJS映射到Granite UI组](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 件可方便地概述ExtJS xtypes和节点类型及其等效的Granite UI资源类型。
   * 自定义字段，有关详细信息，请参阅[自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的AEM Gems会话。
   * 从vtypes迁移到[Granite UI验证](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS监听器，有关详细信息，请参阅[处理字段事件](#handling-field-events)和[自定义对话框字段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)上的AEM Gems会话。

### 迁移cq：监听器代码{#migrating-cq-listener-code}

如果您迁移的项目是为经典UI设计的，则`cq:listener`代码（和与组件相关的clientlibs）可能使用特定于经典UI的函数（如`CQ.wcm.*`）。 对于迁移，必须使用触屏优化UI中的对等对象/函数更新此类代码。

如果您的项目正在完全迁移到触屏优化UI，您需要替换此类代码以使用与触屏优化UI相关的对象和功能。

但是，如果您的项目在迁移期间（通常情况）必须同时满足经典UI和触屏优化UI的需求，则您需要实现一个切换以区分引用相应对象的单独代码。

此切换机制可实现为：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 正在记录您的组件{#documenting-your-component}

作为开发人员，您需要轻松访问组件文档，以便快速了解：

* 描述
* 预期用途
* 内容结构和属性
* 暴露的API和扩展点
* 等等

因此，很容易将组件本身中可用的任何现有文档标记设置为可用。

您只需将`README.md`文件放入组件结构中。 此标记随后将显示在[组件控制台](/help/sites-authoring/default-components-console.md)中。

![chlimage_1-7](assets/chlimage_1-7.png)

支持的标记与[内容片段](/help/assets/content-fragments/content-fragments-markdown.md)的标记相同。
