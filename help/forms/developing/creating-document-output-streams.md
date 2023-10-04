---
title: 创建文档输出流
description: 使用Output服务将文档转换为PDF(包括PDF/A文档)、PostScript、Printer Control Language (PCL)和Zebra - ZPL、Intermec - IPL、Datamax - DPL和TecToshiba - TPCL标签格式。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# 创建文档输出流  {#creating-document-output-streams}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

**关于输出服务**

Output服务允许您以PDF(包括PDF/A文档)、PostScript、打印机控制语言(PCL)和以下标签格式输出文档：

* 斑马 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服务，您可以将XML表单数据与表单设计合并，并将文档输出到网络打印机或文件。

可通过两种方式将表单设计（XDP文件）传递到Output服务。 您可以传递 `com.adobe.idp.Document` 包含表单设计到Output服务的实例。 或者，您可以传递一个用于指定表单设计位置的URI值。 这两种方法将在中介绍 *使用AEM表单编程*.

>[!NOTE]
>
>Output服务不支持包含应用程序对象特定脚本的AcroformPDF文档。 包含应用程序对象特定脚本的AcroformPDF文档不会渲染。

以下部分将演示如何使用URI值将表单设计传递到Output服务：

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)

以下各节将演示如何在 `com.adobe.idp.Document` 实例：

* [将位于Content Services（已弃用）中的文档传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

在决定使用哪种技术时，需要考虑的一个事项是，如果您从其他AEM Forms服务获取表单设计，然后在一个解决方案中传递它， `com.adobe.idp.Document` 实例。 两者都是 *将文档传递到Output服务* 和 *使用片段创建PDF文档* 部分将演示如何从其他AEM Forms服务获取表单设计。 第一部分从内容服务中检索表单设计（已弃用）。 第二部分从Assembler服务检索窗体设计。

如果您从固定位置（如文件系统）获取窗体设计，则可以使用任一技术。 也就是说，您可以为XDP文件指定URI值，或者使用 `com.adobe.idp.Document` 实例。

要在创建PDF文档时传递指定表单设计位置的URI值，请使用 `generatePDFOutput` 方法。 同样，要传递 `com.adobe.idp.Document` 创建PDF文档时，使用 `generatePDFOutput2` 方法。

在将输出流发送到网络打印机时，也可以使用任一技术。 要通过传递输出流到打印机，请执行以下操作 `com.adobe.idp.Document` 包含表单设计的实例，请使用 `sendToPrinter2`方法。 要通过传递URI值将输出流发送到打印机，请使用 `sendToPrinter`方法。 此 *将打印流发送到打印机* 部分使用 `sendToPrinter` 方法。

您可以使用Output服务完成这些任务：

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)
* [将位于Content Services（已弃用）中的文档传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [打印到文件](creating-document-output-streams.md#printing-to-files)
* [将打印流发送到打印机](creating-document-output-streams.md#sending-print-streams-to-printers)
* [创建多个输出文件](creating-document-output-streams.md#creating-multiple-output-files)
* [创建搜索规则](creating-document-output-streams.md#creating-search-rules)
* [拼合PDF文档](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 创建PDF文档 {#creating-pdf-documents}

您可以使用Output服务创建基于表单设计和您提供的XML表单数据的PDF文档。 Output服务创建的PDF文档不是交互式PDF文档；用户无法输入或修改表单数据。

如果要创建用于长期存储的PDF文档，建议您创建一个PDF/A文档。 (请参阅 [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents).)

要创建可让用户输入数据的交互式PDF表单，请使用Forms服务。 (请参阅 [呈现交互式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

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

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 您计划使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

考虑以下示例贷款申请表。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要将数据合并到此表单设计，必须创建与表单相对应的XML数据源。 以下XML表示与示例抵押应用程序表单相对应的XDP XML数据源。

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

创建PDF文档时设置文件URI选项。 此选项指定Output服务生成的PDF文件的名称和位置。

>[!NOTE]
>
>您可以用编程方式从输出服务返回的复杂数据类型检索PDF文档，而不是设置文件URI运行时选项。 但是，通过设置文件URI运行时选项，您无需创建以编程方式检索PDF文档的应用程序逻辑。

**设置渲染运行时选项**

创建PDF文档时，可以设置渲染运行时选项。 虽然这些选项不是必需的(与所需的PDF运行时选项不同)，但您可以执行诸如提高输出服务性能的任务。 例如，您可以缓存Output服务使用的表单设计以提高其性能。

如果您使用已标记的Acrobat表单作为输入，则无法使用输出服务Java或Web服务API来关闭已标记的设置。 如果您尝试以编程方式将此选项设置为 `false`，则结果PDF文档仍被标记。

>[!NOTE]
>
>如果未指定渲染运行时选项，则使用默认值。 有关呈现运行时选项的信息，请参见 `RenderOptionsSpec` 类引用。 (请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**生成PDF文档**

在引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用Output服务，从而生成PDF文档。

在生成PDF文档时，您可以指定Output服务创建PDF文档所需的URI值。 窗体设计可以存储在服务器文件系统等位置或作为AEM Forms应用程序的一部分进行存储。 可以使用内容根URI值引用作为Forms应用程序一部分的表单设计（或其他资源，例如图像文件） `repository:///`. 例如，考虑以下名为的表单设计 *Loan.xdp* 位于名为的Forms应用程序中 *Applications/FormsApplication*：

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

要访问上图所示的Loan.xdp文件，请指定 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 作为传递给的第三个参数 `OutputClient` 对象的 `generatePDFOutput` 方法。 指定表单名称(*Loan.xdp*)作为传递给的第二个参数 `OutputClient` 对象的 `generatePDFOutput` 方法。

如果XDP文件包含图像（或其他资源，如片段），请将资源放置在与XDP文件相同的应用程序文件夹中。 AEM Forms使用内容根URI作为基本路径来解析对图像的引用。 例如，如果Loan.xdp文件包含图像，请确保将该图像放在 `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Forms在调用 `OutputClient` 对象的 `generatePDFOutput` 或 `generatePrintedOutput` 方法。

>[!NOTE]
>
>要查看通过引用Forms应用程序中的XDP来创建PDF文档的完整快速入门，请参阅 [快速入门（EJB模式）：使用Java API基于应用程序XDP文件创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**检索操作的结果**

在Output服务执行操作之后，它会返回各种数据项，如指定操作是否成功的状态XML数据。

**另请参阅**

[使用Java API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服务API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF文档 {#create-a-pdf-document-using-the-java-api}

使用输出API (Java)创建PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 对象，表示用于填充PDF文档的XML数据源，该数据源使用其构造函数，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象。 传递 `java.io.FileInputStream` 对象。

1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setFileURI` 方法。 传递一个字符串值，该值指定Output服务生成的PDF文件的位置。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计以通过调用 `RenderOptionsSpec` 对象的 `setCacheEnabled` 和传递 `true`.

   >[!NOTE]
   >
   >不能使用设置PDF文档的版本 `RenderOptionsSpec` 对象的 `setPdfVersion` 方法：输入文档是Acrobat表单(在Acrobat中创建的表单)或已签名或认证的XFA文档。 输出PDF文档保留原始PDF版本。 Adobe PDF同样，您无法通过调用 `RenderOptionsSpec` 对象的 `setTaggedPDF` 方法：输入文档是Acrobat表单或已签名或认证的XFA文档。

   >[!NOTE]
   >
   >不能使用设置线性PDF选项 `RenderOptionsSpec` 对象的 `setLinearizedPDF` 方法，如果输入的PDF文件经过认证或数字签名。 (请参阅 [对PDF文档进行数字签名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 生成PDF文档。

   PDF通过调用 `OutputClient` 对象的 `generatePDFOutput` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象。

   此 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >当通过调用PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名或认证的XFAPDF表单合并。 (请参阅 [数字签名和认证文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >此 `OutputResult` 对象的 `getRecordLevelMetaDataList` 方法返回 `null`*.*

   >[!NOTE]
   >
   >PDF您还可以通过调用 `OutputClient` 对象的 `generatePDFOutput2` 方法。 (请参阅 [将位于Content Services（已弃用）中的文档传递到输出服务&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 检索操作的结果。

   * 检索 `com.adobe.idp.Document` 表示以下对象的状态： `generatePDFOutput` 操作方法是调用 `OutputResult` 对象的 `getStatusDoc` 方法。 此方法返回指定操作是否成功的状态XML数据。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getStatusDoc` 方法)。

   尽管Output服务将PDF文档写入由传递到的参数指定的位置 `PDFOutputOptionsSpec` 对象的 `setFileURI` PDF方法，您可以通过调用 `OutputResult` 对象的 `getGeneratedDoc` 方法。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速入门（SOAP模式）：使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建PDF文档 {#create-a-pdf-document-using-the-web-service-api}

使用输出API（Web服务）创建PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储将与PDF文档合并的XML数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含表单数据的XML文件的文件位置。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成的PDF文件的位置。 `PDFOutputOptionsSpec` 对象的 `fileURI` 数据成员。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计以通过分配值提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象的 `cacheEnabled` 数据成员。

   >[!NOTE]
   >
   >不能使用设置PDF文档的版本 `RenderOptionsSpec` 对象的 `setPdfVersion` 方法：输入文档是Acrobat表单(在Acrobat中创建的表单)或已签名或认证的XFA文档。 输出PDF文档保留原始PDF版本。 Adobe PDF同样，您无法通过调用 `RenderOptionsSpec` 对象的 `setTaggedPDF`*方法(如果输入文档是Acrobat表单或已签名或认证的XFA文档)。*

   >[!NOTE]
   >
   >不能使用设置线性PDF选项 `RenderOptionsSpec` 对象的 `linearizedPDF` 成员，如果输入的PDF文档经过认证或数字签名。 (请参阅 [对PDF文档进行数字签名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. 生成PDF文档。

   PDF通过调用 `OutputServiceService` 对象的 `generatePDFOutput`方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用结果数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * An `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值）。

   >[!NOTE]
   >
   >当通过调用PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名或认证的XFAPDF表单合并。 (请参阅 [数字签名和认证文档&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >PDF您还可以通过调用 `OutputClient` 对象的 `generatePDFOutput2` 方法。 (请参阅 [将位于Content Services（已弃用）中的文档传递到输出服务&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建一个字节数组，用于存储 `BLOB` 使用结果数据填充的对象 `OutputServiceService` 对象的 `generatePDFOutput` 方法（第八个参数）。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` `field`.
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

   另请参阅

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >此 `OutputServiceService` 对象的 `generateOutput` 方法已弃用。

## 创建PDF/A文档 {#creating-pdf-a-documents}

您可以使用Output服务创建PDF/A文档。 由于PDF/A是用于长期保存文档内容的存档格式，因此所有字体都将嵌入，并且文件是未压缩的。 因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/文档不包含音频和视频内容。 与其他“输出”服务任务一样，提供表单设计和数据以与表单设计合并，以创建PDF/文档。

PDF/A-1规范包含两个一致性级别，即a和b。两者之间的主要区别在于对逻辑结构（辅助功能）的支持，合规性级别b不需要该支持。无论符合性级别如何，PDF/A-1都会指示所有字体都嵌入到生成的PDF/A文档中。

尽管PDF/A是归档PDF文档的标准，但是如果标准PDF文档满足公司的需要，则不必使用PDF/A进行归档。 PDF/A标准的目的是建立一个PDF文件，它可以长期存储并且满足文档保存要求。 例如，无法将URL嵌入到PDF/A中，因为随着时间的推移，该URL可能会变得无效。

您的组织必须评估自己的需求、您打算保留文档的时间长度、文件大小考虑因素，并确定自己的归档策略。 您可以使用DocConverter服务以编程方式确定PDF文档是否符合PDF/A标准。 (请参阅 [以编程方式确定PDF/A合规性](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

PDF/文档必须使用在表单设计中指定的字体，且不能替换字体。 因此，如果位于PDF文档中的字体在主机操作系统(OS)上不可用，则会发生异常。

在Acrobat中打开PDF/A文档时，将显示一条消息，确认该文档为PDF/A文档，如下图所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM网站中有一个PDF/常见问题解答部分，您可以在以下位置访问该部分： [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_65).

### 步骤摘要 {#summary_of_steps-1}

要创建PDF/文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置PDF/A运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF/文档。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建自定义应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置PDF/A运行时选项**

创建PDF/A文档时，可以设置“文件URI”选项。 URI相对于托管AEM Forms的J2EE应用程序服务器。 也就是说，如果设置C:\Adobe ，文件将写入服务器上的文件夹，而不是客户端计算机。 URI指定Output服务生成的PDF/A文件的名称和位置。

**设置渲染运行时选项**

在创建PDF/A文档时，可以设置渲染运行时选项。 可以设置的两个PDF/A相关选项是 `PDFAConformance` 和 `PDFARevisionNumber` 值。 此 `PDFAConformance` 值指的是PDF文档如何遵守规定保存长期电子文档的要求。 此选项的有效值为 `A` 和 `B`. 有关级别a和b合规性的信息，请参阅标题为PDF/A-1的ISO规范 *ISO 19005-1文档管理*.

此 `PDFARevisionNumber` 值表示PDF/A文档的修订号。 有关PDF/A文档的修订版本号的信息，请参阅标题为“PDF/A-1 ISO规范”的 *ISO 19005-1文档管理*.

>[!NOTE]
>
>您不能将已标记的Adobe PDF选项设置为 `false` 创建PDF/A 1A文档时。 PDF/A 1A将始终是带标签的PDF文档。 此外，您无法将已标记的Adobe PDF选项设置为 `true` 创建PDF/A 1B文档时。 PDF/A 1B将始终是未标记的PDF文档。

**生成PDF/文档**

在引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用输出服务，使其生成PDF/A文档。

**检索操作的结果**

在Output服务执行操作后，它会返回各种数据项，如指定操作是否成功的XML数据。

**另请参阅**

[使用Java API创建PDF/文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服务API创建PDF/文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF/文档 {#create-a-pdf-a-document-using-the-java-api}

使用输出API (Java)创建PDF/文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 对象，表示用于填充PDF/A文档的XML数据源，该数据源使用其构造函数，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置PDF/A运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setFileURI` 方法。 传递一个字符串值，该值指定Output服务生成的PDF文件的位置。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 设置 `PDFAConformance` 值(通过调用 `RenderOptionsSpec` 对象的 `setPDFAConformance` 方法和传递 `PDFAConformance` 指定一致性级别的枚举值。 例如，要指定一致性级别A，请通过 `PDFAConformance.A`.
   * 设置 `PDFARevisionNumber` 值(通过调用 `RenderOptionsSpec` 对象的 `setPDFARevisionNumber` 方法和传递 `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >PDF/A文档的PDF版本是1.4，无论您为指定的值是什么 `RenderOptionsSpec` 对象的 `setPdfVersion`*方法。*

1. 生成PDF/文档。

   PDF通过调用 `OutputClient` 对象的 `generatePDFOutput` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF/文档，请指定 `TransformationFormat.PDFA`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象。

   此 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >此 `OutputResult` 对象的 `getRecordLevelMetaDataList` 方法返回 `null`.

   >[!NOTE]
   >
   >PDF您还可以通过调用 `OutputClient` 对象的 `generatePDFOutput`2方法。 (请参阅 [将位于Content Services（已弃用）中的文档传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示以下对象的状态： `generatePDFOutput` 方法调用 `OutputResult` 对象的 `getStatusDoc` 方法。
   * 创建 `java.io.File` 将包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getStatusDoc` 方法)。

   >[!NOTE]
   >
   >尽管Output服务将PDF/A文档写入由传递到的参数指定的位置 `PDFOutputOptionsSpec` 对象的 `setFileURI` PDF方法，您可以通过调用 `OutputResult` 对象的 `getGeneratedDoc` 方法。

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
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储将与PDF/A文档合并的数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 设置PDF/A运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成的PDF文件的位置。 `PDFOutputOptionsSpec` 对象的 `fileURI` 数据成员。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 设置 `PDFAConformance` 值（通过分配） `PDFAConformance` 枚举值到 `RenderOptionsSpec` 对象的 `PDFAConformance` 数据成员。 例如，要指定一致性级别A，请指定 `PDFAConformance.A` 至此数据成员。
   * 设置 `PDFARevisionNumber` 值（通过分配） `PDFARevisionNumber` 枚举值到 `RenderOptionsSpec` 对象的 `PDFARevisionNumber` 数据成员。 分配 `PDFARevisionNumber.Revision_1` 至此数据成员。

   >[!NOTE]
   >
   >无论您指定哪个值，PDF/A文档的PDF版本均为1.4。

1. 生成PDF/文档。

   PDF通过调用 `OutputServiceService` 对象的 `generatePDFOutput`方法并传递以下值：

   * TransformationFormat枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDFA`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值。）
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用结果数据填充此对象。 （只有Web服务调用才需要此参数值。）
   * An `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值。）

   >[!NOTE]
   >
   >PDF您还可以通过调用 `OutputClient` 对象的 `generatePDFOutput`2方法。 (请参阅 [将位于Content Services（已弃用）中的文档传递到输出服务](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建一个字节数组，用于存储 `BLOB` 使用结果数据填充的对象 `OutputServiceService` 对象的 `generatePDFOutput` 方法（第八个参数）。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 字段。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将位于Content Services（已弃用）中的文档传递到输出服务 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Output服务呈现基于表单设计的非交互式PDF表单，该表单通常保存为XDP文件并在Designer中创建。 您可以传递 `com.adobe.idp.Document` 包含表单设计到Output服务的对象。 然后，Output服务将渲染位于 `com.adobe.idp.Document` 对象。

通过的优势 `com.adobe.idp.Document` 对象到Output服务，即其他AEM Forms服务操作返回 `com.adobe.idp.Document` 实例。 那就是，你可以 `com.adobe.idp.Document` 来自另一个服务操作的实例并呈现它。 例如，假设XDP文件存储在名为的内容服务（已弃用）节点中 `/Company Home/Form Designs`，如下图所示。

您可以通过编程方式从内容服务中检索Loan.xdp（已弃用），并将XDP文件传递给 `com.adobe.idp.Document` 对象。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-2}

要将从Content Services（已弃用）获得的文档传递到输出服务，请执行以下任务：

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从Content Services检索表单设计（已弃用）。
1. 呈现非交互式PDF表单。
1. 对数据流执行操作。

**包含项目文件**

将必要的文件包含到开发项目中。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流从内容服务中检索XDP文件（已弃用），因此请创建文档管理API对象。

**从Content Services检索表单设计（已弃用）**

使用Java或Web服务API从内容服务中检索XDP文件（已弃用）。 XDP文件将在 `com.adobe.idp.Document` 实例(或 `BLOB` 实例)。 然后，您可以传递 `com.adobe.idp.Document` Output服务的实例。

**呈现非交互式PDF表单**

要呈现非交互式表单，请传递 `com.adobe.idp.Document` 从Content Services（已弃用）返回到Output服务的实例。

>[!NOTE]
>
>两个名为的新方法 `generatePDFOutput2`和g `eneratePrintedOutput2`接受 `com.adobe.idp.Document` 包含表单设计的对象。 您也可以传递 `com.adobe.idp.Document`在将打印流发送到网络打印机时包含到Output服务的表单设计。

**对表单数据流执行操作**

您可以将非交互式表单另存为PDF文件。 该表单可在Adobe Reader或Acrobat中查看。

**另请参阅**

[使用Java API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用Web服务API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-java-api}

使用输出服务和内容服务（已弃用）API (Java)传递从内容服务（已弃用）检索的文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 创建输出和文档管理客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。
   * 创建 `DocumentManagementServiceClientImpl` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 从Content Services检索表单设计（已弃用）。

   调用 `DocumentManagementServiceClientImpl` 对象的 `retrieveContent` 方法并传递以下值：

   * 一个字符串值，它指定添加内容的存储。 默认存储为 `SpacesStore`. 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。

   此 `retrieveContent` 方法返回 `CRCResult` 包含XDP文件的对象。 检索 `com.adobe.idp.Document` 通过调用 `CRCResult` 对象的 `getDocument` 方法。

1. 呈现非交互式PDF表单。

   调用 `OutputClient` 对象的 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定其他资源（如图像）所在的内容根。
   * A `com.adobe.idp.Document` 表示表单设计的对象(使用返回的实例 `CRCResult` 对象的 `getDocument` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象。

   此 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 检索 `com.adobe.idp.Document` 通过调用 `OutputResult` 对象的 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getGeneratedDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速启动（EJB模式）：使用Java API将文档传递到Output Service](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速入门（SOAP模式）：使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-web-service-api}

使用输出服务和内容服务（已弃用）API（Web服务）传递从内容服务（已弃用）检索的文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 为与Output服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   对与Document Management服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   因为 `BLOB` 数据类型对两个服务引用都是通用的，完全限定 `BLOB` 数据类型。 在相应的Web服务快速启动中， `BLOB` 实例是完全限定的。

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出和文档管理客户端API对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >对重复这些步骤 `DocumentManagementServiceClient`服务客户端。

1. 从Content Services检索表单设计（已弃用）。

   通过调用 `DocumentManagementServiceClient` 对象的 `retrieveContent` 方法并传递以下值：

   * 一个字符串值，它指定添加内容的存储。 默认存储为 `SpacesStore`. 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   * 用于存储浏览链接值的字符串输出参数。
   * A `BLOB` 用于存储内容的输出参数。 您可以使用此输出参数检索内容。
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 用于存储内容属性的输出参数。
   * A `CRCResult` 输出参数。 除了使用此对象之外，您还可以使用 `BLOB` 用于检索内容的输出参数。

1. 呈现非交互式PDF表单。

   调用 `OutputServiceClient` 对象的 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定其他资源（如图像）所在的内容根。
   * A `BLOB` 表示表单设计的对象(使用 `BLOB` 由Content Services返回的实例（已弃用）。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * 输出 `BLOB` 由填充的对象 `generatePDFOutput2` 方法。 此 `generatePDFOutput2` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * 输出 `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值）。

   此 `generatePDFOutput2` 方法返回 `BLOB` 包含非交互式PDF表单的对象。

1. 对表单数据流执行操作。

   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 对象检索自 `generatePDFOutput2` 方法。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 将存储库中的文档传递到输出服务 {#passing-documents-located-in-the-repository-to-the-output-service}

Output服务呈现基于表单设计的非交互式PDF表单，该表单通常保存为XDP文件并在Designer中创建。 您可以传递 `com.adobe.idp.Document` 包含表单设计到Output服务的对象。 然后，Output服务将渲染位于 `com.adobe.idp.Document` 对象。

通过的优势 `com.adobe.idp.Document` 对象到Output服务，即其他AEM Forms服务操作返回 `com.adobe.idp.Document` 实例。 那就是，你可以 `com.adobe.idp.Document` 来自另一个服务操作的实例并呈现它。 例如，假设XDP文件存储在AEM Forms存储库中，如下图所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

此 *FormsFolder* 文件夹是AEM Forms存储库中用户定义的位置（此位置就是一个示例，默认情况下不存在）。 在此示例中，名为Loan.xdp的表单设计位于此文件夹中。 除了表单设计之外，还可以在此位置存储其他表单宣传资料，例如图像。 位于AEM Forms存储库中的资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以以编程方式从AEM Forms存储库检索Loan.xdp，并将其传递到中的输出服务 `com.adobe.idp.Document` 对象。

您可以使用两种方式之一，基于存储库中的XDP文件创建PDF。 您可以按引用传递XDP位置，也可以以编程方式从存储库检索XDP，并将其传递到XDP文件中的Output服务。

[快速入门（EJB模式）：使用Java API基于应用程序XDP文件创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （显示如何通过引用传递XDP文件的位置）。

[快速入门（EJB模式）：使用Java API将位于AEM Forms存储库中的文档传递到Output服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (演示了如何以编程方式从AEM Forms存储库检索XDP文件，并将其传递到中的输出服务 `com.adobe.idp.Document` 实例)。 （本节讨论如何执行此任务）

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-3}

要将从AEM Forms存储库获得的文档传递到输出服务，请执行以下任务：

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从AEM Forms存储库检索表单设计。
1. 呈现非交互式PDF表单。
1. 对数据流执行操作。

**包含项目文件**

将必要的文件包含到开发项目中。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流从内容服务中检索XDP文件（已弃用），因此请创建文档管理API对象。

**从AEM Forms存储库检索表单设计**

使用存储库API从AEM Forms存储库检索XDP文件。 (请参阅 [正在读取资源](/help/forms/developing/aem-forms-repository.md#reading-resources).)

XDP文件将在 `com.adobe.idp.Document` 实例(或 `BLOB` 实例)。 然后，您可以传递 `com.adobe.idp.Document` Output服务的实例。

**呈现非交互式PDF表单**

要呈现非交互式表单，请传递 `com.adobe.idp.Document` 使用AEM Forms存储库API返回的实例。

>[!NOTE]
>
>两个名为的新方法 `generatePDFOutput2`和 `generatePrintedOutput2`接受 `com.adobe.idp.Document`包含表单设计的对象。 您也可以传递 `com.adobe.idp.Document` 在将打印流发送到网络打印机时包含到Output服务的表单设计。

**对表单数据流执行操作**

您可以将非交互式表单另存为PDF文件。 该表单可在Adobe Reader或Acrobat中查看。

**另请参阅**

[使用Java API将存储库中的文档传递到输出服务](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API将存储库中的文档传递到输出服务 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用输出服务和存储库API (Java)传递从存储库检索到的文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar和adobe-repository-client.jar。

1. 创建输出和文档管理客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。
   * 创建 `DocumentManagementServiceClientImpl` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 从AEM Forms存储库检索表单设计。

   调用 `ResourceRepositoryClient` 对象的 `readResourceContent` 方法将指定URI位置的字符串值传递给XDP文件。 例如，`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。此值为必填项。 此方法会返回 `com.adobe.idp.Document` 表示XDP文件的实例。

1. 呈现非交互式PDF表单。

   调用 `OutputClient` 对象的 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定其他资源（如图像）所在的内容根。 例如：`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * A `com.adobe.idp.Document` 表示表单设计的对象(使用返回的实例 `ResourceRepositoryClient` 对象的 `readResourceContent` 方法)。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象。

   此 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 检索 `com.adobe.idp.Document` 通过调用 `OutputResult` 对象的 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getGeneratedDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API将位于AEM Forms存储库中的文档传递到Output服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段创建PDF文档 {#creating-pdf-documents-using-fragments}

您可以使用Output和Assembler服务创建基于片段的输出流，例如PDF文档。 Assembler服务基于位于多个XDP文件中的片段来组合XDP文档。 组装的XDP文档被传递到Output服务，该服务将创建一个PDF文档。 尽管此工作流显示正在生成的PDF文档，但“输出”服务可以为此工作流生成其他输出类型，如ZPL。 PDF文档仅用于讨论目的。

下图显示了此工作流。

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

阅读前 *使用片段创建PDF文档*，建议您熟悉使用Assembler服务来汇编多个XDP文档。 (请参阅 [组装多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>您还可以将由Assembler服务组装的表单设计传递到Forms服务，而不是输出服务。 Output服务和Forms服务的主要区别在于Forms服务生成交互式PDF文档，而Output服务生成非交互式PDF文档。 此外，Forms服务无法生成ZPL等基于打印机的输出流。

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-4}

要基于片段创建PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Output and Assembler客户端对象。
1. 使用Assembler服务生成表单设计。
1. 使用Output服务生成PDF文档。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建输出和汇编程序客户端对象**

在以编程方式执行输出服务API操作之前，请先创建输出客户端API对象。 此外，由于此工作流调用Assembler服务来创建表单设计，因此请创建Assembler客户端API对象。

**使用Assembler服务生成表单设计**

使用Assembler服务生成使用片段的表单设计。 Assembler服务返回 `com.adobe.idp.Document` 包含窗体设计的实例。

**使用Output服务生成PDF文档**

您可以使用Output服务使用Assembler服务创建的表单设计生成PDF文档。 传递 `com.adobe.idp.Document` Assembler服务返回到Output服务的实例。

**将PDF文档另存为PDF文件**

在Output服务生成PDF文档之后，可以将其另存为PDF文件。

**另请参阅**

[使用Java API基于片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服务API基于片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[组装多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API基于片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用输出服务API和汇编程序服务API (Java)基于片段创建PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。

1. 创建Output and Assembler客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 使用Assembler服务生成表单设计。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象。
   * A `java.util.Map` 包含输入XDP文件的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象。

   此 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含已装配XDP文档的对象。 要检索装配的XDP文档，请执行以下步骤：

   * 调用 `AssemblerResult` 对象的 `getDocuments` 方法。 此方法会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果为止 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 提取装配XDP文档的方法。

1. 使用Output服务生成PDF文档。

   调用 `OutputClient` 对象的 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`
   * 一个字符串值，它指定其他资源（如图像）所在的内容根
   * A `com.adobe.idp.Document` 表示表单设计的对象（使用Assembler服务返回的实例）
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象

   此 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象

1. 将PDF文档另存为PDF文件。

   * 检索 `com.adobe.idp.Document` PDF通过调用 `OutputResult` 对象的 `getGeneratedDoc` 方法。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件。 (确保您使用 `com.adobe.idp.Document` 对象 `getGeneratedDoc` 方法已返回。)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API基于片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速入门（SOAP模式）：使用Java API基于片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### 使用Web服务API基于片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用输出服务API和汇编程序服务API（Web服务），基于片段创建PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 为与Output服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   对与Assembler服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   因为 `BLOB` 数据类型对两个服务引用都是通用的，完全限定 `BLOB` 数据类型。 在相应的Web服务快速启动中， `BLOB` 实例是完全限定的。

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建Output and Assembler客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给 `OutputServiceClient.ClientCredentials.UserName.UserName`字段。
      * 将相应的密码值分配给 `OutputServiceClient.ClientCredentials.UserName.Password`字段。
      * 分配常量值 `HttpClientCredentialType.Basic` 到 `BasicHttpBindingSecurity.Transport.ClientCredentialType`字段。

   * 分配 `BasicHttpSecurityMode.TransportCredentialOnly` 的常量值 `BasicHttpBindingSecurity.Security.Mode`字段。

   >[!NOTE]
   >
   >对重复这些步骤 `AssemblerServiceClient`对象。

1. 使用Assembler服务生成表单设计。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含所需文件的对象
   * An `AssemblerOptionSpec` 指定运行时选项的对象

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和发生的任何异常的对象。 要获取新创建的XDP文档，请执行以下步骤：

   * 访问 `AssemblerResult` 对象的 `documents` 字段，即 `Map` 包含结果PDF文档的对象。
   * 循环访问 `Map` 对象以检索装配后的表单设计。 转换该数组成员的 `value` 到 `BLOB`. 传递此 `BLOB` Output服务的实例。

1. 使用Output服务生成PDF文档。

   调用 `OutputServiceClient` 对象的 `generatePDFOutput2` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定其他资源（如图像）所在的内容根。
   * A `BLOB` 表示表单设计的对象(使用 `BLOB` （由Assembler服务返回的实例）。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * 输出 `BLOB` 对象 `generatePDFOutput2` 方法将填充。 此 `generatePDFOutput2` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * 输出 `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值）。

   此 `generatePDFOutput2` 方法返回 `BLOB` 包含非交互式PDF表单的对象。

1. 将PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 对象检索自 `generatePDFOutput2` 方法。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到文件 {#printing-to-files}

您可以使用Output服务将流(如PostScript、打印机控制语言(PCL)或以下标签格式打印到文件：

* 斑马 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服务，您可以将XML数据与表单设计合并，并将表单打印到文件。 下图显示了Output服务创建激光和标签文件。

>[!NOTE]
>
>有关将打印流发送到打印机的信息，请参见 [将打印流发送到打印机](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-5}

要打印到文件，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置打印到文件所需的打印运行时选项。
1. 将打印流打印到文件。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。 (请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

要打印包含数据的文档，您必须为要填充数据的每个表单字段引用包含XML元素的XML数据源。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置打印到文件所需的打印运行时选项**

要打印到文件，必须通过指定Output服务打印到的文件的位置和名称来设置File URI运行时选项。 例如，要指示Output服务打印名为的PostScript文件 *MortgageForm.ps* 至C:\Adobe，请指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定义可选的运行时选项。 有关可设置的所有选项的信息，请参见 `PrintedOutputOptionsSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**将打印流打印到文件**

在引用包含表单数据的有效XML数据源并设置打印运行时选项后，可以调用Output服务，使其打印文件。

**检索操作的结果**

在Output服务执行操作之后，它会返回各种数据项，例如XML数据，这些数据项指定操作是否成功。

**另请参阅**

[使用Java API打印到文件](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服务API打印到文件](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API打印到文件 {#print-to-files-using-the-java-api}

使用输出API (Java)打印到文件：

1. 包括项目文件。

   将客户端JAR文件（如adobe-output-client.jar）包含在Java项目的类路径中。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 对象，表示用于填充文档的XML数据源，该数据源使用其构造函数，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置打印到文件所需的打印运行时选项。

   * 创建 `PrintedOutputOptionsSpec` 对象。
   * 通过调用PrintedOutputOptionsSpec对象的 `setFileURI` 方法，并传递一个表示文件名称和位置的字符串值。 例如，如果希望输出服务打印到位于C:\Adobe中的名为MortgageForm.ps的PostScript文件，请指定C:\\Adobe\MortgageForm.ps。
   * 通过调用 `PrintedOutputOptionsSpec` 对象的 `setCopies` 方法，并传递一个表示副本数的整数值。

1. 将打印流打印到文件。

   通过调用 `OutputClient` 对象的 `generatePrintedOutput` 方法并传递以下值：

   * A `PrintFormat` 指定要创建的打印流格式的枚举值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
   * 一个字符串值，它指定要使用的XDC文件的位置(您可以传递 `null` 如果您通过使用 `PrintedOutputOptionsSpec` 对象)。
   * 此 `PrintedOutputOptionsSpec` 包含打印到文件所需的运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含包含表单数据的XML数据源的对象。

   此 `generatePrintedOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >此 `OutputResult` 对象的 `getRecordLevelMetaDataList` 方法返回 `null`.

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示以下对象的状态： `generatePrintedOutput` 方法调用 `OutputResult` 对象的 `getStatusDoc` 方法( `OutputResult` 对象由 `generatePrintedOutput` 方法)。
   * 创建 `java.io.File` 将包含操作结果的对象。 确保文件扩展名为XML。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getStatusDoc` 方法)。

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
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储表单数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值指定包含表单数据的XML文件的位置。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `binaryData` 属性与字节数组的内容。

1. 设置打印到文件所需的打印运行时选项。

   * 创建 `PrintedOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来指定文件，该字符串值表示文件的位置和名称。 `PrintedOutputOptionsSpec` 对象的 `fileURI` 数据成员。 例如，如果希望输出服务打印到名为的PostScript文件 *MortgageForm.ps* 位于C:\Adobe中，请指定C:\\Adobe\MortgageForm.ps。
   * 指定打印的份数，方法是：指定一个整数值，该值表示打印的份数。 `PrintedOutputOptionsSpec` 对象的 `copies` 数据成员。

1. 将打印流打印到文件。

   通过调用 `OutputServiceService` 对象的 `generatePrintedOutput` 方法并传递以下值：

   * A `PrintFormat` 指定要创建的打印流格式的枚举值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
   * 一个字符串值，它指定要使用的XDC文件的位置(您可以传递 `null` 如果您通过使用 `PrintedOutputOptionsSpec` 对象)。
   * 此 `PrintedOutputOptionsSpec` 包含打印到文件所需的打印运行时选项的对象。
   * 此 `BLOB` 包含包含表单数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值。）
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用结果数据填充此对象。 （只有Web服务调用才需要此参数值。）
   * An `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值。）

1. 检索操作的结果。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示包含结果数据的XML文件位置。 确保文件扩展名为XML。
   * 创建一个字节数组，用于存储 `BLOB` 使用结果数据填充的对象 `OutputServiceService` 对象的 `generatePDFOutput` 方法（第八个参数）。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将打印流发送到打印机 {#sending-print-streams-to-printers}

可以使用Output服务将打印流(如PostScript、打印机控制语言(PCL)或以下标签格式)发送到网络打印机：

* 斑马 — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用Output服务，您可以将XML数据与表单设计合并，并将表单作为打印流输出。 例如，您可以创建PostScript打印流并将其发送到网络打印机。 下图显示了Output服务将打印流发送到网络打印机。

>[!NOTE]
>
>为了演示如何将打印流发送到网络打印机，本节使用SharedPrinter打印机协议将PostScript打印流发送到网络打印机。

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-6}

要将打印流发送到网络打印机，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 设置打印运行时选项
1. 检索要打印的文档。
1. 将文档发送到网络打印机。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

在以编程方式执行输出服务操作之前，请先创建输出服务客户端对象。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceClient` 对象。

**引用XML数据源**

要打印包含数据的文档，您必须为要填充数据的每个表单字段引用包含XML元素的XML数据源。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置打印运行时选项**

在向打印机发送打印流时，可以设置运行时选项，包括以下选项：

* **副本**：指定发送到打印机的副本数。 默认值为 1。
* **装订**：使用订书机时设置XCI选项。 此选项可通过装订元素在配置模型中指定，仅用于PS和PCL打印机。
* **OutputJog**：当输出页面需要角拐时（在输出托盘中实际移动），会设置XCI选项。 此选项仅适用于PS和PCL打印机。
* **输出纸盒**：用于使打印驱动程序选择相应输出纸盒的XCI值。

>[!NOTE]
>
>有关可设置的所有运行时选项的信息，请参见 `PrintedOutputOptionsSpec` 类引用。

**检索要打印的文档**

检索要发送到打印机的打印流。 例如，您可以检索PostScript文件并将其发送到打印机。

如果打印机支持PDF，则可以选择发送PDF文件。 但是，向打印机发送PDF文档的问题是每个打印机制造商对PDF解释器的实现方式不同。 也就是说，有些打印制造商使用Adobe PDF的解释，但具体取决于打印机。 其他打印机有自己的PDF解释器。 因此，打印结果可能会有所不同。

将PDF文档发送到打印机的另一个限制是它只能打印；它不能访问双面打印、纸盒选择和装订，除非通过打印机上的设置。

要检索要打印的文档，请使用 `generatePrintedOutput` 方法。 下表指定在使用时为给定打印流设置的内容类型 `generatePrintedOutput` 方法。

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
   <td><p>默认或自定义xdc输出流创建dpl203.xdc。</p></td>
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
   <td><p>GenericColorPCL </p></td>
   <td><p>创建通用颜色PCL (5c)输出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>创建通用PostScript 3级输出流。</p></td>
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
   <td><p>创建通用单色PCL (5e)输出流。</p></td>
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
>您还可以使用将打印流发送到打印机 `generatePrintedOutput2` 方法。 但是，与“向打印机发送打印流”部分相关的快速启动使用 `generatePrintedOutput` 方法。

**将打印流发送到网络打印机**

检索要打印的文档后，可以调用Output服务，使其向网络打印机发送打印流。 要使输出服务成功找到打印机，必须指定打印服务器和打印机名称。 此外，还必须指定打印协议。

>[!NOTE]
>
>如果PDFG安装在表单服务器上，并且服务器在Windows Server 2008上运行，则无法使用SharedPrinter属性。 在这种情况下，请使用不同的打印机协议。

>[!NOTE]
>
>如果您使用的是网络打印机，并且访问机制为SharedPrinter，则需要指定打印机的完整网络路径。使用Java API将打印流发送到网络打印机

使用输出API (Java)将打印流发送到网络打印机：

1. 包括项目文件。

   将客户端JAR文件（如adobe-output-client.jar）包含在Java项目的类路径中。

1. 创建输出客户端对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源

   * 创建 `java.io.FileInputStream` 对象，表示用于填充文档的XML数据源，该数据源使用其构造函数，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置打印运行时选项

   创建 `PrintedOutputOptionsSpec` 表示打印运行时选项的对象。 例如，您可以通过调用 `PrintedOutputOptionsSpec` 对象的 `setCopies` 方法。

   >[!NOTE]
   >
   >不能使用设置分页值 `PrintedOutputOptionsSpec` 对象的 `setPagination` 方法（如果要生成ZPL打印流）。 同样，不能为ZPL打印流设置下列选项： OutputJog、PageOffset和Staple。 此 `setPagination` 方法对于PostScript生成无效。 它仅对PCL生成有效。

1. 检索要打印的文档

   * 通过调用 `OutputClient` 对象的 `generatePrintedOutput` 方法并传递以下值：

      * A `PrintFormat` 指定打印流的枚举值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`.
      * 一个字符串值，它指定窗体设计的名称。
      * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
      * 一个字符串值，它指定要使用的XDC文件的位置。
      * 此 `PrintedOutputOptionsSpec` 包含打印到文件所需的运行时选项的对象。
      * 此 `com.adobe.idp.Document` 表示包含要与表单设计合并的表单数据的XML数据源的对象。

     此方法会返回 `OutputResult` 包含操作结果的对象。

   * 创建 `com.adobe.idp.Document` 对象通过调用 `OutputResult` 对象 `getGeneratedDoc` 方法。 此方法会返回 `com.adobe.idp.Document` 对象。

1. 将打印流发送到网络打印机

   通过调用 `OutputClient` 对象的 `sendToPrinter` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示要发送到打印机的打印流的对象。
   * A `PrinterProtocol` 指定要使用的打印机协议的枚举值。 例如，要指定SharedPrinter协议，请传递 `PrinterProtocol.SharedPrinter`.
   * 一个字符串值，它指定打印服务器的名称。 例如，假定打印服务器的名称为PrintSever1，请通过 `\\\PrintSever1`.
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1，请通过 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >此 `sendToPrinter` 方法已添加到8.2.1版的AEM Forms API中。

### 使用Web服务API将打印流发送到打印机 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用输出API（Web服务）将打印流发送到网络打印机：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储表单数据。
   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值指定包含表单数据的XML文件的位置。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 设置打印运行时选项。

   创建 `PrintedOutputOptionsSpec` 对象。 例如，您可以指定要打印的份数，方法为指定一个整数值，该值代表要打印的份数。 `PrintedOutputOptionsSpec` 对象的 `copies` 数据成员。

   >[!NOTE]
   >
   >不能使用设置分页值 `PrintedOutputOptionsSpec` 对象的 `pagination` 数据成员（如果要生成ZPL打印流）。 同样，不能为ZPL打印流设置以下选项：OutputJog、PageOffset和Staple。 此 `pagination` 数据成员对于PostScript生成无效。 它仅对PCL生成有效。

1. 检索要打印的文档。

   * 通过调用 `OutputServiceService` 对象的 `generatePrintedOutput` 方法并传递以下值：

      * A `PrintFormat` 指定打印流的枚举值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`.
      * 一个字符串值，它指定窗体设计的名称。
      * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
      * 一个字符串值，它指定要使用的XDC文件的位置。
      * 此 `PrintedOutputOptionsSpec` 包含向网络打印机发送打印流时使用的打印运行时选项的对象。
      * 此 `BLOB` 包含包含表单数据的XML数据源的对象。
      * A `BLOB` 由填充的对象 `generatePrintedOutput` 方法。 此 `generatePrintedOutput` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值。）
      * A `BLOB` 由填充的对象 `generatePrintedOutput` 方法。 此 `generatePrintedOutput` 方法使用结果数据填充此对象。 （只有Web服务调用才需要此参数值。）
      * An `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值。）

   * 创建 `BLOB` 对象通过获取以下对象的值发送到打印机： `OutputResult` 对象 `generatedDoc` 方法。 此方法会返回 `BLOB` 包含由返回的PostScript数据的对象 `generatePrintedOutput` 方法。

1. 将打印流发送到网络打印机。

   通过调用 `OutputClient` 对象的 `sendToPrinter` 方法并传递以下值：

   * A `BLOB` 表示要发送到打印机的打印流的对象。
   * A `PrinterProtocol` 指定要使用的打印机协议的枚举值。 例如，要指定SharedPrinter协议，请传递 `PrinterProtocol.SharedPrinter`.
   * A `bool` 指定是否使用上一个参数值的值。 传递值 `true`. （只有Web服务调用才需要此参数值。）
   * 一个字符串值，它指定打印服务器的名称。 例如，假定打印服务器的名称为PrintSever1，请通过 `\\\PrintSever1`.
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1，请通过 `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >此 `sendToPrinter` 方法已添加到8.2.1版的AEM Forms API中。

## 创建多个输出文件 {#creating-multiple-output-files}

Output服务可以为XML数据源内的每个记录创建单独的文档，也可以为包含所有记录的单个文件创建单独的文档（此功能是默认设置）。 例如，假设有10条记录位于XML数据源中，并且您指示输出服务使用输出服务API为每个记录创建单独的PDF文档（或其他类型的输出）。 因此，Output服务会生成十份PDF文档。 （您可以向打印机发送多个打印流，而不是创建文档。）

下图还显示了处理包含多个记录的XML数据文件的Output服务。 但是，假定您指示Output服务创建包含所有数据记录的单个PDF文档。 在这种情况下，Output服务会生成一个包含所有记录的文档。

下图显示了处理包含多个记录的XML数据文件的Output服务。 假设您指示Output服务为每个数据记录创建一个单独的PDF文档。 在这种情况下，Output服务将为每个数据记录生成单独的PDF文档。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

以下XML数据显示了包含三个数据记录的数据文件的示例。

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

请注意，每个数据记录的开始和结束的XML元素为 `LoanRecord`. 此XML元素由生成多个文件的应用程序逻辑引用。

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

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

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceService` 对象。

**引用XML数据源**

引用包含多个记录的XML数据源。 必须使用XML元素来分隔数据记录。 例如，在本节前面显示的示例XML数据源中，用于分隔数据记录的XML元素名为 `LoanRecord`.

要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必匹配XML元素的显示顺序。

**设置PDF运行时选项**

您必须为输出服务设置以下运行时选项，才能基于XML数据源成功创建多个文件：

* **许多文件**：指定Output服务是创建单个文档还是多个文档。 您可以指定true或false。 要为XML数据源中的每个数据记录创建单独的文档，请指定true。
* **文件URI**：指定Output服务生成的文件的位置。 例如，假设您指定了C:\\Adobe\forms\Loan.pdf。 在这种情况下，Output服务会创建一个名为Loan.pdf的文件，并将该文件放在C:\\Adobe\forms文件夹中。 当有多个文件时，其文件名为Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果指定文件位置，则文件将放置在服务器上，而不是客户端计算机上。
* **记录名称**：指定数据源中用于分隔数据记录的XML元素名称。 例如，在本节前面显示的示例XML数据源中，将调用用于分隔数据记录的XML元素 `LoanRecord`. (您可以设置记录级别，而不是设置记录名称运行时选项，方法是为其指定一个数字值，该值表示包含数据记录的元素级别。 但是，您只能设置“记录名称”或“记录级别”。 不能同时设置这两个值。)

**设置渲染运行时选项**

您可以在创建多个文件时设置渲染运行时选项。 虽然这些选项不是必需的（与所需的输出运行时选项不同），但您可以执行诸如提高输出服务性能的任务。 例如，您可以缓存Output服务使用的表单设计以提高性能。

当Output服务处理批处理记录时，它会以增量方式读取包含多个记录的数据。 也就是说，Output服务将数据读取到内存中，并在处理记录批次时释放数据。 在设置了两个运行时选项之一时，输出服务会以增量方式加载数据。 如果设置记录名运行时选项，则输出服务将以增量方式读取数据。 同样，如果将“记录级别”运行时选项设置为2或更大，输出服务将以增量方式读取数据。

您可以使用来控制输出服务是否执行增量加载 `PDFOutputOptionsSpec` 或 `PrintedOutputOptionSpec` 对象的 `setLazyLoading` 方法。 您可以传递值 `false` 更改为此方法以关闭增量加载。

**生成多个PDF文件**

在引用包含多个数据记录的有效XML数据源并设置运行时选项后，可以调用Output服务，这会使其生成多个文件。 生成多个记录时， `OutputResult` 对象的 `getGeneratedDoc` 方法返回 `null`.

**检索操作的结果**

Output服务执行操作后，会返回用于指定操作是否成功的XML数据。 Output服务返回以下XML。 在这种情况下，Output服务产生了42份文件。

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

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建多个PDF文件 {#create-multiple-pdf-files-using-the-java-api}

使用输出API (Java)创建多个PDF文件：

1. 包括项目文件”

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。.

1. 创建输出客户端对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源

   * 创建 `java.io.FileInputStream` 对象表示XML数据源，该数据源包含多个记录，方法是使用其构造函数并传递一个指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setGenerateManyFiles` 方法。 例如，传递值 `true` 指示Output服务为XML数据源中的每个记录创建单独的PDF文件。 (如果通过 `false`，则输出服务会生成包含所有记录的单个PDF文档)。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setFileUri` 方法，并传递一个字符串值，该值指定输出服务生成的文件位置。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。
   * 通过调用 `OutputOptionsSpec` 对象的 `setRecordName` 方法并传递一个字符串值，该值指定用于分隔数据记录的数据源中的XML元素名称。 (例如，请考虑本节前面显示的XML数据源。 用于分隔数据记录的XML元素的名称为LoanRecord)。

1. 设置渲染运行时选项

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计以通过调用 `RenderOptionsSpec` 对象的 `setCacheEnabled` 并传递 `Boolean` 值 `true`.

1. 生成多个PDF文件

   PDF通过调用 `OutputClient` 对象的 `generatePDFOutput` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含要与表单设计合并的数据的XML数据源的对象。

   此 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作的结果

   * 创建 `java.io.File` 表示将包含结果的XML文件 `generatePDFOutput` 方法。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `applyUsageRights` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API创建多个PDF文件](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建多个PDF文件 {#create-multiple-pdf-files-using-the-web-service-api}

使用输出API（Web服务）创建多个PDF文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含多个记录的表单数据。
   * 创建 `System.IO.FileStream` 对象通过调用其构造函数。 传递一个字符串值，该值表示包含多个记录的XML文件的文件位置。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过为指定布尔值来设置“多个文件”选项 `OutputOptionsSpec` 对象的 `generateManyFiles` 数据成员。 例如，分配值 `true` 指示输出服务为XML数据源中的每个记录创建单独的PDF文件。 (如果您指定 `false` 之后，Output服务将生成包含所有记录的单个PDF)。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成文件的位置。 `OutputOptionsSpec` 对象的 `fileURI` 数据成员。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。
   * 通过指定一个字符串值来设置记录名称选项，该字符串值指定数据源中的XML元素名称，该数据源将数据记录分隔到 `OutputOptionsSpec` 对象的 `recordName` 数据成员。
   * 通过指定一个整数值来设置copies选项，该值指定输出服务生成到的副本数 `OutputOptionsSpec` 对象的 `copies` 数据成员。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计以通过分配值提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象的 `cacheEnabled` 数据成员。

1. 生成多个PDF文件。

   PDF通过调用 `OutputServiceService` 对象的 `generatePDFOutput`方法并传递以下值：

   * TransformationFormat枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用生成的描述文档的元数据填充此对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用结果数据填充此对象。
   * An `OutputResult` 包含操作结果的对象。

1. 检索操作的结果

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示包含结果数据的XML文件位置。 确保文件扩展名为.xml。
   * 创建一个字节数组，用于存储 `BLOB` 使用结果数据填充的对象 `OutputServiceService` 对象的 `generatePDFOutput` 方法（第八个参数）。 通过获取的值，填充字节数组 `BLOB` 对象的 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建搜索规则 {#creating-search-rules}

您可以创建搜索规则，以导致Output服务检查输入数据并根据数据内容使用不同的表单设计来生成输出。 例如，如果文本 *抵押* 位于输入数据内，则Output服务可使用名为Mortgage.xdp的表单设计。 同样，如果文本 *汽车* 位于输入数据中，则Output服务可以使用保存为AutomobileLoan.xdp的表单设计。 尽管Output服务可以生成不同的输出类型，但本节假定Output服务生成一个PDF文件。 下图显示了通过处理XML数据文件并使用多种表单设计之一来生成PDF文件的Output服务。

此外，输出服务能够生成文档包，其中在数据集中提供了多个记录，并且每个记录与表单设计匹配，并且单个文档由多个表单设计组成。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-8}

要指示Output服务在生成文档时使用搜索规则，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 引用XML数据源。
1. 定义搜索规则。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF文档。
1. 检索操作的结果。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在受支持的J2EE应用程序服务器（不是JBoss）上，则需要使用特定于部署AEM Forms的J2EE应用程序服务器的JAR文件替换adobe-utilities.jar和jbossall-client.jar。

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。

**引用XML数据源**

要使用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 只要指定了所有XML元素，就不必匹配XML元素的显示顺序。

**定义搜索规则**

要定义搜索规则，您可以定义Output服务在输入数据中搜索的一个或多个文本模式。 对于您定义的每个文本模式，指定在找到文本模式时所使用的相应表单设计。 如果找到文本模式，则Output服务将使用相应的表单设计来生成输出。 文本模式的示例为 *抵押*.

>[!NOTE]
>
>如果找不到文本模式，则使用默认表单。 确保您使用的所有表单设计都位于内容根中。

**设置PDF运行时选项**

设置以下PDF运行时选项，以便Output服务基于多个表单设计成功创建PDF文档：

* **文件URI**：指定输出服务生成的PDF文件的名称和位置。
* **规则**：指定您定义的规则。
* **LookAhead**：指定从输入数据文件的开头起用于扫描所定义的文本模式的字节数。 缺省值为500字节。

**设置渲染运行时选项**

可以在创建PDF文件时设置渲染运行时选项。 虽然这些选项不是必需的(与PDF运行时选项不同)，但您可以执行诸如提高Output服务性能之类的任务。 例如，您可以缓存Output服务使用的表单设计以提高性能。

**生成PDF文档**

在引用有效的XML数据源并设置运行时选项后，可以调用Output服务，从而生成PDF文档。 如果Output服务在输入数据中找到指定的文本模式，则它使用相应的表单设计。 如果未使用文本模式，则Output服务将使用默认表单设计。

**检索操作的结果**

Output服务执行操作后，会返回用于指定操作是否成功的XML数据。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建搜索规则 {#create-search-rules-using-the-java-api}

使用输出API (Java)创建搜索规则：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用XML数据源。

   * 创建 `java.io.FileInputStream` 对象，表示用于填充PDF文档的XML数据源，该数据源使用其构造函数，并传递指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 定义搜索规则。

   * 创建 `Rule` 对象。
   * 通过调用 `Rule` 对象的 `setPattern` 方法，并传递指定文本模式的字符串值。
   * 通过调用 `Rule` 对象的 `setForm` 方法。 传递一个指定窗体设计名称的字符串值。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 创建 `java.util.List` 对象 `java.util.ArrayList` 构造函数。
   * 对于每个 `Rule` 创建的对象，调用 `java.util.List` 对象的 `add` 方法并传递 `Rule` 对象。

1. 设置PDF运行时选项。

   * 创建 `PDFOutputOptionsSpec` 对象。
   * PDF指定输出服务通过调用 `PDFOutputOptionsSpec` 对象的 `setFileURI` 方法。 传递一个指定PDF文件位置的字符串值。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setRules` 方法。 传递 `java.util.List` 包含 `Rule` 对象。
   * 通过调用 `PDFOutputOptionsSpec` 对象的 `setLookAhead` 方法。 传递一个表示字节数的整数值。

1. 设置渲染运行时选项。

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计，以便通过调用 `RenderOptionsSpec` 对象的 `setCacheEnabled` 和传递 `true`.

1. 生成PDF文档。

   PDF通过调用 `OutputClient` 对象的 `generatePDFOutput` 方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定默认表单设计的名称。 也就是说，在找不到文本图案时所使用的窗体设计。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `com.adobe.idp.Document` 包含Output服务为定义的文本模式搜索的表单数据的对象。

   此 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作的结果。

   * 创建 `com.adobe.idp.Document` 表示以下对象的状态： `generatePDFOutput` 方法调用 `OutputResult` 对象的 `getStatusDoc` 方法。
   * 创建 `java.io.File` 将包含操作结果的对象。 确保文件扩展名为.xml。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制 `com.adobe.idp.Document` 对象到文件(确保您使用 `com.adobe.idp.Document` 返回的对象 `getStatusDoc` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速入门（SOAP模式）：使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建搜索规则 {#create-search-rules-using-the-web-service-api}

使用输出API（Web服务）创建搜索规则：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用XML数据源。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储将与PDF文档合并的数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 定义搜索规则。

   * 创建 `Rule` 对象。
   * 通过指定字符串值来定义文本模式，该字符串值指定文本模式 `Rule` 对象的 `pattern` 数据成员。
   * 通过指定一个字符串值来定义相应的窗体设计，该值指定窗体设计给 `Rule` 对象的 `form` 数据成员。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 创建 `MyArrayOf_xsd_anyType` 存储规则的对象。
   * 分配每个 `Rule` 对象到的元素 `MyArrayOf_xsd_anyType` 数组。 调用 `MyArrayOf_xsd_anyType` 对象的 `Add` 方法（每种） `Rule` 对象。

1. 设置PDF运行时选项

   * 创建 `PDFOutputOptionsSpec` 对象。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成的PDF文件的位置。 `PDFOutputOptionsSpec` 对象的 `fileURI` 数据成员。 文件URI选项相对于托管AEM Forms的J2EE应用程序服务器，而不是客户端计算机。
   * 通过指定一个整数值来设置copies选项，该值指定输出服务生成到的副本数 `PDFOutputOptionsSpec` 对象的 `copies` 数据成员。
   * 通过分配 `MyArrayOf_xsd_anyType` 将规则存储到的对象 `PDFOutputOptionsSpec` 对象的 `rules` 数据成员。
   * 通过指定整数值来设置所定义的文本模式要扫描的字节数，整数值表示要扫描的字节数。 `PDFOutputOptionsSpec` 对象的 `lookAhead` 数据方法。

1. 设置渲染运行时选项

   * 创建 `RenderOptionsSpec` 对象。
   * 缓存表单设计，以便通过分配值来提高输出服务的性能 `true` 到 `RenderOptionsSpec` 对象的 `cacheEnabled` 数据成员。

   >[!NOTE]
   >
   >不能使用设置PDF文档的版本 `RenderOptionsSpec` 对象的 `pdfVersion` 成员(如果输入文档是Acrobat表单)。 输出PDF文档保留Acrobat表单的PDF版本。 PDF同样，不能通过使用 `RenderOptionsSpec` 对象的 `taggedPDF` 方法(如果输入文档是Acrobat表单)。

   >[!NOTE]
   >
   >不能使用设置线性PDF选项 `RenderOptionsSpec` 对象的 `linearizedPDF` 成员，如果输入的PDF文档经过认证或数字签名。 有关信息，请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. 生成PDF文档

   PDF通过调用 `OutputServiceService` 对象的 `generatePDFOutput`方法并传递以下值：

   * A `TransformationFormat` 枚举值。 要生成PDF单据，请指定 `TransformationFormat.PDF`.
   * 一个字符串值，它指定窗体设计的名称。
   * 一个字符串值，它指定表单设计所在的内容根。
   * A `PDFOutputOptionsSpec` 包含PDF运行时选项的对象。
   * A `RenderOptionsSpec` 包含渲染运行时选项的对象。
   * 此 `BLOB` 包含要与表单设计合并的数据的XML数据源的对象。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用生成的描述文档的元数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * A `BLOB` 由填充的对象 `generatePDFOutput` 方法。 此 `generatePDFOutput` 方法使用结果数据填充此对象。 （只有Web服务调用才需要此参数值）。
   * An `OutputResult` 包含操作结果的对象。 （只有Web服务调用才需要此参数值）。

   >[!NOTE]
   >
   >当通过调用PDF文档时 `generatePDFOutput` 方法，请注意，您无法将数据与已签名、已验证或包含使用权限的XFAPDF表单合并。 有关使用权限的信息，请参阅 [将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. 检索操作的结果

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示包含结果数据的XML文件位置。 确保文件扩展名为XML。
   * 创建一个字节数组，用于存储 `BLOB` 使用结果数据填充的对象 `OutputServiceService` 对象的 `generatePDFOutput` 方法（第八个参数）。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 拼合PDF文档 {#flattening-pdf-documents}

可以使用Output服务将交互式PDF文档转换为非交互式PDF。 交互式PDF文档允许用户输入或修改PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为 *平面化*. 当PDF文档被拼合时，用户无法修改文档字段中的数据。 拼合PDF文档的一个原因是确保无法修改数据。

您可以拼合以下类型的PDF文档：

* 交互式XFAPDF文档
* Acrobat Forms

尝试拼合非交互式PDFPDF会导致异常。

>[!NOTE]
>
>有关Output服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-9}

要将交互式PDF文档拼合为非交互式PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建输出客户端对象。
1. 检索交互式PDF文档。
1. 转换PDF文档。
1. 将非交互式PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果正在使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果将AEM Forms部署在受支持的J2EE应用程序服务器而不是JBoss上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于已部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建输出客户端对象**

必须先创建输出服务客户端对象，然后才能以编程方式执行输出服务操作。 如果您使用的是Java API，请创建 `OutputClient` 对象。 如果您使用Output Web service API，请创建 `OutputServiceService` 对象。

**检索交互式PDF文档**

检索要转换为非交互式PDF文档的交互式PDF文档。 尝试转换非交互式PDF文档会导致异常。

**转换PDF文档**

检索交互式PDF文档后，可将其转换为非交互式PDF文档。 Output服务返回非交互式PDF文档。

**将非交互式PDF文档另存为PDF文件**

可以将非交互式PDF文档另存为PDF文件。

**另请参阅**

[使用Java API拼合PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服务API拼合PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速启动](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API拼合PDF文档 {#flatten-a-pdf-document-using-the-java-api}

使用输出API (Java)将交互式PDF文档拼合为非交互式PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-output-client.jar。

1. 创建输出客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `OutputClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 检索交互式PDF文档。

   * 创建 `java.io.FileInputStream` 表示要转换的交互式PDF文档的对象，该文档使用其构造函数，并传递一个指定交互式PDF文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 转换PDF文档。

   通过调用，将交互式PDF文档转换为非交互式PDF文档 `OutputServiceService` 对象的 `transformPDF` 方法并传递以下值：

   * 此 `com.adobe.idp.Document` 包含交互式PDF文档的对象。
   * A `TransformationFormat` 枚举值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修订号的enum值。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * 表示修订编号和年份的字符串值，用冒号分隔。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * A `PDFAConformance` 表示PDF/A合规性级别的枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `null`.

   此 `transformPDF` 方法返回 `com.adobe.idp.Document` 包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `Document` 对象的 `copyToFile` 用于复制 `Document` 对象到文件(确保您使用 `Document` 返回的对象 `transformPDF` 方法)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速入门（EJB模式）：使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速入门（SOAP模式）：使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API拼合PDF文档 {#flatten-a-pdf-document-using-the-web-service-api}

使用输出API（Web服务）将交互式PDF文档拼合为非交互式PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建输出客户端对象。

   * 创建 `OutputServiceClient` 对象使用默认构造函数。
   * 创建 `OutputServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/OutputService?blob=mtom`.) 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。 但是，请指定 `?blob=mtom` 使用MTOM。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `OutputServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `OutputServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索交互式PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储交互式PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示交互式PDF文档的文件位置。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 属性与字节数组的内容。

1. 转换PDF文档。

   通过调用，将交互式PDF文档转换为非交互式PDF文档 `OutputClient` 对象的 `transformPDF` 方法并传递以下值：

   * A `BLOB` 包含交互式PDF文档的对象。
   * A `TransformationFormat` 枚举值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` 指定修订号的enum值。
   * 一个布尔值，它指定 `PDFARevisionNumber` 使用枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `false`.
   * 表示修订编号和年份的字符串值，用冒号分隔。 由于此参数适用于PDF/文档，因此您可以指定 `null`.
   * A `PDFAConformance` 表示PDF/A合规性级别的枚举值。
   * 布尔值，指定 `PDFAConformance` 使用枚举值。 由于此参数适用于PDF/文档，因此您可以指定 `false`.

   此 `transformPDF` 方法返回 `BLOB` 包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该值表示非交互式PDF文档的文件位置。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `transformPDF` 方法。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
