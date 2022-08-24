---
title: 创建文档输出流
seo-title: Creating Document Output Streams
description: 使用输出服务将文档转换为PDF(包括PDF/A文档)、PostScript、打印机控制语言(PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL标签格式。
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# 创建文档输出流  {#creating-document-output-streams}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于输出服务**

“输出”服务允许您将文档输出为PDF(包括PDF/A文档)、PostScript、打印机控制语言(PCL)，以及以下标签格式：

* 泽布拉 — 兹普尔
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用“输出”服务，可以将XML表单数据与表单设计合并，并将文档输出到网络打印机或文件。

有两种方法可以将表单设计（XDP文件）传递到输出服务。 您可以通过 `com.adobe.idp.Document` 包含输出服务的表单设计的实例。 或者，您可以传递指定表单设计位置的URI值。 在 *使用AEM表单进行编程*.

>[!NOTE]
>
>输出服务不支持包含特定于应用程序对象的脚本的AcroformPDF文档。 包含应用程序对象特定脚本的AcroformPDF文档不会呈现。

以下各节显示如何使用URI值将表单设计传递到输出服务：

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)

以下部分显示如何在 `com.adobe.idp.Document` 实例：

* [将位于Content Services中的文档（已弃用）传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

在决定使用哪种技术时，一个注意事项是如果您要从其他AEM Forms服务获取表单设计，然后在 `com.adobe.idp.Document` 实例。 和 *将文档传递到输出服务* 和 *使用片段创建PDF文档* 部分显示如何从其他AEM Forms服务获取表单设计。 第一部分从内容服务中检索表单设计（已弃用）。 第二部分从汇编程序服务中检索表单设计。

如果您从固定位置（如文件系统）获取表单设计，则可以使用任一技术。 即，您可以为XDP文件指定URI值，或使用 `com.adobe.idp.Document` 实例。

要在创建表单文档时传递指定表单设计位置的URI值，请使用 `generatePDFOutput` 方法。 同样，要通过 `com.adobe.idp.Document` 在创建PDF文档时实例到输出服务，请使用 `generatePDFOutput2` 方法。

在向网络打印机发送输出流时，您还可以使用任一技术。 通过传递 `com.adobe.idp.Document` 包含表单设计的实例，请使用 `sendToPrinter2`方法。 要通过传递URI值将输出流发送到打印机，请使用 `sendToPrinter`方法。 的 *将打印流发送到打印机* 部分使用 `sendToPrinter` 方法。

您可以使用输出服务完成以下任务：

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)
* [将位于Content Services中的文档（已弃用）传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [打印到文件](creating-document-output-streams.md#printing-to-files)
* [将打印流发送到打印机](creating-document-output-streams.md#sending-print-streams-to-printers)
* [创建多个输出文件](creating-document-output-streams.md#creating-multiple-output-files)
* [创建搜索规则](creating-document-output-streams.md#creating-search-rules)
* [拼合PDF文档](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 创建PDF文档 {#creating-pdf-documents}

您可以使用输出服务创建基于您提供的表单设计和XML表单数据的PDF文档。 由输出服务创建的PDF文档不是交互式PDF文档；用户无法输入或修改表单数据。

如果要创建用于长期存储的PDF文档，建议创建PDF/文档。 (请参阅 [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents).)

要创建允许用户输入数据的交互式PDF表单，请使用Forms服务。 (请参阅 [呈现交互式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要创建PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF文档。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 您计划使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

请考虑以下示例贷款申请表。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要将数据合并到此表单设计中，必须创建与表单对应的XML数据源。 以下XML表示与示例抵押申请表单对应的XDP XML数据源。

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**设置PDF运行时选项**

在创建PDF文档时设置文件URI选项。 此选项指定输出服务生成的PDF文件的名称和位置。

>[!NOTE]
>
>您可以以编程方式从Output服务返回的复杂数据类型中检索PDF文档，而不是设置文件URI运行时选项。 但是，通过设置文件URI运行时选项，您无需创建以编程方式检索PDF文档的应用程序逻辑。

**设置渲染运行时选项**

创建PDF文档时，可以设置渲染运行时选项。 尽管这些选项不是必需的(与所需的PDF运行时选项不同)，但您可以执行诸如提高输出服务性能之类的任务。 例如，您可以缓存输出服务使用的表单设计，以提高其性能。

如果使用标记的Acrobat表单作为输入，则无法使用输出服务Java或Web服务API来关闭标记设置。 如果您尝试以编程方式将此选项设置为 `false`，结果PDF文档仍会被标记。

>[!NOTE]
>
>如果未指定渲染运行时选项，则使用默认值。 有关渲染运行时选项的信息，请参阅 `RenderOptionsSpec` 类引用。 (请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**生成PDF文档**

在引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用输出服务，这会导致其生成PDF文档。

在生成PDF文档时，您可以指定输出服务创建PDF文档所需的URI值。 表单设计可以存储在诸如服务器文件系统之类的位置或作为AEM Forms应用程序的一部分。 作为Forms应用程序一部分存在的表单设计（或其他资源，如图像文件），可以使用内容根URI值进行引用 `repository:///`. 例如，请考虑以下名为 *Loan.xdp* 位于名为的Forms应用程序内 *应用程序/表单应用程序*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

要访问上图所示的Loan.xdp文件，请指定 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 作为传递到 `OutputClient` 对象 `generatePDFOutput` 方法。 指定表单名称(*Loan.xdp*)作为传递到 `OutputClient` 对象 `generatePDFOutput` 方法。

如果XDP文件包含图像（或其他资源，如片段），请将这些资源放在与XDP文件相同的应用程序文件夹中。 AEM Forms使用内容根URI作为解析对图像的引用的基本路径。 例如，如果Loan.xdp文件包含图像，请确保将该图像放置在 `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>调用 `OutputClient` 对象 `generatePDFOutput` 或 `generatePrintedOutput` 方法。

>[!NOTE]
>
>要查看通过引用位于Forms应用程序中的XDP创建PDF文档的完整快速入门，请参阅 [快速启动（EJB模式）：使用Java API根据应用程序XDP文件创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**检索操作的结果**

输出服务执行操作后，它会返回各种数据项，如指定操作是否成功的状态XML数据。

**另请参阅**

[使用Java API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服务API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF文档 {#create-a-pdf-document-using-the-java-api}

使用输出API(Java)创建PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 表示XML数据源的对象，该XML数据源使用其构造函数填充PDF文档，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象。 传递 `java.io.FileInputStream` 对象。

1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setFileURI` 方法。 传递一个字符串值，以指定输出服务生成的PDF文件的位置。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 通过调用 `RenderOptionsSpec` 对象 `setCacheEnabled` 传递 `true`.

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `setPdfVersion` 方法。 输出PDF文档保留原始PDF版本。 同样，您也无法通过调用 `RenderOptionsSpec` 对象 `setTaggedPDF` 方法(如果输入文档是Acrobat表单或已签名或认证的XFA文档)。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `setLinearizedPDF` 方法，输入PDF文档经认证或数字签名。 (请参阅 [数字签名PDF文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 生成PDF文档。

   通过调用 `OutputClient` 对象 `generatePDFOutput` 方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >通过调用生成PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名或已认证的XFAPDF表单合并。 (请参阅 [数字签名和认证文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >的 `OutputResult` 对象 `getRecordLevelMetaDataList` 方法返回 `null`*.*

   >[!NOTE]
   >
   >您还可以通过调用 `OutputClient` 对象 `generatePDFOutput2` 方法。 (请参阅 [将位于Content Services中的文档（已弃用）传递到输出服务&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 检索操作的结果。

   * 检索 `com.adobe.idp.Document` 表示 `generatePDFOutput` 操作 `OutputResult` 对象 `getStatusDoc` 方法。 此方法会返回状态XML数据，以指定操作是否成功。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getStatusDoc` 方法)。

   尽管输出服务会将PDF文档写入由参数指定的位置，该位置将传递到 `PDFOutputOptionsSpec` 对象 `setFileURI` 方法中，您可以通过调用以编程方式检索PDF/A文档 `OutputResult` 对象 `getGeneratedDoc` 方法。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入门（SOAP模式）：使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建PDF文档 {#create-a-pdf-document-using-the-web-service-api}

使用输出API（Web服务）创建PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储将与PDF文档合并的XML数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含表单数据的XML文件的文件位置。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置“文件URI”选项，该字符串值指定输出服务生成到的PDF文件的位置 `PDFOutputOptionsSpec` 对象 `fileURI` 数据成员。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计，以通过分配值来提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象 `cacheEnabled` 数据成员。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `setPdfVersion` 方法。 输出PDF文档保留原始PDF版本。 同样，您也无法通过调用 `RenderOptionsSpec` 对象 `setTaggedPDF`*方法(如果输入文档是Acrobat表单或经签名或认证的XFA文档)。*

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `linearizedPDF` 成员。 (请参阅 [数字签名PDF文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 生成PDF文档。

   通过调用 `OutputServiceService` 对象 `generatePDFOutput`方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用描述文档的生成元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用结果数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 安 `OutputResult` 包含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   >[!NOTE]
   >
   >通过调用生成PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名或已认证的XFAPDF表单合并。 (请参阅 [数字签名和认证文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >您还可以通过调用 `OutputClient` 对象 `generatePDFOutput2` 方法。 (请参阅 [将位于Content Services中的文档（已弃用）传递到输出服务&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建用于存储 `BLOB` 由 `OutputServiceService` 对象 `generatePDFOutput` 方法（第八个参数）。 通过获取 `BLOB` 对象 `MTOM` `field`.
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

   另请参阅

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >的 `OutputServiceService` 对象 `generateOutput` 方法已弃用。

## 创建PDF/A文档 {#creating-pdf-a-documents}

您可以使用输出服务创建PDF/文档。 由于PDF/A是用于长期保留文档内容的存档格式，因此所有字体都会被嵌入并且文件未压缩。 因此，PDF/A文档通常比标准PDF文档大。 此外，PDF/文档不包含音频和视频内容。 与其他输出服务任务一样，您提供要与表单设计合并的表单设计和数据，以创建PDF/文档。

PDF/A-1规范包含两个符合级别，即a和b。二者的主要区别在于逻辑结构（无障碍）支持，而符合性级别b不需要此支持。无论符合性级别如何，PDF/A-1都指示所有字体都嵌入在生成的PDF/A文档中。

尽管PDF/A是归档PDF文档的标准，但是，如果标准PDF文档满足您公司的需求，则不必强制使用PDF/A进行归档。 PDF/A标准的目的是建立一个PDF文件，该文件可以长时间存储，并满足文档保存要求。 例如，URL无法嵌入到PDF/A中，因为URL会随着时间的推移而变为无效。

贵组织必须评估其自身需求、您打算保留文档的时长、文件大小考虑因素，并确定您自己的归档策略。 您可以使用DocConverter服务以编程方式确定PDF文档是否符合PDF/A。 (请参阅 [以编程方式确定PDF/符合性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

PDF/文档必须使用在表单设计中指定的字体，并且字体无法替换。 因此，如果位于PDF文档内的字体在主机操作系统(OS)上不可用，则会发生异常。

在Acrobat中打开PDF/文档时，会显示一条消息，确认该文档是PDF/A文档，如下图所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM网站有一个PDF/常见问题解答部分，您可以在 [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_65).

### 步骤摘要 {#summary_of_steps-1}

要创建PDF/文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置PDF/运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF/文档。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建自定义应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置PDF/运行时选项**

创建PDF/文档时，可以设置“文件URI”选项。 URI相对于托管AEM Forms的J2EE应用程序服务器。 也就是说，如果设置C:\Adobe ，则文件将写入服务器上的文件夹，而不是客户端计算机。 URI指定输出服务生成的PDF/A文件的名称和位置。

**设置渲染运行时选项**

创建PDF/A文档时，可以设置渲染运行时选项。 两个PDF/A相关选项可设置为 `PDFAConformance` 和 `PDFARevisionNumber` 值。 的 `PDFAConformance` 值是指PDF文档如何遵守指定如何保留长期电子文档的要求。 此选项的有效值为 `A` 和 `B`. 有关a级和b级符合性的信息，请参阅标题为PDF/A-1 ISO规范 *ISO 19005-1文档管理*.

的 `PDFARevisionNumber` 值是指PDF/A文档的修订版号。 有关PDF/A文档的修订号的信息，请参阅PDF/A-1 ISO规范的标题 *ISO 19005-1文档管理*.

>[!NOTE]
>
>无法将标记的Adobe PDF选项设置为 `false` 创建PDF/A 1A文档时。 PDF/A 1A将始终是标记的PDF文档。 此外，您无法将标记的Adobe PDF选项设置为 `true` 创建PDF/A 1B文档时。 PDF/A 1B将始终为未标记的PDF文档。

**生成PDF/文档**

在引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用输出服务，使其生成PDF/文档。

**检索操作的结果**

输出服务执行操作后，它会返回各种数据项，如指定操作是否成功的XML数据。

**另请参阅**

[使用Java API创建PDF/文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服务API创建PDF/文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF/文档 {#create-a-pdf-a-document-using-the-java-api}

使用输出API(Java)创建PDF/文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 表示XML数据源的对象，该XML数据源使用其构造函数填充PDF/A文档，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置PDF/运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setFileURI` 方法。 传递一个字符串值，以指定输出服务生成的PDF文件的位置。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 设置 `PDFAConformance` 值 `RenderOptionsSpec` 对象 `setPDFAConformance` 方法和通过 `PDFAConformance` 指定符合性级别的枚举值。 例如，要指定符合性级别A，请传递 `PDFAConformance.A`.
   * 设置 `PDFARevisionNumber` 值 `RenderOptionsSpec` 对象 `setPDFARevisionNumber` 方法和传递 `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >PDF/文档的PDF版本为1.4，无论您为 `RenderOptionsSpec` 对象 `setPdfVersion`*方法。*

1. 生成PDF/文档。

   通过调用 `OutputClient` 对象 `generatePDFOutput` 方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF/文档，请指定 `TransformationFormat.PDFA`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >的 `OutputResult` 对象 `getRecordLevelMetaDataList` 方法返回 `null`.

   >[!NOTE]
   >
   >您还可以通过调用 `OutputClient` 对象 `generatePDFOutput`2方法。 (请参阅 [将位于Content Services中的文档（已弃用）传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示 `generatePDFOutput` 方法 `OutputResult` 对象 `getStatusDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getStatusDoc` 方法)。

   >[!NOTE]
   >
   >尽管输出服务会将PDF/A文档写入到由参数指定的位置，该位置将传递到 `PDFOutputOptionsSpec` 对象 `setFileURI` 方法中，您可以通过调用以编程方式检索PDF/A文档 `OutputResult` 对象 `getGeneratedDoc` 方法。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API创建PDF/文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服务API创建PDF/文档 {#create-a-pdf-a-document-using-the-web-service-api}

使用输出API（Web服务）创建PDF/文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储将与PDF/A文档合并的数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字节数组内容的字段。

1. 设置PDF/运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置“文件URI”选项，该字符串值指定输出服务生成到的PDF文件的位置 `PDFOutputOptionsSpec` 对象 `fileURI` 数据成员。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 设置 `PDFAConformance` 值 `PDFAConformance` 枚举值 `RenderOptionsSpec` 对象 `PDFAConformance` 数据成员。 例如，要指定符合性级别A，请指定 `PDFAConformance.A` 到此数据成员。
   * 设置 `PDFARevisionNumber` 值 `PDFARevisionNumber` 枚举值 `RenderOptionsSpec` 对象 `PDFARevisionNumber` 数据成员。 分配 `PDFARevisionNumber.Revision_1` 到此数据成员。

   >[!NOTE]
   >
   >PDF/文档的PDF版本为1.4，无论您指定哪个值。

1. 生成PDF/文档。

   通过调用 `OutputServiceService` 对象 `generatePDFOutput`方法和传递以下值：

   * TransformationFormat枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDFA`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用描述文档的生成元数据填充此对象。 （仅Web服务调用需要此参数值。）
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用结果数据填充此对象。 （仅Web服务调用需要此参数值。）
   * 安 `OutputResult` 包含操作结果的对象。 （仅Web服务调用需要此参数值。）

   >[!NOTE]
   >
   >您还可以通过调用 `OutputClient` 对象 `generatePDFOutput`2方法。 (请参阅 [将位于Content Services中的文档（已弃用）传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建用于存储 `BLOB` 由 `OutputServiceService` 对象 `generatePDFOutput` 方法（第八个参数）。 通过获取 `BLOB` 对象 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将位于Content Services中的文档（已弃用）传递到输出服务 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

输出服务会呈现一个非交互式PDF表单，该表单基于表单设计，通常另存为XDP文件，并在Designer中创建。 您可以通过 `com.adobe.idp.Document` 包含表单设计到输出服务的对象。 然后，输出服务会呈现位于 `com.adobe.idp.Document` 对象。

传递 `com.adobe.idp.Document` 输出服务的对象是其他AEM Forms服务操作返回 `com.adobe.idp.Document` 实例。 也就是说，你可以 `com.adobe.idp.Document` 实例，并渲染。 例如，假定XDP文件存储在名为的Content Services（已弃用）节点中 `/Company Home/Form Designs`，如下图所示。

您可以以编程方式从Content Services中检索Loan.xdp（已弃用），并将XDP文件传递到 `com.adobe.idp.Document` 对象。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-2}

要将从Content Services（已弃用）获取的文档传递到输出服务，请执行以下任务：

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从内容服务中检索表单设计（已弃用）。
1. 呈现非交互式PDF表单。
1. 对数据流执行操作。

**包含项目文件**

将必需的文件包含到您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流从Content Services检索XDP文件（已弃用），因此请创建一个文档管理API对象。

**从内容服务中检索表单设计（已弃用）**

使用Java或Web服务API从内容服务中检索XDP文件（已弃用）。 在 `com.adobe.idp.Document` 实例(或 `BLOB` 实例（如果您使用的是web服务）。 然后，您可以通过 `com.adobe.idp.Document` 实例添加到输出服务。

**呈现非交互式PDF表单**

要渲染非交互式表单，请传递 `com.adobe.idp.Document` 从内容服务（已弃用）返回到输出服务的实例。

>[!NOTE]
>
>两种新方法名为 `generatePDFOutput2`和g `eneratePrintedOutput2`接受 `com.adobe.idp.Document` 包含表单设计的对象。 您还可以通过 `com.adobe.idp.Document`在向网络打印机发送打印流时，将表单设计添加到输出服务。

**对表单数据流执行操作**

您可以将非交互式表单另存为PDF文件。 可以在Adobe Reader或Acrobat中查看表单。

**另请参阅**

[使用Java API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用Web服务API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-java-api}

使用输出服务和内容服务（已弃用）API(Java)传递从Content Services检索的文档（已弃用）：

1. 包括项目文件。

   将客户端JAR文件（如adobe-output-client.jar和adobe-contentservices-client.jar）包含到您Java项目的类路径中。

1. 创建输出和文档管理客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。
   * 创建 `DocumentManagementServiceClientImpl` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 从内容服务中检索表单设计（已弃用）。

   调用 `DocumentManagementServiceClientImpl` 对象 `retrieveContent` 方法并传递以下值：

   * 一个字符串值，用于指定添加内容的商店。 默认存储区为 `SpacesStore`. 此值是必需参数。
   * 一个字符串值，用于指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递一个空字符串。 在这种情况下，将检索最新版本。

   的 `retrieveContent` 方法返回 `CRCResult` 包含XDP文件的对象。 检索 `com.adobe.idp.Document` 实例 `CRCResult` 对象 `getDocument` 方法。

1. 呈现非交互式PDF表单。

   调用 `OutputClient` 对象 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，用于指定图像等其他资源所在的内容根目录。
   * A `com.adobe.idp.Document` 表示表单设计的对象(使用 `CRCResult` 对象 `getDocument` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 检索 `com.adobe.idp.Document` 通过调用 `OutputResult` 对象 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getGeneratedDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入门（SOAP模式）：使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-web-service-api}

使用输出服务和内容服务（已弃用）API（Web服务）传递从Content Services检索的文档（已弃用）：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 对与输出服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   对与文档管理服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   因为 `BLOB` 数据类型对于两个服务引用都是通用的，可完全限定 `BLOB` 数据类型。 在相应的Web服务快速启动中， `BLOB` 实例完全限定。

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出和文档管理客户端API对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >对 `DocumentManagementServiceClient`服务客户端。

1. 从内容服务中检索表单设计（已弃用）。

   通过调用 `DocumentManagementServiceClient` 对象 `retrieveContent` 方法和传递以下值：

   * 一个字符串值，用于指定添加内容的商店。 默认存储区为 `SpacesStore`. 此值是必需参数。
   * 一个字符串值，用于指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递一个空字符串。 在这种情况下，将检索最新版本。
   * 用于存储浏览链接值的字符串输出参数。
   * A `BLOB` 用于存储内容的输出参数。 您可以使用此输出参数检索内容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 用于存储内容属性的输出参数。
   * A `CRCResult` 输出参数。 您可以使用 `BLOB` 用于检索内容的输出参数。

1. 呈现非交互式PDF表单。

   调用 `OutputServiceClient` 对象 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，用于指定图像等其他资源所在的内容根目录。
   * A `BLOB` 表示表单设计的对象(使用 `BLOB` 由内容服务返回的实例（已弃用）。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 输出 `BLOB` 由填充的对象 `generatePDFOutput2` 方法。 的 `generatePDFOutput2` 方法使用描述文档的生成元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 输出 `OutputResult` 包含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   的 `generatePDFOutput2` 方法返回 `BLOB` 包含非交互式PDF表单的对象。

1. 对表单数据流执行操作。

   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，以表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `BLOB` 从检索的对象 `generatePDFOutput2` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 将存储库中的文档传递到输出服务 {#passing-documents-located-in-the-repository-to-the-output-service}

输出服务会呈现一个非交互式PDF表单，该表单基于表单设计，通常另存为XDP文件，并在Designer中创建。 您可以通过 `com.adobe.idp.Document` 包含表单设计到输出服务的对象。 然后，输出服务会呈现位于 `com.adobe.idp.Document` 对象。

传递 `com.adobe.idp.Document` 输出服务的对象是其他AEM Forms服务操作返回 `com.adobe.idp.Document` 实例。 也就是说，你可以 `com.adobe.idp.Document` 实例，并渲染。 例如，假定XDP文件存储在AEM Forms存储库中，如下图所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

的 *FormsFolder* 文件夹是AEM Forms存储库中用户定义的位置（此位置是一个示例，默认情况下不存在）。 在此示例中，名为Loan.xdp的表单设计位于此文件夹中。 除了表单设计之外，还可以在此位置存储其他表单辅助内容，如图像。 位于AEM Forms存储库中的资源的路径是：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以以编程方式从AEM Forms存储库中检索Loan.xdp，并将其传递到 `com.adobe.idp.Document` 对象。

您可以使用两种方式之一，根据位于存储库中的XDP文件创建PDF。 您可以通过引用传递XDP位置，也可以以编程方式从存储库中检索XDP，并将其传递到XDP文件中的输出服务。

[快速启动（EJB模式）：使用Java API根据应用程序XDP文件创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （显示如何通过引用传递XDP文件的位置）。

[快速启动（EJB模式）：使用Java API将位于AEM Forms存储库中的文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (显示如何以编程方式从AEM Forms存储库中检索XDP文件，并将其传递到 `com.adobe.idp.Document` 实例)。 （本节讨论如何执行此任务）

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-3}

要将从AEM Forms存储库获取的文档传递到输出服务，请执行以下任务：

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从AEM Forms存储库检索表单设计。
1. 呈现非交互式PDF表单。
1. 对数据流执行操作。

**包含项目文件**

将必需的文件包含到您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流从Content Services检索XDP文件（已弃用），因此请创建一个文档管理API对象。

**从AEM Forms存储库检索表单设计**

使用存储库API从AEM Forms存储库中检索XDP文件。 (请参阅 [读取资源](/help/forms/developing/aem-forms-repository.md#reading-resources).)

在 `com.adobe.idp.Document` 实例(或 `BLOB` 实例（如果您使用的是web服务）。 然后，您可以通过 `com.adobe.idp.Document` 输出服务实例。

**呈现非交互式PDF表单**

要渲染非交互式表单，请传递 `com.adobe.idp.Document` 使用AEM Forms存储库API返回的实例。

>[!NOTE]
>
>两种新方法名为 `generatePDFOutput2`和 `generatePrintedOutput2`接受 `com.adobe.idp.Document`包含表单设计的对象。 您还可以通过 `com.adobe.idp.Document` 在向网络打印机发送打印流时，将表单设计添加到输出服务。

**对表单数据流执行操作**

您可以将非交互式表单另存为PDF文件。 可以在Adobe Reader或Acrobat中查看表单。

**另请参阅**

[使用Java API将位于存储库中的文档传递到输出服务](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API将位于存储库中的文档传递到输出服务 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用输出服务和存储库API(Java)传递从存储库检索的文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar和adobe-repository-client.jar。

1. 创建输出和文档管理客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。
   * 创建 `DocumentManagementServiceClientImpl` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 从AEM Forms存储库中检索表单设计。

   调用 `ResourceRepositoryClient` 对象 `readResourceContent` 方法并将指定URI位置的字符串值传递到XDP文件。 例如：`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。此值是必填项。 此方法将返回 `com.adobe.idp.Document` 表示XDP文件的实例。

1. 呈现非交互式PDF表单。

   调用 `OutputClient` 对象 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，用于指定图像等其他资源所在的内容根目录。 例如：`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * A `com.adobe.idp.Document` 表示表单设计的对象(使用 `ResourceRepositoryClient` 对象 `readResourceContent` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 检索 `com.adobe.idp.Document` 通过调用 `OutputResult` 对象 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getGeneratedDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API将位于AEM Forms存储库中的文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段创建PDF文档 {#creating-pdf-documents-using-fragments}

您可以使用“输出”和“汇编程序”服务创建基于片段的输出流，如PDF文档。 汇编程序服务会根据位于多个XDP文件中的片段组合一个XDP文档。 装配的XDP文档将传递到输出服务，该服务将创建一个PDF文档。 尽管此工作流显示正在生成的PDF文档，但输出服务可以为此工作流生成其他输出类型，如ZPL。 PDF文档仅用于讨论目的。

下图显示了此工作流。

![cp_cp_outputsamsellefragments](assets/cp_cp_outputassemblefragments.png)

阅读前 *使用片段创建PDF文档*，建议您熟悉使用汇编程序服务来汇编多个XDP文档。 (请参阅 [组装多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>您还可以将由汇编程序服务组装的表单设计传递到Forms服务，而不是输出服务。 输出服务与Forms服务的主要区别在于，Forms服务生成交互式PDF文档，而输出服务生成非交互式PDF文档。 此外，Forms服务无法生成基于打印机的输出流，如ZPL。

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-4}

要基于片段创建PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出和汇编程序客户端对象。
1. 使用汇编程序服务生成表单设计。
1. 使用输出服务生成PDF文档。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建输出和汇编程序客户端对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流会调用汇编程序服务来创建表单设计，因此请创建汇编程序客户端API对象。

**使用汇编程序服务生成表单设计**

使用汇编程序服务使用片段生成表单设计。 汇编程序服务返回 `com.adobe.idp.Document` 包含表单设计的实例。

**使用输出服务生成PDF文档**

您可以使用“输出”服务通过汇编程序服务创建的表单设计生成PDF文档。 传递 `com.adobe.idp.Document` 汇编程序服务返回到输出服务的实例。

**将PDF文档另存为PDF文件**

输出服务生成PDF文档后，可将其另存为PDF文件。

**另请参阅**

[使用Java API根据片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服务API根据片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[组装多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API根据片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用输出服务API和汇编程序服务API(Java)根据片段创建PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出和汇编程序客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 使用汇编程序服务生成表单设计。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象。
   * A `java.util.Map` 包含输入XDP文件的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象。

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已装配的XDP文档的对象。 要检索已装配的XDP文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 此方法将返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 提取组合XDP文档的方法。


1. 使用输出服务生成PDF文档。

   调用 `OutputClient` 对象 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`
   * 一个字符串值，用于指定其他资源（如图像）所在的内容根目录
   * A `com.adobe.idp.Document` 表示表单设计的对象（使用汇编程序服务返回的实例）
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据

   的 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象

1. 将PDF文档另存为PDF文件。

   * 检索 `com.adobe.idp.Document` 表示PDF文档的对象(通过调用 `OutputResult` 对象 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象。 (确保使用 `com.adobe.idp.Document` 对象 `getGeneratedDoc` 方法返回。)

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API根据片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入门（SOAP模式）：使用Java API根据片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服务API根据片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用输出服务API和汇编程序服务API（Web服务），根据片段创建PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 对与输出服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   对与汇编程序服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因为 `BLOB` 数据类型对于两个服务引用都是通用的，可完全限定 `BLOB` 数据类型。 在相应的Web服务快速启动中， `BLOB` 实例完全限定。

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出和汇编程序客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给 `OutputServiceClient.ClientCredentials.UserName.UserName`字段。
      * 为 `OutputServiceClient.ClientCredentials.UserName.Password`字段。
      * 指定常量值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`字段。
   * 分配 `BasicHttpSecurityMode.TransportCredentialOnly` 常量值 `BasicHttpBindingSecurity.Security.Mode`字段。

   >[!NOTE]
   >
   >对 `AssemblerServiceClient`对象。

1. 使用汇编程序服务生成表单设计。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需文件的对象
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何例外的对象。 要获取新创建的XDP文档，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含生成PDF文档的对象。
   * 循环访问 `Map` 对象来检索装配的表单设计。 将阵列成员的 `value` 至 `BLOB`. 传递此 `BLOB` 实例添加到输出服务。


1. 使用输出服务生成PDF文档。

   调用 `OutputServiceClient` 对象 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，用于指定其他资源（如图像）所在的内容根目录。
   * A `BLOB` 表示表单设计的对象(使用 `BLOB` 由汇编程序服务返回的实例)。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 输出 `BLOB` 对象 `generatePDFOutput2` 方法填充。 的 `generatePDFOutput2` 方法使用描述文档的生成元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 输出 `OutputResult` 包含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   的 `generatePDFOutput2` 方法返回 `BLOB` 包含非交互式PDF表单的对象。

1. 将PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，以表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `BLOB` 从检索的对象 `generatePDFOutput2` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到文件 {#printing-to-files}

您可以使用输出服务将流(如PostScript、打印机控制语言(PCL))或以下标签格式打印到文件：

* 泽布拉 — 兹普尔
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用输出服务，可以将XML数据与表单设计合并，并将表单打印到文件中。 下图显示了输出服务创建激光和标签文件。

>[!NOTE]
>
>有关将打印流发送到打印机的信息，请参阅 [将打印流发送到打印机](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-5}

要打印到文件，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置打印到文件所需的打印运行时选项。
1. 将打印流打印到文件。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 (请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要打印包含数据的文档，必须引用XML数据源，该数据源包含要用数据填充的每个表单字段的XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置打印到文件所需的打印运行时选项**

要打印到文件，必须通过指定输出服务打印到的文件的位置和名称来设置文件URI运行时选项。 例如，指示输出服务打印名为的PostScript文件 *MortgageForm.ps* 至C:\Adobe，指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定义一些可选的运行时选项。 有关可设置的所有选项的信息，请参阅 `PrintedOutputOptionsSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**将打印流打印到文件**

在引用包含表单数据的有效XML数据源并设置打印运行时选项后，可以调用输出服务，这会导致其打印文件。

**检索操作的结果**

输出服务执行操作后，它会返回各种数据项，如XML数据，以指定操作是否成功。

**另请参阅**

[使用Java API打印到文件](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服务API打印到文件](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API打印到文件 {#print-to-files-using-the-java-api}

使用输出API(Java)打印到文件：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 表示XML数据源的对象，该数据源使用其构造函数填充文档，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置打印到文件所需的打印运行时选项。

   * 创建 `PrintedOutputOptionsSpec` 对象。
   * 通过调用PrintedOutputOptionsSpec对象的 `setFileURI` 方法和传递表示文件名称和位置的字符串值。 例如，如果希望输出服务打印到C:\Adobe中名为MortgageForm.ps的PostScript文件，请指定C:\\Adobe\MortgageForm.ps。
   * 通过调用 `PrintedOutputOptionsSpec` 对象 `setCopies` 方法和传递表示副本数的整数值。

1. 将打印流打印到文件。

   通过调用 `OutputClient` 对象 `generatePrintedOutput` 方法和传递以下值：

   * A `PrintFormat` 指定要创建的打印流格式的枚举值。 例如，要创建PostScript打印流，请通过 `PrintFormat.PostScript`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定相关辅助文件（如图像文件）的位置。
   * 一个字符串值，用于指定要使用的XDC文件的位置(您可以通过 `null` 如果您使用 `PrintedOutputOptionsSpec` 对象)。
   * 的 `PrintedOutputOptionsSpec` 包含打印到文件所需的运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含包含表单数据的XML数据源的对象。

   的 `generatePrintedOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >的 `OutputResult` 对象 `getRecordLevelMetaDataList` 方法返回 `null`.

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示 `generatePrintedOutput` 方法 `OutputResult` 对象 `getStatusDoc` 方法( `OutputResult` 对象由 `generatePrintedOutput` 方法)。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为XML。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getStatusDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API打印到文件](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服务API打印到文件 {#print-to-files-using-the-web-service-api}

使用输出API（Web服务）打印到文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储表单数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值指定包含表单数据的XML文件的位置。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `binaryData` 属性。

1. 设置打印到文件所需的打印运行时选项。

   * 创建 `PrintedOutputOptionsSpec` 对象。
   * 通过为指定表示文件位置和名称的字符串值来指定文件 `PrintedOutputOptionsSpec` 对象 `fileURI` 数据成员。 例如，如果希望将输出服务打印到名为 *MortgageForm.ps* 位于C:\Adobe中，请指定C:\\Adobe\MortgageForm.ps。
   * 通过为指定表示副本数的整数值来指定要打印的副本数 `PrintedOutputOptionsSpec` 对象 `copies` 数据成员。

1. 将打印流打印到文件。

   通过调用 `OutputServiceService` 对象 `generatePrintedOutput` 方法和传递以下值：

   * A `PrintFormat` 指定要创建的打印流格式的枚举值。 例如，要创建PostScript打印流，请通过 `PrintFormat.PostScript`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定相关辅助文件（如图像文件）的位置。
   * 一个字符串值，用于指定要使用的XDC文件的位置(您可以通过 `null` 如果您使用 `PrintedOutputOptionsSpec` 对象)。
   * 的 `PrintedOutputOptionsSpec` 包含打印到文件所需的打印运行时选项的对象。
   * 的 `BLOB` 包含包含表单数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用描述文档的生成元数据填充此对象。 （仅Web服务调用需要此参数值。）
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用结果数据填充此对象。 （仅Web服务调用需要此参数值。）
   * 安 `OutputResult` 包含操作结果的对象。 （仅Web服务调用需要此参数值。）

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为XML。
   * 创建用于存储 `BLOB` 由 `OutputServiceService` 对象 `generatePDFOutput` 方法（第八个参数）。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将打印流发送到打印机 {#sending-print-streams-to-printers}

您可以使用输出服务将打印流(如PostScript、打印机控制语言(PCL))或以下标签格式发送到网络打印机：

* 泽布拉 — 兹普尔
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用输出服务，您可以将XML数据与表单设计合并，并将表单输出为打印流。 例如，您可以创建PostScript打印流并将其发送到网络打印机。 下图显示了将打印流发送到网络打印机的输出服务。

>[!NOTE]
>
>为了演示如何向网络打印机发送打印流，本部分使用SharedPrinter打印机协议向网络打印机发送PostScript打印流。

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-6}

要向网络打印机发送打印流，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置打印运行时选项
1. 检索要打印的文档。
1. 将文档发送到网络打印机。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，请创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceClient` 对象。

**引用XML数据源**

要打印包含数据的文档，必须引用XML数据源，该数据源包含要用数据填充的每个表单字段的XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置打印运行时选项**

向打印机发送打印流时，可以设置运行时选项，包括以下选项：

* **副本**:指定要发送到打印机的副本数。 默认值为 1。
* **订书钉**:使用订书机时设置XCI选项。 此选项可由订书钉元素在配置模型中指定，并仅用于PS和PCL打印机。
* **OutputJog**:当输出页面应合页（在输出托盘中发生物理移动）时，会设置XCI选项。 此选项仅适用于PS和PCL打印机。
* **OutputBin**:用于使打印驱动程序能够选择相应输出站的XCI值。

>[!NOTE]
>
>有关可设置的所有运行时选项的信息，请参阅 `PrintedOutputOptionsSpec` 类引用。

**检索要打印的文档**

检索要发送到打印机的打印流。 例如，您可以检索PostScript文件，并将其发送到打印机。

如果打印机支持PDF，则可以选择发送PDF文件。 但是，向打印机发送PDF文档的问题是每个打印机制造商都有不同的PDF解释器实现。 也就是说，一些印刷厂家使用Adobe PDF解释，但这取决于打印机。 其他打印机有自己的PDF解释器。 因此，打印结果可能会有所不同。

向打印机发送PDF文档的另一个限制是，它只是打印；除了通过打印机上的设置，它无法访问双工、纸盒选择和装订。

要检索要打印的文档，请使用 `generatePrintedOutput` 方法。 下表指定了在使用 `generatePrintedOutput` 方法。

<table>
 <thead>
  <tr>
   <th><p>打印格式 </p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>默认创建dpl203.xdc或自定义xdc输出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>创建DPL 300 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>创建DPL 400 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>创建DPL 600 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>通用颜色PCL </p></td>
   <td><p>创建通用颜色PCL(5c)输出流。</p></td>
  </tr>
  <tr>
   <td><p>通用PSLevel3 </p></td>
   <td><p>创建通用PostScript第3级输出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>创建自定义IPL输出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>创建IPL 300 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>创建IPL 400 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>创建通用单色PCL(5e)输出流。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>创建通用PostScript 2级输出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>创建自定义TPCL输出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>创建TPCL 305 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>创建TPCL 600 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>创建ZPL 203 DPI输出流。</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>创建ZPL 300 DPI输出流。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您还可以使用 `generatePrintedOutput2` 方法。 但是，与“将打印流发送到打印机”部分关联的快速入门使用 `generatePrintedOutput` 方法。

**将打印流发送到网络打印机**

在检索要打印的文档后，可以调用输出服务，这会使其向网络打印机发送打印流。 要使输出服务成功找到打印机，必须指定打印服务器和打印机名称。 此外，还必须指定打印协议。

>[!NOTE]
>
>如果PDFG安装在Forms服务器上，并且服务器在Windows Server 2008上运行，则无法使用SharedPrinter属性。 在这种情况下，请使用其他打印机协议。

>[!NOTE]
>
>如果您使用网络打印机，并且访问机制为SharedPrinter，则需要指定打印机的完整网络路径。使用Java API将打印流发送到网络打印机

使用输出API(Java)将打印流发送到网络打印机：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源

   * 创建 `java.io.FileInputStream` 表示XML数据源的对象，该数据源使用其构造函数填充文档，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置打印运行时选项

   创建 `PrintedOutputOptionsSpec` 表示打印运行时选项的对象。 例如，您可以通过调用 `PrintedOutputOptionsSpec` 对象 `setCopies` 方法。

   >[!NOTE]
   >
   >不能使用 `PrintedOutputOptionsSpec` 对象 `setPagination` 方法。 同样，您不能为ZPL打印流设置以下选项：OutputJog、PageOffset和Stapter。 的 `setPagination` 方法对于PostScript生成无效。 此插件仅对PCL生成有效。

1. 检索要打印的文档

   * 通过调用 `OutputClient` 对象 `generatePrintedOutput` 方法和传递以下值：

      * A `PrintFormat` 指定打印流的枚举值。 例如，要创建PostScript打印流，请通过 `PrintFormat.PostScript`.
      * 指定表单设计名称的字符串值。
      * 一个字符串值，用于指定相关辅助文件（如图像文件）的位置。
      * 一个字符串值，用于指定要使用的XDC文件的位置。
      * 的 `PrintedOutputOptionsSpec` 对象，其中包含打印到文件所需的运行时选项。
      * 的 `com.adobe.idp.Document` 表示包含要与表单设计合并的表单数据的XML数据源的对象。

      此方法将返回 `OutputResult` 包含操作结果的对象。

   * 创建 `com.adobe.idp.Document` 通过调用发送到打印机的对象 `OutputResult` 对象s `getGeneratedDoc` 方法。 此方法将返回 `com.adobe.idp.Document` 对象。


1. 将打印流发送到网络打印机

   通过调用 `OutputClient` 对象 `sendToPrinter` 方法和传递以下值：

   * A `com.adobe.idp.Document` 表示要发送到打印机的打印流的对象。
   * A `PrinterProtocol` 指定要使用的打印机协议的枚举值。 例如，要指定SharedPrinter协议，请通过 `PrinterProtocol.SharedPrinter`.
   * 指定打印服务器名称的字符串值。 例如，假定打印服务器的名称为PrintSever1，请传递 `\\\PrintSever1`.
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1, pass `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >的 `sendToPrinter` 方法已添加到版本8.2.1中的AEM Forms API。

### 使用Web服务API将打印流发送到打印机 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用输出API（Web服务）将打印流发送到网络打印机：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储表单数据。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，以指定包含表单数据的XML文件的位置。
   * 创建用于存储 `System.IO.FileStream` 对象。 通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 设置打印运行时选项。

   创建 `PrintedOutputOptionsSpec` 对象。 例如，您可以通过为 `PrintedOutputOptionsSpec` 对象 `copies` 数据成员。

   >[!NOTE]
   >
   >不能使用 `PrintedOutputOptionsSpec` 对象 `pagination` 数据成员。 同样，您不能为ZPL打印流设置以下选项：OutputJog、PageOffset和Steper。 的 `pagination` 数据成员对于PostScript生成无效。 此插件仅对PCL生成有效。

1. 检索要打印的文档。

   * 通过调用 `OutputServiceService` 对象 `generatePrintedOutput` 方法和传递以下值：

      * A `PrintFormat` 指定打印流的枚举值。 例如，要创建PostScript打印流，请通过 `PrintFormat.PostScript`.
      * 指定表单设计名称的字符串值。
      * 一个字符串值，用于指定相关辅助文件（如图像文件）的位置。
      * 一个字符串值，用于指定要使用的XDC文件的位置。
      * 的 `PrintedOutputOptionsSpec` 包含在向网络打印机发送打印流时使用的打印运行时选项的对象。
      * 的 `BLOB` 包含包含表单数据的XML数据源的对象。
      * A `BLOB` 由填充的对象 `generatePrintedOutput` 方法。 的 `generatePrintedOutput` 方法使用描述文档的生成元数据填充此对象。 （仅Web服务调用需要此参数值。）
      * A `BLOB` 由填充的对象 `generatePrintedOutput` 方法。 的 `generatePrintedOutput` 方法使用结果数据填充此对象。 （仅Web服务调用需要此参数值。）
      * 安 `OutputResult` 包含操作结果的对象。 （仅Web服务调用需要此参数值。）
   * 创建 `BLOB` 对象。 `OutputResult` 对象s `generatedDoc` 方法。 此方法将返回 `BLOB` 包含由 `generatePrintedOutput` 方法。


1. 将打印流发送到网络打印机。

   通过调用 `OutputClient` 对象 `sendToPrinter` 方法和传递以下值：

   * A `BLOB` 表示要发送到打印机的打印流的对象。
   * A `PrinterProtocol` 指定要使用的打印机协议的枚举值。 例如，要指定SharedPrinter协议，请通过 `PrinterProtocol.SharedPrinter`.
   * A `bool` 值，指定是否使用前一个参数值。 传递值 `true`. （仅Web服务调用需要此参数值。）
   * 指定打印服务器名称的字符串值。 例如，假定打印服务器的名称为PrintSever1，请传递 `\\\PrintSever1`.
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1，传递 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >的 `sendToPrinter` 方法已添加到版本8.2.1中的AEM Forms API。

## 创建多个输出文件 {#creating-multiple-output-files}

输出服务可以为XML数据源中的每条记录创建单独的文档，或为包含所有记录的单个文件创建单独的文档（默认功能为此功能）。 例如，假定有10条记录位于XML数据源中，并且您指示输出服务使用输出服务API为每个记录创建单独的PDF文档（或其他类型的输出）。 因此，输出服务会生成十个PDF文档。 （您可以向打印机发送多个打印流，而不是创建文档。）

下图还显示了输出服务处理包含多个记录的XML数据文件。 但是，假设您指示输出服务创建包含所有数据记录的单个PDF文档。 在这种情况下，输出服务会生成一个包含所有记录的文档。

下图显示了输出服务处理包含多个记录的XML数据文件。 假设您指示输出服务为每个数据记录创建单独的PDF文档。 在这种情况下，输出服务会为每个数据记录生成单独的PDF文档。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

以下XML数据显示了一个包含三个数据记录的数据文件示例。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

请注意，开始和结束每个数据记录的XML元素是 `LoanRecord`. 此XML元素由生成多个文件的应用程序逻辑引用。

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-7}

要基于XML数据源创建多个PDF文件，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成多个PDF文件。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

引用包含多个记录的XML数据源。 必须使用XML元素来分隔数据记录。 例如，在本节前面显示的示例XML数据源中，用于分隔数据记录的XML元素将被命名 `LoanRecord`.

要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置PDF运行时选项**

必须为输出服务设置以下运行时选项，才能基于XML数据源成功创建多个文件：

* **许多文件**:指定输出服务是创建单个文档还是多个文档。 您可以指定true或false。 要为XML数据源中的每个数据记录创建单独的文档，请指定true。
* **文件URI**:指定输出服务生成的文件的位置。 例如，假定您指定C:\\Adobe\forms\Loan.pdf。 在这种情况下，输出服务将创建一个名为Loan.pdf的文件，并将该文件放在C:\\Adobe\forms folder文件夹中。 如果有多个文件，文件名为Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果指定文件位置，则文件将放在服务器上，而不是客户端计算机上。
* **记录名称**:在数据源中指定用于分隔数据记录的XML元素名称。 例如，在本节前面显示的示例XML数据源中，用于分隔数据记录的XML元素被调用 `LoanRecord`. (您可以通过为记录级别分配一个指示包含数据记录的元素级别的数值，来设置记录级别，而不是设置记录名称运行时选项。 但是，您只能设置记录名称或记录级别。 不能同时设置两个值。)

**设置渲染运行时选项**

创建多个文件时，可以设置渲染运行时选项。 尽管这些选项不是必需的（与输出运行时选项不同，它们是必需的），但您可以执行诸如提高输出服务性能之类的任务。 例如，您可以缓存输出服务使用的表单设计以提高性能。

当输出服务处理批处理记录时，它将以增量方式读取包含多个记录的数据。 即，输出服务将数据读入内存，并在处理批处理记录时释放数据。 当设置了两个运行时选项中的任一选项时，输出服务会以增量方式加载数据。 如果设置记录名称运行时选项，输出服务将以增量方式读取数据。 同样，如果将“记录级别”运行时间选项设置为2或更大，则“输出”服务会以增量方式读取数据。

您可以使用 `PDFOutputOptionsSpec` 或 `PrintedOutputOptionSpec` 对象 `setLazyLoading` 方法。 您可以传递值 `false` 关闭增量加载的方法。

**生成多个PDF文件**

在引用包含多个数据记录并设置运行时选项的有效XML数据源后，可以调用输出服务，以使其生成多个文件。 在生成多个记录时， `OutputResult` 对象 `getGeneratedDoc` 方法返回 `null`.

**检索操作的结果**

输出服务执行操作后，将返回指定操作是否成功的XML数据。 输出服务返回以下XML。 在这种情况下，输出服务生成了42个文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建多个PDF文件 {#create-multiple-pdf-files-using-the-java-api}

使用输出API(Java)创建多个PDF文件：

1. 包含项目文件”

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。.

1. 创建输出客户端对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源

   * 创建 `java.io.FileInputStream` 表示包含多个记录的XML数据源的对象。该对象使用其构造函数并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setGenerateManyFiles` 方法。 例如，传递值 `true` 指示输出服务为XML数据源中的每个记录创建单独的PDF文件。 (如果您通过 `false`，则输出服务会生成包含所有记录的单个PDF文档)。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setFileUri` 方法，并传递一个字符串值，该值指定输出服务生成的文件的位置。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。
   * 通过调用 `OutputOptionsSpec` 对象 `setRecordName` 方法，并传递一个字符串值，该字符串值指定用于分隔数据记录的数据源中的XML元素名称。 (例如，请考虑本节前面显示的XML数据源。 用于分隔数据记录的XML元素的名称为LoanRecord)。

1. 设置渲染运行时选项

   * 创建 `RenderOptionsSpec` 对象。
   * 通过调用 `RenderOptionsSpec` 对象 `setCacheEnabled` 和 `Boolean` 值 `true`.

1. 生成多个PDF文件

   通过调用 `OutputClient` 对象 `generatePDFOutput` 方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作的结果

   * 创建 `java.io.File` 表示将包含 `generatePDFOutput` 方法。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `applyUsageRights` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API创建多个PDF文件](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建多个PDF文件 {#create-multiple-pdf-files-using-the-web-service-api}

使用输出API（Web服务）创建多个PDF文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储包含多个记录的表单数据。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示包含多个记录的XML文件的文件位置。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过为 `OutputOptionsSpec` 对象 `generateManyFiles` 数据成员。 例如，分配值 `true` 指示输出服务为XML数据源中的每个记录创建单独的PDF文件的数据成员。 (如果您为 `false` 对于此数据成员，输出服务将生成一个包含所有记录的PDF)。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成的文件到 `OutputOptionsSpec` 对象 `fileURI` 数据成员。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。
   * 通过指定一个字符串值来设置记录名称选项，该字符串值指定将数据记录分隔到 `OutputOptionsSpec` 对象 `recordName` 数据成员。
   * 通过分配一个整数值来设置副本选项，该整数值指定输出服务生成的副本数 `OutputOptionsSpec` 对象 `copies` 数据成员。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计，以通过分配值来提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象 `cacheEnabled` 数据成员。

1. 生成多个PDF文件。

   通过调用 `OutputServiceService` 对象 `generatePDFOutput`方法和传递以下值：

   * TransformationFormat枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用描述文档的生成元数据填充此对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用结果数据填充此对象。
   * 安 `OutputResult` 包含操作结果的对象。

1. 检索操作的结果

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建用于存储 `BLOB` 由 `OutputServiceService` 对象 `generatePDFOutput` 方法（第八个参数）。 通过获取 `BLOB` 对象 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建搜索规则 {#creating-search-rules}

您可以创建搜索规则，以使输出服务检查输入数据，并根据数据内容使用不同的表单设计来生成输出。 例如，如果文本 *抵押* 位于输入数据内，则输出服务可以使用名为Mortgage.xdp的表单设计。 同样，如果文本 *汽车* 位于输入数据中，则输出服务可以使用另存为AutomicalLoan.xdp的表单设计。 尽管输出服务可以生成不同的输出类型，但此部分假定输出服务生成一个PDF文件。 下图显示了通过处理XML数据文件并使用多个表单设计之一来生成PDF文件的输出服务。

此外，输出服务还能够生成文档包，其中在数据集中提供了多个记录，并且每个记录都与表单设计匹配，并且单个文档由多个表单设计组成。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-8}

要指示输出服务在生成文档时使用搜索规则，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 定义搜索规则。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF文档。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您将需要将adobe-utilities.jar和jbossall-client.jar替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。

**引用XML数据源**

要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 只要指定了所有XML元素，就不必匹配XML元素的显示顺序。

**定义搜索规则**

要定义搜索规则，您需要定义输出服务在输入数据中搜索的一个或多个文本模式。 对于您定义的每个文本模式，可指定相应的表单设计（如果文本模式已找到）。 如果找到文本模式，则输出服务将使用相应的表单设计来生成输出。 文本模式的示例有 *抵押*.

>[!NOTE]
>
>如果未找到文本模式，则使用默认表单。 确保您使用的所有表单设计都位于内容根目录中。

**设置PDF运行时选项**

为使输出服务能够基于多个表单设计成功创建PDF文档，请设置以下PDF运行时选项：

* **文件URI**:指定输出服务生成的PDF文件的名称和位置。
* **规则**:指定您定义的规则。
* **LookAHead**:指定要从输入数据文件的开头扫描定义的文本模式的字节数。 默认为500字节。

**设置渲染运行时选项**

在创建PDF文件时，可以设置渲染运行时选项。 尽管这些选项不是必需的(与PDF运行时选项不同)，但您可以执行诸如提高输出服务性能之类的任务。 例如，您可以缓存输出服务使用的表单设计以提高性能。

**生成PDF文档**

在引用有效的XML数据源并设置运行时选项后，可以调用输出服务，从而生成PDF文档。 如果输出服务在输入数据中找到指定的文本模式，则使用相应的表单设计。 如果未使用文本模式，则输出服务将使用默认的表单设计。

**检索操作的结果**

输出服务执行操作后，将返回指定操作是否成功的XML数据。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建搜索规则 {#create-search-rules-using-the-java-api}

使用输出API(Java)创建搜索规则：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 表示XML数据源的对象，该XML数据源使用其构造函数填充PDF文档，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 定义搜索规则。

   * 创建 `Rule` 对象。
   * 通过调用 `Rule` 对象 `setPattern` 方法和传递指定文本模式的字符串值。
   * 通过调用 `Rule` 对象 `setForm` 方法。 传递指定表单设计名称的字符串值。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 创建 `java.util.List` 对象 `java.util.ArrayList` 构造函数。
   * 对于 `Rule` 创建的对象，调用 `java.util.List` 对象 `add` 方法和通过 `Rule` 对象。


1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 指定输出服务通过调用 `PDFOutputOptionsSpec` 对象 `setFileURI` 方法。 传递指定PDF文件位置的字符串值。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setRules` 方法。 传递 `java.util.List` 包含的对象 `Rule` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象 `setLookAhead` 方法。 传递表示字节数的整数值。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 通过调用 `RenderOptionsSpec` 对象 `setCacheEnabled` 传递 `true`.

1. 生成PDF文档。

   通过调用 `OutputClient` 对象 `generatePDFOutput` 方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定默认表单设计名称的字符串值。 即，在未找到文本模式时使用的表单设计。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `com.adobe.idp.Document` 对象，其中包含由输出服务搜索的表单数据以查找定义的文本模式。

   的 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示 `generatePDFOutput` 方法 `OutputResult` 对象 `getStatusDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `getStatusDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入门（SOAP模式）：使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建搜索规则 {#create-search-rules-using-the-web-service-api}

使用输出API（Web服务）创建搜索规则：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储将与PDF文档合并的数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 定义搜索规则。

   * 创建 `Rule` 对象。
   * 通过为 `Rule` 对象 `pattern` 数据成员。
   * 通过为指定表单设计的字符串值指定 `Rule` 对象 `form` 数据成员。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 创建 `MyArrayOf_xsd_anyType` 用于存储规则的对象。
   * 分配每个 `Rule` 对象到的元素 `MyArrayOf_xsd_anyType` 数组。 调用 `MyArrayOf_xsd_anyType` 对象 `Add` 方法 `Rule` 对象。


1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成到的PDF文件的位置 `PDFOutputOptionsSpec` 对象 `fileURI` 数据成员。 “文件URI”选项与托管AEM Forms的J2EE应用程序服务器（而非客户端计算机）相关。
   * 通过分配一个整数值来设置副本选项，该整数值指定输出服务生成的副本数 `PDFOutputOptionsSpec` 对象 `copies` 数据成员。
   * 通过为 `MyArrayOf_xsd_anyType` 将规则存储到 `PDFOutputOptionsSpec` 对象 `rules` 数据成员。
   * 通过指定一个整数值来设置要扫描的字节数，该整数值表示要扫描到的字节数 `PDFOutputOptionsSpec` 对象 `lookAhead` 数据方法。

1. 设置渲染运行时选项

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计，以便通过分配值来提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象 `cacheEnabled` 数据成员。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `pdfVersion` 成员(如果输入文档是Acrobat表单)。 输出PDF文档保留了Acrobat表单的PDF版本。 同样，您不能使用 `RenderOptionsSpec` 对象 `taggedPDF` 方法(如果输入文档是Acrobat表单)。

   >[!NOTE]
   >
   >不能使用 `RenderOptionsSpec` 对象 `linearizedPDF` 成员。 有关信息，请参阅 [数字签名PDF文档](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. 生成PDF文档

   通过调用 `OutputServiceService` 对象 `generatePDFOutput`方法和传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`.
   * 指定表单设计名称的字符串值。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含呈现运行时选项的对象。
   * 的 `BLOB` 包含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用描述文档的生成元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 的 `generatePDFOutput` 方法使用结果数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 安 `OutputResult` 包含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   >[!NOTE]
   >
   >通过调用生成PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名、已认证或包含使用权限的XFAPDF表单合并。 有关使用权限的信息，请参阅 [将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. 检索操作的结果

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为XML。
   * 创建用于存储 `BLOB` 由 `OutputServiceService` 对象 `generatePDFOutput` 方法（第八个参数）。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 拼合PDF文档 {#flattening-pdf-documents}

您可以使用输出服务将交互式PDF文档转换为非交互式PDF。 交互式PDF文档允许用户输入或修改PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为 *拼合*. 对PDF文档进行扁平化处理后，用户无法修改文档字段中的数据。 扁平化PDF文档的一个原因是要确保数据无法修改。

您可以拼合以下类型的PDF文档：

* 交互式XFAPDF文档
* AcrobatForms

尝试拼合非交互式PDF文档的PDF会导致异常。

>[!NOTE]
>
>有关输出服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-9}

要将交互式PDF文档扁平化为非交互式PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 检索交互式PDF文档。
1. 转换PDF文档。
1. 将非交互式PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用的是输出Web服务API，请创建 `OutputServiceService` 对象。

**检索交互式PDF文档**

检索要转换为非交互式PDF文档的交互式PDF文档。 尝试转换非交互式PDF文档时，会导致异常。

**转换PDF文档**

检索交互式PDF文档后，可将其转换为非交互式PDF文档。 输出服务会返回非交互式PDF文档。

**将非交互式PDF文档另存为PDF文件**

您可以将非交互式PDF文档另存为PDF文件。

**另请参阅**

[使用Java API扁平化PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服务API拼合PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速入门](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API扁平化PDF文档 {#flatten-a-pdf-document-using-the-java-api}

使用输出API(Java)将交互式PDF文档扁平化为非交互式PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 检索交互式PDF文档。

   * 创建 `java.io.FileInputStream` 表示要通过使用其构造函数进行转换的交互式PDF文档的对象，并传递指定交互式PDF文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 转换PDF文档。

   通过调用 `OutputServiceService` 对象 `transformPDF` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含交互式PDF文档的对象。
   * A `TransformationFormat` 枚举值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修订号的枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * 一个字符串值，表示修正数和年份，以冒号分隔。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * A `PDFAConformance` 表示PDF/A符合性级别的枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `null`.

   的 `transformPDF` 方法返回 `com.adobe.idp.Document` 包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `Document` 对象 `copyToFile` 复制内容的方法 `Document` 对象到文件(确保使用 `Document` 由返回的对象 `transformPDF` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入门（SOAP模式）：使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API拼合PDF文档 {#flatten-a-pdf-document-using-the-web-service-api}

使用输出API（Web服务）将交互式PDF文档扁平化为非交互式PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。 但是，请指定 `?blob=mtom` 来使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索交互式PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储交互式PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示交互式PDF文档的文件位置。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 转换PDF文档。

   通过调用 `OutputClient` 对象 `transformPDF` 方法和传递以下值：

   * A `BLOB` 包含交互式PDF文档的对象。
   * A `TransformationFormat` 枚举值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修订号的枚举值。
   * 一个布尔值，用于指定 `PDFARevisionNumber` 使用枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `false`.
   * 一个字符串值，表示修正数和年份，以冒号分隔。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * A `PDFAConformance` 表示PDF/A符合性级别的枚举值。
   * 布尔值，指定 `PDFAConformance` 使用枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `false`.

   的 `transformPDF` 方法返回 `BLOB` 包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示非交互式PDF文档的文件位置。
   * 创建用于存储 `BLOB` 由返回的对象 `transformPDF` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
