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
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 0%

---


# 将文档传递到Forms服务{#passing-documents-to-the-formsservice}

AEM Forms服务向客户端设备（通常是Web浏览器）提供交互式PDF forms，以从用户收集信息。 交互式PDF表单基于表单设计，通常另存为XDP文件并在设计器中创建。 从AEM Forms开始，您可以将包含表单设计的`com.adobe.idp.Document`对象传递给Forms服务。 然后，Forms服务将呈现位于`com.adobe.idp.Document`对象中的表单设计。

将`com.adobe.idp.Document`对象传递到Forms服务的一个优点是其他服务操作返回`com.adobe.idp.Document`实例。 也就是说，您可以从另一个服务操作获取`com.adobe.idp.Document`实例并渲染它。 例如，假定XDP文件存储在名为`/Company Home/Form Designs`的Content Services（已弃用）节点中，如下图所示。

您可以通过编程方式从Content Services（已弃用）（已弃用）检索Loan.xdp，并将XDP文件传递到`com.adobe.idp.Document`对象内的Forms服务。

>[!NOTE]
>
>有关Forms服务的详细信息，请参见[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要将从内容服务（已弃用）获取的文档传递到Forms服务，请执行以下任务:

1. 包括项目文件。
1. 创建一个Forms和一个文档管理客户端API对象。
1. 从Content Services检索表单设计（已弃用）。
1. 渲染交互式PDF表单。
1. 对表单数据流执行操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

**创建Forms和文档管理客户端API对象**

在以编程方式执行Forms服务API操作之前，请创建一个Forms客户端API对象。 此外，由于此工作流从Content Services检索XDP文件（已弃用），因此请创建一个文档管理API对象。

**从Content Services检索表单设计（已弃用）**

使用Java或Web服务API从Content Services检索XDP文件（已弃用）。 XDP文件在`com.adobe.idp.Document`实例（如果您使用Web服务，则返回`BLOB`实例）中。 然后，您可以将`com.adobe.idp.Document`实例传递给Forms服务。

**渲染交互式PDF表单**

要呈现交互式表单，请将从Content Services（已弃用）返回的`com.adobe.idp.Document`实例传递给Forms服务。

>[!NOTE]
>
>您可以将包含表单设计的`com.adobe.idp.Document`传递给Forms服务。 名为`renderPDFForm2`和`renderHTMLForm2`的两种新方法接受包含表单设计的`com.adobe.idp.Document`对象。

**对表单数据流执行操作**

根据客户端应用程序的类型，您可以将表单写入客户端Web浏览器或将表单另存为PDF文件。 基于Web的应用程序通常将表单写入Web浏览器。 但是，桌面应用程序通常将表单另存为PDF文件。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速开始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API {#pass-documents-to-the-forms-service-using-the-java-api}将文档传递给Forms服务

通过使用Forms服务和内容服务（已弃用）API(Java)传递从Content Services（已弃用）获取的文档:

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 创建Forms和文档管理客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用`FormsServiceClient`对象的构造函数创建`ServiceClientFactory`对象。
   * 使用`DocumentManagementServiceClientImpl`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 从Content Services检索表单设计（已弃用）

   调用`DocumentManagementServiceClientImpl`对象的`retrieveContent`方法并传递以下值：

   * 一个字符串值，它指定添加内容的存储。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径（例如，`/Company Home/Form Designs/Loan.xdp`）。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。

   `retrieveContent`方法返回包含XDP文件的`CRCResult`对象。 通过调用`CRCResult`对象的`getDocument`方法获取`com.adobe.idp.Document`实例。

1. 渲染交互式PDF表单

   调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

   * `com.adobe.idp.Document`对象，它包含从Content Services检索的表单设计（已弃用）。
   * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 此值是可选参数，如果不想指定运行时选项，可以指定`null`。
   * 包含URI值的`URLSpec`对象。 此值是可选参数，您可以指定`null`。
   * 存储文件附件的`java.util.HashMap`对象。 此值是可选参数，如果不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含一个必须写入客户端Web浏览器的表单数据流。

1. 对表单数据流执行操作

   * 通过调用`FormsResult`对象“s `getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型，设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法，创建一个字节数组并用表单数据流填充它。 将字节数组作为参数传递。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速开始（SOAP模式）:使用Java API将文档传递到Forms服务](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#pass-documents-to-the-forms-service-using-the-web-service-api}将文档传递给Forms服务

通过使用Forms服务和内容服务（已弃用）API（Web服务）传递从内容服务（已弃用）获取的文档:

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此创建两个服务引用。 将以下WSDL定义用于与Forms服务关联的服务引用：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   对与文档管理服务关联的服务引用使用以下WSDL定义：`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   由于`BLOB`数据类型是两种服务引用的通用类型，因此在使用`BLOB`数据类型时，完全限定该数据类型。 在相应的Web服务快速开始中，所有`BLOB`实例都完全限定。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Forms和文档管理客户端API对象

   * 使用其默认构造函数创建`FormsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/FormsService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`FormsServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`FormsServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`FormsServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >为`DocumentManagementServiceClient`服务客户端重复这些步骤。

1. 从Content Services检索表单设计（已弃用）

   通过调用`DocumentManagementServiceClient`对象的`retrieveContent`方法并传递以下值来检索内容：

   * 一个字符串值，它指定添加内容的存储。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径（例如，`/Company Home/Form Designs/Loan.xdp`）。 此值是必需参数。
   * 指定版本的字符串值。 此值是可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   * 存储浏览链接值的字符串输出参数。
   * 存储内容的`BLOB`输出参数。 您可以使用此输出参数检索内容。
   * 存储内容属性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`输出参数。
   * `CRCResult`输出参数。 您可以使用`BLOB`输出参数来获取内容，而不是使用此对象。

1. 渲染交互式PDF表单

   调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

   * `BLOB`对象，它包含从Content Services检索的表单设计（已弃用）。
   * `BLOB`对象，其中包含要与表单合并的数据。 如果不想合并数据，请传递一个空`BLOB`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 此值是可选参数，如果不想指定运行时选项，可以指定`null`。
   * 包含URI值的`URLSpec`对象。 此值是可选参数，您可以指定`null`。
   * 存储文件附件的`Map`对象。 此值是可选参数，如果不想将文件附加到表单，可以指定`null`。
   * 用于存储页面计数的长输出参数。
   * 用于存储区域设置值的字符串输出参数。
   * 用于存储交互式PDF表单`.`的`FormsResult`输出参数

   `renderPDFForm2`方法返回一个`FormsResult`对象，该对象包含交互式PDF表单。

1. 对表单数据流执行操作

   * 通过获取`FormsResult`对象的`outputContent`字段的值，创建包含表单数据的`BLOB`对象。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，它表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储从`FormsResult`对象检索的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
