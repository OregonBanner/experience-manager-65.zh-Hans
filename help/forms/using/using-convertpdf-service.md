---
title: ConvertPDF服务
description: 使用Adobe Experience Manager Forms ConvertPDF服务将PDF文档转换为PostScript或图像文件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
exl-id: 575bab27-d973-47fa-a0da-fa889cec6f27
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# ConvertPDF服务 {#convertpdf-service}

## 概述 {#overview}

转换PDF服务将PDF文档转换为PostScript或图像文件(JPEG、JPEG2000、PNG和TIFF)。 将PDF文档转换为PostScript对于任何PostScript打印机上基于服务器的自动打印很有用。 在不支持PDF文档的内容管理系统中归档文档时，将PDF文档转换为多页TIFF文件是切实可行的。

您可以使用ConvertPDF服务完成以下操作：

* 将PDF文档转换为PostScript。 转换为PostScript时，可以使用转换操作指定源文档以及是否转换为PostScript级别2或级别3。 转换为PostScript文件的PDF文档必须是非交互式文档。
* 将PDF文档转换为JPEG、JPEG2000、PNG和TIFF图像格式。 当转换为任何这些图像格式时，可以使用转换操作来指定源文档和图像选项规范。 该规范包含各种首选项，如图像转换格式、图像分辨率和颜色转换。

## 配置服务的属性   {#properties}

您可以使用 **AEMFD ConvertPDF服务** 在AEM Console中配置此服务的属性。 AEM控制台的默认URL为 `https://[host]:'port'/system/console/configMgr`.

## 使用服务 {#using-the-service}

ConvertPDF服务提供以下两个API：

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**：将PDF文档转换为PostScript文件。

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**：将PDF文档转换为图像文件。 支持的图像格式为JPEG、JPEG2000、PNG和TIFF。

### 将toPS API与JSP或Servlet一起使用 {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### 将toImage API与JSP或Servlet一起使用 {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### 在AEM工作流中使用ConvertPDF服务 {#using-convertpdf-service-with-aem-workflows}

从工作流运行ConvertPDF服务与从JSP/Servlet运行类似。

唯一的区别是在从JSP/Servlet运行服务时，文档对象会自动从ResourceResolverHelper对象中检索ResourceResolver对象的实例。 从工作流调用代码时，此自动机制不起作用。 对于工作流，请将ResourceResolver对象的实例显式传递给Document类构造函数。 然后，Document对象使用提供的ResourceResolver对象从存储库中读取内容。

以下示例工作流进程将输入文档转换为PostScript文档。 该代码在ECMAScript中编写，文档作为工作流有效负载传递：

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

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

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
