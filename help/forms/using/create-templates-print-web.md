---
title: “教程：创建模板”
seo-title: 为交互式通信创建打印和Web模板
description: 为交互式通信创建打印和Web模板
seo-description: 为交互式通信创建打印和Web模板
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 教程：创建模板{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

本教程是创建您的第一个交 [互式通信系列中的一个步骤](/help/forms/using/create-your-first-interactive-communication.md) 。 建议按照时间顺序按照这一系列来了解、执行和演示完整的教程用例。

要创建交互式通信，您必须在AEM服务器上提供用于打印和Web渠道的模板。

打印渠道的模板在Adobe Forms Designer中创建并上传到AEM服务器。 然后，这些模板可在创建交互式通信时使用。

Web渠道的模板是在AEM中创建的。 模板作者和管理员可以创建、编辑和启用Web模板。 创建并启用这些模板后，即可在创建交互式通信时使用。

本教程将指导您逐步创建用于印刷和Web渠道的模板，以便在创建交互式通信时使用这些模板。 在本教程的结尾，您将能够：

* 使用Adobe Forms Designer创建用于印刷渠道的XDP模板
* 将XDP模板上传到AEM Forms Server
* 创建和启用Web渠道的模板

## 为打印渠道创建模板 {#create-template-for-print-channel}

使用以下渠道创建和管理交互式通信的打印任务的模板：

* [使用Forms Designer创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [将XDP模板上传到AEM Forms服务器](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [为布局片段创建XDP模板](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### 使用Forms Designer创建XDP模板 {#create-xdp-template-using-forms-designer}

根据用例 [和解剖结](/help/forms/using/create-your-first-interactive-communication.md) 构 [](/help/forms/using/planning-interactive-communications.md)，在XDP模板中创建以下子表单：

* 帐单详细信息：包括文档片段
* 客户详细信息：包括文档片段
* 帐单汇总：包括文档片段
* 摘要：包括文档片段（Charges子表单）和图表（Charts子表单）
* 分项调用：包括表（布局片段）
* 立即付款：包括图像
* 增值服务：包括图像

![create_print_template](assets/create_print_template.gif)

在将XDP文件上传到Forms服务器后，这些子表单在“打印”模板中显示为目标区域。 创建交互式通信时，所有实体(如文档片段、图表、布局片段和图像)都会添加到目标区域。

执行以下步骤以为打印渠道创建XDP模板：

1. 打开表单设计器，选择“文 **件** ”>“新建 **”>** 使用空白表单，点按下一个表单，然后点 ************ 按NextFinish（下一个完成），打开表单以创建模板。

   确保从“窗 **口”菜单中选** 择 **“对象库** ”和 **“对象** ”选项。

1. 将子表单组件从 **对象库** 拖 **放到表单中** 。
1. 选择子表单，在右侧窗格的“对象”窗口中显 **示子表** 单的选项。
1. 选择“ **子表单** ”选项卡，然后从“内容 **”下拉** 列表中选择 **“** 已排列”。 拖动子表单的左端点以调整长度。
1. 在“绑 **定** ”选项卡中：

   1. 在“名 **称** ”字段中指 **定BillDetails** 。

   1. 从“ **数据绑定** ”下拉 **列表中选择“无数据绑定** ”。
   ![设计人员子表单](assets/forms_designer_subform_new.png)

1. 同样，选择根子表单，选择 **子表单** ，然后从“内容 **”下拉列表中选** 择“流过 **** ”。 在“绑 **定** ”选项卡中：

   1. 在“ **名称** ”字段中指 **定TelecaBill** 。

   1. 从“ **数据绑定** ”下拉 **列表中选择“无数据绑定** ”。
   ![用于打印模板的子表单](assets/root_subform_print_template_new.png)

1. 重复步骤2 - 5以创建以下子表单：

   * BillDetails
   * 客户详细信息
   * BillSummary
   * 摘要——选择子表 **单选项卡** ，然后从此子表单的“内容 **”下拉列表中选****** 择“已定位”。 在“摘要”子表单中插 **入以** 下子表单。

      * 费用
      * 图表
   * ItemisedCalls
   * PayNow
   * ValueAddedServices
   为节省时间，您还可以复制并粘贴现有子表单以创建新子表单。

   要将 **Charts** 子表单移到Charges子表单的右侧，请从左侧窗格中选择 **Charts** 子表单，选择 **Layout选项卡，然后为****** AnchorXField指定一个值。 该值必须大于Charges子表单的 **Width** 字段 **的值** 。 选择“ **Charges** ”子表单，然后选择“ **Layout** ”选项卡以视图“ **Width** ”字段的值。

1. 将 **Text** 对象从对象库拖放到表单中，然后在框中输入 **Dial XXXX以订阅文本****** 。
1. 右键单击左窗格中的文本对象，选择“重命 **名对象**”，然后输入文本对象的名称为“ **订阅”**。

   ![XDP模板](assets/print_xdp_template_subform_new.png)

1. 选择“ **文件** ”>“ **另存为** ”，将文件保存到本地文件系统中：

   1. 导览至保存文件的位置，并指定 **create_first_ic_print_template的名称**。
   1. 从“ **另存为类** 型”下拉列表中选择 **** .xdp。

   1. 点按&#x200B;**保存**。

### 将XDP模板上传到AEM Forms服务器 {#upload-xdp-template-to-the-aem-forms-server}

使用Forms Designer创建XDP模板后，必须将其上传到AEM Forms服务器，以便该模板在创建交互通信时可用。

1. 选择“ **表单** ”>“ **表单和文档”**。
1. 点按 **创建** > **文件上传**。

   导航并选择 **create_first_ic_print_template** template(XDP)，然后点按 **Open** ，将XDP模板导入AEM Forms服务器。

### 为布局片段创建XDP模板 {#create-xdp-template-for-layout-fragments}

要为交互通信的打印渠道创建布局片段，请使用Forms Designer创建XDP，然后将其上传到AEM Forms服务器。

1. 打开表单设计器，选择“文 **件** ”>“新建 **”>** 使用空白表单，点按下一个表单，然后点 ************ 按NextFinish（下一个完成），打开表单以创建模板。

   确保从“窗 **口”菜单中选** 择 **“对象库** ”和 **“对象** ”选项。

1. 将表组件从对 **象库** 拖 **放到表单中** 。
1. 在“插入表”对话框中：

   1. 将列数指定为 **5**。
   1. 将正文行数指定为 **1**。
   1. 选中“ **在表中包含标题行** ”复选框。
   1. 选项卡 **确定**。

1. 点按 **+** (在表 **1旁边的左窗格中)，右键单击“Cell1** ”，然后在“Cell1”中选 **择Object** ，以重命名 ******** DateRename。

   同样，将 **Cell2**、 **Cell3**、Cell3 **、** Cell4和 **Cell Time重命名为TimeCell、Number、CellNumber、CellDember、CellCarges和****************** CellCarges5分别重命名为Cell4、TimellCellCellCellD。

1. 单击设计器视图中的“ **** ”文本字段，并将其重命名为 **Time**、 **Number**、Duration ********、ChargesChargesChargesChargesChargesChargesChargesS。

   ![布局片段](assets/layout_fragment_print_new.png)

1. 从左 **窗格中选择** 1行，然后选择“对 **象** ”>“绑定 **”******>“重复每个数据项”的行。

   ![为布局片段重复属性](assets/layout_fragment_print_repeat_new.png)

1. 将“文本字段”组 **件从“对象库** ”拖 **放到“设** 计器”视图 ****。

   ![布局片段的文本字段](assets/layout_fragment_print_text_field_new.png)

   同样，将“文本字 **段** ”组件拖放到“时间 ****”、“数 **字”、“持续时**&#x200B;间”和“ ******** 收费”行。

1. 选择“ **文件** ”>“ **另存为** ”，将文件保存到本地文件系统中：

   1. 导览至保存文件的位置，并将名称指 **定为table_lf**。
   1. 从“ **另存为类** 型”下拉列表中选择 **** .xdp。

   1. 点按&#x200B;**保存**。
   使用Forms Designer为布局片段创建XDP模板后，必须将其上传 [](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) AEM Forms服务器，以便该模板在创建布局片段时可用。

## 创建Web渠道模板 {#create-template-for-web-channel}

使用以下渠道创建和管理交互式通信的Web任务的模板：

* [为模板创建文件夹](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [创建模板](../../forms/using/create-templates-print-web.md#create-the-template)
* [启用模板](../../forms/using/create-templates-print-web.md#enable-the-template)
* [在交互通信中启用按钮](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### 为模板创建文件夹 {#create-folder-for-templates}

要创建Web渠道模板，请定义一个文件夹，您可以在其中保存创建的模板。 在该文件夹内创建模板后，启用该模板可允许表单用户基于该模板创建交互式通信的Web渠道。

执行以下步骤为可编辑的模板创建文件夹：

1. 点按 **工具** > ![](assets/hammer-icon.svg) 配 **置浏览器**。
1. 在“配置浏览器”页面中，点按 **创建**。
1. 在“创 **建配置** ”对话框中，指定 **Create_First_IC_templates** 作为文件夹的标题，选中“可编辑的模板 **”，然后点按******&#x200B;创建。

   ![配置Web模板](assets/create_first_ic_web_template_new.png)

   将 **创建Create_First_IC_templates文件夹** ，并在“配置浏览器”页 **面上列出** 。

### 创建模板 {#create-the-template}

根据用例 [和解剖结](/help/forms/using/create-your-first-interactive-communication.md) 构 [](/help/forms/using/planning-interactive-communications.md)，在Web模板中创建以下面板：

* 帐单详细信息：包括文档片段
* 客户详细信息：包括文档片段
* 帐单汇总：包括文档片段
* 费用汇总：包括文档片段和图表（双列布局）
* 分项调用：包括表
* 立即付款：包括“立 **即付费** ”按钮和图像
* 增值服务：包括图像和“订 **阅** ”按钮。

![create_web_template](assets/create_web_template.gif)

创建交互式通信时会添加所有实体，如文档片段、图表、表、图像和按钮。

执行以下步骤，在 **Create_First_IC_templates文件夹中为Web渠道创建模板** :

1. 通过选择“工具”>“模板 **”** >“ **Create_First_IC_templates”文件夹，导览至相应的模板文件夹****** 。
1. 点按&#x200B;**创建**。
1. 在“选 **择模板类型** ”配置向导中，选择“ **交互式通信- Web渠道** ”并点按“下 **一步**”。
1. 在“模 **板详细信息** ”配置向导中，指定 **Create_First_IC_Web_Template** 作为模板标题。 指定可选说明，然后点按 **创建**。

   显示 **Create_First_IC_Web_Template的确认消息** 。

1. 点按 **打开** ，以在模板编辑器中打开模板。
1. 从 **列表选项旁的下拉预览中选择初始** 内容 **** 。

   ![模板编辑器](assets/template_editor_initial_content_new.png)

1. 点 **按根面板** ，然后点 **** 按+以视图可添加到模板的组件列表。
1. 从列表 **中选择** “面板”，在“根面板”上方添加 **一个面板**。
1. 选择左 **窗格中** “内容”选项卡。 在第8步中添加的新面板显示在内容树 **的根面板** 下方。

   ![内容树](assets/content_tree_root_panel_new.png)

1. 选择面板，然后点 ![](assets/configure_icon.png) 按（配置）。
1. 在“属性”窗格中：

   1. 在“名 **称** ”字段中指定帐单详细信息。
   1. 在“ **标题** ”字段中指定清单详细信息。
   1. 从 **“列** 数”下拉列表 **中选择** 1。

   1. 点 ![](/help/forms/using/assets/done_icon.png) 按以保存属性。
   面板的名称将更新为内容树 **中的“清单详细信** 息”。

1. 重复第7 - 11步，将具有以下属性的面板添加到模板中：

   | 名称 | 标题 | 列数 |
   |---|---|---|
   | 客户详细信息 | 客户详细信息 | 1 |
   | billsument | 帐单汇总 | 1 |
   | 摘要费用 | 费用汇总 | 2 |
   | itimisedcalls | 分项调用 | 1 |
   | 立即付款 | 立即付款 | 2 |
   | vas | 增值服务 | 1 |

   以下图像描述了将所有面板添加到模板后的内容树：

   ![所有面板的内容树](assets/content_tree_all_panels_new.png)

### 启用模板 {#enable-the-template}

创建Web模板后，您必须启用该模板才能在创建交互式通信时使用该模板。

执行以下步骤以启用Web模板：

1. 点按 **工具** > ![](assets/hammer-icon.svg) 模 **板**。
1. 导航到 **Create_First_IC_Web_Template模板** ，选择它，然后点按启 **用**。
1. 选项卡 **再次启用** ，以进行确认。

   模板已启用，其状态显示为“已启用”。 您可以在创建用于Web渠道的交互式通信时使用此模板。

### 在交互通信中启用按钮 {#enabling-buttons-in-interactive-communications}

根据用例，您必须在交互通信中包 **含“立即支付** ”和“ **订阅** ”按钮（自适应表单组件）。 要在交互通信中启用这些按钮，请执行以下步骤：

1. 从 **列表** 、预览选项旁边的下拉框中选择 **** 。
1. 使用内 **容树选择文档容器根面板，然后点** 按策略 **** ，以选择允许在交互通信中使用的组件。

   ![配置策略](assets/structure_configure_policy_new.png)

1. 在“属性 **”的“允许的组件** ”部分 **中，从“自适应表单组件”** 选项卡中选 ******** 择“按钮”。

   ![允许的组件](assets/allowed_components_af_new.png)

1. 点 ![](assets/done_icon.png) 按以保存属性。