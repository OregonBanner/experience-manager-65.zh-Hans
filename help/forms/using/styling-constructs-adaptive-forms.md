---
title: 自适应表单的样式结构
description: 使用LESS框架自定义自适应表单的外观。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: 691608a6-be82-4d81-b876-427de997e5be
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2348'
ht-degree: 5%

---

# 自适应表单的样式结构{#styling-constructs-for-adaptive-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 前提条件 {#prerequisites}

了解CSS和LESS框架。

## 可自定义的内容 {#what-can-be-customized}

本文列出了自适应表单的公开可用css类。 您可以使用这些类设置自适应表单各种组件的样式。 创作组件（如显示警告的对话框和状态栏）的样式超出了本文的范围。 仅当您无法通过以下方式设置组件的样式时，才使用这些样式构造创建样式（使用CSS或更少）： [主题编辑器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## 在自适应表单中自定义样式 {#customizing-styles-in-adaptive-forms}

LESS框架简化了自定义自适应表单中样式的用例。 该框架允许您使用一组变量和函数(mixin)定义样式。 LESS框架有助于减小捆绑代码的大小并提高其可重用性。

您可以通过以下方式自定义自适应表单样式：

* 更改主题
* 更改组件的样式

## 更改主题 {#changing-theme}

您可以更改自适应表单的主题，以确保其外观与嵌入了自适应表单的网页一致。

使用CSS属性更改自适应表单的整体外观通常是主题更改的一部分。 对自适应表单的“确定和感觉”所做的重大更改（如组件布局和放置的更改）不被视为主题更改。

根据引导，以下几组CSS属性定义了网页的主题：

* 背景颜色
* 边框（类型、颜色、粗细）
* 字体颜色
* 边距
* 边距
* 字体大小
* 行高

目前，仅针对自适应表单中各种元素的这些属性定义了LESS变量。

## 更改组件样式 {#changing-component-style}

可更改元素的外观、布局、位置和可见性。 要完成此任务，请创建或更新您的自定义.css文件，以包含本文中列出的样式构造。

要将样式应用于自适应表单，请在中打开自适应表单进行编辑，打开自适应表单容器的属性，在基本选项卡中指定自定义CSS文件的路径。 自适应表单的样式构造是默认的，并且被自定义.css文件中列出的构造覆盖。

## 组件 {#components}

本文中讨论的组件具有预定义的CSS类。 您可以编辑变量以修改CSS类中的样式。 或者，您可以重写整个类。 本节介绍可以使用变量修改的组件和样式中的类。

## 容器样式 {#container-styling}

容器是顶级组件。 其他面板和字段位于容器组件下。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量说明</strong></p> </td>
   <td><p><strong>变量说明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>容器的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>容器的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>容器的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字体颜色</p> </td>
  </tr>
 </tbody>
</table>

## 字段样式 {#field-styling}

自适应表单包括各种类型的字段。 每个字段都有一个唯一的类名称，即字段的名称。 该字段还具有公共类名称 `guideFieldNode`.

字段包括标签、小组件、帮助描述（长描述和短描述）和字段帮助图标（问号）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>字段的内边距</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>字段错误消息的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>字段错误消息的字体大小</p> </td>
  </tr>
 </tbody>
</table>

## 标签样式 {#label-styling}

HTML元素 **标签** 用于字段包括类 **左侧** 或 **top** 标签在顶部还是左侧。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>字段标签的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>字段标签的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>字段标签的CSS行高属性 </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>字段标签的CSS字体粗细属性 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>字段标签的边距</p> </td>
  </tr>
 </tbody>
</table>

使用以下方式应用标签的CSS规则 **guideFieldLabel** 标签。 如果您是作者，请覆盖此规则以使自定义更改可见。

## 构件样式 {#widgets-styling}

根据其类型，构件还包含类。 通常，小组件包括 `guideFieldWidget` 类。 随HTML一起提供的小组件通常使用标准HTML元素输入和选择。 样式设置会相应地完成。 您不能通过更改变量来设置自定义小组件的样式。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 <code></code></strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>构件的背景颜色（复选框和单选按钮不起作用）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>构件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>构件的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>构件的边框半径</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>构件的边框类型</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>构件边框的焦点类型</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>小部件的合并边框样式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>构件内文本的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>构件内文本的大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>构件的CSS lineheight属性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>构件的CSS填充属性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>小组件聚焦时的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>必填字段的构件边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必填字段小组件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>禁用字段时构件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>字段被禁用时的小部件的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>字段被禁用时构件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>小部件的高度（复选框和单选按钮无法正常使用）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>复选框和单选按钮的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多选下拉菜单的最大高度</p> </td>
  </tr>
 </tbody>
</table>

### 构件样式设置的限制 {#limitations-in-widget-styling}

焦点、必填和禁用的字段的样式受变量限制。 但是，您可以通过覆盖样式来更改它。 提供了使用变量的限制，主要是为了控制变量的数量。 如果字段由于处于前面讨论的任何状态而发生显着变化，则可以放松该限制。

## 帮助描述 {#help-description}

作者可以使用短描述组件和长描述组件在字段中指定帮助内容。 两个组件都有一个公共类 `.guideHelpDescription` 和另一堂课 `.long`/ `.short`，具体取决于描述的类型。 帮助内容包含在段落元素中，用于覆盖描述的样式。 使用以widgetshelp开头的变量修改帮助说明（长说明和短说明），如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>小组件长时间帮助的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>构件长帮助的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>小组件长帮助的左指示器边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>小部件的简短帮助的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>小部件的简短帮助的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>构件简短工具提示的背景颜色帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>小部件的简短工具提示帮助的字体颜色</p> </td>
  </tr>
 </tbody>
</table>

## 条款和条件 {#terms-and-conditions}

条款和条件(TnC) `` ``)小组件允许您指定条款和条件。 您可以使用下表所述的变量自定义构件。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>未访问的tnc链接的字体颜色。</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>已访问的tnc链接的字体颜色。</td>
  </tr>
 </tbody>
</table>

## 按钮 {#button}

按钮也是小组件。 但是，它们的样式与小组件略有不同。 在自适应表单中，以下任意值构成按钮：

* 输入[类型=文本]
* 按钮
* 带类的元素.button

按钮的HTML代码：

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>提供按钮的图标</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>样式按钮标签/标题</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 <code></code></strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>按钮的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>边框类型</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>按钮的CSS填充属性</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>按钮的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>大按钮（具有类.buttonlarge的按钮）的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按钮（具有类.buttonsmall的按钮）的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>信息按钮（具有类.buttoninformative的按钮）的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>信息性按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>信息性按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>带有警告样式的按钮（具有类.buttonwarning的按钮）的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告样式按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告样式按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>警报按钮（具有类.buttonalert的按钮）的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>警报按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>警报按钮的边框颜色</p> </td>
  </tr>
 </tbody>
</table>

## 问号 {#question-mark}

对于小组件，当作者在帮助内容中添加详细描述时，会显示问号。 使用bootstrap中提供的默认图标。 要使用自定义图标，可以自定义引导图标。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>图标的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>将鼠标悬停在图标上时图标的颜色</p> </td>
  </tr>
 </tbody>
</table>

## 表 {#table}

您可以使用以下变量更改表格中标题行和正文行的颜色主题。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>标题行的背景颜色。 默认值为 <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>奇数正文行的背景颜色。 默认值为 <code>rgb(255, 255, 255)</code>。</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶数正文行的背景颜色。 默认值为 <code>#eee</code>。</p> </td>
  </tr>
 </tbody>
</table>

## 文件附件 {#file-attachment}

自适应表单的文件附件小组件允许您上传文件。 您还可以使用变量自定义构件。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>填充小部件中显示的文件</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>文件项的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>上边框的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>文件项的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>构件中“预览”图标(Bootstrap图标)的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>文件项的注释高度</p> </td>
  </tr>
 </tbody>
</table>

## 导航器样式 {#navigator-styles}

导航器选项卡有四种类型。 这些选项卡包括左侧选项卡、顶部选项卡、向导中的选项卡和折叠面板。 每个导航器具有不同的类。

<table>
 <tbody>
  <tr>
   <td><p><strong>导航器</strong></p> </td>
   <td><p><strong>CSS 类</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab — 导航器 — 垂直</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigator</p> </td>
  </tr>
 </tbody>
</table>

以下是Tab导航器元素的HTML代码（与bootstrap选项卡类似）：

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

可以使用选择元素的CSS规则更改导航器的样式，这些元素使用 **子项** 选择器。 例如，要向锚点标记添加文本修饰样式，请执行以下操作：

顶部选项卡导航器：

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

此外，还有一些类可根据选项卡导航器（包括左侧和顶部）是否具有嵌套/子项/子导航器来设置其样式。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有嵌套/子/子导航器的选项卡导航器（左和上）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>没有嵌套/子项/子项导航器的选项卡导航器（左侧和顶部）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon类提供了一个默认图标，用于选项卡导航器（左侧和顶部）和向导导航器。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在创作（表单示例）的面板上提供CSS类，可以更改特定导航器的图标 &lt;class_name>. 您添加 **&lt;class_name>_nav** 用于导航器的图标。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>选项卡导航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>整个选项卡导航器的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>选项卡的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>选项卡的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>悬停时选项卡的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>悬停时选项卡的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>面板聚焦时的背景颜色（活动）</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>面板成为焦点时的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成表达式返回true时的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成表达式返回true时的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>面板聚焦一次但完成表达式返回false时的背景颜色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>面板聚焦一次但完成表达式返回false时的字体颜色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>选项卡的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>选项卡的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>选项卡的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>选项卡的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直选项卡的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>选项卡的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>选项卡的最小高度</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>嵌套选项卡的缩进</p> </td>
  </tr>
  <tr>
   <td><p><strong>向导导航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>整个向导导航器的背景颜色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>向导的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>向导的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>面板聚焦时的背景颜色（活动）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>面板成为焦点时的字体颜色（焦点）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成表达式返回true时的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成表达式返回true时的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>面板聚焦一次但完成表达式返回false时的背景颜色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>面板聚焦一次但完成表达式返回false时的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>向导的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>向导的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>向导的内边距</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>向导的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>向导导航器项目符号的边框颜色（在标题/标签前加前缀）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>向导导航器进度条的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>进度条的填充颜色</p> </td>
  </tr>
  <tr>
   <td><p><strong>可折叠项导航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>折叠的边距</p> </td>
  </tr>
 </tbody>
</table>

## 面板样式 {#panel-styling}

面板包括可选工具栏及其内容。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>面板的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>面板文本的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>面板文本的字体颜色<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>面板内的内边距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板说明的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板说明的边距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>面板帮助的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>面板帮助的指示器边框颜色</p> </td>
  </tr>
 </tbody>
</table>

面板节点分为导航器和内容。 那里 `` `` 对于内容，没有单独的样式组件。 所描述的变量适用于导航器和内容。

最上面的面板(RootPanel)没有此类。

## 移动设备样式 {#mobile-styling}

## 标题栏 {#header-bar}

这些变量会影响在包含面板标题以及下一个和背面导航器的移动设备或小屏幕设备上显示的标题栏。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>标题栏的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>标题栏中文本的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>标题栏的内边距</p> </td>
  </tr>
 </tbody>
</table>

## 滚动指示器 {#scroll-indicator}

这些变量会影响滚动指示器，即出现在移动设备或小屏幕设备上的橙色箭头。 滚动指示器指示屏幕可见部分以外的内容存在。 您可以向下滚动查看它。 点击内容结尾时，箭头消失。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>滚动指示器从底部的固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>滚动指示器的固定位置（从右侧）</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>滚动指示器的宽度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>滚动指示器的高度</p> </td>
  </tr>
 </tbody>
</table>

## 移动设备固定工具栏布局特定的变量 {#mobile-fixed-toolbar-layout-specific-variables}

下表中的这些变量会影响移动设备固定工具栏的布局。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>固定位置的工具栏，在移动设备上，从底部开始</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>在移动设备上从顶部固定工具栏位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>固定工具栏在移动设备左侧的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>固定工具栏在移动设备上的位置（从右侧）</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>从顶部固定工具栏按钮图标的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>移动设备上工具栏按钮图标的宽度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>移动设备上工具栏按钮图标的高度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>移动设备上工具栏的背景颜色</p> </td>
  </tr>
 </tbody>
</table>

## 主题特定变量 {#theme-specific-variable}

此 **简单注册** /etc/clientlibs/fd/af/guidetheme/simpleEnrollment上的主题和类别 `guide.theme.simpleEnrollment` 还引入了几个变量。 如果要创建主题以增强简单注册，您可以使用以下“额外变量：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>焦点按钮的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>悬停时按钮的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>按钮的半径</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>导航按钮的背景颜色（后退/下一步）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>悬停时导航按钮（后退/下一个）的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>向导导航器的背景颜色和相应的进度条（首次渲染时）。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>当前/活动向导导航器的背景颜色和相应的进度条 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>向导导航器的背景颜色和相应的进度条（已访问）。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>将容器边框颜色分叉为导航器和面板</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左侧的制表符（制表符导航器）的下边框颜色分隔制表符。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>导航器的嵌套/子项/子导航器的背景颜色</p> </td>
  </tr>
 </tbody>
</table>
