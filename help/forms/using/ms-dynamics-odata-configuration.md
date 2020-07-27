---
title: Microsoft Dynamics OData配置
seo-title: Microsoft Dynamics ODta配置
description: 通过表单数据模型利用、集成和使用在线和内部Microsoft Dynamics服务。
seo-description: 了解如何通过表单数据模型利用并与在线和本地Microsoft Dynamics服务结合使用。
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---


# Microsoft Dynamics OData配置{#microsoft-dynamics-odata-configuration}

![数据集成](assets/data-integeration.png)

Microsoft Dynamics是一款客户关系管理(CRM)和企业资源规划(ERP)软件，为创建和管理客户帐户、联系人、潜在客户、机会和案例提供企业解决方案。 [AEM Forms数据集成](../../forms/using/data-integration.md) 提供OData云服务配置，将表单与在线和本地Microsoft Dynamics服务器集成。 它允许您根据Microsoft Dynamics服务中定义的实体、属性和服务创建表单数据模型。 表单数据模型可用于创建与Microsoft Dynamics服务器交互的自适应表单，以支持业务工作流。 例如：

* 查询Microsoft Dynamics Server的数据并预填充自适应表单
* 在自适应表单提交时将数据写入Microsoft Dynamics
* 通过表单数据模型中定义的自定义实体在Microsoft Dynamics中写入数据，反之亦然

AEM Forms附加包还包含参考OData配置，您可以利用此配置快速将Microsoft Dynamics与AEM Forms集成。

安装包后，AEM Forms实例上提供以下实体和服务：

* MS Dynamics ODataCloud Service（OData服务）
* 使用预配置的Microsoft Dynamics实体和服务建立数据模型。

仅当AEM实例的运行模式设置为（默认）时，具有预配置的Microsoft Dynamics实体和服务的ODataCloud Service和表单模型才可在AEM Forms实例 `samplecontent`上使用。 有关为AEM实例配置运行模式的详细信息，请参阅 [运行模式](/help/sites-deploying/configure-runmodes.md)。

## 前提条件 {#prerequisites}

在开始设置和配置Microsoft Dynamics之前，请确保：

* 已安 [装AEM Forms加载项包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已在线配置Microsoft Dynamics 365，或已安装下列Microsoft Dynamics版本之一的实例：

   * Microsoft Dynamics 365内部部署
   * Microsoft Dynamics 2016内部部署

* [已在Microsoft Azure Active Directory中注册Microsoft Dynamics在线服务的应用程序](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。 记下注册服务的客户端ID(也称为应用程序 ID)和客户端机密的值。 这些值用于为 [您的Microsoft Dynamics服务配置云服务](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)。

## 为已注册的Microsoft Dynamics应用程序设置回复URL {#set-reply-url-for-registered-microsoft-dynamics-application}

请执行以下操作，为注册的Microsoft Dynamics应用程序设置回复URL:

>[!NOTE]
>
>仅在将AEM Forms与在线Microsoft Dynamics服务器集成时，才使用此过程。

1. 转到Microsoft Azure Active Directory帐户，在注册应用程序的“回复URL” **设置中添** 加以下云服务配置URL:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目录](assets/azure_directory_new.png)

1. 保存配置。

## 为IFD配置Microsoft Dynamics {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics使用基于声明的身份验证向外部用户提供对Microsoft Dynamics CRM服务器上数据的访问。 要启用此功能，请执行以下操作，为面向Internet的部署(IFD)配置Microsoft Dynamics，并配置声明设置。

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时使用此过程。

1. 按照为Microsoft Dynamics配置IFD中所述，为IFD配 [置Microsoft Dynamics本地实例](https://technet.microsoft.com/en-us/library/dn609803.aspx)。
1. 使用Windows PowerShell运行以下命令，在启用IFD的Microsoft Dynamics上配置声明设置：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   有关 [详细信息，请参阅CRM本地(IFD)的应用程序注](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) 册。

## 在AD FS计算机上配置OAuth客户端 {#configure-oauth-client-on-ad-fs-machine}

执行以下操作，在Active Directory Federation Services(AD FS)计算机上注册OAuth客户端并授予对AD FS计算机的访问权限：

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时使用此过程。

1. 运行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   其中：

   * `Client-ID` 是可使用任何GUID生成器生成的客户端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData云服务的URL。 随AEM Forms包一起安装的默认云服务将部署在以下URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 运行以下命令以授予对AD FS计算机的访问权限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   其中：

   * `resource` 是Microsoft Dynamics组织URL。

1. Microsoft Dynamics使用HTTPS协议。 要从Forms服务器调用AD FS端点，请使用运行AEM Forms的计算机上的命令将Microsoft Dynamics站点证 `keytool` 书安装到Java证书存储区。

## 为Microsoft Dynamics服务配置云服务 {#configure-cloud-service-for-your-microsoft-dynamics-service}

MS **Dynamics ODataCloud Service（OData服务）配置** ，默认的OData配置。 要将其配置为与Microsoft Dynamics服务连接，请执行以下操作。

1. 导航到 **[!UICONTROL 工具>Cloud Service>数据源]**，然后点按配 `global` 置文件夹。
1. 选 **择MS Dynamics ODataCloud Service（OData服务）配置** ，然后点按 **[!UICONTROL 属性]**。 将打开云服务配置属性对话框。

   在“身份验证 **设置** ”选项卡中：

   1. 输入“服务根” **字段的值** 。 转到Dynamics实例，并导航到 **Developer Resources** ，以视图“服务根”字段的值。 例如，https://&lt;tenant-name>/api/data/v9.1/

   1. 将客户端Id **(也称为**&#x200B;应用程序 ID **)、客户端Secret、OA OA UTH********************** REFRESH客户端访问令牌、、URL资源URL字段中的默认值替换为Microsoft Dynamics服务配置中的URL和资源URL值。 必须在“资源”字段中指定动态实 **例** URL，才能使用表单数据模型配置Microsoft Dynamics。 使用服务根URL派生动态实例URL。 例如， [https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在Microsoft **Dynamics** 的授 **权范围字** 段中指定openid，以进行授权过程。

   ![身份验证设置](assets/dynamics_authentication_settings_new.png)

1. 单击 **[!UICONTROL “连接到OAuth”]**。 您将被重定向到Microsoft Dynamics登录页面。
1. 使用Microsoft Dynamics凭据登录并接受，以允许云服务配置连接到Microsoft Dynamics服务。 在云服务与服务之间建立连接是一次性任务。

   然后，您将被重定向到云服务配置页，该页显示一条消息，显示OData配置已成功保存。

MS Dynamics ODataCloud Service（OData服务）云服务已配置并与Dynamics服务连接。

## Create form data model {#create-form-data-model}

安装AEM Forms包时，表单模型&#x200B;**Microsoft Dynamics FDM**，将部署在AEM实例上。 默认情况下，表单数据模型使用在MS Dynamics ODataCloud Service（OData服务）中配置的Microsoft Dynamics服务作为其数据源。

首次打开表单数据模型时，它将连接到已配置的Microsoft Dynamics服务，并从Microsoft Dynamics实例中获取实体。 Microsoft Dynamics的“联系人”和“潜在客户”实体已添加到表单数据模型中。

要查看表单数据模型，请转到“表 **[!UICONTROL 单”>“数据集成”]**。 选择 **Microsoft Dynamics FDM** ，然后单 **击“编辑** ”以在编辑模式下打开表单数据模型。 或者，您也可以直接从以下URL打开表单数据模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下来，您可以基于表单数据模型创建自适应表单并将其用于各种自适应表单用例，例如：

* 通过从Microsoft Dynamics实体和服务查询信息预填自适应表单
* 使用自适应表单规则调用在表单数据模型中定义的Microsoft Dynamics服务器操作
* 将提交的表单数据写入Microsoft Dynamics实体

建议创建随AEM Forms包提供的表单数据模型副本，并配置数据模型和服务以满足您的要求。 它将确保将来对包的任何更新不会覆盖表单数据模型。

有关在业务工作流中创建和使用表单数据模型的更多信息，请参 [阅数据集成](../../forms/using/data-integration.md)。
