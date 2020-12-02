---
title: 转换PDF服务
seo-title: 转换PDF服务
description: 使用AEM FormsConvertPDF服务将PDF文档转换为PostScript或图像文件。
seo-description: 使用AEM FormsConvertPDF服务将PDF文档转换为PostScript或图像文件。
uuid: 7fa94c8c-485b-4a77-bcd3-ed716e3cf316
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 5ec4f0ec-a9fd-4571-9b9a-278f4622c028
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# ConvertPDF Service {#convertpdf-service}

## 概述 {#overview}

“转换PDF”服务将PDF文档转换为PostScript或图像文件（JPEG、JPEG 2000、PNG和TIFF）。 将PDF文档转换为PostScript对于在任何PostScript打印机上基于服务器的无人值守打印都很有用。 在不支持PDF文档的内容管理系统中存档文档时，将PDF文档转换为多页TIFF文件非常实用。

通过“转换PDF”服务，您可以完成以下操作：

* 将PDF文档转换为PostScript。 转换为PostScript时，可以使用转换操作指定源文档以及是转换为PostScript级别2还是3。 转换为PostScript文件的PDF文档必须是非交互式的。
* 将PDF文档转换为JPEG、JPEG 2000、PNG和TIFF图像格式。 转换为任何这些图像格式时，您可以使用转换操作指定源文档和图像选项规范。 该规范包含各种首选项，如图像转换格式、图像分辨率和颜色转换。

## 配置服务的属性   {#properties}

可以使用AEM控制台中的&#x200B;**AEMFD ConvertPDF服务**&#x200B;配置此服务的属性。 AEM控制台的默认URL为`https://[host]:'port'/system/console/configMgr`。

## 使用服务{#using-the-service}

ConvertPDF服务提供以下两个API:

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**:将PDF文档转换为PostScript文件。

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**:将PDF文档转换为图像文件。支持的图像格式为JPEG、JPEG2000、PNG和TIFF。

### 对JSP或Servlet {#using-tops-api-with-a-jsp-or-servlets}使用toPS API

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
 // please replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript langauge
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### 对JSP或Servlet {#using-toimage-api-with-a-jsp-or-servlets}使用toImage API

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
 // please replace this with path to your document
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

### 将ConvertPDF服务与AEM工作流{#using-convertpdf-service-with-aem-workflows}一起使用

从工作流运行ConvertPDF服务与从JSP/Servlet运行类似。

唯一的区别在于从JSP/Servlet运行服务，文档对象从ResourceResolverHelper对象自动检索ResourceResolver对象的实例。 这个自动机构
从工作流调用代码时不工作。 对于工作流，将ResourceResolver对象的实例显式传递给文档类构造函数。 然后，文档对象使用
提供了用于从存储库读取内容的ResourceResolver对象。

以下工作流程示例将输入文档转换为PostScript文档。 代码以ECMAScript编写，文档作为工作流有效负荷传递：

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

