---
title: 端点类型
seo-title: 端点类型
description: 了解不同类型的端点。
seo-description: 了解不同类型的端点。
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# 端点类型{#types-of-endpoints}

在使用服务之前，必须配置并启用端点。 端点指定如何调用服务。

>[!NOTE]
>
>在Workbench中，端点称为开始点。

可以向服务添加以下类型的端点。 并非所有服务都支持所有端点：

**电子邮** 件：通过向指定的电子邮件帐户发送包含一个或多个文件附件的电子邮件来启用服务。配置电子邮件端点之前，必须配置所需的电子邮件帐户。 （请参阅配置电子邮件端点。）

**监视的文** 件夹：允许用户通过将文件放入一个文件夹来调用服务，该文件夹以定义的时间间隔进行扫描。（请参阅配置监视的文件夹端点。）

**TaskManager:** 使Workspace用户能够调用服务。

**远程处理：** 使用Flex构建的应用程序能够使用(AEM表单已弃用)AEM表单远程处理调用服务。将自动为每个已激活的服务创建远程处理端点。 创建与端点同名的Flex目标，Flex客户端可以创建指向此目标的远程对象以调用相关服务上的操作。

**SOAP：使** 用AEM表单编程API开发的客户端应用程序能够使用SOAP模式调用服务。将自动为每个已激活的服务创建一个SOAP端点。

**注**: *当在Adobe Acrobat或Adobe Reader查看文档时使用SOAP端点时，可以从文档安全文档中删除安全性。有关如何在LCRM文档上禁用SOAP端点的详细信息，请参阅[禁用文档安全文档的SOAP端点](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** 使使用AEM表单编程API开发的客户端应用程序能够使用企业JavaBeans(EJB)模式调用服务。将自动为每个已激活的服务创建一个EJB端点。

**WSDL：使** 用AEM表单编程API开发的客户端应用程序能够使用Web服务定义语言(WSDL)调用服务。“核心配置”页包含一个选项，用于为AEM表单的所有服务启用WSDL生成。 (请参阅配置常规AEM表单设置。)

**REST：可** 以配置在Workbench中创建的流程，以便您通过代表性状态转移(REST)请求调用它们。REST请求从HTML页发送。 即，您可以使用REST请求直接从网页调用AEM表单进程。

电子邮件、任务管理器、监视文件夹和远程处理端点仅显示服务的特定操作。 添加这些端点需要第二个配置步骤来选择调用服务、设置配置参数以及指定输入和输出参数映射的方法。
