---
title: 使用凭据
seo-title: 使用凭据
description: 'null'
seo-description: 'null'
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用凭据 {#working-with-credentials}

**关于凭证服务**

凭据包含签名或识别文档所需的私钥信息。 证书是您为信任配置的公钥信息。 AEM Forms使用证书和凭据用于多种用途：

* Acrobat Reader DC扩展使用凭据在PDF文档中启用Adobe Reader使用权限。 (请参 [阅将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。)
* 签名服务在执行对PDF文档进行数字签名等操作时访问证书和凭据。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

您可以使用Trust Manager Java API与凭证服务进行有序交互。 您可以执行以下任务：

* [使用Trust Manager API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您还可以使用管理控制台导入和删除证书。 (请参阅 [管理帮助。](https://www.adobe.com/go/learn_aemforms_admin_63))

## 使用Trust Manager API导入凭据 {#importing-credentials-by-using-the-trust-manager-api}

您可以使用Trust Manager API以编程方式将凭据导入AEM Forms。 例如，您可以导入用于对PDF文档进行签名的凭证。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

在导入凭据时，需要为凭据指定别名。 别名用于执行需要凭据的表单操作。 导入后，可以在管理控制台中查看凭据，如下图所示。 请注意，凭据的别名是安 *全的*。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>不能使用Web服务将凭据导入AEM Forms。

### 步骤摘要 {#summary-of-steps}

要将凭据导入AEM Forms，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 引用凭据。
1. 执行导入操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时为必需）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建凭据服务客户端**

在以编程方式将凭据导入AEM Forms之前，请先创建凭据服务客户端。 有关信息，请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用凭据**

引用要导入AEM Forms的凭证。 与此部分关联的快速入门引用位于文件系统中的P12文件。

**执行导入操作**

在引用凭证后，将凭证导入AEM Forms。 如果未成功导入凭据，则会引发异常。 在导入凭据时，需要为凭据指定别名。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[凭据服务API快速入门](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API导入凭据 {#import-credentials-using-the-java-api}

使用Trust Manager API(Java)将凭据导入AEM Forms:

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `CredentialServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 引用凭据

   * 使用对 `java.io.FileInputStream` 象的构造函数创建对象。 传递一个指定凭证位置的字符串值。
   * 使用构 `com.adobe.idp.Document` 造函数创建存储凭据的对 `com.adobe.idp.Document` 象。 将包含 `java.io.FileInputStream` 凭据的对象传递给构造函数。

1. 执行导入操作

   * 创建一个包含一个元素的字符串数组。 为元素 `truststore.usage.type.sign` 赋值。
   * 调用对 `CredentialServiceClient` 象的方 `importCredential` 法并传递以下值：

      * 一个字符串值，它指定凭据的别名值。
      * 存 `com.adobe.idp.Document` 储凭据的实例。
      * 一个字符串值，它指定与凭证关联的口令。
      * 包含使用值的字符串数组。 例如，您可以指定此值 `truststore.usage.type.sign`。 要导入Reader扩展凭据，请指定 `truststore.usage.type.lcre`。

**另请参阅**

[使用Trust Manager API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速入门（SOAP模式）:使用Java API导入凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Trust Manager API删除凭据 {#deleting-credentials-by-using-the-trust-manager-api}

您可以使用Trust Manager API以编程方式删除凭据。 在删除凭据时，您需要指定与凭据对应的别名。 删除后，凭据便无法用于执行操作。

>[!NOTE]
>
>不能使用Web服务将凭据删除到AEM Forms中。

### 步骤摘要 {#summary_of_steps-1}

要删除凭据，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 执行删除操作。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时为必需）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建凭据服务客户端**

在以编程方式删除凭据之前，请先创建Data Integration服务客户端。 创建服务客户端时，您定义调用服务所需的连接设置。 有关信息，请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**执行删除操作**

要删除凭据，请指定与凭据对应的别名。 如果指定的别名不存在，则会引发异常。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

### 使用Java API删除凭据 {#deleting-credentials-using-the-java-api}

使用Trust Manager API(Java)从AEM Forms中删除凭据：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `CredentialServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 执行删除操作

   调用对 `CredentialServiceClient` 象的方 `deleteCredential` 法并传递指定别名值的字符串值。

**另请参阅**

[使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速入门（SOAP模式）:使用Java API删除凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
