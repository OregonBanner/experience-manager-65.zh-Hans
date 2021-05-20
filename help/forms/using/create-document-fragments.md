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
feature: 交互式通信
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 2%

---

# 教程：创建文档片段{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

文档片段是用于撰写交互式通信的通信的可重用组件。 文档片段的类型如下：

* 文本 — 文本资产是由一个或多个文本段落组成的一段内容。 段落可以是静态的或动态的。
* 列表 — 列表是一组文档片段，包括文本、列表、条件和图像。
* 条件 — 条件允许您根据从表单数据模型收到的数据定义交互式通信中包含的内容。

本教程将指导您完成根据[规划交互式通信](/help/forms/using/planning-interactive-communications.md)部分中提供的解剖结构创建多个文本文档片段的步骤。 在本教程结束时，您将能够：

* 创建文档片段
* 创建变量
* 创建和应用规则

![text_document_fragments](assets/text_document_fragments.gif)

以下是本教程中创建的文档片段列表：

* [帐单详细信息](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [客户详细信息](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [帐单汇总](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [费用汇总](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

每个文档片段都包含具有静态文本的字段、从表单数据模型接收的数据以及使用代理UI输入的数据。 [规划交互式通信](/help/forms/using/planning-interactive-communications.md)部分中描述了所有这些字段。

在本教程中创建文档片段时，会为使用代理UI接收数据的字段创建变量。

如[创建表单数据模型](../../forms/using/create-form-data-model0.md)部分中所述，使用&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，以在本教程中创建文档片段。

## 步骤1:创建清单详细信息文本文档片段{#step-create-bill-details-text-document-fragment}

“清单详细信息”单据片段包含以下字段：

| 字段 | 数据源 |
|---|---|
| 发票编号 | 代理 UI |
| 帐单期间 | 代理 UI |
| 帐单日期 | 代理 UI |
| 您的计划 | 表单数据模型 |

执行以下步骤，为以Agent UI作为数据源的字段创建变量，创建静态文本，并在文档片段中使用表单数据模型元素：

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。

1. 选择&#x200B;**创建** > **文本**。
1. 指定以下信息：

   1. 在&#x200B;**标题**&#x200B;字段中输入&#x200B;**bill_details_first_ic**&#x200B;作为名称。 将在&#x200B;**Name**&#x200B;字段中自动填充标题。

   1. 从&#x200B;**数据模型**&#x200B;部分选择&#x200B;**表单数据模型**。

   1. 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**Next**。

1. 选择左窗格中的&#x200B;**Variables**&#x200B;选项卡，然后点按&#x200B;**创建**。
1. 在&#x200B;**创建变量**&#x200B;部分中：

   1. 输入&#x200B;**Invoicenumber**&#x200B;作为变量的名称。
   1. 选择&#x200B;**字符串**&#x200B;作为类型。
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

1. 将光标放在&#x200B;**发票编号**&#x200B;字段旁边，并双击左窗格&#x200B;**变量**&#x200B;选项卡中的&#x200B;**InvoiceNumber**&#x200B;变量。
1. 将光标放在&#x200B;**Bill Period**&#x200B;字段旁边，并双击&#x200B;**Billperiod**&#x200B;变量。
1. 将光标放在&#x200B;**帐单日期**&#x200B;字段旁边，并双击&#x200B;**帐单日期**&#x200B;变量。
1. 选择左窗格中的&#x200B;**数据模型对象**&#x200B;选项卡。
1. 将光标放在&#x200B;**Your Plan**&#x200B;字段旁边，并双击&#x200B;**customer** > **customerplan**&#x200B;属性。

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. 单击&#x200B;**保存**&#x200B;以创建“清单详细信息”文本文档片段。

## 步骤2:创建客户详细信息文本文档片段{#step-create-customer-details-text-document-fragment}

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

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**创建** > **文本**。
1. 指定以下信息：

   1. 在&#x200B;**标题**&#x200B;字段中输入&#x200B;**customer_details_first_ic**&#x200B;作为名称。 将在&#x200B;**Name**&#x200B;字段中自动填充标题。

   1. 从&#x200B;**数据模型**&#x200B;部分选择&#x200B;**表单数据模型**。

   1. 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**Next**。

1. 选择左窗格中的&#x200B;**Variables**&#x200B;选项卡，然后点按&#x200B;**创建**。
1. 在&#x200B;**创建变量**&#x200B;部分中：

   1. 输入&#x200B;**Placesupply**&#x200B;作为变量的名称。
   1. 选择&#x200B;**字符串**&#x200B;作为类型。
   1. 点按&#x200B;**创建**。

   重复步骤4和5以创建以下变量：

   * Statecode:数字类型
   * 数字连接：数字类型


1. 选择&#x200B;**数据模型对象**&#x200B;选项卡，将光标放在右侧窗格中，然后双击&#x200B;**customer** > **name**&#x200B;属性。
1. 按Enter将光标移到下一行，然后双击&#x200B;**customer** > **address**&#x200B;属性。
1. 使用右侧窗格为以下字段创建静态文本：

   * 手机号码
   * 备用联系人号码
   * 供应地
   * 关系数
   * 状态代码
   * 连接数

   ![客户详细信息静态文本](assets/customer_details_static_text_new.png)

1. 将光标放在&#x200B;**Mobile Number**&#x200B;字段旁边，并双击&#x200B;**customer** > **mobilenum**&#x200B;属性。
1. 将光标放在&#x200B;**Alternate Contact Number**&#x200B;字段旁边，并双击** customer** > **alternatemobilenumber**&#x200B;属性。
1. 将光标放在&#x200B;**Relationship Number**&#x200B;字段旁边，并双击&#x200B;**customer** > **relationshipnumber**&#x200B;属性。
1. 选择&#x200B;**变量**&#x200B;选项卡，将光标放在&#x200B;**供应地点**&#x200B;字段旁边，并双击&#x200B;**供应**&#x200B;变量。
1. 将光标放在&#x200B;**State Code**&#x200B;字段旁边，并双击&#x200B;**Statecode**&#x200B;变量。
1. 将光标放在&#x200B;**连接数**&#x200B;字段旁边，并双击&#x200B;**连接数**&#x200B;变量。

   ![客户详细信息](assets/customer_details_df2_new.png)

1. 单击&#x200B;**Save**&#x200B;以创建“客户详细信息”文本文档片段。

## 步骤3:创建清单汇总文本文档片段{#step-create-bill-summary-text-document-fragment}

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

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**创建** > **文本**。
1. 指定以下信息：

   1. 在&#x200B;**标题**&#x200B;字段中输入&#x200B;**bill_summary_first_ic**&#x200B;作为名称。 将在&#x200B;**Name**&#x200B;字段中自动填充标题。

   1. 从&#x200B;**数据模型**&#x200B;部分选择&#x200B;**表单数据模型**。

   1. 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**Next**。

1. 选择左窗格中的&#x200B;**Variables**&#x200B;选项卡，然后点按&#x200B;**创建**。
1. 在&#x200B;**创建变量**&#x200B;部分中：

   1. 输入&#x200B;**Previousbalance**&#x200B;作为变量的名称。
   1. 选择&#x200B;**Number**&#x200B;作为类型。
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

1. 将光标放在&#x200B;**上一余额**&#x200B;字段旁边，并双击&#x200B;**上一余额**&#x200B;变量。
1. 将光标放在&#x200B;**Payments**&#x200B;字段旁边，并双击&#x200B;**Payments**&#x200B;变量。
1. 将光标放在&#x200B;**Adjustments**&#x200B;字段旁边，并双击&#x200B;**Adjustments**&#x200B;变量。
1. 将光标放在&#x200B;**Amount Due**&#x200B;字段旁边，并双击&#x200B;**Amountdue**&#x200B;变量。
1. 将光标放在&#x200B;**到期日**&#x200B;字段旁边，并双击&#x200B;**Duedate**&#x200B;变量。
1. 选择&#x200B;**数据模型对象**&#x200B;选项卡，将光标放在右窗格的&#x200B;**当前帐单期间**&#x200B;字段旁边，然后双击&#x200B;**帐单** > **usagecharges**&#x200B;属性。

   ![帐单汇总](assets/bill_summary_static_variables_new.png)

1. 单击&#x200B;**Save**&#x200B;以创建“客户详细信息”文本文档片段。

## 步骤4:创建费用汇总文本文档片段{#step-create-summary-of-charges-text-document-fragment}

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

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**创建** > **文本**。
1. 指定以下信息：

   1. 在&#x200B;**标题**&#x200B;字段中输入&#x200B;**summary_charges_first_ic**&#x200B;作为名称。 将在“名称”字段中自动填充标题。

   1. 从&#x200B;**数据模型**&#x200B;部分选择&#x200B;**表单数据模型**。

   1. 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**Next**。

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

1. 选择&#x200B;**数据模型对象**&#x200B;选项卡。
1. 将光标放在&#x200B;**呼叫费用**&#x200B;字段旁边，并双击&#x200B;**bills** > **呼叫费用**&#x200B;属性。
1. 将光标放在&#x200B;**电话会议费用**&#x200B;字段旁边，并双击&#x200B;**bills** > **confcallcarges**&#x200B;属性。
1. 将光标放在&#x200B;**SMS Carges**&#x200B;字段旁边，并双击&#x200B;**bills** > **smscarges**&#x200B;属性。
1. 将光标放在&#x200B;**Mobile Internet Charges**&#x200B;字段旁边，并双击&#x200B;**bills** > **internetcharges**&#x200B;属性。
1. 将光标放在&#x200B;**国家漫游费用**&#x200B;字段旁边，并双击&#x200B;**bills** > **国家漫游费用**&#x200B;属性。
1. 将光标放在&#x200B;**国际漫游费用**&#x200B;字段旁边，并双击&#x200B;**bills** > **roamingintnl**&#x200B;属性。
1. 将光标放在&#x200B;**Value Added Services Charges**&#x200B;字段旁边，并双击&#x200B;**bills** > **vas**&#x200B;属性。
1. 将光标放在&#x200B;**总费用**&#x200B;字段旁边，并双击&#x200B;**bills** > **usagecharges**&#x200B;属性。
1. 将光标放在&#x200B;**TOTAL PAYABLE**&#x200B;字段旁边，并双击&#x200B;**bills** > **usagecharges**&#x200B;属性。

   ![费用汇总](assets/summary_charges_static_fdm_new.png)

1. 选择&#x200B;**增值服务费用**&#x200B;行中的文本，然后点按&#x200B;**创建规则**&#x200B;以创建一个条件，根据该条件在交互通信中显示该行：
1. 在&#x200B;**创建规则**&#x200B;弹出窗口中：

   1. 选择&#x200B;**数据模型和变量**，然后选择&#x200B;**bills** > **callcarges**。

   1. 选择&#x200B;**小于**&#x200B;作为运算符。
   1. 选择&#x200B;**Number**&#x200B;并输入值作为&#x200B;**60**。

   根据此条件，仅当“呼叫费用”字段的值小于60时，才会显示“增值服务费用”行。

   ![create_rules_caption](assets/create_rules_caption.gif)

1. 单击&#x200B;**Save**&#x200B;以创建费用摘要文本文档片段。
