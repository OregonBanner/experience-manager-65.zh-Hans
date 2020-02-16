---
title: AEM触屏优化UI的概念
seo-title: AEM触屏优化UI的概念
description: 借助AEM 5.6,Adobe引入了新的触屏优化UI，该UI具有针对创作环境的响应式设计
seo-description: 借助AEM 5.6,Adobe引入了新的触屏优化UI，该UI具有针对创作环境的响应式设计
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# AEM触屏优化UI的概念{#concepts-of-the-aem-touch-enabled-ui}

AEM提供触屏优化UI，该UI为创作环 [境提供响应式设计](/help/sites-authoring/responsive-layout.md) ，设计用于在触控和桌面设备上运行。

>[!NOTE]
>
>触屏优化UI是AEM的标准UI。 经典UI在AEM 6.4中已弃用。

触屏优化UI包括：

* 包标题：
   * 显示徽标
   * 提供指向全局导航的链接
   * 提供指向其他通用操作的链接；例如搜索、帮助、Marketing cloud解决方案、通知和用户设置。
* 左边栏（根据需要显示并可隐藏），可显示：
   * 时间轴
   * 引用
   * 筛选器
* 导航标题，它同样与上下文相关，并且可显示：
   * 指示您当前使用的控制台和／或该控制台中的位置
   * 选择左边栏
   * 痕迹导航
   * 访问相应的创 **建操作**
   * 查看选择
* 内容区域：
   * 列出内容项（无论是页面、资产、论坛帖子等）
   * 可以按照请求设置格式，例如列、卡或列表
   * 使用响应式设计（显示屏会根据您的设备和／或窗口大小自动调整大小）
   * 使用无限滚动（不再分页，所有项目都在一个窗口中列出）

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>几乎所有AEM功能都已移植到触屏优化UI。 但是，在某些有限情况下，功能将恢复到经典UI。 有关更 [多信息，请参阅触屏](/help/release-notes/touch-ui-features-status.md) UI功能状态。

触屏优化UI由Adobe设计，旨在提供跨多个产品的用户体验的一致性。 它基于：

* **Coral UI** (CUI)是对触屏优化UI实现Adobe的可视样式。 Coral UI提供您的产品／项目/ web应用程序采用UI可视样式所需的一切。
* **Granite UI组件** 是使用Coral UI构建的。

触屏优化UI的基本原理是：

* 移动优先（考虑桌面）
* 响应式设计
* 上下文相关显示
* 可重用
* 包括嵌入的参考文档
* 包括嵌入测试
* 自下而上的设计确保这些原则适用于每个元素和组件

有关触屏优化UI结构的进一步概述，请参阅 [AEM触屏优化UI的结构文章](/help/sites-developing/touch-ui-structure.md)。

## AEM技术堆栈 {#aem-technology-stack}

AEM将Granite平台用作基础，Granite平台包括Java内容存储库等。

![chlimage_1-80](assets/chlimage_1-80.png)

## 花岗岩 {#granite}

Granite是Adobe的Open web堆栈，提供包括：

* 应用程序启动器
* 一个OSGi框架，其中部署了所有内容
* 支助建筑应用的若干OSGi简编服务
* 提供各种日志记录API的全面日志记录框架
* JCR API规范的CRX存储库实现
* Apache Sling web框架
* 当前CRX产品的其他部分

>[!NOTE]
>
>Granite在Adobe内作为开放开发项目运行：对代码、讨论和问题的贡献来自整个公司。
>
>但是，Granite不 **是开** 放源项目。 它主要基于几个开放源码项目（特别是Apache Sling、Felix、Jackrabbit和Lucene），但Adobe在公开内容与内部内容之间划出了明确的界限。

## Granite UI {#granite-ui}

Granite工程平台还提供了基础UI框架。 其主要目标是：

* 提供粒度级UI构件
* 实施UI概念并说明最佳实践（长列表渲染、列表筛选、对象CRUD、CUD向导……）
* 提供基于扩展和插件的管理UI

这些要求符合：

* 尊重“移动优先”
* 可扩展
* 易于覆盖

![chlimage_1-81](assets/chlimage_1-81.png)GraniteUI.pdf

[获取文件](assets/graniteui.pdf)Granite UI:

* 使用Sling的REST风格架构
* 实施用于构建以内容为中心的Web应用程序的组件库
* 提供粒度级UI构件
* 提供默认的标准化UI
* 可扩展
* 专为移动和桌面设备设计（首先考虑移动）
* 可用于任何基于Granite的平台／产品／项目；eg AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI基础组件](#granite-ui-foundation-components)此基础组件库可由其他库使用或扩展。
* [Granite UI管理组件](#granite-ui-administration-components)

### 客户端与服务器端 {#client-side-vs-server-side}

Granite UI中的客户端与服务器通信由超文本而非对象组成，因此客户端无需了解业务逻辑

* 服务器丰富了语义数据的HTML
* 客户端通过超媒体（交互）丰富超文本

![chlimage_1-83](assets/chlimage_1-83.png)

#### Client-Side {#client-side}

它使用HTML词汇的扩展，以便作者能够表达他们构建交互式Web应用程序的意图。 这与WAI-ARIA和微格 [式类似](https://www.w3.org/TR/wai-aria/) , [也相似](https://microformats.org/)。

它主要由一组交互模式（例如，异步提交表单）组成，这些模式由JS和CSS代码解释，在客户端运行。 客户端的作用是增强交互性的标记（作为服务器提供的超媒体）。

客户端独立于任何服务器技术。 只要服务器给出相应的标记，客户端就可以完成其角色。

目前，JS和CSS代码作为Granite [clientlibs交付](/help/sites-developing/clientlibs.md) ，位于类别下：

`granite.ui.foundation and granite.ui.foundation.admin`

这些内容作为内容包的一部分提供：

`granite.ui.content`

#### 服务器端 {#server-side}

这由使作者能快速构建Web应用程序的一组sling *组件* 构成。 开发人员开发组件，作者将组件组合为网络应用程序。 服务器端的角色是为客户端提供超媒体支持（标记）。

当前，这些组件位于Granite存储库中：

`/libs/granite/ui/components/foundation`

它作为内容包的一部分提供：

`granite.ui.content`

### 与经典UI的区别 {#differences-with-the-classic-ui}

Granite UI与ExtJS（用于经典UI）之间的差异也值得关注：

<table>
 <tbody>
  <tr>
   <td><strong>ExtJS</strong></td>
   <td><strong>Granite UI</strong></td>
  </tr>
  <tr>
   <td>远程过程调用<br /> </td>
   <td>状态过渡</td>
  </tr>
  <tr>
   <td>数据传输对象</td>
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>客户端了解服务器内部</td>
   <td>客户端不知道内部信息</td>
  </tr>
  <tr>
   <td>“胖客户”</td>
   <td>“瘦客户端”</td>
  </tr>
  <tr>
   <td>专用客户端库</td>
   <td>通用客户端库</td>
  </tr>
 </tbody>
</table>

### Granite UI基础组件 {#granite-ui-foundation-components}

Granite UI基 [础组件提供构建任何UI所需的基本构建块](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 。 其中包括：

* 按钮
* 超链接
* 用户头像

基础组件位于：

`/libs/granite/ui/components/foundation`

此库包含每个Coral元素的Granite UI组件。 组件是内容驱动的，其配置驻留在存储库中。 这使得无需手工编写HTML标记即可构建Granite UI应用程序。

用途:

* HTML元素的组件模型
* 组分组合物
* 自动单元和功能测试

实施:

* 基于存储库的合成和配置
* 利用Granite平台提供的测试设施
* JSP模板

此基础组件库可由其他库使用或扩展。

### ExtJS和相应的Granite UI组件 {#extjs-and-corresponding-granite-ui-components}

将ExtJS代码升级为使用Granite UI时，以下列表将方便地概述ExtJS xtypes和节点类型及其等效的Granite UI资源类型。

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

Granite UI管 [理组件构建于基础组件之上](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) ，以提供任何管理应用程序都可以实现的通用构建块。 其中包括：

* 全局导航栏
* 边栏（骨架）
* 搜索面板

用途:

* 管理应用程序的统一外观
* 管理应用程序的RAD

实施:

* 使用基础组件的预定义组件
* 可以自定义组件

## Coral UI {#coral-ui}

CoralUI.pdf

[Get File](assets/coralui.pdf)Coral UI(CUI)是Adobe针对触屏优化UI的可视样式的实现，旨在提供跨多个产品的一致用户体验。 Coral UI提供了采用创作环境中使用的可视样式所需的一切。

>[!CAUTION]
>
>Coral UI是AEM客户提供的一个UI库，用于在他们许可的产品使用范围内构建应用程序和Web界面。
>
>仅允许使用Coral UI:
>
>
>* 当它已装运并与AEM捆绑时。
>* 用于在扩展创作环境的现有UI时使用。
>* Adobe公司附属品、广告和演示文稿。
>* Adobe品牌应用程序的UI（字体不得随时用于其他用途）。
>* 具有较小的自定义。
>
>
应避免在以下位置使用Coral UI:
>
>* 文档和其他与Adobe无关的项目。
>* 内容创建环境（其中前面的项目可能由其他人生成）。
>* 未明确连接到Adobe的应用程序／组件／网页。
>



Coral UI是用于开发Web应用程序的构件块的集合。

![chlimage_1-84](assets/chlimage_1-84.png)

设计为从开始起就是模块化的，每个模块根据其主要角色形成一个不同的层。 尽管这些图层设计为相互支持，但也可以根据需要单独使用它们。 这使得在任何支持HTML的环境中实施Coral的用户体验成为可能。

在Coral UI中，不必使用特定开发模型和／或平台。 Coral的主要目标是提供统一、简洁的HTML5标记，与发出此标记的实际方法无关。 这可能用于客户端或服务器端渲染、模板、JSP、PHP甚至Adobe Flash RIA应用程序——只是几个。

### HTML元素——标记层 {#html-elements-the-markup-layer}

HTML元素为所有基本UI元素（包括导航栏、按钮、菜单、边栏等）提供通用的外观。

在最基本的级别上，HTML元素是具有专用类名的HTML标签。 更复杂的元素可以由多个彼此嵌套在一起（以特定方式）的标签组成。

CSS用于提供实际的外观。 为了便于自定义外观（例如，对于品牌），实际样式值声明为变量，由 [LESS](https://lesscss.org/) 预处理器在运行时扩展。

用途:

* 为基本UI元素提供通用的外观
* 提供默认网格系统

实施:

* HTML标签，其样式灵感来自bootstrap [](https://twitter.github.com/bootstrap/)
* 类在LESS文件中定义
* 图标定义为字体精灵

例如，标记：

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

显示为：

![chlimage_1-85](assets/chlimage_1-85.png)

外观在LESS中定义，它通过专用的类名称绑定到元素（为简便起见，以下提取已缩短）:

```xml
.btn {
    font-size: @baseFontSize;
    line-height: @baseLineHeight;
    .buttonBackground(@btnBackground,
                                @btnBackgroundHighlight,
                                @grayDark, 0 1px 1px rgba(255,255,255,.75));
```

实际值在LESS变量文件中定义（为了简便起见，以下提取已缩短）:

```xml
@btnBackgroundHighlight: darken(@white, 10%);
@btnPrimaryBackgroundHighlight: spin(@btnPrimaryBackground, 20%);
@baseFontSize: 17px;
@baseFontFamily: @sansFontFamily;
```

### 元素插件 {#element-plugins}

许多HTML元素需要表现出某种动态行为，如打开和关闭弹出菜单。 这是元素插件的角色，它通过使用JavaScript操作DOM来完成此类任务。

插件可以是：

* 设计为在特定DOM元素上操作。 例如，对话框插件需要查找 `DIV class=dialog`
* 自然通用。 例如，布局管理器为任何元素列表提供 `DIV` 布 `LI` 局

可以通过以下任一方式使用参数自定义插件行为：

* 通过javascript调用传递参数
* 使用与HTML `data-*` 标记绑定的专用属性

尽管开发人员可以为任何插件选择最佳方法，但经验法则是：

* `data-*` 与HTML布局相关的选项的属性。 例如，要指定列数
* API选项／类，用于与数据相关的功能。 例如，构建要显示的项目列表

同样的概念用于实现表单验证。 对于要验证的元素，必须将所需的输入表单指定为自定义属 `data-*` 性。 然后，此属性将用作验证插件的选项。

>[!NOTE]
>
>应尽可能使用HTML5本机表单验证和／或在验证时进行扩展。

用途:

* 为HTML元素提供动态行为
* 提供纯CSS无法实现的自定义布局
* 执行表单验证
* 执行高级DOM操作

实施:

* jQuery插件，绑定到特定DOM元素
* 使用 `data-*` 属性自定义行为

示例标记的提取（请注意指定为data-*属性的选项）:

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

调用jQuery插件：

```
$(‘.cards’).cardlayout ();
```

这将显示为：

![chlimage_1-86](assets/chlimage_1-86.png)

插 `cardLayout` 件根据各个元素的高 `UL` 度来布局包含的元素，并考虑到父元素的宽度。

### HTML Elements构件 {#html-elements-widgets}

小部件将一个或多个基本元素与javascript插件组合在一起，以形成“更高级别”的UI元素。 这些功能可以实现比单个元素更复杂的行为以及更复杂的外观。 例如，标签选取器或边栏构件。

构件可以触发和侦听自定义事件以与页面上的其他构件合作。 某些构件实际上是使用Coral HTML元素的原生jQuery构件。

用途:

* 实现表现复杂行为的更高级别UI元素
* 触发和处理事件

实施:

* jQuery plugin + HTML标记
* 可以利用客户端／服务器端模板

示例标记为：

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

调用jQuery插件（带有选项）:

```
$(".tagManager").tagsManager({
        prefilled: ["Pisa", "Rome"] })
```

插件发出HTML标记（此标记使用基本元素，这些元素可能在内部使用其他插件）:

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

这将显示为：

![chlimage_1-87](assets/chlimage_1-87.png)

### 实用程序库 {#utility-library}

此库是Javascript Helper插件和／或函数的集合，这些插件和／或函数包括：

* UI独立
* 但对于构建功能齐备的Web应用程序至关重要

这包括XSS处理和事件总线。

尽管HTML元素插件和构件可能依赖于实用程序库提供的功能，但实用程序库不能对元素和构件本身有任何硬依赖性。

用途:

* 提供通用功能
* 事件总线实现
* 客户端模板
* XSS

实施:

* jQuery插件或符合AMD规范的JavaScript模块
