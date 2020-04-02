---
title: 将PDF文档与书签组合
seo-title: 将PDF文档与书签组合
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: e3f700b52446505224fa4b4688d439750a66f471

---


# 将PDF文档与书签组合 {#assembling-pdf-documents-with-bookmarks}

您可以组合包含书签的PDF文档。 例如，假定您的PDF文档不包含书签，并且您希望通过提供书签来修改它。 使用Assembler服务，您可以将不包含书签的PDF文档传递给它，然后返回包含书签的PDF文档。

书签包含以下属性：

* 屏幕上显示为文本的标题。
* 一个操作，它指定用户单击书签时发生的情况。 书签的典型操作是移到当前文档中的其他位置或打开另一个PDF文档，但可以指定其他操作。

在本讨论中，假定使用以下DDX文档。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

在此DDX文档中，请注意为源属性分配了值 `Loan.pdf`。 此DDX文档指定将单个PDF文档传递给Assembler服务。 在将PDF文档与书签组合时，必须指定书签XML文档，以在结果文档中描述书签。 要指定书签XML文档，请确保在DDX `Bookmarks` 文档中指定该元素。

在此示例DDX文档中，元 `Bookmarks` 素指定 `doc2` 为值。 此值指示传递给Assembler服务的输入映射包含一个名为的键 `doc2`。 键的值是 `doc2` 表示书 `com.adobe.idp.Document` 签XML文档的值。 (请参阅汇编器服务和DDX [参考中的“书签语言”](https://www.adobe.com/go/learn_aemforms_ddx_63)。)

本主题使用以下XML书签语言组合包含书签的PDF文档。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

在此书签XML文档中，请注意定义用户单击书签时执行的操作的“操作”元素。 在“操作”元素下面是启动元素，用于启动应用程序（如NotePad）和打开文件（如PDF文件）。 要打开PDF文件，必须使用指定要打开的文件的“文件”元素。 例如，在本节中指定的书签XML文件中，打开的文件的名称为LoanDetails.pdf。

>[!NOTE]
>
>有关支持的操作的完整详细信息，请参 `Action` 阅“汇编器服务”和“ [DDX参考”中的“元素”](https://www.adobe.com/go/learn_aemforms_ddx_63)。

给定本节中指定的DDX文档，并将XML文件加为书签作为输入，Assembler服务将组合一个包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击“打开贷 *款详细信息”书签* ，将打开LoanDetails.pdf。 同样，当用户单击 *Launch NotePad书签时* ,NotePad会启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 本节不讨论概念，如创建包含输入文档的集合对象或了解如何从返回的集合对象中提取结果。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合包含书签的PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用添加书签的PDF文档。
1. 引用书签XML文档。
1. 将PDF文档和书签XML文档添加到Map集合。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存包含书签的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在上的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 此DDX文档必须包含元 `Bookmarks` 素，元素指示Assembler服务组合包含书签的PDF。 (有关示例，请参阅本节前面显示的DDX文档。)

**引用添加书签的PDF文档**

引用添加书签的PDF文档。 引用的PDF文档是否已包含书签并不重要。 如果元 `Bookmarks` 素是PDF源元素的子元素，则书签将替换PDF源中已存在的子元素。 但是，如果要保留现有书签，请确保它 `Bookmarks` 是PDF源元素的同级。 例如，请考虑以下示例：

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用书签XML文档**

要组合包含新书签的PDF，必须引用书签XML文档。 书签XML文档将传递给Map集合对象中的Assembler服务。 (有关示例，请参阅本节前面显示的书签XML文档。)

>[!NOTE]
>
>请参阅汇编器服务和DDX参考 [中的“书签语言”](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**将PDF文档和书签XML文档添加到地图集合**

您必须将添加书签的PDF文档和书签XML文档添加到地图集合。 因此，Map集合对象包含两个元素：PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，这些选项控制Assembler服务在执行作业时的行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM Forms API参考 [中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**组合PDF文档**

要组合包含新书签的PDF文档，请使用Assembler服务的操 `invokeDDX` 作。 您必须将该操作与其他Assembler服务操作( `invokeDDX` 如，Assembler服务)相对使用的原因 `invokeOneDocument` 是，Assembler服务需要在Map集合对象内传递的书签XML文档。 此对象是操作的一个参 `invokeDDX` 数。

**保存包含书签的PDF文档**

必须从返回的映射对象中提取结果并保存相应的PDF文档。 (请参阅以编程方式组合PDF文档 [中的“提取结果](/help/forms/developing/programmatically-assembling-pdf-documents.md)”。)

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API将PDF文档与书签组合在一起 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用Assembler Service API(Java)将PDF文档与书签组合起来：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示该DDX域的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 引用添加书签的PDF文档。

   * 使用 `java.io.FileInputStream` 对象的构造函数并传递PDF文档的位置，创建对象。
   * 使用 `com.adobe.idp.Document` 其构造函数创建对象，并传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 引用书签XML文档。

   * 通过使用 `java.io.FileInputStream` 其构造函数并传递表示书签XML文档的XML文件的位置，创建一个对象。
   * 创建一 `com.adobe.idp.Document` 个对象，并传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 将PDF文档和书签XML文档添加到Map集合。

   * 创建 `java.util.Map` 一个对象，该对象用于存储输入PDF文档和书签XML文档。
   * 通过调用对象的方法并传递以 `java.util.Map` 下参数来添 `put` 加输入PDF文档:

      * 表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素的值匹配。
      * 包 `com.adobe.idp.Document` 含输入PDF文档的对象。
   * 通过调用对象的方法并传递以 `java.util.Map` 下参数来添 `put` 加书签XML文档:

      * 表示键名的字符串值。 此值必须与在DDX文档中指定的“书签”源元素的值匹配。
      * 包 `com.adobe.idp.Document` 含书签XML文档的对象。


1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用对 `AssemblerOptionSpec` 象的方 `setFailOnError` 法并传递 `false`。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下所需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 一个 `java.util.Map` 对象，它同时包含输入PDF文档和书签XML文档。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象
   该方 `invokeDDX` 法返回一个对 `com.adobe.livecycle.assembler.client.AssemblerResult` 象，该对象包含作业的结果和发生的任何例外。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 这将返回一个 `java.util.Map` 对象。
   * 遍历对象， `java.util.Map` 直到找到生成的对 `com.adobe.idp.Document` 象。 (可以使用在DDX文档中指定的PDF结果元素获取文档。)
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[快速开始（SOAP模式）:使用Java API将PDF文档与书签组合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将PDF文档与书签组合在一起 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler Service API（Web服务）将PDF文档与书签组合起来：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对 `AssemblerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 引用添加书签的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储输入的PDF。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 引用书签XML文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储书签XML文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 将PDF文档和书签XML文档添加到地图集合。

   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储输入的PDF文档和书签XML文档。
   * 对于每个输入的PDF文档和书签XML文档，创建一个对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的PDF源元素的值匹配。
   * 将存 `BLOB` 储PDF文档的对象指定到该对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象的字 `value` 段。
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 (对每个输入PDF任务和书签XML文档执行此文档。)

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的数 `AssemblerOptionSpec` 据成员分 `failOnError` 配。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含输入文档的数组
   * 指定 `AssemblerOptionSpec` 运行时选项的对象
   该方 `invokeDDX` 法返回一个对 `AssemblerResult` 象，该对象包含作业的结果以及可能发生的任何例外。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 结果PDF文档的对象。
   * 遍历对 `Map` 象，直到找到与生成文档的名称匹配的键。 然后将该阵列成员转 `value` 换为 `BLOB`。
   * 通过访问PDF文档对象的字段提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
