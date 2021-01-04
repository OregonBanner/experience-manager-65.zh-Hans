---
title: 使用凭据
seo-title: 使用凭据
description: 使用Trust Manager API和Java API将凭据导入AEM Forms。 此外，了解如何使用Trust Manager API和Java API删除凭据。
seo-description: 使用Trust Manager API和Java API将凭据导入AEM Forms。 此外，了解如何使用Trust Manager API和Java API删除凭据。
uuid: b794428f-49bf-4a91-bc5f-d855881f4f38
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: bc06d9bd-af6c-47b1-b46f-aab990ef5816
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# 使用凭据{#working-with-credentials}

**关于凭据服务**

凭据包含签名或识别文档所需的私钥信息。 证书是您为信任配置的公钥信息。 AEM Forms使用证书和证书用于以下几个用途：

* Acrobat Reader DC扩展使用凭据启用PDF文档中的Adobe Reader使用权。 (请参阅[将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。)
* 签名服务在执行诸如对PDF文档进行数字签名等操作时访问证书和凭据。 (请参阅[对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

您可以使用Trust Manager Java API与凭据服务进行有序交互。 您可以执行以下任务:

* [使用Trust Manager API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)
* [使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

>[!NOTE]
>
>您还可以使用管理控制台导入和删除证书。 （请参阅[管理帮助。](https://www.adobe.com/go/learn_aemforms_admin_63)）

## 使用Trust Manager API {#importing-credentials-by-using-the-trust-manager-api}导入凭据

您可以使用Trust Manager API以编程方式将凭据导入AEM Forms。 例如，您可以导入用于签署PDF文档的凭据。 (请参阅[对PDF文档进行数字签名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents))。

在导入凭据时，您为凭据指定别名。 别名用于执行需要凭据的Forms操作。 导入后，可以在管理控制台中查看凭据，如下图所示。 请注意，凭据的别名为&#x200B;*Secure*。

![ww_ww_truststore](assets/ww_ww_truststore.png)

>[!NOTE]
>
>不能使用Web服务将凭据导入AEM Forms。

### 步骤{#summary-of-steps}的摘要

要将凭据导入AEM Forms，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 引用凭据。
1. 执行导入操作。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时是必需的)
* jbossall-client.jar(在JBoss上部署AEM Forms时是必需的)

有关这些JAR文件的位置的信息，请参阅[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建凭据服务客户端**

在以编程方式将凭据导入AEM Forms之前，请创建凭据服务客户端。 有关信息，请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**引用凭据**

引用要导入AEM Forms的凭据。 与此部分关联的快速开始引用文件系统中的P12文件。

**执行导入操作**

引用凭据后，将凭据导入AEM Forms。 如果凭据未成功导入，则会引发异常。 在导入凭据时，您为凭据指定别名。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[凭据服务API快速开始](/help/forms/developing/credential-service-java-api-quick.md#credential-service-java-api-quick-start-soap)

[使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

### 使用Java API {#import-credentials-using-the-java-api}导入凭据

使用Trust Manager API(Java)将凭据导入AEM Forms:

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`CredentialServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 引用凭据

   * 使用`java.io.FileInputStream`对象的构造函数创建&lt;a0/>对象。 传递一个指定凭据位置的字符串值。
   * 使用`com.adobe.idp.Document`构造函数创建存储凭据的`com.adobe.idp.Document`对象。 将包含凭据的`java.io.FileInputStream`对象传递给构造函数。

1. 执行导入操作

   * 创建一个包含一个元素的字符串数组。 将值`truststore.usage.type.sign`指定给元素。
   * 调用`CredentialServiceClient`对象的`importCredential`方法并传递以下值：

      * 一个字符串值，它指定凭据的别名值。
      * 存储凭据的`com.adobe.idp.Document`实例。
      * 一个字符串值，它指定与凭据关联的口令。
      * 包含使用值的字符串数组。 例如，可以指定此值`truststore.usage.type.sign`。 要导入Reader扩展凭据，请指定`truststore.usage.type.lcre`。

**另请参阅**

[使用Trust Manager API导入凭据](credentials.md#importing-credentials-by-using-the-trust-manager-api)

[快速开始（SOAP模式）:使用Java API导入凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Trust Manager API {#deleting-credentials-by-using-the-trust-manager-api}删除凭据

您可以使用信任管理器API以编程方式删除凭据。 在删除凭据时，您需要指定与凭据对应的别名。 删除后，凭据便无法用于执行操作。

>[!NOTE]
>
>不能使用Web服务将凭据删除到AEM Forms。

### 步骤{#summary_of_steps-1}的摘要

要删除凭据，请执行以下步骤：

1. 包括项目文件。
1. 创建凭据服务客户端。
1. 执行删除操作。

**包括项目文件**

将必要的文件包含在您的开发项目中。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-truststore-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时是必需的)
* jbossall-client.jar(在JBoss上部署AEM Forms时是必需的)

有关这些JAR文件的位置的信息，请参阅[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建凭据服务客户端**

在以编程方式删除凭据之前，请先创建数据集成服务客户端。 在创建服务客户端时，您定义调用服务所需的连接设置。 有关信息，请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**执行删除操作**

要删除凭据，请指定与凭据对应的别名。 如果指定的别名不存在，则会引发异常。

**另请参阅**

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[使用Java API导入凭据](credentials.md#import-credentials-using-the-java-api)

### 使用Java API {#deleting-credentials-using-the-java-api}删除凭据

使用Trust Manager API(Java)从AEM Forms删除凭据：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-truststore-client.jar。

1. 创建凭据服务客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`CredentialServiceClient`对象的构造函数并传递`ServiceClientFactory`对象，创建&lt;a0/>对象。

1. 执行删除操作

   调用`CredentialServiceClient`对象的`deleteCredential`方法并传递一个指定别名值的字符串值。

**另请参阅**

[使用Trust Manager API删除凭据](credentials.md#deleting-credentials-by-using-the-trust-manager-api)

[快速开始（SOAP模式）:使用Java API删除凭据](/help/forms/developing/credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

[包括AEM FormsJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
