---
title: 巴科德Forms
seo-title: 使用AEM FormsBarcodedForms服务
description: '使用AEM FormsBarcodedForms服务从条形码的电子图像中提取数据。 '
seo-description: '使用AEM FormsBarcodedForms服务从条形码的电子图像中提取数据。 '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---


# 巴科德Forms{#barcoded-forms-service}

## 概述 {#overview}

BarcodedForms服务从条形码的电子图像中提取数据。 该服务接受包含一个或多个条码的TIFF和PDF文件作为输入并提取条形码数据。 条形码数据可以采用各种方式格式化，包括XML、分隔字符串或使用JavaScript创建的任何自定义格式。

BarcodedForms服务支持以 **下二维(2D)符号** ，它们作为扫描的TIFF或PDF文档提供：

* PDF417
* 数据矩阵
* QR码

该服务还支持作为扫 **描的TIFF或PDF文档** 提供的以下一维符号：

* 科达巴尔
* Code128
* 代码3（共9个）
* EAN13
* EAN8

您可以使用BarcodedForms服务完成以下任务:

* 从条形码图像（TIFF或PDF）提取条形码数据。 数据以分隔文本的形式存储。
* 将分隔文本数据转换为XML（XDP或XFDF）。 XML数据比分隔文本更易于分析。 此外，XDP或XFDF格式的数据可用作AEM Forms中其他服务的输入。

对于图像中的每个条形码，BarcodedForms服务将定位条形码、解码并提取数据。 服务在XML文档的内容元素中返回条形码数据（在需要时使用实体编码）。 例如，表单的以下扫描TIFF图像包含两个条码：

![示例](assets/example.png)

BarcodedForms服务在解码条形码后返回以下XML文档:

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

## 服务注意事项 {#considerations}

### 使用条形码表单的工作流 {#workflows-that-use-barcoded-forms}

表单作者使用设计器创建交互式条码表单。 (请参阅 [设计人员帮](https://www.adobe.com/go/learn_aemforms_designer_63)助。) 当用户使用Adobe Reader或Acrobat填充条码表单时，条形码会自动更新以对表单数据进行编码。

BarcodedForms服务可用于将纸质上的数据转换为电子格式。 例如，当填写和打印条形码表单时，可以扫描打印的副本并将其用作BarcodedForms服务的输入。

监视的文件夹端点通常用于开始使用Barcoded Forms服务的应用程序。 例如，文档扫描仪可将条形码表单的TIFF或PDF图像保存到监视的文件夹中。 监视的文件夹端点将图像传递给服务进行解码。

### 推荐的编码和解码格式 {#recommended-encoding-and-decoding-formats}

在条形码中对数据进行编码时，鼓励作者使用简单的分隔格式（如制表符分隔格式）。 另外，请避免使用回车作为字段分隔符。 设计人员提供一系列分隔的编码，这些编码自动生成JavaScript脚本以对条码进行编码。 解码数据具有第一行上的字段名称和第二行上的字段值，并且每个字段之间有制表符。

在解码条码时，指定用于分隔字段的字符。 为解码指定的字符必须与用于编码条形码的字符相同。 例如，在使用建议的制表符分隔格式时，“提取到XML”操作必须使用“制表符”的默认值作为字段分隔符。

### 用户指定的字符集 {#user-specified-character-sets}

当表单作者使用设计器将条形码对象添加到其表单时，他们可以指定字符编码。 公认的编码为UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 默认情况下，所有数据都以UTF-8的条形码进行编码。

在解码条形码时，可以指定要使用的字符集编码。 要确保正确解码所有数据，请指定表单作者在设计表单时指定的相同字符集。

### API限制 {#api-limitations}

使用BCF API时，请考虑以下限制：

* 不支持动态表单。
* 除非拼合交互式表单，否则无法正确解码它们。
* 1-D条形码只能包含字母数字值（如果支持）。 包含特殊符号的1-D条码不解码。

### 其他限制 {#other-limitations}

此外，在使用BarcodedForms服务时，请考虑以下限制：

* 该服务完全支持AcroForms和包含2D条形码的静态表单，这些条形码是使用Adobe Reader或Acrobat保存的。 但是，对于1D条形码，可拼合表单或以扫描的PDF或TIFF文档提供表单。
* 不完全支持动态XFA表单。 要对动态表单中的1D和2D条码进行正确解码，请拼合表单或将其作为扫描的PDF或TIFF文档提供。

此外，如果遵守上述限制，该服务可以解码使用受支持的符号的任何条形码。 有关如何创建交互式条码表单的更多信息，请参阅设计 [人员帮助](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 配置服务的属性   {#configureproperties}

您可以使用AEM **控制台中的AEMFD Barcoded** Forms服务，为此服务配置属性。 AEM控制台的默认URL为 `https://[host]:'port'/system/console/configMgr`。

## 使用服务 {#using}

BarcodedForms服务提供以下两个API:

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: 解码输入PDF文档或tiff图像中可用的所有条码。 它返回另一个XML文档，该文档包含从输入或图像中所有可用的条形码检索到的数据。

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: 将使用解码API解码的数据转换为XML数据。 此XML数据可以与XFA表单合并。 它返回一列表XML文档，每个条形码对应一个。

### 将BCF服务与JSP或Servlet一起使用 {#using-bcf-service-with-a-jsp-or-servlets}

以下范例代码解码文档中的条形码并将输出XML保存到磁盘。

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

### 将BCF服务与AEM工作流一起使用 {#using-the-bcf-service-with-aem-workflows}

从工作流运行BarcodedForms服务与从JSP/Servlet运行服务类似。 唯一的区别在于从JSP/Servlet运行服务，文档对象从ResourceResolverHelper对象自动检索ResourceResolver对象的实例。 从工作流调用代码时，此自动机制不工作。

对于工作流，将ResourceResolver对象的实例显式传递给文档类构造函数。 然后，文档对象使用提供的ResourceResolver对象从存储库读取内容。

以下范例工作流程解码文档中的条形码并将结果保存到磁盘。 代码以ECMAScript编写，文档作为工作流有效负荷传递：

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

