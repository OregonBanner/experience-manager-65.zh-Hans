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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---


# 将PDF文档与书签组合 {#assembling-pdf-documents-with-bookmarks}

您可以组合包含书签的PDF文档。 例如，假定您的PDF文档不包含书签，并且您希望通过提供书签来修改它。 使用Assembler服务，您可以将不包含书签的PDF文档传递给它，并返回包含书签的PDF文档。

书签包含以下属性：

* 在屏幕上显示为文本的标题。
* 一个操作，指定当用户单击书签时发生的情况。 书签的典型操作是移动到当前文档中的其他位置或打开另一个PDF文档，但可以指定其他操作。

在本讨论中，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

在此DDX文档中，请注意为源属性分配了值 `Loan.pdf`。 此DDX文档指定将单个PDF文档传递给Assembler服务。 将PDF文档与书签组合时，必须指定书签XML文档，在结果文档中描述书签。 要指定书签XML文档，请确保在 `Bookmarks` DDX文档中指定元素。

在此示例DDX文档中，元 `Bookmarks` 素指 `doc2` 定为值。 此值指示传递给Assembler服务的输入映射包含一个名为的键 `doc2`。 键的值是 `doc2` 表示书 `com.adobe.idp.Document` 签XML文档的值。 (请参阅Assembler Service和DDX参考 [中的“书签语言](https://www.adobe.com/go/learn_aemforms_ddx_63)”。)

本主题使用以下XML书签语言组合包含书签的PDF文档。

```xml
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

在此书签XML文档中，请注意定义用户单击书签时执行的操作的“操作”元素。 在“操作”元素下方是启动元素，用于启动NotePad等应用程序并打开PDF文件等文件。 要打开PDF文件，必须使用指定要打开的文件的“文件”元素。 例如，在本节中指定的书签XML文件中，打开的文件的名称为LoanDetails.pdf。

>[!NOTE]
>
>有关支持的操作的完整详细信息，请参 `Action` 阅“汇编器服务” [和“DDX参考”中的“元素](https://www.adobe.com/go/learn_aemforms_ddx_63)”。

给定本节中指定的DDX文档并将XML文件加为书签作为输入，Assembler服务将汇编一个包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击“打开贷 *款详细信息”书签* 时，将打开LoanDetails.pdf。 同样，当用户单击Launch NotePad书 *签时* ,NotePad也会启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 本节不讨论概念，如创建包含输入文档的集合对象，或学习如何从返回的集合对象中提取结果。 (请参 [阅以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

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

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在其上的J2EE应用程序服务器的JAR文件。 有关所有AEM FormsJAR文件的位置的信息，请参 [阅包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 此DDX文档必须包含元 `Bookmarks` 素，该元素指示Assembler服务组合包含书签的PDF。 (有关示例，请参阅本节前面显示的DDX文档。)

**引用添加书签的PDF文档**

引用添加书签的PDF文档。 引用的PDF文档是否已包含书签并不重要。 如果元 `Bookmarks` 素是PDF源元素的子元素，则书签将替换PDF源中已存在的那些元素。 但是，如果要保留现有书签，请确保 `Bookmarks` 它是PDF源元素的同级。 例如，请考虑以下示例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用书签XML文档**

要组合包含新书签的PDF，必须引用书签XML文档。 书签XML文档将传递到Map集合对象中的Assembler服务。 (有关示例，请参阅本节前面显示的书签XML文档。)

>[!NOTE]
>
>请参阅Assembler Service和DDX参考 [中的“书签语言”](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**将PDF文档和书签XML文档添加到Map集合**

您必须将添加书签的PDF文档和书签XML文档添加到地图集合。 因此，Map集合对象包含两个元素： PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可以设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM FormsAPI参 [考中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**组合PDF文档**

要组合包含新书签的PDF文档，请使用Assembler服务的操 `invokeDDX` 作。 您必须将该操作与其他 `invokeDDX` Assembler服务操作(如， `invokeOneDocument` )相对使用的原因是Assembler服务需要在Map集合对象中传递的书签XML文档。 此对象是操作的参 `invokeDDX` 数。

**保存包含书签的PDF文档**

必须从返回的映射对象中提取结果并保存相应的PDF文档。 (请参阅以编程方式组合PDF [文档中的“提取结果](/help/forms/developing/programmatically-assembling-pdf-documents.md)”。)

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API将PDF文档与书签组合 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用Assembler Service API(Java)将PDF文档与书签组合在一起：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 引用添加书签的PDF文档。

   * 使用 `java.io.FileInputStream` 对象的构造函数并传递PDF文档的位置，创建对象。
   * 使用 `com.adobe.idp.Document` 其构造函数创建对象并传 `java.io.FileInputStream` 递包含PDF文档的对象。

1. 引用书签XML文档。

   * 通过使用 `java.io.FileInputStream` 其构造函数并传递表示书签XML文档的XML文件的位置，创建一个对象。
   * 创建一 `com.adobe.idp.Document` 个对象，并传 `java.io.FileInputStream` 递包含PDF文档的对象。

1. 将PDF文档和书签XML文档添加到Map集合。

   * 创建 `java.util.Map` 用于存储输入PDF文档和书签XML文档的对象。
   * 通过调用对象的方法并传递 `java.util.Map` 以下参数 `put` 来添加输入PDF文档:

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
      * 包 `com.adobe.idp.Document` 含输入PDF文档的对象。
   * 通过调用对象的方法并传递 `java.util.Map` 以下参数 `put` 来添加书签XML文档:

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的“书签”源元素的值匹配。
      * 包 `com.adobe.idp.Document` 含书签XML文档的对象。


1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 包 `java.util.Map` 含输入PDF文档和书签XML文档的对象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象

   该方 `invokeDDX` 法返回一 `com.adobe.livecycle.assembler.client.AssemblerResult` 个对象，其中包含作业的结果以及发生的任何异常。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 这将返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。 (您可以使用在DDX文档中指定的PDF结果元素获取文档。)
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[快速开始（SOAP模式）: 使用Java API将PDF文档与书签组合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将PDF文档与书签组合 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler Service API（Web服务）将PDF文档与书签组合在一起：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用对象 `AssemblerServiceClient` 的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建 `System.ServiceModel.EndpointAddress` 对象。 将指定WSDL的字符串值传递给AEM Forms服务(例如 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 此属性在您创建服务引用时使用。
   * 通过获 `System.ServiceModel.BasicHttpBinding` 取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常量值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常量值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取 `System.IO.FileStream` 的字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 引用添加书签的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 引用书签XML文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储书签XML文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 将PDF文档和书签XML文档添加到Map集合。

   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储输入的PDF文档和书签XML文档。
   * 对于每个输入PDF文档和书签XML文档，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
   * 将存 `BLOB` 储PDF文档的对象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 定到对象 `value` 字段。
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 (对每个输入PDF任务和书签XML文档执行此文档。)

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的数据 `failOnError` 成员。

1. 组合PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含输入文档的数组
   * 指定 `AssemblerOptionSpec` 运行时选项的对象

   该方 `invokeDDX` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果以及可能发生的任何异常。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 结果PDF文档的对象。
   * 遍历对 `Map` 象，直到找到与生成文档的名称匹配的键。 然后将该数组成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象字段提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
