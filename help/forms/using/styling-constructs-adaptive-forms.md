---
title: 調適型表單的樣式結構
seo-title: Styling constructs for adaptive forms
description: 使用LESS框架來自訂最適化表單的外觀。
seo-description: Use LESS framework to customize appearance of adaptive forms.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Adaptive Forms
exl-id: 691608a6-be82-4d81-b876-427de997e5be
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 3%

---

# 調適型表單的樣式結構{#styling-constructs-for-adaptive-forms}

## 前提条件 {#prerequisites}

CSS和LESS架構的知識。

## 可自訂的專案 {#what-can-be-customized}

本文列出可公開使用的調適型表單css類別。 您可以利用這些類別來設定最適化表單各種元件的樣式。 製作元件（例如顯示警告的對話方塊和狀態列）的樣式超出本文章的範圍。 只有在您無法使用下列專案來樣式元件時，才使用這些樣式建構來建立樣式（使用CSS或更少）： [主題編輯器](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## 在調適型表單中自訂樣式 {#customizing-styles-in-adaptive-forms}

LESS架構簡化了使用案例，進而可在調適型表單中自訂樣式。 此框架可讓您使用一組變數和函式(mixin)來定義樣式。 LESS架構有助於減少套件程式碼的大小，並提高其重複使用性。

您可以透過下列方式自訂最適化表單樣式：

* 變更主題
* 變更元件的樣式

## 變更主題 {#changing-theme}

您可以變更最適化表單的主題，以確保其外觀與內嵌最適化表單的網頁一致。

使用CSS屬性的最適化表單的整體外觀變更通常是主題變更的一部分。 最適化表單的lo &quot;ok和feel的重大變更（例如元件版面配置和位置的變更）不被視為主題變更。

根據啟動程式，以下一組CSS屬性會定義網頁的主題：

* 背景颜色
* 邊框（文字、顏色、粗細）
* 字体颜色
* 边距
* 边距
* 字体大小
* 行高

目前，LESS變數的定義僅適用於最適化表單中各種元素的這些屬性。

## 變更元件樣式 {#changing-component-style}

您可以變更元素的外觀、配置、位置和可見度。 若要完成此工作，請建立或更新您的自訂.css檔案，以包含本文中列出的樣式建構。

若要將樣式套用至最適化表單，請在中開啟最適化表單進行編輯、開啟最適化表單容器的屬性，以及在基本索引標籤中指定自訂CSS檔案的路徑。 預設最適化表單的樣式建構，並以自訂.css檔案中所列的建構加以覆寫。

## 组件 {#components}

本文討論的元件具有預先定義的CSS類別。 您可以編輯變數來修改CSS類別中的樣式。 或者，您也可以重寫整個類別。 本節說明可使用變數修改的元件和樣式中的類別。

## 容器樣式 {#container-styling}

容器是頂層元件。 其他面板和欄位則位於容器元件下。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>變數說明</strong></p> </td>
   <td><p><strong>變數說明</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>容器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>容器的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>容器的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>容器的字型顏色</p> </td>
  </tr>
 </tbody>
</table>

## 欄位樣式 {#field-styling}

調適型表單包含各種型別的欄位。 每個欄位都有唯一的類別名稱，即欄位名稱。 欄位也有常見的類別名稱 `guideFieldNode`.

欄位包含標籤、Widget、說明說明（長說明和短說明）以及欄位說明圖示（問號）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>欄位內距</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>欄位錯誤訊息的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>欄位錯誤訊息的字型大小</p> </td>
  </tr>
 </tbody>
</table>

## 標籤樣式 {#label-styling}

HTML元素 **標籤** 用於欄位，包括類別 **left** 或 **top** 標籤位於頂端還是左側。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>欄位標籤的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>欄位標籤的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>欄位標籤的CSS行高屬性 </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>欄位標籤的CSS字型權重屬性 </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>欄位標籤的邊界</p> </td>
  </tr>
 </tbody>
</table>

標籤的CSS規則是使用 **guideFieldLabel** 標籤。 如果您是作者，請覆寫此規則，使自訂變更可見。

## Widget樣式 {#widgets-styling}

視其型別而定，Widget也包含類別。 通常，Widget包含 `guideFieldWidget` 類別。 HTML隨附的Widget通常使用標準HTML元素輸入並選取。 樣式設定會據此進行。 您無法藉由變更變數來設定自訂Widget的樣式。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 <code></code></strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>Widget的背景顏色（核取方塊和選項按鈕無法運作）</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Widget的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Widget的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Widget邊框半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Widget的邊框型別</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Widget邊框的焦點型別</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Widget的整合邊框樣式</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>Widget內文字的色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Widget內文字的大小</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Widget的CSS lineheight屬性 </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Widget的CSS填補屬性</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Widget成為焦點時的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>必要欄位的Widget邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>必要欄位的Widget背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>欄位停用時Widget的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>欄位停用時Widget的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>欄位停用時Widget的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Widget的高度（核取方塊和選項按鈕無法運作）</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>核取方塊和選項按鈕的高度。</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>多選下拉式清單的最大高度</p> </td>
  </tr>
 </tbody>
</table>

### Widget樣式限制 {#limitations-in-widget-styling}

焦點、強制和停用欄位的樣式受到變數的限制。 不過，您可以覆寫樣式來變更它。 提供使用變數的限制主要是為了控制變數的數量。 如果欄位處於先前討論的任何狀態，因此其外觀會大幅變更，則可放寬限制。

## 說明說明 {#help-description}

作者可以使用簡短和長篇說明元件在欄位中指定說明內容。 兩個元件都有共同類別 `.guideHelpDescription` 和另一個類別 `.long`/ `.short`，視說明型別而定。 說明內容會包含在段落元素中，以覆寫說明的樣式。 說明說明（長與短）會使用以widgetshelp開頭的變數加以修改，如下表所述：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Widget詳細說明的背景色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Widget長說明的邊框色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Widget長說明的左側指示器邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Widget簡短說明的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Widget簡短說明的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Widget簡短工具提示的背景顏色說明</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Widget簡短工具提示的字型顏色說明</p> </td>
  </tr>
 </tbody>
</table>

## 条款和条件 {#terms-and-conditions}

條款與條件(TnC) `` ``) widget可讓您指定條款與條件。 您可以使用下表所述的變數來自訂Widget。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>未造訪的tnc連結的字型色彩。</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>造訪的tnc連結的字型色彩。</td>
  </tr>
 </tbody>
</table>

## 按钮 {#button}

按鈕也是Widget。 不過，它們的樣式與Widget稍有不同。 在最適化表單中，下列任何一項都會構成按鈕：

* 輸入[type =文字]
* 按钮
* 具有類別的元素.button

按鈕的HTML代碼：

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>提供按鈕的圖示</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>樣式按鈕標籤/註解</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 <code></code></strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>按鈕的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>邊框型別</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>按鈕的CSS填補屬性</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>按鈕的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>大型按鈕（具有.buttonlarge類別的按鈕）的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>大型按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>小型按鈕（具有.buttonsmall類別的按鈕）的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>小按鈕的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>資訊按鈕（具有.buttoninformative類別的按鈕）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>資訊按鈕的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>資訊按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>警告樣式按鈕（具有.buttonwarning類別的按鈕）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>警告樣式按鈕的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>警告樣式按鈕的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>警示按鈕（類別為.buttonalert的按鈕）的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>警示按鈕的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>警示按鈕的邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

## 問號 {#question-mark}

對於Widget，當作者在說明內容中新增詳細說明，會顯示問號。 會使用啟動程式中提供的預設圖示。 若要使用自訂圖示，您可以自訂啟動載入圖示。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>圖示的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>將滑鼠游標停留在圖示上時圖示的顏色</p> </td>
  </tr>
 </tbody>
</table>

## 表 {#table}

您可以使用下列變數來變更表格中標題和本文列的顏色主題。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>標題列的背景顏色。 默认值为 <code>#333</code>。<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>奇數正文列的背景顏色。 默认值为 <code>rgb(255, 255, 255)</code>。</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>偶數正文列的背景顏色。 默认值为 <code>#eee</code>。</p> </td>
  </tr>
 </tbody>
</table>

## 文件附件 {#file-attachment}

最適化表單的檔案附件Widget可讓您上傳檔案。 您也可以使用變數自訂Widget。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Widget中顯示之檔案的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>檔案專案的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>上邊框的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>檔案專案的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Widget中預覽圖示(Bootstrap圖示)的顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>檔案專案的註解高度</p> </td>
  </tr>
 </tbody>
</table>

## 瀏覽器樣式 {#navigator-styles}

有四種型別的導覽器標籤。 這些標籤包括左側、頂部、精靈和摺疊式功能表中的標籤。 每個瀏覽器都有不同的類別。

<table>
 <tbody>
  <tr>
   <td><p><strong>導覽器</strong></p> </td>
   <td><p><strong>CSS 类</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigator</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

以下是Tab鍵瀏覽元素的HTML代碼（類似於Bootstrap標籤）：

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

您可以使用CSS規則來變更導覽器的樣式，該規則會使用以下方式選取元素 **下級** 選取器。 例如，若要將文字裝飾樣式新增至錨點標籤：

頂端的Tab導覽器：

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

此外，根據索引標籤導覽器是否有巢狀/子項/子項導覽器，也有類別可設定索引標籤導覽器的樣式（左側和頂部）。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>具有巢狀/子項/子項導覽器的索引標籤導覽器（左側和頂部）</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>沒有巢狀/子項/子項導覽器的索引標籤導覽器（左側和頂部）</p> </td>
  </tr>
 </tbody>
</table>

guideNavIcon類別會提供定位點導覽器（左側和頂部）和精靈導覽器的預設圖示。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以在編寫表單範例的面板上提供CSS類別，以變更特定導覽器的圖示 &lt;class_name>. 您新增 **&lt;class_name>_nav** 以取得瀏覽器的圖示。

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>標籤導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>整個標籤導覽器的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>標籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>標籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>暫留時索引標籤的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>暫留時索引標籤的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>面板成為焦點時的背景顏色（作用中）</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>面板成為焦點時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>面板成為焦點一次，但完成運算式傳回false時的背景顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>面板成為焦點一次，但完成運算式傳回false時的字型顏色 </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>標籤的邊框顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>標籤的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>標籤的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>索引標籤的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>垂直標籤的邊界</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>標籤的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>標籤的最小高度</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>巢狀索引標籤的縮排</p> </td>
  </tr>
  <tr>
   <td><p><strong>精靈導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>整個精靈導覽器的背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>精靈的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>精靈的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>面板成為焦點時的背景顏色（作用中）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>面板成為焦點時的字型顏色（焦點）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>面板的完成運算式傳回true時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>面板成為焦點一次但完成運算式傳回false時的背景顏色</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>面板已聚焦一次，但完成運算式傳回false時的字型顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>精靈的色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>精靈的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>精靈的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>精靈的邊框大小</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>精靈導覽器專案符號的邊框顏色（註解/標籤的前置詞）</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>精靈導覽器進度列的背景色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>進度列的填色色彩</p> </td>
  </tr>
  <tr>
   <td><p><strong>收合式選單導覽器</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>摺疊式功能表的內距</p> </td>
  </tr>
 </tbody>
</table>

## 面板樣式 {#panel-styling}

面板包含選用的工具列及其內容。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>面板的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>面板文字的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>面板文字的字型色彩<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>面板內的內距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>面板說明的字型大小</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>面板說明的內邊距</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>面板說明的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>面板說明的指標邊框顏色</p> </td>
  </tr>
 </tbody>
</table>

面板節點分為導覽器和內容。 那裡 `` `` 內容沒有獨立的樣式元件。 所描述的變數會套用至導覽器及內容。

最上方的面板(RootPanel)沒有此類別。

## 行動樣式 {#mobile-styling}

## 標題列 {#header-bar}

這些變數會影響在包含面板標題以及下一個和背面導覽器的行動裝置或小熒幕裝置上顯示的標題列。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>標題列的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>標頭列中文字的字型色彩</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>標頭列的邊框間距</p> </td>
  </tr>
 </tbody>
</table>

## 捲動指示器 {#scroll-indicator}

這些變數會影響捲動指示器，也就是出現在行動裝置或小熒幕裝置上的橘色箭頭。 捲動指示器表示畫面可見部分以外的內容存在。 您可以向下捲動來檢視。 當您按下內容的結尾時，箭頭會消失。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>從底部固定卷軸指示器的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>從右側固定卷軸指示器的位置</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>卷軸指示器的寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>卷軸指示器的高度</p> </td>
  </tr>
 </tbody>
</table>

## 行動固定工具列配置特定變數 {#mobile-fixed-toolbar-layout-specific-variables}

下表中的這些變數會影響行動固定工具列版面配置。

<table>
 <tbody>
  <tr>
   <td><p><strong>CSS 类 </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>固定工具列位置，在行動裝置上，從底部</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>固定工具列位置，在行動裝置上，從上方</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>固定工具列位置，在行動裝置上，從左側</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>固定工具列位置，在行動裝置上，從右側</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>固定工具列按鈕圖示的位置（從頂端）</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>行動裝置上工具列按鈕圖示的寬度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>行動裝置上工具列按鈕圖示的高度</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>行動裝置上工具列的背景顏色</p> </td>
  </tr>
 </tbody>
</table>

## 主題特定變數 {#theme-specific-variable}

此 **簡單註冊** /etc/clientlibs/fd/af/guidetheme/simpleEnrollment的主題和類別 `guide.theme.simpleEnrollment` 也會介紹一些變數。 如果要建立主題來增強簡單註冊，您可以使用以下「額外變數：

<table>
 <tbody>
  <tr>
   <td><p><strong>变量 </strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>焦點按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>暫留時按鈕的背景顏色</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>按鈕的半徑</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>導覽按鈕的背景顏色（上一頁/下一頁）</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>暫留時導覽按鈕的背景顏色（上一頁/下一頁）</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>第一次呈現精靈導覽器和對應進度列的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>目前/作用中精靈導覽器的背景顏色與對應的進度列 </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>已造訪的精靈導覽器和對應進度列的背景顏色。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>邊框顏色將容器分成導覽器和面板</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>左側索引標籤（索引標籤導覽器）的底部邊框顏色分隔索引標籤。</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>導覽器的巢狀/子項/子項導覽器的背景顏色</p> </td>
  </tr>
 </tbody>
</table>
