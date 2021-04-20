---
title: 使用条形码表单
seo-title: 使用条形码表单
description: 使用Java API和Web服务API对PDF表单或包含条形码的图像中的数据进行解码。
seo-description: 使用Java API和Web服务API对PDF表单或包含条形码的图像中的数据进行解码。
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---


# 使用条形码表单{#working-with-barcoded-forms}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 关于条码表单服务{#about-the-barcoded-forms-service}

barcoded forms服务可自动从填写和打印表单捕获数据，并将捕获的信息集成到组织机构的核心IT系统中。

使用条码表单服务，您可以向交互式PDF forms添加一维和二维条码。 然后，您可以将条形码表单发布到网站或通过电子邮件或CD分发。 当用户使用Adobe Reader、Acrobat Professional或Acrobat Standard填充条形码表单时，条形码会自动更新以对用户提供的表单数据进行编码。 用户可以以电子方式提交表单，或将表单打印成纸张，然后通过邮件、传真或手工提交。 您以后可以提取用户提供的数据作为自动工作流程的一部分，在审批流程和业务系统之间路由数据。

有关barcoded forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 解码条形码表单数据{#decoding-barcoded-form-data}

您可以使用条形码表单服务API对PDF表单或包含条形码的图像中的数据进行解码。 解码表单数据是指提取位于条形码中的数据。 在从PDF表单（或图像）解码数据之前，用户必须用数据填充表单。

>[!NOTE]
>
>有关barcoded forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要对PDF表单中的数据进行解码，请执行以下步骤：

1. 包括项目文件。
1. 创建barcoded formsClient API对象。
1. 获取包含条形码数据的PDF表单。
1. 对PDF表单中的数据进行解码。
1. 将数据转换为XML数据源。
1. 处理解码的数据。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时为必需)
* jbossall-client.jar(在JBoss上部署AEM Forms时为必需)
* xercesImpl.jar(位于&lt;install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

如果AEM Forms部署在非JBOSS的受支持J2EE应用程序服务器上，则您需要将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建条形码表单客户端API对象**

在以编程方式执行barcoded forms服务操作之前，必须创建Barcoded Forms服务客户端。 如果您使用Java API，请创建`BarcodedFormsServiceClient`对象。 如果您使用barcoded forms Web服务API，请创建`BarcodedFormsServiceService`对象。

**获取包含条形码数据的PDF表单**

您必须获取包含已填充用户数据的条形码的PDF表单。

**从PDF表单解码数据**

获得包含条形码的PDF表单（或图像）后，可以对数据进行解码。 Barcoded Forms服务支持以下类型的条码：

* PDF417条码。
* 数据矩阵条码。
* QR码条码。
* 科达巴条形码。
* 128条码。
* 39条码。
* EAN-13条形码。
* EAN-8条码。

在解码API中，字符集输入为十六进制意味着条形码的内容将作为十六进制字符串进行编码。 例如，如果将UTF-8指定为格式的字符编码，而在解码操作中指定了Hex，则在解码输出的&lt;`xb:content`>元素中，条形码的内容将编码为Hex字符串。 您可以转换此十六进制值，在客户端应用程序中创建应用程序逻辑，以获得原始内容。

**将数据转换为XML数据源**

在对表单数据进行解码后，可以将其转换为XDP或XFDF数据。 例如，假设您要将数据导入其他表单。 要将数据导入XFA表单，您必须将数据转换为XDP数据。 有关信息，请参阅[导入表单数据](/help/forms/developing/importing-exporting-data.md#importing-form-data)。

**处理解码的数据**

您可以处理转换后的数据以满足您的业务需求。 例如，在对数据进行解码和转换后，可以将其保存到文件中，将其存储在企业数据库中，填充其他表单，等等。 本节讨论如何将转换后的数据另存为XML文件。

>[!NOTE]
>
>当行分隔符和字段分隔符参数具有相同的值时，条形码表单服务无法解码条形码数据

**另请参阅**

[使用Java API对条形码表单数据进行解码](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[使用Web服务API对条形码表单数据进行解码](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#decode-barcoded-form-data-using-the-java-api}对表单数据进行条形码解码

使用barcoded forms API(Java)对表单数据进行解码：

1. 包括项目文件

   将客户端JAR文件包含在Java项目的类路径中。

1. 创建条形码表单客户端API对象

   使用`BarcodedFormsServiceClient`对象的构造函数并传递包含连接属性的`ServiceClientFactory`对象，创建对象。

1. 获取包含条形码数据的PDF表单

   * 创建一个`java.io.FileInputStream`对象，该对象使用其构造函数并传递一个指定PDF文档位置的字符串值来表示包含条形码数据的PDF表单。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建对象。

1. 从PDF表单解码数据

   通过调用`BarcodedFormsServiceClient`对象的`decode`方法并传递以下值，对表单数据进行解码：

   * 包含PDF表单的`com.adobe.idp.Document`对象。
   * 一个`java.lang.Boolean`对象，它指定是否对PDF417条形码进行解码。
   * 一个`java.lang.Boolean`对象，它指定是否解码数据矩阵条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码QR码条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码codabar条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码代码128条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码代码39条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码EAN-13条形码。
   * 一个`java.lang.Boolean`对象，它指定是否解码EAN-8条形码。
   * 一个`com.adobe.livecycle.barcodedforms.CharSet`明细列表值，它指定条形码中使用的字符集编码值。

   `decode`方法返回包含已解码表单数据的`org.w3c.dom.Document`对象。

1. 将数据转换为XML数据源

   通过调用`BarcodedFormsServiceClient`对象的`extractToXML`方法并传递以下值，将解码的数据转换为XDP或XFDF数据：

   * 包含解码数据的`org.w3c.dom.Document`对象（请确保使用`decode`方法的返回值）。
   * 指定行分隔符的`com.adobe.livecycle.barcodedforms.Delimiter`明细列表值。 建议您指定`Delimiter.Carriage_Return`。
   * 指定字段分隔符的`com.adobe.livecycle.barcodedforms.Delimiter`明细列表值。 例如，指定`Delimiter.Tab`。
   * 一个`com.adobe.livecycle.barcodedforms.XMLFormat`明细列表值，它指定将条形码数据转换为XDP还是XFDF XML数据。 例如，指定`XMLFormat.XDP`将数据转换为XDP数据。

   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   `extractToXML`方法返回一个`java.util.List`对象，其中每个元素都是一个`org.w3c.dom.Document`对象。 表单上的每个条形码都有一个单独的元素。 也就是说，如果表单上有四个条码，则返回的`java.util.List`对象中有四个元素。

1. 处理解码的数据

   * 对`java.util.List`对象进行迭代，以获取位于该列表中的每个`org.w3c.dom.Document`对象。
   * 对于列表中的每个元素，将`org.w3c.dom.Document`对象转换为`com.adobe.idp.Document`对象。 （使用Java API示例将`org.w3c.dom.Document`对象转换为`com.adobe.idp.Document`对象的应用程序逻辑显示在解码条形码表单数据中）。
   * 通过调用`com.adobe.idp.Document`对象的`copyToFile`并传递表示XML文件的File对象，将XML数据另存为XML文件。

**另请参阅**

[快速开始（SOAP模式）：使用Java API解码条形码表单数据](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#decode-barcoded-form-data-using-the-web-service-api}解码条形码表单数据

使用barcoded forms API（web服务）对表单数据进行解码：

1. 包括项目文件

   * 创建一个Microsoft .NET客户端程序集，它使用barcoded forms服务WSDL。 有关信息，请参阅[使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)调用AEM Forms。
   * 引用Microsoft .NET客户端程序集。 有关信息，请参阅[使用Base64编码](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)调用AEM Forms中的“引用.NET客户端程序集”。

1. 创建条形码表单客户端API对象

   使用使用barcoded forms服务WSDL的Microsoft .NET客户端程序集，通过调用其默认构造函数创建`BarcodedFormsServiceService`对象。

1. 获取包含条形码数据的PDF表单

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储包含条形码的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`System.IO.FileStream`对象的内容。 可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将`binaryData`属性赋予字节数组的内容，填充`BLOB`对象。

1. 从PDF表单解码数据

   通过调用`BarcodedFormsServiceService`对象的`decode`方法并传递以下值，对表单数据进行解码：

   * 包含PDF表单的`BLOB`对象。
   * 一个`Boolean`对象，它指定是否对PDF417条形码进行解码。
   * 一个`Boolean`对象，它指定是否解码数据矩阵条形码。
   * 一个`Boolean`对象，它指定是否解码QR码条形码。
   * 一个`Boolean`对象，它指定是否解码codabar条形码。
   * 一个`Boolean`对象，它指定是否解码代码128条形码。
   * 一个`Bolean`对象，它指定是否解码代码39条形码。
   * 一个`Boolean`对象，它指定是否解码EAN-13条形码。
   * 一个`Boolean`对象，它指定是否解码EAN-8条形码。
   * 一个`CharSet`明细列表值，它指定条形码中使用的字符集编码值。

   `decode`方法返回包含已解码表单数据的字符串值。

1. 将数据转换为XML数据源

   通过调用`BarcodedFormsServiceService`对象的`extractToXML`方法并传递以下值，将解码的数据转换为XDP或XFDF数据：

   * 包含解码数据的字符串值（请确保使用`decode`方法的返回值）。
   * 指定行分隔符的`Delimiter`明细列表值。 建议您指定`Delimiter.Carriage_Return`。
   * 指定字段分隔符的`Delimiter`明细列表值。 例如，指定`Delimiter.Tab`。
   * 一个`XMLFormat`明细列表值，它指定将条形码数据转换为XDP还是XFDF XML数据。 例如，指定`XMLFormat.XDP`将数据转换为XDP数据。

   >[!NOTE]
   >
   >请勿为行分隔符和字段分隔符参数指定相同的值。

   `extractToXML`方法返回一个`Object`数组，其中每个元素都是一个`BLOB`实例。 表单上的每个条形码都有一个单独的元素。 也就是说，如果表单上有四个条码，则返回的`Object`数组中有四个元素。

1. 处理解码的数据

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示受保护PDF文档的文件位置。
   * 创建一个字节数组，用于存储`encryptPDFUsingPassword`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`binaryData`数据成员的值来填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象，创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
