---
title: 使用 Brand Portal 配置 AEM Assets
seo-title: 使用 Brand Portal 配置 AEM Assets
description: 了解如何通过Brand Portal配置AEM资产，以将资产和集合发布到Brand Portal。
seo-description: 了解如何通过Brand Portal配置AEM资产，以将资产和集合发布到Brand Portal。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: fb59bd52be86894e93063f4b7c32aef0ed23250b
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 43%

---


# 使用 Brand Portal 配置 AEM Assets {#configure-integration-65}

Adobe Experience Manager (AEM) Assets 通过 Adobe I/O 使用 Brand Portal 进行了配置，从而可获取 IMS 令牌以授权您的 Brand Portal 租户。

>[!NOTE]
>
>AEM 6.5.4.0及更高版本支持通过Adobe I/O在品牌门户中配置AEM资产。
>
>以前，品牌门户通过旧版OAuth网关在经典UI中配置，该网关使用JWT令牌交换获得IMS访问令牌进行授权。
>
>从2020年4月6日起，不再支持通过旧版OAuth进行配置，现已更改为通过Adobe I/O进行配置。


>[!TIP]
>
>***仅限现有客户***
>
>建议继续使用现有的旧版OAuth网关配置。 如果您在旧版OAuth网关配置中遇到问题，请删除现有配置并通过Adobe I/O创建新配置。



本帮助描述以下两个用例：
* [新配置](#configure-new-integration-65): 如果您是新的Brand Portal用户，并且希望在Brand Portal中配置AEM资产作者实例，则可以在Adobe I/O上创建新配置。
* [升级配置](#upgrade-integration-65): 如果您是现有Brand Portal用户，且AEM Assets作者实例在旧版OAuth Gateway上配置了Brand Portal，建议您删除现有配置并在Adobe I/O上创建新配置。

提供的信息基于以下假设：阅读本帮助的任何人都熟悉以下技术：

* 安装、配置和管理Adobe Experience Manager和AEM包

* 使用Linux和Microsoft Windows操作系统

## 前提条件 {#prerequisites}

您需要以下各项才能使用 Brand Portal 配置 AEM Assets：

* 具有最新Service Pack的正在运行的AEM Assets作者实例。
* Brand Portal 租户 URL。
* 对 Brand Portal 租户的 IMS 组织具有系统管理员权限的用户。


[下载并安装AEM 6.5](#aemquickstart)

[下载并安装最新的AEM Service Pack](#servicepack)

### 下载并安装AEM 6.5 {#aemquickstart}

建议让AEM 6.5设置AEM作者实例。 如果您尚未启动并运行AEM，请从以下位置下载它：

* 如果您是现有AEM客户，请从Adobe授权许可网站下 [载AEM 6.5](http://licensing.adobe.com)。

* 如果您是Adobe合作伙伴，请使 [用Adobe合作伙伴培训项目](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) ，请求AEM 6.5。

下载AEM后，有关设置AEM作者实例的说明，请参阅部 [署和维护](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)。

### 下载并安装AEM最新Service Pack {#servicepack}

有关详细说明，请参阅

* [AEM 6.5 Service Pack 发行说明](https://helpx.adobe.com/cn/experience-manager/6-5/release-notes/sp-release-notes.html)

**如果找不到** 最新的AEM包或服务包，请与客户服务部门联系。

## 创建配置 {#configure-new-integration-65}

如果您是首次使用Brand Portal配置AEM资产，请在列出的序列中执行以下步骤：
1. [获取公共证书](#public-certificate)
1. [创建 Adobe I/O 集成](#createnewintegration)
1. [创建 IMS 帐户配置](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-integration)

### 创建 IMS 配置 {#create-ims-configuration}

IMS 配置通过 AEM Assets 作者实例对您的 Brand Portal 租户进行身份验证。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [创建 IMS 帐户配置](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公共证书允许您在 Adobe I/O 上验证配置文件。

1. 登录AEM资产作者实例默认URL: http://本地主机：4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** >> **[!UICONTROL Adobe IMS Configurations]**.

   ![Adobe IMS 帐户配置 UI](assets/ims-config1.png)

1. 打开 Adobe IMS 配置页面。

   单击&#x200B;**[!UICONTROL 创建]**。

   这会将您转到 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。

1. 默认情况下，将打开&#x200B;**证书**&#x200B;选项卡。

   在&#x200B;**云解决方案**&#x200B;中，选择 **[!UICONTROL Adobe Brand Portal]**。

1. 标记&#x200B;**[!UICONTROL 创建新证书]**&#x200B;复选框，并指定证书的&#x200B;**别名**。别名将用作对话框的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。将显示一个对话框。单击&#x200B;**[!UICONTROL 确定]**&#x200B;以生成公共证书。

   ![创建证书](assets/ims-config2.png)

1. 单击&#x200B;**[!UICONTROL 下载公钥]**，然后将 *AEM-Adobe-IMS.crt* 证书文件保存到您的计算机上。该证书文件将用于[创建 Adobe I/O 集成](#createnewintegration)。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在&#x200B;**帐户**&#x200B;选项卡中，您可以创建 Adobe IMS 帐户，但您需要集成详细信息。暂时保持此页面打开。

   打开新选项卡并[创建 Adobe I/O 集成](#createnewintegration)，以获取 IMS 帐户配置的集成详细信息。

### 创建 Adobe I/O 集成 {#createnewintegration}

Adobe I/O 集成可生成 API 密钥、客户端密钥和有效负荷 (JWT)，这是设置 IMS 帐户配置所必需的。

1. 使用 Brand Portal 租户的 IMS 组织的系统管理员权限登录到 Adobe I/O 控制台。

   默认 URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 单击&#x200B;**[!UICONTROL 创建集成]**。

1. 选择&#x200B;**[!UICONTROL 访问 API]**，然后单击&#x200B;**[!UICONTROL 继续]**。

   ![创建新集成](assets/create-new-integration1.png)

1. 此时将打开新的集成页面。

   从下拉列表中选择您的组织。

   在 **[!UICONTROL Experience Cloud]** 中，选择 **[!UICONTROL AEM Brand Portal]**，然后单击&#x200B;**[!UICONTROL 继续]**。

   如果您禁用了 Brand Portal 选项，请确保您从 **[!UICONTROL Adobe Services]** 选项上方的下拉框中选择了正确的组织。如果您不了解您的组织，请与管理员联系。

   ![创建集成](assets/create-new-integration2.png)

1. 指定集成的名称和描述。单击&#x200B;**[!UICONTROL 从计算机中选择文件]**，然后上传在[获取公共证书](#public-certificate)部分下载的 `AEM-Adobe-IMS.crt` 文件。

1. 选择您的组织的配置文件。

   或者，选择默认的配置文件 **[!UICONTROL Brand Portal]**，然后单击&#x200B;**[!UICONTROL 创建集成]**。将创建集成。

1. 单击&#x200B;**[!UICONTROL 继续查看集成详细信息]**，以查看集成信息。

   复制 **[!UICONTROL API 密钥]**

   单击&#x200B;**[!UICONTROL 检索客户端密钥]**，并复制客户端密钥。

   ![集成的 API 密钥、客户端密钥和有效负荷信息](assets/create-new-integration3.png)

1. 导航到 **[!UICONTROL JWT]** 选项卡，并复制 **[!UICONTROL JWT 有效负荷]**。

   API 密钥、客户端密钥和 JWT 有效负荷信息将用于创建 IMS 帐户配置。

### 创建 IMS 帐户配置 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建 Adobe I/O 集成](#createnewintegration)

**创建 IMS 帐户配置的步骤：**

1. 打开“IMS 配置”页面的&#x200B;**[!UICONTROL 帐户]**&#x200B;选项卡。保持打开该页面[获取公共证书](#public-certificate)的结尾部分。

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在&#x200B;**[!UICONTROL 授权服务器]**&#x200B;中，输入 URL：[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   粘贴您在[创建 Adobe I/O 集成](#createnewintegration)结束时复制的 API 密钥、客户端密钥和 JWT 有效负荷。

   单击&#x200B;**[!UICONTROL 创建]**。

   将创建集成。

   ![IMS 帐户配置](assets/create-new-integration6.png)


1. 选择 IMS 配置，然后单击&#x200B;**[!UICONTROL 检查运行状况]**。将显示一个对话框。

   单击&#x200B;**[!UICONTROL 检查]**。成功连接时，将显示&#x200B;*已成功检索令牌*&#x200B;消息。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一个IMS配置。 请勿创建多个 IMS 配置。
>
>确保IMS配置通过运行状况检查。 如果配置未通过运行状况检查，则无效。 您必须删除它并创建新的有效配置。


### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以创建 Brand Portal 云服务配置：

1. 登录AEM Assets作者实例

   默认URL: http://本地主机：4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services >> AEM Brand Portal]**.

   此时将打开 Brand Portal 的“配置”页面。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配置的&#x200B;**[!UICONTROL 标题]**。

   选择您在[创建 IMS 帐户配置](#create-ims-account-configuration)步骤中创建的“IMS 配置”。

   在&#x200B;**[!UICONTROL 服务 URL]** 中，输入您的 Brand Portal 租户 URL。

   ![](assets/create-cloud-service.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。将创建云配置。您的AEM资产作者实例现已与Brand Portal租户集成。

### 测试配置{#test-integration}

1. 登录AEM Assets作者实例

   默认URL: http://本地主机：4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

   ![](assets/test-integration1.png)

1. 复制页面打开。

   单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

1. 为每个租户创建四个复制代理。

   找到Brand Portal租户的复制代理。

   单击复制代理URL。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >复制代理并行工作并平等地共享作业分配，从而将发布速度提高四倍于原始速度。 配置云服务后，无需进行额外配置即可启用默认激活的复制代理以启用多个资产的并行发布。

   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能会导致某些资产的复制失败。


1. To verify the connection between AEM Assets author and Brand Portal, click **[!UICONTROL Test Connection]**.

   ![](assets/test-integration4.png)

1. 查看测试结果的底部，验证复制是否成功。

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >复制代理并行工作并平等地共享作业分配，从而将发布速度提高四倍于原始速度。 配置云服务后，无需进行额外配置即可启用默认激活的复制代理以启用多个资产的并行发布。

1. 逐一验证所有四个复制代理的测试结果。


   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能会导致某些资产的复制失败。

Brand Portal已成功配置AEM资产作者实例。 您现在可以：

* [将资产从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [将文件夹从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [将收藏集从 AEM Assets 发布到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [配置资产来源](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) ，使Brand Portal用户能够将资产贡献和发布到AEM资产。

## 升级配置 {#upgrade-integration-65}

按照列出的顺序执行以下步骤以升级现有配置：
1. [验证正在运行的作业](#verify-jobs)
1. [删除现有配置](#delete-existing-configuration)
1. [创建配置](#configure-new-integration-65)

### 验证正在运行的作业 {#verify-jobs}

在进行任何修改之前，请确保AEM资产作者实例上未运行发布作业。 对于此，您可以验证所有四个复制代理，并确保队列是理想／空的。

1. 登录AEM Assets作者实例

   默认URL: http://本地主机：4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

1. 复制页面打开。

   单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

1. 找到Brand Portal租户的复制代理。

   确保所有 **复制代理的队列** “空闲”，没有发布作业处于活动状态。

   ![](assets/test-integration3.png)

### 删除现有配置 {#delete-existing-configuration}

删除现有配置时，必须运行以下检查列表。
* 删除所有四个复制代理
* 删除云服务
* 删除MAC用户

1. 登录AEM Assets作者实例，以管理员身份打开CRX Lite。

   默认URL: http://本地主机：4502/crx/de/index.jsp

1. 导航到 `/etc/replications/agents.author` 并删除Brand Portal租户的所有四个复制代理。

   ![](assets/delete-replication-agent.png)

1. 导航到 `/etc/cloudservices/mediaportal` 并删除云 **服务配置**。

   ![](assets/delete-cloud-service.png)

1. 导航到 `/home/users/mac` 并删除您 **的Brand** Portal租户的MAC用户。

   ![](assets/delete-mac-user.png)


您现在可 [以在Adobe](#configure-new-integration-65) I/O上的AEM 6.5创作实例上创建配置。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

复制成功后，您可以将资产、文件夹和集合发布到Brand Portal。 有关详细信息，请参阅：

* [将资产发布到 Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [将文件夹发布到 Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [将集合发布到品牌门户](/help/assets/brand-portal-publish-collection.md)
