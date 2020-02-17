---
title: 使用API调用AEM Forms
seo-title: 使用API调用AEM Forms
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用API调用AEM Forms {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms是基于J2EE的企业软件，它包含在共享基础结构中运行的服务。 服务操作通常会消耗或生成文档。 通过使用AEM Forms，您可以将表单工作流程与电子表单、文档安全性和文档生成结合到一套集成且紧密衔接的服务中。 这些服务可从防火墙内外访问。

客户端应用程序可以使用Java API、Web服务、远程处理和REST以编程方式调用AEM Forms服务。 使用管理控制台，您可以配置服务以公开允许通过有序调用AEM Forms服务的端点。 默认情况下，大多数服务都经过预配置以显示远程处理、Java和Web服务端点。

您的业务需求决定了要使用的调用方法。 例如，使用Java API，您可以将AEM Forms功能集成到Java企业应用程序（如Java实体和消息Bean）中。 同样，您可以使用Web服务将AEM Forms功能集成到。NET项目（或使用支持Web服务标准的开发环境开发的其他项目）中。

服务需要一个服务容器来运行，这与Enterprise javaBeans™(EJB)需要J2EE容器的方式类似。 AEM Forms只包括一个服务容器的实现。 服务容器负责管理服务的生命周期，包括部署服务并确保所有请求都发送到正确的服务。 它还管理服务使用或生成的文档。

>[!NOTE]
>
>使用AEM表单进行编程不包括有关如何使用监视文件夹或电子邮件调用AEM表单的信息。

