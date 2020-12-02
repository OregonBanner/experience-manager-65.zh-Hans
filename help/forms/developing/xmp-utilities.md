---
title: 使用XMP实用程序
seo-title: 使用XMP实用程序
description: 'null'
seo-description: 'null'
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---


# 使用XMP实用程序{#working-with-xmp-utilities}

**关于XMP Utilities服务**

PDF文档包含元数据，该元数据是关于文档与文档内容区分的信息，如文本和图形。 Adobe可扩展元数据平台(XMP)是处理文档元数据的标准。

XMP实用程序服务可以从PDF文档检索和保存XMP元数据，并将XMP元数据导入PDF文档。

您可以使用XMP实用程序服务完成以下任务:

* 将元数据导入PDF文档。 (请参阅[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)。)
* 从PDF文档导出元数据。 (请参阅[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)。)

>[!NOTE]
>
>有关XMP Utilities服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将元数据导入PDF文档{#importing-metadata-into-pdf-documents}

您可以使用XMP实用程序Java和Web服务API以编程方式将XMP元数据导入PDF文档。 元数据提供有关PDF文档的信息，如文档的作者和与文档相关的关键字。 元数据可以位于文档的文档属性对话框中，如下图所示。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

要以编程方式将元数据导入PDF文档，您可以使用指定元数据值的现有XML文档，也可以使用类型为`XMPUtilityMetadata`的对象。 (请参阅[AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

>[!NOTE]
>
>本节讨论如何使用XML文档将元数据导入PDF文档。

以下XML代码包含与上图对应的元数据值。 例如，请注意粗体项，它指定关键字。

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
>有关XMP Utilities服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要将XMP元数据导入PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建XMPUtilityService客户端。
1. 调用XMP元数据导入操作。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建XMPUtilityService客户端**

在以编程方式执行XMP实用程序操作之前，必须创建XMPUtilityService客户端。 使用Java API，可通过创建`XMPUtilityServiceClient`对象来完成此操作。 借助Web服务API，这可通过使用`XMPUtilityServiceService`对象来完成。

**调用XMP元数据导入操作**

创建服务客户端后，可以调用XMP元数据导入操作之一，将XMP元数据导入到指定的PDF文档。

**另请参阅**

[使用Java API导入XMP元数据](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服务API导入XMP元数据](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#import-xmp-metadata-using-the-java-api}导入XMP元数据

使用XMP实用程序API(Java)导入XMP元数据：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar文件包含允许您以编程方式调用XMP Utilities服务的类。

1. 创建XMPUtilityService客户端

   使用`XMPUtilityServiceClient`对象的构造函数创建一个`ServiceClientFactory`对象，并传递一个包含连接属性的&lt;a1/>对象。

1. 调用XMP元数据导入操作

   要修改XMP元数据，请调用`XMPUtilityServiceClient`对象的`importMetadata`方法或其`importXMP`方法。

   如果使用`importMetadata`方法，请传递以下值：

   * 表示PDF文件的`com.adobe.idp.Document`对象。
   * `XMPUtilityMetadata`对象，其中包含要导入的元数据。

   如果使用`importXMP`方法，请传递以下值：

   * 表示PDF文件的`com.adobe.idp.Document`对象。
   * 一个`com.adobe.idp.Document`对象，它表示一个XML文件，其中包含要导入的元数据。

   无论哪种情况，返回的值都是`com.adobe.idp.Document`对象，它用新导入的元数据表示PDF文件。 然后，可以将此对象保存到磁盘。

**另请参阅**

[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#importing-xmp-metadata-using-the-web-service-api}导入XMP元数据

要使用XMP实用程序Web服务API以编程方式导入XMP元数据，请执行以下任务:

1. 包括项目文件

   * 创建一个Microsoft .NET客户端程序集，它使用XMP实用程序服务WSDL文件。 (请参阅[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。)
   * 引用Microsoft .NET客户端程序集。 （请参阅[创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。）

1. 创建XMPUtilityService客户端

   使用代理类构造函数创建`XMPUtilityServiceService`对象。

1. 调用XMP元数据导入操作

   要修改XMP元数据，请调用`XMPUtilityServiceService`对象的`importMetadata`方法或其`importXMP`方法。

   如果使用`importMetadata`方法，请传递以下值：

   * 表示PDF文件的`BLOB`对象。
   * `XMPUtilityMetadata`对象，其中包含要导入的元数据。

   如果使用`importXMP`方法，请传递以下值：

   * 表示PDF文件的`BLOB`对象。
   * 一个`BLOB`对象，它表示一个XML文件，其中包含要导入的元数据。

   无论哪种情况，返回的值都是`BLOB`对象，它用新导入的元数据表示PDF文件。 然后，可以将此对象保存到磁盘。

**另请参阅**

[将元数据导入PDF文档](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 从PDF文档{#exporting-metadata-from-pdf-documents}导出元数据

您可以使用XMP实用程序Java和Web服务API以编程方式从PDF文档检索和保存XMP元数据。

>[!NOTE]
>
>有关XMP Utilities服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要从PDF文档导出XMP元数据，请执行以下步骤：

1. 包括项目文件。
1. 创建XMPUtilityService客户端。
1. 调用XMP元数据导出操作。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建XMPUtilityService客户端**

在以编程方式执行XMP实用程序操作之前，必须创建XMPUtilityService客户端。 对于Java AP，如果这是通过创建`XMPUtilityServiceClient`对象来完成的。 借助Web服务API，这是使用`XMPUtilityServiceService`对象实现的。

**调用XMP元数据导出操作**

创建服务客户端后，可以调用XMP元数据导出操作之一，该操作可用于检查XMP元数据或将其保存到磁盘。

**另请参阅**

[使用Java API导入XMP元数据](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[使用Web服务API导入XMP元数据](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#export-xmp-metadata-using-the-java-api}导出XMP元数据

通过使用XMP实用程序API(Java)导出XMP元数据：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

   >[!NOTE]
   >
   >adobe-pdfutile-client.jar文件包含允许您以编程方式调用XMP Utility服务的类。

1. 创建XMPUtilityService客户端

   使用`XMPUtilityServiceClient`对象的构造函数创建一个`ServiceClientFactory`对象，并传递一个包含连接属性的&lt;a1/>对象。

1. 调用XMP元数据导入操作

   要检查XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportMetadata`方法，并传入表示PDF文件的`com.adobe.idp.Document`对象。 该方法返回一个`XMPUtilityMetadata`对象，该对象包含检索到的元数据。

   要检索和保存XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportXMP`方法并传入表示PDF文件的`com.adobe.idp.Document`对象。 该方法返回一个`com.adobe.idp.Document`对象，该对象包含检索到的元数据，您随后可以将该元数据另存为XML文件保存到磁盘。

**另请参阅**

[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#export-xmp-metadata-using-the-web-service-api}导出XMP元数据

使用XMP实用程序API（Web服务）导出XMP元数据：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端程序集，它使用XMP实用程序服务WSDL文件。
   * 引用Microsoft .NET客户端程序集。

1. 创建XMPUtilityService客户端

   使用代理类构造函数创建`XMPUtilityServiceService`对象。

1. 调用XMP元数据导入操作

   要检查XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportMetadata`方法，并传入表示PDF文件的`BLOB`对象。 该方法返回一个`XMPUtilityMetadata`对象，该对象包含检索到的元数据。

   要检索和保存XMP元数据，请调用`XMPUtilityServiceClient`对象的`exportXMP`方法并传入表示PDF文件的`BLOB`对象。 该方法返回一个`BLOB`对象，该对象包含检索到的元数据，您随后可以将该元数据另存为XML文件保存到磁盘。

**另请参阅**

[从PDF文档导出元数据](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
