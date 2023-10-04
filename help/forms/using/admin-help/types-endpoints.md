---
title: 端点类型
description: 了解不同类型的端点。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 端点类型 {#types-of-endpoints}

必须先配置和启用端点，然后才能使用服务。 终结点指定如何调用服务。

>[!NOTE]
>
>在Workbench中，端点称为起点。

可以将以下类型的端点添加到服务。 并非所有服务都支持所有端点：

**电子邮件：** 使用户可以通过向指定的电子邮件帐户发送带有一个或多个文件附件的电子邮件来调用服务。 在配置电子邮件端点之前，必须配置所需的电子邮件帐户。 （请参阅配置电子邮件端点。）

**观察文件夹：** 使用户可以通过将文件放在文件夹中调用服务，该文件夹以定义的时间间隔进行扫描。 （请参阅配置观察文件夹端点。）

**任务管理器：** 使Workspace用户能够调用服务。

**远程处理：** 允许使用Flex构建的应用程序使用(不推荐用于AEM表单)AEM表单远程处理来调用该服务。 将为每个激活的服务自动创建远程端点。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的远程对象，以调用对相关服务的操作。

**SOAP：** 使使用AEM表单编程API开发的客户端应用程序能够使用SOAP模式调用服务。 将为每个激活的服务自动创建SOAP端点。

**注意**： *在Adobe Acrobat或Adobe Reader中查看文档时使用SOAP端点时，可以从Document Security文档中删除安全性。 有关如何在LCRM文档上禁用SOAP端点的详细信息，请参阅 [禁用Document Security文档的SOAP端点](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB：** 使使用AEM表单编程API开发的客户端应用程序能够使用Enterprise JavaBeans (EJB)模式调用服务。 将为每个激活的服务自动创建EJB端点。

**WSDL：** 使使用AEM表单编程API开发的客户端应用程序能够使用Web服务定义语言(WSDL)调用服务。 “核心配置”页包含一个选项，用于为AEM表单中的所有服务启用WSDL生成。 (请参阅配置常规AEM表单设置。)

**REST：** 可以配置在Workbench中创建的进程，以便您可以通过代表性状态传输(REST)请求来调用它们。 从HTML页发送REST请求。 即，您可以使用REST请求直接从网页调用AEM表单进程。

电子邮件、 TaskManager 、 Watched Folder和Remoting端点仅公开服务的特定操作。 添加这些端点需要执行第二个配置步骤，以选择用于调用服务的方法、设置配置参数以及指定输入和输出参数映射。
