---
title: 交互式通信和字母中的内联条件和重复
seo-title: Inline condition and repeat in Interactive Communications and letters
description: 通过在交互式通信和信件中使用内联条件和重复，您可以创建高度情境化且结构良好的通信。
seo-description: Using inline condition and repeat in Interactive Communications and letters, you can create communications that are highly contextual and well structured.
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
feature: Correspondence Management
exl-id: bc5d6c5b-c833-4849-aace-e07f8a522b32
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 0%

---

# 交互式通信和字母中的内联条件和重复{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## 内联条件 {#inline-conditions}

AEM Forms允许您在文本模块中使用内联条件来自动呈现依赖于与表单数据模型（在交互式通信中）或数据字典（在字母中）关联的上下文或数据的文本。 内联条件根据条件评估为true或false来显示特定内容。

条件对表单数据模型/数据字典或最终用户提供的数据值执行计算。 使用内联条件，您可以节省时间并减少人为错误，同时创建高度情境化和个性化的交互式通信/信件。

有关更多信息，请参阅:

* [创建交互式通信](../../forms/using/create-interactive-communication.md)
* [通信管理概述](/help/forms/using/cm-overview.md)
* [交互式通信中的文本](../../forms/using/texts-interactive-communications.md)

### 示例：使用规则条件化交互式通信中的内联文本 {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

要在交互式通信中条件化句子、段落或文本字符串，您可以在相应的文本文档片段中创建规则。 以下示例使用规则仅向交互式通信的美国收件人显示免费号码。

有关更多信息，请参阅中的在文本中创建规则 [交互式通信中的文本](../../forms/using/texts-interactive-communications.md).

在交互式通信中包含文本片段且代理使用代理UI准备交互式通信后，将评估收件人的（表单数据模型）数据，并且文本仅向美国境内的收件人显示。

### 示例：在信件中使用内联条件呈现相应的地址  {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

通过在相应的文本模块中插入内联条件，可以在信件中插入内联条件。 下面的示例使用两个条件来评估并显示相应的地址，即Sir或Ma&#39;am（基于DD元素Gender）。 使用类似的步骤，您可以创建其他条件。

>[!NOTE]
>
>如果您现有的资产包含旧的condition/repeat表达式（早于6.2 SP1 CFP 4），则资产会显示condition和repeat的旧语法。 但是，旧条件/重复项有效。 新旧条件/重复表达式相互兼容，以创建旧条件/重复表达式的嵌套组合。

1. 在相关的文本模块中，选择要条件化的文本部分并选择 **条件**.

   ![1_selecttext](assets/1_selecttext.png)

   此时将显示“条件”对话框，其中显示空条件。

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >无法保存空的或无效的条件表达式。 内部必须存在有效的条件表达式 `${}` 以保存表达式。

1. 执行以下操作可构造一个条件，用于评估所选/条件化文本是否显示在信件中，然后选择复选标记以保存表达式：

   双击一个DD元素以将其插入到条件中。 在对话框中插入相应的运算符并构造以下条件。

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   有关创建表达式的详细信息，请参见 **使用表达式生成器创建表达式和远程函数** 在 [表达式生成器](../../forms/using/expression-builder.md). 数据字典中的元素必须支持表达式中指定的值。 有关更多信息，请参阅 [数据字典](../../forms/using/data-dictionary.md).

   插入条件后，您可以将鼠标悬停在条件左侧的句柄上以查看条件。 可以选择控制滑块以查看条件的弹出菜单，从中可编辑或删除条件。

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. 通过选择文本插入相似条件 `Ma'am`.

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 预览相关信件，并注意文本已根据内联条件呈现。 可以使用以下方式输入DD元素Gender的值：

   * 在预览包含示例数据的信件时，根据相关数据字典创建的示例XML数据文件。
   * 附加到相关数据字典的XML数据文件。

   有关更多信息，请参阅 [数据字典](../../forms/using/data-dictionary.md).

   ![5_letteroutput](assets/5_letteroutput.png)

## 重复 {#repeat}

交互式通信/信件中可能包含动态信息，如信用卡对帐单中的交易，其实例或发生次数可能会随生成的每个信件而不断变化。 使用重复，您可以在文本文档片段中设置此类动态信息的格式和结构。

此外，您可以在重复构造中指定规则/条件，以条件化在交互式通信/信件中呈现的信息/条目。

### 示例：在交互式通信中使用重复来格式化、构造和显示信用卡交易列表 {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例为您提供了在交互式通信中使用重复来构造和呈现信用卡交易的步骤。

1. 在基于表单数据模型的文本文档片段中，插入相关的表单数据模型对象（以及标签所需的嵌入文本，如本示例所示）：

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >可重复内容必须至少包含一个类型为Collection的属性。

1. 选择要重复应用的内容。

   ![2_selection](assets/2_selection.png)

1. 选择“重复”。

   出现“重复”对话框。

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 选择换行符作为分隔符，并根据需要选择添加条件以创建规则。 也可以使用文本作为分隔符，并指定要用作分隔符的文本字符。

   此时将显示“创建规则”对话框。

1. 创建一个规则以显示日期在2018年2月28日之后的事务处理，以便在交互式通信中仅包含3月份的事务处理。

   >[!NOTE]
   >
   >此示例假定Agent将在2018年3月底创建语句。 否则，您可以创建另一个规则以包含2018-04-01之前的交易，以排除2018年3月之后的交易。

   ![4_createrule](assets/4_createrule.png)

1. 保存条件/规则，然后保存重复。 条件重复将应用于所选内容。

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   将鼠标悬停在上面时，文本文档片段显示应用于内容的重复中使用的条件和分隔符。

1. 保存文本文档片段并预览相关的交互式通信。 根据表单数据模型中的数据，对元素应用的重复将呈现类似于预览中的以下内容的事务详细信息：

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 示例：在信件中使用重复来格式化、构造和显示信用卡交易列表 {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例为您提供了使用重复来构建和呈现信件中信用卡交易的步骤。 通过使用类似的步骤，您可以在不同的场景中重复使用。

1. 打开（在编辑或创建时）一个文本模块，该模块具有呈现重复/动态数据的DD元素，并在DD元素周围嵌入所需的文本。 例如，文本模块具有以下DD元素，用于创建信用卡上的交易对帐单：

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   这些DD元素呈现对信用卡进行的交易的列表，其中包含以下信息：

   事务处理日期、事务处理金额和事务处理类型（借项或贷项）

1. 将文本嵌入到DD元素中以使语句更易读，如下所示：

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   但是，呈现格式正确的语句的工作尚未完成。 如果根据迄今为止完成的工作呈现信件，则它显示如下：

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   要与DD元素一起重复静态文本，您需要按照后续步骤中的说明应用repeat。

1. 选择静态文本和要重复的DD元素，如下所示：

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 选择 **重复**. 此时将出现“重复”对话框，其中具有空的内联条件。

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 如有必要，请插入条件以选择性地呈现交易，如呈现超过50美分的交易金额：

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   否则，如果您不需要有选择地呈现信息（此处为事务），请通过在对话框中删除以下内容来保持条件为空： `${}`. 当重复表达式窗口为空（不含$）时，将启用保存重复表达式{} （当不需要重复时）或包含有效的重复条件时。

1. 选择用于设置动态文本格式的分隔符，然后选择要保存的复选标记：

   * **换行符**：在输出书信中的每个事务条目之后插入换行符。
   * **文本**：在输出字母中的每个交易条目之后插入指定的文本字符。

   插入条件后，带有重复项的文本会以红色加亮显示，并且其左侧会出现一个句柄。 您可以将鼠标悬停在重复左侧的控制滑块上以查看重复构建。

   ![4_repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   可选取控制滑块以查看重复项的弹出菜单，从中可编辑或删除重复构造。

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 预览相关信件，并注意文本已根据重复呈现。 可以使用以下方式输入DD元素的值：

   * 在预览包含示例数据的信件时，根据相关数据字典创建的示例XML数据文件。
   * 附加到相关数据字典的XML数据文件。

   有关更多信息，请参阅 [数据字典](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html).

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   静态文本与事务详细信息重复。 重复静态文本可通过在此过程中对文本进行重复来简化。 条件${DD_creditcard_TransactionAmount > 0。5}，确保不到USD .5的交易不会在信件中呈现。

   >[!NOTE]
   >
   >只有在创建或编辑相关文本模块时才能插入条件并重复执行上述操作。 预览信件时，尽管您可以对文本模块进行编辑，但无法插入条件或重复执行操作。

## 使用内联条件和重复 — 一些用例  {#using-inline-condition-and-repeat-some-use-cases}

### 在条件中重复 {#repeat-within-condition}

您可能需要在条件中使用repeat。 通信管理允许您在内联条件构造中使用重复。

例如，以下内容在一个条件（绿色格式）中重复（红色格式）。

当重复渲染信用卡交易记录时，条件${DD_creditcard_nooftransactions > 0} 确保仅在至少有一个事务时才呈现重复构造。

![repeatwitincondition](assets/repeatwitincondition.png)

同样，根据您的要求，您可以创建：

* 条件中的一个或多个条件
* 重复中的一个或多个条件
* 条件和重复条件的组合在一个条件或重复项内重复

### 空的内联条件 {#empty-inline-condition}

您可能需要插入空的内联条件并在以后嵌入文本和DD元素。 通信管理允许您执行此操作。

![emptycondition](assets/emptycondition.png)

但是，建议尽可能首先在文本模块中使用预期格式（如项目符号）插入文本和DD元素，然后应用内联条件。
