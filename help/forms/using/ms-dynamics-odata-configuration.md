---
title: Microsoft Dynamics OData配置
seo-title: Microsoft Dynamics ODtata configuration
description: 通过表单数据模型利用、集成在线和本地Microsoft Dynamics服务并与之合作。
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 5ca6c5abeb5ed09d8929d1986aa24c1416e0cc06
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 1%

---

# Microsoft Dynamics OData配置{#microsoft-dynamics-odata-configuration}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html) |
| AEM 6.5 | 本文 |

![数据集成](assets/data-integeration.png)

Microsoft Dynamics是一款客户关系管理(CRM)和企业资源规划(ERP)软件，可提供用于创建和管理客户帐户、联系人、潜在客户、机会和案例的企业解决方案。 [AEM Forms数据集成](../../forms/using/data-integration.md) 提供OData云服务配置以将Forms与在线和本地Microsoft Dynamics服务器集成。 它使您能够根据Microsoft Dynamics服务中定义的实体、属性和服务创建表单数据模型。 表单数据模型可用于创建与Microsoft Dynamics Server交互以启用业务工作流的自适应表单。 例如：

* 查询Microsoft Dynamics服务器以获取数据并预填充自适应表单
* 提交自适应表单时将数据写入Microsoft Dynamics
* 通过表单数据模型中定义的自定义实体在Microsoft Dynamics中写入数据，反之亦然

AEM Forms附加组件包还包括引用OData配置，您可以利用它将Microsoft Dynamics与AEM Forms快速集成。

安装该软件包后，您的AEM Forms实例上提供了以下实体和服务：

* MS Dynamics ODataCloud Service（OData服务）
* 具有预配置的Microsoft Dynamics实体和服务的表单数据模型。

仅当将Microsoft实例的运行模式设置为时，表单数据模型中预配置的AEM Dynamics实体和服务才在您的AEM Forms实例上可用 `samplecontent` （默认）。 MS Dynamics ODataCloud Service（OData服务）也可用于其他运行模式。 有关为AEM实例配置运行模式的更多信息，请参阅 [运行模式](/help/sites-deploying/configure-runmodes.md).

## 前提条件 {#prerequisites}

在开始设置和配置Microsoft Dynamics之前，请确保您具有：

* 已安装 [AEM Forms附加组件包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已在线配置Microsoft Dynamics 365，或已安装以下某个Microsoft Dynamics版本的实例：

   * Microsoft Dynamics 365内部部署
   * Microsoft Dynamics 2016内部部署

* [已在Microsoft Azure Active Directory中注册Microsoft Dynamics在线服务的应用程序](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). 记下已注册服务的客户端ID（也称为应用程序ID）和客户端密钥的值。 在以下情况下会使用这些值： [为Microsoft Dynamics服务配置云服务](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## 为已注册的Microsoft Dynamics应用程序设置回复URL {#set-reply-url-for-registered-microsoft-dynamics-application}

执行以下操作以设置已注册的Microsoft Dynamics应用程序的回复URL：

>[!NOTE]
>
>只有在将AEM Forms与联机Microsoft Dynamics服务器集成时，才使用此过程。

1. 转到Microsoft Azure Active Directory帐户，并在中添加以下云服务配置URL **回复URL** 已注册应用程序的设置：

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目录](assets/azure_directory_new.png)

1. 保存配置。

## 为IFD配置Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用基于声明的身份验证向外部用户提供对Microsoft Dynamics CRM服务器上的数据的访问权限。 要启用此功能，请执行以下操作以配置Microsoft Dynamics for Internet-facing deployment (IFD)并配置声明设置。

>[!NOTE]
>
>只有在将AEM Forms与内部部署Microsoft Dynamics服务器集成时，才使用此过程。

1. 为IFD配置Microsoft Dynamics本地实例，如中所述 [为Microsoft Dynamics配置IFD](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. 使用Windows PowerShell运行以下命令，以在启用了IFD的Microsoft Dynamics上配置声明设置：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   参见 [CRM内部部署(IFD)的应用程序注册](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 了解详细信息。

## 在AD FS计算机上配置OAuth客户端 {#configure-oauth-client-on-ad-fs-machine}

执行以下操作可在Active Directory联合身份验证服务(AD FS)计算机上注册OAuth客户端并授予对AD FS计算机的访问权限：

>[!NOTE]
>
>只有在将AEM Forms与内部部署Microsoft Dynamics服务器集成时，才使用此过程。

1. 运行以下命令：

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是一个可以使用任何GUID生成器生成的客户端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData云服务的URL。 与AEM Forms包一起安装的默认Cloud Service部署在以下URL：
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 运行以下命令以授予对AD FS计算机的访问权限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics组织URL。

1. Microsoft Dynamics使用HTTPS协议。 要从Forms服务器调用AD FS端点，请使用将Microsoft Dynamics站点证书安装到Java证书存储区 `keytool` AEM Forms命令。

## 为Microsoft Dynamics服务配置云服务 {#configure-cloud-service-for-your-microsoft-dynamics-service}

此 **MS Dynamics ODataCloud Service（OData服务）** 配置附带默认OData配置。 要将其配置为与Microsoft Dynamics服务连接，请执行以下操作。

1. 导航到 **[!UICONTROL “工具”>“Cloud Services”>“数据源”]**，然后点按 `global` 配置文件夹。
1. 选择 **MS Dynamics ODataCloud Service（OData服务）** 配置和点按 **[!UICONTROL 属性]**. 将打开Cloud Service配置属性对话框。

   在 **身份验证设置** 选项卡：

   1. 输入值 **服务根目录** 字段。 转到Dynamics实例并导航到 **开发人员资源** 查看“服务根”字段的值。 例如， https://&lt;tenant-name>/api/data/v9.1/

   1. 将缺省值替换为 **客户端ID**(也称为 **应用程序ID**)， **客户端密码**， **OAuth URL**， **刷新令牌URL**， **访问令牌URL**、和 **资源** 包含Microsoft Dynamics服务配置中的值的字段。 必须在以下位置指定动态实例URL： **资源** 用于使用表单数据模型配置Microsoft Dynamics的字段。 使用服务根URL派生动态实例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. 指定 **openid** 在 **授权范围** Microsoft Dynamics上授权过程的字段。

   ![身份验证设置](assets/dynamics_authentication_settings_new.png)

1. 单击 **[!UICONTROL 连接到OAuth]**. 您将被重定向到Microsoft Dynamics登录页面。
1. 使用您的Microsoft Dynamics凭据登录并接受以允许云服务配置连接到Microsoft Dynamics服务。 在Cloud Service和服务之间建立连接是一项一次性任务。

   然后，您将被重定向到Cloud Service配置页面，该页面显示一条消息，指出已成功保存OData配置。

MS Dynamics ODataCloud Service（OData服务）云服务已配置并与您的Dynamics服务连接。

## 创建表单数据模型 {#create-form-data-model}

安装AEM Forms包、表单数据模型时，**Microsoft Dynamics FDM**，部署在您的AEM实例上。 默认情况下，表单数据模型使用在MS Dynamics ODataCloud Service（OData服务）中配置的Microsoft Dynamics服务作为其数据源。

首次打开表单数据模型时，它会连接到配置的Microsoft Dynamics服务，并从Microsoft Dynamics实例中获取实体。 表单数据模型中已添加Microsoft Dynamics中的“联系人”和“潜在客户”实体。

要检查表单数据模型，请转到 **[!UICONTROL Forms >数据集成]**. 选择 **Microsoft Dynamics FDM** 并单击 **编辑** 以在编辑模式下打开表单数据模型。 或者，您也可以直接从以下URL打开表单数据模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下来，您可以基于表单数据模型创建自适应表单，并将其用于各种自适应表单用例，例如：

* 通过查询Microsoft Dynamics实体和服务中的信息预填充自适应表单
* 使用自适应表单规则调用在表单数据模型中定义的Microsoft Dynamics Server操作
* 将提交的表单数据写入Microsoft Dynamics实体

建议创建随AEM Forms包一起提供的表单数据模型副本，并配置数据模型和服务以满足您的要求。 它将确保以后对包的任何更新都不会覆盖您的表单数据模型。

有关在业务工作流中创建和使用表单数据模型的更多信息，请参阅 [数据集成](../../forms/using/data-integration.md).
