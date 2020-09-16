---
title: 使用 Brand Portal 配置 AEM Assets
seo-title: 使用 Brand Portal 配置 AEM Assets
description: 了解如何使用Brand Portal配置AEM Assets，以将资产和集合发布到Brand Portal。
seo-description: 了解如何使用Brand Portal配置AEM Assets，以将资产和集合发布到Brand Portal。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 7c03ba5e2ec7954cca8b129f453919d151956df5
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 9%

---


# 使用 Brand Portal 配置 AEM Assets {#configure-integration-65}

Adobe Experience Manager资产品牌门户允许您将获准的品牌资产从Adobe Experience Manager资产发布到品牌门户，并将其分发给品牌门户用户。

AEM Assets通过Adobe开发者控制台配置了品牌门户，该控制台为品牌门户租户购买AdobeIdentity Management服务(IMS)帐户令牌。

>[!NOTE]
>
>在AEM 6.5.4.0及更高版本上支持通过Adobe开发人员控制台在AEM Assets中配置品牌门户。
>
>以前，品牌门户是通过旧版OAuth网关配置的，该网关使用JSON Web Token(JWT)交换获得IMS访问令牌进行授权。
>
>从2020年4月6日起，不再支持通过传统OAuth网关进行配置，现已更改为Adobe开发人员控制台。


>[!TIP]
>
>***仅限现有客户***
>
>建议继续使用现有的旧版OAuth网关配置。 如果您在旧版OAuth网关配置中遇到问题，请删除现有配置并通过Adobe开发人员控制台创建新配置。



本帮助描述以下两个用例：
* [新配置](#configure-new-integration-65):如果您是新的Brand Portal用户，并且希望使用Brand Portal配置您的AEM Assets作者实例，则可以通过Adobe开发人员控制台创建配置。
* [升级配置](#upgrade-integration-65):如果您是在旧版OAuth网关上进行配置的现有Brand Portal用户，请删除现有配置并通过Adobe开发人员控制台创建新配置。

提供的信息基于以下假设：阅读本帮助的任何人都熟悉以下技术：

* 安装、配置和管理Adobe Experience Manager和AEM包。

* 使用Linux和Microsoft Windows操作系统。

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 具有最新Service Pack的正在运行的AEM Assets作者实例
* 品牌门户租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户


[下载并安装AEM 6.5](#aemquickstart)

[下载并安装最新的AEM Service Pack](#servicepack)

### 下载并安装AEM 6.5 {#aemquickstart}

建议使AEM 6.5设置AEM作者实例。 如果您没有AEM并且正在运行，请从以下位置下载它：

* 如果您是现有的AEM客户，请从Adobe授权网站下 [载AEM 6.5](http://licensing.adobe.com)。

* 如果您是Adobe合作伙伴，请使 [用Adobe合作伙伴培](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 训项目来请求AEM 6.5。

下载AEM后，有关设置AEM作者实例的说明，请参阅部署 [和维护](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install)。

### 下载并安装AEM最新Service Pack {#servicepack}

有关详细说明，请参阅

* [AEM 6.5 Service Pack 发行说明](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**如果找不到** 最新的AEM包或服务包，请与支持部门联系。

## 创建配置 {#configure-new-integration-65}

使用Brand Portal配置AEM Assets需要在AEM Assets创作实例和Adobe开发者控制台中进行配置。

1. 在AEM Assets，创建IMS帐户并生成公共证书（公钥）。
1. 在Adobe开发人员控制台中，为您的Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户(JWT)连接。
1. 获取服务帐户凭据和JWT有效负荷信息。
1. 在AEM Assets，使用服务帐户凭据和JWT有效负荷配置IMS帐户。
1. 在AEM Assets，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资产从AEM Assets发布到Brand Portal来测试配置。


>[!NOTE]
>
>AEM Assets作者实例仅应配置一个Brand Portal租户。



如果您是首次使用Brand Portal配置AEM Assets，请在列出的序列中执行以下步骤：
1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-integration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置通过Brand Portal租户验证您的AEM Assets作者实例。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）在Adobe开发者控制台上验证您的用户档案。

1. 登录您的AEM Assets作者实例。 默认URL为 `http://localhost:4502/aem/start.html`。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. 在“AdobeIMS配置”页中，单击 **[!UICONTROL 创建]**。 It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.

1. 在“ **[!UICONTROL 云解决方案]** ”下拉 **[!UICONTROL 列表中选]** 择AdobeBrand Portal。

1. 选中“ **[!UICONTROL 创建新证书]** ”复选框，并指 **定公钥的** 别名。 别名用作公钥的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。Then, click **[!UICONTROL OK]** to generate the public key.

   ![创建证书](assets/ims-config2.png)

1. 单击“ **[!UICONTROL 下载公钥]** ”图标，并将公钥(.crt)文件保存到您的计算机上。

   公钥稍后将用于为您的Brand Portal租户配置API并在Adobe开发人员控制台中生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在“帐 **户** ”选项卡中，将创建AdobeIMS帐户，该帐户需要在Adobe开发者控制台中生成的服务帐户凭据。 暂时保持此页面打开。

   在Adobe开发者控 [制台中打开一个新选项卡并创建服务帐户(JWT)连接](#createnewintegration) ，以获取用于配置IMS帐户的凭据和JWT有效负荷。

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe开发人员控制台中，项目和API在Brand Portal租户（组织）级别进行配置。 配置API可创建服务帐户(JWT)连接。 可通过生成密钥对（私钥和公钥）或上传公钥来配置API的方法有两种。 要通过Brand Portal配置AEM Assets，您必须在AEM Assets生成公钥（证书），并通过上传公钥在Adobe开发者控制台中创建凭据。 在AEM Assets配置IMS帐户时需要这些凭据。 配置IMS帐户后，即可在AEM Assets配置Brand Portal云服务。

执行以下步骤以生成服务帐户凭据和JWT有效负荷：

1. 使用IMS组织（Brand Portal租户）的系统管理员权限登录Adobe开发人员控制台。 默认URL为 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)。


   >[!NOTE]
   >
   >确保您已从右上角的下拉（组织）列表中选择了正确的IMS组织（Brand Portal租户）。

1. Click **[!UICONTROL Create new project]**. 将为您的组织创建一个空白项目，其名称由系统生成。

   单击 **[!UICONTROL “编辑]** ”项目以更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 说明]**，然 **[!UICONTROL 后单击“]**&#x200B;保存”。

1. 在“项 **[!UICONTROL 目概述]** ”选项卡中， **[!UICONTROL 单击添加API]**。

1. 在“添 **[!UICONTROL 加API”窗口中]**，选 **[!UICONTROL 择AEM Brand Portal]** ，然后单 **[!UICONTROL 击“下一步]**”。

   确保您有权访问AEM Brand Portal服务。

1. 在“配 **[!UICONTROL 置API]** ”窗口中， **[!UICONTROL 单击“上传公钥”]**。 然后，单 **[!UICONTROL 击“Select a File]** （选择文件）”并上传您在“Obtain public certificate（获取公共证书）”部分下 [载的公钥(.crt](#public-certificate) 文件)。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公钥](assets/service-account3.png)

1. 验证公钥，然后单击“下 **[!UICONTROL 一步]**”。

1. 选择 **[!UICONTROL Assets Brand Portal]** 作为默认产品用户档案，然后单 **[!UICONTROL 击保存配置的API]**。

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![选择产品用户档案](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述页面。 在左侧导航的“凭 **[!UICONTROL 据]**”下，单 **[!UICONTROL 击“服务帐户(JWT)]** ”选项。

   >[!NOTE]
   >
   >您可以视图凭据并执行诸如生成JWT令牌、复制凭据详细信息、检索客户端机密等操作。

1. 从“客 **[!UICONTROL 户端凭据]** ”选项卡中，复 **[!UICONTROL 制客户端ID]**。

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![服务帐户凭据](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information.

您现在可以使用客户端ID（API密钥）、客户端机密和JWT负载 [配置AEM Assets的IMS帐户](#create-ims-account-configuration) 。

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### 配置IMS帐户 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建服务帐户(JWT)连接](#createnewintegration)

请执行以下步骤配置IMS帐户。

1. 打开IMS配置并导航到“帐 **[!UICONTROL 户]** ”选项卡。 您在获取公共证书时使 [页面保持打开状态](#public-certificate)。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在创建服务帐户( **[!UICONTROL JWT)连接时]** ，在您复制的API密钥字段 **[!UICONTROL 、客户端机密和]**&#x200B;有效负荷 **[!UICONTROL （JWT有效负荷）中]**[](#createnewintegration)指定客户端ID。

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   在对 **[!UICONTROL 话框]** 中单击“检查”。 成功配置时，将显示一条消息，告 *示标记已成功检索*。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它并创建新的有效配置。



### 配置云服务 {#configure-the-cloud-service}

请执行以下步骤来配置Brand Portal云服务：

1. 登录您的AEM Assets作者实例。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在Brand Portal的“配置”页中，单击“ **[!UICONTROL 创建]**”。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择配置IMS帐户时已 [创建的IMS配置](#create-ims-account-configuration)。

   在“服 **[!UICONTROL 务URL]** ”字段中，指定您的Brand Portal租户（组织）URL。

   ![](assets/create-cloud-service.png)

1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。

   您的AEM Assets创作实例现已配置Brand Portal租户。

### 测试配置{#test-integration}

请执行以下步骤以验证配置：

1. 登录您的AEM Assets云实例。

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. 在复制页面中，单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

   您可以看到为Brand Portal租户创建的四个复制代理。

   找到Brand Portal租户的复制代理，然后单击复制代理URL。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >复制代理并行工作并平等地共享作业分配，从而将发布速度提高四倍于原始速度。 配置云服务后，无需进行额外配置即可启用默认激活的复制代理以启用多个资产的并行发布。


1. To verify the connection between AEM Assets and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-integration4.png)

   将显示一条消息， *表明测试包已成功交付*。

   ![](assets/test-integration5.png)

1. 验证所有四个复制代理的测试结果。


   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能会导致资产复制（在队列中运行）失败。
   >
   >确保将所有四个复制代理都配置为避免超时错误。 See [troubleshoot issues in parallel publishing to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).

您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [将资产从Brand Portal发布到AEM Assets](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Brand Portal中的资产来源补充
* [将文件夹从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [将收藏集从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [将预设、架构和 Facet 发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/home.html) for more information.


## 升级配置 {#upgrade-integration-65}

按照所列顺序执行以下步骤，将现有配置升级到Adobe开发人员控制台：
1. [验证正在运行的作业](#verify-jobs)
1. [删除现有配置](#delete-existing-configuration)
1. [创建配置](#configure-new-integration-65)

### 验证正在运行的作业 {#verify-jobs}

在进行任何修改之前，请确保没有在您的AEM Assets作者实例上运行发布作业。 为此，您可以验证所有四个复制代理上的活动作业的状态，并确保队列处于空闲状态。

1. 登录您的AEM Assets作者实例。

1. 从“工 **具**![”面](assets/do-not-localize/tools.png) 板，导航至“部 **[!UICONTROL 署]** ”>“ ****&#x200B;部署复制”。

1. 在复制页面中，单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

1. 找到Brand Portal租户的复制代理。

   确保所有 **复制代理的队列** “空闲”，未激活任何发布作业。

   ![](assets/test-integration3.png)

### 删除现有配置 {#delete-existing-configuration}

删除现有配置时，必须运行以下核对清单：
* 删除所有四个复制代理
* 删除Brand Portal云服务
* 删除MAC用户

1. 登录您的AEM Assets创作实例，以管理员身份打开CRX Lite。 默认URL为 `http://localhost:4502/crx/de/index.jsp`。

1. 导航到 `/etc/replications/agents.author` 并删除Brand Portal租户的所有四个复制代理。

   ![](assets/delete-replication-agent.png)

1. 导航到 `/etc/cloudservices/mediaportal` 并删除Brand Portal云服务配置。

   ![](assets/delete-cloud-service.png)

1. 导航到 `/home/users/mac` 并删除您 **的Brand** Portal租户的MAC用户。

   ![](assets/delete-mac-user.png)


您现在可以 [通过AEM](#configure-new-integration-65) 6.5作者实例上的Adobe开发者控制台创建配置。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


