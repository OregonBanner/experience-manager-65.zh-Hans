---
title: HTML5表單的指令碼支援
seo-title: Scripting support for HTML5 forms
description: HTML5 Forms支援的JavaScript、FormCalc屬性及其他方法。
seo-description: JavaScript, FormCalc properties, and other methods that are supported in HTML5 Forms.
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: Mobile Forms
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: c4045313200ffecbf05abfacd67aabc80ad67e7f
workflow-type: tm+mt
source-wordcount: '3892'
ht-degree: 6%

---

# HTML5表單的指令碼支援 {#scripting-support-for-html-forms}

HTML5表單支援的JavaScript、FormCalc屬性和方法如下：

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>指定欄位在回應使用者的動作而變更前的內容。 此值可重新呼叫，類似於撤消功能。</td>
   <td><p>不適用於下拉式清單和清單方塊。 <code>PrevText </code>在下列情況下無法正常運作：</p>
    <ul>
     <li>在iPad的數值欄位中輸入一些特殊字元鍵(例如$、(、)、&amp;、@等)時，以及 </li>
     <li>針對「日期」欄位（透過行事曆輸入日期時）。<br /> </li>
    </ul> <p>不支援透過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件對其執行動作的物件。</td>
   <td>不支援透過指令碼設定值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定欄位在回應使用者動作而變更後的內容。</td>
   <td><p>此 <code>newText</code> 屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>選取 — 取代文字時</li>
     <li>刪除、複製和貼上文字時。</li>
     <li>在數值欄位中輸入一些特殊字元鍵(例如$、(、)、&amp;、@等)時<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul>
    <div>
      不支援透過指令碼設定值。
    </div> </td>
  </tr>
  <tr>
   <td>更改</td>
   <td>指定使用者在執行動作後，立即鍵入或貼到欄位中的值。 </td>
   <td><p>變更屬性在下列情況下無法正常運作：</p>
    <ul>
     <li>選取 — 取代文字時</li>
     <li>刪除、複製和貼上文字時。</li>
     <li>在數值欄位中輸入一些特殊字元鍵(例如$、(、)、&amp;、@等)時<br /> </li>
     <li>使用Shift+英數字元組合時。 </li>
     <li>使用日期/時間欄位時。</li>
    </ul> <p>不支援透過指令碼設定值。</p> </td>
  </tr>
  <tr>
   <td>Keydown</td>
   <td>判斷使用者是否按箭頭鍵進行選取。 此屬性僅適用於清單方塊和下拉式清單。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>修飾元</td>
   <td>決定當特定事件執行時，是否按住修飾元鍵(例如，Microsoft® Windows®上的Ctrl)。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>傳回主機的應用程式型別。 僅適用於使用者端應用程式。</td>
   <td>傳回 <code>HTML 5</code>.</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>傳回目前應用程式的名稱。</td>
   <td>傳回瀏覽器名稱及其版本。 例如，在Chrome瀏覽器中，傳回的值是 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>傳回檔案中的頁數。</td>
   <td>HTML5表單的分頁原則與PDF forms分頁原則不相同。 因此，在這兩種情況下， numPages API都可以傳回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>傳回代表執行指令碼之電腦平台的字串。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定檔案的標題。 它僅適用於使用者端應用程式。</td>
   <td>它會以表單傳回HTML檔案的標題，而不是以PDF forms方式傳回表單中繼資料標題。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>傳回代表目前應用程式版本號碼的字串。</td>
   <td>它會傳回表單的版本。</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>指定是否執行計算指令碼。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>指定是否執行驗證指令碼。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>前往上一頁。</td>
   <td>HTML5表單不遵循與PDF表單相同的分頁原則，因此HTML5表單的上一頁與PDF表單的上一頁不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移至表單的下一頁。 在執行階段使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>將鍵盤焦點設定為指定的欄位。 欄位會指定為物件，或由欄位的SOM運算式指定。 它僅適用於使用者端應用程式。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>將檔案中的欄位重設為預設值。</td>
   <td>清除具有合併資料的表單中的所有資料，而不是將其還原為預設值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在熒幕上顯示對話方塊。 它僅適用於使用者端應用程式</td>
   <td>型別為「是/否」的訊息方塊會轉換為「確定/取消」。 不支援含有三個按鈕的訊息方塊。</td>
  </tr>
  <tr>
   <td>目前頁面</td>
   <td><p>在執行階段設定檔案的目前作用中頁面。</p> <p>頁面值以0為基礎，因此檔案的第一頁會傳回0值。</p> <p>在使用者端上執行layout：ready時，currentPage屬性可用。 但是，當layout：ready在伺服器上執行時無法使用，因為屬性要等到表單配置執行後才會執行。</p> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 字段 {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>属性</span></strong></th>
   <th><strong><span>描述<br /> </span></strong></th>
   <th><strong><span>例外</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>控制相關物件在處理的不同階段中的參與。 如果物件是容器，則容器的內容會繼承此控制項套用的任何限制。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制使用者對內容的存取權。</td>
   <td>不適用於排除群組。 此外，HTML5表單對非互動和受保護物件提供相同的處理方式。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>HTML5表單不允許設定物件的名稱屬性。 它是HTML5表單的唯讀屬性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>包含單一資料內容單位的內容元素。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>指定此欄位的未格式化值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>指定此欄位的格式化值。</td>
   <td>設定 <code>formattedValue</code> 不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>指定此欄位的編輯值。</td>
   <td>設定 <code>editValue </code>不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>指定此欄位的格式驗證訊息字串。</td>
   <td>設定 <code>formatMessage </code>不支援透過指令碼。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>指定此欄位的背景色彩值。 您需要將border.fill.presence屬性設定為單獨可見。</td>
   <td>它無法正確傳回欄位的預設顏色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>border物件說明物件周圍的邊框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>ui物件會包含表單物件的使用者介面說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>指定欄位的nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此欄位的邊框色彩值。 您需要將border.edge.presence屬性設定為單獨可見。</td>
   <td>它無法正確傳回欄位的預設邊框顏色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>清單中的專案數。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>將新專案新增至目前欄位。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>移除欄位中的所有專案。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>取得下拉式清單或清單方塊之特定顯示專案的繫結值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>執行欄位的計算指令碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>執行欄位的驗證指令碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>執行物件的事件指令碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>傳回指定專案的選取狀態</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>設定指定專案的選取狀態。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>擷取指定專案索引的專案顯示文字。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>擷取指定專案索引的資料值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>刪除指定索引處的專案。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>設定目前欄位中的指定專案。 它會取代原先存在的專案。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定版面寬度的測量值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>註解物件說明與表單設計物件相關聯的描述性標籤。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單存留期間被多次啟動。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>指定此欄位的父子表單（頁面）。</td>
   <td>一律會傳回父項子表單，而非傳回第一個非領域化的父項子表單。<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>第一個選取專案的索引。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 表单 {#form}

| **属性** | **描述** | **例外** |
|---|---|---|
| formNodes | 傳回繫結至指定資料物件的所有表單模型物件清單。 |  |

## 執行個體管理員 {#instancemanager}

| 属性 | 描述 |
|---|---|
| `name` | 用於在指令碼運算式中識別此元素的識別碼。 |
| `occur` | 說明其封閉容器允許的執行個體數目的限制。 |
| `min` | 指定可具現化的執行個體數目下限。 |
| `max` | 指定可具現化的執行個體數目上限。 |
| `count` | 指定目前具現化的執行個體數目。 |
| `setInstances` | 從此節點新增或移除指定的子表單或子表單集。 |
| `addInstance` | 將子表單或子表單集的新例項新增至此節點。 |
| `removeInstance` | 從此節點移除子表單或子表單集。 |
| `moveInstance` | 將表單模型物件的子物件移動到表單模型內的另一個指定位置。 物件的對應資料模型資訊也會在資料模型中重新定位。 |
| `insertInstance` | 將子表單或子表單集的新執行個體插入此節點。 |

## list {#list}

| 属性 | 描述 |
|---|---|
| `length` | 清單中的元素數量。 |
| `item` | 集合中的索引（從零開始）。 |
| `append` | 將節點附加至節點清單的結尾。 |
| `remove` | 從節點清單中移除節點。 |
| `insert` | 在節點清單中的特定節點之前插入節點。 |

## 節點 {#node}

| 属性 | 描述 | 例外 |
|---|---|---|
| createNode | 根據有效的類別名稱建立新節點。 | 无 |
| `isContainer` | 指定此物件是否為容器物件。 | 无 |
| `isNull` | 指出目前的資料值是否為Null值。 | 无 |
| `resolveNode` | 從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。 | 无 |
| `resolveNodes` | 從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。 | 无 |
| oneOfChild | 根據有效的類別名稱建立新節點。 | 无 |
| getElement | 傳回指定的子物件。 | 无 |
| getAttribute | 取得指定的屬性值。 | 无 |
| setAttribute | 設定指定屬性的值。 | 无 |

## 模型 {#model}

| 属性 | 描述 | 例外 |
|---|---|---|
| NA | NA | NA |

## 子表單 {#subform}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>指定物件相對於其他例項化執行個體的索引。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>執行物件的事件指令碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>傳回子表單（含）中包含且驗證測試失敗的節點清單。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>border物件說明物件周圍的邊框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此欄位的邊框色彩值。 您需要將border.edge.presence屬性設定為單獨可見。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定版面寬度的測量值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單存留期間被多次啟動。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>name</td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制使用者對容器物件（如子表單）內容的存取權。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execvalidate</td>
   <td>根據子表單或子表單集相對於相同表單物件其他例項的位置計算其索引。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager物件可管理表單模型物件的建立、移除和移動。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 属性 | 描述 |
|---|---|
| 目標 | 資料提交至的URL。 缺少此屬性表示XFA處理應用程式使用產品特定技術取得URI，例如存取設定物件中的產品特定資訊。 |

## 樹狀 {#tree}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>節點</td>
   <td>傳回目前物件之所有子物件的清單。</td>
   <td>
    <ul>
     <li>不支援xfa.nodes， desc</li>
     <li>針對PDF和HTML報告的節點數量不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定此節點的名稱。</td>
   <td>HTML中不允許使用指令碼設定名稱。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>取得此節點的父系。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>index</td>
   <td>傳回此節點在其類似名稱、範圍內、類似子系關係節點的集合中的位置。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>somexpression</td>
   <td>取得此節點的SOM運算式。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>從目前的XML表單物件模型物件開始，評估指定的SOM運算式，並傳回SOM運算式中指定的物件值。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 子表單集 {#subformset}

| 属性 | 描述 | 例外 |
|---|---|---|
| instanceManager | instanceManager物件可管理表單模型物件的建立、移除和移動。 | 无 |

## content {#content}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指出目前的資料值是否為null值。 |  |

## dataValue {#datavalue}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指出目前的資料值是否為null值。 |  |

## edge {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>属性 </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明圖樣物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 填滿 {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>顏色屬性會定義填色的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 線性 {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明表單上線性漸層填色的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 折线图 {#line}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>Edge物件可描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。<br /> </td>
  </tr>
 </tbody>
</table>

## 圖樣 {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明圖樣物件的獨特顏色。 </td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 半徑 {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明放射狀物件的獨特顏色</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 點膠 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明點狀物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## draw {#draw}

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>描述</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui物件會包含表單物件的使用者介面說明。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>caption</td>
   <td>註解物件說明與表單設計物件相關聯的描述性標籤。</td>
   <td> </td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定可用於在指令碼運算式中指定此物件或事件的識別碼。</td>
   <td>不支援在執行階段設定值</td>
  </tr>
  <tr>
   <td>值</td>
   <td>value物件會包含單一資料內容單位。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 轉角 {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color屬性說明轉角物件的獨特顏色。</td>
   <td>
    <ul>
     <li>無法擷取預設值。 </li>
     <li>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>border物件說明checkButton物件周圍的邊框。 </td>
   <td>這些變更會反映在模型中，且可用於編寫指令碼，但不會同步至HTML元素。 因此，變更不會反映在UI中。<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>border物件說明圍繞choiceList物件的邊框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 邊框 | border物件說明dateTimeEdit物件周圍的邊框。 |  |

## 图像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>內容型別</td>
   <td>指定參考檔案中的內容型別，以MIME型別表示。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>用於在指令碼運算式中識別此元素的識別碼。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 邊框 | border物件說明imageEdit物件周圍的邊框。 |  |

## numericEdit {#numericedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 邊框 | border物件說明物件周圍的邊框。 | 无 |

## 对象 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>類別名稱</td>
   <td>決定此物件的類別名稱。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 矩形 {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>Edge物件可描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>border物件說明物件周圍的邊框。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>布局</td>
   <td>指定此物件要使用的版面配置策略。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>邊框</td>
   <td>指定此欄位周圍的邊框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>強制</td>
   <td>指定欄位的nullTest值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此欄位的邊框色彩值。您必須先定義邊框，才能透過指令碼變更顏色。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>指定此欄位的邊框寬度。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>版面高度測量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>暫時性</td>
   <td>指定處理應用程式是否必須將排除群組的值儲存為表單提交或儲存作業的一部分。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定版面寬度的測量值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的x座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>指定以定位版面配置放置時，容器錨點相對於父容器左上角的y座標。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>註解物件說明與表單設計物件相關聯的描述性標籤。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>驗證</td>
   <td>驗證物件可控制表單上使用者所提供資料的驗證。 驗證物件可在表單存留期間被多次啟動。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>取得合併後表單節點繫結至的資料節點。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>是否存在</td>
   <td>指定物件的可見性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存取</td>
   <td>控制使用者對容器物件（如子表單）內容的存取權。</td>
   <td>對於排除中的個別專案，它一律會傳回open。 </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定可用於在指令碼運算式中指定此物件或事件的識別碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>成员</td>
   <td>指定排除群組的成員。 </td>
   <td>无</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>傳回排除群組的選取成員。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>對指定物件的計算事件以及任何子物件執行任何指令碼。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>計算</td>
   <td>calculate物件可控制欄位值的計算。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 圓弧 {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>Edge物件可描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。 </td>
  </tr>
 </tbody>
</table>

## 邊框 {#border}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>edge</td>
   <td>Edge物件可描述圓弧、直線或邊框或矩形的一側。<br /> </td>
   <td>不支援顏色、端點等屬性。 </td>
  </tr>
 </tbody>
</table>

## $布局 {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>決定給定表單設計物件的高度。<br /> </td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援Height (h)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>決定給定表單設計物件的寬度。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援寬度(w)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>決定給定表單設計物件相對於其父物件的x座標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援x座標(x)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>決定給定表單設計物件相對於其父物件的y座標。</td>
   <td>
    <ul>
     <li>頁面區域和內容區域不支援y座標(y)屬性。 </li>
     <li>不支援「XFA-Form物件發生於第一個內容區域的位移」引數。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法會為PDF和HTML表單傳回不同的值。</li>
     <li>藉由隱藏物件來減少頁數時，abspagecount方法傳回不正確的值。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecontent</td>
   <td>從表單的指定頁面擷取表單設計物件的型別。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>決定目前表單的頁數。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法會為PDF和HTML表單傳回不同的值。</li>
     <li>藉由隱藏物件來減少頁數時，abspagecount方法傳回不正確的值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 项目 {#items}

| **属性** | **描述** | **例外** |
|---|---|---|
| 是否存在 | 指定物件的可見性。 | 无 |

## FormCal {#formcalc}

FormCalc是XFA專屬的語言，用於建立以電子錶單為中心的邏輯和計算根。 FormCalculation提供了一組強大的建置函式。

### FormCalc支援的函式 {#formcalc-supported-functions}

### FormCalc運算式支援 {#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>类别 </strong></td>
   <td><strong>描述 </strong></td>
   <td><strong>样本 </strong></td>
  </tr>
  <tr>
   <td>簡單運算式</td>
   <td>加、減、乘、除和括弧</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>變數宣告</td>
   <td>定義變數</td>
   <td>變數a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>邏輯運算式</td>
   <td>
    <ul>
     <li>邏輯（和/或）</li>
     <li>比較（大於/小於/等於）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A或1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>If運算式</td>
   <td><br type="_moz" /> </td>
   <td>如果(a&gt;b)則2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>當(i lt 5)do i = i + 1 endwhile</td>
  </tr>
  <tr>
   <td> 的 </td>
   <td><br type="_moz" /> </td>
   <td>i = 100降到1 <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>針對每個</td>
   <td><br type="_moz" /> </td>
   <td>每個i (1， 2， 3) <br /> do s = s + i endfor</td>
  </tr>
  <tr>
   <td>函式宣告</td>
   <td>在FormCalc中定義自訂函式</td>
   <td>func foo(n) do var f = n endfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API支援 {#acrobat-api-support}

1. **算術函式**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 计数()
   1. Floor()
   1. Max()
   1. 最小()
   1. Mod()
   1. Round()
   1. 总计()

1. **科學功能**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. 棕褐色()
   1. Exp()
   1. 日志()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **財務函式**

   1. 四月()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. 术语()

1. **邏輯函式**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **字串函式**

   1. 于()
   1. Concat()
   1. 左()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. 替换()
   1. 右()
   1. Rtrim()
   1. 空间()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日期與時間**

   1. 日期()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>像差</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>此acrobat API會將輸出傾印到JavaScript主控台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此acrobat API會透過JavaScript快顯視窗傳送警示訊息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>讓系統播放音效。</td>
   <td>不會執行任何動作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>向使用者顯示強制回應對話方塊。 必須先關閉強制回應對話方塊，使用者才能再次直接使用主機應用程式。</td>
   <td>不會執行任何動作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在瀏覽器視窗中啟動URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript指令碼和時段。 每次經過該時段時都會執行指令碼。 此方法的傳回值必須儲存在JavaScript變數中。 否則，間隔物件會接受垃圾回收，這會導致時鐘停止。 若要終止定期執行，請將傳回的間隔物件傳遞給clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript指令碼和時段。 指令碼只會在經過句點後執行一次。此方法的傳回值必須儲存在JavaScript變數中。 否則，逾時物件會接受垃圾回收，這會導致時鐘停止。 若要取消逾時事件，請將傳回的逾時物件傳遞給clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消先前由setInterval方法所設定的暫存間隔。</td>
   <td>在HTML5表單中，API無法正常運作。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消先前登入的超時間隔。 此間隔最初由setTimeOut設定。</td>
   <td>在HTML5表單中，API無法正常運作。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>執行指定的指令碼。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每個使用中檔案的Doc物件的陣列。 如果沒有使用中的檔案，activeDocs不會傳回任何內容，也就是說，它與d =核心JavaScript中的new Array(0)的行為相同。</td>
   <td>傳回HTMl5表單的空白陣列。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果為true （預設值），則可執行計算。 如果為false，則不允許計算。</td>
   <td>HTMl5 Forms一律為True。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用來儲存各種常數值的包裝函式物件。 目前，此屬性會傳回具有單一屬性align的物件。</td>
   <td>HTML5表單傳回空的對齊物件。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>開啟和關閉焦點矩形。 焦點矩形是按鈕、核取方塊、選項按鈕和簽章周圍模糊的虛線，表示表單欄位具有鍵盤焦點。 若值為true，會開啟焦點矩形。</td>
   <td>HTML5表單一律為True。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>檢視器表單軟體的版本號碼。 如果您想要在指令碼中維持回溯相容性，請核取此屬性以判斷較新版本軟體中的物件、屬性或方法是否可用。</td>
   <td>一律為11.001。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>執行中的Acrobat檢視器的語言。</td>
   <td>HTMl5表單一律為「繁體中文」。</td>
  </tr>
 </tbody>
</table>

## 支援的XFA事件 {#supported-xfa-events}

支援下列使用者端XFA事件：

* 初始化
* 验证
* 计算
* 单击
* 輸入
* 退出
* 更改
* ValidationState

>[!NOTE]
>
>HTML5表單會在使用者端（瀏覽器）上呈現。 建議使用使用者端 **驗證** 和 **計算** 指令碼而非伺服器端指令碼。
