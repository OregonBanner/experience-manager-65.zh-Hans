---
title: 使用CustomToolbars呈現HTMLForms
seo-title: Rendering HTML Forms with CustomToolbars
description: 使用Forms服務來自訂以HTML表單呈現的工具列。 您可以使用Java API和Web服務API，使用自訂工具列來轉譯HTML表單。
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用CustomToolbars呈現HTMLForms {#rendering-html-forms-with-customtoolbars}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

## 使用自訂工具列呈現HTMLForms {#rendering-html-forms-with-custom-toolbars}

Forms服務可讓您自訂以HTML表單呈現的工具列。 您可以自訂工具列，以透過覆寫預設CSS樣式來變更其外觀，並透過覆寫Java指令碼來新增動態行為。 使用名為fscmenu.xml的XML檔案自訂工具列。 依預設，Forms服務會從內部指定的URI位置擷取此檔案。

>[!NOTE]
>
>此URI位置位於adobe-forms-core.jar檔案中，該檔案位於adobe-forms-dsc.jar檔案中。 adobe-forms-dsc.jar檔案位於C:\Adobe\Adobe_Experience_Manager_forms\資料夾(C:\是安裝目錄)。 您可以使用檔案擷取工具（例如Win RAR）來開啟Adobe。

您可以從此位置複製fscmenu.xml，修改它以符合您的要求，然後將其置於自訂URI位置。 接下來，使用Forms Service API，從指定位置使用您的fscmenu.xml檔案設定導致Forms服務的執行階段選項。 這些動作會導致Forms服務呈現具有自訂工具列的HTML表單。

除了fscmenu.xml檔案外，您還需要取得下列檔案：

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS是與每個節點相關聯的Java指令碼。 必須為以下專案提供一個 `div#fscmenu` 節點和（選擇性） `ul#fscmenuItem` 節點。 JS檔案會實作核心工具列功能，且預設檔案也可運作。

fscCSS是與特定節點相關聯的樣式表。 CSS檔案中的樣式會指定工具列外觀。 *fscVCSS* 是垂直工具列的樣式表，顯示在已轉譯HTML表單的左側。 *fscIECSS* 是樣式表，用於HTML在Internet Explorer中轉譯的表單。

確定上述所有檔案都在fscmenu.xml檔案中參照。 也就是說，在fscmenu.xml檔案中，指定指向這些檔案的URI位置，讓Forms服務可以找到它們。 依預設，這些檔案可在以內部關鍵字開頭的URI位置取得 `FSWebRoot` 或 `ApplicationWebRoot`.

若要自訂工具列，請使用外部關鍵字取代關鍵字 `FSToolBarURI`. 此關鍵字代表在執行階段傳遞至Forms服務的URI （此作法稍後會在本小節中顯示）。

您也可以指定這些JS和CSS檔案的絕對位置，例如https://www.mycompany.com/scripts/misc/fscmenu.js。 在此情況下，您不需要使用 `FSToolBarURI` 關鍵字。

>[!NOTE]
>
>不建議您混合參考這些檔案的方式。 也就是說，所有URI都應該透過以下其中一種方式來參照： `FSToolBarURI` 關鍵字或絕對位置。

您可以開啟adobe-forms以取得JS和CSS檔案。&lt;appserver>.ear檔案。 在此檔案中，開啟adobe-forms-res.war。 所有這些檔案都位於WAR檔案中。 Adobe-forms-&lt;appserver>.ear檔案位於AEM forms安裝資料夾中(C:\是安裝目錄)。 您可以開啟Adobe Forms-&lt;appserver>.ear使用檔案擷取工具，例如WinRAR。

下列XML語法顯示範例fscmenu.xml檔案。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>粗體文字代表必須參考之CSS和JS檔案的URI。

下列專案說明如何自訂工具列：

* 變更值 `fscJS`， `fscCSS`， `fscVCSS`， `fscIECSS` 屬性（在fscmenu.xml檔案中），以使用本節中說明的其中一種方法來反映參照檔案的自訂位置(例如， `fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* 必須指定所有CSS和JS檔案。 如果未修改任何檔案，請在自訂位置提供預設檔案。 您可以依照本節所述開啟各種檔案來取得預設檔案。
* 允許為任何檔案提供絕對參照(例如https://www.example.com/scripts/custom-vertical-fscmenu.css)。
* JS和CSS檔案將 `div#fscmenu` 節點需要工具列功能的必要專案。 個人 `ul#fscmenuItem` 節點可能有或沒有支援的JS或CSS檔案。

**變更本機值**

在自訂工具列時，您可以變更工具列的地區設定值。 也就是說，您可以用其他語言顯示它。 下圖顯示以法文顯示的自訂工具列。

>[!NOTE]
>
>無法建立多種語言的自訂工具列。 工具列無法根據地區設定使用不同的XML檔案。

若要變更工具列的地區設定值，請確定fscmenu.xml檔案包含您要顯示的語言。 下列XML語法顯示用來顯示法文工具列的fscmenu.xml檔案。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>與此區段相關聯的「快速入門」會使用此XML檔案來顯示法文自訂工具列，如上圖所示。

此外，請叫用 `HTMLRenderSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。 例如，通過 `fr_FR` 以指定法文。 Forms服務隨附本地化工具列。

>[!NOTE]
>
>在轉譯使用自訂工具列的HTML表單之前，您必須知道HTML表單的轉譯方式。 (請參閱 [將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md).)

如需Forms服務的詳細資訊，請參閱 [AEM Forms的服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

若要呈現包含自訂工具列的HTML表單，請執行下列工作：

1. 包含專案檔案。
1. 建立Forms Java API物件。
1. 參考自訂fscmenu XML檔案。
1. 呈現HTML表單。
1. 將表單資料流寫入使用者端網頁瀏覽器。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請包含Proxy檔案。

**建立Forms Java API物件**

您必須先建立Forms使用者端物件，才能以程式設計方式執行Forms服務支援的操作。

**參考自訂fscmenu XML檔案**

若要呈現包含自訂工具列的HTML表單，請參照描述工具列的fscmenu XML檔案。 （本節提供兩個fscmenu XML檔案的範例。） 此外，請確定fscmenu.xml檔案正確指定所有參照檔案的位置。 如本節先前所述，請確定所有檔案都由 `FSToolBarURI` 關鍵字或其絕對位置。

**呈現HTML表單**

若要呈現HTML表單，請指定在Designer中建立並儲存為XDP檔案的表單設計。 同時選取HTML轉換型別。 例如，您可以指定轉譯Internet Explorer 5.0或更新版本之動態HTML的HTML轉換型別。

呈現HTML表單也需要值，例如呈現其他表單型別的URI值。

**將表單資料流寫入使用者端網頁瀏覽器**

Forms服務轉譯HTML表單時，會傳回您必須寫入使用者端網頁瀏覽器的表單資料流，才能讓使用者看到HTML表單。

**另请参阅**

[使用Java API呈現具有自訂工具列的HTML表單](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[使用Web服務API呈現具有自訂工具列的HTML表單](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服務API快速入門](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈現互動式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[將Forms呈現為HTML](/help/forms/developing/rendering-forms-html.md)

[建立轉譯Forms的網頁應用程式](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API呈現具有自訂工具列的HTML表單 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

使用Forms Service API (Java)呈現包含自訂工具列的HTML表單：

1. 包含專案檔案

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-forms-client.jar。

1. 建立Forms Java API物件

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `FormsServiceClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 參考自訂fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 物件（使用其建構函式）。
   * 若要使用工具列呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setHTMLToolbar` 方法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`.
   * 透過叫用 `HTMLRenderSpec` 物件的 `setToolbarURI` 方法並傳遞字串值，以指定XML檔案的URI位置。
   * 如果適用，請叫用 `HTMLRenderSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。 預設值為English。

   >[!NOTE]
   >
   >與此區段關聯的「快速入門」會將此值設定為 `fr_FR`*.*

1. 呈現HTML表單

   叫用 `FormsServiceClient` 物件的 `renderHTMLForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML偏好設定型別的列舉值。 例如，若要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞空白 `com.adobe.idp.Document` 物件。
   * 此 `HTMLRenderSpec` 儲存HTML執行階段選項的物件。
   * 字串值，指定 `HTTP_USER_AGENT` 標頭值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` 儲存轉譯HTML表單所需的URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此為選用引數，您可以指定 `null` 如果您不想將檔案附加至表單。

   此 `renderHTMLForm` 方法傳回 `FormsResult` 包含必須寫入使用者端Web瀏覽器的表單資料流的物件。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `com.adobe.idp.Document` 物件(透過叫用 `FormsResult` 物件 `getOutputContent` 方法。
   * 取得的內容型別 `com.adobe.idp.Document` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `com.adobe.idp.Document` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立 `java.io.InputStream` 物件(透過叫用 `com.adobe.idp.Document` 物件的 `getInputStream` 方法。
   * 建立位元組陣列，並叫用 `InputStream` 物件的 `read` 方法，並將位元組陣列作為引數傳遞。
   * 叫用 `javax.servlet.ServletOutputStream` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[快速入門（SOAP模式）：使用Java API使用自訂工具列轉譯HTML表單](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API呈現具有自訂工具列的HTML表單 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

使用Forms Service API （Web服務）呈現包含自訂工具列的HTML表單：

1. 包含專案檔案

   * 建立使用Forms服務WSDL的Java Proxy類別。
   * 在類別路徑中加入Java Proxy類別。

1. 建立Forms Java API物件

   建立 `FormsService` 物件並設定驗證值。

1. 參考自訂fscmenu XML檔案

   * 建立 `HTMLRenderSpec` 物件（使用其建構函式）。
   * 若要使用工具列呈現HTML表單，請叫用 `HTMLRenderSpec` 物件的 `setHTMLToolbar` 方法並傳遞 `HTMLToolbar` 列舉值。 例如，若要顯示垂直HTML工具列，請傳遞 `HTMLToolbar.Vertical`.
   * 透過叫用 `HTMLRenderSpec` 物件的 `setToolbarURI` 方法並傳遞字串值，以指定XML檔案的URI位置。
   * 如果適用，請叫用 `HTMLRenderSpec` 物件的 `setLocale` 方法並傳遞字串值，以指定地區設定值。 預設值為English。

   >[!NOTE]
   >
   >與此區段關聯的「快速入門」會將此值設定為 `fr_FR`*.*

1. 呈現HTML表單

   叫用 `FormsService` 物件的 `renderHTMLForm` 方法並傳遞下列值：

   * 字串值，指定表單設計名稱，包括副檔名。 如果您參照的表單設計屬於Forms應用程式的一部分，請務必指定完整路徑，例如 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` 指定HTML偏好設定型別的列舉值。 例如，若要呈現與Internet Explorer 5.0或更新版本的動態HTML相容的HTML表單，請指定 `TransformTo.MSDHTML`.
   * A `BLOB` 包含要與表單合併之資料的物件。 如果您不想合併資料，請傳遞 `null`.
   * 此 `HTMLRenderSpec` 儲存HTML執行階段選項的物件。
   * 字串值，指定 `HTTP_USER_AGENT` 標頭值，例如 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)。 如果您不想設定此值，可以傳遞空字串。
   * A `URLSpec` 儲存轉譯HTML表單所需的URI值的物件。
   * A `java.util.HashMap` 儲存檔案附件的物件。 此引數為選用引數，您可以指定 `null` 如果您不打算將檔案附加至表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數值會儲存演算後的表單。
   * 空白 `com.adobe.idp.services.holders.BLOBHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存輸出XML資料。
   * 空白 `javax.xml.rpc.holders.LongHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存表單中的頁數。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存地區設定值。
   * 空白 `javax.xml.rpc.holders.StringHolder` 由填入的物件 `renderHTMLForm` 方法。 此引數會儲存所使用的HTML演算值。
   * 空白 `com.adobe.idp.services.holders.FormsResultHolder` 將包含此作業結果的物件。

   此 `renderHTMLForm` 方法填入 `com.adobe.idp.services.holders.FormsResultHolder` 以表單資料流傳遞作為最後一個引數值的物件，必須寫入使用者端Web瀏覽器。

1. 將表單資料流寫入使用者端網頁瀏覽器

   * 建立 `FormResult` 物件，方法是取得 `com.adobe.idp.services.holders.FormsResultHolder` 物件的 `value` 資料成員。
   * 建立 `BLOB` 包含表單資料的物件(透過叫用 `FormsResult` 物件的 `getOutputContent` 方法。
   * 取得的內容型別 `BLOB` 物件(透過叫用其 `getContentType` 方法。
   * 設定 `javax.servlet.http.HttpServletResponse` 物件的內容型別，透過叫用其 `setContentType` 方法和傳遞的內容型別 `BLOB` 物件。
   * 建立 `javax.servlet.ServletOutputStream` 用來將表單資料流寫入使用者端網頁瀏覽器的物件，方法是叫用 `javax.servlet.http.HttpServletResponse` 物件的 `getOutputStream` 方法。
   * 建立位元組陣列，並透過叫用 `BLOB` 物件的 `getBinaryData` 方法。 此任務指派 `FormsResult` 物件至位元組陣列。
   * 叫用 `javax.servlet.http.HttpServletResponse` 物件的 `write` 將表單資料流傳送至使用者端Web瀏覽器的方法。 將位元組陣列傳遞至 `write` 方法。

**另请参阅**

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
