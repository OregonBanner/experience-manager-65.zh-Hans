---
title: 在HTML5表单中创建自定义外观
seo-title: 在HTML5表单中创建自定义外观
description: 可将自定义构件插入到移动表单中。 您可以扩展现有的jQuery构件或开发您自己的自定义构件。
seo-description: 可将自定义构件插入到移动表单中。 您可以扩展现有的jQuery构件或开发您自己的自定义构件。
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在HTML5表单中创建自定义外观{#create-custom-appearances-in-html-forms}

可将自定义构件插入到移动表单中。 您可以扩展现有的jQuery构件，或使用外观框架开发您自己的自定义构件。 XFA引擎使用各种构件，有关详细 [信息，请参阅自适应表单和HTML5表单的外观框架](/help/forms/using/introduction-widgets.md) 。

![默认和自定义构件的示例](assets/custom-widgets.jpg)

默认和自定义构件的示例

## 将自定义构件与HTML5表单集成 {#integrating-custom-widgets-with-html-forms}

### 创建用户档案 {#create-a-profile-nbsp}

您可以创建用户档案或选择现有用户档案来添加自定义构件。 有关创建用户档案的详细信息，请参阅 [创建自定义用户档案](/help/forms/using/custom-profile.md)。

### 创建构件 {#create-a-widget}

HTML5表单提供了构件框架的实现，该框架可以扩展以创建新构件。 该实现是一个jQuery Widget *abstractWidget* ，可扩展以编写新构件。 只有通过扩展／覆盖下面提到的功能，才能使新构件正常工作。

<table>
 <tbody>
  <tr>
   <td>函数／类</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>渲染</td>
   <td>渲染函数返回构件的默认HTML元素的jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，&lt;a&gt;、&lt;input&gt;和&lt;li&gt;。 返回的元素将用作$userControl。 如果$userControl指定上述约束，则AbstractWidget类的函数将按预期工作，否则某些常见API（焦点、单击）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> {模糊<br /> :XFA_EXIT_事件,<br /><br /> }此示例说明模糊是HTML事件,XFA_EXIT_事件是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一个映射，它提供选项更改时要执行的操作的详细信息。 键是提供给构件的选项，值是检测到该选项的更改时调用的函数。 该构件为所有常用选项（value和displayValue除外）提供处理函数</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>只要将构件的值保存在XFAModel中(例如，在textField的退出事件上)，构件框架就会加载该函数。 实施应返回保存在构件中的值。 该处理函数提供了选项的新值。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>默认情况下，在XFA中输入事件时，将显示字段的rawValue。 调用此函数向用户显示rawValue。 </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>默认情况下，在退出事件的XFA中，将显示字段的formattedValue。 调用此函数向用户显示formattedValue。 </td>
  </tr>
 </tbody>
</table>

要创建您自己的构件，请在上面创建的用户档案中包括对JavaScript文件的引用，该文件包含被覆盖的函数和新添加的函数。 例如，sliderNumericFieldWidget *是数字字段的构件* 。 要在标题部分的用户档案中使用构件，请包括以下行：

```
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA脚本引擎注册自定义构件 {#register-custom-widget-with-xfa-scripting-engine-nbsp}

当自定义构件代码准备就绪时，请使用 `registerConfig`Form Bridge的 [API向脚本引擎注册构](/help/forms/using/form-bridge-apis.md)件。 它以widgetConfigObject为输入。

```
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

构件配置作为JSON对象（键值对的集合）提供，其中键标识字段，值表示要与这些字段一起使用的构件。 示例配置如下所示：

*{*

*&quot;identifier1&quot; :&quot;customwidgetname&quot;,&quot;identifier2&quot; :&quot;customwidgetname2&quot;,...}*

其中，“identifier”是表示特定字段、特定类型的字段集或所有字段的jQuery CSS选择器。 以下列表了不同情况下标识符的值：

| 标识符类型 | 标识符 | 描述 |
|---|---|---|
| 具有名称字段名称的特定字段 | 标识符：&quot;div.fieldname&quot; | 名称为“fieldname”的所有字段均使用构件呈现。 |
| 类型为“type”的所有字段（其中类型为NumericField、DateField等。）:  | 标识符：“div.type” | 对于Timefield和DateTimeField，类型为文本字段，因为不支持这些字段。 |
| 所有字段 | 标识符：“div.field” |  |
