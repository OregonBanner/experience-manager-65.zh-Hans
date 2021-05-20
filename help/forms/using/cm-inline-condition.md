---
title: 在交互式通信和信件中重复使用内嵌条件
seo-title: 在交互式通信和信件中重复使用内嵌条件
description: 使用内联条件并在交互式通信和信件中重复，您可以创建高度上下文且结构良好的通信。
seo-description: 使用内联条件并在交互式通信和信件中重复，您可以创建高度上下文且结构良好的通信。
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
feature: 通信管理
exl-id: bc5d6c5b-c833-4849-aace-e07f8a522b32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# 在Interactive Communications和字母中重复的内联条件{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## 内联条件{#inline-conditions}

AEM Forms允许您在文本模块中使用内联条件，以自动呈现取决于与表单数据模型（在交互式通信中）或数据字典（在字母中）关联的上下文或数据的文本。 内联条件根据条件评估为true或false显示特定内容。

条件对表单数据模型/数据字典或最终用户提供的数据值执行计算。 使用内联条件，您可以节省时间并减少人为错误，同时创建高度符合上下文的个性化交互式通信/信件。

有关更多信息，请参阅：

* [创建交互式通信](../../forms/using/create-interactive-communication.md)
* [通信管理概述](/help/forms/using/cm-overview.md)
* [交互式通信中的文本](../../forms/using/texts-interactive-communications.md)

### 示例：使用规则在交互式通信{#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}中条件化内联文本

要在交互式通信中条件化句子、段落或文本字符串，您可以在相应的文本文档片段中创建规则。 以下示例使用规则仅向交互式通信的美国收件人显示免费电话。

有关更多信息，请参阅[Interactive Communications](../../forms/using/texts-interactive-communications.md)文本中的以文本创建规则。

在交互式通信中包含文本片段后，代理使用代理UI准备交互式通信后，将评估收件人的（表单数据模型）数据，并且该文本仅显示给美国的收件人。

### 示例：在信件中使用内联条件来呈现相应的地址{#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

您可以在信件中插入内嵌条件，方法是在相应的文本模块中插入内嵌条件。 以下示例使用两个条件在基于DD元素“性别”的信件中评估和显示相应的地址（Sir或Ma&#39;am）。 使用类似步骤，您可以创建其他条件。

>[!NOTE]
>
>如果您的现有资产包含旧条件/重复表达式（6.2 SP1 CFP 4之前），则资产会显示旧条件语法和重复。 但是，旧条件/重复可以正常工作。 新条件/重复表达式和旧条件/重复表达式相互兼容，以创建新旧条件/重复表达式的嵌套混合。

1. 在相关文本模块中，选择要条件化的文本部分，然后点按&#x200B;**条件**。

   ![1_selecttext](assets/1_selecttext.png)

   出现“条件”(Condition)对话框，其中条件为空。

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >无法保存空或无效的条件表达式。 `${}`内必须有有效的条件表达式才能保存表达式。

1. 执行以下操作以构建一个条件，用于评估所选/条件化文本是否显示在信件中，然后点按复选标记以保存表达式：

   双击某个DD元素以在条件中插入该元素。 插入相应的运算符并在对话框中构建以下条件。

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   有关创建表达式的更多信息，请参阅[表达式生成器](../../forms/using/expression-builder.md)中的&#x200B;**使用表达式生成器**&#x200B;创建表达式和远程函数。 数据字典中的元素必须支持表达式中指定的值。 有关更多信息，请参阅[数据字典](../../forms/using/data-dictionary.md)。

   插入条件后，您可以将鼠标悬停在条件左侧的句柄上以查看该条件。 您可以点按控制滑块以查看条件的弹出菜单，该菜单允许您编辑或删除条件。

   ![3_气垫手柄](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. 通过选择文本`Ma'am`插入类似条件。

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 预览相关信件，并注意文本是根据内嵌条件呈现的。 您可以使用以下方法输入DD元素Gender的值：

   * 在预览包含示例数据的信件时，基于相关数据字典创建的示例XML数据文件。
   * 附加到相关数据字典的XML数据文件。

   有关更多信息，请参阅[数据字典](../../forms/using/data-dictionary.md)。

   ![5_leteroutput](assets/5_letteroutput.png)

## 重复 {#repeat}

您的交互式通信/信函中可能包含动态信息，例如信用卡对帐单中的交易，其实例或发生次数可能会随每个生成的信函而不断变化。 使用重复，您可以在文本文档片段中格式化和构建此类动态信息。

此外，您还可以在重复结构中指定规则/条件，以条件化在交互式通信/信件中呈现的信息/条目。

### 示例：在交互式通信中使用重复项来设置、构建和显示信用卡交易列表{#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例向您介绍了使用重复来在交互式通信中构建和渲染信用卡交易的步骤。

1. 在基于表单数据模型的文本文档片段中，插入相关表单数据模型对象（以及标签所需的嵌入文本，如本例中所示）：

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >可重复内容必须至少包含一个“收藏集”类型的属性。

1. 选择要应用重复的内容。

   ![2_selection](assets/2_selection.png)

1. 点按重复。

   此时将出现重复对话框。

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 选择换行符作为分隔符，并根据需要点按添加条件以创建规则。 您还可以使用文本作为分隔符，并指定要用作分隔符的文本字符。

   此时将显示创建规则对话框。

1. 创建一个规则以显示日期为2018年2月28日之后的交易记录，以便在交互式通信中仅包含3月份的交易记录。

   >[!NOTE]
   >
   >本示例假定代理将在2018年3月底创建语句。 否则，您可以创建另一个规则以在2018年3月之2018-04-01之前包含交易以排除交易。

   ![4_createrule](assets/4_createrule.png)

1. 保存条件/规则，然后保存重复。 条件重复将应用于选定的内容。

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   将鼠标悬停在文本文档片段上时，会显示条件以及应用于内容的重复中使用的分隔符。

1. 保存文本文档片段并预览相关的交互式通信。 根据表单数据模型中的数据，对元素应用的重复将呈现与预览中的以下内容类似的事务详细信息：

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 示例：在信件中重复使用，以格式、结构和显示信用卡交易列表{#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例为您提供了使用重复来在信件中构建和渲染信用卡交易的步骤。 使用类似步骤，您可以在不同的情景中使用重复。

1. 打开（在编辑或创建时）一个文本模块，该模块具有DD元素，该元素可呈现重复/动态数据并在DD元素周围嵌入所需文本。 例如，文本模块具有以下DD元素，用于在信用卡上创建交易报表：

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   这些DD元素会呈现信用卡上进行的交易列表，其中包含以下信息：

   事务处理日期、事务处理金额和事务处理类型（借项或贷项）

1. 在DD元素中嵌入文本，以使语句更易读，如下所示：

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   但是，呈现格式良好的语句的任务尚未完成。 如果您根据迄今完成的工作渲染信件，则会显示如下：

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   要重复静态文本和DD元素，您需要按照后续步骤中所述应用重复。

1. 选择静态文本以及要重复的DD元素，如下所示：

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 点按&#x200B;**Repeat**。 此时将显示重复对话框，其中包含空的内联条件。

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 如果需要，请插入一个条件以选择性地渲染事务，例如渲染大于50美分的事务金额：

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   否则，如果您不需要选择性地渲染信息（此处为事务），请在对话框中删除以下内容，以将条件保留为空：`${}`。 当重复表达式窗口为空（不需要重复时不带${}）或包含有效的重复条件时，将启用保存重复表达式。

1. 选择用于设置动态文本格式的分隔符，然后点按要保存的复选标记：

   * **换行符**:在输出信件中的每个事务条目后插入换行符。
   * **文本**:在输出信件中的每个事务条目后面插入指定的文本字符。

   插入条件后，具有重复的文本将以红色突出显示，并在其左侧显示一个句柄。 您可以将鼠标悬停在重复左侧的句柄上以查看重复构造。

   ![4_repeat_strasfdetail](assets/4_repeat_hoverdetail.png)

   您可以点按手柄以查看重复的弹出菜单，该菜单允许您编辑或删除重复结构。

   ![5_repeatediterremove](assets/5_repeateditremove.png)

1. 预览相关信件，并注意文本已根据重复进行渲染。 您可以使用以下方法输入DD元素的值：

   * 在预览包含示例数据的信件时，基于相关数据字典创建的示例XML数据文件。
   * 附加到相关数据字典的XML数据文件。

   有关更多信息，请参阅[数据字典](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html)。

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   静态文本与事务详细信息重复。 对此过程中的文本应用重复，有助于重复静态文本。 条件${DD_creditcard_TransactionAmount > 0.5}可确保USD .5以下的事务不会呈现在信件中。

   >[!NOTE]
   >
   >您只能在创建或编辑相关文本模块时插入条件并重复。 在预览信件时，虽然您可以对文本模块进行编辑，但无法插入条件或重复。

## 使用内联条件并重复 — 某些用例{#using-inline-condition-and-repeat-some-use-cases}

### 在条件{#repeat-within-condition}内重复

您可能需要在条件中使用重复。 通信管理允许您在内联条件结构中使用重复。

例如，在条件中重复执行（以红色格式）（以绿色格式）。

当重复呈现信用卡交易时，条件${DD_creditcard_nooftransactions> 0}确保仅当至少存在一次交易时才呈现重复构造。

![repewitincondition](assets/repeatwitincondition.png)

同样，根据您的要求，您可以创建：

* 条件中的一个或多个条件
* 重复中的一个或多个条件
* 条件和在条件或重复中重复的组合

### 空内联条件{#empty-inline-condition}

您可能需要插入空的内嵌条件，并稍后嵌入文本和DD元素。 通信管理允许您执行此操作。

![empcondition](assets/emptycondition.png)

但是，建议在可能的情况下，首先在文本模块中使用预期格式（如项目符号）插入文本和DD元素，然后应用内联条件。
