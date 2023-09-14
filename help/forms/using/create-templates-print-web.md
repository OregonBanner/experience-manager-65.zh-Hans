---
title: “教程：创建模板”
description: 为交互式通信创建打印模板和Web模板
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 0%

---

# 教程：创建模板{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建议您按照时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

要创建交互式通信，必须在AEM服务器上为打印和Web渠道提供模板。

打印渠道的模板在AdobeForms Designer中创建，并上传到AEM服务器。 然后，这些模板便可在创建交互式通信时使用。

Web渠道的模板是在AEM中创建的。 模板作者和管理员可以创建、编辑和启用Web模板。 创建并启用后，这些模板便可在创建交互式通信时使用。

本教程将指导您完成为打印和Web渠道创建模板的步骤，以便在创建交互式通信时使用这些模板。 在本教程结束时，您将能够：

* 使用AdobeForms Designer为打印渠道创建XDP模板
* 将XDP模板上传到AEM Forms服务器
* 为Web渠道创建和启用模板

## 为打印渠道创建模板 {#create-template-for-print-channel}

使用以下任务为交互式通信的打印渠道创建和管理模板：

* [使用Forms设计器创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [将XDP模板上传到AEM Forms服务器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [为布局片段创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms设计器创建XDP模板 {#create-xdp-template-using-forms-designer}

基于 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖学](/help/forms/using/planning-interactive-communications.md)，在XDP模板中创建以下子表单：

* 帐单详细信息：包括文档片段
* 客户详细信息：包含文档片段
* 帐单摘要：包含文档片段
* 摘要：包括文档片段（费用子表单）和图表（图表子表单）
* 分项调用：包含表（布局片段）
* 立即支付：包含图像
* 增值服务：包含图像

![create_print_template](assets/create_print_template.gif)

将XDP文件上传到Forms服务器后，这些子表单在打印模板中显示为目标区域。 创建交互式通信时，文档片段、图表、布局片段和图像等所有实体都将添加到目标区域。

要为打印渠道创建XDP模板，请执行以下操作：

1. 打开Forms Designer，选择 **文件** > **新建** > **使用空白表单，** 点按 **下一个**，然后点击 **完成** 以打开用于创建模板的表单。

   确保 **对象库** 和 **对象** 从以下位置选择选项 **窗口** 菜单。

1. 拖放 **子表单** 来自的组件 **对象库** 到窗体。
1. 选择子表单，以便您能够在以下位置查看子表单的选项： **对象** 窗户。
1. 选择 **子表单** 选项卡并选择 **已流动** 从 **内容** 下拉列表。 要调整长度，请拖动子表单的左端点。
1. 在 **绑定** 选项卡：

   1. 指定 **账单详细信息** 在 **名称** 字段。

   1. 选择 **无数据绑定** 从 **数据绑定** 下拉列表。

   ![Designer子表单](assets/forms_designer_subform_new.png)

1. 同样，选择根子表单，选择 **子表单** 选项卡，然后选择 **已流动** 从 **内容** 下拉列表。 在 **绑定** 选项卡：

   1. 指定 **TelecaBill** 在 **名称** 字段。

   1. 选择 **无数据绑定** 从 **数据绑定** 下拉列表。

   ![打印模板的子表单](assets/root_subform_print_template_new.png)

1. 重复步骤2 - 5以创建以下子表单：

   * 账单详细信息
   * 客户详细信息
   * 账单摘要
   * 摘要 — 选择 **子表单** 选项卡并选择 **已定位** 从 **内容** 此子表单的下拉列表。 将以下子表单插入到 **摘要** 子表单。

      * 费用
      * 图表

   * ItemisedCalls
   * Paynow
   * ValueAddedServices

   为了节省时间，您还可以复制并粘贴现有子表单以创建其他子表单。

   要移动 **图表** 子表单在Charges子表单右侧，选择 **图表** 从左窗格中选择子表单 **布局** 选项卡，并为 **锚点X** 字段。 该值必须大于 **宽度** 字段 **费用** 子表单。 选择 **费用** 子表单并选择 **布局** 选项卡，以便您查看 **宽度** 字段。

1. 拖放 **文本** 对象来自 **对象库** 至表单并输入 **拨打XXXX进行订购** 文本。
1. 在左窗格中右键单击文本对象，选择 **重命名对象**，并输入文本对象的名称作为 **订阅**.

   ![XDP模板](assets/print_xdp_template_subform_new.png)

1. 选择 **文件** > **另存为** 将文件保存在本地文件系统中：

   1. 导航到可以保存文件的位置，并将名称指定为 **create_first_ic_print_template**.
   1. 选择 **.xdp** 从 **另存为类型** 下拉列表。

   1. 点按 **保存**.

### 将XDP模板上传到AEM Forms服务器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer创建XDP模板后，必须将其上传到AEM Forms服务器，以便该模板可在创建交互式通信时使用。

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **创建** > **文件上传**.

   导航并选择 **create_first_ic_print_template** 模板(XDP)并点按 **打开** 以将XDP模板导入AEM Forms服务器。

### 为布局片段创建XDP模板 {#create-xdp-template-for-layout-fragments}

要为交互式通信的打印渠道创建布局片段，请使用Forms Designer创建XDP并将其上传到AEM Forms服务器。

1. 打开Forms Designer，选择 **文件** > **新建** > **使用空白表单，** 点按 **下一个**，然后点击 **完成** 以打开用于创建模板的表单。

   确保 **对象库** 和 **对象** 从以下位置选择选项 **窗口** 菜单。

1. 拖放 **表** 来自的组件 **对象库** 到窗体。
1. 在“插入表”对话框中：

   1. 指定列数为 **5**.
   1. 将正文行数指定为 **1**.
   1. 选择 **在表中包含标题行** 复选框。
   1. 选项卡 **确定**.

1. 点按 **+** 在左窗格中单击 **表** 1并右键单击 **单元格1** 并选择 **重命名对象** 到 **日期**.

   同样，重命名 **单元格2**， **单元格3**， **单元格4**、和 **单元格5** 到 **时间**， **数字**， **持续时间**、和 **费用** 的量度。

1. 单击 **设计器视图** 并将其重命名为 **时间**， **数字**， **持续时间**、和 **费用**.

   ![布局片段](assets/layout_fragment_print_new.png)

1. 选择 **行1** 从左窗格中选择 **对象** > **绑定** > **对每个数据项重复一行**.

   ![重复布局片段的属性](assets/layout_fragment_print_repeat_new.png)

1. 拖放 **文本字段** 来自的组件 **对象库** 到 **设计器视图**.

   ![布局片段的文本字段](assets/layout_fragment_print_text_field_new.png)

   同样，拖放 **文本字段** 组件到 **时间**， **数字**， **持续时间**、和 **费用** 行。

1. 选择 **文件** > **另存为** 将文件保存在本地文件系统中：

   1. 导航到可以保存文件的位置，并将名称指定为 **table_lf**.
   1. 选择 **.xdp** 从 **另存为类型** 下拉列表。

   1. 点按 **保存**.

   使用Forms Designer为布局片段创建XDP模板后，您必须 [上传](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) AEM Forms以使其可在创建布局片段时使用。

## 为Web渠道创建模板 {#create-template-for-web-channel}

使用以下任务为交互式通信的Web渠道创建和管理模板：

* [为模板创建文件夹](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [创建模板](../../forms/using/create-templates-print-web.md#create-the-template)
* [启用模板](../../forms/using/create-templates-print-web.md#enable-the-template)
* [在交互式通信中启用按钮](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 为模板创建文件夹 {#create-folder-for-templates}

要创建Web渠道模板，请定义一个文件夹，您可以在其中保存创建的模板。 在该文件夹中创建模板后，启用该模板以允许表单用户根据该模板创建交互式通信的Web渠道。

要为可编辑模板创建文件夹，请执行以下操作：

1. 点按 **工具** ![锤子图标](assets/hammer-icon.svg) > **配置浏览器**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
1. 在配置浏览器页面中，点按 **创建**.
1. 在 **创建配置** 对话框，指定 **Create_First_IC_templates** 作为文件夹的标题，选中 **可编辑的模板**，然后点击 **创建**.

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   此 **Create_First_IC_templates** 文件夹创建并列在 **配置浏览器** 页面。

### 创建模板 {#create-the-template}

基于 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖学](/help/forms/using/planning-interactive-communications.md)，在Web模板中创建以下面板：

* 帐单详细信息：包括文档片段
* 客户详细信息：包含文档片段
* 帐单摘要：包含文档片段
* 费用汇总：包括文档片段和图表（两列式布局）
* 分项调用：包含表
* 立即支付：包括 **立即付款** 按钮和图像
* 增值服务：包括图像和 **订阅** 按钮。

![create_web_template](assets/create_web_template.gif)

创建交互式通信时，会添加所有实体，例如文档片段、图表、表格、图像和按钮。

在中为Web渠道创建模板 **Create_First_IC_templates** 文件夹，请执行以下步骤：

1. 通过选择 **工具** > **模板** > **Create_First_IC_templates** 文件夹。
1. 点按&#x200B;**创建**。
1. 在 **选择模板类型** 配置向导，选择 **交互式通信 — Web渠道** 并点击 **下一个**.
1. 在 **模板详细信息** 配置向导，指定 **Create_First_IC_Web_Template** 作为模板标题。 指定可选描述，然后点击 **创建**.

   确认消息 **Create_First_IC_Web_Template** 将显示。

1. 点按 **打开** 以在模板编辑器中打开模板。
1. 选择 **初始内容** 从旁边下拉列表中 **预览** 选项。

   ![模板编辑器](assets/template_editor_initial_content_new.png)

1. 点按 **根面板** 然后点击 **+** 查看可添加到模板的组件列表。
1. 在上方添加面板 **根面板**，选择 **面板** 从名单上。
1. 选择 **内容** 选项卡。 在步骤8中添加的新面板显示在 **根面板** 在内容树中。

   ![内容树](assets/content_tree_root_panel_new.png)

1. 选择面板并点按 ![configure_icon](assets/configure_icon.png) （配置）。
1. 在“属性”窗格中：

   1. 指定 **帐单详细信息** 在“名称”字段中。
   1. 指定 **帐单详细信息** 在标题字段中。
   1. 选择 **1** 从 **列数** 下拉列表。

   1. 要保存属性，请点击 ![保存](/help/forms/using/assets/done_icon.png).

   面板的名称将更新为 **帐单详细信息** 在内容树中。

1. 重复步骤7 - 11，向模板中添加具有以下属性的面板：

   | 名称 | 标题 | 列数 |
   |---|---|---|
   | customerdetails | 客户详细信息 | 1 |
   | 帐单摘要 | 账单摘要 | 1 |
   | 汇总费用 | 费用汇总 | 2 |
   | itemisedcalls | 分项呼叫 | 1 |
   | paynow | 立即付款 | 2 |
   | vas | 增值服务 | 1 |

   下图描述了将所有面板添加到模板后的内容树：

   ![所有面板的内容树](assets/content_tree_all_panels_new.png)

### 启用模板 {#enable-the-template}

创建Web模板后，必须在创建交互式通信时启用该模板以使用该模板。

要启用Web模板，请执行以下操作：

1. 点按 **工具** ![锤子图标](assets/hammer-icon.svg) > **模板**.
1. 导航至 **Create_First_IC_Web_Template** 模板，选择它，然后点按 **启用**.
1. 点按 **启用** 再次确认。

   模板已启用，其状态显示为“已启用”。 在为Web渠道创建交互式通信时，可以使用此模板。

### 在交互式通信中启用按钮 {#enabling-buttons-in-interactive-communications}

根据用例，您必须包含 **立即付款** 和 **订阅** 交互式通信中的按钮（自适应表单组件）。 要在交互式通信中启用这些按钮，请执行以下操作：

1. 选择 **结构** 从旁边下拉列表中 **预览** 选项。
1. 选择 **文档容器** 使用内容树并点按根面板 **策略** 以选择允许在交互式通信中使用的组件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在 **允许的组件** 选项卡 **属性** 部分，选择 **按钮** 从 **自适应表单** 组件。

   ![允许的组件](assets/allowed_components_af_new.png)

1. 要保存属性，请点击 ![保存](assets/done_icon.png).
