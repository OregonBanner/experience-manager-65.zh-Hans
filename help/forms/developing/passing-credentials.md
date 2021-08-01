---
title: 如何使用WS-security标头来传递凭据？
description: 了解如何使用WS-security标头来传递凭据
source-git-commit: 9b118ef4f852e3df1e717bb27b9be272caeb0456
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 使用WS-Security标头传递凭据 {#using-execute-script-service-aem-forms-jee-workbench}

在使用Web服务的JEE服务上调用AEM Forms时，您可以使用WS-Security标头来传递JEE上AEM Forms所需的客户端身份验证信息。 WS-Security定义SOAP扩展，以实现客户端身份验证、消息机密性和消息完整性。 因此，当JEE上的AEM Forms部署为独立服务器或群集环境中时，您可以在JEE服务中调用AEM Forms。

在JEE上将WS-Security标头传递到AEM Forms的方式取决于您使用的是Axis生成的Java类还是使用服务本机SOAP堆栈的.NET客户端程序集。

>[!NOTE]
>
>以使用WS-Security标头调用服务的示例为例，本主题通过调用加密服务，使用密码加密PDF文档。

本文档涵盖以下主题：

* 使用Axis生成的Java类传递客户端身份验证

* 生成调用加密服务所需的轴库文件

* 使用WS-Security标头调用加密服务

* 使用.NET客户端程序集传递客户端身份验证

* 使用WS-Security标头调用加密服务


## 要求 {#requirements}

为了充分利用本文档，您需要对JEE上的AEM Forms软件有深入的了解。

>[!MORELIKETHIS]
>
>* [使用WS-Security标头传递凭据](assets/passing-credentials-using-ws-security-headers.pdf)


