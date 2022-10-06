---
title: “教程：创建模板”
seo-title: Create Print and Web templates for Interactive Communication
description: 为交互式通信创建打印模板和Web模板
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 1%

---

# 教程：创建模板{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教程是 [创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

要创建交互式通信，您必须在AEM服务器上提供用于打印和Web渠道的模板。

打印渠道的模板在AdobeForms Designer中创建并上传到AEM服务器。 然后，在创建交互式通信时，即可使用这些模板。

Web渠道的模板在AEM中创建。 模板作者和管理员可以创建、编辑和启用Web模板。 创建并启用后，这些模板便可在创建交互式通信时使用。

本教程将指导您完成为打印和Web渠道创建模板的步骤，以便在创建交互式通信时使用这些模板。 在本教程结束时，您将能够：

* 使用AdobeForms Designer为打印渠道创建XDP模板
* 将XDP模板上传到AEM Forms Server
* 为Web渠道创建和启用模板

## 为打印渠道创建模板 {#create-template-for-print-channel}

使用以下任务为交互式通信的打印渠道创建和管理模板：

* [使用Forms Designer创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [将XDP模板上传到AEM Forms服务器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [为布局片段创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer创建XDP模板 {#create-xdp-template-using-forms-designer}

基于 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖学](/help/forms/using/planning-interactive-communications.md)，在XDP模板中创建以下子表单：

* 帐单详细信息：包括文档片段
* 客户详细信息：包括文档片段
* 帐单汇总：包括文档片段
* 摘要：包括文档片段（费用子表单）和图表（图表子表单）
* 明细调用：包括表（布局片段）
* 立即付款：包括图像
* 增值服务：包括图像

![create_print_template](assets/create_print_template.gif)

将XDP文件上传到Forms服务器后，这些子表单会在打印模板中显示为目标区域。 创建交互式通信时，所有实体（如文档片段、图表、布局片段和图像）都会添加到目标区域。

执行以下步骤为打印渠道创建XDP模板：

1. 打开Forms Designer，选择 **文件** > **新建** > **使用空白表单，** 点按 **下一个**，然后点按 **完成** 打开模板创建表单。

   确保 **对象库** 和 **对象** 选项 **窗口** 菜单。

1. 拖放 **子表单** 组件 **对象库** 到表单。
1. 选择子表单以在 **对象** 窗口。
1. 选择 **子表单** 选项卡，选择 **流** 从 **内容** 下拉列表。 拖动子表单的左端点以调整长度。
1. 在 **绑定** 选项卡：

   1. 指定 **帐单详细信息** 在 **名称** 字段。

   1. 选择 **无数据绑定** 从 **数据绑定** 下拉列表。

   ![Designer子表单](assets/forms_designer_subform_new.png)

1. 同样，选择根子表单，选择 **子表单** ，然后选择 **流** 从 **内容** 下拉列表。 在 **绑定** 选项卡：

   1. 指定 **电信账单** 在 **名称** 字段。

   1. 选择 **无数据绑定** 从 **数据绑定** 下拉列表。

   ![打印模板的子表单](assets/root_subform_print_template_new.png)

1. 重复步骤2 - 5以创建以下子表单：

   * 帐单详细信息
   * 客户详细信息
   * 帐单摘要
   * 摘要 — 选择 **子表单** 选项卡，选择 **已定位** 从 **内容** 下拉列表。 在 **概要** 子窗体。

      * 费用
      * 图表
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   为了节省时间，您还可以复制并粘贴现有子表单以创建新子表单。

   要将 **图表** 在“费用”子表单的右侧选择 **图表** 从左窗格中，选择 **布局** 选项卡，并为 **AnchorX** 字段。 的值必须大于 **宽度** 字段 **费用** 子窗体。 选择 **费用** 子窗体并选择 **布局** 选项卡来查看 **宽度** 字段。

1. 拖放 **文本** 对象 **对象库** 输入 **拨打XXXX订阅** 的双曲余切值。
1. 右键单击左窗格中的文本对象，选择 **重命名对象**，并输入文本对象的名称( **订阅**.

   ![XDP模板](assets/print_xdp_template_subform_new.png)

1. 选择 **文件** > **另存为** 要在本地文件系统上保存文件，请执行以下操作：

   1. 导航到要保存文件的位置，并将名称指定为 **create_first_ic_print_template**.
   1. 选择 **.xdp** 从 **另存为类型** 下拉列表。

   1. 点按&#x200B;**保存**。

### 将XDP模板上传到AEM Forms服务器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer创建XDP模板后，必须将其上传到AEM Forms服务器，以便该模板在创建交互式通信时可供使用。

1. 选择 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 点按 **创建** > **文件上传**.

   导航并选择 **create_first_ic_print_template** 模板(XDP)并点按 **打开** 将XDP模板导入AEM Forms服务器。

### 为布局片段创建XDP模板 {#create-xdp-template-for-layout-fragments}

要为交互式通信的打印渠道创建布局片段，请使用Forms Designer创建XDP，并将其上传到AEM Forms服务器。

1. 打开Forms Designer，选择 **文件** > **新建** > **使用空白表单，** 点按 **下一个**，然后点按 **完成** 打开模板创建表单。

   确保 **对象库** 和 **对象** 选项 **窗口** 菜单。

1. 拖放 **表** 组件 **对象库** 到表单。
1. 在插入表对话框中：

   1. 将列数指定为 **5**.
   1. 将主体行数指定为 **1**.
   1. 选择 **在表中包含标题行** 复选框。
   1. 选项卡 **确定**.

1. 点按 **+** 在左窗格中 **表** 1并右键单击 **单元格1** 选择 **重命名对象** to **日期**.

   同样，重命名 **Cell2**, **Cell3**, **Cell4**&#x200B;和 **单元格5** to **时间**, **数值**, **持续时间**&#x200B;和 **费用** 分别进行。

1. 单击 **设计器视图** 将其重命名为 **时间**, **数值**, **持续时间**&#x200B;和 **费用**.

   ![布局片段](assets/layout_fragment_print_new.png)

1. 选择 **行1** 从左窗格中选择 **对象** > **绑定** > **每个数据项的重复行**.

   ![布局片段的重复属性](assets/layout_fragment_print_repeat_new.png)

1. 拖放 **文本字段** 组件 **对象库** 到 **设计器视图**.

   ![布局片段的文本字段](assets/layout_fragment_print_text_field_new.png)

   同样，拖放 **文本字段** 组件 **时间**, **数值**, **持续时间**&#x200B;和 **费用** 行。

1. 选择 **文件** > **另存为** 要在本地文件系统上保存文件，请执行以下操作：

   1. 导航到要保存文件的位置，并将名称指定为 **table_lf**.
   1. 选择 **.xdp** 从 **另存为类型** 下拉列表。

   1. 点按&#x200B;**保存**。
   使用Forms Designer为布局片段创建XDP模板后，您必须 [上传](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) 会发送到AEM Forms服务器，以便模板可在创建布局片段时使用。

## 为Web渠道创建模板 {#create-template-for-web-channel}

使用以下任务为交互式通信的Web渠道创建和管理模板：

* [为模板创建文件夹](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [创建模板](../../forms/using/create-templates-print-web.md#create-the-template)
* [启用模板](../../forms/using/create-templates-print-web.md#enable-the-template)
* [在交互式通信中启用按钮](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 为模板创建文件夹 {#create-folder-for-templates}

要创建Web渠道模板，请定义一个文件夹，以保存创建的模板。 在该文件夹中创建模板后，启用该模板，以允许表单用户基于模板创建交互式通信的Web渠道。

执行以下步骤为可编辑的模板创建文件夹：

1. 点按 **工具** ![锤子图标](assets/hammer-icon.svg) > **配置浏览器**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档以了解更多信息。
1. 在配置浏览器页面中，点按 **创建**.
1. 在 **创建配置** 对话框，指定 **Create_First_IC_templates** 作为文件夹的标题，请检查 **可编辑的模板**，然后点按 **创建**.

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   的 **Create_First_IC_templates** 文件夹已创建并列在 **配置浏览器** 页面。

### 创建模板 {#create-the-template}

基于 [用例](/help/forms/using/create-your-first-interactive-communication.md) 和 [解剖学](/help/forms/using/planning-interactive-communications.md)，在Web模板中创建以下面板：

* 帐单详细信息：包括文档片段
* 客户详细信息：包括文档片段
* 帐单汇总：包括文档片段
* 费用汇总：包括文档片段和图表（双列布局）
* 明细调用：包括表
* 立即付款：包括 **立即付款** 按钮和图像
* 增值服务：包括图像和 **订阅** 按钮。

![create_web_template](assets/create_web_template.gif)

创建交互式通信时，会添加所有实体，如文档片段、图表、表、图像和按钮。

执行以下步骤以在 **Create_First_IC_templates** 文件夹：

1. 通过选择 **工具** > **模板** > **Create_First_IC_templates** 文件夹。
1. 点按&#x200B;**创建**。
1. 在 **选取模板类型** 配置向导，选择 **交互式通信 — Web渠道** 点按 **下一个**.
1. 在 **模板详细信息** 配置向导，指定 **Create_First_IC_Web_Template** 作为模板标题。 指定可选描述并点按 **创建**.

   确认消息显示 **Create_First_IC_Web_Template** 中。

1. 点按 **打开** 以在模板编辑器中打开模板。
1. 选择 **初始内容** 从 **预览** 选项。

   ![模板编辑器](assets/template_editor_initial_content_new.png)

1. 点按 **根面板** 然后点按 **+** 查看可添加到模板的组件列表。
1. 选择 **面板** ，以在 **根面板**.
1. 选择 **内容** 选项卡。 步骤8中添加的新面板将显示在 **根面板** 在内容树中。

   ![内容树](assets/content_tree_root_panel_new.png)

1. 选择面板并点按 ![configure_icon](assets/configure_icon.png) （配置）。
1. 在属性窗格中：

   1. 指定 **计费详细信息** （在“名称”字段中）。
   1. 指定 **帐单详细信息** 字段中。
   1. 选择 **1** 从 **列数** 下拉列表。

   1. 点按 ![](/help/forms/using/assets/done_icon.png) 以保存属性。

   面板的名称会更新为 **帐单详细信息** 在内容树中。

1. 重复步骤7 - 11，向模板添加具有以下属性的面板：

   | 名称 | 标题 | 列数 |
   |---|---|---|
   | customerdetails | 客户详细信息 | 1 |
   | 计费摘要 | 帐单汇总 | 1 |
   | 汇总费用 | 费用汇总 | 2 |
   | itemisedcalls | 明细调用 | 1 |
   | paynow | 立即付款 | 2 |
   | vas | 增值服务 | 1 |

   下图描述了向模板添加所有面板后的内容树：

   ![所有面板的内容树](assets/content_tree_all_panels_new.png)

### 启用模板 {#enable-the-template}

创建Web模板后，必须启用该模板才能在创建交互式通信时使用该模板。

执行以下步骤以启用Web模板：

1. 点按 **工具** ![锤子图标](assets/hammer-icon.svg) > **模板**.
1. 导航到 **Create_First_IC_Web_Template** 模板，选择它，然后点按 **启用**.
1. 选项卡 **启用** 再次确认。

   模板已启用，其状态显示为“已启用”。 在为Web渠道创建交互式通信时，可以使用此模板。

### 在交互式通信中启用按钮 {#enabling-buttons-in-interactive-communications}

根据用例，您必须包含 **立即付款** 和 **订阅** 交互式通信中的按钮（自适应表单组件）。 要在交互式通信中启用这些按钮，请执行以下步骤：

1. 选择 **结构** 从 **预览** 选项。
1. 选择 **文档容器** 使用内容树的根面板并点按 **策略** ，以选择允许在交互式通信中使用的组件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在 **允许的组件** 选项卡 **属性** 选择 **按钮** 从 **自适应表单** 组件。

   ![允许的组件](assets/allowed_components_af_new.png)

1. 点按 ![done_icon](assets/done_icon.png) 以保存属性。
