---
title: 为JEE上的AEM Forms配置安全管理设置
description: 了解如何管理用户帐户和服务，这些用户帐户和服务虽然在专用开发环境中是必需的，但在AEM Forms on JEE的生产环境中不是必需的。
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# 为JEE上的AEM Forms配置安全管理设置 {#configuring-secure-administration-settings-for-aem-forms-on-jee}

了解如何管理用户帐户和服务，这些用户帐户和服务虽然在专用开发环境中是必需的，但在AEM Forms on JEE的生产环境中不是必需的。

通常，开发人员不使用生产环境来构建和测试其应用程序。 因此，您必须管理用户帐户和服务，虽然这些用户帐户和服务在专用开发环境中是必需的，但在生产环境中却不是必需的。

本文介绍了通过AEM Forms on JEE提供的管理选项来减少整体攻击表面的方法。

## 禁用对服务的非必要远程访问 {#disabling-non-essential-remote-access-to-services}

安装并配置JEE上的AEM Forms后，可以通过SOAP和Enterprise JavaBeans™ (EJB)进行远程调用的许多服务。在本例中，术语remote是指对应用程序服务器的SOAP、EJB或Action Message Format (AMF)端口具有网络访问权限的任何调用方。

尽管JEE服务上的AEM Forms要求向授权调用方传递有效凭据，但您应仅允许远程访问您需要远程访问的服务。 要获得有限的可访问性，您应该尽可能减少可远程访问的服务集，以便系统正常工作，然后为您所需的其他服务启用远程调用。

JEE服务上的AEM Forms始终需要至少SOAP访问权限。 Workbench通常需要使用这些服务，但这些服务还包括Workspace Web应用程序调用的服务。

使用Administration Console中的“应用程序和服务”网页完成以下过程：

1. 通过在Web浏览器中键入以下URL来登录Administration Console：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击 **服务>应用程序和服务>首选项**.
1. 设置“首选项”可查看同一页面上最多200个服务和端点。
1. 单击 **服务** > **应用程序和服务** > **端点管理**.
1. 选择 **EJB** 从 **提供商** 列表，然后单击 **筛选**.
1. 要禁用所有EJB端点，请选中列表中每个端点旁边的复选框，然后单击 **禁用**.
1. 单击 **下一个** 并对所有EJB端点重复上一步骤。 在禁用端点之前，请确保在提供程序列中列出了EJB。
1. 选择 **SOAP** 从 **提供商** 列表，然后单击 **筛选**.
1. 要删除SOAP端点，请选中列表中每个端点旁边的复选框，然后单击 **移除**. 请勿删除以下端点：

   * AuthenticationmanagerService
   * 目录管理器服务
   * 作业管理器
   * event_management_service
   * 事件配置服务
   * 进程管理器
   * TemplateManager
   * 存储库服务
   * 任务管理器服务
   * 任务队列管理器
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * 应用程序管理器

1. 单击 **下一个** 对于不在上述列表中的SOAP端点，重复上一步骤。 在删除端点之前，请确保在提供程序列中列出SOAP。

## 禁用对服务的非基本匿名访问 {#disabling-non-essential-anonymous-access-to-services}

某些Forms Server服务允许对某些操作进行未经身份验证（匿名）的调用。 这意味着服务公开的一个或多个操作可以作为任何经过身份验证的用户或根本不是经过身份验证的用户调用。

1. 通过在Web浏览器中键入以下URL登录到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击 **服务>应用程序和服务>服务管理**.
1. 单击要禁用的服务的名称（例如，AuthenticationManagerService）。
1. 单击 **“安全”选项卡**，取消选择 **允许匿名访问**，然后单击 **保存**.
1. 完成以下服务的步骤3和4：

   * AuthenticationmanagerService
   * EJB
   * 电子邮件
   * 作业管理器
   * 观察文件夹
   * UsermanagerUtilservice
   * 远程处理
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * 任务管理器服务
   * 任务管理器连接器
   * TaskManagerQueryService
   * 任务队列管理器
   * 任务端点管理器
   * 用户服务
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * 输出服务
   * 表单服务

   如果您打算公开这些服务中的任意服务以进行远程调用，则还应考虑禁用这些服务的匿名访问。 否则，任何对此服务具有网络访问权限的调用者都可以在不传递有效凭据的情况下调用该服务。

   对于任何不需要的服务，应禁用匿名访问。 许多内部服务要求启用匿名身份验证，因为它们需要由系统中的任何潜在用户调用，而无需获得预授权。

## 更改默认全局超时 {#changing-the-default-global-time-out}

最终用户可以通过Workbench、AEM Forms Web应用程序或调用AEM Forms服务器服务的自定义应用程序来验证AEM Forms。 一个全局超时设置用于指定此类用户在被迫重新进行身份验证之前可以与AEM Forms交互的时间（使用基于SAML的断言）。 默认设置为2小时。 在生产环境中，时间量需要减少到可接受的最小分钟数。

### 最大程度地减少重新身份验证时间限制 {#minimize-reauthentication-time-limit}

1. 通过在Web浏览器中键入以下URL登录到管理控制台：

   ```java
            https://[host name]:'port'/adminui
   ```

1. 单击 **设置>用户管理>配置>导入和导出配置文件**.
1. 单击 **导出** 以生成具有现有AEM Forms设置的config.xml文件。
1. 在编辑器中打开XML文件，并找到以下条目：

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. 将该值更改为大于5（以分钟为单位）的任何数字，并保存文件。
1. 在管理控制台中，导航到导入和导出配置文件页面。
1. 输入修改的config.xml文件的路径，或单击“浏览”导航到该文件。
1. 单击 **导入** 上传修改的config.xml文件，然后单击 **确定**.
