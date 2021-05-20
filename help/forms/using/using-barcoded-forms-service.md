---
title: 条形码Forms服务
seo-title: 使用AEM Forms Barcoded Forms服务
description: '使用AEM Forms Barcoded Forms服务从条形码的电子图像中提取数据。 '
seo-description: '使用AEM Forms Barcoded Forms服务从条形码的电子图像中提取数据。 '
uuid: b044a788-0e4a-4718-b71a-bd846933d51b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: d431c4cb-e4be-41a5-8085-42393d4d468c
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# 条形码Forms服务{#barcoded-forms-service}

## 概述 {#overview}

条形码Forms服务从条形码的电子图像中提取数据。 该服务接受包含一个或多个条形码的TIFF和PDF文件作为输入，并提取条形码数据。 条形码数据可以采用多种方式进行格式设置，包括XML、分隔字符串或使用JavaScript创建的任何自定义格式。

条形码Forms服务支持作为扫描的TIFF或PDF文档提供的以下&#x200B;**二维(2D)**&#x200B;符号：

* PDF417
* 数据矩阵
* QR代码

该服务还支持作为扫描的TIFF或PDF文档提供的以下&#x200B;**一维**&#x200B;符号：

* 科达巴尔
* 代码128
* 代码3（共9）
* EAN13
* EAN8

您可以使用条形码Forms服务完成以下任务：

* 从条形码图像（TIFF或PDF）中提取条形码数据。 数据以分隔文本形式存储。
* 将分隔文本数据转换为XML（XDP或XFDF）。 XML数据比分隔文本更易于解析。 此外，XDP或XFDF格式的数据可用作AEM Forms中其他服务的输入。

对于图像中的每个条形码，条形码Forms服务会定位条形码、对其进行解码并提取数据。 该服务在XML文档的内容元素中返回条形码数据（在需要时使用实体编码）。 例如，以下表单的扫描TIFF图像包含两个条形码：

![示例](assets/example.png)

条形码Forms服务在解码条形码后返回以下XML文档：

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

### 使用条形码表单{#workflows-that-use-barcoded-forms}的工作流

表单作者使用Designer创建交互式条形码表单。 （请参阅[Designer Help](https://www.adobe.com/go/learn_aemforms_designer_63)。） 当用户使用Adobe Reader或Acrobat填写条形码表单时，条形码会自动更新以对表单数据进行编码。

条形码Forms服务可用于将纸质上存在的数据转换为电子格式。 例如，在填写和打印条形码表单时，可以扫描打印的副本并将其用作条形码Forms服务的输入。

监视文件夹端点通常用于启动使用条形码Forms服务的应用程序。 例如，文档扫描仪可以将条形码表单的TIFF或PDF图像保存在监视文件夹中。 监视的文件夹端点将图像传递到服务以进行解码。

### 建议的编码和解码格式{#recommended-encoding-and-decoding-formats}

在条形码中对数据进行编码时，鼓励条形码表单作者使用简单的分隔格式（如制表符分隔）。 此外，请避免使用回车符作为字段分隔符。 Designer提供了一系列分隔编码选项，这些编码会自动生成JavaScript脚本以对条形码进行编码。 解码数据在第一行上具有字段名称，在第二行上具有其值，每个字段之间具有制表符。

在解码条形码时，指定用于分隔字段的字符。 为解码指定的字符必须与用于编码条形码的字符相同。 例如，在使用建议的制表符分隔格式时，提取到XML操作必须使用Tab的默认值作为字段分隔符。

### 用户指定的字符集{#user-specified-character-sets}

当表单作者使用Designer将条形码对象添加到其表单时，他们可以指定字符编码。 已识别的编码为UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16。 默认情况下，所有数据都以UTF-8格式的条形码进行编码。

在解码条形码时，您可以指定要使用的字符集编码。 为确保所有数据都正确解码，请指定与设计表单时表单作者指定的字符集相同的字符集。

### API限制{#api-limitations}

使用BCF API时，请考虑以下限制：

* 不支持动态表单。
* 除非将交互式表单扁平化，否则无法正确解码它们。
* 1-D条形码必须只包含字母数字值（如果支持）。 不对包含特殊符号的1-D条形码进行解码。

### 其他限制{#other-limitations}

此外，在使用条形码Forms服务时，请考虑以下限制：

* 该服务完全支持AcroForms和静态表单，其中包含使用Adobe Reader或Acrobat保存的2D条形码。 但是，对于1D条形码，可拼合表单或将其作为扫描的PDF或TIFF文档提供。
* 不完全支持动态XFA表单。 要在动态表单中正确解码1D和2D条形码，请拼合表单或将其作为扫描的PDF或TIFF文档提供。

此外，如果符合上述限制，该服务可以对使用支持的符号的任何条形码进行解码。 有关如何创建交互式条形码表单的更多信息，请参阅[Designer Help](https://www.adobe.com/go/learn_aemforms_designer_63)。

## 配置服务的属性   {#configureproperties}

您可以使用AEM控制台中的&#x200B;**AEMFD条形码Forms服务**&#x200B;来配置此服务的属性。 AEM控制台的默认URL为`https://[host]:'port'/system/console/configMgr`。

## 使用服务 {#using}

条形码Forms服务提供以下两个API:

* **[decode](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:解码输入PDF文档或tiff图像中所有可用的条形码。它会返回另一个XML文档，其中包含从输入文档或图像中所有可用的条形码检索到的数据。

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**:将使用解码API解码的数据转换为XML数据。此XML数据可与XFA表单合并。 它会返回XML文档列表，每个条形码对应一个文档。

### 将BCF服务与JSP或Servlet {#using-bcf-service-with-a-jsp-or-servlets}结合使用

以下示例代码将文档中的条形码解码并将输出XML保存到磁盘。

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

### 将BCF服务与AEM工作流{#using-the-bcf-service-with-aem-workflows}结合使用

从工作流运行条形码Forms服务与从JSP/Servlet运行服务类似。 唯一的区别在于从JSP/Servlet运行服务时，文档对象会自动从ResourceResolverHelper对象中检索ResourceResolver对象的实例。 从工作流调用代码时，此自动机制不起作用。

对于工作流，将ResourceResolver对象的实例显式传递到Document类构造函数。 然后，文档对象使用提供的ResourceResolver对象从存储库中读取内容。

以下示例工作流进程将解码文档中的条形码并将结果保存到磁盘。 代码将写入ECMAScript中，并且文档将作为工作流有效负载传递：

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
