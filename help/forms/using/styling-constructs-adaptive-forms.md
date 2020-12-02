---
title: 自适应表单的样式构造
seo-title: 自适应表单的样式构造
description: 使用LESS框架自定义自适应表单的外观。
seo-description: 使用LESS框架自定义自适应表单的外观。
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
translation-type: tm+mt
source-git-commit: 5a76200a573d95026e2347d2049a089d975b5619
workflow-type: tm+mt
source-wordcount: '2322'
ht-degree: 3%

---


# 自适应表单的样式构造{#styling-constructs-for-adaptive-forms}

## 前提条件 {#prerequisites}

了解CSS和LESS框架。

## 可以自定义的{#what-can-be-customized}

文章列表公开的自适应表单的css类。 您可以利用这些类来设计自适应表单的各个组件的样式。 创作组件的样式（如显示警告的对话框和状态栏）超出本文的范围。 仅当无法使用[主题编辑器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html)设置组件样式时，使用这些样式构造创建样式（使用CSS或更少）。

## 自定义自适应表单中的样式{#customizing-styles-in-adaptive-forms}

LESS框架简化了自适应表单样式的使用案例。 该框架允许您使用一组变量和函数（混合）定义样式。 LESS框架有助于减小捆绑代码的大小并增加其可重用性。

可以通过以下方式自定义自适应表单样式：

* 更改主题
* 更改组件样式

## 更改主题{#changing-theme}

您可以更改自适应表单的主题以确保其外观与嵌入自适应表单的网页保持一致。

使用CSS属性对自适应表单的整体外观进行更改通常是主题更改的一部分。 对“自适应表单的确定和感觉”这个选项所做的重大更改（如组件布局和位置的更改）不会被视为主题更改。

根据引导，以下CSS属性集定义网页的主题：

* 背景颜色
* 边框（类型、颜色、粗细）
* 字体颜色
* 边距
* 边距
* 字体大小
* LineHeight

目前，LESS变量仅为自适应表单中各个元素的这些属性定义。

## 更改组件样式{#changing-component-style}

您可以更改元素的外观、布局、位置和可见性。 要实现此任务，请创建或更新自定义。css文件，以包含本文中列出的样式构造。

要将样式应用于自适应表单，请在中打开自适应表单进行编辑，打开自适应表单容器的属性，在基本选项卡中指定自定义CSS文件的路径。 自适应表单的默认样式构造，并由自定义。css文件中列出的构造覆盖。

## 组件 {#components}

本文中讨论的组件有其预定义的CSS类。 您可以编辑变量以修改CSS类中的样式。 或者，也可以重写整个类。 本节介绍组件和样式中的类，您可以使用变量修改这些类。

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
   <td><p>容器的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>容器边距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字体颜色</p> </td>
  </tr>
 </tbody>
</table>

## 字段样式{#field-styling}

自适应表单包括各种类型的字段。 每个字段都有一个唯一的类名，即字段的名称。 该字段还具有公用类名`guideFieldNode`。

字段包括标签、构件、帮助说明（长说明和短说明）和字段帮助图标（问号）。

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
   <td><p>字段的填充</p> </td>
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

用于字段的HTML元素&#x200B;**label**&#x200B;包括类&#x200B;**left**&#x200B;或&#x200B;**top**，具体取决于标签在顶部还是左侧。

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
   <td>字段标签的CSS字体权重属性 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>字段标签的边距</p> </td>
  </tr>
 </tbody>
</table>

标签的CSS规则使用&#x200B;**guideFieldLabel**&#x200B;标签进行应用。 如果您是作者，请覆盖此规则以使自定义更改可见。

## 构件样式{#widgets-styling}

构件还包含类，具体取决于其类型。 通常，构件包括`guideFieldWidget`类。 随HTML一起提供的构件通常使用标准HTML元素输入和选择。 样式将相应地进行。 无法通过更改变量来设置自定义构件的样式。

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
   <td>构件的背景颜色（对复选框和单选按钮不起作用）</td>
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
   <td><p>构件的合并边框样式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>构件中文本的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>构件中文本的大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>构件的CSS线条高度属性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>构件的CSS填充属性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>构件处于焦点时的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>必填字段的构件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必填字段的构件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>禁用字段时构件的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>禁用字段时构件的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>禁用字段时构件的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>构件的高度（复选框和单选按钮不工作）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>复选框和单选按钮的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多选下拉列表的最大高度</p> </td>
  </tr>
 </tbody>
</table>

### 构件样式{#limitations-in-widget-styling}的限制

焦点、必填和禁用字段的样式使用变量进行限制。 但是，可以通过覆盖样式来更改它。 使用变量的限制主要是为了保持变量的数量受到限制。 当场的外观发生显着变化时，该限制可以放松，因为它位于前面讨论的任何状态中。

## 帮助说明{#help-description}

作者可以使用简短和详细说明组件在字段中指定帮助内容。 两个组件都有一个公用类`.guideHelpDescription`和另一个类`.long`/ `.short`，具体取决于描述的类型。 “帮助”内容会包含在段落元素中以覆盖描述的样式。 帮助说明（长和短）使用以widgetshelp开头的变量进行修改，如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>构件的背景颜色长帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>构件的边框颜色的长帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>构件的左指示器边框颜色的长帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>构件的背景颜色简短帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>构件的字体颜色简短帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>构件的背景颜色简短工具提示帮助</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>构件的字体颜色简短工具提示帮助</p> </td>
  </tr>
 </tbody>
</table>

## 条款和条件 {#terms-and-conditions}

条款与条件(TnC `` ``)构件允许您指定条款和条件。 您可以使用下表中描述的变量自定义构件。

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

按钮也是构件。 但是，其样式与构件略有不同。 在自适应表单中，以下任一项构成按钮：

* 输入[类型= text]
* 按钮
* 元素与类。button

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
   <td><p>提供按钮图标</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>样式按钮标签／题注</p> </td>
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
   <td><p>大按钮的边距（类为。buttonlarge的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小按钮的边距（类为。buttonsmall的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按钮的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>信息性按钮的背景颜色（具有类。buttoninformative的按钮）</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>信息性按钮的字体颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>用于信息性按钮的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告样式按钮的背景颜色（类为。buttonwarning的按钮）</p> </td>
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
   <td><p>警报按钮的背景颜色（具有类。buttonalert的按钮）</p> </td>
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

对于构件，当作者在“帮助”内容中添加详细说明时，将显示questionMark。 使用引导中提供的默认图标。 要使用自定义图标，可以自定义引导图标。

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
   <td><p>鼠标悬停在图标上时图标的颜色</p> </td>
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
   <td><p>偶数体行的背景颜色。 默认值为 <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## 文件附件 {#file-attachment}

自适应表单的文件附件构件允许您上传文件。 您还可以使用变量自定义构件。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>构件中显示的文件的边距</p> </td>
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
   <td><p>构件中预览图标(Bootstrap图标)的颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>文件项的注释高度</p> </td>
  </tr>
 </tbody>
</table>

## 导航器样式{#navigator-styles}

有四种类型的导航器选项卡。 这些选项卡包括向导和折叠面板左侧、顶部的选项卡。 每个导航器都有不同的类。

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
   <td><p>.向导——导航器</p> </td>
  </tr>
 </tbody>
</table>

以下是选项卡导航器元素的HTML代码（与引导选项卡类似）:

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

您可以使用CSS规则更改导航器的样式，这些规则使用&#x200B;**后代**&#x200B;选择器选择元素。 例如，要向锚点标签添加文本装饰样式：

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

此外，还根据选项卡导航器是否具有嵌套／子/子导航器，提供样式选项卡导航器（左侧和顶部）的类。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有嵌套／子/子导航器的选项卡导航器（左侧和顶部）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>没有嵌套／子/子导航器的选项卡导航器（左侧和顶部）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon类提供一个默认图标，用于标记导航器（左上）和向导导航器。

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
>在创作过程中，通过在面板上提供CSS类（表单示例&lt;CLASS_NAME>），可以更改特定导航器的图标。 添加&#x200B;**&lt;CLASS_NAME>_nav**&#x200B;作为导航器图标。

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
   <td><p>面板处于焦点时的背景颜色（活动）</p> </td>
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
   <td>当面板聚焦一次但完成表达式返回false时的背景颜色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>当面板已聚焦一次但完成表达式返回false时的字体颜色 </td>
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
   <td><p>选项卡的填充</p> </td>
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
   <td><p>面板处于焦点时的背景颜色（活动）</p> </td>
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
   <td>当面板聚焦一次但完成表达式返回false时的背景颜色</td>
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
   <td><p>向导的填充</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>向导的边框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>向导导航器项目符号的边框颜色（在标题／标签前添加前缀）</p> </td>
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
   <td><p>折叠面板的填充</p> </td>
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
   <td><p>面板内填充</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板说明的字体大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板说明的填充</p> </td>
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

面板节点被分为导航器和内容。 `` ``没有单独的内容样式组件。 描述的变量应用于导航器和内容。

最上面的面板(RootPanel)没有此类。

## 移动样式{#mobile-styling}

## 标题栏{#header-bar}

这些变量会影响在移动设备或小屏幕设备上可见的标题栏，这些设备包含面板标题以及后面和后面的导航器。

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
   <td><p>标题栏的填充</p> </td>
  </tr>
 </tbody>
</table>

## 滚动指示符{#scroll-indicator}

这些变量影响滚动指示器，该指示器是在移动设备或小屏幕设备上显示的橙色箭头。 “滚动”指示符指示屏幕的可见部分之外有内容。 您可以向下滚动以查看它。 点击内容结尾时，箭头消失。

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
   <td><p>从底部固定滚动条的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>从右侧固定滚动条的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>滚动条宽度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>滚动条高度</p> </td>
  </tr>
 </tbody>
</table>

## 移动固定工具栏特定于布局的变量{#mobile-fixed-toolbar-layout-specific-variables}

下表中的这些变量会影响移动固定工具栏布局。

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
   <td><p>固定工具栏在移动设备上的底部位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>修复了工具栏在移动设备上的顶部位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>在移动设备上从左侧修复工具栏的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>固定工具栏在移动设备上的右侧位置</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>从顶部修复工具栏按钮图标的位置</p> </td>
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

## 主题特定变量{#theme-specific-variable}

**简单登记**&#x200B;主题（位于/etc/clientlibs/fd/af/guidetheme/simpleEnromment）和类别`guide.theme.simpleEnrollment`还引入了一些变量。 如果要创建主题以增强简单登记，可以使用以下“额外变量：

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
   <td><p>导航按钮的背景颜色（后退／下一步）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>悬停时导航按钮（后退／下一步）的背景颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>首次呈现时，向导导航器和相应进度栏的背景颜色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>当前／活动向导导航器和相应进度栏的背景颜色 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已访问的向导导航器和相应进度栏的背景颜色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>将容器分成导航器和面板的边框颜色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左侧选项卡（选项卡导航器）的底部边框颜色分隔选项卡。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>导航器的嵌套／子/子导航器的背景颜色</p> </td>
  </tr>
 </tbody>
</table>

