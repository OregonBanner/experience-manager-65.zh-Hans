---
title: 開發Forms (Classic UI)
seo-title: Developing Forms (Classic UI)
description: 瞭解如何開發表單
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---

# 開發Forms (Classic UI){#developing-forms-classic-ui}

表單的基本結構為：

* 表單開始
* 表單元素
* 表單結尾

所有這些都是透過一系列預設值實現的 [表單元件](/help/sites-authoring/default-components.md#form)，適用於標準AEM安裝。

除了 [開發新元件](/help/sites-developing/developing-components-samples.md) 若要在表單上使用，您也可以：

* [使用值預先載入您的表單](#preloading-form-values)
* [預先載入（特定）具有多個值的欄位](#preloading-form-fields-with-multiple-values)
* [開發新動作](#developing-your-own-form-actions)
* [開發新的限制](#developing-your-own-form-constraints)
* [顯示或隱藏特定表單欄位](#showing-and-hiding-form-components)

[使用指令碼](#developing-scripts-for-use-with-forms) 以視需要擴充功能。

>[!NOTE]
>
>本檔案著重於使用開發表單 [基礎元件](/help/sites-authoring/default-components-foundation.md) 在傳統UI中。 Adobe建議使用新的 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [隱藏條件](/help/sites-developing/hide-conditions.md) 用於觸控式UI中的表單開發。

## 預先載入表單值 {#preloading-form-values}

表單開始元件提供 **載入路徑**，指向存放庫中節點的可選路徑。

載入路徑是節點屬性的路徑，用於將預先定義的值載入表單上的多個欄位中。

此選擇性欄位指定存放庫中節點的路徑。 當此節點具有符合欄位名稱的屬性時，則表單上的適當欄位將使用這些屬性的值預先載入。 如果不存在相符專案，則欄位包含預設值。

>[!NOTE]
>
>A [表單動作](#developing-your-own-form-actions) 也可以設定載入初始值的來源。 這是使用來完成的 `FormsHelper#setFormLoadResource` 裡面 `init.jsp`.
>
>只有未設定時，才會從作者在起始表單元件中設定的路徑填入表單。

### 預先載入具有多個值的表單欄位 {#preloading-form-fields-with-multiple-values}

各種表單欄位也具有 **專案載入路徑**，也是指向存放庫中的節點的可選路徑。

此 **專案載入路徑** 是節點屬性的路徑，用來將預先定義的值載入表單上的特定欄位，例如 [下拉式清單](/help/sites-authoring/default-components-foundation.md#dropdown-list)， [核取方塊群組](/help/sites-authoring/default-components-foundation.md#checkbox-group) 或 [選項群組](/help/sites-authoring/default-components-foundation.md#radio-group).

#### 範例 — 預先載入含有多個值的下拉式清單 {#example-preloading-a-dropdown-list-with-multiple-values}

下拉式清單可設定您選取的值範圍。

此 **專案載入路徑** 可用來從存放庫中的資料夾存取清單，並將清單預先載入欄位中：

1. 建立新的sling資料夾( `sling:Folder`)例如， `/etc/designs/<myDesign>/formlistvalues`

1. 新增屬性(例如， `myList`)的字串( `String[]`)以包含下拉式清單中的專案。 也可以使用指令碼匯入內容，例如使用JSP指令碼或shell指令碼中的cURL。

1. 在中使用完整路徑 **專案載入路徑** 欄位：例如， `/etc/designs/geometrixx/formlistvalues/myList`

請注意，如果 `String[]` 格式如下：

* `AL=Alabama`
* `AK=Alaska`
* 以此类推。

然後AEM將產生「 」清單為：

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

舉例來說，這項功能可以在多語言設定中妥善運用。

### 開發您自己的表單動作 {#developing-your-own-form-actions}

表單需要動作。 動作會定義隨使用者資料提交表單時執行的操作。

標準AEM安裝提供了一系列動作，這些動作可在下列位置檢視：

`/libs/foundation/components/form/actions`

和 **動作型別** 以下專案的清單 **表單** 元件：

![chlimage_1-8](assets/chlimage_1-8.png)

本節說明如何開發自己的表單動作以包含在此清單中。

您可以在底下新增自己的動作 `/apps` 如下所示：

1. 建立型別的節點 `sling:Folder`. 指定要實作之動作的名稱。

   例如：

   `/apps/myProject/components/customFormAction`

1. 在此節點上定義下列屬性，然後按一下 **全部儲存** 若要保留您的變更：

   * `sling:resourceType`  — 設為 `foundation/components/form/action`

   * `componentGroup`  — 定義為 `.hidden`

   * 選擇性：

      * `jcr:title`  — 指定您選擇的標題，這會顯示在下拉式選擇清單中。 如果未設定，則會顯示節點名稱

      * `jcr:description`  — 輸入您選擇的說明

1. 在資料夾中建立對話方塊節點：

   1. 新增欄位，以便在選擇動作後，作者可以編輯表單對話方塊。

1. 在資料夾中建立：

   1. 貼文指令碼。
指令碼的名稱為 `post.POST.<extension>`，例如 `post.POST.jsp`
提交表單以處理表單時會叫用貼文指令碼，其中包含處理表單所傳送資料的程式碼 
`POST`。

   1. 新增在提交表單時叫用的轉寄指令碼。
指令碼的名稱為 `forward.<extension`>，例如 `forward.jsp`
此指令碼可定義路徑。 然後會將目前的請求轉送至指定的路徑。
   必要的呼叫是 `FormsHelper#setForwardPath` （2種變體）。 典型案例是執行一些驗證或邏輯，以尋找目標路徑，然後前進到該路徑，讓預設的SlingPOSTservlet在JCR中執行實際儲存。

   也可能會有另一個servlet執行實際處理，在這種情況下，表單動作和 `forward.jsp` 只能當作「粘合」程式碼。 這方面的範例為郵件動作： `/libs/foundation/components/form/actions/mail`，會將詳細資料轉送至 `<currentpath>.mail.html`郵件servlet所在的位置。

   所以：

   * a `post.POST.jsp` 對於完全由動作本身完成的小型作業非常有用
   * 而 `forward.jsp` 在只需要委派時很有用。

   指令碼的執行順序為：

   * 呈現表單時( `GET`)：

      1. `init.jsp`
      1. 對於所有欄位的限制： `clientvalidation.jsp`
      1. 表單的validationRt： `clientvalidation.jsp`
      1. 表單已透過載入資源載入（如果已設定）
      1. `addfields.jsp` 在演算內時 `<form></form>`
   * 處理表單時 `POST`：

      1. `init.jsp`
      1. 對於所有欄位的限制： `servervalidation.jsp`
      1. 表單的validationRt： `servervalidation.jsp`
      1. `forward.jsp`
      1. 若已設定正向路徑( `FormsHelper.setForwardPath`)、轉送請求，然後呼叫 `cleanup.jsp`

      1. 如果未設定轉送路徑，請呼叫 `post.POST.jsp` (結尾為，否 `cleanup.jsp` called)




1. 再次在資料夾中選擇性新增：

   1. 用於新增欄位的指令碼。
指令碼的名稱為 `addfields.<extension>`，例如 `addfields.jsp`
一個 
`addfields` 在寫入表單開頭的HTML後，會立即叫用指令碼。 這可讓動作在表單內新增自訂輸入欄位或其他此類HTML。

   1. 初始化指令碼。
指令碼的名稱為 `init.<extension>`，例如 `init.jsp`
此指令碼會在表單轉譯時叫用。 它可用來初始化動作細節。

   1. 清除指令碼。
指令碼的名稱為 `cleanup.<extension>`，例如 `cleanup.jsp`
此指令碼可用於執行清理。

1. 使用 **Forms** parsys中的元件。 此 **動作型別** 下拉式清單現在會包含您的新動作。

   >[!NOTE]
   >
   >若要檢視屬於產品一部分的預設動作：
   >
   >
   >`/libs/foundation/components/form/actions`

### 開發您自己的表單限制 {#developing-your-own-form-constraints}

限制可施加於兩個層級：

* 對象 [個別欄位（請參閱下列程式）](#constraints-for-individual-fields)
* 作為 [表單全域驗證](#form-global-constraints)

#### 個別欄位的限制 {#constraints-for-individual-fields}

您可以為個別欄位新增自己的限制(在 `/apps`)如下所示：

1. 建立型別的節點 `sling:Folder`. 指定反映要實作之限制的名稱。

   例如：

   `/apps/myProject/components/customFormConstraint`

1. 在此節點上定義下列屬性，然後按一下 **全部儲存** 若要保留您的變更：

   * `sling:resourceType`  — 設定為 `foundation/components/form/constraint`

   * `constraintMessage`  — 提交表單時，根據限制，如果欄位無效將顯示自訂訊息

   * 選擇性：

      * `jcr:title`  — 指定您選擇的標題，這會顯示在選擇清單中。 如果未設定，則會顯示節點名稱
      * `hint`  — 使用者如何使用該欄位的額外資訊

1. 在此資料夾中，您可能需要下列指令碼：

   * 使用者端驗證指令碼：指令碼的名稱為 `clientvalidation.<extension>`，例如 `clientvalidation.jsp`
這會在表單欄位轉譯時叫用。 它可用來建立使用者端JavaScript來驗證使用者端上的欄位。

   * 伺服器驗證指令碼：指令碼的名稱為 `servervalidation.<extension>`，例如 `servervalidation.jsp`
這會在提交表單時叫用。 提交欄位後，可使用它來驗證伺服器上的欄位。

>[!NOTE]
>
>範例限制可見於：
>
>`/libs/foundation/components/form/constraints`

#### 表單全域限制 {#form-global-constraints}

透過在起始表單元件( `validationRT`)。 例如：

`apps/myProject/components/form/validation`

然後，您可以定義：

* a `clientvalidation.jsp`  — 插入在欄位的使用者端驗證指令碼之後
* 和 `servervalidation.jsp`  — 也是在個別欄位伺服器驗證之後呼叫 `POST`.

### 顯示和隱藏表單元件 {#showing-and-hiding-form-components}

您可以根據表單中其他欄位的值，設定表單以顯示或隱藏表單元件。

只有在特定條件下才需要表單欄位時，變更欄位的可見度會很有用。 例如，在意見回饋表單上，系統會詢問客戶是否希望以電子郵件傳送產品資訊。 選取「是」後，會出現文字欄位，讓客戶輸入其電子郵件地址。

使用 **編輯顯示/隱藏規則** 對話方塊來指定顯示或隱藏表單元件的條件。

![showhideeditor](assets/showhideeditor.png)

使用對話方塊頂端的欄位來指定下列資訊：

* 指定隱藏或顯示元件的條件。
* 顯示或隱藏元件是否需要任何或全部條件為true。

一或多個條件會顯示在這些欄位下方。 條件會將另一個表單元件（在相同表單上）的值與一個值比較。 如果欄位中的實際值符合條件，則條件的評估結果為true。 條件包括下列資訊：

* 測試的表單欄位的標題。
* 運運算元。
* 比對的值會與欄位值比較。

例如，標題為「 」的選項群組元件 `Receive email notifications?`* *包含 `Yes` 和 `No` 選項按鈕。 標題為「 」的文字欄位元件 `Email Address` 會使用以下條件，以便在以下情況下可見： `Yes` 已選取：

![SHOWHIDECONDITION](assets/showhidecondition.png)

在Javascript中，條件會使用Element Name屬性的值來參照欄位。 在上一個範例中，「選項群組」元件的「元素名稱」屬性是 `contact`. 下列程式碼為該範例的等效Javascript程式碼：

`((contact == "Yes"))`

**若要顯示或隱藏表單元件：**

1. 編輯特定的表單元件。

1. 選取 **顯示/隱藏** 以開啟 **編輯顯示/隱藏規則** 對話方塊：

   * 在第一個下拉式清單中選取 **顯示** 或 **隱藏** 以指定條件是否決定要顯示或隱藏元件。

   * 在頂端行尾的下拉式清單中選取：

      * **全部**  — 如果所有條件都必須為true才能顯示或隱藏元件
      * **任何**  — 如果只有一個或多個條件必須為true以顯示或隱藏元件
   * 在條件行（預設為其中一行）中，選取元件、運運算元，然後指定值。
   * 視需要按一下「 」，以新增更多條件 **新增條件**.

   例如：

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 按一下 **確定** 以儲存定義。

1. 儲存定義後， **編輯規則** 連結會出現在 **顯示/隱藏** 選項中設定的預設值。 按一下此連結以開啟 **編輯顯示/隱藏規則** 進行變更的對話方塊。

   按一下 **確定** 以儲存所有變更。

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >可以看見並測試「顯示/隱藏」定義的效果：
   >
   >* 在 **預覽** 作者環境上的模式（第一次切換為預覽時需要重新載入頁面）
   >
   >* 在發佈環境中


#### 處理損壞的元件參照 {#handling-broken-component-references}

顯示/隱藏條件會使用Element Name屬性的值來參照表單中的其他元件。 當任何條件引用已刪除或已變更Element Name屬性的元件時，顯示/隱藏設定無效。 發生這種情況時，您需要手動更新條件，否則表單載入時發生錯誤。

當「顯示/隱藏」設定無效時，設定僅以JavaScript程式碼形式提供。 編輯程式碼以修正問題。程式碼會使用原本用來參考元件的Element Name屬性。

### 開發指令碼以與Forms搭配使用 {#developing-scripts-for-use-with-forms}

如需可在編寫指令碼時使用的API元素的詳細資訊，請參閱 [與表單相關的javadoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

您可以將此用於動作，例如在提交表單前呼叫服務，以及在服務失敗時取消服務：

* 定義驗證資源型別
* 包含用於驗證的指令碼：

   * 在您的JSP中，呼叫您的Web服務並建立 `com.day.cq.wcm.foundation.forms.ValidationInfo` 包含錯誤訊息的物件。 如果出現錯誤，將不會發佈表單資料。
