---
title: 创建通信
seo-title: 创建通信
description: 创建信件模板后，可以使用该模板在AEM Forms中通过管理数据、内容和附件来创建通信。
seo-description: 创建信件模板后，可以使用该模板在AEM Forms中通过管理数据、内容和附件来创建通信。
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: 通信管理
exl-id: da966787-a3b9-420f-8b7c-f00d05c61d43
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3722'
ht-degree: 0%

---

# 创建通信{#create-correspondence}

## 在创建通信用户界面{#create-correspondence-in-the-create-correspondence-user-interface}中创建通信

在通信管理](../../forms/using/create-letter.md)中创建[信件模板后，最终用户/代理/声明调整器可以在“创建通信”用户界面中打开信件，并通过输入数据、设置内容和管理附件来创建通信。 最后，理赔员或代理人可以在预览模式下管理内容并提交信件。

### 预览通信{#preview-a-correspondence}

使用以下步骤选择要预览的信件：

1. 在“信件”页面上，点按&#x200B;**选择**。
1. 点按相应的信件以选择相应的信件。

   ![选择信件](assets/1_selectletter.png)

   选择信件

1. 对于基于数据字典的信件，请选择&#x200B;**预览** > **预览**。 或者，对于不基于数据字典的信件，选择&#x200B;**预览**。 您还可以将鼠标悬停在信件上（未选择该信件），然后点按信件预览图标以预览该信件。

   >[!NOTE]
   >
   >如果数据字典与信件未关联，则会打开信件预览。 否则，如果信件基于数据字典，则“通信管理”会在“预览”菜单中显示“预览”和“自定义”选项，您可以选择两个选项之一。 您还可以将测试数据与数据字典相关联。 当[数据字典具有关联的测试数据](../../forms/using/data-dictionary.md#p-working-with-test-data-p)时，在选择预览选项时，将打开常规预览，并填充测试数据。

1. 要在预览通信时渲染通信，您应是管理员或以下任一组的成员：

   * 表单用户（在创作实例上预览）
   * cm-agent-users（用于发布实例上的演绎版）

   如果您没有所需的权限，请请求管理员获得相应的访问权限。 有关创建用户并将其添加到群组的更多信息，请参阅[将用户或群组添加到群组](/help/sites-administering/security.md)。 如果您尝试在没有相应权限的情况下渲染通信，则会显示404错误页面。

1. 如果已选择&#x200B;**预览** > **自定义**，则会打开一个对话框。 在对话框中，选择与数据字典对应的数据文件以预览字母，然后选择&#x200B;**预览**。 根据特定信件的数据字典创建数据文件。 有关数据文件的更多信息，请参阅[数据字典](../../forms/using/data-dictionary.md#p-working-with-test-data-p)。

   ![预览信件](assets/8_previewcustomdatafile.png)

1. 默认情况下，将打开信件HTML预览（移动设备表单预览），其中焦点是“数据”选项卡。

   有关移动设备表单及其支持的功能的更多信息，请参阅[Mobile Forms与PDF forms之间的功能区别](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html)。

   有三个选项卡：数据、内容和附件。 如果没有数据元素（占位符变量和布局字段），则在中直接打开信件，并显示“内容”选项卡。 仅当存在附件或启用了库访问时，“附件”选项卡才可用。

   >[!NOTE]
   >
   >有关在信件预览的HTML或PDF呈现模式之间切换的更多信息，请参阅[更改信件](#changerenditionmode)的呈现模式。 有关通信管理和AEM中PDF支持的更多信息，请参阅[停止NPAPI浏览器插件及其影响](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)和[对HTML5 Forms的PDF forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html)。

### 输入数据 {#enterdata}

在“数据”选项卡中，填充可用的布局字段和占位符。

1. 根据需要在字段中输入数据和内容变量。 填写所有标有星号(*)的必填字段，以启用&#x200B;**Submit**&#x200B;按钮。

   点按HTML信件预览中的数据字段值，以在“数据”选项卡中突出显示相应的数据字段。

   ![在信件](assets/2_enterdata.png) ![2_1_enterdata中输入数据](assets/2_1_enterdata.png)

### 管理内容 {#managecontent}

在内容选项卡中，管理信件中的内容，如文档片段和内容变量。

1. 选择&#x200B;**内容**。 通信管理显示信件的内容选项卡。

   ![“内容”选项卡 — 突出显示内容中的模块](assets/3_content.png)

1. 根据需要，在内容选项卡中编辑内容模块。 要集中查看内容层次结构中的相关内容模块，您可以点按信件预览中的相关行或段落，也可以直接点按内容层次结构中的内容模块。

   例如，在下图中选择了“我们已审阅……”一行，并在“内容”选项卡中选择了相关的内容模块。

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   在“内容”或“数据”选项卡中，通过点按HTML信件预览左上角的高亮显示选定模块(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，可以禁用或启用在信件预览中选择相关文本、段落或数据字段时转到内容/数据模块的功能。

   有关“创建通信”用户界面中各个模块可用的操作的更多信息，请参阅“创建通信”用户界面](#actions-and-info-available-in-the-create-correspondence-content-tab)中的[操作和信息。

1. 要查找内容模块，请使用“查找”字段。 输入内容模块的完整或部分名称或标题，以在通信中搜索内容模块。
1. 点按列表、文本、条件或目标区域前面的显示图标(![display](assets/display.png))，以在信件中显示或隐藏该图标。
1. 要编辑内嵌或可编辑的文本模块，请点按相关的&#x200B;**编辑**&#x200B;图标(![edittextmodule](assets/edittextmodule.png))，或在信件预览中双击相关文本模块。

   系统会显示文本编辑器以编辑文本并设置其格式。

   浏览器中的默认拼写检查程序在文本编辑器中检查拼写。 要管理拼写和语法检查，您可以编辑浏览器的拼写检查设置或安装浏览器插件/插件以检查拼写和语法。

   您还可以使用文本编辑器中的各种键盘快捷键来管理、编辑和设置文本格式。 有关“通信管理键盘快捷键”中[文本编辑器](/help/forms/using/keyboard-shortcuts.md#correspondence-management)键盘快捷键的详细信息。

   ![5_edittextmodule](assets/5_edittextmodule.png)

   您可能希望重复使用另一个文档应用程序中存在的多个文本段落之一。 您可以直接复制并粘贴文本，例如从MS Word、HTML页面或任何其他应用程序复制和粘贴文本。

   您可以在可编辑的文本模块中复制并粘贴一个或多个文本段落。 例如，您可能有一个MS Word文档，其中包含可接受居住证明的项目符号列表，如下所示：

   ![pastetextword](assets/pastetextmsword.png)

   您可以直接将MS Word文档中的文本复制并粘贴到可编辑的文本模块中。 文本模块中会保留格式（如项目符号列表、字体和文本颜色）。

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >但是，粘贴文本的格式存在一些[限制](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html)。

   您可以使用Tab键缩进信件中的文本和数字。 例如，可以使用Tab键将列表中的多列文本对齐为表格格式。

   ![tabspaces](assets/tabspaces.png)

   示例：使用Tab键将多列文本对齐为表格格式

   >[!NOTE]
   >
   >有关为文本模块和字母设置制表符间距的详细信息，请参阅[有关使用制表符间距排列文本的详细信息](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)。

1. 如果需要，在通信中插入特殊字符。 例如，您可以使用“特殊字符”面板插入：

   * 货币符号，如€、¥和£
   * 数学符号，如∑、√、∂和^
   * 标点符号，如&quot;和&quot;

   ![特殊字符](assets/specialcharacters.png)

   通信管理内置了210个特殊字符。 管理员可以通过自定义](../../forms/using/custom-special-characters.md)添加对更多/自定义特殊字符的支持。[

1. 要在可编辑的内嵌模块中突出显示\强调部分文本，请选择该文本，然后点按“高亮显示颜色”。

   ![背景颜色](assets/letterbackgroundcolor.png)

   您可以直接点按“基本颜色”调板中存在的基本颜色`**[A]**`，或使用滑块`**[B]**`后点按&#x200B;**选择**&#x200B;以选择相应的颜色阴影。

   或者，您也可以转到“高级”选项卡以选择适当的“色相”、“明度”和“饱和度” `**[C]**`以创建精确颜色，然后点按“选择`**[D]**`”以应用颜色以突出显示文本。

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. 进行适当的内容和格式更改，然后点按&#x200B;**保存**。 点按(![editnextmoduleccr](assets/editnextmoduleccr.png))以在可编辑的文本模块之间移动，或点按&#x200B;**保存并下一步**&#x200B;以保存更改并移至下一个可编辑的文本模块。
1. 系统还会显示每个分支的未填充变量。 当没有未填充的变量时，未填充的变量将显示为0。 如果存在未填充的变量，您可以点按分支以展开该变量，然后找到未填充的变量。 使用内容工具栏可删除内容、增加/减少内容缩进，以及在内容之前/之后插入分页符。

   您可以在数据模块的上方和下方插入分页符，即使这些分页符是列表和条件的一部分也是如此。

1. 点按打开/关闭内容变量(![opencontentvariables](assets/opencontentvariables.png))以打开内容变量并相应地填充它们。
1. 正确填充未填充的变量后，未填充变量的计数将设置为0。

   在“创建通信”用户界面中，未填充的变量计数显示在任何包含至少一个变量的模块层次结构的每个级别。 如果模块包含未填充的变量，则计数将显示在变量、模块、目标区域和信件模板级别。

   未填充的变量计数包括：

   * 仅不受保护的数据字典和占位符变量。 变量计数不包括布局或受保护的数据字典变量。
   * 必填字段。
   * 布局字段（如果为必填字段），且已绑定到用户。
   * 仅独特变量实例。 如果模块、目标区域或信件模板包含同一变量的两个或多个实例，则计数将显示为1(1)。 但是，对于每个实例，计数显示为1。

   未填充的变量计数不包括已取消选择的模块。 如果某个模块包含在信件模板中，但不在信件中，则不会显示此模块中未填充变量的计数。

   对于目标区域、模块和变量，计数显示在信件模板中每个对象的右侧。 但是，对于完整模板，计数显示在创建通信状态栏中。

   信件模板中的模块显示未填充的变量计数，如下所述：

   * **** 文本显示文本模块中包含的唯一未填充占位符变量和数据字典元素的总和。
   * **** 条件显示条件中包含的唯一未填充条件变量和结果模块中包含的变量的总和。
   * **** 列表显示分配给列表的模块中包含的所有唯一未填充变量的总和。
   * **目标** 区域显示分配给目标区域的模块中包含的所有唯一未填充变量的总和。

   请注意以下有关具有默认值的变量的信息：

   * 布尔变量字段默认为&#x200B;*false*。 但是，该变量会被视为未填充。 这意味着变量计数包含值&#x200B;*false*&#x200B;的所有布尔变量字段。

   * 数值变量字段默认为&#x200B;*0（零）*。 但是，该变量会被视为未填充。 这意味着变量计数包含值&#x200B;*0（零）*&#x200B;的所有数字变量字段。



#### “创建通信内容”选项卡{#actions-and-info-available-in-the-create-correspondence-content-tab}中可用的操作和信息

**目标区域**

* 插入空行：插入新的空行。
* 插入内联文本：插入新文本模块。
* 订单锁定（信息）：表示内容的顺序无法更改。
* 未填充的值（信息）：指示目标区域中未填充变量的数量。

**模块**

* 选择（眼睛图标）：包含\排除信件中的模块。
* 跳过项目符号（适用于列表模块及其子模块）：跳过特定模块中的项目符号。
* 之前的分页符（适用于目标区域的子模块）：在模块之前插入分页符。
* 之后的分页符（适用于目标区域的子模块）：在模块之前插入分页符。
* 未填充的值（信息）：指示目标区域中未填充变量的数量。
* 编辑（仅限文本模块）：打开富文本编辑器以编辑文本模块。
* 数据面板（文本和条件模块）：打开模块的所有变量。

**列表模块**

* 插入空行：插入新的空行。
* 内容库：打开内容库以将模块添加到列表。
* 列表设置（仅嵌套列表）：
* 订单锁定（信息）：表示无法更改列表项的顺序。

### 管理附件{#manage-attachments}

1. 选择&#x200B;**附件**。 通信管理按照创建信件模板时的设置显示可用附件。
1. 您可以通过点按视图图标，选择不随信件一起提交附件，然后点按附件中的十字，以将其从信件中删除。 对于指定的附件，在创建信件模板时，视图和删除图标将作为“必填”禁用。
1. 点按库访问（![库访问](assets/libraryaccess.png)）图标以访问内容库，以将DAM资产作为附件插入。

   >[!NOTE]
   >
   >“库访问”图标仅在创作信件时启用库访问。

1. 如果在创建通信时附件的顺序未锁定，则可以通过选择附件并点按向下和向上箭头来重新排序附件。

   有关更多信息，请参阅[附件投放](#attachmentdelivery)。

### 在预览中管理内容并提交信件{#manage-content-in-preview-and-submit-the-letter}

您可以进行布局和内容相关更改，以确保信件按您预期的方式显示并提交到各种帖子流程。

1. 要突出显示信件中的所有可编辑内容，请点按&#x200B;**突出显示可编辑的部分**。

   信件的可编辑内容以灰色背景突出显示。

   ![突出显示可编辑的内容](assets/4_highlightmoduleincontent-1.png)

1. 根据需要，在内容选项卡中编辑内容模块。 要集中查看内容层次结构中的相关内容模块，您可以点按信件预览中的相关行或段落，也可以直接点按内容层次结构中的内容模块。

   例如，行“允许我们访问……” 将在下图中进行选择，并在“内容”选项卡中选择相应的内容模块。

   通过点按内容中的突出显示选定模块(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以禁用或启用在信件预览中点按相关文本、段落或数据字段时在“内容”选项卡中突出显示内容模块的功能。

   有关“创建通信”用户界面中各个模块可用的操作的更多信息，请参阅“创建通信”用户界面](#actions-and-info-available-in-the-create-correspondence-content-tab)中的[操作和信息。

1. 要向信件中添加分页符，请点按要插入分页符的位置，然后选择此分页符之前或之后分页符(![pagebreakbeforeafter](assets/pagebreakbeforeafter.png))。

   在信件中插入显式分页符占位符。 要查看显式分页符对信件的影响，请参阅扁平化PDF预览。

   >[!NOTE]
   >
   >由于移动设备表单不支持分页，因此页眉和页脚只显示一次。 但是，您可以在布局（每页）中显式设置页眉和页脚，以在移动设备表单预览中显示。 此外，信件中的空白页面（如果有）不会显示在移动设备表单预览中。

   ![显式分页符](assets/8_pagebreak.png)

1. 要将信件另存为草稿（稍后可继续处理），请点按另存为草稿。 要使用此选项，您的信件必须是[published](../../forms/using/publishing-unpublishing-forms.md#publishanasset)。 有关更多信息，请参阅[保存草稿并提交信件实例](#savingdrafts)下的草稿实例。

   ![saveasdraft](assets/saveasdraft.png)

   将出现“起草信件名称”对话框，其中包含信件实例ID。 您可以选择编辑此ID。 记下信件ID，然后点按&#x200B;**Done**。 您稍后可以使用此ID来[重新加载草稿字母](submit-letter-topostprocess.md#reloaddraft)。

1. 要以扁平化PDF形式预览信件，并在提交信件时使用确切的布局和分页符，请点按(![preview](assets/preview.png))预览。

   信件显示为扁平的PDF。 扁平化PDF是信件的精确表示形式，因为它将使用正确的字体、断点和信件布局提交。

   >[!NOTE]
   >
   >如果您使用的是Mozilla Firefox和HTML呈现版本类型，则要将信件预览为扁平PDF，请确保您使用本机浏览器插件，而不是Acrobat插件。 要选择本机浏览器插件，请转到Mozilla Firefox的设置，然后对于内容类型PDF，选择在Firefox中预览。

1. 如果您发现扁平化PDF预览令人满意，请点按&#x200B;**Submit**&#x200B;以提交信件。 或者，要更改信件，请点按&#x200B;**退出预览**，以返回信件的创建通信UI预览，以更改信件。 点按提交后，如果发布实例上启用了管理信件实例配置，则会生成提交信件实例。

   有关更多信息，请参阅保存草稿和提交信件实例下的草稿实例。

   您还可以将信件另存为草稿，以便稍后更改信件。

   进行所需更改后，您可以从HTML5预览提交信件，或再次点按预览以查看扁平化PDF输出。

   有关HTML5表单与PDF forms之间差异的信息，请参阅[HTML5表单与PDF forms之间的功能区别](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md)。

## 保存草稿并提交信件实例 {#savingdrafts}

在创建通信用户界面中呈现信件后，您可以将该信件保存为已查看。

可以保存两种类型的信件实例：草稿实例和提交实例。

* **草稿实例**:草稿实例会捕获您正在预览的信件的当前状态。要保存草稿实例，请首先确保信件和信件引用的所有资产处于“已发布”状态。 有关发布信件的信息，请参阅[发布资产](../../forms/using/publishing-unpublishing-forms.md#publishanasset)。 您需要先发布信件，然后才能将其另存为草稿，因为当您发布信件时，会创建该信件、其从属资产和数据的版本。 信件的已发布版本无法由您或其他用户编辑，并且以后可以恢复，而不会与已发布版本出现任何意外差异。 您稍后可以返回到此实例，并从您离开的位置继续操作。

* **提交实例**:提交实例会在提交时捕获信件的状态。在处理信件实例后，提交实例会存储该信件实例的PDF状态以及用户在创建通信用户界面中输入的数据。

只有在发布实例上查看信件时，才能保存此类实例。 默认情况下，“保存实例”处于关闭状态。 要启用信件实例的保存，请执行以下步骤。

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr
1. 找到&#x200B;**[!UICONTROL 通信管理配置]**&#x200B;并单击它。
1. 选中&#x200B;**[!UICONTROL 管理Publish]**&#x200B;配置上的信件实例，然后单击&#x200B;**[!UICONTROL 保存]**。

打开信件实例的保存时，您可以选择在何处保存信件实例。 保存信件实例有两个选项：本地保存或远程保存。

### 本地保存{#local-save}

信件实例保存在发布实例上，并在创作实例上反向复制。

### 远程保存{#remote-save}

如果用户担心在发布实例上保存用户数据，则他们可以使用此选项，通常情况下，该选项会位于公司防火墙之外。 打开远程保存后，信件实例不会保存在发布实例上，而是会在通过LiveCycle客户端SDK配置指定的处理作者上远程保存。

#### 启用远程保存{#enable-remote-save}

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：`https://<server>:<port>/<contextpath>/system/console/configMgr`
1. 搜索&#x200B;**[!UICONTROL 通信管理配置]**&#x200B;并单击它。
1. 找到&#x200B;**[!UICONTROL 远程保存]**&#x200B;配置，检查该配置，然后单击&#x200B;**[!UICONTROL 保存]**。

#### 指定处理创作设置{#specify-processing-author-settings}

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：`https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Adobe Experience Manager Web控制台配置](assets/2configmanager.png)

1. 在此页面中，找到AdobeLiveCycle客户端SDK配置，并单击以将其展开。

1. 在处理服务器URL中，输入LiveCycle服务器的名称，提供登录信息，然后单击&#x200B;**Save**。

   ![输入LiveCycle服务器的名称和登录信息](assets/3configmanager.png)

1. 如有必要，请设置您要用来访问服务器的用户名和密码。

#### 附件投放 {#attachmentdelivery}

* 信件附件在PDF中是可用的后处理，该PDF在提交信件后创建。
* 当使用服务器端API作为交互式或非交互式PDF呈现信件时，呈现的PDF包含作为PDF附件的附件。
* 当使用“创建通信”用户界面将与信件模板关联的后处理作为“提交”或“完成通信”操作的一部分加载时，附件将作为AttachmentDocs参数中的List&lt;com.adobe.idp.Document>传递。
* 即装即用的投放机制（如电子邮件和打印）也会发送附件以及生成的通信的PDF。

## 信件预览的呈现模式：移动设备表单预览和PDF预览{#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms通信管理在创建通信UI中将信件显示为HTML。 但是，通信管理仍支持还原到PDF预览，而不是HTML预览。 有关在HTML和PDF预览模式之间切换的更多信息，请参阅[更改字母](#changerenditionmode)的呈现模式。

以下是HTML和PDF预览版中提供的优势和功能。

**移动表单/HTML预览的好处**

* **点按数据字段值以高亮显示相应的数据字段**:在创建通信用户界面中，您可以点按信件中的数据字段值，以在数据选项卡中突出显示相应的数据字段。有关更多信息，请参阅[输入数据](#enterdata)。

* **浏览器支持**:浏览器逐渐取消对NPAPI的支持，这会影响信件的PDF预览。信件的HTML/移动表单预览不受此影响。
* **突出显示信件中的可编辑内容**:在“创建通信”用户界面中，您可以点按高亮显示可编辑内容，以灰色突出显示信件中的所有可编辑内容。有关更多信息，请参阅[管理内容](#managecontent)。

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **PDF预览的好处**

* **分页符**:在PDF预览中，您可以准确查看信件中的分页对其输出的影响。
* **最终预览**:在PDF预览中，您可以查看信件在其输出中显示的确切格式和外观。

有关PDF forms中脚本支持的信息，请参阅[脚本支持](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html)。

有关HTML5表单中脚本支持的更多信息，请参阅[HTML5表单脚本支持](/help/forms/using/scripting-support.md)。

### 更改信件的呈现模式 {#changerenditionmode}

默认情况下，创建通信UI使用HTML或移动表单来渲染信件预览。 移动设备表单预览在任何浏览器中呈现时均无问题，因为它使用浏览器的本机插件，并且不需要任何其他插件。 您可以将信件预览模式更改为PDF。 但是，浏览器限制可能会为信件的交互式PDF预览的不同功能产生问题。

有关与信件预览兼容的浏览器的更多信息，请参阅[停止使用NPAPI浏览器插件及其影响](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)。

要更改信件的预览模式，请完成以下步骤：

1. 转到`https://[system]:'port'/system/console/configMgr`，并根据需要以管理员身份登录。
1. 转到&#x200B;**[!UICONTROL 通信管理配置]** > **[!UICONTROL 演绎版类型]**&#x200B;并选择&#x200B;**HTML演绎版**（默认）或&#x200B;**PDF演绎版**。
1. 单击&#x200B;**[!UICONTROL 保存]**。
