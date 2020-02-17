---
title: 将文档传递到FormsService
seo-title: 将文档传递到FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 将文档传递到Forms服务 {#passing-documents-to-the-formsservice}

AEM Forms服务将交互式PDF表单呈现到客户端设备（通常是Web浏览器），以收集用户的信息。 交互式PDF表单基于表单设计，通常另存为XDP文件并在Designer中创建。 从AEM Forms开始，您可以将包含表 `com.adobe.idp.Document` 单设计的对象传递给Forms服务。 然后，表单服务将呈现位于对象中的表单 `com.adobe.idp.Document` 设计。

将对象传递到Forms服 `com.adobe.idp.Document` 务的一个优点是其他服务操作会返回一个 `com.adobe.idp.Document` 实例。 即，您可以从其他服务操 `com.adobe.idp.Document` 作获取实例并渲染它。 例如，假定XDP文件存储在名为的Content Services（已弃用）节点中， `/Company Home/Form Designs`如下图所示。

您可以从Content Services（已弃用）（已弃用）以编程方式检索Loan.xdp，并将XDP文件传递到对象中的Forms服 `com.adobe.idp.Document` 务。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要将从Content Services（已弃用）（已弃用）获取的文档传递到Forms服务，请执行以下任务：

1. 包括项目文件。
1. 创建表单和文档管理客户端API对象。
1. 从Content Services（已弃用）检索表单设计。
1. 渲染交互式PDF表单。
1. 对表单数据流执行操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建表单和文档管理客户端API对象**

在以编程方式执行Forms服务API操作之前，请先创建Forms Client API对象。 此外，由于此工作流从Content Services（已弃用）检索XDP文件，因此请创建一个Document Management API对象。

**从Content services检索表单设计（已弃用）**

使用Java或Web服务API从Content Services（已弃用）检索XDP文件。 XDP文件在实例(或 `com.adobe.idp.Document` 在使用Web `BLOB` 服务时的实例)中返回。 然后，您可以将该 `com.adobe.idp.Document` 实例传递给Forms服务。

**渲染交互式PDF表单**

要渲染交互式表单，请将 `com.adobe.idp.Document` 从Content Services（已弃用）返回的实例传递给Forms服务。

>[!NOTE]
>
>可以将包含表 `com.adobe.idp.Document` 单设计的表单传递给表单服务。 命名并接受包 `renderPDFForm2` 含表 `renderHTMLForm2` 单设计 `com.adobe.idp.Document` 的对象的两种新方法。

**使用表单数据流执行操作**

根据客户端应用程序的类型，您可以将表单写入客户端Web浏览器或将表单另存为PDF文件。 基于Web的应用程序通常将表单写入Web浏览器。 但是，桌面应用程序通常将表单另存为PDF文件。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API将文档传递到Forms Service {#pass-documents-to-the-forms-service-using-the-java-api}

通过使用Forms服务和Content Services（已弃用）API(Java)传递从Content Services（已弃用）获取的文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 创建表单和文档管理客户端API对象

   * 创建包 `ServiceClientFactory` 含连接属性的对象。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `DocumentManagementServiceClientImpl` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 从Content services检索表单设计（已弃用）

   调用对 `DocumentManagementServiceClientImpl` 象的方 `retrieveContent` 法并传递以下值：

   * 一个字符串值，它指定添加内容的商店。 默认存储为 `SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   该方 `retrieveContent` 法返回包 `CRCResult` 含XDP文件的对象。 通过 `com.adobe.idp.Document` 调用对象的方 `CRCResult` 法获取实 `getDocument` 例。

1. 渲染交互式PDF表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm2` 法并传递以下值：

   * 包含 `com.adobe.idp.Document` 从Content Services（已弃用）检索的表单设计的对象。
   * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `com.adobe.idp.Document` 象。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 此值是可选参数，您可以指 `null` 定是否不想指定运行时选项。
   * 包 `URLSpec` 含URI值的对象。 此值是可选参数，您可以指定 `null`。
   * 存储 `java.util.HashMap` 文件附件的对象。 此值是可选参数，您可以指 `null` 定是否不想将文件附加到表单。
   该方 `renderPDFForm` 法返回一个对 `FormsResult` 象，该对象包含必须写入客户端Web浏览器的表单数据流。

1. 使用表单数据流执行操作

   * 通过 `com.adobe.idp.Document` 调用对象的方 `FormsResult` 法创建对 `getOutputContent` 象。
   * 通过调用对象的方 `com.adobe.idp.Document` 法获取对象的内容 `getContentType` 类型。
   * 通过调 `javax.servlet.http.HttpServletResponse` 用对象的方法并传递对象的 `setContentType` 内容类型来设置对象的内容 `com.adobe.idp.Document` 类型。
   * 创建一 `javax.servlet.ServletOutputStream` 个对象，该对象通过调用该对象的方法将表单数据流写入客户端Web `javax.servlet.http.HttpServletResponse` 浏览器 `getOutputStream` 中。
   * 通过 `java.io.InputStream` 调用对象的方 `com.adobe.idp.Document` 法创建对 `getInputStream` 象。
   * 创建一个字节数组，并通过调用对象的方法用表单数据 `InputStream` 流填充该数 `read` 组。 将字节数组作为参数传递。
   * 调用对 `javax.servlet.ServletOutputStream` 象的方 `write` 法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给该 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）:使用Java API将文档传递到Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将文档传递到Forms Service {#pass-documents-to-the-forms-service-using-the-web-service-api}

通过使用Forms服务和Content Services（已弃用）API（Web服务）传递从Content Services（已弃用）获取的文档：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 对于与Forms服务关联的服务引用，请使用以下WSDL定义： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   对与文档管理服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   由于两 `BLOB` 种服务引用都使用数据类型，因此在使用数据类 `BLOB` 型时完全限定数据类型。 在相应的Web服务快速启动中，所有实 `BLOB` 例都完全限定。

   >[!NOTE]
   >
   >替 `localhost`换为承载AEM Forms的服务器的IP地址。

1. 创建表单和文档管理客户端API对象

   * 使用对 `FormsServiceClient` 象的默认构造函数创建对象。
   * 使用构 `FormsServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/FormsService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `FormsServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `FormsServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。
   >[!NOTE]
   >
   >为服务客户端重复 `DocumentManagementServiceClient`这些步骤。

1. 从Content services检索表单设计（已弃用）

   通过调用对象的方 `DocumentManagementServiceClient` 法并传递以 `retrieveContent` 下值来检索内容：

   * 一个字符串值，它指定添加内容的商店。 默认存储为 `SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径(例如， `/Company Home/Form Designs/Loan.xdp`)。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   * 存储浏览链接值的字符串输出参数。
   * 存储 `BLOB` 内容的输出参数。 您可以使用此输出参数检索内容。
   * 存储 `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 内容属性的输出参数。
   * 输出 `CRCResult` 参数。 您可以使用output参数来获取内容，而 `BLOB` 不是使用此对象。

1. 渲染交互式PDF表单

   调用对 `FormsServiceClient` 象的方 `renderPDFForm2` 法并传递以下值：

   * 包含 `BLOB` 从Content Services（已弃用）检索的表单设计的对象。
   * 包含 `BLOB` 要与表单合并的数据的对象。 如果不想合并数据，请传递空对 `BLOB` 象。
   * 存 `PDFFormRenderSpec` 储运行时选项的对象。 此值是可选参数，您可以指 `null` 定是否不想指定运行时选项。
   * 包 `URLSpec` 含URI值的对象。 此值是可选参数，您可以指定 `null`。
   * 存储 `Map` 文件附件的对象。 此值是可选参数，您可以指 `null` 定是否不想将文件附加到表单。
   * 用于存储页数的长输出参数。
   * 用于存储区域设置值的字符串输出参数。
   * 用于 `FormsResult` 存储交互式PDF表单的输出参数 `.`
   该方 `renderPDFForm2` 法返回一个 `FormsResult` 包含交互式PDF表单的对象。

1. 使用表单数据流执行操作

   * 通过获 `BLOB` 取对象字段的值，创建包含表单 `FormsResult` 数据的对 `outputContent` 象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储从对象检 `BLOB` 索到的对象的内 `FormsResult` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
