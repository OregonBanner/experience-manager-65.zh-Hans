---
title: 在JEE上为AEM Forms配置安全管理设置
seo-title: 在JEE上为AEM Forms配置安全管理设置
description: 了解如何管理用户帐户和服务，这些帐户和服务虽然在专用开发环境中是必需的，但在JEE上的AEM Forms生产环境中却不是必需的。
seo-description: 了解如何管理用户帐户和服务，这些帐户和服务虽然在专用开发环境中是必需的，但在JEE上的AEM Forms生产环境中却不是必需的。
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Administrator
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# 在JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}上为AEM Forms配置安全管理设置

了解如何管理用户帐户和服务，这些帐户和服务虽然在专用开发环境中是必需的，但在JEE上的AEM Forms生产环境中却不是必需的。

通常，开发人员不会使用生产环境来构建和测试其应用程序。 因此，您必须管理用户帐户和服务，尽管在专用开发环境中是必需的，但在生产环境中却不是必需的。

本文介绍了通过JEE上的AEM Forms提供的管理选项来减少整体攻击面的方法。

## 禁用对服务的非必要远程访问{#disabling-non-essential-remote-access-to-services}

在JEE上安装和配置AEM Forms后，许多服务都可用于通过SOAP和Enterprise JavaBeans™(EJB)进行远程调用。在本例中，“远程”一词是指对应用程序服务器的SOAP、EJB或“操作消息格式”(AMF)端口具有网络访问权限的任何调用方。

尽管JEE服务上的AEM Forms要求为授权调用方传递有效凭据，但您应仅允许远程访问您需要远程访问的服务。 要实现有限的无障碍性，您应将远程访问服务集减少到尽可能少的功能系统，然后启用对您需要的其他服务的远程调用。

JEE服务上的AEM Forms始终至少需要SOAP访问。 这些服务通常是Workbench使用所必需的，但也包括由工作区Web应用程序调用的服务。

使用管理控制台中的“应用程序和服务”网页完成此过程：

1. 在Web浏览器中键入以下URL以登录到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击&#x200B;**服务>应用程序和服务>首选项**。
1. 设置首选项，以查看同一页面上最多200个服务和端点。
1. 单击&#x200B;**Services** > **Applications and Services** > **Endpoint Management**。
1. 从&#x200B;**Provider**&#x200B;列表中选择&#x200B;**EJB**，然后单击&#x200B;**Filter**。
1. 要禁用所有EJB端点，请选中列表中每个端点旁边的复选框，然后单击&#x200B;**禁用**。
1. 单击&#x200B;**Next**，然后对所有EJB端点重复上一步骤。 在禁用端点之前，请确保EJB在“提供程序”列中列出。
1. 从&#x200B;**Provider**&#x200B;列表中选择&#x200B;**SOAP**，然后单击&#x200B;**Filter**。
1. 要删除SOAP端点，请选中列表中每个端点旁边的复选框，然后单击&#x200B;**删除**。 请勿删除以下端点：

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * 模板管理器
   * 存储库服务
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * 工作区单点登录
   * ApplicationManager

1. 单击&#x200B;**Next**，然后对上面列表中未包含的SOAP端点重复上一步。 在删除端点之前，请确保SOAP列在提供程序列中。

## 禁用对服务的非必要匿名访问{#disabling-non-essential-anonymous-access-to-services}

某些形式的服务器服务允许对某些操作进行未经身份验证（匿名）的调用。 这意味着，该服务公开的一个或多个操作可以作为任何经过身份验证的用户或根本不作为经过身份验证的用户来调用。

1. 在Web浏览器中键入以下URL以登录到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击&#x200B;**服务>应用程序和服务>服务管理**。
1. 单击要禁用的服务的名称（例如，AuthenticationManagerService）。
1. 单击&#x200B;**安全选项卡**，取消选择&#x200B;**允许匿名访问**，然后单击&#x200B;**保存**。
1. 完成以下服务的步骤3和4:

   * AuthenticationManagerService
   * EJB
   * 电子邮件
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * 远程处理
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * 用户服务
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   如果您打算公开这些服务中的任何服务进行远程调用，则还应考虑禁用这些服务的匿名访问。 否则，任何具有此服务网络访问权限的呼叫者都可以调用该服务，而不传递有效的凭据。

   对于任何不需要的服务，应禁用匿名访问。 许多内部服务都要求启用匿名身份验证，因为此类身份验证需要系统中的潜在任何用户调用，而无需预先授权。

## 更改默认的全局超时{#changing-the-default-global-time-out}

最终用户可以通过Workbench、AEM Forms Web应用程序或调用AEM Forms服务器服务的自定义应用程序对AEM Forms进行身份验证。 一个全局超时设置用于指定此类用户在被强制重新验证之前可以与AEM Forms（使用基于SAML的断言）进行交互的时长。 默认设置为2小时。 在生产环境中，需要将时间缩短到可接受的最小分钟数。

### 将重新验证时间限制最小化{#minimize-reauthentication-time-limit}

1. 在Web浏览器中键入以下URL以登录到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击&#x200B;**设置>用户管理>配置>导入和导出配置文件**。
1. 单击&#x200B;**导出**&#x200B;以生成具有现有AEM Forms设置的config.xml文件。
1. 在编辑器中打开XML文件，并找到以下条目：

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 将值更改为大于5的任意数字（以分钟为单位）并保存文件。
1. 在管理控制台中，导航到导入和导出配置文件页面。
1. 输入修改后的config.xml文件的路径，或单击浏览以导航到该文件。
1. 单击&#x200B;**Import**&#x200B;以上传修改后的config.xml文件，然后单击&#x200B;**确定**。
