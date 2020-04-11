---
title: 为HTML5表单创建CSS样式
seo-title: 为HTML5表单创建CSS样式
description: 了解如何通过修改与HTML表单元素关联的CSS类来更改HTML5表单的外观。
seo-description: 了解如何通过修改与HTML表单元素关联的CSS类来更改HTML5表单的外观。
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 为HTML5表单创建CSS样式 {#creating-css-styles-for-html-forms}

基于XFA的表单模板的HTML5再现由多个HTML元素组成。 这些元件按顺序排列。 每个元素都有定义良好的CSS类。 可以使用这些CSS类选择和更改元素的外观。

>[!NOTE]
>
>在CSS类中，不要更改宽度、高度、边框粗细、顶部、左侧、右侧、底部、填充、边距以及其他位置和大小属性的值。 位置和大小属性的任何更改都会对表单的布局进行更改。

## 元素的CSS类 {#css-classes-nbsp-for-elements-nbsp}

每个元素都包含定义良好的CSS类。 您可以修改这些类以更改元素的外观。 除字段和绘制元素外，每个元素都有两个CSS类——类和名类。

* Type **类表示** XFA字段的类型。 您可以覆盖 `type` 类以修改特定类型所有元素的样式。

* Name **类与** XFA字段的名称相对应。 可以覆盖类以 `name` 修改自定义样式并将其应用于元素。

>[!NOTE]
>
>某些XFA元素没有名称。 要更改此类组件的样式，请修改该特定类型的所有组件。

对于未在AEM Forms Designer中命名的页面，HTML5表单中的页面按其编号的递增顺序命名。 例如，对于包含两页的HTML5表单，页面名称为Page1, Page2。

## 字段元素 {#field-element}

字段元素包含两个嵌套元素：构件和题注。

**构件元素**

构件元素包含用户界面元素，用于与用户交互。 它有三个CSS类：

* **构件**:每个小部件都有这个类。
* **name**:AEM附带的所有构件都包含构件名称类。 对于自定义构件，构件开发人员提供构件名称类。
* **类型**:每个构件都有一个用户界面元素。 该类定义用户界面元素的类型。

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

除了类型和名称类，字段组件还包含另一个名为subtype的CSS **类**。 子类型标识其属于哪种类型的字段，例如，NumericField、DateField、TextField。 您可以覆盖子类型类以修改所有子类型字段的样式。

## 不同组件的CSS类 {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>名称</strong></td>
  </tr>
  <tr>
   <td>页面</td>
   <td>页</td>
   <td>用户定义的名称<br /> 或<br /> Page&lt;pageNumber&gt;（默认）</td>
  </tr>
  <tr>
   <td>内容区域</td>
   <td>contentarea</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>子表单</td>
   <td>子表单</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>排除组</td>
   <td>exclgroup</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>绘图</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>字段</td>
   <td>字段</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>caption</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>小组件</td>
   <td>构件</td>
   <td>构件开发人员定义了它（有关用户定义的构件，请参阅下一节中的表）</td>
  </tr>
 </tbody>
</table>

## 不同字段的CSS类 {#css-classes-for-different-fields}

AEM Forms Designer支持表单中不同类型的字段，如NumericField、DecimalField和Date Field。 HTML中的所有这些字段都包含上述CSS类。 根据字段的类型，它们还包含一些额外的类。

每个字段都有一个表示UI元素的关联构件。 下面列出了每个字段的类以及与每个字段关联的构件。

<table>
 <tbody>
  <tr>
   <td><strong>字段类型</strong></td>
   <td><strong>子类型</strong></td>
   <td><strong>构件名称</strong></td>
   <td><strong>构件类型</strong></td>
   <td><strong>HTML UI标签</strong></td>
  </tr>
  <tr>
   <td>按钮<br type="_moz" /> </td>
   <td>NA</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>按钮域构件<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>输入类型=复选框<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidged<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>数字场<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>数字域构件<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>选择者<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelist构件<br type="_moz" /> </td>
   <td>选择</td>
  </tr>
  <tr>
   <td>列表框<br type="_moz" /> </td>
   <td>选择者<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelist构件<br type="_moz" /> </td>
   <td>醇</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>数字场<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>数字域构件<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>密码字段<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>密码域构件<br type="_moz" /> </td>
   <td>输入类型=密码<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>单选按钮<br type="_moz" /> </td>
   <td>辐射场<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>输入类型=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同绘图元素的CSS类 {#css-classes-for-different-draw-elements}

您可以使用AEM Forms Designer插入静态绘图元素，如文本和图像。 对于每个绘制元素，一个单独的CSS类与该元素相关联。 下面列出了绘图元素的CSS类的列表。 每个绘制元素都有一个与之关联的绘制类。

| **绘制类型** | **CSS 类** |
|---|---|
| 文本 | 文本 |
| 图像 | 图像 |
| 矩形 | 矩形 |
| Line | 折线图 |

## 设置表单的其他部分的样式 {#styling-other-parts-of-the-form}

除了HTML表单中的UI组件外观，您还可以更改元素的样式，如内联错误、内联警告和存在验证错误的字段。

`Styling Inline Errors`

当字段验证导致错误时，当字段处于活动状态时，将显示内联错误。 要更改内联错误的样式，请覆盖CSS ID **error-msg**。

`Styling Inline Warnings`

当字段验证导致警告时，当字段处于活动状态时，将显示内联警告。 要更改这些内联警告的样式，请覆盖CSS ID **warning-msg**。

`Styling Fields with Validation Errors`

当字段验证失败时，构件的样式会发生更改。 通过对构件组件应用CSS类 **widgetError** ，可完成此样式更改。 要修改默认样式，请覆盖 **widgetError类** 。
