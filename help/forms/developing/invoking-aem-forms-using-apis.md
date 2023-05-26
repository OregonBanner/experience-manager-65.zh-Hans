---
title: 使用API调用AEM Forms
seo-title: Invoking AEM Forms using APIs
description: 使用API调用AEM Forms
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 使用API调用AEM Forms {#invoking-aem-forms-using-apis}

**本文档中的示例和示例仅适用于AEM Forms on JEE环境。**

Adobe Experience Manager Forms是基于J2EE的企业软件，包含在共享基础架构中运行的服务。 服务操作通常使用或生成文档。 通过使用AEM Forms，您可以将表单工作流程与电子表单、文档安全和文档生成结合到一组集成且有凝聚力的服务中。 可以从防火墙内部和外部访问这些服务。

客户端应用程序可以使用Java API、Web服务、远程处理和REST以编程方式调用AEM Forms服务。 使用管理控制台，您可以配置服务以通过编程方式调用来公开允许AEM Forms服务的端点。 默认情况下，大多数服务都预先配置为公开远程处理、Java和Web服务端点。

您的业务要求决定了要使用的调用方法。 例如，使用Java API，您可以将AEM Forms功能集成到Java企业应用程序，如Java实体和消息Bean。 同样，您可以使用Web服务将AEM Forms功能集成到.NET项目（或使用支持Web服务标准的开发环境开发的其他项目）中。

服务需要服务容器才能运行，这与Enterprise JavaBeans™ (EJB)需要J2EE容器类似。 AEM Forms仅包含一个服务容器实现。 服务容器负责管理服务的生命周期，包括部署服务并确保将所有请求发送到正确的服务。 它还管理服务使用或产生的文档。

>[!NOTE]
>
>使用AEM表单编程不包括有关如何使用Watched文件夹或电子邮件调用AEM Forms的信息。
