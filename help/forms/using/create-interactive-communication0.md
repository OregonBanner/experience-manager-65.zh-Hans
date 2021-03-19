---
title: “教程：创建交互通信"
seo-title: 创建用于印刷和Web的交互式通信
description: 使用所有构件块创建交互式通信
seo-description: 使用所有构件块创建交互式通信
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: 交互式通信
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# 教程：创建交互通信{#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的一个步骤。 建议按照时间顺序按照该系列进行操作，以了解、执行和演示完整的教程用例。

创建所有构建基块(如表单数据模型、文档片段、模板和Web版主题)后，您可以开始创建交互式通信。

交互式通信可通过两种渠道提供：印刷和Web。 您还可以创建交互式通信，将打印渠道作为主控。 Web渠道的打印为主控选项可确保Web渠道的内容、继承和数据绑定是从打印渠道派生的。 它还确保在打印渠道中所做的更改在Web渠道中同步。 但是，允许交互通信作者中断Web渠道中特定组件的继承。

本教程将指导您逐步创建适用于印刷和Web渠道的交互式通信。 在本教程的结尾，您将能够：

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建印刷和Web交互式通信，使印刷主控

## 创建无同步{#create-interactive-communications-for-print-and-web-with-no-synchronization}的用于打印和Web的交互式通信

### 为打印渠道{#create-interactive-communication-for-print-channel}创建交互式通信

以下是本教程中已创建的、在为打印渠道创建交互式通信时需要的资源列表:

**打印模** [板：create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表单数据模** [型：FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片** [段：bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**布局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**图像：** PayNow和ValueAddedServices

1. 登录到AEM作者实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**&#x200B;并选择&#x200B;**交互通信**。 此时将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**渠道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为“打印”模板，然后点按&#x200B;**选择**。 确保未选中&#x200B;**“使用Print as 主控于Web渠道**”复选框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按&#x200B;**编辑**&#x200B;以在右侧窗格中打开交互式通信。
1. 转到&#x200B;**资产**&#x200B;选项卡，并应用筛选器以在左侧窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

   ![文档片段](assets/create_first_ic_doc_fragments_new.png)

1. 点按&#x200B;**图表**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**图表**&#x200B;组件。
1. 点按图表组件并选择![configure_icon](assets/configure_icon.png)（配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从&#x200B;**图表类型**&#x200B;下拉列表中选择&#x200B;**饼图**。
   1. 从&#x200B;**X轴**&#x200B;部分的&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。
   1. 从&#x200B;**Function**&#x200B;下拉列表中选择&#x200B;**Frequency**。
   1. 从&#x200B;**Y轴**&#x200B;部分的&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。
   1. 点按![done_icon](assets/done_icon.png)以保存图表属性。

1. 转到&#x200B;**资产**&#x200B;选项卡，并应用筛选器以在左侧窗格中仅显示布局片段。 将&#x200B;**table_lf**&#x200B;布局片段拖放到&#x200B;**明细调用**&#x200B;目标区。
1. 在&#x200B;**Date**&#x200B;列中选择文本字段，然后点按![configure_icon](assets/configure_icon.png)(Configure)。
1. 从&#x200B;**绑定类型**&#x200B;下拉列表中选择&#x200B;**数据模型对象**，然后选择&#x200B;**调用** > **调用日期**。 点按两次![done_icon](assets/done_icon.png)以保存属性。

   同样，为&#x200B;**Time**、**Number**、**和**&#x200B;中的文本字段创建与&#x200B;**调用时间**、**调用号**、**和**&#x200B;调用2/>持续时间&#x200B;**和**&#x200B;费用&#x200B;**列。**

1. 点按&#x200B;**PayNow**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**Image**&#x200B;组件。
1. 点按图像组件并选择![configure_icon](assets/configure_icon.png)（配置）。 图像属性显示在左窗格中：

   1. 在&#x200B;**名称**&#x200B;字段中指定&#x200B;**PayNow**&#x200B;作为图像的名称。
   1. 点按&#x200B;**上载**，选择保存在本地文件系统中的图像，然后点按&#x200B;**打开**。
   1. 点按![done_icon](assets/done_icon.png)以保存图像属性。

1. 重复步骤13和14，将&#x200B;**ValueAddedServices**&#x200B;图像添加到&#x200B;**ValueAddedServices**&#x200B;目标区。

### 为Web渠道{#create-interactive-communication-for-web-channel}创建交互式通信

以下是本教程中已创建的资源的列表，创建Web渠道的交互式通信时需要这些资源：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表单数据模** [型：FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片** [段：bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**图像：** PayNowWeb和ValueAddedServicesWeb

1. 登录到AEM作者实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**&#x200B;并选择&#x200B;**交互通信**。 此时将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**渠道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为“打印”模板，然后点按&#x200B;**选择**。 确保未选中&#x200B;**“使用Print as 主控于Web渠道**”复选框。

   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按&#x200B;**编辑**&#x200B;以在右侧窗格中打开交互式通信。
1. 点按左窗格中的&#x200B;**渠道**&#x200B;选项卡，然后点按&#x200B;**Web**。
1. 转到&#x200B;**资产**&#x200B;选项卡，并应用筛选器以在左侧窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

1. 点按&#x200B;**“费用汇总**”目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**图表**&#x200B;组件。
1. 点按图表组件并选择![configure_icon](assets/configure_icon.png)（配置）。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从&#x200B;**图表类型**&#x200B;下拉列表中选择&#x200B;**饼图**。

   1. 从&#x200B;**X轴**&#x200B;部分的&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。

   1. 从&#x200B;**Function**&#x200B;下拉列表中选择&#x200B;**Frequency**。

   1. 从&#x200B;**Y轴**&#x200B;部分的&#x200B;**调用**&#x200B;数据模型对象类型中选择&#x200B;**calltype**&#x200B;属性。 点按![done_icon](assets/done_icon.png)。

   1. 点按![done_icon](assets/done_icon.png)以保存图表属性。

1. 从左侧窗格中选择&#x200B;**数据源**&#x200B;选项卡，并将&#x200B;**调用**&#x200B;数据模型对象拖放到&#x200B;**明细调用**&#x200B;目标区。 **调用**&#x200B;数据模型对象中的所有属性均显示为右侧窗格的&#x200B;**明细调用**&#x200B;目标区中的表列。

   根据用例，您需要在表中的“呼叫日期”、“呼叫时间”、“呼叫号码”、“呼叫持续时间”和“呼叫费用”列。

   ![交互通信表](assets/table_ic_web_new.png)

1. 选择&#x200B;**Mobilenum**&#x200B;表列标题，然后选择&#x200B;**更多选项** > **删除列**。 同样，删除&#x200B;**Calltype**&#x200B;列。
1. 选择&#x200B;**调用日期**&#x200B;表列标题，然后点按![edit](assets/edit.png)（编辑）将文本重命名为&#x200B;**调用日期**。 同样，重命名表中的其他列标题。
1. 根据用例，在交互通信中插入&#x200B;**立即付费**&#x200B;按钮，该按钮为用户提供通过单击按钮进行付款的选项。 执行以下步骤以插入按钮：

   1. 点按&#x200B;**立即付款**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**文本**&#x200B;组件。

   1. 点按文本组件，然后点按![edit](assets/edit.png)（编辑）。
   1. 将文本重命名为&#x200B;**立即付款**。
   1. 选择文本，然后点按超链接图标。
   1. 在&#x200B;**路径**&#x200B;字段中指定付款URL。
   1. 从&#x200B;**目标**&#x200B;下拉列表中选择&#x200B;**新建选项卡**。

   1. 点按![done_icon](assets/done_icon.png)以保存超链接属性。

1. 从&#x200B;**预览**&#x200B;选项旁边的下拉列表中选择&#x200B;**样式**。

   ![为交互式通信选择样式模式](assets/select_style_ic_web_new.png)

1. 设置超链接文本的样式，以在交互式通信中将其显示为按钮，步骤如下：

   1. 点按文本组件并选择![edit](assets/edit.png)（编辑）。
   1. 在&#x200B;**边框**&#x200B;部分，将&#x200B;**1.5px**&#x200B;指定为&#x200B;**边框宽度**，选择&#x200B;**实底**&#x200B;为&#x200B;**边框样式**，将&#x200B;**46px**&#x200B;指定为&#x200B;**边框半径**。

   1. 从&#x200B;**Background**&#x200B;部分选择Red作为按钮的背景颜色。
   1. 在&#x200B;**Dimension和位置**&#x200B;部分的&#x200B;**边距**&#x200B;字段中，点按&#x200B;**同时编辑**&#x200B;图标，并将&#x200B;**右**&#x200B;边距设置为&#x200B;**450px**。 “顶部”、“底部”和“左侧”字段设置为空。

   ![在交互通信中插入超链接](assets/ic_web_hyperlink_new.png)

1. 点按&#x200B;**立即付费**&#x200B;目标区域，然后点按&#x200B;**+**&#x200B;以添加&#x200B;**图像**&#x200B;组件。
1. 点按图像组件并选择![configure_icon](assets/configure_icon.png)（配置）。 图像属性显示在左窗格中：

   1. 在&#x200B;**名称**&#x200B;字段中指定&#x200B;**PayNow**&#x200B;作为图像的名称。

   1. 点按&#x200B;**上载**，选择保存在本地文件系统上的&#x200B;**PayNowWeb**&#x200B;图像，然后点按&#x200B;**打开**。

   1. 点按![done_icon](assets/done_icon.png)以保存图像属性。

1. 根据用例，在交互通信中插入&#x200B;**订阅**&#x200B;按钮，该按钮为用户提供通过单击该按钮订阅增值服务的选项。

   重复步骤13 - 17，将&#x200B;**订阅**&#x200B;按钮添加到&#x200B;**增值服务**&#x200B;目标区域，并添加&#x200B;**增值服务Web**&#x200B;图像。

## 使用自动同步{#create-interactive-communications-for-print-and-web-with-auto-synchronization}创建用于打印和Web的交互式通信

您还可以通过启用打印和Web渠道之间的自动同步来创建交互式通信。 要启用自动同步，请在创建交互式通信时选择“打印为主控”选项。 选择“打印为主控”选项可确保Web渠道的内容、继承和数据绑定是从“打印”渠道派生的。 它还确保在打印渠道中所做的更改反映在Web渠道中。

执行以下步骤，以使用“打印渠道”衍生Web渠道内容：

1. 登录到AEM作者实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**创建**&#x200B;并选择&#x200B;**交互通信**。 此时将显示&#x200B;**创建交互式通信**&#x200B;向导。
1. 在&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;字段中指定&#x200B;**create_first_ic**。 选择&#x200B;**FDM_Create_First_IC**&#x200B;作为表单数据模型，然后点按&#x200B;**下一个**。
1. 在&#x200B;**渠道**&#x200B;向导中：

   1. 指定&#x200B;**create_first_ic_print_template**&#x200B;作为“打印”模板，然后点按&#x200B;**选择**。

   1. 选中&#x200B;**“使用打印作为Web渠道的主控”复选框**。
   1. 指定&#x200B;**Create_First_IC_templates**&#x200B;文件夹> **Create_First_IC_Web_Template**&#x200B;作为Web模板，然后点按&#x200B;**选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按&#x200B;**编辑**&#x200B;以在右侧窗格中打开交互式通信。
1. 执行[创建用于打印渠道的交互式通信部分的步骤6 - 15。](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel)
1. 点按左窗格中的&#x200B;**渠道**&#x200B;选项卡，然后点按&#x200B;**Web**&#x200B;以从“打印”渠道自动生成Web渠道的内容。
1. 在步骤4中选中&#x200B;**将“打印为Web渠道的主控”复选框**&#x200B;时，将从“打印”渠道自动为Web渠道生成内容和绑定。

   打印渠道内容会插入到Web渠道模板内容的下方。 要修改从“打印”渠道自动生成的Web渠道内容，可以取消任何目标区域的继承。

   将鼠标悬停在Web渠道中的相关目标区域上，选择![canceliheritance](assets/cancelinheritance.png)（取消继承），然后在&#x200B;**取消继承**&#x200B;对话框中，点按&#x200B;**是**。

   ![取消继承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消某个组件的继承，则可以重新启用该组件。 要重新启用继承，请将指针悬停在包含该组件的相关目标区域的边界上，然后点按![重新启用继承](assets/reenableinheritance.png)。

1. 在左窗格中选择&#x200B;**内容**&#x200B;选项卡。
1. 使用内容树将自动生成的Web渠道内容拖放到Web模板中的现有面板。 以下是需要重新排列的组件的列表:

   * “清单详细信息”组件至“清单详细信息”面板
   * 客户详细信息组件到“客户详细信息”面板
   * “开单汇总”组件至“开单汇总”面板
   * “费用”组件汇总至“费用汇总”面板
   * 布局片段（表）到“分项调用”面板

   ![Web内容树](assets/ic_web_content_tree_new.png)

1. 重复[“为Web渠道](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel)创建交互式通信”中的步骤13 - 18，以在交互式通信的Web渠道中插入&#x200B;**立即付费**&#x200B;和&#x200B;**订阅**&#x200B;超链接。

