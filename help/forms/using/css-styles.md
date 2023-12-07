---
title: 为HTML5表单创建CSS样式
description: 了解如何通过修改与HTML表单元素关联的CSS类来更改HTML5表单的外观。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 2%

---

# 为HTML5表单创建CSS样式 {#creating-css-styles-for-html-forms}

基于XFA的表单模板的HTML5演绎版包含多个HTML元素。 这些元素按顺序排列。 每个元素都有明确定义的CSS类。 您可以使用这些CSS类选择和更改元素的外观。

>[!NOTE]
>
>在CSS类中，请勿更改width、height、border-thickness、top、left、right、bottom、padding、margin以及其他位置和大小属性的值。 位置和大小属性的任何更改都会使表单的布局发生变化。

## 元素的CSS类  {#css-classes-nbsp-for-elements-nbsp}

每个元素都包含明确定义的CSS类。 可以修改这些类以更改元素的外观。 每个元素（字段和绘制元素除外）都有两个CSS类 — Type类和Name类。

* 此 **类型类** 表示XFA字段的类型。 您可以覆盖 `type` 类，用于修改特定类型的所有元素的样式。

* 此 **Name类** 对应于XFA字段的名称。 您可以覆盖 `name` 类，用于修改自定义样式并将自定义样式应用于元素。

>[!NOTE]
>
>某些XFA元素没有名称。 要更改此类组件的样式，请修改该特定类型的所有组件。

对于AEM Forms Designer中未命名的页面，HTML5表单中的页面将按其数量的递增顺序进行命名。 例如，对于具有两个页面的HTML5表单，这些页面将命名为Page1、Page2。

## 字段元素 {#field-element}

字段元素包含两个嵌套元素：小部件和标题。

**构件元素**

构件元素包含用于与用户交互的用户界面元素。 它有三个CSS类：

* **构件**：每个构件都具有此类。
* **name**：AEM随附的所有构件都包含构件名称类。 对于自定义构件，构件开发人员提供构件名称类。
* **type**：每个构件都有一个用户界面元素。 此类定义用户界面元素的类型。

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

除了类型和名称类之外，字段组件还包含一个名为的附加CSS类 **子类型**. 子类型标识它的字段类型，例如NumericField、DateField、TextField。 可以覆盖子类型类来修改所有类型、子类型字段的样式。

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
   <td>用户定义的名称<br /> 或<br /> 页面&lt;pagenumber&gt; （默认）</td>
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
   <td>排除组</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>字段</td>
   <td>字段</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>描述</td>
   <td>题注</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>小组件</td>
   <td>构件</td>
   <td>构件开发人员定义它（对于用户定义的构件，请参阅下节中的表）</td>
  </tr>
 </tbody>
</table>

## 不同字段的CSS类 {#css-classes-for-different-fields}

AEM Forms Designer支持表单中各种类型的字段，如NumericField、DecimalField和Date Field。 HTML中的所有字段都包含上述CSS类。 它们还包含一些额外的类，具体取决于字段类型。

每个字段都有一个表示UI元素的关联构件。 下面列出了每个字段的类以及与每个字段关联的构件。

<table>
 <tbody>
  <tr>
   <td><strong>字段类型</strong></td>
   <td><strong>子类型</strong></td>
   <td><strong>构件名称</strong></td>
   <td><strong>构件类型</strong></td>
   <td><strong>HTMLUI标记</strong></td>
  </tr>
  <tr>
   <td>按钮<br type="_moz" /> </td>
   <td>NA</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfield构件<br type="_moz" /> </td>
   <td>输入类型=按钮<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>勾选按钮<br type="_moz" /> </td>
   <td>复选框字段<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>复选框字段小组件<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期字段<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>日期字段小组件<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期时间字段<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>文本字段小组件</td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>数值输入<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>下拉列表<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>选择</td>
  </tr>
  <tr>
   <td>列表框<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>数值字段<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>数值输入<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密码字段<br type="_moz" /> </td>
   <td>密码字段<br type="_moz" /> </td>
   <td>defaultwidget<br type="_moz" /> </td>
   <td>密码字段小组件<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>单选按钮<br type="_moz" /> </td>
   <td>辐射场<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>Radiofield小组件<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>文本字段<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>文本字段小组件<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>文本字段小组件<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同绘制元素的CSS类 {#css-classes-for-different-draw-elements}

可以使用AEM Forms Designer插入静态绘制元素，如文本和图像。 对于每个绘制元素，单独的CSS类与该元素关联。 绘制元素的CSS类列表如下所列。 每个绘制元素都有一个与之关联的绘制类。

| **Draw Type** | **CSS类** |
|---|---|
| 文本 | text |
| 图像 | 图像 |
| 矩形 | 矩形 |
| Line | 折线图 |

## 设置窗体其他部分的样式 {#styling-other-parts-of-the-form}

除了HTML表单中UI组件的外观之外，您还可以更改元素的样式，如内联错误、内联警告和有验证错误的字段。

`Styling Inline Errors`

如果字段的验证导致错误，则字段处于活动状态时会显示内联错误。 要更改内联错误的样式，请覆盖CSS ID **error-msg**.

`Styling Inline Warnings`

当字段的验证导致警告时，如果字段处于活动状态，则显示内联警告。 要更改这些内联警告的样式，请覆盖CSS ID **warning-msg**.

`Styling Fields with Validation Errors`

当字段验证失败时，小组件的样式会更改。 此样式更改通过应用CSS类来完成 **widgetError** 在构件组件上。 要修改默认样式，请覆盖 **widgetError** 类。
