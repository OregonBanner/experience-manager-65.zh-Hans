---
title: 在HTML5表单中创建自定义外观
seo-title: 在HTML5表单中创建自定义外观
description: 您可以将自定义小组件插入到移动设备Forms。 您可以扩展现有的jQuery小组件，或开发您自己的自定义小组件。
seo-description: 您可以将自定义小组件插入到移动设备Forms。 您可以扩展现有的jQuery小组件，或开发您自己的自定义小组件。
uuid: a9013c3d-20c7-45c9-be24-8e9d4525eff8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 17a86543-30d3-4e16-a373-67b46d551da9
docset: aem65
feature: 移动设备表单
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 在HTML5表单中创建自定义外观{#create-custom-appearances-in-html-forms}

您可以将自定义小组件插入到移动设备Forms。 您可以扩展现有的jQuery小组件，或使用外观框架开发您自己的自定义小组件。 XFA引擎使用各种小组件，有关详细信息，请参阅[自适应表单和HTML5表单的外观框架](/help/forms/using/introduction-widgets.md)。

![默认和自定义小组件的示例](assets/custom-widgets.jpg)

默认和自定义小组件的示例

## 将自定义小组件与HTML5表单{#integrating-custom-widgets-with-html-forms}集成

### 创建用户档案  {#create-a-profile-nbsp}

您可以创建配置文件或选择现有配置文件以添加自定义小组件。 有关创建用户档案的更多信息，请参阅[创建自定义用户档案](/help/forms/using/custom-profile.md)。

### 创建小组件{#create-a-widget}

HTML5表单提供了小组件框架的实施，可扩展以创建新小组件。 该实施是一个jQuery小组件&#x200B;*abstractWidget*，可扩展以编写新小组件。 只有扩展/覆盖上述功能，新小组件才能正常工作。

<table>
 <tbody>
  <tr>
   <td>函数/类</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>render</td>
   <td>呈现函数返回小组件默认HTML元素的jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，&lt;a&gt;、&lt;input&gt;和&lt;li&gt;。 返回的元素将用作$userControl。 如果$userControl指定了上述约束，则AbstractWidget类的函数可按预期工作，否则某些常用API（焦点、单击）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> {<br /> blur:XFA_EXIT_EVENT，<br /> }<br /> 此示例显示模糊是HTML事件，XFA_EXIT_EVENT是对应的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一个映射，其中提供了在更改选项时要执行的操作的详细信息。 键是提供给小组件的选项，值是每当检测到该选项发生更改时调用的函数。 小组件为所有常用选项（value和displayValue除外）提供处理程序</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>每当小组件的值保存在XFAModel中（例如，在textField的退出事件中）时，小组件框架便会加载该函数。 实施应返回小组件中保存的值。 处理程序将为选项提供新值。</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>默认情况下，在XFA中，输入事件时，将显示字段的rawValue。 调用此函数时，会向用户显示rawValue。 </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>默认情况下，在退出事件时的XFA中，将显示字段的formattedValue 。 调用此函数时，会向用户显示带格式的值。 </td>
  </tr>
 </tbody>
</table>

要创建您自己的小组件，请在上面创建的配置文件中，包含JavaScript文件的引用，该文件包含被覆盖的函数和新添加的函数。 例如，*sliderNumericFieldWidget*&#x200B;是用于数字字段的小组件。 要在用户档案的标题部分中使用小组件，请加入以下行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 使用XFA脚本引擎注册自定义小组件  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

自定义小组件代码准备就绪后，使用`registerConfig`API for [Form Bridge](/help/forms/using/form-bridge-apis.md)向脚本引擎注册小组件。 它将widgetConfigObject作为输入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

小组件配置作为JSON对象（键值对的集合）提供，其中键标识字段，值表示要用于这些字段的小组件。 配置示例如下所示：

```
*{*

*“identifier1” : “customwidgetname”,
“identifier2” : “customwidgetname2”,
..
}*
```

其中，“identifier”是jQuery CSS选择器，它表示特定字段、特定类型的字段集或所有字段。 下面列出了不同情况下标识符的值：

| 标识符类型 | 标识符 | 描述 |
|---|---|---|
| 名称为“字段名称”的特定字段 | 标识符：&quot;div.fieldname&quot; | 所有名为“fieldname”的字段均使用小组件呈现。 |
| 所有类型为“type”的字段（其中类型为NumericField、DateField等）。:  | 标识符：&quot;div.type&quot; | 对于Timefield和DateTimeField，类型为文本字段，因为这些字段不受支持。 |
| 所有字段 | 标识符：&quot;div.field&quot; |  |
