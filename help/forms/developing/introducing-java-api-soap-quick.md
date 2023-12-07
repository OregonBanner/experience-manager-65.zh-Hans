---
title: Java&trade； API快速入门简介
description: 了解如何使用通过SOAP连接启用的强类型API，即AEM Forms Java&trade；来执行AEM Forms操作。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Java™ API快速入门简介 {#introducing-java-api-quickstart}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

AdobeAEM Forms API快速入门可以帮助您加速开发与AEM Forms服务交互的程序。 *快速入门*&#x200B;是完整的程序，您可以将其复制并粘贴到您自己的项目中，并用作起点。 您可以运行快速入门以了解其行为方式，并根据自己的需求对其进行修改。

AEM Forms操作可以使用AEM Forms强类型API执行，并且连接模式应设置为SOAP。

Java™强类型API快速入门提供了执行Java™应用程序所需的JAR文件列表。 大多数Java™快速启动程序都是在中运行的控制台应用程序 `main`. 但是，Forms Java™强类型API快速入门是作为在Web应用程序中运行的Java™ Servlet实现的。

JAR文件列表位于“快速入门”开头的注释部分中。 例如，以下注释位于输出快速入门中，并且是在每个Java™快速入门中找到的典型JAR文件列表。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 多服务快速入门 {#multiple-services-quick-start}

最快速入门 *在JEE中使用AEM Forms编程* 调用特定服务以执行操作。 但是，有些快速入门会调用多个AEM Forms服务来执行给定工作流。 以下列表提供了可调用多个AEM Forms服务的Java™快速启动：

[快速入门（SOAP模式）：使用Java™ API将AEM Forms存储库中的文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （调用Repository and Output服务）

[快速入门（SOAP模式）：使用Java™ API基于片段创建PDF文档](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （调用Assembler and Output服务）

[快速入门（SOAP模式）：使用Java™ API创建包含提交的XML数据的PDF文档](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (调用Forms、输出和文档管理服务)

[快速入门（SOAP模式）：使用Java™ API将文档传递到Forms服务](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (调用Forms和文档管理服务)

[快速入门（SOAP模式）：使用Java™ API对基于XFA的表单进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (调用Forms和签名服务)

[快速入门（SOAP模式）：使用Java™ API管理角色和权限](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （调用DirectoryManager和AuthorizationManager服务）

[快速入门（SOAP模式）：使用Java™ API将文档传递到输出服务](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （调用Output and Document Management服务）

>[!NOTE]
>
>《使用AEM Forms进行编程快速入门》基于在JBoss®应用程序服务器和Microsoft® Windows®操作系统上部署的AEM Forms。 但是，如果您使用的是其他操作系统(如UNIX®)，请将特定于Windows的路径替换为适用的操作系统支持的路径。 同样，如果您使用的是其他J2EE应用程序服务器，请确保指定有效的连接属性。 (请参阅 [设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
大多数Web服务快速启动都使用C#编写，并使用.NET Framework。 但是，您可以创建客户端应用程序逻辑，以便能够在支持SOAP标准的任何开发环境中调用AEM Forms服务。 (请参阅 [使用Web服务调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
