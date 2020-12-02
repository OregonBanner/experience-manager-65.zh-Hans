---
title: 确定文档是否符合PDF/A规范
seo-title: 确定文档是否符合PDF/A规范
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# 确定文档是否符合PDF/A规范{#determining-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服务确定PDF文档是否符合PDF/A规范。 PDF/A文档以存档格式存在，用于长期保留文档的内容。 字体嵌入在文档中，且文件未压缩。 因此，PDF/A文档通常大于标准PDF文档。 此外，PDF/A文档不包含音频和视频内容。

PDF/A-1规范由两个符合性级别组成，即A和B。两个级别之间的主要区别是逻辑结构（辅助功能）支持，这是符合性级别B所不要求的。无论符合性级别如何，PDF/A-1都指示所有字体嵌入到生成的PDF/A文档中。 目前，验证（和转换）只支持PDF/A-1b。

在本讨论中，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文档中，`DocumentInformation`元素指示Assembler服务返回有关输入PDF文档的信息。 在`DocumentInformation`元素中，`PDFAValidation`元素指示Assembler服务指示输入的PDF文档符合PDF/A标准。

Assembler服务返回的信息指定输入的PDF文档在包含`PDFAConformance`元素的XML文档中是否符合PDF/A规范。 如果输入的PDF文档符合PDF/A规范，则`PDFAConformance`元素的`isCompliant`属性的值为`true`。 如果PDF文档不符合PDF/A规范，则`PDFAConformance`元素的`isCompliant`属性的值为`false`。

>[!NOTE]
>
>由于本节中指定的DDX文档包含`DocumentInformation`元素，Assembler服务返回XML数据而不是PDF文档。 即，汇编服务不会汇编或反汇编PDF文档;它返回有关XML文档中输入PDF文档的信息。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参阅[Assembler Service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要确定PDF文档是否符合PDF/A规范，请执行以下任务:

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 参考用于确定PDF/A兼容性的PDF文档。
1. 设置运行时选项。
1. 检索有关PDF文档的信息。
1. 保存返回的XML文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，则为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必需)

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署的J2EE应用程序服务器的JAR文件。 有关所有AEM FormsJAR文件的位置的信息，请参阅[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能执行Assembler服务操作。 要确定输入的PDF文档是否符合PDF/A规范，请确保DDX文档包含`DocumentInformation`元素中的`PDFAValidation`元素。 `PDFAValidation`元素指示Assembler服务返回一个XML文档，它指定输入的PDF文档是否与PDF/A兼容。

**参考用于确定PDF/A兼容性的PDF文档**

必须引用PDF文档并将其传递给Assembler服务，以确定PDF文档是否符合PDF/A规范。

**设置运行时选项**

您可以设置运行时选项，这些选项在Assembler服务执行作业时控制其行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可以设置的运行时选项的信息，请参见[AEM FormsAPI参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

**检索有关PDF文档的信息**

在创建Assembler服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用`invokeDDX`操作。 由于DDX文档包含`DocumentInformation`元素，Assembler服务返回XML数据而不是PDF文档。

**保存返回的XML文档**

Assembler服务返回的XML文档指定输入的PDF文档是否与PDF/A兼容。 例如，如果输入的PDF文档符不符合PDF/A规范，Assembler服务将返回一个包含以下元素的XML文档符：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

将XML文档另存为XML文件，以便打开文件并视图结果。

**另请参阅**

[使用Java API确定文档是否符合PDF/A规范](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服务API确定文档是否符合PDF/A规范](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}确定文档是否符合PDF/A规范

使用Assembler Service API(Java)确定PDF文档是否符合PDF/A规范：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF Assembler客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`AssemblerServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示DDX文件的`java.io.FileInputStream`对象。 要确定PDF文档是否符合PDF/A规范，请确保DDX文档包含`PDFAValidation`元素，该元素包含在`DocumentInformation`元素中。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 参考用于确定PDF/A兼容性的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个&lt;a0/>对象，并传递用于确定PDF/A兼容性的PDF文档的位置。
   * 使用`com.adobe.idp.Document`对象的构造函数创建`java.io.FileInputStream`对象，并传递包含PDF文档的&lt;a1/>对象。
   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名称的字符串值。 此值必须与在DDX文档中指定的源元素值匹配。 例如，本节引入的DDX文档中的源元素的值为Loan.pdf。
      * 一个`com.adobe.idp.Document`对象，它包含输入PDF文档。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 检索有关PDF文档的信息。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 一个`com.adobe.idp.Document`对象，它表示要使用的DDX文档
   * 一个`java.util.Map`对象，它包含用于确定PDF/A兼容性的输入PDF文件
   * 指定运行时选项的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，该对象包含指定输入PDF文档是否符合PDF/A规范的XML数据。

1. 保存返回的XML文档。

   要获取指定输入PDF文档是否为PDF/A文档的XML数据，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这将返回`java.util.Map`对象。
   * 对`java.util.Map`对象进行迭代，直到找到生成的`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取XML文档。 确保将XML数据另存为XML文件。

**另请参阅**

[快速开始（SOAP模式）:使用Java API（SOAP模式）确定文档是否符合](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) PDF/A规范

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}确定文档是否符合PDF/A规范

使用Assembler Service API（Web服务）确定PDF文档是否符合PDF/A规范：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建PDF Assembler客户端。

   * 使用其默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段指定字节数组的内容，填充`BLOB`对象。

1. 参考用于确定PDF/A兼容性的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储输入的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储PDF文档。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段指定表示键名的字符串值。 此值必须与在DDX文档中指定的PDF源元素值匹配。
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象&#39; `Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。

1. 设置运行时选项。

   * 使用其构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在出现错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 检索有关PDF文档的信息。

   调用`AssemblerServiceService`对象的`invoke`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 包含输入PDF文档的`MyMapOf_xsd_string_To_xsd_anyType`对象。 其键必须与PDF源文件的名称匹配，其值必须是与输入PDF文件对应的`BLOB`对象。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invoke`方法返回一个`AssemblerResult`对象，该对象包含指定输入PDF文档是否为PDF/A文档的XML数据。

1. 保存返回的XML文档。

   要获取指定输入PDF文档是否为PDF/A文档的XML数据，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是一个`Map`对象，它包含指定输入PDF文档是否为PDF/A文档的XML数据。
   * 对`Map`对象进行迭代以获得每个生成文档。 然后，将该数组成员的值转换为`BLOB`。
   * 通过访问XML对象的`BLOB`字段提取表示XML数据的二进制数据。 `MTOM`此字段存储可以作为XML文件写入的字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
