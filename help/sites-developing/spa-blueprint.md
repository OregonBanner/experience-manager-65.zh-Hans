---
title: SPA Blueprint
seo-title: SPA Blueprint
description: 本文档介绍任何SPA框架在AEM中实施可编辑的SPA组件时应履行的与框架无关的一般合同。
seo-description: 本文档介绍任何SPA框架在AEM中实施可编辑的SPA组件时应履行的与框架无关的一般合同。
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# SPA Blueprint{#spa-blueprint}

要使作者能够使用AEM SPA编辑器来编辑SPA的内容，SPA必须满足一些要求，这些要求在本文档中有所描述。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染(例如，React或Angular)的项目，推荐使用SPA编辑器解决方案。

## 简介 {#introduction}

本文档介绍了任何SPA框架为在AEM中实施可编辑的SPA组件而应履行的一般合同(即AEM支持层的类型)。

>[!NOTE]
>
>以下要求与框架无关。 如果满足这些要求，则可以提供由模块、组件和服务组成的框架特定层。
>
>**AEM中的React和Angular框架已满足这些要求。** 仅当您希望实施其他框架以与AEM一起使用时，此Blueprint中的要求才相关。

>[!CAUTION]
>
>尽管AEM的SPA功能与框架无关，但当前仅支持React和Angular框架。

要使作者能够使用AEM页面编辑器来编辑由单页应用程序框架公开的数据，项目必须能够解释表示为AEM存储库内的应用程序存储的数据的语义的模型结构。 为实现此目标，提供了两个与框架无关的库：`PageModelManager`和`ComponentMapping`。

### PageModelManager {#pagemodelmanager}

`PageModelManager`库作为NPM包提供，供SPA项目使用。 它与SPA一起提供，用作数据模型管理器。

它代表SPA抽象了表示实际内容结构的JSON结构的检索和管理。 它还负责与SPA同步，以告知其何时必须重新渲染其组件。

请参阅NPM包[@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

初始化`PageModelManager`时，库首先加载提供的应用程序根模型（通过参数、元属性或当前URL）。 如果库确定当前页面的模型不是其获取的根模型的一部分，则会将其作为子页面的模型包含在内。

![page_model_consolidation](assets/page_model_consolidation.png)

### 组件映射 {#componentmapping}

`ComponentMapping`模块作为NPM包提供到前端项目。 它存储前端组件，并为SPA提供了一种将前端组件映射到AEM资源类型的方法。 这样，在解析应用程序的JSON模型时，就可以动态解析组件。

模型中存在的每个项目都包含一个公开AEM资源类型的`:type`字段。 装载后，前端组件可以使用从基础库收到的模型片段呈现自身。

#### 将动态模型映射到组件{#dynamic-model-to-component-mapping}

有关在AEM的Javascript SPA SDK中如何进行动态模型到组件映射的详细信息，请参阅文章[Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定层{#framework-specific-layer}

每个前端框架必须实现第三层。 第三个库负责与基础库交互，并提供一系列集成良好且易于使用的入口点，以便与数据模型交互。

本文件的其余部分描述了这一中间框架特定层的要求，并希望与框架无关。 通过遵循以下要求，可以为项目组件提供一个特定于框架的层，以便与负责管理数据模型的底层库进行交互。

## 一般概念{#general-concepts}

### 页面模型{#page-model}

页面的内容结构存储在AEM中。 页面模型用于映射和实例化SPA组件。 SPA开发人员会创建SPA组件，并将其映射到AEM组件。 为此，他们使用资源类型(或AEM组件的路径)作为唯一键。

SPA组件必须与页面模型同步，并相应地更新以更改其内容。 必须使用利用动态组件的模式来按照提供的页面模型结构即时实例化组件。

### 元字段{#meta-fields}

页面模型可利用JSON模型导出器，该导出器本身基于[Sling Model](https://sling.apache.org/documentation/bundles/models.html) API。 可导出的Sling模型会公开以下字段列表，以便启用基础库来解释数据模型：

* `:type`:AEM资源的类型（默认=资源类型）
* `:children`:当前资源的分层子级。子项不是当前资源内部内容的一部分（可以在表示页面的项目上找到）
* `:hierarchyType`:资源的分层类型。`PageModelManager`当前支持页面类型

* `:items`:当前资源的子内容资源（嵌套结构，仅存在于容器中）
* `:itemsOrder`:订了孩子的名单。JSON映射对象不保证其字段的顺序。 通过让映射和当前数组成为API的使用者，这两种结构都具有好处
* `:path`:项目的内容路径（在表示页面的项目上存在）

另请参阅[AEM Content Services快速入门。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 特定于框架的模块{#framework-specific-module}

分散关注有助于促进项目实施。 因此，应提供特定于npm的包。 此资源包负责聚合和公开基本模块、服务和组件。 这些组件必须封装数据模型管理逻辑，并提供对项目组件所期望数据的访问。 该模块还负责传递性地公开基础库的有用入口点。

为了促进库的互操作性，Adobe建议特定于框架的模块捆绑以下库。 如有必要，层可以在将底层API公开到项目之前，对它们进行封装和调整。

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### 实施 {#implementations}

#### React {#react}

npm模块：[@adobe-aem-react-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

npm模块：即将推出

## 主要服务和组件{#main-services-and-components}

应按照每个框架的具体准则执行以下实体。 基于框架架构，实现方式可能差异很大，但必须提供描述的功能。

### 模型提供程序{#the-model-provider}

项目组件必须将模型片段的访问权限委派给模型提供程序。 然后，模型提供程序负责侦听对模型的指定片段所做的更改，并将更新的模型返回到委派组件。

为此，模型提供程序必须注册到` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`。 然后，当发生更改时，它会接收更新的数据并将其传递到委派组件。 按照惯例，用于将包含模型片段的委派组件的属性名为`cqModel`。 该实施可以免费向组件提供此属性，但应当考虑一些方面，例如与框架架构的集成、可发现性和易用性。

### 组件HTML解码器{#the-component-html-decorator}

组件修饰器负责使用页面编辑器预期的一系列数据属性和类名称来修饰每个组件实例的元素的外部HTML。

#### 组件声明{#component-declaration}

以下元数据必须添加到由项目组件生成的外部HTML元素中。 它们允许页面编辑器检索相应的编辑配置。

* `data-cq-data-path`:资源相对于  `jcr:content`

#### 编辑功能声明和占位符{#editing-capability-declaration-and-placeholder}

以下元数据和类名称必须添加到项目组件生成的外部HTML元素中。 它们允许页面编辑器提供相关功能。

* `cq-placeholder`:用于标识空组件占位符的类名称
* `data-emptytext`:组件实例为空时由叠加图显示的标签

**空组件占位符**

每个组件都必须扩展一个功能，该功能将在组件被标识为空时，使用特定于占位符和相关叠加的数据属性和类名称来装饰外部HTML元素。

**论构件的空虚性**

* 组件在逻辑上为空吗？
* 组件为空时，叠加图应显示什么标签？

### 容器 {#container}

容器是用于包含和渲染子组件的组件。 为此，容器会遍历其模型的`:itemsOrder`、`:items`和`:children`属性。

容器会从` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)`库的存储中动态获取子组件。 然后，容器使用模型提供程序功能扩展子组件，并最终将其实例化。

### 页面 {#page}

`Page`组件扩展`Container`组件。 容器是用于包含和渲染子组件（包括子页面）的组件。 为此，容器会遍历其模型的`:itemsOrder`、`:items`和`:children`属性。 `Page`组件从[ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)库的存储中动态获取子组件。 `Page`负责实例化子组件。

### 响应式网格 {#responsive-grid}

响应式网格组件是一个容器。 它包含表示其列的模型提供程序的特定变体。 响应式网格及其列负责使用模型中包含的特定类名称来装饰项目组件的外部HTML元素。

响应式网格组件应预映射到其AEM对应组件，因为该组件非常复杂，且很少进行自定义。

#### 特定模型字段{#specific-model-fields}

* `gridClassNames:` 为响应式网格提供的类名称
* `columnClassNames:` 为响应列提供的类名称

另请参阅npm资源[@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### 响应式网格{#placeholder-of-the-reponsive-grid}的占位符

SPA组件会映射到图形容器（如响应式网格），并且在创作内容时必须添加虚拟子占位符。 当页面编辑器创作SPA内容时，该内容会使用iframe嵌入到编辑器中，并且`data-cq-editor`属性会添加到该内容的文档节点。 当存在`data-cq-editor`属性时，容器必须包含HTMLElement，以表示作者在将新组件插入页面时与之交互的区域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>页面编辑器当前需要示例中使用的类名称。
>
>* `"new section"`:指示当前元素是容器的占位符
>* `"aem-Grid-newComponent"`:将组件标准化以用于布局创作

>



#### 组件映射{#component-mapping}

基础[`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping)库及其`MapTo`函数可以封装和扩展，以提供与当前组件类旁边提供的编辑配置相关的功能。

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

在上述实施中，项目组件在实际注册到[组件映射](/help/sites-developing/spa-blueprint.md#componentmapping)存储中之前，会使用空白功能进行扩展。 这是通过封装和扩展[`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping)库来引入`EditConfig`配置对象的支持来完成的：

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 与页面编辑器{#contract-with-the-page-editor}合同

项目组件必须至少生成以下数据属性，以便编辑器能够与它们交互。

* `data-cq-data-path`:组件的相对路径( `PageModel` 例如 `"root/responsivegrid/image"`)。不应将此属性添加到页面。

总之，要让页面编辑器将其解释为可编辑，项目组件必须遵守以下合同：

* 提供将前端组件实例关联到AEM资源的预期属性。
* 提供可创建空占位符的一系列预期属性和类名称。
* 提供可执行资产拖放的预期类名称。

### 典型HTML元素结构{#typical-html-element-structure}

以下片段说明了页面内容结构的典型HTML表示形式。 以下是几个重要要点：

* 响应式网格元素带有前缀为`aem-Grid--`的类名
* 响应列元素带有前缀为`aem-GridColumn--`的类名称
* 将封装响应式网格（也是父网格的列），如前两个前缀不出现在同一元素上
* 与可编辑资源对应的元素具有`data-cq-data-path`属性。 请参阅本文档的[与页面编辑器](#contract-wtih-the-page-editor)合同部分。

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 导航和路由{#navigation-and-routing}

应用程序拥有路由。 前端开发人员首先需要实施导航组件(映射到AEM导航组件)。 此组件将呈现要与一系列路由一起使用的URL链接，这些路由将显示或隐藏内容片段。

基础[ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)库及其` [ModelRouter](/help/sites-developing/spa-routing.md)`模块（默认启用）负责预取和提供对与给定资源路径关联的模型的访问权限。

两个实体与路由概念相关，但` [ModelRouter](/help/sites-developing/spa-routing.md)`仅负责使` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`加载与当前应用程序状态同步的数据模型。

有关更多信息，请参阅文章[SPA Model Routing](/help/sites-developing/spa-routing.md)。

## SPA操作{#spa-in-action}

请继续阅读文档[AEM](/help/sites-developing/spa-getting-started-react.md)中的SPA快速入门，以了解简单的SPA如何工作并亲自体验SPA。

## 进一步阅读{#further-reading}

有关AEM中SPA的更多信息，请参阅以下文档：

* [SPA创](/help/sites-developing/spa-overview.md) 作概述，了解AEM中的SPA和通信模型的概述
* [SPA AEM入门，](/help/sites-developing/spa-getting-started-react.md) 以了解简单SPA及其工作原理的指南
