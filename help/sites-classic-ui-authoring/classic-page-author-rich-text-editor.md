---
title: 富文本编辑器
description: RTF編輯器是將文字內容輸入至AEM的基本建置區塊。
uuid: 4bcce45a-e14f-41b7-8c6f-89d1e1bb595c
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: ccc0e434-8847-4e12-8a18-84b55fb2964b
docset: aem65
exl-id: 5623dcf4-bda9-4dee-ace3-5a1f6057e96c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 1%

---

# 富文本编辑器 {#rich-text-editor}

RTF編輯器是將文字內容輸入至AEM的基本建置區塊。 它構成各種元件的基礎，包括：

* 文本
* 文本图像
* 表

## 富文本编辑器 {#rich-text-editor-1}

所見即所得編輯對話方塊提供廣泛的功能：

![cq55_rte_basicchars](assets/cq55_rte_basicchars.png)

>[!NOTE]
>
>可用的功能可針對個別專案進行設定，因此安裝時可能會有所不同。

## 就地编辑 {#in-place-editing}

除了對話方塊式RTF編輯模式外，AEM還提供就地編輯模式，允許直接編輯顯示在頁面版面中的文字。

在段落上按兩下（緩慢連按兩下）以進入就地編輯模式（元件邊框現在將為橘色）。

您將能夠直接編輯頁面上的文字，而不是在對話方塊視窗內。 只需進行變更，系統就會自動儲存變更。

![cq55_rte_inlineediting](assets/cq55_rte_inlineediting.png)

>[!NOTE]
>
>如果您已開啟內容尋找器，則含有RTE格式選項的工具列將顯示在索引標籤的頂端（如上所述）。
>
>如果內容尋找器未開啟，則不會顯示工具列。

目前，系統已為產生的頁面元素啟用就地編輯模式。 **文字** 和 **標題** 元件。

>[!NOTE]
>
>此 [!UICONTROL 標題] 元件設計為包含不含分行符號的簡短文字。 在「就地編輯」模式下編輯標題時，輸入分行符號將會開啟新的 **文字** 標題下方的元件。

## RTF編輯器的功能 {#features-of-the-rich-text-editor}

RTF編輯器提供了一系列功能，包括 [視設定而定](/help/sites-administering/rich-text-editor.md) 個別元件的ID。 這些功能適用於觸控最佳化的UI和傳統UI。

### 基本字元格式 {#basic-character-formats}

![](do-not-localize/cq55_rte_basicchars.png)

您可以在此處將格式套用至您選取（反白顯示）的字元；有些選項也有快捷鍵：

* 粗體(Ctrl-B)
* 斜體(Ctrl-I)
* 底線(Ctrl-U)
* 下标
* 上标

![cq55_rte_basicchars_use](assets/cq55_rte_basicchars_use.png)

所有內容都會以切換方式運作，因此重新選取會移除格式。

### 預先定義的樣式和格式 {#predefined-styles-and-formats}

![cq55_rte_stylesparagraph](assets/cq55_rte_stylesparagraph.png)

您的安裝可包含預先定義的樣式和格式。 這些功能可搭配 **[!UICONTROL 樣式]** 和 **[!UICONTROL 格式]** 下拉式清單，並可套用至您已選取的文字。

樣式可套用至特定字串（與CSS相關的樣式）：

![cq55_rte_styles_use](assets/cq55_rte_styles_use.png)

而格式會套用至整個文欄位落(格式是以HTML為基礎)：

![cq55_rte_paragraph_use](assets/cq55_rte_paragraph_use.png)

特定格式只能變更(預設為 **[!UICONTROL 段落]**)。

可以移除樣式；將游標置於已套用樣式的文字內，然後按一下移除圖示：

>[!CAUTION]
>
>實際上不要重新選取已套用樣式的文字，否則圖示會停用。

### 剪下、複製、貼上 {#cut-copy-paste}

![](do-not-localize/cq55_rte_cutcopypaste.png)

的標準函式 **[!UICONTROL 剪下]** 和 **[!UICONTROL 複製]** 可用。 幾種口味 **[!UICONTROL 貼上]** 提供以滿足不同格式的需求。

* 剪下(Ctrl-X)
* 複製(Ctrl-C)
* 貼上這是元件的預設貼上機制(Ctrl-V)；當現成安裝時，此機制會設定為 [!UICONTROL 從Word貼上].

* 貼上成文字：將所有的樣式和格式都刪除，只貼上純文字。

* 從Word貼上：這樣會將內容貼上為HTML（包含一些必要的重新格式化）。

### 還原，重做 {#undo-redo}

![](do-not-localize/cq55_rte_undoredo.png)

AEM會依時間順序保留目前元件中最後50個動作的記錄。 如有需要，這些動作可以嚴格順序復原（然後重做）。

>[!CAUTION]
>
>歷史記錄僅會保留目前的編輯工作階段。 每次開啟元件進行編輯時，都會重新啟動它。

>[!NOTE]
>
>預設任務數為50。 您的安裝可能會有所不同。

### 对齐方式 {#alignment}

![](do-not-localize/cq55_rte_alignment.png)

文字可以靠左、置中或靠右對齊。

![cq55_rte_alignment_use](assets/cq55_rte_alignment_use.png)

### 缩进 {#indentation}

![](do-not-localize/cq55_rte_indent.png)

段落的縮排可以增加或減少。 所選段落將縮排，輸入的任何新文字將保留目前的縮排層級。

![cq55_rte_indent_use](assets/cq55_rte_indent_use.png)

### 列表 {#lists}

![](do-not-localize/cq55_rte_lists.png)

專案符號和編號清單都可以在文字中建立。 選取清單型別並開始鍵入或反白要轉換的文字。 在這兩種情況下，換行字元都會開始新的清單專案。

巢狀清單可以透過縮排一個或多個清單專案來達成。

只需將游標置於清單內，然後選取其他樣式，即可變更清單的樣式。 子清單也可以有與包含清單不同的樣式。 一旦建立子清單後（透過縮排），即可套用此選項。

![cq55_rte_lists_use](assets/cq55_rte_lists_use.png)

### 链接 {#links}

![](do-not-localize/cq55_rte_links.png)

反白必要文字，然後按一下超連結圖示，會產生指向URL的連結（位於您的網站內或外部位置）：

![](do-not-localize/chlimage_1-9.png)

對話方塊可讓您指定目標URL，以及是否應在新視窗中開啟。

![cq55_rte_link_use](assets/cq55_rte_link_use.png)

您可以：

* 直接輸入URI
* 使用網站地圖在您的網站內選取頁面
* 輸入URI，然後附加目標錨點；例如。 `www.TargetUri.org#AnchorName`
* 僅輸入錨點（參照「目前頁面」）；例如， `#anchor`
* 在內容尋找器中搜尋頁面，然後將頁面圖示拖放至「超連結」對話方塊中

>[!NOTE]
>
>URI可附加任何針對您的安裝所設定的通訊協定。 在標準安裝中，這些是 `https://`， `ftp://`、和 `mailto:`. 未針對您的安裝設定的通訊協定將被拒絕並標籤為無效。

若要中斷連結位置，將游標置於連結文字中的任何位置，然後按一下 [!UICONTROL 取消連結] 圖示：

![](do-not-localize/chlimage_1-10.png)

### 锚点 {#anchors}

![](do-not-localize/cq55_rte_anchor.png)

您可以透過定位游標或選取某些文字，在文字內的任何位置建立錨點。 然後按一下 **錨點** 圖示以開啟對話方塊。

輸入錨點的名稱，然後按一下 **確定** 以儲存。

![cq55_rte_anchor_use](assets/cq55_rte_anchor_use.png)

當編輯元件時會顯示錨點，且現在可以在連結的目標中使用。

![chlimage_1-104](assets/chlimage_1-104.png)

### 尋找和取代 {#find-and-replace}

![](do-not-localize/cq55_rte_findreplace.png)

AEM同時提供 **尋找** 和 **Replace** （尋找和取代）函式。

兩者都有 **尋找下一個** 按鈕來搜尋所指定文字的開啟元件。 您也可以指定是否需要比對大小寫（大/小）。

搜尋一律會從文字內目前的游標位置開始。 到達元件結尾時，會出現一則訊息，通知您下一個搜尋操作將從頂部開始。

![cq55_rte_find_use](assets/cq55_rte_find_use.png)

此 **Replace** 選項可讓您 **尋找**，則 **Replace** 具有指定文字的個別執行個體，或 **全部取代** 目前元件中的例證。

![cq55_rte_findreplace_use](assets/cq55_rte_findreplace_use.png)

### 图像 {#images}

您可以從內容尋找器拖曳影像，以將影像新增至文字。

![cq55_rte_image_use](assets/cq55_rte_image_use.png)

>[!NOTE]
>
>AEM也提供專門的元件，以提供更詳細的影像設定。 例如 **影像** 和 **文字影像** 元件可供使用。

### 拼字檢查 {#spelling-checker}

![](do-not-localize/cq55_rte_spellchecker.png)

拼字檢查程式會檢查目前元件中的所有文字。

任何錯誤的拼字都會反白顯示：

![cq55_rte_spellchecker_use](assets/cq55_rte_spellchecker_use.png)

>[!NOTE]
>
>拼字檢查程式會使用子樹狀結構的language屬性或從URL擷取語言，以在網站的語言中運作。 例如 `en` 將檢查分支的英文和 `de` 德文分支。

### 表格 {#tables}

表格可供兩種方式使用：

* 作為 **表格** 元件

   ![chlimage_1-105](assets/chlimage_1-105.png)

* 從 **文字** 元件

   ![](do-not-localize/chlimage_1-11.png)

   >[!NOTE]
   >
   >雖然RTE中已有表格，但建議您使用 **表格** 建立表格時的元件。

在 **文字** 和 **表格** 元件表格功能可透過在表格內按一下前後關聯選單（通常是按滑鼠右鍵）來使用；例如：

![cq55_rte_tablemenu](assets/cq55_rte_tablemenu.png)

>[!NOTE]
>
>在 **表格** 元件外，也提供專門的工具列，包括各種標準RTF編輯器功能，以及表格特定功能的子集。

表格的特定功能包括：

* [表格屬性](#table-properties)
* [儲存格屬性](#cell-properties)
* [新增或刪除列](#add-or-delete-rows)
* [新增或刪除欄](#add-or-delete-columns)
* [選取整列或整欄](#selecting-entire-rows-or-columns)
* [合併儲存格](#merge-cells)
* [拆分单元格](#split-cells)
* [巢狀表格](#creating-nested-tables)
* [移除表格](#remove-table)

#### 表格屬性 {#table-properties}

![cq55_rte_tableproperties_icon](assets/cq55_rte_tableproperties_icon.png)

在按一下之前，可以設定表格的基本屬性 **確定** 若要儲存：

![cq55_rte_tableproperties_dialog](assets/cq55_rte_tableproperties_dialog.png)

* **寬度**：表格的總寬度。

* **高度**：表格的總高度。

* **邊框**：表格邊框的大小。

* **儲存格邊距**：這會定義儲存格內容與其邊界之間的空白字元。

* **儲存格間距**：這會定義儲存格之間的距離。

>[!NOTE]
>
>有些儲存格屬性（例如「寬度」和「高度」）可定義為畫素或百分比。

>[!CAUTION]
>
>Adobe建議您為表格定義寬度。

#### 儲存格屬性 {#cell-properties}

![cq55_rte_cellproperties_icon](assets/cq55_rte_cellproperties_icon.png)

可以設定特定儲存格或一系列儲存格的屬性：

![cq55_rte_cellproperties_dialog](assets/cq55_rte_cellproperties_dialog.png)

* **宽度**
* **高度**
* **水準對齊**  — 左、中或右
* **垂直對齊**  — 頂端、中間、底部或基準線
* **儲存格型別** — 資料或標題
* **套用至：** 單一儲存格、整列、整欄

#### 新增或刪除列 {#add-or-delete-rows}

![cq55_rte_rows](assets/cq55_rte_rows.png)

可在目前列上方或下方新增列。

也可以刪除目前列。

#### 新增或刪除欄 {#add-or-delete-columns}

![cq55_rte_columns](assets/cq55_rte_columns.png)

欄可以新增到目前欄的左側或右側。

也可以刪除目前欄。

#### 選取整列或整欄 {#selecting-entire-rows-or-columns}

![chlimage_1-106](assets/chlimage_1-106.png)

選取整個目前列或欄。 然後可以使用特定動作（例如合併）。

#### 合併儲存格 {#merge-cells}

![cq55_rte_cellmerge](assets/cq55_rte_cellmerge.png) ![cq55_rte_cellmerge-1](assets/cq55_rte_cellmerge-1.png)

* 如果您選取了儲存格群組，可以將這些儲存格合併為一個儲存格。
* 如果您只選取了一個儲存格，則可以將它與右側或下方的儲存格合併。

#### 拆分单元格 {#split-cells}

![cq55_rte_cellsplit](assets/cq55_rte_cellsplit.png)

選取要分割的單一儲存格：

* 水準分割儲存格會在目前欄內產生目前儲存格右側的新儲存格。
* 垂直分割儲存格會在目前儲存格下產生新儲存格，但會在目前列內產生。

#### 建立巢狀表格 {#creating-nested-tables}

![chlimage_1-107](assets/chlimage_1-107.png)

建立巢狀表格時，會在目前儲存格內建立新的獨立表格。

>[!NOTE]
>
>某些其他行為取決於瀏覽器：
>
>* Windows IE：使用Ctrl+按住滑鼠鍵（通常是左鍵）以選取多個儲存格。
>* Firefox：拖曳指標以選取儲存格範圍。


#### 移除表格 {#remove-table}

![cq55_rte_removetable](assets/cq55_rte_removetable.png)

使用選項將表格從 **[!UICONTROL 文字]** 元件。

### 特殊字符 {#special-characters}

![](do-not-localize/cq55_rte_specialchars.png)

RTF編輯器可使用特殊字元；這些字元可能會因您的安裝而異。

![cq55_rte_specialchars_use](assets/cq55_rte_specialchars_use.png)

使用滑鼠懸停來檢視字元的放大版本，然後按一下以將其包含在文字中的目前位置。

### 來源編輯模式 {#source-editing-mode}

![](do-not-localize/cq55_rte_sourceedit.png)

來源編輯模式可讓您檢視及編輯元件的基礎HTML。

所以文字：

![cq55_rte_sourcemode_1](assets/cq55_rte_sourcemode_1.png)

在來源模式中看起來會像這樣（來源通常更長，所以您必須捲動）：

![cq55_rte_sourcemode_2](assets/cq55_rte_sourcemode_2.png)

>[!CAUTION]
>
>離開來源模式時，AEM會進行某些驗證檢查（例如，確保文字正確包含/巢狀內嵌在區塊中）。 這可能會導致編輯內容變更。
