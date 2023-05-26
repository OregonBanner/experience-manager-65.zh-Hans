---
title: 数字签名和认证文档
seo-title: Digitally Signing and Certifying Documents
description: 使用签名服务向PDF文档添加和删除数字签名字段、检索位于PDF文档中的签名字段的名称、修改签名字段、对PDF文档进行数字签名、验证PDF文档中的数字签名、验证PDF文档中的所有数字签名、以及从PDF文档中删除数字签名。
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# 数字签名和认证文档 {#digitally-signing-and-certifying-documents}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

**关于签名服务**

签名服务允许贵组织保护其分发和接收的Adobe PDF文档的安全性和隐私。 此服务使用数字签名和认证，确保只有目标收件人才能更改文档。 由于安全功能应用于文档本身，因此文档在整个生命周期中保持安全和受控制。 在防火墙之外，当文档离线下载以及将文档提交回您的组织时，文档将保持安全。

>[!NOTE]
>
>您可以为签名服务创建自定义签名处理程序，在调用某些操作(如签署PDF文档)时调用该签名服务。

**签名字段名称**

某些签名服务操作要求您指定执行操作的签名字段的名称。 例如，在签署PDF文档时，您可以指定要签名的签名字段的名称。 假定签名字段的全名是 `form1[0].Form1[0].SignatureField1[0]`. 您可以指定 `SignatureField1[0]` 而不是 `form1[0].Form1[0].SignatureField1[0]`.

有时，冲突会导致签名服务签署（或执行其他需要签名字段名称的操作）错误的字段。 此冲突是名称的结果 `SignatureField1[0]` 出现在同一PDF文档中的两个或多个位置。 例如，假定一个PDF文档包含两个名为的签名字段 `form1[0].Form1[0].SignatureField1[0]` 和 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 并且您指定 `SignatureField1[0]`. 在这种情况下，签名服务在遍历文档中的所有签名字段时对其找到的第一个签名字段进行签名。

如果PDF文档中有多个签名字段，建议您指定签名字段的全名。 即，指定 `form1[0].Form1[0].SignatureField1[0]`而不是 `SignatureField1[0]`.

您可以使用Signature服务完成这些任务：

* 向PDF文档添加和删除数字签名字段。 (请参阅 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields).)
* 检索位于PDF文档中的签名字段的名称。 (请参阅 [正在检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* 修改签名字段。 (请参阅 [修改签名字段](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* 对PDF文档进行数字签名。 (请参阅 [对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* 认证PDF文档。 (请参阅 [认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* 验证位于PDF文档中的数字签名。 (请参阅 [验证数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 验证PDF文档中的所有数字签名。 (请参阅 [验证多个数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 从签名字段中删除数字签名。 (请参阅 [删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>有关Signature服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)..

## 添加签名字段 {#adding-signature-fields}

数字签名出现在签名字段中，这些签名字段是包含签名的图形表示的表单字段。 签名字段可以是可见的，也可以不可见。 签名者可以使用预先存在的签名字段，也可以以编程方式添加签名字段。 无论哪种情况，签名字段都必须存在，然后才能对PDF文档进行签名。

您可以使用签名服务Java API或签名Web服务API以编程方式添加签名字段。 您可以将多个签名字段添加到PDF文档；但是，每个签名字段名称必须是唯一的。

>[!NOTE]
>
>某些PDF文档类型不允许您以编程方式添加签名字段。 有关Signature服务和添加签名字段的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要将签名字段添加到PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取添加了签名字段的PDF文档。
1. 添加签名字段。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建签名客户端**

必须先创建签名服务客户端，然后才能以编程方式执行签名服务操作。

**获取添加了签名字段的PDF文档**

您必须获取添加签名字段的PDF文档。

**添加签名字段**

要成功地将签名字段添加到PDF文档，请指定标识签名字段位置的坐标值。 （如果添加不可见的签名字段，则不需要这些值。） 此外，您还可以指定在将签名应用于签名字段后，PDF文档中的哪些字段被锁定。

**将PDF文档另存为PDF文件**

签名服务向PDF文档添加签名字段后，您可以将文档另存为PDF文件，以便用户在Acrobat或Adobe Reader中打开它。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API添加签名字段 {#add-signature-fields-using-the-java-api}

使用签名API (Java)添加签名字段：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在Java项目的类路径中。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取添加了签名字段的PDF文档

   * 创建 `java.io.FileInputStream` 表示签名字段添加到的PDF文档的对象，方法是使用其构造函数并传递指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 添加签名字段

   * 创建 `PositionRectangle` 使用构造函数指定签名字段位置的对象。 在构造函数中，指定坐标值。
   * 如果需要，可创建 `FieldMDPOptions` 指定在将数字签名应用于签名字段时锁定的字段的对象。
   * PDF通过调用 `SignatureServiceClient` 对象的 `addSignatureField` 方法，并传递以下值：

      * A `com.adobe.idp`. `Document` 表示已向其添加签名字段的PDF文档的对象。
      * 一个字符串值，它指定签名字段的名称。
      * A `java.lang.Integer` 表示向其添加签名字段的页码的值。
      * A `PositionRectangle` 指定签名字段位置的对象。
      * A `FieldMDPOptions` 指定在将数字签名应用于签名字段后锁定的PDF文档中的字段的对象。 此参数值是可选的，您可以传递 `null`.
   * A `PDFSeedValueOptions` 指定各种运行时值的对象。 此参数值是可选的，您可以传递 `null`.

      此 `addSignatureField` 方法返回 `com.adobe.idp`. `Document` 表示包含签名字段的PDF文档的对象。
   >[!NOTE]
   >
   >您可以调用 `SignatureServiceClient` 对象的 `addInvisibleSignatureField` 方法以添加不可见的签名字段。

1. 将PDF文档另存为PDF文件

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp`. `Document` 对象的 `copyToFile` 用于复制目录内容的方法 `Document` 对象到文件。 确保您使用 `com.adobe.idp`. `Document` 返回的对象 `addSignatureField` 方法。

**另请参阅**

[签名服务API快速启动](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服务API添加签名字段 {#add-signature-fields-using-the-web-service-api}

要使用签名API（Web服务）添加签名字段，请执行以下操作：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取添加了签名字段的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储将包含签名字段的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性与字节数组的内容。

1. 添加签名字段

   PDF通过调用 `SignatureServiceClient` 对象的 `addSignatureField` 方法，并传递以下值：

   * A `BLOB` 表示已向其添加签名字段的PDF文档的对象。
   * 指定签名字段名称的字符串值。
   * 一个整数值，表示向其中添加签名字段的页码。
   * A `PositionRect` 指定签名字段位置的对象。
   * A `FieldMDPOptions` 指定在将数字签名应用于签名字段后锁定的PDF文档中的字段的对象。 此参数值是可选的，您可以传递 `null`.
   * A `PDFSeedValueOptions` 指定各种运行时值的对象。 此参数值是可选的，您可以传递 `null`.

   此 `addSignatureField` 方法返回 `BLOB` 表示包含签名字段的PDF文档的对象。

1. 将PDF文档另存为PDF文件

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置，其中将包含签名字段和打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `addSignatureField` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在检索签名字段名称 {#retrieving-signature-field-names}

您可以检索位于要签名或认证的PDF文档中的所有签名字段的名称。 如果不确定位于PDF文档中的签名字段名称，或者要验证该名称，则可以通过编程方式检索它们。 Signature服务返回签名字段的完全限定名称，例如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>有关Signature服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤摘要 {#summary_of_steps-1}

要检索签名字段名称，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含签名字段的PDF文档。
1. 检索签名字段名称。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

必须先创建签名服务客户端，然后才能以编程方式执行签名服务操作。

**获取包含签名字段的PDF文档**

检索包含签名字段的PDF文档。

**检索签名字段名称**

在检索包含一个或多个签名字段的PDF文档后，可以检索签名字段名称。

**另请参阅**

[使用Java API检索签名字段名称](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服务API检索签名字段](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API检索签名字段名称 {#retrieve-signature-field-names-using-the-java-api}

使用签名API (Java)检索签名字段名称：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在Java项目的类路径中。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取包含签名字段的PDF文档

   * 创建 `java.io.FileInputStream` 表示包含签名字段的PDF文档的对象，方法是使用其构造函数并传递指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 检索签名字段名称

   * 通过调用 `SignatureServiceClient` 对象的 `getSignatureFieldList` 方法和传递 `com.adobe.idp.Document` 包含包含签名字段的PDF文档的对象。 此方法会返回 `java.util.List` 对象，其中每个元素包含 `PDFSignatureField` 对象。 使用此对象，您可以获取有关签名字段的其他信息，如它是否可见。
   * 循环访问 `java.util.List` 确定是否存在签名字段名称的对象。 对于PDF文档中的每个签名字段，您可以获取单独的 `PDFSignatureField` 对象。 要获取签名字段的名称，请调用 `PDFSignatureField` 对象的 `getName` 方法。 此方法返回一个指定签名字段名称的字符串值。

**另请参阅**

[正在检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入门（SOAP模式）：使用Java API检索签名字段名称](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索签名字段 {#retrieve-signature-field-using-the-web-service-api}

使用签名API（Web服务）检索签名字段名称：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取包含签名字段的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含签名字段的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 字段字节数组内容。

1. 检索签名字段名称

   * 通过调用检索签名字段名称 `SignatureServiceClient` 对象的 `getSignatureFieldList` 方法和传递 `BLOB` 包含包含签名字段的PDF文档的对象。 此方法会返回 `MyArrayOfPDFSignatureField` 集合对象，其中每个元素包含 `PDFSignatureField` 对象。
   * 循环访问 `MyArrayOfPDFSignatureField` 用于确定是否存在签名字段名称的对象。 对于PDF文档中的每个签名字段，您可以获取 `PDFSignatureField` 对象。 要获取签名字段的名称，请调用 `PDFSignatureField` 对象的 `getName` 方法。 此方法返回一个指定签名字段名称的字符串值。

**另请参阅**

[正在检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改签名字段 {#modifying-signature-fields}

您可以使用Java API和Web服务API修改位于PDF文档中的签名字段。 修改签名字段涉及处理其签名字段锁定字典值或种子值字典值。

A *字段锁定词典* 指定签名字段签名时锁定的字段列表。 锁定的字段可阻止用户对该字段进行更改。 A *种子值字典* 包含应用签名时使用的约束信息。 例如，您可以更改在不使签名失效的情况下控制可能发生的操作的权限。

通过修改现有签名字段，可以更改PDF文档以反映不断变化的业务要求。 例如，新的业务要求可能要求在签署文档后锁定所有文档字段。

本节说明如何通过修改字段锁定字典和种子值字典值来修改签名字段。 对签名字段锁定字典所做的更改导致签名字段签名时PDF文档中的所有字段被锁定。 对种子值词典所做的更改禁止对文档进行特定类型的更改。

>[!NOTE]
>
>有关Signature服务和修改签名字段的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-2}

要修改位于PDF文档中的签名字段，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要修改的签名字段的PDF文档。
1. 设置字典值。
1. 修改签名字段。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包含LiveCycleJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

必须先创建签名服务客户端，然后才能以编程方式执行签名服务操作。

**获取包含要修改的签名字段的PDF文档**

检索包含要修改的签名字段的PDF文档。

**设置字典值**

要修改签名字段，请为其字段锁定字典或种子值字典分配值。 指定签名字段锁定字典值涉及指定签名字段签名时锁定的PDF文档字段。 （本节讨论如何锁定所有字段。）

可以设置以下种子值字典值：

* **修订检查**：指定在将签名应用于签名字段时是否执行吊销检查。
* **证书选项**：将值分配给证书种子值字典。 在指定证书选项之前，建议您熟悉证书种子值词典。 (请参阅 [PDF引用](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **摘要选项**：分配用于签名的摘要算法。 有效值为SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **筛选条件**：指定与签名字段一起使用的过滤器。 例如，您可以使用Adobe.PPKLite过滤器。 (请参阅 [PDF引用](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **标记选项**：指定与此签名字段关联的标志值。 值为1表示签名者必须仅使用条目指定的值。 值为0表示允许使用其他值。 以下是Bit位置：

   * **1（过滤器）：** 用于对签名字段签名的签名处理程序
   * **2（子过滤器）：** 一个名称数组，指示签名时要使用的可接受编码
   * **3 (V)**：用于对签名字段签名的签名处理程序的最低要求版本号
   * **4（原因）：** 一个字符串数组，指定签署文档的可能原因
   * **5 (PDFLegalWarnings)：** 一个字符串数组，用于指定可能的法律证明

* **法律证明**：当文档经过认证时，将自动扫描特定类型的内容，这些内容可能会使文档的可见内容含糊或误导用户。 例如，注释可能会模糊文本，而这些文本对于了解所认证的内容非常重要。 扫描过程会生成指示存在此类内容的警告。 它还提供了可能生成警告的内容的其他解释。
* **权限**：指定可用于文档而不使签名失效的PDF的权限。
* **原因**：指定必须对此文档签名的原因。
* **时间戳**：指定时间戳选项。 例如，您可以设置所使用时间戳服务器的URL。
* **版本**：指定用于对签名字段签名的签名处理程序的最小版本号。

**修改签名字段**

创建签名服务客户端后，检索包含要修改的签名字段的PDF文档，并设置字典值，可以指示Signature service修改签名字段。 然后，签名服务返回包含修改后的签名字段的PDF文档。 原始PDF文档不受影响。

**将PDF文档另存为PDF文件**

将包含修改后的签名字段的PDF文档保存为PDF文件，以便用户可以在Acrobat或Adobe Reader中打开该文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[签名服务API快速启动](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改签名字段 {#modify-signature-fields-using-the-java-api}

使用签名API (Java)修改签名字段：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取包含要修改的签名字段的PDF文档

   * 创建 `java.io.FileInputStream` 表示包含签名字段的PDF文档的对象，可通过使用其构造函数并传递指定PDF文档位置的字符串值来修改该文档。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置字典值

   * 创建 `PDFSignatureFieldProperties` 对象。 A `PDFSignatureFieldProperties` 对象存储签名字段锁定字典和种子值字典信息。
   * 创建 `PDFSeedValueOptionSpec` 对象。 此对象允许您设置种子值字典值。
   * PDF通过调用 `PDFSeedValueOptionSpec` 对象的 `setMdpValue` 方法和传递 `MDPPermissions.NoChanges` 枚举值。
   * 创建 `FieldMDPOptionSpec` 对象。 此对象允许您设置签名字段锁定字典值。
   * PDF通过调用 `FieldMDPOptionSpec` 对象的 `setMdpValue` 方法和传递 `FieldMDPAction.ALL` 枚举值。
   * 通过调用 `PDFSignatureFieldProperties` 对象的 `setSeedValue` 方法和传递 `PDFSeedValueOptionSpec` 对象。
   * 通过调用 `PDFSignatureFieldProperties`对象的 `setFieldMDP` 方法和传递 `FieldMDPOptionSpec` 对象。

   >[!NOTE]
   >
   >要查看可以设置的所有种子值字典值，请参阅 `PDFSeedValueOptionSpec` 类引用。 (请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. 修改签名字段

   通过调用 `SignatureServiceClient` 对象的 `modifySignatureField` 方法，并传递以下值：

   * 此 `com.adobe.idp.Document` 存储包含要修改的签名字段的PDF文档的对象
   * 指定签名字段名称的字符串值
   * 此 `PDFSignatureFieldProperties` 存储签名字段锁定字典和种子值字典信息的对象

   此 `modifySignatureField` 方法返回 `com.adobe.idp.Document` 存储包含修改后的签名字段的PDF文档的对象。

1. 将PDF文档另存为PDF文件

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制目录内容的方法 `com.adobe.idp.Document` 对象到文件。 确保您使用 `com.adobe.idp.Document` 对象 `modifySignatureField` 方法已返回。

### 使用Web服务API修改签名字段 {#modify-signature-fields-using-the-web-service-api}

使用签名API（Web服务）修改签名字段：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取包含要修改的签名字段的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含要修改的签名字段的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。

1. 设置字典值

   * 创建 `PDFSignatureFieldProperties` 对象。 此对象存储签名字段锁定字典和种子值字典信息。
   * 创建 `PDFSeedValueOptionSpec` 对象。 此对象允许您设置种子值字典值。
   * 通过分配PDF文档来禁止对其进行更改 `MDPPermissions.NoChanges` 的枚举值 `PDFSeedValueOptionSpec` 对象的 `mdpValue` 数据成员。
   * 创建 `FieldMDPOptionSpec` 对象。 此对象允许您设置签名字段锁定字典值。
   * 通过分配PDF文档中的所有字段 `FieldMDPAction.ALL` 的枚举值 `FieldMDPOptionSpec` 对象的 `mdpValue` 数据成员。
   * 通过分配 `PDFSeedValueOptionSpec` 对象 `PDFSignatureFieldProperties` 对象的 `seedValue` 数据成员。
   * 通过分配 `FieldMDPOptionSpec` 对象 `PDFSignatureFieldProperties` 对象的 `fieldMDP` 数据成员。

   >[!NOTE]
   >
   >要查看可以设置的所有种子值字典值，请参阅 `PDFSeedValueOptionSpec` 类引用。 (请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改签名字段

   通过调用 `SignatureServiceClient` 对象的 `modifySignatureField` 方法，并传递以下值：

   * 此 `BLOB` 存储包含要修改的签名字段的PDF文档的对象
   * 指定签名字段名称的字符串值
   * 此 `PDFSignatureFieldProperties` 存储签名字段锁定字典和种子值字典信息的对象

   此 `modifySignatureField` 方法返回 `BLOB` 存储包含修改后的签名字段的PDF文档的对象。

1. 将PDF文档另存为PDF文件

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示将包含签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 对象 `addSignatureField` 方法会返回。 通过获取的值填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对PDF文档进行数字签名 {#digitally-signing-pdf-documents}

可以将数字签名应用于PDF文档，以提供一定程度的安全性。 数字签名（如手写签名）提供了一种方法，签名者通过它来标识自己并就文档发表声明。 用于对文档进行数字签名的技术，有助于确保签名者和收件人都清楚已签署的内容，并且确信文档自签署以来未发生更改。

PDF文件采用公钥技术签名。 签名者有两个密钥：公钥和私钥。 私钥存储在用户的凭据中，该凭据在签名时必须可用。 公钥存储在用户的证书中，收件人必须可以使用它来验证签名。 证书吊销列表(CRL)和由证书颁发机构(CA)分发的联机证书状态协议(OCSP)响应中可以找到有关吊销证书的信息。 签名时间可以从称为时间戳颁发机构的受信任源获得。

>[!NOTE]
>
>在对PDF文档进行数字签名之前，必须确保将证书添加到AEM Forms。 使用管理控制台或以编程方式使用信任管理器API添加证书。 (请参阅 [使用信任管理器API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

您可以以编程方式对PDF文档进行数字签名。 对PDF文档进行数字签名时，必须引用AEM Forms中存在的安全凭据。 凭据是用于签名的私钥。

签名服务在签署PDF文档时执行以下步骤：

1. 签名服务通过传递请求中指定的别名从Truststore检索凭据。
1. Truststore搜索指定的凭据。
1. 凭据将返回到Signature服务，并用于签署文档。 此外，还会根据别名缓存凭据，以供将来请求使用。

有关处理安全凭据的信息，请参阅 *安装和部署AEM Forms* 应用程序服务器的指南。

>[!NOTE]
>
>签名和认证文档之间存在差异。 (请参阅 [认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>并非所有PDF文档都支持签名。 有关Signature服务和数字签名文档的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>签名服务不支持将PDF数据嵌入到操作输入的XDP文件，例如证书文档。 此操作导致签名服务抛出 `PDFOperationException`. 要解决此问题，请使用PDF实用程序服务将XDP文件转换为PDF文件，然后将转换后的PDF文件传递给签名服务操作。 (请参阅 [使用PDF实用程序](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**nCipher nShield HSM凭据**

使用nCipher nShield HSM凭据签名或认证PDF文档时，只有在重新启动部署AEM Forms的J2EE应用程序服务器后，才能使用新凭据。 但是，您可以设置配置值，从而无需重新启动J2EE应用程序服务器即可执行签名或认证操作。

可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

**签名不受信任**

在对同一PDF文档进行认证和签名时，如果认证签名不可信，则在Acrobat或Adobe Reader中打开PDF文档时，第一个签名旁边会出现一个黄色三角形。 为了避免这种情况，认证签名必须可信。

**签署基于XFA的表单**

如果您尝试使用签名服务API对基于XFA的表单进行签名，则可能缺少 `View` `Signed` `Version` (位于Acrobat)。 例如，请考虑以下工作流：

* 通过使用设计器创建的XDP文件，可以合并包含签名字段的表单设计和包含表单数据的XML数据。 您可以使用Forms服务生成交互式PDF文档。
* 您可使用签名服务API对PDF文档进行签名。

### 步骤摘要 {#summary_of_steps-3}

要对PDF文档进行数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名服务客户端。
1. 获取要签名的PDF文档。
1. 签署PDF文档。
1. 将已签名的PDF文件另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建签名客户端**

必须先创建签名服务客户端，然后才能以编程方式执行签名服务操作。

**获取要签名的PDF文档**

要对PDF文档进行签名，必须获取包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行签名。 签名字段可以通过使用设计器或以编程方式添加。

**签署PDF文档**

签名PDF文档时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

可以使用 `PDFSignatureAppearanceOptionSpec` 对象。 例如，您可以通过调用 `PDFSignatureAppearanceOptionSpec` 对象的 `setShowDate` 方法和传递 `true`.

您还可以指定是否执行吊销检查，以确定用于对PDF文档进行数字签名的证书是否已吊销。 要执行吊销检查，可以指定以下值之一：

* **NoCheck**：不执行吊销检查。
* **BestEfort**：始终尝试检查链中所有证书的吊销情况。 如果在检查时出现任何问题，则假定吊销有效。 如果发生任何故障，则假定证书未被吊销。
* **CheckIfAvailable：** 如果撤销信息可用，请检查链中所有证书的撤销。 如果在检查时出现任何问题，则假定吊销无效。 如果发生任何故障，则假定证书被吊销且无效。 （这是默认值。）
* **AlwaysCheck**：检查是否撤销链中的所有证书。 如果任何证书中不存在吊销信息，则假定吊销无效。

要对证书执行吊销检查，可以使用指定到证书吊销列表(CRL)服务器的URL `CRLOptionSpec` 对象。 但是，如果要执行吊销检查，但未指定CRL服务器的URL，则签名服务将从证书中获取该URL。

在执行吊销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，在使用OCSP服务器而不是CRL服务器时，执行吊销检查的速度会更快。 (请参阅“在线证书状态协议”，网址为 [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在Adobe应用程序和服务中设置了OCSP服务器，则会检查OCSP服务器，然后检查CRL服务器。 （请参阅AAC帮助中的“使用信任存储区管理证书和凭据”）。

如果您指定不执行吊销检查，则签名服务不会检查用于签名或证明文档的证书是否已吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>虽然可以在证书中指定CRL或OCSP服务器，但可以使用覆盖证书中指定的URL `CRLOptionSpec` 和 `OCSPOptionSpec` 对象。 例如，要覆盖CRL服务器，您可以调用 `CRLOptionSpec` 对象的 `setLocalURI` 方法。

时间戳是指跟踪已签署或已验证文档修改时间的过程。 文档一旦签署，即不应对其进行修改，即使文档所有者也不应进行修改。 时间戳有助于强制实施已签署或已认证文档的有效性。 可以使用设置时间戳选项 `TSPOptionSpec` 对象。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务浏览部分以及相应的快速启动中，使用吊销检查。 由于未指定CRL或OCSP服务器信息，因此服务器信息是从用于对PDF文档进行数字签名的证书中获取的。

要成功签署PDF文档，您可以指定包含数字签名的签名字段的完全限定名称，例如 `form1[0].#subform[1].SignatureField3[3]`. 在使用XFA表单字段时，还可以使用签名字段的部分名称： `SignatureField3[3]`.

您还必须引用安全凭据才能对PDF文档进行数字签名。 要引用安全凭据，请指定别名。 别名是对PKCS#12文件（扩展名为.pfx）或硬件安全模块(HSM)中实际凭据的引用。 有关安全凭据的信息，请参阅 *安装和部署AEM Forms* 应用程序服务器的指南。

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件，以便用户在Acrobat或Adobe Reader中打开文档。

**另请参阅**

[使用Java API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服务API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

[正在检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API对PDF文档进行数字签名 {#digitally-sign-pdf-documents-using-the-java-api}

使用签名API (Java)对PDF文档进行数字签名：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在Java项目的类路径中。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取要签名的PDF文档

   * 创建 `java.io.FileInputStream` 表示要数字签名的PDF文档的对象，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 签署PDF文档

   PDF通过调用 `SignatureServiceClient` 对象的 `sign` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 表示要签名的PDF文档的对象。
   * 一个字符串值，表示将包含数字签名的签名字段的名称。
   * A `Credential` 表示用于对PDF文档进行数字签名的凭据的对象。 创建 `Credential` 对象 `Credential` 对象的静态 `getInstance` 方法和传递一个字符串值，该值指定与安全凭据对应的别名值。
   * A `HashAlgorithm` 指定静态数据成员的对象，该成员表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个字符串值，表示PDF文档被数字签名的原因。
   * 表示签名者联系信息的字符串值。
   * A `PDFSignatureAppearanceOptions` 控制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * A `java.lang.Boolean` 指定是否对签名者的证书执行吊销检查的对象。
   * An `OCSPOptionSpec` 存储联机证书状态协议(OCSP)支持的首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 此参数是可选的，可以是 `null`. 有关更多信息，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   此 `sign` 方法返回 `com.adobe.idp.Document` 表示已签署PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 方法和路径 `java.io.File`以复制 `Document` 对象到文件。 确保您使用 `com.adobe.idp.Document` 返回的对象 `sign` 方法。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入门（SOAP模式）：使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对PDF文档进行数字签名 {#digitally-signing-pdf-documents-using-the-web-service-api}

要使用签名API（Web服务）对PDF文档进行数字签名，请执行以下操作：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取要签名的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储已签名的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。

1. 签署PDF文档

   PDF通过调用 `SignatureServiceClient` 对象的 `sign` 方法，并传递以下值：

   * A `BLOB` 表示要签名的PDF文档的对象。
   * 一个字符串值，表示将包含数字签名的签名字段的名称。
   * A `Credential` 表示用于对PDF文档进行数字签名的凭据的对象。 创建 `Credential` 对象，并通过将值指定给 `Credential` 对象的 `alias` 属性。
   * A `HashAlgorithm` 指定静态数据成员的对象，该成员表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个布尔值，指定是否使用哈希算法。
   * 一个字符串值，表示PDF文档被数字签名的原因。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * A `PDFSignatureAppearanceOptions` 控制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * A `System.Boolean` 指定是否对签名者的证书执行吊销检查的对象。 如果完成此吊销检查，则会将其嵌入签名中。 默认为 `false`。
   * An `OCSPOptionSpec` 存储联机证书状态协议(OCSP)支持的首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`. 有关此对象的信息，请参见 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 此参数是可选的，可以是 `null`.

   此 `sign` 方法返回 `BLOB` 表示已签署PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `sign` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对交互式Forms进行数字签名 {#digitally-signing-interactive-forms}

您可以对Forms服务创建的交互式表单进行签名。 例如，请考虑以下工作流：

* 您可以合并使用设计器创建的基于XFA的PDF表单，并使用Forms服务合并位于XML文档中的表单数据。 Forms服务器渲染交互式表单。
* 您可使用签名服务API对交互式表单进行签名。

结果是一个经过数字签名的交互式PDF表单。 在签署基于XFA表单的PDF表单时，请确保将PDF文件另存为Adobe静态PDF表单。 如果尝试对另存为“PDF动态PDF”表单的Adobe表单进行签名，则会发生异常。 由于您正在对从Forms服务返回的表单进行签名，因此请确保该表单包含签名字段。

>[!NOTE]
>
>在对交互式表单进行数字签名之前，必须确保将证书添加到AEM Forms。 使用管理控制台或以编程方式使用信任管理器API添加证书。 (请参阅 [使用信任管理器API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

使用Forms服务API时，将 `GenerateServerAppearance` 运行时选项 `true`. 此运行时选项可确保在Acrobat或Adobe Reader中打开时，服务器上生成的表单外观保持有效。 在使用Forms API生成要签名的交互式表单时，建议您设置此运行时选项。

>[!NOTE]
>
>在阅读数字签名交互式Forms之前，建议您熟悉签名PDF文档。 (请参阅 [对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 步骤摘要 {#summary_of_steps-4}

要对Forms服务返回的交互式表单进行数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建Forms和签名客户端。
1. 使用Forms服务获取交互式表单。
1. 对交互式表单进行签名。
1. 将已签名的PDF文件另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建Forms和签名客户端**

由于此工作流会同时调用Forms和签名服务，因此请创建Forms服务客户端和签名服务客户端。

**使用Forms服务获取交互式表单**

您可以使用Forms服务获取要签名的交互式PDF表单。 从AEM Forms开始，您可以传递 `com.adobe.idp.Document` 包含要呈现的表单的Forms服务的对象。 此方法的名称为 `renderPDFForm2`. 此方法会返回 `com.adobe.idp.Document` 包含要签名的表单的对象。 您可以传递此 `com.adobe.idp.Document` 实例到Signature service。

同样，如果您使用的是Web服务，则可以传递 `BLOB` Forms服务返回到Signature服务的实例。

>[!NOTE]
>
>与“数字签名交互式Forms”部分关联的快速入门将调用 `renderPDFForm2` 方法。

**签署交互式表单**

签名PDF文档时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

可以使用 `PDFSignatureAppearanceOptionSpec` 对象。 例如，您可以通过调用 `PDFSignatureAppearanceOptionSpec` 对象的 `setShowDate` 方法和传递 `true`.

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件。 PDF文件可在Acrobat或Adobe Reader中打开。

**另请参阅**

[使用Java API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用Web服务API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[渲染交互式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API对交互式表单进行数字签名 {#digitally-sign-an-interactive-form-using-the-java-api}

使用Forms和签名API (Java)对交互式表单进行数字签名：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar和adobe-forms-client.jar）包含在Java项目的类路径中。

1. 创建Forms和签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。
   * 创建 `FormsServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 使用Forms服务获取交互式表单

   * 创建 `java.io.FileInputStream` 表示要使用构造函数传递到Forms服务的PDF文档的对象。 传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。
   * 创建 `java.io.FileInputStream` 表示包含表单数据的XML文档的对象，将使用该文档的构造函数传递到Forms服务。 传递一个指定XML文件位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。
   * 创建 `PDFFormRenderSpec` 用于设置运行时选项的对象。 调用 `PDFFormRenderSpec` 对象的 `setGenerateServerAppearance` 方法和路径 `true`.
   * 调用 `FormsServiceClient` 对象的 `renderPDFForm2` 方法，并传递以下值：

      * A `com.adobe.idp.Document` 包含要渲染的PDF表单的对象。
      * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。
      * A `PDFFormRenderSpec` 存储运行时选项的对象。
      * A `URLSpec` 包含Forms服务所需的URI值的对象。 您可以指定 `null` 参数值。
      * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

      此 `renderPDFForm2` 方法返回 `FormsResult` 包含表单数据流的对象

   * PDF通过调用 `FormsResult` 对象的 `getOutputContent` 方法。 此方法会返回 `com.adobe.idp.Document` 表示交互式表单的对象。


1. 签署交互式表单

   PDF通过调用 `SignatureServiceClient` 对象的 `sign` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 表示要签名的PDF文档的对象。 确保此对象是 `com.adobe.idp.Document` 从Forms服务获得的对象。
   * 一个字符串值，表示已签名的签名字段的名称。
   * A `Credential` 表示用于对PDF文档进行数字签名的凭据的对象。 创建 `Credential` 对象 `Credential` 对象的静态 `getInstance` 方法。 传递一个字符串值，该值指定与安全凭据对应的别名值。
   * A `HashAlgorithm` 指定静态数据成员的对象，该成员表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个字符串值，表示PDF文档被数字签名的原因。
   * 表示签名者联系信息的字符串值。
   * A `PDFSignatureAppearanceOptions` 控制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * A `java.lang.Boolean` 指定是否对签名者的证书执行吊销检查的对象。
   * An `OCSPPreferences` 存储联机证书状态协议(OCSP)支持的首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 此参数是可选的，可以是 `null`.

   此 `sign` 方法返回 `com.adobe.idp.Document` 表示已签署PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 方法和路径 `java.io.File`以复制 `Document` 对象到文件。 确保您使用 `com.adobe.idp.Document` 对象 `sign` 方法已返回。

**另请参阅**

[对交互式Forms进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入门（SOAP模式）：使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对交互式表单进行数字签名 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用Forms和签名API（Web服务）对交互式表单进行数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 为与Signature服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   对与Forms服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   因为 `BLOB` 数据类型对两个服务引用都是通用的，完全限定 `BLOB` 数据类型。 在相应的Web服务快速启动中，所有 `BLOB` 实例是完全限定的。

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建Forms和签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >对Forms服务客户端重复这些步骤。

1. 使用Forms服务获取交互式表单

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储已签名的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。
   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储表单数据。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示包含表单数据的XML文件的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。
   * 创建 `PDFFormRenderSpec` 用于设置运行时选项的对象。 分配值 `true` 到 `PDFFormRenderSpec` 对象的 `generateServerAppearance` 字段。
   * 调用 `FormsServiceClient` 对象的 `renderPDFForm2` 方法，并传递以下值：

      * A `BLOB` 包含要渲染的PDF表单的对象。
      * A `BLOB` 包含要与表单合并的数据的对象。
      * A `PDFFormRenderSpec` 存储运行时选项的对象。
      * A `URLSpec` 包含Forms服务所需的URI值的对象。 您可以指定 `null` 参数值。
      * A `java.util.HashMap` 存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
      * 长输出参数，用于存储表单中的页数。
      * 用于区域设置值的字符串输出参数。
      * A `FormResult` 用于存储交互式表单的输出参数。
   * PDF通过调用 `FormsResult` 对象的 `outputContent` 字段。 此字段存储 `BLOB` 表示交互式表单的对象。


1. 签署交互式表单

   PDF通过调用 `SignatureServiceClient` 对象的 `sign` 方法，并传递以下值：

   * A `BLOB` 表示要签名的PDF文档的对象。 使用 `BLOB` Forms服务返回的实例。
   * 一个字符串值，表示已签名的签名字段的名称。
   * A `Credential` 表示用于对PDF文档进行数字签名的凭据的对象。 创建 `Credential` 对象，并通过将值指定给 `Credential` 对象的 `alias` 属性。
   * A `HashAlgorithm` 指定静态数据成员的对象，该成员表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个布尔值，指定是否使用哈希算法。
   * 一个字符串值，表示PDF文档被数字签名的原因。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * A `PDFSignatureAppearanceOptions` 控制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * A `System.Boolean` 指定是否对签名者的证书执行吊销检查的对象。 如果完成此吊销检查，则会将其嵌入签名中。 默认为 `false`。
   * An `OCSPPreferences` 存储联机证书状态协议(OCSP)支持的首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`. 有关此对象的信息，请参见 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 此参数是可选的，可以是 `null`.

   此 `sign` 方法返回 `BLOB` 表示已签署PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `sign` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[对交互式Forms进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## 认证PDF文档 {#certifying-pdf-documents}

您可以通过使用称为认证签名的特定签名类型来认证PDF文档来保护文档。 认证签名与数字签名的区别如下：

* 它必须是应用于PDF文件的第一个签名；也就是说，在应用认证签名时，文件中的任何其他签名字段都必须未签名。 PDF文档中只允许一个认证签名。 如果要签署和认证PDF文档，则必须在签署之前对其进行认证。 在认证PDF文档后，您可以对附加签名字段进行数字签名。
* 文档的作者或创建者可以指定以特定方式修改文档，而不会使已验证签名失效。 例如，文档可能允许填写表单或添加注释。 如果作者指定不允许进行某些修改，则Acrobat会限制用户以这种方式修改文档。 如果进行了此类修改，例如使用其他应用程序，则认证签名无效，Acrobat会在用户打开文档时发出警告。 （对于未验证的签名，不会阻止修改，并且正常的编辑操作不会使原始签名失效。）
* 在签署时，将扫描文档以查找可能会使文档内容不明确或误导性的特定内容类型。 例如，注释可能会遮盖页面上的某些文本，而这些文本对于了解正在验证的内容非常重要。 可以就此类内容提供解释（法律证明）。

您可以使用签名服务Java API或签名Web服务API以编程方式认证PDF文档。 在认证PDF文档时，必须引用凭据服务中存在的安全凭据。 有关安全凭据的信息，请参阅 *安装和部署AEM Forms* 应用程序服务器的指南。

>[!NOTE]
>
>在对同一PDF文档进行认证和签名时，如果认证签名不可信，则当您在Acrobat或Adobe Reader中打开PDF文档时，第一个签名签名旁边会出现一个黄色三角形。 验证签名必须可信以避免这种情况。

>[!NOTE]
>
>使用nCipher nShield HSM凭据签署或认证PDF文档时，只有在重新启动部署AEM Forms的J2EE应用程序服务器后，才能使用新凭据。 但是，您可以设置配置值，从而无需重新启动J2EE应用程序服务器即可执行签名或认证操作。

可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc （或c：\nfast\cknfastrc）：

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

>[!NOTE]
>
>有关Signature服务和证明文档的更多信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-5}

要认证PDF文档，请执行下列任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取要认证的PDF文档。
1. 认证PDF文档。
1. 将认证的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

必须先创建签名客户端，然后才能以编程方式执行签名操作。

**获取要认证的PDF文档**

要认证PDF文档，必须获得包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行认证。 签名字段可以通过使用设计器或以编程方式添加。 有关以编程方式添加签名字段的信息，请参见 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields).

**认证PDF文档**

要成功认证PDF单据，您需要以下输入值，签名服务使用这些值来认证PDF单据：

* **PDF文档**：包含签名字段的PDF文档，签名字段是包含已验证签名的图形表示的表单字段。 PDF文档必须包含签名字段，然后才能进行认证。 签名字段可以通过使用设计器或以编程方式添加。 (请参阅 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **签名字段名称**：已验证的签名字段的完全限定名称。 以下值是一个示例： `form1[0].#subform[1].SignatureField3[3]`. 在使用XFA表单字段时，还可以使用签名字段的部分名称： `SignatureField3[3]`. 如果为字段名称传递了null值，则会动态创建并验证不可见的签名字段。
* **安全凭据**：用于验证PDF文档的凭据。 此安全凭据包含密码和别名，它们必须与Credential服务内凭据中显示的别名匹配。 别名是对PKCS#12文件（扩展名为.pfx）或硬件安全模块(HSM)中实际凭据的引用。
* **哈希算法**：用于摘要PDF文档的哈希算法。
* **签名原因**：在Acrobat或Adobe Reader中显示的值，以便其他用户知道PDF文档获得认证的原因。
* **签名者的位置**：凭据指定的签名者的位置。
* **联系信息**：签名者的联系信息，如地址和电话号码。
* **权限信息**：控制最终用户可以对文档执行的操作而不导致已验证签名无效的权限。 例如，您可以设置权限，以便对PDF文档所做的任何更改都会导致认证签名无效。
* **法律解释**：当文档经过验证时，将自动扫描其特定类型的内容，这可能会使文档的内容不明确或产生误导。 例如，注释可能会遮盖页面上的某些文本，而这些文本对于了解正在验证的内容非常重要。 扫描过程会生成有关这些类型内容的警告。 此值提供了对可能生成警告的内容的附加说明。
* **外观选项**：控制已验证签名外观的选项。 例如，已验证的签名可以显示日期信息。
* **吊销检查**：此值指定是否对签名者的证书进行吊销检查。 默认设置 `false` 表示不执行吊销检查。
* **OCSP设置**：联机证书状态协议(OCSP)支持的设置，它提供有关用于验证PDF文档的凭据状态的信息。 例如，您可以指定服务器的URL，该服务器提供有关用于登录到PDF文档的凭据的信息。
* **CRL设置**：如果已完成吊销检查，则设置证书吊销列表(CRL)首选项。 例如，您可以指定始终检查凭据是否被吊销。
* **时间戳**：定义应用于已验证签名的时间戳信息的设置。 时间戳表示特定数据在特定时间之前建立。 这些知识有助于在签名者和验证者之间建立信任关系。

**将认证的PDF文档另存为PDF文件**

签名服务验证PDF文档后，您可以将其保存为PDF文件，以便用户在Acrobat或Adobe Reader中打开文档。

**另请参阅**

[使用Java API认证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服务API认证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API认证PDF文档 {#certify-pdf-documents-using-the-java-api}

使用签名API (Java)认证PDF文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取要认证的PDF文档

   * 创建 `java.io.FileInputStream` 表示要验证的PDF文档的对象，验证方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 认证PDF文档

   PDF通过调用 `SignatureServiceClient` 对象的 `certify` 方法，并传递以下值：

   * 此 `com.adobe.idp.Document` 表示要认证的PDF文档的对象。
   * 一个字符串值，表示将包含该签名的签名字段的名称。
   * A `Credential` 表示用于验证PDF文档的凭据的对象。 创建 `Credential` 对象 `Credential` 对象的静态 `getInstance` 方法和传递一个字符串值，该值指定与安全凭据对应的别名值。
   * A `HashAlgorithm` 指定静态数据成员的对象，表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个字符串值，它表示PDF文档获得认证的原因。
   * 表示签名者联系信息的字符串值。
   * A `MDPPermissions` 指定可以对使签名失效的PDF文档执行的操作的对象。
   * A `PDFSignatureAppearanceOptions` 控制认证签名外观的对象。 如果需要，可通过调用方法修改签名的外观，例如 `setShowDate`.
   * 一个字符串值，它说明使签名失效的操作。
   * A `java.lang.Boolean` 指定是否对签名者的证书执行吊销检查的对象。 如果完成此吊销检查，则会将其嵌入签名中。 默认为 `false`。
   * A `java.lang.Boolean` 指定验证的签名字段是否锁定的对象。 如果该字段已锁定，则签名字段将标记为只读，其属性无法修改，不具有所需权限的任何人都无法清除该字段。 默认为 `false`。
   * An `OCSPPreferences` 存储联机证书状态协议(OCSP)支持的首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`. 有关此对象的信息，请参见 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 例如，在您创建 `TSPPreferences` 对象，您可以通过调用 `TSPPreferences` 对象的 `setTspServerURL` 方法。 此参数是可选的，可以是 `null`. 有关更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

   此 `certify` 方法返回 `com.adobe.idp.Document` 表示已验证PDF文档的对象。

1. 将认证的PDF文档另存为PDF文件

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 用于复制目录内容的方法 `com.adobe.idp.Document` 对象到文件。

**另请参阅**

[认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入门（SOAP模式）：使用Java API认证PDF文档](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API认证PDF文档 {#certify-pdf-documents-using-the-web-service-api}

使用签名API（Web服务）认证PDF文档：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取要认证的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储已验证的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要认证的PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 数据成员字节数组的内容。

1. 认证PDF文档

   PDF通过调用 `SignatureServiceClient` 对象的 `certify` 方法，并传递以下值：

   * 此 `BLOB` 表示要认证的PDF文档的对象。
   * 一个字符串值，表示将包含该签名的签名字段的名称。
   * A `Credential` 表示用于验证PDF文档的凭据的对象。 创建 `Credential` 对象，并通过将值指定给 `Credential` 对象的 `alias` 属性。
   * A `HashAlgorithm` 指定静态数据成员的对象，表示用于摘要PDF文档的哈希算法。 例如，您可以指定 `HashAlgorithm.SHA1` 以使用SHA1算法。
   * 一个布尔值，指定是否使用哈希算法。
   * 一个字符串值，它表示PDF文档获得认证的原因。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * An `MDPPermissions` 对象的静态数据成员，指定可以对使签名失效的PDF文档执行的操作。
   * 一个布尔值，指定是否使用 `MDPPermissions` 作为上一个参数值传递的对象。
   * 一个字符串值，它说明使签名失效的操作。
   * A `PDFSignatureAppearanceOptions` 控制认证签名外观的对象。 创建 `PDFSignatureAppearanceOptions` 对象。 可以通过设置特征码的一个数据成员来修改特征码的外观。
   * A `System.Boolean` 指定是否对签名者的证书执行吊销检查的对象。 如果完成此吊销检查，则会将其嵌入签名中。 默认为 `false`。
   * A `System.Boolean` 指定验证的签名字段是否锁定的对象。 如果该字段已锁定，则签名字段将标记为只读，其属性无法修改，不具有所需权限的任何人都无法清除该字段。 默认为 `false`。
   * A `System.Boolean` 指定签名字段是否锁定的对象。 也就是说，如果你通过 `true` 到上一个参数，然后传递 `true` 至此参数。
   * An `OCSPPreferences` 存储联机证书状态协议(OCSP)支持首选项的对象，提供用于验证PDF文档的凭据的状态信息。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `CRLPreferences` 存储证书吊销列表(CRL)首选项的对象。 如果未完成吊销检查，则不会使用此参数，您可以指定 `null`.
   * A `TSPPreferences` 存储时间戳提供程序(TSP)支持的首选项的对象。 例如，在您创建 `TSPPreferences` 对象，您可以通过设置 `TSPPreferences` 对象的 `tspServerURL` 数据成员。 此参数是可选的，可以是 `null`.

   此 `certify` 方法返回 `BLOB` 表示已验证PDF文档的对象。

1. 将认证的PDF文档另存为PDF文件

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示将包含已验证PDF文档的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `certify` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证数字签名 {#verifying-digital-signatures}

可以验证数字签名，以确保已签名的PDF文档未被修改并且数字签名有效。 验证数字签名时，您可以检查签名的状态和签名的属性，如签名者的身份。 在信任数字签名之前，建议您对其进行验证。 验证数字签名时，引用包含数字签名的PDF文档。

假定签名者的身份未知。 在Acrobat中打开PDF文档时，将显示一条警告消息，指出签名者的身份未知，如下图所示。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同样，当您以编程方式验证数字签名时，可以确定签名者的身份状态。 例如，如果您验证上图所示文档中的数字签名，则结果会是签名者的身份未知。

>[!NOTE]
>
>有关签名服务和验证数字签名的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-6}

要验证数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 验证数字签名。
1. 确定签名的状态。
1. 确定签名者的身份。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

以编程方式执行签名服务操作之前，请先创建签名服务客户端。

**获取包含要验证的签名的PDF文档**

要验证用于数字签名或认证PDF文档的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置签名服务在PDF文档中验证签名时使用的PKI运行时选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证器计算机上的时间），以指示使用当前时间。 有关不同时间值的信息，请参见 `VerificationTime` 中的枚举值 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您还可以指定是否在验证过程中执行吊销检查。 例如，您可以执行吊销检查以确定证书是否被吊销。 有关吊销检查选项的信息，请参见 `RevocationCheckStyle` 中的枚举值 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

要对证书执行吊销检查，请使用 `CRLOptionSpec` 对象。 但是，如果您没有指定CRL服务器的URL，则签名服务会从证书中获取该URL。

在执行吊销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，在使用OCSP服务器而不是CRL服务器时，吊销检查的执行速度会更快。 (请参阅 [联机证书状态协议](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe应用程序和服务来设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在Adobe应用程序和服务中设置了OCSP服务器，则会检查OCSP服务器，然后检查CRL服务器。

如果不执行吊销检查，签名服务将不会检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>您可以使用覆盖证书中指定的URL `CRLOptionSpec` 和 `OCSPOptionSpec` 对象。 例如，要覆盖CRL服务器，您可以调用 `CRLOptionSpec` 对象的 `setLocalURI` 方法。

时间戳是指跟踪已签署或已验证文档修改时间的过程。 文档签署后，任何人都无法对其进行修改。 时间戳有助于强制实施已签署或已认证文档的有效性。 可以使用设置时间戳选项 `TSPOptionSpec` 对象。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间设置为 `VerificationTime.CURRENT_TIME` 吊销检查设置为 `RevocationCheckStyle.BestEffort`. 由于未指定CRL或OCSP服务器信息，因此将从证书中获取服务器信息。

**验证数字签名**

要成功验证签名，请指定包含该签名的签名字段的完全限定名，例如 `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表单字段时，您还可以使用签名字段的部分名称： `SignatureField3`.

默认情况下，签名服务将验证后文档可签名的时间限制为65分钟。 如果用户尝试在当前时间验证签名，并且签名时间晚于当前时间且在65分钟内，则签名服务不会创建验证错误。

>[!NOTE]
>
>有关验证签名时所需的其他值，请参见 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**确定签名的状态**

作为验证数字签名的一部分，您可以检查签名的状态。

**确定签名者的身份**

您可以确定签名者的身份，可以是以下值之一：

* **未知**：此签名者未知，因为无法执行签名者验证。
* **受信任**：此签名者值得信任。
* **不受信任**：此签名者不受信任。

**另请参阅**

[使用Java API验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API验证数字签名 {#verify-digital-signatures-using-the-java-api}

使用签名服务API (Java)验证数字签名：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在Java项目的类路径中。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取包含要验证的签名的PDF文档

   * 创建 `java.io.FileInputStream` 表示包含签名的PDF文档的对象，要使用签名的构造函数进行验证。 传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置PKI运行时选项

   * 创建 `PKIOptions` 对象。
   * 通过调用 `PKIOptions` 对象的 `setVerificationTime` 方法和传递 `VerificationTime` 指定验证时间的枚举值。
   * 通过调用设置吊销检查选项 `PKIOptions` 对象的 `setRevocationCheckStyle` 方法和传递 `RevocationCheckStyle` 指定是否执行吊销检查的枚举值。

1. 验证数字签名

   通过调用 `SignatureServiceClient` 对象的 `verify2` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 包含经过数字签名或认证的PDF文档的对象。
   * 一个字符串值，表示包含要验证的签名的签名字段名称。
   * A `PKIOptions` 包含PKI运行时选项的对象。
   * A `VerifySPIOptions` 包含SPI信息的实例。 您可以指定 `null` （对于此参数）。

   此 `verify2` 方法返回 `PDFSignatureVerificationInfo` 包含可用于验证数字签名的信息的对象。

1. 确定签名的状态

   * 通过调用 `PDFSignatureVerificationInfo` 对象的 `getStatus` 方法。 此方法会返回 `SignatureStatus` 指定签名状态的对象。 例如，如果未修改已签名的PDF文档，则此方法将返回 `SignatureStatus.DocumentSigNoChanges`.

1. 确定签名者的身份

   * 通过调用 `PDFSignatureVerificationInfo` 对象的 `getSigner` 方法。 此方法会返回 `IdentityInformation` 对象。
   * 调用 `IdentityInformation` 对象的 `getStatus` 确定签名者身份的方法。 此方法会返回 `IdentityStatus` 指定标识的枚举值。 例如，如果签名者受信任，则此方法将返回 `IdentityStatus.TRUSTED`.

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[快速入门（SOAP模式）：使用Java API验证数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API验证数字签名 {#verify-digital-signatures-using-the-web-service-api}

使用签名服务API（Web服务）验证数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取包含要验证的签名的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含要验证的数字或认证签名的PDF文档。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。

1. 设置PKI运行时选项

   * 创建 `PKIOptions` 对象。
   * 通过分配 `PKIOptions` 对象的 `verificationTime` 数据成员a `VerificationTime` 指定验证时间的枚举值。
   * 通过分配 `PKIOptions` 对象的 `revocationCheckStyle` 数据成员a `RevocationCheckStyle` 指定是否执行吊销检查的枚举值。

1. 验证数字签名

   通过调用 `SignatureServiceClient` 对象的 `verify2` 方法，并传递以下值：

   * 此 `BLOB` 包含经过数字签名或认证的PDF文档的对象。
   * 一个字符串值，表示包含要验证的签名的签名字段名称。
   * A `PKIOptions` 包含PKI运行时选项的对象。
   * A `VerifySPIOptions` 包含SPI信息的实例。 您可以指定 `null` （对于此参数）。

   此 `verify2` 方法返回 `PDFSignatureVerificationInfo` 包含可用于验证数字签名的信息的对象。

1. 确定签名的状态

   通过获取 `PDFSignatureVerificationInfo` 对象的 `status` 数据成员。 此数据成员存储 `SignatureStatus` 指定签名状态的对象。 例如，如果修改了已签名的PDF文档， `status` 数据成员存储值 `SignatureStatus.DocumentSigNoChanges`.

1. 确定签名者的身份

   * 通过检索的值，确定签名者的身份 `PDFSignatureVerificationInfo` 对象的 `signer` 数据成员。 此成员返回 `IdentityInformation` 对象。
   * 检索 `IdentityInformation` 对象的 `status` 用于确定签名者身份的数据成员。 此数据成员返回 `IdentityStatus` 指定标识的枚举值。 例如，如果签名者受信任，则此成员会返回 `IdentityStatus.TRUSTED`.

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证多个数字签名 {#verifying-multiple-digital-signatures}

AEM Forms提供了用于验证位于PDF文档中的所有数字签名的方法。 假设PDF文档包含多个数字签名，这是需要多个签名者签名的业务流程的结果。 例如，假设一项金融交易需要一位贷款管理人员和一位经理的签名。 您可以使用签名服务Java API或Web服务API来验证PDF文档中的所有签名。 验证多个数字签名时，您可以检查每个签名的状态和属性。 在信任数字签名之前，建议您对其进行验证。 建议您熟悉验证单个数字签名。

>[!NOTE]
>
>有关签名服务和验证数字签名的更多信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-7}

要验证多个数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 检索所有数字签名。
1. 对所有签名进行迭代。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

以编程方式执行签名服务操作之前，请先创建签名服务客户端。

**获取包含要验证的签名的PDF文档**

要验证用于数字签名或认证PDF文档的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置以下PKI运行时选项，签名服务在验证PDF文档中的所有签名时使用这些选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证器计算机上的时间），以指示使用当前时间。 有关不同时间值的信息，请参见 `VerificationTime` 中的枚举值 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

您还可以指定是否在验证过程中执行吊销检查。 例如，您可以执行吊销检查以确定证书是否被吊销。 有关吊销检查选项的信息，请参见 `RevocationCheckStyle` 中的枚举值 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

要对证书执行吊销检查，请使用 `CRLOptionSpec` 对象。 但是，如果您没有指定指向CRL服务器的URL，则签名服务会从证书中获取该URL。

在执行吊销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，在使用OCSP服务器而不是CRL服务器时，吊销检查的执行速度会更快。 (请参阅 [联机证书状态协议](https://tools.ietf.org/html/rfc2560).)

您可以使用Adobe应用程序和服务来设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在Adobe应用程序和服务中设置了OCSP服务器，则会检查OCSP服务器，然后检查CRL服务器。

如果不执行吊销检查，签名服务将不会检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>您可以使用覆盖证书中指定的URL `CRLOptionSpec` 和 `OCSPOptionSpec` 对象。 例如，要覆盖CRL服务器，您可以调用 `CRLOptionSpec` 对象的 `setLocalURI` 方法。

时间戳是指跟踪已签署或已验证文档修改时间的过程。 文档签署后，任何人都无法对其进行修改。 时间戳有助于强制实施已签署或已认证文档的有效性。 可以使用设置时间戳选项 `TSPOptionSpec` 对象。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间设置为 `VerificationTime.CURRENT_TIME` 吊销检查设置为 `RevocationCheckStyle.BestEffort`. 由于未指定CRL或OCSP服务器信息，因此将从证书中获取服务器信息。

**检索所有数字签名**

要验证位于PDF文档中的所有数字签名，请从PDF文档中检索数字签名。 所有签名都将返回一个列表。 作为验证数字签名的一部分，检查签名的状态。

>[!NOTE]
>
>与验证单个数字签名不同，验证多个签名时，不需要指定签名字段名称。

**对所有签名进行迭代**

逐个签名进行迭代。 即对每个签名，验证数字签名，并检查签名者的身份和每个签名的状态。 (请参阅 [验证数字签名](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>如果要求是整个文档，则无需迭代所有签名。

**另请参阅**

[使用Java API验证多个数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证多个数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API验证多个数字签名 {#verify-multiple-digital-signatures-using-the-java-api}

使用签名服务API (Java)验证多个数字签名：

1. 包括项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在Java项目的类路径中。

1. 创建签名客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取包含要验证的签名的PDF文档

   * 创建 `java.io.FileInputStream` 表示包含多个数字签名的PDF文档的对象，可通过使用其构造函数进行验证。 传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 设置PKI运行时选项

   * 创建 `PKIOptions` 对象。
   * 通过调用 `PKIOptions` 对象的 `setVerificationTime` 方法和传递 `VerificationTime` 指定验证时间的枚举值。
   * 通过调用设置吊销检查选项 `PKIOptions` 对象的 `setRevocationCheckStyle` 方法和传递 `RevocationCheckStyle` 指定是否执行吊销检查的枚举值。

1. 检索所有数字签名

   调用 `SignatureServiceClient` 对象的 `verifyPDFDocument` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 包含包含包含多个数字签名的PDF文档的对象。
   * A `PKIOptions` 包含PKI运行时选项的对象。
   * A `VerifySPIOptions` 包含SPI信息的实例。 您可以指定 `null` （对于此参数）。

   此 `verifyPDFDocument` 方法返回 `PDFDocumentVerificationInfo` 包含有关PDF文档中所有数字签名信息的对象。

1. 对所有签名进行迭代

   * 通过调用 `PDFDocumentVerificationInfo` 对象的 `getVerificationInfos` 方法。 此方法会返回 `java.util.List` 对象，其中每个元素为 `PDFSignatureVerificationInfo` 对象。 使用 `java.util.Iterator` 对象对签名列表进行迭代。
   * 使用 `PDFSignatureVerificationInfo` 对象，则可以通过调用 `PDFSignatureVerificationInfo` 对象的 `getStatus` 方法。 此方法会返回 `SignatureStatus` 其静态数据成员通知您签名状态的对象。 例如，如果签名未知，此方法将返回 `SignatureStatus.DocumentSignatureUnknown`.

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[快速入门（SOAP模式）：使用Java API验证多个数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API验证多个数字签名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用签名服务API（Web服务）验证多个数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取包含要验证的签名的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象存储包含多个要验证的数字签名的PDF文档。
   * 创建 `System.IO.FileStream` 对象。 传递一个字符串值，该值表示PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性字节数组的内容。

1. 设置PKI运行时选项

   * 创建 `PKIOptions` 对象。
   * 通过分配 `PKIOptions` 对象的 `verificationTime` 数据成员a `VerificationTime` 指定验证时间的枚举值。
   * 通过分配 `PKIOptions` 对象的 `revocationCheckStyle` 数据成员a `RevocationCheckStyle` 指定是否执行吊销检查的枚举值。

1. 检索所有数字签名

   调用 `SignatureServiceClient` 对象的 `verifyPDFDocument` 方法，并传递以下值：

   * A `BLOB` 包含包含包含多个数字签名的PDF文档的对象。
   * A `PKIOptions` 包含PKI运行时选项的对象。
   * A `VerifySPIOptions` 包含SPI信息的实例。 您可以为此参数指定null。

   此 `verifyPDFDocument` 方法返回 `PDFDocumentVerificationInfo` 包含有关PDF文档中所有数字签名信息的对象。

1. 对所有签名进行迭代

   * 通过获取 `PDFDocumentVerificationInfo` 对象的 `verificationInfos` 数据成员。 此数据成员返回 `Object` 数组，其中每个元素为 `PDFSignatureVerificationInfo` 对象。
   * 使用 `PDFSignatureVerificationInfo` 对象，您可以通过获取 `PDFSignatureVerificationInfo` 对象的 `status` 数据成员。 此数据成员返回 `SignatureStatus` 其静态数据成员通知您签名状态的对象。 例如，如果签名未知，此方法将返回 `SignatureStatus.DocumentSignatureUnknown`.

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除数字签名 {#removing-digital-signatures}

必须先从签名字段中删除数字签名，然后才能应用更新的数字签名。 无法覆盖数字签名。 如果尝试将数字签名应用于包含签名的签名字段，则会发生异常。

>[!NOTE]
>
>有关Signature服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-8}

要从签名字段中删除数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要删除的签名的PDF文档。
1. 从签名字段中移除数字签名。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，则包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建签名客户端**

必须先创建签名服务客户端，然后才能以编程方式执行签名服务操作。

**获取包含要删除的签名的PDF文档**

要从PDF文档中删除签名，必须获取包含签名的PDF文档。

**从签名字段中移除数字签名**

要成功地从PDF文档中删除数字签名，必须指定包含数字签名的签名字段的名称。 此外，您必须具有删除数字签名的权限；否则，会发生异常。

**将PDF文档另存为PDF文件**

签名服务从签名字段中移除数字签名后，您可以将PDF文档另存为PDF文件，以便用户可在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服务API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API删除数字签名 {#remove-digital-signatures-using-the-java-api}

使用签名API (Java)删除数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `SignatureServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 获取包含要删除的签名的PDF文档

   * 创建 `java.io.FileInputStream` 表示包含要移除的签名的PDF文档的对象，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 从签名字段中移除数字签名

   通过调用 `SignatureServiceClient` 对象的 `clearSignatureField` 方法，并传递以下值：

   * A `com.adobe.idp.Document` 表示包含要删除的签名的PDF文档的对象。
   * 一个字符串值，指定包含数字签名的签名字段的名称。

   此 `clearSignatureField` 方法返回 `com.adobe.idp.Document` 表示从中删除数字签名的PDF文档的对象。

1. 将PDF文档另存为PDF文件

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象的 `copyToFile` 方法。 传递 `java.io.File` 对象以复制 `com.adobe.idp.Document` 对象到文件。 确保您使用 `Document` 返回的对象 `clearSignatureField` 方法。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入门（SOAP模式）：使用Java API删除数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除数字签名 {#remove-digital-signatures-using-the-web-service-api}

使用签名API（Web服务）删除数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Replace `localhost` 包含托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 创建 `SignatureServiceClient` 对象。
   * 创建 `SignatureServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用 `lc_version` 属性。 创建服务引用时使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `SignatureServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取包含要删除的签名的PDF文档

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储包含要删除的数字签名的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示已签名PDF文档的文件位置和打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法。 传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象(通过指定其 `MTOM` 属性与字节数组的内容。

1. 从签名字段中移除数字签名

   通过调用 `SignatureServiceClient` 对象的 `clearSignatureField` 方法，并传递以下值：

   * A `BLOB` 包含已签名PDF文档的对象。
   * 一个字符串值，表示包含要删除的数字签名的签名字段的名称。

   此 `clearSignatureField` 方法返回 `BLOB` 表示从中删除数字签名的PDF文档的对象。

1. 将PDF文档另存为PDF文件

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示PDF文档的文件位置（包含空签名字段和打开文件的模式）。
   * 创建一个字节数组，用于存储 `BLOB` 返回的对象 `sign` 方法。 通过获取的值填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 方法和传递字节数组。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
