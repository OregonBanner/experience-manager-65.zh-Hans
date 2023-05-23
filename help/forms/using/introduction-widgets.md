---
title: 最適化和HTML5表單的外觀架構
seo-title: Appearance framework for adaptive and HTML5 forms
description: Mobile Forms會將表單範本轉譯為HTML5表單。 這些表單使用jQuery、Backbone.js和Underscore.js檔案作為外觀並啟用指令碼。
seo-description: Mobile Forms render Form Templates as HTML5 forms. These forms use jQuery, Backbone.js and Underscore.js files for the appearance and to enable scripting.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 2%

---

# 最適化和HTML5表單的外觀架構 {#appearance-framework-for-adaptive-and-html-forms}

Forms (適用性表單和HTML5表單)使用 [jQuery](https://jquery.com/)， [Backbone.js](https://backbonejs.org/) 和 [底線.js](https://underscorejs.org/) 用於外觀和指令碼的程式庫。 這些表單也使用 [jQuery UI](https://jqueryui.com/) **Widget** 表單中所有互動式元素（例如欄位和按鈕）的架構。 此架構可讓Form開發人員在Forms中使用一組豐富的可用jQuery Widget和外掛程式。 您也可以從使用者擷取資料（例如leadDigits/trailDigits限制或實作圖片子句）時實作表單特定邏輯。 表單開發人員可以建立和使用自訂外觀，以改善資料擷取體驗，並使其更人性化。

本文內容適用於對jQuery和jQuery Widget有足夠瞭解的開發人員。 它提供外觀架構的深入分析，並可讓開發人員為表單欄位建立替代外觀。

外觀架構仰賴各種選項、事件（觸發器）和函式來擷取使用者與表單的互動，並回應模型變更以通知一般使用者。 此外：

* 此架構提供一組欄位外觀的選項。 這些選項是索引鍵/值組，分為兩個類別：通用選項和欄位型別特定選項。
* 作為合約的一部分，外觀會觸發一系列事件，例如enter和exit。
* 實作一組函式需要外觀。 有些函式是通用的，有些則是欄位型別函式專用的。

## 常用選項 {#common-options}

以下是設定的全域選項。 這些選項適用於每個欄位。

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>name</td>
   <td>用於在指令碼運算式中指定此物件或事件的識別碼。 例如，此屬性會指定主機應用程式的名稱。</td>
  </tr>
  <tr>
   <td>值</td>
   <td>欄位的實際值。 </td>
  </tr>
  <tr>
   <td>displayvalue</td>
   <td>此時會顯示欄位的這個值。 </td>
  </tr>
  <tr>
   <td>screenreaderText</td>
   <td>熒幕Reader使用此值來提供欄位相關資訊的旁白。 表單會提供值，您可以覆寫值。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>欄位在表單索引標籤序列中的位置。 只有在您想要變更表單的預設tab鍵順序時，才覆寫tabIndex。</td>
  </tr>
  <tr>
   <td>角色</td>
   <td>元素的角色，例如，標題或表格。</td>
  </tr>
  <tr>
   <td>高度</td>
   <td>Widget的高度。 以畫素為單位指定。 </td>
  </tr>
  <tr>
   <td>宽度</td>
   <td>Widget的寬度。 以畫素為單位指定。</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>用來存取容器物件（例如子表單）內容的控制項。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>Widget之XFA元素的para屬性。</td>
  </tr>
  <tr>
   <td>目錄</td>
   <td>文字的方向。 可能的值為ltr （由左至右）和rtl （由右至左）。</td>
  </tr>
 </tbody>
</table>

除了這些選項，框架還提供其他選項，這些選項會因欄位型別而異。 以下列出欄位特定選項的詳細資料。

### 與表單框架的互動 {#interaction-with-forms-framework}

為了與表單架構互動，Widget會觸發一些事件，讓表單指令碼運作。 如果Widget未擲回這些事件，則在該欄位表單中撰寫的某些指令碼將無法運作。

#### Widget觸發的事件 {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Event </th>
   <th>描述</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>每當欄位成為焦點時，就會觸發此事件。 它可讓「enter」指令碼在欄位上執行。 觸發事件的語法為<br /> (Widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>只要使用者離開欄位，就會觸發此事件。 它可讓引擎設定欄位的值並執行其「退出」指令碼。 觸發事件的語法為<br /> (Widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>此事件會觸發，以允許引擎執行在欄位上寫入的「變更」指令碼。 觸發事件的語法為<br /> (Widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>只要按一下欄位，就會觸發此事件。 它可讓引擎執行在欄位上寫入的「click」指令碼。 觸發事件的語法為<br /> (Widget)。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### 由Widget實作的API {#apis-implemented-by-widget}

外觀架構會呼叫在自訂Widget中實作的Widget的某些函式。 Widget必須實作下列函式：

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>聚焦：function()</td>
   <td>將焦點放在欄位。</td>
  </tr>
  <tr>
   <td>click： function()</td>
   <td>將焦點放在欄位上並呼叫XFA_CLICK_EVENT。</td>
  </tr>
  <tr>
   <td><p>markError：function(errorMessage， errorType)<br /> <br /> <em>錯誤訊息：字串 </em>代表錯誤<br /> <em>errorType：字串("warning"/"error")</em></p> <p><strong>注意</strong>：僅適用於HTML5表單。</p> </td>
   <td>傳送錯誤訊息和錯誤型別至Widget。 Widget會顯示錯誤。</td>
  </tr>
  <tr>
   <td><p>clearError： function()</p> <p><strong>注意</strong>：僅適用於HTML5表單。</p> </td>
   <td>如果欄位中的錯誤已修正，則呼叫。 Widget會隱藏錯誤。</td>
  </tr>
 </tbody>
</table>

## 欄位型別特定的選項 {#options-specific-to-type-of-field}

所有自訂Widget都應符合上述規格。 若要使用不同欄位的功能，Widget必須符合該特定欄位的准則。

### 文字編輯：文字欄位 {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>多行</td>
   <td>如果欄位支援輸入新行字元，則為True，否則為false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>可在欄位中輸入的最大字元數。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>：僅適用於HTML5表單</p> </td>
   <td>指定文字寬度超過Widget寬度時文字欄位的行為。</td>
  </tr>
 </tbody>
</table>

### ChoiceList： DropDownList， ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>值<br /> </td>
   <td>選取值的陣列。<br /> </td>
  </tr>
  <tr>
   <td>项目<br /> </td>
   <td>要顯示為選項的物件陣列。 每個物件包含兩個屬性 — <br /> 儲存：值儲存，顯示：值顯示。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>可編輯</p> <p><strong>注意</strong>：僅適用於HTML5表單。<br /> </p> </td>
   <td>如果值為true，則會在Widget中啟用自訂文字輸入。<br /> </td>
  </tr>
  <tr>
   <td>displayvalue<br /> </td>
   <td>要顯示的值陣列。<br /> </td>
  </tr>
  <tr>
   <td>多選<br /> </td>
   <td>如果允許多重選取，則為True，否則為false。<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>函数</th>
   <th>描述</th>
  </tr>
  <tr>
   <td><p>addItem：<em> function(itemValues)<br /> itemvalues：包含顯示和儲存值的物件 <br /> {sDisplayVal： &lt;displayvalue&gt;，儲存值： &lt;save value=""&gt;}</em></p> </td>
   <td>將專案新增至清單。</td>
  </tr>
  <tr>
   <td>deleteItem<em>：函式(nIndex)<br /> nIndex：要從清單中移除之專案的索引<br /> </em><br /> <br /> </td>
   <td>從清單中刪除選項。</td>
  </tr>
  <tr>
   <td>clearItems：<code> function()</code></td>
   <td>清除清單中的所有選項。</td>
  </tr>
 </tbody>
</table>

### NumericEdit： NumericField， DecimalField {#numericedit-numericfield-decimalfield}

| 选项 | 描述 |
|---|---|
| 資料型別 | 代表欄位資料型別（整數/小數）的字串。 |
| leadDigits | 十進位數字中允許的前置位數上限。 |
| fracDigits | 十進位數字中允許的分數位數上限。 |
| 零 | 欄位地區設定中零的字串表示。 |
| 小數 | 欄位地區設定中十進位的字串表示。 |

### CheckButton： RadioButton， CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>选项</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>值的陣列（開啟/關閉/中性）。</p> <p>它是checkButton不同狀態的值陣列。 values[0]是狀態為開啟時的值，values[1]是狀態為關閉時的值，<br /> values[2]是狀態為NEUTRAL時的值。 值陣列的長度等於狀態選項的值。<br /> </p> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td><p>允許的狀態數。 </p> <p>兩個用於調適型表單（開、關），三個用於HTML5表單（開、關、中性）。</p> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td><p>元素的目前狀態。</p> <p>兩個用於調適型表單（開、關），三個用於HTML5表單（開、關、中性）。</p> </td>
  </tr>
 </tbody>
</table>

### 日期時間編輯： （日期欄位） {#datetimeedit-datefield}

| 选项 | 描述 |
|---|---|
| 天 | 該欄位的本地化天數名稱。 |
| 个月 | 該欄位的當地語系化月份名稱。 |
| 零 | 數字0本地化文字。 |
| cleartext | 清除按鈕的本地化文字。 |
