---
title: 自适应表单规则编辑器
seo-title: 自适应表单规则编辑器
description: 自适应表单规则编辑器允许您添加动态行为并将复杂逻辑构建到表单中，而无需编码或脚本编写。
seo-description: 自适应表单规则编辑器允许您添加动态行为并将复杂逻辑构建到表单中，而无需编码或脚本编写。
uuid: c1b3d6e4-6f36-4352-ab57-9850d718e47c
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 自适应表单规则编辑器{#adaptive-forms-rule-editor}

## 概述 {#overview}

Adobe Experience Manager Forms中的规则编辑器功能使表单商业用户和开发人员能够编写自适应表单对象的规则。 这些规则根据预设条件、用户输入和用户对表单的操作定义对表单对象触发的操作。 它有助于进一步简化表单填写体验，确保准确性和速度。

规则编辑器提供了直观且简化的用户界面来编写规则。 规则编辑器为所有用户优惠一个可视编辑器。 此外，规则编辑器仅为高级表单用户提供代码编辑器来编写规则和脚本。 您可以使用规则对自适应表单对象执行的一些关键操作包括：

* 显示或隐藏对象
* 启用或禁用对象
* 为对象设置值
* 验证对象的值
* 执行函数以计算对象的值
* 调用表单数据模型服务并执行操作
* 设置对象的属性

规则编辑器取代了AEM 6.1 Forms及更早版本中的脚本功能。 但是，现有脚本将保留在新规则编辑器中。 有关在规则编辑器中使用现有脚本的详细信息，请参 [阅规则编辑器对现有脚本的影响](../../forms/using/rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p)。

添加到表单高级用户组的用户可以创建新脚本和编辑现有脚本。 表单用户组中的用户可以使用脚本，但不能创建或编辑脚本。

## 了解规则 {#understanding-a-rule}

规则是操作和条件的组合。 在规则编辑器中，操作包括隐藏、显示、启用、禁用或计算表单中对象值等活动。 条件是布尔表达式，通过对表单对象的状态、值或属性执行检查和操作来计算。 根据通过评估条件返回的值( `True` 或 `False`)执行操作。

规则编辑器提供了一组预定义的规则类型，如“时间”、“显示”、“隐藏”、“启用”、“禁用”、“设置值”和“验证”，以帮助您编写规则。 每个规则类型允许您定义规则中的条件和操作。 该文档进一步详细说明了每个规则类型。

规则通常遵循以下构造之一：

**条件——操作** 在此构造中，规则首先定义一个条件，然后定义一个动作以触发。 该构造类似于编程语言中的if-then语句。

在规则编辑器中，“ **When** ”（当）规则类型强制实施条件——操作构造。

**操作条件** 在此构造中，规则首先定义要触发的操作，然后定义要评估的条件。 此构造的另一个变体是action-condition-alternate操作，该操作还定义了在条件返回False时触发的替代操作。

规则编辑器中的显示、隐藏、启用、禁用、设置值和验证规则类型可强制执行操作条件规则构建。 默认情况下，“显示”的替代操作为“隐藏”,“启用”的替代操作为“禁用”，反之亦然。 您无法更改默认替代操作。

>[!NOTE]
>
>可用的规则类型（包括您在规则编辑器中定义的条件和操作）也取决于您创建规则时所依据的表单对象的类型。 规则编辑器仅显示用于为特定表单对象类型编写条件和操作语句的有效规则类型和选项。 例如，您看不到面板对象的验证、设置值、启用和禁用规则类型。

有关规则编辑器中可用的规则类型的详细信息，请参阅规 [则编辑器中的可用规则类型](../../forms/using/rule-editor.md#p-available-rule-types-in-rule-editor-p)。

### 选择规则构造的准则 {#guidelines-for-choosing-a-rule-construct}

虽然使用任何规则构建都可以实现大多数用例，但以下是选择一个构建而不是另一个构建的一些准则。 有关规则编辑器中可用规则的详细信息，请参阅规 [则编辑器中的可用规则类型](../../forms/using/rule-editor.md#p-available-rule-types-in-rule-editor-p)。

* 创建规则时，通常的经验法则是在要编写规则的对象上下文中考虑它。 请考虑根据用户在字段A中指定的值隐藏或显示字段B。在这种情况下，您将评估字段A上的条件，并根据它返回的值，触发字段B上的操作。

   因此，如果您正在字段B上编写规则（您对其评估条件的对象），请使用条件——操作构造或“当”规则类型。 同样，在字段A上使用操作条件构造或显示或隐藏规则类型。

* 有时，您需要根据一个条件执行多个操作。 在这种情况下，建议使用条件——操作构造。 在此构造中，可以对一个条件求一次值并指定多个操作语句。

   例如，要根据检查用户在字段A中指定的值的条件隐藏字段B、C和D，请使用条件——操作构造或在字段A上的规则类型编写一个规则，并指定控制字段B、C和D的可见性的操作。否则，您需要对字段B、C和D分别使用三个规则，其中每个规则检查条件并显示或隐藏相应的字段。 在此示例中，在一个对象上编写When规则类型比在三个对象上显示或隐藏规则类型更有效。

* 要根据多个条件触发动作，建议使用动作条件构造。 例如，要通过评估字段B、C和D上的条件来显示和隐藏字段A，请对字段A使用显示或隐藏规则类型。
* 如果规则包含一个条件的操作，则使用条件——操作或操作条件构造。
* 如果规则检查某个条件并在字段中提供值或退出字段时立即执行操作，则建议在对条件进行评估的字段上使用条件——操作构造或“当”规则类型编写规则。
* 当用户更改应用了When规则的对象的值时，将计算When规则中的条件。 但是，如果您希望操作在服务器端的值发生变化时触发（例如预填充值时），建议编写在字段初始化时触发操作的When规则。
* 编写下拉、单选按钮或复选框对象的规则时，表单中这些表单对象的选项或值会预填充到规则编辑器中。

## 规则编辑器中可用的运算符类型和事件 {#available-operator-types-and-events-in-rule-editor}

规则编辑器提供了以下逻辑运算符和事件，您可以使用它们创建规则。

* **等于**
* **不等于**
* **开始**
* **结束于**
* **包含**
* **为空**
* **不为空**
* **已选择：** 当用户为复选框、下拉框和单选按钮选择特定选项时，返回true。
* **已初始化(事件):** 当表单对象在浏览器中呈现时，返回true。
* **更改(事件):** 当用户更改表单对象的输入值或选定选项时，返回true。

## 规则编辑器中的可用规则类型 {#available-rule-types-in-rule-editor}

规则编辑器提供了一组预定义的规则类型，您可以使用这些类型编写规则。 我们来详细看一下每个规则类型。 有关在规则编辑器中编写规则的详细信息，请参阅 [编写规则](../../forms/using/rule-editor.md#p-write-rules-p)。

### 当 {#whenruletype}

当规 **则类型遵循条件-** action-alternate操作规则构造时 **，或者有时只遵循条件-** action构造 **** 。 在此规则类型中，您首先指定一个评估条件，然后在满足条件时触发一个操作( `True`)。 在使用“当”规则类型时，可以使用多个AND和OR运算符创建嵌套 [表达式](#nestedexpressions)。

使用“当”(When)规则类型，可以评估表单对象上的条件并对一个或多个对象执行操作。

简言之，典型的“当”规则的结构如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

对对象B采取操作2;C对象上的ANDAction 3;

_

当您有多值组件(如单选按钮或列表)时，在为该组件创建规则时，会自动检索这些选项并将其提供给规则创建者。 您无需再次键入选项值。

例如，列表有四个选项：红色、蓝色、绿色和黄色。 创建规则时，会自动检索选项（单选按钮），并将这些选项提供给规则创建者，如下所示：

![多值显示选项](assets/multivaluefcdisplaysoptions.png)

在编写“当时”规则时，可以触发“清除值”动作。 “清除值”(Clear Value Of)操作将清除指定对象的值。 将“清除值”设置为When语句中的选项，可创建包含多个字段的复杂条件。

![clearvalues](assets/clearvalueof.png)

**隐藏** 隐藏指定的对象。

**显示** “显示指定的对象”。

**启用** 启用指定的对象。

**禁用** 禁用指定的对象。

**调用服务** 调用在表单数据模型中配置的服务。 选择“调用服务”操作时，将显示一个字段。 点击该字段后，它将显示在AEM实例上所有表单数据模型中配置的所有服务。 在选择表单数据模型服务时，将显示其他字段，您可以在其中使用指定服务的输入和输出参数映射表单对象。 请参阅调用表单数据模型服务的示例规则。

除了表单数据模型服务外，还可以指定直接WSDL URL来调用Web服务。 但是，表单数据模型服务具有许多优点和建议的调用服务的方法。

有关在表单数据模型中配置服务的详细信息，请参 [阅AEM表单数据集成](/help/forms/using/data-integration.md)。

**设置值** Computes并设置指定对象的值。 您可以将对象值设置为字符串、另一个对象的值、使用数学表达式或函数计算的值、对象属性的值或配置的表单数据模型服务的输出值。 当您选择Web服务选项时，它将显示在AEM实例上所有表单数据模型中配置的所有服务。 在选择表单数据模型服务时，将显示其他字段，您可以在其中使用指定服务的输入和输出参数映射表单对象。

有关在表单数据模型中配置服务的详细信息，请参 [阅AEM表单数据集成](/help/forms/using/data-integration.md)。

“设 **置属性** ”(Set Property)规则类型允许您基于条件操作设置指定对象的属性值。

它允许您定义规则以动态地向自适应表单添加复选框。 您可以使用自定义函数、表单对象或对象属性来定义规则。

![设置属性](assets/set_property_rule_new.png)

要根据自定义函数定义规则，请从下拉列表中选择 **Function Output** ，然后从“Functions”（函数）选项卡中拖放自定义函数 **** 。 如果满足条件操作，则自定义函数中定义的复选框数将添加到自适应表单。

要定义基于表单对象的规则，请从下拉列表中选择 **Form Object** ，然后从“表单对象”选项卡中拖放一个表单 **对象** 。 如果满足条件操作，则在表单对象中定义的复选框数将添加到自适应表单。

基于对象属性的设置属性规则允许您根据自适应表单中包含的另一个对象属性在自适应表单中添加复选框的数量。

下图描述了根据自适应表单中的下拉列表数动态添加复选框的示例：

![对象属性](assets/object_property_set_property_new.png)

**清除值** ：清除指定对象的值。

**设置焦点** ：将焦点集聚焦到指定的对象。

**保存表单** 保存表单。

**提交表单** 提交表单。

**重置表单** 重置表单。

**验证表单** 验证表单。

**添加实例** ：添加指定的可重复面板或表行的实例。

**删除实例** ：删除指定的可重复面板或表行的实例。

**导航到** “导航到其他交互通信”、自适应表单、图像或文档片段等其他资产或外部URL。 有关详细信息，请参 [阅向交互式通信添加按钮](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel)。

### 设置值{#set-value-of}

规则 **[!UICONTROL 类型的“设置值]** ”(Set Value)允许您根据是否满足指定的条件来设置表单对象的值。 该值可以设置为另一个对象的值、文本字符串、从数学表达式或函数派生的值、另一个对象的属性的值或表单数据模型服务的输出。 同样，您可以检查从函数或数学表达式派生的组件、字符串、属性或值上的条件。

请注意，“设置规则类型的值”并非适用于所有表单对象，如面板和工具栏按钮。 标准的“设置值”规则具有以下结构：



将对象A的值设置为：

(string ABC)OR（对象C的对象属性X）OR（函数值）OR(数学表达式值)OR（数据模型服务或Web服务的输出值）;

When（可选）:

（条件1和条件2和条件3）为TRUE;



以下示例将字段中的 `dependentid` 值作为输入，并将字段的值设置为表单数据模型服务 `Relation` 的参数 `Relation``getDependent` 的输出。

![set-value-web-service](assets/set-value-web-service.png)

使用表单数据模型服务的设置值规则示例

>[!NOTE]
>
>此外，您还可以使用“设置规则值”从表单数据模型服务或Web服务的输出填充下拉式列表组件中的所有值。 但是，请确保您选择的输出参数为数组类型。 数组中返回的所有值在指定的下拉列表中都可用。

### 显示 {#show}

使用“ **显示** ”规则类型，您可以编写规则来根据是否满足条件显示或隐藏表单对象。 在条件不满足或返回时，显示规则类型也会触发隐藏操作 `False`。

典型的“显示”规则的结构如下：



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### 隐藏 {#hide}

与“显示”规则类型类似，您可以使用 **Hide** rule类型根据是否满足条件显示或隐藏表单对象。 如果条件不满足或返回，“隐藏”规则类型也会触发“显示”(Show)操作 `False`。

典型的隐藏规则的结构如下：



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### 启用 {#enable}

通过 **“启用** ”规则类型，您可以根据是否满足条件启用或禁用表单对象。 在条件不满足或返回时，启用规则类型也会触发禁用操作 `False`。

典型的“启用”规则的结构如下：



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### 禁用 {#disable}

与启用规则类型类似， **** 禁用规则类型允许您根据是否满足条件启用或禁用表单对象。 如果条件不满足或返回，则禁用规则类型也会触发启用操作 `False`。

典型的禁用规则如下所示：



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### 验证 {#validate}

“验 **证** ”规则类型使用表达式验证字段中的值。 例如，您可以编写表达式来检查用于指定名称的文本框是否不包含特殊字符或数字。

典型的验证规则的结构如下：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值与“验证”规则不符，则可以向用户显示验证消息。 您可以在提要栏的组件属性的 **[!UICONTROL “脚本验证消息]** ”字段中指定消息。

![脚本验证](assets/script-validation.png)

### Set Options Of {#setoptionsof}

规则 **类型的“设置选项** ”(Set Options Of)允许您定义规则，以将复选框动态添加到自适应表单。 您可以使用表单数据模型或自定义函数来定义规则。

要根据自定义函数定义规则，请从下拉列表中选择 **Function Output** ，然后从“Functions”（函数）选项卡中拖放自定义函数 **** 。 自定义函数中定义的复选框数将添加到自适应表单中。

![自定义函数](assets/custom_functions_set_options_new.png)

要创建自定义函数，请参阅规 [则编辑器中的自定义函数](../../forms/using/rule-editor.md#main-pars-header-296220653)。

要定义基于表单数据模型的规则，请执行以下操作：

1. 从 **下拉列表中** ，选择服务输出。
1. 选择数据模型对象。
1. 从显示值下拉列表中选 **择数据模型对象** 属性。 自适应表单中的复选框数量是从数据库中为该属性定义的实例数量中派生的。
1. 从“保存值”(Save Value **** )下拉列表中选择数据模型对象属性。

![FDM设置选项](assets/fdm_set_options_new.png)

## 了解规则编辑器用户界面 {#understanding-the-rule-editor-user-interface}

规则编辑器提供了一个全面而简单的用户界面，用于编写和管理规则。 您可以在创作模式下从自适应表单中启动规则编辑器用户界面。

要启动规则编辑器用户界面，请执行以下操作：

1. 在创作模式下打开自适应表单。
1. 点按要为其编写规则的表单对象，然后在组件工具栏中点按 ![edit-rules](assets/edit-rules.png)。 将显示规则编辑器用户界面。

   ![create-rules](assets/create-rules.png)

   此视图中列出了选定表单对象的任何现有规则。 有关管理现有规则的信息，请参阅 [管理规则](../../forms/using/rule-editor.md#p-manage-rules-p)。

1. 点按 **[!UICONTROL 创建]** ，以编写新规则。 默认情况下，在您首次启动规则编辑器时，将打开规则编辑器用户界面的可视编辑器。
[规 ![则编辑器UI](assets/rule-editor-ui.png)

   单击以视图放大的图像

   ](assets/rule-editor-ui-1.png)让我们详细查看规则编辑器UI的每个组件。

### 答：组件规则显示 {#a-component-rule-display}

显示用于启动规则编辑器的自适应表单对象的标题以及当前选定的规则类型。 在上例中，规则编辑器从标题为Salary的自适应表单对象启动，所选规则类型为When。

### B. Form objects and functions {#b-form-objects-and-functions-br}

规则编辑器用户界面左侧的窗格包括两个选项卡： 表 **[!UICONTROL 单对象]** 和 **[!UICONTROL 函数]**。

“表单对象”选项卡显示自适应表单中包含的所有对象的分层视图。 它显示对象的标题和类型。 编写规则时，可以将表单对象拖放到规则编辑器上。 在创建或编辑规则时，将对象或函数拖放到占位符中时，占位符会自动采用相应的值类型。

应用了一个或多个有效规则的表单对象将标有绿点。 如果应用于表单对象的任何规则无效，则表单对象将标有黄点。

“函数”选项卡包括一组内置函数，如“总和”、“最小值”、“最大值”、“平均值”、“数量”和“验证表单”。 您可以使用这些函数在可重复面板和表行中计算值，并在编写规则时在操作和条件语句中使用它们。 但是，您也可以创建自 [定义函数](../../forms/using/rule-editor.md#custom-functions) 。

![“函数”选项卡](assets/functions.png)

>[!NOTE]
>
>您可以在“表单对象”和“函数”选项卡中对对象和函数名称和标题执行文本搜索。

在表单对象的左树中，您可以点按表单对象以显示应用于每个对象的规则。 您不仅可以浏览各种表单对象的规则，还可以在表单对象之间复制粘贴规则。 有关详细信息，请 [参阅复制粘贴规则](../../forms/using/rule-editor.md#p-copy-paste-rules-p)。

### C.表单对象和功能切换 {#c-form-objects-and-functions-toggle-br}

点击切换按钮可切换表单对象和函数窗格。

### D.可视规则编辑器 {#d-visual-rule-editor}

可视规则编辑器是规则编辑器用户界面的可视编辑器模式中用于编写规则的区域。 它允许您选择规则类型并相应地定义条件和操作。 在规则中定义条件和操作时，可以从“表单对象和函数”窗格拖放表单对象和函数。

有关使用可视规则编辑器的详细信息，请参阅 [编写规则](../../forms/using/rule-editor.md#p-write-rules-p)。

### E.可视代码编辑器切换器 {#e-visual-code-editors-switcher}

表单用户组中的用户可以访问代码编辑器。 对于其他用户，代码编辑器不可用。 如果您有权限，则可以使用规则编辑器正上方的切换器从可视编辑器模式切换到规则编辑器的代码编辑器模式，反之亦然。 首次启动规则编辑器时，该编辑器会在可视编辑器模式下打开。 您可以在可视编辑器模式下编写规则，也可以切换到代码编辑器模式以编写规则脚本。 但是，请注意，如果您修改规则或在代码编辑器中编写规则，则无法切换回该规则的可视编辑器，除非清除代码编辑器。

AEM Forms会跟踪您上次用于编写规则的规则编辑器模式。 下次启动规则编辑器时，该编辑器将以该模式打开。 但是，您也可以配置默认模式以在指定模式下打开规则编辑器。 为此，请执行以下操作：

1. 转到AEM Web控制台(位于 `https://[host]:[port]/system/console/configMgr`)。
1. 单击以编辑 **[!UICONTROL 自适应表单配置服务]**。
1. 从规 **[!UICONTROL 则编辑器的默]** 认模式下拉菜单中选择可视编辑器 ******** ，或选择代码编辑器。

1. 单击&#x200B;**[!UICONTROL 保存]**。

### F.完成和取消按钮 {#f-done-and-cancel-buttons}

“完 **[!UICONTROL 成]** ”按钮用于保存规则。 可保存不完整的规则。 但是，未完成无效且不执行。 下次从同一表单对象启动规则编辑器时，将列出表单对象上保存的规则。 您可以管理该视图中的现有规则。 有关详细信息，请参阅 [管理规则](../../forms/using/rule-editor.md#p-manage-rules-p)。

“取 **[!UICONTROL 消]** ”按钮将放弃您对规则所做的任何更改并关闭规则编辑器。

## 编写规则 {#write-rules}

您可以使用可视规则编辑器或代码编辑器编写规则。 首次启动规则编辑器时，该编辑器会在可视编辑器模式下打开。 您可以切换到代码编辑器模式并编写规则。 但是，请注意，如果您在代码编辑器中编写或修改规则，则无法切换到该规则的可视编辑器，除非清除代码编辑器。 下次启动规则编辑器时，该编辑器将以您上次用于创建规则的模式打开。

我们首先来看如何使用可视编辑器编写规则。

### 使用可视编辑器 {#using-visual-editor}

让我们了解如何使用以下示例表单在可视编辑器中创建规则。

![create-rule-example](assets/create-rule-example.png)

贷款申请表示例中的“贷款要求”部分要求申请人指定其婚姻状况、薪金，如果结婚，则指定其配偶的薪金。 该规则根据用户输入计算贷款资格金额并显示在“贷款资格”字段中。 应用以下规则以实施方案：

* “配偶的工资”字段仅在“婚姻状态”为“已婚”时显示。
* 贷款资格金额是总工资的50%。

请执行以下步骤来编写规则：

1. 首先，根据用户为“婚姻状态”单选按钮选择的选项，编写规则以控制“配偶工资”字段的可见性。

   在创作模式下打开贷款申请表。 点按“婚 **姻状态** ”组件并点 ![按edit-rules](assets/edit-rules.png)。 然后，点按创 **[!UICONTROL 建]** ，启动规则编辑器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   当您启动规则编辑器时，默认情况下会选择规则。 此外，在When语句中指定了从中启动规则编辑器的表单对象（本例中为“婚姻状态”）。

   当您无法更改或修改选定对象时，可以使用规则下拉列表选择其他规则类型，如下所示。 如果要在另一个对象上创建规则，请点按取消以退出规则编辑器，然后从所需的表单对象中再次启动它。

1. 点 **[!UICONTROL 按选择状态]** ，下拉列表中的 **[!UICONTROL 选择等于]**。 将显 **[!UICONTROL 示“输入字符串]** ”字段。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在“婚姻状态”单选按钮中，分 **别为“已婚** ”和“单一 **”选** 项分配0 **和** 1个“婚姻状 **** 态”值。 您可以验证在“编辑”单选按钮对话框的“标题”选项卡中分配的值，如下所示。

   ![来自规则编辑器的单选按钮值](assets/radio-button-values.png)

1. 在规 **则的输入字符串** ，指定 **0**。

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已将条件定义为 `When Marital Status is equal to Married`。 接下来，定义在此条件为True时要执行的操作。

1. 在Then语句中，从选 **[!UICONTROL 择]****[!UICONTROL 操作下拉框中选]** 择显示。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 将“配偶薪金”字 **段从“放置”对象的“表单对象** ”选项卡中拖 **放，或选择此处字段** 。 或者，点按放 **置对象或选择此处****** ，然后从弹出菜单中选择配偶薪金字段，该字段将列表表单中的所有表单对象。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   规则在规则编辑器中显示如下。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   点按 **完成** ，以保存规则。

1. 重复第1步到第5步，以定义另一个规则，在婚姻状态为“单身”时隐藏“配偶工资”字段。 规则在规则编辑器中显示如下。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您也可以在“配偶薪金”字段中编写一个“显示”规则，而不是在“婚姻状态”字段中编写两个“当”规则，以实施相同的行为。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接下来，编写一条规则以计算贷款资格金额（即总工资的50%），并在“贷款资格”字段中显示该金额。 为此，请在“贷款 **资格”字段中创建** “规则的设置值”。

   在创作模式中，点按贷 **[!UICONTROL 款资格字段]** ，然后点 ![按edit-rules](assets/edit-rules.png)。 然后，点按创 **[!UICONTROL 建]** ，启动规则编辑器。

1. 从 **[!UICONTROL 规则下拉菜单中选择]** “设置规则值”。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 点按 **[!UICONTROL 选择选项]** ，然后选择 **[!UICONTROL 数学表达式]**。 将打开一个用于编写数学表达式的字段。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在表达式字段中：

   * 从“表单对象”选项卡的第一个“拖放”对象中的“ **薪金** ”字段中选择或拖 **放，或选择此处字段** 。

   * 从“选 **择运算符** ”字段 **中选择加号** 。

   * 从“表单对象”选项卡中选择或拖放另一“放置”对 **象中的“配偶薪金** ”字段， **或选择此处字段** 。
   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下来，点按表达式字段周围高亮显示的区域，然后点按扩 **展表达式**。

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在扩展表达式字段中，从 **选择运算符字** 段中选择除 **，从选择选项字段中选********** 择编号。 然后，在 **数字字段** 中指定2。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以通过使用组件、函数、数学表达式和“选择选项”字段中的属性值创建复杂表达式。

   接下来，创建一个条件，当返回True时，表达式将执行。

1. 点按 **添加条件** ，以添加When语句。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When语句中：

   * 从“表单对象”选项卡的第一个“放置”对象的“婚姻状 **态** ”字段中选择或拖 **放，或选择此处字段** 。

   * 从“**选择运算符** ”字 **段中选择等于** 。

   * 在另一个“放置”对 **象中选择“字符串”** ，或选择此处字段，并在“输入字符串”字段中指定“已结婚” ******** 。
   规则最后在规则编辑器中显示如下。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   点按 **完成** ，以保存规则。

1. 重复第7步到第12步，以定义另一个规则，在婚姻状态为“单一”时计算贷款资格。 规则在规则编辑器中显示如下。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您也可以使用“设置值”规则计算您创建的用于显示——隐藏“配偶薪金”字段的“何时”规则中的贷款资格。 “婚姻状态”为“单一”时生成的组合规则在规则编辑器中显示如下。
>
>同样，您可以编写一个组合规则来控制“配偶工资”字段的可见性，并在“婚姻状态”为“已婚”时计算贷款资格。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

### 使用代码编辑器 {#using-code-editor}

添加到表单高级用户组的用户可以使用代码编辑器。 规则编辑器会自动为您使用可视编辑器创建的任何规则生成JavaScript代码。 您可以从可视编辑器切换到代码编辑器以视图生成的代码。 但是，如果在代码编辑器中修改规则代码，则无法切换回可视编辑器。 如果您希望在代码编辑器而不是可视编辑器中编写规则，则可以在代码编辑器中重新编写规则。 可视代码编辑器切换器可帮助您在两种模式之间切换。

代码编辑器JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，并使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关自适应表单类、事件、对象和公共API的完整列表，请参阅自适应表单的 [JavaScript库API参考](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)。

有关在代码编辑器中编写规则的准则的详细信息，请参阅自适 [应表单表达式](/help/forms/using/adaptive-form-expressions.md)。

在规则编辑器中编写JavaScript代码时，以下可视提示可帮助您了解结构和语法：

* 语法亮点
* 自动缩进
* 表单对象、函数及其属性的提示和建议
* 自动完成表单组件名称和常见JavaScript函数

![javascriptrueditor](assets/javascriptruleeditor.png)

#### 规则编辑器中的自定义函数 {#custom-functions}

除了列在“函数输出”下的现成功 *能* （如“总和”）之外，您还可以编写您经常需要的自定义函数。 确保您编写的函数与上面的函数 `jsdoc` 一起使用。

需要 `jsdoc` 附带：

* 如果您需要自定义配置和说明。
* 由于在和注释中声明函数有多种方 `JavaScript,` 法，因此您可以跟踪函数。

有关详细信息，请 [参阅usejsdoc.org](https://usejsdoc.org/)。

支持的 `jsdoc` 标记：

* **专用**&#x200B;语法：私有 `@private`函数不作为自定义函数包含在内。

* **名称**&#x200B;语法：或 `@name funcName <Function Name>`者， `,` 您也可以使用： `@function funcName <Function Name>`**或**`@func``funcName <Function Name>`。
   `funcName` 是函数的名称（不允许使用空格）。
   `<Function Name>` 是函数的显示名称。

* **成员**&#x200B;语法：将 `@memberof namespace`命名空间附加到函数。

* **参数**&#x200B;语法：或 `@param {type} name <Parameter Description>`者，您也可以使用： `@argument``{type} name <Parameter Description>`**或者**`@arg``{type}``name <Parameter Description>`..
显示函数使用的参数。 一个函数可以有多个参数标签，每个参数的标签按出现顺序排列。
   `{type}` 表示参数类型。 允许的参数类型包括：

   1. 字符串
   1. 数字
   1. 布尔型
   所有其他参数类型都属于上述类型之一。 不支持“无”。 确保您选择了以上类型之一。 类型不区分大小写。 参数中不允许有空格 `name`。 `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **返回类型**&#x200B;语法：或 `@return {type}`者，您也可以使用 `@returns {type}`。
添加有关函数的信息，如其目标。
{type}表示函数的返回类型。 允许的返回类型有：

   1. 字符串
   1. 数字
   1. 布尔型
   所有其他退回类型均按上述某一种分类。 不支持“无”。 确保您选择了以上类型之一。 返回类型不区分大小写。

>[!NOTE]
>
>自定义函数之前的注释用于摘要。 摘要可扩展到多行，直到遇到标记。 将大小限制为单个规则生成器中的简明说明。

**添加自定义函数**

例如，您希望添加一个自定义函数，该函数计算正方形的面积。 侧长是用户输入到自定义函数中的内容，该功能可使用表单中的数字框接受。 计算的输出将显示在表单的另一个数字框中。 要添加自定义函数，您首先必须创建客户端库，然后将其添加到CRX存储库。

执行以下步骤以创建客户端库并将其添加到CRX存储库。

1. 创建客户端库。 有关详细信息，请 [参阅使用客户端库](/help/sites-developing/clientlibs.md)。
1. 在CRXDE中，向文件夹添 `categories`加字符串类型值为 `customfunction` 的属 `clientlib` 性。

   >[!NOTE]
   >
   >`customfunction`是示例类别。 您可以为在文件夹中创建的类别选择任意 `clientlib`名称。

在CRX存储库中添加客户端库后，请在自适应表单中使用它。 它允许您将自定义函数用作表单中的规则。 执行以下步骤以自适应表单添加客户端库。

1. 在编辑模式下打开表单。
要在编辑模式下打开表单，请选择一个表单，然后点按打 **开**。
1. 在编辑模式中，选择一个组件，然后点 ![按字段级别](assets/field-level.png) >自 **适应表单容器**，然后点 ![按cmppr](assets/cmppr.png)。
1. 在提要栏中，在“客户端库的名称”下，添加您的客户端库。 ( `customfunction` 在示例中。)

   ![添加自定义函数客户端库](assets/clientlib.png)

1. 选择输入数字框，然后点 ![按edit-rules](assets/edit-rules.png) 以打开规则编辑器。
1. 点按 **创建规则**。 使用下面显示的选项，创建一个规则以在表单的“输出”字段中保存输入的平方值。
   [ 使 ![用自定义函数创建规则](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)点按 **完成**。 您的自定义功能已添加。

#### 支持的函数声明类型 {#function-declaration-supported-types}

**函数语句**

```
function area(len) {
    return len*len;
}
```

此函数包含时不添加 `jsdoc` 注释。

**函数表达式**

```
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函数表达式和语句**

```
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函数声明为变量**

```
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自定义函数只从变量列表中选取第一个函数声明（如果是一起）。 您可以对声明的每个函数使用函数表达式。

**函数声明为对象**

```
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>确保对每个自定 `jsdoc` 义函数都使用。 尽管 `jsdoc`建议添加注释，但应包含一 `jsdoc`个空注释，以将您的函数标记为自定义函数。 它启用自定义函数的默认处理。

## 管理规则 {#manage-rules}

当您点按表单对象并点按edit-rules1时，将列出表单对象上的 ![任何现有规则](assets/edit-rules1.png)。 您可以视图标题和预览规则摘要。 此外，UI还允许您扩展和视图完整的规则摘要、更改规则的顺序、编辑规则和删除规则。

![列表规则](assets/list-rules.png)

您可以对规则执行以下操作：

* **展开／折叠**:规则列表中的“内容”列显示规则内容。 如果整个规则内容在默认视图中不可见，请点 ![按expand-rule-content](assets/expand-rule-content.png) 以展开它。

* **重新排序**:您创建的任何新规则都会堆放在规则列表的底部。 规则从上到下执行。 顶部的规则首先执行，后跟同一类型的其他规则。 例如，如果规则分别位于从上到下的第一、第二、第三和第四个位置的When、Show、Enable和When，则顶部的When规则首先被执行，后跟位于第四个位置的When规则。 然后，将执行“显示”和“启用”规则。
您可以通过点按规则排序来更 ![改规则的顺序](assets/sort-rules.png) ，或将规则拖放到列表中所需的顺序。

* **编辑**:要编辑规则，请选中规则标题旁边的复选框。 此时会显示用于编辑和删除规则的其他选项。 点按 **编辑** ，以可视或代码编辑器模式在规则编辑器中打开选定规则，具体取决于创建规则的模式。

* **删除**:要删除规则，请选择该规则，然后点按删 **除**。

* **启用／禁用**:您可能需要暂时暂停规则的使用。 您可以选择一个或多个规则，然后点按操作工具栏中的禁用以禁用这些规则。 如果某个规则被禁用，则它不会在运行时执行。 要启用已禁用的规则，您可以选择该规则，然后点按操作工具栏中的启用。 规则的状态列显示规则是启用还是禁用。

![disablerule](assets/disablerule.png)

## 复制粘贴规则 {#copy-paste-rules}

您可以将规则从一个字段复制并粘贴到其他类似字段以节省时间。

要复制粘贴规则，请执行以下操作：

1. 点按要从中复制规则的表单对象，然后在组件工具栏中点按编辑 ![规则](assets/editrule.png)。 将显示规则编辑器用户界面，同时选择表单对象并显示现有规则。

   ![文案规则](assets/copyrule.png)

   有关管理现有规则的信息，请参阅 [管理规则](../../forms/using/rule-editor.md#p-manage-rules-p)。

1. 选中规则标题旁边的复选框。 此时会显示用于管理规则的其他选项。 点按&#x200B;**复制**。

   ![copyrule2](assets/copyrule2.png)

1. 选择要将规则粘贴到的另一个表单对象，然后点按粘 **贴**。 此外，您还可以编辑规则以在其中进行更改。

   >[!NOTE]
   >
   >只有在表单对象支持复制的规则的事件时，才能将规则粘贴到其他表单对象。 例如，按钮支持单击事件。 您可以将带有单击事件的规则粘贴到按钮，但不能粘贴到复选框。

1. 点按 **完成** ，以保存规则。

## 嵌套表达式 {#nestedexpressions}

规则编辑器允许您使用多个AND和OR运算符创建嵌套规则。 您可以在规则中混合使用多个AND和OR运算符。

以下是嵌套规则的示例，该规则在满足所需条件时向用户显示有关子女托管资格的消息。

![络合表达](assets/complexexpression.png)

您还可以在规则中拖放条件以对其进行编辑。 点按并悬停在条件前 ![面的句柄](assets/handle.png)(handle)上。 当指针变为如下所示的手形符号后，将条件拖放到规则内的任意位置。 规则结构会更改。

![拖放](assets/drag-and-drop.png)

## 日期表达式条件 {#dateexpression}

规则编辑器允许您使用日期比较来创建条件。

下面是一个示例条件，如果房屋上的抵押已被抵押，则显示一个静态文本对象，用户通过填写日期字段来表示该条件。

当用户填写的物业抵押日期为过去时，自适应表单会显示收入计算的附注。 以下规则将用户填写的日期与当前日期进行比较，如果用户填写的日期早于当前日期，则表单将显示文本消息（名为“收入”）。

![dateexpressioncondition](assets/dateexpressioncondition.png)

当填写日期早于当前日期时，表单将显示以下文本消息（收入）:

![dateexpressionconditionment](assets/dateexpressionconditionmet.png)

## 数量比较条件 {#number-comparison-conditions}

规则编辑器允许您创建比较两个数字的条件。

以下是一个示例条件，如果申请人当前地址的月数小于36，则显示一个静态文本对象。

![数字比较条件](assets/numbercomparisoncondition.png)

当用户表示他住在他目前的居住地址不到36个月时，表格显示通知，可请求额外的居住验证。

![请求附加校对](assets/additionalproofrequested.png)

## 规则编辑器对现有脚本的影响 {#impact-of-rule-editor-on-existing-scripts}

在AEM 6.1 Forms功能包1之前的AEM Forms版本中，表单作者和开发人员用于在“编辑”组件对话框的“脚本”选项卡中编写表达式，以向自适应表单添加动态行为。 “脚本”选项卡现在由规则编辑器替换。

必须在“脚本”选项卡中编写的任何脚本或表达式在规则编辑器中都可用。 虽然您无法在可视编辑器中视图或编辑脚本，但如果您是表单高级用户组的一部分，则可以在代码编辑器中编辑脚本。

## 示例规则 {#example}

### Invoke form data model service {#invoke}

考虑使用贷 `GetInterestRates` 款金额、保有权和申请人的信用评分作为输入并返回贷款计划（包括EMI金额和利率）的Web服务。 使用Web服务作为数据源创建表单数据模型。 可向表单模型添加数据模 `get` 型对象和服务。 服务显示在表单数据模型的“服务”选项卡中。 然后，创建包含数据模型对象字段的自适应表单，以捕获贷款额、保有权和信用评分的用户输入。 添加一个按钮，用于触发Web服务以获取计划详细信息。 输出将填充到相应的字段中。

以下规则显示如何配置调用服务操作以完成示例方案。

![example-invoke-services](assets/example-invoke-services.png)

使用自适应表单规则调用表单数据模型服务

### 使用“时间”规则触发多个操作 {#triggering-multiple-actions-using-the-when-rule}

在贷款申请表中，您希望了解贷款申请人是否为现有客户。 根据用户提供的信息，客户ID字段应显示或隐藏。 此外，如果用户是现有客户，您还希望将焦点设置在客户ID字段上。 贷款申请表包含以下组件：

* 单选按钮，您 **是Geometrixx的现有客户吗？**，其中提供“是”和“否”选项。 “是”的值为 **0** ,“否”为 **1**。

* 用于指定客 **户ID的文本字段**,Geometrixx客户ID。

在单选按钮上编写“当”规则以实现此行为时，该规则在可视规则编辑器中显示如下。  ![when-rule-example](assets/when-rule-example.png)

可视编辑器中的规则

在示例规则中，When部分中的语句是条件，当返回True时，该条件将执行Then部分中指定的操作。

该规则在代码编辑器中显示如下。

![when-rule-example-code](assets/when-rule-example-code.png)

代码编辑器中的规则

### 在规则中使用函数输出 {#using-a-function-output-in-a-rule}

在采购订单表单中，您有下表，用户将在其中填写订单。 在此表中：

* 第一行是可重复的，因此用户可以订购多个产品并指定不同的数量。 其元素名称为 `Row1`。
* 可重复行的“产品数量”列中单元格的标题为“数量”。 此单元格的元素名称为 `productquantity`。
* 表中的第二行是不可重复的，该行中“产品数量”列中单元格的标题是“总数量”。

![example-function-table](assets/example-function-table.png)

**答：** Row1 **B。** 数 **量C.总数** 量

现在，您要为所有产品在“产品数量”列中添加指定数量，并在“总数量”单元格中显示总数。 要实现此目的，请在“总量”(Total Quantity)单元格中编写“设置值”(Set Value Of)规则，如下所示。

![example-function-output](assets/example-function-output.png)

可视编辑器中的规则

该规则在代码编辑器中显示如下。

![example-function-output-code](assets/example-function-output-code.png)

代码编辑器中的规则

### 使用表达式验证字段值 {#validating-a-field-value-using-expression}

在上一个示例中介绍的采购订单表中，您希望限制用户订购超过一个数量的任何定价超过10000的产品。 为此，您可以编写验证规则，如下所示。

![example-validate](assets/example-validate.png)

可视编辑器中的规则

该规则在代码编辑器中显示如下。

![example-validate-code](assets/example-validate-code.png)

代码编辑器中的规则

