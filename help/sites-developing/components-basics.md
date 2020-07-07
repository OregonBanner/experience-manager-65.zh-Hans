---
title: AEM组件——基础知识
seo-title: AEM组件——基础知识
description: 开始开发新组件时，您需要了解其结构和配置的基础知识
seo-description: 开始开发新组件时，您需要了解其结构和配置的基础知识
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '4719'
ht-degree: 1%

---


# AEM组件——基础知识{#aem-components-the-basics}

开始开发新组件时，您需要了解其结构和配置的基础知识。

此过程涉及阅读理论并查看标准AEM实例中的各种组件实现。 虽然AEM已转向新的标准、新式、触屏优化UI，但它仍支持经典UI，因此后一种方法略为复杂。

## 概述 {#overview}

本部分介绍开发您自己的组件时所需的详细信息，包括主要概念和问题。

### 规划 {#planning}

在开始实际配置或编码组件之前，您应该询问：

* 您到底需要新组件做什么？
   * 清晰的规范有助于在开发、测试和移交的所有阶段。 详细信息可能随时间而更改，但规范可以更新（尽管更改也应记录在案）。
* 您是需要从头开始创建组件，还是可以从现有组件继承基础知识？
   * 没有必要再费力去发挥。
   * AEM提供了多种机制，允许您继承和扩展其他组件定义的详细信息，包括覆盖、叠加和 [Sling资源合并](/help/sites-developing/sling-resource-merger.md)。
* 您的组件是否需要逻辑才能选择／操作内容？
   * 逻辑应与用户界面层保持分离。 HTL旨在帮助确保这种情况发生。
* 您的组件是否需要CSS格式？
   * CSS格式应与组件定义分开。 定义命名HTML元素的约定，以便通过外部CSS文件修改它们。
* 我应该考虑哪些安全方面？
   * 有关更 [多详细信息，请参阅安全核对清单](/help/sites-administering/security-checklist.md#development-best-practices) -开发最佳实践。

### 触屏优化与经典UI {#touch-enabled-vs-classic-ui}

在进行任何有关开发组件的严肃讨论开始之前，您需要了解您的作者将使用的UI:

* **触屏优化 UI**
   [标准用户界面](/help/sites-developing/touch-ui-concepts.md) 基于Adobe Marketing Cloud的统一用户体验，使用Coral UI和Granite UI的 [底层技](/help/sites-developing/touch-ui-concepts.md#coral-ui) 术进 [行设计](/help/sites-developing/touch-ui-concepts.md#granite-ui)。
* **经典UI**&#x200B;基于AEM 6.4中已弃用的ExtJS技术的用户界面。

有关更 [多详细信息，请参阅](/help/sites-deploying/ui-recommendations.md) “客户的UI界面推荐”。

可以实施组件以支持触屏优化UI、经典UI或两者。 在查看标准实例时，您还会看到最初为经典UI或触屏优化UI设计的现成组件，或者两者兼有。

因此，本页将介绍两者的基础知识，以及如何识别它们。

>[!NOTE]
>
>Adobe建议利用触屏优化UI从最新技术中受益。 [AEM Modernination Tools&amp;(moderniatzion-tools.md)可让迁移更轻松。

### 内容逻辑和渲染标记  {#content-logic-and-rendering-markup}

建议将标记和渲染的代码与控制用于选择组件内容的逻辑的代码分开，以使代码负责。

HTL支持这一理 [念](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html),HTL是一种模板语言，故意限制该语言，以确保使用真正的编程语言来定义基础业务逻辑。 此（可选）逻辑从HTL中使用特定命令调用。 此机制会高亮显示为给定视图调用的代码，并根据需要允许同一组件的不同视图使用特定逻辑。

### HTL与JSP {#htl-vs-jsp}

HTL是AEM 6.0引入的一种HTML模板语言。

在开发您自己的组 [件时](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) ，有关是使用HTL还是JSP（Java服务器页面）的讨论应该很简单，因为HTL现在是AEM的推荐脚本语言。

HTL和JSP都可用于为经典和触屏优化UI开发组件。 尽管有一种倾向认为HTL仅适用于经典UI的触屏优化UI和JSP，但这是一种误解，而且更多是由于时间原因。 触屏优化UI和HTL大约在同一时间段内并入AEM。 由于现在推荐使用HTL语言，因此它用于新组件，这些组件通常用于触屏优化UI。

>[!NOTE]
>
>除Granite UI Foundation表单字段外（在对话框中使用）。 这些仍需要使用JSP。

### 开发您自己的组件 {#developing-your-own-components}

要为相应的UI创建您自己的组件，请参阅（阅读此页面后）:

* [触屏优化UI的AEM组件](/help/sites-developing/developing-components.md)
* [经典UI的AEM组件](/help/sites-developing/developing-components-classic.md)

快速入门的方法是复制现有组件，然后进行所需的更改。 要了解如何创建您自己的组件并将其添加到段落系统，请参阅：

* [开发组件](/help/sites-developing/developing-components-samples.md) （侧重于触屏优化UI）

### 将组件移到Publish实例 {#moving-components-to-the-publish-instance}

呈现内容的组件必须部署在与内容相同的AEM实例上。 因此，必须在发布实例上部署用于创作和呈现页面的所有组件。 部署后，组件可用于呈现已激活的页面。

使用以下工具将组件移至发布实例：

* [使用包管理器](/help/sites-administering/package-manager.md) ，将您的组件添加到包中，并将它们移至另一个AEM实例。
* [使用激活树复制工具](/help/sites-authoring/publishing-pages.md#manage-publication) ，复制组件。

>[!NOTE]
>
>这些机制还可用于在其他实例之间传输组件，例如从开发到测试实例。

### 要从开始中识别的组件 {#components-to-be-aware-of-from-the-start}

* 页面:

   * AEM具有 *页面* 组件( `cq:Page`)。
   * 这是对内容管理很重要的特定类型的资源。
      * 页面与包含网站内容的网页相对应。

* 段落系统：

   * 段落系统是网站的关键部分，因为它管理一列表段落。 它用于保存和构建保存实际内容的各个组件。
   * 您可以在段落系统中创建、移动、复制和删除段落。
   * 您还可以选择可在特定段落系统中使用的组件。
   * 标准实例中有各种可用的段落系统( `parsys`例如 ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`,)。

## 结构 {#structure}

AEM组件的结构强大而灵活，主要考虑事项有：

* 资源类型
* 组件定义
* 组件的属性和子节点
* 对话框
* 设计对话框
* 组件可用性
* 组件及其创建的内容

### 资源类型 {#resource-type}

结构的关键元素是资源类型。

* 内容结构声明意图。
* 资源类型实现它们。

这是一个抽象，有助于确保即使外观和感觉随着时间而改变，意图也会保持时间。

### 组件定义 {#component-definition}

#### 组件基础知识 {#component-basics}

组件的定义可以按如下方式进行划分：

* AEM组件基于 [Sling](https://sling.apache.org/documentation.html)。
* AEM组件（通常）位于：

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* 项目／站点特定组件（通常）位于：

   * `/apps/<myApp>/components`

* AEM标准组件定义为 `cq:Component` 并包含关键元素：

   * jcr属性：

      一列表jcr属性； 这些是变量，某些可能是可选的，尽管组件节点的基本结构，其属性和子节点由定义定 `cq:Component` 义

   * 资源:

      这些组件定义组件使用的静态元素。

   * 脚本:

   用于实现组件的结果实例的行为。

* **根节点**:

   * `<mycomponent> (cq:Component)` -组件的层次结构节点。

* **重要属性**:

   * `jcr:title` -组件标题； 例如，当组件在组件浏览器或Sidekick中列出时，将用作标签。
   * `jcr:description` -组件说明； 可用作组件浏览器或Sidekick中的鼠标悬停提示。
   * 经典 UI：

      * `icon.png` -此组件的图标。
      * `thumbnail.png` -如果此组件列在段落系统中，则显示的图像。
   * 触屏UI

      * 有关详细信息， [请参阅触屏UI中的组](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 件图标部分。


* **重要子节点**:

   * `cq:editConfig (cq:EditConfig)` -定义组件的编辑属性，并使组件显示在组件浏览器或Sidekick中。

      注意： 如果组件具有对话框，则它将自动显示在组件浏览器或Sidekick中，即使cq:editConfig不存在也是如此。

   * `cq:childEditConfig (cq:EditConfig)` -控制未定义其自身的子组件的作者UI方面 `cq:editConfig`。
   * 触屏优化 UI:

      * `cq:dialog` ( `nt:unstructured`)-此组件的对话框。 定义允许用户配置组件和／或编辑内容的界面。
      * `cq:design_dialog` ( `nt:unstructured`)-此组件的设计编辑
   * 经典 UI：

      * `dialog` ( `cq:Dialog`)-此组件的对话框。 定义允许用户配置组件和／或编辑内容的界面。
      * `design_dialog` ( `cq:Dialog`)-此组件的设计编辑。


#### 触屏UI中的组件图标 {#component-icon-in-touch-ui}

当开发人员创建组件时，组件的图标或缩写是通过组件的JCR属性定义的。 这些属性将按以下顺序计算，并使用找到的第一个有效属性。

1. `cq:icon` -指向Coral UI库中要在组件浏览 [器中显示的标准图](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 标的字符串属性
   * 使用Coral图标的HTML属性值。
1. `abbreviation` -用于自定义组件浏览器中组件名称的缩写的字符串属性
   * 缩写应限制为两个字符。
   * 如果提供空字符串，则将根据属性的前两个字符生成缩 `jcr:title` 写。
      * 例如，“Im”表示“Image”
      * 本地化的标题将用于构建缩写。
   * 仅当组件具有属性时，缩写才 `abbreviation_commentI18n` 会进行翻译，然后用作翻译提示。
1. `cq:icon.png` 或 `cq:icon.svg` -此组件的图标，显示在组件浏览器中
   * 20 x 20像素是标准组件图标的大小。
      * 将缩小较大的图标（客户端）。
   * 建议颜色为rgb(112, 112, 112)> #707070
   * 标准组件图标的背景是透明的。
   * Only `.png` and `.svg` files are supported.
   * 如果通过Eclipse插件从文件系统导入，则文件名需要重 `_cq_icon.png` 新 `_cq_icon.svg` 显示或替换。
   * `.png` 如果两者 `.svg` 都存在，就先例

如果组件上没有 `cq:icon`上 `abbreviation`述属 `cq:icon.png` 性(、 `cq:icon.svg`或):

* 系统将在超级组件上搜索属性，属性位于后 `sling:resourceSuperType` 面。
* 如果在超级组件级别找不到任何缩写或空缩写，则系统将根据当前组件属性的首字母 `jcr:title` 构建缩写。

要取消超级组件中图标的继承，在组件 `abbreviation` 上设置空属性将恢复为默认行为。

组 [件控制台](/help/sites-authoring/default-components-console.md#component-details) ，显示如何定义特定组件的图标。

#### SVG图标示例 {#svg-icon-example}

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

### 组件的属性和子节点 {#properties-and-child-nodes-of-a-component}

定义组件所需的许多节点／属性对于两个UI都是通用的，差异保持独立，这样您的组件就可以在两个环境中工作。

组件是类型的节点， `cq:Component` 具有以下属性和子节点：

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
   <td>当前组件. 组件为节点类型 <code>cq:Component</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>在组件浏览器（触屏优化UI）或Sidekick（经典UI）中选择组件的组。<br /> 值用于 <code>.hidden</code> 无法从UI（如实际段落系统）中进行选择的组件。</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>指示组件是否为容器组件，因此可以包含其他组件，如段落系统。</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>触屏优化UI的编辑对话框定义。</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>经典UI的编辑对话框的定义。</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>触屏优化UI的设计对话框的定义。</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>经典UI的设计对话框的定义。<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>当组件没有对话框节点时用于覆盖案例的对话框路径。<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>如果设置，则此属性将作为单元格ID。 有关详细信息，请参阅知识库文章 <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">如何构建设计单元格ID</a>。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>当组件是容器时（例如段落系统），这将驱动子节点的编辑配置。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">编辑组件的配置</a>。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>返回添加到周围html标签的其他标签属性。 支持向自动生成的div添加属性。</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>如果为true，则不会使用自动生成的div和css类呈现组件。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>如果找到此节点，则当从组件浏览器或Sidekick添加组件时，该节点将用作内容模板。</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>当从组件浏览器或Sidekick添加组件时，要用作内容模板的节点的路径。 这必须是绝对路径，而不是相对于组件节点。<br /> 除非您希望重新使用其他位置已有的内容，否则这不是必需的， <code>cq:template</code> 而且是足够的（请参阅下文）。</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>组件的创建日期。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>组件的说明。<br /> </td>
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
   <td>支持创建虚拟组件。 要查看示例，请查看联系人组件：<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
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
   <td>从Sidekick将组件拖动到位时显示的可选缩略图。<br /> </td>
  </tr>
 </tbody>
</table>

如果我们查看文 **本组件** （任一版本），我们可以看到以下元素：

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

特定权益的物业包括：

* `jcr:title` -组件的标题； 这可用于标识组件，例如，它显示在组件浏览器或Sidekick的组件列表中
* `jcr:description` -组件说明； 可用作sidekick中组件列表中的鼠标悬停提示
* `sling:resourceSuperType`: 这表示在扩展组件（通过覆盖定义）时继承的路径

特定感兴趣的子节点包括：

* `cq:editConfig` ( `cq:EditConfig`-此控制视觉方面； 例如，它可以定义条形或构件的外观，也可以添加自定义控件
* `cq:childEditConfig` ( `cq:EditConfig`)-它控制没有自己定义的子组件的可视方面
* 触屏优化 UI:
   * `cq:dialog` ( `nt:unstructured`)-定义用于编辑此组件内容的对话框
   * `cq:design_dialog` ( `nt:unstructured`)-指定此组件的设计编辑选项
* 经典 UI：
   * `dialog` ( `cq:Dialog`)-定义用于编辑此组件内容的对话框（特定于经典UI）
   * `design_dialog` ( `cq:Dialog`)-指定此组件的设计编辑选项
   * `icon.png` -图形文件，用作Sidekick中组件的图标
   * `thumbnail.png` -从Sidekick拖动组件时用作组件缩略图的图形文件

### 对话框 {#dialogs}

对话框是组件的关键元素，因为它们为作者提供了一个界面，用于配置该组件并为其提供输入。

根据组件的复杂性，对话框可能需要一个或多个选项卡——以保持对话框简短和对输入字段进行排序。

对话框定义特定于UI:

>[!NOTE]
>
>* 出于兼容性考虑，当未为触屏优化UI定义对话框时，触屏优化UI可以使用经典UI对话框的定义。
>* 还提 [供了对话框转换](/help/sites-developing/dialog-conversion.md) 工具，帮助您扩展／转换仅为经典UI定义了对话框的组件。

>



* 触屏优化 UI
   * `cq:dialog` ( `nt:unstructured`节点：
      * 定义用于编辑此组件内容的对话框
      * 特定于触屏优化UI
      * 是使用Granite UI组件定义的
      * 拥有作为标 `sling:resourceType`准Sling内容结构的属性
      * 可以具有一个属 `helpPath` 性来定义在帮助图标(? 图标)。
         * 对于现成组件，这通常引用文档中的页面。
         * 如果未 `helpPath` 指定，则显示默认URL（文档概述页面）。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   在对话框中，定义了单个字段：

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 经典 UI
   * `dialog` (节 `cq:Dialog`点)
      * 定义用于编辑此组件内容的对话框
      * 特定于经典UI
      * 是使用ExtJS构件定义的
      * 具有引 `xtype`用ExtJS的属性
      * 可以有一个属 `helpPath` 性来定义选择“帮助”按钮时访问的上下文相关帮助资源(绝对或相 **对路径** )。
         * 对于现成组件，这通常引用文档中的页面。
         * 如果未 `helpPath` 指定，则显示默认URL（文档概述页面）。

   ![chlimage_1-243](assets/chlimage_1-243.png)

   在对话框中，定义了单个字段：

   ![chlimage_1-244](assets/chlimage_1-244.png)

   在经典对话框中：

   * 您可以创建对话框 `cq:Dialog`，该对话框将提供单个选项卡——如在文本组件中，或者，如果您需要多个选项卡，如在textimage组件中，该对话框可定义为 `cq:TabPanel`。
   * a `cq:WidgetCollection` ( `items`)用于为输入字段()或更多选项 `cq:Widget`卡()提供基 `cq:Widget`础。 可以扩展此层次结构。


### 设计对话框 {#design-dialogs}

设计对话框与用于编辑和配置内容的对话框非常相似，但它们为作者提供了界面，用于配置和提供该组件的设计详细信息。

[设计对话框在设计模式下可用](/help/sites-authoring/default-components-designmode.md)，但并非所有组件（如标题和图像）都 **需要** , **但文本却不需要****** 它们。

段落系统（例如parsys）的设计对话框是一个特殊情况，因为它允许用户在页面上选择特定的其他组件（从组件浏览器或Sidekick）。

### 将组件添加到段落系统 {#adding-your-component-to-the-paragraph-system}

定义组件后，必须允许其使用。 要使组件可用于段落系统，您可以执行以下任一操作：

1. 打开 [页面的](/help/sites-authoring/default-components-designmode.md) “设计模式”并启用所需的组件。
1. 将所需的组件添加到模板定 `components` 义的属性中：

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   例如，请参阅：

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 组件及其创建的内容 {#components-and-the-content-they-create}

如果我们在页面上创建和配置 **标题** 组件的实例： `<content-path>/Prototype.html`

* 触屏优化 UI

   ![chlimage_1-246](assets/chlimage_1-246.png)

* 经典 UI

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

然后，我们可以看到在存储库中创建的内容的结构：

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

特别是，如果您查看标题的实际文 **本**:

* 定义（对于两个UI）具有属 `name`性= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 在内容中，它将生成包含 `jcr:title` 作者内容的属性。

定义的属性取决于各个定义。 虽然比起上面更复杂，但也遵循相同的基本原则。

## 组件层次结构和继承 {#component-hierarchy-and-inheritance}

AEM中的组件受3个不同层次结构的约束：

* **资源类型层次结构**

   它用于使用属性扩展组件 `sling:resourceSuperType`。 这允许组件继承。 例如，文本组件将继承标准组件的各种属性。

   * 脚本（由Sling解析）
   * 对话
   * 描述（包括缩略图图像、图标等）

* **容器层次结构**

   它用于将配置设置填充到子组件中，最常用于parsys方案。

   例如，可在父组件上定义编辑栏按钮、控制集布局（编辑栏、滚动）、对话框布局（内联、浮动）的配置设置并传播到子组件。

   中的配置设置（与编辑功能相关） `cq:editConfig` 和 `cq:childEditConfig` 被传播。

* **包括层次结构**

   在运行时，这由包括序列强加。

   此层次结构由设计人员使用，而设计人员又作为渲染的各个设计方面的基础； 包括布局信息、css信息、parsys中的可用组件等。

## 编辑行为 {#edit-behavior}

本节介绍如何配置组件的编辑行为。 这包括一些属性，如可用于组件的操作、就地编辑器的特性以及与组件上的事件相关的监听器。

该配置对于触屏优化UI和经典UI都是通用的，尽管有某些特定的差异。

通过在组件节点（类型）下添加类 `cq:editConfig` 型的节点 `cq:EditConfig` ，并添加特定属性和子节点，可 `cq:Component`以配置组件的编辑行为。 以下属性和子节点可用：

* [ `cq:editConfig` 节点属性](#configuring-with-cq-editconfig-properties):

   * `cq:actions` ( `String array`): 定义可对组件执行的操作。
   * `cq:layout` ( `String`): : 定义如何在经典UI中编辑组件。
   * `cq:dialogMode` ( `String`): 定义如何在经典UI中打开组件对话框

      * 在触屏优化UI中，对话框始终以桌面模式浮动，并在移动设备中以全屏方式自动打开。
   * `cq:emptyText` ( `String`): 定义当不存在可视内容时显示的文本。
   * `cq:inherit` ( `Boolean`): 定义是否从它继承的组件继承缺失值。
   * `dialogLayout` （字符串）: 定义对话框的打开方式。


* [ `cq:editConfig` 子节点](#configuring-with-cq-editconfig-child-nodes):

   * `cq:dropTargets` (节点类 `nt:unstructured`型): 定义拖放列表目标，可接受内容查找器资产的删除

      * 多个拖放目标仅在经典UI中可用。
      * 在触屏优化UI中，允许使用单个拖放目标。
   * `cq:actionConfigs` (节点类 `nt:unstructured`型): 定义附加到cq:actions列表的新操作列表。
   * `cq:formParameters` (节点类 `nt:unstructured`型): 定义添加到对话框表单的其他参数。
   * `cq:inplaceEditing` (节点类 `cq:InplaceEditingConfig`型): 为组件定义就地编辑配置。
   * `cq:listeners` (节点类 `cq:EditListenersConfig`型): 定义在组件上执行操作之前或之后发生的情况。


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

存储库中有许多现有配置。 您可以轻松搜索特定属性或子节点：

* 要查找节点的属 `cq:editConfig` 性，例如 `cq:actions`，您可以在CRXDE Lite中使用查询 **工具** ，并使用以下XPath查询字符串进行搜索：

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 要查找的子节 `cq:editConfig`点，例如，可以 `cq:dropTargets`搜索类型的子节点 `cq:DropTargetConfig`; 您可以在** CRXDE Lite**中使用查询工具，并使用以下XPath查询字符串进行搜索：

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### 使用cq:EditConfig属性进行配置 {#configuring-with-cq-editconfig-properties}

### cq：动作 {#cq-actions}

属 `cq:actions` 性( `String array`)定义可对组件执行的一个或多个操作。 以下值可用于配置：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>显示静态文本值&lt;some text&gt;<br /> Only visible in classic UI。 触屏优化UI不在上下文菜单中显示操作，因此不适用。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>添加间隔符。<br /> 仅在经典UI中可见。 触屏优化UI不在上下文菜单中显示操作，因此不适用。</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>添加用于编辑组件的按钮。</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>添加一个按钮以编辑组件以及允许 <a href="/help/sites-authoring/annotations.md">注释</a>。</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>添加用于删除组件的按钮</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>在当前组件之前添加一个按钮以插入新组件</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>添加用于复制和剪切组件的按钮。</td>
  </tr>
 </tbody>
</table>

以下配置将编辑按钮、分隔条、删除和插入按钮添加到组件编辑栏：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

以下配置将文本“从基础框架继承的配置”添加到组件编辑栏：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq：布局（仅限经典UI） {#cq-layout-classic-ui-only}

属 `cq:layout` 性( `String`)定义如何在经典UI中编辑组件。 以下值可用：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>默认值。 组件版本可通过单击和／或上下文菜单“鼠标悬停”访问。<br /> 要进行高级使用，请注意相应的客户端对象是： <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>组件版本可通过工具栏访问。<br /> 要进行高级使用，请注意相应的客户端对象是： <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>选择由客户端代码进行。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>翻转和编辑栏的概念在触屏优化UI中不适用。

以下配置将编辑按钮添加到组件编辑栏：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode（仅限经典UI） {#cq-dialogmode-classic-ui-only}

组件可以链接到编辑对话框。 属 `cq:dialogMode` 性( `String`)定义如何在经典UI中打开组件对话框。 以下值可用：

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
   <td>(默认值). 对话框锚定在组件上。<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>如果组件宽度小于客户端值，则 <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> 对话框是浮动的，否则它是内嵌的。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在触屏优化UI中，对话框始终以桌面模式浮动，并在移动设备中自动以全屏方式打开。

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

属 `cq:emptyText` 性( `String`)定义在不存在可视内容时显示的文本。 默认为： `Drag components or assets here`.

### cq:inherit {#cq-inherit}

属 `cq:inherit` 性( `boolean`)定义是否从其继承的组件继承缺失值。 默认为 `false`。

### dialogLayout {#dialoglayout}

属性 `dialogLayout` 定义默认情况下打开对话框的方式。

* 值将全 `fullscreen` 屏打开对话框。
* 默认情况下，空值或属性的缺失将正常打开对话框。
* 请注意，用户始终可以在对话框中切换全屏模式。
* 不适用于经典UI。

### 使用cq:EditConfig子节点进行配置 {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

节 `cq:dropTargets` 点（节点类型） `nt:unstructured`定义一个放置目标列表，可以接受从内容查找器拖动的资产中的放置。 它用作类型节点的集合 `cq:DropTargetConfig`。

>[!NOTE]
>
>多个拖放目标仅在经典UI中可用。
>
>在触屏优化UI中，只使用第一个目标。

每个类型的子节 `cq:DropTargetConfig` 点都定义组件中的放置目标。 节点名称很重要，因为它必须用在JSP中，如下所示，才能生成分配给DOM元素的CSS类名称，该元素是有效的放置目标:

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

由 `<drag and drop prefix>` Java属性定义：

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`。

例如，类名在Download component()的JSP中定义如下 `/libs/foundation/components/download/download.jsp`，其中 `file` 是Download组件编辑配置中放置目标的节点名：

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

类型的节 `cq:DropTargetConfig` 点需要具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>对资产MIME类型应用的正则表达式，以验证是否允许删除。</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>放置目标组阵列。 每个组必须与内容查找器扩展中定义的并附加到资产的组类型相匹配。</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>在有效删除后将更新的属性的名称。</td>
  </tr>
 </tbody>
</table>

下列配置是从下载组件中进行的。 它允许将组中的任何资产（mime类型可以是任何字符串） `media` 从内容查找器丢弃到组件中。 放置后，组件属性 `fileReference` 将更新：

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs（仅限经典UI） {#cq-actionconfigs-classic-ui-only}

节 `cq:actionConfigs` 点(节点类 `nt:unstructured`型)定义新操作的列表，这些操作附加到属性定义的 `cq:actions` 列表。 每个子节点 `cq:actionConfigs` 通过定义构件来定义新操作。

以下示例配置定义一个新按钮（带有经典UI的分隔符）:

* 由xtype定义的分隔符 `tbseparator`;

   * 仅经典UI使用。
   * 触屏优化UI会忽略此定义，因为xtypes会被忽略（而且，由于在触屏优化UI中以不同方式构建操作工具栏，因此不必使用分隔符）。

* 一个名为“管 **理注释** ”的按钮，它运行处理函数 `CQ_collab_forum_openCollabAdmin()`。

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
>请参 [阅将新操作添加到组件工具栏](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) ，作为触屏优化UI的示例。

### cq:formParameters {#cq-formparameters}

节 `cq:formParameters` 点(节点类 `nt:unstructured`型)定义添加到对话框表单的其他参数。 每个属性都映射到一个表单参数。

以下配置将一个名为的 `name`参数（用值设置）添 `photos/primary` 加到对话框表单：

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

节 `cq:inplaceEditing` 点(节点类 `cq:InplaceEditingConfig`型)定义组件的就地编辑配置。 它可以具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>)启用组件的就地编辑。</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>)编辑器配置的路径。 配置节点可以指定配置。</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>()<code>String</code>编辑器类型。 可用类型有：</p>
    <ul>
     <li>纯文本： 用于非HTML内容。<br /> </li>
     <li>标题： 是一种增强的纯文本编辑器，在开始编辑之前将图形字幕转换为纯文本。 由Geometrixx标题组件使用。<br /> </li>
     <li>文本： 用于HTML内容（使用富文本编辑器）。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

以下配置启用组件的就地编辑并定 `plaintext` 义为编辑器类型：

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq：监听器 {#cq-listeners}

节 `cq:listeners` 点(节点类 `cq:EditListenersConfig`型)定义在组件上执行操作之前或之后发生的情况。 下表定义了其可能的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
   <td><p><strong>默认值</strong></p> <p>（仅限经典UI）</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>在删除组件之前将触发处理程序。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>在编辑组件之前将触发该处理函数。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>在复制组件之前将触发该处理函数。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>在移动组件之前触发处理程序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>在插入组件之前将触发处理程序。<br /> 仅适用于触屏优化UI。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>在将组件插入另一个组件之前，将触发该处理程序(仅容器)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>删除组件后将触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>编辑组件后将触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>在复制组件后将触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>插入组件后将触发处理程序。</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>在移动组件后将触发处理程序。</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>该处理函数在组件插入另一个组件后触发(仅容器)。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只有 `REFRESH_INSERTED` 经典 `REFRESH_SELFMOVED` UI中提供这些和处理函数。

>[!NOTE]
>
>监听器的默认值仅在经典UI中设置。

>[!NOTE]
>
>对于嵌套组件，对于定义为节点上属性的操作有一些 `cq:listeners` 限制：
>
>* 对于嵌套组件，以下属性的值 *必须* 为 `REFRESH_PAGE`: >
>  * `aftermove`
>  * `aftercopy`


事件处理函数可以通过自定义实现实现。 例如(其 `project.customerAction` 中是静态方法):

`afteredit = "project.customerAction"`

以下示例与配置相 `REFRESH_INSERTED` 同：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>有关经典UI，请参阅和构件文档的“和 `before<action>` 事件 `after<action>` ”部分，以查看可在处理 [ 函数中 `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) 使用 [ 的参 `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover) 数。

使用以下配置，在删除、编辑、插入或移动组件后刷新页面：

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
