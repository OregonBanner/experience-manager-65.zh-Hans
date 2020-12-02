---
title: AEM触屏优化UI的概念
seo-title: AEM触屏优化UI的概念
description: 借助AEM 5.6Adobe，为创作环境引入了具有响应式设计的全新触屏优化UI
seo-description: 借助AEM 5.6Adobe，为创作环境引入了具有响应式设计的全新触屏优化UI
uuid: 401c5a65-6ddc-4942-ab8e-395016f9c629
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: df3aaed1-97b5-4a4a-af74-cb887462475b
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 0%

---


# AEM触屏优化UI的概念{#concepts-of-the-aem-touch-enabled-ui}

AEM为创作环境提供了触屏优化UI，该UI具有[响应式设计](/help/sites-authoring/responsive-layout.md)，设计用于在触控和桌面设备上运行。

>[!NOTE]
>
>触屏优化UI是AEM的标准UI。 AEM 6.4已弃用经典UI。

触屏优化UI包括：

* 包标题：
   * 显示徽标
   * 提供指向全局导航的链接
   * 提供指向其他通用操作的链接；例如搜索、帮助、Marketing Cloud解决方案、通知和用户设置。
* 左边栏（根据需要显示并可隐藏），可显示：
   * 时间轴
   * 引用
   * 筛选器
* 导航标题，它同样与上下文相关，可显示：
   * 指示您当前使用的控制台和／或该控制台中的位置
   * 选择左边栏
   * 痕迹导航
   * 访问相应的&#x200B;**创建**&#x200B;操作
   * 视图选择
* 内容区域：
   * 列表内容项（包括页面、资产、论坛帖子等）
   * 可以按照请求设置格式，如列、卡或列表
   * 使用响应式设计（显示屏根据您的设备和／或窗口大小自动调整大小）
   * 使用无限滚动（不再分页，所有项目都在一个窗口中列出）

![chlimage_1-79](assets/chlimage_1-79.png)

>[!NOTE]
>
>几乎所有AEM功能都移植到触屏优化UI。 但是，在某些有限情况下，功能将恢复到经典UI。 有关详细信息，请参阅[触屏UI功能状态](/help/release-notes/touch-ui-features-status.md)。

触屏优化UI由Adobe设计，可跨多个产品提供一致的用户体验。 它基于：

* **Coral UI** (CUI)是Adobe在触屏优化UI中的可视样式的实现。Coral UI提供您的产品／项目/Web应用程序采用UI可视样式所需的一切。
* **Granite** UI组件是使用Coral UI构建的。

触屏优化UI的基本原则是：

* 移动优先（以桌面为中心）
* 响应式设计
* 上下文相关显示
* 可重用
* 包含嵌入的参考文档
* 包含嵌入测试
* 自下而上的设计，确保将这些原则应用于每个元素和组件

有关触屏优化UI结构的进一步概述，请参阅文章[AEM触屏优化UI结构](/help/sites-developing/touch-ui-structure.md)。

## AEM技术堆栈{#aem-technology-stack}

AEM以Granite平台为基础，Granite平台包括Java内容存储库等。

![chlimage_1-80](assets/chlimage_1-80.png)

## Granite {#granite}

Granite是Adobe的Open Web堆栈，提供各种组件，包括：

* 应用程序启动器
* 一个OSGi框架，其中部署了所有内容
* 支助建筑申请的若干OSGi简编服务
* 提供各种日志记录API的全面日志记录框架
* JCR API规范的CRX存储库实现
* Apache Sling Web Framework
* 当前CRX产品的其他部件

>[!NOTE]
>
>Granite在Adobe内作为开放开发项目运行：在整个公司对准则、讨论和问题作出贡献。
>
>但是，Granite是&#x200B;**不**&#x200B;一个开放源项目。 它主要基于几个开放源码项目（特别是Apache Sling、Felix、Jackrabbit和Lucene），但Adobe在公开内容和内部内容之间划出了清晰的界限。

## Granite UI {#granite-ui}

Granite工程平台还提供一个基础UI框架。 其主要目标是：

* 提供精细的UI构件
* 实施UI概念并说明最佳实践(长列表渲染、列表过滤、对象CRUD、CUD向导……)
* 提供基于扩展和插件的管理UI

这些要求符合：

* 尊重“移动优先”
* 可扩展
* 易于覆盖

![chlimage_1-81](assets/chlimage_1-81.png)
GraniteUI.pdf

[获取](assets/graniteui.pdf)
文件Granite UI:

* 使用Sling的REST风格架构
* 实现用于构建以内容为中心的Web应用程序的组件库
* 提供精细的UI构件
* 提供默认的标准化UI
* 可扩展
* 专为移动和桌面设备设计（首先考虑移动）
* 可用于任何基于Granite的平台／产品／项目；eg AEM

![chlimage_1-82](assets/chlimage_1-82.png)

* [Granite UI Foundation组](#granite-ui-foundation-components)
件此基础组件库可由其他库使用或扩展。
* [Granite UI管理组件](#granite-ui-administration-components)

### 客户端与服务器端{#client-side-vs-server-side}

Granite UI中的客户端与服务器通信由超文本而非对象组成，因此客户端无需了解业务逻辑

* 服务器丰富了HTML语义数据
* 客户端通过超媒体（交互）丰富超文本

![chlimage_1-83](assets/chlimage_1-83.png)

#### 客户端{#client-side}

它使用HTML词汇的扩展，以便作者能够表达他们构建交互式Web应用程序的意图。 这是对[WAI-ARIA](https://www.w3.org/TR/wai-aria/)和[microformats](https://microformats.org/)的类似方法。

它主要由在客户端运行的由JS和CSS代码解释的交互模式集合（例如，异步提交表单）组成。 客户端的作用是增强交互性标记（作为服务器提供的超媒体）。

客户端独立于任何服务器技术。 只要服务器提供适当的标记，客户端就可以完成其角色。

目前，JS和CSS代码以Granite [clientlibs](/help/sites-developing/clientlibs.md)形式在类别下传送：

`granite.ui.foundation and granite.ui.foundation.admin`

这些内容作为内容包的一部分提供：

`granite.ui.content`

#### 服务器端{#server-side}

它由sling组件集合组成，这些组件使作者能够快速&#x200B;*组合* Web应用程序。 开发人员开发组件，作者将组件组装成Web应用程序。 服务器端的作用是为客户端提供超媒体支持（标记）。

当前，这些组件位于Granite存储库中：

`/libs/granite/ui/components/foundation`

它作为内容包的一部分提供：

`granite.ui.content`

### 与经典UI {#differences-with-the-classic-ui}的区别

Granite UI与ExtJS（用于经典UI）之间的区别也值得关注：

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
   <td>Hypermedia</td>
  </tr>
  <tr>
   <td>客户端了解服务器内部信息</td>
   <td>客户端不知道内部信息</td>
  </tr>
  <tr>
   <td>“胖客户”</td>
   <td>"瘦客户端"</td>
  </tr>
  <tr>
   <td>专用客户端库</td>
   <td>通用客户端库</td>
  </tr>
 </tbody>
</table>

### Granite UI基础组件{#granite-ui-foundation-components}

[Granite UI基础组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)提供构建任何UI所需的基本构建块。 其中包括：

* 按钮
* 超链接
* 用户头像

基础组件位于：

`/libs/granite/ui/components/foundation`

此库包含每个Coral元素的Granite UI组件。 组件是内容驱动的，其配置驻留在存储库中。 这样，无需手工编写HTML标记即可构建Granite UI应用程序。

用途:

* HTML元素的组件模型
* 组分组合
* 自动单元和功能测试

实施:

* 基于存储库的合成和配置
* 利用Granite平台提供的测试设施
* JSP模板

此基础组件库可由其他库使用或扩展。

### ExtJS和相应的Granite UI组件{#extjs-and-corresponding-granite-ui-components}

升级ExtJS代码以使用Granite UI时，以下列表将提供ExtJS xtypes和节点类型与其等效的Granite UI资源类型的便捷概述。

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

### Granite UI管理组件{#granite-ui-administration-components}

[Granite UI管理组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)构建于基础组件上，以提供任何管理应用程序都可以实现的通用构建块。 其中包括：

* 全局导航栏
* 边栏（骨架）
* 搜索面板

用途:

* 管理应用程序的统一外观
* RAD管理应用程序

实施:

* 使用基础组件的预定义组件
* 可以自定义组件

## Coral UI {#coral-ui}

CoralUI.pdf

[Get ](assets/coralui.pdf)
FileCoral UI(CUI)是Adobe对触屏优化UI的视觉风格的实现，旨在提供跨多个产品的用户体验的一致性。Coral UI提供采用创作环境中使用的可视样式所需的一切。

>[!CAUTION]
>
>Coral UI是一个UI库，可供AEM客户在许可产品使用范围内构建应用程序和Web界面。
>
>仅允许使用Coral UI:
>
>
>* 当它已装运并与AEM捆绑在一起时。
>* 用于扩展创作环境的现有UI。
>* Adobe公司宣传资料、广告和演示。
>* Adobe品牌应用程序的UI（字体不能随时供其他使用）。
>* 具有少量自定义。

>
>
应避免在以下位置使用Coral UI:
>
>* 文档和其他与Adobe无关的项目。
>* 内容创建环境符（前面的项目可能由其他人生成）。
>* 未明确连接到Adobe的应用程序／组件／网页。

>



Coral UI是用于开发Web应用程序的构件块的集合。

![chlimage_1-84](assets/chlimage_1-84.png)

设计为从开始模块化，每个模块根据其主要角色形成一个不同的层。 尽管这些图层设计为相互支持，但也可以根据需要单独使用它们。 这使得在任何支持HTML的环境中实施Coral的用户体验成为可能。

对于Coral UI，不必使用特定开发模型和／或平台。 Coral的主要目标是提供统一、清晰的HTML5标记，与发出此标记的实际方法无关。 这可能用于客户端或服务器端渲染、模板、JSP、PHP，甚至AdobeFlashRIA应用程序——只有几个。

### HTML元素——标记层{#html-elements-the-markup-layer}

HTML元素为所有基本UI元素（包括导航栏、按钮、菜单、边栏等）提供了通用的外观。

在最基本的级别上，HTML元素是具有专用类名的HTML标签。 更复杂的元素可以由多个标签组成，它们彼此嵌套在一起（以特定方式）。

CSS用于提供实际的外观。 为了便于自定义外观（例如，对于品牌），实际样式值声明为变量，在运行时期间由[LESS](https://lesscss.org/)预处理器展开。

用途:

* 为基本UI元素提供通用的外观
* 提供默认网格系统

实施:

* 具有由[bootstrap](https://twitter.github.com/bootstrap/)启发的样式的HTML标签
* 类在LESS文件中定义
* 图标定义为字体精灵

例如，标记：

```xml
<button class="btn btn-large btn-primary" type="button">Large button</button>
<button class="btn btn-large" type="button">Large button</button>
```

显示为：

![chlimage_1-85](assets/chlimage_1-85.png)

外观在LESS中定义，它通过专用的类名与元素绑定（为简便起见，以下提取已缩短）:

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

### 元素插件{#element-plugins}

许多HTML元素需要显示某种动态行为，如打开和关闭弹出菜单。 这是元素插件的角色，它们通过使用JavaScript操作DOM来完成此类任务。

插件为：

* 设计为在特定DOM元素上操作。 例如，对话框插件需要查找`DIV class=dialog`
* 自然通用。 例如，布局管理器为`DIV`或`LI`元素的任何列表提供布局

可以通过以下任一方式使用参数自定义插件行为：

* 通过javascript调用传递参数
* 使用与HTML标记关联的专用`data-*`属性

尽管开发人员可以为任何插件选择最佳方法，但经验法则是：

* `data-*` 与HTML布局相关的选项的属性。例如，要指定列数
* 与数据相关的功能的API选项／类。 例如，构建要显示的项的列表

同样的概念用于实现表单验证。 对于要验证的元素，必须将所需的输入表单指定为自定义`data-*`属性。 然后，此属性将用作验证插件的选项。

>[!NOTE]
>
>应尽可能使用HTML5本机表单验证和／或展开验证。

用途:

* 为HTML元素提供动态行为
* 提供纯CSS无法实现的自定义布局
* 执行表单验证
* 执行高级DOM处理

实施:

* jQuery插件，绑定到特定DOM元素
* 使用`data-*`属性自定义行为

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

此操作将显示为：

![chlimage_1-86](assets/chlimage_1-86.png)

`cardLayout`插件根据各元素的高度布局包含的`UL`元素，并考虑父元素的宽度。

### HTML元素构件{#html-elements-widgets}

构件将一个或多个基本元素与javascript插件组合，以形成“更高级别”的UI元素。 这些元素可以实现比单个元素更复杂的行为，也可以实现更复杂的外观。 例如，标签选取器或边栏构件。

构件可以触发和侦听自定义事件以与页面上的其他构件配合。 某些构件实际上是使用Coral HTML元素的原生jQuery构件。

用途:

* 实现表现复杂行为的更高级别UI元素
* 触发和处理事件

实施:

* jQuery插件+ HTML标记
* 可以利用客户端／服务器端模板

标记示例为：

```
<input type="text" name="tags" placeholder="Tags" class="tagManager"/>
```

对jQuery插件的调用（带有选项）:

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

此操作将显示为：

![chlimage_1-87](assets/chlimage_1-87.png)

### 实用程序库{#utility-library}

此库是javascript帮助程序插件和／或函数的集合，这些插件和／或函数包括：

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
