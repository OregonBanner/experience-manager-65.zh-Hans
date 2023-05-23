---
title: 最適化表單運算式
seo-title: Adaptive Form Expressions
description: 使用調適型表單運算式來新增自動驗證、計算，以及開啟或關閉區段的可見度。
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: Adaptive Forms
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

# 最適化表單運算式{#adaptive-form-expressions}

適用性表單透過動態指令碼功能，為使用者提供最佳化和簡化的表單填寫體驗。 它可讓您編寫運算式以新增各種行為，例如動態顯示/隱藏欄位和面板。 它也可讓您新增計算欄位、讓欄位成為唯讀、新增驗證邏輯等。 動態行為取決於使用者輸入或預填的資料。

JavaScript是適用性表單的運算式語言。 所有運算式都是有效的JavaScript運算式，且使用適用性表單指令碼模型API。 這些運算式會傳回某些型別的值。 如需最適化表單類別、事件、物件和公用API的完整清單，請參閱 [適用性表單的JavaScript資料庫API參考](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## 撰寫運算式的最佳作法 {#best-practices-for-writing-expressions}

* 在撰寫運算式時，若要存取欄位和面板，您可以使用欄位或面板的名稱。 若要存取欄位的值，請使用value屬性。 例如，`field1.value`
* 對表單中的欄位和面板使用唯一名稱。 它有助於避免在撰寫運算式時所使用的欄位名稱發生任何可能的衝突。
* 撰寫多行運算式時，請使用分號來終止陳述式。

## 涉及重複面板之運算式的最佳作法 {#best-practices-for-expressions-involving-repeating-panel}

重複面板是使用指令碼API或預先填入的資料，以動態方式新增或移除的面板例項。 如需有關使用重複面板的詳細資訊，請參閱 [建立具有可重複區段的表單](/help/forms/using/creating-forms-repeatable-sections.md).

* 若要建立重複面板，請在面板對話方塊中開啟設定，並將最大計數欄位的值設定為大於1。
* 面板重複設定的最小計數值可以是一個或多個，但不能超過最大計數值。
* 當運算式參考重複面板的欄位時，運算式中的欄位名稱會解析為最接近的重複元素。
* 調適型表單提供一些特殊函式，可簡化可重複面板的計算，例如sum、count、min、max、filter等等。 如需完整的函式清單，請參閱 [適用性表單的JavaScript資料庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* 用於操作重複面板例項的API包括：

   * 若要新增面板執行個體： `panel1.instanceManager.addInstance()`
   * 若要取得面板重複索引： `panel1.instanceIndex`
   * 若要取得面板的instanceManager： `_panel1 or panel1.instanceManager`
   * 若要移除面板的執行個體： `_panel1.removeInstance(panel1.instanceIndex)`

## 運算式型別 {#expression-types}

在調適型表單中，您可以撰寫運算式來新增行為，例如動態顯示/隱藏欄位和面板。 您也可以撰寫運算式來新增計算欄位、將欄位設為唯讀、驗證邏輯等等。 調適型表單支援下列運算式：

* **[存取運算式](#access-expression-enablement-expression)**：啟用/停用欄位。
* **[計算運算式](#calculate-expression)**：用於自動計算欄位的值。
* **[點按運算式](#click-expression)**：處理按鈕點選事件的動作。
* **[初始化指令碼](#initialization-script)：** 在欄位初始化時執行動作。
* **[選項運算式](#options-expression)**：以動態填入下拉式清單。
* **[摘要運算式](#summary)**：動態計算摺疊式功能表的標題。
* **[驗證運算式](#validate-expression)**：驗證欄位。
* **[值認可指令碼](#value-commit-script)：** 在欄位值變更後變更表單元件。
* **[可見度運算式](#visibility-expression)**：控制欄位和面板的可見度。
* **[步驟完成運算式](#step-completion-expression)**：防止使用者進入精靈的下一個步驟。

### 存取運算式（啟用運算式） {#access-expression-enablement-expression}

您可以使用存取運算式來啟用或停用欄位。 如果運算式使用欄位的值，則每當欄位的值變更時，就會擷取運算式。

**套用至**：欄位

**傳回型別**：運算式會傳回布林值，代表欄位已啟用或已停用。 **true** 表示欄位已啟用，而且 **false** 表示欄位已停用。

**範例**：若要僅在 **欄位1** 設為 **X**，存取運算式為： `field1.value == "X"`

### 計算運算式 {#calculate-expression}

計算運算式可用來使用運算式自動計算欄位的值。 通常，這類運算式會使用其他欄位的值屬性。 例如， `field2.value + field3.value`. 每當值 `field2`或 `field3`會變更、重新觸發運算式並重新計算值。

**套用至**：欄位

**傳回型別**：運算式會傳回與顯示運算式結果的欄位相容的值（例如decimal）。

**範例**：計算運算式會顯示中兩個欄位的總和 **欄位1** 為：
`field2.value + field3.value`

### 按一下運算式 {#click-expression}

click運算式會處理對按鈕的點選事件執行的動作。 GuideBridge開箱即用地提供API來執行各種功能，例如提交、驗證和點選運算式一起使用。 如需API的完整清單，請參閱 [GuideBridge API](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**套用至**：按鈕欄位

**傳回型別**：click運算式未傳回任何值。 如果有任何運算式傳回值，則會忽略該值。

**範例**：填入文字方塊 **textbox1** 具有值的按鈕的點選動作 **AEM Forms**，則按鈕的點選運算式為 `textbox1.value="AEM Forms"`

### 初始化脚本 {#initialization-script}

初始化最適化表單時會觸發初始化指令碼。 視情況而定，初始化指令碼會以下列方式運作：

* 當適用性表單在轉譯時沒有資料預填，初始化指令碼會在表單初始化後執行。
* 使用資料預填來轉譯調適型表單時，指令碼會在預填作業完成後執行。
* 觸發最適化表單的伺服器端重新驗證時，會執行初始化指令碼。

**套用至：** 欄位和面板

**傳回型別：** 初始化指令碼運算式未傳回任何值。 如果有任何運算式傳回值，則會忽略該值。

**範例：** 在資料預填案例中，以預設值填入欄位 `'Adaptive Forms'` 當它們的值儲存為null時，初始化指令碼運算式為：
`if(this.value==null) this.value='Adaptive Forms';`

### 選項運算式 {#options-expression}

選項運算式可用來動態填入下拉式清單欄位的選項。

**套用至**：下拉式清單欄位

**傳回型別**：選項運算式會傳回字串值的陣列。 每個值都可以是簡單字串，例如 **男性**，或採用索引鍵=值配對格式，例如 **1=男性**

**範例**：若要根據其他欄位的值填入欄位的值，請提供簡單的選項運算式。 例如，若要填入欄位， **兒童數量**，根據 **婚姻狀況** 在另一個欄位中表達，運算式為：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

每當值 **writeral_status** 欄位變更，則會擷取運算式。 您也可以填入REST服務的下拉式清單。 如需詳細資訊，請參閱 [動態填入下拉式清單](../../forms/using/dynamically-populate-dropdowns.md).

### 摘要運算式 {#summary}

摘要運算式會動態計算摺疊式功能表版面面板的子面板標題。 您可以在規則中指定摘要運算式，這會使用表單欄位或自訂邏輯來評估標題。 運算式會在表單初始化時執行。 如果您要預先填寫表單，運算式會在資料預先填寫後或運算式中使用的相依欄位值變更時執行。

摘要運算式通常用於重複摺疊式功能表配置面板的子項，以為每個子項面板提供有意義的標題。

**套用至：** 面板是版面配置為Accordion之面板的直接子系。

**傳回型別：** 運算式會傳回成為摺疊式功能表標題的字串。

**範例：** &quot;帳號：&quot; + textbox1.value

### 驗證運算式 {#validate-expression}

驗證運算式是使用給定的運算式來驗證欄位。 通常，這類運算式會使用規則運算式以及欄位值來驗證欄位。 系統會擷取運算式，並在欄位值發生任何變更時，重新計算欄位的驗證狀態。

**套用至**：欄位

**傳回型別**：運算式傳回布林值，代表欄位的驗證狀態。 值 **false** 表示欄位無效，並且 **true** 表示欄位有效。
**範例**：對於代表UK郵遞區號的欄位，驗證運算式為：

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上述範例中，如果非空白值不符合模式，運算式會傳回 **false** 表示欄位無效。

>[!NOTE]
>
>如果您撰寫非必要或必要欄位的驗證運算式，則無論欄位的可見度狀態為何，都會評估運算式。 若要停止隱藏欄位的驗證，請將Initialization或Value Commit指令碼中的validationsDisabled屬性設定為true。 例如，`this.validationsDisabled=true`

### 值提交脚本 {#value-commit-script}

當出現下列情況時，就會觸發「值認可」指令碼：

* 使用者從UI變更欄位的值。
* 欄位的值會因其他欄位的變更而以程式設計方式變更。

**套用至：** 欄位

**傳回型別：** 值認可指令碼運算式未傳回任何值。 如果有任何運算式傳回值，則會忽略該值。

**範例：** 若要在認可時將欄位中輸入的字母大小寫轉換為大寫，值認可運算式為：
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>當欄位的值以程式設計方式變更時，您可以停用值認可指令碼的執行。 若要這麼做，請前往https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr和變更 **最適化Forms版本相容性** 至 **AEM Forms 6.1**. 此後，只有當使用者從UI變更欄位的值時，才會執行值認可指令碼。

### 可见性表达式 {#visibility-expression}

「可見性」運算式可用來控制欄位/面板的可見性。 通常，可見性運算式會使用欄位的值屬性，每當該值變更時就會重新觸發。

**套用至**：欄位和面板

**傳回型別**：運算式傳回布林值，代表欄位/面板是否可見。 **false** 表示欄位或面板不可見，而true表示欄位或面板可見。

**範例**：適用於只有當 **欄位1** 設為 **男性**，可見度運算式為： `field1.value == "Male"`

### 步驟完成運算式 {#step-completion-expression}

步驟完成運算式用於防止使用者進入精靈配置的下一個步驟。 當面板具有精靈版面配置（一次顯示一個步驟的多步驟表單）時，會使用這些運算式。 只有當目前區段中的所有必要值都已填滿且有效時，使用者才能移至下一個步驟、面板或子區段。

**套用至**：專案版面設定為精靈的面板。

**傳回型別**：運算式傳回布林值，代表目前面板是否有效。 **True** 表示目前面板有效，且使用者可導覽至下一個面板。

**範例**：在以各種面板組織的表單中，在導覽至下一個面板之前，會驗證目前的面板。 在這種情況下，會使用步驟完成運算式。 一般而言，這些運算式會使用GuideBridge驗證API。 步驟完成運算式的範例為：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 最適化表單中的驗證 {#validations-in-adaptive-form}

有多種方法可以將欄位驗證新增至最適化表單。 如果在欄位上新增驗證檢查， **True** 表示在欄位中輸入的值有效。 **False** 表示值無效。 如果您在欄位中或欄位外執行Tab鍵，則不會產生錯誤訊息。

在欄位上新增驗證的方法如下：

### 必填 {#required}

若要將元件設為必要元件，請在 **編輯** 元件對話方塊中，您可以選取選項 **標題和文字>必填**. 您也可以新增適當的 **必要訊息** （選擇性）。.

### 驗證模式 {#validation-patterns}

一個欄位有多個現成的驗證模式。 若要選取驗證模式，請在 **編輯** 在元件的對話方塊中，找到 **模式** 區段並選取 **圖樣**. 您可以在中建立自己的自訂驗證模式 **圖樣** 文字方塊。 已傳回驗證狀態 **True** 僅當填入的資料符合驗證模式時，否則 **False** 會傳回。 若要撰寫您自己的自訂驗證模式，請參閱 [HTML5表單的Picture子句支援](/help/forms/using/picture-clause-support.md).

### 驗證運算式 {#validation-expressions}

欄位驗證也可使用不同欄位上的運算式來計算。 這些運算式會寫入內部 **驗證指令碼** 的欄位 **指令碼** 索引標籤/ **編輯** 元件的對話方塊。 欄位的驗證狀態取決於運算式傳回的值。 如需如何撰寫這類運算式的詳細資訊，請參閱 [驗證運算式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## 附加信息 {#additional-information}

### 使用欄位顯示格式 {#using-field-display-format}

「顯示格式」可用於以不同格式顯示資料。 例如，您可以使用顯示格式來顯示含有連字型大小、郵遞區號格式或日期選擇器的電話號碼。 這些顯示模式可從 **模式** 元件之「編輯」對話方塊的區段。 您可以撰寫與上述驗證模式類似的自訂顯示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用來與瀏覽器中記憶體模型中的調適型表單互動。 如需Guide Bridge API、類別方法、公開事件的詳細介紹，請參閱 [適用性表單的JavaScript資料庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>建議不要在運算式中使用GuideBridge事件接聽程式。

#### 在各種運算式中使用GuideBridge {#guidebridge-usage-in-various-expressions}

* 若要重設表單欄位，您可以觸發 `guideBridge.reset()` 按鈕的點選運算式上的API。 同樣地，也有提交API，可作為click運算式呼叫 `guideBridge.submit()`**.**

* 您可以使用 `setFocus()` 用於跨不同欄位或面板設定焦點的API （面板的焦點會自動設定為第一個欄位）。 `setFocus()`提供廣泛的導覽選項，例如跨面板導覽、上一個/下一個周遊、將焦點設定為特定欄位等等。 例如，若要移至下一個面板，您可以使用： `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 若要驗證最適化表單或其特定面板，請使用 `guideBridge.validate(errorList, somExpression).`

#### 在運算式外部使用GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

您也可以在運算式之外使用GuideBridge API。 例如，您可以使用GuideBridge API來設定託管最適化表單和表單模型的頁面HTML之間的通訊。 此外，您也可以設定來自託管表單之Iframe父級的值。

若要針對上述範例使用GuideBridge API，請擷取GuideBridge的例項。 若要擷取執行處理，請接聽 `bridgeInitializeStart`事件 `window`物件：

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>在AEM中，最好在clientLib中撰寫程式碼，並將其包含在頁面（頁面的header.jsp或footer.jsp）中

若要在初始化表單後使用GuideBridge (請 `bridgeInitializeComplete` 事件已傳送)，請使用取得GuideBridge例項 `window.guideBridge`. 您可以使用檢查GuideBridge初始化狀態 `guideBride.isConnected` API。

#### GuideBridge事件 {#guidebridge-events}

GuideBridge也會在託管頁面上提供某些外部指令碼事件。 外部指令碼可監聽這些事件並執行各種作業。 例如，每當表單中的使用者名稱變更時，頁面標頭中顯示的名稱也會變更。 如需此類事件的詳細資訊，請參閱 [適用性表單的JavaScript資料庫API參考](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

使用下列程式碼來註冊處理常式：

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 建立欄位的自訂模式 {#creating-custom-patterns-for-a-field}

如上所述，調適型表單可讓作者提供驗證或顯示格式的模式。 除了使用現成可用的模式外，您還可以為最適化表單元件定義可重複使用的自訂模式。 例如，您可以定義文字欄位或數值欄位。 定義之後，您可以在指定元件型別的所有表單中使用這些模式。 例如，您可以為文字欄位建立自訂模式，並在其最適化表單的文字欄位中使用它。 您可以存取元件之「編輯」對話方塊中的「模式」區段，以選取自訂模式。 如需有關陣列定義或格式的詳細資訊，請參閱 [HTML5表單的Picture子句支援](/help/forms/using/picture-clause-support.md).

執行以下步驟來建立特定欄位型別的自訂模式，並重複用於相同型別的其他欄位：

1. 導覽至您編寫執行個體上的CRXDE Lite。
1. 建立資料夾以維護您的自訂模式。 在/apps目錄下，建立sling：folder型別的節點。 例如，以名稱建立節點 `customPatterns`. 在此節點下，建立另一個型別節點 `nt:unstructed` 並為其命名 `textboxpatterns`. 此節點包含您要新增的各種自訂模式。
1. 開啟已建立節點的「屬性」標籤。 例如，開啟的「屬性」標籤 `textboxpatterns`. 新增 `guideComponentType` 屬性並設定其值為 *fd/af/components/formatter/guideTextBox*.

1. 此屬性的值會依您要定義模式的欄位而有所不同。 數值欄位中， `guideComponentType` 屬性為 *fd/af/components/formatter/guideNumericBox*. 「日期挑選器」欄位的值為 *fd/af/components/formatter/guideDatepicker*.&quot;
1. 您可以將屬性指派給，以新增自訂模式 `textboxpatterns` 節點。 以名稱新增屬性(例如 `pattern1`)，並將其值設定為您要新增的模式。 例如，新增屬性 `pattern1` 值為Fax=text{99-999-9999999}。 此模式適用於您在Adaptive Forms中使用的所有文字方塊。

   ![為CrxDe中的欄位建立自訂模式](assets/creating-custom-patterns.png)

   建立自訂圖樣
