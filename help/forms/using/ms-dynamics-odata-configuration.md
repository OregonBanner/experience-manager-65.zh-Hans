---
title: Microsoft Dynamics OData配置
seo-title: Microsoft Dynamics ODtata configuration
description: 通过表单数据模型利用、集成和使用在线和本地Microsoft Dynamics服务。
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Microsoft Dynamics OData配置{#microsoft-dynamics-odata-configuration}

![数据集成](assets/data-integeration.png)

Microsoft Dynamics是一款客户关系管理(CRM)和企业资源规划(ERP)软件，为创建和管理客户帐户、联系人、潜在客户、机会和案例提供企业解决方案。 [AEM Forms数据集成](../../forms/using/data-integration.md) 提供OData云服务配置，以将Forms与联机和本地Microsoft Dynamics服务器集成。 它允许您根据Microsoft Dynamics服务中定义的实体、属性和服务创建表单数据模型。 表单数据模型可用于创建与Microsoft Dynamics服务器交互的自适应表单，以启用业务工作流。 例如：

* 查询Microsoft Dynamics服务器以获取数据并预填充自适应表单
* 在自适应表单提交时，将数据写入Microsoft Dynamics
* 通过在表单数据模型中定义的自定义实体在Microsoft Dynamics中写入数据，反之亦然

AEM Forms附加组件包还包含引用OData配置，您可以利用这些配置来快速将Microsoft Dynamics与AEM Forms集成。

安装包后，可以在您的AEM Forms实例上使用以下实体和服务：

* MS Dynamics ODataCloud Service（OData服务）
* 使用预配置的Microsoft Dynamics实体和服务来表单数据模型。

仅当将AEM实例的运行模式设置为 `samplecontent` （默认）。 MS Dynamics ODataCloud Service（OData服务）也可以与其他运行模式一起使用。 有关为AEM实例配置运行模式的更多信息，请参阅 [运行模式](/help/sites-deploying/configure-runmodes.md).

## 前提条件 {#prerequisites}

在开始设置和配置Microsoft Dynamics之前，请确保：

* 已安装 [AEM Forms附加组件包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已联机配置Microsoft Dynamics 365，或安装了以下某个Microsoft Dynamics版本的实例：

   * Microsoft Dynamics 365内部部署
   * Microsoft Dynamics 2016内部部署

* [在Microsoft Azure Active Directory中注册了Microsoft Dynamics在线服务的应用程序](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 记下注册服务的客户端ID（也称为应用程序ID）值和客户端密钥。 这些值在 [为Microsoft Dynamics服务配置云服务](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## 为注册的Microsoft Dynamics应用程序设置回复URL {#set-reply-url-for-registered-microsoft-dynamics-application}

请执行以下操作，为已注册的Microsoft Dynamics应用程序设置“回复URL”：

>[!NOTE]
>
>仅在将AEM Forms与联机Microsoft Dynamics服务器集成时，才使用此过程。

1. 转到Microsoft Azure Active Directory帐户，并在 **回复URL** 注册应用程序的设置：

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目录](assets/azure_directory_new.png)

1. 保存配置。

## 为IFD配置Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用基于声明的身份验证来向外部用户提供对Microsoft Dynamics CRM服务器上数据的访问。 要启用此功能，请执行以下操作来配置Microsoft Dynamics以用于面向Internet的部署(IFD)并配置声明设置。

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时，才使用此过程。

1. 按照 [为Microsoft Dynamics配置IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell运行以下命令，以配置启用IFD的Microsoft Dynamics的声明设置：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   请参阅 [内部部署CRM(IFD)的应用程序注册](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 以了解详细信息。

## 在AD FS计算机上配置OAuth客户端 {#configure-oauth-client-on-ad-fs-machine}

执行以下操作，以在Active Directory联合身份验证服务(AD FS)计算机上注册OAuth客户端，并在AD FS计算机上授予访问权限：

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时，才使用此过程。

1. 运行以下命令：

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可以使用任何GUID生成器生成的客户端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData云服务的URL。 随AEM Forms包一起安装的默认云服务部署在以下URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 运行以下命令以在AD FS计算机上授予访问权限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics组织URL。

1. Microsoft Dynamics使用HTTPS协议。 要从Forms服务器调用AD FS端点，请使用将Microsoft Dynamics站点证书安装到Java证书存储区 `keytool` 命令。

## 为Microsoft Dynamics服务配置云服务 {#configure-cloud-service-for-your-microsoft-dynamics-service}

的 **MS Dynamics ODataCloud Service（OData服务）** 配置附带默认OData配置。 要将其配置为与Microsoft Dynamics服务连接，请执行以下操作。

1. 导航到 **[!UICONTROL 工具>Cloud Services>数据源]**，然后点按 `global` 配置文件夹。
1. 选择 **MS Dynamics ODataCloud Service（OData服务）** 配置和点按 **[!UICONTROL 属性]**. 将打开云服务配置属性对话框。

   在 **身份验证设置** 选项卡：

   1. 输入 **服务根** 字段。 转到Dynamics实例，然后导航到 **开发人员资源** 查看服务根字段的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 替换 **客户端Id**(也称为 **应用程序ID**)、 **客户端密钥**, **OAuth URL**, **刷新令牌URL**, **访问令牌URL**&#x200B;和 **资源** 字段，其值来自Microsoft Dynamics服务配置。 必须在 **资源** 字段，用于使用表单数据模型配置Microsoft Dynamics。 使用服务根URL派生dynamics实例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **openid** 在 **授权范围** 用于Microsoft Dynamics上的授权流程的字段。

   ![身份验证设置](assets/dynamics_authentication_settings_new.png)

1. 单击 **[!UICONTROL 连接到OAuth]**. 您将被重定向到Microsoft Dynamics登录页面。
1. 使用Microsoft Dynamics凭据登录，并接受以允许云服务配置连接到Microsoft Dynamics服务。 在云服务和服务之间建立连接是一次性任务。

   然后，系统会将您重定向到云服务配置页面，该页面会显示一条OData配置已成功保存的消息。

MS Dynamics ODataCloud Service（OData服务）云服务已配置并与您的Dynamics服务连接。

## 创建表单数据模型 {#create-form-data-model}

安装AEM Forms包（表单数据模型）时，**Microsoft Dynamics FDM**，将部署在AEM实例上。 默认情况下，表单数据模型使用在MS Dynamics ODataCloud Service（OData服务）中配置的Microsoft Dynamics服务作为其数据源。

首次打开表单数据模型时，它会连接到配置的Microsoft Dynamics服务，并从Microsoft Dynamics实例中获取实体。 Microsoft Dynamics的“联系人”和“潜在客户”实体已添加到表单数据模型中。

要查看表单数据模型，请转到 **[!UICONTROL Forms >数据集成]**. 选择 **Microsoft Dynamics FDM** 单击 **编辑** 以编辑模式打开表单数据模型。 或者，您也可以直接从以下URL打开表单数据模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下来，您可以基于表单数据模型创建自适应表单，并将其用在各种自适应表单用例中，例如：

* 通过查询来自Microsoft Dynamics实体和服务的信息来预填自适应表单
* 使用自适应表单规则在表单数据模型中定义调用Microsoft Dynamics服务器操作
* 将提交的表单数据写入Microsoft Dynamics实体

建议创建随AEM Forms包提供的表单数据模型副本，并配置数据模型和服务以符合您的要求。 它将确保将来对资源包的任何更新不会覆盖您的表单数据模型。

有关在业务工作流中创建和使用表单数据模型的更多信息，请参阅 [数据集成](../../forms/using/data-integration.md).
