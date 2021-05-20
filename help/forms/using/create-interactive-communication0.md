---
title: “教程：创建交互式通信“
seo-title: 为打印和Web创建交互式通信
description: 使用所有构建基块创建交互式通信
seo-description: 使用所有构建基块创建交互式通信
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: 交互式通信
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# 教程：创建交互式通信{#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

在为Web版本创建了所有构建基块（如表单数据模型、文档片段、模板和主题）后，即可开始创建交互式通信。

交互式通信可以通过两种渠道来提供：打印和Web。 您还可以创建与打印渠道的交互式通信作为主控。 Web渠道的打印为主控选项可确保Web渠道的内容、继承和数据绑定是从打印渠道派生的。 它还可确保在打印渠道中所做的更改在Web渠道中同步。 但是，允许交互式通信作者中断Web渠道中特定组件的继承。

本教程将指导您完成为打印和Web渠道创建交互式通信的步骤。 在本教程结束时，您将能够：

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建打印和Web交互式通信与打印作为主控

## 创建无同步的打印和Web交互式通信{#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 为打印渠道创建交互式通信{#create-interactive-communication-for-print-channel}

以下是本教程中已创建并在为打印渠道创建交互式通信时需要的资源列表：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**布局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**图像：** PayNow和ValueAddedServices

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**，然后选择&#x200B;**交互式通信**。 将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**通道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为打印模板，然后点按&#x200B;**选择**。 确保未选中&#x200B;**使用打印作为Web渠道的主控复选框**。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示确认消息，表明已成功创建交互式通信。

1. 点按&#x200B;**编辑** ，以在右侧窗格中打开交互式通信。
1. 转到&#x200B;**Assets**&#x200B;选项卡，然后应用过滤器以在左侧窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互式通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 帐单详细信息 |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

   ![交互式通信的文档片段](assets/create_first_ic_doc_fragments_new.png)

1. 点按&#x200B;**Charts**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**Chart**&#x200B;组件。
1. 点按图表组件，然后选择![configure_icon](assets/configure_icon.png)（配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从&#x200B;**图表类型**&#x200B;下拉列表中选择&#x200B;**饼图**。
   1. 在&#x200B;**X轴**&#x200B;部分中，从&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。
   1. 从&#x200B;**函数**&#x200B;下拉列表中选择&#x200B;**频率**。
   1. 在&#x200B;**Y轴**&#x200B;部分中，从&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。
   1. 点按![done_icon](assets/done_icon.png)以保存图表属性。

1. 转到&#x200B;**Assets**&#x200B;选项卡，然后应用过滤器以在左侧窗格中仅显示布局片段。 将&#x200B;**table_lf**&#x200B;布局片段拖放到&#x200B;**明细调用**&#x200B;目标区域。
1. 选择&#x200B;**Date**&#x200B;列中的文本字段，然后点按![configure_icon](assets/configure_icon.png)(Configure)。
1. 从&#x200B;**绑定类型**&#x200B;下拉列表中选择&#x200B;**数据模型对象**，然后选择&#x200B;**调用** > **调用日期**。 点按![done_icon](assets/done_icon.png)两次以保存属性。

   同样，为&#x200B;**Time**、**Number**、**Duration**、**Callduration**&#x200B;和&#x200B;**Callcarges**&#x200B;中的文本字段分别创建与&#x200B;**calltime**、**Duration**&#x200B;和&#x200B;**Carges**&#x200B;列中的文本字段的绑定。

1. 点按&#x200B;**PayNow**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**图像**&#x200B;组件。
1. 点按图像组件，然后选择![configure_icon](assets/configure_icon.png)（配置）。 图像属性显示在左窗格中：

   1. 在&#x200B;**名称**&#x200B;字段中指定&#x200B;**PayNow**&#x200B;作为图像的名称。
   1. 点按&#x200B;**Upload**，选择本地文件系统上保存的图像，然后点按&#x200B;**Open**。
   1. 点按![done_icon](assets/done_icon.png)以保存图像属性。

1. 重复步骤13和14，将&#x200B;**ValueAddedServices**&#x200B;图像添加到&#x200B;**ValueAddedServices**&#x200B;目标区域。

### 为Web渠道创建交互式通信{#create-interactive-communication-for-web-channel}

以下是本教程中已创建并在为Web渠道创建交互式通信时需要的资源列表：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**图像：** PayNowWeb和ValueAddedServicesWeb

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**，然后选择&#x200B;**交互式通信**。 将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**通道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为打印模板，然后点按&#x200B;**选择**。 确保未选中&#x200B;**使用打印作为Web渠道的主控复选框**。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示确认消息，表明已成功创建交互式通信。

1. 点按&#x200B;**编辑** ，以在右侧窗格中打开交互式通信。
1. 点按左窗格中的&#x200B;**渠道**&#x200B;选项卡，然后点按&#x200B;**Web**。
1. 转到&#x200B;**Assets**&#x200B;选项卡，然后应用过滤器以在左侧窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互式通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | 帐单详细信息 |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

1. 点按&#x200B;**费用摘要**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**Chart**&#x200B;组件。
1. 点按图表组件，然后选择![configure_icon](assets/configure_icon.png)（配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从&#x200B;**图表类型**&#x200B;下拉列表中选择&#x200B;**饼图**。

   1. 在&#x200B;**X轴**&#x200B;部分中，从&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。

   1. 从&#x200B;**函数**&#x200B;下拉列表中选择&#x200B;**频率**。

   1. 在&#x200B;**Y轴**&#x200B;部分中，从&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。

   1. 点按![done_icon](assets/done_icon.png)以保存图表属性。

1. 从左窗格中选择&#x200B;**数据源**&#x200B;选项卡，并将&#x200B;**调用**&#x200B;数据模型对象拖放到&#x200B;**明细调用**&#x200B;目标区域。 **调用**&#x200B;数据模型对象中的所有属性都以表列的形式显示在右侧窗格的&#x200B;**明细调用**&#x200B;目标区域中。

   根据用例，您需要在表中填写“呼叫日期”、“呼叫时间”、“呼叫号码”、“呼叫持续时间”和“呼叫费用”列。

   ![交互式通信表](assets/table_ic_web_new.png)

1. 选择&#x200B;**Mobilenum**&#x200B;表列标题，然后选择&#x200B;**更多选项** > **删除列**。 同样，删除&#x200B;**Calltype**&#x200B;列。
1. 选择&#x200B;**调用日期**&#x200B;表列标题，然后点按![编辑](assets/edit.png)（编辑），将文本重命名为&#x200B;**调用日期**。 同样，重命名表中的其他列标题。
1. 根据用例，在交互式通信中插入&#x200B;**立即付款**&#x200B;按钮，该按钮为用户提供通过单击按钮进行付款的选项。 执行以下步骤以插入按钮：

   1. 点按&#x200B;**立即付款**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**Text**&#x200B;组件。

   1. 点按文本组件，然后点按![编辑](assets/edit.png)（编辑）。
   1. 将文本重命名为&#x200B;**Pay Now**。
   1. 选择文本，然后点按超链接图标。
   1. 在&#x200B;**Path**&#x200B;字段中指定付款URL。
   1. 从&#x200B;**Target**&#x200B;下拉列表中选择&#x200B;**新建选项卡**。

   1. 点按![done_icon](assets/done_icon.png)以保存超链接属性。

1. 从&#x200B;**预览**&#x200B;选项旁边的下拉列表中选择&#x200B;**样式**。

   ![选择交互式通信的样式模式](assets/select_style_ic_web_new.png)

1. 设置超链接文本的样式，以在交互式通信中将其显示为按钮，具体步骤如下：

   1. 点按文本组件，然后选择![编辑](assets/edit.png)（编辑）。
   1. 在&#x200B;**边框**&#x200B;部分中，将&#x200B;**1.5px**&#x200B;指定为&#x200B;**边框宽度**，选择&#x200B;**实体**&#x200B;作为&#x200B;**边框样式**，并将&#x200B;**46px**&#x200B;指定为&#x200B;**边框半径**。

   1. 从&#x200B;**Background**&#x200B;部分选择红色作为按钮的背景颜色。
   1. 在&#x200B;**Dimension和位置**&#x200B;部分的&#x200B;**边距**&#x200B;字段中，点按&#x200B;**同时编辑**&#x200B;图标，并将&#x200B;**右**&#x200B;边距设置为&#x200B;**450px**。 “顶部”、“底部”和“左侧”字段设置为空。

   ![在交互式通信中插入超链接](assets/ic_web_hyperlink_new.png)

1. 点按&#x200B;**立即付款**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**图像**&#x200B;组件。
1. 点按图像组件，然后选择![configure_icon](assets/configure_icon.png)（配置）。 图像属性显示在左窗格中：

   1. 在&#x200B;**名称**&#x200B;字段中指定&#x200B;**PayNow**&#x200B;作为图像的名称。

   1. 点按&#x200B;**上载**，选择本地文件系统上保存的&#x200B;**PayNowWeb**&#x200B;图像，然后点按&#x200B;**打开**。

   1. 点按![done_icon](assets/done_icon.png)以保存图像属性。

1. 根据用例，在交互式通信中插入&#x200B;**Subscribe**&#x200B;按钮，通过单击该按钮为用户提供订阅增值服务的选项。

   重复步骤13 - 17，将&#x200B;**订阅**&#x200B;按钮添加到&#x200B;**增值服务**&#x200B;目标区域，并添加&#x200B;**ValueAddedServicesWeb**&#x200B;图像。

## 使用自动同步创建打印和Web的交互式通信{#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您还可以通过启用打印和Web渠道之间的自动同步来创建交互式通信。 要启用自动同步，请在创建交互式通信时选择“打印为主控”选项。 选择“打印为主控”选项可确保从“打印”渠道派生Web渠道的内容、继承和数据绑定。 它还可确保在打印渠道中所做的更改反映在Web渠道中。

执行以下步骤以使用打印渠道获取Web渠道内容：

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**，然后选择&#x200B;**交互式通信**。 将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**通道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为打印模板，然后点按&#x200B;**选择**。

   1. 选中&#x200B;**使用打印作为Web渠道的主控复选框**。
   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示确认消息，表明已成功创建交互式通信。

1. 点按&#x200B;**编辑** ，以在右侧窗格中打开交互式通信。
1. 执行[为打印渠道创建交互式通信部分的步骤6 - 15。](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)
1. 点按左窗格中的&#x200B;**渠道**&#x200B;选项卡，然后点按&#x200B;**Web**&#x200B;以从“打印”渠道中自动生成Web渠道的内容。
1. 在步骤4中选中&#x200B;**使用打印作为Web渠道的主控复选框**&#x200B;时，将从打印渠道为Web渠道自动生成内容和绑定。

   打印渠道内容会插入到Web渠道模板内容的下方。 要修改从打印渠道自动生成的Web渠道内容，可以取消任何目标区域的继承。

   将鼠标悬停在Web渠道中的相关目标区域上，选择![cancelerientation](assets/cancelinheritance.png)（取消继承），然后在&#x200B;**取消继承**&#x200B;对话框中，点按&#x200B;**是**。

   ![取消继承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消组件的继承，则可以重新启用该组件。 要重新启用继承，请将鼠标悬停在相关目标区域（包括该组件）的边界上，然后点按![reenableintance](assets/reenableinheritance.png)。

1. 在左窗格中选择&#x200B;**Content**&#x200B;选项卡。
1. 使用内容树将自动生成的Web渠道内容拖放到Web模板中的现有面板。 以下是需要重新排列的组件列表：

   * “清单详细信息”组件至“清单详细信息”面板
   * “客户详细信息”组件到“客户详细信息”面板
   * 清单汇总组件至清单汇总面板
   * “费用汇总”面板中的“费用汇总”组件汇总
   * “明细调用”面板的布局片段（表）

   ![Web内容树](assets/ic_web_content_tree_new.png)

1. 重复[为Web渠道创建交互式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)的步骤13 - 18，以在交互式通信的Web渠道中插入&#x200B;**立即付费**&#x200B;和&#x200B;**订阅**&#x200B;超链接。
