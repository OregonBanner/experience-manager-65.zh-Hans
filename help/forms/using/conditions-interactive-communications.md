---
title: 交互通信中的条件
seo-title: 交互通信中的条件
description: 创建和编辑要在交互通信中使用的条件片段 — 条件是用于构建交互通信的四种类型的文档片段之一。 另外三个是文本、列表和布局片段。
seo-description: 创建和编辑要在交互通信中使用的条件
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---


# 交互通信中的条件{#conditions-in-interactive-communications}

创建和编辑要在交互通信中使用的条件片段 — 条件是用于构建交互通信的四种类型的文档片段之一。 另外三个是文本、列表和布局片段。

## 概述 {#overview}

条件是可以包含在交互通信中的文档片段。 其他文档片段是[text](../../forms/using/texts-interactive-communications.md)、列表和布局片段。 条件允许您根据提供的数据和规则定义包含在交互式通信中的一个或多个上下文资产。

示例：

* 在信用卡对帐单中，根据客户信用卡的类型显示信用卡年费和信用卡图像。
* 在保险费到期提醒中，显示根据客户州税计算的税。

基于已应用规则和传递到规则的值呈现的条件中的资产。 条件中的规则可以检查以下类型数据中的值：

* 关联表单数据模型的属性
* 在条件中创建的任何变量
* 字符串
* 数字
* 数学表达式
* 日期

## 创建条件{#createcondition}

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 条件]**。
1. 指定以下信息：

   * **[!UICONTROL 标题]**:（可选）输入条件的标题。标题不需要唯一，并且可以包含特殊字符和非英语字符。 条件由其标题（如果可用）引用，如缩览图和属性中。
   * **[!UICONTROL 名称]**:文件夹内条件的唯一名称。任何状态中都不能存在两个文档片段(文本、条件或列表)，并且文件夹中的名称相同。 在“名称”字段中，您只能输入英语字符、数字和连字符。 系统会根据标题字段自动填充名称字段。 在“标题”字段中输入的特殊字符、空格、数字和非英文字符将替换为“名称”字段中的连字符。 尽管“标题”字段中的值会自动复制到“名称”中，但您可以编辑该值。

   * **[!UICONTROL 描述]**:键入文档片段的描述。
   * **[!UICONTROL 表单数据模型]**:（可选）选择“表单数据模型”单选按钮，以基于表单数据模型创建条件。选择“表单数据模型”单选按钮时，将显示&#x200B;**[!UICONTROL 表单数据模型]**&#x200B;字段。 浏览并选择表单数据模型。 在为交互式通信创建条件时，请确保您使用的数据模型与要在交互式通信中使用的数据模型相同。 有关表单数据模型的详细信息，请参阅[数据集成](../../forms/using/data-integration.md)。

   * **[!UICONTROL 标记]**:（可选）要创建自定义标记，请在文本字段中输入值，然后点按Enter。保存此条件时，将创建新添加的标记。

1. 点按&#x200B;**[!UICONTROL 下一步]**。

   “创建条件”页面。

   ![createcondition](assets/createcondition.png)

1. 点按&#x200B;**[!UICONTROL 添加资产]**。

   选择资产页面会出现，并显示可在条件中添加的文本、列表、条件和图像。

   >[!NOTE]
   >
   >“选择资产”页面中仅显示基于无的新创建资产和基于FDM的资产（使用与所创建条件相同的FDM创建）。

1. 点按相应的资产以选择要包含在条件中的资产，然后点按&#x200B;**[!UICONTROL 完成]**。

   此时会显示“创建条件”页面，并列表添加的资产。

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   您可以使用以下选项来管理某个条件中的资产：

   ![createconditionscreenassetsaddennoted](assets/createconditionscreenassetsaddedannotated.png)

   **[AReject ] Change。** 点按此图标可拒绝您对资产和条件中的规则所做的更改。
   **[] 更改。** 点按此图标以接受您在资产中所做的更改，并在条件中使用规则。
   **[复] 制资产。** 点按此图标，以在条件中创建资产的副本以及应用的规则（如果有）。然后，您可以继续编辑重复资产的规则和资产。 复制资产对于创建类似规则以根据特定上下文显示替代资产非常有用。
   **[] DS如何预览** 点按此图标可在创建\编辑条件页面中显示资产的预览。
   **“server”重新排序。** 点按并按住此图标，可拖放资产以在某个条件内对其重新排序。

   您可以选择以下选项来指定条件在运行时的行为方式：

   * **已禁用多个结果评估\启用多个结果评估**:启用此选项（显示为“已启用多个结果评估”）后，将评估所有规则，结果为所有真实规则的总和。如果禁用此选项（显示为“已禁用多个结果评估”），则仅评估发现为true的第一个规则，并成为条件的输出。

   * **分页符**:选择此选项 ![(break](assets/break.png))可在条件的资产之间添加分页符。如果未选择此选项(![nobreak](assets/nobreak.png))，则如果条件溢出到打印输出中的下一页，则整个条件将移至下一页，而不是在该条件中资产之间的页中断。

1. 点按&#x200B;**[!UICONTROL 创建规则]**，以根据需要添加规则以显示或隐藏资产。 要在规则中使用变量，请参阅[创建变量](#variables)。 有关详细信息，请参阅[将规则添加到条件](#ruleeditor)。

   创建的规则将显示在“创建条件”屏幕的“规则”列中。

   ![createconditionscreenrules added](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >您可以在已应用规则或重复应用的条件中插入资产。

1. 点按&#x200B;**[!UICONTROL 保存]**。

   将创建条件。 现在，您可以在创建交互式通信时继续将条件用作构建块。

   >[!NOTE]
   >
   >要保存新的或已编辑的条件，您必须在该条件中添加的每个资产至少有一个规则。

## 编辑条件{#edit-a-condition}

可以使用以下步骤编辑条件。 您还可以通过在弹出菜单中选择编辑片段来选择在交互式通信中编辑条件。

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 导航到该条件并选择它。
1. 点按&#x200B;**[!UICONTROL 编辑]**。
1. 在条件中进行所需的更改。 有关在条件中可以更改的信息的详细信息，请参阅[创建条件](#createcondition)。
1. 点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 关闭]**。

## 在条件{#ruleeditor}中创建规则

使用条件中的规则编辑器，您可以创建规则，以根据&#x200B;**预设条件**&#x200B;显示或隐藏资产。 这些条件可以基于：

* 字符串
* 数字
* 数学表达式
* 日期
* 关联表单数据模型的属性
* 您可能已创建的任何[变量](#variables)

### 在条件{#create-rule-in-condition}中创建规则

1. 在创建或编辑条件时，点按相关资产的![规则编辑器图标](assets/ruleeditoricon.png)（规则编辑器）图标。

   此时将显示创建规则对话框。 除了字符串、数字、数学表达式和日期之外，规则编辑器中还提供以下内容，用于创建规则语句：

   * 关联表单数据模型的属性
   * 您可能已创建的任何[变量](#variables)。

   ![createruledialog](assets/createruledialog.png)

   选择要评估的相应选项。

   >[!NOTE]
   >
   >创建用于显示资产的规则时不支持集合属性。

1. 选择相应的运算符以计算规则，如“等于”、“包含”和“开始为”。
1. 插入计算表达式、字符串、数据模型属性、变量或日期。

   ![策略类型为标准时显示资产的规则](assets/ruleincondition.png)

   策略类型为标准时显示资产的规则

   * 在创建或编辑规则时，您还可以点按![icon_resize](assets/icon_resize.png)(Resize)以展开“创建规则/编辑规则”对话框。 扩展的全窗口对话框允许您创建[变量](#variables)来构建规则。 再次点按调整大小以返回到常规的创建规则对话框。

   * 您还可以在规则中创建多个条件。

1. 点按&#x200B;**[!UICONTROL 完成]**。

   规则将应用于资产。

## 在条件{#variables}中创建和使用变量

在条件中创建或编辑规则时，可点按![icon_resize](assets/icon_resize.png)(Resize)以展开“创建规则\编辑规则”对话框。 在展开的全窗口对话框中，您可以：

* 在规则中创建和使用变量
* 在规则中拖放表单数据模型的属性和变量

再次点按调整大小以返回“创建规则\编辑规则”对话框。

### 创建变量{#create-variables}

1. 在条件中创建或编辑规则时，可点按![icon_resize](assets/icon_resize.png)(Resize)以展开“创建规则\编辑规则”对话框。

   此时将显示“已扩展的全窗口”对话框。

   ![expandeditrule对话框](assets/expandededitruledialog.png)

1. 在左窗格中，点按&#x200B;**[!UICONTROL 变量]**。

   将出现“变量”窗格。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 点按&#x200B;**[!UICONTROL 创建]**。

   此时将显示“创建变量”窗格。

1. 输入以下信息，然后点按&#x200B;**[!UICONTROL 创建]**:

   * **[!UICONTROL 名称]**:变量的名称。
   * **[!UICONTROL 描述]**:（可选）输入有关变量的说明。
   * **[!UICONTROL 类型]**:选择变量的类型：字符串、数字、布尔值或日期。
   * **[!UICONTROL 仅允许特定值]**:对于字符串和数字变量，您可以确保代理从代理UI中占位符的特定值集中进行选择。要指定值集，请选择此选项，然后指定在&#x200B;**[!UICONTROL Values]**&#x200B;字段中允许的以逗号分隔的值。

1. 点按&#x200B;**[!UICONTROL 创建]**。

   变量将创建并列在“变量”窗格中。

1. 要在规则中插入变量，请将该变量拖放到规则中某个选项的占位符中。
1. 构建有效规则后，点按&#x200B;**[!UICONTROL 完成]**。

   根据需要，继续在条件中进行进一步更改并保存。

