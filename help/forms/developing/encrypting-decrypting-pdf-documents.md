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
workflow-type: tm+mt
source-wordcount: '8118'
ht-degree: 0%

---


# 加密和解密PDF文档{#encrypting-and-decrypting-pdf-documents}

**关于加密服务**

加密服务允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问。 如果PDF文档是使用口令加密的，则用户必须指定打开口令，才能在Adobe Reader或Adobe Acrobat查看文档。 同样，如果PDF文档用证书加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥对PDF文档进行解密。

您可以使用加密服务完成以下任务:

* 使用口令加密PDF文档。 (请参阅[使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用证书加密PDF文档。 (请参阅[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 从PDF文档中删除基于密码的加密。 （请参阅[删除密码加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）
* 从PDF文档中删除基于证书的加密。 （请参阅[删除基于证书的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）
* 解锁PDF文档，以便执行其他服务操作。 例如，在解锁密码加密的PDF文档后，您可以对其应用数字签名。 (请参阅[解锁已加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 确定安全PDF文档的加密类型。 （请参阅[确定加密类型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密码{#encrypting-pdf-documents-with-a-password}加密PDF文档

当您使用口令加密PDF文档时，用户必须指定口令才能在Adobe Reader或Acrobat打开PDF文档。 此外，在对AEM Forms执行另一项文档操作(如对PDF文档进行数字签名)之前，必须解锁密码加密的PDF文档。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前不要对其进行加密。 （请参阅[编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要使用口令加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建Encryption Client API对象。
1. 获取要加密的PDF文档。
1. 设置加密运行时选项。
1. 添加密码。
1. 将加密的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，则为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必需)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。

**获取要加密的PDF文档**

您必须获取未加密的PDF文档才能使用密码加密文档。 如果尝试保护已加密的PDF文档，将引起异常。

**设置加密运行时选项**

要使用口令加密PDF文档，您指定四个值，包括两个口令值。 第一个口令值用于加密PDF文档，在打开PDF文档时必须指定。 第二个密码值(名为主控密码值)用于从PDF文档中删除加密。 密码值区分大小写，这两个密码值不能相同。

必须指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据外的所有内容，或仅加密文档的附件。 如果仅加密文档的附件，则当用户尝试访问文件附件时，系统会提示用户输入口令。

在加密PDF文档时，您可以指定与安全文档关联的权限。 通过指定权限，您可以控制打开密码加密的PDF文档的用户可以执行的操作。 例如，要成功提取表单数据，您必须设置以下权限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>权限指定为`PasswordEncryptionPermission`明细列表值。

**添加密码**

在检索不安全的PDF文档并设置加密运行时值后，可以向PDF文档添加口令。

**将加密的PDF文档另存为PDF文件**

您可以将密码加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服务API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API {#encrypt-a-pdf-document-using-the-java-api}加密PDF文档

使用Encryption API(Java)使用口令加密PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密客户端API。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取要加密的PDF文档。

   * 创建一个`java.io.FileInputStream`对象，它表示要加密的PDF文档，方法是使用它的构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 设置加密运行时选项。

   * 通过调用其构造函数创建`PasswordEncryptionOptionSpec`对象。
   * 通过调用`PasswordEncryptionOptionSpec`对象的`setEncryptOption`方法并传递指定要加密的文档资源的`PasswordEncryptionOption`明细列表值，指定要加密的文档资源。 例如，要加密整个PDF文档，包括其元数据及其附件，请指定`PasswordEncryptionOption.ALL`。
   * 使用`ArrayList`构造函数创建存储加密权限的`java.util.List`对象。
   * 通过调用`java.util.List`对象“s `add`”方法并传递与要设置的权限对应的明细列表值来指定权限。 例如，要设置允许用户复制PDF文档中数据的权限，请指定`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （对要设置的每个权限重复此步骤）。
   * 通过调用`PasswordEncryptionOptionSpec`对象的`setCompatability`方法并传递指定Acrobat兼容性级别的明细列表值，指定Acrobat兼容性选项。 例如，可以指定`PasswordEncryptionCompatability.ACRO_7`。
   * 指定允许用户通过调用`PasswordEncryptionOptionSpec`对象的`setDocumentOpenPassword`方法并传递表示打开口令的字符串值来打开已加密的PDF文档的口令值。
   * 指定主控密码值，允许用户通过调用`PasswordEncryptionOptionSpec`对象的`setPermissionPassword`方法并传递表示主控密码的字符串值，从PDF文档中删除加密。

1. 添加密码。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingPassword`方法并传递以下值，加密PDF文档:

   * `com.adobe.idp.Document`对象，它包含要使用口令加密的PDF文档。
   * 包含加密运行时选项的`PasswordEncryptionOptionSpec`对象。

   `encryptPDFUsingPassword`方法返回一个`com.adobe.idp.Document`对象，该对象包含口令加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。 确保使用由`encryptPDFUsingPassword`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#encrypting-a-pdf-document-using-the-web-service-api}加密PDF文档

使用Encryption API（Web服务）使用口令加密PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Encryption Client API对象。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储使用密码加密的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。

1. 设置加密运行时选项。

   * 使用`PasswordEncryptionOptionSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过为`PasswordEncryptionOptionSpec`对象的`encryptOption`文档成员分配`PasswordEncryptionOption`明细列表值，指定要加密的PDF资源。 要加密整个PDF，包括其元数据及其附件，请将`PasswordEncryptionOption.ALL`分配给此数据成员。
   * 通过为`PasswordEncryptionOptionSpec`对象的`compatability`数据成员分配`PasswordEncryptionCompatability`明细列表值，指定Acrobat兼容性选项。 例如，将`PasswordEncryptionCompatability.ACRO_7`分配给此数据成员。
   * 指定允许用户通过为`PasswordEncryptionOptionSpec`对象的`documentOpenPassword`数据成员指定表示打开口令的字符串值来打开加密的PDF文档的口令值。
   * 指定密码值，允许用户通过为`PasswordEncryptionOptionSpec`对象的`permissionPassword`文档成员指定表示主控密码的字符串值，从PDF中删除加密。

1. 添加密码。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingPassword`方法并传递以下值，加密PDF文档:

   * `BLOB`对象，它包含要使用口令加密的PDF文档。
   * 包含加密运行时选项的`PasswordEncryptionOptionSpec`对象。

   `encryptPDFUsingPassword`方法返回一个`BLOB`对象，该对象包含口令加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示受保护PDF文档的文件位置。
   * 创建一个字节数组，用于存储`encryptPDFUsingPassword`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用证书{#encrypting-pdf-documents-with-certificates}加密PDF文档

基于证书的加密允许您通过公钥技术为特定收件人加密文档。 可以为各种收件人授予不同的文档权限。 公钥技术使加密的许多方面成为可能。 算法用于生成两个大数字，称为&#x200B;*keys*，它们具有以下属性：

* 一个密钥用于加密一组数据。 随后，只能使用其他密钥解密数据。
* 一把钥匙和另一把钥匙分不开。

其中一个密钥充当用户的私钥。 只有用户才有权访问此密钥，这一点很重要。 另一个密钥是用户的公钥，可与他人共享。

公钥证书包含用户的公钥和标识信息。 X.509格式用于存储证书。 证书通常由证书颁发机构(CA)颁发和数字签名，该机构是提供对证书有效性的信任度的公认实体。 证书的到期日期已过期，在此日期后，证书不再有效。 此外，证书吊销列表(CRL)还提供有关在其过期日期之前已吊销的证书的信息。 CRL由证书颁发机构定期发布。 证书的吊销状态也可以通过网络通过联机证书状态协议(OCSP)进行检索。

>[!NOTE]
>
>如果将加密的PDF文档上传到AEM Forms存储库，它将无法解密PDF文档并提取XDP内容。 建议在将文档上传到AEM Forms存储库之前不要对其进行加密。 （请参阅[编写资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>在使用证书加密PDF文档之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用Trust Manager API以编程方式添加的。 （请参阅[使用Trust Manager API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)导入凭据。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-1}的摘要

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

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建`EncrytionServiceClient`对象。 如果您使用Web服务Encryption Service API，请创建`EncryptionServiceService`对象。

**获取要加密的PDF文档**

您必须获得未加密的PDF文档才能加密。 如果尝试保护已加密的PDF文档，将引发异常。

**引用证书**

要使用证书加密PDF文档，请引用用于加密PDF文档的证书。 证书是。cer文件、.crt文件或。pem文件。 PKCS#12文件用于存储具有相应证书的私钥。

使用证书加密PDF文档时，指定与安全文档关联的权限。 通过指定权限，您可以控制打开证书加密PDF文档的用户可以执行的操作。

**设置加密运行时选项**

指定要加密的PDF文档资源。 您可以加密整个PDF文档、除文档元数据以外的所有内容，或仅加密文档的附件。

**创建证书加密的PDF文档**

在检索不安全的PDF文档、引用证书并设置运行时选项后，您可以创建证书加密的PDF文档。 PDF文档加密后，您需要相应的公钥才能解密它。

**将加密的PDF文档另存为PDF文件**

您可以将加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服务API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}使用证书加密PDF文档

使用Encryption API(Java)使用证书加密PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建Encryption Client API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取要加密的PDF文档。

   * 创建一个`java.io.FileInputStream`对象，它表示要加密的PDF文档，方法是使用它的构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 引用证书。

   * 创建一个`java.util.List`对象，它使用其构造函数存储权限信息。
   * 通过调用`java.util.List`对象的`add`方法并传递一个`CertificateEncryptionPermissions`文档值，指定与加密的明细列表关联的权限，该值表示向打开受保护的PDF文档的用户授予的权限。 例如，要指定所有权限，请传递`CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用`Recipient`对象的构造函数创建&lt;a0/>对象。
   * 创建一个`java.io.FileInputStream`对象，它表示用于加密PDF文档的证书，方法是使用它的构造函数并传递一个指定证书位置的字符串值。
   * 使用`com.adobe.idp.Document`对象的构造函数创建`java.io.FileInputStream`对象，并传递表示证书的&lt;a1/>对象。
   * 调用`Recipient`对象的`setX509Cert`方法并传递包含证书的`com.adobe.idp.Document`对象。 （此外，`Recipient`对象可以具有Truststore证书别名或LDAP URL作为证书源。）
   * 使用`CertificateEncryptionIdentity`对象的构造函数创建一个用于存储权限和证书信息的对象。
   * 调用`CertificateEncryptionIdentity`对象的`setPerms`方法并传递存储权限信息的`java.util.List`对象。
   * 调用`CertificateEncryptionIdentity`对象的`setRecipient`方法并传递存储证书信息的`Recipient`对象。
   * 创建一个`java.util.List`对象，它使用其构造函数存储证书信息。
   * 调用`java.util.List`对象的add方法并传递`CertificateEncryptionIdentity`对象。 （此`java.util.List`对象作为参数传递给`encryptPDFUsingCertificates`方法。）

1. 设置加密运行时选项。

   * 通过调用其构造函数创建`CertificateEncryptionOptionSpec`对象。
   * 通过调用`CertificateEncryptionOptionSpec`对象的`setOption`方法并传递指定要加密的文档资源的`CertificateEncryptionOption`明细列表值，指定要加密的文档资源。 例如，要加密整个PDF文档，包括其元数据及其附件，请指定`CertificateEncryptionOption.ALL`。
   * 通过调用`CertificateEncryptionOptionSpec`对象的`setCompat`方法并传递指定Acrobat兼容性级别的`CertificateEncryptionCompatibility`明细列表值，指定Acrobat兼容性选项。 例如，可以指定`CertificateEncryptionCompatibility.ACRO_7`。

1. 创建证书加密的PDF文档。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingCertificates`方法并传递以下值，使用证书加密PDF文档:

   * 包含要加密的PDF文档的`com.adobe.idp.Document`对象。
   * 存储证书信息的`java.util.List`对象。
   * 包含加密运行时选项的`CertificateEncryptionOptionSpec`对象。

   `encryptPDFUsingCertificates`方法返回一个`com.adobe.idp.Document`对象，该对象包含证书加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。 确保使用由`encryptPDFUsingCertificates`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API使用证书加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}使用证书加密PDF文档

使用Encryption API（Web服务）使用证书加密PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Encryption Client API对象。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储使用证书加密的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的&lt;a1/>属性指定字节数组的内容，填充`BLOB`对象。

1. 引用证书。

   * 使用`Recipient`对象的构造函数创建&lt;a0/>对象。 此对象将存储证书信息。
   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 此`BLOB`对象将存储加密PDF文档的证书。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示证书的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。
   * 将存储证书的`BLOB`对象分配给`Recipient`对象的`x509Cert`数据成员。
   * 创建一个`CertificateEncryptionIdentity`对象，它使用其构造函数存储证书信息。
   * 将存储证书的`Recipient`对象分配给`CertificateEncryptionIdentity`对象的收件人数据成员。
   * 创建`Object`数组，将`CertificateEncryptionIdentity`对象分配给`Object`数组的第一个元素。 此`Object`数组作为参数传递给`encryptPDFUsingCertificates`方法。

1. 设置加密运行时选项。

   * 使用`CertificateEncryptionOptionSpec`对象的构造函数创建&lt;a0/>对象。
   * 通过为`CertificateEncryptionOptionSpec`对象的`option`文档成员分配`CertificateEncryptionOption`明细列表值，指定要加密的PDF资源。 要加密整个PDF文档，包括其元数据及其附件，请为此数据成员分配`CertificateEncryptionOption.ALL`。
   * 通过为`CertificateEncryptionOptionSpec`对象的`compat`数据成员分配`CertificateEncryptionCompatibility`明细列表值，指定Acrobat兼容性选项。 例如，将`CertificateEncryptionCompatibility.ACRO_7`分配给此数据成员。

1. 创建证书加密的PDF文档。

   通过调用`EncryptionServiceService`对象的`encryptPDFUsingCertificates`方法并传递以下值，使用证书加密PDF文档:

   * 包含要加密的PDF文档的`BLOB`对象。
   * 存储证书信息的`Object`阵列。
   * 包含加密运行时选项的`CertificateEncryptionOptionSpec`对象。

   `encryptPDFUsingCertificates`方法返回一个`BLOB`对象，该对象包含证书加密的PDF文档。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示受保护PDF文档的文件位置。
   * 创建一个字节数组，用于存储`encryptPDFUsingCertificates`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`binaryData`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除基于证书的加密{#removing-certificate-based-encryption}

可以从PDF文档中删除基于证书的加密，以便用户可以在Adobe Reader或Acrobat打开PDF文档。 要从使用证书加密的PDF文档中删除加密，必须引用公钥。 从PDF文档删除加密后，它不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要从PDF文档中删除基于证书的加密，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除加密。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建`EncrytionServiceClient`对象。 如果您使用Web服务Encryption Service API，请创建`EncryptionServiceService`对象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能删除基于证书的加密。 如果尝试从未加密的PDF文档中删除加密，将引发异常。 同样，如果尝试从密码加密文档删除基于证书的加密，则会引发异常。

**删除加密**

要从加密的PDF文档中删除基于证书的加密，您需要加密的PDF文档和与用于加密PDF文档的密钥相对应的私钥。 从加密的PDF文档删除基于证书的加密时，将指定私钥的别名值。 有关公钥的信息，请参阅[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私钥存储在AEM Forms信任商店。 将证书放在该位置时，将指定别名值。

**保存PDF文档**

从加密的PDF文档中删除基于证书的加密后，您可以将PDF文档另存为PDF文件。 用户可以在Adobe Reader或Acrobat打开PDF文档。

**另请参阅**

[使用Java API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服务API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#remove-certificate-based-encryption-using-the-java-api}删除基于证书的加密

使用Encryption API(Java)从PDF文档中删除基于证书的加密：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定加密PDF文档位置的字符串值，创建一个表示加密PDF文档的&lt;a0/>对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 删除加密。

   通过调用`EncryptionServiceClient`对象的`removePDFCertificateSecurity`方法并传递以下值，从PDF文档中删除基于证书的加密：

   * `com.adobe.idp.Document`对象，它包含加密的PDF文档。
   * 一个字符串值，它指定与用于加密PDf文档的密钥对应的私钥的别名。

   `removePDFCertificateSecurity`方法返回一个`com.adobe.idp.Document`对象，该对象包含一个不安全的PDF文档。

1. 保存PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件。 确保使用由`removePDFCredentialSecurity`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API删除基于证书的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#remove-certificate-based-encryption-using-the-web-service-api}删除基于证书的加密

使用Encryption API（Web服务）删除基于证书的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储加密的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。

1. 删除加密。

   调用`EncryptionServiceClient`对象的`removePDFCertificateSecurity`方法并传递以下值：

   * `BLOB`对象，它包含表示加密PDF文档的文件流数据。
   * 一个字符串值，它指定与用于加密PDf文档的私钥对应的公钥的别名。

   `removePDFCredentialSecurity`方法返回一个`BLOB`对象，该对象包含一个不安全的PDF文档。

1. 保存PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示不安全的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`removePDFPasswordSecurity`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除密码加密{#removing-password-encryption}

可以从PDF文档中删除基于密码的加密，这样用户无需指定密码即可在Adobe Reader或Acrobat打开PDF文档。 从PDF文档删除基于密码的加密后，文档不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-3}的摘要

要从PDF文档中删除基于密码的加密，请执行以下步骤：

1. 包括项目文件
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除密码。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss上，则为必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必需)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建`EncrytionServiceClient`对象。 如果您使用Web服务Encryption Service API，请创建`EncryptionServiceService`对象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能删除基于密码的加密。 如果尝试从未加密的PDF文档中删除加密，将引发异常。

**删除密码**

要从加密的PDF文档中删除基于密码的加密，您需要加密的PDF文档和用于从PDF文档中删除加密的主控密码值。 用于打开密码加密的PDF文档的密码不能用于删除加密。 当用密码加密PDF文档时，将指定主控密码。 (请参阅[使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**保存PDF文档**

在Encryption服务从PDF文档删除基于密码的加密后，您可以将PDF文档另存为PDF文件。 用户无需指定口令即可在Adobe Reader或Acrobat打开PDF文档。

**另请参阅**

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API {#remove-password-based-encryption-using-the-java-api}删除基于口令的加密

使用Encryption API(Java)从PDF文档中删除基于密码的加密：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示已加密PDF文档的&lt;a0/>对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 删除密码。

   通过调用`EncryptionServiceClient`对象的`removePDFPasswordSecurity`方法并传递以下值，从PDF文档中删除基于口令的加密：

   * 一个`com.adobe.idp.Document`对象，它包含加密的PDF文档。
   * 一个字符串值，它指定用于从PDF文档中删除加密的主控密码值。

   `removePDFPasswordSecurity`方法返回一个`com.adobe.idp.Document`对象，该对象包含一个不安全的PDF文档。

1. 保存PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为。pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件。 确保使用由`removePDFPasswordSecurity`方法返回的`Document`对象。

**另请参阅**

[快速开始（SOAP模式）:使用Java API删除基于密码的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服务API {#remove-password-based-encryption-using-the-web-service-api}删除基于口令的加密

使用Encryption API（Web服务）删除基于密码的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。 `BLOB`对象用于存储经过密码加密的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。

1. 删除密码。

   调用`EncryptionServiceService`对象的`removePDFPasswordSecurity`方法并传递以下值：

   * `BLOB`对象，它包含表示加密PDF文档的文件流数据。
   * 一个字符串值，它指定用于从PDF文档中删除加密的口令值。 使用口令加密PDF文档时指定此值。

   `removePDFPasswordSecurity`方法返回一个`BLOB`对象，该对象包含一个不安全的PDF文档。

1. 保存PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示不安全的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`removePDFPasswordSecurity`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值，填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象，创建&lt;a0/>对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解锁加密的PDF文档{#unlocking-encrypted-pdf-documents}

必须先解锁密码加密或证书加密的PDF文档，然后才能对其执行其他AEM Forms操作。 如果尝试对加密的PDF文档执行操作，将生成异常。 解锁加密的PDF文档后，可以对其执行一个或多个操作。 这些业务可以属于其他服务，如Acrobat Reader DC扩展服务。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-4}的摘要

要解锁加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 解锁文档。
1. 执行AEM Forms操作。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建`EncrytionServiceClient`对象。 如果您使用Web服务Encryption Service API，请创建`EncryptionServiceService`对象。

**获取加密的PDF文档**

您必须获得加密的PDF文档才能将其解锁。 如果尝试解锁未加密的PDF文档，将引发异常。

**解锁文档**

要解锁密码加密的PDF文档，您需要加密的PDF文档和用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。 (请参阅[使用口令加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

要解锁证书加密的PDF文档，您需要加密的PDF文档以及与用于加密PDF文档的私钥对应的公钥的别名值。

**执行AEM Forms操作**

解锁加密的PDF文档后，您可以对其执行其他服务操作，如对其应用使用权限。 此操作属于Acrobat Reader DC扩展服务。

**另请参阅**

[使用Java API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服务API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API {#unlock-an-encrypted-pdf-document-using-the-java-api}解锁加密的PDF文档

使用Encryption API(Java)解锁加密的PDF文档:

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数并传递一个指定加密PDF文档位置的字符串值，创建一个表示加密PDF文档的&lt;a0/>对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 解锁文档。

   通过调用`EncryptionServiceClient`对象的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法解锁已加密的PDF文档。

   要解锁使用密码加密的PDF文档，请调用`unlockPDFUsingPassword`方法并传递以下值：

   * `com.adobe.idp.Document`对象，它包含密码加密的PDF文档。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用`unlockPDFUsingCredential`方法并传递以下值：

   * `com.adobe.idp.Document`对象，它包含证书加密的PDF文档。
   * 一个字符串值，它指定与用于加密PDF文档的私钥对应的公钥的别名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都返回一个`com.adobe.idp.Document`对象，您将该对象传递给另一个AEM FormsJava方法以执行操作。

1. 执行AEM Forms操作。

   在已解锁的PDF文档上执行AEM Forms操作，以满足您的业务要求。 例如，假定要对已解锁的PDF文档应用使用权限，请将`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`com.adobe.idp.Document`对象传递给`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API（SOAP模式）解锁加密的](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) PDF文档。

[将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#unlock-an-encrypted-pdf-document-using-the-web-service-api}解锁加密的PDF文档

使用Encryption API（Web服务）解锁加密的PDF文档:

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。

1. 解锁文档。

   通过调用`EncryptionServiceClient`对象的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法解锁已加密的PDF文档。

   要解锁使用密码加密的PDF文档，请调用`unlockPDFUsingPassword`方法并传递以下值：

   * `BLOB`对象，它包含密码加密的PDF文档。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用口令加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用`unlockPDFUsingCredential`方法并传递以下值：

   * `BLOB`对象，它包含证书加密的PDF文档。
   * 一个字符串值，它指定与用于加密PDf文档的私钥对应的公钥的别名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都返回一个`com.adobe.idp.Document`对象，您将该对象传递给另一个AEM Forms方法以执行操作。

1. 执行AEM Forms操作。

   在已解锁的PDF文档上执行AEM Forms操作，以满足您的业务要求。 例如，假定要对已解锁的PDF文档应用使用权限，请将`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`BLOB`对象传递给`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 确定加密类型{#determining-encryption-type}

您可以使用Java Encryption Service API或Web服务Encryption Service API以编程方式确定保护PDF文档的加密类型。 有时，需要动态确定PDF文档是否已加密，如果是，则需要动态确定加密类型。 例如，您可以确定PDF文档是使用基于口令的加密还是Rights Management策略进行保护。

PDF文档可以受以下加密类型的保护：

* 基于密码的加密
* 基于证书的加密
* 由Rights Management服务创建的策略
* 另一种加密

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-5}的摘要

要确定保护PDF文档的加密类型，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 确定加密类型。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

**创建服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用Java Encryption Service API，请创建`EncrytionServiceClient`对象。 如果您使用Web服务Encryption Service API，请创建`EncryptionServiceService`对象。

**获取加密的PDF文档**

您必须获得PDF文档，以确定保护该文件的加密类型。

**确定加密类型**

您可以确定保护PDF文档的加密类型。 如果PDF文档没有保护，则加密服务会通知您PDF文档没有保护。

**另请参阅**

[使用Java API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服务API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速开始](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保护文档](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API {#determine-the-encryption-type-using-the-java-api}确定加密类型

使用Encryption API(Java)确定保护PDF文档的加密类型：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-encryption-client.jar。

1. 创建服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EncryptionServiceClient`对象的构造函数创建`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用PDF文档的构造函数并传递一个指定PDF文档位置的字符串值，创建一个表示PDF的`java.io.FileInputStream`对象。
   * 使用`com.adobe.idp.Document`对象的构造函数并传递`java.io.FileInputStream`对象，创建&lt;a0/>对象。

1. 确定加密类型。

   * 通过调用`EncryptionServiceClient`对象的`getPDFEncryption`方法并传递包含PDF文档的`com.adobe.idp.Document`对象，确定加密类型。 此方法返回一个`EncryptionTypeResult`对象。
   * 调用`EncryptionTypeResult`对象的`getEncryptionType`方法。 此方法返回指定加密类型的`EncryptionType`枚举值。 例如，如果PDF文档受基于密码的加密保护，则此方法返回`EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速开始（SOAP模式）:使用Java API确定加密类型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#determine-the-encryption-type-using-the-web-service-api}确定加密类型

使用Encryption API（Web服务）确定保护PDF文档的加密类型：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建服务客户端。

   * 使用其默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在您创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`指定AEM表单用户名。
      * 为字段`EncryptionServiceClient.ClientCredentials.UserName.Password`分配相应的口令值。
      * 将常量值`HttpClientCredentialType.Basic`指定到字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`指定到字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用`BLOB`对象的构造函数创建&lt;a0/>对象。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建存储`System.IO.FileStream`对象内容的字节数组。 通过获取`System.IO.FileStream`对象的`Length`属性，可以确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员，填充`BLOB`对象。

1. 确定加密类型。

   * 调用`EncryptionServiceClient`对象的`getPDFEncryption`方法并传递包含PDF文档的`BLOB`对象。 此方法返回一个`EncryptionTypeResult`对象。
   * 获取`EncryptionTypeResult`对象的`encryptionType`数据方法的值。 例如，如果PDF文档使用基于密码的加密进行保护，则此数据成员的值为`EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)