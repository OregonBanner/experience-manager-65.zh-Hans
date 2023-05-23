---
title: 條碼式Forms服務
seo-title: Using AEM Forms Barcoded Forms Service
description: 使用AEM Forms條碼Forms服務，從條碼的電子影像擷取資料。
seo-description: Use AEM Forms Barcoded Forms service to extract data from electronic images of barcodes.
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 條碼式Forms服務{#barcoded-forms-service}

## 概述 {#overview}

條碼Forms服務會從條碼的電子影像中擷取資料。 此服務接受包含一或多個條碼作為輸入的TIFF和PDF檔案，並擷取條碼資料。 條碼資料可以透過各種方式格式化，包括XML、分隔字串或任何使用JavaScript建立的自訂格式。

條碼式Forms服務支援下列專案 **二維(2D)** 作為掃描的TIFF或PDF檔案提供的符號：

* PDF417
* 資料矩陣
* QR碼

此服務也支援下列專案 **一維** 作為掃描的TIFF或PDF檔案提供的符號：

* Codabar
* Code128
* 代碼3/9
* EAN13
* EAN8

您可以使用條碼Forms服務完成下列工作：

* 從條碼影像擷取條碼資料(TIFF或PDF)。 資料會儲存為分隔文字。
* 將分隔文字資料轉換為XML （XDP或XFDF）。 XML資料比分隔文字更容易剖析。 此外，XDP或XFDF格式的資料也可以用作AEM Forms中其他服務的輸入。

條碼Forms服務會針對影像中的每個條碼，找出並解碼該條碼，然後擷取資料。 此服務會傳回XML檔案內容元素中的條碼資料（必要時使用實體編碼）。 例如，表單的下列掃描TIFF影像包含兩個條碼：

![範例](assets/example.png)

條碼式Forms服務會在解碼條碼後傳回下列XML檔案：

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## 服務的考量事項 {#considerations}

### 使用條碼式表單的工作流程 {#workflows-that-use-barcoded-forms}

表單作者可使用Designer建立互動式條碼式表單。 (請參閱 [Designer說明](https://www.adobe.com/go/learn_aemforms_designer_63_cn).) 當使用者使用Adobe Reader或Acrobat填寫條碼表單時，條碼會自動更新以編碼表單資料。

條碼式Forms服務適用於將紙張上的資料轉換為電子格式。 例如，填寫並列印條碼表單時，可以掃描列印的復本並用作條碼Forms服務的輸入。

觀察資料夾端點通常用於啟動使用條碼Forms服務的應用程式。 例如，檔案掃描器可以將條碼表單的TIFF或PDF影像儲存在觀察資料夾中。 觀察資料夾端點會將影像傳遞至服務以進行解碼。

### 建議的編碼和解碼格式 {#recommended-encoding-and-decoding-formats}

條碼格式的作者在編碼條碼中的資料時，建議使用簡易的分隔格式（例如以Tab分隔）。 此外，請避免使用歸位作為欄位分隔符號。 Designer提供一系列分隔編碼，可自動產生JavaScript指令碼來編碼條碼。 解碼的資料在第一行上有欄位名稱，在第二行上有其值，每個欄位之間有索引標籤。

解碼條碼時，請指定用來分隔欄位的字元。 為解碼指定的字元必須與用來編碼條碼的字元相同。 例如，在使用建議的Tab字元分隔格式時，「擷取至XML」作業必須使用欄位分隔字元的Tab字元預設值。

### 使用者指定的字元集 {#user-specified-character-sets}

表單作者使用Designer將條碼物件新增至表單時，可以指定字元編碼。 已識別的編碼為UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 依預設，所有資料都會以條碼編碼為UTF-8。

在解碼條碼時，您可以指定要使用的字元集編碼。 為確保所有資料都正確解碼，請指定與設計表單時表單作者指定的字元集相同的字元集。

### API限制 {#api-limitations}

使用BCF API時，請考量下列限制：

* 不支援動態表單。
* 除非將互動式表單平面化，否則無法正確解碼。
* 1D條碼僅可包含英數字元值（若支援）。 包含特殊符號的1-D條碼不會解碼。

### 其他限制 {#other-limitations}

此外，使用條碼Forms服務時，請考量下列限制：

* 此服務完全支援AcroForms和靜態表單，其中包含使用Adobe Reader或Acrobat儲存的2D條碼。 不過，若是1D條碼，請平面化表單或提供掃描的PDF或TIFF檔案。
* 尚未完全支援動態XFA表單。 若要正確解碼動態表單中的1D和2D條碼，請平面化表單或將其提供為掃描的PDF或TIFF檔案。

此外，如果符合上述限制，服務可解碼任何使用支援符號的條碼。 如需如何建立互動式條碼表單的詳細資訊，請參閱 [Designer說明](https://www.adobe.com/go/learn_aemforms_designer_63_cn).

## 設定服務的屬性   {#configureproperties}

您可以使用 **AEMFD條碼式Forms服務** 在AEM Console中設定此服務的屬性。 AEM主控台的預設URL為 `https://[host]:'port'/system/console/configMgr`.

## 使用服務 {#using}

條碼式Forms服務提供下列兩個API：

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：解碼輸入PDF檔案或tiff影像中可用的所有條碼。 它會傳回另一個XML檔案，其中包含從輸入檔案或影像中可用的所有條碼擷取的資料。

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：將使用解碼API解碼的資料轉換為XML資料。 此XML資料可與XFA表單合併。 它會傳回XML檔案清單，每個條碼各一個。

### 搭配JSP或Servlet使用BCF服務 {#using-bcf-service-with-a-jsp-or-servlets}

下列範常式式碼會解碼檔案中的條碼，並將輸出XML儲存至磁碟。

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // Please see Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // Please see javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### 搭配AEM Workflow使用BCF服務 {#using-the-bcf-service-with-aem-workflows}

從工作流程執行條碼式Forms服務類似於從JSP/Servlet執行服務。 唯一的差異是從JSP/Servlet執行服務，檔案物件會自動從ResourceResolverHelper物件擷取ResourceResolver物件的執行個體。 從工作流程呼叫程式碼時，此自動機制無法運作。

對於工作流程，請明確將ResourceResolver物件的例項傳遞給Document類別建構函式。 然後，Document物件會使用提供的ResourceResolver物件來讀取存放庫中的內容。

下列範例工作流程程式會解碼檔案中的條碼，並將結果儲存至磁碟。 程式碼會以ECMAScript撰寫，而檔案會以工作流程裝載的方式傳遞：

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```
