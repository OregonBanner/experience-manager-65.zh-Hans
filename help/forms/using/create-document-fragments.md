---
title: “教程：创建文档片段”
seo-title: Create document fragments for Interactive Communication
description: 为交互式通信创建文档片段
seo-description: Create document fragments for Interactive Communication
uuid: 677d717e-e92e-434e-8266-6fbbf94f3867
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8ae97a21-83af-4615-9be3-61e2f8065081
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 2%

---

# 教程：创建文档片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

文档片段是用于撰写交互式通信的通信的可重用组件。 文档片段的类型如下：

* 文本 — 文本资产是由一个或多个文本段落组成的一段内容。 段落可以是静态的或动态的。
* 列表 — 列表是一组文档片段，包括文本、列表、条件和图像。
* 条件 — 条件允许您根据从表单数据模型收到的数据定义交互式通信中包含的内容。

本教程将指导您完成根据 [规划交互式通信](/help/forms/using/planning-interactive-communications.md) 中。 在本教程结束时，您将能够：

* 创建文档片段
* 创建变量
* 创建和应用规则

![text_document_fragments](assets/text_document_fragments.gif)

以下是本教程中创建的文档片段列表：

* [帐单详细信息](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客户详细信息](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帐单汇总](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [费用汇总](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每个文档片段都包含具有静态文本的字段、从表单数据模型接收的数据以及使用代理UI输入的数据。 所有这些字段均在 [规划交互式通信](/help/forms/using/planning-interactive-communications.md) 中。

在本教程中创建文档片段时，会为使用代理UI接收数据的字段创建变量。

使用 **FDM_Create_First_IC**，如 [创建表单数据模型](../../forms/using/create-form-data-model0.md) 部分作为用于创建文档片段的表单数据模型。

## 步骤1:创建清单详细信息文本文档片段 {#step-create-bill-details-text-document-fragment}

“清单详细信息”单据片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 发票编号 | 代理 UI |
| 帐单期间 | 代理 UI |
| 帐单日期 | 代理 UI |
| 您的计划 | 表单数据模型 |

执行以下步骤，为以Agent UI作为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.

1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **bill_details_first_ic** 作为 **标题** 字段。 标题将在 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 中。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型并点按 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 选项卡，然后点按 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **发票编号** 作为变量的名称。
   1. 选择 **字符串** 类型。
   1. 点按&#x200B;**创建**。

   ![创建字符串类型的变量](assets/variable_create_string_new.png)

   重复步骤4和5以创建以下变量：

   * 计费周期：字符串类型
   * 帐单日期：日期类型

   ![帐单详细信息](assets/variable_bill_details_new.png)

1. 使用右侧窗格为以下字段创建静态文本：

   * 发票编号
   * 帐单期间
   * 帐单日期
   * 您的计划

   ![静态文本](assets/variable_bill_details_static_text_new.png)

1. 将光标放在 **发票编号** 字段，然后双击 **发票编号** 变量 **变量** 选项卡。
1. 将光标放在 **帐单期间** 字段，然后双击 **计费周期** 变量。
1. 将光标放在 **帐单日期** 字段，然后双击 **帐单日期** 变量。
1. 选择 **数据模型对象** 选项卡。
1. 将光标放在 **您的计划** 字段，然后双击 **客户** > **customerplan** 属性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 单击 **保存** 创建“清单详细信息”文本文档片段。

## 步骤2:创建客户详细信息文本文档片段 {#step-create-customer-details-text-document-fragment}

“客户详细信息”文档片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 客户名称 | 表单数据模型 |
| 地址 | 表单数据模型 |
| 供应地 | 代理 UI |
| 状态代码 | 代理 UI |
| 手机号码 | 表单数据模型 |
| 备用联系人号码 | 表单数据模型 |
| 关系数 | 表单数据模型 |
| 连接数 | 代理 UI |

执行以下步骤，为以Agent UI作为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **customer_details_first_ic** 作为 **标题** 字段。 标题将在 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 中。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型并点按 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 选项卡，然后点按 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **Placesupply** 作为变量的名称。
   1. 选择 **字符串** 类型。
   1. 点按&#x200B;**创建**。

   重复步骤4和5以创建以下变量：

   * Statecode:数字类型
   * 数字连接：数字类型


1. 选择 **数据模型对象** 选项卡，将光标置于右窗格中，然后双击 **客户** > **name** 属性。
1. 按Enter键将光标移动到下一行，然后双击 **客户** > **地址** 属性。
1. 使用右侧窗格为以下字段创建静态文本：

   * 手机号码
   * 备用联系人号码
   * 供应地
   * 关系数
   * 状态代码
   * 连接数

   ![客户详细信息静态文本](assets/customer_details_static_text_new.png)

1. 将光标放在 **手机号码** 字段，然后双击 **客户** > **mobilenum** 属性。
1. 将光标放在 **备用联系人号码** 字段中，并双击**客户** > **alternatemobilenumber** 属性。
1. 将光标放在 **关系数** 字段，然后双击 **客户** > **关系编号** 属性。
1. 选择 **变量** 选项卡，将光标放在 **供应地** 字段，然后双击 **Placesupply** 变量。
1. 将光标放在 **状态代码** 字段，然后双击 **Statecode** 变量。
1. 将光标放在 **连接数** 字段，然后双击 **编号连接** 变量。

   ![客户详细信息](assets/customer_details_df2_new.png)

1. 单击 **保存** 创建“客户详细信息”文本文档片段。

## 步骤3:创建清单汇总文本文档片段 {#step-create-bill-summary-text-document-fragment}

清单汇总单据片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 上一余额 | 代理 UI |
| 支付 | 代理 UI |
| 调整 | 代理 UI |
| 当前帐单期间费用 | 表单数据模型 |
| 到期金额 | 代理 UI |
| 到期日期 | 代理 UI |

执行以下步骤，为以Agent UI作为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **bill_summary_first_ic** 作为 **标题** 字段。 标题将在 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 中。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型并点按 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 选项卡，然后点按 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **上一余额** 作为变量的名称。
   1. 选择 **数值** 类型。
   1. 点按&#x200B;**创建**。

   重复步骤4和5以创建以下变量：

   * 付款：数字类型
   * 调整：数字类型
   * 应付款项：数字类型
   * 委托日期：日期类型


1. 使用右侧窗格为以下字段创建静态文本：

   * 上一余额
   * 支付
   * 调整
   * 当前帐单期间费用
   * 到期金额
   * 到期日期
   * 到期日后的延迟付款费用为$ 20

   ![清单汇总静态文本](assets/bill_summary_static_new.png)

1. 将光标放在 **上一余额** 字段，然后双击 **上一余额** 变量。
1. 将光标放在 **支付** 字段，然后双击 **支付** 变量。
1. 将光标放在 **调整** 字段，然后双击 **调整** 变量。
1. 将光标放在 **到期金额** 字段，然后双击 **到期款项** 变量。
1. 将光标放在 **到期日期** 字段，然后双击 **杜代特** 变量。
1. 选择 **数据模型对象** 选项卡，将光标放在 **当前帐单期间费用** 字段，然后双击 **票据** > **乌萨盖查尔** 属性。

   ![帐单汇总](assets/bill_summary_static_variables_new.png)

1. 单击 **保存** 创建“客户详细信息”文本文档片段。

## 步骤4:创建费用汇总文本文档片段 {#step-create-summary-of-charges-text-document-fragment}

费用汇总单据片段包括以下字段：

| 字段 | 数据源 |
|---|---|
| 通话费 | 表单数据模型 |
| 电话会议费用 | 表单数据模型 |
| 短信费用 | 表单数据模型 |
| 移动互联网收费 | 表单数据模型 |
| 国家漫游收费 | 表单数据模型 |
| 国际漫游费 | 表单数据模型 |
| 增值服务费 | 表单数据模型 |
| 总费用 | 表单数据模型 |
| 应付总额 | 表单数据模型 |

执行以下步骤以创建静态文本并在文档片段中使用表单数据模型元素：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **summary_charges_first_ic** 作为 **标题** 字段。 将在“名称”字段中自动填充标题。

   1. 选择 **表单数据模型** 从 **数据模型** 中。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型并点按 **选择**.

   1. 点按 **下一个**.

1. 使用右侧窗格为以下字段创建静态文本：

   * 通话费
   * 电话会议费用
   * 短信费用
   * 移动互联网收费
   * 国家漫游收费
   * 国际漫游费
   * 增值服务费
   * 总费用
   * 应付总额

   ![汇总费用](assets/summary_charges_static_new.png)

1. 选择 **数据模型对象** 选项卡。
1. 将光标放在 **通话费** 字段，然后双击 **票据** > **催缴费** 属性。
1. 将光标放在 **电话会议费用** 字段，然后双击 **票据** > **concallcharces** 属性。
1. 将光标放在 **短信费用** 字段，然后双击 **票据** > **smscharges** 属性。
1. 将光标放在 **移动互联网收费** 字段，然后双击 **票据** > **internetcarines** 属性。
1. 将光标放在 **国家漫游收费** 字段，然后双击 **票据** > **罗马尼亚** 属性。
1. 将光标放在 **国际漫游费** 字段，然后双击 **票据** > **roamingintnl** 属性。
1. 将光标放在 **增值服务费** 字段，然后双击 **票据** > **vas** 属性。
1. 将光标放在 **总费用** 字段，然后双击 **票据** > **乌萨盖查尔** 属性。
1. 将光标放在 **应付总额** 字段，然后双击 **票据** > **乌萨盖查尔** 属性。

   ![费用汇总](assets/summary_charges_static_fdm_new.png)

1. 在 **增值服务费** 行和点按 **创建规则** 要创建在交互式通信中显示该行的条件，请执行以下操作：
1. 在 **创建规则** 弹出窗口：

   1. 选择 **数据模型和变量** 然后 **票据** > **催缴费**.

   1. 选择 **小于** 作为运算符。
   1. 选择 **数值** 并输入值作为 **60**.

   根据此条件，仅当“呼叫费用”字段的值小于60时，才会显示“增值服务费用”行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 单击 **保存** 创建费用汇总文本文档片段。
