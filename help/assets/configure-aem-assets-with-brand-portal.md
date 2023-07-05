---
title: 使用 Brand Portal 配置 AEM Assets
seo-title: Configure AEM Assets with Brand Portal
description: 了解如何使用Brand Portal配置AEM Assets，以将资源和收藏集发布到Brand Portal。
seo-description: Learn how to configure AEM Assets with Brand Portal for publishing assets and Collections to Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
source-git-commit: 14988b55c21131391fdcb033373774ee170f5305
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 8%

---


# 使用 Brand Portal 配置 AEM Assets {#configure-integration-65}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

Adobe Experience Manager Assets Brand Portal允许您将已批准的品牌资产从Adobe Experience Manager Assets发布到Brand Portal，并将其分发给Brand Portal用户。

AEM Assets是通过Brand Portal控制台使用Adobe Developer配置的，该控制台可获取AdobeIdentity Management服务(IMS)帐户令牌以授权Brand Portal租户。

>[!NOTE]
>
>AEM 6.5.4.0及更高版本支持通过Adobe Developer控制台使用Brand Portal配置AEM Assets。
>
>以前，通过旧版OAuth网关配置Brand Portal，后者使用JSON Web令牌(JWT)交换获取IMS访问令牌进行授权。
>
>从2020年4月6日起，将不再支持通过旧版OAuth网关进行配置，并且已将配置更改为Adobe Developer控制台。

>[!TIP]
>
>***仅适用于现有客户***
>
>建议继续使用现有的旧版OAuth网关配置。 如果您遇到旧版OAuth网关配置问题，请删除现有配置，并通过Adobe Developer控制台创建新配置。

此帮助描述了以下两个用例：

* [新配置](#configure-new-integration-65)：如果您是新Brand Portal用户，并且希望使用Brand Portal配置AEM Assets创作实例，则可以通过Adobe Developer控制台创建配置。
* [升级配置](#upgrade-integration-65)：如果您是在旧版OAuth网关上进行配置的现有Brand Portal用户，请删除现有配置，并通过Adobe Developer控制台创建新配置。

所提供的信息基于这样一种假设，即任何阅读本“帮助”的人都熟悉以下技术：

* 安装、配置和管理Adobe Experience Manager和AEM软件包。

* 使用Linux和Microsoft Windows操作系统。

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 使用最新Service Pack启动并运行的AEM Assets创作实例
* Brand Portal租户URL
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户

[下载并安装AEM 6.5](#aemquickstart)

[下载并安装最新的AEM Service Pack](#servicepack)

### 下载并安装AEM 6.5 {#aemquickstart}

建议使用AEM 6.5来设置AEM创作实例。 如果您没有启动并运行AEM，请从以下位置下载它：

* 如果您是现有AEM客户，请从下载AEM 6.5 [Adobe授权网站](https://licensing.adobe.com).

* 如果您是Adobe合作伙伴，请使用 [Adobe合作伙伴培训计划](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) 以请求AEM 6.5。

下载AEM后，有关设置AEM创作实例的说明，请参阅 [部署和维护](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#default-local-install).

### 下载并安装AEM最新版Service Pack {#servicepack}

有关详细说明，请参阅

* [AEM 6.5 Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**联系支持人员** 如果您找不到最新的AEM包或Service Pack。

## 创建配置 {#configure-new-integration-65}

使用Brand Portal配置AEM Assets需要在AEM Assets创作实例和Adobe Developer控制台中进行配置。

1. 在AEM Assets中，创建IMS帐户并生成公共证书（公共密钥）。
1. 在Adobe Developer Console中，为您的Brand Portal租户（组织）创建一个项目。
1. 在项目下，使用公钥配置API以创建服务帐户(JWT)连接。
1. 获取服务帐户凭据和JWT有效负载信息。
1. 在AEM Assets中，使用服务帐户凭据和JWT有效负载配置IMS帐户。
1. 在AEM Assets中，使用IMS帐户和Brand Portal端点（组织URL）配置Brand Portal云服务。
1. 通过将资源从AEM Assets发布到Brand Portal来测试配置。

>[!NOTE]
>
>AEM Assets创作实例只能配置一个Brand Portal租户。

如果您是首次使用Brand Portal配置AEM Assets，请按照列出的顺序执行以下步骤：

1. [获取公共证书](#public-certificate)
1. [创建服务帐户(JWT)连接](#createnewintegration)
1. [配置IMS帐户](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-integration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS配置使用AEM Assets租户对您的Brand Portal创作实例进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）在Adobe Developer控制台上验证您的配置文件。

1. 登录到您的AEM Assets创作实例。 默认URL为 `http://localhost:4502/aem/start.html`.

1. 从 **工具** ![工具](assets/do-not-localize/tools.png) 面板，导航到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.

1. 在“Adobe IMS配置”页面中，单击 **[!UICONTROL 创建]**. 它将重定向到 **[!UICONTROL Adobe IMS技术帐户配置]** 页面。 默认情况下， **证书** 选项卡打开。

1. 选择 **[!UICONTROL AdobeBrand Portal]** 在 **[!UICONTROL 云解决方案]** 下拉列表。

1. 选择 **[!UICONTROL 创建新证书]** 复选框，并指定 **别名** 用于公钥。 别名用作公钥的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击 **[!UICONTROL 确定]** 以生成公钥。

   ![创建证书](assets/ims-config2.png)

1. 单击 **[!UICONTROL 下载公钥]** 图标并将公钥(.crt)文件保存到计算机上。

   公钥稍后将用于为您的Brand Portal租户配置API，并在Adobe Developer控制台中生成服务帐户凭据。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在 **帐户** 选项卡中创建的Adobe IMS帐户需要在Adobe Developer Console中生成的服务帐户凭据。 暂时保持此页面打开。

   打开新选项卡并 [在Adobe Developer控制台中创建服务帐户(JWT)连接](#createnewintegration) 获取用于配置IMS帐户的凭据和JWT有效负载。

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe Developer控制台中，项目和API是在Brand Portal租户（组织）级别配置的。 配置API会创建服务帐户(JWT)连接。 配置API的方法有两种：生成密钥对（私钥和公钥）或上传公钥。 要使用Brand Portal配置AEM Assets，您必须在AEM Assets中生成公钥（证书），并通过上传公钥在Adobe Developer控制台中创建凭据。 在AEM Assets中配置IMS帐户需要这些凭据。 配置IMS帐户后，您可以在AEM Assets中配置Brand Portal云服务。

执行以下步骤可生成服务帐户凭据和JWT有效负载：

1. 使用IMS组织(Adobe Developer租户)的系统管理员权限登录到Brand Portal控制台。 默认URL为 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >确保您从右上角的下拉（组织）列表中选择了正确的IMS组织(Brand Portal租户)。

1. 单击 **[!UICONTROL 创建新项目]**. 系统会为您的组织创建一个名称由系统生成的空白项目。

   单击 **[!UICONTROL 编辑项目]** 更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 描述]**，然后单击 **[!UICONTROL 保存]**.

1. 在 **[!UICONTROL 项目概述]** 选项卡，单击 **[!UICONTROL 添加API]**.

1. 在 **[!UICONTROL 添加API窗口]**，选择 **[!UICONTROL AEM Brand Portal]** 并单击 **[!UICONTROL 下一个]**.

   确保您有权访问AEM Brand Portal服务。

1. 在 **[!UICONTROL 配置API]** 窗口，单击 **[!UICONTROL 上传公钥]**. 然后，单击 **[!UICONTROL 选择文件]** 并上传您在中下载的公共密钥（.crt文件） [获取公共证书](#public-certificate) 部分。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![上传公钥](assets/service-account3.png)

1. 验证公钥并单击 **[!UICONTROL 下一个]**.

1. 选择 **[!UICONTROL Assets Brand Portal]** 作为默认产品配置文件，然后单击 **[!UICONTROL 保存配置的API]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![选择产品配置文件](assets/service-account4.png)

1. 配置API后，您将被重定向到API概述页面。 从左侧导航栏中的 **[!UICONTROL 凭据]**，单击 **[!UICONTROL 服务帐户(JWT)]** 选项。

   >[!NOTE]
   >
   >您可以查看凭据并执行操作，如生成JWT令牌、复制凭据详细信息、检索客户端密码等。

1. 从 **[!UICONTROL 客户端凭据]** 选项卡，复制 **[!UICONTROL 客户端ID]**.

   单击 **[!UICONTROL 检索客户端密码]** 并复制 **[!UICONTROL 客户端密码]**.

   ![服务帐户凭据](assets/service-account5.png)

1. 导航到 **[!UICONTROL 生成JWT]** 制表并复制 **[!UICONTROL JWT有效负荷]** 信息。

您现在可以将客户端ID（API密钥）、客户端密钥和JWT有效负载用于 [配置IMS帐户](#create-ims-account-configuration) 在AEM Assets中。

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

执行以下步骤来配置IMS帐户。

1. 打开IMS配置并导航到 **[!UICONTROL 帐户]** 选项卡。 您保持页面打开的时间 [获取公共证书](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授权服务器]** 字段中，指定URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在中指定客户端ID **[!UICONTROL API密钥]** 字段， **[!UICONTROL 客户端密码]**、和 **[!UICONTROL 有效负荷]** （JWT有效负荷）之前复制的时间 [创建服务帐户(JWT)连接](#createnewintegration).

   单击&#x200B;**[!UICONTROL 创建]**。

   已配置IMS帐户。

   ![IMS 帐户配置](assets/create-new-integration6.png)

1. 选择IMS帐户配置并单击 **[!UICONTROL 检查运行状况]**.

   单击 **[!UICONTROL Check]** 对话框中。 成功配置后，将显示一条消息，指出 *已成功检索令牌*.

   ![配置正常确认对话框](assets/create-new-integration5.png)

>[!CAUTION]
>
>您必须只有一个IMS配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则该配置无效。 您必须删除它并创建一个新的有效配置。

### 配置云服务 {#configure-the-cloud-service}

执行以下步骤来配置Brand Portal云服务：

1. 登录到您的AEM Assets创作实例。

1. 从 **工具** ![工具](assets/do-not-localize/tools.png) 面板，导航到 **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. 在“Brand Portal配置”页面中，单击 **[!UICONTROL 创建]**.

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择您已在以下时间创建的IMS配置： [配置IMS帐户](#create-ims-account-configuration).

   在 **[!UICONTROL 服务URL]** 字段中，指定您的Brand Portal租户（组织）URL。

   ![“Brand Portal配置”窗口](assets/create-cloud-service.png)

1. 单击“**[!UICONTROL 保存并关闭]**”。将创建云配置。

   您的AEM Assets创作实例现在已配置有Brand Portal租户。

### 测试配置 {#test-integration}

执行以下步骤来验证配置：

1. 登录到您的AEM Assets云实例。

1. 从 **工具** ![工具](assets/do-not-localize/tools.png) 面板，导航到 **[!UICONTROL 部署]** > **[!UICONTROL 复制]**.

   ![“工具”面板](assets/test-integration1.png)

1. 在“复制”页中，单击 **[!UICONTROL 作者代理]**.

   ![复制页面](assets/test-integration2.png)

   您可以看到为您的Brand Portal租户创建的四个复制代理。

   找到Brand Portal租户的复制代理，然后单击复制代理URL。

   ![资产复制配置](assets/test-integration3.png)

   >[!NOTE]
   >
   >复制代理并行工作，并均匀地共享作业分发，从而将发布速度提高到原始速度的四倍。 配置云服务后，无需进行其他配置即可启用复制代理，默认情况下，激活复制代理可启用多个资产的并行发布。

1. 要验证AEM Assets与Brand Portal之间的连接，请单击 **[!UICONTROL 测试连接]** 图标。

   ![验证资产复制设置](assets/test-integration4.png)

   此时将显示一条消息，表明 *测试包已成功交付*.

   ![测试确认输出](assets/test-integration5.png)

1. 验证所有四个复制代理的测试结果。


   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能会导致资产（在队列中运行）复制失败。
   >
   >请确保所有四个复制代理均已配置为避免出现超时错误。 参见 [对并行发布到Brand Portal时出现的问题进行故障诊断](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).
   >
   >请勿修改任何自动生成的设置。

您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [将资源从Brand Portal发布到AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hans) - Brand Portal中的资源源
* [将文件夹从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [将收藏集从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [将预设、架构和 Facet 发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [将标记发布到 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

参见 [Brand Portal文档](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 了解更多信息。


## 升级配置 {#upgrade-integration-65}

按照列出的顺序执行以下步骤，将现有配置升级到Adobe Developer Console：

1. [验证正在运行的作业](#verify-jobs)
1. [删除现有配置](#delete-existing-configuration)
1. [创建配置](#configure-new-integration-65)

### 验证正在运行的作业 {#verify-jobs}

在进行任何修改之前，请确保您的AEM Assets创作实例上未运行任何发布作业。 为此，您可以验证所有四个复制代理上活动作业的状态，并确保队列处于空闲状态。

1. 登录到您的AEM Assets创作实例。

1. 从 **工具** ![工具](assets/do-not-localize/tools.png) 面板，导航到 **[!UICONTROL 部署]** > **[!UICONTROL 部署复制]**.

1. 在“复制”页中，单击 **[!UICONTROL 作者代理]**.

   ![资产复制代理](assets/test-integration2.png)

1. 找到Brand Portal租户的复制代理。

   确保 **队列空闲** 对于所有复制代理，没有处于活动状态的发布作业。

   ![复制队列设置](assets/test-integration3.png)

### 删除现有配置 {#delete-existing-configuration}

删除现有配置时，必须运行以下核对清单：
* 删除全部四个复制代理
* 删除Brand Portal云服务
* 删除MAC用户

1. 登录到您的AEM Assets创作实例，并以管理员身份打开CRX Lite。 默认URL为 `http://localhost:4502/crx/de/index.jsp`.

1. 导航到 `/etc/replications/agents.author` 并删除Brand Portal租户的所有四个复制代理。

   ![CRXDE中的复制代理](assets/delete-replication-agent.png)

1. 导航到 `/etc/cloudservices/mediaportal` 并删除Brand Portal云服务配置。

   ![CRXDE中复制代理的详细信息](assets/delete-cloud-service.png)

1. 导航到 `/home/users/mac` 并删除 **Mac用户** 您的Brand Portal租户的。

   ![CRXDE中复制代理的更多详细信息](assets/delete-mac-user.png)


您现在可以 [创建配置](#configure-new-integration-65) 通过AEM 6.5创作实例上的Adobe Developer控制台。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
