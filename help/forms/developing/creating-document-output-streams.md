---
title: 创建文档输出流
seo-title: 创建文档输出流
description: 'null'
seo-description: 'null'
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '18972'
ht-degree: 0%

---


# 创建文档输出流  {#creating-document-output-streams}

**关于输出服务**

输出服务允许您将文档输出为PDF(包括PDF/A文档)、PostScript、打印机控制语言(PCL)和以下标签格式：

* 泽布拉- ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用“输出”服务，您可以将XML表单数据与表单设计合并，并将文档输出到网络打印机或文件。

有两种方法可将表单设计（XDP文件）传递到输出服务。 您可以将包含表 `com.adobe.idp.Document` 单设计的实例传递给输出服务。 或者，您可以传递指定表单设计位置的URI值。 在使用AEM表单进行编程 *时，将讨论这两种方式*。

>[!NOTE]
>
>输出服务不支持包含应用程序对象特定脚本的Acroform PDF文档。 不渲染包含应用程序对象特定脚本的Acroform PDF文档。

以下各节介绍如何使用URI值将表单设计传递给输出服务：

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)

以下部分说明如何在实例中传递表单 `com.adobe.idp.Document` 设计：

* [将位于Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

决定使用哪种技术时的一个考虑因素是，如果您从其他AEM Forms服务获取表单设计，然后在实例中传 `com.adobe.idp.Document` 递它。 将文档 *传递到输出服务* , *以及使用片段创建PDF文档* ，都显示如何从其他AEM Forms服务获取表单设计。 第一部分从Content Services检索表单设计（已弃用）。 第二部分从Assembler服务检索表单设计。

如果从固定位置（如文件系统）获取表单设计，则可以使用两种方法。 即，可以为XDP文件指定URI值或使用实 `com.adobe.idp.Document` 例。

要传递指定创建PDF文档时表单设计位置的URI值，请使用该方 `generatePDFOutput` 法。 同样，要在创 `com.adobe.idp.Document` 建PDF文档时将实例传递到输出服务，请使用该 `generatePDFOutput2` 方法。

向网络打印机发送输出流时，您还可以使用这两种技术。 要通过传递包含表单设计的实例将输 `com.adobe.idp.Document` 出流发送到打印机，请使用 `sendToPrinter2`该方法。 要通过传递URI值将输出流发送到打印机，请使用该 `sendToPrinter`方法。 “将 *打印流发送到打印机* ”部分使用 `sendToPrinter` 该方法。

您可以使用输出服务完成这些任务:

* [创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)
* [创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)
* [将位于Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [打印到文件](creating-document-output-streams.md#printing-to-files)
* [向打印机发送打印流](creating-document-output-streams.md#sending-print-streams-to-printers)
* [创建多个输出文件](creating-document-output-streams.md#creating-multiple-output-files)
* [创建搜索规则](creating-document-output-streams.md#creating-search-rules)
* [拼合PDF文档](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

## 创建PDF文档 {#creating-pdf-documents}

您可以使用“输出”服务创建基于您提供的表单设计和XML表单文档的PDF。 由输出服务创建的PDF文档不是交互式PDF文档; 用户无法输入或修改表单数据。

如果要创建用于长期存储的PDF文档，建议您创建PDF/A文档。 (请参 [阅创建PDF/A文档](creating-document-output-streams.md#creating-pdf-a-documents)。)

要创建允许用户输入数据的交互式PDF表单，请使用Forms服务。 (请参阅 [渲染交互式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)。)

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要创建PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF文档。
1. 检索操作结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 您计划用数据填充的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必与XML元素的显示顺序匹配。

请考虑以下贷款申请表示例。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

要将数据合并到此表单设计中，必须创建与表单对应的XML数据源。 以下XML表示与示例按揭贷款应用程序表单对应的XDP XML数据源。

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

创建PDF文档时设置文件URI选项。 此选项指定输出服务生成的PDF文件的名称和位置。

>[!NOTE]
>
>您可以从Output服务返回的复杂数据类型以编程方式检索PDF文档，而不是设置文件URI运行时选项。 但是，通过设置文件URI运行时选项，您无需创建以编程方式检索PDF文档的应用程序逻辑。

**设置渲染运行时选项**

您可以在创建PDF文档时设置渲染运行时选项。 尽管这些选项不是必需的（与所需的PDF运行时选项不同），但您可以执行任务，如提高输出服务的性能。 例如，您可以缓存输出服务使用的表单设计以提高其性能。

如果使用标记的Acrobat表单作为输入，则无法使用输出服务Java或Web服务API关闭标记设置。 如果尝试以编程方式将此选项设 `false`置为，则结果PDF文档仍会被标记。

>[!NOTE]
>
>如果不指定渲染运行时选项，则使用默认值。 有关渲染运行时选项的信息，请参 `RenderOptionsSpec` 阅类参考。 (请参 [阅AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**生成PDF文档**

引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用输出服务，这会导致生成PDF文档。

在生成PDF文档时，您指定输出服务创建PDF文档所需的URI值。 表单设计可以存储在诸如服务器文件系统之类的位置，或者作为AEM Forms应用程序的一部分。 作为Forms应用程序的一部分存在的表单设计（或其他资源，如图像文件）可以使用内容根URI值进行引用 `repository:///`。 例如，请考虑位于名为Applications/FormsApplication *的Forms应用程序* 中的以下名 *为Loan.xdp的表单设计*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

要访问上图所示的Loan.xdp文件，请指 `repository:///Applications/FormsApplication/1.0/FormsFolder/` 定为传递给对象方法的 `OutputClient` 第三个参 `generatePDFOutput` 数。 指定表单名称(*Loan.xdp*)作为传递给对象方 `OutputClient` 法的第二个参 `generatePDFOutput` 数。

如果XDP文件包含图像（或其他资源，如片段），请将资源放在与XDP文件相同的应用程序文件夹中。 AEM Forms使用内容根URI作为基本路径来解析对图像的引用。 例如，如果Loan.xdp文件包含图像，请确保将图像放入 `Applications/FormsApplication/1.0/FormsFolder/`。

>[!NOTE]
>
>在调用对象或方法时，可以引 `OutputClient` 用Forms应用程 `generatePDFOutput` 序 `generatePrintedOutput` URI。

>[!NOTE]
>
>要查看通过引用位于Forms应用程序中的XDP创建PDF开始的完整快速文档，请参 [阅快速开始（EJB模式）: 使用Java API创建基于应用程序XDP文件的PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)。

**检索操作结果**

输出服务执行操作后，它会返回各种数据项，如指定操作是否成功的状态XML数据。

**另请参阅**

[使用Java API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[使用Web服务API创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF文档 {#create-a-pdf-document-using-the-java-api}

使用输出API(Java)创建PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output Client对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源。

   * 创建一 `java.io.FileInputStream` 个对象，它表示用于填充PDF文档的XML数据源，方法是使用其构造函数并传递一个指定XML文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数创建对象。 传递对 `java.io.FileInputStream` 象。

1. 设置PDF运行时选项。

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象的方法来设 `PDFOutputOptionsSpec` 置文件URI `setFileURI` 选项。 传递一个字符串值，它指定输出服务生成的PDF文件的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象并传递来缓存表单设计，以 `RenderOptionsSpec` 提高输出服 `setCacheEnabled` 务的性 `true`能。

   >[!NOTE]
   >
   >如果输入文档是Acrobat表单(在Acrobat中创建的表 `RenderOptionsSpec` 单)或已签名或认证的XFA文档，则 `setPdfVersion` 不能使用对象的方法设置PDF文档的版本。 输出PDF文档保留原始PDF版本。 同样，如果输入文档是Acrobat表单或已签名或已认证的XFA文档, `RenderOptionsSpec` 则无 `setTaggedPDF` 法通过调用对象的方法来设置加标签的Adobe PDF选项。

   >[!NOTE]
   >
   >如果输入的PDF文档经过认证或数字签名， `RenderOptionsSpec` 则不能 `setLinearizedPDF` 使用对象的方法设置线性化的PDF选项。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 生成PDF文档。

   通过调用对象的方法并 `OutputClient` 传递以 `generatePDFOutput` 下值，创建PDF文档:

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   该 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >通过调用方法生成PDF文档 `generatePDFOutput` 时，请注意，您不能将数据与已签名或已验证的XFA PDF表单合并。 (请参 [阅数字签名和认证文档](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。)*

   >[!NOTE]
   >
   >返 `OutputResult` 回对象的 `getRecordLevelMetaDataList` 方法 `null`*。*

   >[!NOTE]
   >
   >还可以通过调用对象的方法 `OutputClient` 创建PDF `generatePDFOutput2` 文档。 (请参 [阅将Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 检索操作结果。

   * 通过调 `com.adobe.idp.Document` 用对象的方法检索表示 `generatePDFOutput` 操作状态 `OutputResult` 的对 `getStatusDoc` 象。 此方法返回指定操作是否成功的状态XML数据。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为。xml。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getStatusDoc` 对象)。

   尽管“输出”服务将PDF文档写入由传递给对象方法的参 `PDFOutputOptionsSpec` 数指定的 `setFileURI` 位置，但您可以通过调用对象的方法以编程方式检索 `OutputResult` PDF/A `getGeneratedDoc` 文档。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[快速开始（SOAP模式）: 使用Java API创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建PDF文档 {#create-a-pdf-document-using-the-web-service-api}

使用输出API（Web服务）创建PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储将与PDF文档合并的XML数据。
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示包含表单数据的XML文件的文件位置。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 设置PDF运行时选项

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过指定一个字符串值来设置“文件URI”选项，该字符串值指定输出服务生成的PDF文件到对 `PDFOutputOptionsSpec` 象数据成员 `fileURI` 的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 将表单设计缓存，通过将值分配给对象的数据成员 `true` 来提 `RenderOptionsSpec` 高输出服务 `cacheEnabled` 的性能。

   >[!NOTE]
   >
   >如果输入文档是Acrobat表单(在Acrobat中创建的表 `RenderOptionsSpec` 单)或已签名或认证的XFA文档，则 `setPdfVersion` 不能使用对象的方法设置PDF文档的版本。 输出PDF文档保留原始PDF版本。 同样，如果输入文档是Acrobat表单或已签名或已认证的XFA文档, `RenderOptionsSpec` 则不能通过调用对 `setTaggedPDF`象的*方法来设置加标签的Adobe PDF选项。*

   >[!NOTE]
   >
   >如果输入的PDF文档经过认证或数字签名， `RenderOptionsSpec` 则不能通 `linearizedPDF` 过使用对象的成员来设置线性化的PDF选项。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*。)*

1. 生成PDF文档。

   通过调用对象的方法并 `OutputServiceService` 传递以 `generatePDFOutput`下值，创建PDF文档:

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 该方 `generatePDFOutput` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 方法 `generatePDFOutput` 使用结果数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 包 `OutputResult` 含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   >[!NOTE]
   >
   >通过调用方法生成PDF文档 `generatePDFOutput` 时，请注意，您不能将数据与已签名或已验证的XFA PDF表单合并。 (请参 [阅数字签名和认证文档](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。)*

   >[!NOTE]
   >
   >还可以通过调用对象的方法 `OutputClient` 创建PDF `generatePDFOutput2` 文档。 (请参 [阅将Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*。)*

1. 检索操作结果。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示包含结果数据的XML文件位置的字符串值来创建对象。 确保文件扩展名为。xml。
   * 创建一个字节数组，它存储由对象 `BLOB` 的方法（第八个参数）填充 `OutputServiceService` 的结果数 `generatePDFOutput` 据的对象的数据内容。 通过获取对象的值来填 `BLOB` 充字节数 `MTOM``field`组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入XML文件。

   另请参阅

   [步骤摘要](creating-document-output-streams.md#summary-of-steps)

   [使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >已 `OutputServiceService` 弃用对象 `generateOutput` 的方法。

## 创建PDF/A文档 {#creating-pdf-a-documents}

您可以使用输出服务创建PDF/A文档。 由于PDF/A是用于长期保留文档内容的存档格式，所有字体都是嵌入的，文件是未压缩的。 因此，PDF/A文档通常大于标准PDF文档。 此外，PDF/A文档不包含音频和视频内容。 与其他输出服务任务一样，您提供表单设计和数据以与表单设计合并，以创建PDF/A文档。

PDF/A-1规范包含两个符合性级别，即a和b。 二者的主要区别在于逻辑结构（辅助功能）支持，而符合性级别b不要求此支持。 无论符合性级别如何，PDF/A-1都规定所有字体都嵌入到生成的PDF/A文档中。

尽管PDF/A是归档PDF文档的标准，但如果标准PDF文档符合您的公司的需求，则不必将PDF/A用于归档。 PDF/A标准旨在建立一个可长期存储并满足文档保留要求的PDF文件。 例如，URL无法嵌入到PDF/A中，因为随着时间的推移，该URL可能会变为无效。

您的组织必须评估自己的需求、您希望保留文档的时间长短、文件大小的考虑因素，并确定您自己的归档战略。 您可以使用DocConverter服务以编程方式确定PDF文档是否符合PDF/A规范。 (请参 [阅以编程方式确定PDF/A兼容](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)。)

PDF/A文档必须使用在表单设计中指定的字体，且无法替换字体。 因此，如果位于PDF文档中的字体在主机操作系统(OS)上不可用，则会出现异常。

在Acrobat中打开PDF/A文档时，会显示一条消息，确认该文档是PDF/A文档，如下图所示。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM网站有一个PDF/A常见问题解答部分，您可以从https://www.aiim.org/documents/standards/19005-1_FAQ.pdf访 [问它](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要创建PDF/A文档，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 设置PDF/A运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF/A文档。
1. 检索操作结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建自定义应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceService` 对象。

**引用XML数据源**

要将数据与表单设计合并，必须引用包含数据的XML数据源。 要填充数据的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必与XML元素的显示顺序匹配。

**设置PDF/A运行时选项**

可在创建PDF/A文档时设置“文件URI”选项。 URI是相对于承载AEM Forms的J2EE应用程序服务器的。 即，如果设置C:\Adobe，则文件将写入服务器上的文件夹，而不是客户端计算机。 URI指定输出服务生成的PDF/A文件的名称和位置。

**设置渲染运行时选项**

您可以在创建PDF/A文档时设置渲染运行时选项。 您可以设置的两个PDF/A相关选项是 `PDFAConformance` 和 `PDFARevisionNumber` 值。 该 `PDFAConformance` 值指PDF文档如何遵守指定如何保留长期电子文档的要求。 此选项的有效值是 `A` 和 `B`。 有关a级和b级符合性的信息，请参阅标题为ISO 19005-1文档管 *理的PDF/A-1 ISO规范*。

该 `PDFARevisionNumber` 值指PDF/A文档的修订版号。 有关PDF/A文档的修订版号的信息，请参阅标题为ISO 19005-1文档管理的 *PDF/A-1 ISO规范*。

>[!NOTE]
>
>创建PDF/A 1A文档时， `false` 无法将加标签的Adobe PDF选项设置为。 PDF/A 1A将始终是加标签的PDF文档。 此外，在创建PDF/A 1B文档时，您 `true` 无法将加标签的Adobe PDF选项设置为。 PDF/A 1B将始终是未加标签的PDF文档。

**生成PDF/A文档**

引用包含表单数据的有效XML数据源并设置运行时选项后，可以调用输出服务，使其生成PDF/A文档。

**检索操作结果**

输出服务执行操作后，它会返回各种数据项，如指定操作是否成功的XML数据。

**另请参阅**

[使用Java API创建PDF/A文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[使用Web服务API创建PDF/A文档](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建PDF/A文档 {#create-a-pdf-a-document-using-the-java-api}

使用Output API(Java)创建PDF/A文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output Client对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源。

   * 创建一 `java.io.FileInputStream` 个对象，它表示用于填充PDF/A文档的XML数据源，方法是使用其构造函数并传递一个指定XML文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置PDF/A运行时选项。

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象的方法来设 `PDFOutputOptionsSpec` 置文件URI `setFileURI` 选项。 传递一个字符串值，它指定输出服务生成的PDF文件的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 通过调 `PDFAConformance` 用对象的方 `RenderOptionsSpec` 法并传递指定符 `setPDFAConformance` 合性级别的枚 `PDFAConformance` 举值来设置该值。 例如，要指定符合性级别A，请通过 `PDFAConformance.A`。
   * 通过调 `PDFARevisionNumber` 用对象的方 `RenderOptionsSpec` 法并传递 `setPDFARevisionNumber` 来设置值 `PDFARevisionNumber.Revision_1`。

   >[!NOTE]
   >
   >PDF/A文档的PDF版本是1.4，无论您为对象的方法指 `RenderOptionsSpec` 定什么 `setPdfVersion`*值。*

1. 生成PDF/A文档。

   通过调用对象的方法并传递 `OutputClient` 以下值 `generatePDFOutput` ，创建PDF/A文档:

   * 明细列表 `TransformationFormat` 值。 要生成PDF/A文档，请指定 `TransformationFormat.PDFA`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   该 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >返 `OutputResult` 回对象的 `getRecordLevelMetaDataList` 方法 `null`。

   >[!NOTE]
   >
   >您还可以通过调用对象的2方法 `OutputClient` 创建PDF/A `generatePDFOutput`文档。 (请参 [阅将Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 检索操作结果。

   * 通过 `com.adobe.idp.Document` 调用对象的方法，创 `generatePDFOutput` 建一个表示方 `OutputResult` 法状态的对 `getStatusDoc` 象。
   * 创建 `java.io.File` 一个将包含操作结果的对象。 确保文件扩展名为。xml。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getStatusDoc` 对象)。

   >[!NOTE]
   >
   >尽管“输出”服务将PDF/A文档写入由传递给对象方法的参 `PDFOutputOptionsSpec` 数指定的 `setFileURI` 位置，但您可以通过调用对象的方法以编程方式 `OutputResult` 检索PDF/A `getGeneratedDoc` 文档。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（SOAP模式）: 使用Java API创建PDF/A文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服务API创建PDF/A文档 {#create-a-pdf-a-document-using-the-web-service-api}

使用输出API（Web服务）创建PDF/A文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储将与PDF/A文档合并的数据。
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象字段指定字 `MTOM` 节数组内容来填充对象。

1. 设置PDF/A运行时选项。

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过指定一个字符串值来设置“文件URI”选项，该字符串值指定输出服务生成的PDF文件到对 `PDFOutputOptionsSpec` 象数据成员 `fileURI` 的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 通过 `PDFAConformance` 为对象的数据 `PDFAConformance` 成员分配枚举 `RenderOptionsSpec` 值来设置 `PDFAConformance` 该值。 例如，要指定符合性级别A，请为 `PDFAConformance.A` 此数据成员分配。
   * 通过 `PDFARevisionNumber` 为对象的数据 `PDFARevisionNumber` 成员分配枚举 `RenderOptionsSpec` 值来设置 `PDFARevisionNumber` 该值。 分配 `PDFARevisionNumber.Revision_1` 给此数据成员。

   >[!NOTE]
   >
   >PDF/A文档的PDF版本是1.4，无论您指定哪个值。

1. 生成PDF/A文档。

   通过调用对象的方法并 `OutputServiceService` 传递以 `generatePDFOutput`下值，创建PDF文档:

   * TransformationFormat明细列表值。 要生成PDF文档，请指定 `TransformationFormat.PDFA`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 该方 `generatePDFOutput` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅用于Web服务调用。）
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 方法 `generatePDFOutput` 使用结果数据填充此对象。 （此参数值仅用于Web服务调用。）
   * 包 `OutputResult` 含操作结果的对象。 （此参数值仅用于Web服务调用。）

   >[!NOTE]
   >
   >您还可以通过调用对象的2方法 `OutputClient` 创建PDF/A `generatePDFOutput`文档。 (请参 [阅将Content Services中的文档（已弃用）传递到Output Service](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)。)

1. 检索操作结果。

   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示包含结果数据的XML文件位置。 确保文件扩展名为。xml。
   * 创建一个字节数组，它存储由对象 `BLOB` 的方法（第八个参数）填充 `OutputServiceService` 的结果数 `generatePDFOutput` 据的对象的数据内容。 通过获取对象字段的值 `BLOB` 填充字节数 `MTOM` 组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入XML文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 将位于Content Services中的文档（已弃用）传递到Output Service {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

输出服务渲染非交互式PDF表单，该表单基于表单设计，通常另存为XDP文件并在设计器中创建。 可以将包含表 `com.adobe.idp.Document` 单设计的对象传递到输出服务。 然后，输出服务将呈现位于对象中的表单 `com.adobe.idp.Document` 设计。

将对象传递到输 `com.adobe.idp.Document` 出服务的一个优点是其他AEM Forms服务操作返回一个 `com.adobe.idp.Document` 实例。 也就是说，您可以从其他服 `com.adobe.idp.Document` 务操作获取实例并渲染它。 例如，假定XDP文件存储在名为的Content Services（已弃用）节 `/Company Home/Form Designs`点中，如下图所示。

您可以从Content Services（已弃用）以编程方式检索Loan.xdp，并将XDP文件传递到对象中的Output服 `com.adobe.idp.Document` 务。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要将从Content Services获取的文档（已弃用）传递到Output服务，请执行以下任务:

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从Content Services检索表单设计（已弃用）。
1. 渲染非交互式PDF表单。
1. 对数据流执行操作。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建一个输出客户端API对象。 此外，由于此工作流从Content Services检索XDP文件（已弃用），因此请创建一个文档管理API对象。

**从Content Services检索表单设计（已弃用）**

使用Java或Web服务API从Content Services检索XDP文件（已弃用）。 XDP文件在实例(或 `com.adobe.idp.Document` 在使用Web `BLOB` 服务时的实例)中返回。 然后，可以将该实 `com.adobe.idp.Document` 例传递给输出服务。

**渲染非交互式PDF表单**

要呈现非交互式表单，请将从 `com.adobe.idp.Document` Content Services返回的实例（已弃用）传递给Output服务。

>[!NOTE]
>
>名为和g的两 `generatePDFOutput2`种新 `eneratePrintedOutput2`方法接 `com.adobe.idp.Document` 受包含表单设计的对象。 在向网络打印机 `com.adobe.idp.Document`发送打印流时，还可以将包含表单设计的文件传递给输出服务。

**对表单数据流执行操作**

可以将非交互式表单另存为PDF文件。 表单可在Adobe Reader或Acrobat中查看。

**另请参阅**

[使用Java API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[使用Web服务API将文档传递到输出服务](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[使用片段创建PDF文档](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### 使用Java API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-java-api}

通过使用Output服务和Content Services（已弃用）API(Java)传递从Content Services（已弃用）检索的文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar和adobe-contentservices-client.jar。

1. 创建输出和文档管理客户端API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `DocumentManagementServiceClientImpl` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 从Content Services检索表单设计（已弃用）。

   调用对 `DocumentManagementServiceClientImpl` 象的方 `retrieveContent` 法并传递以下值：

   * 一个字符串值，它指定添加内容的存储。 默认存储为 `SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。

   该 `retrieveContent` 方法返回 `CRCResult` 包含XDP文件的对象。 通过调 `com.adobe.idp.Document` 用对象的方 `CRCResult` 法检索实 `getDocument` 例。

1. 渲染非交互式PDF表单。

   调用对 `OutputClient` 象的方 `generatePDFOutput2` 法并传递以下值：

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 一个字符串值，它指定图像等其他资源所在的内容根目录。
   * 表 `com.adobe.idp.Document` 示表单设计的对象(使用对象方法返 `CRCResult` 回的实 `getDocument` 例)。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   该 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 通过 `com.adobe.idp.Document` 调用对象的方法检索表示非交互式 `OutputResult` 表单的对 `getGeneratedDoc` 象。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为。pdf。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getGeneratedDoc` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[快速开始（SOAP模式）: 使用Java API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将文档传递到输出服务 {#pass-documents-to-the-output-service-using-the-web-service-api}

通过使用输出服务和内容服务（已弃用）API（Web服务）传递从Content Services检索的文档（已弃用）:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此创建两个服务引用。 对与输出服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   对与文档管理服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   由于数 `BLOB` 据类型是两种服务引用的通用类型，因此在使用数据 `BLOB` 类型时完全限定数据类型。 在相应的Web服务快速开始中，所 `BLOB` 有实例都完全限定。

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建输出和文档管理客户端API对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。)
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >为服务客户端重 `DocumentManagementServiceClient`复这些步骤。

1. 从Content Services检索表单设计（已弃用）。

   通过调用对象的方 `DocumentManagementServiceClient` 法并传递 `retrieveContent` 以下值来检索内容：

   * 一个字符串值，它指定添加内容的存储。 默认存储为 `SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如 `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   * 存储浏览链接值的字符串输出参数。
   * 存储 `BLOB` 内容的输出参数。 您可以使用此输出参数检索内容。
   * 存储 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 内容属性的输出参数。
   * 输 `CRCResult` 出参数。 您可以使用输出参数来检索内 `BLOB` 容，而不是使用此对象。

1. 渲染非交互式PDF表单。

   调用对 `OutputServiceClient` 象的方 `generatePDFOutput2` 法并传递以下值：

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 一个字符串值，它指定图像等其他资源所在的内容根目录。
   * 表 `BLOB` 示表单设计的对象(使用Content Services `BLOB` 返回的实例（已弃用）)。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 由方 `BLOB` 法填充的输出对 `generatePDFOutput2` 象。 该方 `generatePDFOutput2` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 包含 `OutputResult` 操作结果的输出对象。 （此参数值仅对于Web服务调用是必需的）。

   该 `generatePDFOutput2` 方法返回 `BLOB` 一个包含非交互式PDF表单的对象。

1. 对表单数据流执行操作。

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储从方法检 `BLOB` 索到的对象的 `generatePDFOutput2` 内容。 通过获取对象数据成员的 `BLOB` 值填充字 `MTOM` 节数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 将存储库中的文档传递到输出服务 {#passing-documents-located-in-the-repository-to-the-output-service}

输出服务渲染非交互式PDF表单，该表单基于表单设计，通常另存为XDP文件并在设计器中创建。 可以将包含表 `com.adobe.idp.Document` 单设计的对象传递到输出服务。 然后，输出服务将呈现位于对象中的表单 `com.adobe.idp.Document` 设计。

将对象传递到输 `com.adobe.idp.Document` 出服务的一个优点是其他AEM Forms服务操作返回一个 `com.adobe.idp.Document` 实例。 也就是说，您可以从其他服 `com.adobe.idp.Document` 务操作获取实例并渲染它。 例如，假定XDP文件存储在AEM Forms存储库中，如下图所示。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

FormsFolder *文件夹* 是AEM Forms存储库中的用户定义位置（此位置是一个示例，默认情况下不存在）。 在此示例中，名为Loan.xdp的表单设计位于此文件夹中。 除了表单设计之外，还可以在此位置存储其他表单附属品，如图像。 位于AEM Forms存储库中的资源的路径为：

`Applications/Application-name/Application-version/Folder.../Filename`

您可以从AEM Forms库以编程方式检索Loan.xdp，并将它传递到对象中的“输出” `com.adobe.idp.Document` 服务。

您可以使用两种方法之一，根据存储库中的XDP文件创建PDF。 可以通过引用传递XDP位置，也可以通过编程方式从存储库中检索XDP，并将其传递给XDP文件中的Output服务。

[快速开始（EJB模式）: 使用Java API创建基于应用程序XDP文件的PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （显示如何通过引用传递XDP文件的位置）。

[快速开始（EJB模式）: 使用Java API将位于文档库中的AEM Forms传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (显示如何以编程方式从AEM Forms库检索XDP文件，并将其传递到实例中的输出 `com.adobe.idp.Document` 服务)。 (本节讨论如何执行此任务)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要将从文档库获取的AEM Forms传递到输出服务，请执行以下任务:

1. 包括项目文件。
1. 创建输出和文档管理客户端API对象。
1. 从AEM Forms库检索表单设计。
1. 渲染非交互式PDF表单。
1. 对数据流执行操作。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建输出和文档管理客户端API对象**

在以编程方式执行输出服务API操作之前，请先创建一个输出客户端API对象。 此外，由于此工作流从Content Services检索XDP文件（已弃用），因此请创建一个文档管理API对象。

**从AEM Forms库检索表单设计**

使用存储库API从AEM Forms存储库检索XDP文件。 (请参阅 [阅读资源](/help/forms/developing/aem-forms-repository.md#reading-resources)。)

XDP文件在实例(或 `com.adobe.idp.Document` 在使用Web `BLOB` 服务时的实例)中返回。 然后，可以将该实 `com.adobe.idp.Document` 例传递给Output服务。

**渲染非交互式PDF表单**

要呈现非交互式表单，请传 `com.adobe.idp.Document` 递使用AEM Forms库API返回的实例。

>[!NOTE]
>
>命名并接受包 `generatePDFOutput2`含 `generatePrintedOutput2`表单 `com.adobe.idp.Document`设计的对象的两种新方法。 向网络打印机 `com.adobe.idp.Document` 发送打印流时，还可以将包含表单设计的表单传递给输出服务。

**对表单数据流执行操作**

可以将非交互式表单另存为PDF文件。 表单可在Adobe Reader或Acrobat中查看。

**另请参阅**

[使用Java API将存储库中的文档传递给输出服务](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### 使用Java API将存储库中的文档传递给输出服务 {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

使用输出服务和存储库API(Java)传递从存储库检索的文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar和adobe-repository-client.jar。

1. 创建输出和文档管理客户端API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `DocumentManagementServiceClientImpl` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 从AEM Forms库检索表单设计。

   调用对 `ResourceRepositoryClient` 象的方 `readResourceContent` 法，并将指定URI位置的字符串值传递给XDP文件。 For example, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. 此值为必填值。 此方法返回 `com.adobe.idp.Document` 一个表示XDP文件的实例。

1. 渲染非交互式PDF表单。

   调用对 `OutputClient` 象的方 `generatePDFOutput2` 法并传递以下值：

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 一个字符串值，它指定图像等其他资源所在的内容根目录。 For example, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * 表 `com.adobe.idp.Document` 示表单设计的对象(使用对象方法返 `ResourceRepositoryClient` 回的实 `readResourceContent` 例)。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   该 `generatePDFOutput2` 方法返回 `OutputResult` 包含操作结果的对象。

1. 对表单数据流执行操作。

   * 通过 `com.adobe.idp.Document` 调用对象的方法检索表示非交互式 `OutputResult` 表单的对 `getGeneratedDoc` 象。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为。pdf。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getGeneratedDoc` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API将位于AEM Forms库中的文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用片段创建PDF文档 {#creating-pdf-documents-using-fragments}

您可以使用“输出”和“汇编器”服务创建基于片段的输出流，如PDF文档。 Assembler服务将基于位于多个XDP文件中的片段组装XDP文档。 装配好的XDP文档会传递到“输出”服务，该服务将创建PDF文档。 尽管此工作流显示正在生成的PDF文档，但输出服务可以为此工作流生成其他输出类型，如ZPL。 PDF文档仅用于讨论目的。

下图显示了此工作流。

![cp_cp_outputsemblefragments](assets/cp_cp_outputassemblefragments.png)

在阅读 *使用片段创建PDF文档之前*，建议您熟悉使用Assembler服务组合多个XDP文档。 (请参 [阅组合多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)。)

>[!NOTE]
>
>还可以将由Assembler服务组合的表单设计传递给Forms服务而不是Output服务。 输出服务和表单服务的主要区别在于，表单服务生成交互式PDF文档，而输出服务生成非交互式PDF文档。 此外，Forms服务无法生成基于打印机的输出流，如ZPL。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要创建基于片段的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output和Assembler客户端对象。
1. 使用Assembler服务生成表单设计。
1. 使用“输出”服务生成PDF文档。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建输出和汇编器客户端对象**

在以编程方式执行输出服务API操作之前，请先创建一个输出客户端API对象。 此外，由于此工作流调用Assembler服务来创建表单设计，因此请创建一个Assembler客户端API对象。

**使用Assembler服务生成表单设计**

使用Assembler服务生成使用片段的表单设计。 Assembler服务返回包 `com.adobe.idp.Document` 含表单设计的实例。

**使用输出服务生成PDF文档**

您可以使用Assembler服务创建的表单设计来使用Output服务生成PDF文档。 将Assembler `com.adobe.idp.Document` 服务返回的实例传递给Output服务。

**将PDF文档另存为PDF文件**

输出服务生成PDF文档后，可将其另存为PDF文件。

**另请参阅**

[使用Java API根据片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[使用Web服务API根据片段创建PDF文档](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[组合多个XDP片段](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[创建PDF文档](creating-document-output-streams.md#creating-pdf-documents)

### 使用Java API根据片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

使用Output Service API和Assembler Service API(Java)根据片段创建PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output和Assembler客户端对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 使用Assembler服务生成表单设计。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象。
   * 包 `java.util.Map` 含输入XDP文件的对象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象。

   该方 `invokeDDX` 法返回包 `com.adobe.livecycle.assembler.client.AssemblerResult` 含已装配的XDP文档的对象。 要检索已装配的XDP文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此方法返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取已装配的XDP文档。


1. 使用“输出”服务生成PDF文档。

   调用对 `OutputClient` 象的方 `generatePDFOutput2` 法并传递以下值：

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`
   * 一个字符串值，它指定附加资源（如图像）所在的内容根
   * 表 `com.adobe.idp.Document` 示表单设计的对象（使用由Assembler服务返回的实例）
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据

   方 `generatePDFOutput2` 法返回 `OutputResult` 包含操作结果的对象

1. 将PDF文档另存为PDF文件。

   * 通过 `com.adobe.idp.Document` 调用对象的方法检索表示PDF文档 `OutputResult` 的对 `getGeneratedDoc` 象。
   * 创建 `java.io.File` 包含操作结果的对象。 确保文件扩展名为。pdf。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容 `com.adobe.idp.Document` 复制到文件。 (确保使用方 `com.adobe.idp.Document` 法返回 `getGeneratedDoc` 的对象。)

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API根据片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[快速开始（SOAP模式）: 使用Java API根据片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服务API根据片段创建PDF文档 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

使用Output Service API和Assembler Service API（Web服务）根据片段创建PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 对与输出服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   对与Assembler服务关联的服务引用使用以下WSDL定义：

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   由于数 `BLOB` 据类型是两种服务引用的通用类型，因此在使用数据 `BLOB` 类型时完全限定数据类型。 在相应的Web服务快速开始中，所 `BLOB` 有实例都完全限定。

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output和Assembler客户端对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给 `OutputServiceClient.ClientCredentials.UserName.UserName`字段。
      * 为字段分配相应的密 `OutputServiceClient.ClientCredentials.UserName.Password`码值。
      * 为字段指 `HttpClientCredentialType.Basic` 定常 `BasicHttpBindingSecurity.Transport.ClientCredentialType`值。
   * 为字段 `BasicHttpSecurityMode.TransportCredentialOnly` 指定常 `BasicHttpBindingSecurity.Security.Mode`数值。

   >[!NOTE]
   >
   >为对象重复这些 `AssemblerServiceClient`步骤。

1. 使用Assembler服务生成表单设计。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含所需文件的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   方 `invokeDDX` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果和发生的任何异常。 要获取新创建的XDP文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 生成的PDF文档的对象。
   * 对对象进 `Map` 行迭代以检索组合的表单设计。 将该阵列成员 `value` 转换为 `BLOB`。 将此实 `BLOB` 例传递给Output服务。


1. 使用“输出”服务生成PDF文档。

   调用对 `OutputServiceClient` 象的方 `generatePDFOutput2` 法并传递以下值：

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 一个字符串值，它指定附加资源（如图像）所在的内容根。
   * 表 `BLOB` 示表单设计的对象(使用 `BLOB` 由Assembler服务返回的实例)。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 方法 `BLOB` 填充的输 `generatePDFOutput2` 出对象。 该方 `generatePDFOutput2` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 包含 `OutputResult` 操作结果的输出对象。 （此参数值仅对于Web服务调用是必需的）。

   该 `generatePDFOutput2` 方法返回 `BLOB` 一个包含非交互式PDF表单的对象。

1. 将PDF文档另存为PDF文件。

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储从方法检 `BLOB` 索到的对象的 `generatePDFOutput2` 内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 打印到文件 {#printing-to-files}

可以使用“输出”服务将PostScript、打印机控制语言(PCL)等流或以下标签格式打印到文件：

* 泽布拉- ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用“输出”服务，您可以将XML数据与表单设计合并，并将表单打印到文件。 下图显示了创建激光和标签文件的输出服务。

>[!NOTE]
>
>有关向打印机发送打印流的信息，请参 [阅向打印机发送打印流](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要打印到文件，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 设置打印到文件所需的打印运行时选项。
1. 将打印流打印到文件。
1. 检索操作结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 (请参 [阅包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。)

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceService` 对象。

**引用XML数据源**

要打印包含数据的文档，必须引用一个XML数据源，该数据源包含要用数据填充的每个表单字段的XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必与XML元素的显示顺序匹配。

**设置打印到文件所需的打印运行时选项**

要打印到文件，必须通过指定输出服务要打印到的文件的位置和名称来设置“文件URI运行时”选项。 例如，要指示输出服务将名为MortgageForm.ps的PostScript文 *件打印到* C:\Adobe，请指定C:\Adobe\MortgageForm.ps。

>[!NOTE]
>
>您可以定义可选的运行时选项。 有关可设置的所有选项的信息，请参阅 `PrintedOutputOptionsSpec` AEM FormsAPI参 [考中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**将打印流打印到文件**

引用包含表单数据的有效XML数据源并设置打印运行时选项后，可以调用输出服务，这会导致其打印文件。

**检索操作结果**

在输出服务执行操作后，它返回各种数据项，如XML数据，这些数据项指定操作是否成功。

**另请参阅**

[使用Java API打印到文件](creating-document-output-streams.md#print-to-files-using-the-java-api)

[使用Web服务API打印到文件](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API打印到文件 {#print-to-files-using-the-java-api}

使用输出API(Java)打印到文件：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output Client对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源。

   * 创建一 `java.io.FileInputStream` 个对象，它表示用于使用文档的构造函数并传递一个指定XML文件位置的字符串值来填充该数据的XML数据源。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置打印到文件所需的打印运行时选项。

   * 使用对 `PrintedOutputOptionsSpec` 象的构造函数创建对象。
   * 通过调用PrintedOutputOptionsSpec对象的方法并传 `setFileURI` 递一个字符串值来指定文件，该字符串值表示文件的名称和位置。 例如，如果希望输出服务打印到位于C:\Adobe的名为MortgageForm.ps的PostScript文件，请指定C:\\Adobe\MortgageForm.ps。
   * 通过调用对象的方法并传递一个表示 `PrintedOutputOptionsSpec` 副本数 `setCopies` 的整数值，指定要打印的副本数。

1. 将打印流打印到文件。

   通过调用对象的方法并 `OutputClient` 传递以 `generatePrintedOutput` 下值，打印到文件：

   * 一个 `PrintFormat` 明细列表值，它指定要创建的打印流格式。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
   * 一个字符串值，它指定要使用的XDC文件的位置(如果 `null` 指定了要使用的XDC文件，则可以通过使用对 `PrintedOutputOptionsSpec` 象传递)。
   * 包含 `PrintedOutputOptionsSpec` 打印到文件所需的运行时选项的对象。
   * 包含 `com.adobe.idp.Document` 包含表单数据的XML数据源的对象。

   该 `generatePrintedOutput` 方法返回 `OutputResult` 包含操作结果的对象。

   >[!NOTE]
   >
   >返 `OutputResult` 回对象的 `getRecordLevelMetaDataList` 方法 `null`。

1. 检索操作结果。

   * 通过 `com.adobe.idp.Document` 调用对象的方法(该方 `generatePrintedOutput` 法返回了该对象)，创 `OutputResult` 建一个表示该方 `getStatusDoc` 法状态的 `OutputResult` 对象(该对 `generatePrintedOutput` 象由该方法返回)。
   * 创建 `java.io.File` 一个将包含操作结果的对象。 确保文件扩展名为XML。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getStatusDoc` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（SOAP模式）: 使用Java API打印到文件](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### 使用Web服务API打印到文件 {#print-to-files-using-the-web-service-api}

使用Output API（Web服务）打印到文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 对象 `BLOB` 用于存储表单数据。
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值指定包含表单数据的XML文件的位置。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象属性 `binaryData` 赋予字节数组的内容来填充对象。

1. 设置打印到文件所需的打印运行时选项。

   * 使用对 `PrintedOutputOptionsSpec` 象的构造函数创建对象。
   * 通过为对象的数据成员指定表示文件位置和名称的字符串值 `PrintedOutputOptionsSpec` 来指定 `fileURI` 文件。 例如，如果希望输出服务打印到位于C:\Adobe的名为 *MortgageForm.ps的PostScript文* 件，请指定C:\\Adobe\MortgageForm.ps。
   * 通过为对象的数据成员分配一个整数值来指定要打印的份 `PrintedOutputOptionsSpec` 数，该整 `copies` 数值表示份数。

1. 将打印流打印到文件。

   通过调用对象的方法并 `OutputServiceService` 传递以 `generatePrintedOutput` 下值，打印到文件：

   * 一个 `PrintFormat` 明细列表值，它指定要创建的打印流格式。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
   * 一个字符串值，它指定要使用的XDC文件的位置(如果 `null` 指定了要使用的XDC文件，则可以通过使用对 `PrintedOutputOptionsSpec` 象传递)。
   * 包 `PrintedOutputOptionsSpec` 含打印到文件所需的打印运行时选项的对象。
   * 包 `BLOB` 含表单数据的XML数据源的对象。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 该方 `generatePDFOutput` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅用于Web服务调用。）
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 方法 `generatePDFOutput` 使用结果数据填充此对象。 （此参数值仅用于Web服务调用。）
   * 包 `OutputResult` 含操作结果的对象。 （此参数值仅用于Web服务调用。）

1. 检索操作结果。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示包含结果数据的XML文件位置的字符串值来创建对象。 确保文件扩展名为XML。
   * 创建一个字节数组，它存储由对象 `BLOB` 的方法（第八个参数）填充 `OutputServiceService` 的结果数 `generatePDFOutput` 据的对象的数据内容。 通过获取对象数据成员的 `BLOB` 值填充字 `MTOM` 节数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入XML文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 向打印机发送打印流 {#sending-print-streams-to-printers}

您可以使用“输出”服务将打印流(如PostScript、打印机控制语言(PCL))或以下标签格式发送到网络打印机：

* 泽布拉- ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

使用“输出”服务，您可以将XML数据与表单设计合并，并将表单输出为打印流。 例如，可以创建PostScript打印流并将其发送到网络打印机。 下图显示了将打印流发送到网络打印机的输出服务。

>[!NOTE]
>
>为了演示如何将打印流发送到网络打印机，本节将使用SharedPrinter打印机协议将PostScript打印流发送到网络打印机。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要向网络打印机发送打印流，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 设置打印运行时选项
1. 检索要打印的文档。
1. 将文档发送到网络打印机。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，请先创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceClient` 对象。

**引用XML数据源**

要打印包含数据的文档，必须引用一个XML数据源，该数据源包含要用数据填充的每个表单字段的XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必与XML元素的显示顺序匹配。

**设置打印运行时选项**

向打印机发送打印流时，可以设置运行时选项，包括以下选项：

* **副本**: 指定要发送到打印机的份数。 默认值为 1。
* **订书**: 使用订书机时设置XCI选项。 此选项可在配置模型中由Staple元素指定，并且仅用于PS和PCL打印机。
* **OutputJog**: 当输出页应合页时（在输出托盘中实际移动），将设置XCI选项。 此选项仅适用于PS和PCL打印机。
* **OutputBin**: 用于使打印驱动程序能够选择相应输出箱的XCI值。

>[!NOTE]
>
>有关可设置的所有运行时选项的信息，请参阅 `PrintedOutputOptionsSpec` 类引用。

**检索要打印的文档**

检索要发送到打印机的打印流。 例如，可以检索PostScript文件并将其发送到打印机。

如果您的打印机支持PDF，则可以选择发送PDF文件。 但是，向打印机发送PDF文档的问题是每个打印机制造商都有不同的PDF解释器实现。 即，一些印刷厂商使用Adobe PDF解释，但这取决于打印机。 其他打印机有自己的PDF解释器。 因此，打印结果可能会有所不同。

将PDF文档发送到打印机的另一个限制是它只能打印； 除非通过打印机设置，否则无法访问双工、纸盒选择和装订。

要检索要打印的文档，请使用 `generatePrintedOutput` 方法。 下表指定了在使用方法时为给定打印流设置的内容 `generatePrintedOutput` 类型。

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
   <td><p>默认情况下创建dpl203.xdc或自定义xdc输出流。</p></td>
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
   <td><p>创建通用颜色PCL(5c)输出流。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>创建通用PostScript Level 3输出流。</p></td>
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
   <td><p>创建通用PostScript Level 2输出流。</p></td>
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
>您还可以使用此方法将打印流发送到打 `generatePrintedOutput2` 印机。 但是，与“将打印流发送到打印机”部分关联的快速开始使用 `generatePrintedOutput` 该方法。

**将打印流发送到网络打印机**

检索要打印的文档后，可以调用输出服务，这会使其向网络打印机发送打印流。 要使输出服务成功找到打印机，您必须指定打印服务器和打印机名称。 此外，还必须指定打印协议。

>[!NOTE]
>
>如果表单服务器上安装了PDFG，且服务器运行于Windows Server 2008上，则无法使用SharedPrinter属性。 在这种情况下，请使用其他打印机协议。

>[!NOTE]
>
>如果您使用网络打印机，并且访问机制是SharedPrinter，则需要指定打印机的完整网络路径。使用Java API将打印流发送到网络打印机

使用Output API(Java)将打印流发送到网络打印机：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建Output Client对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源

   * 创建一 `java.io.FileInputStream` 个对象，它表示用于使用文档的构造函数并传递一个指定XML文件位置的字符串值来填充该数据的XML数据源。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置打印运行时选项

   创建一 `PrintedOutputOptionsSpec` 个表示打印运行时选项的对象。 例如，可以通过调用对象的方法来指定要打 `PrintedOutputOptionsSpec` 印的副本 `setCopies` 数。

   >[!NOTE]
   >
   >如果生成的是ZPL打印流， `PrintedOutputOptionsSpec` 则不能使 `setPagination` 用对象的方法设置分页值。 同样，您无法为ZPL打印流设置以下选项： OutputJog、PageOffset和Stapler。 该 `setPagination` 方法对PostScript生成无效。 它仅对PCL生成有效。

1. 检索要打印的文档

   * 通过调用对象的方法并传 `OutputClient` 递以下值 `generatePrintedOutput` 来检索要打印的文档:

      * 指定 `PrintFormat` 打印流的明细列表值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`。
      * 指定表单设计名称的字符串值。
      * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
      * 一个字符串值，它指定要使用的XDC文件的位置。
      * 包含 `PrintedOutputOptionsSpec` 打印到文件所需的运行时选项的对象。
      * 表示 `com.adobe.idp.Document` 包含要与表单设计合并的表单数据的XML数据源的对象。

      此方法返回 `OutputResult` 包含操作结果的对象。

   * 通过调 `com.adobe.idp.Document` 用对象的方法创建要发送到打 `OutputResult` 印机的 `getGeneratedDoc` 对象。 此方法返回一个 `com.adobe.idp.Document` 对象。


1. 将打印流发送到网络打印机

   通过调用对象的方法并传递以下值，将 `OutputClient` 打印流发 `sendToPrinter` 送到网络打印机：

   * 表示 `com.adobe.idp.Document` 要发送到打印机的打印流的对象。
   * 一个 `PrinterProtocol` 明细列表值，它指定要使用的打印机协议。 例如，要指定SharedPrinter协议，请传递 `PrinterProtocol.SharedPrinter`。
   * 指定打印服务器名称的字符串值。 例如，假定打印服务器的名称为PrintServer1，请传递 `\\\PrintSever1`。
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1，请传递 `\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >该 `sendToPrinter` 方法已添加到版本8.2.1中的AEM FormsAPI。

### 使用Web服务API将打印流发送到打印机 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

使用Output API（Web服务）将打印流发送到网络打印机：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 对象 `BLOB` 用于存储表单数据。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它指定包含表单数据的XML文件的位置。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 通过获取对象的属性来确 `System.IO.FileStream` 定字节数组 `Length` 长度。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 设置打印运行时选项。

   使用对 `PrintedOutputOptionsSpec` 象的构造函数创建对象。 例如，可以通过为对象的数据成员分配一个整数值来指定要打印的份 `PrintedOutputOptionsSpec` 数，该整 `copies` 数值表示份数。

   >[!NOTE]
   >
   >如果生成的是ZPL打印流，则 `PrintedOutputOptionsSpec` 不能使用对 `pagination` 象的数据成员设置分页值。 同样，您无法为ZPL打印流设置以下选项： OutputJog、PageOffset和Stapler。 数 `pagination` 据成员对PostScript生成无效。 它仅对PCL生成有效。

1. 检索要打印的文档。

   * 通过调用对象的方法并传 `OutputServiceService` 递以下值 `generatePrintedOutput` 来检索要打印的文档:

      * 指定 `PrintFormat` 打印流的明细列表值。 例如，要创建PostScript打印流，请传递 `PrintFormat.PostScript`。
      * 指定表单设计名称的字符串值。
      * 一个字符串值，它指定相关附属文件（如图像文件）的位置。
      * 一个字符串值，它指定要使用的XDC文件的位置。
      * 包 `PrintedOutputOptionsSpec` 含向网络打印机发送打印流时使用的打印运行时选项的对象。
      * 包 `BLOB` 含表单数据的XML数据源的对象。
      * 由 `BLOB` 方法填充的对 `generatePrintedOutput` 象。 该方 `generatePrintedOutput` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅用于Web服务调用。）
      * 由 `BLOB` 方法填充的对 `generatePrintedOutput` 象。 方法 `generatePrintedOutput` 使用结果数据填充此对象。 （此参数值仅用于Web服务调用。）
      * 包 `OutputResult` 含操作结果的对象。 （此参数值仅用于Web服务调用。）
   * 通过 `BLOB` 获取对象‘s方法的值，创建要发送到打 `OutputResult` 印机的对 `generatedDoc` 象。 此方法返回一 `BLOB` 个对象，该对象包含由该方法返回的PostScript `generatePrintedOutput` 数据。


1. 将打印流发送到网络打印机。

   通过调用对象的方法并传递以下值，将 `OutputClient` 打印流发 `sendToPrinter` 送到网络打印机：

   * 表示 `BLOB` 要发送到打印机的打印流的对象。
   * 一个 `PrinterProtocol` 明细列表值，它指定要使用的打印机协议。 例如，要指定SharedPrinter协议，请传递 `PrinterProtocol.SharedPrinter`。
   * 一个 `bool` 值，它指定是否使用先前的参数值。 传递值 `true`。 （此参数值仅用于Web服务调用。）
   * 指定打印服务器名称的字符串值。 例如，假定打印服务器的名称为PrintServer1，请传递 `\\\PrintSever1`。
   * 指定打印机名称的字符串值。 例如，假定打印机的名称为Printer1，请传递 `\\\PrintSever1\Printer1`。

   >[!NOTE]
   >
   >该 `sendToPrinter` 方法已添加到版本8.2.1中的AEM FormsAPI。

## 创建多个输出文件 {#creating-multiple-output-files}

输出服务可以为XML数据源中的每条记录或包含所有记录的单个文件（此功能是默认功能）创建单独的文档。 例如，假定XML数据源中有十条记录，并且您指示输出服务使用输出服务API为每个记录创建单独的PDF文档（或其他类型的输出）。 因此，输出服务会生成十个PDF文档。 (您可以向打印机发送多个打印流，而不是创建文档。)

下图还显示了处理包含多个记录的XML数据文件的Output服务。 但是，假定您指示输出服务创建包含所有数据记录的单个PDF文档。 在这种情况下，输出服务将生成一个包含所有记录的文档。

下图显示了Output服务处理包含多个记录的XML数据文件。 假定您指示输出服务为每个数据记录创建单独的PDF文档。 在这种情况下，输出服务会为每个数据记录生成单独的PDF文档。

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

请注意，开始和结束每个数据记录的XML元素是 `LoanRecord`。 此XML元素由生成多个文件的应用程序逻辑引用。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要根据XML数据源创建多个PDF文件，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成多个PDF文件。
1. 检索操作结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceService` 对象。

**引用XML数据源**

引用包含多个记录的XML数据源。 必须使用XML元素来分隔数据记录。 例如，在本节前面显示的示例XML数据源中，将命名用于分隔数据记录的XML元素 `LoanRecord`。

要填充数据的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 如果指定了所有XML元素，则不必与XML元素的显示顺序匹配。

**设置PDF运行时选项**

必须为输出服务设置以下运行时选项，才能基于XML数据源成功创建多个文件：

* **许多文件**: 指定输出服务是创建单个文档还是创建多个文档。 可以指定true或false。 要为XML数据源中的每个数据记录创建单独的文档，请指定true。
* **文件URI**: 指定输出服务生成的文件的位置。 例如，假定您指定C:\\Adobe\forms\Loan.pdf。 在这种情况下，输出服务将创建一个名为Loan.pdf的文件，并将该文件放在C:\\Adobe\forms folder文件夹中。 当存在多个文件时，文件名为Loan0001.pdf、Loan0002.pdf、Loan0003.pdf等。 如果指定文件位置，则文件将放在服务器上，而不放在客户端计算机上。
* **记录名称**: 指定用于分隔数据记录的数据源中的XML元素名称。 例如，在本节前面显示的示例XML数据源中，将调用用于分隔数据记录的XML元素 `LoanRecord`。 (除了设置“记录名称”运行时选项之外，您还可以通过为记录级别分配一个数值来设置记录级别，该值指示包含数据记录的元素级别。 但是，您只能设置记录名称或记录级别。 不能同时设置这两个值。)

**设置渲染运行时选项**

在创建多个文件时，可以设置渲染运行时选项。 尽管这些选项不是必需的（与输出运行时选项不同，它们是必需的），但您可以执行任务，如提高输出服务的性能。 例如，您可以缓存输出服务用于提高性能的表单设计。

当输出服务处理批处理记录时，它以增量方式读取包含多个记录的数据。 即，输出服务将数据读入内存并在处理批处理记录时释放数据。 设置两个运行时选项之一时，输出服务以增量方式加载数据。 如果设置“记录名称”运行时选项，则“输出”服务以增量方式读取数据。 同样，如果将“记录级别”运行时选项设置为2或更大，则“输出”服务以增量方式读取数据。

您可以使用或对象的方法控制输出服务 `PDFOutputOptionsSpec` 是否执 `PrintedOutputOptionSpec` 行增量加 `setLazyLoading` 载。 您可以将值传递 `false` 给此方法，这将关闭增量加载。

**生成多个PDF文件**

引用包含多个数据记录和设置运行时选项的有效XML数据源后，可以调用输出服务，这会导致它生成多个文件。 生成多个记录时， `OutputResult` 对象的方法 `getGeneratedDoc` 会返回 `null`。

**检索操作结果**

输出服务执行操作后，它返回指定操作是否成功的XML数据。 输出服务返回以下XML。 在这种情况下，输出服务生成42个文档。

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

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建多个PDF文件 {#create-multiple-pdf-files-using-the-java-api}

使用Output API(Java)创建多个PDF文件：

1. 包括项目文件”

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。 .

1. 创建Output Client对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源

   * 通过使 `java.io.FileInputStream` 用XML数据源的构造函数并传递一个指定XML文件位置的字符串值，创建一个表示包含多个记录的XML数据源的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 设置PDF运行时选项

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象的方法 `PDFOutputOptionsSpec` 设置“多文件” `setGenerateManyFiles` 选项。 例如，传递该值 `true` 以指示输出服务为XML数据源中的每条记录创建单独的PDF文件。 (如果通过， `false`输出服务将生成包含所有记录的单个PDF文档)。
   * 通过调用对象的方法并传 `PDFOutputOptionsSpec` 递一个字符串 `setFileUri` 值来设置“文件URI”选项，该字符串值指定输出服务生成的文件的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。
   * 通过调用对象的方法并传 `OutputOptionsSpec` 递一个字符串值来 `setRecordName` 设置“记录名称”选项，该字符串值指定用于分隔数据记录的数据源中的XML元素名称。 (例如，请考虑本节前面显示的XML数据源。 用于分隔数据记录的XML元素的名称为LoanRecord)。

1. 设置渲染运行时选项

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象并传递值来缓存表单设计，以 `RenderOptionsSpec` 提高输 `setCacheEnabled` 出服务 `Boolean` 的性能 `true`。

1. 生成多个PDF文件

   通过调用对象的方法并 `OutputClient` 传递以 `generatePDFOutput` 下值，生成多个PDF文件：

   * 枚举 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。

   该 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作结果

   * 创建一 `java.io.File` 个对象，它表示将包含方法结果的XML文 `generatePDFOutput` 件。 确保文件扩展名为。xml。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `applyUsageRights` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API创建多个PDF文件](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建多个PDF文件 {#create-multiple-pdf-files-using-the-web-service-api}

使用Output API（Web服务）创建多个PDF文件：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储包含多个记录的表单数据。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示包含多个记录的XML文件的文件位置。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 设置PDF运行时选项。

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过为对象的数据成员分配布尔值来 `OutputOptionsSpec` 设置“多 `generateManyFiles` 个文件”选项。 例如，为此数据成 `true` 员指定值，以指示输出服务为XML数据源中的每条记录创建单独的PDF文件。 (如果您为此 `false` 数据成员分配，则输出服务将生成一个包含所有记录的PDF)。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成的文件到对象数 `OutputOptionsSpec` 据成员的 `fileURI` 位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。
   * 通过在数据源中指定指定XML元素名称的字符串值来设置记录名称选项，该XML元素名称将数据记录分 `OutputOptionsSpec` 隔为对象的 `recordName` 数据成员。
   * 通过指定一个整数值来设置副本选项，该整数值指定输出服务为对象的数据成 `OutputOptionsSpec` 员生成的 `copies` 副本数。

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 将表单设计缓存，通过将值分配给对象的数据成员 `true` 来提 `RenderOptionsSpec` 高输出服务 `cacheEnabled` 的性能。

1. 生成多个PDF文件。

   通过调用对象的方法并 `OutputServiceService` 传递以 `generatePDFOutput`下值，创建多个PDF文件：

   * TransformationFormat枚举值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 该方 `generatePDFOutput` 法使用生成的描述文档的元数据填充此对象。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 方法 `generatePDFOutput` 使用结果数据填充此对象。
   * 包 `OutputResult` 含操作结果的对象。

1. 检索操作结果

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示包含结果数据的XML文件位置的字符串值来创建对象。 确保文件扩展名为。xml。
   * 创建一个字节数组，它存储由对象 `BLOB` 的方法（第八个参数）填充 `OutputServiceService` 的结果数 `generatePDFOutput` 据的对象的数据内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入XML文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 创建搜索规则 {#creating-search-rules}

您可以创建搜索规则，使“输出”服务检查输入数据并根据数据内容使用不同的表单设计生成输出。 例如，如果文本按 *揭* 位于输入数据中，则输出服务可以使用名为Mortgage.xdp的表单设计。 同样，如果文本 *汽车* 位于输入数据中，则输出服务可以使用另存为AutobileLoan.xdp的表单设计。 尽管输出服务可以生成不同的输出类型，但本节假定输出服务生成PDF文件。 下图显示了通过处理XML数据文件并使用多种表单设计之一生成PDF文件的输出服务。

此外，输出服务能够生成文档包，其中在数据集中提供多个记录，并且每个记录与表单设计匹配，并且生成由多个表单设计组成的单个文档。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要指示输出服务在生成文档时使用搜索规则，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 引用XML数据源。
1. 定义搜索规则。
1. 设置PDF运行时选项。
1. 设置渲染运行时选项。
1. 生成PDF文档。
1. 检索操作结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。

**引用XML数据源**

要填充数据的每个表单字段都必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 只要指定了所有XML元素，就不必与XML元素的显示顺序匹配。

**定义搜索规则**

要定义搜索规则，您需定义输出服务在输入数据中搜索的一个或多个文本模式。 对于您定义的每个文本模式，您指定在找到文本模式时使用的相应表单设计。 如果找到文本模式，则输出服务将使用相应的表单设计生成输出。 文本模式的一个示例是 *按揭贷款*。

>[!NOTE]
>
>如果找不到文本模式，则使用默认表单。 确保您使用的所有表单设计都位于内容根目录中。

**设置PDF运行时选项**

设置以下PDF运行时选项，使“输出”服务能够基于多个表单设计成功创建PDF文档:

* **文件URI**: 指定输出服务生成的PDF文件的名称和位置。
* **规则**: 指定您定义的规则。
* **LookAHead**: 指定从输入数据文件开始扫描所定义文本模式的字节数。 默认为500字节。

**设置渲染运行时选项**

您可以在创建PDF文件时设置渲染运行时选项。 尽管这些选项不是必需的（与PDF运行时选项不同），但您可以执行任务，如提高输出服务的性能。 例如，您可以缓存输出服务用于提高性能的表单设计。

**生成PDF文档**

引用有效的XML数据源并设置运行时选项后，可以调用输出服务，以生成PDF文档。 如果输出服务在输入数据中查找指定的文本模式，则使用相应的表单设计。 如果未使用文本模式，则输出服务将使用默认的表单设计。

**检索操作结果**

输出服务执行操作后，它返回指定操作是否成功的XML数据。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API创建搜索规则 {#create-search-rules-using-the-java-api}

使用Output API(Java)创建搜索规则：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output Client对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用XML数据源。

   * 创建一 `java.io.FileInputStream` 个对象，它表示用于填充PDF文档的XML数据源，方法是使用其构造函数并传递一个指定XML文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 定义搜索规则。

   * 使用对 `Rule` 象的构造函数创建对象。
   * 通过调用对象的方法并传 `Rule` 递指定文 `setPattern` 本模式的字符串值来定义文本模式。
   * 通过调用对象的方法来定 `Rule` 义相应的表单 `setForm` 设计。 传递指定表单设计名称的字符串值。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 使用构 `java.util.List` 造函数创建 `java.util.ArrayList` 对象。
   * 对于您 `Rule` 创建的每个对象，调用 `java.util.List` 对象的方 `add` 法并传递该 `Rule` 对象。


1. 设置PDF运行时选项。

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 指定输出服务通过调用对象的方法生成的PDF文件 `PDFOutputOptionsSpec` 的名称和位 `setFileURI` 置。 传递一个指定PDF文件位置的字符串值。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。
   * 设置通过调用对象的方法 `PDFOutputOptionsSpec` 定义的规 `setRules` 则。 传递包 `java.util.List` 含对象的 `Rule` 对象。
   * 通过调用对象的方法，设置要扫描的字节数以查 `PDFOutputOptionsSpec` 找已定义的文 `setLookAhead` 本模式。 传递一个表示字节数的整数值。

1. 设置渲染运行时选项。

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 通过调用对象并传递来缓存表单设计，以 `RenderOptionsSpec` 提高输出服 `setCacheEnabled` 务的性 `true`能。

1. 生成PDF文档。

   通过调用对象的方法并传递以下值，生成基 `OutputClient` 于多个表 `generatePDFOutput` 单设计的PDF文档:

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 一个字符串值，它指定默认表单设计的名称。 即在未找到文本图案时使用的表单设计。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `com.adobe.idp.Document` 含表单数据的对象，Output服务会搜索定义的文本模式。

   该 `generatePDFOutput` 方法返回 `OutputResult` 包含操作结果的对象。

1. 检索操作结果。

   * 通过 `com.adobe.idp.Document` 调用对象的方法，创 `generatePDFOutput` 建一个表示方 `OutputResult` 法状态的对 `getStatusDoc` 象。
   * 创建 `java.io.File` 一个将包含操作结果的对象。 确保文件扩展名为。xml。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `com.adobe.idp.Document` 中(确保使用该方 `com.adobe.idp.Document` 法返回的 `getStatusDoc` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[快速开始（SOAP模式）: 使用Java API创建搜索规则](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API创建搜索规则 {#create-search-rules-using-the-web-service-api}

使用输出API（Web服务）创建搜索规则：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用XML数据源。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储将与PDF文档合并的数据。
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 定义搜索规则。

   * 使用对 `Rule` 象的构造函数创建对象。
   * 通过为对象的数据成员指定指定文本模式的字符串值来 `Rule` 定义文本 `pattern` 模式。
   * 通过为对象的数据成员指定指定表单设计的字符串值来 `Rule` 定义相应的 `form` 表单设计。

   >[!NOTE]
   >
   >对于要定义的每个文本模式，重复前三个子步骤。

   * 创建存 `MyArrayOf_xsd_anyType` 储规则的对象。
   * 将每个 `Rule` 对象指定给数组的一个 `MyArrayOf_xsd_anyType` 元素。 为每个 `MyArrayOf_xsd_anyType` 对象调 `Add` 用对象的 `Rule` 方法。


1. 设置PDF运行时选项

   * 使用对 `PDFOutputOptionsSpec` 象的构造函数创建对象。
   * 通过指定一个字符串值来设置文件URI选项，该字符串值指定输出服务生成给对象数据成 `PDFOutputOptionsSpec` 员的PDF文件 `fileURI` 的位置。 “文件URI”选项与承载AEM Forms的J2EE应用程序服务器相关，而与客户端计算机无关。
   * 通过指定一个整数值来设置副本选项，该整数值指定输出服务为对象的数据成 `PDFOutputOptionsSpec` 员生成的 `copies` 副本数。
   * 通过将存储规则的对象分配给 `MyArrayOf_xsd_anyType` 对象的数据成员来设置您 `PDFOutputOptionsSpec` 定义的 `rules` 规则。
   * 通过为对象的数据方法指定一个整数值来设置要扫描的字节数，该整数值表示要扫 `PDFOutputOptionsSpec` 描的字节数，以 `lookAhead` 便扫描定义文本。

1. 设置渲染运行时选项

   * 使用对 `RenderOptionsSpec` 象的构造函数创建对象。
   * 将表单设计缓存，以便通过将值分配给对象的数据成 `true` 员来 `RenderOptionsSpec` 改进输出 `cacheEnabled` 服务。

   >[!NOTE]
   >
   >如果输入文档是Acrobat表单，则不能使 `RenderOptionsSpec` 用对象 `pdfVersion` 的成员设置PDF文档的版本。 输出PDF文档保留Acrobat表单的PDF版本。 同样，如果输入文档是Acrobat表单，则不 `RenderOptionsSpec` 能使用对 `taggedPDF` 象的方法设置加标签的PDF选项。

   >[!NOTE]
   >
   >如果输入的PDF文档经过认证或数字签名， `RenderOptionsSpec` 则不能通 `linearizedPDF` 过使用对象的成员来设置线性化的PDF选项。 有关信息，请参 [阅对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。

1. 生成PDF文档

   通过调用对象的方法并 `OutputServiceService` 传递以 `generatePDFOutput`下值，创建PDF文档:

   * 明细列表 `TransformationFormat` 值。 要生成PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。
   * 一个字符串值，它指定表单设计所在的内容根目录。
   * 包 `PDFOutputOptionsSpec` 含PDF运行时选项的对象。
   * 包含 `RenderOptionsSpec` 渲染运行时选项的对象。
   * 包 `BLOB` 含XML数据源的对象，该数据源包含要与表单设计合并的数据。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 该方 `generatePDFOutput` 法使用生成的描述文档的元数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 由 `BLOB` 方法填充的对 `generatePDFOutput` 象。 方法 `generatePDFOutput` 使用结果数据填充此对象。 （此参数值仅对于Web服务调用是必需的）。
   * 包 `OutputResult` 含操作结果的对象。 （此参数值仅对于Web服务调用是必需的）。

   >[!NOTE]
   >
   >通过调用方法生成PDF文档 `generatePDFOutput` 时，请注意，您不能将数据与已签名、已验证或包含使用权限的XFA PDF表单合并。 有关使用权限的信息，请参 [阅将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 检索操作结果

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示包含结果数据的XML文件位置的字符串值来创建对象。 确保文件扩展名为XML。
   * 创建一个字节数组，它存储由对象 `BLOB` 的方法（第八个参数）填充 `OutputServiceService` 的结果数 `generatePDFOutput` 据的对象的数据内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入XML文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 拼合PDF文档 {#flattening-pdf-documents}

您可以使用输出服务将交互式PDF文档转换为非交互式PDF。 交互式PDF文档允许用户输入或修改PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为 *拼合*。 拼合PDF文档时，用户无法修改文档字段中的数据。 拼合PDF文档的一个原因是确保无法修改数据。

您可以拼合以下类型的PDF文档:

* 交互式XFA PDF文档
* Acrobat Forms

尝试拼合非交互式PDF文档的PDF会导致异常。

>[!NOTE]
>
>有关输出服务的详细信息，请参 [阅服务参考AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-9}

要将交互式PDF文档拼合为非交互式PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Output Client对象。
1. 检索交互式PDF文档。
1. 转换PDF文档。
1. 将非交互式PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则需要将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM FormsJAR文件的位置的信息，请参 [阅包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Output Client对象**

在以编程方式执行输出服务操作之前，必须创建输出服务客户端对象。 如果您使用Java API，请创建一个 `OutputClient` 对象。 如果您使用Output Web服务API，请创建一个 `OutputServiceService` 对象。

**检索交互式PDF文档**

检索要转换为非交互式PDF文档的交互式PDF文档。 尝试转换非交互式PDF文档会导致异常。

**转换PDF文档**

检索交互式PDF文档后，可以将其转换为非交互式PDF文档。 输出服务返回非交互式PDF文档。

**将非交互式PDF文档另存为PDF文件**

您可以将非交互式PDF文档另存为PDF文件。

**另请参阅**

[使用Java API拼合PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[使用Web服务API拼合PDF文档](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[输出服务API快速开始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### 使用Java API拼合PDF文档 {#flatten-a-pdf-document-using-the-java-api}

使用Output API(Java)将交互式PDF文档拼合为非交互式PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-output-client.jar。

1. 创建一个Output Client对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `OutputClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 检索交互式PDF文档。

   * 创建一 `java.io.FileInputStream` 个对象，它使用其构造函数并传递一个字符串值来表示要转换的交互式PDF文档，该字符串值指定交互式PDF文件的位置。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 转换PDF文档。

   通过调用对象的方法并传递以下值，将交互式PDF文档 `OutputServiceService` 转换为非 `transformPDF` 交互式PDF文档:

   * 包 `com.adobe.idp.Document` 含交互式PDF文档的对象。
   * 枚举 `TransformationFormat` 值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定 `PDFARevisionNumber` 修订号的枚举值。 由于此参数用于PDF/A文档，您可以指定 `null`。
   * 一个字符串值，它表示修改编号和年份，以冒号分隔。 由于此参数用于PDF/A文档，您可以指定 `null`。
   * 表 `PDFAConformance` 示PDF/A符合性级别的枚举值。 由于此参数用于PDF/A文档，您可以指定 `null`。

   该 `transformPDF` 方法返回 `com.adobe.idp.Document` 一个包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 创建对 `java.io.File` 象，并确保文件扩展名为。pdf。
   * 调用 `Document` 对象的方 `copyToFile` 法，将对象的内容复制到文件 `Document` 中(确保使用该方 `Document` 法返回的 `transformPDF` 对象)。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[快速开始（EJB模式）: 使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[快速开始（SOAP模式）: 使用Java API转换PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API拼合PDF文档 {#flatten-a-pdf-document-using-the-web-service-api}

使用Output API（Web服务）将交互式PDF文档拼合为非交互式PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建一个Output Client对象。

   * 使用对象 `OutputServiceClient` 的默认构造函数创建对象。
   * 使用构 `OutputServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/OutputService?blob=mtom`。) 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。 但是，请指 `?blob=mtom` 定使用MTOM。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `OutputServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `OutputServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `OutputServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 检索交互式PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储交互式PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示交互式PDF文档的文件位置的字符串值来创建对象。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象属性 `MTOM` 赋予字节数组的内容来填充对象。

1. 转换PDF文档。

   通过调用对象的方法并传递以下值，将交互式PDF文档 `OutputClient` 转换为非 `transformPDF` 交互式PDF文档:

   * 包 `BLOB` 含交互式PDF文档的对象。
   * 明细列表 `TransformationFormat` 值。 要生成非交互式PDF文档，请指定 `TransformationFormat.PDF`。
   * 指定 `PDFARevisionNumber` 修订号的枚举值。
   * 一个布尔值，它指定是否 `PDFARevisionNumber` 使用枚举值。 由于此参数用于PDF/A文档，您可以指定 `false`。
   * 一个字符串值，它表示修改编号和年份，以冒号分隔。 由于此参数用于PDF/A文档，您可以指定 `null`。
   * 表 `PDFAConformance` 示PDF/A符合性级别的枚举值。
   * 指定是否使用枚举 `PDFAConformance` 值的布尔值。 由于此参数用于PDF/A文档，您可以指定 `false`。

   该 `transformPDF` 方法返回 `BLOB` 一个包含非交互式PDF文档的对象。

1. 将非交互式PDF文档另存为PDF文件。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递表示非交互式PDF文档的文件位置的字符串值来创建对象。
   * 创建一个字节数组，它存储由方 `BLOB` 法返回的对象的数据 `transformPDF` 内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的 `Write` 内容写入PDF文件。

**另请参阅**

[步骤摘要](creating-document-output-streams.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
