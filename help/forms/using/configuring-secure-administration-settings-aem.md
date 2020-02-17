---
title: 在JEE上为AEM Forms配置安全管理设置
seo-title: 在JEE上为AEM Forms配置安全管理设置
description: 了解如何管理用户帐户和服务，尽管这些帐户和服务在私人开发环境中是必需的，但在JEE上的AEM Forms的生产环境中却不是必需的。
seo-description: 了解如何管理用户帐户和服务，尽管这些帐户和服务在私人开发环境中是必需的，但在JEE上的AEM Forms的生产环境中却不是必需的。
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# 在JEE上为AEM Forms配置安全管理设置 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

了解如何管理用户帐户和服务，尽管这些帐户和服务在私人开发环境中是必需的，但在JEE上的AEM Forms的生产环境中却不是必需的。

通常，开发人员不使用生产环境构建和测试其应用程序。 因此，您必须管理用户帐户和服务，尽管在专用开发环境中是必需的，但在生产环境中却不是必需的。

本文介绍了通过JEE上的AEM Forms提供的管理选项来减少整个攻击面的方法。

## 禁用对服务的非基本远程访问 {#disabling-non-essential-remote-access-to-services}

在JEE上安装和配置AEM表单后，许多服务都可通过SOAP和Enterprise javaBeans™(EJB)进行远程调用。在本例中，术语“remote”是指对应用程序服务器的SOAP、EJB或操作消息格式(AMF)端口具有网络访问权限的任何调用者。

尽管JEE服务上的AEM表单需要为授权调用者传递有效凭据，但您应仅允许远程访问需要远程访问的服务。 为了实现有限的辅助功能，您应将远程访问服务集减少到功能系统所能达到的最低限度，然后为需要的其他服务启用远程调用。

JEE服务上的AEM表单始终至少需要SOAP访问。 这些服务通常由Workbench使用，但也包括由Workspace web应用程序调用的服务。

使用管理控制台中的“应用程序和服务”网页完成此过程：

1. 在Web浏览器中键入以下URL，以登录到管理控制台：

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 单击“ **服务”>“应用程序和服务”>“首选项”**。
1. 设置“首选项”可在同一页面上查看多达200个服务和端点。
1. 单击“ **服务** ”>“应 **用程序和服务** ” **>“端**&#x200B;点管理”。
1. 从“提 **供者** ”列表中选择 **EJB** ，然后单击“过 **滤器”**。
1. 要禁用所有EJB端点，请选中列表中每个端点旁边的复选框，然后单击“禁 **用”**。
1. 单击 **下一步** ，然后为所有EJB端点重复上一步。 在禁用端点之前，请确保EJB列在“提供者”列中。
1. 从“ **提供者** ”列表中选 **择SOAP** ，然后单击“ **过滤器**”。
1. 要删除SOAP端点，请选中列表中每个端点旁边的复选框，然后单击“删 **除”**。 请勿删除以下端点：

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * 工作区单点登录
   * ApplicationManager

1. 单击 **下一步** ，然后对上面列表中不存在的SOAP端点重复上一步。 在删除端点之前，请确保SOAP列在“提供者”列中。

## 禁用对服务的非必要匿名访问 {#disabling-non-essential-anonymous-access-to-services}

某些表单服务器服务允许对某些操作进行未经身份验证（匿名）的调用。 这意味着，由服务公开的一个或多个操作可以作为任何已验证用户或根本不作为已验证用户被调用。

1. 在Web浏览器中键入以下URL，登录到管理控制台：

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 单击“ **服务”>“应用程序和服务”>“服务管理”**。
1. 单击要禁用的服务的名称（例如，AuthenticationManagerService）。
1. 单击“安 **全性”选项卡**，取消选 **择“允许匿名访问**”，然后单击“ **保存**”。
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
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService
   如果要公开这些服务中的任何一项以进行远程调用，您还应考虑禁用这些服务的匿名访问。 否则，任何有权访问此服务的呼叫者都可能调用该服务而不传递有效凭据。

   对于任何不需要的服务，应禁用匿名访问。 许多内部服务需要启用匿名身份验证，因为可能需要系统中的任何用户调用这些身份验证，而无需预先授权。

## 更改默认全局超时 {#changing-the-default-global-time-out}

最终用户可以通过Workbench、AEM Forms web应用程序或调用AEM Forms服务器服务的自定义应用程序验证到AEM Forms。 一个全局超时设置用于指定此类用户在被迫重新验证之前可以与AEM表单交互（使用基于SAML的断言）的时间。 默认设置为两小时。 在生产环境中，需要将时间减少到可接受的最小分钟数。

### 将重新验证时间限制降至最低 {#minimize-reauthentication-time-limit}

1. 在Web浏览器中键入以下URL，登录到管理控制台：

   ```as3
            https://[host name]:[port]/adminui
   ```

1. 单击 **设置>用户管理>配置>导入和导出配置文件**。
1. 单击 **导出** ，以生成具有现有AEM Forms设置的config.xml文件。
1. 在编辑器中打开XML文件并找到以下条目：

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. 将该值更改为大于5（以分钟为单位）的任意数字，并保存文件。
1. 在管理控制台中，导航到“导入和导出配置文件”页。
1. 输入修改后的config.xml文件的路径，或单击“浏览”导航到该文件。
1. 单击 **导入** ，上传修改后的config.xml文件，然后单击确 **定**。

