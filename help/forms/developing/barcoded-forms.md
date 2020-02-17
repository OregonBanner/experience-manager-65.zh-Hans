---
title: 使用条形码表单
seo-title: 使用条形码表单
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# 使用条形码表单 {#working-with-barcoded-forms}

## 关于条形码表单服务 {#about-the-barcoded-forms-service}

条形码表单服务可自动从填写和打印表单中捕获数据，并将捕获的信息集成到组织的核心IT系统中。

使用条形码表单服务，可向交互式PDF表单添加一维和二维条码。 然后，您可以将条形码表单发布到网站或通过电子邮件或CD分发。 当用户使用Adobe Reader、Acrobat Professional或Acrobat Standard填充条形码表单时，条形码会自动更新以对用户提供的表单数据进行编码。 用户可以以电子方式提交表单，或将表单打印到纸张上并通过邮件、传真或手工提交。 您以后可以提取用户提供的数据作为自动工作流程的一部分，在批准流程和业务系统之间传送数据。

有关条形码表单服务的详细信息，请参 [阅AEM表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解码条形码表单数据 {#decoding-barcoded-form-data}

您可以使用条形码表单服务API对PDF表单或包含条形码的图像中的数据进行解码。 解码表单数据是指提取位于条形码中的数据。 在从PDF表单（或图像）解码数据之前，用户必须用数据填充表单。

>[!NOTE]
>
>有关条形码表单服务的详细信息，请参 [阅AEM表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要解码PDF表单中的数据，请执行以下步骤：

1. 包括项目文件。
1. 创建条形码的formsClient API对象。
1. 获取包含条形码数据的PDF表单。
1. 从PDF表单解码数据。
1. 将数据转换为XML数据源。
1. 处理解码的数据。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时为必需）
* xercesImpl.jar（位于&lt;安装目录>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty）

如果AEM Forms部署在非JBOSS的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建条形码表单客户端API对象**

在以编程方式执行条形码表单服务操作之前，必须创建Barcoded Forms服务客户端。 如果您使用Java API，请创建一个对 `BarcodedFormsServiceClient` 象。 如果您使用条形码表单Web服务API，请创建一个对 `BarcodedFormsServiceService` 象。

**获取包含条形码数据的PDF表单**

您必须获取包含已填充用户数据的条形码的PDF表单。

**从PDF表单解码数据**

获得包含条形码的PDF表单（或图像）后，可以对数据进行解码。 Barcoded Forms服务支持以下类型的条形码：

* PDF417条码。
* 数据矩阵条码。
* QR码条码。
* 科达巴条码。
* 代码128条码。
* 39码条码。
* EAN-13条码。
* EAN-8条码。

在解码API中输入为十六进制的字符集意味着条形码的内容编码为十六进制字符串。 例如，如果在表单中将UTF-8指定为字符编码，而在解码操作中指定了十六进制，则条形码的内容在解码输出的&lt; `xb:content`>元素中将编码为十六进制字符串。 您可以转换此十六进制值，在客户端应用程序中创建应用程序逻辑以获取原始内容。

**将数据转换为XML数据源**

对表单数据进行解码后，可将其转换为XDP或XFDF数据。 例如，假设您要将数据导入到其他表单中。 要将数据导入XFA表单，您必须将数据转换为XDP数据。 有关信息，请参阅 [导入表单数据](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**处理解码的数据**

您可以处理转换后的数据以满足您的业务需求。 例如，在对数据进行解码和转换后，可以将其保存到文件中，将其存储在企业数据库中，填充其他表单，等等。 本节讨论如何将转换后的数据另存为XML文件。

>[!NOTE]
>
>当行分隔符和字段分隔符参数具有相同的值时，条形码表单服务无法解码条形码数据

**另请参阅**

[使用Java API对条形码表单数据进行解码](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用Web服务API对条形码表单数据进行解码](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API对条形码表单数据进行解码 {#decode-barcoded-form-data-using-the-java-api}

使用条形码表单API(Java)对表单数据进行解码：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件。

1. 创建条形码表单客户端API对象

   使用对 `BarcodedFormsServiceClient` 象的构造函数并传递一个包含连接属 `ServiceClientFactory` 性的对象来创建对象。

1. 获取包含条形码数据的PDF表单

   * 创建一 `java.io.FileInputStream` 个对象，该对象通过使用其构造函数并传递一个指定PDF文档位置的字符串值来表示包含条形码数据的PDF表单。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 从PDF表单解码数据

   通过调用对象的方法并传 `BarcodedFormsServiceClient` 递以下值来解 `decode` 码表单数据：

   * 包 `com.adobe.idp.Document` 含PDF表单的对象。
   * 指定 `java.lang.Boolean` 是否对PDF417条形码进行解码的对象。
   * 指定 `java.lang.Boolean` 是否解码数据矩阵条形码的对象。
   * 指定 `java.lang.Boolean` 是否解码QR码条形码的对象。
   * 指定 `java.lang.Boolean` 是否解码codabar条形码的对象。
   * 指定 `java.lang.Boolean` 是否解码代码128条形码的对象。
   * 指定 `java.lang.Boolean` 是否解码代码39条形码的对象。
   * 指定 `java.lang.Boolean` 是否对EAN-13条形码进行解码的对象。
   * 指定 `java.lang.Boolean` 是否对EAN-8条形码进行解码的对象。
   * 一个 `com.adobe.livecycle.barcodedforms.CharSet` 枚举值，它指定条形码中使用的字符集编码值。
   该方 `decode` 法返回包含 `org.w3c.dom.Document` 已解码的表单数据的对象。

1. 将数据转换为XML数据源

   通过调用对象的方法并传递以下值，将解码的数 `BarcodedFormsServiceClient` 据转换为XDP `extractToXML` 或XFDF数据：

   * 包 `org.w3c.dom.Document` 含解码数据的对象(确保使用 `decode` 方法的返回值)。
   * 指定 `com.adobe.livecycle.barcodedforms.Delimiter` 行分隔符的枚举值。 建议您指定 `Delimiter.Carriage_Return`。
   * 指定 `com.adobe.livecycle.barcodedforms.Delimiter` 字段分隔符的枚举值。 例如，指定 `Delimiter.Tab`。
   * 指定 `com.adobe.livecycle.barcodedforms.XMLFormat` 是将条形码数据转换为XDP还是XFDF XML数据的枚举值。 例如，指定 `XMLFormat.XDP` 将数据转换为XDP数据。
   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   该方 `extractToXML` 法返回一个对 `java.util.List` 象，其中每个元素都是一个 `org.w3c.dom.Document` 对象。 表单上的每个条形码都有一个单独的元素。 即，如果表单上有四个条码，则返回的对象中有四个元 `java.util.List` 素。

1. 处理解码的数据

   * 遍历对 `java.util.List` 象以获取列 `org.w3c.dom.Document` 表中的每个对象。
   * 对于列表中的每个元素，将对 `org.w3c.dom.Document` 象转换为对 `com.adobe.idp.Document` 象。 (将对象转换为对象的应 `org.w3c.dom.Document` 用程序逻辑 `com.adobe.idp.Document` 使用Java API示例在解码条形码表单数据中显示)。
   * 通过调用对象并传递表示XML文件的File `com.adobe.idp.Document` 对象 `copyToFile`，将XML数据另存为XML文件。

**另请参阅**

[快速入门（SOAP模式）:使用Java API解码条形码表单数据](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对条形码表单数据进行解码 {#decode-barcoded-form-data-using-the-web-service-api}

使用条形码表单API（web服务）对表单数据进行解码：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端组件，它使用条形码表单服务WSDL。 有关信息，请参 [阅使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * 参考Microsoft .NET客户端程序集。 有关信息，请参阅使用Base64编码调用AEM Forms中的“ [引用。NET客户端程序集”](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。

1. 创建条形码表单客户端API对象

   使用使用barcoded forms服务WSDL的Microsoft .NET客户端组件，通过调用其默认 `BarcodedFormsServiceService` 构造函数创建一个对象。

1. 获取包含条形码数据的PDF表单

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储包含条形码的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `binaryData` 为字节数组的内容来填充对象。

1. 从PDF表单解码数据

   通过调用对象的方法并传 `BarcodedFormsServiceService` 递以下值来解 `decode` 码表单数据：

   * 包 `BLOB` 含PDF表单的对象。
   * 指定 `Boolean` 是否对PDF417条形码进行解码的对象。
   * 指定 `Boolean` 是否解码数据矩阵条形码的对象。
   * 指定 `Boolean` 是否解码QR码条形码的对象。
   * 指定 `Boolean` 是否解码codabar条形码的对象。
   * 指定 `Boolean` 是否解码代码128条形码的对象。
   * 指定 `Bolean` 是否解码代码39条形码的对象。
   * 指定 `Boolean` 是否对EAN-13条形码进行解码的对象。
   * 指定 `Boolean` 是否对EAN-8条形码进行解码的对象。
   * 一个 `CharSet` 枚举值，它指定条形码中使用的字符集编码值。
   该方 `decode` 法返回包含解码的表单数据的字符串值。

1. 将数据转换为XML数据源

   通过调用对象的方法并传递以下值，将解码的数 `BarcodedFormsServiceService` 据转换为XDP `extractToXML` 或XFDF数据：

   * 包含解码数据的字符串值(确保使 `decode` 用方法的返回值)。
   * 指定 `Delimiter` 行分隔符的枚举值。 建议您指定 `Delimiter.Carriage_Return`。
   * 指定 `Delimiter` 字段分隔符的枚举值。 例如，指定 `Delimiter.Tab`。
   * 指定 `XMLFormat` 是将条形码数据转换为XDP还是XFDF XML数据的枚举值。 例如，指定 `XMLFormat.XDP` 将数据转换为XDP数据。
   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   该方 `extractToXML` 法返回一个数 `Object` 组，其中每个元素都是一个 `BLOB` 实例。 表单上的每个条形码都有一个单独的元素。 即，如果表单上有四个条码，则返回的数组中有四个元 `Object` 素。

1. 处理解码的数据

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示受保护PDF文档的文件位置的字符串值，创建一个对象。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `encryptPDFUsingPassword` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
