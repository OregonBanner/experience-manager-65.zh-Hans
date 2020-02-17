---
title: 配置AEM资产与Experience cloud和Creative cloud的集成
seo-title: 配置AEM资产与Marketing cloud和Creative cloud的集成
description: 了解如何配置AEM资产与Experience cloud和Creative cloud的集成。
seo-description: 了解如何配置AEM资产与Experience cloud和Creative cloud的集成。
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: c62a7f12ea6a988cee597516d2f73d15c3802c62

---


# 配置AEM资产与Experience cloud和Creative cloud的集成 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience cloud客户，则可以将Adobe Experience Manager(AEM)资产中的资产与Adobe Creative cloud同步，反之亦然。 您还可以将资产与Experience cloud同步，反之亦然。 您可以通过Adobe I/O设置此同步。

设置此集成的工作流是：

1. 在Adobe I/O中使用公共网关创建身份验证并获取应用程序ID。
1. 使用应用程序ID在AEM资产实例上创建配置文件。
1. 使用此配置可将AEM资产中的资产与Creative cloud同步。

在后端，AEM服务器使用网关验证您的配置文件，然后在AEM资产和Experience cloud之间同步数据。

>[!CAUTION]
>
>AEM到Creative cloud文件夹共享功能在AEM资产中已弃用。 了解更多信息并查找 [AEM和Creative Cloud集成最佳实践中的替代内容](/help/assets/aem-cc-integration-best-practices.md)。

![集成AEM资产和Creative cloud时的数据流](assets/chlimage_1-48.png)

集成AEM资产和Creative cloud时的数据流

>[!NOTE]
>
>在Adobe Experience cloud和Adobe Creative cloud之间共享资产需要AEM实例的管理员权限。

>[!CAUTION]
>
>Adobe Marketing cloud已重新命名为Adobe Experience Cloud。 下面的步骤仍然提到Marketing Cloud，以反映当前的界面。 这些提及将在以后的日期进行更改。

## 创建应用程序 {#create-an-application}

1. 通过登录https://legacy-oauth.cloud.adobe.io访问Adobe开发人员网关 [界面](https://legacy-oauth.cloud.adobe.io/)。

   >[!NOTE]
   >
   >您需要管理员权限才能创建应用程序ID。

1. 从左侧窗格，导航到“开发人 **[!UICONTROL 员工具]** ”>“ **[!UICONTROL 应用程序]** ”以查看应用程序列表。
1. 单 **[!UICONTROL 击添]** 加 ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 以创建应用程序。
1. 从“客 **[!UICONTROL 户端凭据]** ”列表中，选择服务 **[!UICONTROL 帐户（JWT断言）]**，该服务是用于服务器身份验证的服务器与服务器之间的通信服务。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定应用程序的名称和可选说明。
1. 从“组 **[!UICONTROL 织]** ”列表中，选择要为其同步资产的组织。
1. 从列 **[!UICONTROL 表中]** ，选 **[!UICONTROL 择dam-read]**、 **[!UICONTROL dam-sync、]********** write Share和Cc-Share。
1. 单击&#x200B;**[!UICONTROL 创建]**。系统会显示一条消息，通知已创建应用程序。

   ![成功创建应用程序以将AEM资产与Adobe CC集成的通知](assets/chlimage_1-50.png)

1. 复制为 **[!UICONTROL 新应用程序生成的]** “应用程序ID”。

   >[!CAUTION]
   >
   >请确保不会因疏忽而复 **[!UICONTROL 制应用程序]** Secret(而 **[!UICONTROL 非应用程序ID)]**。

## 将新配置添加到Marketing Cloud {#add-a-new-configuration-to-marketing-cloud}

1. 单击本地AEM资产实例的用户界面上的AEM徽标，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**。

1. 找到 **[!UICONTROL Adobe Marketing cloud服务]** 。 如果不存在配置，请单击“ **[!UICONTROL 立即配置”]**。 如果存在配置，请单 **[!UICONTROL 击“显示配置]** ”, **[!UICONTROL [然后单击]]** +以添加新配置。

   >[!NOTE]
   >
   >使用具有组织管理员权限的Adobe ID帐户。

1. 在“创 **[!UICONTROL 建配置]** ”对话框中，指定新配置的标题和名称，然后单击“创 **[!UICONTROL 建”]**。

   ![为新配置命名以集成AEM Assets和CC](assets/chlimage_1-51.png)

1. 在租 **[!UICONTROL 户URL字段]** ，指定AEM资产的URL。

   >[!CAUTION]
   >
   >由于需要重新设定品牌，如果您输入的租户URL `https://<tenant_id>.marketing.adobe.com` 需要将其更改为 `https://<tenant_id>.experiencecloud.adobe.com.` “要这样做，请执行以下步骤：
   >
   >1. 导航到 **工具>云服务>旧版云服务**。
   1. 在Adobe Marketing cloud下，单击“显 **示配置”**。
   1. 选择在设置AEM-MAC-CC同步时创建的配置。
   1. 编辑云服务配置并 **替换租户URL字段中的marketing.adobe** .com **，体**&#x200B;验cloud.adobe.com。
   1. 保存配置。
   1. 测试mac-sync复制代理。


1. 在“客 **[!UICONTROL 户端ID]** ”字段中，粘贴您复制的应用程序ID，该ID位于创建应用程 [序过程的末尾](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)。

   ![提供集成AEM资产和Creative cloud所需的应用程序ID值](assets/cloudservices_tenant_info.png)

1. 在“同 **[!UICONTROL 步]** ”下，选 **[!UICONTROL 择“已启用]** ”以启用同步，然后单击“ **[!UICONTROL 确定”]**。

   >[!NOTE]
   如果选择禁 **用**，则同步将单向工作。

1. 在配置页面中，单击 **[!UICONTROL 显示公钥]** ，以显示为实例生成的公钥。 或者，单击 **[!UICONTROL “下载OAuth网关的公钥]** ”以下载包含公钥的文件。 然后，打开文件以显示公钥。

## 启用同步 {#enable-synchronization}

1. 使用步骤向Marketing cloud添加新配置的最后一步中提到的以下方法之一 [显示公钥](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud)。 单击 **[!UICONTROL 显示公钥]**。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 复制公钥并将其粘贴到您在创建应用程序中 **[!UICONTROL 创建的应用程序的配置界面的]** 公钥字段中 [](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. Click **[!UICONTROL Update]**. 立即将您的资产与AEM资产实例同步。

## 测试同步 {#test-the-synchronization}

1. 单击本地AEM资产实例用户界面上的AEM徽标，然后导航到 **[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**，找到为同步创建的复制配置文件。
1. 在复制页 **[!UICONTROL 面上]** ，单击作 **[!UICONTROL 者上的代理]**。
1. 从配置文件列表中，单击组织的默认复制配置文件以将其打开。
1. 在对话框中，单击“ **[!UICONTROL 测试连接”]**。

   ![测试连接并设置组织的默认复制配置文件](assets/chlimage_1-54.png)

1. 当复制架完成时，在测试结果末尾检查成功消息。

## 将用户添加到Marketing Cloud {#add-users-to-marketing-cloud}

1. 使用管理员凭据登录到Marketing Cloud。
1. 从边栏中，转到“管 **[!UICONTROL 理]** ”，然后单击／点按启 **[!UICONTROL 动Enterprise Dashboard]**。
1. 在边栏中，单击“用 **[!UICONTROL 户]** ”以打开“ **[!UICONTROL 用户管理]** ”页面。
1. 在工具栏中，单击／点 **按**![添加aem_assets_add_icon](assets/aem_assets_add_icon.png)。
1. 添加一个或多个用户，以便您能够与Creative cloud共享资产。

   >[!NOTE]
   只有您添加到Marketing cloud的用户才能将AEM资产中的资产共享到Creative Cloud。

## 在AEM Assets和Marketing cloud之间交换资产 {#exchange-assets-between-aem-assets-and-marketing-cloud}

1. 登录 AEM 资产。
1. 在“资产”控制台中，创建一个文件夹并将一些资产上传到该文件夹。 例如，创建文件夹 **mc-demo** ，然后将资产上传到该文件夹。
1. 选择文件夹，然后单 **击**![Share](assets/assets_share.png)assets_share。
1. 从菜单中，选择 **[!UICONTROL Adobe Marketing Cloud]** ，然后单击 **[!UICONTROL 共享]**。 系统会显示一条消息，通知您已与Marketing cloud共享文件夹。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   在Adobe Marketing cloud中共享时， `sling:OrderedFolder`不支持共享类型的“资产”文件夹。 如果要共享文件夹，则在AEM资产中创建文件夹时，请勿选择“已排序” **[!UICONTROL 选项]** 。

1. 刷新AEM Assets用户界面。 您在本地AEM资产实例的“资产”控制台中创建的文件夹将复制到Marketing Cloud UI。 您上传到AEM资产中文件夹的资产，在AEM服务器处理后，该资产会显示在Marketing cloud中该文件夹的副本中。
1. 您还可以在Marketing cloud中上传文件夹复制副本中的资产。 处理完资产后，该资产会显示在AEM资产的共享文件夹中。

## 在AEM资产和Creative cloud之间交换资产 {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
已弃用“AEM到Creative cloud文件夹共享”功能。 强烈建议客户使用较新的功能，如 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) 或 [AEM桌面应用程序](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)。 了解有关 [AEM和Creative cloud集成最佳实践的更多信息](/help/assets/aem-cc-integration-best-practices.md)。

通过AEM资产，您可以与Adobe Creative cloud用户共享包含资产的文件夹。

1. 在“资产”控制台中，选择要与Creative cloud共享的文件夹。
1. 在工具栏中，单 **[!UICONTROL 击]**![Share](assets/assets_share.png)assets_share。
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   这些选项对于在根目录上具有读取权限的用户可用。 用户必须拥有访问Marketing cloud的复制代理信息所需的权限。

1. 在Creative cloud共 **[!UICONTROL 享页面中]** ，添加要与其共享文件夹的用户，然后为该用户选择角色。 单击“ **[!UICONTROL 保存]** ”，然后单 **[!UICONTROL 击“确定”]**。

1. 使用您与其共享文件夹的用户的凭证，登录到 Creative Cloud。此时共享的文件夹便可在 Creative Cloud 中使用。

AEM Assets-Marketing cloud同步的设计方式是，上传资产的用户计算机实例保留修改资产的权利。 只有这些更改才会传播到另一个实例。

例如，如果资产是从AEM资产（内部部署）实例上传的，则对该实例中资产所做的更改会传播到Marketing cloud实例。 但是，从Marketing cloud实例对同一资产所做的更改不会传播到AEM实例，从Marketing cloud上传的资产也会传播到AEM实例，反之亦然。

>[!MORELIKETHIS]
* [AEM与Creative cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)
* [AEM到Creative cloud文件夹共享最佳实践](/help/assets/aem-cc-folder-sharing-best-practices.md)

