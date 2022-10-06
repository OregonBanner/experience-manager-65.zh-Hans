---
title: 分配使用权限
seo-title: Assigning Usage Rights
description: 使用Acrobat Reader DC扩展Java客户端API和Web服务API来应用PDF文档的使用权限，并从中删除这些权限。
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3926'
ht-degree: 0%

---

# 分配使用权限 {#assigning-usage-rights}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

## 关于Acrobat Reader DC扩展服务 {#about-the-acrobat-reader-dc-extensions-service}

通过Acrobat Reader DC扩展服务，您的组织可以通过扩展Adobe Reader的功能轻松共享交互式PDF文档。 Acrobat Reader DC扩展服务完全支持PDF1.7之前（含该版本）的任何PDF文档。它可与Adobe Reader 7.0及更高版本配合使用。 该服务可向PDF文档添加使用权限，从而激活在使用Adobe Reader打开PDF文档时通常不可用的功能。 第三方用户无需使用其他软件或插件即可处理启用了权限的文档。

您可以使用Acrobat Reader DC扩展服务完成以下任务：

* 将使用权限应用于PDF文档。 有关信息，请参阅 [将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).
* 从PDF文档中删除使用权限。 有关信息，请参阅 [从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).
* 检索凭据详细信息。 有关信息，请参阅 [检索凭据信息](assigning-usage-rights.md#retrieving-credential-information).

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 将使用权限应用于PDF文档 {#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC扩展Java客户端API和Web服务将使用权限应用于PDF文档。 使用权限与Acrobat中默认提供但Adobe Reader中不提供的功能有关，例如向表单添加注释或填写表单字段并保存表单的功能。 PDF文档（对其应用了使用权限）称为启用权限的文档。 在Adobe Reader中打开启用了权限的文档的用户可以执行为该特定文档启用的操作。

>[!NOTE]
>
>在使用将使用权限应用于PDF文档时 `applyUsageRights` 方法（Java API的一部分），您可以设置 `isModeFinal` 参数 `ReaderExtensionsOptionSpec` 对象 `false`. 这会导致表单处理计数器不更新，并提高性能。 如果您不关心更新已处理的表单计数器，建议您将 `isModeFinal` 参数 `false`.

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要对PDF文档应用使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索PDF文档。
1. 指定要应用的使用权限。
1. 将使用权限应用于PDF文档。
1. 保存启用权限的PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

要以编程方式执行Acrobat Reader DC扩展服务操作，必须创建Acrobat Reader DC扩展服务客户端对象。 如果您使用的是Acrobat Reader DC扩展Java API，请创建 `ReaderExtensionsServiceClient` 对象。 如果您使用的是Acrobat Reader DC扩展Web服务API，请创建 `ReaderExtensionsServiceService` 对象。

**检索PDF文档**

必须检索PDF文档才能应用使用权限。 启用权限的PDF文档包含使用权限字典。 当Adobe Reader打开包含此类词典的文档时，它将仅启用该文档在词典中指定的使用权限。 如果文档不包含使用权限词典，则Acrobat Reader DC扩展服务将创建一个。 如果Acrobat Reader DC扩展服务已包含词典，则它将使用您指定的使用权限覆盖现有的使用权限。 词典指定启用的使用权限。 当用户在Adobe Reader中打开文档时，只允许使用词典中指定的使用权限。

**指定要应用的使用权限**

您可以设置的使用权限取决于您从Adobe Systems Incorporated购买的凭据。 凭据通常提供设置一组相关使用权限的权限，例如与交互式表单相关的使用权限。 每个凭据都提供创建一定数量的启用权限的PDF文档的权限。 评估凭据赋予创建无限数量的草稿文档的权利。

>[!NOTE]
>
>如果您尝试分配凭据不允许的使用权限，则会引发异常。

**将使用权限应用于PDF文档**

要将使用权限应用于PDF文档，请引用用于应用使用权限的凭据的别名(通常在AEM Forms安装期间安装凭据)。 此外，您还必须指定将使用权限应用到的PDF文档。 有关配置凭据的信息，请参阅应用程序服务器的安装和部署指南。

**保存启用权限的PDF文档**

在Acrobat Reader DC扩展服务将使用权限应用于PDF文档后，您可以将启用权限的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用Web服务API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API应用使用权限 {#apply-usage-rights-using-the-java-api}

使用Acrobat Reader DC扩展API(Java)将使用权限应用于PDF文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `ReaderExtensionsServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 检索PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象使用其构造函数并传递指定PDF文档位置的字符串值来表示PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 指定要应用的使用权限。

   * 创建 `UsageRights` 使用其构造函数表示使用权限的对象。
   * 对于要应用的每个使用权，调用属于 `UsageRights` 对象。 例如，要将 `enableFormFillIn` 使用权，调用 `UsageRights` 对象 `enableFormFillIn` 方法和传递 `true`. （对要应用的每个使用权限重复此步骤）。

1. 将使用权限应用于PDF文档。

   * 创建 `ReaderExtensionsOptionSpec` 对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。 调用此构造函数时，必须指定以下值：

      * 的 `UsageRights` 包含要应用于文档的使用权限的对象。
      * 一个字符串值，用于指定在Adobe Reader 7.x中打开启用了权限的PDF文档时用户看到的消息。此消息未显示在Adobe Reader 8.0中。
   * 通过调用 `ReaderExtensionsServiceClient` 对象 `applyUsageRights` 方法和传递以下值：

      * 的 `com.adobe.idp.Document` 对象，其中包含应用了使用权限的PDF文档。
      * 一个字符串值，用于指定用于应用使用权限的凭据的别名。
      * 指定相应密码值的字符串值。 (当前，此参数被忽略。 您可以通过 `null`.)
   * 的 `ReaderExtensionsOptionSpec` 包含运行时选项的对象。

   的 `applyUsageRights` 方法返回 `com.adobe.idp.Document` 包含启用权限的PDF文档的对象。

1. 保存启用权限的PDF文档。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象到文件(确保使用 `com.adobe.idp.Document` 由返回的对象 `applyUsageRights` 方法)。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入门（SOAP模式）：使用Java API应用使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API应用使用权限 {#apply-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务）将使用权限应用于PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 创建 `ReaderExtensionsServiceClient` 对象。
   * 创建 `ReaderExtensionsServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 确保指定 `?blob=mtom`.)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `ReaderExtensionsServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储应用了使用权限的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法。 传递字节数组、开始位置和流长度以读取。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 指定要应用的使用权限。

   * 创建 `UsageRights` 使用其构造函数表示使用权限的对象。
   * 对于要应用的每个使用权限，分配值 `true` 到属于的相应数据成员 `UsageRights` 对象。 例如，要将 `enableFormFillIn` 使用权限，分配 `true` 到 `UsageRights` 对象 `enableFormFillIn` 数据成员。 （对要应用的每个使用权限重复此步骤）。

1. 将使用权限应用于PDF文档。

   * 创建 `ReaderExtensionsOptionSpec` 对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。
   * 分配 `UsageRights` 对象 `ReaderExtensionsOptionSpec` 对象 `usageRights` 数据成员。
   * 为分配一个字符串值，以指定在Adobe Reader中打开启用了权限的PDF文档时用户看到的消息，并将该消息分配给 `ReaderExtensionsOptionSpec` 对象 `message` 数据成员。
   * 通过调用 `ReaderExtensionsServiceClient` 对象 `applyUsageRights` 方法和传递以下值：

      * 的 `BLOB` 对象，其中包含应用了使用权限的PDF文档。
      * 一个字符串值，用于指定用于应用使用权限的凭据的别名。
      * 指定相应密码值的字符串值。 (当前，此参数被忽略。 您可以通过 `null`.)
   * 的 `ReaderExtensionsOptionSpec` 包含运行时选项的对象。

   的 `applyUsageRights` 方法返回 `BLOB` 包含启用权限的PDF文档的对象。

1. 保存启用权限的PDF文档。

   * 创建 `System.IO.FileStream` 对象。 传递表示启用权限的PDF文档的文件位置的字符串值。
   * 创建用于存储 `BLOB` 由返回的对象 `applyUsageRights` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 从PDF文档中删除使用权限 {#removing-usage-rights-from-pdf-documents}

您可以从启用了权限的文档中删除使用权限。 要对启用了权限的PDF文档执行其他AEM Forms操作，还需要从该文档中删除使用权限。 例如，在设置使用权限之前，您必须对PDF文档进行数字签名（或验证）。 因此，如果要对启用权限的文档执行操作，则必须从PDF文档中删除使用权限，执行其他操作（如对文档进行数字签名），然后对文档重新应用使用权限。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要从启用权限的PDF文档中删除使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索启用权限的PDF文档。
1. 从PDF文档中删除使用权限。
1. 保存PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

要以编程方式执行Acrobat Reader DC扩展服务操作，必须先创建Acrobat Reader DC扩展服务客户端对象。 如果您使用的是Java API，请创建 `ReaderExtensionsServiceClient` 对象。 如果您使用的是Acrobat Reader DC扩展Web服务API，请创建 `ReaderExtensionsServiceService` 对象。

**检索启用权限的PDF文档**

检索启用权限的PDF文档，以删除使用权限。

**从PDF文档中删除使用权限**

在检索启用了权限的PDF文档后，您可以删除使用权限。 删除使用权限后，在Adobe Reader中查看PDF文档时，该文档将没有任何其他功能。

**保存PDF文档**

可以将不再包含使用权限的PDF文档另存为PDF文件。 保存为PDF文件后，即可在Adobe Reader或Acrobat中查看PDF文档。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API删除使用权限 {#remove-usage-rights-using-the-java-api}

使用Acrobat Reader DC扩展API(Java)从启用了权限的PDF文档中删除使用权限：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建Acrobat Reader DC扩展客户端对象。

   创建 `ReaderExtensionsServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 包含连接属性的对象。

1. 检索PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象通过使用其构造函数并传递指定PDF文档位置的字符串值来表示启用权限的PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 从PDF文档中删除使用权限。

   通过调用 `ReaderExtensionsServiceClient` 对象 `removeUsageRights` 方法和通过 `com.adobe.idp.Document` 包含启用权限的PDF文档的对象。 此方法将返回 `com.adobe.idp.Document` 对象，其中包含没有使用权限的PDF文档。

1. 将使用权限应用于PDF文档。

   * 创建 `java.io.File` 对象，并确保文件扩展名为。PDF。
   * 调用 `Document` 对象 `copyToFile` 复制内容的方法 `Document` 对象到文件(确保使用 `Document` 由返回的对象 `removeUsageRights` 方法)。

**另请参阅**

[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入门（SOAP模式）：使用Java API从PDF文档中删除使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除使用权限 {#remove-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务）从启用了权限的PDF文档中删除使用权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 创建 `ReaderExtensionsServiceClient` 对象。
   * 创建 `ReaderExtensionsServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 确保指定 `?blob=mtom`.)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `ReaderExtensionsServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储启用权限的PDF文档，从中删除了使用权限。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 从PDF文档中删除使用权限。

   通过调用 `ReaderExtensionsServiceClient` 对象 `removeUsageRights` 方法和通过 `BLOB` 包含启用权限的PDF文档的对象。 此方法将返回 `BLOB` 对象，其中包含没有使用权限的PDF文档。

1. 将使用权限应用于PDF文档。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递表示PDF文件位置的字符串值。
   * 创建用于存储 `BLOB` 由返回的对象 `removeUsageRights` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。

**另请参阅**

[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检索凭据信息 {#retrieving-credential-information}

您可以检索有关用于将使用权限应用到启用权限的PDF文档的凭据的信息。 通过检索有关凭据的信息，您可以获取诸如证书失效日期之类的信息。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-2}

要检索有关用于将使用权限应用于PDF文档的凭据的信息，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索启用权限的PDF文档。
1. 检索有关凭据的信息。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

要以编程方式执行Acrobat Reader DC扩展服务操作，必须先创建Acrobat Reader DC扩展服务客户端对象。 如果您使用的是Java API，请创建 `ReaderExtensionsServiceClient` 对象。 如果您使用的是Acrobat Reader DC扩展Web服务API，请创建 `ReaderExtensionsServiceService` 对象。

**检索启用权限的PDF文档**

必须检索启用权限的PDF文档，才能检索有关凭据的信息。 您还可以通过指定凭据的别名来检索有关凭据的信息；但是，如果要检索有关用于将使用权限应用于启用特定权限的PDF文档的凭据的信息，则必须检索该文档。

**检索有关凭据的信息**

在检索启用了权限的PDF文档后，您可以获取有关用于向其应用使用权限的凭据的信息。 您可以获取有关凭据的以下信息：

* 打开启用了权限的PDF文档时，在Adobe Reader中显示的消息。
* 凭据失效的日期。
* 凭据无效的日期。
* 为此启用权限的PDF文档设置的使用权限。
* 已使用凭据的次数。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API检索凭据信息 {#retrieve-credential-information-using-the-java-api}

使用Acrobat Reader DC扩展API(Java)检索凭据信息：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-reader-extensions-client.jar。

1. 创建Acrobat Reader DC扩展客户端对象。

   创建 `ReaderExtensionsServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 包含连接属性的对象。

1. 检索PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象通过使用其构造函数并传递一个字符串值来表示启用权限的PDF文档，该字符串值指定启用权限的PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 从PDF文档中删除使用权限。

   * 通过调用 `ReaderExtensionsServiceClient` 对象 `getDocumentUsageRights` 方法和通过 `com.adobe.idp.Document` 包含启用权限的PDF文档的对象。 此方法将返回 `GetUsageRightsResult` 包含凭据信息的对象。
   * 通过调用 `GetUsageRightsResult` 对象 `getNotAfter` 方法。 此方法将返回 `java.util.Date` 表示凭据失效日期的对象。
   * 通过调用 `GetUsageRightsResult` 对象 `getMessage` 方法。 此方法会返回表示消息的字符串值。

**另请参阅**

[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[快速入门（SOAP模式）：使用Java API检索凭据信息](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索凭据信息 {#retrieve-credential-information-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务）检索凭据信息：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 创建 `ReaderExtensionsServiceClient` 对象。
   * 创建 `ReaderExtensionsServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`. 确保指定 `?blob=mtom`.)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `ReaderExtensionsServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 检索PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储启用权限的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示启用权限的PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 从PDF文档中删除使用权限。

   * 通过调用 `ReaderExtensionsServiceClient` 对象 `getDocumentUsageRights` 方法和通过 `com.adobe.idp.Document` 包含启用权限的PDF文档的对象。 此方法将返回 `GetUsageRightsResult` 包含凭据信息的对象。
   * 通过获取 `GetUsageRightsResult` 对象 `notAfter` 数据成员。 此数据成员的数据类型为 `System.DateTime`.
   * 通过获取的值，检索在Adobe Reader中打开启用权限的PDF文档时显示的消息 `GetUsageRightsResult` 对象 `message` 数据成员。 此数据成员的数据类型是字符串。
   * 通过获取 `GetUsageRightsResult` 对象 `useCount` 数据成员。 此数据成员的数据类型是整数。

**另请参阅**

[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
