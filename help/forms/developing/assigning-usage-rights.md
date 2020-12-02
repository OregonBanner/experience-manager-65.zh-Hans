---
title: 分配使用权限
seo-title: 分配使用权限
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '3895'
ht-degree: 0%

---


# 分配使用权限{#assigning-usage-rights}

## 关于Acrobat Reader DC扩展服务{#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC扩展服务通过扩展Adobe Reader的功能使您的组织能够轻松共享交互式PDF文档。 Acrobat Reader DC扩展服务完全支持任何PDF文档，最高包括PDF 1.7。它可与Adobe Reader7.0及更高版本一起使用。 本服务向PDF文档添加使用权限，激活使用Adobe Reader打开PDF文档时通常不可用的功能。 第三方用户不需要额外的软件或插件即可与启用权限的文档配合使用。

您可以使用Acrobat Reader DC扩展服务完成以下任务:

* 将使用权限应用于PDF文档。 有关信息，请参阅[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 从PDF文档中删除使用权限。 有关信息，请参阅[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 检索凭据详细信息。 有关信息，请参阅[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将使用权限应用于PDF文档{#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC扩展Java客户端API和Web服务将使用权限应用于PDF文档。 使用权限与默认在Acrobat但在Adobe Reader不可用的功能有关，如向表单添加注释或填写表单字段并保存表单的功能。 对其应用了使用权限的PDF文档称为启用权限的文档。 在Adobe Reader打开启用权限的文档的用户可以执行为该特定文档启用的操作。

>[!NOTE]
>
>使用`applyUsageRights`方法（它是Java API的一部分）对PDF文档应用使用权限时，可以将`ReaderExtensionsOptionSpec`对象的`isModeFinal`参数设置为`false`。 这会导致表单处理计数器不被更新，并且性能得到改进。 如果您不担心更新已处理的表单计数器，建议将`isModeFinal`参数设置为`false`。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要对PDF文档应用使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Acrobat Reader DC扩展Client对象。
1. 检索PDF文档。
1. 指定要应用的使用权限。
1. 将使用权限应用于PDF文档。
1. 保存启用权限的PDF文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

要以编程方式执行Acrobat Reader DC扩展服务操作，必须创建Acrobat Reader DC扩展服务客户端对象。 如果您使用Acrobat Reader DC扩展Java API，请创建`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建`ReaderExtensionsServiceService`对象。

**检索PDF文档**

您必须检索PDF文档才能应用使用权限。 支持权限的PDF文档包含使用权限词典。 当Adobe Reader打开包含此类词典的文档时，它将启用字典中指定的仅用于该文档的使用权限。 如果文档不包含使用权词典，Acrobat Reader DC扩展服务将创建一个。 如果它已包含词典，则Acrobat Reader DC扩展服务会用您指定的词典覆盖现有的使用权限。 词典指定启用哪些使用权限。 当用户在Adobe Reader打开文档时，仅允许在词典中指定的使用权限。

**指定要应用的使用权限**

您可以设置的使用权限由您从Adobe Systems Incorporated购买的凭证决定。 凭据通常提供设置一组相关使用权限的权限，如与交互式表单相关的权限。 每个凭据都提供创建特定数量的启用权限的PDF文档的权利。 评估凭据赋予您创建不限数量的草稿文档的权利。

>[!NOTE]
>
>如果尝试分配凭据不允许的使用权，将导致异常。

**将使用权限应用于PDF文档**

要对PDF文档应用使用权限，请引用您用于应用使用权限的凭据的别名(通常在AEM Forms安装过程中会安装凭据)。 此外，还必须指定应用使用权限的PDF文档。 有关配置凭据的信息，请参阅应用程序服务器的安装和部署指南。

**保存启用权限的PDF文档**

在Acrobat Reader DC扩展服务将使用权限应用于PDF文档后，您可以将启用权限的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用Web服务API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速开始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#apply-usage-rights-using-the-java-api}应用使用权限

使用Acrobat Reader DC扩展API(Java)将使用权限应用于PDF文档:

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建一个Acrobat Reader DC扩展Client对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`ReaderExtensionsServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 检索PDF文档。

   * 使用PDF文档的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示PDF的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 指定要应用的使用权限。

   * 使用其构造函数创建一个表示使用权限的`UsageRights`对象。
   * 对于要应用的每个使用权，调用属于`UsageRights`对象的相应方法。 例如，要添加`enableFormFillIn`使用权限，请调用`UsageRights`对象的`enableFormFillIn`方法并传递`true`。 （对要应用的每个使用权限重复此步骤）。

1. 将使用权限应用于PDF文档。

   * 使用`ReaderExtensionsOptionSpec`对象的构造函数创建&lt;a0/>对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。 调用此构造函数时，必须指定以下值：

      * `UsageRights`对象，其中包含要应用于文档的使用权限。
      * 一个字符串值，它指定用户在Adobe Reader7.x中打开启用权限的PDF文档时看到的消息。此消息未在Adobe Reader8.0中显示。
   * 通过调用`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法并传递以下值，将使用权限应用于PDF文档:

      * `com.adobe.idp.Document`对象，其中包含应用了使用权限的PDF文档。
      * 一个字符串值，它指定用于应用使用权限的凭据的别名。
      * 一个字符串值，它指定相应的密码值。 (当前忽略此参数。 您可以传递`null`。)
   * 包含运行时选项的`ReaderExtensionsOptionSpec`对象。

   `applyUsageRights`方法返回一个`com.adobe.idp.Document`对象，该对象包含启用权限的PDF文档。

1. 保存启用权限的PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件（确保使用`applyUsageRights`方法返回的`com.adobe.idp.Document`对象）。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速开始（SOAP模式）：使用Java API应用使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#apply-usage-rights-using-the-web-service-api}应用使用权限

使用Acrobat Reader DC扩展API（Web服务）将使用权限应用于PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建一个Acrobat Reader DC扩展Client对象。

   * 使用其默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储应用了使用权限的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，用流数据填充字节数组。 传递要读取的字节数组、开始位置和流长度。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 指定要应用的使用权限。

   * 使用其构造函数创建一个表示使用权限的`UsageRights`对象。
   * 对于要应用的每个使用权限，将值`true`指定给属于`UsageRights`对象的相应数据成员。 例如，要添加`enableFormFillIn`使用权限，请将`true`分配给`UsageRights`对象的`enableFormFillIn`数据成员。 （对要应用的每个使用权限重复此步骤）。

1. 将使用权限应用于PDF文档。

   * 使用`ReaderExtensionsOptionSpec`对象的构造函数创建&lt;a0/>对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。
   * 将`UsageRights`对象指定给`ReaderExtensionsOptionSpec`对象的`usageRights`数据成员。
   * 为`ReaderExtensionsOptionSpec`对象的`message`文档成员指定一个字符串值，该值指定用户在Adobe Reader打开启用权限的PDF时看到的消息。
   * 通过调用`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法并传递以下值，将使用权限应用于PDF文档:

      * `BLOB`对象，其中包含应用了使用权限的PDF文档。
      * 一个字符串值，它指定用于应用使用权限的凭据的别名。
      * 一个字符串值，它指定相应的密码值。 (当前忽略此参数。 您可以传递`null`。)
   * 包含运行时选项的`ReaderExtensionsOptionSpec`对象。

   `applyUsageRights`方法返回一个`BLOB`对象，该对象包含启用权限的PDF文档。

1. 保存启用权限的PDF文档。

   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示启用权限的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`applyUsageRights`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 从PDF文档{#removing-usage-rights-from-pdf-documents}删除使用权限

您可以从启用权限的文档中删除使用权限。 要对启用权限的PDF文档执行其他AEM Forms操作，还必须从其中删除使用权限。 例如，在设置使用权限之前，您必须对PDF文档进行数字签名（或验证）。 因此，如果要对启用权限的文档执行操作，则必须从PDF文档中删除使用权限，执行其他操作，如对文档进行数字签名，然后重新对文档应用使用权限。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要从启用权限的PDF文档中删除使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Acrobat Reader DC扩展Client对象。
1. 检索启用权限的PDF文档。
1. 从PDF文档中删除使用权限。
1. 保存PDF文档。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

在以编程方式执行Acrobat Reader DC扩展服务操作之前，必须创建Acrobat Reader DC扩展服务客户端对象。 如果您使用Java API，请创建`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建`ReaderExtensionsServiceService`对象。

**检索启用权限的PDF文档**

检索启用权限的PDF文档以删除使用权限。

**从PDF文档中删除使用权限**

检索启用权限的PDF文档后，您可以删除使用权限。 删除使用权限后，在Adobe Reader内查看PDF文档时，将没有任何其他功能。

**保存PDF文档**

可将不再包含使用权限的PDF文档另存为PDF文件。 保存为PDF文件后，可在Adobe Reader或Acrobat查看PDF文档。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速开始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API {#remove-usage-rights-using-the-java-api}删除使用权限

使用Acrobat Reader DC扩展API(Java)从启用权限的PDF文档中删除使用权限：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建一个Acrobat Reader DC扩展Client对象。

   使用`ReaderExtensionsServiceClient`对象的构造函数创建一个`ServiceClientFactory`对象，并传递一个包含连接属性的&lt;a1/>对象。

1. 检索PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定PDF文档位置的字符串值，创建一个&lt;a0/>对象，它表示启用权限的PDF文档。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 从PDF文档中删除使用权限。

   通过调用`ReaderExtensionsServiceClient`对象的`removeUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，从PDF文档中删除使用权限。 此方法返回一个`com.adobe.idp.Document`对象，该对象包含没有使用权限的PDF文档。

1. 将使用权限应用于PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为。PDF。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件（确保使用`removeUsageRights`方法返回的`Document`对象）。

**另请参阅**

[从PDF文档删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速开始（SOAP模式）:使用Java API从PDF文档删除使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#remove-usage-rights-using-the-web-service-api}删除使用权限

使用Acrobat Reader DC扩展API（Web服务）从启用权限的PDF文档中删除使用权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建一个Acrobat Reader DC扩展Client对象。

   * 使用其默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储启用权限的PDF文档，从中删除了使用权限。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 从PDF文档中删除使用权限。

   通过调用`ReaderExtensionsServiceClient`对象的`removeUsageRights`方法并传递包含启用权限的PDF文档的`BLOB`对象，从PDF文档中删除使用权限。 此方法返回一个`BLOB`对象，该对象包含没有使用权限的PDF文档。

1. 将使用权限应用于PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个表示PDF文件位置的字符串值，创建一个&lt;a0/>对象。
   * 创建一个字节数组，用于存储`removeUsageRights`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。

**另请参阅**

[从PDF文档删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检索凭据信息{#retrieving-credential-information}

您可以检索有关用于将使用权限应用于启用权限的PDF文档的凭据的信息。 通过检索有关凭据的信息，您可以获取诸如证书失效日期等信息。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要检索有关用于将使用权限应用于PDF文档的凭据的信息，请执行以下步骤：

1. 包括项目文件。
1. 创建一个Acrobat Reader DC扩展Client对象。
1. 检索启用权限的PDF文档。
1. 检索有关凭据的信息。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

在以编程方式执行Acrobat Reader DC扩展服务操作之前，必须创建Acrobat Reader DC扩展服务客户端对象。 如果您使用Java API，请创建`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建`ReaderExtensionsServiceService`对象。

**检索启用权限的PDF文档**

您必须检索启用权限的PDF文档才能检索有关凭据的信息。 您还可以通过指定凭据的别名来检索有关凭据的信息；但是，如果要检索有关用于将使用权限应用于启用特定权限的PDF文档的凭据的信息，则必须检索该文档。

**检索有关凭据的信息**

在检索启用权限的PDF文档后，您可以获取有关用于向其应用使用权限的凭证的信息。 您可以获取有关凭据的以下信息：

* 在启用权限的PDF文档打开时在Adobe Reader内显示的消息。
* 此凭据失效的日期。
* 此凭据无效的日期。
* 为此启用权限的PDF文档设置的使用权限。
* 凭据的使用次数。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速开始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API {#retrieve-credential-information-using-the-java-api}检索凭据信息

使用Acrobat Reader DC扩展API(Java)检索凭据信息：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建一个Acrobat Reader DC扩展Client对象。

   使用`ReaderExtensionsServiceClient`对象的构造函数创建一个`ServiceClientFactory`对象，并传递一个包含连接属性的&lt;a1/>对象。

1. 检索PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个字符串值，该字符串值指定启用权限的PDF文档的位置，以创建表示启用权限的PDF文档的对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 从PDF文档中删除使用权限。

   * 通过调用`ReaderExtensionsServiceClient`对象的`getDocumentUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，检索有关用于将使用权限应用于PDF文档的凭据的信息。 此方法返回包含凭据信息的`GetUsageRightsResult`对象。
   * 通过调用`GetUsageRightsResult`对象的`getNotAfter`方法检索凭据不再有效的日期。 此方法返回一个`java.util.Date`对象，它表示凭据不再有效的日期。
   * 通过调用`GetUsageRightsResult`对象的`getMessage`方法，检索在Adobe Reader打开启用权限的PDF文档时显示的消息。 此方法返回表示消息的字符串值。

**另请参阅**

[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[快速开始（SOAP模式）:使用Java API检索凭据信息](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#retrieve-credential-information-using-the-web-service-api}检索凭据信息

使用Acrobat Reader DC扩展API（Web服务）检索凭据信息：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建一个Acrobat Reader DC扩展Client对象。

   * 使用其默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储启用权限的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示启用权限的PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 从PDF文档中删除使用权限。

   * 通过调用`ReaderExtensionsServiceClient`对象的`getDocumentUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，检索有关用于将使用权限应用于PDF文档的凭据的信息。 此方法返回包含凭据信息的`GetUsageRightsResult`对象。
   * 获取`GetUsageRightsResult`对象的`notAfter`数据成员的值，检索此凭据不再有效的日期。 此数据成员的数据类型为`System.DateTime`。
   * 通过获取`GetUsageRightsResult`对象的`message`文档成员的值，检索在Adobe Reader打开启用权限的PDF时显示的消息。 此数据成员的数据类型是字符串。
   * 获取`GetUsageRightsResult`对象的`useCount`数据成员的值，检索凭据的使用次数。 此数据成员的数据类型是整数。

**另请参阅**

[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
