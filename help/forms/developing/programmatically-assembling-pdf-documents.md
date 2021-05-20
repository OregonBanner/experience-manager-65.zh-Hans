---
title: 以编程方式组合PDF文档
seo-title: 以编程方式组合PDF文档
description: 使用汇编程序服务API，使用Java API和Web服务API将多个PDF文档组合为单个PDF文档。
seo-description: 使用汇编程序服务API，使用Java API和Web服务API将多个PDF文档组合为单个PDF文档。
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 0%

---

# 以编程方式组合PDF文档{#programmatically-assembling-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以使用汇编程序服务API将多个PDF文档组合为一个PDF文档。 下图显示了三个PDF文档被合并到单个PDF文档中。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

要将两个或多个PDF文档组合为一个PDF文档，您需要DDX文档。 DDX文档描述汇编程序服务生成的PDF文档。 即，DDX文档指示汇编程序服务执行哪些操作。

在本讨论中，假定使用了以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

此DDX文档将名为&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的两个PDF文档合并到一个PDF文档中。

>[!NOTE]
>
>要查看分解PDF文档的DDX文档，请参阅[以编程方式分解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 使用Web服务{#considerations-when-invoking-assembler-service-using-web-services}调用汇编程序服务时的注意事项

在装配大型文档期间添加页眉和页脚时，可能会遇到`OutOfMemory`错误，文件将不会装配。 要减少出现此问题的机率，请向DDX文档中添加`DDXProcessorSetting`元素，如以下示例所示。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

可以将此元素添加为`DDX`元素的子元素或作为`PDF result`元素的子元素。 此设置的默认值为0（零），这会关闭检查点并且DDX的行为类似于`DDXProcessorSetting`元素不存在。 如果遇到`OutOfMemory`错误，则可能需要将值设置为整数，通常介于500到5000之间。 小的检查点值会导致检查点更频繁。

## 步骤{#summary-of-steps}的摘要

要从多个PDF文档组合单个PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 参考输入PDF文档。
1. 设置运行时选项。
1. 组合输入的PDF文档。
1. 提取结果。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 例如，以本节中引入的DDX文档为例。 此DDX文档指示汇编程序服务将两个PDF文档合并为一个PDF文档。

**参考输入PDF文档**

引用要传递给汇编程序服务的输入PDF文档。 例如，如果要传递名为“映射”和“方向”的两个输入PDF文档，则必须传递相应的PDF文件。

map.pdf文件和directions.pdf文件都必须放置在收藏对象中。 键的名称必须与DDX文档中PDF源属性的值匹配。 如果DDX文档中的键和源属性匹配，则PDF文件的名称无关紧要。

>[!NOTE]
>
>如果调用`invokeDDX`操作，则返回包含集合对象的`AssemblerResult`对象。 将两个或更多输入的PDF文档传递到汇编程序服务时，会使用此操作。 但是，如果只将一个输入PDF传递给汇编程序服务，而只希望返回一个文档，则调用`invokeOneDocument`操作。 调用此操作时，将返回一个文档。 有关使用此操作的信息，请参阅[组装加密的PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

**组合输入的PDF文档**

在创建服务客户端、引用DDX文件、创建存储输入PDF文档的集合对象并设置运行时选项后，可以调用DDX操作。 使用本节中指定的DDX文档时，map.pdf和direction.pdf文件将合并到一个PDF文档中。

**提取结果**

汇编程序服务返回一个`java.util.Map`对象，该对象可以从`AssemblerResult`对象获取，并且包含操作结果。 返回的`java.util.Map`对象包含生成文档和任何例外。

下表汇总了可位于返回的`java.util.Map`对象中的一些键值和对象类型。

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

[以编程方式拆解PDF文档](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## 使用Java API {#assemble-pdf-documents-using-the-java-api}组合PDF文档

使用汇编程序服务API(Java)汇编PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 参考输入PDF文档。

   * 使用`HashMap`构造函数创建一个`java.util.Map`对象，用于存储输入的PDF文档。
   * 对于每个输入PDF文档，使用其构造函数创建一个`java.io.FileInputStream`对象，并传递输入PDF文档的位置。
   * 对于每个输入的PDF文档，创建一个`com.adobe.idp.Document`对象，并传递包含该PDF文档的`java.io.FileInputStream`对象。
   * 对于每个输入文档，通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。
      * 包含源PDF文档的`com.adobe.idp.Document`对象（或指定多个文档的`java.util.List`对象）。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法来设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合输入的PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * `java.util.Map`对象，其中包含要组装的输入PDF文件
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，用于指定运行时选项，包括默认字体和作业日志级别

   `invokeDDX`方法会返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，其中包含作业的结果以及发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这会返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。 （可以使用DDX文档中指定的PDF结果元素获取文档。）
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

   >[!NOTE]
   >
   >如果将`LOG_LEVEL`设置为生成日志，则可以使用`AssemblerResult`对象的`getJobLog`方法提取日志。

**另请参阅**

[快速入门（SOAP模式）：使用Java API汇编PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#assemble-pdf-documents-using-the-web-service-api}组合PDF文档

使用汇编程序服务API（Web服务）汇编PDF文档：

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
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。

1. 参考输入PDF文档。

   * 对于每个输入PDF文档，请使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此收集对象用于存储输入的PDF文档。
   * 对于每个输入的PDF文档，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。 例如，如果使用两个输入PDF文档，则创建两个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段分配表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。 （对每个输入的PDF文档执行此任务。）
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 （对每个输入的PDF文档执行此任务。）
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 （对每个输入的PDF文档执行此任务。）

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合输入的PDF文档。

   调用`AssemblerServiceClient`对象的`invoke`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 包含输入PDF文档的`mapItem`数组。 其键必须与PDF源文件的名称匹配，其值必须是与这些文件对应的`BLOB`对象。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invoke`方法会返回一个`AssemblerResult`对象，其中包含作业的结果以及可能发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含结果PDF文档的`Map`对象。
   * 遍历`Map`对象，直到找到与生成文档的名称匹配的键。 然后，将该阵列成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性，提取表示该文档的二进制数据。 这会返回一个字节数组，您可以将其写出到PDF文件。

   >[!NOTE]
   >
   >如果将`LOG_LEVEL`设置为生成日志，则可以通过获取`AssemblerResult`对象`jobLog`数据成员的值来提取日志。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
