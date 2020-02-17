---
title: 使用PDF实用程序
seo-title: 使用PDF实用程序
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用PDF实用程序 {#working-with-pdf-utilities}

**关于PDF实用程序服务**

PDF实用程序服务可以在PDF和XDP文件格式之间转换，设置和检索PDF文档属性，以及处理XMP元数据。 例如，在将PDF文档转换为其他格式之前，检查其属性以确定要调用哪个服务操作以进行转换会很有用。

您可以使用“PDF实用程序”服务完成以下任务：

* 将PDF文档转换为XDP文档。
* 将XDP文档转换为PDF文档。 (请参阅 [将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)。)
* 检索PDF文档属性。 (请参阅 [检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)。)
* 保存PDF文档并对其进行优化，以便快速进行Web查看。 (请参阅 [设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)。)

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将PDF文档转换为XDP文档 {#converting-pdf-documents-into-xdp-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为XDP文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用PDF到XDP转换操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行“PDF实用程序”操作之前，必须创建PDFUtilityService客户端。 使用Java API，这可以通过创建对象来 `PDFUtilityServiceClient` 实现。 借助Web服务API，这是通过使用对象来实现 `PDFUtilityServiceService` 的。

**调用PDF到XDP转换操作**

创建服务客户端后，可以调用PDF到XDP转换操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API将PDF文档转换为XDP文档 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF实用程序API(Java)将PDF文档转换为XDP文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用对 `PDFUtilityServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用PDF到XDP转换操作

   要执行转换，请调用对 `PDFUtilityServiceClient` 象的方 `convertPDFtoXDP` 法并传入表示PDF `com.adobe.idp.Document` 文件的对象。 该方法返回一 `com.adobe.idp.Document` 个表示新创建的XDP文件的对象。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为XDP文档 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF实用程序API（Web服务）将PDF文档转换为XDP文档：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用PDF实用程序服务WSDL文件。
   * 参考Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代 `PDFUtilityServiceService` 理类构造函数创建对象。

1. 调用PDF到XDP转换操作

   调用对 `PDFUtilityServiceService` 象的方 `convertPDFtoXDP` 法并传入表示PDF `BLOB` 文件的对象。 该方法返回一 `BLOB` 个表示新创建的XDP文件的对象。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 将XDP文档转换为PDF文档 {#converting-xdp-documents-into-pdf-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将XDP文档转换为PDF文档。

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要将XDP文档转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用XDP到PDF的转换操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行“PDF实用程序”操作之前，必须创建PDFUtilityService客户端。 使用Java API，这可以通过创建对象来 `PDFUtilityServiceClient` 实现。 借助Web服务API，这是通过使用对象来实现 `PDFUtilityServiceService` 的。

**调用XDP到PDF的转换操作**

创建服务客户端后，可以调用XDP到PDF的转换操作。

**另请参阅**

[使用Java API将XDP文档转换为PDF文档](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服务API将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API将XDP文档转换为PDF文档 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF实用程序API(Java)将XDP文档转换为PDF文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用对 `PDFUtilityServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用XDP到PDF的转换操作

   要执行转换，请调 `PDFUtilityServiceClient` 用对象的方 `convertXDPtoPDF` 法并传入表示XDP `com.adobe.idp.Document` 文件的对象。 该方法返回一 `com.adobe.idp.Document` 个表示新创建的PDF文件的对象。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将XDP文档转换为PDF文档 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF实用程序API（Web服务API）将XDP文档转换为PDF文档：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用PDF实用程序服务WSDL文件。
   * 参考Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代 `PDFUtilityServiceService` 理类构造函数创建对象。

1. 调用XDP到PDF的转换操作

   要执行转换，请调 `PDFUtilityServiceService` 用对象的方 `convertXDPtoPDF` 法并传入表示XDP `BLOB` 文件的对象。 该方法返回一 `BLOB` 个表示新创建的PDF文件的对象。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 检索PDF文档属性 {#retrieving-pdf-document-properties}

您可以使用PDF实用程序Java和Web服务API以编程方式检索PDF文档属性，如文档是可填写的表单还是读取文档所需的最低版本的Acrobat。

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参阅AEM [表单服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤摘要 {#summary_of_steps-2}

要检索PDF文档属性，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用属性检索操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行“PDF实用程序”操作之前，必须创建PDFUtilityService客户端。 使用Java API，这可以通过创建对象来 `PDFUtilityServiceClient` 实现。 借助Web服务API，这是使用对象完 `PDFUtilityServiceService` 成的。

**调用属性检索操作**

创建服务客户端后，可以调用属性检索操作。

**另请参阅**

[使用Java API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服务API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检索PDF文档属性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF实用程序API(Java)检索PDF文档属性：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用对 `PDFUtilityServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用属性检索操作

   要执行转换，请调用对 `PDFUtilityServiceClient` 象的方 `getPDFProperties` 法并传递以下信息：

   * 表示 `com.adobe.idp.Document` PDF文档的对象。
   * 包 `PDFPropertiesOptionSpec` 含要计算的属性的对象。
   该方法返回 `PDFPropertiesResult` 一个包含查询结果的对象。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索PDF文档属性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF实用程序Web服务API检索PDF文档属性：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用PDF实用程序服务WSDL文件。
   * 参考Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代 `PDFUtilityServiceService` 理类构造函数创建对象。

1. 调用属性检索操作

   要执行转换，请调用对 `PDFUtilityServiceService` 象的方 `getPDFProperties` 法并传递以下信息：

   * 表示 `BLOB` PDF文档的对象。
   * 包 `PDFPropertiesOptionSpec` 含要计算的属性的对象。
   该方法返回 `PDFPropertiesResult` 一个包含查询结果的对象。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 设置PDF文档保存模式 {#setting-pdf-document-save-modes}

您可以使用PDF实用程序服务Java和Web服务API以编程方式为PDF文档设置保存模式。 当使用“PDF实用程序”服务设置保存模式时，“PDF实用程序”服务仅设置保存模式，而不实际保存PDF文档。 当PDF文档被传递到其他服务操作时，将保存该文档。 例如，您可以使用“PDF实用程序”服务设置特定的保存模式并将其传递给“加密”服务，在该服务中，PDF文档实际被保存和加密。

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要设置PDF文档的保存选项，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 设置保存模式。
1. 调用保存操作。
1. 将PDF文档传递给其他操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

在以编程方式执行“PDF实用程序”操作之前，必须创建PDFUtilityService客户端。 使用Java API，这可以通过创建对象来 `PDFUtilityServiceClient` 实现。 借助Web服务API，这是使用对象完 `PDFUtilityServiceService` 成的。

**设置保存模式**

您可以选择以下保存选项之一：

* `INCREMENTAL`:以增量方式节省以缩短节省所需时间
* `FAST_WEB_VIEW`:保存为快速Web查看
* `FULL`:使用完整保存进行保存（无优化）

**调用保存样式操作**

创建服务客户端后，可以调用属性检索操作。

**将PDF文档传递到另一个AEM Forms操作**

PDF实用程序服务设置指定的保存模式后，将PDF文档传递到另一个AEM Forms操作。 从该操作返回后，PDF文档将保存在指定的模式中。 例如，如果您使用“PDF实用程序”服务设置模式，然后将 `FAST_WEB_VIEW` PDF文档传递给“加密”服务的操作，则返回的PDF文档将使用密码进行加密并保存在该模 `encryptUsingPassword``FAST_WEB_VIEW` 式中。

>[!NOTE]
>
>与此部分关联的快速入门设置模 `FAST_WEB_VIEW` 式，然后将PDF文档传递给加密服务的操 `encryptUsingPassword` 作。

**另请参阅**

[使用Java API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服务API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用口令加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API设置PDF文档保存选项 {#set-pdf-document-save-options-using-the-java-api}

使用PDF实用程序API(Java)设置PDF文档保存选项：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用对 `PDFUtilityServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 设置保存模式

   * 使用对 `PDFUtilitySaveMode` 象的构造函数创建对象。
   * 通过调用对象的方法并传 `PDFUtilitySaveMode` 递指定保存 `setSaveStyle` 模式的字符串值来设置保存模式。 例如，要保存以便快速查看Web，请传递 `FAST_WEB_VIEW`。

1. 调用保存样式操作

   调用对 `PDFUtilityServiceClient` 象的方 `setSaveMode` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` PDF文档的对象。
   * 包 `PDFUtilitySaveMode` 含要使用的保存样式的对象。
   * 用于确定是否覆盖任何以前设置的布尔值。
   该方法返回使用 `com.adobe.idp.Document` 指定的保存样式格式化的对象。

1. 将PDF文档传递到另一个AEM Forms操作

   * 将返回的对 `com.adobe.idp.Document` 象传递给另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API设置PDF文档保存选项 {#set-pdf-document-save-options-using-the-web-service-api}

使用“PDF实用程序”AP（Web服务）设置PDF文档保存选项：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用PDF实用程序服务WSDL文件。
   * 参考Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   使用代 `PDFUtilityServiceService` 理类构造函数创建对象。

1. 设置保存模式

   * 使用对 `PDFUtilitySaveMode` 象的构造函数创建对象。
   * 通过为指定保存模式的对象的方法 `PDFUtilitySaveMode` 分配字符串 `saveStyle` 值来设置保存模式。 例如，要保存以便快速查看Web，请指定 `FAST_WEB_VIEW`。

1. 调用保存样式操作

   调用对 `PDFUtilityServiceService` 象的方 `setSaveMode` 法并传递以下值：

   * 表示 `BLOB` PDF文档的对象。
   * 包 `PDFUtilitySaveMode` 含要使用的保存样式的对象。
   * 用于确定是否覆盖任何以前设置的布尔值。
   该方法返回使用 `BLOB` 指定的保存样式格式化的对象。 然后，可将该对象另存为PDF文档。

1. 将PDF文档传递到其他表单操作

   * 将返回的对 `BLOB` 象传递给另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的。NET客户端组件](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 整理PDF文档 {#sanitizing-pdf-documents}

您可以使用PDF实用程序Java API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关PDF实用程序服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要清理PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用清理操作。

**包括项目文件**

在开发项目中包含必要的文件。 要使用Java创建客户端应用程序，请包含必需的JAR文件。

**创建PDFUtilityService客户端**

在以编程方式执行清理操作之前，必须创建PDFUtilityService客户端。 使用Java API，这可以通过创建对象来 `PDFUtilityServiceClient` 实现。

**调用PDF到XDP转换操作**

创建服务客户端后，可以调用清理操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API清理PDF文档 {#sanitize-pdf-documents-using-the-java-api}

使用PDF Utilities API(Java)清理文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-pdfutility-client.jar。

1. 创建PDFUtilityService客户端

   使用对 `PDFUtilityServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 调用PDF到XDP转换操作

   要执行转换，请调用对 `PDFUtilityServiceClient` 象的方 `convertPDFtoXDP` 法并传入表示PDF `com.adobe.idp.Document` 文件的对象。 该方法返回一 `com.adobe.idp.Document` 个表示新创建的XDP文件的对象。

**另请参阅**

[整理PDF文档](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
