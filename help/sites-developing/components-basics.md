---
title: AEM组件 — 基础知识
seo-title: AEM组件 — 基础知识
description: 开始开发新组件时，您需要了解其结构和配置的基础知识
seo-description: 开始开发新组件时，您需要了解其结构和配置的基础知识
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4974'
ht-degree: 1%

---

# AEM组件 — 基础知识{#aem-components-the-basics}

开始开发新组件时，您需要了解其结构和配置的基础知识。

此过程包括阅读理论并查看标准AEM实例中的各种组件实施。 虽然AEM已转为使用新的标准现代触屏UI，但它仍继续支持经典UI，这让后一种方法略为复杂。

## 概述 {#overview}

本节介绍一些关键概念和问题，并介绍开发您自己的组件时所需的详细信息。

### 规划 {#planning}

在开始实际配置或编码组件之前，您应该先询问：

* 您到底需要新组件执行哪些操作？
   * 明确的规格有助于在开发、测试和移交的所有阶段。 详细信息可能会随着时间的推移而发生更改，但规范可以更新（尽管更改也应记录在案）。
* 您是需要从头开始创建组件，还是可以从现有组件继承基础知识？
   * 没有必要再次发明轮子。
   * AEM提供了多种机制，允许您继承和扩展其他组件定义的详细信息，包括覆盖、覆盖和[Sling Resource Mober](/help/sites-developing/sling-resource-merger.md)。
* 您的组件是否需要逻辑才能选择/操作内容？
   * 逻辑应与用户界面层分开。 HTL旨在帮助确保实现此目的。
* 您的组件是否需要CSS格式？
   * CSS格式应与组件定义分开。 定义命名HTML元素的约定，以便您能够通过外部CSS文件修改它们。
* 我应该考虑哪些安全方面？
   * 有关更多详细信息，请参阅[安全检查表 — 开发最佳实践](/help/sites-administering/security-checklist.md#development-best-practices)。

### 触屏优化与经典UI {#touch-enabled-vs-classic-ui}

在开始任何有关开发组件的严肃讨论之前，您需要知道作者将使用的UI:

* **触屏优化 UI**
   [标准用户](/help/sites-developing/touch-ui-concepts.md) 界面基于Adobe Marketing Cloud的统一用户体验，采用Coral UI和Granite UI [的](/help/sites-developing/touch-ui-concepts.md#coral-ui) 底层 [技术](/help/sites-developing/touch-ui-concepts.md#granite-ui)。
* **基**
于AEM 6.4中已弃用的ExtJS技术的经典UIUser界面。

有关更多详细信息，请参阅[面向客户的UI界面Recommendations](/help/sites-deploying/ui-recommendations.md)。

可以实施组件以支持触屏优化UI和经典UI，也可以同时支持这两种方式。 在查看标准实例时，您还会看到最初为经典UI或触屏UI设计的现成组件，或者两者都设计的组件。

因此，我们将在此页面中介绍这两个工具的基础知识以及如何识别它们。

>[!NOTE]
>
>Adobe建议利用触屏优化UI从最新技术中受益。 [AEM现代化工](modernization-tools.md) 具扫描可简化迁移过程。

### 内容逻辑和渲染标记{#content-logic-and-rendering-markup}

建议将负责标记和渲染的代码与用于控制组件内容选择逻辑的代码分开。

[HTL](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)支持此理念，它是一种模板语言，经过刻意限制，可确保使用真正的编程语言来定义底层业务逻辑。 可通过特定命令从HTL调用此（可选）逻辑。 此机制会突出显示为给定视图调用的代码，并在必要时，允许对同一组件的不同视图使用特定逻辑。

### HTL与JSP {#htl-vs-jsp}

HTL是AEM 6.0中引入的一种HTML模板语言。

在开发您自己的组件时，有关是使用[HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)还是JSP(Java Server Pages)的讨论应该很简单，因为HTL现在是AEM的推荐脚本语言。

HTL和JSP都可用于为经典用户界面和触屏优化用户界面开发组件。 虽然可能会倾向于认为HTL仅适用于触屏UI，而JSP则适用于经典UI，但这是一种误解，而且更多是由于时间原因。 触屏优化UI和HTL大约在同一时段合并到AEM中。 由于HTL现在是推荐的语言，因此它正用于新组件，这些组件通常用于触屏UI。

>[!NOTE]
>
>Granite UI Foundation表单字段（在对话框中使用）除外。 这些仍然需要使用JSP。

### 开发您自己的组件{#developing-your-own-components}

要为相应的UI创建您自己的组件，请参阅（阅读此页面后）：

* [AEM触屏UI组件](/help/sites-developing/developing-components.md)
* [AEM Classic UI的组件](/help/sites-developing/developing-components-classic.md)

快速入门的方法是复制现有组件，然后进行所需的更改。 要了解如何创建您自己的组件并将其添加到段落系统，请参阅：

* [开发组件](/help/sites-developing/developing-components-samples.md) （重点介绍触屏优化UI）

### 将组件移动到发布实例{#moving-components-to-the-publish-instance}

呈现内容的组件必须部署在与内容相同的AEM实例上。 因此，必须在发布实例上部署用于创作和渲染创作实例上页面的所有组件。 部署后，组件可用于呈现已激活的页面。

使用以下工具将组件移动到发布实例：

* [使用包](/help/sites-administering/package-manager.md) 管理器将您的组件添加到包中，然后将其移动到另一个AEM实例。
* [使用激活树复制工](/help/sites-authoring/publishing-pages.md#manage-publication) 具复制组件。

>[!NOTE]
>
>这些机制还可用于在其他实例（例如，从开发到测试实例）之间传输组件。

### 从{#components-to-be-aware-of-from-the-start}开始注意的组件

* 页面:

   * AEM具有&#x200B;*page*&#x200B;组件(`cq:Page`)。
   * 这是一种对内容管理非常重要的特定类型的资源。
      * 页面对应于包含网站内容的网页。

* 段落制度：

   * 段落系统是网站的关键部分，因为它管理着段落列表。 它用于保存和构建保存实际内容的各个组件。
   * 您可以在段落系统中创建、移动、复制和删除段落。
   * 您还可以选择可在特定段落系统中使用的组件。
   * 标准实例中有各种可用的段落系统（例如`parsys`、` [responsivegrid](/help/sites-authoring/responsive-layout.md)`）。

## 结构 {#structure}

AEM组件的结构强大而灵活，主要考虑事项包括：

* 资源类型
* 组件定义
* 组件的属性和子节点
* 对话框
* 设计对话框
* 组件可用性
* 组件及其创建的内容

### 资源类型 {#resource-type}

结构的一个关键元素是资源类型。

* 内容结构声明意图。
* 资源类型实施它们。

这是一个抽象，有助于确保即使外观随时间而改变，意图也会保持不变。

### 组件定义{#component-definition}

#### 组件基础知识{#component-basics}

组件的定义可按如下方式划分：

* AEM组件基于[Sling](https://sling.apache.org/documentation.html)。
* AEM组件（通常位于以下位置）：

   * HTL: `/libs/wcm/foundation/components`
   * JSP:`/libs/foundation/components`

* 项目/站点特定组件（通常）位于以下位置：

   * `/apps/<myApp>/components`

* AEM标准组件定义为`cq:Component`，且具有关键元素：

   * jcr属性：

      jcr属性列表；这些是变量，虽然组件节点的基本结构、其属性和子节点由`cq:Component`定义定义，但有些是可选的

   * 资源:

      这些属性定义组件使用的静态元素。

   * 脚本:

   用于实现组件结果实例的行为。

* **根节点**:

   * `<mycomponent> (cq:Component)`  — 组件的层次结构节点。

* **重要属性**:

   * `jcr:title`  — 组件标题；例如，当组件在组件浏览器或Sidekick中列出时，会将该组件用作标签。
   * `jcr:description`  — 组件说明；可用作组件浏览器或Sidekick中的鼠标悬停提示。
   * 经典 UI：

      * `icon.png`  — 此组件的图标。
      * `thumbnail.png`  — 如果此组件在段落系统中列出，则显示图像。
   * 触屏 UI

      * 有关详细信息，请参阅触屏UI](/help/sites-developing/components-basics.md#component-icon-in-touch-ui)中的[组件图标部分。


* **重要子节点**:

   * `cq:editConfig (cq:EditConfig)`  — 定义组件的编辑属性，并允许组件显示在组件浏览器或Sidekick中。

      注意：如果组件具有对话框，则它将自动显示在组件浏览器或Sidekick中，即使cq:editConfig不存在也是如此。

   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定义其自身的子组件的创作UI方 `cq:editConfig`面。
   * 触屏优化 UI:

      * `cq:dialog` () `nt:unstructured` — 此组件的对话框。定义允许用户配置组件和/或编辑内容的界面。
      * `cq:design_dialog` ( `nt:unstructured`) — 编辑此组件的设计
   * 经典 UI：

      * `dialog` () `cq:Dialog` — 此组件的对话框。定义允许用户配置组件和/或编辑内容的界面。
      * `design_dialog` ( `cq:Dialog`) — 编辑此组件的设计。


#### 触屏UI中的组件图标{#component-icon-in-touch-ui}

组件的图标或缩写是在开发人员创建组件时，通过组件的JCR属性来定义的。 这些属性将按以下顺序计算，并使用找到的第一个有效属性。

1. `cq:icon`  — 字符串属性，指向要在组件浏览器中 [显示](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 的Coral UI库中的标准图标
   * 使用Coral图标的HTML属性值。
1. `abbreviation`  — 用于自定义组件浏览器中组件名称的缩写的字符串属性
   * 缩写应限制为两个字符。
   * 如果提供空字符串，则将从`jcr:title`属性的前两个字符生成缩写。
      * 例如，“Image”的“Im”
      * 将使用本地化的标题来构建缩写。
   * 仅当组件具有`abbreviation_commentI18n`属性时，缩写才会被翻译，该属性随后会用作翻译提示。
1. `cq:icon.png` 或 —  `cq:icon.svg` 此组件的图标，该图标显示在组件浏览器中
   * 20 x 20像素是标准组件的图标大小。
      * 大图标的大小将会缩小（客户端）。
   * 推荐颜色为rgb(112, 112, 112)> #707070
   * 标准组件图标的背景是透明的。
   * 仅支持`.png`和`.svg`文件。
   * 如果通过Eclipse插件从文件系统导入，则文件名需要转义为`_cq_icon.png`或`_cq_icon.svg`。
   * `.png` 如果两者都 `.svg` 存在，就会先例

如果在组件上找不到以上属性（`cq:icon`、`abbreviation`、`cq:icon.png`或`cq:icon.svg`）：

* 系统将在超级组件上搜索与`sling:resourceSuperType`属性后面的相同属性。
* 如果在超级组件级别中未找到任何缩写或空缩写，则系统将从当前组件`jcr:title`属性的前几个字母构建缩写。

要取消超级组件中图标的继承，在组件上设置空`abbreviation`属性将还原为默认行为。

[组件控制台](/help/sites-authoring/default-components-console.md#component-details)显示特定组件图标的定义方式。

#### SVG图标示例{#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### 组件{#properties-and-child-nodes-of-a-component}的属性和子节点

定义组件所需的许多节点/属性对于两个UI都是通用的，其中差异仍保持独立，因此您的组件可以在这两个环境中工作。

组件是`cq:Component`类型的节点，具有以下属性和子节点：

<table>
 <tbody>
  <tr>
   <td><strong>名称 <br /> </strong></td>
   <td><strong>类型 <br /> </strong></td>
   <td><strong>描述 <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td><code>cq:Component</code></td>
   <td>当前组件. 组件的节点类型为<code>cq:Component</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>可在组件浏览器（触屏优化UI）或Sidekick（经典UI）中选择组件的组。<br /> 值用于 <code>.hidden</code> 无法从UI中进行选择的组件，例如实际段落系统。</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>指示组件是否是容器组件，因此可以包含其他组件，如段落系统。</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>触屏UI的编辑对话框的定义。</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>经典UI的编辑对话框的定义。</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>触屏UI的设计对话框的定义。</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>经典UI的设计对话框的定义。<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>用于在组件没有对话框节点时覆盖该情况的对话框路径。<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>如果已设置，则此属性将被用作单元格ID。 有关更多信息，请参阅知识库文章<a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">如何构建设计单元格ID</a>。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>当组件是容器（例如段落系统）时，这将驱动子节点的编辑配置。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">编辑组件的配置</a>。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>返回添加到周围html标记的其他标记属性。 允许向自动生成的div中添加属性。</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>如果为true，则组件不会呈现为自动生成的div和css类。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>如果找到，则当从组件浏览器或Sidekick添加组件时，此节点将用作内容模板。</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>从组件浏览器或Sidekick添加组件时，要用作内容模板的节点的路径。 此路径必须是绝对路径，而不是相对于组件节点。<br /> 除非您希望重复使用其他位置已有的内容，否则不需要这样做，因 <code>cq:template</code> 此就足够了（请参阅下文）。</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>组件的创建日期。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>组件的描述。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>组件的标题。<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>设置后，组件会从此组件继承。<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>支持创建虚拟组件。 要查看示例，请访问以下联系人组件：<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code> </td>
   <td>脚本文件。<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>组件的图标，显示在Sidekick中的标题旁边。<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>将组件从Sidekick拖动到位时显示的可选缩略图。<br /> </td>
  </tr>
 </tbody>
</table>

如果查看&#x200B;**Text**&#x200B;组件（任一版本），我们可以看到以下元素：

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP(`/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

特定权益的物业包括：

* `jcr:title`  — 组件标题；此组件可用于标识组件，例如，它显示在组件浏览器或Sidekick的组件列表中
* `jcr:description`  — 组件说明；可用作Sidekick中组件列表中的鼠标悬停提示
* `sling:resourceSuperType`:这表示扩展组件（通过覆盖定义）时的继承路径

特定感兴趣的子节点包括：

* `cq:editConfig` ( `cq:EditConfig`) — 此控件可控制视觉方面；例如，它可以定义条形图或小组件的外观，也可以添加自定义控件
* `cq:childEditConfig` ( `cq:EditConfig`) — 此选项控制没有自己定义的子组件的可视化方面
* 触屏优化 UI:
   * `cq:dialog` ( `nt:unstructured`) — 定义用于编辑此组件内容的对话框
   * `cq:design_dialog` ( `nt:unstructured`) — 指定此组件的设计编辑选项
* 经典 UI：
   * `dialog` ( `cq:Dialog`) — 定义用于编辑此组件内容的对话框（特定于经典UI）
   * `design_dialog` ( `cq:Dialog`) — 指定此组件的设计编辑选项
   * `icon.png`  — 图形文件，用作Sidekick中组件的图标
   * `thumbnail.png`  — 图形文件，当从Sidekick拖动组件时用作组件的缩略图

### 对话框 {#dialogs}

对话框是组件的关键元素，因为它们为作者提供了一个界面，用于配置该组件并为其提供输入。

根据组件的复杂性，对话框可能需要一个或多个选项卡 — 用于缩短对话框并对输入字段进行排序。

对话框定义特定于UI:

>[!NOTE]
>
>* 出于兼容性目的，当未为触屏UI定义任何对话框时，触屏UI可以使用经典UI对话框的定义。
>* 还提供[AEM现代化工具](/help/sites-developing/modernization-tools.md)，以帮助您扩展/转换只为经典UI定义对话框的组件。

>



* 触屏优化 UI
   * `cq:dialog` ( `nt:unstructured`)节点：
      * 定义用于编辑此组件内容的对话框
      * 特定于触屏优化UI
      * 使用Granite UI组件进行定义
      * 具有属性`sling:resourceType`作为标准Sling内容结构
      * 可以具有属性`helpPath`来定义在“帮助”图标(? 图标)。
         * 对于现成的组件，通常会引用文档中的页面。
         * 如果未指定`helpPath`，则会显示默认URL（文档概述页面）。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   在对话框中，定义了各个字段：

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 经典 UI
   * `dialog` ( `cq:Dialog`)节点
      * 定义用于编辑此组件内容的对话框
      * 特定于经典UI
      * 使用ExtJS小组件定义
      * 具有属性`xtype`，该属性引用ExtJS
      * 可以具有属性`helpPath`来定义在选择&#x200B;**Help**&#x200B;按钮时访问的上下文相关帮助资源（绝对或相对路径）。
         * 对于现成的组件，通常会引用文档中的页面。
         * 如果未指定`helpPath`，则会显示默认URL（文档概述页面）。

   ![chlimage_1-243](assets/chlimage_1-243.png)

   在对话框中，定义了各个字段：

   ![chlimage_1-244](assets/chlimage_1-244.png)

   在经典对话框中：

   * 您可以创建`cq:Dialog`对话框，该对话框将提供单个选项卡 — 如在文本组件中一样，或者如果您需要多个选项卡，如在文本时间组件中那样，该对话框可定义为`cq:TabPanel`。
   * a `cq:WidgetCollection`(`items`)用于为输入字段(`cq:Widget`)或进一步的制表符(`cq:Widget`)提供基。 可以扩展此层次结构。


### 设计对话框{#design-dialogs}

设计对话框与用于编辑和配置内容的对话框非常相似，但它们为作者提供了用于配置和提供该组件设计详细信息的界面。

[设计对话框在设计模式下可用](/help/sites-authoring/default-components-designmode.md)，但并非所有组件（如标题和图像）都需要 **** 设计对话框，而文本则 ****  **** 不需要。

段落系统（例如parsys）的设计对话框是一个特殊情况，因为它允许用户在页面上选择特定的其他组件（从组件浏览器或Sidekick）。

### 将组件添加到段落系统{#adding-your-component-to-the-paragraph-system}

定义组件后，必须使其可供使用。 要使组件可在段落系统中使用，您可以执行以下任一操作：

1. 打开页面的[设计模式](/help/sites-authoring/default-components-designmode.md)并启用所需的组件。
1. 将所需的组件添加到模板定义的`components`属性中，如下所示：

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   例如，请参阅：

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 组件及其创建的内容{#components-and-the-content-they-create}

如果在页面上创建并配置&#x200B;**Title**&#x200B;组件的实例：`<content-path>/Prototype.html`

* 触屏优化 UI

   ![chlimage_1-246](assets/chlimage_1-246.png)

* 经典 UI

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

然后，我们可以看到在存储库中创建的内容的结构：

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

特别是，如果您查看&#x200B;**Title**&#x200B;的实际文本：

* 定义（适用于两个UI）的属性为`name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 在内容中，将生成包含作者内容的属性`jcr:title`。

定义的属性取决于各个定义。 尽管它们可能比上面更复杂，但它们仍遵循相同的基本原则。

## 组件层次结构和继承{#component-hierarchy-and-inheritance}

AEM中的组件受3个不同层次结构的约束：

* **资源类型层次结构**

   用于使用属性`sling:resourceSuperType`扩展组件。 这允许组件继承。 例如，文本组件将从标准组件继承各种属性。

   * 脚本（由Sling解析）
   * 对话框
   * 描述（包括缩略图图像、图标等）

* **容器层次结构**

   该变量用于向子组件填充配置设置，最常用于parsys方案。

   例如，可以在父组件上定义编辑栏按钮、控制集布局（编辑栏、滚动）、对话框布局（内联、浮动）的配置设置，并将其传播到子组件。

   将传播`cq:editConfig`和`cq:childEditConfig`中的配置设置（与编辑功能相关）。

* **包含层级**

   这是在运行时由包含序列强加的。

   此层次结构由设计人员使用，而设计人员又充当渲染各个设计方面的基础；包括布局信息、css信息、parsys中的可用组件等。

## 编辑行为{#edit-behavior}

本节介绍如何配置组件的编辑行为。 这包括一些属性，例如组件可用的操作、就地编辑器的特性以及与组件上的事件相关的侦听器。

触屏UI和经典UI都使用此配置，尽管这两种配置存在某些特定差异。

组件的编辑行为通过以下方法进行配置：在组件节点（`cq:Component`类型）下添加`cq:editConfig`类型的节点，并添加特定属性和子节点。 `cq:EditConfig`以下属性和子节点可用：

* [ `cq:editConfig` 节点属性](#configuring-with-cq-editconfig-properties):

   * `cq:actions` ( `String array`):定义可对组件执行的操作。
   * `cq:layout` ( `String`)::定义如何在经典UI中编辑组件。
   * `cq:dialogMode` ( `String`):定义在经典UI中打开组件对话框的方式

      * 在触屏优化UI中，对话框始终在桌面模式下浮动，并在移动设备中自动以全屏方式打开。
   * `cq:emptyText` ( `String`):定义不显示可视内容时显示的文本。
   * `cq:inherit` ( `Boolean`):定义是否从其继承的组件继承了缺少的值。
   * `dialogLayout` （字符串）：定义对话框的打开方式。


* [ `cq:editConfig` 子节点](#configuring-with-cq-editconfig-child-nodes):

   * `cq:dropTargets` (节点类 `nt:unstructured`型):定义可以接受内容查找器资产中删除的放置目标列表

      * 只有经典UI中提供了多个放置目标。
      * 在触屏优化UI中，允许使用单个放置目标。
   * `cq:actionConfigs` (节点类 `nt:unstructured`型):定义附加到cq:actions列表的新操作列表。
   * `cq:formParameters` (节点类 `nt:unstructured`型):定义添加到对话框表单的其他参数。
   * `cq:inplaceEditing` (节点类 `cq:InplaceEditingConfig`型):为组件定义就地编辑配置。
   * `cq:listeners` (节点类 `cq:EditListenersConfig`型):定义在组件上执行操作之前或之后发生的情况。


>[!NOTE]
>
>在此页中，节点（属性和子节点）表示为XML，如以下示例所示。

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"/>
</jcr:root>
```

存储库中存在许多现有配置。 您可以轻松搜索特定属性或子节点：

* 要查找`cq:editConfig`节点的属性，例如`cq:actions`，您可以使用&#x200B;**CRXDE Lite**&#x200B;中的“查询”工具，并使用以下XPath查询字符串进行搜索：

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 要查找`cq:editConfig`的子节点，例如，可以搜索`cq:dropTargets`，该节点类型为`cq:DropTargetConfig`;您可以在**CRXDE Lite**中使用查询工具，并使用以下XPath查询字符串进行搜索：

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### 组件占位符{#component-placeholders}

组件必须始终呈现一些对作者可见的HTML，即使组件没有内容也是如此。 否则，它可能会从编辑器的界面中以可视方式消失，从而使其在技术上呈现，但在页面和编辑器中却不可见。 在这种情况下，作者将无法选择空组件并与之进行交互。

因此，只要组件在页面编辑器中呈现页面时（当WCM模式为`edit`或`preview`时）不呈现任何可见输出，组件就应呈现占位符。
占位符的典型HTML标记如下所示：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

呈现上述占位符HTML的典型HTL脚本如下所示：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一个示例中，`isEmpty`是一个变量，仅当组件没有内容且作者不可见时，该变量才为true。

为避免重复，Adobe建议组件实施者为这些占位符使用HTL模板， [类似于核心组件提供的模板。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

然后，使用以下HTL行完成模板在上一个链接中的使用：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一个示例中，`model.text`是仅当内容包含且可见时才为true的变量。

此模板的用法示例可在核心组件[中查看，如标题组件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq:EditConfig属性{#configuring-with-cq-editconfig-properties}进行配置

### cq:actions {#cq-actions}

`cq:actions`属性(`String array`)定义可对组件执行的一个或多个操作。 以下值可用于配置：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>仅在经典UI中显示静态文本值&lt;some text&gt;<br />。 触屏优化UI在上下文菜单中不显示操作，因此不适用。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>添加间隔符。<br /> 仅在经典UI中可见。触屏优化UI在上下文菜单中不显示操作，因此不适用。</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>添加按钮以编辑组件。</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>添加按钮以编辑组件并允许<a href="/help/sites-authoring/annotations.md">注释</a>。</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>添加用于删除组件的按钮</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>添加按钮以在当前组件之前插入新组件</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>添加按钮以复制和剪切组件。</td>
  </tr>
 </tbody>
</table>

以下配置向组件编辑栏添加编辑按钮、分隔符、删除和插入按钮：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

以下配置将文本“从基本框架继承的配置”添加到组件编辑栏：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout（仅限经典UI）{#cq-layout-classic-ui-only}

`cq:layout`属性(`String`)定义如何在经典UI中编辑组件。 以下值可用：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>默认值。 组件版可通过单击和/或上下文菜单“鼠标悬停”访问。<br /> 要进行高级使用，请注意相应的客户端对象是： <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>组件版本可通过工具栏访问。<br /> 要进行高级使用，请注意相应的客户端对象是： <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>选项将留给客户端代码。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>滚动更新和编辑栏的概念在触屏UI中不适用。

以下配置会向组件编辑栏中添加编辑按钮：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode（仅经典UI）{#cq-dialogmode-classic-ui-only}

该组件可以链接到编辑对话框。 `cq:dialogMode`属性(`String`)定义在经典UI中打开组件对话框的方式。 以下值可用：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>对话框是浮动的。<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(默认值). 对话框将锚定在组件上。<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>如果组件宽度小于客户端<code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code>值，则对话框将处于浮动状态，否则将处于内联状态。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在触屏UI中，对话框始终在桌面模式下浮动，并在移动设备中自动以全屏方式打开。

以下配置定义了一个带有编辑按钮的编辑栏和一个浮动对话框：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:emptyText {#cq-emptytext}

`cq:emptyText`属性(`String`)定义在没有可视内容时显示的文本。 默认为：`Drag components or assets here`。

### cq:inherit {#cq-inherit}

`cq:inherit`属性(`boolean`)定义是否从继承的组件继承了缺少的值。 默认为`false`。

### dialogLayout {#dialoglayout}

默认情况下， `dialogLayout`属性定义应如何打开对话框。

* 值`fullscreen`将全屏打开对话框。
* 属性的空值或缺失值默认为正常打开对话框。
* 请注意，用户始终可以在对话框中切换全屏模式。
* 不适用于经典UI。

### 使用cq:EditConfig子节点{#configuring-with-cq-editconfig-child-nodes}进行配置

### cq:dropTargets {#cq-droptargets}

`cq:dropTargets`节点（节点类型`nt:unstructured`）定义了一个放置目标列表，这些放置目标可以接受从内容查找器中拖动的资产中的放置。 它用作`cq:DropTargetConfig`类型节点的集合。

>[!NOTE]
>
>只有经典UI中提供了多个放置目标。
>
>在触屏优化UI中，仅使用第一个目标。

类型`cq:DropTargetConfig`的每个子节点都定义组件中的放置目标。 节点名称很重要，因为必须在JSP中使用它，如下所示，来生成分配给DOM元素的CSS类名称，该元素是有效的放置目标：

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

`<drag and drop prefix>`由Java属性定义：

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`。

例如，类名称在下载组件的JSP中定义如下
(`/libs/foundation/components/download/download.jsp`)，其中`file`是下载组件编辑配置中放置目标的节点名称：

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

类型`cq:DropTargetConfig`的节点需要具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>将正则表达式应用于资产mime类型以验证是否允许删除。</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>放置目标组的数组。 每个组必须匹配内容查找器扩展中定义并附加到资产的组类型。</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>在有效删除后将更新的属性的名称。</td>
  </tr>
 </tbody>
</table>

下载组件中提供了以下配置。 它允许将`media`组中的任何资产（mime类型可以是任何字符串）从内容查找器拖放到组件中。 放置后，将更新组件属性`fileReference`:

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs（仅限经典UI）{#cq-actionconfigs-classic-ui-only}

`cq:actionConfigs`节点（节点类型`nt:unstructured`）定义一个新操作列表，这些新操作将附加到由`cq:actions`属性定义的列表中。 `cq:actionConfigs`的每个子节点都通过定义小组件来定义新操作。

以下配置示例定义了一个新按钮（带有经典UI的分隔符）：

* 由xtype `tbseparator`定义的分隔符；

   * 该设置仅用于经典UI。
   * 触屏UI会忽略此定义，因为xtype会被忽略（由于触屏UI中操作工具栏的构造方式不同，因此无需使用分隔符）。

* 名为&#x200B;**管理注释**&#x200B;的按钮，运行处理程序函数`CQ_collab_forum_openCollabAdmin()`。

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:actions="[EDIT,COPYMOVE,DELETE,INSERT]"
    jcr:primaryType="cq:EditConfig">
    <cq:actionConfigs jcr:primaryType="nt:unstructured">
        <separator0
            jcr:primaryType="nt:unstructured"
            xtype="tbseparator"/>
        <manage
            jcr:primaryType="nt:unstructured"
            handler="function(){CQ_collab_forum_openCollabAdmin();}"
            text="Manage comments"/>
    </cq:actionConfigs>
</jcr:root>
```

>[!NOTE]
>
>请参阅[向组件工具栏添加新操作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar)作为触屏UI的示例。

### cq:formParameters {#cq-formparameters}

`cq:formParameters`节点（节点类型`nt:unstructured`）定义了添加到对话框表单的其他参数。 每个属性都会映射到一个表单参数。

以下配置将名为`name`的参数（使用值`photos/primary`设置）添加到对话框表单中：

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

`cq:inplaceEditing`节点（节点类型`cq:InplaceEditingConfig`）定义组件的就地编辑配置。 它可以具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>)True可启用组件的就地编辑。</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>)编辑器配置的路径。 配置节点可以指定。</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>)编辑器类型。 可用类型包括：</p>
    <ul>
     <li>纯文本：用于非HTML内容。<br /> </li>
     <li>标题：是一个增强的纯文本编辑器，在开始编辑之前，可将图形标题转换为纯文本。 由Geometrixx标题组件使用。<br /> </li>
     <li>文本：用于HTML内容（使用富文本编辑器）。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

以下配置允许就地编辑组件，并将`plaintext`定义为编辑器类型：

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq:listeners {#cq-listeners}

`cq:listeners`节点（节点类型`cq:EditListenersConfig`）定义在对组件执行操作之前或之后所发生的情况。 下表定义了其可能的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
   <td><p><strong>默认值</strong></p> <p>（仅限经典UI）</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>处理程序在删除组件之前触发。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>处理程序在编辑组件之前触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>在复制组件之前触发处理程序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>在移动组件之前触发处理程序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>在插入组件之前触发处理程序。<br /> 仅适用于触屏优化UI。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>在将组件插入其他组件（仅限容器）之前，会触发处理程序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>处理程序在删除组件后触发。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>编辑组件后会触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>处理程序在复制组件后触发。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>在插入组件后触发处理程序。</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>处理程序在组件移动后触发。</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>将组件插入另一个组件（仅限容器）后，将触发处理程序。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>`REFRESH_INSERTED`和`REFRESH_SELFMOVED`处理程序仅在经典UI中可用。

>[!NOTE]
>
>监听器的默认值仅在经典UI中设置。

>[!NOTE]
>
>对于嵌套的组件，对于定义为`cq:listeners`节点上属性的操作有一些限制：
>
>* 对于嵌套的组件，以下属性&#x200B;*的值必须*&#x200B;为`REFRESH_PAGE`:>
>  * `aftermove`
>  * `aftercopy`


事件处理程序可以通过自定义实施来实施。 例如（其中`project.customerAction`是静态方法）：

`afteredit = "project.customerAction"`

以下示例等效于`REFRESH_INSERTED`配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>对于经典UI，要查看可以在处理程序中使用的参数，请参阅[ `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)和[ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)小组件文档的`before<action>`和`after<action>`事件部分。

通过以下配置，在删除、编辑、插入或移动组件后会刷新页面：

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
