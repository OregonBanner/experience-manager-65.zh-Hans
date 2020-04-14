---
title: 使用Brand Portal配置AEM资产
seo-title: 使用Brand Portal配置AEM资产
description: 了解如何配置带有Brand Portal的AEM资产，以将资产和集合发布到Brand Portal。
seo-description: 了解如何配置带有Brand Portal的AEM资产，以将资产和集合发布到Brand Portal。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 28354bd9785fa83939f9e3b051aac195d7706633

---


# 使用Brand Portal配置AEM资产 {#configure-integration-65}

Adobe Experience Manager(AEM)资产通过Adobe I/O配置了Brand Portal,Adobe I/O可获取IMS令牌以授权您的Brand Portal租户。

>[!NOTE]
>
>AEM 6.5.4.0及更高版本支持通过Adobe I/O在Brand Portal中配置AEM资产。
>
>以前，Brand Portal是通过旧版OAuth网关在经典UI中配置的，该网关使用JWT令牌交换获得IMS访问令牌进行授权。
>
>从2020年4月6日起，不再支持通过旧版OAuth进行配置，并已更改为通过Adobe I/O进行配置。


>[!TIP]
>
>***仅适用于现有客户***
>
>建议继续使用现有的传统OAuth网关配置。 如果您遇到旧版OAuth网关配置问题，请删除现有配置并通过Adobe I/O创建新配置。



本帮助描述了以下两个用例：
* [新配置](#configure-new-integration-65):如果您是新的Brand Portal用户，并且希望使用Brand Portal配置AEM Assets作者实例，则可以在Adobe I/O上创建新配置。
* [升级配置](#upgrade-integration-65):如果您是现有Brand Portal用户，且AEM Assets作者实例在旧版OAuth网关上配置了Brand Portal，则建议删除现有配置并在Adobe I/O上创建新配置。

提供的信息基于以下假设：阅读本帮助的任何人都熟悉以下技术：

* 安装、配置和管理Adobe Experience Manager和AEM包

* 使用Linux和Microsoft Windows操作系统

## 前提条件 {#prerequisites}

您需要以下各项才能在Brand Portal中配置AEM资产：

* 具有最新Service Pack的AEM Assets作者实例正在运行。
* Brand Portal租户URL。
* 对Brand Portal租户的IMS组织具有系统管理员权限的用户。


[下载并安装AEM 6.5](#aemquickstart)

[下载并安装最新的AEM Service Pack](#servicepack)

### 下载并安装AEM 6.5 {#aemquickstart}

建议让AEM 6.5设置AEM作者实例。 如果尚未启动并运行AEM，请从以下位置下载它：

* 如果您是现有AEM客户，请从 [Adobe授权许可网站下载AEM 6.5](http://licensing.adobe.com)。

* 如果您是Adobe合作伙伴，请使用 [Adobe合作伙伴培训项目](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) ，请求AEM 6.5。

下载AEM后，有关设置AEM作者实例的说明，请参阅部署 [和维护](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)。

### 下载和安装AEM最新Service Pack {#servicepack}

有关详细说明，请参阅

* [AEM 6.5 Service Pack 发行说明](https://helpx.adobe.com/cn/experience-manager/6-5/release-notes/sp-release-notes.html)

**如果找不到最新的AEM包或Service Pack，请与支持部门联系。**

## Create configuration {#configure-new-integration-65}

如果您是首次将AEM资产与Brand Portal一起配置，请在列出的序列中执行以下步骤：
1. [获取公共证书](#public-certificate)
1. [创建Adobe I/O集成](#createnewintegration)
1. [创建IMS帐户配置](#create-ims-account-configuration)
1. [配置云服务](#configure-the-cloud-service)
1. [测试配置](#test-integration)

### 创建IMS配置 {#create-ims-configuration}

IMS配置使用AEM Assets作者实例验证您的Brand Portal租户。

IMS配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [创建IMS帐户配置](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公共证书允许您在Adobe I/O上验证用户档案。

1. 登录AEM资产作者实例默认URL:http://本地主机：4502/aem/start.html
1. 从“工 **具**![”面板中，导航至“安全](assets/tools.png) ” **[!UICONTROL >]** >“ **** Adobe IMS配置”。

   ![Adobe IMS帐户配置UI](assets/ims-config1.png)

1. Adobe IMS配置页面打开。

   单击&#x200B;**[!UICONTROL 创建]**。

   此操作将转到 **[!UICONTROL Adobe IMS技术帐户配置页]** 。

1. 默认情况下，“证 **书** ”选项卡打开。

   在 **Cloud Solution**，选择 **[!UICONTROL Adobe Brand Portal]**。

1. 标记复选 **[!UICONTROL 框创建新证书]** ，并指定证 **书的别名** 。 别名用作对话框的名称。

1. 单击“ **[!UICONTROL 创建证书]**”。 将显示一个对话框。 单击 **[!UICONTROL 确定]** ，以生成公共证书。

   ![创建证书](assets/ims-config2.png)

1. 单 **[!UICONTROL 击“下载公钥]** ”，然后将 ** AEM-Adobe-IMS.crt证书文件保存到您的计算机上。 证书文件用于创 [建Adobe I/O集成](#createnewintegration)。

   ![下载证书](assets/ims-config3.png)

1. 单击&#x200B;**[!UICONTROL 下一步]**。

   在“帐 **户** ”选项卡中，您创建Adobe IMS帐户，但为此您需要集成详细信息。 此页面暂时打开。

   打开新选项卡并 [创建Adobe I/O集成](#createnewintegration) ，获取IMS帐户配置的集成详细信息。

### 创建Adobe I/O集成 {#createnewintegration}

Adobe I/O集成生成API密钥、客户端机密和有效负荷(JWT)，这是设置IMS帐户配置所必需的。

1. 使用Brand Portal租户的IMS组织的系统管理员权限登录到Adobe I/O控制台。

   默认URL: [https://console.adobe.io/](https://console.adobe.io/)

1. 单击“ **[!UICONTROL 创建集成]**”。

1. 选择 **[!UICONTROL 访问API]**，然后单击 **[!UICONTROL 继续]**。

   ![创建新集成](assets/create-new-integration1.png)

1. 此时将打开新的集成页面。

   从下拉列表中选择您的组织。

   在 **[!UICONTROL Experience Cloud中]**，选择 **[!UICONTROL AEM Brand Portal]** ，然后单击 **[!UICONTROL 继续]**。

   如果您禁用了“品牌门户”选项，请确保您从 **[!UICONTROL Adobe Services选项上方的下拉框中选择了正确的组织]** 。 如果您不了解您的组织，请与管理员联系。

   ![创建集成](assets/create-new-integration2.png)

1. 指定集成的名称和说明。 单击 **[!UICONTROL 从计算机中选择文件]** ，然后上传在“获取公 `AEM-Adobe-IMS.crt` 共证书”部分下 [载的文件](#public-certificate) 。

1. 选择您的组织的用户档案。

   或者，选择默认的用户档案资 **[!UICONTROL 产Brand Portal]** ，然后单 **[!UICONTROL 击创建集成]**。 将创建集成。

1. 单击 **[!UICONTROL 继续以视图集成详细信息]** ，以便集成信息。

   复制 **[!UICONTROL API密钥]**

   单击 **[!UICONTROL “检索客户端机密]** ”并复制客户端机密密钥。

   ![集成的API密钥、客户端机密和有效负荷信息](assets/create-new-integration3.png)

1. 导航到 **[!UICONTROL JWT]** 选项卡，并复制 **[!UICONTROL JWT有效负荷]**。

   API密钥、客户端密钥和JWT有效负荷信息将用于创建IMS帐户配置。

### 创建IMS帐户配置 {#create-ims-account-configuration}

确保您已执行以下步骤：

* [获取公共证书](#public-certificate)
* [创建Adobe I/O集成](#createnewintegration)

**创建IMS帐户配置的步骤：**

1. 打开“IMS配置”页的“帐 **[!UICONTROL 户]** ”选项卡。 您在“获取公共证书”部分的结尾处保持 [该页面打开](#public-certificate)。

1. 为IMS **[!UICONTROL 帐户指定]** “标题”。

   在授 **[!UICONTROL 权服务器]**，输入URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   粘贴您在创建Adobe I/O集成结束时复制的API密钥、客户端机密和 [JWT有效负荷](#createnewintegration)。

   单击&#x200B;**[!UICONTROL 创建]**。

   将创建集成。

   ![IMS帐户配置](assets/create-new-integration6.png)


1. 选择IMS配置，然后单击“检 **[!UICONTROL 查运行状况”]**。 将显示一个对话框。

   单击 **[!UICONTROL 检查]**。 成功连接时，将显示 *已成功检索的令牌* 消息。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>仅创建一个有效的IMS配置。
>
> 确保配置正常。 如果配置不健康，请删除该配置并创建一个新的健康配置。


### 配置云服务 {#configure-the-cloud-service}

执行以下步骤以创建Brand Portal云服务配置：

1. 登录AEM Assets作者实例

   默认URL:http://本地主机：4502/aem/start.html
1. 从工 **具** 面板 ![，导航至](assets/tools.png) 云服务>> AEM Brand Portal ****。

   Brand Portal配置页面打开。

1. 单击&#x200B;**[!UICONTROL 创建]**。

1. 指定配 **[!UICONTROL 置的]** “标题”。

   选择您在步骤中创建的IMS配置，创建 [IMS帐户配置](#create-ims-account-configuration)。

   在服 **[!UICONTROL 务URL中]**，输入您的Brand Portal租户URL。

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. 云配置已创建。 您的AEM资产作者实例现在已与Brand Portal租户集成。

### Test configuration {#test-integration}

1. 登录AEM Assets作者实例

   默认URL:http://本地主机：4502/aem/start.html

1. 从“工 **具**![”面板中，导](assets/tools.png) 航到“部署”>>“复制 ****”。

   ![](assets/test-integration1.png)

1. 复制页面打开。

   单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

1. 为每个租户创建四个复制代理。

   找到您的Brand Portal租户的复制代理。

   单击复制代理URL。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >复制代理并行工作并平等地共享作业分配，从而将发布速度提高了四倍于原始速度。 配置云服务后，无需进行其他配置即可启用复制代理，默认情况下激活复制代理可启用多个资产的并行发布。

   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能导致某些资产的复制失败。


1. 要验证AEM Assets作者与Brand Portal之间的连接，请单击“测 **[!UICONTROL 试连接”]**。

   ![](assets/test-integration4.png)

1. 查看测试结果的底部以验证复制是否成功。

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >复制代理并行工作并平等地共享作业分配，从而将发布速度提高了四倍于原始速度。 配置云服务后，无需进行其他配置即可启用复制代理，默认情况下激活复制代理可启用多个资产的并行发布。

1. 对所有四个复制代理逐一验证测试结果。


   >[!NOTE]
   >
   >请避免禁用任何复制代理，因为这可能导致某些资产的复制失败。

Brand Portal已成功配置AEM Assets作者实例。 您现在可以：

* [将资产从AEM资产发布到Brand Portal](../assets/brand-portal-publish-assets.md)
* [将文件夹从AEM资产发布到Brand Portal](../assets/brand-portal-publish-folder.md)
* [将集合从AEM资产发布到Brand Portal](../assets/brand-portal-publish-collection.md)
* [配置资产来源补充](https://docs.adobe.com/content/help/zh-Hans/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) ，使Brand Portal用户能够将资产贡献和发布到AEM资产。

## 升级配置 {#upgrade-integration-65}

按照所列顺序执行以下步骤以升级现有配置：
1. [验证正在运行的作业](#verify-jobs)
1. [删除现有配置](#delete-existing-configuration)
1. [创建配置](#configure-new-integration-65)

### 验证正在运行的作业 {#verify-jobs}

在进行任何修改之前，请确保AEM资产作者实例上未运行发布作业。 对于这一点，您可以验证所有四个复制代理，并确保队列是理想／空的。

1. 登录AEM Assets作者实例

   默认URL:http://本地主机：4502/aem/start.html

1. 从“工 **具**![”面板中，导](assets/tools.png) 航到“部署”>>“复制 ****”。

1. 复制页面打开。

   单击作 **[!UICONTROL 者上的代理]**。

   ![](assets/test-integration2.png)

1. 找到您的Brand Portal租户的复制代理。

   确保所有复 **制代理的队列都处于空闲状态** ，任何发布作业都不处于活动状态。

   ![](assets/test-integration3.png)

### 删除现有配置 {#delete-existing-configuration}

删除现有配置时，必须运行以下检查列表。
* 删除所有四个复制代理
* 删除云服务
* 删除MAC用户

1. 登录AEM Assets作者实例，以管理员身份打开CRX Lite。

   默认URL:http://本地主机：4502/crx/de/index.jsp

1. 导航到 `/etc/replications/agents.author` 并删除Brand Portal租户的所有四个复制代理。

   ![](assets/delete-replication-agent.png)

1. 导航到 `/etc/cloudservices/mediaportal` 并删除云 **服务配置**。

   ![](assets/delete-cloud-service.png)

1. 导航到 `/home/users/mac` 并删除您的 **Brand Portal租户的MAC用户** 。

   ![](assets/delete-mac-user.png)


您现在可 [以在Adobe I/O上的AEM 6](#configure-new-integration-65) .5创作实例上创建配置。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

复制成功后，您可以将资产、文件夹和集合发布到Brand Portal。 有关详细信息，请参阅：

* [将资产发布到Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [将文件夹发布到Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [将集合发布到Brand Portal](/help/assets/brand-portal-publish-collection.md)
