---
title: 加密和解密PDF文档
seo-title: 加密和解密PDF文档
description: 'null'
seo-description: 'null'
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# 加密和解密PDF文档 {#encrypting-and-decrypting-pdf-documents}

**关于加密服务**

Encryption服务允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可解密文档以获得对内容的访问。 如果PDF文档使用密码进行加密，则用户必须指定打开密码，才能在Adobe Reader或Adobe Acrobat中查看文档。 同样，如果PDF文档使用证书加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥对PDF文档进行解密。

您可以使用加密服务完成以下任务:

* 使用口令加密PDF文档。 (请参 [阅使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用证书加密PDF文档。 (请参阅 [使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 从PDF文档中删除基于密码的加密。 (请参阅 [删除密码加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。)
* 从PDF文档中删除基于证书的加密。 (请参阅 [删除基于证书的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。)
* 解锁PDF文档，以便执行其他服务操作。 例如，在解锁密码加密的PDF文档后，您可以对其应用数字签名。 (请参阅解 [锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 确定受保护的PDF文档的加密类型。 (请参阅 [确定加密类型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。)

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密码加密PDF文档 {#encrypting-pdf-documents-with-a-password}

当您使用口令加密PDF文档时，用户必须指定口令才能在Adobe Reader或Acrobat中打开PDF文档。 此外，在对PDF文档进行数字签名等其他AEM表单操作之前，必须先对文档执行密码加密的PDF文档。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，则它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前，不要加密该订阅。 (请参阅 [编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要使用口令加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Encryption Client API对象。
1. 获取要加密的PDF文档。
1. 设置加密运行时选项。
1. 添加密码。
1. 将加密的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。

**获取要加密的PDF文档**

您必须获得未加密的PDF文档，才能使用密码加密文档。 如果尝试保护已加密的PDF文档，则会引起异常。

**设置加密运行时选项**

要使用口令加密PDF文档，请指定四个值，包括两个口令值。 第一个口令值用于加密PDF文档，打开PDF文档时必须指定该值。 第二个口令值（名为主口令值）用于从PDF文档中删除加密。 密码值区分大小写，这两个密码值不能相同。

必须指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据之外的所有内容，或仅加密文档的附件。 如果仅加密文档的附件，则用户尝试访问文件附件时会提示输入口令。

在加密PDF文档时，您可以指定与安全文档关联的权限。 通过指定权限，您可以控制打开密码加密的PDF文档的用户允许执行的操作。 例如，要成功提取表单数据，您必须设置以下权限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>权限指定为 `PasswordEncryptionPermission` 明细列表值。

**添加密码**

在检索不安全的PDF文档并设置加密运行时值后，可向PDF文档添加密码。

**将加密的PDF文档另存为PDF文件**

您可以将密码加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服务API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF文档 {#encrypt-a-pdf-document-using-the-java-api}

使用加密API(Java)使用口令加密PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密客户端API。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取要加密的PDF文档。

   * 创建一 `java.io.FileInputStream` 个对象，它表示要加密的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置加密运行时选项。

   * 通过调 `PasswordEncryptionOptionSpec` 用对象的构造函数创建对象。
   * 通过调用对象的方法并传递指定要加密的文档 `PasswordEncryptionOptionSpec` 资源的文档 `setEncryptOption` 值，指定要加 `PasswordEncryptionOption` 密的PDF明细列表资源。 例如，要加密整个PDF文档，包括其元数据及其附件，请指定 `PasswordEncryptionOption.ALL`。
   * 使用构 `java.util.List` 造函数创建存储加密权限的对 `ArrayList` 象。
   * 通过调用对象“s `java.util.List` 方法”并传 `add` 递与要设置的权限对应的明细列表值来指定权限。 例如，要设置允许用户复制PDF文档中的数据的权限，请指定 `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （对于要设置的每个权限，重复此步骤）。
   * 通过调用对象的方法并传递指定Acrobat `PasswordEncryptionOptionSpec` 兼容性级 `setCompatability` 别的明细列表值，指定Acrobat兼容性选项。 For example, you can specify `PasswordEncryptionCompatability.ACRO_7`.
   * 指定密码值，允许用户通过调用对象的方法并传递表示打开密码的 `PasswordEncryptionOptionSpec` 字符串值 `setDocumentOpenPassword` 来打开加密的PDF文档。
   * 指定主口令值，该值允许用户通过调用对象的方法并传递表示主口令的字符串值 `PasswordEncryptionOptionSpec` , `setPermissionPassword` 从PDF文档中删除加密。

1. 添加密码。

   通过调用对象的方法并传 `EncryptionServiceClient` 递以下值 `encryptPDFUsingPassword` 来加密PDF文档:

   * 包 `com.adobe.idp.Document` 含要使用口令加密的PDF文档的对象。
   * 包含 `PasswordEncryptionOptionSpec` 加密运行时选项的对象。
   该方 `encryptPDFUsingPassword` 法返回一个 `com.adobe.idp.Document` 对象，该对象包含密码加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。 确保使用由 `com.adobe.idp.Document` 该方法返回的对 `encryptPDFUsingPassword` 象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API加密PDF文档 {#encrypting-a-pdf-document-using-the-web-service-api}

使用Encryption API（Web服务）使用口令加密PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Encryption Client API对象。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储使用密码加密的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。

1. 设置加密运行时选项。

   * 使用对 `PasswordEncryptionOptionSpec` 象的构造函数创建对象。
   * 通过为对象的数据成员分配文档值， `PasswordEncryptionOption` 指定要加密 `PasswordEncryptionOptionSpec` 的PDF明细列表 `encryptOption` 资源。 要加密整个PDF（包括其元数据及其附件），请将 `PasswordEncryptionOption.ALL` 其分配给该数据成员。
   * 通过为对象的数据成员分 `PasswordEncryptionCompatability` 配明细列表值来指 `PasswordEncryptionOptionSpec` 定Acrobat兼 `compatability` 容性选项。 例如，分配 `PasswordEncryptionCompatability.ACRO_7` 给此数据成员。
   * 指定密码值，允许用户通过为对象的数据成员分配表示打开密码的字符串值来打 `PasswordEncryptionOptionSpec` 开加密的PDF `documentOpenPassword` 文档。
   * 指定密码值，允许用户通过为对象的数据成员分配表示主密码的字符串值，从PDF文档中删 `PasswordEncryptionOptionSpec` 除加 `permissionPassword` 密。

1. 添加密码。

   通过调用对象的方法并传 `EncryptionServiceClient` 递以下值 `encryptPDFUsingPassword` 来加密PDF文档:

   * 包 `BLOB` 含要使用口令加密的PDF文档的对象。
   * 包含 `PasswordEncryptionOptionSpec` 加密运行时选项的对象。
   该方 `encryptPDFUsingPassword` 法返回一个 `BLOB` 对象，该对象包含密码加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示受保护PDF文档的文件位置的字符串值，创建一个对象。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `encryptPDFUsingPassword` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用证书加密PDF文档 {#encrypting-pdf-documents-with-certificates}

基于证书的加密允许您通过公钥技术为特定收件人加密文档。 可以为各种收件人授予不同的文档权限。 公钥技术使加密的许多方面成为可能。 算法用于生成两个大数字，即 *键*，它们具有以下属性：

* 一个密钥用于加密一组数据。 随后，只能使用其他密钥解密数据。
* 不可能把一个钥匙和另一个钥匙区分开来。

其中一个键用作用户的私钥。 只有用户才有权访问此密钥，这一点很重要。 另一个密钥是用户的公钥，可与他人共享。

公钥证书包含用户的公钥和标识信息。 X.509格式用于存储证书。 证书通常由证书颁发机构(CA)颁发和数字签名，该机构是提供对证书有效性的置信度的公认实体。 证书的到期日期已到期，之后证书不再有效。 此外，证书撤销列表(CRL)还提供在证书到期日前被吊销的证书的相关信息。 CRL由证书颁发机构定期发布。 还可以通过网络上的联机证书状态协议(OCSP)检索证书的撤销状态。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，则它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前，不要加密该订阅。 (请参阅 [编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。)

>[!NOTE]
>
>在使用证书加密PDF文档之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用Trust Manager API以编程方式添加的。 (请参 [阅使用Trust Manager API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要使用证书加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Encryption Client API对象。
1. 获取要加密的PDF文档。
1. 引用证书。
1. 设置加密运行时选项。
1. 创建证书加密的PDF文档。
1. 将加密的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建一个对 `EncrytionServiceClient` 象。 如果您使用Web服务Encryption Service API，请创建一个对 `EncryptionServiceService` 象。

**获取要加密的PDF文档**

您必须获得未加密的PDF文档才能加密。 如果尝试保护已加密的PDF文档，则会引发异常。

**引用证书**

要使用证书加密PDF文档，请引用用于加密PDF文档的证书。 证书是。cer文件、.crt文件或。pem文件。 PKCS#12文件用于存储具有相应证书的私钥。

使用证书加密PDF文档时，请指定与安全文档相关的权限。 通过指定权限，您可以控制打开证书加密的PDF文档的用户可以执行的操作。

**设置加密运行时选项**

指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据之外的所有内容，或仅加密文档的附件。

**创建证书加密的PDF文档**

在检索不安全的PDF文档、引用证书并设置运行时选项后，您可以创建一个证书加密的PDF文档。 在PDF文档加密后，您需要相应的公钥才能解密它。

**将加密的PDF文档另存为PDF文件**

您可以将加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服务API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用加密API(Java)使用证书加密PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建Encryption Client API对象。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取要加密的PDF文档。

   * 创建一 `java.io.FileInputStream` 个对象，它表示要加密的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 引用证书。

   * 创建一个 `java.util.List` 对象，该对象使用其构造函数存储权限信息。
   * 通过调用对象的方法并传递一个文档值，指 `java.util.List``add``CertificateEncryptionPermissions` 定与加密关联的权限，该明细列表值表示授予打开受保护PDF文档的用户的权限。 例如，要指定所有权限，请通过 `CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用对 `Recipient` 象的构造函数创建对象。
   * 创建一 `java.io.FileInputStream` 个对象，它表示使用PDF文档的构造函数并传递一个指定证书位置的字符串值来加密该证书。
   * 通过使用 `com.adobe.idp.Document` 其构造函数并传递表示证书的 `java.io.FileInputStream` 对象来创建对象。
   * 调用对 `Recipient` 象的方 `setX509Cert` 法并传递包 `com.adobe.idp.Document` 含证书的对象。 (此外，该对 `Recipient`象可以有Truststore证书别名或LDAP URL作为证书源。)
   * 使用 `CertificateEncryptionIdentity` 其构造函数创建存储权限和证书信息的对象。
   * 调用对 `CertificateEncryptionIdentity` 象的方 `setPerms` 法并传递存储 `java.util.List` 权限信息的对象。
   * 调用对 `CertificateEncryptionIdentity` 象的方 `setRecipient` 法并传递存储证 `Recipient` 书信息的对象。
   * 使用 `java.util.List` 其构造函数创建存储证书信息的对象。
   * 调用 `java.util.List` 对象的add方法并传递对 `CertificateEncryptionIdentity` 象。 (此对 `java.util.List` 象作为参数传递给该 `encryptPDFUsingCertificates` 方法。)

1. 设置加密运行时选项。

   * 通过调 `CertificateEncryptionOptionSpec` 用对象的构造函数创建对象。
   * 通过调用对象的方法并传递指定要加密的文档 `CertificateEncryptionOptionSpec` 资源的文档 `setOption` 值，指定要加 `CertificateEncryptionOption` 密的PDF明细列表资源。 例如，要加密整个PDF文档，包括其元数据及其附件，请指定 `CertificateEncryptionOption.ALL`。
   * 通过调用对象的方法并传递 `CertificateEncryptionOptionSpec` 指定Acrobat兼容 `setCompat` 性级别的 `CertificateEncryptionCompatibility` 明细列表值来指定Acrobat兼容性选项。 For example, you can specify `CertificateEncryptionCompatibility.ACRO_7`.

1. 创建证书加密的PDF文档。

   通过调用对象的方法并传递以下值， `EncryptionServiceClient` 使用证书 `encryptPDFUsingCertificates` 加密PDF文档:

   * 包 `com.adobe.idp.Document` 含要加密的PDF文档的对象。
   * 存储 `java.util.List` 证书信息的对象。
   * 包含 `CertificateEncryptionOptionSpec` 加密运行时选项的对象。
   该方 `encryptPDFUsingCertificates` 法返回一个 `com.adobe.idp.Document` 对象，该对象包含证书加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。 确保使用由 `com.adobe.idp.Document` 该方法返回的对 `encryptPDFUsingCertificates` 象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API使用证书加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用Encryption API（Web服务）使用证书加密PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Encryption Client API对象。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储使用证书加密的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 引用证书。

   * 使用对 `Recipient` 象的构造函数创建对象。 此对象将存储证书信息。
   * 使用对 `BLOB` 象的构造函数创建对象。 此对 `BLOB` 象将存储加密PDF文档的证书。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示证书的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。
   * 将存储 `BLOB` 证书的对象分配给该对象 `Recipient` 的数据成 `x509Cert` 员。
   * 使用 `CertificateEncryptionIdentity` 其构造函数创建存储证书信息的对象。
   * 将存储 `Recipient` 证书的对象指定给对 `CertificateEncryptionIdentity`象的收件人数据成员。
   * 创建数 `Object` 组，然后将对 `CertificateEncryptionIdentity` 象指定给该数组的第一个元 `Object` 素。 此 `Object` 数组作为参数传递给方 `encryptPDFUsingCertificates` 法。

1. 设置加密运行时选项。

   * 使用对 `CertificateEncryptionOptionSpec` 象的构造函数创建对象。
   * 通过为对象的数据成员分配文档值， `CertificateEncryptionOption` 指定要加密 `CertificateEncryptionOptionSpec` 的PDF明细列表 `option` 资源。 要加密整个PDF文档（包括其元数据及其附件），请为此数 `CertificateEncryptionOption.ALL` 据成员分配。
   * 通过为对象的数据成员分 `CertificateEncryptionCompatibility` 配明细列表值来指 `CertificateEncryptionOptionSpec` 定Acrobat兼 `compat` 容性选项。 例如，分配 `CertificateEncryptionCompatibility.ACRO_7` 给此数据成员。

1. 创建证书加密的PDF文档。

   通过调用对象的方法并传递以下值， `EncryptionServiceService` 使用证书 `encryptPDFUsingCertificates` 加密PDF文档:

   * 包 `BLOB` 含要加密的PDF文档的对象。
   * 存储 `Object` 证书信息的数组。
   * 包含 `CertificateEncryptionOptionSpec` 加密运行时选项的对象。
   该方 `encryptPDFUsingCertificates` 法返回一个 `BLOB` 对象，该对象包含证书加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个表示受保护PDF文档的文件位置的字符串值，创建一个对象。
   * 创建一个字节数组，它存储由方法返 `BLOB` 回的对象的数据内 `encryptPDFUsingCertificates` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除基于证书的加密 {#removing-certificate-based-encryption}

可以从PDF文档中删除基于证书的加密，以便用户可以在Adobe Reader或Acrobat中打开PDF文档。 要从使用证书加密的PDF文档中删除加密，必须引用公钥。 从PDF文档删除加密后，加密不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要从PDF文档中删除基于证书的加密，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除加密。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建一个对 `EncrytionServiceClient` 象。 如果您使用Web服务Encryption Service API，请创建一个对 `EncryptionServiceService` 象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能删除基于证书的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。 同样，如果尝试从密码加密的文档中删除基于证书的加密，则会引发异常。

**删除加密**

要从加密的PDF文档中删除基于证书的加密，您需要加密的PDF文档和与用于加密PDF文档的密钥相对应的私钥。 从加密的PDF文档删除基于证书的加密时，将指定私钥的别名值。 有关公钥的信息，请参阅使用证 [书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私钥存储在AEM Forms信任存储中。 将证书放在该位置时，将指定别名值。

**保存PDF文档**

从加密的PDF文档删除基于证书的加密后，您可以将PDF文档另存为PDF文件。 用户可以在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[使用Java API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服务API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-java-api}

使用Encryption API(Java)从PDF文档中删除基于证书的加密：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取加密的PDF文档。

   * 使用 `java.io.FileInputStream` 其构造函数并传递指定加密PDF文档位置的字符串值，创建表示加密PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 删除加密。

   通过调用对象的方法并传递以下值，从PDF文档 `EncryptionServiceClient` 中删除基 `removePDFCertificateSecurity` 于证书的加密：

   * 包 `com.adobe.idp.Document` 含加密的PDF文档的对象。
   * 一个字符串值，它指定私钥的别名，该别名与用于加密PDf文档的密钥相对应。
   该方 `removePDFCertificateSecurity` 法返回一个对 `com.adobe.idp.Document` 象，该对象包含不安全的PDF文档。

1. 保存PDF文档。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `Document` 制到文件。 确保使用由 `com.adobe.idp.Document` 该方法返回的对 `removePDFCredentialSecurity` 象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API删除基于证书的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用Encryption API（Web服务）删除基于证书的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储加密的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。

1. 删除加密。

   调用对 `EncryptionServiceClient` 象的方 `removePDFCertificateSecurity` 法并传递以下值：

   * 包含 `BLOB` 表示加密PDF文档的文件流数据的对象。
   * 一个字符串值，它指定与用于加密PDF文档的私钥对应的公钥的别名。
   该方 `removePDFCredentialSecurity` 法返回一个对 `BLOB` 象，该对象包含不安全的PDF文档。

1. 保存PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建一个对象，该字符串值表示不安全PDF文档的文件位置。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `removePDFPasswordSecurity` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除密码加密 {#removing-password-encryption}

可以从PDF文档中删除基于密码的加密，这样用户就可以在Adobe Reader或Acrobat中打开PDF文档，而无需指定密码。 从PDF文档删除基于密码的加密后，该文档将不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要从PDF文档中删除基于口令的加密，请执行以下步骤：

1. 包括项目文件
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除密码。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

将必要的文件包含到开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建一个对 `EncrytionServiceClient` 象。 如果您使用Web服务Encryption Service API，请创建一个对 `EncryptionServiceService` 象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能删除基于密码的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。

**删除密码**

要从加密的PDF文档中删除基于密码的加密，您需要加密的PDF文档和用于从PDF文档中删除加密的主密码值。 用于打开密码加密的PDF文档的密码不能用于删除加密。 当PDF文档使用密码加密时，将指定主密码。 (请参 [阅使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**保存PDF文档**

在“加密”服务从PDF文档中删除基于密码的加密后，您可以将PDF文档另存为PDF文件。 用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API删除基于口令的加密 {#remove-password-based-encryption-using-the-java-api}

使用Encryption API(Java)从PDF文档中删除基于密码的加密：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取加密的PDF文档。

   * 使用 `java.io.FileInputStream` 其构造函数并传递指定PDF文档位置的字符串值，创建表示加密的PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 删除密码。

   通过调用对象的方法并传递以下值，从PDF文档 `EncryptionServiceClient` 中删除基 `removePDFPasswordSecurity` 于口令的加密：

   * 包 `com.adobe.idp.Document` 含加密的PDF文档的对象。
   * 一个字符串值，它指定用于从PDF文档中删除加密的主密码值。
   该方 `removePDFPasswordSecurity` 法返回一个对 `com.adobe.idp.Document` 象，该对象包含不安全的PDF文档。

1. 保存PDF文档。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `Document` 制到文件。 确保使用由 `Document` 该方法返回的对 `removePDFPasswordSecurity` 象。

**另请参阅**

[快速开始（SOAP模式）:使用Java API删除基于口令的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服务API删除基于密码的加密 {#remove-password-based-encryption-using-the-web-service-api}

使用Encryption API（Web服务）删除基于密码的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储经过密码加密的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。

1. 删除密码。

   调用对 `EncryptionServiceService` 象的方 `removePDFPasswordSecurity` 法并传递以下值：

   * 包含 `BLOB` 表示加密PDF文档的文件流数据的对象。
   * 一个字符串值，它指定用于从PDF文档中删除加密的口令值。 使用口令加密PDF文档时指定此值。
   该方 `removePDFPasswordSecurity` 法返回一个对 `BLOB` 象，该对象包含不安全的PDF文档。

1. 保存PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建一个对象，该字符串值表示不安全PDF文档的文件位置。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `removePDFPasswordSecurity` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解锁加密的PDF文档 {#unlocking-encrypted-pdf-documents}

必须先解锁密码加密或证书加密的PDF文档，然后才能对其执行其他AEM Forms操作。 如果尝试对加密的PDF文档执行操作，将生成异常。 解锁加密的PDF文档后，可以对其执行一个或多个操作。 这些操作可以属于其他服务，如Acrobat Reader DC扩展服务。

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要解锁加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 解锁文档。
1. 执行AEM Forms操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建一个对 `EncrytionServiceClient` 象。 如果您使用Web服务Encryption Service API，请创建一个对 `EncryptionServiceService` 象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能将其解锁。 如果尝试解锁未加密的PDF文档，则会引发异常。

**解锁文档**

要解锁密码加密的PDF文档，您需要加密的PDF文档和用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。 (请参 [阅使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

要解锁证书加密的PDF文档，您需要加密的PDF文档以及与用于加密PDF文档的私钥相对应的公钥的别名值。

**执行AEM Forms操作**

解锁加密的PDF文档后，您可以对其执行其他服务操作，如对其应用使用权限。 此操作属于Acrobat Reader DC Extensions服务。

**另请参阅**

[使用Java API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服务API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用Encryption API(Java)解锁加密的PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取加密的PDF文档。

   * 使用 `java.io.FileInputStream` 其构造函数并传递指定加密PDF文档位置的字符串值，创建表示加密PDF文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 解锁文档。

   通过调用对象或方法解锁加 `EncryptionServiceClient` 密的PDF `unlockPDFUsingPassword` 文档 `unlockPDFUsingCredential` 。

   要解锁使用密码加密的PDF文档，请调用该方 `unlockPDFUsingPassword` 法并传递以下值：

   * 包 `com.adobe.idp.Document` 含密码加密的PDF文档的对象。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。
   要解锁使用证书加密的PDF文档，请调用该方 `unlockPDFUsingCredential` 法并传递以下值：

   * 包 `com.adobe.idp.Document` 含证书加密的PDF文档的对象。
   * 一个字符串值，它指定与用于加密PDF文档的私钥相对应的公钥的别名。
   该方 `unlockPDFUsingPassword` 法和 `unlockPDFUsingCredential` 方法都会返回一个对象，您将该对象传递给另 `com.adobe.idp.Document` 一个AEM Forms Java方法以执行操作。

1. 执行AEM Forms操作。

   在已解锁的PDF文档上执行AEM Forms操作，以满足您的业务要求。 例如，假定要将使用权限应用于已解锁的PDF文档，请将由或方法返回的对 `com.adobe.idp.Document` 象传递 `unlockPDFUsingPassword``unlockPDFUsingCredential` 给对 `ReaderExtensionsServiceClient` 象的方 `applyUsageRights` 法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) （SOAP模式）解锁加密的PDF文档

[将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用加密API（Web服务）解锁加密的PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。

1. 解锁文档。

   通过调用对象或方法解锁加 `EncryptionServiceClient` 密的PDF `unlockPDFUsingPassword` 文档 `unlockPDFUsingCredential` 。

   要解锁使用密码加密的PDF文档，请调用该方 `unlockPDFUsingPassword` 法并传递以下值：

   * 包 `BLOB` 含密码加密的PDF文档的对象。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。
   要解锁使用证书加密的PDF文档，请调用该方 `unlockPDFUsingCredential` 法并传递以下值：

   * 包 `BLOB` 含证书加密的PDF文档的对象。
   * 一个字符串值，它指定与用于加密PDF文档的私钥对应的公钥的别名。
   该方 `unlockPDFUsingPassword` 法和 `unlockPDFUsingCredential` 方法都会返回一个对象，您将该对象传递给 `com.adobe.idp.Document` 另一个AEM Forms方法以执行操作。

1. 执行AEM Forms操作。

   在已解锁的PDF文档上执行AEM Forms操作，以满足您的业务要求。 例如，假定要将使用权限应用于已解锁的PDF文档，请将由或方法返回的对 `BLOB` 象传递 `unlockPDFUsingPassword``unlockPDFUsingCredential` 给对 `ReaderExtensionsServiceClient` 象的方 `applyUsageRights` 法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 确定加密类型 {#determining-encryption-type}

您可以使用Java Encryption Service API或Web服务Encryption Service API以编程方式确定保护PDF文档的加密类型。 有时，需要动态确定PDF文档是否已加密，如果已加密，则还需要确定加密类型。 例如，您可以确定PDF文档是使用基于密码的加密还是使用Rights Management策略进行保护。

PDF文档可以受以下加密类型的保护：

* 基于密码的加密
* 基于证书的加密
* 由Rights Management服务创建的策略
* 另一种加密

>[!NOTE]
>
>有关加密服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要确定保护PDF文档的加密类型，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 确定加密类型。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar（在JBoss Application Server上部署AEM Forms时为必需）
* jbossall-client.jar（在JBoss Application Server上部署AEM表单时需要）

**创建服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建一个对 `EncrytionServiceClient` 象。 如果您使用Web服务Encryption Service API，请创建一个对 `EncryptionServiceService` 象。

**获取加密的PDF文档**

您必须获得PDF文档，以确定保护它的加密类型。

**确定加密类型**

您可以确定保护PDF文档的加密类型。 如果PDF文档未受保护，则加密服务会通知您PDF文档未受到保护。

**另请参阅**

[使用Java API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服务API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Encryption Service API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保护文档](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API确定加密类型 {#determine-the-encryption-type-using-the-java-api}

使用加密API(Java)确定保护PDF文档的加密类型：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建服务客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `EncryptionServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取加密的PDF文档。

   * 使用 `java.io.FileInputStream` PDF文档的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示PDF的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 确定加密类型。

   * 通过调用对象的方法并 `EncryptionServiceClient` 传递包含PDF `getPDFEncryption` 文档的 `com.adobe.idp.Document` 对象，确定加密类型。 此方法返回一个 `EncryptionTypeResult` 对象。
   * 调用 `EncryptionTypeResult` 对象的方 `getEncryptionType` 法。 此方法返回 `EncryptionType` 指定加密类型的enum值。 例如，如果PDF文档使用基于密码的加密进行保护，则此方法将返回 `EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API确定加密类型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API确定加密类型 {#determine-the-encryption-type-using-the-web-service-api}

使用Encryption API（Web服务）确定保护PDF文档的加密类型：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建服务客户端。

   * 使用对 `EncryptionServiceClient` 象的默认构造函数创建对象。
   * 使用构 `EncryptionServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/EncryptionService?WSDL`.)您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `EncryptionServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 将字 `BLOB` 节数组的内容分配给对象的数据成 `BLOB` 员，以填充 `MTOM` 对象。

1. 确定加密类型。

   * 调用对 `EncryptionServiceClient` 象的方 `getPDFEncryption` 法并传递包 `BLOB` 含PDF文档的对象。 此方法返回一个 `EncryptionTypeResult` 对象。
   * 获取对象的数 `EncryptionTypeResult` 据方法 `encryptionType` 的值。 例如，如果PDF文档使用基于密码的加密进行保护，则此数据成员的值为 `EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)