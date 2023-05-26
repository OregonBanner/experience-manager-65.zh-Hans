---
title: AEM组件 — 基础知识
seo-title: AEM Components - The Basics
description: 在开始开发新组件时，您需要了解其结构和配置的基础知识
seo-description: When you start to develop new components you need to understand the basics of their structure and configuration
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '4948'
ht-degree: 1%

---

# AEM组件 — 基础知识{#aem-components-the-basics}

在开始开发新组件时，您需要了解其结构和配置的基础知识。

此过程包括阅读相关理论，并查看标准AEM实例中的各种组件实施。 尽管AEM已转移到新的标准、现代、触屏优化UI，但它继续支持经典UI，这一事实使后一种方法稍微复杂一些。

## 概述 {#overview}

此部分涵盖关键概念和问题，并介绍开发您自己的组件时所需的详细信息。

### 规划 {#planning}

在开始实际配置或编码组件之前，您应该询问：

* 您到底需要新组件做什么？
   * 明确的规范有助于开发、测试和移交的所有阶段。 详细信息可能会随着时间的推移而改变，但规范可以更新（尽管更改也应记录在案）。
* 您是需要从头开始创建组件，还是可以从现有组件继承基础知识？
   * 不需要重新发明轮子。
   * AEM提供了多种机制，允许您从其他组件定义继承和扩展详细信息，包括覆盖、叠加和 [Sling资源合并器](/help/sites-developing/sling-resource-merger.md).
* 您的组件是否需要逻辑来选择/处理内容？
   * 逻辑应与用户界面层分开。 HTL旨在帮助确保实现此目的。
* 您的组件是否需要CSS格式？
   * CSS格式应与组件定义分开。 定义用于命名HTML元素的约定，以便您可以通过外部CSS文件修改这些约定。
* 我应该考虑哪些安全方面？
   * 参见 [安全核对清单 — 开发最佳实践](/help/sites-administering/security-checklist.md#development-best-practices) 了解更多详细信息。

### 触屏优化vs经典UI {#touch-enabled-vs-classic-ui}

在就开发组件展开任何严肃讨论之前，您需要知道作者将使用哪种UI：

* **触屏优化UI**
   [标准用户界面](/help/sites-developing/touch-ui-concepts.md) 基于Adobe Marketing Cloud的统一用户体验，使用以下底层技术： [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui).
* **经典Ui**
基于ExtJS技术的用户界面，AEM 6.4已弃用。

参见 [适用于客户的UI界面Recommendations](/help/sites-deploying/ui-recommendations.md) 了解更多详细信息。

可以实施组件以支持触屏UI和/或经典UI。 在查看标准实例时，您还会看到最初为经典UI或触屏UI或两者而设计的现成组件。

因此，在本页中，我们将介绍这两个规则的基本知识以及如何识别它们。

>[!NOTE]
>
>Adobe建议利用触屏优化UI来从最新技术中获益。 [AEM现代化工具](modernization-tools.md) 可以更轻松地迁移。

### 内容逻辑和渲染标记  {#content-logic-and-rendering-markup}

建议将负责标记和渲染的代码与控制用于选择组件内容的逻辑的代码分开。

这一理念得到以下支持 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，一种模板化语言，专门用于确保使用真正的编程语言来定义底层业务逻辑。 此（可选）逻辑通过特定命令从HTL调用。 此机制会突出显示为给定视图调用的代码，如果需要，还允许为同一组件的不同视图使用特定逻辑。

### HTL与JSP {#htl-vs-jsp}

HTL是AEM 6.0中引入的一种HTML模板语言。

关于是否使用的讨论 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 或JSP (Java Server Pages)在开发您自己的组件时应该简单明了，因为HTL现在是AEM推荐的脚本语言。

HTL和JSP都可用于为经典用户界面和触屏优化UI开发组件。 尽管可能会倾向于认为HTL仅适用于触屏UI和经典UI的JSP，但这是一种误解，并且更多是由于时间原因。 触摸式UI和HTL大约在同一时期内合并到AEM中。 由于HTL现在是推荐的语言，因此它被用于新组件，这些组件倾向于用于触屏优化UI。

>[!NOTE]
>
>Granite UI Foundation表单字段除外（在对话框中使用）。 这些仍需要使用JSP。

### 开发您自己的组件 {#developing-your-own-components}

要为相应的UI创建自己的组件，请参阅（阅读本页后）：

* [触屏UI的AEM组件](/help/sites-developing/developing-components.md)
* [经典UI的AEM组件](/help/sites-developing/developing-components-classic.md)

快速入门方法是复制现有组件，然后进行所需的更改。 要了解如何创建自己的组件并将它们添加到段落系统，请参阅：

* [开发组件](/help/sites-developing/developing-components-samples.md) （侧重于触屏UI）

### 将组件移动到发布实例 {#moving-components-to-the-publish-instance}

呈现内容的组件必须部署在与内容相同的AEM实例上。 因此，必须在发布实例上部署用于创作和渲染创作实例上的页面的所有组件。 部署后，组件可用于渲染已激活的页面。

使用以下工具将组件移动到发布实例：

* [使用包管理器](/help/sites-administering/package-manager.md) 以将组件添加到资源包并将它们移动到另一个AEM实例。
* [使用激活树复制工具](/help/sites-authoring/publishing-pages.md#manage-publication) 以复制组件。

>[!NOTE]
>
>这些机制还可用于在其他实例之间传输组件，例如，从开发实例传输到测试实例。

### 从头开始要注意的组件 {#components-to-be-aware-of-from-the-start}

* 页面:

   * AEM具有 *页面* 组件( `cq:Page`)。
   * 这是特定类型的资源，对内容管理很重要。
      * 页面对应于包含您网站内容的网页。

* 段落系统：

   * 段落系统是网站的一个关键部分，因为它管理着段落列表。 它用于保存和构建包含实际内容的各个组件。
   * 您可以在段落系统中创建、移动、复制和删除段落。
   * 您还可以选择可在特定段落系统中使用的组件。
   * 标准实例中有各种可用的段落系统(例如 `parsys`， ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`)。

## 结构 {#structure}

AEM组件的结构强大而灵活，主要考虑因素包括：

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

这是一个抽象，有助于确保即使当外观和感觉随时间变化时，意图仍会停留在时间上。

### 组件定义 {#component-definition}

#### 组件基础知识 {#component-basics}

组件的定义可细分如下：

* AEM组件基于 [Sling](https://sling.apache.org/documentation.html).
* AEM组件（通常）位于以下位置：

   * HTL: `/libs/wcm/foundation/components`
   * JSP： `/libs/foundation/components`

* 项目/站点特定的组件（通常）位于以下位置：

   * `/apps/<myApp>/components`

* AEM标准组件定义为 `cq:Component` 并具有关键元素：

   * jcr属性：

      jcr属性的列表；这些属性是变量的，有些可能是可选的，但组件节点的基本结构、其属性和子节点由定义。 `cq:Component` 定义

   * 资源:

      这些定义组件使用的静态元素。

   * 脚本:

   用于实施组件的结果实例的行为。

* **根节点**：

   * `<mycomponent> (cq:Component)`  — 组件的层次结构节点。

* **重要属性**：

   * `jcr:title`  — 组件标题；例如，当组件在组件浏览器或Sidekick中列出时用作标签。
   * `jcr:description`  — 组件的描述；可用作组件浏览器或Sidekick中的鼠标悬停提示。
   * 经典 UI:

      * `icon.png`  — 此组件的图标。
      * `thumbnail.png`  — 如果此组件在段落系统中列出，则显示图像。
   * 触屏 UI

      * 请参阅部分 [触屏UI中的组件图标](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 了解详细信息。


* **重要子节点**：

   * `cq:editConfig (cq:EditConfig)`  — 定义组件的编辑属性，并使组件显示在组件浏览器或Sidekick中。

      注意：如果组件有对话框，它将自动显示在组件浏览器或Sidekick中，即使cq：editConfig不存在。

   * `cq:childEditConfig (cq:EditConfig)`  — 控制子组件的创作UI方面，这些组件未定义自己的组件 `cq:editConfig`.
   * 触屏优化UI：

      * `cq:dialog` ( `nt:unstructured`) — 此组件的对话框。 定义允许用户配置组件和/或编辑内容的界面。
      * `cq:design_dialog` ( `nt:unstructured`) — 此组件的设计编辑
   * 经典 UI:

      * `dialog` ( `cq:Dialog`) — 此组件的对话框。 定义允许用户配置组件和/或编辑内容的界面。
      * `design_dialog` ( `cq:Dialog`) — 此组件的设计编辑。


#### 触屏UI中的组件图标 {#component-icon-in-touch-ui}

组件的图标或缩写在开发人员创建组件时通过组件的JCR属性定义。 这些属性的计算顺序如下，并且使用找到的第一个有效属性。

1. `cq:icon`  — 字符串属性，指向 [Coral UI库](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 在组件浏览器中显示
   * 使用Coral图标的HTML属性的值。
1. `abbreviation`  — 字符串属性，用于自定义组件浏览器中组件名称的缩写
   * 缩写应限制为两个字符。
   * 提供空字符串将构建 `jcr:title` 属性。
      * 例如，“Im”表示“图像”
      * 本地化的标题将用于构建缩写。
   * 仅组件具有以下特征时，才会翻译缩写： `abbreviation_commentI18n` 属性，然后用作翻译提示。
1. `cq:icon.png` 或 `cq:icon.svg`  — 此组件的图标，显示在组件浏览器中
   * 20 x 20像素是标准组件的图标大小。
      * 较大的图标将被缩小（客户端）。
   * 推荐的颜色为rgb(112， 112， 112) > #707070
   * 标准组件图标的背景透明。
   * 仅 `.png` 和 `.svg` 文件受支持。
   * 如果通过Eclipse插件从文件系统导入，则需要将文件名转义为 `_cq_icon.png` 或 `_cq_icon.svg` 例如。
   * `.png` 让先例重演 `.svg` 如果两者都存在

如果以上属性均不( `cq:icon`， `abbreviation`， `cq:icon.png` 或 `cq:icon.svg`)，具体情况如下：

* 系统将在超级组件上搜索相同的属性，如下所示 `sling:resourceSuperType` 属性。
* 如果在超级组件级别上未找到任何内容或发现空缩写，则系统将根据 `jcr:title` 当前组件的属性。

要取消从超级组件继承图标，请将设置为空 `abbreviation` 组件上的属性将还原为默认行为。

此 [组件控制台](/help/sites-authoring/default-components-console.md#component-details) 显示如何定义特定组件的图标。

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

定义组件所需的许多节点/属性对这两个UI都是通用的，不同之处保持独立，以便您的组件可以在两个环境中工作。

组件是类型的节点 `cq:Component` 和具有以下属性和子节点：

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
   <td>当前组件. 组件属于节点类型 <code>cq:Component</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>可以在组件浏览器（触屏UI）或Sidekick（经典UI）中选择组件的组。<br /> 值 <code>.hidden</code> 用于无法从UI中选择的组件，例如实际段落系统。</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>指示组件是否为容器组件，因此可以包含其他组件，例如段落系统。</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>触屏UI的“编辑”对话框的定义。</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>经典UI的“编辑”对话框的定义。</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>触屏UI的“设计”对话框的定义。</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>经典UI的“设计”对话框的定义。<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>指向对话框的路径，以在组件没有对话框节点时覆盖这种情况。<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>如果设置，此属性将被视为单元格ID。 有关更多信息，请参阅知识库文章 <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">如何构建设计单元格ID</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>当组件是容器时（例如，段落系统），这会驱动子节点的编辑配置。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">编辑组件的配置</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>返回添加到周围html标记的其他标记属性。 允许向自动生成的div添加属性。</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>如果为true，则组件不会使用自动生成的div和css类渲染。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>如果找到，则在从组件浏览器或Sidekick添加组件时，此节点将用作内容模板。</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>从组件浏览器或Sidekick添加组件时用作内容模板的节点的路径。 这必须是绝对路径，而不是相对于组件节点的路径。<br /> 除非您希望重新使用其他地方已有的内容，否则不需要这样做，并且 <code>cq:template</code> 足够（见下文）。</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>创建组件的日期。<br /> </td>
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
   <td>设置后，组件会继承此组件。<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>允许创建虚拟组件。 要查看示例，请查看位于以下位置的联系人组件：<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
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
   <td>将组件从Sidekick拖动到适当位置时显示的可选缩略图。<br /> </td>
  </tr>
 </tbody>
</table>

如果我们查看 **文本** 组件（无论是哪个版本），我们可以看到以下元素：

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP ( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

特别感兴趣之物业包括：

* `jcr:title`  — 组件的标题；这可用于识别组件，例如，它显示在组件浏览器或sidekick内的组件列表中
* `jcr:description`  — 组件的描述；可以用作sidekick中组件列表的鼠标悬停提示
* `sling:resourceSuperType`：表示扩展组件时（通过覆盖定义）的继承路径

特别感兴趣的子节点包括：

* `cq:editConfig` ( `cq:EditConfig`) — 此选项控制可视方面；例如，可以定义条形图或小部件的外观，或者可以添加自定义控件
* `cq:childEditConfig` ( `cq:EditConfig`) — 这控制没有自己的定义的子组件的可视化方面
* 触屏优化UI：
   * `cq:dialog` ( `nt:unstructured`) — 定义用于编辑此组件内容的对话框
   * `cq:design_dialog` ( `nt:unstructured`) — 指定此组件的设计编辑选项
* 经典 UI:
   * `dialog` ( `cq:Dialog`) — 定义用于编辑此组件内容的对话框（特定于经典UI）
   * `design_dialog` ( `cq:Dialog`) — 指定此组件的设计编辑选项
   * `icon.png`  — 用作Sidekick中组件的图标的图形文件
   * `thumbnail.png`  — 从Sidekick拖动组件时用作组件缩略图的图形文件

### 对话框 {#dialogs}

对话框是组件的关键元素，因为它们为作者提供了一个界面来配置该组件并提供输入。

根据组件的复杂性，您的对话框可能需要一个或多个选项卡 — 缩短对话框并对输入字段进行排序。

对话框定义特定于UI：

>[!NOTE]
>
>* 为兼容起见，如果没有为触屏UI定义对话框，触屏UI可以使用经典UI对话框的定义。
>* 此 [AEM现代化工具](/help/sites-developing/modernization-tools.md) 此外，还帮助您扩展/转换仅具有为经典UI定义的对话框的组件。
>


* 触屏优化UI
   * `cq:dialog` ( `nt:unstructured`)节点：
      * 定义用于编辑此组件内容的对话框
      * 特定于触屏UI
      * 使用Granite UI组件定义
      * 具有属性 `sling:resourceType`，作为标准Sling内容结构
      * 可以具有属性 `helpPath` 定义在帮助图标(？ 图标)时，不会将鼠标指针置于“已更改”区域中。
         * 对于开箱即用的组件，这通常会引用文档中的页面。
         * 如果否 `helpPath` 指定时，将显示默认URL（文档概述页面）。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   在该对话框中，定义了各个字段：

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 经典 UI
   * `dialog` ( `cq:Dialog`)节点
      * 定义用于编辑此组件内容的对话框
      * 特定于经典UI
      * 使用ExtJS构件定义
      * 具有属性 `xtype`，是指ExtJS
      * 可以具有属性 `helpPath` 定义在下列情况下访问的上下文相关帮助资源：绝对路径或相对路径 **帮助** 按钮处于选中状态。
         * 对于开箱即用的组件，这通常会引用文档中的页面。
         * 如果否 `helpPath` 指定时，将显示默认URL（文档概述页面）。

   ![chlimage_1-243](assets/chlimage_1-243.png)

   在该对话框中，定义了各个字段：

   ![chlimage_1-244](assets/chlimage_1-244.png)

   在Classic对话框中：

   * 您可以创建对话框为 `cq:Dialog`，这将提供单个选项卡 — 与文本组件中一样，或者如果您需要多个选项卡（与文本时间组件一样），则可以将该对话框定义为 `cq:TabPanel`.
   * a `cq:WidgetCollection` ( `items`)为任一输入字段提供基础( `cq:Widget`)或其他选项卡( `cq:Widget`)。 此层次结构可以扩展。


### 设计对话框 {#design-dialogs}

“设计”对话框与用于编辑和配置内容的对话框非常相似，但它们为作者提供了配置该组件并提供其设计详细信息的界面。

[设计对话框在设计模式下可用](/help/sites-authoring/default-components-designmode.md)，尽管并非所有组件都需要它们，例如 **标题** 和 **图像** 两者都具有设计对话框，而 **文本** 不会。

段落系统的“设计”对话框（例如parsys）是一种特殊情况，因为它允许用户在页面上选择特定的其他组件（从组件浏览器或sidekick）。

### 将组件添加到段落系统 {#adding-your-component-to-the-paragraph-system}

定义组件后，必须使其可用。 要使组件可用于段落系统，您可以：

1. 打开 [设计模式](/help/sites-authoring/default-components-designmode.md) ，并启用所需的组件。
1. 将所需的组件添加到 `components` 属性下的模板定义：

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   例如，请参阅：

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 组件及其创建的内容 {#components-and-the-content-they-create}

如果我们创建和配置 **标题** 页面上的组件： `<content-path>/Prototype.html`

* 触屏优化UI

   ![chlimage_1-246](assets/chlimage_1-246.png)

* 经典 UI

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

然后，我们可以查看在存储库中创建的内容的结构：

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

特别是，如果您查看 **标题**：

* 定义（适用于两个UI）具有属性 `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 在内容中，这将生成属性 `jcr:title` 保存作者的内容。

定义的属性取决于各个定义。 尽管它们可能比上面更复杂，但它们仍然遵循同样的基本原则。

## 组件层次结构和继承 {#component-hierarchy-and-inheritance}

AEM中的组件遵循3个不同的层次结构：

* **资源类型层次结构**

   这用于使用属性扩展组件 `sling:resourceSuperType`. 这将使组件能够继承。 例如，文本组件将继承标准组件的各种属性。

   * 脚本（由Sling解析）
   * 对话框
   * 描述（包括缩略图图像、图标等）

* **容器层次结构**

   这用于向子组件填充配置设置，并且最常用于parsys场景。

   例如，可以在父组件上定义编辑栏按钮的配置设置、控件集布局（编辑栏、变换）、对话框布局（内联、浮动）并传播到子组件。

   中的配置设置（与编辑功能相关） `cq:editConfig` 和 `cq:childEditConfig` 都会被传播。

* **包括层次结构**

   这是在运行时由include序列施加的。

   设计器使用此层级，而此层级又用作呈现的各个设计方面的基础；包括布局信息、css信息、parsys中的可用组件等。

## 编辑行为 {#edit-behavior}

本节介绍如何配置组件的编辑行为。 这包括各种属性，例如组件可用的操作、就地编辑器的特征以及与组件上的事件相关的侦听器。

尽管存在某些特定差异，但配置对于触屏优化UI和经典UI都是通用的。

组件的编辑行为可通过添加 `cq:editConfig` 类型节点 `cq:EditConfig` 在组件节点下(类型为 `cq:Component`)，并添加特定属性和子节点。 以下属性和子节点可用：

* [ `cq:editConfig` 节点属性](#configuring-with-cq-editconfig-properties)：

   * `cq:actions` ( `String array`)：定义可以对组件执行的操作。
   * `cq:layout` ( `String`)： ：定义如何在经典UI中编辑组件。
   * `cq:dialogMode` ( `String`)：定义如何在经典UI中打开组件对话框

      * 在触屏优化UI中，对话框在桌面模式下始终处于浮动状态，并在移动设备中自动作为全屏打开。
   * `cq:emptyText` ( `String`)：定义不存在可视内容时显示的文本。
   * `cq:inherit` ( `Boolean`)：定义缺少的值是否从它继承的组件继承。
   * `dialogLayout` （字符串）：定义应如何打开对话框。


* [ `cq:editConfig` 子节点](#configuring-with-cq-editconfig-child-nodes)：

   * `cq:dropTargets` (节点类型 `nt:unstructured`)：定义可以接受从内容查找器的资源进行放置的放置目标的列表

      * 多个放置目标仅在经典UI中可用。
      * 在触屏优化UI中，允许使用单个放置目标。
   * `cq:actionConfigs` (节点类型 `nt:unstructured`)：定义附加到cq：actions列表的新操作的列表。
   * `cq:formParameters` (节点类型 `nt:unstructured`)：定义添加到对话框表单的其他参数。
   * `cq:inplaceEditing` (节点类型 `cq:InplaceEditingConfig`)：定义组件的就地编辑配置。
   * `cq:listeners` (节点类型 `cq:EditListenersConfig`)：定义在组件上发生操作之前或之后发生的情况。


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

* 要查找 `cq:editConfig` 节点，例如 `cq:actions`中，您可以使用查询工具 **CRXDE Lite** 和搜索以下XPath查询字符串：

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 查找的子节点 `cq:editConfig`，例如，您可以搜索 `cq:dropTargets`，属于类型 `cq:DropTargetConfig`；您可以使用查询工具在**CRXDE Lite**和搜索中使用以下XPath查询字符串：

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### 组件占位符 {#component-placeholders}

组件必须始终呈现对作者可见的一些HTML，即使组件没有内容也是如此。 否则，它可能会从编辑器的界面中消失，从技术上讲，它会存在，但在页面和编辑器中不可见。 在这种情况下，作者将无法选择空组件并与之交互。

因此，组件应呈现占位符，前提是在页面编辑器中呈现页面时(当WCM模式为 `edit` 或 `preview`)。
占位符的典型HTML标记如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

呈现上述占位符HTML的典型HTL脚本如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一个示例中， `isEmpty` 是一个变量，仅当组件没有内容并且作者不可见时为真。

为避免重复，Adobe建议组件的实施者为这些占位符使用HTL模板， [类似于核心组件提供的插件。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

然后，使用下面一行HTL完成上一个链接中的模板使用：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一个示例中， `model.text` 是变量，仅当内容包含内容且可见时为真。

可在核心组件中查看此模板的示例用法， [例如，在标题组件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq：EditConfig属性进行配置 {#configuring-with-cq-editconfig-properties}

### cq：actions {#cq-actions}

此 `cq:actions` 属性( `String array`)定义可以对组件执行的一个或多个操作。 以下值可用于配置：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>显示静态文本值 &lt;some text=""&gt;<br /> 仅在经典UI中可见。 触屏优化UI不会在上下文菜单中显示操作，因此这不适用。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>添加分隔符。<br /> 仅在经典UI中可见。 触屏优化UI不会在上下文菜单中显示操作，因此这不适用。</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>添加按钮以编辑组件。</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>添加按钮以编辑组件并允许 <a href="/help/sites-authoring/annotations.md">批注</a>.</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>添加按钮以删除组件</td>
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

以下配置向组件编辑栏中添加了编辑按钮、分隔符、删除和插入按钮：

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

### cq：layout（仅限经典UI） {#cq-layout-classic-ui-only}

此 `cq:layout` 属性( `String`)定义如何在经典UI中编辑组件。 可以使用以下值：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>默认值。 组件版本可通过单击和/或上下文菜单“在鼠标悬停时”访问。<br /> 对于高级使用，请注意，相应的客户端对象为： <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>组件版本可通过工具栏访问。<br /> 对于高级使用，请注意，相应的客户端对象为： <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>该选项将保留在客户端代码中。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>变换和编辑栏的概念不适用于触屏UI。

以下配置会将编辑按钮添加到组件编辑栏：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq：dialogMode（仅限经典UI） {#cq-dialogmode-classic-ui-only}

该组件可以链接到“编辑”对话框。 此 `cq:dialogMode` 属性( `String`)定义如何在经典UI中打开组件对话框。 可以使用以下值：

<table>
 <tbody>
  <tr>
   <td><strong>属性值</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>对话框浮动。<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(默认值). 该对话框定位在组件上。<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>如果组件宽度小于客户端 <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> 值，则对话框处于浮动状态，否则对话框处于内联状态。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在触屏优化UI中，对话框在桌面模式下始终处于浮动状态，并在移动设备中自动作为全屏打开。

以下配置定义了一个带有编辑按钮的编辑栏和一个浮动对话框：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq：emptyText {#cq-emptytext}

此 `cq:emptyText` 属性( `String`)定义不存在可视内容时显示的文本。 默认为： `Drag components or assets here`.

### cq：inherit {#cq-inherit}

此 `cq:inherit` 属性( `boolean`)定义缺少的值是否从它继承的组件继承。 默认为 `false`.

### 对话框布局 {#dialoglayout}

此 `dialogLayout` 属性定义默认情况下应如何打开对话框。

* 值 `fullscreen` 全屏打开对话框。
* 如果属性为空值或缺失，则默认正常打开对话框。
* 请注意，用户始终可以在对话框中切换全屏模式。
* 不适用于经典UI

### 使用cq：EditConfig子节点进行配置 {#configuring-with-cq-editconfig-child-nodes}

### cq：dropTargets {#cq-droptargets}

此 `cq:dropTargets` 节点（节点类型） `nt:unstructured`)定义一个放置目标列表，这些放置目标可以接受从内容查找器拖动的资产中的放置。 它用作类型节点的集合 `cq:DropTargetConfig`.

>[!NOTE]
>
>多个放置目标仅在经典UI中可用。
>
>在触屏优化UI中，将仅使用第一个目标。

每个类型的子节点 `cq:DropTargetConfig` 在组件中定义放置目标。 节点名称非常重要，因为它必须在JSP中使用，如下所示，才能生成分配给作为有效放置目标的DOM元素的CSS类名称：

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

此 `<drag and drop prefix>` 由Java属性定义：

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`。

例如，类名在下载组件的JSP中定义如下( `/libs/foundation/components/download/download.jsp`)，其中 `file` 是下载组件的编辑配置中的放置目标的节点名称：

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

类型的节点 `cq:DropTargetConfig` 需要具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>应用于资源mime类型的正则表达式，以验证是否允许删除。</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>放置目标组的数组。 每个组必须匹配内容查找器扩展中定义的组类型以及附加到资产的组类型。</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>有效放置后将更新的属性的名称。</td>
  </tr>
 </tbody>
</table>

以下配置是从下载组件中获取的。 它支持来自的任意资源（mime类型可以是任意字符串） `media` 组从内容查找器放入组件中。 放置后，组件属性 `fileReference` 正在更新：

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq：actionConfigs（仅限经典UI） {#cq-actionconfigs-classic-ui-only}

此 `cq:actionConfigs` 节点（节点类型） `nt:unstructured`)定义附加到由定义的列表的新操作列表。 `cq:actions` 属性。 的每个子节点 `cq:actionConfigs` 通过定义构件来定义新操作。

以下示例配置定义了一个新按钮（带有用于经典UI的分隔符）：

* 分隔符，由xtype定义 `tbseparator`；

   * 此变量仅供经典UI使用。
   * 触屏UI会忽略此定义，因为xtypes会被忽略（并且无需使用分隔符，因为操作工具栏在触屏UI中的结构不同）。

* 名为的按钮 **管理评论** 运行handler函数的 `CQ_collab_forum_openCollabAdmin()`.

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
>参见 [将新操作添加到组件工具栏](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 作为触屏UI的示例。

### cq：formParameters {#cq-formparameters}

此 `cq:formParameters` 节点（节点类型） `nt:unstructured`)定义添加到对话框表单的其他参数。 每个属性都映射到一个表单参数。

以下配置添加了一个名为的参数 `name`，使用值设置 `photos/primary` 到对话框窗体：

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq：inplaceEditing {#cq-inplaceediting}

此 `cq:inplaceEditing` 节点（节点类型） `cq:InplaceEditingConfig`)为组件定义就地编辑配置。 它可以具有以下属性：

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>) True以启用组件的就地编辑。</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>)编辑器配置的路径。 配置可以由配置节点指定。</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>)编辑器类型。 可用的类型包括：</p>
    <ul>
     <li>纯文本：用于非HTML内容。<br /> </li>
     <li>标题：是一种增强的纯文本编辑器，可在编辑开始之前将图形标题转换为纯文本。 由Geometrixx标题组件使用。<br /> </li>
     <li>文本：用于HTML内容（使用富文本编辑器）。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

以下配置允许就地编辑组件并定义 `plaintext` 作为编辑器类型：

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq：listeners {#cq-listeners}

此 `cq:listeners` 节点（节点类型） `cq:EditListenersConfig`)定义对组件执行操作之前或之后执行的操作。 下表定义了它可能的属性。

<table>
 <tbody>
  <tr>
   <td><strong>属性名称</strong></td>
   <td><strong>属性值<br /> </strong></td>
   <td><p><strong>默认值</strong></p> <p>（仅限经典UI）</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>该处理程序会在删除组件之前触发。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>处理程序在编辑组件之前触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>该处理程序在复制组件之前触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>处理程序在组件移动之前触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>处理程序会在插入组件之前触发。<br /> 仅适用于触屏UI。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>处理程序会在将组件插入另一个组件（仅限容器）之前触发。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>在删除组件后，将触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>处理程序在编辑组件后触发。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>在复制组件后，将触发处理程序。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>在插入组件后，将触发处理程序。</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>在移动组件后，将触发处理程序。</td>
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
>此 `REFRESH_INSERTED` 和 `REFRESH_SELFMOVED` 处理程序仅在经典UI中可用。

>[!NOTE]
>
>监听器的默认值仅在经典UI中设置。

>[!NOTE]
>
>对于嵌套组件，对定义为属性的 `cq:listeners` 节点：
>
>* 对于嵌套组件，以下属性的值 *必须* 是 `REFRESH_PAGE`： >
>  * `aftermove`
>  * `aftercopy`


事件处理程序可以通过自定义实施来实施。 例如(其中 `project.customerAction` 是静态方法)：

`afteredit = "project.customerAction"`

以下示例等效于 `REFRESH_INSERTED` 配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>对于经典UI，要查看哪些参数可以在处理程序中使用，请参阅 `before<action>` 和 `after<action>` 的事件部分 [ `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) 和 [ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover) 构件文档。

使用下列配置，在删除、编辑、插入或移动组件后刷新页面：

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
