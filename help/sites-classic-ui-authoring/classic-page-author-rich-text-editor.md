---
title: 富文本编辑器
description: 富文本编辑器是用于向AEM输入文本内容的基本构建块。
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 2%

---

# 富文本编辑器 {#rich-text-editor}

富文本编辑器是用于向AEM输入文本内容的基本构建块。 它构成了各种组件的基础，包括：

* 文本
* 文本图像
* 表

## 富文本编辑器 {#rich-text-editor-1}

所见即所得编辑对话框提供了一系列广泛的功能：

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>可用的功能可以为各个项目进行配置，因此您的安装可能会有所不同。

## 就地编辑 {#in-place-editing}

除了基于对话框的富文本编辑模式外，AEM还提供就地编辑模式，该模式允许直接编辑显示在页面布局中的文本。

单击段落两次（缓慢双击）以进入就地编辑模式（组件边框现在将为橙色）。

您将能够直接编辑页面上的文本，而不是在对话框窗口中编辑。 只需进行更改，更改将自动保存。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>如果打开了内容查找器，则选项卡顶部将显示一个包含RTE格式选项的工具栏（如上所述）。
>
>如果未打开内容查找器，则不会显示工具栏。

目前，为生成的页面元素启用就地编辑模式。 **文本** 和 **标题** 组件。

>[!NOTE]
>
>此 [!UICONTROL 标题] 组件设计为包含不带换行符的短文本。 在“就地编辑”模式下编辑标题时，输入换行符将打开一个新标题 **文本** 标题下的组件。

## 富文本编辑器的功能 {#features-of-the-rich-text-editor}

富文本编辑器提供了一系列功能，包括 [取决于配置](/help/sites-administering/rich-text-editor.md) 单个组件的ID。 这些功能适用于触控优化用户界面和经典UI。

### 基本字符格式 {#basic-character-formats}

![“字符格式”工具栏](do-not-localize/cq55_rte_basicchars.png)

在这里，您可以对已选择（高亮显示）的字符应用格式；某些选项也具有快捷键：

* 粗体(Ctrl-B)
* 斜体(Ctrl-I)
* 下划线(Ctrl-U)
* 下标
* 上标

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

所有操作都作为切换操作，因此重新选择将移除格式。

### 预定义的样式和格式 {#predefined-styles-and-formats}

![cq55_rte_stylesepage](assets/cq55_rte_stylesparagraph.png)

您的安装可以包括预定义的样式和格式。 这些功能在 **[!UICONTROL 样式]** 和 **[!UICONTROL 格式]** 下拉列表，并且可以应用于已选择的文本。

样式可以应用于特定字符串（样式与CSS关联）：

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

而格式应用于整个文本段落(格式基于HTML)：

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

只能更改特定格式(默认为 **[!UICONTROL 段落]**)。

可以移除样式；将光标置于已应用样式的文本中，然后单击移除图标：

>[!CAUTION]
>
>实际上，不要重新选择应用了样式的文本或图标将被停用。

### 剪切、复制、粘贴 {#cut-copy-paste}

![剪切、复制、粘贴工具栏](do-not-localize/cq55_rte_cutcopypaste.png)

的标准功能 **[!UICONTROL 剪切]** 和 **[!UICONTROL 复制]** 可用。 几种口味 **[!UICONTROL 粘贴]** 格式不同。

* 剪切(Ctrl-X)
* 复制(Ctrl-C)
* 粘贴这是组件的默认粘贴机制(Ctrl-V)；当现成安装时，这配置为 [!UICONTROL 从Word粘贴].

* 粘贴为文本：剥离所有样式和格式以仅粘贴纯文本。

* 从Word粘贴：此操作会将内容粘贴为HTML（进行一些必要的重新格式设置）。

### 撤消，重做 {#undo-redo}

![撤消，重做工具栏](do-not-localize/cq55_rte_undoredo.png)

AEM会按时间顺序保留当前组件中最后50个操作的记录。 如果需要，可以严格按照顺序撤消（然后重新完成）这些操作。

>[!CAUTION]
>
>历史记录仅保留当前编辑会话。 每次打开组件进行编辑时，它都会重新启动。

>[!NOTE]
>
>五十是默认的任务数。 对于您的安装，这可能有所不同。

### 对齐方式 {#alignment}

![对齐工具栏](do-not-localize/cq55_rte_alignment.png)

文本可以左对齐、居中对齐或右对齐。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### 缩进 {#indentation}

![缩进工具栏](do-not-localize/cq55_rte_indent.png)

可以增加或减少段落的缩进。 所选段落将缩进，输入的任何新文本将保留当前缩进级别。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### 列表 {#lists}

![列表工具栏](do-not-localize/cq55_rte_lists.png)

项目符号和编号列表均可在文本内创建。 选择列表类型并开始键入或突出显示要转换的文本。 在这两种情况下，换行符将启动新的列表项。

可通过缩进一个或多个列表项实现嵌套列表。

只需将光标置于列表内，然后选择另一种样式，即可更改列表的样式。 子列表也可以具有与包含列表不同的样式。 创建子列表后（通过缩进）即可应用此选项。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### 链接 {#links}

![链接工具栏](do-not-localize/cq55_rte_links.png)

通过突出显示所需文本，然后单击超链接图标，会生成指向URL（网站内或外部位置中）的链接：

![“超链接”图标](do-not-localize/chlimage_1-9.png)

您将看到一个对话框，用于指定目标URL，以及是否应在新窗口中打开该URL。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

您可以：

* 直接键入URI
* 使用站点地图选择网站中的页面
* 输入URI，然后附加目标锚点；例如， `www.TargetUri.org#AnchorName`
* 仅输入锚点（引用“当前页面”）；例如， `#anchor`
* 在内容查找器中搜索页面，然后将页面图标拖放到超链接对话框中

>[!NOTE]
>
>URI可以在任何为您的安装配置的协议前加上。 在标准安装中， `https://`， `ftp://`、和 `mailto:`. 未针对您的安装配置的协议将被拒绝并标记为无效。

要断开链接位置，将光标置于链接文本中的任何位置，然后单击 [!UICONTROL 取消链接] 图标：

![“取消链接”图标](do-not-localize/chlimage_1-10.png)

### 锚点 {#anchors}

![锚点工具栏](do-not-localize/cq55_rte_anchor.png)

通过定位光标或选取某些文本，可以在文本中的任意位置创建锚点。 然后，单击 **锚点** 图标以打开对话框。

输入锚点的名称，然后单击 **确定** 以保存。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

在编辑组件时会显示锚点，现在可以在链接的目标中使用。

![chlimage_1-104](assets/chlimage_1-104.png)

### 查找和替换 {#find-and-replace}

![查找和替换工具栏](do-not-localize/cq55_rte_findreplace.png)

AEM同时提供 **查找** 和 **替换** （查找和替换）函数。

两者都有 **查找下一个** 按钮，在打开的组件中搜索指定的文本。 您还可以指定是否需要匹配大小写（大写/小写）。

搜索将始终从文本中的当前光标位置开始。 当组件结束时将显示一条消息，通知您下一个搜索操作将从顶部开始。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

此 **替换** 选项 **查找**，则 **替换** 具有指定文本的单个实例，或者 **全部替换** 当前组件中的实例。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 图像 {#images}

可以从内容查找器中拖动图像以将其添加到文本中。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM还提供了专门的组件，用于更详细的图像配置。 例如， **图像** 和 **文本图像** 组件可用。

### 拼写检查程序 {#spelling-checker}

![拼写检查器](do-not-localize/cq55_rte_spellchecker.png)

拼写检查器将检查当前组件中的所有文本。

任何错误的拼写都会突出显示：

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>拼写检查器将通过获取子树的语言属性或从URL中提取语言来使用网站的语言。 例如， `en` 将检查分支的英语和 `de` 德语分支。

### 表 {#tables}

表可用于以下两种情况：

* 作为 **表** 组件

  ![表格组件](assets/chlimage_1-105.png)

* 从 **文本** 组件

  ![文本工具栏](do-not-localize/chlimage_1-11.png)

  >[!NOTE]
  >
  >虽然RTE中提供了表格，但建议使用 **表** 组件。

在 **文本** 和 **表** “组件”表格功能可通过在表格内单击上下文菜单（通常是鼠标右键）来使用；例如：

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>在 **表** 组件时，还提供了专门的工具栏，包括各种标准的富文本编辑器功能以及特定于表的功能的子集。

该表的特定功能包括：

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

在单击之前，可以配置表的基本属性 **确定** 要保存，请执行以下操作：

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **宽度**：表的总宽度。

* **高度**：表的总高度。

* **边框**：表边框的大小。

* **单元格边距**：此属性定义单元格内容与其边框之间的空格。

* **单元格间距**：定义单元格之间的距离。

>[!NOTE]
>
>一些单元格属性（如“宽度”和“高度”）可以定义为像素或百分比。

>[!CAUTION]
>
>Adobe建议您为表格定义宽度。

#### 单元格属性 {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

可以配置特定单元格或一系列单元格的属性：

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **宽度**
* **高度**
* **水平对齐**  — 左、中或右
* **垂直对齐**  — 顶部、中间、底部或基线
* **单元格类型** — 数据或标题
* **应用于：** 单个单元格、整行、整列

#### 添加或删除行 {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

可以在当前行的上方或下方添加行。

也可以删除当前行。

#### 添加或删除列 {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

可以将列添加到当前列的左侧或右侧。

也可以删除当前列。

#### 选择整行或整列 {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

选择整个当前行或列。 随后即可使用特定操作（例如合并）。

#### 合并单元格 {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* 如果您选择了一组单元格，则可以将这些单元格合并为一个单元格。
* 如果您只选择了一个单元格，则可以将其与右侧或下方的单元格合并。

#### 拆分单元格 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

选择要拆分的单个单元格：

* 水平拆分单元格将在当前列中的当前单元格右侧生成一个新单元格。
* 垂直拆分单元格将在当前单元格下方但在当前行内生成一个新单元格。

#### 创建嵌套表 {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

创建嵌套表将在当前单元格中创建一个新的自包含表。

>[!NOTE]
>
>某些其他行为取决于浏览器：
>
>* Windows IE：使用Ctrl +鼠标主键单击（通常是左键）选择多个单元格。
>* Firefox：拖动指针以选择单元格范围。

#### 删除表 {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

使用选项，将表从 **[!UICONTROL 文本]** 组件。

### 特殊字符 {#special-characters}

![特殊字符工具栏](do-not-localize/cq55_rte_specialchars.png)

富文本编辑器可以使用特殊字符；这些字符可能会因您的安装而异。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

使用鼠标悬停可查看字符的放大版本，然后单击以将其包含在文本中的当前位置。

### 源编辑模式 {#source-editing-mode}

![源编辑模式工具栏](do-not-localize/cq55_rte_sourceedit.png)

源编辑模式允许您查看和编辑组件的基础HTML。

因此，文本：

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

在源模式下，将如下所示（源通常更长，因此您必须滚动）：

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>离开源模式时，AEM会进行某些验证检查（例如，确保文本正确包含/嵌套在块中）。 这可能会导致编辑内容发生更改。
