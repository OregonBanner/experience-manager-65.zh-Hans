---
title: 为IBM FileNet配置连接器
seo-title: 为IBM FileNet配置连接器
description: 了解如何配置Connector for IBM FileNet以实现AEM表单与IBM FileNet之间的通信。
seo-description: 了解如何配置Connector for IBM FileNet以实现AEM表单与IBM FileNet之间的通信。
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# 为IBM FileNet {#configuring-connector-for-ibm-filenet}配置连接器

IBM FileNet连接器支持AEM表单与IBM FileNet之间的通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“Connectors for ECM”。

>[!NOTE]
>
>在早期版本中，资产可以存储在ECM存储库中。 在此版本中，资产存储在AEM forms本机存储库中，并且已弃用存储库提供程序服务。 将资产从ECM存储库迁移到AEM表单存储库是在您执行升级到AEM表单时完成的。 有关详细信息，请参阅适用于应用程序服务器的AEM表单升级指南。

## 配置与内容引擎{#configure-the-connection-to-the-content-engine}的连接

IBM FileNet P8内容引擎提供软件服务，用于管理FileNet内容存储库中的企业内容和客户定义的业务对象。

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 在“内容引擎URL”框中，输入完整的连接URL。 例如：

   如果您正在将FileNet Content Engine 4.x与CEWS传输结合使用，请输入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果将FileNet Content Engine 4.x与EJB传输一起使用（仅WebLogic支持），请输入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在凭据保护方案列表中，选择以下保护级别之一：

   * **清除：以** 不受保护的模式通过网络发送凭据
   * **对称：在** 网络中发送加密凭据

1. 在“加密文件位置”框中，输入加密文件的路径：

   * 如果选择“清除”作为凭据保护方案，则忽略此关键字及其值。
   * 如果选择“对称”作为凭据保护方案，则输入的路径将指向表单服务器上包含要使用的加密密钥的加密文件的位置。

1. 在“默认对象存储”框中，输入AEM表单默认连接到的对象存储连接器。
1. 在“用户名”框中，输入您在上一步中指定的对默认对象存储具有访问权限的用户的用户名。
1. 在“口令”框中，输入用户的口令，然后单击“保存”。

## 配置进程引擎设置{#configure-the-process-engine-settings}

IBM FileNet的连接器包含用于IBM FileNet的Process Engine Connector服务，该服务用于与IBM FileNet Process Engine进行交互。 您可以配置此服务的设置。

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 要启用IBM FileNet服务的Process Engine Connector，请选择“Use Process Engine Connector Service”。
1. 在“进程路由器／连接点”框中，输入主机名或IP地址和端口号，后跟进程路由器的名称。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在“用户名”框中，输入用于连接到流程引擎的用户名。
1. 在“口令”框中，输入用于连接到流程引擎的口令，然后单击“保存”。

## 服务设置{#validation-of-service-settings}的验证

如果在配置与内容引擎的连接或流程引擎设置时输入了不正确的用户名或密码，您将获得以下结果，具体取决于服务当前是否正在运行：

* 如果同时停止IBM FileNet的存储库提供程序服务和IBM FileNet的内容存储库连接器服务，则在保存服务配置信息时，不会显示错误。 但是，下次开始服务时，将引发异常，服务将不开始。
* 如果启动IBM FileNet的存储库提供程序服务或IBM FileNet的内容存储库连接器服务，则保存服务配置信息时，该服务将尝试立即验证凭据信息。 在这种情况下，将发生错误，并且不保存配置信息。

## 更改存储库服务提供商{#change-the-repository-service-provider}

您可以配置要与FileNet一起使用的存储库服务提供商。 存储库服务调用将委派给您配置的提供程序。

以下选项可供选择：

**当前存储库提供** 者名称：当前存储库服务提供商的名称

**IBM FileNet存储库提供** 程序：使FileNet存储库提供程序成为存储库的提供程序。此选项已弃用。

**存储库提供** 者：使本机存储库提供者成为存储库的提供者

>[!NOTE]
>
>要选择除所列服务提供商之外的存储库服务，请在应用程序和服务中配置RepositoryService。<!-- Fix broken link(See Managing Services) -->

1. 在管理控制台中，单击“服务”>“IBM FileNet连接器”。
1. 在“存储库服务提供商信息”区域，选择替代存储库服务提供商，然后单击“保存”。
