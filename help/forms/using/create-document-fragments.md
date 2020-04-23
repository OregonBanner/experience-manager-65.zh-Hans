---
title: “教程：创建文档片段”
seo-title: 为交互式通信创建文档片段
description: 为交互式通信创建文档片段
seo-description: 为交互式通信创建文档片段
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
translation-type: tm+mt
source-git-commit: e545fc5e2ea139bd8ebb7f84138ba68e03d71d19

---


# 教程：创建文档片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教程是创建您的第一个交 [互式通信系列中的一个步骤](/help/forms/using/create-your-first-interactive-communication.md) 。 建议按照时间顺序按照这一系列来了解、执行和演示完整的教程用例。

文档片段是用于构成交互式通信的通信的可重用组件。 文档片段有以下类型：

* 文本——文本资产是由一个或多个文本段落组成的一段内容。 段落可以是静态的或动态的。
* 列表-列表是一组文档片段，包括文本、列表、条件和图像。
* 条件——条件允许您根据从表单数据模型接收的数据定义交互通信中包含的内容。

本教程将指导您逐步根据“规划交互式通信”部分中提供的解剖结构创建 [多个文本文档片段](/help/forms/using/planning-interactive-communications.md) 。 在本教程的结尾，您将能够：

* 创建文档片段
* 创建变量
* 创建和应用规则

![text_文档_fragments](assets/text_document_fragments.gif)

以下是本教程中创建的文档片段的列表:

* [帐单详细信息](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客户详细信息](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帐单摘要](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [费用汇总](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每个文档片段包括带有静态文本的字段、从表单数据模型接收的数据以及使用代理UI输入的数据。 “计划交互式通信”部分中描 [述了所有这些字段](/help/forms/using/planning-interactive-communications.md) 。

在本教程中创建文档片段时，将为使用代理UI接收数据的字段创建变量。

如 **Create form data model(创建表单数据模型**[](../../forms/using/create-form-data-model0.md) )部分中所述，使用FDM_Create_First_IC作为表单数据模型以在本教程中创建文档片段。

## 第1步：创建清单详细信息文本文档片段 {#step-create-bill-details-text-document-fragment}

“清单详细信息”文档片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 发票编号 | 代理 UI |
| 帐单期间 | 代理 UI |
| 帐单日期 | 代理 UI |
| 您的计划 | 表单数据模型 |

执行以下步骤，为以Agent UI为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择“ **[!UICONTROL 表单]** ”>“ **[!UICONTROL 文档片段”]**。

1. 选择 **创建** > **文本**。
1. 指定以下信息：

   1. 在“ **标题”字段中输入bill_details_first_ic****作为名称** 。 标题将自动填充到“名称” **字段** 。

   1. 从“ **数据模型** ”(Data Model)部分 **中选择“表单数据模型** ”(Form Data Model)。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点按 **选择**。

   1. 点按下 **一步**。

1. 选择左 **窗格中** “变量”选项卡，然后点 **按创建**。
1. 在创建 **变量部分** :

   1. 输入 **发票编号** ，作为变量的名称。
   1. 选择“ **字符串** ”作为类型。
   1. 点按&#x200B;**创建**。
   ![创建字符串类型的变量](assets/variable_create_string_new.png)

   重复第4步和第5步以创建以下变量：

   * 开单期间：字符串类型
   * BillDate:日期类型
   ![帐单详细信息](assets/variable_bill_details_new.png)

1. 使用右侧窗格为以下字段创建静态文本：

   * 发票编号
   * 帐单期间
   * 帐单日期
   * 您的计划
   ![静态文本](assets/variable_bill_details_static_text_new.png)

1. 将光标放在“发票否”字 **段旁边** ，并在左窗格的“变量”标签中按住 **InvoiceNumber** （发票编号） **** 变量。
1. 将光标放在“帐单期间”字 **段旁边** ，然后按住多次单 **击“帐单期间** ”变量。
1. 将光标放在“帐单日期”字 **段旁边** ，然后按住多次单 **击“帐单日期** ”变量。
1. 选择左 **窗格中的** “数据模型对象”选项卡。
1. 将光标放在“您的计 **划** ”字段旁边，并按住多次单击 **customer** > **customerplan** 属性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 单击 **保存** ，以创建“清单详细信息”文本文档片段。

## 第2步：创建客户详细信息文本文档片段 {#step-create-customer-details-text-document-fragment}

“客户详细信息”文档片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 客户姓名 | 表单数据模型 |
| 地址 | 表单数据模型 |
| 供应地点 | 代理 UI |
| 状态代码 | 代理 UI |
| 移动号码 | 表单数据模型 |
| 备用联系人号码 | 表单数据模型 |
| 关系编号 | 表单数据模型 |
| 连接数 | 代理 UI |

执行以下步骤，为以Agent UI为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择“ **[!UICONTROL 表单]** ”>“ **[!UICONTROL 文档片段”]**。
1. 选择 **创建** > **文本**。
1. 指定以下信息：

   1. 在“ **标题”字段中输入customer_details_first_ic****作为名称** 。 标题将自动填充到“名称” **字段** 。

   1. 从“ **数据模型** ”(Data Model)部分 **中选择“表单数据模型** ”(Form Data Model)。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点按 **选择**。

   1. 点按下 **一步**。

1. 选择左 **窗格中** “变量”选项卡，然后点 **按创建**。
1. 在创建 **变量部分** :

   1. 输 **入Placesupply** 作为变量的名称。
   1. 选择“ **字符串** ”作为类型。
   1. 点按&#x200B;**创建**。
   重复第4步和第5步以创建以下变量：

   * Statecode:数字类型
   * 数字连接：数字类型


1. 选择“ **数据模型对象** ”选项卡，将光标放在右侧窗格中，然后多次单击 **customer** > **name** 属性。
1. 按Enter将光标移到下一行，然后多次并单击 **customer** > **address** 属性。
1. 使用右侧窗格为以下字段创建静态文本：

   * 移动号码
   * 备用联系人号码
   * 供应地点
   * 关系编号
   * 状态代码
   * 连接数
   ![客户详细信息静态文本](assets/customer_details_static_text_new.png)

1. 将光标放在“ **Mobile Number** ”字段旁边，并按住多次 **单击customer** > **mobilenum** 属性。
1. 将光标放在“替代联系 **人号码** ”字段旁边，并按住多次单击** customer** > **alternatemobilenumber属性** 。
1. 将光标放在“关系编号” **字段旁边** ，并按住多次键 **单击customer** > **relationshipnumber属性** 。
1. 选择“ **变量** ”选项卡，将光标放在“供应地点”字 **段旁边，然后按住多次单击“** Placesupply **** ”变量。
1. 将光标放在“状态代码”字 **段旁边** ，并多次单击“状态 **代码”变量** 。
1. 将光标放在“连接数 **”字段旁边** ，并按多次单击“ **Numberconnections** ”变量。

   ![客户详细信息](assets/customer_details_df2_new.png)

1. 单击 **保存** ，以创建Customer Details（客户详细信息）文本文档片段。

## 第3步：创建帐单汇总文本文档片段 {#step-create-bill-summary-text-document-fragment}

“清单汇总”文档片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 上一余额 | 代理 UI |
| 付款 | 代理 UI |
| 调整 | 代理 UI |
| 本期费用 | 表单数据模型 |
| 应付款项 | 代理 UI |
| 到期日期 | 代理 UI |

执行以下步骤，为以Agent UI为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择“ **[!UICONTROL 表单]** ”>“ **[!UICONTROL 文档片段”]**。
1. 选择 **创建** > **文本**。
1. 指定以下信息：

   1. 在“ **标题”字段中输入bill_summary_first_ic** 作为 **名称** 。 标题将自动填充到“名称” **字段** 。

   1. 从“ **数据模型** ”(Data Model)部分 **中选择“表单数据模型** ”(Form Data Model)。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点按 **选择**。

   1. 点按下 **一步**。

1. 选择左 **窗格中** “变量”选项卡，然后点 **按创建**。
1. 在创建 **变量部分** :

   1. 输 **入** Previousbalance作为变量的名称。
   1. 选择 **数字** （类型）。
   1. 点按&#x200B;**创建**。
   重复第4步和第5步以创建以下变量：

   * 付款：数字类型
   * 调整：数字类型
   * 应付款项：数字类型
   * Duedate:日期类型


1. 使用右侧窗格为以下字段创建静态文本：

   * 上一余额
   * 付款
   * 调整
   * 本期费用
   * 应付款项
   * 到期日期
   * 到期日后的延迟付款费用为20美元
   ![Bill Summary静态文本](assets/bill_summary_static_new.png)

1. 将光标放在“上一平衡”字 **段旁边** ，并按住多次单击“ **上一平衡** ”变量。
1. 将光标放在“付款”字 **段旁** ，然后多次单击“付款” **变量** 。
1. 将光标放在“调整”字 **段旁** ，然后多次单击“调 **整** ”变量。
1. 将光标放在“到期 **金额** ”字段旁边，并按住多次单 **击“Amountdue** ”变量。
1. 将光标放在“到期日 **期** ”字段旁边，并按住多次单 **击Duedate** 变量。
1. 选择“数 **据模型对象** ”选项卡，将光标放在右侧窗格中的“ **Charges current bill period****”（当前开单期间收费）字段旁，并按住“多次”单击“Bills** > **UsagechargesProperty”(清单** > UsagechargesProperty)。

   ![帐单摘要](assets/bill_summary_static_variables_new.png)

1. 单击 **保存** ，以创建Customer Details（客户详细信息）文本文档片段。

## 第4步：创建费用汇总文本文档片段 {#step-create-summary-of-charges-text-document-fragment}

“费用汇总”文档片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 电话费 | 表单数据模型 |
| 电话会议费用 | 表单数据模型 |
| SMS费用 | 表单数据模型 |
| 移动Internet费用 | 表单数据模型 |
| 国家漫游费用 | 表单数据模型 |
| 国际漫游费用 | 表单数据模型 |
| 增值服务费 | 表单数据模型 |
| 总费用 | 表单数据模型 |
| 应付总额 | 表单数据模型 |

执行以下步骤以创建静态文本并在文档片段中使用表单数据模型元素：

1. 选择“ **[!UICONTROL 表单]** ”>“ **[!UICONTROL 文档片段”]**。
1. 选择 **创建** > **文本**。
1. 指定以下信息：

   1. 在“ **标题”字段中输入** summary_charges_first_ic **作为名** 称。 标题将自动填充在名称字段中。

   1. 从“ **数据模型** ”(Data Model)部分 **中选择“表单数据模型** ”(Form Data Model)。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点按 **选择**。

   1. 点按下 **一步**。

1. 使用右侧窗格为以下字段创建静态文本：

   * 电话费
   * 电话会议费用
   * SMS费用
   * 移动Internet费用
   * 国家漫游费用
   * 国际漫游费用
   * 增值服务费
   * 总费用
   * 应付总额
   ![汇总费用](assets/summary_charges_static_new.png)

1. 选择“数 **据模型对象** ”选项卡。
1. 将光标放在“呼叫费 **用** ”字段旁边，并按住多次键 **单击“帐单** > **呼叫费用** ”属性。
1. 将光标放在“电话会议费 **用”字段旁** ，并按住多次单击“ **帐单** > **confcallcarges** ”属性。
1. 将光标放在“ **SMS Carges** ( **SMS费用** )”字段旁边，并按住多次单击“ **bills** > smscarges（帐单）”属性。
1. 将光标放在“ **Mobile Internet Charges** ”字段旁边，并按住多次键 **单击“bills** > **internetcharges** ”属性。
1. 将光标放在“国家漫游 **费用** ”字段旁边，并多次键 **击帐单** > **Roaming国家财产** 。
1. 将光标放在“国际漫游 **费用** ”字段旁边，并按住多次 **单击“帐单** ” **>** “漫游”属性。
1. 将光标放在“增值服 **务费用”字段旁** ，并按住多次单 **击“帐单** > **vas** ”属性。
1. 将光标放在“总费用”字 **段旁边** ，并按住多次键 **单击“帐单** ” **>** Usagecharges属性。
1. 将光标放在“ **TOTAL PAYABLE** ”字段旁边，并按住多次单 **击Bills** > **Usagecharges** 属性。

   ![费用汇总](assets/summary_charges_static_fdm_new.png)

1. 选择“增值服 **务费用** ”行中的文本，然后点按 **创建规则** ，以创建在交互通信中显示该行的条件：
1. 在“创 **建规则** ”弹出窗口中：

   1. 选择 **数据模型和变量** ，然后选 **择清单** >调 **用费用**。

   1. 选 **择小于** （作为运算符）。
   1. 选 **择Number** ，然后输入 **60值**。
   根据此条件，仅当“呼叫费用”字段的值小于60时，才会显示“增值服务费用”行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 单击 **保存** ，以创建费用摘要文本文档片段。
