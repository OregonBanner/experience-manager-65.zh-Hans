---
title: 使用凭据
seo-title: Working with Credentials
description: 使用信任管理器API和Java API将凭据导入AEM Forms。 此外，了解如何使用信任管理器API和Java API删除凭据。
seo-description: Import credentials into AEM Forms using the Trust Manager API and Java API. In addition, learn how to delete credentials using the Trust Manager API and Java API.
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
role: Developer
exl-id: 1101c85a-6a90-471d-a7be-8d25765e84bf
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# 使用凭据 {#working-with-credentials}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

**关于凭据服务**

凭据包含签名或识别文档所需的私钥信息。 证书是您为信任配置的公钥信息。 AEM Forms将证书和凭据用于多种用途：

* Acrobat Reader DC扩展使用凭据在PDF文档中启用Adobe Reader使用权限。 (请参阅 [将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).)
* 签名服务在执行操作(如对PDF文档进行数字签名)时访问证书和凭据。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

您可以使用信任管理器Java API以编程方式与Credential服务交互。 您可以执行以下任务：

* [使用信任管理器API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用信任管理器API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您还可以使用管理控制台导入和删除证书。 (请参阅 [管理帮助。](https://www.adobe.com/go/learn_aemforms_admin_63))

## 使用信任管理器API导入凭据 {#importing-credentials-by-using-the-trust-manager-api}

您可以使用信任管理器API以编程方式将凭据导入AEM Forms。 例如，您可以导入用于签署PDF文档的凭据。 (请参阅 [对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

导入凭据时，请指定凭据的别名。 别名用于执行需要凭据的Forms操作。 导入凭据后，即可在管理控制台中查看，如下图所示。 请注意，凭据的别名是 *安全*.

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>无法使用Web服务将凭据导入AEM Forms。

### 步骤摘要 {#summary-of-steps}

要将凭据导入AEM Forms，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 引用凭据。
1. 执行导入操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建凭据服务客户端**

在以编程方式将凭据导入AEM Forms之前，请创建凭据服务客户端。 有关信息，请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**引用凭据**

引用要导入到AEM Forms中的凭据。 与此部分关联的快速入门引用文件系统中的一个P12文件。

**执行导入操作**

引用凭据后，将该凭据导入AEM Forms。 如果未成功导入凭据，则会引发异常。 导入凭据时，请指定凭据的别名。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[凭据服务API快速启动](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用信任管理器API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API导入凭据 {#import-credentials-using-the-java-api}

使用信任管理器API (Java)将凭据导入AEM Forms：

1. 包含项目文件

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `CredentialServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用凭据

   * 创建 `java.io.FileInputStream` 对象。 传递一个指定凭据位置的字符串值。
   * 创建 `com.adobe.idp.Document` 通过使用 `com.adobe.idp.Document` 构造函数。 传递 `java.io.FileInputStream` 包含构造函数的凭据的对象。

1. 执行导入操作

   * 创建一个包含一个元素的字符串数组。 分配值 `truststore.usage.type.sign` 到元素。
   * 调用 `CredentialServiceClient` 对象的 `importCredential` 方法并传递以下值：

      * 指定凭据的别名值的字符串值。
      * 此 `com.adobe.idp.Document` 存储凭据的实例。
      * 一个字符串值，它指定与凭据关联的密码。
      * 包含用法值的字符串数组。 例如，您可以指定此值 `truststore.usage.type.sign`. 要导入Reader扩展凭据，请指定 `truststore.usage.type.lcre`.

**另请参阅**

[使用信任管理器API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速入门（SOAP模式）：使用Java API导入凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用信任管理器API删除凭据 {#deleting-credentials-by-using-the-trust-manager-api}

您可以使用信任管理器API以编程方式删除凭据。 删除凭据时，请指定与该凭据对应的别名。 删除后，无法使用凭据执行操作。

>[!NOTE]
>
>无法使用Web服务删除AEM Forms中的凭据。

### 步骤摘要 {#summary_of_steps-1}

要删除凭据，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 执行删除操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar (如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

有关这些JAR文件位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建凭据服务客户端**

在以编程方式删除凭据之前，请先创建数据集成服务客户端。 创建服务客户端时，您可以定义调用服务所需的连接设置。 有关信息，请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**执行删除操作**

要删除凭据，请指定与该凭据对应的别名。 如果指定的别名不存在，则会引发异常。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

### 使用Java API删除凭据 {#deleting-credentials-using-the-java-api}

使用信任管理器API (Java)从AEM Forms中删除凭据：

1. 包含项目文件

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `CredentialServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 执行删除操作

   调用 `CredentialServiceClient` 对象的 `deleteCredential` 方法，并传递一个指定别名值的字符串值。

**另请参阅**

[使用信任管理器API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速入门（SOAP模式）：使用Java API删除凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
