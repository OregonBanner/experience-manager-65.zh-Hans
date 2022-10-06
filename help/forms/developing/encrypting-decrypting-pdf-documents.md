---
title: 加密和解密PDF文档
seo-title: Encrypting and Decrypting PDF Documents
description: 使用加密服务来加密和解密文档。 该加密服务任务包括：用密码对PDF文档加密；用证书对PDF文档加密；从PDF文档中删除基于密码的加密；从PDF文档中删除基于证书的加密；解锁PDF文档以便能够执行其他服务操作；以及确定安全PDF文档的加密类型。
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8189'
ht-degree: 0%

---

# 加密和解密PDF文档 {#encrypting-and-decrypting-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于加密服务**

加密服务允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问。 如果PDF文档使用密码进行加密，则用户必须指定打开密码，才能在Adobe Reader或Adobe Acrobat中查看该文档。 同样，如果PDF文档使用证书进行加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥来解密PDF文档。

您可以使用加密服务完成以下任务：

* 使用密码加密PDF文档。 (请参阅 [使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* 使用证书加密PDF文档。 (请参阅 [使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* 从PDF文档中删除基于密码的加密。 (请参阅 [删除密码加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* 从PDF文档中删除基于证书的加密。 (请参阅 [删除基于证书的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* 解锁PDF文档，以便能够执行其他服务操作。 例如，在解锁密码加密的PDF文档后，您可以对其应用数字签名。 (请参阅 [解锁加密PDF文档](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* 确定安全PDF文档的加密类型。 (请参阅 [确定加密类型](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

## 使用密码加密PDF文档 {#encrypting-pdf-documents-with-a-password}

使用密码加密PDF文档时，用户必须指定密码才能在Adobe Reader或Acrobat中打开PDF文档。 此外，在可以对文档执行其他AEM Forms操作(例如对PDF文档进行数字签名)之前，必须解锁密码加密的PDF文档。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，则它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前，不要对其进行加密。 (请参阅 [编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要使用密码加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密客户端API对象。
1. 获取要加密的PDF文档。
1. 设置加密运行时选项。
1. 添加密码。
1. 将加密的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。

**获取要加密的PDF文档**

必须获取未加密的PDF文档，才能使用密码加密文档。 如果尝试保护已加密的PDF文档，则会引发异常。

**设置加密运行时选项**

要使用密码加密PDF文档，请指定四个值，包括两个密码值。 第一个密码值用于加密PDF文档，并且必须在打开PDF文档时指定。 第二个密码值(称为主控密码值)用于从PDF文档中删除加密。 密码值区分大小写，并且这两个密码值不能相同。

必须指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据之外的所有内容，或仅加密文档的附件。 如果仅加密文档的附件，则当用户尝试访问文件附件时，系统会提示用户输入密码。

在对PDF文档进行加密时，您可以指定与安全文档关联的权限。 通过指定权限，您可以控制用户打开密码加密的PDF文档时允许执行的操作。 例如，要成功提取表单数据，您必须设置以下权限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>权限指定为 `PasswordEncryptionPermission` 枚举值。

**添加密码**

在检索不安全的PDF文档并设置加密运行时值后，可以向PDF文档添加密码。

**将加密的PDF文档另存为PDF文件**

您可以将密码加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服务API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF文档 {#encrypt-a-pdf-document-using-the-java-api}

使用加密API(Java)使用密码加密PDF文档：

1. 包括项目文件。

   将客户端JAR文件（如adobe-encryption-client.jar）包含在您Java项目的类路径中。

1. 创建加密客户端API。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取要加密的PDF文档。

   * 创建 `java.io.FileInputStream` 表示要使用其构造函数加密的PDF文档的对象，并传递指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 设置加密运行时选项。

   * 创建 `PasswordEncryptionOptionSpec` 对象。
   * 通过调用 `PasswordEncryptionOptionSpec` 对象 `setEncryptOption` 方法和通过 `PasswordEncryptionOption` 指定要加密的文档资源的枚举值。 例如，要加密整个PDF文档（包括其元数据及其附件），请指定 `PasswordEncryptionOption.ALL`.
   * 创建 `java.util.List` 使用 `ArrayList` 构造函数。
   * 通过调用 `java.util.List` 对象s `add` 方法和传递与要设置的权限对应的枚举值。 例如，要设置允许用户复制位于PDF文档中的数据的权限，请指定 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. （对要设置的每个权限重复此步骤）。
   * 通过调用 `PasswordEncryptionOptionSpec` 对象 `setCompatability` 方法和传递指定Acrobat兼容性级别的枚举值。 例如，您可以指定 `PasswordEncryptionCompatability.ACRO_7`.
   * 指定允许用户通过调用 `PasswordEncryptionOptionSpec` 对象 `setDocumentOpenPassword` 方法和传递表示打开密码的字符串值。
   * 指定主控密码值，该值允许用户通过调用 `PasswordEncryptionOptionSpec` 对象 `setPermissionPassword` 方法和传递表示主控密码的字符串值。

1. 添加密码。

   通过调用 `EncryptionServiceClient` 对象 `encryptPDFUsingPassword` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含要使用密码加密的PDF文档的对象。
   * 的 `PasswordEncryptionOptionSpec` 包含加密运行时选项的对象。

   的 `encryptPDFUsingPassword` 方法返回 `com.adobe.idp.Document` 包含密码加密PDF文档的对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象。 确保使用 `com.adobe.idp.Document` 由返回的对象 `encryptPDFUsingPassword` 方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API加密PDF文档 {#encrypting-a-pdf-document-using-the-web-service-api}

使用密码加密PDF文档(使用Encryption API（Web服务）):

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建加密客户端API对象。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取要加密的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储使用密码加密的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。

1. 设置加密运行时选项。

   * 创建 `PasswordEncryptionOptionSpec` 对象。
   * 通过分配 `PasswordEncryptionOption` 枚举值 `PasswordEncryptionOptionSpec` 对象 `encryptOption` 数据成员。 要加密整个PDF（包括其元数据及其附件），请分配 `PasswordEncryptionOption.ALL` 到此数据成员。
   * 通过分配 `PasswordEncryptionCompatability` 枚举值 `PasswordEncryptionOptionSpec` 对象 `compatability` 数据成员。 例如，分配 `PasswordEncryptionCompatability.ACRO_7` 到此数据成员。
   * 指定密码值，以允许用户通过为 `PasswordEncryptionOptionSpec` 对象 `documentOpenPassword` 数据成员。
   * 指定口令值，该口令值允许用户通过为PDF文档分配表示主控口令的字符串值来从密码文档中删除加密 `PasswordEncryptionOptionSpec` 对象 `permissionPassword` 数据成员。

1. 添加密码。

   通过调用 `EncryptionServiceClient` 对象 `encryptPDFUsingPassword` 方法和传递以下值：

   * 的 `BLOB` 包含要使用密码加密的PDF文档的对象。
   * 的 `PasswordEncryptionOptionSpec` 包含加密运行时选项的对象。

   的 `encryptPDFUsingPassword` 方法返回 `BLOB` 包含密码加密PDF文档的对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示安全PDF文档的文件位置。
   * 创建用于存储 `BLOB` 由返回的对象 `encryptPDFUsingPassword` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用证书加密PDF文档 {#encrypting-pdf-documents-with-certificates}

基于证书的加密允许您通过公钥技术加密特定收件人的文档。 可以为不同的收件人授予文档不同的权限。 公钥技术使加密的许多方面成为可能。 算法用于生成两个大数，称为 *键*，具有以下属性：

* 一个密钥用于加密一组数据。 随后，只能使用其他密钥解密数据。
* 不可能区分一个键和另一个键。

其中一个密钥用作用户的私钥。 只有用户才有权访问此密钥，这一点很重要。 另一个密钥是用户的公共密钥，可以与他人共享。

公钥证书包含用户的公钥和标识信息。 X.509格式用于存储证书。 证书通常由证书颁发机构(CA)颁发并进行数字签名，该机构是一个公认的实体，可提供对证书有效性的置信度。 证书的过期日期为，之后证书将不再有效。 此外，证书吊销列表(CRL)还提供有关证书过期日期之前已吊销的证书的信息。 CRL由证书颁发机构定期发布。 证书的吊销状态也可以通过网络上的联机证书状态协议(OCSP)进行检索。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，则它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前，不要对其进行加密。 (请参阅 [编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>在使用证书加密PDF文档之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用信任管理器API以编程方式添加的。 (请参阅 [使用信任管理器API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-1}

要使用证书加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密客户端API对象。
1. 获取要加密的PDF文档。
1. 引用证书。
1. 设置加密运行时选项。
1. 创建证书加密的PDF文档。
1. 将加密的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建 `EncrytionServiceClient` 对象。 如果您使用Web服务加密服务API，请创建 `EncryptionServiceService` 对象。

**获取要加密的PDF文档**

必须获取未加密的PDF文档才能加密。 如果尝试保护已加密的PDF文档，则会引发异常。

**引用证书**

要使用证书加密PDF文档，请引用用于加密PDF文档的证书。 证书是.cer文件、.crt文件或.pem文件。 PKCS#12文件用于存储具有相应证书的私钥。

使用证书对PDF文档进行加密时，请指定与安全文档关联的权限。 通过指定权限，您可以控制打开证书加密PDF文档的用户可以执行的操作。

**设置加密运行时选项**

指定要加密的PDF文档资源。 您可以加密整个PDF文档、除文档元数据之外的所有内容，或仅加密文档的附件。

**创建证书加密的PDF文档**

在检索不安全的PDF文档、引用证书并设置运行时选项后，您可以创建一个证书加密的PDF文档。 PDF文档加密后，需要相应的公钥才能解密。

**将加密的PDF文档另存为PDF文件**

您可以将加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服务API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用加密API(Java)使用证书加密PDF文档：

1. 包括项目文件。

   将客户端JAR文件（如adobe-encryption-client.jar）包含在您Java项目的类路径中。

1. 创建加密客户端API对象。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取要加密的PDF文档。

   * 创建 `java.io.FileInputStream` 表示要使用其构造函数加密的PDF文档的对象，并传递指定PDF文档位置的字符串值。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用证书。

   * 创建 `java.util.List` 使用其构造函数存储权限信息的对象。
   * 通过调用 `java.util.List` 对象 `add` 方法和通过 `CertificateEncryptionPermissions` 枚举值，表示授予打开安全PDF文档的用户的权限。 例如，要指定所有权限，请通过 `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * 创建 `Recipient` 对象。
   * 创建 `java.io.FileInputStream` 对象，表示用于通过使用其构造函数并传递指定证书位置的字符串值来加密PDF文档的证书。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 表示证书的对象。
   * 调用 `Recipient` 对象 `setX509Cert` 方法和通过 `com.adobe.idp.Document` 包含证书的对象。 (此外， `Recipient`对象可以将Truststore证书别名或LDAP URL作为证书源。)
   * 创建 `CertificateEncryptionIdentity` 使用其构造函数存储权限和证书信息的对象。
   * 调用 `CertificateEncryptionIdentity` 对象 `setPerms` 方法和通过 `java.util.List` 存储权限信息的对象。
   * 调用 `CertificateEncryptionIdentity` 对象 `setRecipient` 方法和通过 `Recipient` 存储证书信息的对象。
   * 创建 `java.util.List` 使用其构造函数存储证书信息的对象。
   * 调用 `java.util.List` 对象的add方法并传递 `CertificateEncryptionIdentity` 对象。 (此 `java.util.List` 对象将作为参数传递到 `encryptPDFUsingCertificates` 方法。)

1. 设置加密运行时选项。

   * 创建 `CertificateEncryptionOptionSpec` 对象。
   * 通过调用 `CertificateEncryptionOptionSpec` 对象 `setOption` 方法和通过 `CertificateEncryptionOption` 指定要加密的文档资源的枚举值。 例如，要加密整个PDF文档（包括其元数据及其附件），请指定 `CertificateEncryptionOption.ALL`.
   * 通过调用 `CertificateEncryptionOptionSpec` 对象 `setCompat` 方法和通过 `CertificateEncryptionCompatibility` 指定Acrobat兼容性级别的枚举值。 例如，您可以指定 `CertificateEncryptionCompatibility.ACRO_7`.

1. 创建证书加密的PDF文档。

   通过调用 `EncryptionServiceClient` 对象 `encryptPDFUsingCertificates` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含要加密的PDF文档的对象。
   * 的 `java.util.List` 存储证书信息的对象。
   * 的 `CertificateEncryptionOptionSpec` 包含加密运行时选项的对象。

   的 `encryptPDFUsingCertificates` 方法返回 `com.adobe.idp.Document` 包含证书加密的PDF文档的对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `com.adobe.idp.Document` 对象。 确保使用 `com.adobe.idp.Document` 由返回的对象 `encryptPDFUsingCertificates` 方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API使用证书对PDF文档进行加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用加密API（Web服务）使用证书加密PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建加密客户端API对象。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取要加密的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储使用证书加密的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。

1. 引用证书。

   * 创建 `Recipient` 对象。 此对象将存储证书信息。
   * 创建 `BLOB` 对象。 此 `BLOB` 对象将存储加密PDF文档的证书。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示证书的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。
   * 分配 `BLOB` 将证书存储到 `Recipient` 对象 `x509Cert` 数据成员。
   * 创建 `CertificateEncryptionIdentity` 使用其构造函数存储证书信息的对象。
   * 分配 `Recipient` 将证书存储到 `CertificateEncryptionIdentity`对象的收件人数据成员。
   * 创建 `Object` 阵列并分配 `CertificateEncryptionIdentity` 对象到的 `Object` 数组。 此 `Object` 数组作为参数传递给 `encryptPDFUsingCertificates` 方法。

1. 设置加密运行时选项。

   * 创建 `CertificateEncryptionOptionSpec` 对象。
   * 通过分配 `CertificateEncryptionOption` 枚举值 `CertificateEncryptionOptionSpec` 对象 `option` 数据成员。 要加密整个PDF文档（包括其元数据及其附件），请分配 `CertificateEncryptionOption.ALL` 到此数据成员。
   * 通过分配 `CertificateEncryptionCompatibility` 枚举值 `CertificateEncryptionOptionSpec` 对象 `compat` 数据成员。 例如，分配 `CertificateEncryptionCompatibility.ACRO_7` 到此数据成员。

1. 创建证书加密的PDF文档。

   通过调用 `EncryptionServiceService` 对象 `encryptPDFUsingCertificates` 方法和传递以下值：

   * 的 `BLOB` 包含要加密的PDF文档的对象。
   * 的 `Object` 用于存储证书信息的数组。
   * 的 `CertificateEncryptionOptionSpec` 包含加密运行时选项的对象。

   的 `encryptPDFUsingCertificates` 方法返回 `BLOB` 包含证书加密的PDF文档的对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示安全PDF文档的文件位置。
   * 创建用于存储 `BLOB` 由返回的对象 `encryptPDFUsingCertificates` 方法。 通过获取 `BLOB` 对象 `binaryData` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除基于证书的加密 {#removing-certificate-based-encryption}

可以从PDF文档中删除基于证书的加密，以便用户可以在Adobe Reader或Acrobat中打开PDF文档。 要从使用证书加密的PDF文档中删除加密，必须引用公钥。 从PDF文档中删除加密后，加密不再安全。

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-2}

要从PDF文档中删除基于证书的加密，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除加密。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

**创建加密服务客户端**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建 `EncrytionServiceClient` 对象。 如果您使用Web服务加密服务API，请创建 `EncryptionServiceService` 对象。

**获取加密的PDF文档**

必须获取加密的PDF文档才能删除基于证书的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。 同样，如果尝试从密码加密文档中删除基于证书的加密，则会引发异常。

**删除加密**

要从加密的PDF文档中删除基于证书的加密，您需要加密的PDF文档和与用于加密PDF文档的密钥对应的私钥。 在从加密的PDF文档中删除基于证书的加密时指定私钥的别名值。 有关公钥的信息，请参阅 [使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>私钥存储在AEM Forms信任存储区中。 将证书放置到此处时，将指定别名值。

**保存PDF文档**

在从加密的PDF文档中删除基于证书的加密后，您可以将PDF文档另存为PDF文件。 用户可以在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[使用Java API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服务API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-java-api}

使用加密API(Java)从PDF文档中删除基于证书的加密：

1. 包括项目文件。

   将客户端JAR文件（如adobe-encryption-client.jar）包含在您Java项目的类路径中。

1. 创建加密服务客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取加密的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象通过使用其构造函数并传递指定加密PDF文档位置的字符串值来表示加密PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 删除加密。

   通过调用 `EncryptionServiceClient` 对象 `removePDFCertificateSecurity` 方法和传递以下值：

   * 的 `com.adobe.idp.Document` 包含加密PDF文档的对象。
   * 一个字符串值，用于指定与用于加密PDf文档的密钥对应的私钥的别名。

   的 `removePDFCertificateSecurity` 方法返回 `com.adobe.idp.Document` 包含不安全的PDF文档的对象。

1. 保存PDF文档。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `Document` 对象。 确保使用 `com.adobe.idp.Document` 由返回的对象 `removePDFCredentialSecurity` 方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API删除基于证书的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用加密API（Web服务）删除基于证书的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取加密的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储加密的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。

1. 删除加密。

   调用 `EncryptionServiceClient` 对象 `removePDFCertificateSecurity` 方法并传递以下值：

   * 的 `BLOB` 包含表示加密PDF文档的文件流数据的对象。
   * 一个字符串值，用于指定与用于加密PDf文档的私钥对应的公钥的别名。

   的 `removePDFCredentialSecurity` 方法返回 `BLOB` 包含不安全的PDF文档的对象。

1. 保存PDF文档。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示不安全PDF文档的文件位置。
   * 创建用于存储 `BLOB` 由返回的对象 `removePDFPasswordSecurity` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除密码加密 {#removing-password-encryption}

可以从PDF文档中删除基于密码的加密，以便用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。 在从PDF文档中删除基于密码的加密后，该文档不再安全。

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-3}

要从PDF文档中删除基于密码的加密，请执行以下步骤：

1. 包含项目文件
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除密码。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

将必需的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建加密服务客户端**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建 `EncrytionServiceClient` 对象。 如果您使用Web服务加密服务API，请创建 `EncryptionServiceService` 对象。

**获取加密的PDF文档**

必须获取加密的PDF文档才能删除基于密码的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。

**删除密码**

要从加密的PDF文档中删除基于密码的加密，您需要加密的PDF文档和用于从PDF文档中删除加密的主控密码值。 用于打开密码加密的PDF文档的密码不能用于删除加密。 在用密码加密PDF文档时指定主控密码。 (请参阅 [使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**保存PDF文档**

在加密服务从PDF文档中删除基于密码的加密后，您可以将PDF文档另存为PDF文件。 用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API删除基于密码的加密 {#remove-password-based-encryption-using-the-java-api}

使用加密API(Java)从PDF文档中删除基于密码的加密：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取加密的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象使用其构造函数并传递指定PDF文档位置的字符串值来表示已加密的PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 删除密码。

   通过调用 `EncryptionServiceClient` 对象 `removePDFPasswordSecurity` 方法和传递以下值：

   * A `com.adobe.idp.Document` 包含加密PDF文档的对象。
   * 一个字符串值，用于指定用于从PDF文档中删除加密的主控密码值。

   的 `removePDFPasswordSecurity` 方法返回 `com.adobe.idp.Document` 包含不安全的PDF文档的对象。

1. 保存PDF文档。

   * 创建 `java.io.File` 对象，并确保文件扩展名为.pdf。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 复制内容的方法 `Document` 对象。 确保使用 `Document` 由返回的对象 `removePDFPasswordSecurity` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API删除基于密码的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服务API删除基于密码的加密 {#remove-password-based-encryption-using-the-web-service-api}

使用加密API（Web服务）删除基于密码的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取加密的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储密码加密的PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。

1. 删除密码。

   调用 `EncryptionServiceService` 对象 `removePDFPasswordSecurity` 方法并传递以下值：

   * 的 `BLOB` 包含表示加密PDF文档的文件流数据的对象。
   * 一个字符串值，用于指定用于从PDF文档中删除加密的密码值。 在使用密码加密PDF文档时指定此值。

   的 `removePDFPasswordSecurity` 方法返回 `BLOB` 包含不安全的PDF文档的对象。

1. 保存PDF文档。

   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示不安全PDF文档的文件位置。
   * 创建用于存储 `BLOB` 由返回的对象 `removePDFPasswordSecurity` 方法。 通过获取 `BLOB` 对象 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象，方法是调用其构造函数并传递 `System.IO.FileStream` 对象。
   * 通过调用 `System.IO.BinaryWriter` 对象 `Write` 方法和传递字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解锁加密PDF文档 {#unlocking-encrypted-pdf-documents}

必须先解锁密码加密或证书加密的PDF文档，然后才能对其执行其他AEM Forms操作。 如果尝试对加密的PDF文档执行操作，将生成异常。 解锁加密的PDF文档后，可以对其执行一个或多个操作。 这些操作可以属于其他服务，如Acrobat Reader DC扩展服务。

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-4}

要解锁加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 解锁文档。
1. 执行AEM Forms操作。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

**创建加密服务客户端**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建 `EncrytionServiceClient` 对象。 如果您使用Web服务加密服务API，请创建 `EncryptionServiceService` 对象。

**获取加密的PDF文档**

您必须获取加密的PDF文档才能解锁。 如果尝试解锁未加密的PDF文档，则会引发异常。

**解锁文档**

要解锁密码加密的PDF文档，您需要加密的PDF文档和用于打开密码加密的PDF文档的密码值。 在使用密码加密PDF文档时指定此值。 (请参阅 [使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

要解锁证书加密的PDF文档，您需要加密的PDF文档以及与用于加密PDF文档的私钥对应的公钥的别名值。

**执行AEM Forms操作**

解锁加密的PDF文档后，您可以对其执行其他服务操作，如对其应用使用权限。 此操作属于Acrobat Reader DC扩展服务。

**另请参阅**

[使用Java API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服务API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用加密API(Java)解锁加密的PDF文档：

1. 包括项目文件。

   将客户端JAR文件（如adobe-encryption-client.jar）包含在您Java项目的类路径中。

1. 创建加密服务客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取加密的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象通过使用其构造函数并传递指定加密PDF文档位置的字符串值来表示加密PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 解锁文档。

   通过调用 `EncryptionServiceClient` 对象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法。

   要解锁使用密码加密的PDF文档，请调用 `unlockPDFUsingPassword` 方法并传递以下值：

   * A `com.adobe.idp.Document` 包含密码加密PDF文档的对象。
   * 一个字符串值，用于指定用于打开密码加密的PDF文档的密码值。 在使用密码加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用 `unlockPDFUsingCredential` 方法并传递以下值：

   * A `com.adobe.idp.Document` 包含证书加密PDF文档的对象。
   * 一个字符串值，用于指定与用于加密PDF文档的私钥对应的公钥的别名。

   的 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都返回 `com.adobe.idp.Document` 对象。

1. 执行AEM Forms操作。

   对已解锁的PDF文档执行AEM Forms操作，以满足您的业务要求。 例如，假定您要将使用权限应用于已解锁的PDF文档，请将 `com.adobe.idp.Document` 由以下任一方返回的对象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 对象 `applyUsageRights` 方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API解锁加密的PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）

[将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用加密API（Web服务）解锁加密的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取加密的PDF文档。

   * 创建 `BLOB` 对象。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。

1. 解锁文档。

   通过调用 `EncryptionServiceClient` 对象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法。

   要解锁使用密码加密的PDF文档，请调用 `unlockPDFUsingPassword` 方法并传递以下值：

   * A `BLOB` 包含密码加密PDF文档的对象。
   * 一个字符串值，用于指定用于打开密码加密的PDF文档的密码值。 在使用密码加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用 `unlockPDFUsingCredential` 方法并传递以下值：

   * A `BLOB` 包含证书加密PDF文档的对象。
   * 一个字符串值，用于指定与用于加密PDf文档的私钥对应的公钥的别名。

   的 `unlockPDFUsingPassword` 和 `unlockPDFUsingCredential` 方法都返回 `com.adobe.idp.Document` 传递给其他AEM Forms方法以执行操作的对象。

1. 执行AEM Forms操作。

   对已解锁的PDF文档执行AEM Forms操作，以满足您的业务要求。 例如，假定您要将使用权限应用于已解锁的PDF文档，请将 `BLOB` 由以下任一方返回的对象 `unlockPDFUsingPassword` 或 `unlockPDFUsingCredential` 方法 `ReaderExtensionsServiceClient` 对象 `applyUsageRights` 方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 确定加密类型 {#determining-encryption-type}

您可以使用Java Encryption Service API或Web服务Encryption Service API以编程方式确定用于保护PDF文档的加密类型。 有时需要动态确定PDF文档是否已加密，如果已加密，则需要确定加密类型。 例如，您可以确定PDF文档是使用基于密码的加密还是Rights Management策略进行保护。

PDF文档可以受以下加密类型的保护：

* 基于密码的加密
* 基于证书的加密
* 由Rights Management服务创建的策略
* 另一种加密

>[!NOTE]
>
>有关加密服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary_of_steps-5}

要确定保护PDF文档的加密类型，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 确定加密类型。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此变量为必需变量)
* jbossall-client.jar(如果AEM Forms部署在JBoss应用程序服务器上，则此为必需字段)

**创建服务客户端**

要以编程方式执行加密服务操作，您必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建 `EncrytionServiceClient` 对象。 如果您使用Web服务加密服务API，请创建 `EncryptionServiceService` 对象。

**获取加密的PDF文档**

必须获取PDF文档，才能确定要保护该文档的加密类型。

**确定加密类型**

您可以确定用于保护PDF文档的加密类型。 如果PDF文档未受保护，则加密服务会通知您PDF文档未受保护。

**另请参阅**

[使用Java API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服务API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速入门](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保护文档](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API确定加密类型 {#determine-the-encryption-type-using-the-java-api}

确定使用加密API(Java)保护PDF文档的加密类型：

1. 包括项目文件。

   将客户端JAR文件（如adobe-encryption-client.jar）包含在您Java项目的类路径中。

1. 创建服务客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `EncryptionServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 获取加密的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，该对象使用其构造函数并传递指定PDF文档位置的字符串值来表示PDF文档。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 确定加密类型。

   * 通过调用 `EncryptionServiceClient` 对象 `getPDFEncryption` 方法和通过 `com.adobe.idp.Document` 包含PDF文档的对象。 此方法将返回 `EncryptionTypeResult` 对象。
   * 调用 `EncryptionTypeResult` 对象 `getEncryptionType` 方法。 此方法将返回 `EncryptionType` 指定加密类型的枚举值。 例如，如果PDF文档受基于密码的加密保护，此方法将返回 `EncryptionType.PASSWORD`.

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门（SOAP模式）：使用Java API确定加密类型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API确定加密类型 {#determine-the-encryption-type-using-the-web-service-api}

确定使用加密API（Web服务）保护PDF文档的加密类型：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建服务客户端。

   * 创建 `EncryptionServiceClient` 对象。
   * 创建 `EncryptionServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.) 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `EncryptionServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 获取加密的PDF文档。

   * 创建 `BLOB` 对象。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 对象，方法是将字节数组的内容分配给 `BLOB` 对象 `MTOM` 数据成员。

1. 确定加密类型。

   * 调用 `EncryptionServiceClient` 对象 `getPDFEncryption` 方法和通过 `BLOB` 包含PDF文档的对象。 此方法将返回 `EncryptionTypeResult` 对象。
   * 获取的值 `EncryptionTypeResult` 对象 `encryptionType` 数据方法。 例如，如果PDF文档受基于密码的加密保护，则此数据成员的值为 `EncryptionType.PASSWORD`.

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
