---
title: 設定RTF編輯器外掛程式
description: 瞭解如何設定Adobe Experience Manager RTF編輯器外掛程式，以啟用個別功能。
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
source-git-commit: 11cda989e6a28428f03a269c407a7672e6eab747
workflow-type: tm+mt
source-wordcount: '4406'
ht-degree: 5%

---


# 設定RTF編輯器外掛程式 {#configure-the-rich-text-editor-plug-ins}

RTE功能可透過一系列外掛程式提供，每個外掛程式都具備功能屬性。 您可以設定功能屬性，以啟用或停用一或多個RTE功能。 本文會說明如何特別設定RTE外掛程式。

如需其他RTE設定的詳細資訊，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md).

>[!NOTE]
>
>使用CRXDE Lite時，建議使用定期儲存變更 [!UICONTROL 全部儲存] 選項。

## 啟動外掛程式並設定功能屬性 {#activateplugin}

若要啟動外掛程式，請依照下列步驟操作。 只有當您第一次設定外掛程式時，才需要執行某些步驟，因為對應的節點不存在。

依預設， `format`， `link`， `list`， `justify`、和 `control` 外掛程式及其所有功能皆會在RTE中啟用。

>[!NOTE]
>
>個別 `rtePlugins` 節點稱為 `<rtePlugins-node>` 以避免本文中的重複專案。

1. 使用CRXDE Lite找到專案的文字元件。
1. 建立以下專案的父節點： `<rtePlugins-node>` 如果不存在，則在設定任何RTE外掛程式之前：

   * 根據您的元件，父節點為：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 替代設定節點： `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 屬於以下型別： **jcr：primaryType** `cq:Widget`
   * 兩者都有以下屬性：

      * **名称** `name`
      * **类型** `String`
      * **值** `./text`


1. 根據您設定的介面，建立節點 `<rtePlugins-node>`，如果它不存在：

   * **名称** `rtePlugins`
   * **类型** `nt:unstructured`

1. 在下方，為要啟用的每個外掛程式建立一個節點：

   * **类型** `nt:unstructured`
   * **名稱** 需要外掛程式的外掛程式ID

啟動外掛程式後，請遵循以下准則來設定 `features` 屬性。

|  | 啟用所有功能 | 啟用幾項特定功能 | 停用所有功能 |
|---|---|---|---|
| 名称 | 功能 | 功能 | 功能 |
| 类型 | 字符串 | 字串[] (多字串；將Type設定為String，然後按一下Multi inCRXDE Lite) | 字符串 |
| 价值 | `*` （星號） | 設定為一或多個特徵值 | - |

## 瞭解findreplace外掛程式 {#findreplace}

此 `findreplace` 外掛程式不需要任何設定。 開箱即用。

在使用替换功能时，要替换的替换字符串应与查找字符串同时输入。不过，您仍可以在替换字符串之前单击“查找”来搜索它。如果在单击“查找”后输入替换字符串，则搜索将重置到文本的开头。

在单击“查找”时，“查找和替换”对话框变为透明；在单击“替换”时，此对话框变为不透明。这允许作者审查自己将替换的文本。如果使用者按一下全部取代，對話方塊會關閉並顯示所做的取代數量。

## 設定貼上模式 {#paste-modes}

使用RTE時，作者可以下列三種模式之一貼上內容：

* **瀏覽器模式**：使用瀏覽器的預設貼上實作貼上文字。 不建議使用此方法，因為它可能會引入不想要的標籤。

* **純文字模式**：以純文字形式貼上剪貼簿內容。 它會在插入之前從複製的內容中移除樣式和格式的所有元素 [!DNL Experience Manager] 元件。

* **MS Word模式**：從MS Word複製時，貼上含有格式設定的文字（包括表格）。 不支援從其他來源（例如網頁或MS Excel）複製和貼上文字，且僅保留部分格式設定。

### 設定RTE工具列上可用的貼上選項  {#configure-paste-options-available-on-the-rte-toolbar}

您可以在RTE工具列中為作者提供以下三個圖示中的部分、全部或都不提供：

* **[!UICONTROL 貼上(Ctrl+V)]**：可預先設定為對應至上述三種貼上模式之一。

* **[!UICONTROL 貼上成文字]**：提供純文字模式功能。

* **[!UICONTROL 從Word貼上]**：提供MS Word模式功能。

若要設定RTE以顯示所需的圖示，請按照以下步驟操作。

1. 導覽至您的元件，例如 `/apps/<myProject>/components/text`.
1. 導覽至節點 `rtePlugins/edit`. 另請參閱 [啟動外掛程式](#activateplugin) 如果節點不存在。
1. 建立 `features` 上的屬性 `edit` 節點並新增一或多個功能。 儲存所有變更。

### 設定貼上(Ctrl+V)圖示和捷徑的行為 {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

您可以預先設定 **[!UICONTROL 貼上(Ctrl+V)]** 圖示，使用下列步驟。 此設定也會定義「作者」用來貼上內容的鍵盤快速鍵Ctrl+V的行為。

此設定允許以下三種使用案例：

* 使用瀏覽器的預設貼上實作來貼上文字。 不建議使用此方法，因為它可能會引入不想要的標籤。 設定方式 `browser` 下方的。

* 以純文字形式貼上剪貼簿內容。 它會先從複製的內容中移除樣式和格式的所有元素，然後再插入AEM元件。 設定方式 `plaintext` 下方的。

* 從MS Word複製時，貼上包含格式設定的文字（包括表格）。 不支援從其他來源（例如網頁或MS Excel）複製和貼上文字，且僅保留部分格式設定。 設定方式 `wordhtml` 下方的。

1. 在您的元件中，導覽至 `<rtePlugins-node>/edit` 節點。 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 在 `edit` 節點會使用下列詳細資料建立屬性：

   * **名称** `defaultPasteMode`
   * **类型** `String`
   * **值** 所需的貼上模式之一 `browser`， `plaintext`，或 `wordhtml`.

### 設定貼上內容時允許的格式 {#pasteformats}

貼上Microsoft文字(`paste-wordhtml`)模式可進行進一步設定，以便您明確定義從其他程式(例如Microsoft Word)在AEM中貼上時允許的樣式。

例如，如果在AEM中貼上時只允許使用粗體格式和清單，您可以篩選掉其他格式。 這稱為可設定的貼上篩選，這可同時針對下列兩項執行：

* [文本](#paste-modes)
* [链接](#linkstyles)

對於連結，您也可以定義自動接受的通訊協定。

若要設定將文字從其他程式貼入AEM時允許的格式：

1. 在您的元件中，導覽至節點 `<rtePlugins-node>/edit`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 在下建立節點 `edit` 用於儲存HTML貼上規則的節點：

   * **名称** `htmlPasteRules`
   * **类型** `nt:unstructured`

1. 在下建立節點 `htmlPasteRules`，以保留允許的基本格式的詳細資訊：

   * **名称** `allowBasics`
   * **类型** `nt:unstructured`

1. 若要控制所接受的個別格式，請在 `allowBasics` 節點：

   * **名称** `bold`
   * **名称** `italic`
   * **名称** `underline`
   * **名稱** `anchor` （適用於連結和已命名的錨點）
   * **名称** `image`

   所有屬性都是 **型別** `Boolean`，因此在適當的 **值** 您可以選取或移除核取記號來啟用或停用該功能。

   >[!NOTE]
   >
   >如果未明確定義，則會使用預設值true並接受格式。

1. 其他格式也可以使用其他屬性或節點範圍來定義，這些屬性或節點也套用至 `htmlPasteRules` 節點。 儲存所有變更。

您可以使用下列屬性 `htmlPasteRules`.

| 属性 | 类型 | 描述 |
|---|---|---|
| `allowBlockTags` | 字符串 | 定義允許的區塊標籤清單。 一些可能的區塊標籤包括： <ul> <li>標題(h1、h2、h3)</li> <li>段落(p)</li> <li>清單(ol、ul)</li> <li>表格（表格）</li> </ul> |
| `fallbackBlockTag` | 字符串 | 定義區塊標籤，此標籤用於任何區塊中不包含區塊標籤 `allowBlockTags`. `p` 大多數情況下就足夠了。 |
| 表格 | nt:unstructured | 定義貼上表格時的行為。 此節點必須具有屬性 `allow` （輸入布林值）以定義是否允許貼上表格。 如果「允許」設為 `false`，您必須指定屬性 `ignoreMode` （輸入字串）以定義如何處理貼上的表格內容。 的有效值 `ignoreMode` 為： <ul> <li>`remove`：移除表格內容。</li> <li>`paragraph`：將表格儲存格轉換為段落。</li> </ul> |
| list | nt:unstructured | 定義貼上清單時的行為。 必須具有屬性 `allow` （輸入布林值）以定義是否允許貼上清單。 若 `allow` 設為 `false`，您必須指定屬性 `ignoreMode` （輸入String）以定義如何處理貼上的任何清單內容。 的有效值 `ignoreMode` 為： <ul><li> `remove`：移除清單內容。</li> <li>`paragraph`：將清單專案轉換為段落。</li> </ul> |

有效的範例 `htmlPasteRules` 結構如下。

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

## 設定文字樣式 {#textstyles}

作者可以套用樣式來變更部分文字的外觀。 樣式是以您在CSS樣式表中預先定義的CSS類別為基礎。 樣式化內容包含在 `span` 標籤使用 `class` 屬性以參照CSS類別。 例如：`<span class=monospaced>Monospaced Text Here</span>`。

第一次啟用樣式外掛程式時，沒有可用的預設樣式。 快顯清單是空的。 若要為作者提供樣式，請執行下列動作：

* 啟用「樣式」下拉式選取器。
* 指定樣式表的位置。
* 指定可從「樣式」下拉式清單中選取的個別樣式。

對於之後的設定，如要新增更多樣式，請僅依照指示參考新的樣式表並指定其他樣式。

>[!NOTE]
>
>您可以定義樣式 [表格或表格儲存格](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles). 這些設定需要單獨的程式。

### 啟用「樣式」下拉式選擇器清單 {#styleselectorlist}

若要這麼做，請啟用樣式外掛程式。

1. 在您的元件中，導覽至節點 `<rtePlugins-node>/styles`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 建立 `features` 上的屬性 `styles` 節點：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星號）

1. 儲存所有變更。

>[!NOTE]
>
>啟用樣式外掛程式後，「樣式」下拉式清單會顯示在編輯對話方塊中。 但是，清單是空的，因為沒有設定樣式。

### 指定樣式表位置 {#locationofstylesheet}

然後，指定您要參照的樣式表位置：

1. 導覽至文字元件的根節點，例如 `/apps/<myProject>/components/text`.
1. 新增屬性 `externalStyleSheets` 至的父節點 `<rtePlugins-node>`：

   * **名称** `externalStyleSheets`
   * **型別** `String[]` (多字串；按一下 **多個** 在CRXDE中)
   * **值** 每個要包含的樣式表的路徑和檔案名稱。 使用存放庫路徑。

   >[!NOTE]
   >
   >您稍後可隨時新增參照至其他樣式表。

1. 儲存所有變更。

>[!NOTE]
>
>在對話方塊（傳統UI）中使用RTE時，您可能想要指定針對RTF編輯最佳化的樣式表。 由於技術限制，編輯器中的CSS上下文會遺失，因此您可能想要模擬此上下文以改善WYSIWYG體驗。
>
>RTF編輯器使用容器DOM元素，ID為 `CQrte` 可提供不同的樣式進行檢視和編輯：
>
>`#CQ td {`
>` // defines the style for viewing }`
>
>`#CQrte td {`
>` // defines the style for editing }`

### 在彈出式清單中指定可用的樣式 {#stylesindropdown}

1. 在元件定義中，導覽至節點 `<rtePlugins-node>/styles`，在中建立 [啟用樣式下拉式選擇器](#styleselectorlist).
1. 在節點下 `styles`，建立新節點(也稱為 `styles`)以保留可供使用的清單：

   * **名称** `styles`
   * **类型** `cq:WidgetCollection`

1. 在下建立新節點 `styles` 代表個別樣式的節點：

   * **名稱**，您可以指定名稱，但名稱應適合樣式
   * **类型** `nt:unstructured`

1. 新增屬性 `cssName` 至此節點以參照CSS類別：

   * **名称** `cssName`
   * **类型** `String`
   * **值** CSS類別的名稱(沒有前置詞&#39;.&#39;；例如， `cssClass` 而非 `.cssClass`)

1. 新增屬性 `text` 至相同節點；這會定義選取方塊中顯示的文字：

   * **名称** `text`
   * **类型** `String`
   * **值** 樣式的描述；顯示在「樣式」下拉式選取方塊中。

1. 保存更改。

   對每個所需樣式重複上述步驟。

### 設定RTE以取得日文的最佳分行符號 {#jpwordwrap}

使用AEM編寫日文語言內容的作者可將樣式套用至字元，以避免在不需要分行符號的情況下出現分行符號。 這可讓作者讓句子在所需位置中斷。 此功能的樣式是以CSS樣式表中預先定義的CSS類別為基礎。

>[!NOTE]
>
>此功能至少需要AEM 6.5 Service Pack 1。

若要建立作者可套用至日文文字的樣式，請遵循下列步驟：

1. 在styles節點下建立新節點。 另請參閱 [指定新樣式](#stylesindropdown).
   * 名称: `jpn-word-wrap`
   * 类型: `nt:unstructure`

1. 新增屬性 `cssName` 至節點以參照CSS類別。 此類別名稱是日文自動換行功能的保留名稱。
   * 名称: `cssName`
   * 类型: `String`
   * 值： `jpn-word-wrap` (無前置詞 `.`)

1. 將屬性文字新增至相同的節點。 值是作者在選取樣式時看到的樣式名稱。
   * 名稱： `text`
*型別： 
`String`
   * 价值: `Japanese word-wrap`

1. 建立樣式表並指定其路徑。 另請參閱 [指定樣式表位置](#locationofstylesheet). 將下列內容新增至樣式表。 視需要變更背景顏色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![讓作者可以使用日文自動換行功能的樣式表](assets/rte_jpwordwrap_stylesheet.jpg)

## 設定段落格式 {#paraformats}

在RTE中編寫的任何文字都會放置在區塊標籤中，預設為 `<p>`. 藉由啟用 `paraformat` 此外掛程式，您可使用下拉式選取清單來指定可指派給段落的其他區塊標籤。 段落格式會透過指定正確的區塊標籤來決定段落型別。 作者可使用「格式」選擇器來選取和指派這些變數。 範例區塊標籤包括標準段落 &lt;p> 和標題 &lt;h1>， &lt;h2>、等等。

>[!CAUTION]
>
>此外掛程式不適用於具有複雜結構的內容，例如清單或表格。

>[!NOTE]
>
>如果區塊標籤，例如 &lt;hr> 標籤，無法指派給段落，這不是引數格式外掛程式的有效使用案例。

第一次啟用「段落格式」外掛程式時，沒有可用的預設段落格式。 快顯清單是空的。 若要為作者提供段落格式，請執行下列動作：

* 啟用「格式」下拉式選擇器清單。
* 指定可從下拉式清單中選取作為段落格式的區塊標籤。

對於稍後（重新）的設定，例如要新增更多格式，請僅遵循指示的相關部分。

### 啟用「格式」下拉式選取器 {#formatselectorlist}

首先啟用paraformat外掛程式：

1. 在您的元件中，導覽至節點 `<rtePlugins-node>/paraformat`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 建立 `features` 上的屬性 `paraformat` 節點：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星號）

>[!NOTE]
如果未進一步設定外掛程式，則會啟用下列預設格式：
* 段落 ( `<p>`)
* 标题 1 ( `<h1>`)
* 标题 2 ( `<h2>`)
* 标题 3 ( `<h3>`)
>


>[!CAUTION]
設定RTE的段落格式時，請勿移除段落標籤 &lt;p> 作為格式選項。 如果 `<p>` 標籤已移除，內容作者無法選取 **段落格式** 選項，即使已設定其他格式亦然。

### 指定可用的段落格式 {#paraformatsindropdown}

段落格式可透過以下方式選取：

1. 在元件定義中，導覽至節點 `<rtePlugins-node>/paraformat`，在中建立 [啟用格式下拉式選擇器](#styleselectorlist).
1. 在 `paraformat` 節點建立新節點，以儲存格式清單：

   * **名称** `formats`
   * **类型** `cq:WidgetCollection`

1. 在下建立新節點 `formats` 節點，這會保留個別格式的詳細資料：

   * **名稱**，您可以指定名稱，但它應該適合格式（例如myparagraph、myheading1）。
   * **类型** `nt:unstructured`

1. 將屬性新增至此節點，以定義使用的區塊標籤：

   * **名称** `tag`
   * **类型** `String`
   * **值** 格式的區塊標籤；例如：p、h1、h2等。

      您不需要輸入分隔角括弧。

1. 若要讓描述性文字出現在下拉式清單中，請在相同節點新增另一個屬性：

   * **名称** `description`
   * **类型** `String`
   * **值** 此格式的描述性文字；例如，段落、標題1、標題2等。 此文字會顯示在「格式」選取項清單中。

1. 保存更改。

   針對每個所需的格式重複這些步驟。

>[!CAUTION]
如果您定義自訂格式，預設格式(`<p>`， `<h1>`， `<h2>`、和 `<h3>`)已移除。 重新建立 `<p>` 格式，因為它是預設格式。

## 設定特殊字元 {#spchar}

在標準AEM安裝中，當 `misctools` 外掛程式已啟用特殊字元(`specialchars`)預設選項可立即使用；例如，版權和商標符號。

您可以設定RTE，讓自己的字元選擇可供使用；藉由定義不同的字元或整個序列。

>[!CAUTION]
新增您自己的特殊字元會覆寫預設選取範圍。 如有需要，可在您自己的選取範圍中（重新）定義這些字元。

### 定義單一字元 {#definesinglechar}

1. 在您的元件中，導覽至節點 `<rtePlugins-node>/misctools`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 建立 `features` 上的屬性 `misctools` 節點：

   * **名称** `features`
   * **类型** `String[]`
   * **值** `specialchars`

          (或 `String / *` 如果套用此外掛程式的所有功能)

1. 下 `misctools` 建立節點以儲存特殊字元設定：

   * **名称** `specialCharsConfig`
   * **类型** `nt:unstructured`

1. 下 `specialCharsConfig` 建立另一個節點來儲存字元清單：

   * **名称** `chars`
   * **类型** `nt:unstructured`

1. 下 `chars` 新增節點以保留個別字元定義：

   * **名稱** 您可以指定名稱，但名稱應反映字元；例如，一半。
   * **类型** `nt:unstructured`

1. 將下列屬性新增至此節點：

   * **名称** `entity`
   * **类型** `String`
   * **值** 所需字元的HTML表示；例如， `&189;` 為分數的一半。

1. 保存更改。

在CRXDE中，儲存屬性後，會顯示表示的字元。 請參閱下方一半的範例。 重複上述步驟，讓作者可以使用更多特殊字元。

![在CRXDE中，新增單一字元，以供RTE工具列使用](assets/chlimage_1-106.png "在CRXDE中，新增單一字元，以供RTE工具列使用")

### 定義字元範圍 {#definerangechar}

1. 使用中的步驟1至3 [定義單一字元](#definesinglechar).
1. 下 `chars` 新增節點以保留字元範圍的定義：

   * **名稱** 您可以指定名稱，但應反映字元範圍；例如，鉛筆。
   * **类型** `nt:unstructured`

1. 在此節點下（根據特殊字元範圍命名）新增以下兩個屬性：

   * **名称** `rangeStart`

      **类型** `Long`
      **值** 此 [Unicode](https://unicode.org/) 表示範圍中第一個字元（十進位）

   * **名称** `rangeEnd`

      **类型** `Long`
      **值** 此 [Unicode](https://unicode.org/) 表示範圍中最後一個字元（十進位）

1. 保存更改。

   例如，定義9998到10000之間的範圍時，會提供下列字元。

   ![在CRXDE中，定義要在RTE中可用的字元範圍](assets/chlimage_1-107.png)

   *圖：在CRXDE中，定義在RTE中可用的字元範圍*

   ![RTE中可用的特殊字元會在快顯視窗中向作者顯示](assets/rtepencil.png "RTE中可用的特殊字元會在快顯視窗中向作者顯示")

## 設定表格樣式 {#tablestyles}

樣式通常會套用至文字，但也可以套用一組個別的樣式至表格或幾個表格儲存格。 作者可從「儲存格屬性」或「表格屬性」對話方塊的「樣式選取器」方塊中使用此類樣式。 在文字元件（或衍生專案）中編輯表格時，樣式而非在標準表格元件中可用。

>[!NOTE]
您只能為傳統UI定義表格和儲存格的樣式。

>[!NOTE]
在RTE元件中或從RTE元件複製和貼上表格會依瀏覽器而定。 並非所有瀏覽器都支援此功能。 根據表格結構和瀏覽器，您可能會得到不同的結果。 例如，當您在Mozilla Firefox的Classic UI和Touch UI中複製並貼上RTE元件中的表格時，不會保留表格的版面。

1. 在您的元件內，導覽至節點 `<rtePlugins-node>/table`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 建立 `features` 上的屬性 `table` 節點：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星號）

   >[!NOTE]
   如果您不想啟用所有表格功能，您可以建立 `features` 屬性為：
   * **类型** `String[]`
   * **值**(s)視需要執行下列其中一項或兩項作業：
      * `table` 允許編輯表格屬性；包括樣式。
      * `cellprops` 允許編輯儲存格屬性，包括樣式。


1. 定義CSS樣式表的位置以參考這些樣式表。 另請參閱 [指定樣式表的位置](#locationofstylesheet) 因為這與定義 [文字樣式](#textstyles). 如果您定義了其他樣式，則可以定義位置。
1. 在 `table` 節點建立以下新節點（視需要）：

   * 定義整個表格的樣式(可在下列位置取得： **表格屬性**)：

      * **名称** `tableStyles`
      * **类型** `cq:WidgetCollection`
   * 定義個別儲存格的樣式(位於 **儲存格屬性**)：

      * **名称** `cellStyles`
      * **类型** `cq:WidgetCollection`


1. 建立新節點(在 `tableStyles` 或 `cellStyles` 節點)，以代表個別樣式：

   * **名稱** 您可以指定名稱，但應反映樣式。
   * **类型** `nt:unstructured`

1. 在此節點上建立屬性：

   * 定義要參考的CSS樣式

      * **名称** `cssName`
      * **类型** `String`
      * **值** CSS類別的名稱（不含前置字元） `.`例如， `cssClass` 而非 `.cssClass`)
   * 定義要在下拉式選擇器中顯示的描述性文字

      * **名称** `text`
      * **类型** `String`
      * **值** 要顯示在選取專案清單中的文字


1. 儲存所有變更。

對每個所需樣式重複上述步驟。

### 在表格中設定隱藏標題以取得協助工具 {#hiddenheader}

有時候，您可以建立資料表，但欄標頭中沒有視覺文字，假設標頭的目的是由欄與其他欄的視覺關係所暗示。 在此情況下，必須在標題儲存格的儲存格中提供隱藏的內部文字，以允許熒幕閱讀程式和其他輔助技術協助有各種需求的閱讀程式瞭解欄的用途。

為了在這類情況下增強協助工具，RTE支援隱藏的標題儲存格。 此外，它提供與表格中隱藏標題相關的組態設定。 這些設定可讓您在編輯和預覽模式中，對隱藏的標題套用CSS樣式。 為協助作者在編輯模式中識別隱藏的標頭，請在程式碼中包含下列引數：

* `hiddenHeaderEditingCSS`：指定在編輯RTE時套用至隱藏標題儲存格的CSS類別名稱。
* `hiddenHeaderEditingStyle`：指定在編輯RTE時套用至隱藏標題儲存格的樣式字串。

如果您在程式碼中同時指定CSS和Style字串，則CSS類別會優先於樣式字串，並可能覆寫Style字串所做的任何設定變更。

若要協助作者在預覽模式下對隱藏的標題套用CSS，您可以在程式碼中包含下列引數：

* `hiddenHeaderClassName`：指定在預覽模式中套用至隱藏標題儲存格的CSS類別名稱。
* `hiddenHeaderStyle`：指定在預覽模式下套用至隱藏標題儲存格的樣式字串。

如果您在程式碼中同時指定CSS和Style字串，則CSS類別會優先於樣式字串，並可能覆寫Style字串所做的任何設定變更。

## 新增拼字檢查器的字典 {#adddict}

啟動spellcheck外掛程式時，RTE會使用每個適當語言的字典。 接著，系統會根據網站的語言，例如採用子樹狀結構的language屬性或從URL擷取語言，來選取這些專案。 此 `/en/` 分支會勾選為英文，而 `/de/` 分支為德文。

>[!NOTE]
訊息 `Spell checking failed` 如果嘗試檢查未安裝的語言，則會顯示。 標準字典位於 `/libs/cq/spellchecker/dictionaries`，以及適當的Readme檔案。 請勿修改檔案。

標準AEM安裝包含美式英文字典(`en_us`)和英式英文(`en_gb`)。 若要新增更多字典，請按照以下步驟操作。

1. 導覽至頁面 [https://extensions.openoffice.org/](https://extensions.openoffice.org/).

1. 執行下列任一項作業，尋找您選擇的語言字典：

   * 搜尋您所選語言的字典。 在字典頁面上，找到原始來源或作者網頁的連結。 在這樣的頁面上找到v2.x的字典檔案。
   * 搜尋v2.x字典檔案： [https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries).

1. 下載含有拼字定義的封存。 解壓縮檔案系統上的封存內容。

   >[!CAUTION]
   僅字典 `MySpell` 支援OpenOffice.org v2.0.1或更舊版本的格式。 由於字典現在是封存檔案，建議您下載後驗證封存。

1. 找到.aff和.dic檔案。 將檔案名稱保留為小寫。 例如， `de_de.aff` 和 `de_de.dic`.
1. 將.aff和.dic檔案載入存放庫，網址為 `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
RTE拼字檢查程式可隨選使用。 當您開始輸入文字時，它不會自動執行。 若要執行拼字檢查程式，請按一下 [!UICONTROL 拼字檢查] （從工具列）。 RTE會檢查單字的拼字，並反白拼錯的單字。
如果您合併拼字檢查器建議的任何變更，文字的狀態會變更，且拼字錯誤的單字不再反白。 若要執行拼字檢查程式，請再次點選/按一下「拼字檢查程式」按鈕。

## 設定還原和重做動作的歷史記錄大小 {#undohistory}

RTE可讓作者還原或重做最後的幾項編輯。 依預設，歷史記錄中會儲存50項編輯。 您可以視需要設定此值。

1. 在您的元件內，導覽至節點 `<rtePlugins-node>/undo`. 如果節點不存在，請建立這些節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 於 `undo` 節點建立屬性：

   * **名称** `maxUndoSteps`
   * **类型** `Long`
   * **值** 您想要儲存在記錄中的還原步驟數。 預設值為50。 使用 `0` 以完全停用還原/重做。

1. 保存更改。

## 設定索引標籤大小 {#tabsize}

在文字中按下Tab字元時，會插入預先定義的空格數；依預設，這是三個不間斷的空格和一個空格。

若要定義定位點大小，請執行下列動作：

1. 在您的元件中，導覽至節點 `<rtePlugins-node>/keys`. 如果節點不存在，請建立節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 於 `keys` 節點建立屬性：

   * **名称** `tabSize`
   * **类型** `String`
   * **值** 用於製表器的空格字元數

1. 保存更改。

## 設定縮排邊界 {#indentmargin}

啟用縮排（預設）時，您可以定義縮排的大小：

>[!NOTE]
此縮排大小只會套用至文字的段落（區塊），不會影響實際清單的縮排。

1. 在您的元件內，導覽至節點 `<rtePlugins-node>/lists`. 如果節點不存在，請建立這些節點。 如需詳細資訊，請參閱 [啟動外掛程式](#activateplugin).
1. 於 `lists` 節點建立 `identSize` 引數：

   * **名称**: `identSize`
   * **类型**: `Long`
   * **值**：縮排邊界所需的畫素數。

## 設定可編輯空間的高度 {#editablespace}

>[!NOTE]
這僅適用於在對話方塊中使用RTE （而非在傳統UI中就地編輯）時。

您可以定義元件對話方塊中顯示的可編輯空間的高度：

1. 於 `../items/text` 節點建立新屬性：

   * **名称** `height`
   * **类型** `Long`
   * **值** 編輯畫布的高度（畫素）。

   >[!NOTE]
   這不會變更對話方塊視窗的高度。

1. 保存更改。

## 設定連結的樣式和通訊協定 {#linkstyles}

在AEM中新增連結時，您可以定義：

* 要使用的CSS樣式
* 自動接受的通訊協定

若要設定如何將連結從其他程式新增至AEM，請定義HTML規則。

1. 使用CRXDE Lite找到專案的文字元件。
1. 在與相同的層級建立新節點 `<rtePlugins-node>`，也就是說，在的父節點下建立節點 `<rtePlugins-node>`：

   * **名称** `htmlRules`
   * **类型** `nt:unstructured`

   >[!NOTE]
   此 `../items/text` 節點具有屬性：
   * **名称** `xtype`
   * **类型** `String`
   * **值** `richtext`

   的位置 `../items/text` 節點會依對話方塊的結構而有所不同；有兩個範例為 `/apps/myProject>/components/text/dialog/items/text` 和 `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. 下 `htmlRules`，建立新節點。

   * **名称** `links`
   * **类型** `nt:unstructured`

1. 在 `links` 節點會視需要定義屬性：

   * 內部連結的CSS樣式：

      * **名称** `cssInternal`
      * **类型** `String`
      * **值** CSS類別的名稱(沒有前置詞&#39;.&#39;；例如， `cssClass` 而非 `.cssClass`)
   * 外部連結的CSS樣式

      * **名称** `cssExternal`
      * **类型** `String`
      * **值** CSS類別的名稱(沒有前置詞&#39;.&#39;；例如， `cssClass` 而非 `.cssClass`)
   * 有效陣列 **通訊協定**. 支援的通訊協定為 `http://`， `https://`， `file://`、和 `mailto:`.

      * **名称** `protocols`
      * **类型** `String[]`
      * **值**(s)一或多個通訊協定
   * **defaultprotocol** (型別的屬性 **字串**)：使用者未明確指定時使用的通訊協定。

      * **名称** `defaultProtocol`
      * **类型** `String`
      * **值**(s)一或多個預設通訊協定
   * 如何處理連結目標屬性的定義。 建立新節點：

      * **名称** `targetConfig`
      * **类型** `nt:unstructured`

      在節點上 `targetConfig`：定義必要的屬性：

      * 指定目標模式：

         * **名称** `mode`
         * **类型** `String`)
         * **值**(s) ：

            * `auto`：表示已選擇自動目標

               (由 `targetExternal` 外部連結或的屬性 `targetInternal` 內部連結使用)。

            * `manual`：不適用於此內容
            * `blank`：不適用於此內容
      * 內部連結的目標：

         * **名称** `targetInternal`
         * **类型** `String`
         * **值** 內部連結的目標(僅在模式為 `auto`)
      * 外部連結的目標：

         * **名称** `targetExternal`
         * **类型** `String`
         * **值** 外部連結的目標(僅在模式為 `auto`)。








1. 儲存所有變更。
