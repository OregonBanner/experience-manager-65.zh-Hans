---
title: 以编程方式组合PDF文档
description: 使用Assembler服务API通过Java API和Web服务API将多个PDF文档组合为单个PDF文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# 以编程方式组合PDF文档 {#programmatically-assembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

您可以使用Assembler服务API将多个PDF文档组合到单个PDF文档中。 下图显示三个PDF文档合并到单个PDF文档中。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要将两个或多个PDF文档组合为单个PDF文档，您需要一个DDX文档。 DDX文档描述了Assembler服务生成的PDF文档。 即，DDX文档会指示Assembler服务要执行的操作。

为了进行此讨论，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX文档合并两个名为的PDF文档 *map.pdf* 和 *directions.pdf* 合并为一个PDF文档。

>[!NOTE]
>
>要查看拆卸PDF文档的DDX文档，请参阅 [以编程方式拆分PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 使用Web服务调用Assembler服务时的注意事项 {#considerations-when-invoking-assembler-service-using-web-services}

在组装大型文档期间添加页眉和页脚时，可能会遇到 `OutOfMemory` 错误，无法组装文件。 要减少出现此问题的可能性，请添加 `DDXProcessorSetting` 元素添加到DDX文档中，如以下示例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

您可以添加此元素作为 `DDX` 元素或作为的子项 `PDF result` 元素。 此设置的默认值为0（零），这将关闭检查点，并且DDX的行为与 `DDXProcessorSetting` 元素不存在。 如果您遇到了 `OutOfMemory` 错误，您可能需要将值设置为整数，通常介于500和5000之间。 较小的检查点值会导致更频繁的检查点操作。

## 步骤摘要 {#summary-of-steps}

要从多个PDF文档组合单个PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用输入PDF文档。
1. 设置运行时选项。
1. 组合输入PDF文档。
1. 提取结果。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

您必须先创建一个Assembler客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要组合PDF文档，必须引用DDX文档。 例如，考虑本节介绍的DDX文档。 此DDX文档指示Assembler服务将两个PDF文档合并为一个PDF文档。

**引用输入PDF文档**

引用要传递到Assembler服务的输入PDF文档。 例如，如果要传递两个名为“映射”和“方向”的输入PDF文档，则必须传递相应的PDF文件。

map.pdf文件和directions.pdf文件都必须放置在集合对象中。 密钥的名称必须与DDX文档中PDF源属性的值匹配。 如果DDX文档中的键和源属性匹配，则PDF文件的名称无关紧要。

>[!NOTE]
>
>An `AssemblerResult` 如果调用，则将返回包含集合对象的对象 `invokeDDX` 操作。 将两个或多个输入PDF文档传递到Assembler服务时，将使用此操作。 但是，如果只将一个输入PDF传递给Assembler服务，并且只期望有一个返回文档，则调用 `invokeOneDocument` 操作。 调用此操作时，将返回单个文档。 有关使用此操作的信息，请参见 [汇编加密的PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。 有关可设置的运行时选项的信息，请参见 `AssemblerOptionSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**组合输入PDF文档**

在创建服务客户端、引用DDX文件、创建存储输入PDF文档的集合对象并设置运行时选项之后，可以调用DDX操作。 使用本节中指定的DDX文档时，map.pdf和direction.pdf文件将合并到一个PDF文档中。

**提取结果**

Assembler服务返回 `java.util.Map` 对象，可从 `AssemblerResult` 对象，并包含操作结果。 返回的 `java.util.Map` 对象包含生成的文档和任何异常。

下表汇总了可返回的一些键值和对象类型 `java.util.Map` 对象。

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

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式拆分PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API组合PDF文档 {#assemble-pdf-documents-using-the-java-api}

使用Assembler服务API (Java)组合PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 通过使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 引用输入PDF文档。

   * 创建 `java.util.Map` 通过使用PDF存储输入文档的对象 `HashMap` 构造函数。
   * 对于每个输入PDF文档，创建 `java.io.FileInputStream` 对象通过构造函数传递输入PDF文件的位置。
   * 对于每个输入PDF文档，创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含PDF文档的对象。
   * 对于每个输入文档，添加一个条目到 `java.util.Map` 对象(通过调用其 `put` 方法并传递以下参数：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
      * A `com.adobe.idp.Document` 对象(或 `java.util.List` 对象)，其中包含源PDF文档。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象的 `setFailOnError` 方法和路径 `false`.

1. 组合输入PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含要装配的输入PDF文件的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象

   此 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含作业结果和发生的任何异常的对象。

1. 提取结果。

   要获取新创建的PDF文档，请执行下列操作：

   * 调用 `AssemblerResult` 对象的 `getDocuments` 方法。 这会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果为止 `com.adobe.idp.Document` 对象。 (可以使用DDX文档中指定的PDF结果元素来获取文档。)
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于提取PDF文档的方法。

   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 设置为生成日志，您可以使用提取日志 `AssemblerResult` 对象的 `getJobLog` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API组合PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合PDF文档 {#assemble-pdf-documents-using-the-web-service-api}

使用Assembler服务API（Web服务）组合PDF文档：

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
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 属性与字节数组的内容。

1. 引用输入PDF文档。

   * 对于每个输入PDF文档，创建 `BLOB` 对象。 此 `BLOB` 对象用于存储输入PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此收藏集对象用于存储输入PDF文档。
   * 对于每个输入PDF文档，创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。 例如，如果使用两个输入PDF文档，则创建两个 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 将代表键名的字符串值分配给 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `key` 字段。 此值必须与DDX文档中指定的PDF源元素的值匹配。 (为每个输入PDF文档执行此任务。)
   * 分配 `BLOB` 将PDF文档存储到的对象 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象的 `value` 字段。 (为每个输入PDF文档执行此任务。)
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象的 `Add` 方法并传递 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 (为每个输入PDF文档执行此任务。)

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过为属于以下对象的数据成员分配值，设置运行时选项以满足您的业务要求 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请分配 `false` 到 `AssemblerOptionSpec` 对象的 `failOnError` 数据成员。

1. 组合输入PDF文档。

   调用 `AssemblerServiceClient` 对象的 `invoke` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 此 `mapItem` 包含输入PDF文档的数组。 其键必须与PDF源文件的名称匹配，其值必须是 `BLOB` 与这些文件对应的对象。
   * An `AssemblerOptionSpec` 指定运行时选项的对象。

   此 `invoke` 方法返回 `AssemblerResult` 包含作业结果和可能已发生的任何异常的对象。

1. 提取结果。

   要获取新创建的PDF文档，请执行下列操作：

   * 访问 `AssemblerResult` 对象的 `documents` 字段，即 `Map` 包含结果PDF文档的对象。
   * 循环访问 `Map` 对象，直到找到与生成文档名称匹配的键为止。 然后强制转换该数组成员的 `value` 到 `BLOB`.
   * 通过访问代表PDF文档的二进制数据 `BLOB` 对象的 `MTOM` 属性。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

   >[!NOTE]
   >
   >如果 `LOG_LEVEL` 设置为生成日志，您可以通过获取 `AssemblerResult` 对象的 `jobLog` 数据成员。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
