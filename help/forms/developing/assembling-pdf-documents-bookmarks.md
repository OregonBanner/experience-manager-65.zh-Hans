---
title: 使用书签组合PDF文档
seo-title: Assembling PDF Documents with Bookmarks
description: 使用汇编程序服务修改包含书签的PDF文档，以使用Java API和Web服务API包含书签。
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 0%

---

# 使用书签组合PDF文档 {#assembling-pdf-documents-with-bookmarks}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以组合包含书签的PDF文档。 例如，假定您的PDF文档不包含书签，并且希望通过提供书签来修改它。 使用汇编程序服务，您可以将不包含书签的PDF文档传递给汇编程序，并返回包含书签的PDF文档。

书签包含以下属性：

* 屏幕上显示为文本的标题。
* 一个操作，用于指定用户单击书签时所发生的情况。 书签的典型操作是移动到当前文档中的其他位置或打开另一个PDF文档，尽管可以指定其他操作。

在本讨论中，假定使用了以下DDX文档。

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

在此DDX文档中，请注意已为源属性分配了值 `Loan.pdf`. 此DDX文档指定将单个PDF文档传递到汇编程序服务。 在将PDF文档与书签组合时，必须指定一个书签XML文档，该文档描述结果文档中的书签。 要指定书签XML文档，请确保 `Bookmarks` 元素。

在此示例DDX文档中， `Bookmarks` 元素指定 `doc2` 作为值。 此值指示传递到汇编程序服务的输入映射包含一个名为的键 `doc2`. 的值 `doc2` 键是 `com.adobe.idp.Document` 表示书签XML文档的值。 (请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).)

本主题使用以下XML书签语言来组合包含书签的PDF文档。

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

在此书签XML文档中，请注意定义用户单击书签时执行的操作的“操作”元素。 在“操作”元素下方是启动应用程序（如NotePad）并打开文件(如PDF文件)的Launch元素。 要打开PDF文件，必须使用指定要打开的文件的File元素。 例如，在本节中指定的书签XML文件中，打开的文件的名称为LoanDetails.pdf。

>[!NOTE]
>
>有关支持操作的完整详细信息，请参阅 `Action` 元素” [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

如果本节中指定的DDX文档并将XML文件加入书签作为输入，汇编程序服务将组合一个包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击 *打开贷款详细信息* 书签，则会打开LoanDetails.pdf。 同样，当用户单击 *启动NotePad* 书签，NotePad已启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 本节不讨论相关概念，例如创建包含输入文档的集合对象，或了解如何从返回的集合对象中提取结果。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要组合包含书签的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用书签被添加到的PDF文档。
1. 引用书签XML文档。
1. 将PDF文档和书签XML文档添加到映射集合。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存包含书签的PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 此DDX文档必须包含 `Bookmarks` 元素，该元素指示汇编程序服务组合包含书签的PDF。 （有关示例，请参阅本节前面显示的DDX文档。）

**引用添加书签的PDF文档**

引用书签被添加到的PDF文档。 引用的PDF文档是否已包含书签无关。 如果 `Bookmarks` 元素是PDF源元素的子元素，则书签将替换PDF源中已存在的元素。 但是，如果要保留现有书签，请确保 `Bookmarks` 是PDF源元素的同级元素。 例如，请考虑以下示例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用书签XML文档**

要组合包含新书签的PDF，必须引用书签XML文档。 书签XML文档将传递到映射收集对象中的汇编程序服务。 （有关示例，请参阅本节前面显示的书签XML文档。）

>[!NOTE]
>
>请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

**将PDF文档和书签XML文档添加到映射集合**

您必须将书签添加到的PDF文档和书签XML文档添加到映射集合中。 因此，映射集合对象包含两个元素：PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**组合PDF文档**

要组合包含新书签的PDF文档，请使用汇编程序服务的 `invokeDDX` 操作。 您必须使用 `invokeDDX` 操作，而不是其它汇编程序服务操作，例如 `invokeOneDocument` 是因为汇编程序服务需要在映射集合对象中传递的书签XML文档。 此对象是 `invokeDDX` 操作。

**保存包含书签的PDF文档**

必须从返回的映射对象中提取结果并保存相应的PDF文档。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API将PDF文档与书签组合 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用汇编程序服务API(Java)将PDF文档与书签组合：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用书签被添加到的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，并传递PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 对象，并传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 引用书签XML文档。

   * 创建 `java.io.FileInputStream` 对象，并传递表示书签XML文档的XML文件位置。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 将PDF文档和书签XML文档添加到映射集合。

   * 创建 `java.util.Map` 用于存储输入PDF文档和书签XML文档的对象。
   * 通过调用 `java.util.Map` 对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
      * A `com.adobe.idp.Document` 包含输入PDF文档的对象。
   * 通过调用 `java.util.Map` 对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须与DDX文档中指定的书签源元素的值匹配。
      * A `com.adobe.idp.Document` 包含书签XML文档的对象。


1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象 `setFailOnError` 方法和传递 `false`.

1. 组合PDF文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含输入PDF文档和书签XML文档的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作业结果和发生的任何例外的对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 这会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。 (可以使用DDX文档中指定的PDF结果元素来获取文档。)
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）：使用Java API将PDF文档与书签组合在一起](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API使用书签组合PDF文档 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用汇编程序服务API（Web服务）将PDF文档与书签组合：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 引用书签被添加到的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储输入PDF。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 引用书签XML文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储书签XML文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 将PDF文档和书签XML文档添加到映射集合。

   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储输入PDF文档和书签XML文档。
   * 对于每个输入PDF文档和书签XML文档，请创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为分配表示键名称的字符串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `key` 字段。 此值必须匹配DDX文档中指定的PDF源元素的值。
   * 分配 `BLOB` 将PDF文档存储到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `value` 字段。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象 `Add` 方法和通过 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 (对每个输入PDF文档和书签XML文档执行此任务。)

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请指定 `false` 到 `AssemblerOptionSpec` 对象 `failOnError` 数据成员。

1. 组合PDF文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含输入文档的数组
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和可能发生的任何例外的对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含结果PDF文档的对象。
   * 循环访问 `Map` 对象，直到您找到与生成文档的名称匹配的键。 然后，将该阵列成员的 `value` 至 `BLOB`.
   * 通过访问表示PDF文档的二进制数据 `BLOB` 对象 `MTOM` 字段。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
