---
title: 为EMC Documentum配置连接器
seo-title: Configuring Connector for EMC Documentum
description: 了解如何配置Connector for EMC Documentum ，以实现AEM Forms与EMC Documentum之间的通信。
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 为EMC Documentum配置连接器 {#configuring-connector-for-emc-documentum}

Connector for EMC Documentum实现了AEM Forms与EMC Documentum之间的通信。 有关其他背景信息，请参阅中的“Connectors for ECM” [服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

为EMC Documentum设置连接器涉及配置服务器连接和存储库凭据。

>[!NOTE]
>
>在早期版本中，资产可以存储在ECM存储库中。 在当前版本中，资产存储在AEM Forms本地存储库中，并且存储库Provider Services已被弃用。 当您升级到AEM表单时，会将资源从ECM存储库迁移到AEM表单存储库。 有关详细信息，请参阅适用于您的应用程序服务器的AEM表单升级指南。

## 配置服务器连接 {#configuring-the-server-connection}

本主题介绍可在“配置设置”页面上执行的EMC Documentum连接器任务。

>[!NOTE]
>
>如果要同时配置所有设置，则只需单击一次保存。

### 配置服务器 {#configure-the-server}

您需要配置连接代理服务器信息。 此信息对于连接到Documentum内容存储库和启动Connector for EMC Documentum是必需的。

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 在“ Documentum配置信息”区域中，输入连接代理的主机名或IP地址和端口号。 端口号必须是正整数（例如，1489）。
1. 单击“保存”。

### 配置主体凭据 {#configure-principal-credentials}

配置主体凭据时，您提供的存储库名称取决于登录期间是否提供明确的存储库名称。

如果输入的用户名或密码不正确，将根据服务当前是否正在运行获得以下结果：

* 如果EMC Documentum Repository Provider服务和EMC Documentum Content Repository Connector服务都已停止，则在保存服务配置信息时，不会出现任何错误。 但是，下次启动服务时，将会引发异常，并且服务不会启动。
* 如果EMC Documentum Repository Provider服务或EMC Documentum Content Repository Connector服务已启动，则在保存服务配置信息时，该服务将尝试立即验证凭据信息。 在这种情况下，会发生错误，并且不会保存配置信息。

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 在“Documentum主体身份证明信息”区域中，键入具有超级管理员权限的用户名和密码。
1. 如果在登录期间未提供显式存储库名称，请输入与凭据关联的存储库名称。
1. 单击“保存”。

### 更改存储库服务提供程序 {#change-the-repository-service-provider}

您可以配置要与Documentum一起使用的存储库服务提供商。 存储库服务调用已委派给您配置的提供程序。 以下选项可供选择：

**当前存储库服务提供程序名称：** 当前存储库服务提供程序的名称

**ECM Documentum存储库提供程序：** 使Documentum存储库提供程序成为存储库的提供程序。 此选项已弃用

**存储库提供程序：** 使本地存储库提供程序成为存储库的提供程序

>[!NOTE]
>
>要选择除列出的系统信息库服务提供程序之外的其他系统信息库服务提供程序，请在应用程序和服务>服务管理中配置RepositoryService。 <!-- Fix broken link (See Managing Services) -->.

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 在“存储库服务提供程序信息”区域中，选择替代存储库服务提供程序。
1. 单击“保存”。

## 配置存储库凭据 {#configuring-repository-credentials}

Documentum凭据信息在AEM表单系统上下文中使用。 存储库凭据特定于Documentum中的特定存储库。 您可以为任意数量的存储库提供凭据；但是，您只能为每个存储库指定一组凭据。

### 添加存储库凭据 {#add-a-repository-credential}

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“存储库凭据设置”。
1. 单击“添加”。 此时将显示“Documentum系统凭据信息”页。
1. 输入存储库的名称。
1. 输入用户名和密码。
1. 单击“保存”。

如果Content Repository Connector for EMC Documentum服务和/或Repository Service for EMC Documentum正在运行，则在将凭据信息存储到数据库中之前，会针对指定的存储库对其进行验证。 如果凭据无效或存在，则会显示错误消息。

### 删除存储库凭据 {#remove-a-repository-credential}

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 选中要从中删除凭据的存储库旁边的复选框，然后单击删除。 所选存储库的凭据将从数据库中删除。

### 更改存储库凭据的用户名和密码 {#change-the-user-name-and-password-for-a-repository-credential}

1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 单击要编辑其凭据的存储库名称。
1. 更改存储库的用户名或密码，或同时更改两者。 （存储库名称是只读的。）
1. 单击“保存”。

如果Content Repository Connector for EMC Documentum服务和/或Repository Service for EMC Documentum正在运行，则在将凭据信息存储到数据库中之前，会针对指定的存储库对其进行验证。 如果凭据无效或存在，则会显示错误消息。

## 启用共享工作区任务队列的请求 {#enable-the-request-for-sharing-of-workspace-task-queues}

需要执行一些手动步骤，以确保Workspace中的“请求共享任务队列”功能可以与Connector for EMC Documentum正常配合使用。

1. 在部署AEM Forms并安装Workbench后，登录到Workbench并打开“资源”视图。 您将确定QueueSharing.swf文件在此视图中的位置。
1. 根据您的操作系统，将QueueSharing.swf文件从“资源视图”拖到Windows桌面或等效位置。
1. 在管理控制台中，单击“服务”>“EMC Documentum连接器”>“配置设置”。
1. 在“存储库服务提供程序信息”下，将配置的存储库提供程序更改为EMC Documentum Repository Provider。
1. 启动Workbench，将QueueSharing.swf文件从最初复制到的位置（例如，Windows桌面或其他位置）复制到EMC Documentum存储库内的现有目录中。
1. 在“工作台流程”视图中，打开“队列共享”流程。
1. 在“变量”视图中，打开“theForm”变量的属性，并更改URI以匹配您在步骤5中放置QueueSharing.swf文件的路径。
1. 保存进程。
1. 根据贵组织的策略将流程迁移到生产环境。
