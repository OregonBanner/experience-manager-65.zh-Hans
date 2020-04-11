---
title: 自适应表单和HTML5表单的外观框架
seo-title: 自适应表单和HTML5表单的外观框架
description: Mobile Forms将表单模板渲染为HTML5表单。 这些表单使用jQuery、Backbone.js和下划线。js文件来显示和启用脚本。
seo-description: Mobile Forms将表单模板渲染为HTML5表单。 这些表单使用jQuery、Backbone.js和下划线。js文件来显示和启用脚本。
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 自适应表单和HTML5表单的外观框架 {#appearance-framework-for-adaptive-and-html-forms}

表单（自适应表单和HTML5表单）使 [用jQuery](https://jquery.com/)、 [Backbone.js](https://backbonejs.org/) 和 [Onderwork.js](https://underscorejs.org/) 库进行外观和脚本编写。 表单还对表单中 [的所有交互式元素（如字段和按钮）使用jQuery UI](https://jqueryui.com/)**** Widgets架构。 此架构使表单开发人员能使用表单中丰富的可用jQuery构件和插件。 您还可以在从用户（如leadDigits/trailDigits限制或实施图片子句）捕获数据时实现表单特定逻辑。 表单开发人员可以创建和使用自定义外观来改进数据捕获体验，使其更易于用户使用。

本文面向对jQuery和jQuery构件有充分认识的开发人员。 它提供对外观框架的洞察，使开发人员能为表单字段创建替代外观。

外观框架依赖各种选项、事件（触发器）和函数来捕获用户与表单的交互，并响应模型更改以通知最终用户。 此外：

* 该框架为字段的外观提供了一组选项。 这些选项是键值对，分为两个类别:常用选项和字段类型特定选项。
* 外观作为合同的一部分，会触发一组事件，如进入和退出。
* 实现一组函数需要外观。 有些函数是通用的，而有些函数是特定于字段类型函数的。

## 常用选项 {#common-options}

以下是设置全局选项。 这些选项适用于每个字段。

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>名称</td>
   <td>用于在脚本表达式中指定此对象或事件的标识符。 例如，此属性指定主机应用程序的名称。</td>
  </tr>
  <tr>
   <td>value</td>
   <td>字段的实际值。 </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>此时将显示字段的此值。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>屏幕阅读器使用此值来解说有关字段的信息。 表单提供值，您可以覆盖该值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>字段在表单的选项卡序列中的位置。 仅当要更改表单的默认Tab键顺序时，才覆盖tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如“标题”或“表”。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>构件的高度。 它以像素为单位指定。 </td>
  </tr>
  <tr>
   <td>宽度</td>
   <td>构件的宽度。 它以像素为单位指定。</td>
  </tr>
  <tr>
   <td>访问</td>
   <td>用于访问容器对象（如子表单）内容的控件。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>XFA元素对构件的para属性。</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>文本的方向。 可能的值为ltr（从左到右）和rtl（从右到左）。</td>
  </tr>
 </tbody>
</table>

除了这些选项之外，框架还提供了一些其他选项，这些选项因字段类型而异。 下面列出了特定于字段的选项的详细信息。

### 与表单框架的交互 {#interaction-with-forms-framework}

要与表单框架交互，构件会触发一些事件，以使表单脚本能够工作。 如果构件不抛出这些事件，则在该字段的表单中编写的某些脚本将不起作用。

#### 事件由构件触发 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>事件 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>XFA_ENTER_事件</td>
   <td>只要字段处于焦点，就会触发此事件。 它允许“enter”脚本在字段上运行。 触发事件的语法是<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_事件)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_事件</td>
   <td>只要用户离开字段，就会触发此事件。 它允许引擎设置字段的值并运行其“退出”脚本。 触发事件的语法是<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_事件)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_事件</td>
   <td>触发此事件后，引擎可运行写入字段的“change”脚本。 触发事件的语法是<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_事件)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_事件</td>
   <td>单击字段时将触发此事件。 它允许引擎运行写在字段上的“单击”脚本。 触发事件的语法是<br /> （构件）。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_事件)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由构件实现的API {#apis-implemented-by-widget}

外观框架调用构件的某些功能，这些功能在自定义构件中实现。 构件必须实现以下功能：

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>焦点：function()</td>
   <td>专注于现场。</td>
  </tr>
  <tr>
   <td>单击：function()</td>
   <td>将焦点放在字段上并调用XFA_CLICK_事件。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> errorMessage <br /><em>:表示 </em>error<br /> <em>errorType的字符串：字符串("warning"/"error")</em></p> <p><strong>注意</strong>:仅适用于HTML5表单。</p> </td>
   <td>向构件发送错误消息和错误类型。 该构件显示错误。</td>
  </tr>
  <tr>
   <td><p>clearError:function()</p> <p><strong>注意</strong>:仅适用于HTML5表单。</p> </td>
   <td>如果字段中的错误已修复，则调用。 构件会隐藏错误。</td>
  </tr>
 </tbody>
</table>

## 特定于字段类型的选项 {#options-specific-to-type-of-field}

所有自定义构件都应符合上述规范。 要使用不同字段的功能，构件必须符合该特定字段的准则。

### 文本编辑：文本字段 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>多行</td>
   <td>如果字段支持输入换行符，则返回true；否则返回false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在字段中输入的最大字符数。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>:仅适用于HTML5表单</p> </td>
   <td>指定当文本宽度超过构件的宽度时文本字段的行为。</td>
  </tr>
 </tbody>
</table>

### ChoiceList:DropDownList、ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>value<br /> </td>
   <td>选定值的数组。<br /> </td>
  </tr>
  <tr>
   <td>项目<br /> </td>
   <td>要显示为选项的对象数组。 每个对象都包含两个属性-<br /> save:要保存的值，显示：值。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可编辑</p> <p><strong>注意</strong>:仅适用于HTML5表单。<br /> </p> </td>
   <td>如果值为true，则构件中将启用自定义文本输入。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>要显示的值的数组。<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>如果允许多个选择，则返回true，否则返回false。<br /> </td>
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
   <td><p>addItem:<em> function(itemValues)<br /> itemValues:包含display的对象并保存值 <br /> {sDisplayVal:&lt;displayValue&gt;, sSaveVal:&lt;save Value&gt;}</em></p> </td>
   <td>向列表添加项目。</td>
  </tr>
  <tr>
   <td>deleteItem<em>:function(nIndex)<br /> nIndex:要从列表中删除的项的索引<br /></em><br /><br /> </td>
   <td>从列表中删除选项。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>从列表中清除所有选项。</td>
  </tr>
 </tbody>
</table>

### 数字编辑：NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| 选项 | 描述 |
|---|---|
| dataType | 表示字段的数据类型（整数／小数）的字符串。 |
| leadDigits | 十进制数中允许的最大前导位数。 |
| fracDigits | 小数位数中允许的最大分数位数。 |
| 零 | 字段区域设置中零的字符串表示形式。 |
| 小数点 | 字段区域设置中小数的字符串表示形式。 |

### CheckButton:RadioButton、CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值的数组（开／关/中性）。</p> <p>它是checkButton不同状态的值数组。 值[0]是状态为ON时的值，值[1]是状态为OFF时的值，<br /> 值[2]是状态为NETRAIL时的值。 值数组的长度等于状态选项的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>国</td>
   <td><p>允许的状态数。 </p> <p>两个用于自适应表单（打开、关闭），三个用于HTML5表单（打开、关闭、中性）。</p> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td><p>元素的当前状态。</p> <p>两个用于自适应表单（打开、关闭），三个用于HTML5表单（打开、关闭、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit:(DateField) {#datetimeedit-datefield}

| 选项 | 描述 |
|---|---|
| 天 | 该字段的本地化天数名称。 |
| 个月 | 该字段的本地化月份名称。 |
| 零 | 数字0的本地化文本。 |
| clearText | 清除按钮的本地化文本。 |
