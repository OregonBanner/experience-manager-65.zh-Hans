---
title: 自适应表单表达式
seo-title: 自适应表单表达式
description: 使用自适应表单表达式添加自动验证、计算以及打开或关闭部分的可见性。
seo-description: 使用自适应表单表达式添加自动验证、计算以及打开或关闭部分的可见性。
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: 自适应表单
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2769'
ht-degree: 0%

---

# 自适应表单表达式{#adaptive-form-expressions}

自适应表单通过动态脚本功能为最终用户提供优化且简化的表单填写体验。 它允许您编写表达式以添加各种行为，如动态显示/隐藏字段和面板。 它还允许您添加计算字段、将字段设为只读、添加验证逻辑等。 动态行为基于用户输入或预填充的数据。

JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，且使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关自适应表单类、事件、对象和公共API的完整列表，请参阅[自适应表单的JavaScript库API引用](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)。

## 编写表达式的最佳实践{#best-practices-for-writing-expressions}

* 在编写表达式时，要访问字段和面板，可以使用字段或面板的名称。 要访问字段的值，请使用value属性。 例如，`field1.value`
* 在表单中为字段和面板使用唯一的名称。 它有助于避免与编写表达式时使用的字段名称发生任何可能的冲突。
* 编写多行表达式时，使用分号终止语句。

## 涉及重复面板{#best-practices-for-expressions-involving-repeating-panel}的表达式的最佳实践

重复面板是使用脚本API或预填充数据动态添加或删除面板的实例。 有关使用重复面板的详细信息，请参阅[创建具有可重复部分的表单](/help/forms/using/creating-forms-repeatable-sections.md)。

* 要创建重复面板，请在面板对话框中打开设置，并将最大计数字段的值设置为大于1。
* 面板重复设置的最小计数值可以是一个或多个，但不能大于最大计数值。
* 当表达式引用重复面板的字段时，表达式中的字段名称将解析为最接近的重复元素。
* 自适应表单提供了一些特殊函数来简化可重复面板的计算，例如总计、计数、最小值、最大值、过滤器等。 有关函数的完整列表，请参阅[自适应表单的JavaScript库API引用](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 用于处理重复面板实例的API包括：

   * 添加面板实例：`panel1.instanceManager.addInstance()`
   * 要获取面板重复索引，请执行以下操作：`panel1.instanceIndex`
   * 要获取面板的instanceManager，请执行以下操作：`_panel1 or panel1.instanceManager`
   * 要删除面板的实例，请执行以下操作：`_panel1.removeInstance(panel1.instanceIndex)`

## 表达式类型{#expression-types}

在自适应表单中，您可以编写表达式来添加动态显示/隐藏字段和面板等行为。 您还可以编写表达式来添加计算字段、使字段为只读、验证逻辑等。 自适应表单支持以下表达式：

* **[访问表达式](#access-expression-enablement-expression)**:启用/禁用字段。
* **[计算表达式](#calculate-expression)**:自动计算字段值。
* **[单击表达式](#click-expression)**:用于处理按钮的单击事件上的操作。
* **[初始化脚本](#initialization-script):** 对字段的初始化执行操作。
* **[选项表达式](#options-expression)**:以动态填写下拉列表。
* **[概要表达式](#summary)**:来动态计算折叠面板的标题。
* **[验证表达式](#validate-expression)**:验证字段。
* **[值提交脚本](#value-commit-script):** 在字段的值发生更改后更改表单的组件。
* **[可见性表达式](#visibility-expression)**:以控制字段和面板的可见性。
* **[步骤完成表达式](#step-completion-expression)**:以阻止用户进入向导的下一步。

### 访问表达式（启用表达式）{#access-expression-enablement-expression}

您可以使用访问表达式启用或禁用字段。 如果表达式使用字段的值，则每当字段的值更改时，都会重新触发表达式。

**适用于**:字段

**返回类型**:表达式会返回一个布尔值，表示字段是启用还是禁用。**** true表示字段已启用，而 **** false表示字段已禁用。

**示例**:要仅在字段1的值设 **置为X** 时启用字 ****&#x200B;段，访问表达式为：  `field1.value == "X"`

### 计算表达式{#calculate-expression}

计算表达式用于使用表达式自动计算字段的值。 通常，此表达式使用其他字段的value属性。 例如，`field2.value + field3.value`。 每当`field2`或`field3`的值发生更改时，都会重新触发表达式并重新计算该值。

**适用于**:字段

**返回类型**:表达式会返回一个与显示表达式结果的字段兼容的值（例如，小数）。

**示例**:用于显示字段1中两个字段总和的计 **算表达式** 为： 
`field2.value + field3.value`

### 单击表达式{#click-expression}

点击表达式可处理对按钮的点击事件执行的操作。 GuideBridge提供了可执行各种功能（如提交、验证与点击表达式一起使用的功能）的开箱即用API。 有关API的完整列表，请参阅[GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

**适用于**:按钮字段

**返回类型**:点击表达式不返回任何值。如果任何表达式返回值，则忽略该值。

**示例**:要在按钮的点 **击操作中填充文本框1** (其值为 **AEM Forms**)，按钮的点击表达式为  `textbox1.value="AEM Forms"`

### 初始化脚本 {#initialization-script}

初始化自适应表单时，会触发初始化脚本。 根据不同情况，初始化脚本的行为方式如下：

* 当在不使用数据预填充的情况下呈现自适应表单时，初始化脚本将在表单初始化后运行。
* 使用数据预填充呈现自适应表单时，脚本将在预填充操作完成后运行。
* 当触发自适应表单的服务器端重新验证时，将执行初始化脚本。

**适用于：** 字段和面板

**返回类型：** 初始化脚本表达式不返回任何值。如果任何表达式返回值，则忽略该值。

**示例：** 在数据预填充方案中，要在字段值另存为空 `'Adaptive Forms'` 值时使用默认值填充字段，初始化脚本表达式为： 
`if(this.value==null) this.value='Adaptive Forms';`

### 选项表达式{#options-expression}

选项表达式用于动态填充下拉列表字段的选项。

**适用于**:下拉列表字段

**返回类型**:选项表达式会返回一个字符串值数组。每个值都可以是一个简单的字符串，如&#x200B;**Male**，或以键=值对格式（如&#x200B;**1=Male**）表示

**示例**:要根据另一个字段的值填充字段的值，请提供简单的选项表达式。例如，要根据另一个字段中表示的&#x200B;**婚姻状态**&#x200B;填充字段&#x200B;**子女数**，表达式为：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

每当&#x200B;**frimery_status**&#x200B;字段的值发生更改时，将重新触发表达式。 您还可以从REST服务中填充下拉菜单。 有关详细信息，请参阅[动态填充下拉列表](../../forms/using/dynamically-populate-dropdowns.md)。

### 概要表达式 {#summary}

“摘要”表达式可动态计算折叠布局面板的子面板的标题。 您可以在规则中指定概要表达式，该表达式使用表单字段或自定义逻辑来评估标题。 表单初始化时，表达式会执行。 如果要预填表单，则在预填数据后或表达式中使用的从属字段值发生更改时，将执行表达式。

摘要表达式通常用于重复折叠布局面板的子项，以便为每个子面板提供有意义的标题。

**适用于：** 布局配置为折叠项的面板的直接子级面板。

**返回类型：** 表达式会返回一个字符串，该字符串将成为折叠面板的标题。

**示例：** &quot;帐号：&quot; + textbox1.value

### 验证表达式{#validate-expression}

验证表达式用于使用给定表达式验证字段。 通常，此类表达式会使用正则表达式和字段值来验证字段。 将重新触发表达式，并根据字段值的任何更改重新计算字段的验证状态。

**适用于**:字段

**返回类型**:表达式会返回一个布尔值，表示字段的验证状态。值&#x200B;**false**&#x200B;表示字段无效，而值&#x200B;**true**表示字段有效。
**示例**:对于表示英国邮政编码的字段，验证表达式为：

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上例中，如果非空值与模式不匹配，表达式会返回&#x200B;**false**&#x200B;以指示字段无效。

>[!NOTE]
>
>如果为非必填或必填字段编写验证表达式，则无论该字段的可见性状态如何，都会计算该表达式。 要停止对隐藏字段的验证，请将Initialization或Value Commit脚本中的validationsDisabled属性设置为true。 例如，`this.validationsDisabled=true`

### 值提交脚本 {#value-commit-script}

Value Commit脚本在以下情况下触发：

* 用户从UI更改字段的值。
* 由于其他字段中的更改，字段的值会以编程方式更改。

**适用于：** 字段

**返回类型：** 值提交脚本表达式不返回任何值。如果任何表达式返回值，则忽略该值。

**示例：** 要在提交时将字段中输入的字母的大小写转换为大写，值提交表达式为： 
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>当字段的值以编程方式更改时，您可以禁用执行Value Commit脚本。 为此，请转到https://&#39;[server]:[port]&#39;/system/console/configMgr，并将&#x200B;**Adaptive Forms Version for Compatibility**&#x200B;更改为&#x200B;**AEM Forms 6.1**。 之后，仅当用户从UI更改字段值时，才执行值提交脚本。

### 可见性表达式 {#visibility-expression}

可见性表达式用于控制字段/面板的可见性。 通常，可见性表达式使用字段的value属性，并在该值发生更改时重新触发。

**适用于**:字段和面板

**返回类型**:表达式会返回一个布尔值，表示字段/面板是否可见。**** false表示字段或面板不可见，true表示字段或面板可见。

**示例**:对于仅当字段1的值设置为“ **Male** ”时才会显 ****&#x200B;示的面板，可见性表达式为：  `field1.value == "Male"`

### 步骤完成表达式{#step-completion-expression}

步骤完成表达式用于阻止用户进入向导布局的下一步。 当面板具有向导布局时（多步表单一次显示一个步骤），会使用这些表达式。 仅当当前部分中的所有必需值都已填充且有效时，用户才能移至下一步、面板或子部分。

**适用于**:将项目布局设置为向导的面板。

**返回类型**:表达式会返回一个布尔值，表示当前面板是否有效。**** true表示当前面板有效，用户可以导航到下一个面板。

**示例**:在各个面板中组织的表单中，先验证当前面板，然后再导航到下一个面板。在这种情况下，使用步骤完成表达式。 通常，这些表达式使用GuideBridge验证API。 步骤完成表达式的示例如下：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 自适应表单{#validations-in-adaptive-form}中的验证

向自适应表单添加字段验证的方法有多种。 如果在字段中添加了验证检查，则&#x200B;**True**&#x200B;表示在字段中输入的值有效。 **** False表示值无效。如果在字段中输入和输出选项卡，则不会生成错误消息。

对字段添加验证的方法包括：

### 必填 {#required}

要强制使组件成为必需组件，请在组件的&#x200B;**编辑**&#x200B;对话框中，选择选项&#x200B;**标题和文本>必需**。 您还可以添加相应的&#x200B;**必需消息**（可选）。.

### 验证模式{#validation-patterns}

一个字段有多个现成的验证模式。 要选择验证模式，请在组件的&#x200B;**编辑**&#x200B;对话框中，找到&#x200B;**模式**&#x200B;部分，然后选择&#x200B;**模式**。 您可以在&#x200B;**模式**&#x200B;文本框中创建自己的自定义验证模式。 仅当填充的数据符合验证模式时，才返回&#x200B;**True**&#x200B;验证状态，否则返回&#x200B;**False**。 要编写您自己的自定义验证模式，请参阅[Picture子句对HTML5表单](/help/forms/using/picture-clause-support.md)的支持。

### 验证表达式{#validation-expressions}

也可以使用不同字段上的表达式计算字段的验证。 这些表达式写入组件&#x200B;**编辑**&#x200B;对话框的&#x200B;**脚本**&#x200B;选项卡的&#x200B;**验证脚本**&#x200B;字段中。 字段的验证状态取决于表达式返回的值。 有关如何编写此类表达式的信息，请参阅[验证表达式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)。

## 附加信息 {#additional-information}

### 使用字段显示格式{#using-field-display-format}

显示格式可用于以不同格式显示数据。 例如，您可以使用显示格式显示带连字符的电话号码、设置邮政编码格式或日期选取器。 这些显示模式可从组件“编辑”对话框的&#x200B;**模式**&#x200B;部分中选择。 您可以编写与上述验证模式类似的自定义显示模式。

### GuideBridge - API和事件{#guidebridge-apis-and-events}

GuideBridge是API的集合，可用于与浏览器中内存模型中的自适应表单进行交互。 有关指南桥API、类方法和事件公开的详细介绍，请参阅[自适应表单的JavaScript库API引用](https://helpx.adobe.com/aem-forms/6/javascript-api/)。

>[!NOTE]
>
>建议不要在表达式中使用GuideBridge事件侦听器。

#### 各种表达式{#guidebridge-usage-in-various-expressions}中的GuideBridge用法

* 要重置表单字段，您可以在按钮的点击表达式中触发`guideBridge.reset()` API。 同样，还有一个提交API，它可以作为点击表达式&#x200B;`guideBridge.submit()`**调用。**

* 您可以使用`setFocus()` API在各个字段或面板中设置焦点（对于面板焦点，会自动设置为第一个字段）。 `setFocus()`提供了多种导航选项，例如跨面板导航、先前/后次遍历、将焦点设置到特定字段等。例如，要移到下一个面板，您可以使用：`guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 要验证自适应表单或其特定面板，请使用`guideBridge.validate(errorList, somExpression).`

#### 在表达式之外使用GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

您还可以在表达式之外使用GuideBridge API。 例如，您可以使用GuideBridge API设置托管自适应表单的页面HTML与表单模型之间的通信。 此外，您还可以设置来自托管表单的Iframe父代的值。

要对上述示例使用GuideBridge API，请捕获GuideBridge的实例。 要捕获实例，请侦听`window`对象的`bridgeInitializeStart`事件：

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>在AEM中，最好在clientLib中写入代码，并将其包含在您的页面（页面的header.jsp或footer.jsp）中

要在初始化表单后使用GuideBridge（调度`bridgeInitializeComplete`事件），请使用`window.guideBridge`获取GuideBridge实例。 您可以使用`guideBride.isConnected` API检查GuideBridge初始化状态。

#### GuideBridge事件{#guidebridge-events}

GuideBridge还为托管页面上的外部脚本提供某些事件。 外部脚本可以侦听这些事件并执行各种操作。 例如，每当表单中的用户名发生更改时，页面标题中显示的名称也会发生更改。 有关此类事件的更多详细信息，请参阅[自适应表单的JavaScript库API引用](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)。

使用以下代码注册处理程序：

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 为字段{#creating-custom-patterns-for-a-field}创建自定义模式

如上所述，自适应表单允许作者提供验证或显示格式的模式。 除了使用开箱即用的模式之外，您还可以为自适应表单组件定义可重用的自定义模式。 例如，您可以定义文本字段或数字字段。 定义后，您可以在所有表单中为指定类型的组件使用这些模式。 例如，您可以为文本字段创建自定义模式，并将其用于其自适应表单的文本字段中。 您可以通过访问组件编辑对话框中的模式部分来选择自定义模式。 有关模式定义或格式的详细信息，请参阅[Picture子句对HTML5表单的支持](/help/forms/using/picture-clause-support.md)。

请执行以下步骤，为特定字段类型创建自定义模式，并将其重复用于同类型的其他字段：

1. 导航到创作实例上的CRXDE Lite。
1. 创建文件夹以维护自定义模式。 在/apps目录下，创建sling:folder类型的节点。 例如，创建名为`customPatterns`的节点。 在此节点下，创建另一个类型为`nt:unstructed`的节点，并将其命名为`textboxpatterns`。 此节点包含您要添加的各种自定义模式。
1. 打开所创建节点的属性选项卡。 例如，打开`textboxpatterns`的“属性”选项卡。 将`guideComponentType`属性添加到此节点，并将其值设置为&#x200B;*fd/af/components/formatter/guideTextBox*。

1. 此属性的值会因您要为其定义模式的字段而异。 对于数值字段，`guideComponentType`属性的值为&#x200B;*fd/af/components/formatter/guideNumericBox*。 “日期选取器”字段的值为&#x200B;*fd/af/components/formatter/guideDatepicker*。
&quot;
1. 您可以通过向`textboxpatterns`节点分配属性来添加自定义模式。 添加名为的属性（例如`pattern1`），并将其值设置为要添加的模式。 例如，添加值为Fax=text{99-999-9999999}的属性`pattern1`。 该模式适用于您在自适应Forms中使用的所有文本框。

   ![为CrxDe中的字段创建自定义模式](assets/creating-custom-patterns.png)

   创建自定义模式
