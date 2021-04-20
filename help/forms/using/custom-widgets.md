---
title: 在HTML5表单中创建自定义外观
seo-title: 在HTML5表单中创建自定义外观
description: 您可以将自定义构件插入Mobile Forms。 您可以扩展现有的jQuery Widget，或开发您自己的自定义Widget。
seo-description: 您可以将自定义构件插入Mobile Forms。 您可以扩展现有的jQuery Widget，或开发您自己的自定义Widget。
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# 在HTML5表单中创建自定义外观{#create-custom-appearances-in-html-forms}

您可以将自定义构件插入Mobile Forms。 您可以扩展现有的jQuery Widget，或使用外观框架开发您自己的自定义Widget。 XFA引擎使用各种构件，有关详细信息，请参阅[自适应和HTML5表单的外观框架](/help/forms/using/introduction-widgets.md)。

![默认和自定义Widget的示例](assets/custom-widgets.jpg)

默认和自定义Widget的示例

## 将自定义构件与HTML5表单{#integrating-custom-widgets-with-html-forms}集成

### 创建用户档案  {#create-a-profile-nbsp}

您可以创建用户档案或选择现有用户档案来添加自定义Widget。 有关创建用户档案的详细信息，请参阅[创建自定义用户档案](/help/forms/using/custom-profile.md)。

### 创建Widget {#create-a-widget}

HTML5表单提供了构件框架的实现，可扩展以创建新构件。 实现是jQuery Widget *abstractWidget*，可扩展以编写新Widget。 只有扩展/覆盖下列功能，才能使新Widget正常工作。

<table>
 <tbody>
  <tr>
   <td>Function/Class</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>渲染</td>
   <td>render函数返回构件的默认HTML元素的jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，&lt;a&gt;、&lt;input&gt;和&lt;li&gt;。 返回的元素将用作$userControl。 如果$userControl指定上述约束，则AbstractWidget类的函数将按预期工作，否则某些常用API（焦点，单击）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> {<br /> blur:XFA_EXIT_事件,<br /> }<br /> 此示例显示模糊是HTML事件,XFA_EXIT_事件是对应的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一个映射，它提供选项更改时要执行的操作的详细信息。 键是提供给Widget的选项，值是每当检测到该选项发生更改时调用的函数。 Widget为所有常用选项（value和displayValue除外）提供处理函数</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>只要将Widget的值保存到XFAModel中(例如，在textField的退出事件),Widget框架就会加载该函数。 实现应返回保存在Widget中的值。 该处理程序随选项的新值提供。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>默认情况下，在XFA中输入事件时，将显示该字段的rawValue。 调用此函数向用户显示rawValue。 </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>默认情况下，在退出事件的XFA中，将显示字段的formattedValue。 调用此函数向用户显示格式化的Value。 </td>
  </tr>
 </tbody>
</table>

要创建您自己的Widget，请在上面创建的用户档案中，包含对JavaScript文件的引用，该文件包含被覆盖的函数和新添加的函数。 例如，*sliderNumericFieldWidget*&#x200B;是数字字段的Widget。 要在标题部分的用户档案中使用Widget，请包含以下行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA脚本引擎注册自定义Widget  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

自定义构件代码准备就绪后，使用`registerConfig`用于[Form Bridge](/help/forms/using/form-bridge-apis.md)的API向脚本引擎注册构件。 它以widgetConfigObject为输入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

Widget配置是作为JSON对象（一组键值对）提供的，其中键标识字段，值表示要与这些字段一起使用的Widget。 示例配置如下所示：

```
*{*

*“identifier1” : “customwidgetname”,
“identifier2” : “customwidgetname2”,
..
}*
```

其中，“identifier”是一个jQuery CSS选择器，它表示特定字段、特定类型的字段集或所有字段。 以下列表了不同情况下标识符的值：

| 标识符类型 | 标识符 | 描述 |
|---|---|---|
| 具有名称字段名称的特定字段 | 标识符：&quot;div.fieldname&quot; | 名称为“fieldname”的所有字段均使用Widget呈现。 |
| 所有类型为“type”的字段（其中类型为NumericField、DateField等。）:  | 标识符：&quot;div.type&quot; | 对于Timefield和DateTimeField，类型为textfield，因为不支持这些字段。 |
| 所有字段 | 标识符：&quot;div.field&quot; |  |
