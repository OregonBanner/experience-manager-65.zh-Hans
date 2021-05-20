---
title: 为EMC Documentum配置Connector
seo-title: 为EMC Documentum配置Connector
description: 了解如何配置EMC Documentum的连接器，以实现AEM表单与EMC Documentum之间的通信。
seo-description: 了解如何配置EMC Documentum的连接器，以实现AEM表单与EMC Documentum之间的通信。
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 1%

---

# 为EMC Documentum {#configuring-connector-for-emc-documentum}配置连接器

EMC Documentum的Connector支持AEM表单与EMC Documentum之间的通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“ECM连接器”。

为EMC Documentum设置Connector涉及配置服务器连接和存储库凭据。

>[!NOTE]
>
>在早期版本中，资产可以存储在ECM存储库中。 在当前版本中，资产存储在AEM Forms本机存储库中，并且已弃用存储库提供程序服务。 在升级到AEM Forms时，会将资产从ECM存储库迁移到AEM Forms存储库。 有关更多信息，请参阅适用于您的应用程序服务器的AEM Forms升级指南。

## 配置服务器连接{#configuring-the-server-connection}

本主题介绍了在“配置设置”页面上可以执行的EMC Documentum Connector的任务。

>[!NOTE]
>
>如果同时配置所有设置，则只需单击保存一次。

### 配置服务器{#configure-the-server}

您需要配置连接代理服务器信息。 此信息对于连接到Documentum内容存储库和启动EMC Documentum的Connector是必需的。

1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 在“Documentum Configuration Information ”区域中，输入连接代理的主机名或IP地址和端口号。 端口号必须为正整数（例如，1489）。
1. 单击保存。

### 配置主凭据{#configure-principal-credentials}

配置主凭据时，您提供的存储库名称取决于登录期间是否提供了明确的存储库名称。

如果输入的用户名或密码不正确，您将获得以下结果，具体取决于服务当前是否正在运行：

* 如果EMC Documentum Repository Provider服务和EMC Documentum Content Repository Connector服务都停止，则在保存服务配置信息时，不会显示任何错误。 但是，下次启动服务时，将引发异常，并且服务将不会启动。
* 如果启动了EMC Documentum Repository Provider服务或EMC Documentum Content Repository Connector服务，则在保存服务配置信息时，该服务会尝试立即验证凭据信息。 在这种情况下，会发生错误，并且未保存配置信息。

1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 在“Documentum Principal Credentials Information ”区域中，键入具有超级管理员权限的用户的用户名和密码。
1. 如果在登录期间未提供明确的存储库名称，请输入与凭据关联的存储库名称。
1. 单击保存。

### 更改存储库服务提供程序{#change-the-repository-service-provider}

您可以配置要与Documentum一起使用的存储库服务提供商。 存储库服务调用将委派给您配置的提供程序。 以下选项可供选择：

**当前存储库服务提供程序名称：** 当前存储库服务提供程序的名称

**ECM Documentum存储库提供程序：** 使Documentum存储库提供程序成为存储库的提供程序。此选项已弃用

**存储库提供程序：** 使本机存储库提供程序成为存储库的提供程序

>[!NOTE]
>
>要选择列出的存储库服务提供商以外的存储库服务提供商，请在“应用程序和服务”>“服务管理”中配置RepositoryService。<!-- Fix broken link (See Managing Services) -->。

1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 在“存储库服务提供程序信息”区域，选择替代的存储库服务提供程序。
1. 单击保存。

## 配置存储库凭据{#configuring-repository-credentials}

Documentum凭据信息在AEM Forms系统上下文中使用。 存储库凭据特定于Documentum中的特定存储库。 您可以为任意数量的存储库提供凭据；但是，您只能为每个存储库指定一组凭据。

### 添加存储库凭据{#add-a-repository-credential}

1. 在管理控制台中，单击“服务”>“ EMC Documentum的连接器”>“存储库凭据设置”。
1. 单击添加。出现“Documentum System Credentials Information（Documentum系统凭据信息）”页。
1. 输入存储库的名称。
1. 输入用户名和密码。
1. 单击保存。

如果Content Repository Connector for EMC Documentum服务和/或Repository Service for EMC Documentum正在运行，则在将凭据信息存储到数据库中之前，会根据指定的存储库验证凭据信息。 如果凭据无效或存在，则会显示错误消息。

### 删除存储库凭据{#remove-a-repository-credential}

1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 选中要从中删除凭据的存储库旁边的复选框，然后单击删除。 所选存储库的凭据将从数据库中删除。

### 更改存储库凭据{#change-the-user-name-and-password-for-a-repository-credential}的用户名和密码

1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 单击存储库的名称以编辑其凭据。
1. 更改存储库的用户名或密码，或同时更改两者。 （存储库名称为只读。）
1. 单击保存。

如果Content Repository Connector for EMC Documentum服务和/或Repository Service for EMC Documentum正在运行，则在将凭据信息存储到数据库中之前，会根据指定的存储库验证凭据信息。 如果凭据无效或存在，则会显示错误消息。

## 启用共享工作区任务队列{#enable-the-request-for-sharing-of-workspace-task-queues}的请求

需要一些手动步骤来确保工作区中“请求共享任务队列”功能与EMC Documentum的Connector一起正常工作。

1. 部署AEM表单并安装Workbench后，登录到Workbench并打开“资源”视图。 您将从此视图确定QueueSharing.swf文件的位置。
1. 将QueueSharing.swf文件从“资源视图”拖到Windows桌面或等效位置，具体取决于您的操作系统。
1. 在管理控制台中，单击“服务”>“EMC Documentum的连接器”>“配置设置”。
1. 在“存储库服务提供商信息”下，将配置的存储库提供商更改为“ EMC Documentum存储库提供商”。
1. 启动Workbench ，并将QueueSharing.swf文件从您最初将其复制到的位置（例如，Windows桌面或其他位置）复制到EMC Documentum存储库内的现有目录中。
1. 在Workbench“进程”视图中，打开队列共享进程。
1. 在“变量”视图中，打开“theForm”变量的属性，并更改URI以匹配在步骤5中放置QueueSharing.swf文件的路径。
1. 保存进程。
1. 根据贵组织的策略将流程迁移到生产环境。
