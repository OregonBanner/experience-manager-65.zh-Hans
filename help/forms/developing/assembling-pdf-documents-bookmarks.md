---
title: 使用书签组合PDF文档
seo-title: 使用书签组合PDF文档
description: 使用汇编程序服务修改包含书签的PDF文档，以使用Java API和Web服务API包含书签。
seo-description: 使用汇编程序服务修改包含书签的PDF文档，以使用Java API和Web服务API包含书签。
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2588'
ht-degree: 0%

---

# 使用书签{#assembling-pdf-documents-with-bookmarks}组合PDF文档

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以组合包含书签的PDF文档。 例如，假定您的PDF文档不包含书签，并且希望通过提供书签来修改它。 使用汇编程序服务，您可以将不包含书签的PDF文档传递给它，并返回包含书签的PDF文档。

书签包含以下属性：

* 屏幕上显示为文本的标题。
* 一个操作，用于指定用户单击书签时所发生的情况。 书签的典型操作是移动到当前文档中的其他位置或打开另一个PDF文档，但可以指定其他操作。

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

在此DDX文档中，请注意为源属性分配了值`Loan.pdf`。 此DDX文档指定将单个PDF文档传递到汇编程序服务。 在将PDF文档与书签组合时，必须指定一个书签XML文档，该文档描述结果文档中的书签。 要指定书签XML文档，请确保在DDX文档中指定了`Bookmarks`元素。

在此示例DDX文档中，`Bookmarks`元素将`doc2`指定为值。 此值表示传递到汇编程序服务的输入映射包含一个名为`doc2`的键。 `doc2`键的值是表示书签XML文档的`com.adobe.idp.Document`值。 （请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“书签语言”。）

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

在此书签XML文档中，请注意定义用户单击书签时执行的操作的“操作”元素。 在“操作”元素下方是启动应用程序（如NotePad）并打开文件（如PDF文件）的Launch元素。 要打开PDF文件，必须使用指定要打开的文件的File元素。 例如，在本节中指定的书签XML文件中，打开的文件的名称为LoanDetails.pdf。

>[!NOTE]
>
>有关支持操作的完整详细信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“ `Action`元素”。

如果本节中指定的DDX文档并将XML文件加入书签作为输入，汇编程序服务将汇编一个包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击&#x200B;*打开贷款详细信息*&#x200B;书签时，将打开LoanDetails.pdf。 同样，当用户单击&#x200B;*启动NotePad*&#x200B;书签时，NotePad将启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 本节不讨论相关概念，例如创建包含输入文档的集合对象，或了解如何从返回的集合对象中提取结果。 （请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。）

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要组合包含书签的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用添加书签的PDF文档。
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

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 此DDX文档必须包含`Bookmarks`元素，该元素会指示汇编程序服务组合包含书签的PDF。 （有关示例，请参阅本节前面显示的DDX文档。）

**引用添加书签的PDF文档**

引用添加书签的PDF文档。 引用的PDF文档是否已包含书签并不重要。 如果`Bookmarks`元素是PDF源元素的子元素，则书签将替换PDF源中已存在的子元素。 但是，如果要保留现有书签，请确保`Bookmarks`是PDF源元素的同级元素。 例如，请考虑以下示例：

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
>请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“书签语言”。

**将PDF文档和书签XML文档添加到映射集合**

您必须将书签添加到的PDF文档和书签XML文档都添加到映射集合中。 因此，映射集合对象包含两个元素：PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

**组合PDF文档**

要组合包含新书签的PDF文档，请使用汇编程序服务的`invokeDDX`操作。 必须使用`invokeDDX`操作而不是其他汇编程序服务操作（如`invokeOneDocument`）的原因是汇编程序服务需要在映射收集对象中传递的书签XML文档。 此对象是`invokeDDX`操作的参数。

**保存包含书签的PDF文档**

必须从返回的映射对象中提取结果并保存相应的PDF文档。 （请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)中的“提取结果”。）

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}使用书签组合PDF文档

使用汇编程序服务API(Java)将PDF文档与书签组合：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 引用添加书签的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个对象，并传递PDF文档的位置。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递包含PDF文档的`java.io.FileInputStream`对象。

1. 引用书签XML文档。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个对象，并传递表示书签XML文档的XML文件的位置。
   * 创建`com.adobe.idp.Document`对象并传递包含PDF文档的`java.io.FileInputStream`对象。

1. 将PDF文档和书签XML文档添加到映射集合。

   * 创建一个`java.util.Map`对象，用于存储输入的PDF文档和书签XML文档。
   * 通过调用`java.util.Map`对象的`put`方法并传递以下参数来添加输入PDF文档：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
      * 包含输入PDF文档的`com.adobe.idp.Document`对象。
   * 通过调用`java.util.Map`对象的`put`方法并传递以下参数来添加书签XML文档：

      * 表示键名称的字符串值。 此值必须与DDX文档中指定的书签源元素的值匹配。
      * 包含书签XML文档的`com.adobe.idp.Document`对象。


1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法来设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * `java.util.Map`对象，其中同时包含输入的PDF文档和书签XML文档。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，用于指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法会返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，其中包含作业的结果以及发生的任何异常。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这会返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。 （可以使用DDX文档中指定的PDF结果元素获取文档。）
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）：使用Java API将PDF文档与书签组合在一起](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}使用书签组合PDF文档

使用汇编程序服务API（Web服务）将PDF文档与书签组合：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 引用添加书签的PDF文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入PDF。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 引用书签XML文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储书签XML文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 将PDF文档和书签XML文档添加到映射集合。

   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储输入的PDF文档和书签XML文档。
   * 对于每个输入的PDF文档和书签XML文档，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段分配表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 （对每个输入的PDF文档和书签XML文档执行此任务。）

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含输入文档的`MyMapOf_xsd_string_To_xsd_anyType`数组
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法会返回一个`AssemblerResult`对象，其中包含作业的结果以及可能发生的任何异常。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含结果PDF文档的`Map`对象。
   * 遍历`Map`对象，直到找到与生成文档的名称匹配的键。 然后，将该阵列成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`字段，提取表示该文档的二进制数据。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
