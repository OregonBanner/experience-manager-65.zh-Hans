---
title: “教程：创建文档片段”
description: 为交互式通信创建文档片段
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 2%

---

# 教程：创建文档片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 Adobe建议您按照时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

文档片段是用于构成交互式通信的通信的可重用组件。 文档片段具有以下类型：

* 文本 — 文本资产是由一个或多个文本段落组成的一段内容。 段落可以是静态的或动态的。
* 列表 — 列表是一组文档片段，包括文本、列表、条件和图像。
* 条件 — 利用条件，可根据从表单数据模型收到的数据定义要包含在交互式通信中的内容。

本教程将指导您完成根据中提供的分析创建多个文本文档片段的步骤。 [规划交互式通信](/help/forms/using/planning-interactive-communications.md) 部分。 在本教程结束时，您应该能够执行以下操作：

* 创建文档片段
* 创建变量
* 创建和应用规则

![text_document_fragments](assets/text_document_fragments.gif)

以下是本教程中创建的文档片段列表：

* [帐单详细信息](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客户详细信息](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [账单摘要](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [费用汇总](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每个文档片段都包含带有静态文本的字段、从表单数据模型接收的数据，以及使用代理UI输入的数据。 所有这些字段在 [规划交互式通信](/help/forms/using/planning-interactive-communications.md) 部分。

在本教程中创建文档片段时，将使用代理UI为接收数据的字段创建变量。

使用 **FDM_Create_First_IC**，如中所述 [创建表单数据模型](../../forms/using/create-form-data-model0.md) 部分，作为表单数据模型，用于在本教程中创建文档片段。

## 步骤1：创建清单详细信息文本文档片段 {#step-create-bill-details-text-document-fragment}

账单详细信息文档片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 发票编号 | 代理 UI |
| 帐单期间 | 代理 UI |
| 记帐日期 | 代理 UI |
| 您的计划 | 表单数据模型 |

要为将代理UI作为数据源的字段创建变量、创建静态文本并在文档片段中使用表单数据模型元素，请执行以下操作：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.

1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **bill_details_first_ic** 作为 **标题** 字段。 标题会自动填充到 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 部分。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点击 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 在左窗格中制表符，然后点击 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **发票号码** 作为变量的名称。
   1. 选择 **字符串** 作为类型。
   1. 点按&#x200B;**创建**。

   ![创建字符串类型的变量](assets/variable_create_string_new.png)

   重复步骤4和5以创建以下变量：

   * 计费周期：字符串类型
   * 帐单日期：日期类型

   ![帐单详细信息](assets/variable_bill_details_new.png)

1. 使用右窗格为以下字段创建静态文本：

   * 发票编号
   * 帐单期间
   * 记帐日期
   * 您的计划

   ![静态文本](assets/variable_bill_details_static_text_new.png)

1. 将光标放在 **发票编号** 字段并双击 **发票编号** 变量来自 **变量** 选项卡。
1. 将光标放在 **帐单期间** 字段并双击 **计费周期** 变量。
1. 将光标放在 **记帐日期** 字段并双击 **记帐日期** 变量。
1. 选择 **数据模型对象** 选项卡。
1. 将光标放在 **您的计划** 字段并双击 **客户** > **customerplan** 属性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 单击 **保存** 创建清单详细信息文本文档片段。

## 步骤2：创建客户详细信息文本文档片段 {#step-create-customer-details-text-document-fragment}

客户详细信息文档片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 客户名称 | 表单数据模型 |
| 地址 | 表单数据模型 |
| 供应地点 | 代理 UI |
| 州代码 | 代理 UI |
| 手机号码 | 表单数据模型 |
| 备用联系电话 | 表单数据模型 |
| 关系编号 | 表单数据模型 |
| 连接数 | 代理 UI |

要为将代理UI作为数据源的字段创建变量、创建静态文本并在文档片段中使用表单数据模型元素，请执行以下操作：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **customer_details_first_ic** 作为 **标题** 字段。 标题会自动填充到 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 部分。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点击 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 在左窗格中制表符，然后点击 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **Placesupply** 作为变量的名称。
   1. 选择 **字符串** 作为类型。
   1. 点按&#x200B;**创建**。

   重复步骤4和5以创建以下变量：

   * 状态码：数字类型
   * Numberconnections：数字类型

1. 选择 **数据模型对象** 选项卡，将光标置于右窗格中，然后双击 **客户** > **name** 属性。
1. 按Enter键将光标移动到下一行，然后双击 **客户** > **地址** 属性。
1. 使用右窗格为以下字段创建静态文本：

   * 手机号码
   * 备用联系电话
   * 供应地点
   * 关系编号
   * 州代码
   * 连接数

   ![客户详细信息静态文本](assets/customer_details_static_text_new.png)

1. 将光标放在 **手机号码** 字段并双击 **客户** > **mobilenum** 属性。
1. 将光标放在 **备用联系电话** 字段并双击** customer** > **alternatemobilenumber** 属性。
1. 将光标放在 **关系编号** 字段并双击 **客户** > **关系编号** 属性。
1. 选择 **变量** 选项卡，将光标放置在 **供应地点** 字段并双击 **Placesupply** 变量。
1. 将光标放在 **州代码** 字段并双击 **Statecode** 变量。
1. 将光标放在 **连接数** 字段并双击 **Numberconnections** 变量。

   ![客户详细信息](assets/customer_details_df2_new.png)

1. 单击 **保存** 创建客户详细信息文本文档片段。

## 步骤3：创建账单摘要文本文档片段 {#step-create-bill-summary-text-document-fragment}

账单汇总单据片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 上一余额 | 代理 UI |
| 支付 | 代理 UI |
| 调整 | 代理 UI |
| 费用当前帐单期间 | 表单数据模型 |
| 应付金额 | 代理 UI |
| 到期日期 | 代理 UI |

要为将代理UI作为数据源的字段创建变量、创建静态文本并在文档片段中使用表单数据模型元素，请执行以下操作：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **bill_summary_first_ic** 作为 **标题** 字段。 标题会自动填充到 **名称** 字段。

   1. 选择 **表单数据模型** 从 **数据模型** 部分。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点击 **选择**.

   1. 点按 **下一个**.

1. 选择 **变量** 在左窗格中制表符，然后点击 **创建**.
1. 在 **创建变量** 部分：

   1. 输入 **以前的平衡** 作为变量的名称。
   1. 选择 **数字** 作为类型。
   1. 点按&#x200B;**创建**。

   重复步骤4和5以创建以下变量：

   * 付款：编号类型
   * 调整：数字类型
   * 金额：数字类型
   * 日期：日期类型

1. 使用右窗格为以下字段创建静态文本：

   * 上一余额
   * 支付
   * 调整
   * 费用当前帐单期间
   * 应付金额
   * 到期日期
   * 到期日期之后的延迟付款费用为20美元

   ![账单摘要静态文本](assets/bill_summary_static_new.png)

1. 将光标放在 **上一余额** 字段并双击 **以前的平衡** 变量。
1. 将光标放在 **支付** 字段并双击 **支付** 变量。
1. 将光标放在 **调整** 字段并双击 **调整** 变量。
1. 将光标放在 **应付金额** 字段并双击 **金额** 变量。
1. 将光标放在 **到期日期** 字段并双击 **Duedate** 变量。
1. 选择 **数据模型对象** 选项卡，将光标放置在 **费用当前帐单期间** 字段，然后双击 **帐单** > **使用费用** 属性。

   ![账单摘要](assets/bill_summary_static_variables_new.png)

1. 单击 **保存** 创建客户详细信息文本文档片段。

## 步骤4：创建费用摘要文本文档片段 {#step-create-summary-of-charges-text-document-fragment}

费用单据片段的摘要包含以下字段：

| 字段 | 数据源 |
|---|---|
| 呼叫费用 | 表单数据模型 |
| 电话会议费用 | 表单数据模型 |
| 短信费用 | 表单数据模型 |
| 移动互联网费用 | 表单数据模型 |
| 国家漫游费用 | 表单数据模型 |
| 国际漫游费用 | 表单数据模型 |
| 增值服务费用 | 表单数据模型 |
| 总费用 | 表单数据模型 |
| 应付总额 | 表单数据模型 |

要创建静态文本并在文档片段中使用表单数据模型元素，请执行以下操作：

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**.
1. 选择 **创建** > **文本**.
1. 指定以下信息：

   1. 输入 **summary_charges_first_ic** 作为 **标题** 字段。 标题将自动填充到“名称”字段中。

   1. 选择 **表单数据模型** 从 **数据模型** 部分。

   1. 选择 **FDM_Create_First_IC** 作为表单数据模型，然后点击 **选择**.

   1. 点按 **下一个**.

1. 使用右窗格为以下字段创建静态文本：

   * 呼叫费用
   * 电话会议费用
   * 短信费用
   * 移动互联网费用
   * 国家漫游费用
   * 国际漫游费用
   * 增值服务费用
   * 总费用
   * 应付总额

   ![汇总费用](assets/summary_charges_static_new.png)

1. 选择 **数据模型对象** 选项卡。
1. 将光标放在 **呼叫费用** 字段并双击 **帐单** > **callcharges** 属性。
1. 将光标放在 **电话会议费用** 字段并双击 **帐单** > **confcallcharges** 属性。
1. 将光标放在 **短信费用** 字段并双击 **帐单** > **smscharges** 属性。
1. 将光标放在 **移动互联网费用** 字段并双击 **帐单** > **网间费用** 属性。
1. 将光标放在 **国家漫游费用** 字段并双击 **帐单** > **roamingnational** 属性。
1. 将光标放在 **国际漫游费用** 字段并双击 **帐单** > **roamingintel** 属性。
1. 将光标放在 **增值服务费用** 字段并双击 **帐单** > **vas** 属性。
1. 将光标放在 **总费用** 字段并双击 **帐单** > **使用费用** 属性。
1. 将光标放在 **应付总额** 字段并双击 **帐单** > **使用费用** 属性。

   ![费用汇总](assets/summary_charges_static_fdm_new.png)

1. 选择以下文件中的文本 **增值服务费用** 行和点按 **创建规则** 要创建在交互式通信中显示行的条件，请执行以下操作：
1. 在 **创建规则** 弹出窗口：

   1. 选择 **数据模型和变量** 然后 **帐单** > **callcharges**.

   1. 选择 **小于** 作为运算符。
   1. 选择 **数字** 并输入值 **60**.

   根据此条件，仅当“呼叫费用”字段的值小于60时，才会显示“增值服务费用”行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 单击 **保存** 创建费用摘要文本文档片段。
