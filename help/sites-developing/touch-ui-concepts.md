---
title: Adobe Experience Manager触屏优化UI的概念
description: 在Adobe Experience Manager 5.6中，Adobe为创作环境引入了新的触屏优化UI，其中带有响应式设计
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: f13ac6c2-16ab-422d-9005-ab0b49172271
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# Adobe Experience Manager触屏优化UI的概念{#concepts-of-the-aem-touch-enabled-ui}

Adobe Experience Manager (AEM)提供了触屏优化UI，其中 [响应式设计](/help/sites-authoring/responsive-layout.md) 适用于专为触摸和桌面设备设计的创作环境。

>[!NOTE]
>
>触屏优化UI是AEM的标准UI。 经典UI已在AEM 6.4中弃用。

触屏优化UI包括：

* 符合以下条件的包标头：
   * 显示徽标
   * 提供指向全局导航的链接
   * 提供指向其他通用操作的链接；例如“搜索”、“帮助”、“Experience Cloud解决方案”、“通知”和“用户设置”。
* 左侧边栏（需要时显示，可隐藏），其中可显示：
   * 时间线
   * 引用
   * 过滤器
* 导航标头，同样是上下文相关的，可以显示：
   * 指示您当前在该控制台中使用的控制台、您的位置或两者
   * 选择左侧边栏
   * 痕迹导航
   * 访问适当的 **创建** 操作
   * 查看选择
* 内容区域：
   * 列出内容项目（可以是页面、资产、论坛帖子等）
   * 可以根据请求设置格式，例如列、卡片或列表
   * 使用响应式设计（显示器根据您的设备和/或窗口大小自动调整大小）
   * 使用无限滚动（不再分页，所有项目都列在一个窗口中）

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>几乎所有的AEM功能都已移植到触屏UI。 但是，在某些有限的情况下，功能会还原为经典UI。 参见 [触屏UI功能状态](/help/release-notes/touch-ui-features-status.md) 了解更多信息。

触屏优化UI由Adobe设计，旨在为多个产品提供一致的用户体验。 它基于：

* **Coral UI** (CUI)用于触屏UI的Adobe可视化样式的实现。 Coral UI提供了您的产品/项目/Web应用程序采用UI可视化样式所需的一切。
* **Granite UI** 组件是使用Coral UI构建的。

触屏UI的基本原则包括：

* 移动优先（考虑台式机）
* 响应式设计
* 上下文相关显示
* 可重用
* 包含嵌入的参考文档
* 包含嵌入的测试
* 自下而上的设计，以确保将这些原则应用于每个元素和组件

有关触屏UI结构的更多概述，请参阅 [AEM触屏优化UI的结构](/help/sites-developing/touch-ui-structure.md).

## AEM技术栈栈 {#aem-technology-stack}

AEM使用Granite平台作为基础，Granite平台包括Java™内容存储库等。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite是Adobe的Open Web栈栈，提供各种组件，包括：

* 应用程序启动器
* 将所有内容部署到其中的OSGi框架
* 几项OSGi简编服务，用于支持建筑应用程序
* 提供各种记录API的综合记录框架
* JCR API规范的CRX存储库实施
* Apache Sling Web框架
* 当前CRX产品的其他部分

>[!NOTE]
>
>Granite作为Adobe中的一个开放开发项目运行：在整个公司中对代码、讨论和问题做出贡献。
>
>但是，Granite **非** 一个开源项目。 它在很大程度上基于多个开源项目（特别是Apache Sling、Felix、Jackrabbit和Lucene），但Adobe在公开和内部之间划出了清晰的界线。

## Granite UI {#granite-ui}

Granite工程平台还提供了基础UI框架。 其主要目标是：

* 提供粒度的UI小组件
* 实施UI概念并阐述最佳实践（长列表渲染、列表过滤、对象CRUD、CUD向导……）
* 提供可扩展且基于插件的管理UI

这些规则符合以下要求：

* 尊重“移动优先”
* 可扩展
* 易于覆盖

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[获取文件](assets/graniteui.pdf)
Granite UI：

* 使用Sling的RESTful架构
* 实施用于构建以内容为中心的Web应用程序的组件库
* 提供粒度UI小组件
* 提供默认的标准化用户界面
* 可扩展
* 专为移动设备和桌面设备而设计（首先考虑移动设备）
* 可用于任何基于Granite的平台/产品/项目；例如AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI基础组件](#granite-ui-foundation-components)
此基础组件库可由其他库使用或扩展。
* [Granite UI管理组件](#granite-ui-administration-components)

### 客户端与服务器端 {#client-side-vs-server-side}

Granite UI中的客户端 — 服务器通信由超文本组成，而不是对象，因此客户端无需理解业务逻辑

* 服务器使用语义数据丰富了HTML
* 客户端使用超媒体（交互）丰富超文本

![chlimage_1-83](assets/chlimage_1-83.png)

#### 客户端 {#client-side}

它使用HTML词汇的扩展，前提是作者可以表达构建交互式Web应用程序的意图。 这是类似于 [WAI-ARIA](https://www.w3.org/TR/wai-aria/) 和 [微格式](https://microformats.org/).

它主要由客户端上运行的JS和CSS代码所解释的一组交互模式（例如，异步提交表单）组成。 客户端的作用是增强标记（由服务器作为超媒体提供）以进行交互。

客户端独立于任何服务器技术。 只要服务器给出适当的标记，客户端就可以完成它的任务。

目前，JS和CSS代码以Granite形式交付 [clientlibs](/help/sites-developing/clientlibs.md) 在类别下：

`granite.ui.foundation and granite.ui.foundation.admin`

这些内容作为内容包的一部分提供：

`granite.ui.content`

#### 服务器端 {#server-side}

这由sling组件的集合组成，这些组件使作者能够 *撰写* Web应用程序速度很快。 开发人员开发组件，作者将组件组装为Web应用程序。 服务器端的角色是为客户端提供超媒体可用性（标记）。

目前，组件位于Granite存储库中：

`/libs/granite/ui/components/foundation`

此内容作为内容包的一部分提供：

`granite.ui.content`

### 与经典用户界面之间的差异 {#differences-with-the-classic-ui}

Granite UI和ExtJS（用于经典UI）之间的差异也值得关注：

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>远程过程调用<br /> </td>
   <td>状态转换</td>
  </tr>
  <tr>
   <td>数据传输对象</td>
   <td>超媒体</td>
  </tr>
  <tr>
   <td>客户端知道服务器内部</td>
   <td>客户端不知道内部版本</td>
  </tr>
  <tr>
   <td>“胖客户端”</td>
   <td>“瘦客户端”</td>
  </tr>
  <tr>
   <td>专用的客户端库</td>
   <td>通用客户端库</td>
  </tr>
 </tbody>
</table>

### Granite UI基础组件 {#granite-ui-foundation-components}

此 [Granite UI基础组件](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供构建任何UI所需的基本构建块。 其中包括：

* 按钮
* 超链接
* 用户头像

可以在以下位置找到基础组件：

`/libs/granite/ui/components/foundation`

此库包含每个Coral元素的Granite UI组件。 组件由内容驱动，其配置驻留在存储库中。 这使得无需手动编写HTML标记即可编写Granite UI应用程序成为可能。

用途:

* HTML元素的组件模型
* 组件组合
* 自动化单元与功能测试

实施:

* 基于存储库的构成和配置
* 使用Granite平台提供的测试设施
* JSP模板

此基础组件库可由其他库使用或扩展。

### ExtJS和相应的Granite UI组件 {#extjs-and-corresponding-granite-ui-components}

升级ExtJS代码以使用Granite UI时，以下列表提供了ExtJS xtypes和节点类型及其等效的Granite UI资源类型的方便概述。

| **ExtJS xtype** | **Granite UI资源类型** |
|---|---|
| `button` | `granite/ui/components/foundation/form/button` |
| `checkbox` | `granite/ui/components/foundation/form/checkbox` |
| `componentstyles` | `cq/gui/components/authoring/dialog/componentstyles` |
| `cqinclude` | `granite/ui/components/foundation/include` |
| `datetime` | `granite/ui/components/foundation/form/datepicker` |
| `dialogfieldset` | `granite/ui/components/foundation/form/fieldset` |
| `hidden` | `granite/ui/components/foundation/form/hidden` |
| `html5smartfile, html5smartimage` | `granite/ui/components/foundation/form/fileupload` |
| `multifield` | `granite/ui/components/foundation/form/multifield` |
| `numberfield` | `granite/ui/components/foundation/form/numberfield` |
| `pathfield, paragraphreference` | `granite/ui/components/foundation/form/pathbrowser` |
| `selection` | `granite/ui/components/foundation/form/select` |
| `sizefield` | `cq/gui/components/authoring/dialog/sizefield` |
| `tags` | `granite/ui/components/foundation/form/autocomplete``cq/gui/components/common/datasources/tags` |
| `textarea` | `granite/ui/components/foundation/form/textarea` |
| `textfield` | `granite/ui/components/foundation/form/textfield` |

| **节点类型** | **Granite UI资源类型** |
|---|---|
| `cq:WidgetCollection` | `granite/ui/components/foundation/container` |
| `cq:TabPanel` | `granite/ui/components/foundation/container``granite/ui/components/foundation/layouts/tabs` |
| `cq:panel` | `granite/ui/components/foundation/container` |

### Granite UI管理组件 {#granite-ui-administration-components}

此 [Granite UI管理组件](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 构建于基础组件之上，以提供任何管理应用程序都可以实施的通用构建块。 其中包括：

* 全局导航栏
* 边栏（骨架）
* 搜索面板

用途:

* 管理应用程序的统一外观
* 管理应用程序的RAD

实施:

* 使用基础组件的预定义组件
* 组件可以自定义

## Coral UI {#coral-ui}

CoralUI.pdf

[获取文件](assets/coralui.pdf)
Coral UI (CUI)是触屏UI中Adobe视觉样式的实现，旨在为多个产品提供一致的用户体验。 Coral UI提供了采用创作环境中使用的视觉样式所需的一切。

>[!CAUTION]
>
>Coral UI是一种UI库，可供AEM客户在其获得产品使用许可的范围内构建应用程序和Web界面。
>
>仅允许使用Coral UI：
>
>
>* 当它与AEM一起发运和捆绑时。
>* 在扩展创作环境的现有UI时使用。
>* Adobe企业宣传资料、广告和演示。
>* Adobe品牌应用程序的UI（字体不能随时用于其他用途）。
>* 进行细微自定义。
>
>应避免在以下位置使用Coral UI：
>
>* 与Adobe无关的文档和其他项目。
>* 内容创建环境（其中前述项目可能由其他人生成）。
>* 未明确连接到Adobe的应用程序/组件/网页。
>

Coral UI是开发Web应用程序的构建块集合。

![chlimage_1-84](assets/chlimage_1-84.png)

每个模块从一开始就设计为模块化，根据其主要角色构成一个不同的层。 尽管这些层的设计目的是相互支持，但如果需要，也可以单独使用这些层。 这使您能够在任何支持HTML的环境中实施Coral的用户体验。

使用Coral UI时，不必使用特定的开发模型和/或平台。 Coral的主要目标是提供统一且干净的HTML5标记，这与用于发出此标记的实际方法无关。 这可以用于客户端或服务器端渲染、模板、JSP、PHP甚至AdobeFlashRIA应用程序 — 仅举几例。

### HTML元素 — 标记层 {#html-elements-the-markup-layer}

HTML元素为所有基本UI元素（包括导航栏、按钮、菜单、边栏等）提供共同的外观。

在最基本的级别上，HTML元素是具有专用类名称的HTML标记。 更复杂的元素可以由多个标签组成，它们彼此嵌套（以特定方式）。

CSS用于提供实际的外观。 为了能够轻松自定义外观（例如，对于品牌策略），实际样式值声明为变量，变量由 [更少](https://lesscss.org/) 运行期间的预处理器。

用途:

* 提供具有通用外观的基本用户界面元素
* 提供默认网格系统

实施:

* 具有灵感源于以下样式的标记HTML： [Bootstrap](https://twitter.github.com/bootstrap/)
* 类在LESS文件中定义
* 图标被定义为字体脚本

例如，标记：

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

显示为：

![chlimage_1-85](assets/chlimage_1-85.png)

look-and-feel在LESS中定义，通过专用类名绑定到元素（为了简洁起见，已缩短以下提取）：

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

实际值在LESS变量文件中定义（为了简洁起见，已缩短以下提取）：

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 元素插件 {#element-plugins}

许多HTML元素需要表现出某种动态行为，例如打开和关闭弹出菜单。 这是元素插件的作用，这些插件通过使用JavaScript操作DOM来完成此类任务。

插件包括：

* 设计用于操作特定的DOM元素。 例如，对话框插件应找到 `DIV class=dialog`
* 本质上是通用的。 例如，布局管理器为任何列表提供布局 `DIV` 或 `LI` 元素

插件行为可通过以下任一方式使用参数自定义：

* 通过JavaScript调用传递参数
* 使用专用 `data-*` 与HTML标记关联的属性

尽管开发人员可以为任何插件选择最佳方法，但经验法则是使用：

* `data-*` 与HTML布局相关的选项的属性。 例如，指定列数
* 用于与数据相关的功能的API选项/类。 例如，构建要显示的项目列表

使用相同的概念来实施表单验证。 对于要验证的元素，必须将所需的输入表单指定为自定义 `data-*` 属性。 此属性随后用作验证插件的选项。

>[!NOTE]
>
>应尽可能使用HTML5本机表单验证和/或对其进行扩展。

用途:

* 为HTML元素提供动态行为
* 提供纯CSS无法提供的自定义布局
* 执行表单验证
* 执行高级DOM操作

实施:

* jQuery插件，绑定到特定的DOM元素
* 使用 `data-*` 用于自定义行为的属性

示例标记的提取(请注意指定为数据的选项 — &#42; 属性)：

```xml
<ul data-column-width="220" data-layout="card" class="cards">
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
          <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
  <li class="item">
    <div class="thumbnail">
      <img href="/a.html" src="/a.thumb.319.319..png">
      <div class="caption">
        <h4>Toolbar</h4>
        <p><small>toolbar</small><br></p>
      </div>
    </div>
  </li>
```

对jQuery插件的调用：

```
$('.cards').cardlayout ();
```

这显示为：

![chlimage_1-86](assets/chlimage_1-86.png)

此 `cardLayout` 插件列出了包含的 `UL` 元素，并考虑父项的宽度。

### HTML元素小组件 {#html-elements-widgets}

构件将一个或多个基本元素与JavaScript插件组合在一起，形成“更高级别”的UI元素。 这些元素可以实施比单个元素所能提供的更复杂的行为和更复杂的外观。 标记选取器或边栏构件就是一个很好的示例。

小组件可以触发和侦听自定义事件，以与页面上的其他小组件协作。 某些构件是使用CoralHTML元素的本机jQuery构件。

用途:

* 实施展示复杂行为的更高级别UI元素
* 触发和处理事件

实施:

* jQuery插件+HTML标记
* 可以使用客户端/服务器端模板

示例标记为：

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

对jQuery插件的调用（使用选项）：

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

插件会发送HTML标记（此标记使用基本元素，这些元素可能在内部使用其他插件）：

```
<span>Pisa</code>
<a title="Removing tag" tagidtoremove="0"
   id="myRemover_0" class="myTagRemover" href="#">x</a></code>

<span id="myTag_1" class="myTag"><span>Rome</code>
<a title="Removing tag" tagidtoremove="1"
   id="myRemover_1" class="myTagRemover" href="#">x</a></code>

<input type="text" data-original-title="" class="input-medium tagManager"
       placeholder="Tags" name="tags" data-provide="typeahead" data-items="6"
       autocomplete="off">
```

这显示为：

![chlimage_1-87](assets/chlimage_1-87.png)

### 实用程序库 {#utility-library}

此库是以下JavaScript帮助程序插件和/或函数的集合：

* 独立于UI
* 但对于构建功能齐全的Web应用程序而言，这一点至关重要

其中包括XSS处理和事件总线。

虽然HTML元素插件和小组件可能依赖于实用程序库提供的功能，但实用程序库无法硬依赖这些元素或小组件本身。

用途:

* 提供常用功能
* 事件总线实现
* 客户端模板
* XSS

实施:

* jQuery插件或符合AMD标准的JavaScript模块
