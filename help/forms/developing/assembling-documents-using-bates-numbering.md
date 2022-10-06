---
title: 使用Bates编号组合文档
seo-title: Assembling Documents Using Bates Numbering
description: 使用Bates编号来使用Java和Web服务API来组合PDF文档。
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# 使用Bates编号组合文档 {#assembling-documents-using-bates-numbering}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以使用Bates编号来组合包含唯一页面标识符的PDF文档。 *Bates编号* 是对一批相关文档应用唯一标识的方法。 文档（或文档集）中的每个页面都会分配一个唯一标识该页面的Bates编号。 例如，包含物料清单信息并与组件生产相关联的制造文档可以包含标识符。 Bates编号包含按顺序递增的数值以及可选前缀和后缀。 前缀+数字+后缀称为 *Bates模式*.

下图显示了一个PDF文档，其中包含位于文档标题中的唯一标识符。

![au_au_batesnumber](assets/au_au_batesnumber.png)

就本讨论而言，唯一页面标识符放置在文档的标题中。 假设使用了以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

此DDX文档可合并两个名为 *map.pdf* 和 *directions.pdf* 到单个PDF文档中。 生成的PDF文档包含包含唯一页面标识符的标题。 例如，上图中的文档显示000016。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 本节不讨论这些概念，例如创建包含输入文档的集合对象，或从返回的集合对象中提取结果。 (请参阅 [以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要组合包含唯一页面标识符（Bates编号）的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用输入PDF文档。
1. 设置初始Bates编号值。
1. 组合输入PDF文档。
1. 提取结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 例如，以本节中引入的DDX文档为例。 要组合包含唯一页面标识符的PDF文档，DDX文档必须包含 `BatesNumber` 元素。

**引用输入PDF文档**

必须引用输入PDF文档来组合PDF文档。 例如，必须引用map.pdf和directions.pdf文档，才能将这些PDF文档组合到单个PDF文档中。

**设置初始Bates编号值**

您可以设置初始Bates编号值以满足您的业务要求。 例如，假定需要将初始值设置为000100。 如果不设置初始值，则第一页的值为000000。

**组合输入PDF文档**

创建汇编程序服务客户端后，引用包含的DDX文档 `BatesNumber` 元素信息、引用输入PDF文档和设置运行时选项，可以调用 `invokeDDX` 导致汇编程序服务组装包含唯一页面标识符的PDF文档的操作。

**提取结果**

汇编程序服务返回包含作业结果的集合对象。 您可以提取生成的PDF文档以及引发的任何异常。 在这种情况下，加密的PDF文档位于收集对象中。

>[!NOTE]
>
>如果调用 `invokeDDX` 操作。 在将两个或多个输入PDF文档传递到汇编程序服务时，将使用此操作。 但是，如果只将一个输入PDF文档传递到汇编程序服务，则应调用 `invokeOneDocument` 操作。 有关使用此操作的信息，请参阅 [汇编加密PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API通过Bates编号来组合文档 {#assemble-documents-with-bates-numbering-using-the-java-api}

使用汇编程序服务API(Java)来汇编使用唯一页面标识符（Bates编号）的PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用输入PDF文档。

   * 创建 `java.util.Map` 用于通过使用 `HashMap` 构造函数。
   * 对于每个输入PDF文档，请创建 `java.io.FileInputStream` 对象，并传递输入PDF文档的位置。 在这种情况下，请传递不安全的PDF文档的位置。
   * 对于每个输入PDF文档，请创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含PDF文档的对象。
   * 在 `java.util.Map` 通过调用对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。 例如，本节中引入的DDX文档中指定的PDF源文件的名称为Loan.pdf。
      * A `com.adobe.idp.Document` 包含不安全的PDF文档的对象。

1. 设置初始Bates编号值。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用 `AssemblerOptionSpec` 对象 `setFirstBatesNumber` 和传递指定初始值的数字值。

1. 组合输入PDF文档。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示DDX文档的对象。
   * A `java.util.Map` 包含输入不安全的PDF文件的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象。

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含密码加密PDF文档的对象。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 此操作将返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到您找到 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）：使用Java API将PDF文档与bates编号组合在一起](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API使用Bates编号来组合文档 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

使用汇编程序服务API（Web服务）来汇编使用唯一页面标识符（Bates编号）的PDF文档：

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
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 引用输入PDF文档。

   * 对于每个输入PDF文档，请创建 `BLOB` 对象。 的 `BLOB` 对象用于存储输入PDF文档。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储输入的PDF文档。
   * 对于每个输入PDF文档，请创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。 例如，如果使用两个输入PDF文档，请创建两个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为分配表示键名称的字符串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `key` 字段。 此值必须匹配DDX文档中指定的PDF源元素的值。 (对每个输入PDF文档执行此任务。)
   * 分配 `BLOB` 将PDF文档存储到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `value` 字段。 (对每个输入PDF文档执行此任务。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象 `Add` 方法和通过 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 (对每个输入PDF文档执行此任务。)

1. 设置初始Bates编号值。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为 `firstBatesNumber` 属于的数据成员 `AssemblerOptionSpec` 对象。

1. 组合输入PDF文档。

   调用 `AssemblerServiceClient` 对象 `invoke` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含输入PDF文档的对象。 其键必须匹配PDF源文件的名称，并且其值必须为 `BLOB` 对应于这些文件的对象。
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象。

   的 `invoke` 方法返回 `AssemblerResult` 包含作业结果和发生的任何例外的对象。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含结果PDF文档的对象。
   * 循环访问 `Map` 对象，直到您找到与生成文档的名称匹配的键。 然后，将该阵列成员的 `value` 至 `BLOB`.
   * 通过访问表示PDF文档的二进制数据 `BLOB` 对象 `MTOM` 属性。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
