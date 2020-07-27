---
title: 以编程方式组合PDF文档
seo-title: 以编程方式组合PDF文档
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2092'
ht-degree: 0%

---


# 以编程方式组合PDF文档 {#programmatically-assembling-pdf-documents}

您可以使用Assembler Service API将多个PDF文档组合为一个PDF文档。 下图显示了三个PDF文档被合并为一个PDF文档。

![pa_pa_文档_assembly](assets/pa_pa_document_assembly.png)

要将两个或多个PDF文档组合到一个PDF文档中，您需要一个DDX文档。 DDX文档描述Assembler服务生成的PDF文档。 即，DDX文档指示Assembler服务要执行的操作。

在本讨论中，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX文档将两个名为map.pdf *的PDF文档**和directions.pdf合并为一* 个PDF文档。

>[!NOTE]
>
>要查看分解PDF文档的DDX文档，请参阅以编 [程方式分解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参 [阅Services Reference forAEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用Web服务调用Assembler服务时的注意事项 {#considerations-when-invoking-assembler-service-using-web-services}

在组装大型文档时添加页眉和页脚时，可能会遇 `OutOfMemory` 到错误，文件将不会组合。 要减少出现此问题的可能性，请向 `DDXProcessorSetting` DDX文档添加元素，如以下示例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

可以将此元素添加为元素的 `DDX` 子项或元素的子 `PDF result` 项。 此设置的默认值为0（零），它关闭检查点，DDX的行为就像元素 `DDXProcessorSetting` 不存在一样。 如果遇到错 `OutOfMemory` 误，您可能需要将值设置为整数，通常介于500到5000之间。 小的检查点值导致检查点更频繁。

## 步骤摘要 {#summary-of-steps}

要从多个PDF文档组合一个PDF文档，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考输入PDF文档。
1. 设置运行时选项。
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

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 例如，请考虑本节中引入的DDX文档。 此DDX文档指示Assembler服务将两个PDF文档合并为一个PDF文档。

**参考输入PDF文档**

引用要传递给Assembler服务的输入PDF文档。 例如，如果要传递名为“映射和方向”的两个输入PDF文档，则必须传递相应的PDF文件。

map.pdf文件和directions.pdf文件都必须放在集合对象中。 键的名称必须与DDX文档中PDF源属性的值相匹配。 如果DDX文档中的键和源属性匹配，则PDF文件的名称不重要。

>[!NOTE]
>
>如 `AssemblerResult` 果调用操作，则返回包含集合对象的对 `invokeDDX` 象。 将两个或多个输入PDF文档传递给Assembler服务时，将使用此操作。 但是，如果只将一个输入PDF传递给Assembler服务并且只希望有一个返回文档，请调用该 `invokeOneDocument` 操作。 调用此操作时，将返回单个文档。 有关使用此操作的信息，请参 [阅汇编加密的PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可以设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM FormsAPI参 [考中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**组合输入的PDF文档**

在创建服务客户端、引用DDX文件、创建存储输入PDF文档的集合对象并设置运行时选项后，可以调用DDX操作。 使用本节中指定的DDX文档时，map.pdf和direction.pdf文件将合并为一个PDF文档。

**提取结果**

Assembler服务返回一 `java.util.Map` 个对象，该对象可以从该对 `AssemblerResult` 象获取，并且包含操作结果。 返回的对 `java.util.Map` 象包含生成文档和任何例外。

下表总结了可位于返回对象中的一些键值和对象类型。 `java.util.Map`

<table>
 <thead>
  <tr>
   <th><p>键值</p></th>
   <th><p>对象类型</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>包含在DDX生成元素中指定的生成文档</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>包含文档的任何例外</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>包含作业日志</p></td>
  </tr>
 </tbody>
</table>

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式反汇编PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API组合PDF文档 {#assemble-pdf-documents-using-the-java-api}

使用Assembler Service API(Java)汇编PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 通过 `java.io.FileInputStream` 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该DDX文件的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。

1. 参考输入PDF文档。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 对于每个输入PDF文档，请使 `java.io.FileInputStream` 用其构造函数创建一个对象，并传递输入PDF文档的位置。
   * 对于每个输入PDF文档，创 `com.adobe.idp.Document` 建一个对象并传 `java.io.FileInputStream` 递包含PDF文档的对象。
   * 对于每个输入文档，通过调用对象 `java.util.Map` 的方法并传递以 `put` 下参数，向对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
      * 包 `com.adobe.idp.Document` 含源PDF `java.util.List` 文档的对象(或指定多个文档的对象)。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调 `AssemblerOptionSpec` 用对象的 `setFailOnError` 方法并传递 `false`。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下必需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 包 `java.util.Map` 含要组合的输入PDF文件的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象

   该方 `invokeDDX` 法返回一 `com.adobe.livecycle.assembler.client.AssemblerResult` 个对象，其中包含作业的结果以及发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 这将返回一个 `java.util.Map` 对象。
   * 遍历对象 `java.util.Map` ，直到找到生成的对 `com.adobe.idp.Document` 象。 (您可以使用在DDX文档中指定的PDF结果元素获取文档。)
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。

   >[!NOTE]
   >
   >如 `LOG_LEVEL` 果设置为生成日志，则可以使用对象的方法 `AssemblerResult` 提取日 `getJobLog` 志。

**另请参阅**

[快速开始（SOAP模式）: 使用Java API汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API汇编PDF文档 {#assemble-pdf-documents-using-the-web-service-api}

使用Assembler Service API（Web服务）汇编PDF文档:

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
   * 通过调用对象的方法并传递要读取的 `System.IO.FileStream` 字节数 `Read` 组、开始位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象属性 `MTOM` 赋予字节数组的内容来填充对象。

1. 参考输入PDF文档。

   * 对于每个输入PDF文档，请使 `BLOB` 用其构造函数创建对象。 该 `BLOB` 对象用于存储输入的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数 `System.IO.FileStream` 据填充字节 `Read` 数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段 `MTOM` 指定字节数组的内容来填充对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储输入的PDF文档。
   * 对于每个输入PDF文档，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。 例如，如果使用两个输入PDF文档，则创建两个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与在DDX文档中指定的PDF源元素值匹配。 (对每个输入的PDF任务执行此文档。)
   * 将存 `BLOB` 储PDF文档的对象指 `MyMapOf_xsd_string_To_xsd_anyType_Item` 定到对象 `value` 字段。 (对每个输入的PDF任务执行此文档。)
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 (对每个输入的PDF任务执行此文档。)

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请 `false` 指定 `AssemblerOptionSpec` 对象的数据 `failOnError` 成员。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invoke` 法并传递以下值：

   * 表 `BLOB` 示DDX文档的对象。
   * 包 `mapItem` 含输入PDF文档的数组。 其键必须与PDF源文件的名称匹配，并且其值必须是与这 `BLOB` 些文件对应的对象。
   * 指 `AssemblerOptionSpec` 定运行时选项的对象。

   该方 `invoke` 法返回一 `AssemblerResult` 个对象，其中包含作业的结果以及可能发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含 `Map` 结果PDF文档的对象。
   * 遍历对 `Map` 象，直到找到与生成文档的名称匹配的键。 然后将该数组成员 `value` 转换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示PDF `BLOB` 的二进制 `MTOM` 数据。 这将返回可写入PDF文件的字节数组。

   >[!NOTE]
   >
   >如 `LOG_LEVEL` 果设置为生成日志，则可以通过获取对象数据成员 `AssemblerResult` 的值来提取 `jobLog` 日志。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
