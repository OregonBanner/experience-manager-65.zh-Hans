---
title: 使用PDF实用程序
description: 使用PDF实用程序服务在PDF和XDP文件格式之间进行转换，设置和检索PDF文档属性，以及处理XMP元数据。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# 使用PDF实用程序 {#working-with-pdf-utilities}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

**关于PDF实用程序服务**

PDF实用程序服务可以在PDF和XDP文件格式之间进行转换，设置和检索PDF文档属性，以及处理XMP元数据。 例如，在将PDF文档转换为另一种格式之前，检查其属性以确定要为转换调用哪个服务操作很有用。

您可以使用“PDF实用程序”服务完成这些任务：

* 将PDF文档转换为XDP文档。
* 将XDP文档转换为PDF文档。 (请参阅 [将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* 检索PDF文档属性。 (请参阅 [检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties).)
* 保存PDF文档并优化该文档，以便快速进行Web查看。 (请参阅 [设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 将PDF文档转换为XDP文档 {#converting-pdf-documents-into-xdp-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要将PDF文档转换为XDP文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用PDF到XDP的转换操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

必须先创建PDFUtilityService客户端，然后才能以编程方式执行PDF实用程序操作。 使用Java API，可通过创建 `PDFUtilityServiceClient` 对象。 使用Web服务API时，可使用 `PDFUtilityServiceService` 对象。

**调用PDF到XDP的转换操作**

创建服务客户端后，可以调用PDF到XDP的转换操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API将PDF文档转换为XDP文档 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

使用PDF实用程序API(Java)将PDF文档转换为XDP文档：

1. 包含项目文件

   将客户端JAR文件（如adobe-pdfutility-client.jar）包含在Java项目的类路径中。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用PDF到XDP的转换操作

   要执行转换，请调用 `PDFUtilityServiceClient` 对象的 `convertPDFtoXDP` 方法并传入 `com.adobe.idp.Document` 表示PDF文件的对象。 此方法会返回 `com.adobe.idp.Document` 表示新创建的XDP文件的对象。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将PDF文档转换为XDP文档 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

使用PDF实用程序API（Web服务）将PDF文档转换为XDP文档：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceService` 对象。

1. 调用PDF到XDP的转换操作

   调用 `PDFUtilityServiceService` 对象的 `convertPDFtoXDP` 方法并传入 `BLOB` 表示PDF文件的对象。 此方法会返回 `BLOB` 表示新创建的XDP文件的对象。

**另请参阅**

[将PDF文档转换为XDP文档](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 将XDP文档转换为PDF文档 {#converting-xdp-documents-into-pdf-documents}

您可以使用PDF实用程序Java和Web服务API以编程方式将XDP文档转换为PDF文档。

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要将XDP文档转换为PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用XDP以PDF转换操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

必须先创建PDFUtilityService客户端，然后才能以编程方式执行PDF实用程序操作。 使用Java API，可通过创建 `PDFUtilityServiceClient` 对象。 使用Web服务API时，可使用 `PDFUtilityServiceService` 对象。

**调用XDP以PDF转换操作**

创建服务客户端后，可以调用XDP以PDF转换操作。

**另请参阅**

[使用Java API将XDP文档转换为PDF文档](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[使用Web服务API将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API将XDP文档转换为PDF文档 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

使用PDF实用程序API (Java)将XDP文档转换为PDF文档：

1. 包含项目文件

   将客户端JAR文件（如adobe-pdfutility-client.jar）包含在Java项目的类路径中。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用XDP以PDF转换操作

   要执行转换，请调用 `PDFUtilityServiceClient` 对象的 `convertXDPtoPDF` 方法并传入 `com.adobe.idp.Document` 表示XDP文件的对象。 此方法会返回 `com.adobe.idp.Document` 表示新创建的PDF文件的对象。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API将XDP文档转换为PDF文档 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

使用PDF实用程序API（Web服务API）将XDP文档转换为PDF文档：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceService` 对象。

1. 调用XDP以PDF转换操作

   要执行转换，请调用 `PDFUtilityServiceService` 对象的 `convertXDPtoPDF` 方法并传入 `BLOB` 表示XDP文件的对象。 此方法会返回 `BLOB` 表示新创建的PDF文件的对象。

**另请参阅**

[将XDP文档转换为PDF文档](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 检索PDF文档属性 {#retrieving-pdf-document-properties}

您可以使用PDF实用程序Java和Web服务API以编程方式检索PDF文档属性，例如文档是可填写表单还是读取文档所需的最低Acrobat版本。

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤摘要 {#summary_of_steps-2}

要检索PDF文档属性，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用属性检索操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

必须先创建PDFUtilityService客户端，然后才能以编程方式执行PDF实用程序操作。 使用Java API，可通过创建 `PDFUtilityServiceClient` 对象。 使用Web服务API，可使用 `PDFUtilityServiceService` 对象。

**调用属性检索操作**

创建服务客户端后，可以调用属性检索操作。

**另请参阅**

[使用Java API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[使用Web服务API检索PDF文档属性](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检索PDF文档属性 {#retrieve-pdf-document-properties-using-the-java-api}

使用PDF实用程序API (Java)检索PDF文档属性：

1. 包含项目文件

   将客户端JAR文件（如adobe-pdfutility-client.jar）包含在Java项目的类路径中。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用属性检索操作

   要执行转换，请调用 `PDFUtilityServiceClient` 对象的 `getPDFProperties` 方法并传递以下内容：

   * A `com.adobe.idp.Document` 表示PDF文档的对象。
   * A `PDFPropertiesOptionSpec` 包含要计算的属性的对象。

   此方法会返回 `PDFPropertiesResult` 包含查询结果的对象。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索PDF文档属性 {#retrieve-pdf-document-properties-using-the-web-service-api}

使用PDF实用程序Web服务API检索PDF文档属性：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceService` 对象。

1. 调用属性检索操作

   要执行转换，请调用 `PDFUtilityServiceService` 对象的 `getPDFProperties` 方法并传递以下内容：

   * A `BLOB` 表示PDF文档的对象。
   * A `PDFPropertiesOptionSpec` 包含要计算的属性的对象。

   此方法会返回 `PDFPropertiesResult` 包含查询结果的对象。

**另请参阅**

[检索PDF文档属性](pdf-utilities.md#retrieving-pdf-document-properties)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 设置PDF文档保存模式 {#setting-pdf-document-save-modes}

您可以使用PDF实用程序服务Java和Web服务API以编程方式设置PDF文档的保存模式。 使用“PDF实用程序”服务设置保存模式时，“PDF实用程序”服务仅设置保存模式，实际上并不保存PDF文档。 PDF文档在传递到另一个服务操作时进行保存。 例如，您可以使用“PDF实用工具”服务设置特定的保存模式，并将其传递给“加密”服务，PDF文档将在此进行实际保存和加密。

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-3}

要为PDF文档设置保存选项，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 设置保存模式。
1. 调用保存操作。
1. 将PDF文档传递到另一个操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建PDFUtilityService客户端**

必须先创建PDFUtilityService客户端，然后才能以编程方式执行PDF实用程序操作。 使用Java API，可通过创建 `PDFUtilityServiceClient` 对象。 使用Web服务API，可使用 `PDFUtilityServiceService` 对象。

**设置保存模式**

您可以选择以下保存选项之一：

* `INCREMENTAL`：增量保存，减少保存所需的时间
* `FAST_WEB_VIEW`：保存以快速Web查看
* `FULL`：使用完全保存（无优化）进行保存

**调用保存样式操作**

创建服务客户端后，可以调用属性检索操作。

**将PDF文档传递到另一个AEM Forms操作**

一旦PDF实用程序服务设置了指定的保存模式，请将PDF文档传递给另一个AEM Forms操作。 从操作返回后，PDF文档将以指定模式保存。 例如，如果使用“PDF实用程序”服务设置 `FAST_WEB_VIEW` 模式，然后将PDF文档传递到加密服务的 `encryptUsingPassword` 操作，返回的PDF文档使用密码加密，并保存在 `FAST_WEB_VIEW` 模式。

>[!NOTE]
>
>与此部分关联的快速入门将 `FAST_WEB_VIEW` 模式，然后将PDF文档传递到加密服务的 `encryptUsingPassword` 操作。

**另请参阅**

[使用Java API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[使用Web服务API设置PDF文档保存选项](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用密码加密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API设置PDF文档保存选项 {#set-pdf-document-save-options-using-the-java-api}

使用PDF实用程序API (Java)设置PDF文档保存选项：

1. 包含项目文件

   将客户端JAR文件（如adobe-pdfutility-client.jar）包含在Java项目的类路径中。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 设置保存模式

   * 创建 `PDFUtilitySaveMode` 对象。
   * 通过调用 `PDFUtilitySaveMode` 对象的 `setSaveStyle` 方法，并传递一个指定保存模式的字符串值。 例如，要保存以快速Web查看，请传递 `FAST_WEB_VIEW`.

1. 调用保存样式操作

   调用 `PDFUtilityServiceClient` 对象的 `setSaveMode` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示PDF文档的对象。
   * A `PDFUtilitySaveMode` 包含要使用的保存样式的对象。
   * 一个布尔值，用于确定是否覆盖任何以前的设置。

   此方法会返回 `com.adobe.idp.Document` 使用指定的保存样式设置对象的格式。

1. 将PDF文档传递到另一个AEM Forms操作

   * 传递返回的 `com.adobe.idp.Document` 对象，用于另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API设置PDF文档保存选项 {#set-pdf-document-save-options-using-the-web-service-api}

使用PDF实用程序AP（Web服务）设置PDF文档保存选项：

1. 包含项目文件

   * 创建使用PDF实用程序服务WSDL文件的Microsoft .NET客户端程序集。
   * 引用Microsoft .NET客户端程序集。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceService` 对象。

1. 设置保存模式

   * 创建 `PDFUtilitySaveMode` 对象。
   * 通过将字符串值分配给 `PDFUtilitySaveMode` 对象的 `saveStyle` 指定保存模式的方法。 例如，要保存以快速Web查看，请指定 `FAST_WEB_VIEW`.

1. 调用保存样式操作

   调用 `PDFUtilityServiceService` 对象的 `setSaveMode` 方法并传递以下值：

   * A `BLOB` 表示PDF文档的对象。
   * A `PDFUtilitySaveMode` 包含要使用的保存样式的对象。
   * 一个布尔值，用于确定是否覆盖任何以前的设置。

   此方法会返回 `BLOB` 使用指定的保存样式设置对象的格式。 然后可将该对象另存为PDF文档。

1. 将PDF文档传递到另一个Forms操作

   * 传递返回的 `BLOB` 对象，用于另一个AEM Forms操作。

**另请参阅**

[设置PDF文档保存模式](pdf-utilities.md#setting-pdf-document-save-modes)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[创建使用Base64编码的.NET客户端程序集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## 清理PDF文档 {#sanitizing-pdf-documents}

您可以使用PDF实用程序Java API以编程方式将PDF文档转换为XDP文档。

>[!NOTE]
>
>有关“PDF实用程序”服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-4}

要整理PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDFUtilityService客户端。
1. 调用清理操作。

**包含项目文件**

在开发项目中包含必要的文件。 要使用Java创建客户端应用程序，请包含必要的JAR文件。

**创建PDFUtilityService客户端**

必须先创建PDFUtilityService客户端，然后才能以编程方式执行清理操作。 使用Java API，可通过创建 `PDFUtilityServiceClient` 对象。

**调用PDF到XDP的转换操作**

创建服务客户端后，可以调用清理操作。

**另请参阅**

[使用Java API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[使用Web服务API将PDF文档转换为XDP文档](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API整理PDF文档 {#sanitize-pdf-documents-using-the-java-api}

使用PDF实用程序API (Java)整理文档：

1. 包含项目文件

   将客户端JAR文件（如adobe-pdfutility-client.jar）包含在Java项目的类路径中。

1. 创建PDFUtilityService客户端

   创建 `PDFUtilityServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 调用PDF到XDP的转换操作

   要执行转换，请调用 `PDFUtilityServiceClient` 对象的 `convertPDFtoXDP` 方法并传入 `com.adobe.idp.Document` 表示PDF文件的对象。 此方法会返回 `com.adobe.idp.Document` 表示新创建的XDP文件的对象。

**另请参阅**

[清理PDF文档](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
