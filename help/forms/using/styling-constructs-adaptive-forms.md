---
title: 自适应表单的样式构建
seo-title: 自适应表单的样式构建
description: 使用LESS框架自定义自适应表单的外观。
seo-description: 使用LESS框架自定义自适应表单的外观。
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: 自适应表单
exl-id: 691608a6-be82-4d81-b876-427de997e5be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 3%

---

# 自适应表单的样式构造{#styling-constructs-for-adaptive-forms}

## 前提条件 {#prerequisites}

了解CSS和LESS框架。

## 可自定义的内容{#what-can-be-customized}

文章列出了自适应表单的公开可用css类。 您可以利用这些类来设置自适应表单中各个组件的样式。 创作组件的样式（如显示警告的对话框和状态栏）不在本文的涵盖范围内。 仅当您无法使用[主题编辑器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)来设置组件的样式时，才使用这些样式结构创建样式（使用CSS或更少）。

## 自定义自适应表单中的样式{#customizing-styles-in-adaptive-forms}

LESS框架简化了用例，以自定义自适应表单中的样式。 框架允许您使用一组变量和函数（混合）来定义样式。 LESS框架有助于减小捆绑代码的大小并增加其可重用性。

您可以通过以下方式自定义自适应表单样式：

* 更改主题
* 更改组件样式

## 更改主题{#changing-theme}

您可以更改自适应表单的主题，以确保其外观与嵌入了自适应表单的网页一致。

使用CSS属性更改自适应表单的整体外观通常是主题更改的一部分。 对“自适应表单的确定和感觉”这一操作进行的重大更改（如组件布局和位置的更改）不会被视为主题更改。

根据引导，以下一组CSS属性定义网页的主题：

* 背景颜色
* 边框（类型、颜色、粗细）
* 字体颜色
* 边距
* 边距
* 字体大小
* LineHeight

目前，只为自适应表单中各元素的这些属性定义LESS变量。

## 更改组件样式{#changing-component-style}

您可以更改元素的外观、布局、位置和可见性。 要完成此任务，请创建或更新自定义.css文件，以包含本文中列出的样式结构。

要将样式应用于自适应表单，请在中打开自适应表单进行编辑，打开自适应表单容器的属性，在基本选项卡中指定自定义CSS文件的路径。 自适应表单的默认样式构造，并使用自定义.css文件中列出的构造来覆盖它。

## 组件 {#components}

本文中讨论的组件具有其预定义的CSS类。 您可以编辑变量以修改CSS类中的样式。 或者，您也可以重写整个类。 本节介绍组件和样式中可以使用变量修改的类。

## 容器样式{#container-styling}

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
   <td><p><strong>变量描述</strong></p> </td>
   <td><p><strong>变量描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>容器的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>容器的内边距</p> </td>
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

## 字段样式{#field-styling}

自适应表单包括各种类型的字段。 每个字段都有一个唯一的类名称，即字段的名称。 该字段还具有通用类名称`guideFieldNode`。

字段包括标签、小组件、帮助描述（包括长描述和短描述）和字段帮助图标（问号）。

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

## 标签样式{#label-styling}

用于该字段的HTML元素&#x200B;**label**&#x200B;包含类&#x200B;**left**&#x200B;或&#x200B;**top**，具体取决于标签位于顶部还是左侧。

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

标签的CSS规则使用&#x200B;**guideFieldLabel**&#x200B;标签来应用。 如果您是作者，请覆盖此规则以使自定义更改可见。

## 小组件样式{#widgets-styling}

小组件还包含类，具体取决于其类型。 通常，小组件包含`guideFieldWidget`类。 随HTML一起提供的小组件通常使用标准HTML元素输入和选择。 样式将相应地进行。 无法通过更改变量来设置自定义小组件的样式。

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
   <td>小组件的背景颜色（复选框和单选按钮不起作用）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>小组件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>小组件的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>小组件的边框半径</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>小组件的边框类型</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>小组件边框的焦点类型</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>小组件的合并边框样式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>小组件内文本的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>小组件内的文本大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>小组件的CSS行高属性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>小组件的CSS内边距属性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>小组件聚焦时的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>用于必填字段的小组件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必填字段小组件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>禁用字段时小组件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>禁用字段时小组件的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>禁用字段时小组件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>小组件的高度（不适用于复选框和单选按钮）</td>
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

### 小组件样式的限制{#limitations-in-widget-styling}

焦点、必填和禁用字段的样式使用变量进行限制。 但是，您可以通过覆盖样式来更改样式。 提供使用变量的限制主要是为了保持对变量数的检查。 如果字段的外观发生显着变化，则可以放松限制，因为它位于前面讨论的任何状态中。

## 帮助说明{#help-description}

作者可以使用短说明和长说明组件在字段中指定帮助内容。 两个组件都具有一个通用类`.guideHelpDescription`和另一个类`.long`/ `.short`，具体取决于描述的类型。 “帮助”内容将包含在段落元素中，以覆盖描述的样式。 帮助描述（长和短）将使用以widgetshelp开头的变量进行修改，如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>小组件的长帮助的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>小组件的边框颜色长帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>小组件的左指示器边框颜色的长帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>小组件的简短帮助的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>小组件的字体颜色简短帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>小组件的短工具提示的背景颜色帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>小组件的短工具提示的字体颜色帮助</p> </td>
  </tr>
 </tbody>
</table>

## 条款和条件 {#terms-and-conditions}

条款和条件(TnC `` ``)小组件允许您指定条款和条件。 您可以使用下表所述的变量自定义小组件。

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
   <td>访问的tnc链接的字体颜色。</td>
  </tr>
 </tbody>
</table>

## 按钮 {#button}

按钮也是小组件。 但是，其样式与小组件略有不同。 在自适应表单中，以下任一选项都构成按钮：

* input[type = text]
* 按钮
* 具有class.button的元素

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
   <td><p>“样式”按钮标签/标题</p> </td>
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
   <td><p>按钮的CSS内边距属性</p> </td>
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
   <td><p>大按钮的内边距（具有类.buttonlarge的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按钮的内边距（具有类.buttonsmall的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>用于提供信息的按钮的背景颜色（具有类.buttoninformative的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>用于提供信息的按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>用于提供信息的按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告样式化按钮的背景颜色（具有类.buttonwarning的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告样式化按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告样式化按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>警报按钮的背景颜色（具有类.buttonalert的按钮）</p> </td>
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

## 问号{#question-mark}

对于小组件，当作者在帮助内容中添加长描述时，将显示问号。 将使用引导中提供的默认图标。 要使用自定义图标，可以自定义引导图标。

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
   <td><p>将鼠标悬停在图标上方时图标的颜色</p> </td>
  </tr>
 </tbody>
</table>

## 表 {#table}

您可以使用以下变量更改表中标题行和正文行的颜色主题。

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
   <td><p>奇数主体行的背景颜色。 默认值为 <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶数主体行的背景颜色。 默认值为 <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## 文件附件 {#file-attachment}

自适应表单的文件附件小组件允许您上传文件。 您还可以使用变量自定义小组件。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>小组件中显示的文件的边距</p> </td>
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
   <td><p>小组件中“预览”图标(Bootstrap图标)的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>文件项的注释高度</p> </td>
  </tr>
 </tbody>
</table>

## 导航器样式{#navigator-styles}

有四种类型的导航器选项卡。 这些选项卡包括向导和折叠面板中左侧、顶部的选项卡。 每个导航器都有一个不同的类。

<table>
 <tbody>
  <tr>
   <td><p><strong>导航器</strong></p> </td>
   <td><p><strong>CSS 类</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.向导 — 导航器</p> </td>
  </tr>
 </tbody>
</table>

以下是选项卡导航器元素的HTML代码（与引导选项卡类似）：

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

您可以使用CSS规则更改导航器的样式，该规则使用&#x200B;**子体**&#x200B;选择器选择元素。 例如，要向锚点标记添加文本修饰样式，请执行以下操作：

顶部的选项卡导航器：

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

此外，还有一些类，可根据它们是否具有嵌套/子/子导航器来显示样式选项卡导航器（包括左侧和顶部）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有嵌套/子/子导航器的选项卡导航器（左侧和顶部）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>没有嵌套/子/子导航器的选项卡导航器（左侧和顶部）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon类为选项卡导航器（左上方）和向导导航器提供了默认图标。

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
>在创作中，通过在面板上提供CSS类（表单示例&lt;CLASS_NAME>），可以更改特定导航器的图标。 为导航器的图标添加&#x200B;**&lt;CLASS_NAME>_nav**。

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
   <td><p>面板聚焦时的字体颜色</p> </td>
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
   <td>当面板聚焦一次但完成表达式返回false时，字体颜色 </td>
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
   <td><p>选项卡的内边距</p> </td>
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
   <td><p>面板聚焦时的字体颜色（聚焦）</p> </td>
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
   <td><p>向导导航器项目符号的边框颜色（在标题/标签前添加前缀）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>向导导航器进度栏的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>进度条的填充颜色</p> </td>
  </tr>
  <tr>
   <td><p><strong>折叠导航器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>折叠面板的内边距</p> </td>
  </tr>
 </tbody>
</table>

## 面板样式{#panel-styling}

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
   <td><p>面板内边距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板描述的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板描述的内边距</p> </td>
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

面板节点分为导航器和内容。 `` ``中没有用于内容的单独样式组件。 描述的变量将应用于导航器和内容。

最顶部的面板(RootPanel)没有此类。

## 移动设备样式{#mobile-styling}

## 标题栏{#header-bar}

这些变量会影响在移动设备或包含面板标题以及下一和后导航器的小屏幕设备上可见的标题栏。

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

## 滚动指示器{#scroll-indicator}

这些变量会影响滚动指示器，该指示器是在移动设备或小屏幕设备上显示的橙色箭头。 滚动指示器指示屏幕的可见部分以外有内容。 您可以向下滚动以查看。 点击内容的结尾时，箭头会消失。

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
   <td><p>从底部固定滚动体位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>从右起的滚动器的固定位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>滚动条宽度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>阴划器高度</p> </td>
  </tr>
 </tbody>
</table>

## 移动设备固定工具栏布局特定变量{#mobile-fixed-toolbar-layout-specific-variables}

下表中的这些变量会影响移动设备固定工具栏布局。

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
   <td><p>固定了工具栏在移动设备上的底部位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>修复了工具栏在移动设备上从顶部的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>修复了工具栏在移动设备上左侧的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>修复了工具栏在移动设备上右侧的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>修复了工具栏按钮图标（从顶部）的位置</p> </td>
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

## 特定于主题的变量{#theme-specific-variable}

位于/etc/clientlibs/fd/af/guidetheme/simpleEnrollment的&#x200B;**Simple enrollment**&#x200B;主题和类别`guide.theme.simpleEnrollment`还引入了一些变量。 如果要创建增强简单注册的主题，可以使用以下“额外变量：

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
   <td><p>按钮半径</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>导航按钮的背景颜色（后退/下一步）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>悬停时导航按钮的背景颜色（后退/下一步）</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>首次渲染时，向导导航器和相应进度条的背景颜色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>当前/活动向导导航器和相应进度条的背景颜色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已访问的向导导航器和相应进度栏的背景颜色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>将边框颜色分叉容器分成导航器和面板</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左侧（制表符导航器）上制表符的下边框颜色分隔选项卡。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>导航器嵌套/子/子导航器的背景颜色</p> </td>
  </tr>
 </tbody>
</table>
