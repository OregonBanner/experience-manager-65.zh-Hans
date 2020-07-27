---
title: “教程： 创建交互式通信“
seo-title: 创建用于印刷和Web的交互式通信
description: 使用所有构件块创建交互式通信
seo-description: 使用所有构件块创建交互式通信
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 0%

---


# 教程： 创建交互式通信 {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

本教程是创建您的第一个 [交互式通信系列中的一个](/help/forms/using/create-your-first-interactive-communication.md) 步骤。 建议按照时间顺序按照系列来了解、执行和演示完整的教程用例。

为Web版本创建了表单数据模型、文档片段、模板和主题等所有构建基块后，您就可以开始创建交互式通信。

交互式通信可通过两种渠道提供： 印刷和Web。 您还可以创建交互式通信，将打印渠道作为主控。 Web渠道的打印为主控选项可确保Web渠道的内容、继承和数据绑定是从打印渠道派生的。 它还确保在打印渠道中所做的更改在Web渠道中同步。 但是，允许交互通信作者在Web渠道中中断特定组件的继承。

本教程将指导您逐步为印刷和Web渠道创建交互式通信。 在本教程的结尾，您将能够：

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建印刷和Web交互式通信，将印刷作为主控

## 无需同步即可创建用于印刷和Web的交互式通信 {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### 创建交互式通信以进行打印渠道 {#create-interactive-communication-for-print-channel}

以下是本教程中已创建的资源列表，创建打印渠道时需要这些资源：

**打印模板：** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**布局片段：** [table_lf](../../forms/using/create-templates-print-web.md)

**图像：** PayNow和ValueAddedServices

1. 登录到AEM作者实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 点按 **创建** ，然后选择 **交互式通信**。 将显 **示“创建交互** ”通信向导。
1. 在“ **标题”和** “名称”字 **段中指** 定create_first **** _ic。 选 **择FDM_Create_First_IC作为表单** “数据模型”，然后点 **按下一**&#x200B;步。
1. 在渠道 **向导** :

   1. 指 **定create_first_ic_print_template** 作为打印模板，然后点按 **选择**。 确保未选 **中“将打印用作Web渠道的主控** ”复选框。

   1. 指定 **Create_First_IC_templates文件夹** > **Create_First_IC_Web_Template作为Web模板** ，然后点按 **选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按 **编辑** ，以在右窗格中打开交互式通信。
1. 转到“资 **产** ”选项卡，应用筛选器以在左窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

   ![交互通信的文档片段](assets/create_first_ic_doc_fragments_new.png)

1. 点按 **图表** 目标区域，然 **后点按** +以添加图 **表组件** 。
1. 点按图表组件，然后选 ![择configure_icon](assets/configure_icon.png) (Configure)。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从“ **图表类** 型 **”下** 拉列表中选择“饼图”。
   1. 从X轴 **节** 的调用数 **据模型** 对象类型中选 **择调用类型属性** 。 点 ![按done_icon](assets/done_icon.png)。
   1. 从 **Function** （函数） **下拉** 列表中选择Frequency（频率）。
   1. 从Y轴 **部分****的调用数据模** 型对象类 **型中选择调** 用类型属性。 点 ![按done_icon](assets/done_icon.png)。
   1. 点按 ![done_icon](assets/done_icon.png) 以保存图表属性。

1. 转到“资 **产** ”选项卡，应用筛选器以在左侧窗格中仅显示布局片段。 将table_lf布局片 **段拖放** 到“项目化调 **用** ”目标区。
1. 在“日期”列中选择 **文本** 字段，然 ![后点按](assets/configure_icon.png) configure_icon(Configure)。
1. 从“ **绑定类型** ”下拉 **列表中选择** “数据模型对象 **”，然后选择“调** 用” **>**“调用日期”。 点按 ![两次done_icon](assets/done_icon.png) ，以保存属性。

   同样，在 **Calltime**、Callnumber、Calldime **、CalldimeCharges**、 **中分别创建与Calltime、CalldimeCarges、********************** 列、CalldimeCharges、CalldCarges列中的文本字段绑定。

1. 点按 **PayNow** 目标区域，然 **后点按+** 以添加图 **像组件** 。
1. 点按图像组件并选 ![择configure_icon](assets/configure_icon.png) (Configure)。 图像属性显示在左窗格中：

   1. 在 **“名** 称”字段中指定PayNow作为图像 **名称** 。
   1. 点 **按上**&#x200B;传 **，选择保存在本地文件系统上的图像，然后点按打**&#x200B;开。
   1. 点 ![按done_icon](assets/done_icon.png) 以保存图像属性。

1. 重复第13步和第14步， **将ValueAddedServices图** 像添加 **到ValueAddedServices** 目标区域中。

### Create Interactive Communication for Web channel {#create-interactive-communication-for-web-channel}

以下是本教程中已创建的资源列表，创建Web渠道时需要这些资源：

**Web模板：** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**表单数据模型：** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**文档片段：** [bill_details_first_ic、customer_details_first_ic、bill_summary_first_ic、summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**图像：** PayNowWeb和ValueAddedServicesWeb

1. 登录到AEM作者实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 点按 **创建** ，然后选择 **交互式通信**。 将显 **示“创建交互** ”通信向导。
1. 在“ **标题”和** “名称”字 **段中指** 定create_first **** _ic。 选 **择FDM_Create_First_IC作为表单** “数据模型”，然后点 **按下一**&#x200B;步。
1. 在渠道 **向导** :

   1. 指 **定create_first_ic_print_template** 作为打印模板，然后点按 **选择**。 确保未选 **中“将打印用作Web渠道的主控** ”复选框。

   1. 指定 **Create_First_IC_templates文件夹** > **Create_First_IC_Web_Template作为Web模板** ，然后点按 **选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按 **编辑** ，以在右窗格中打开交互式通信。
1. 点按左 **窗格** 中的渠道选项卡，然后点 **按Web**。
1. 转到“资 **产** ”选项卡，应用筛选器以在左窗格中仅显示文档片段。
1. 将以下文档片段拖放到交互通信中的目标区域：

   | 文档片段 | 目标区域 |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | 客户详细信息 |
   | bill_summary_first_ic | 帐单摘要 |
   | summary_charges_first_interactive_communication | 费用 |

1. 点按 **“费用汇总** ”目标区域，然 **后点按+** 以添加图表 **组件** 。
1. 点按图表组件，然后选 ![择configure_icon](assets/configure_icon.png) (Configure)。 图表属性显示在左窗格中：

   1. 指定图表的名称。
   1. 从“ **图表类** 型 **”下** 拉列表中选择“饼图”。

   1. 从X轴 **节** 的调用数 **据模型** 对象类型中选 **择调用类型属性** 。 点 ![按done_icon](assets/done_icon.png)。

   1. 从 **Function** （函数） **下拉** 列表中选择Frequency（频率）。

   1. 从Y轴 **节的** “调用 ******”数据模型对象类型** 中选择calltype属性。 点 ![按done_icon](assets/done_icon.png)。

   1. 点按 ![done_icon](assets/done_icon.png) 以保存图表属性。

1. 从左 **窗格中** ，选择“数据源”选项卡，将调用数据模型 **对象拖放到** “分项调用 **”** 目标区。 调用数据模 **型对象** 中的所有属性均显示为右侧窗 **格的“分项调用** ”目标区中的表列。

   根据用例，您需要表中的“呼叫日期”、“呼叫时间”、“呼叫号码”、“呼叫持续时间”和“呼叫费用”列。

   ![交互通信表](assets/table_ic_web_new.png)

1. 选择 **Mobilenum** 表列标题，然后选 **择更多选项** > **删除列**。 同样，删除“ **Calltype** ”列。
1. 选择调 **用日** 期表列标题并点 ![按编辑](assets/edit.png) （编辑）以将文本重命名为 **调用日期**。 同样，重命名表中的其他列标题。
1. 根据用例，在交互通信 **中插入** “立即付费”按钮，该按钮为用户提供通过单击按钮进行付款的选项。 执行以下步骤以插入按钮：

   1. 点按 **立即付** 目标区域，然后点 **按+** 以添加文 **本组件** 。

   1. 点按文本组件，然后点 ![按编](assets/edit.png) 辑（编辑）。
   1. 将文本重命名为“ **立即支付**”。
   1. 选择文本并点按超链接图标。
   1. 在“路径”字段中指定 **付款** URL。
   1. 从 **目标** 下拉 **式列表** 中选择“新建选项卡”。

   1. 点按 ![done_icon](assets/done_icon.png) 以保存超链接属性。

1. 从 **列表** (位于预览选项旁)的下拉 **中选择** Style。

   ![选择交互式通信的样式模式](assets/select_style_ic_web_new.png)

1. 设置超链接文本的样式，以在交互通信中将其显示为按钮，步骤如下：

   1. 点按文本组件，然后选择 ![编辑](assets/edit.png) （编辑）。
   1. 在“边 **框** ”部分中， **将1.5** px指定为“边框宽度 **”，选择“**&#x200B;边框”样式为边框样式，并指 ****************&#x200B;定4 px作为边框。

   1. 从“背景”部分选择红色作为按钮的背 **景颜** 色。
   1. 在“维 **度** 和位置 **的边距** ”字段 **中，点按“同时编** 辑”图标，并将 **“右边距”设置******&#x200B;为450px。 “顶部”、“底部”和“左侧”字段设置为空。

   ![在交互式通信中插入超链接](assets/ic_web_hyperlink_new.png)

1. 点按 **立即付** 目标区域，然后点 **按+** 以添加图 **像组件** 。
1. 点按图像组件并选 ![择configure_icon](assets/configure_icon.png) (Configure)。 图像属性显示在左窗格中：

   1. 在 **“名** 称”字段中指定PayNow作为图像 **名称** 。

   1. 点 **按上**&#x200B;传 **，选择保存在本** 地文件系统上的 **PayNowWeb图像，然后点按打**&#x200B;开。

   1. 点 ![按done_icon](assets/done_icon.png) 以保存图像属性。

1. 根据用例，在交互式 **通信** 中插入一个“订阅”按钮，该按钮通过单击该按钮为用户提供订阅增值服务的选项。

   重复第13 - 17步，将“订 **阅** ”按钮添 **加到“增值服务** ”目标区 **域并添加** ValueAddedServicesWeb图像。

## 使用自动同步创建用于打印和Web的交互式通信 {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

您还可以通过启用打印和Web渠道之间的自动同步来创建交互式通信。 要启用自动同步，请在创建交互式通信时选择“打印为主控”选项。 选择“打印为主控”选项可确保Web渠道的内容、继承和数据绑定是从“打印”渠道派生的。 它还确保在打印渠道中所做的更改反映在Web渠道中。

执行以下步骤，使用“打印渠道”衍生Web渠道内容：

1. 登录到AEM作者实例，然后导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 点按 **创建** ，然后选择 **交互式通信**。 将显 **示“创建交互** ”通信向导。
1. 在“ **标题”和** “名称”字 **段中指** 定create_first **** _ic。 选 **择FDM_Create_First_IC作为表单** “数据模型”，然后点 **按下一**&#x200B;步。
1. 在渠道 **向导** :

   1. 指 **定create_first_ic_print_template** 作为打印模板，然后点按 **选择**。

   1. 选中“ **使用打印作为主控进行Web渠道** ”复选框。
   1. 指定 **Create_First_IC_templates文件夹** > **Create_First_IC_Web_Template作为Web模板** ，然后点按 **选择**。

   1. 点按&#x200B;**创建**。

   将显示一条确认消息，提示已成功创建交互式通信。

1. 点按 **编辑** ，以在右窗格中打开交互式通信。
1. 执行“为打印渠道创 [建交互式通信”部分的步骤](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel) 6 - 15。
1. 点按左 **侧窗** 格中的渠道选项卡， **然后点按** Web，从打印渠道自动生成Web渠道的内容。
1. 在第4 **步中选中了“将打印用** 作主控渠道”复选框，将从“打印”渠道自动为Web渠道生成内容和绑定。

   打印渠道内容会插入到Web渠道模板内容的下方。 要修改已从“打印”渠道自动生成的Web渠道内容，可取消任何目标区域的继承。

   将指针悬停在Web目标中的相关渠道区域上，选 ![择取消继承](assets/cancelinheritance.png) （取消继承），然后在取消继承 **对话框中** ，点按 **是**。

   ![取消继承](assets/cancel_inheritance_web_channel_new.png)

   如果已取消某个组件的继承，则可以重新启用该继承。 要重新启用继承，请将指针悬停在包括该组件的相关目标区域的边界上，然后点按重新启 ![用继承](assets/reenableinheritance.png)。

1. 选择左 **窗格中** 的“内容”选项卡。
1. 使用内容树将自动生成的Web渠道内容拖放到Web模板中的现有面板。 以下是需要重新排列的组件的列表:

   * “清单详细信息”组件到“清单详细信息”面板
   * 客户详细信息组件到“客户详细信息”面板
   * “开单汇总”组件至“开单汇总”面板
   * “费用”组件汇总至“费用”面板汇总
   * 布局片段（表）到“明细的调用”面板

   ![Web内容树](assets/ic_web_content_tree_new.png)

1. 重复“为Web渠道创 [建交互式通信](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) ”中的第13 - 18步 **，将“立即** 付费”和“ **订阅** ”超链接插入交互式通信的Web渠道。

