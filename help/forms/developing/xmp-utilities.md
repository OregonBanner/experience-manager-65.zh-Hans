---
title: 使用XMP实用程序
seo-title: 使用XMP实用程序
description: 使用XMP实用程序Java和Web服务API以编程方式将XMP元数据导入PDF文档，并从PDF文档中检索和保存XMP元数据。
seo-description: 使用XMP实用程序Java和Web服务API以编程方式将XMP元数据导入PDF文档，并从PDF文档中检索和保存XMP元数据。
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1437'
ht-degree: 0%

---

# 使用XMP实用程序{#working-with-xmp-utilities}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于XMP Utilities服务**

PDF文档包含元数据，元数据是与文档内容区分的有关文档的信息，如文本和图形。 Adobe可扩展元数据平台(XMP)是处理文档元数据的标准。

XMP实用程序服务可以从PDF文档中检索和保存XMP元数据，以及将XMP元数据导入PDF文档。

您可以使用XMP Utilities服务完成以下任务：

* 将元数据导入PDF文档。 （请参阅[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)。）
* 从PDF文档导出元数据。 （请参阅[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)。）

>[!NOTE]
>
>有关XMP Utilities服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将元数据导入PDF文档{#importing-metadata-into-pdf-documents}

您可以使用XMP实用程序Java和Web服务API以编程方式将XMP元数据导入PDF文档。 元数据提供有关PDF文档的信息，如文档的作者和与文档相关的关键字。 元数据可以在文档的“文档属性”对话框中找到，如下图所示。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

要以编程方式将元数据导入PDF文档，您可以使用指定元数据值的现有XML文档，也可以使用类型为`XMPUtilityMetadata`的对象。 (请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

>[!NOTE]
>
>本节讨论如何使用XML文档将元数据导入PDF文档。

以下XML代码包含与上图对应的元数据值。 例如，请注意指定关键词的粗体项目。

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>有关XMP Utilities服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要将XMP元数据导入PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建XMPUtilityService客户端。
1. 调用XMP元数据导入操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建XMPUtilityService客户端**

在以编程方式执行XMP实用程序操作之前，必须创建XMPUtilityService客户端。 使用Java API，可通过创建`XMPUtilityServiceClient`对象来实现此目的。 使用Web服务API，可使用`XMPUtilityServiceService`对象来实现此目的。

**调用XMP元数据导入操作**

创建服务客户端后，可以调用其中一个XMP元数据导入操作，以将XMP元数据导入指定的PDF文档。

**另请参阅**

[使用Java API导入XMP元数据](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服务API导入XMP元数据](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#import-xmp-metadata-using-the-java-api}导入XMP元数据

使用XMP实用程序API(Java)导入XMP元数据：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar文件包含允许您以编程方式调用XMP实用程序服务的类。

1. 创建XMPUtilityService客户端

   使用其构造函数创建`XMPUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用XMP元数据导入操作

   要修改XMP元数据，请调用`XMPUtilityServiceClient`对象的`importMetadata`方法或其`importXMP`方法。

   如果使用`importMetadata`方法，请传递以下值：

   * 表示PDF文件的`com.adobe.idp.Document`对象。
   * `XMPUtilityMetadata`对象，其中包含要导入的元数据。

   如果使用`importXMP`方法，请传递以下值：

   * 表示PDF文件的`com.adobe.idp.Document`对象。
   * `com.adobe.idp.Document`对象，表示包含要导入的元数据的XML文件。

   无论哪种情况，返回的值都是一个`com.adobe.idp.Document`对象，用于表示包含新导入元数据的PDF文件。 然后，可将此对象保存到磁盘。

**另请参阅**

[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#importing-xmp-metadata-using-the-web-service-api}导入XMP元数据

要使用XMP实用程序Web服务API以编程方式导入XMP元数据，请执行以下任务：

1. 包含项目文件

   * 创建使用XMP实用程序服务WSDL文件的Microsoft .NET客户端程序集。 (请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)的.NET客户端程序集。）

1. 创建XMPUtilityService客户端

   使用代理类构造函数创建`XMPUtilityServiceService`对象。

1. 调用XMP元数据导入操作

   要修改XMP元数据，请调用`XMPUtilityServiceService`对象的`importMetadata`方法或其`importXMP`方法。

   如果使用`importMetadata`方法，请传递以下值：

   * 表示PDF文件的`BLOB`对象。
   * `XMPUtilityMetadata`对象，其中包含要导入的元数据。

   如果使用`importXMP`方法，请传递以下值：

   * 表示PDF文件的`BLOB`对象。
   * `BLOB`对象，表示包含要导入的元数据的XML文件。

   无论哪种情况，返回的值都是一个`BLOB`对象，用于表示包含新导入元数据的PDF文件。 然后，可将此对象保存到磁盘。

**另请参阅**

[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 从PDF文档导出元数据{#exporting-metadata-from-pdf-documents}

您可以使用XMP实用程序Java和Web服务API以编程方式从PDF文档中检索和保存XMP元数据。

>[!NOTE]
>
>有关XMP Utilities服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要从PDF文档导出XMP元数据，请执行以下步骤：

1. 包括项目文件。
1. 创建XMPUtilityService客户端。
1. 调用XMP元数据导出操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建XMPUtilityService客户端**

在以编程方式执行XMP实用程序操作之前，必须创建XMPUtilityService客户端。 使用Java AP，如果这是通过创建`XMPUtilityServiceClient`对象来完成的。 使用Web服务API，可使用`XMPUtilityServiceService`对象来实现此目的。

**调用XMP元数据导出操作**

创建服务客户端后，可以调用其中一个XMP元数据导出操作，该操作可用于检查XMP元数据或将其保存到磁盘。

**另请参阅**

[使用Java API导入XMP元数据](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服务API导入XMP元数据](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#export-xmp-metadata-using-the-java-api}导出XMP元数据

使用XMP实用程序API(Java)导出XMP元数据：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar文件包含允许您以编程方式调用XMP Utility服务的类。

1. 创建XMPUtilityService客户端

   使用其构造函数创建`XMPUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用XMP元数据导入操作

   要检查XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportMetadata`方法，并传入表示PDF文件的`com.adobe.idp.Document`对象。 方法会返回一个`XMPUtilityMetadata`对象，其中包含检索到的元数据。

   要检索并保存XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportXMP`方法，并传入表示PDF文件的`com.adobe.idp.Document`对象。 方法会返回一个`com.adobe.idp.Document`对象，其中包含检索到的元数据，您随后可以将其另存为XML文件，保存到磁盘。

**另请参阅**

[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#export-xmp-metadata-using-the-web-service-api}导出XMP元数据

使用XMP实用程序API（Web服务）导出XMP元数据：

1. 包含项目文件

   * 创建使用XMP实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建XMPUtilityService客户端

   使用代理类构造函数创建`XMPUtilityServiceService`对象。

1. 调用XMP元数据导入操作

   要检查XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportMetadata`方法，并传入表示PDF文件的`BLOB`对象。 方法会返回一个`XMPUtilityMetadata`对象，其中包含检索到的元数据。

   要检索并保存XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportXMP`方法，并传入表示PDF文件的`BLOB`对象。 方法会返回一个`BLOB`对象，其中包含检索到的元数据，您随后可以将其另存为XML文件，保存到磁盘。

**另请参阅**

[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
