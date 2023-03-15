---
title: 使用条形码表单
seo-title: Working with barcoded forms
description: 使用Java API和Web服务API从PDF表单或包含条形码的图像中解码数据。
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# 使用条形码表单 {#working-with-barcoded-forms}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

## 关于条形码表单服务 {#about-the-barcoded-forms-service}

条形码表单服务可自动从填写和打印表单中捕获数据，并将捕获的信息集成到组织的核心IT系统中。

使用条形码表单服务，可以向交互式PDF forms添加一维和二维条形码。 然后，您可以将条形码表单发布到网站或通过电子邮件或CD分发这些表单。 当用户使用Adobe Reader、Acrobat Professional或Acrobat Standard填写条形码表单时，将自动更新条形码以编码用户提供的表单数据。 用户可以通过电子方式提交表单，也可以打印成纸张，然后以邮件、传真或手写方式提交。 您以后可以提取用户提供的数据作为自动化工作流的一部分，在审批流程和业务系统之间传送数据。

有关条形码表单服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 解码条形码表单数据 {#decoding-barcoded-form-data}

您可以使用条形码表单服务API来解码PDF表单或包含条形码的图像中的数据。 解码表单数据是指提取位于条形码中的数据。 在从PDF表单（或图像）中解码数据之前，用户必须使用数据填充表单。

>[!NOTE]
>
>有关条形码表单服务的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要解码PDF表单中的数据，请执行以下步骤：

1. 包括项目文件。
1. 创建条形码的formsClient API对象。
1. 获取包含条形码数据的PDF表单。
1. 从PDF表单中解码数据。
1. 将数据转换为XML数据源。
1. 处理已解码的数据。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，则包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(如果将AEM Forms部署在JBoss上，则此为必需字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* xercesImpl.jar(位于 &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果将AEM Forms部署在支持的J2EE应用程序服务器（不是JBOSS）上，则需要将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建条形码表单客户端API对象**

您必须先创建条形码Forms服务客户端，然后才能以编程方式执行条形码表单服务操作。 如果您使用的是Java API，请创建 `BarcodedFormsServiceClient` 对象。 如果您使用的是条形码表单Web服务API，请创建 `BarcodedFormsServiceService` 对象。

**获取包含条形码数据的PDF表单**

您必须获取一个PDF表单，其中包含已填充了用户数据的条形码。

**从PDF表单中解码数据**

在获取包含条形码的PDF表单（或图像）后，可以对数据进行解码。 条形码Forms服务支持以下类型的条形码：

* PDF417条码。
* 数据矩阵条形码。
* QR代码条形码。
* 代码标签条形码。
* 128条码。
* 代码39条码。
* EAN-13条形码。
* EAN-8条形码。

在解码API中，字符集输入为十六进制表示条形码的内容被编码为十六进制字符串。 例如，如果在表单中将UTF-8指定为字符编码，并在解码操作中指定了十六进制，则条形码的内容将在&lt;中编码为十六进制字符串 `xb:content`>个元素。 您可以通过在客户端应用程序中创建应用程序逻辑来转换此Hex值以获取原始内容。

**将数据转换为XML数据源**

对表单数据进行解码后，可将其转换为XDP或XFDF数据。 例如，假设您要将数据导入到其他表单中。 要将数据导入XFA表单，则必须将数据转换为XDP数据。 有关信息，请参阅 [导入表单数据](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**处理解码的数据**

您可以处理转换后的数据，以满足您的业务需求。 例如，在解码和转换数据后，可以将其保存到文件、将其存储在企业数据库中、填充其他表单等。 本节讨论如何将转换的数据另存为XML文件。

>[!NOTE]
>
>当行分隔符和字段分隔符参数具有相同的值时，条形码表单服务无法解码条形码数据

**另请参阅**

[使用Java API解码条形码表单数据](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用Web服务API解码条形码表单数据](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API解码条形码表单数据 {#decode-barcoded-form-data-using-the-java-api}

使用条形码表单API(Java)对表单数据进行解码：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建条形码表单客户端API对象

   创建 `BarcodedFormsServiceClient` 对象通过使用该对象的构造函数传递 `ServiceClientFactory` 包含连接属性的对象。

1. 获取包含条形码数据的PDF表单

   * 创建 `java.io.FileInputStream` 对象，表示包含条形码数据的PDF表单，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 从PDF表单中解码数据

   通过调用 `BarcodedFormsServiceClient` 对象的 `decode` 方法，并传递以下值：

   * 此 `com.adobe.idp.Document` 包含PDF表单的对象。
   * A `java.lang.Boolean` 指定是否对PDF417条形码进行解码的对象。
   * A `java.lang.Boolean` 指定是否解码数据矩阵条形码的对象。
   * A `java.lang.Boolean` 指定是否对QR代码条形码进行解码的对象。
   * A `java.lang.Boolean` 指定是否对代码标签条形码进行解码的对象。
   * A `java.lang.Boolean` 指定是否解码代码128条形码的对象。
   * A `java.lang.Boolean` 指定是否对代码39条形码进行解码的对象。
   * A `java.lang.Boolean` 指定是否对EAN-13条形码进行解码的对象。
   * A `java.lang.Boolean` 指定是否对EAN-8条形码进行解码的对象。
   * A `com.adobe.livecycle.barcodedforms.CharSet` 指定条形码中使用的字符集编码值的枚举值。

   此 `decode` 方法返回 `org.w3c.dom.Document` 包含已解码表单数据的对象。

1. 将数据转换为XML数据源

   通过调用 `BarcodedFormsServiceClient` 对象的 `extractToXML` 方法，并传递以下值：

   * 此 `org.w3c.dom.Document` 包含已解码数据的对象(确保您使用 `decode` 方法的返回值)。
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定行分隔符的枚举值。 建议您指定 `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` 指定字段分隔符的枚举值。 例如，指定 `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` 指定将条形码数据转换为XDP还是XFDF XML数据的枚举值。 例如，指定 `XMLFormat.XDP` 将数据转换为XDP数据。

   >[!NOTE]
   >
   >不要为行分隔符和字段分隔符参数指定相同的值。

   此 `extractToXML` 方法返回 `java.util.List` 对象，其中每个元素为 `org.w3c.dom.Document` 对象。 表单上的每个条形码都有一个单独的元素。 也就是说，如果表单上有四个条形码，则返回的元素有四个 `java.util.List` 对象。

1. 处理解码的数据

   * 循环访问 `java.util.List` 要获取每个对象的对象 `org.w3c.dom.Document` 位于列表中的对象。
   * 对于列表中的每个元素，将 `org.w3c.dom.Document` 对象到 `com.adobe.idp.Document` 对象。 (用于转换应用程序逻辑的 `org.w3c.dom.Document` 对象转换为 `com.adobe.idp.Document` 对象在解码条形码表单数据中使用Java API示例显示)。
   * 通过调用 `com.adobe.idp.Document` 对象的 `copyToFile`，并传递表示XML文件的File对象。

**另请参阅**

[快速入门（SOAP模式）：使用Java API对条形码表单数据进行解码](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API解码条形码表单数据 {#decode-barcoded-form-data-using-the-web-service-api}

使用条形码表单API（Web服务）对表单数据进行解码：

1. 包括项目文件

   * 创建使用条形码表单服务WSDL的Microsoft .NET客户端程序集。 有关信息，请参阅 [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * 引用Microsoft .NET客户端程序集。 有关信息，请参阅中的“引用.NET客户端程序集” [使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. 创建条形码表单客户端API对象

   使用使用条形码表单服务WSDL的Microsoft .NET客户端程序集，创建 `BarcodedFormsServiceService` 对象。

1. 获取包含条形码数据的PDF表单

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含条形码的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `binaryData` 属性与字节数组的内容。

1. 从PDF表单中解码数据

   通过调用 `BarcodedFormsServiceService` 对象的 `decode` 方法，并传递以下值：

   * 此 `BLOB` 包含PDF表单的对象。
   * A `Boolean` 指定是否对PDF417条形码进行解码的对象。
   * A `Boolean` 指定是否解码数据矩阵条形码的对象。
   * A `Boolean` 指定是否对QR代码条形码进行解码的对象。
   * A `Boolean` 指定是否对代码标签条形码进行解码的对象。
   * A `Boolean` 指定是否解码代码128条形码的对象。
   * A `Bolean` 指定是否对代码39条形码进行解码的对象。
   * A `Boolean` 指定是否对EAN-13条形码进行解码的对象。
   * A `Boolean` 指定是否对EAN-8条形码进行解码的对象。
   * A `CharSet` 指定条形码中使用的字符集编码值的枚举值。

   此 `decode` 方法会返回一个包含已解码表单数据的字符串值。

1. 将数据转换为XML数据源

   通过调用 `BarcodedFormsServiceService` 对象的 `extractToXML` 方法，并传递以下值：

   * 包含已解码数据的字符串值(确保您使用 `decode` 方法的返回值)。
   * A `Delimiter` 指定行分隔符的枚举值。 建议您指定 `Delimiter.Carriage_Return`.
   * A `Delimiter` 指定字段分隔符的枚举值。 例如，指定 `Delimiter.Tab`.
   * A `XMLFormat` 指定将条形码数据转换为XDP还是XFDF XML数据的枚举值。 例如，指定 `XMLFormat.XDP` 将数据转换为XDP数据。

   >[!NOTE]
   >
   >不要为行分隔符和字段分隔符参数指定相同的值。

   此 `extractToXML` 方法返回 `Object` 数组，其中每个元素为 `BLOB` 实例。 表单上的每个条形码都有一个单独的元素。 也就是说，如果表单上有四个条形码，则返回的元素有四个 `Object` 数组。

1. 处理解码的数据

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递表示受保护PDF文档的文件位置的字符串值。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `encryptPDFUsingPassword` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
