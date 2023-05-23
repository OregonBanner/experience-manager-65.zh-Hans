---
title: 將Forms呈現為HTML
seo-title: Rendering Forms as HTML
description: 使用Forms服務將表單轉譯為HTML，以回應來自網頁瀏覽器的HTTP請求。 您可以使用Java API和Web服務API將表單轉譯為HTML。
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 0%

---

# 將Forms呈現為HTML {#rendering-forms-as-html}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

Forms服務會根據來自網頁瀏覽器的HTTP請求，將表單轉譯為HTML。 將表單轉譯為HTML的好處是，使用者端網頁瀏覽器所在的電腦不需要Adobe Reader、Acrobat或Flash Player (適用於表單指南（已棄用）)。

若要將表單轉譯為HTML，表單設計必須儲存為XDP檔案。 儲存為PDF檔案的表單設計無法呈現為HTML。 在Designer中開發將轉譯為HTML的表單設計時，請考慮以下條件：

* 請勿使用物件的邊框屬性在表單上繪製線條、方塊或格點。 有些瀏覽器可能不會將邊界排列成與預覽中顯示的完全一致。 物件可能顯示為圖層狀，或可能將其他物件推離其預期位置。
* 您可以使用直線、矩形和圓來定義背景。
* 繪製的文字略大於容納文字所需的文字。 有些網頁瀏覽器無法清楚顯示文字。

>[!NOTE]
>
>呈現包含TIFF影像的表單時，使用 `FormServiceClient` 物件的 `(Deprecated) renderHTMLForm` 和 `renderHTMLForm2` 方法，在Internet Explorer或Mozilla Firefox瀏覽器中顯示的呈現HTML表單中，不會顯示TIFF影像。 這些瀏覽器不提供TIFF影像的原生支援。

## HTML頁面 {#html-pages}

當表單設計呈現為HTML表單時，每個第二層級子表單會呈現為HTML頁面（面板）。 您可以在Designer中檢視子表單的階層。 屬於根子表單的子表單（根子表單的預設名稱為form1）是面板子表單。 下列範例顯示表單設計的子表單。

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

當表單設計呈現為HTML表單時，面板不受任何特定頁面大小的限制。 如果您有動態子表單，應該將它們巢狀內嵌在面板子表單中。 動態子表單可擴充至無限數量的HTML頁面。

當表單呈現為HTML表單時，頁面大小(對呈現為PDF的表單進行分頁所必需)沒有意義。 由於具有可流動版面的表單可展開至無限數量的HTML頁面，請務必避免主版頁面上的頁尾。 主版頁面內容區域下方的頁尾可能會覆寫流經頁面邊界的HTML內容。

您必須使用，明確地在面板之間移動 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 您可以傳送表單至Forms服務，並讓Forms服務將表單轉譯回使用者端裝置（通常為網頁瀏覽器）來變更頁面。

>[!NOTE]
>
>將表單傳送至Forms服務，然後讓Forms服務將表單轉譯回使用者端裝置的程式，稱為將資料四捨五入至伺服器。

>[!NOTE]
>
>如果您想要自訂HTML表單上「HTML數位簽名」按鈕的外觀，您必須在fscdigsig.css檔案（在adobe-forms-ds.ear > adobe-forms-ds.war檔案中）中變更以下屬性：

**.fsc-ds-ssb**：此樣式表適用於空白符號欄位的情況。

**.fsc-ds-ssv**：此樣式表適用於有效符號欄位的情況。

**.fsc-ds-ssc**：此樣式表適用於有效符號欄位但資料已變更的情況。

**.fsc-ds-ssi**：此樣式表適用於無效符號欄位的情況。

**.fsc-ds-popup-bg**：未使用此樣式表屬性。

**.fsc-ds-popup-btn**：未使用此樣式表屬性。

## 執行指令碼 {#running-scripts}

表單作者會指定指令碼是在伺服器上還是使用者端上執行。 Forms服務會建立分散式的事件處理環境，以執行可在使用者端與伺服器之間使用的表單情報。 `runAt` 屬性。 如需此屬性或在表單設計中建立指令碼的相關資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn)

Forms服務可在表單轉譯時執行指令碼。 因此，您可以連線至資料庫或使用者端可能無法使用的Web服務，預先填入含有資料的表單。 您也可以設定按鈕的 `Click` 要在伺服器上執行的事件，讓使用者端往返資料至伺服器。 這可讓使用者端在使用者與表單互動時，執行可能需要伺服器資源的指令碼，例如企業資料庫。 對於HTML表單，formcalc指令碼只能在伺服器上執行。 因此，您必須標籤這些指令碼以在 `server` 或 `both`.

您可以藉由呼叫「 」，設計可在頁面（面板）之間移動的表單 `xfa.host.pageUp` 和 `xfa.host.pageDown` 方法。 此指令碼會放置在按鈕的 `Click` 事件與 `runAt` 屬性已設定為 `Both`. 您選擇的原因 `Both` 如此，Adobe Reader或Acrobat (適用於呈現為PDF的表單)就能在不前往伺服器的情況下變更頁面，而HTML表單則可藉由將擷取資料舍入至伺服器來變更頁面。 也就是說，表單會傳送至Forms服務，而表單會呈現為HTML，並顯示新頁面。

建議您不要將指令碼變數和表單欄位命名為相同的名稱，例如專案。 有些網頁瀏覽器（例如Internet Explorer）可能不會初始化與表單欄位同名的變數，進而導致指令碼錯誤。 為表單欄位和指令碼變數指定不同名稱是建議的做法。

在呈現包含頁面導覽功能和表單指令碼的HTML表單時（例如，假設指令碼在每次呈現表單時都會從資料庫擷取欄位資料），請確定表單指令碼位於form：calculate事件中，而不是form：readyevent中。

位於form：ready事件中的表單指令碼在表單的初始轉譯期間只會執行一次，而不會在後續的頁面擷取中執行。 相較之下，form：calculate事件會針對每個呈現表單的頁面導覽執行。

>[!NOTE]
在多頁表單中，如果您移至其他頁面，JavaScript對頁面所做的變更不會保留。

您可以在提交表單前叫用自訂指令碼。 此功能適用於所有可用瀏覽器。 但是，它只能在使用者轉譯具有它的HTML表單時使用 `Output Type` 屬性設定為 `Form Body`. 當 `Output Type` 是 `Full HTML`. 如需設定此功能的步驟，請參閱管理說明中的設定表單。

您必須先定義呼叫的回呼函式，才能提交表單，其中函式名稱為 `_user_onsubmit`. 我們假設函式不會擲回任何例外狀況，否則會忽略例外狀況。 建議將JavaScript函式放在html的head區段中；不過，您可以在指令碼標籤的結尾之前的任何位置宣告該函式，其中包括 `xfasubset.js`.

表單伺服器轉譯包含下拉式清單的XDP時，除了建立下拉式清單外，還會建立兩個隱藏的文字欄位。 這些文字欄位會儲存下拉式清單的資料（其中一個儲存選項的顯示名稱，另一個儲存選項的值）。 因此，每次使用者提交表單時，都會提交下拉式清單的完整資料。 假設您不想每次都提交那麼多的資料，您可以撰寫自訂指令碼來停用它。 例如：下拉式清單的名稱為 `drpOrderedByStateProv` 並將其包裝在子表單標題下。 HTML輸入元素的名稱將為 `header[0].drpOrderedByStateProv[0]`. 儲存及提交下拉式清單資料的隱藏欄位名稱如下： `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

如果您不想張貼資料，可以下列方式停用這些輸入元素。 `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## XFA子集 {#xfa-subsets}

建立要呈現為HTML的表單設計時，您必須將指令碼限製為JavaScript語言指令碼的XFA子集。

在使用者端上執行或在使用者端和伺服器上執行的指令碼必須寫入XFA子集中。 在伺服器上執行的指令碼可以使用完整的XFA指令碼模型，也可以使用FormCalc。 如需使用JavaScript的相關資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

在使用者端上執行指令碼時，只有目前顯示的面板可以使用指令碼；例如，當顯示面板B時，您無法針對面板A中的欄位編寫指令碼。 在伺服器上執行指令碼時，可以存取所有面板。

在使用者端執行的指令碼中使用指令碼物件模型(SOM)運算式時，也必須小心。 在使用者端上執行的指令碼僅支援SOM運算式的簡化子集。

## 事件計時 {#event-timing}

XFA子集會定義對應至HTML事件的XFA事件。 計算及驗證事件的時間在行為上稍有不同。 在網頁瀏覽器中，當您退出欄位時會執行完整的計算事件。 當您變更欄位值時，計算事件不會自動執行。 您可以藉由呼叫 `xfa.form.execCalculate` 方法。

在網頁瀏覽器中，驗證事件僅在退出欄位或提交表單時執行。 您可以使用強制驗證事件 `xfa.form.execValidate` 方法。

網頁瀏覽器中顯示的Forms (與Adobe Reader或Acrobat不同)符合必要欄位的XFA null測試（錯誤或警告）。

* 如果Null測試產生錯誤，而您結束欄位時並未指定值，則會顯示訊息方塊，且您會在按一下「確定」後重新定位至欄位。
* 如果Null測試產生警告，而您結束欄位時未指定值，系統會提示您按一下「確定」或「取消」，讓您選擇繼續但不指定值或返回欄位輸入值。

如需Null測試的詳細資訊，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

## 表單按鈕 {#form-buttons}

按一下提交按鈕會將表單資料傳送至Forms服務，並代表表單處理的結尾。 此 `preSubmit` 事件可設定為在使用者端或伺服器上執行。 此 `preSubmit` 事件會在提交表單之前執行（如果設定為在使用者端上執行）。 否則， `preSubmit` 事件會在表單提交期間在伺服器上執行。 如需更多有關「 」的資訊， `preSubmit` 事件，請參閱 [Forms設計工具](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

如果按鈕沒有關聯的使用者端指令碼，則會將資料提交至伺服器、在伺服器上執行計算，並重新產生HTML表單。 如果按鈕包含使用者端指令碼，資料不會傳送至伺服器，而使用者端指令碼會在網頁瀏覽器中執行。

## HTML4.0網頁瀏覽器 {#html-4-0-web-browser}

僅支援HTML4.0的網頁瀏覽器無法支援XFA子集使用者端指令碼模型。 建立可在HTML4.0和MSDHTML或CSS2HTML中運作的表單設計時，標示為在使用者端執行的指令碼實際上將會在伺服器上執行。 例如，假設使用者按一下位於HTML4.0網頁瀏覽器中所顯示表單上的按鈕。 在此情況下，表單資料會傳送至執行使用者端指令碼的伺服器。

建議您將表單邏輯置於計算事件中，這些計算事件會在HTML為4.0的伺服器上執行，並在MSDHTML或CSS2HTML的使用者端上執行。

## 維護簡報變更 {#maintaining-presentation-changes}

當您在HTML頁面（面板）之間移動時，只會保留資料的狀態。 不會維護背景顏色或強制欄位設定等設定（如果與初始設定不同）。 若要維持呈現狀態，您必須建立代表欄位呈現狀態的欄位（通常是隱藏的）。 如果您將指令碼新增至欄位的 `Calculate` 根據隱藏欄位值變更簡報的事件，您可以在HTML頁面（面板）之間來回移動時保留簡報狀態。

以下指令碼會維護 `fillColor` 的欄位，其值基於 `hiddenField`. 假設此指令碼位於欄位的 `Calculate` 事件。

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
巢狀內嵌於表格儲存格時，靜態物件不會顯示在演算後的HTML表單中。 例如，巢狀在表格儲存格內的圓形和矩形不會顯示在轉譯HTML表單中。 不過，當這些相同的靜態物件位於表格外部時，會正確顯示。

## 數位簽署HTML表單 {#digitally-signing-html-forms}

如果表單呈現為下列HTML轉換之一，則您無法簽署包含數位簽名欄位的HTML表單：

* AHTML
* HTML4
* StaticHTML
* NoScriptXHTML

如需以數位方式簽署檔案的相關資訊，請參閱 [數位簽署和認證檔案](/help/forms/developing/digitally-signing-certifying-documents.md)

## 呈現符合協助工具指南的XHTML表單 {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

您可以呈現符合協助工具准則的完整HTML表單。 也就是說，表單會在完整HTML標籤中呈現，而不是在body標籤中呈現HTML表單(不是完整的HTML頁面)。

## 驗證表單資料 {#validating-form-data}

在將表單轉譯為HTML表單時，建議您限制對表單欄位使用驗證規則。 HTML表單可能不支援某些驗證規則。 例如，將MM-DD-YYYY的驗證模式套用至 `Date/Time` 位於呈現為HTML表單之表單設計中的欄位，即使正確輸入日期，也無法正常運作。 不過，此驗證模式適用於轉譯為PDF的表單。

>[!NOTE]
如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 步驟摘要 {#summary-of-steps}

若要呈現HTML表單，請執行下列步驟：

1. 包含專案檔案。
1. 建立Forms使用者端API物件。
1. 設定HTML執行階段選項。
1. 呈現HTML表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請確定您包含Proxy檔案。

**建立Forms使用者端API物件**

您必須先建立表單資料整合服務使用者端，才能以程式設計方式將資料匯入PDF表單使用者端API。 建立服務使用者端時，您可以定義呼叫服務所需的連線設定。

**設定HTML執行階段選項**

呈現HTML表單時，您可以設定HTML執行階段選項。 例如，您可以將工具列新增至HTML表單，讓使用者能夠選取位於使用者端電腦上的檔案附件，或擷取以HTML表單呈現的檔案附件。 HTML工具列預設為停用。 若要將工具列新增至HTML表單，您必須以程式設計方式設定執行階段選項。 依預設，HTML工具列包含下列按鈕：

* `Home`：提供應用程式網頁根目錄的連結。
* `Upload`：提供使用者介面，以選取要附加至目前表單的檔案。
* `Download`：提供顯示附加檔案的使用者介面。

當HTML工具列出現在HTML表單上時，使用者可以選擇最多10個要與表單資料一起提交的檔案。 提交檔案後，Forms服務即可擷取檔案。

將表單轉譯為HTML時，您可以指定使用者代理程式值。 使用者代理程式值提供瀏覽器和系統資訊。 這是選用值，您可以傳遞空字串值。 使用Java API快速入門呈現HTML表單會顯示如何取得使用者代理程式值，並使用它來將表單呈現為HTML。

使用Forms服務使用者端API設定目標URL即可指定表單資料張貼處的HTTP URL，或可在XDP表單設計內含的提交按鈕中指定。 如果在表單設計中指定了目標URL，則請勿使用Forms服務使用者端API設定值。

>[!NOTE]
使用工具列呈現HTML表單為選用。

>[!NOTE]
如果您轉譯AHTML表單，建議您不要將工具列新增至表單。

**呈現HTML表單**

若要呈現HTML表單，您必須指定在Designer中建立並儲存為XDP檔案的表單設計。 您也必須選取HTML轉換型別。 例如，您可以指定轉譯Internet Explorer 5.0或更新版本之動態HTML的HTML轉換型別。

呈現HTML表單也需要值，例如呈現其他表單型別所需的URI值。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯HTML表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流。 寫入使用者端網頁瀏覽器時，使用者可看到HTML表單。

**另请参阅**

[使用Java API將表單轉譯為HTML](#render-a-form-as-html-using-the-java-api)

[使用Web服務API將表單轉譯為HTML](#render-a-form-as-html-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[使用自訂工具列呈現HTMLForms](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API將表單轉譯為HTML {#render-a-form-as-html-using-the-java-api}

使用Forms API (Java)轉譯HTML表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms使用者端API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定HTML執行階段選項

   * 建立 `HTMLRenderSpec` 物件（使用其建構函式）。
   * 若要使用工具列呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setHTMLToolbar` 方法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`.
   * 若要設定HTML表單的地區設定值，請叫用 `HTMLRenderSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。 （此為選擇性設定）。
   * 若要在完整HTML標籤內呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setOutputType` 方法與傳遞 `OutputType.FullHTMLTags`. （此為選擇性設定）。

   >[!NOTE]
   Forms無法成功在HTML中呈現，當 `StandAlone` 選項為 `true` 和 `ApplicationWebRoot` 會參考裝載AEM Forms之J2EE應用程式伺服器以外的伺服器( `ApplicationWebRoot` 值是使用 `URLSpec` 傳遞至的物件 `FormsServiceClient` 物件的 `(Deprecated) renderHTMLForm` 方法)。 當 `ApplicationWebRoot` 是另一部託管AEM Forms的伺服器，管理控制檯中的Web根URI值需要設定為表單的Web應用程式URI值。 您可以登入管理主控台，按一下「服務> Forms」，然後將Web根URI設為https://server-name:port/FormServer，即可完成這項作業。 然後，儲存您的設定。

1. 呈現HTML表單

   叫用 `FormsServiceClient` 物件的 `(Deprecated) renderHTMLForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML偏好設定型別的列舉值。 例如，若要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * 此 `HTMLRenderSpec` 儲存HTML執行階段選項的物件。
   * 字串值，指定 `HTTP_USER_AGENT` 標頭值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 儲存轉譯HTML表單所需的URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `(Deprecated) renderHTMLForm` 方法傳回 `FormsResult` 包含可寫入使用者端網頁瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[將Forms呈現為HTML](#rendering-forms-as-html)

[快速入門（SOAP模式）：使用Java API轉譯HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服務API將表單轉譯為HTML {#render-a-form-as-html-using-the-web-service-api}

使用Forms API （Web服務）轉譯HTML表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 將Java Proxy類別納入您的類別路徑中。

1. 建立Forms使用者端API物件

   建立 `FormsService` 物件並設定驗證值。

1. 設定HTML執行階段選項

   * 建立 `HTMLRenderSpec` 物件（使用其建構函式）。
   * 若要使用工具列呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setHTMLToolbar` 方法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`.
   * 若要設定HTML表單的地區設定值，請叫用 `HTMLRenderSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 若要在完整HTML標籤內呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setOutputType` 方法與傳遞 `OutputType.FullHTMLTags`.

   >[!NOTE]
   Forms無法成功在HTML中呈現，當 `StandAlone` 選項為 `true` 和 `ApplicationWebRoot` 會參考裝載AEM Forms之J2EE應用程式伺服器以外的伺服器( `ApplicationWebRoot` 值是使用 `URLSpec` 傳遞至的物件 `FormsServiceClient` 物件的 `(Deprecated) renderHTMLForm` 方法)。 當 `ApplicationWebRoot` 是另一部託管AEM Forms的伺服器，管理控制檯中的Web根URI值需要設定為表單的Web應用程式URI值。 您可以登入管理主控台，按一下「服務> Forms」，然後將Web根URI設為https://server-name:port/FormServer，即可完成這項作業。 然後，儲存您的設定。

1. 呈現HTML表單

   叫用 `FormsService` 物件的 `(Deprecated) renderHTMLForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML偏好設定型別的列舉值。 例如，若要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`. (請參閱 [使用可流動版面預先填入Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * 此 `HTMLRenderSpec` 儲存HTML執行階段選項的物件。
   * 字串值，指定 `HTTP_USER_AGENT` 標頭值；例如， `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. 如果您不想設定此值，可以傳遞空字串。
   * A `URLSpec` 儲存轉譯HTML表單所需的URI值的物件。 (請參閱 [指定URI值](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。 (請參閱 [將檔案附加至表單](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 此引數值會儲存演算後的表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 方法填入的物件。 此引數會儲存輸出XML資料。
   * 空白 `javax.xml.rpc.holders.LongHolder` 方法填入的物件。 此引數會儲存表單中的頁數。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 此引數將會儲存地區設定值。
   * 空白 `javax.xml.rpc.holders.StringHolder` 方法填入的物件。 此引數將會儲存所使用的HTML演算值。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `(Deprecated) renderHTMLForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[將Forms呈現為HTML](#rendering-forms-as-html)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
