---
title: 汇编加密的PDF文档
seo-title: 汇编加密的PDF文档
description: 使用Java API和Web服务API组合加密的PDF文档。
seo-description: 使用Java API和Web服务API组合加密的PDF文档。
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: 开发人员
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# 汇编加密的PDF文档{#assembling-encrypted-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以使用Assembler服务使用口令加密PDF文档。 在用密码加密PDF文档后，用户必须指定密码才能在Adobe Reader或Acrobat中视图PDF文档。 要使用口令加密PDF文档,DDX文档必须包含加密PDF文档所需的加密元素值。

在此讨论中，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

在此DDX文档中，请注意为source属性赋值`inDoc`。 如果只有一个输入的PDF文档传递给Assembler服务，并返回一个PDF文档，并调用`invokeOneDocument`操作，则将值`inDoc`赋给PDF源属性。 在调用`invokeOneDocument`操作时，`inDoc`值是预定义的键，必须在DDX文档中指定。

相反，在将两个或多个输入PDF文档传递到Assembler服务时，可以调用`invokeDDX`操作。 在这种情况下，将输入PDF文档的文件名指定到`source`属性。

加密服务不必成为AEM表单安装的一部分，即可使用密码加密PDF文档。 请参阅[加密和解密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅[AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)服务参考。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}摘要

要组合加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用不安全的PDF文档。
1. 设置运行时选项。
1. 加密文档。
1. 保存加密的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则为必需)

如果AEM Forms部署在JBoss以外的受支持的J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 例如，请考虑本节中引入的DDX文档。 要加密PDF文档,DDX文档必须包含`PasswordEncryptionProfile`元素。

**引用不安全的PDF文档**

必须引用一个不安全的PDF文档并将其传递给Assembler服务以对其进行加密。 如果引用的PDF文档已加密，将引发异常。

**设置运行时选项**

您可以设置运行时选项，以在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可以设置的运行时选项的信息，请参阅[AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

**加密文档**

创建Assembler服务客户端后，请引用包含加密信息的DDX文档、引用一个不安全的PDF文档并设置运行时选项，您可以调用`invokeOneDocument`操作。 因为只有一个输入的PDF文档被传递给Assembler服务(并且返回一个文档)，所以您可以使用`invokeOneDocument`操作而不是`invokeDDX`操作。

**保存加密的PDF文档**

如果仅将单个PDF文档传递给Assembler服务，则Assembler服务返回单个文档而不是集合对象。 即，在调用`invokeOneDocument`操作时，返回单个文档。 由于本节中引用的DDX文档包含加密信息，Assembler服务会返回用密码加密的PDF文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-an-encrypted-pdf-document-using-the-java-api}组合加密的PDF文档

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建对象。

1. 引用不安全的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递不安全的PDF文档的位置，创建对象。
   * 创建`com.adobe.idp.Document`对象，并传递包含PDF文档的`java.io.FileInputStream`对象。 此`com.adobe.idp.Document`对象将传递给`invokeOneDocument`方法。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 加密文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。 确保此DDX文档包含PDF源元素的值`inDoc`。
   * 一个`com.adobe.idp.Document`对象，它包含不安全的PDF文档。
   * 一个`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，它指定运行时选项，包括默认字体和作业日志级别。

   `invokeOneDocument`方法返回一个`com.adobe.idp.Document`对象，该对象包含密码加密的PDF文档。

1. 保存加密的PDF文档。

   * 创建一个`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件。 确保使用`invokeOneDocument`方法返回的`Document`对象。

**另请参阅**

[快速开始（SOAP模式）：使用Java API组合加密的PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用Web服务API {#assemble-an-encrypted-pdf-document-using-the-web-service-api}组合加密的PDF文档

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 请确保在设置服务引用时使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建一个对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`赋给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`赋给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 将`BLOB`对象的`MTOM`字段指定为字节数组的内容，从而填充该对象。

1. 引用不安全的PDF文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象作为参数传递给`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及在中打开文件的模式，创建一个对象。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 将`BLOB`对象的`MTOM`字段指定为字节数组的内容，从而填充该对象。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务需求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 加密文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 一个`BLOB`对象，它表示不安全的PDF文档
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeOneDocument`方法返回一个`BLOB`对象，该对象包含加密的PDF文档。

1. 保存加密的PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示加密的PDF文档的文件位置以及在中打开文件的模式，创建一个对象。
   * 创建一个字节数组，用于存储`invokeOneDocument`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值来填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象，创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
