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
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 以编程方式组合PDF文档 {#programmatically-assembling-pdf-documents}

您可以使用Assembler Service API将多个PDF文档组合到一个PDF文档中。 下图显示了三个PDF文档被合并到一个PDF文档中。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要将两个或多个PDF文档合并到一个PDF文档中，您需要一个DDX文档。 DDX文档描述Assembler服务生成的PDF文档。 即，DDX文档指示Assembler服务要执行的操作。

在本讨论中，请假定使用以下DDX文档。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX文档将两个名为 *map.pdf和*** directions.pdf的PDF文档合并为一个PDF文档。

>[!NOTE]
>
>要查看拆分PDF文档的DDX文档，请参阅以编程 [方式拆分PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用Web服务调用Assembler服务时的注意事项 {#considerations-when-invoking-assembler-service-using-web-services}

在组装大型文档期间添加页眉和页脚时，可能会遇 `OutOfMemory` 到错误，文件将不会组合。 要减少出现此问题的可能性，请向DDX `DDXProcessorSetting` 文档中添加元素，如以下示例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

可以将此元素添加为元素的子 `DDX` 元素或元素的子元 `PDF result` 素。 此设置的默认值为0（零），这会关闭检查点，而DDX的行为就像元素不 `DDXProcessorSetting` 存在一样。 如果您遇到错 `OutOfMemory` 误，可能需要将该值设置为整数，通常介于500到5000之间。 小的检查点值导致检查点更频繁。

## 步骤摘要 {#summary-of-steps}

要从多个PDF文档组合一个PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考输入PDF文档。
1. 设置运行时选项。
1. 组合输入的PDF文档。
1. 提取结果。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须先创建Assembler客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 例如，请考虑本节中引入的DDX文档。 此DDX文档指示Assembler服务将两个PDF文档合并到一个PDF文档中。

**参考输入PDF文档**

引用要传递给Assembler服务的输入PDF文档。 例如，如果要传递两个名为“地图和方向”的输入PDF文档，则必须传递相应的PDF文件。

map.pdf文件和directions.pdf文件必须都放置在集合对象中。 键的名称必须与DDX文档中PDF源属性的值相匹配。 如果DDX文档中的键和源属性匹配，则PDF文件的名称不重要。

>[!NOTE]
>
>如 `AssemblerResult` 果调用操作，将返回一个包含集合对象的对 `invokeDDX` 象。 将两个或多个输入的PDF文档传递给Assembler服务时，将使用此操作。 但是，如果只将一个输入PDF传递给Assembler服务并且只希望有一个返回文档，请调用该操 `invokeOneDocument` 作。 调用此操作时，将返回一个文档。 有关使用此操作的信息，请参阅 [Massigning Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**设置运行时选项**

您可以设置运行时选项，这些选项控制Assembler服务在执行作业时的行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM Forms API参考 [中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**组合输入的PDF文档**

在创建服务客户端、引用DDX文件、创建存储输入PDF文档的集合对象并设置运行时选项后，您可以调用DDX操作。 使用本节中指定的DDX文档时，map.pdf和direction.pdf文件将合并到一个PDF文档中。

**提取结果**

Assembler服务返回一个对 `java.util.Map` 象，该对象可以从该对象中获 `AssemblerResult` 得，并且包含操作结果。 返回的对 `java.util.Map` 象包含生成的文档和任何例外。

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

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式拆解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API组合PDF文档 {#assemble-pdf-documents-using-the-java-api}

使用Assembler Service API(Java)组合PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 使用 `java.io.FileInputStream` DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 参考输入PDF文档。

   * 使用构 `java.util.Map` 造函数创建用于存储输入PDF文档的对 `HashMap` 象。
   * 对于每个输入的PDF文档，使用其构 `java.io.FileInputStream` 造函数创建一个对象，并传递输入的PDF文档的位置。
   * 对于每个输入的PDF文档，创建一 `com.adobe.idp.Document` 个对象并传递包 `java.io.FileInputStream` 含该PDF文档的对象。
   * 对于每个输入文档，通过调用对象的方 `java.util.Map` 法并传递以下参 `put` 数，向对象添加一个条目：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
      * 包 `com.adobe.idp.Document` 含源PDF文档 `java.util.List` 的对象（或指定多个文档的对象）。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用对 `AssemblerOptionSpec` 象的方 `setFailOnError` 法并传递 `false`。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeDDX` 法并传递以下所需值：

   * 表 `com.adobe.idp.Document` 示要使用的DDX文档的对象
   * 包 `java.util.Map` 含要组合的输入PDF文件的对象
   * 指定 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 运行时选项（包括默认字体和作业日志级别）的对象
   该方 `invokeDDX` 法返回一个对 `com.adobe.livecycle.assembler.client.AssemblerResult` 象，该对象包含作业的结果和发生的任何例外。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用 `AssemblerResult` 对象的方 `getDocuments` 法。 这将返回一个 `java.util.Map` 对象。
   * 遍历对象， `java.util.Map` 直到找到生成的对 `com.adobe.idp.Document` 象。 （可以使用在DDX文档中指定的PDF结果元素获取文档。）
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法以提取PDF文档。
   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 设置为生成日志，则可以使用对象的方法提取 `AssemblerResult` 日志 `getJobLog` 。

**另请参阅**

[快速入门（SOAP模式）:使用Java API汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合PDF文档 {#assemble-pdf-documents-using-the-web-service-api}

使用Assembler Service API（Web服务）组合PDF文档：

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
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 参考输入PDF文档。

   * 对于每个输入的PDF文档，使用其构 `BLOB` 造函数创建一个对象。 对 `BLOB` 象用于存储输入的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。
   * 创建对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 此集合对象用于存储输入的PDF文档。
   * 对于每个输入的PDF文档，创建一个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。 例如，如果使用两个输入的PDF文档，则创建两个对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象。
   * 为对象的字段指定表示键名 `MyMapOf_xsd_string_To_xsd_anyType_Item` 的字符串 `key` 值。 此值必须与DDX文档中指定的PDF源元素的值匹配。 （对每个输入的PDF文档执行此任务。）
   * 将存 `BLOB` 储PDF文档的对象指定到该对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象的字 `value` 段。 （对每个输入的PDF文档执行此任务。）
   * 将对 `MyMapOf_xsd_string_To_xsd_anyType_Item` 象添加到对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的方 `Add` 法并传递对 `MyMapOf_xsd_string_To_xsd_anyType` 象。 （对每个输入的PDF文档执行此任务。）

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的数 `AssemblerOptionSpec` 据成员分 `failOnError` 配。

1. 组合输入的PDF文档。

   调用对 `AssemblerServiceClient` 象的方 `invoke` 法并传递以下值：

   * 表示 `BLOB` DDX文档的对象。
   * 包 `mapItem` 含输入PDF文档的数组。 其键必须与PDF源文件的名称匹配，并且其值必须是与这 `BLOB` 些文件相对应的对象。
   * 指定 `AssemblerOptionSpec` 运行时选项的对象。
   该方 `invoke` 法返回一个对 `AssemblerResult` 象，该对象包含作业的结果以及可能发生的任何例外。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问对 `AssemblerResult` 象的字 `documents` 段，该字段是包含结果PDF `Map` 文档的对象。
   * 遍历对 `Map` 象，直到找到与生成文档的名称匹配的键。 然后将该阵列成员转 `value` 换为 `BLOB`。
   * 通过访问PDF文档对象的属性提取表示该PDF文 `BLOB` 档的二进制数 `MTOM` 据。 这将返回可写入PDF文件的字节数组。
   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 设置为生成日志，则可以通过获取对象数据成员的值来提取 `AssemblerResult` 该日 `jobLog` 志。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
