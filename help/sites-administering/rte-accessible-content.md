---
title: 設定RTF編輯器以建立無障礙的網頁和網站。
description: 設定RTF編輯器以建立無障礙的網頁和網站。
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 設定RTE以建立無障礙的網頁和網站 {#configure-rte-for-accessibility}

Adobe Experience Manager支援符合各種協助工具標準的多種標準協助工具功能。 此外，開發人員可以自訂或擴充，以提供有助於使用使用RTF編輯器(RTE)的Experience Manager元件建立無障礙內容的功能。

在設計網頁並將內容新增至頁面時，內容開發人員和作者可以使用RTE的功能來提供協助工具的相關資訊。 例如，透過標題和段落元素新增結構資訊。

若要設定和自訂這些功能， [設定RTE外掛程式](#configure-the-plugin-features) 用於元件。 例如， `paraformat` 外掛程式可讓您新增其他區塊層級語意元素，包括擴充基本標題以外支援的標題層級數目 `H1`， `H2`、和 `H3` 預設提供。

RTE有多種元件可供觸控式使用者介面和傳統使用者介面使用。 不過，使用RTE的主要元件是 **文字** 兩個介面都可用的元件。 下列影像顯示已啟用一系列外掛程式的RTE，包括 `paraformat`：

![觸控式UI中全熒幕模式的文字元件(RTE)。](assets/chlimage_1-206.png)

*圖：觸控式使用者介面中的文字元件。*

![傳統UI中文字元件的「編輯」對話方塊(RTE)。](assets/chlimage_1-207.png)

*圖： Classic使用者介面中的文字元件。*

如需各種介面中可用的RTE功能之間的差異，請參閱 [外掛程式及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins).

## 設定外掛程式功能 {#configure-the-plugin-features}

如需設定RTE的完整指示，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md) 頁面。 這涵蓋所有問題，包括關鍵步驟：

* [外掛程式和功能](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [設定位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [啟動外掛程式並設定功能屬性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [設定RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

藉由在適當位置中設定外掛程式 `rtePlugins` CRXDE Lite的子分支，您可以為該外掛程式啟動所有或特定功能。

![顯示rtePlugin範例的CRXDE Lite。](assets/chlimage_1-208.png)

### 範例 — 指定RTE選取欄位中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

新的語意區塊格式可能可供下列使用者選擇：

1. 根據您的RTE，決定並導覽至 [設定位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [啟用段落選擇欄位](/help/sites-administering/rich-text-editor.md)；依據 [啟用外掛程式](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [在「段落選取」欄位中指定您想要的可用格式](/help/sites-administering/rich-text-editor.md).
1. 然後，內容作者可以從RTE的選擇欄位中使用段落格式。 它們可以存取：

   * 在觸控式UI中使用段落枕頭圖示。
   * 使用 **格式** 傳統UI中的欄位（彈出式選取器）。

透過RTE中可透過段落格式選項使用的結構元素，AEM為開發無障礙內容提供了良好的基礎。 內容作者無法使用RTE來格式化字型大小、顏色或其他相關屬性，因而無法建立內嵌格式。 相反地，他們必須選取適當的結構元素（例如標題），並使用從「樣式」選項中選擇的全域樣式。 這可確保為使用自己的樣式表和正確結構化的內容瀏覽的使用者提供乾淨的標示、更豐富的選項。

## 使用來源編輯功能 {#use-of-the-source-edit-feature}

在某些情況下，內容作者會發現必須檢查和調整使用RTE建立的HTML原始碼。 例如，在RTE內建立的內容片段可能需要額外的標籤，以確保符合WCAG 2.0。您可以透過以下專案完成此作業： [來源編輯](/help/sites-administering/rich-text-editor.md#aboutplugins) RTE選項。 您可以指定 [ `sourceedit` 上的功能 `misctools` 外掛程式](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>使用 `sourceedit` 功能精心。 輸入錯誤和/或不支援的功能可能會導致更多問題。

## 新增對更多HTML元素和屬性的支援 {#add-support-for-more-html-elements-and-attributes}

若要進一步擴充AEM的協助工具功能，您可以根據RTE擴充現有元件(例如 **文字** 和 **表格** 元件)與其他元素和屬性。

下列程式說明如何延伸 **表格** 元件與 **註解** 向輔助技術使用者提供有關資料表資訊的元素：

### 範例 — 將註解新增至表格屬性對話方塊 {#example-adding-the-caption-to-the-table-properties-dialog}

在的建構函式 `TablePropertiesDialog`，新增其他文字輸入欄位來編輯標題。 請注意 `itemId` 必須設定為 `caption` （即DOM屬性的名稱）以自動處理其內容。

在 **表格**，明確設定或移除DOM元素中的屬性。 此值會由以下位置的對話方塊傳遞： `config` 物件。 請注意，應使用對應的設定/移除DOM屬性 `CQ.form.rte.Common` 方法( `com` 是以下專案的捷徑： `CQ.form.rte.Common`)以避免瀏覽器實作的常見陷阱。

>[!NOTE]
>
>此程式僅適用於Classic使用者介面。

### 範例 — 在文字中使用強調時建立無障礙HTML {#create-accessible-html-for-text}

RTE可以使用 `strong` 和 `em` 標籤取代 `b` 和 `i`. 將下列節點新增為同層級至 `uiSettings` 和 `rtePlugins` 對話方塊中的節點。

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### 逐步指示 {#step-by-step-instructions}

1. 開始CRXDE Lite。 例如： [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 复制：

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >如果中間資料夾尚不存在，您可能需要建立它們。

1. 复制：

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 開啟下列檔案進行編輯（按兩下即可開啟）：

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在 `constructor` 方法，在行讀取之前：

   ```
   var dialogRef = this;
   ```

   新增下列程式碼：

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 開啟下列檔案：

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`。

1. 將下列程式碼新增至 `transferConfigToTable` 方法：

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. 儲存您的變更，使用 **全部儲存……**

>[!NOTE]
>
>純文字欄位不是註解元素值允許的唯一輸入型別。 您可以使用任何ExtJS Widget，透過其提供註解值 `getValue()` 方法。
>
>若要為其他元素和屬性新增編輯功能，請確定兩者：
>
>* 此 `itemId` 每個對應欄位的屬性都會設定為適當DOM屬性的名稱(`TablePropertiesDialog`)。
>* 在DOM元素上明確設定和/或移除屬性(`Table`)。


>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [建立無障礙內容（符合WCAG 2.0）](/help/sites-authoring/creating-accessible-content.md)

