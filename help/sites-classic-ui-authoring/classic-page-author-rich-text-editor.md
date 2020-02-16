---
title: 富文本编辑器
description: 富文本编辑器是将文本内容输入到 AEM 中的基本构建块。
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
translation-type: tm+mt
source-git-commit: 7bf6657a8fd7677ab15e0f91324a065b684e2f92

---


# 富文本编辑器 {#rich-text-editor}

富文本编辑器是将文本内容输入到 AEM 中的基本构建块。它构成各种组件的基础，包括：

* 文本
* 文本图像
* 表

## 富文本编辑器 {#rich-text-editor-1}

所见即所得 (WYSIWYG) 编辑对话框提供各类功能：

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>可为各个项目配置可用功能，因此根据您的安装，这些功能可能有所不同。

## 就地编辑 {#in-place-editing}

除了基于对话框的富文本编辑模式外，AEM 还提供就地编辑模式，当文本在页面布局中显示时，该模式允许直接编辑文本。

单击段落两次（慢速双击）可进入就地编辑模式（组件边框随即变为橙色）。

您将能够直接在页面上编辑文本，而不是在对话框窗口中编辑。只需进行更改即可，系统将自动保存这些更改。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>如果内容查找器处于打开状态，则带有 RTE（富文本编辑器）格式设置选项的工具栏将显示在选项卡顶部（如上图所示）。
>
>如果没有打开内容查找器，则不会显示该工具栏。

现在，为通过&#x200B;**文本**&#x200B;和&#x200B;**标题**&#x200B;组件生成的页面元素启用了就地编辑模式。

>[!NOTE]
>
>[!UICONTROL 标题]组件设计用于包含短文本（没有换行符）。在就地编辑模式中编辑标题时，输入换行符将在标题下方打开一个新&#x200B;**文本**&#x200B;组件。

## 富文本编辑器的功能 {#features-of-the-rich-text-editor}

The Rich Text Editor provides a range of featues, these [depend on the configuration](/help/sites-administering/rich-text-editor.md) of the individual component. The features are available for both the touch-optimized and classic UI.

### 基本字符格式 {#basic-character-formats}

![](do-not-localize/cq55_rte_basicchars.png)

您可在此对您已选的（突出显示的）字符应用格式；一些选项还具有快捷键：

* 粗体 (Ctrl-B)
* 斜体 (Ctrl-I)
* 下划线 (Ctrl-U)
* 下标
* 上标

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

所有都以切换方式运行，因此重新选择将删除格式。

### 预定义样式和格式 {#predefined-styles-and-formats}

![cq55_rte_styles段落](assets/cq55_rte_stylesparagraph.png)

您的安装可以包括预定义的样式和格式。它们随&#x200B;**[!UICONTROL 样式]**&#x200B;和&#x200B;**[!UICONTROL 格式]**&#x200B;下拉列表提供且可应用于您选定的文本。

样式可应用于特定字符串（样式与 CSS 关联）：

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

而格式应用于整个文本段落（格式是基于 HTML 的）：

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

特定格式只能进行更改（默认为&#x200B;**[!UICONTROL 段落]**）。

可以删除样式；将光标放置在已应用样式的文本中并单击删除图标：

>[!CAUTION]
>
>不要实际重新选择任何已应用样式的文本，否则将停用图标。

### 剪切、复制、粘贴 {#cut-copy-paste}

![](do-not-localize/cq55_rte_cutcopypaste.png)

**[!UICONTROL 剪切]**&#x200B;和&#x200B;**[!UICONTROL 复制]**&#x200B;的标准功能可以使用。提供了多种版本的&#x200B;**[!UICONTROL 粘贴]**&#x200B;以满足不同格式的需要。

* 剪切 (Ctrl-X)
* 复制 (Ctrl-C)
* Paste
This is the default paste mechanism (Ctrl-V) for the component; when installed out-of-the-box this is configured to be [!UICONTROL Paste from Word].

* 粘贴为文本：去除所有样式和格式，仅粘贴纯文本。

* 从Word粘贴：这会将内容粘贴为HTML（需要重新设置一些格式）。

### 撤消、重做 {#undo-redo}

![](do-not-localize/cq55_rte_undoredo.png)

AEM 会按时间顺序保留您在当前组件中过去 50 次操作的记录。如有必要，可以按严格顺序撤消（然后恢复）这些操作。

>[!CAUTION]
>
>历史记录仅针对当前编辑会话保留。每次您打开组件进行编辑时，都会重新开始历史记录。

>[!NOTE]
>
>50 次是默认的任务数量。您的安装可以使用不同的值。

### 对齐 {#alignment}

![](do-not-localize/cq55_rte_alignment.png)

您的文本可以左对齐、居中对齐或右对齐。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### 缩进 {#indentation}

![](do-not-localize/cq55_rte_indent.png)

段落缩进可以增大或减小。将缩进所选段落，输入的任何新文本将保留当前的缩进级别。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### 列表 {#lists}

![](do-not-localize/cq55_rte_lists.png)

项目符号列表和编号列表均可在您的文本中进行创建。可选择列表类型并开始键入内容或突出显示要转换的文本。在这两种情况下，换行均将开始新的列表项。

嵌套列表可通过缩进一个或多个列表项实现。

只需将光标置于列表中，然后选择其他样式即可更改列表样式。子列表也可以具有不同于包含列表的样式。在创建子列表（通过缩进）后，即可应用样式。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### 链接 {#links}

![](do-not-localize/cq55_rte_links.png)

通过突出显示所需文本，然后单击超链接图标，可生成指向URL（在网站中或外部位置）的链接：

![](do-not-localize/chlimage_1-9.png)

对话框将允许您指定目标 URL；同样允许指定是否应在新窗口中打开它。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

您可以：

* 直接键入URI
* 使用站点地图在您的网站中选择页面
* Enter the URI, then append the target anchor; e.g. `www.TargetUri.org#AnchorName`
* Enter an anchor only (to reference &quot;the current page&quot;); For example, `#anchor`
* 在内容查找器中搜索页面，然后将页面图标拖放到“超链接”对话框中

>[!NOTE]
>
>URI 可以使用为您的安装配置的任何协议作为前缀。In a standard installation these are `https://`, `ftp://`, and `mailto:`. 将拒绝并非为您的安装配置的协议，并将其标记为无效。

要中断链接，请将光标置于链接文本中的任意位置并单击[!UICONTROL 取消链接]图标：

![](do-not-localize/chlimage_1-10.png)

### 锚点 {#anchors}

![](do-not-localize/cq55_rte_anchor.png)

通过放置光标或选择某些文本可以在文本中的任意位置创建锚点。然后单击&#x200B;**锚点**&#x200B;图标以打开对话框。

输入锚点的名称，然后单击&#x200B;**确定**&#x200B;进行保存。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

当编辑组件时会显示锚点，现在可在链接的目标中使用锚点。

![chlimage_1-104](assets/chlimage_1-104.png)

### 查找并替换 {#find-and-replace}

![](do-not-localize/cq55_rte_findreplace.png)

AEM 提供了&#x200B;**查找**&#x200B;和&#x200B;**替换**（查找并替换）功能。

两者均有一个&#x200B;**查找下一个**&#x200B;按钮以在打开的组件中搜索指定的文本。您还可以指定是否需要匹配大小写。

搜索将始终从文本中的当前光标位置开始。当到达组件末尾时，将有消息告知您下个搜索操作将从头开始。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

通过&#x200B;**替换**&#x200B;选项，您可以&#x200B;**查找**，然后用指定文本&#x200B;**替换**&#x200B;当前组件中的单个实例，或者&#x200B;**全部替换**&#x200B;这些实例。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 图像 {#images}

可从内容查找中拖动图像以将其添加到文本。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM 还提供了用于进行更详细图像配置的专用组件。For example the **Image** and **Text Image** components are available.

### 拼写检查 {#spelling-checker}

![](do-not-localize/cq55_rte_spellchecker.png)

拼写检查将检查当前组件中的所有文本。

所有不正确的拼写将突出显示：

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>拼写检查将通过采用子树的语言属性或从 URL 中提取语言，来以网站的语言运行。例如，对于 `en` 分支，将检查英语；对于 `de` 分支，将检查德语。

### 表 {#tables}

可通过以下两种方式使用表：

* 作为&#x200B;**表**&#x200B;组件

   ![chlimage_1-105](assets/chlimage_1-105.png)

* 从&#x200B;**文本**&#x200B;组件中

   ![](do-not-localize/chlimage_1-11.png)

   >[!NOTE]
   >
   >Although tables are available in the RTE, it is recommended to use the **Table** component when creating tables.

在&#x200B;**文本**&#x200B;和&#x200B;**表**&#x200B;组件中，可通过单击表中的上下文菜单（通常是鼠标右键按钮）使用表功能；例如：

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>在&#x200B;**表**&#x200B;组件中，专用工具栏同样可用，包括各种标准富文本编辑器功能，以及一部分特定于表的功能。

特定于表的功能包括：

* [表属性](#table-properties)
* [单元格属性](#cell-properties)
* [添加或删除行](#add-or-delete-rows)
* [添加或删除列](#add-or-delete-columns)
* [选择整行或整列](#selecting-entire-rows-or-columns)
* [合并单元格](#merge-cells)
* [拆分单元格](#split-cells)
* [嵌套表](#creating-nested-tables)
* [删除表](#remove-table)

#### 表属性 {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

单击&#x200B;**确定**&#x200B;保存之前，可配置表的基本属性：

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **宽度**:表的总宽度。

* **高度**:表的总高度。

* **边框**:表边框的大小。

* **单元格边距**:这定义单元格内容与其边框之间的空白。

* **单元格间距**:这定义单元格之间的距离。

>[!NOTE]
>
>“宽度”和“高度”等一些单元格属性可以定义为像素或百分比。

>[!CAUTION]
>
>Adobe建议您为表定义宽度。

#### 单元格属性 {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

可以配置特定单元格或单元格系列的属性：

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **宽度**
* **高度**
* **水平对齐** - 左对齐、居中对齐或右对齐
* **垂直对齐** -顶部、中间、底部或基线
* **单元格类型**-数据或标题
* **** 应用于：单个单元格，整行，整列

#### 添加或删除行 {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

可以在当前行的上方或下方添加行。

还可删除当前行。

#### 添加或删除列 {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

可以在当前列的左侧或右侧添加列。

还可删除当前列。

#### 选择整行或整列 {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

选择整个当前行或列。随后可进行特定操作（例如合并）。

#### 合并单元格 {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* 如果您选择了一组单元格，可以将这些单元格合并为一个。
* 如果您只选择了一个单元格，可以将其与右侧或下方的单元格合并。

#### 拆分单元格 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

选择单一单元格以将其拆分：

* 水平拆分单元格将在当前单元格的右侧、当前列中生成新单元格。
* 垂直拆分单元格将在当前单元格的下方、但在当前行中生成新单元格。

#### 创建嵌套表 {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

创建嵌套表将在当前单元格中创建一个新的独立表。

>[!NOTE]
>
>某些附加行为取决于浏览器：
>
>* Windows IE：使用 Ctrl 并单击主鼠标按钮（通常是左键）可选择多个单元格。
>* Firefox:拖动指针以选择单元格范围。


#### 删除表 {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

使用此选项可从文本组件中删除 **[!UICONTROL 表]** 。

### 特殊字符 {#special-characters}

![](do-not-localize/cq55_rte_specialchars.png)

富文本编辑器能够使用某些特殊字符；这些字符可能根据您的安装而有所不同。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

使用鼠标悬停可查看字符的放大版本，然后单击以便将其包含在您的文本中的当前位置。

### 源编辑模式 {#source-editing-mode}

![](do-not-localize/cq55_rte_sourceedit.png)

源编辑模式允许您查看和编辑组件的基础 HTML。

因此文本：

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

在源模式下将如下所示（通常源比较长，因此您将必须滚动鼠标）：

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>离开源模式时，AEM 将进行某些验证检查（例如，确保文本正确包含/嵌套在块中）。这会导致更改您的编辑。
