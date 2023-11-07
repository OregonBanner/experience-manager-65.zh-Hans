---
title: 在HTML5表单中创建自定义外观
seo-title: Create custom appearances in HTML5 forms
description: 您可以将自定义构件插入到Mobile Forms。 您可以扩展现有的jQuery构件或开发自己的自定义构件。
seo-description: You can plug in custom widgets to a Mobile Forms. You can extend existing jQuery Widgets or develop your own custom widgets.
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
feature: Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 在HTML5表单中创建自定义外观{#create-custom-appearances-in-html-forms}

您可以将自定义构件插入到Mobile Forms。 您可以扩展现有的jQuery小组件，也可以使用外观框架开发自己的自定义小组件。 XFA引擎使用各种小组件，请参见 [自适应表单和HTML5表单的外观框架](/help/forms/using/introduction-widgets.md) 以了解详细信息。

![默认小部件和自定义小部件的示例](assets/custom-widgets.jpg)

默认小部件和自定义小部件的示例

## 将自定义构件与HTML5表单集成 {#integrating-custom-widgets-with-html-forms}

### 创建用户档案  {#create-a-profile-nbsp}

您可以创建配置文件或选择现有配置文件以添加自定义构件。 有关创建用户档案的详细信息，请参阅 [创建自定义配置文件](/help/forms/using/custom-profile.md).

### 创建构件 {#create-a-widget}

HTML5提供了构件框架的一种实现方式，通过扩展这种实现方式可创建新构件。 实施是一个jQuery构件 *抽象构件* 可以扩展以编写新的构件。 只有通过扩展/覆盖以下提及的函数，才能使新构件正常工作。

<table>
 <tbody>
  <tr>
   <td>函数/类</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>渲染</td>
   <td>渲染函数为小部件的默认HTML元素返回jQuery对象。 默认的HTML元素应为可聚焦类型。 例如， &lt;a&gt;， &lt;input&gt;、和 &lt;li&gt;. 返回的元素用作$userControl。 如果$userControl指定上述约束，则AbstractWidget类的函数将按预期工作，否则，某些常用API（集中、单击）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> {<br /> 模糊：XFA_EXIT_EVENT，<br /> }<br /> 此示例显示模糊是一个HTML事件，而XFA_EXIT_EVENT是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一个映射，该映射提供更改选项时要执行的操作的详细信息。 这些键是提供给构件的选项，值是每当检测到该选项发生更改时调用的函数。 小组件为所有常用选项（value和displayValue除外）提供处理程序</td>
  </tr>
  <tr>
   <td>getcommitvalue</td>
   <td>每当小部件的值保存在XFAModel中（例如，在textField的退出事件中）时，Widget框架就会加载函数。 该实施应返回保存在小组件中的值。 将为处理程序提供选项的新值。</td>
  </tr>
  <tr>
   <td>show值</td>
   <td>默认情况下，在XFA输入事件中，显示该字段的rawValue。 调用此函数是为了向用户显示rawValue。 </td>
  </tr>
  <tr>
   <td>showdisplayvalue</td>
   <td>默认情况下，在退出事件的XFA中，显示该字段的formattedValue 。 调用此函数是为了向用户显示formattedValue。 </td>
  </tr>
 </tbody>
</table>

要创建自己的构件，请在上面创建的配置文件中，包含对JavaScript文件的引用，该文件包含覆盖的函数和新添加的函数。 例如， *sliderNumericFieldWidget* 是数值字段的小部件。 要在用户档案中的标题部分中使用构件，请包括以下行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 向XFA脚本引擎注册自定义构件  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

当自定义构件代码准备就绪时，请使用在脚本引擎中注册该构件 `registerConfig`API [Form Bridge](/help/forms/using/form-bridge-apis.md). 它将widgetConfigObject作为输入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

构件配置作为JSON对象（键值对的集合）提供，其中键标识字段，值表示用于这些字段的构件。 示例配置如下所示：

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

其中，“identifier”是一个jQuery CSS选择器，它表示特定字段、特定类型的一组字段或所有字段。 下面列出了标识符在不同情况下的值：

| 标识符类型 | 标识符 | 描述 |
|---|---|---|
| 名为fieldname的特定字段 | 标识符：&quot;div.fieldname&quot; | 所有名为“fieldname”的字段都使用小组件渲染。 |
| &#39;type&#39;类型的所有字段（其中，类型为NumericField、DateField等）:  | 标识符： &quot;div.type&quot; | 对于Timefield和DateTimeField，类型为textfield，因为这些字段不受支持。 |
| 所有字段 | 标识符： &quot;div.field&quot; |  |
