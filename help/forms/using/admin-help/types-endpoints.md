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
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 端点类型{#types-of-endpoints}

必须配置并启用端点，才能使用服务。 端点指定如何调用服务。

>[!NOTE]
>
>在Workbench中，端点称为起点。

可以向服务添加以下类型的端点。 并非所有服务都支持所有端点：

**电子邮件：** 通过向指定的电子邮件帐户发送包含一个或多个文件附件的电子邮件，使用户能够调用服务。在配置电子邮件端点之前，必须配置所需的电子邮件帐户。 （请参阅配置电子邮件端点。）

**监视文件夹：** 允许用户通过将文件放置在文件夹中来调用服务，该文件夹以定义的间隔进行扫描。（请参阅配置监视文件夹端点。）

**TaskManager:** 使工作区用户能够调用服务。

**远程处理：** 使用由Flex构建的应用程序能够使用(AEM表单已弃用)AEM Forms Remoting调用服务。将自动为每个已激活的服务创建远程处理端点。 创建与端点同名的Flex目标，Flex客户端可以创建指向此目标的远程对象以调用相关服务上的操作。

**SOAP:** 使使用AEM表单编程API开发的客户端应用程序能够使用SOAP模式调用服务。将为每个激活的服务自动创建SOAP端点。

**注意**: *在Adobe Acrobat或Adobe Reader中查看文档时，如果使用SOAP端点，则可以从文档安全文档中删除安全性。有关如何在LCRM文档上禁用SOAP端点的详细信息，请参阅[禁用文档安全文档的SOAP端点](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** 使使用AEM Forms编程API开发的客户端应用程序能够使用企业JavaBeans(EJB)模式调用服务。将为每个激活的服务自动创建EJB端点。

**WSDL:** 使使用AEM表单编程API开发的客户端应用程序能够使用Web服务定义语言(WSDL)调用服务。“核心配置”页包含一个选项，用于为AEM表单所包含的所有服务启用WSDL生成。 (请参阅配置常规AEM表单设置。)

**REST:** 可以配置在Workbench中创建的进程，以便您能够通过代表状态传输(REST)请求调用它们。REST请求从HTML页面发送。 即，您可以使用REST请求直接从网页调用AEM表单进程。

电子邮件、TaskManager、监视文件夹和远程处理端点仅显示服务的特定操作。 添加这些端点需要第二个配置步骤来选择调用服务、设置配置参数以及指定输入和输出参数映射的方法。
