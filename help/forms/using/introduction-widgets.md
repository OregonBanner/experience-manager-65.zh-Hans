---
title: 自适应表单和HTML5表单的外观框架
seo-title: 自适应表单和HTML5表单的外观框架
description: 移动设备Forms将表单模板渲染为HTML5表单。 这些表单使用jQuery、Backbone.js和Underscore.js文件来显示外观并启用脚本。
seo-description: 移动设备Forms将表单模板渲染为HTML5表单。 这些表单使用jQuery、Backbone.js和Underscore.js文件来显示外观并启用脚本。
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# 自适应表单和HTML5表单的外观框架{#appearance-framework-for-adaptive-and-html-forms}

Forms（自适应表单和HTML5表单）使用[jQuery](https://jquery.com/)、[Backbone.js](https://backbonejs.org/)和[Undersore.js](https://underscorejs.org/)库进行外观和脚本编写。 表单还使用[jQuery UI](https://jqueryui.com/) **Widgets**&#x200B;架构来处理表单中的所有交互元素（如字段和按钮）。 此架构使表单开发人员能够在Forms中使用一组丰富的可用jQuery小组件和插件。 您还可以在从用户（如leadDigits/trailDigits限制或实施图片子句）中捕获数据时实施表单特定逻辑。 表单开发人员可以创建并使用自定义设备来改进数据捕获体验，并使其更加用户友好。

本文面向对jQuery和jQuery小组件有充分了解的开发人员。 它提供了对外观框架的分析，并允许开发人员为表单字段创建替代外观。

外观框架依赖于各种选项、事件（触发器）和函数来捕获用户与表单的交互，并响应模型更改以通知最终用户。 此外：

* 框架提供了一组用于显示字段的选项。 这些选项是键值对，分为两类：常用选项和字段类型特定选项。
* 作为合同一部分的外观会触发一系列事件，如进入和退出。
* 实施一组函数时需要显示外观。 某些函数是常用的，而其他函数则特定于字段类型函数。

## 常用选项{#common-options}

以下是设置的全局选项。 这些选项适用于每个字段。

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>name</td>
   <td>用于在脚本表达式中指定此对象或事件的标识符。 例如，此属性指定主机应用程序的名称。</td>
  </tr>
  <tr>
   <td>选定</td>
   <td>字段的实际值。 </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>将显示字段的此值。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>屏幕Reader使用此值讲述有关该字段的信息。 表单提供值，您可以覆盖该值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>字段在表单的制表符序列中的位置。 仅当要更改表单的默认制表符顺序时，才覆盖tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如“标题”或“表”。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>小组件的高度。 以像素为单位指定。 </td>
  </tr>
  <tr>
   <td>宽度</td>
   <td>小组件的宽度。 以像素为单位指定。</td>
  </tr>
  <tr>
   <td>访问</td>
   <td>用于访问容器对象（如子表单）内容的控件。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>XFA元素对小组件的para属性。</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>文本的方向。 可能的值为ltr（从左到右）和rtl（从右到左）。</td>
  </tr>
 </tbody>
</table>

除了这些选项外，框架还提供了一些其他选项，这些选项会因字段类型而异。 下面列出了特定于字段的选项的详细信息。

### 与表单框架{#interaction-with-forms-framework}的交互

为了与表单框架进行交互，小组件会触发一些事件，以使表单脚本正常工作。 如果小组件未引发这些事件，则在该字段的表单中编写的某些脚本将不起作用。

#### 由小组件{#events-triggered-by-widget}触发的事件

<table>
 <tbody>
  <tr>
   <th>事件 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>当字段处于焦点时，会触发此事件。 它允许在字段上运行“enter”脚本。 触发事件的语法为<br />（小组件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>每当用户离开字段时，都会触发此事件。 它允许引擎设置字段的值并运行其“退出”脚本。 触发事件的语法为<br />（小组件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>此事件将触发，以允许引擎运行在字段中编写的“change”脚本。 触发事件的语法为<br />（小组件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要单击字段，就会触发此事件。 它允许引擎运行在字段上编写的“click”脚本。 触发事件的语法为<br />（小组件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由小组件{#apis-implemented-by-widget}实施的API

外观框架会调用在自定义小组件中实施的小组件的某些功能。 小组件必须实施以下功能：

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>焦点：function()</td>
   <td>关注现场。</td>
  </tr>
  <tr>
   <td>单击：function()</td>
   <td>重点关注字段并调用XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage， errorType)<br /> <br /> <em>errMessage:字符串</em>表示错误<br /> <em>errorType:字符串("warning"/"error")</em></p> <p><strong>注意</strong>:仅适用于HTML5表单。</p> </td>
   <td>向小组件发送错误消息和错误类型。 小组件会显示错误。</td>
  </tr>
  <tr>
   <td><p>clearError:function()</p> <p><strong>注意</strong>:仅适用于HTML5表单。</p> </td>
   <td>如果字段中的错误已修复，则调用。 小组件可隐藏错误。</td>
  </tr>
 </tbody>
</table>

## 特定于字段类型{#options-specific-to-type-of-field}的选项

所有自定义小部件都应符合上述规范。 要使用不同字段的功能，小组件必须符合该特定字段的准则。

### 文本编辑：文本字段{#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>多线</td>
   <td>如果字段支持输入换行符，则返回true；否则返回false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在字段中输入的最大字符数。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>:仅适用于HTML5表单</p> </td>
   <td>指定当文本的宽度超过小组件的宽度时文本字段的行为。</td>
  </tr>
 </tbody>
</table>

### ChoiceList:DropDownList， ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>选定<br /> </td>
   <td>选定值的数组。<br /> </td>
  </tr>
  <tr>
   <td>项目<br /> </td>
   <td>要显示为选项的对象数组。 每个对象都包含两个属性 — <br /> save:保存、显示的值：值。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可编辑</p> <p><strong>注意</strong>:仅适用于HTML5表单。<br /> </p> </td>
   <td>如果值为true，则小组件中会启用自定义文本条目。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>要显示的值数组。<br /> </td>
  </tr>
  <tr>
   <td>多选<br /> </td>
   <td>如果允许多个选择，则返回true；否则返回false。<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues:包含显示和保存值<br /> {sDisplayVal：的对象&lt;displayValue&gt;, sSaveVal:&lt;保存值&gt;}</em></p> </td>
   <td>将项目添加到列表。</td>
  </tr>
  <tr>
   <td>deleteItem<em>:function(nIndex)<br /> nIndex:要从列表中删除的项的索引<br /> </em><br /> <br /> </td>
   <td>从列表中删除选项。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>清除列表中的所有选项。</td>
  </tr>
 </tbody>
</table>

### 数值编辑：NumericField， DecimalField {#numericedit-numericfield-decimalfield}

| 选项 | 描述 |
|---|---|
| dataType | 表示字段数据类型（整数/小数）的字符串。 |
| leadDigits | 小数中允许的最大前导位数。 |
| fracDigits | 小数中允许的最大小数位数。 |
| 零 | 字段区域设置中零的字符串表示形式。 |
| 小数 | 字段区域设置中小数的字符串表示形式。 |

### CheckButton:RadioButton， CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值数组（开/关/中性）。</p> <p>它是checkButton不同状态的值数组。 values[0]是状态为ON时的值，values[1]是状态为OFF时的值，<br /> values[2]是状态为NETRAME时的值。 值数组的长度等于state选项的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>国家</td>
   <td><p>允许的状态数。 </p> <p>两个用于自适应表单（开、关），三个用于HTML5表单（开、关、中性）。</p> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td><p>元素的当前状态。</p> <p>两个用于自适应表单（开、关），三个用于HTML5表单（开、关、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit:(DateField){#datetimeedit-datefield}

| 选项 | 描述 |
|---|---|
| 天 | 该字段的本地化天数名称。 |
| 个月 | 该字段的本地化月份名称。 |
| 零 | 数字0的本地化文本。 |
| clearText | 用于清除按钮的本地化文本。 |
