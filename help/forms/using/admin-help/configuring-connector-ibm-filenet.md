---
title: 为IBM fileNet配置Connector
seo-title: 为IBM fileNet配置Connector
description: 了解如何配置Connector for IBM fileNet以实现AEM表单与IBM fileNet之间的通信。
seo-description: 了解如何配置Connector for IBM fileNet以实现AEM表单与IBM fileNet之间的通信。
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 为IBM fileNet配置Connector {#configuring-connector-for-ibm-filenet}

IBM fileNet连接器支持AEM表单与IBM fileNet之间的通信。 有关其他背景信息，请参阅服务参考中的“ECM [连接器”](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>在早期版本中，资产可以存储在ECM存储库中。 在此版本中，资产存储在AEM表单本机存储库中，存储库提供者服务已弃用。 将资产从ECM存储库迁移到AEM表单存储库是在您升级到AEM表单时完成的。 有关详细信息，请参阅适用于应用程序服务器的AEM表单升级指南。

## 配置与内容引擎的连接 {#configure-the-connection-to-the-content-engine}

IBM fileNet P8内容引擎提供软件服务，用于管理FileNet内容存储库中的企业内容和客户定义的业务对象。

1. 在管理控制台中，单击“服务”>“IBM fileNet连接器”。
1. 在“内容引擎URL”框中，输入完整的连接URL。 例如：

   如果要将FileNet Content Engine 4.x与CEWS传输结合使用，请输入：

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   如果将FileNet Content Engine 4.x与EJB传输一起使用（仅WebLogic支持），请输入：

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. 在“凭据保护方案”列表中，选择以下保护级别之一：

   * **** 清晰：以不受保护的模式通过网络发送凭据
   * **** 对称：通过网络发送加密凭据

1. 在“加密文件位置”框中，输入加密文件的路径：

   * 如果选择“清除”作为凭据保护方案，则忽略此关键字及其值。
   * 如果选择“对称”作为凭据保护方案，则输入的路径将指向表单服务器上包含要使用的加密密钥的加密文件的位置。

1. 在“默认对象存储”框中，输入AEM表单默认连接到的对象存储连接器。
1. 在“用户名”框中，输入您在上一步中指定的默认对象存储的访问权限用户的用户名。
1. 在“口令”框中，输入用户的口令，然后单击“保存”。

## 配置进程引擎设置 {#configure-the-process-engine-settings}

IBM fileNet连接器包含用于IBM fileNet服务的Process Engine Connector，该服务用于与IBM fileNet Process Engine交互。 您可以配置此服务的设置。

1. 在管理控制台中，单击“服务”>“Connector for IBM FileNet”。
1. 要启用Process Engine Connector for IBM fileNet服务，请选择“使用Process Engine Connector Service”。
1. 在“进程路由器／连接点”框中，输入主机名或IP地址和端口号，后跟进程路由器的名称。 例如：

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. 在“用户名”框中，输入用于连接到进程引擎的用户名。
1. 在“口令”框中，输入用于连接进程引擎的口令，然后单击“保存”。

## 服务设置的验证 {#validation-of-service-settings}

如果在配置到内容引擎或进程引擎设置的连接时输入的用户名或口令不正确，则根据服务当前是否正在运行，您将获得以下结果：

* 如果同时停止IBM fileNet的存储库提供者服务和IBM fileNet的Content Repository Connector服务，则在保存服务配置信息时，不会显示错误。 但是，下次启动服务时，将引发异常，且服务将不启动。
* 如果启动IBM FileNet的存储库提供者服务或IBM FileNet的Content Repository Connector服务，则在保存服务配置信息时，该服务将尝试立即验证凭据信息。 在这种情况下，会发生错误，并且不会保存配置信息。

## 更改存储库服务提供商 {#change-the-repository-service-provider}

可以配置要与FileNet一起使用的存储库服务提供商。 存储库服务调用将委派给您配置的提供者。

以下选项可供选择：

**** 当前存储库提供者名称：当前存储库服务提供商的名称

**** IBM fileNet存储库提供商：使FileNet存储库提供者成为存储库的提供者。 已弃用此选项。

**** 存储库提供者：使本机存储库提供者成为存储库的提供者

***注意&#x200B;**:要选择除列出的存储库服务提供者之外的存储库服务提供者，请在“应用程序和服务”中配置RepositoryService。<!-- Fix broken link(See Managing Services) -->*

1. 在管理控制台中，单击“服务”>“IBM fileNet连接器”。
1. 在“存储库服务提供者信息”区域，选择替代存储库服务提供者，然后单击“保存”。

