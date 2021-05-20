---
title: 使用Bates编号组合文档
seo-title: 使用Bates编号组合文档
description: '使用Bates编号来使用Java和Web服务API来组合PDF文档。 '
seo-description: '使用Bates编号来使用Java和Web服务API来组合PDF文档。 '
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
source-wordcount: '1941'
ht-degree: 0%

---

# 使用Bates编号{#assembling-documents-using-bates-numbering}组合文档

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以使用Bates编号来组合包含唯一页面标识符的PDF文档。 *Bates编* 号是对一批相关文档应用唯一标识的方法。文档（或文档集）中的每个页面都会分配一个唯一标识该页面的Bates编号。 例如，包含物料清单信息并与组件生产相关联的制造文档可以包含标识符。 Bates编号包含按顺序递增的数值以及可选前缀和后缀。 前缀+数字+后缀称为&#x200B;*bates模式*。

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

此DDX文档将名为&#x200B;*map.pdf*&#x200B;和&#x200B;*directions.pdf*&#x200B;的两个PDF文档合并到一个PDF文档中。 生成的PDF文档包含包含唯一页面标识符的标题。 例如，上图中的文档显示000016。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 本节不讨论这些概念，例如创建包含输入文档的集合对象，或从返回的集合对象中提取结果。 （请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要组合包含唯一页面标识符（Bates编号）的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 参考输入PDF文档。
1. 设置初始Bates编号值。
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

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 例如，以本节中引入的DDX文档为例。 要组合包含唯一页面标识符的PDF文档，DDX文档必须包含`BatesNumber`元素。

**参考输入PDF文档**

必须引用输入PDF文档来组合PDF文档。 例如，必须引用map.pdf和directions.pdf文档，才能将这些PDF文档组合为一个PDF文档。

**设置初始Bates编号值**

您可以设置初始Bates编号值以满足您的业务要求。 例如，假定需要将初始值设置为000100。 如果不设置初始值，则第一页的值为000000。

**组合输入的PDF文档**

在创建汇编程序服务客户端后，引用包含`BatesNumber`元素信息的DDX文档，引用输入的PDF文档，并设置运行时选项，您可以调用`invokeDDX`操作，该操作会导致汇编程序服务汇编包含唯一页面标识符的PDF文档。

**提取结果**

汇编程序服务返回包含作业结果的集合对象。 您可以提取生成的PDF文档以及引发的任何例外。 在这种情况下，加密的PDF文档位于收藏对象中。

>[!NOTE]
>
>如果调用`invokeDDX`操作，则返回集合对象。 在将两个或更多输入的PDF文档传递到汇编程序服务时，会使用此操作。 但是，如果只将一个输入的PDF文档传递到汇编程序服务，则应调用`invokeOneDocument`操作。 有关使用此操作的信息，请参阅[组装加密的PDF文档](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-documents-with-bates-numbering-using-the-java-api}组合带有Bates编号的文档

使用汇编程序服务API(Java)汇编使用唯一页面标识符（Bates编号）的PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 参考输入PDF文档。

   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 对于每个输入PDF文档，使用其构造函数创建一个`java.io.FileInputStream`对象，并传递输入PDF文档的位置。 在这种情况下，请传递不安全的PDF文档的位置。
   * 对于每个输入的PDF文档，创建一个`com.adobe.idp.Document`对象，并传递包含该PDF文档的`java.io.FileInputStream`对象。
   * 通过调用`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。 例如，本节中引入的DDX文档中指定的PDF源文件的名称为Loan.pdf。
      * `com.adobe.idp.Document`对象，其中包含不安全的PDF文档。

1. 设置初始Bates编号值。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过调用`AssemblerOptionSpec`对象的`setFirstBatesNumber`并传递指定初始值的数值来设置初始Bates编号。

1. 组合输入的PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。
   * `java.util.Map`对象，其中包含输入不安全的PDF文件。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，用于指定运行时选项，包括默认字体和作业日志级别。

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，该对象包含密码加密的PDF文档。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此操作会返回`java.util.Map`对象。
   * 遍历`java.util.Map`对象，直到找到`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDF文档。

**另请参阅**

[快速入门（SOAP模式）：使用Java API将PDF文档与Bates编号拼合在一起](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#assemble-documents-with-bates-numbering-using-the-web-service-api}组合带有Bates编号的文档

使用汇编程序服务API（Web服务）汇编使用唯一页面标识符（Bates编号）的PDF文档：

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
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式，可创建对象。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 参考输入PDF文档。

   * 对于每个输入PDF文档，请使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此收集对象用于存储输入的PDF文档。
   * 对于每个输入的PDF文档，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。 例如，如果使用两个输入PDF文档，则创建两个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 为`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段分配表示键名称的字符串值。 此值必须匹配DDX文档中指定的PDF源元素的值。 （对每个输入的PDF文档执行此任务。）
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 （对每个输入的PDF文档执行此任务。）
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 （对每个输入的PDF文档执行此任务。）

1. 设置初始Bates编号值。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的`firstBatesNumber`数据成员分配一个数值来设置初始Bates编号。

1. 组合输入的PDF文档。

   调用`AssemblerServiceClient`对象的`invoke`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 包含输入PDF文档的`MyMapOf_xsd_string_To_xsd_anyType`对象。 其键必须与PDF源文件的名称匹配，其值必须是与这些文件对应的`BLOB`对象。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invoke`方法会返回一个`AssemblerResult`对象，其中包含作业的结果以及发生的任何异常。

1. 提取结果。

   要获取新创建的PDF文档，请执行以下操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含结果PDF文档的`Map`对象。
   * 遍历`Map`对象，直到找到与生成文档的名称匹配的键。 然后，将该阵列成员的`value`转换为`BLOB`。
   * 通过访问PDF文档的`BLOB`对象的`MTOM`属性，提取表示该文档的二进制数据。 这会返回一个字节数组，您可以将其写出到PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
