---
title: 使用PDF实用程序
seo-title: 使用PDF实用程序
description: 使用“PDF实用程序”服务在PDF和XDP文件格式之间进行转换，设置和检索PDF文档属性，以及处理XMP元数据。
seo-description: 使用“PDF实用程序”服务在PDF和XDP文件格式之间进行转换，设置和检索PDF文档属性，以及处理XMP元数据。
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2606'
ht-degree: 1%

---

# 使用PDF实用程序{#working-with-pdf-utilities}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于PDF实用程序服务**

“PDF实用程序”服务可以在PDF和XDP文件格式之间进行转换，设置和检索PDF文档属性，以及处理XMP元数据。 例如，在将PDF文档转换为其他格式之前，检查其属性以确定要为转换调用的服务操作非常有用。

您可以使用PDF实用程序服务完成以下任务：

* 将PDF文档转换为XDP文档。
* 将XDP文档转换为PDF文档。 （请参阅[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。）
* 检索PDF文档属性。 （请参阅[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)。）
* 保存PDF文档并对其进行优化，以便快速查看Web文档。 （请参阅[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)。）

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PDF文档转换为XDP文档{#converting-pdf-documents-into-xdp-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要将PDF文档转换为XDP文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用PDF到XDP的转换操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行PDF实用程序操作之前，必须创建PDFUtilityService客户端。 使用Java API，可通过创建`PDFUtilityServiceClient`对象来完成此操作。 使用Web服务API，可使用`PDFUtilityServiceService`对象来实现此目的。

**调用PDF到XDP的转换操作**

创建服务客户端后，可以调用PDF到XDP的转换操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}将PDF文档转换为XDP文档

使用PDF实用程序API(Java)将PDF文档转换为XDP文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用其构造函数创建`PDFUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用PDF到XDP的转换操作

   要执行转换，请调用`PDFUtilityServiceClient`对象的`convertPDFtoXDP`方法，并传入表示PDF文件的`com.adobe.idp.Document`对象。 方法会返回一个`com.adobe.idp.Document`对象，该对象表示新创建的XDP文件。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}将PDF文档转换为XDP文档

使用PDF实用程序API（Web服务）将PDF文档转换为XDP文档：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代理类构造函数创建`PDFUtilityServiceService`对象。

1. 调用PDF到XDP的转换操作

   调用`PDFUtilityServiceService`对象的`convertPDFtoXDP`方法，并在表示PDF文件的`BLOB`对象中传递。 方法会返回一个`BLOB`对象，该对象表示新创建的XDP文件。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 将XDP文档转换为PDF文档{#converting-xdp-documents-into-pdf-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将XDP文档转换为PDF文档。

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

要将XDP文档转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用XDP到PDF的转换操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行PDF实用程序操作之前，必须创建PDFUtilityService客户端。 使用Java API，可通过创建`PDFUtilityServiceClient`对象来完成此操作。 使用Web服务API，可使用`PDFUtilityServiceService`对象来实现此目的。

**调用XDP到PDF的转换操作**

创建服务客户端后，可以调用XDP到PDF的转换操作。

**另请参阅**

[使用Java API将XDP文档转换为PDF文档](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服务API将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#convert-xdp-documents-into-pdf-documents-using-the-java-api}将XDP文档转换为PDF文档

使用PDF实用程序API(Java)将XDP文档转换为PDF文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用其构造函数创建`PDFUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用XDP到PDF的转换操作

   要执行转换，请调用`PDFUtilityServiceClient`对象的`convertXDPtoPDF`方法，并传入表示XDP文件的`com.adobe.idp.Document`对象。 方法会返回一个`com.adobe.idp.Document`对象，该对象表示新创建的PDF文件。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}将XDP文档转换为PDF文档

使用PDF实用程序API（Web服务API）将XDP文档转换为PDF文档：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代理类构造函数创建`PDFUtilityServiceService`对象。

1. 调用XDP到PDF的转换操作

   要执行转换，请调用`PDFUtilityServiceService`对象的`convertXDPtoPDF`方法，并传入表示XDP文件的`BLOB`对象。 方法会返回一个`BLOB`对象，该对象表示新创建的PDF文件。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 检索PDF文档属性{#retrieving-pdf-document-properties}

您可以使用PDF实用程序Java和Web服务API以编程方式检索PDF文档属性，例如文档是可填写表单还是读取文档所需的最低Acrobat版本。

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤{#summary_of_steps-2}的摘要

要检索PDF文档属性，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用属性检索操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行PDF实用程序操作之前，必须创建PDFUtilityService客户端。 使用Java API，可通过创建`PDFUtilityServiceClient`对象来完成此操作。 使用Web服务API，可使用`PDFUtilityServiceService`对象来实现此目的。

**调用属性检索操作**

创建服务客户端后，可以调用属性检索操作。

**另请参阅**

[使用Java API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服务API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#retrieve-pdf-document-properties-using-the-java-api}检索PDF文档属性

使用PDF实用程序API(Java)检索PDF文档属性：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用其构造函数创建`PDFUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用属性检索操作

   要执行转换，请调用`PDFUtilityServiceClient`对象的`getPDFProperties`方法，并传入以下代码：

   * 表示PDF文档的`com.adobe.idp.Document`对象。
   * `PDFPropertiesOptionSpec`对象，其中包含要评估的属性。

   方法会返回一个`PDFPropertiesResult`对象，其中包含查询结果。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#retrieve-pdf-document-properties-using-the-web-service-api}检索PDF文档属性

使用PDF实用工具Web服务API检索PDF文档属性：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代理类构造函数创建`PDFUtilityServiceService`对象。

1. 调用属性检索操作

   要执行转换，请调用`PDFUtilityServiceService`对象的`getPDFProperties`方法，并传入以下代码：

   * 表示PDF文档的`BLOB`对象。
   * `PDFPropertiesOptionSpec`对象，其中包含要评估的属性。

   方法会返回一个`PDFPropertiesResult`对象，其中包含查询结果。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 设置PDF文档保存模式{#setting-pdf-document-save-modes}

您可以使用PDF实用程序服务Java和Web服务API以编程方式设置PDF文档的保存模式。 使用“PDF实用程序”服务设置保存模式时，“PDF实用程序”服务仅设置保存模式，而不会实际保存PDF文档。 当PDF文档被传递到其他服务操作时，将保存该文档。 例如，您可以使用“PDF实用程序”服务设置特定的保存模式，并将其传递到“加密”服务，在该服务中，PDF文档实际上会被保存和加密。

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-3}的摘要

要设置PDF文档的保存选项，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 设置保存模式。
1. 调用保存操作。
1. 将PDF文档传递到其他操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行PDF实用程序操作之前，必须创建PDFUtilityService客户端。 使用Java API，可通过创建`PDFUtilityServiceClient`对象来完成此操作。 使用Web服务API，可使用`PDFUtilityServiceService`对象来实现此目的。

**设置保存模式**

您可以选择以下保存选项之一：

* `INCREMENTAL`:以增量方式节省，以缩短节省所需的时间
* `FAST_WEB_VIEW`:保存以快速查看web
* `FULL`:使用完全保存进行保存（无优化）

**调用保存样式操作**

创建服务客户端后，可以调用属性检索操作。

**将PDF文档传递到另一个AEM Forms操作**

在“PDF实用程序”服务设置指定的保存模式后，将PDF文档传递到另一个AEM Forms操作。 从该操作返回后，PDF文档将以指定的模式保存。 例如，如果您使用PDF实用程序服务设置`FAST_WEB_VIEW`模式，然后将PDF文档传递到加密服务的`encryptUsingPassword`操作，则返回的PDF文档将使用密码进行加密并保存在`FAST_WEB_VIEW`模式下。

>[!NOTE]
>
>与此部分关联的快速入门设置`FAST_WEB_VIEW`模式，然后将PDF文档传递到加密服务的`encryptUsingPassword`操作。

**另请参阅**

[使用Java API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服务API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#set-pdf-document-save-options-using-the-java-api}设置PDF文档保存选项

使用PDF实用程序API(Java)设置PDF文档保存选项：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用其构造函数创建`PDFUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 设置保存模式

   * 使用`PDFUtilitySaveMode`对象的构造函数创建对象。
   * 通过调用`PDFUtilitySaveMode`对象的`setSaveStyle`方法并传递指定保存模式的字符串值来设置保存模式。 例如，要保存以便快速查看Web，请传递`FAST_WEB_VIEW`。

1. 调用保存样式操作

   调用`PDFUtilityServiceClient`对象的`setSaveMode`方法并传递以下值：

   * 表示PDF文档的`com.adobe.idp.Document`对象。
   * `PDFUtilitySaveMode`对象，其中包含要使用的保存样式。
   * 一个布尔值，用于确定是否覆盖以前的任何设置。

   方法会返回使用指定的保存样式格式化的`com.adobe.idp.Document`对象。

1. 将PDF文档传递到另一个AEM Forms操作

   * 将返回的`com.adobe.idp.Document`对象传递到另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#set-pdf-document-save-options-using-the-web-service-api}设置PDF文档保存选项

使用“PDF实用程序AP”（Web服务）设置PDF文档保存选项：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代理类构造函数创建`PDFUtilityServiceService`对象。

1. 设置保存模式

   * 使用`PDFUtilitySaveMode`对象的构造函数创建对象。
   * 通过为`PDFUtilitySaveMode`对象的`saveStyle`方法分配字符串值来设置保存模式，该方法指定保存模式。 例如，要保存以便快速查看Web，请指定`FAST_WEB_VIEW`。

1. 调用保存样式操作

   调用`PDFUtilityServiceService`对象的`setSaveMode`方法并传递以下值：

   * 表示PDF文档的`BLOB`对象。
   * `PDFUtilitySaveMode`对象，其中包含要使用的保存样式。
   * 一个布尔值，用于确定是否覆盖以前的任何设置。

   方法会返回使用指定的保存样式格式化的`BLOB`对象。 然后，可将该对象另存为PDF文档。

1. 将PDF文档传递到另一个Forms操作

   * 将返回的`BLOB`对象传递到另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 整理PDF文档{#sanitizing-pdf-documents}

您可以使用PDF实用程序Java API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关PDF实用程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-4}的摘要

要整理PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用清理操作。

**包含项目文件**

在开发项目中包含必需的文件。 要使用Java创建客户端应用程序，请包含必要的JAR文件。

**创建PDFUtilityService客户端**

在以编程方式执行清理操作之前，必须创建PDFUtilityService客户端。 使用Java API，可通过创建`PDFUtilityServiceClient`对象来完成此操作。

**调用PDF到XDP的转换操作**

在创建服务客户端后，可以调用清理操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#sanitize-pdf-documents-using-the-java-api}整理PDF文档

使用PDF实用程序API(Java)整理文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用其构造函数创建`PDFUtilityServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 调用PDF到XDP的转换操作

   要执行转换，请调用`PDFUtilityServiceClient`对象的`convertPDFtoXDP`方法，并传入表示PDF文件的`com.adobe.idp.Document`对象。 方法会返回一个`com.adobe.idp.Document`对象，该对象表示新创建的XDP文件。

**另请参阅**

[整理PDF文档](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
