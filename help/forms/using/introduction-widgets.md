---
title: 自适应表单和HTML5表单的外观框架
description: Mobile Forms将表单模板渲染为HTML5表单。 这些表单使用jQuery、Backbone.js和Underscore.js文件作为外观并启用脚本。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# 自适应表单和HTML5表单的外观框架 {#appearance-framework-for-adaptive-and-html-forms}

Forms(自适应表单和HTML5表单)使用 [jQuery](https://jquery.com/)， [Backbone.js](https://backbonejs.org/) 和 [下划线.js](https://underscorejs.org/) 用于外观和脚本的库。 这些表单还使用 [jQuery UI](https://jqueryui.com/) **小组件** 表单中所有交互元素（如字段和按钮）的架构。 此架构使Form开发人员能够使用Forms中一组丰富的可用jQuery小部件和插件。 在从leadDigits/trailDigits限制或实施picture子句等用户捕获数据时，您还可以实施特定于表单的逻辑。 表单开发人员可以创建和使用自定义外观，以改进数据捕获体验，并使其更便于用户使用。

本文面向对jQuery和jQuery构件具有充分了解的开发人员。 它提供了外观框架的洞察信息，并使开发人员能够为表单字段创建替代外观。

外观框架依赖各种选项、事件（触发器）和函数来捕获用户与表单的交互，并响应模型更改以通知最终用户。 此外：

* 该框架为字段的外观提供了一组选项。 这些选项是键值对，分为两个类别：常用选项和特定于字段类型的选项。
* 作为合同的一部分，外观会触发一系列事件，如进入和退出。
* 实现一组函数需要外观。 某些函数是通用的，而其他函数则特定于字段类型函数。

## 常用选项 {#common-options}

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
   <td>值</td>
   <td>字段的实际值。 </td>
  </tr>
  <tr>
   <td>displayvalue</td>
   <td>将显示字段的此值。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>屏幕Reader使用此值来讲述有关字段的信息。 表单会提供值，您可以覆盖该值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>字段在表单的选项卡序列中的位置。 仅当您要更改表单的默认Tab键顺序时，才覆盖tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如标题或表。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>小部件的高度。 以像素为单位指定。 </td>
  </tr>
  <tr>
   <td>宽度</td>
   <td>构件的宽度。 以像素为单位指定。</td>
  </tr>
  <tr>
   <td>访问</td>
   <td>用于访问容器对象（如子表单）内容的控件。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>XFA元素到小组件的para属性。</td>
  </tr>
  <tr>
   <td>目录</td>
   <td>文本的方向。 可能的值为ltr （从左至右）和rtl （从右至左）。</td>
  </tr>
 </tbody>
</table>

除了这些选项，框架还提供了其他选项，这些选项因字段类型而异。 下面列出了特定于字段的选项的详细信息。

### 与表单框架的交互 {#interaction-with-forms-framework}

要与表单框架交互，构件会触发一些事件以使表单脚本正常工作。 如果构件不引发这些事件，则在该字段的表单中编写的某些脚本不起作用。

#### 构件触发的事件 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>事件 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>每当字段成为焦点时，将触发此事件。 它允许“enter”脚本在字段中运行。 触发事件的语法为<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>此事件在用户离开字段时触发。 它允许引擎设置字段的值并运行其“退出”脚本。 触发事件的语法为<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>触发此事件是为了允许引擎运行在字段中写入的“更改”脚本。 触发事件的语法为<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要单击字段，就会触发此事件。 它允许引擎运行在字段上编写的“click”脚本。 触发事件的语法为<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由小组件实现的API {#apis-implemented-by-widget}

外观框架调用在自定义构件中实现的构件的一些函数。 该构件必须实现以下功能：

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>聚焦：函数()</td>
   <td>把重点放在现场。</td>
  </tr>
  <tr>
   <td>click： function()</td>
   <td>将焦点置于字段并调用XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError：function(errorMessage， errorType)<br /> <br /> <em>错误消息：字符串 </em>表示错误<br /> <em>errorType：字符串("warning"/"error")</em></p> <p><strong>注意</strong>：仅适用于HTML5表单。</p> </td>
   <td>向构件发送错误消息和错误类型。 构件显示错误。</td>
  </tr>
  <tr>
   <td><p>clearError：函数()</p> <p><strong>注意</strong>：仅适用于HTML5表单。</p> </td>
   <td>如果修复了字段中的错误，则调用。 构件将隐藏错误。</td>
  </tr>
 </tbody>
</table>

## 特定于字段类型的选项 {#options-specific-to-type-of-field}

所有自定义构件都应符合上述规范。 要使用不同字段的功能，构件必须遵循适用于该特定字段的准则。

### TextEdit：文本字段 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>多行</td>
   <td>如果字段支持输入换行符，则为true，否则为false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在字段中输入的最大字符数。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>：仅适用于HTML5表单</p> </td>
   <td>指定当文本宽度超过小部件的宽度时文本字段的行为。</td>
  </tr>
 </tbody>
</table>

### ChoiceList： DropDownList， ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>值<br /> </td>
   <td>选定值的数组。<br /> </td>
  </tr>
  <tr>
   <td>个项目<br /> </td>
   <td>要显示为选项的对象的数组。 每个对象包含两个属性 — <br /> 保存：要保存的值，显示：要显示的值。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可编辑</p> <p><strong>注意</strong>：仅适用于HTML5表单。<br /> </p> </td>
   <td>如果值为true，则在构件中启用自定义文本输入。<br /> </td>
  </tr>
  <tr>
   <td>displayvalue<br /> </td>
   <td>要显示的值数组。<br /> </td>
  </tr>
  <tr>
   <td>多选<br /> </td>
   <td>如果允许多项选择，则为true ，否则为false。<br /> </td>
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
   <td><p>addItem：<em> 函数(itemValues)<br /> itemvalues：包含显示和保存值的对象 <br /> {sDisplayVal： &lt;displayvalue&gt;，sSaveVal： &lt;save value=""&gt;}</em></p> </td>
   <td>向列表添加项目。</td>
  </tr>
  <tr>
   <td>deleteItem<em>：函数(nIndex)<br /> nIndex：要从列表中删除的项的索引<br /> </em><br /> <br /> </td>
   <td>从列表中删除选项。</td>
  </tr>
  <tr>
   <td>清除项目：<code> function()</code></td>
   <td>清除列表中的所有选项。</td>
  </tr>
 </tbody>
</table>

### NumericEdit： NumericField， DecimalField {#numericedit-numericfield-decimalfield}

| 选项 | 描述 |
|---|---|
| 数据类型 | 表示字段的数据类型（整数/小数）的字符串。 |
| leadDigits | 小数位数中允许的前导位数上限。 |
| fracDigits | 小数位数中允许的最多小数位数。 |
| 零 | 字段区域设置中零的字符串表示形式。 |
| 小数 | 字段区域设置中十进制的字符串表示形式。 |

### CheckButton： RadioButton， CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>值</td>
   <td><p>值数组（开/关/中性）。</p> <p>它是checkButton的不同状态的值数组。 values[0]是状态为ON时的值，values[1]是状态为OFF时的值，<br /> values[2]是状态为NEUTRAL的值。 值数组的长度等于状态选项的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td><p>允许的状态数。 </p> <p>两个用于自适应表单（开、关），三个用于HTML5表单（开、关、中性）。</p> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td><p>元素的当前状态。</p> <p>两个用于自适应表单（开、关），三个用于HTML5表单（开、关、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### 日期时间编辑： （日期字段） {#datetimeedit-datefield}

| 选项 | 描述 |
|---|---|
| 天 | 该字段的本地化日期名称。 |
| 个月 | 该字段的本地化月份名称。 |
| 零 | 数字0的本地化文本。 |
| 明文 | 清除按钮的本地化文本。 |
