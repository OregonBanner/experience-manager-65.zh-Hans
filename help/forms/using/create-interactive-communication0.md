---
title: “教程：创建交互式通信”
seo-title: Create an Interactive Communication for Print and Web
description: 使用所有构建块创建交互式通信
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# 教程：创建交互式通信 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建议按时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

为Web版本创建了所有构建块（如表单数据模型、文档片段、模板和主题）后，即可开始创建交互式通信。

交互式通信可通过两种渠道提供：打印和Web。 您还可以创建以Print channel作为母版的交互式通信。 Web渠道的“打印为主文件”选项确保Web渠道的内容、继承和数据绑定派生自“打印”渠道。 它还可确保在Print channel中所做的更改在Web channel中同步。 但是，允许交互式通信作者中断Web渠道中特定组件的继承。

本教程将指导您完成为打印和Web渠道创建交互式通信的步骤。 在本教程结束时，您将能够：

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建Print和Web交互通信并将Print作为母版

## 为打印和Web创建无同步的交互式通信 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 为打印渠道创建交互式通信 {#create-interactive-communication-for-print-channel}

以下是本教程中已创建、且在为打印渠道创建交互式通信时所需的资源列表：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic， customer_details_first_ic， bill_summary_first_ic， summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**布局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**图像：** paynow和ValueAddedServices

1. 登录到AEM创作实例并导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择 **创建** 并选择 **交互式通信**. 此 **创建交互式通信** 此时将显示向导。
1. 指定 **create_first_ic** 在 **标题** 和 **名称** 字段。 选择 **FDM_Create_First_IC** 作为表单数据模型，然后选择 **下一个**.
1. 在 **渠道** 向导：

   1. 指定 **create_first_ic_print_template** 作为打印模板，然后选择 **选择**. 确保 **为Web渠道使用“打印为主版”** 未选中复选框。

   1. 指定 **Create_First_IC_templates** 文件夹> **Create_First_IC_Web_Template** 作为Web模板，然后选择 **选择**.

   1. 选择&#x200B;**创建**。

   此时将显示一条确认消息，表明已成功创建交互式通信。

1. 选择 **编辑** 在右窗格中打开交互式通信。
1. 转到 **资产** 选项卡，并应用过滤器以在左窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互式通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 账单详细信息 |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 账单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

   ![交互式通信的文档片段](assets/create_first_ic_doc_fragments_new.png)

1. 选择 **图表** 目标区域，然后选择 **+** 以添加 **图表** 组件。
1. 选择图表组件并选择 ![configure_icon](assets/configure_icon.png) （配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 选择 **饼图** 从 **图表类型** 下拉列表。
   1. 选择 **calltype** 属性来自 **调用** 中的数据模型对象类型 **X轴** 部分。 选择 ![完成图标](assets/done_icon.png).
   1. 选择 **频率** 从 **函数** 下拉列表。
   1. 选择 **calltype** 属性来自 **调用** 中的数据模型对象类型 **Y轴** 部分。 选择 ![完成图标](assets/done_icon.png).
   1. 选择 ![完成图标](assets/done_icon.png) 以保存图表属性。

1. 转到 **资产** 选项卡，并应用过滤器以在左窗格中仅显示布局片段。 拖放 **table_lf** 布局片段到 **分项呼叫** 目标区域。
1. 选择中的文本字段 **日期** 列并选择 ![configure_icon](assets/configure_icon.png) （配置）。
1. 选择 **数据模型对象** 从 **绑定类型** 下拉列表并选择 **调用** > **calldate**. 选择 ![完成图标](assets/done_icon.png) 保存属性两次。

   同样，创建与的绑定 **calltime**， **callnum**， **callduration**、和 **callcharges** 中的文本字段 **时间**， **数字**， **持续时间**、和 **费用** 列进行归类。

1. 选择 **Paynow** 目标区域，然后选择 **+** 以添加 **图像** 组件。
1. 选择图像组件并选择 ![configure_icon](assets/configure_icon.png) （配置）。 图像属性显示在左窗格中：

   1. 指定 **Paynow** 作为图像在 **名称** 字段。
   1. 选择 **上传**，选择保存在本地文件系统中的图像，然后选择 **打开**.
   1. 选择 ![完成图标](assets/done_icon.png) 以保存图像属性。

1. 重复步骤13和14以添加 **ValueAddedServices** 图像到 **ValueAddedServices** 目标区域。

### 为Web渠道创建交互式通信 {#create-interactive-communication-for-web-channel}

以下是本教程中已创建、且在为Web渠道创建交互式通信时所需的资源列表：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic， customer_details_first_ic， bill_summary_first_ic， summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**图像：** PayNowWeb和ValueAddedServicesWeb

1. 登录到AEM创作实例并导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择 **创建** 并选择 **交互式通信**. 此 **创建交互式通信** 此时将显示向导。
1. 指定 **create_first_ic** 在 **标题** 和 **名称** 字段。 选择 **FDM_Create_First_IC** 作为表单数据模型，然后选择 **下一个**.
1. 在 **渠道** 向导：

   1. 指定 **create_first_ic_print_template** 作为打印模板，然后选择 **选择**. 确保 **为Web渠道使用“打印为主版”** 未选中复选框。

   1. 指定 **Create_First_IC_templates** 文件夹> **Create_First_IC_Web_Template** 作为Web模板，然后选择 **选择**.

   1. 选择&#x200B;**创建**。

   此时将显示一条确认消息，表明已成功创建交互式通信。

1. 选择 **编辑** 在右窗格中打开交互式通信。
1. 选择 **渠道** 选项卡，然后选择 **Web**.
1. 转到 **资产** 选项卡，并应用过滤器以在左窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互式通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 账单详细信息 |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 账单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

1. 选择 **费用汇总** 目标区域，然后选择 **+** 以添加 **图表** 组件。
1. 选择图表组件并选择 ![configure_icon](assets/configure_icon.png) （配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 选择 **饼图** 从 **图表类型** 下拉列表。

   1. 选择 **calltype** 属性来自 **调用** 中的数据模型对象类型 **X轴** 部分。 选择 ![完成图标](assets/done_icon.png).

   1. 选择 **频率** 从 **函数** 下拉列表。

   1. 选择 **calltype** 属性来自 **调用** 中的数据模型对象类型 **Y轴** 部分。 选择 ![完成图标](assets/done_icon.png).

   1. 选择 ![完成图标](assets/done_icon.png) 以保存图表属性。

1. 选择 **数据源** 选项卡，并拖放 **调用** 数据模型对象到 **分项呼叫** 目标区域。 中的全部属性 **调用** 数据模型对象将作为表列显示在 **分项呼叫** 右窗格中的目标区域。

   根据用例，您需要表中的呼叫日期、呼叫时间、呼叫编号、呼叫持续时间和呼叫费用列。

   ![交互式通信表](assets/table_ic_web_new.png)

1. 选择 **Mobilenum** 表列标题并选择 **更多选项** > **删除列**. 同样，删除 **调用类型** 列。
1. 选择 **Calldate** 表列标题并选择 ![编辑](assets/edit.png) （编辑）将文本重命名为 **通话日期**. 同样，重命名表中的其他列标题。
1. 根据用例，插入 **立即付款** 交互式通信中的按钮，它通过单击按钮为用户提供进行付款的选项。 执行以下步骤以插入按钮：

   1. 选择 **立即付款** 目标区域，然后选择 **+** 以添加 **文本** 组件。

   1. 选择文本组件并选择 ![编辑](assets/edit.png) （编辑）。
   1. 将文本重命名为 **立即付款**.
   1. 选择文本并选择“超链接”图标。
   1. 在中指定付款URL **路径** 字段。
   1. 选择 **新建选项卡** 从 **Target** 下拉列表。

   1. 选择 ![完成图标](assets/done_icon.png) 以保存超链接属性。

1. 选择 **样式** 从旁边下拉列表中 **预览** 选项。

   ![选择交互式通信的样式模式](assets/select_style_ic_web_new.png)

1. 使用以下步骤，将超链接文本设置为在交互式通信中作为按钮显示：

   1. 选择文本组件并选择 ![编辑](assets/edit.png) （编辑）。
   1. 在 **边框** 部分，指定 **1.5像素** 作为 **边框宽度**，选择 **实线** 作为 **边框样式**，并指定 **46像素** 作为 **边框半径**.

   1. 从中选择红色作为按钮的背景颜色 **背景** 部分。
   1. 在 **边距** 字段 **Dimension和位置** 部分，选择 **同时编辑** 图标，然后设置 **右** 边距 **450像素**. “顶部”、“底部”和“左侧”字段设置为空白。

   ![在交互式通信中插入超链接](assets/ic_web_hyperlink_new.png)

1. 选择 **立即付款** 目标区域，然后选择 **+** 以添加 **图像** 组件。
1. 选择图像组件并选择 ![configure_icon](assets/configure_icon.png) （配置）。 图像属性显示在左窗格中：

   1. 指定 **Paynow** 作为图像在 **名称** 字段。

   1. 选择 **上传**，选择 **paynowweb** 保存在本地文件系统中的图像，然后选择 **打开**.

   1. 选择 ![完成图标](assets/done_icon.png) 以保存图像属性。

1. 根据用例，插入 **订阅** 交互式通信中的按钮，通过单击此按钮，用户可以选择订阅增值服务。

   重复步骤13 - 17以添加 **订阅** 按钮至 **增值服务** 目标区域并添加 **ValueAddServicesWeb** 图像。

## 使用自动同步为打印和Web创建交互式通信 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您还可以通过启用打印和Web渠道之间的自动同步来创建交互式通信。 要启用自动同步，请在创建交互式通信时选择打印为主选项。 选择“打印为主文件”选项可以确保Web渠道的内容、继承和数据绑定派生自“打印”渠道。 它还可确保在打印渠道中所做的更改反映在Web渠道中。

执行以下步骤以使用打印渠道获取Web渠道内容：

1. 登录到AEM创作实例并导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择 **创建** 并选择 **交互式通信**. 此 **创建交互式通信** 此时将显示向导。
1. 指定 **create_first_ic** 在 **标题** 和 **名称** 字段。 选择 **FDM_Create_First_IC** 作为表单数据模型，然后选择 **下一个**.
1. 在 **渠道** 向导：

   1. 指定 **create_first_ic_print_template** 作为打印模板，然后选择 **选择**.

   1. 选择 **为Web渠道使用“打印为主版”** 复选框。
   1. 指定 **Create_First_IC_templates** 文件夹> **Create_First_IC_Web_Template** 作为Web模板，然后选择 **选择**.

   1. 选择&#x200B;**创建**。

   此时将显示一条确认消息，表明已成功创建交互式通信。

1. 选择 **编辑** 在右窗格中打开交互式通信。
1. 执行第6 - 15步，共 [为打印渠道创建交互式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 部分。
1. 选择 **渠道** 选项卡，然后选择 **Web** 从Print channel自动生成Web渠道的内容。
1. 作为 **为Web渠道使用“打印为主版”** 如果在步骤4中选中复选框，则会从Print channel为Web channel自动生成内容和绑定。

   打印渠道内容插入Web渠道模板内容下方。 要修改已从打印渠道自动生成的Web渠道内容，您可以取消任何目标区域的继承。

   将鼠标悬停在Web渠道中的相关目标区域上，然后选择 ![取消继承](assets/cancelinheritance.png) （取消继承），然后在 **取消继承** 对话框，选择 **是**.

   ![取消继承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消组件的继承，则可以重新启用它。 要重新启用继承，请将鼠标悬停在相关目标区域（包括组件）的边界上，然后选择 ![reenableinheritance](assets/reenableinheritance.png).

1. 选择 **内容** 选项卡。
1. 使用内容树将自动生成的Web渠道内容拖放到Web模板中的现有面板。 以下是需要重新排列的组件列表：

   * “清单详细信息”面板中的清单详细信息组件
   * “客户详细信息”组件到“客户详细信息”面板
   * “清单汇总”面板中的清单汇总组件
   * “费用汇总”组件到“费用汇总”面板
   * “分项调用”面板的布局片段（表）

   ![Web内容树](assets/ic_web_content_tree_new.png)

1. 重复步骤13 - 18，共 [为Web渠道创建交互式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) 插入 **立即付款** 和 **订阅** 交互式通信Web渠道中的超链接。
