---
title: 使用Bates编号汇编文档
seo-title: 使用Bates编号汇编文档
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---


# 使用Bates编号汇编文档 {#assembling-documents-using-bates-numbering}

您可以使用Bates编号来组合包含唯一页面标识符的PDF文档。 *Bates编号* 是一种将唯一标识应用于一批相关文档的方法。 文档(或一组文档)中的每个页面都分配有一个Bates编号，用于唯一标识该页面。 例如，包含物料清单信息并与组件生产关联的制造文档可以包含标识符。 Bates编号包含按顺序递增的数值以及可选前缀和后缀。 前缀+数字+后缀称为Bates *模式*。

下图显示了一个PDF文档，它包含位于文档标题中的唯一标识符。

![au_au_batesnumber](assets/au_au_batesnumber.png)

为便于进行此讨论，唯一的页面标识符会放在文档的标题中。 假定使用以下DDX文档。

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

此DDX文档将两个名为map.pdf *的PDF文档**和directions.pdf合并为一* 个PDF文档。 生成的PDF文档包含由唯一页面标识符组成的标题。 例如，上图中的文档显示000016。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务汇编PDF文档。 本节不讨论这些概念，如创建包含输入文档的集合对象，或从返回的集合对象中提取结果。 (请参 [阅以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合包含唯一页面标识符（Bates编号）的PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考输入PDF文档。
1. 设置初始Bates编号值。
1. 组合输入的PDF文档。
1. 提取结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时需要)

如果AEM Forms部署在受支持的J2EE应用程序服务器（JBoss除外）上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM FormsJAR文件的位置的信息，请参 [阅包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 例如，请考虑本节中引入的DDX文档。 要组合包含唯一页面标识符的PDF文档,DDX文档必须包含该 `BatesNumber` 元素。

**参考输入PDF文档**

必须引用输入PDF文档才能组合PDF文档。 例如，必须引用map.pdf和directions.pdf文档，才能将这些PDF文档组合到一个PDF文档中。

**设置初始Bates编号值**

您可以设置初始Bates编号值以满足您的业务要求。 例如，假定要求将初始值设置为000100。 如果不设置初始值，则第一页的值为00000。

**组合输入的PDF文档**

在创建Assembler服务客户端后，请引用包含元素信息的 `BatesNumber``invokeDDX` DDX文档、引用输入的PDF文档和设置运行时选项，您可以调用Assembler服务中导致汇编包含唯一页面标识符的PDF文档的操作。

**提取结果**

Assembler服务返回包含作业结果的集合对象。 您可以提取生成的PDF文档以及引发的任何异常。 在这种情况下，加密的PDF文档位于集合对象中。

>[!NOTE]
>
>如果调用该操作，则返回集合 `invokeDDX` 对象。 将两个或多个输入的PDF文档传递到Assembler服务时使用此操作。 但是，如果只将一个输入PDF文档传递给Assembler服务，则应调用该操 `invokeOneDocument` 作。 有关使用此操作的信息，请参 [阅汇编加密的PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API将文档与Bates编号组合 {#assemble-documents-with-bates-numbering-using-the-java-api}

通过使用Assembler Service API(Java)组合使用唯一页面标识符（Bates编号）的PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 参考输入PDF文档。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的 `HashMap` 对象。
   * 对于每个输入PDF文档，请使 `java.io.FileInputStream` 用其构造函数创建一个对象，并传递输入PDF文档的位置。 在这种情况下，请通过不安全PDF文档的位置。
   * 对于每个输入PDF文档，创 `com.adobe.idp.Document` 建一个对象并传 `java.io.FileInputStream` 递包含PDF文档的对象。
   * 通过调用对象的方 `java.util.Map` 法并传递以 `put` 下参数，向对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。 例如，本节引入的DDX文档中指定的PDF源文件的名称为Loan.pdf。
      * 包 `com.adobe.idp.Document` 含不安全PDF文档的对象。

1. 设置初始Bates编号值。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用对象并传递指定 `AssemblerOptionSpec` 初始值 `setFirstBatesNumber` 的数值来设置初始Bates编号。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示DDX文档的对象。
   * 包 `java.util.Map` 含输入不安全的PDF文件的对象。
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象。

   该方 `invokeDDX` 法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 一个对象，该对象包含口令加密的PDF文档。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 此操作返回一 `java.util.Map` 个对象。
   * 遍历对 `java.util.Map` 象，直到找到对 `com.adobe.idp.Document` 象。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

**另请参阅**

[快速开始（SOAP模式）: 使用Java API将PDF文档与bates编号组合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将文档与Bates编号组合 {#assemble-documents-with-bates-numbering-using-the-web-service-api}

通过使用Assembler Service API（Web服务）组合使用唯一页面标识符（Bates编号）的PDF文档:

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
   * 通过调 `System.IO.FileStream` 用其构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。

1. 参考输入PDF文档。

   * 对于每个输入PDF文档，请使 `BLOB` 用其构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 将对象属性 `MTOM` 赋予字节数组的内容来填充对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储输入的PDF文档。
   * 对于每个输入PDF文档，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。 例如，如果使用两个输入PDF文档，则创建两个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的PDF源元素值匹配。 (对每个输入的PDF任务执行此文档。)
   * 将存 `BLOB` 储PDF文档的对象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 定到对象 `value` 字段。 (对每个输入的PDF任务执行此文档。)
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 (对每个输入的PDF任务执行此文档。)

1. 设置初始Bates编号值。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配 `firstBatesNumber` 一个数值来设置初始Bates `AssemblerOptionSpec` 编号。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invoke` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象。
   * 包 `MyMapOf_xsd_string_To_xsd_anyType` 含输入PDF文档的对象。 其键必须与PDF源文件的名称匹配，并且其值必须是与这 `BLOB` 些文件对应的对象。
   * 指 `AssemblerOptionSpec` 定运行时选项的对象。

   方 `invoke` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果和发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 结果PDF文档的对象。
   * 遍历对 `Map` 象，直到找到与生成文档的名称匹配的键。 然后将该数组成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
