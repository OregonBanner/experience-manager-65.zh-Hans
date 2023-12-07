---
title: 使用书签组合PDF文档
description: 使用Assembler服务通过Java API和Web服务API修改包含书签的PDF文档，以包含书签。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# 使用书签组合PDF文档 {#assembling-pdf-documents-with-bookmarks}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

您可以组合包含书签的PDF文档。 例如，假设您有一个不包含书签的PDF文档，并且您想通过提供书签来修改它。 使用Assembler服务，您可以向其传递不包含书签的PDF文档，并取回包含书签的PDF文档。

书签包含以下属性：

* 在屏幕上显示为文本的标题。
* 一个操作，指定用户单击书签时执行的操作。 书签的典型操作是移动到当前文档中的另一个位置或打开另一个PDF文档，但可以指定其他操作。

为了进行此讨论，假定使用以下DDX文档。

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

在此DDX文档中，请注意已将值指定给源属性 `Loan.pdf`. 此DDX文档指定将单个PDF文档传递到Assembler服务。 在组合带有书签的PDF文档时，必须指定描述结果文档中书签的书签XML文档。 要指定书签XML文档，请确保 `Bookmarks` 元素在DDX文档中指定。

在此示例DDX文档中， `Bookmarks` 元素指定 `doc2` 作为值。 此值表示传递到Assembler服务的输入映射包含一个名为的键 `doc2`. 的值 `doc2` 键是 `com.adobe.idp.Document` 表示书签XML文档的值。 (请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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

在此书签XML文档中，请注意定义用户单击书签时执行的操作的操作元素。 在Action元素下是Launch元素，该元素可启动应用程序（如NotePad）并打开文件(如PDF文件)。 要打开PDF文件，必须使用指定要打开的文件的File元素。 例如，在此部分指定的书签XML文件中，打开的文件名为LoanDetails.pdf。

>[!NOTE]
>
>有关支持的操作的完整详细信息，请参阅&quot; `Action` 元素” [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

给定本节中指定的DDX文档并将XML文件标记为书签，Assembler服务将组合包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击 *打开贷款详细信息* 书签时，将打开LoanDetails.pdf。 同样，当用户单击 *启动便笺* 书签，便笺板已启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务组合PDF文档。 本节不讨论相关概念，例如创建包含输入文档的收藏集对象，或者了解如何从返回的收藏集对象中提取结果。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要组合包含书签的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用添加书签的PDF文档。
1. 引用书签XML文档。
1. 将PDF文档和书签XML文档添加到地图收藏集。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存包含书签的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为JAR文件，这些文件特定于部署AEM Forms的J2EE应用程序服务器。 有关所有AEM Forms JAR文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建PDF汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要组合PDF文档，必须引用DDX文档。 此DDX文档必须包含 `Bookmarks` 元素，指示Assembler服务组合包含书签的PDF。 （有关示例，请参阅本节前面显示的DDX文档。）

**引用添加书签的PDF文档**

引用添加书签的PDF文档。 所引用的PDF文档是否已包含书签并不重要。 如果 `Bookmarks` 元素是PDF源元素的子元素，则书签将替换PDF源中已存在的书签。 但是，如果要保留现有书签，请确保 `Bookmarks` 是PDF源元素的同级。 例如，请考虑以下示例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用书签XML文档**

要组合包含新书签的PDF，必须引用书签XML文档。 书签XML文档将传递到Map集合对象中的Assembler服务。 （有关示例，请参阅本节前面显示的书签XML文档。）

>[!NOTE]
>
>请参阅中的“书签语言” [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

**将PDF文档和书签XML文档添加到地图收藏集**

将添加书签的PDF文档以及书签XML文档添加到映射集合中。 因此，映射集合对象包含两个元素：PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。 有关可设置的运行时选项的信息，请参见 `AssemblerOptionSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**汇编PDF文档**

要组合包含新书签的PDF文档，请使用Assembler服务的 `invokeDDX` 操作。 为什么您必须使用 `invokeDDX` 操作而不是其他Assembler服务操作，例如 `invokeOneDocument` 是因为Assembler服务需要在Map集合对象中传递的书签XML文档。 此对象是 `invokeDDX` 操作。

**保存包含书签的PDF文档**

从返回的映射对象中提取结果并保存相应的PDF文档。 （请参阅中的“提取结果”） [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合带有书签的PDF文档 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用Assembler服务API (Java)组合带有书签的PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 通过使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 引用添加书签的PDF文档。

   * 创建 `java.io.FileInputStream` 对象通过使用该对象的构造函数并传递PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 对象，然后传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 引用书签XML文档。

   * 创建 `java.io.FileInputStream` 对象通过使用该对象的构造函数并传递表示书签XML文档的XML文件的位置。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含PDF文档的对象。

1. 将PDF文档和书签XML文档添加到地图收藏集。

   * 创建 `java.util.Map` 用于存储输入PDF文档和书签XML文档的对象。
   * PDF通过调用 `java.util.Map` 对象的 `put` 方法并传递以下参数：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 包含输入PDF文档的对象。

   * 通过调用书签XML文档 `java.util.Map` 对象的 `put` 方法并传递以下参数：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的书签源元素的值匹配。
      * A `com.adobe.idp.Document` 包含书签XML文档的对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象的 `setFailOnError` 方法和路径 `false`.

1. 组合PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含输入PDF文档和书签XML文档的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   此 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作业结果和发生的任何异常的对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行下列操作：

   * 调用 `AssemblerResult` 对象的 `getDocuments` 方法。 这会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果为止 `com.adobe.idp.Document` 对象。 (可以使用DDX文档中指定的PDF结果元素来获取文档。)
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于提取PDF文档的方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API组合带有书签的PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合带有书签的PDF文档 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler服务API（Web服务）组合带有书签的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象使用默认构造函数。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 引用添加书签的PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储输入PDF。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 引用书签XML文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储书签XML文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 将PDF文档和书签XML文档添加到地图收藏集。

   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储输入的PDF文档和书签XML文档。
   * 对于每个输入PDF文档和书签XML文档，创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 将代表键名的字符串值分配给 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `key` 字段。 此值必须与DDX文档中指定的PDF源元素的值匹配。
   * 分配 `BLOB` 将PDF文档存储到的对象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `value` 字段。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的 `Add` 方法并传递 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 (为每个输入PDF文档和书签XML文档执行此任务。)

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过为属于以下对象的数据成员分配值，设置运行时选项以满足您的业务要求 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请分配 `false` 到 `AssemblerOptionSpec` 对象的 `failOnError` 数据成员。

1. 组合PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * 此 `MyMapOf_xsd_string_To_xsd_anyType` 包含输入文档的数组
   * An `AssemblerOptionSpec` 指定运行时选项的对象

   此 `invokeDDX` 方法返回 `AssemblerResult` 包含作业结果和可能已发生的任何异常的对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行下列操作：

   * 访问 `AssemblerResult` 对象的 `documents` 字段，即 `Map` 包含结果PDF文档的对象。
   * 循环访问 `Map` 对象，直到找到与生成文档名称匹配的键为止。 然后强制转换该数组成员的 `value` 到 `BLOB`.
   * 通过访问代表PDF文档的二进制数据 `BLOB` 对象的 `MTOM` 字段。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
