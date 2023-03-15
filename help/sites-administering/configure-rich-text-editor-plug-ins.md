---
title: 配置富文本编辑器插件
description: 了解如何配置Adobe Experience Manager富文本编辑器插件以启用各个功能。
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: 11cda989e6a28428f03a269c407a7672e6eab747
workflow-type: tm+mt
source-wordcount: '4406'
ht-degree: 5%

---


# 配置富文本编辑器插件 {#configure-the-rich-text-editor-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有功能属性。 您可以将features属性配置为启用或禁用一个或多个RTE功能。 本文介绍了如何专门配置RTE插件。

有关其他RTE配置的详细信息，请参见 [配置富文本编辑器](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>在使用CRXDE Lite时，建议使用定期保存更改 [!UICONTROL 全部保存] 选项。

## 激活插件并配置功能属性 {#activateplugin}

要激活插件，请执行以下步骤。 仅在首次配置插件时才需要执行某些步骤，因为对应的节点不存在。

默认情况下， `format`， `link`， `list`， `justify`、和 `control` 插件及其所有功能均在RTE中启用。

>[!NOTE]
>
>各自的 `rtePlugins` 节点称为 `<rtePlugins-node>` 以避免本文中的重复。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 创建父节点 `<rtePlugins-node>` 如果该文件不存在，则在配置任何RTE插件之前：

   * 根据您的组件，父节点包括：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 替代配置节点： `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 属于以下类型： **jcr：primaryType** `cq:Widget`
   * 两者都具有以下属性：

      * **名称** `name`
      * **类型** `String`
      * **值** `./text`


1. 根据您配置的接口，创建一个节点 `<rtePlugins-node>`，如果它不存在：

   * **名称** `rtePlugins`
   * **类型** `nt:unstructured`

1. 在此路径下，为要激活的每个插件创建一个节点：

   * **类型** `nt:unstructured`
   * **名称** 需要此插件的插件ID

激活插件后，请按照以下指南配置 `features` 属性。

|  | 启用所有功能 | 启用一些特定功能 | 禁用所有功能 |
|---|---|---|---|
| 名称 | 功能 | 功能 | 功能 |
| 类型 | 字符串 | 字符串[] (多字符串；将Type设置为String，然后单击Multi inCRXDE Lite) | 字符串 |
| 值 | `*` （星号） | 设置为一个或多个特征值 | - |

## 了解findreplace插件 {#findreplace}

此 `findreplace` 此插件不需要任何配置。 开箱即用。

在使用替换功能时，要替换的替换字符串应与查找字符串同时输入。不过，您仍可以在替换字符串之前单击“查找”来搜索它。如果在单击“查找”后输入替换字符串，则搜索将重置到文本的开头。

在单击“查找”时，“查找和替换”对话框变为透明；在单击“替换”时，此对话框变为不透明。这允许作者审查自己将替换的文本。如果用户单击“全部替换”，对话框将关闭并显示所做的替换次数。

## 配置粘贴模式 {#paste-modes}

使用RTE时，作者可以使用以下三种模式之一粘贴内容：

* **浏览器模式**：使用浏览器的默认粘贴实施粘贴文本。 不建议使用此方法，因为它可能会引入不需要的标记。

* **纯文本模式**：以纯文本形式粘贴剪贴板内容。 在插入之前，它会从复制的内容中剥离所有样式和格式元素 [!DNL Experience Manager] 组件。

* **MS Word模式**：从MS Word复制时粘贴带格式的文本，包括表格。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并且仅保留部分格式。

### 配置RTE工具栏上可用的粘贴选项  {#configure-paste-options-available-on-the-rte-toolbar}

您可以在RTE工具栏中为作者提供以下三个图标中的部分、全部或不提供：

* **[!UICONTROL 粘贴(Ctrl+V)]**：可预配置为对应于以上三种粘贴模式之一。

* **[!UICONTROL 粘贴为文本]**：提供纯文本模式功能。

* **[!UICONTROL 从Word粘贴]**：提供MS Word模式功能。

要配置RTE以显示所需的图标，请执行以下步骤。

1. 导航到您的组件，例如 `/apps/<myProject>/components/text`.
1. 导航到节点 `rtePlugins/edit`. 参见 [激活插件](#activateplugin) 如果节点不存在，则为。
1. 创建 `features` 上的属性 `edit` 节点并添加一项或多项功能。 保存所有更改。

### 配置粘贴(Ctrl+V)图标和快捷键的行为 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

您可以预配置 **[!UICONTROL 粘贴(Ctrl+V)]** 图标，请执行以下步骤。 此配置还定义了作者用于粘贴内容的键盘快捷键Ctrl+V的行为。

该配置允许使用以下三种类型的用例：

* 使用浏览器的默认粘贴实施粘贴文本。 不建议使用此方法，因为它可能会引入不需要的标记。 配置方式 `browser` 下面的。

* 将剪贴板内容粘贴为纯文本。 在AEM组件中插入之前，它会从复制的内容中剥离样式和格式的所有元素。 配置方式 `plaintext` 下面的。

* 从MS Word复制时，粘贴包含格式设置的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并且仅保留部分格式。 配置方式 `wordhtml` 下面的。

1. 在组件中，导航到 `<rtePlugins-node>/edit` 节点。 如果节点不存在，请创建节点。 有关更多信息，请参阅 [激活插件](#activateplugin).
1. 在 `edit` 节点使用以下详细信息创建属性：

   * **名称** `defaultPasteMode`
   * **类型** `String`
   * **值** 所需的粘贴模式之一 `browser`， `plaintext`，或 `wordhtml`.

### 配置粘贴内容时允许的格式 {#pasteformats}

粘贴为Microsoft-Word (`paste-wordhtml`)模式可进行进一步配置，以便您可以明确定义在从其他程序(如Microsoft Word)粘贴到AEM时允许使用哪些样式。

例如，如果在AEM中粘贴时只允许使用粗体格式和列表，则可以筛选掉其他格式。 这称为可配置的粘贴筛选，可以对以下两项执行：

* [文本](#paste-modes)
* [链接](#linkstyles)

对于链接，您还可以定义自动接受的协议。

要配置在将文本从其他程序粘贴到AEM时允许的格式，请执行以下操作：

1. 在组件中，导航到节点 `<rtePlugins-node>/edit`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `edit` 用于保存HTML粘贴规则的节点：

   * **名称** `htmlPasteRules`
   * **类型** `nt:unstructured`

1. 在下创建节点 `htmlPasteRules`，保存允许的基本格式的详细信息：

   * **名称** `allowBasics`
   * **类型** `nt:unstructured`

1. 要控制接受的各个格式，请在 `allowBasics` 节点：

   * **名称** `bold`
   * **名称** `italic`
   * **名称** `underline`
   * **名称** `anchor` （对于链接和已命名锚点）
   * **名称** `image`

   所有属性都是 **类型** `Boolean`，因此在适当的 **值** 您可以选择或删除复选标记以启用或禁用该功能。

   >[!NOTE]
   >
   >如果未明确定义，则使用默认值true ，并且接受格式。

1. 也可以使用一系列其他属性或节点定义其他格式，这些属性或节点也应用于 `htmlPasteRules` 节点。 保存所有更改。

您可以将以下属性用于 `htmlPasteRules`.

| 属性 | 类型 | 描述 |
|---|---|---|
| `allowBlockTags` | 字符串 | 定义允许的块标记列表。 一些可能的块标记包括： <ul> <li>头条(h1、h2、h3)</li> <li>第(p)款</li> <li>列表(ol， ul)</li> <li>表(table)</li> </ul> |
| `fallbackBlockTag` | 字符串 | 定义块标记，该标记用于具有块标记但未包含到的任何块 `allowBlockTags`. `p` 大多数情况下就足够了。 |
| 表 | nt:unstructured | 定义粘贴表时的行为。 此节点必须具有属性 `allow` （键入布尔值）以定义是否允许粘贴表。 如果“允许”设置为 `false`，您必须指定属性 `ignoreMode` （键入字符串）以定义如何处理粘贴的表内容。 的有效值 `ignoreMode` 为： <ul> <li>`remove`：删除表内容。</li> <li>`paragraph`：将表格单元格转换为段落。</li> </ul> |
| list | nt:unstructured | 定义粘贴列表时的行为。 必须具有属性 `allow` （键入布尔值）以定义是否允许粘贴列表。 如果 `allow` 设置为 `false`，您必须指定属性 `ignoreMode` （键入字符串）以定义如何处理粘贴的任何列表内容。 的有效值 `ignoreMode` 为： <ul><li> `remove`：删除列表内容。</li> <li>`paragraph`：将列表项转换为段落。</li> </ul> |

有效示例 `htmlPasteRules` 结构如下所示。

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

## 配置文本样式 {#textstyles}

作者可以应用样式来更改部分文本的外观。 样式基于您在CSS样式表中预定义的CSS类。 风格化的内容包含在 `span` 标记使用 `class` 属性以引用CSS类。 例如：`<span class=monospaced>Monospaced Text Here</span>`。

首次启用样式插件时，没有默认样式可用。 弹出列表为空。 要向作者提供样式，请执行以下操作：

* 启用样式下拉选择器。
* 指定样式表的位置。
* 指定可从“样式”下拉列表中选择的单个样式。

对于以后的配置，如要添加更多样式，请仅按照说明引用新的样式表并指定其他样式。

>[!NOTE]
>
>您可以为以下对象定义样式 [表或表单元格](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). 这些配置需要单独的过程。

### 启用样式下拉选择器列表 {#styleselectorlist}

启用样式插件即可完成此操作。

1. 在组件中，导航到节点 `<rtePlugins-node>/styles`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 上的属性 `styles` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

1. 保存所有更改。

>[!NOTE]
>
>启用样式插件后，“样式”下拉列表将显示在“编辑”对话框中。 但是，列表为空，因为未配置样式。

### 指定样式表位置 {#locationofstylesheet}

然后，指定要引用的样式表的位置：

1. 导航到文本组件的根节点，例如 `/apps/<myProject>/components/text`.
1. 添加属性 `externalStyleSheets` 至的父节点 `<rtePlugins-node>`：

   * **名称** `externalStyleSheets`
   * **类型** `String[]` (多字符串；单击 **多个** 在CRXDE中)
   * **值** 要包含的每个样式表的路径和文件名。 使用存储库路径。

   >[!NOTE]
   >
   >以后可随时向其它样式表添加参照。

1. 保存所有更改。

>[!NOTE]
>
>在对话框（经典UI）中使用RTE时，您可能需要指定针对富文本编辑优化的样式表。 由于技术限制，编辑器中的CSS上下文丢失，因此您可能希望模拟此上下文以改进WYSIWYG体验。
>
>富文本编辑器使用一个容器DOM元素，其ID为 `CQrte` 可用于提供不同的样式进行查看和编辑：
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### 在弹出列表中指定可用的样式 {#stylesindropdown}

1. 在组件定义中，导航到节点 `<rtePlugins-node>/styles`，如中创建的 [启用样式下拉选择器](#styleselectorlist).
1. 在节点下 `styles`，创建新节点(也称为 `styles`)，以保存可用的列表：

   * **名称** `styles`
   * **类型** `cq:WidgetCollection`

1. 在 `styles` 表示单个样式的节点：

   * **名称**，您可以指定名称，但它应该适合样式
   * **类型** `nt:unstructured`

1. 添加属性 `cssName` 要引用CSS类，请执行以下操作：

   * **名称** `cssName`
   * **类型** `String`
   * **值** CSS类的名称(不带前缀“。”；例如， `cssClass` 而不是 `.cssClass`)

1. 添加属性 `text` 到同一节点；这将定义选择框中显示的文本：

   * **名称** `text`
   * **类型** `String`
   * **值** 样式的描述；显示在“样式”下拉选择框中。

1. 保存更改。

   对每个所需的样式重复上述步骤。

### 配置RTE以优化日语断字 {#jpwordwrap}

使用AEM创作日语内容的作者可以将样式应用于字符，以避免在不需要换行符的情况下出现换行符。 这允许作者在所需的位置处使句子断开。 此功能的样式基于CSS样式表中预定义的CSS类。

>[!NOTE]
>
>此功能至少需要AEM 6.5 Service Pack 1。

要创建作者可以应用于日语文本的样式，请执行以下步骤：

1. 在styles节点下创建新节点。 参见 [指定新样式](#stylesindropdown).
   * 名称: `jpn-word-wrap`
   * 类型: `nt:unstructure`

1. 添加属性 `cssName` 到节点以引用CSS类。 此类名称是日语自动换行功能的保留名称。
   * 名称: `cssName`
   * 类型: `String`
   * 值： `jpn-word-wrap` (无前置词 `.`)

1. 将属性文本添加到同一节点。 值是作者在选择样式时看到的样式名称。
   * 名称： `text`
*类型： 
`String`
   * 值: `Japanese word-wrap`

1. 创建样式表并指定其路径。 参见 [指定样式表的位置](#locationofstylesheet). 将以下内容添加到样式表中。 根据需要更改背景颜色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![使日语自动换行功能可供作者使用的样式表](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式 {#paraformats}

在RTE中创作的任何文本都放置在块标记中，默认设置为 `<p>`. 启用 `paraformat` 插件，您可使用下拉选择列表指定可分配给段落的其他块标记。 段落格式通过分配正确的块标记来确定段落类型。 作者可以使用“格式”选择器选择和分配格式。 示例块标记包括标准段落 &lt;p> 和标题 &lt;h1>， &lt;h2>，等等。

>[!CAUTION]
>
>此插件不适用于具有复杂结构的内容，例如列表或表。

>[!NOTE]
>
>如果块标记，例如 &lt;hr> 标签，无法分配给段落，它不是paraformat插件的有效用例。

首次启用段落格式插件时，没有默认的段落格式可用。 弹出列表为空。 要向作者提供段落格式，请执行以下操作：

* 启用格式下拉选择器列表。
* 指定可从下拉列表中选择作为段落格式的块标记。

对于以后的（重新）配置（如添加更多格式），请仅遵循说明中的相关部分。

### 启用“格式”下拉选择器 {#formatselectorlist}

首先启用paraformat插件：

1. 在组件中，导航到节点 `<rtePlugins-node>/paraformat`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 上的属性 `paraformat` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

>[!NOTE]
如果未进一步配置此插件，则会启用以下默认格式：
* 段落 ( `<p>`)
* 标题 1 ( `<h1>`)
* 标题 2 ( `<h2>`)
* 标题 3 ( `<h3>`)
>


>[!CAUTION]
配置RTE的段落格式时，请勿删除段落标记 &lt;p> 作为格式选项。 如果 `<p>` 标记被删除，那么内容作者无法选择 **段落格式** 选项，即使配置了其他格式也是如此。

### 指定可用的段落格式 {#paraformatsindropdown}

可以通过以下方式使段落格式可供选择：

1. 在组件定义中，导航到节点 `<rtePlugins-node>/paraformat`，如中创建的 [启用格式下拉选择器](#styleselectorlist).
1. 在 `paraformat` 节点创建一个新节点，保存格式列表：

   * **名称** `formats`
   * **类型** `cq:WidgetCollection`

1. 在 `formats` 节点，这将保存单个格式的详细信息：

   * **名称**，您可以指定名称，但它应该适合该格式（例如myparagraph、myheading1）。
   * **类型** `nt:unstructured`

1. 在此节点中，添加属性以定义使用的块标记：

   * **名称** `tag`
   * **类型** `String`
   * **值** 格式的块标记；例如：p、h1、h2等。

      您无需输入分隔尖括号。

1. 要添加到同一节点，请添加另一个属性，以便在下拉列表中显示描述性文本：

   * **名称** `description`
   * **类型** `String`
   * **值** 此格式的描述性文本；例如，段落、标题1、标题2等。 此文本显示在“格式”选择列表中。

1. 保存更改。

   对每个所需的格式重复这些步骤。

>[!CAUTION]
如果定义自定义格式，则默认格式(`<p>`， `<h1>`， `<h2>`、和 `<h3>`)将被删除。 重新创建 `<p>` 格式，因为它是默认格式。

## 配置特殊字符 {#spchar}

在标准AEM安装中， `misctools` 插件已启用特殊字符(`specialchars`)默认选项可立即使用；例如，版权和商标符号。

您可以配置RTE以使您自己的字符选择可用；通过定义不同的字符或整个序列。

>[!CAUTION]
添加您自己的特殊字符会覆盖默认选项。 如果需要，可在您自己的选择中（重新）定义这些字符。

### 定义单个字符 {#definesinglechar}

1. 在组件中，导航到节点 `<rtePlugins-node>/misctools`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 上的属性 `misctools` 节点：

   * **名称** `features`
   * **类型** `String[]`
   * **值** `specialchars`

          (或 `String / *` （如果为此插件应用了所有功能）

1. 下 `misctools` 创建一个节点来保存特殊字符配置：

   * **名称** `specialCharsConfig`
   * **类型** `nt:unstructured`

1. 下 `specialCharsConfig` 创建另一个节点来保存字符列表：

   * **名称** `chars`
   * **类型** `nt:unstructured`

1. 下 `chars` 添加新节点以保存单个字符定义：

   * **名称** 您可以指定名称，但名称应反映字符；例如，一半。
   * **类型** `nt:unstructured`

1. 要添加到此节点，请添加以下属性：

   * **名称** `entity`
   * **类型** `String`
   * **值** 所需字符的HTML表示形式；例如， `&189;` 小数点的一半。

1. 保存更改。

在CRXDE中，保存属性后，将显示表示的字符。 请参阅下面一半的示例。 重复上述步骤以使作者可以使用更多特殊字符。

![在CRXDE中，添加单个字符以使其在RTE工具栏中可用](assets/chlimage_1-106.png "在CRXDE中，添加单个字符以使其在RTE工具栏中可用")

### 定义字符范围 {#definerangechar}

1. 使用中的步骤1至3 [定义单个字符](#definesinglechar).
1. 下 `chars` 添加新节点以保存字符范围的定义：

   * **名称** 您可以指定名称，但它应反映字符范围；例如，铅笔。
   * **类型** `nt:unstructured`

1. 在此节点下（根据特殊字符范围命名）添加以下两个属性：

   * **名称** `rangeStart`

      **类型** `Long`
      **值** 此 [Unicode](https://unicode.org/) 表示范围中第一个字符（小数）

   * **名称** `rangeEnd`

      **类型** `Long`
      **值** 此 [Unicode](https://unicode.org/) 范围中最后一个字符的表示形式（小数）

1. 保存更改。

   例如，定义从9998到10000之间的范围，为您提供以下字符。

   ![在CRXDE中，定义要在RTE中可用的字符范围](assets/chlimage_1-107.png)

   *图：在CRXDE中，定义要在RTE中可用的字符范围*

   ![RTE中可用的特殊字符会在弹出窗口中向作者显示](assets/rtepencil.png "RTE中可用的特殊字符会在弹出窗口中向作者显示")

## 配置表样式 {#tablestyles}

样式通常应用于文本，但也可以对表或几个表单元格应用单独的样式集。 作者可以在“单元格属性”或“表属性”对话框的“样式选择器”框中找到此类样式。 在文本组件（或派生项）而非标准表组件中编辑表时，可以使用样式。

>[!NOTE]
您只能为经典UI定义表和单元格的样式。

>[!NOTE]
在RTE组件中或从RTE组件中复制和粘贴表依赖于浏览器。 并非所有浏览器都支持开箱即用。 根据表结构和浏览器，可能会得到不同的结果。 例如，在经典UI和触屏UI中，当您在Mozilla Firefox的RTE组件中复制并粘贴表时，不会保留表的布局。

1. 在组件内，导航到节点 `<rtePlugins-node>/table`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 创建 `features` 上的属性 `table` 节点：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

   >[!NOTE]
   如果不希望启用所有表格功能，可创建 `features` 属性为：
   * **类型** `String[]`
   * **值**(s)视需要提供以下一项或两项内容：
      * `table` 允许编辑表属性；包括样式。
      * `cellprops` 允许编辑单元格属性，包括样式。


1. 定义CSS样式表的位置以引用这些样式表。 参见 [指定样式表的位置](#locationofstylesheet) 因为这与定义 [文本样式](#textstyles). 如果定义了其他样式，则可以定义位置。
1. 在 `table` 节点创建以下新节点（根据需要）：

   * 为整个表定义样式(可在 **表属性**)：

      * **名称** `tableStyles`
      * **类型** `cq:WidgetCollection`
   * 为各个单元格定义样式(可在 **单元格属性**)：

      * **名称** `cellStyles`
      * **类型** `cq:WidgetCollection`


1. 创建新节点(在 `tableStyles` 或 `cellStyles` 节点)，以表示单个样式：

   * **名称** 您可以指定名称，但它应反映样式。
   * **类型** `nt:unstructured`

1. 在此节点上创建属性：

   * 定义要引用的CSS样式

      * **名称** `cssName`
      * **类型** `String`
      * **值** CSS类的名称（不带前缀） `.`例如， `cssClass` 而不是 `.cssClass`)
   * 定义要在下拉选择器中显示的描述性文本

      * **名称** `text`
      * **类型** `String`
      * **值** 要显示在选择列表中的文本


1. 保存所有更改。

对每个所需的样式重复上述步骤。

### 为辅助功能配置表中的隐藏标头 {#hiddenheader}

有时，您可以创建没有可视文本的数据表，但前提是列标题的用途隐含在列与其他列的可视关系中。 在这种情况下，有必要在标题单元格的单元格中提供隐藏的内部文本，以允许屏幕阅读器和其他辅助技术帮助有各种需求的阅读器了解列的用途。

为了在这种情况下增强辅助功能，RTE支持隐藏的标题单元格。 此外，它还提供与表中隐藏标头相关的配置设置。 这些设置允许您在编辑和预览模式下对隐藏的标题应用CSS样式。 为帮助作者在编辑模式下识别隐藏的标头，请在代码中包含以下参数：

* `hiddenHeaderEditingCSS`：指定在编辑RTE时应用于hidden-header单元格的CSS类的名称。
* `hiddenHeaderEditingStyle`：指定在编辑RTE时应用于隐藏标题单元格的样式字符串。

如果在代码中同时指定CSS和样式字符串，则CSS类将优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

为帮助作者在预览模式下对隐藏的标题应用CSS，您可以在代码中包含以下参数：

* `hiddenHeaderClassName`：指定在预览模式下应用于隐藏标题单元格的CSS类的名称。
* `hiddenHeaderStyle`：指定在预览模式下应用于hidden-header单元格的样式字符串。

如果在代码中同时指定CSS和样式字符串，则CSS类将优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

## 为拼写检查器添加词典 {#adddict}

激活spellcheck插件后，RTE会使用字典来表示每种相应的语言。 然后，通过获取子树的语言属性或从URL中提取语言来根据网站的语言选择这些语言；例如。 此 `/en/` 分支被选为英语， `/de/` 分支为德语。

>[!NOTE]
消息 `Spell checking failed` 如果尝试检查未安装的语言，则会显示。 标准词典位于 `/libs/cq/spellchecker/dictionaries`，以及相应的自述文件。 请勿修改文件。

标准AEM安装包括美式英语词典(`en_us`)和英式英语(`en_gb`)。 要添加更多词典，请按照以下步骤操作。

1. 导航到页面 [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. 执行以下操作之一，查找您选择的语言的词典：

   * 搜索您选择的语言的词典。 在词典页面上，找到指向原始源或作者网页的链接。 在此类页面上找到v2.x的字典文件。
   * 在v2.x词典文件中搜索 [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. 下载包含拼写定义的档案。 提取文件系统中存档的内容。

   >[!CAUTION]
   仅词典位于 `MySpell` 支持OpenOffice.org v2.0.1或更低版本的格式。 由于字典现在是存档文件，因此建议您在下载后验证存档。

1. 找到.aff和.dic文件。 将文件名保留为小写。 例如， `de_de.aff` 和 `de_de.dic`.
1. 将.aff和.dic文件加载到存储库中的 `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
RTE拼写检查器可按需使用。 当您开始键入文本时，它不会自动运行。 要运行拼写检查器，请单击 [!UICONTROL 拼写检查程序] 工具栏中。 RTE检查单词的拼写并突出显示拼写错误的单词。
如果合并拼写检查器建议的任何更改，则文本的状态会更改，拼写错误的单词将不再突出显示。 要运行拼写检查器，请再次点按/单击拼写检查器按钮。

## 配置撤消和重做操作的历史记录大小 {#undohistory}

RTE允许作者撤消或重做最后的几次编辑。 默认情况下，历史中存储50次编辑。 您可以根据需要配置此值。

1. 在组件内，导航到节点 `<rtePlugins-node>/undo`. 如果这些节点不存在，请创建它们。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `undo` 节点创建属性：

   * **名称** `maxUndoSteps`
   * **类型** `Long`
   * **值** 要在历史记录中保存的撤消步骤数。 默认为 50。使用 `0` 以完全禁用撤消/重做。

1. 保存更改。

## 配置选项卡大小 {#tabsize}

在任意文本中按制表符字符时，会插入预定义的空格数；默认情况下，这是三个不间断的空格和一个空格。

要定义制表符大小，请执行以下操作：

1. 在组件中，导航到节点 `<rtePlugins-node>/keys`. 如果节点不存在，请创建节点。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `keys` 节点创建属性：

   * **名称** `tabSize`
   * **类型** `String`
   * **值** 用于制表符的空格字符数

1. 保存更改。

## 设置缩进边距 {#indentmargin}

启用缩进（默认）后，您可以定义缩进的大小：

>[!NOTE]
此缩进大小仅适用于文本的段落（块）；它不会影响实际列表的缩进。

1. 在组件内，导航到节点 `<rtePlugins-node>/lists`. 如果这些节点不存在，请创建它们。 有关更多详细信息，请参阅 [激活插件](#activateplugin).
1. 在 `lists` 节点创建 `identSize` 参数：

   * **名称**: `identSize`
   * **类型**: `Long`
   * **值**：缩进边距所需的像素数。

## 配置可编辑空间的高度 {#editablespace}

>[!NOTE]
这仅适用于在对话框中使用RTE（而不是在经典UI中就地编辑）的情况。

您可以定义组件对话框中显示的可编辑空间的高度：

1. 在 `../items/text` 节点时，创建新属性：

   * **名称** `height`
   * **类型** `Long`
   * **值** 编辑画布的高度（像素）。

   >[!NOTE]
   这不会更改对话框窗口的高度。

1. 保存更改。

## 为链接配置样式和协议 {#linkstyles}

在AEM中添加链接时，您可以定义：

* 要使用的CSS样式
* 自动接受的协议

要配置如何将链接从其他程序添加到AEM中，请定义HTML规则。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在与相同的级别创建新节点 `<rtePlugins-node>`，即，在父节点下创建节点 `<rtePlugins-node>`：

   * **名称** `htmlRules`
   * **类型** `nt:unstructured`

   >[!NOTE]
   此 `../items/text` 节点具有属性：
   * **名称** `xtype`
   * **类型** `String`
   * **值** `richtext`

   的位置 `../items/text` 节点可能因对话框的结构而异；示例有两种 `/apps/myProject>/components/text/dialog/items/text` 和 `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. 下 `htmlRules`，创建一个新节点。

   * **名称** `links`
   * **类型** `nt:unstructured`

1. 在 `links` 节点根据需要定义属性：

   * 内部链接的CSS样式：

      * **名称** `cssInternal`
      * **类型** `String`
      * **值** CSS类的名称(不带前缀“。”；例如， `cssClass` 而不是 `.cssClass`)
   * 外部链接的CSS样式

      * **名称** `cssExternal`
      * **类型** `String`
      * **值** CSS类的名称(不带前缀“。”；例如， `cssClass` 而不是 `.cssClass`)
   * 有效数组 **协议**. 支持的协议包括 `http://`， `https://`， `file://`、和 `mailto:`.

      * **名称** `protocols`
      * **类型** `String[]`
      * **值**(s)一个或多个协议
   * **defaultprotocol** (类型的属性 **字符串**)：用户未明确指定时使用的协议。

      * **名称** `defaultProtocol`
      * **类型** `String`
      * **值**(s)一个或多个默认协议
   * 如何处理链接的目标属性的定义。 创建新节点：

      * **名称** `targetConfig`
      * **类型** `nt:unstructured`

      在节点上 `targetConfig`：定义所需的属性：

      * 指定目标模式：

         * **名称** `mode`
         * **类型** `String`)
         * **值**(s) ：

            * `auto`：表示选择了自动目标

               (由 `targetExternal` 外部链接或的属性 `targetInternal` （对于内部链接）。

            * `manual`：不适用于此上下文
            * `blank`：不适用于此上下文
      * 内部链接的目标：

         * **名称** `targetInternal`
         * **类型** `String`
         * **值** 内部链接的目标(仅在模式为 `auto`)
      * 外部链接的目标：

         * **名称** `targetExternal`
         * **类型** `String`
         * **值** 外部链接的目标(仅在模式为 `auto`)。








1. 保存所有更改。
