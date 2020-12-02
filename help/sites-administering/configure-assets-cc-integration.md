---
title: 配置AEM Assets与Experience Cloud和Creative Cloud的集成
seo-title: 配置AEM Assets与Marketing Cloud和Creative Cloud的集成
description: 了解如何配置AEM Assets与Experience Cloud和Creative Cloud的集成。
seo-description: 了解如何配置AEM Assets与Experience Cloud和Creative Cloud的集成。
uuid: ec36ea0e-607f-4c73-89df-e095067fccd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 82a8e807-a2df-4fe3-a68c-2dabc9328eca
docset: aem65
translation-type: tm+mt
source-git-commit: c7f06670ca8b488a661fde7a133bce6886ee7f5d
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 3%

---


# 配置AEM Assets与Experience Cloud和Creative Cloud{#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}的集成

如果您是Adobe Experience Cloud客户，则可以将Adobe Experience Manager(AEM)资产内的资产与Adobe Creative Cloud同步，反之亦然。 您还可以将资产与Experience Cloud同步，反之亦然。 您可以通过Adobe I/O设置此同步。

设置此集成的工作流是：

1. 在Adobe I/O使用公共网关创建身份验证并获得应用程序 ID。
1. 使用用户档案在AEM Assets实例上创建应用程序 ID。
1. 使用此配置将您在AEM Assets的资产与Creative Cloud同步。

在后端，AEM服务器使用网关验证您的用户档案，然后在AEM Assets和Experience Cloud之间同步数据。

>[!CAUTION]
>
>AEM到Creative Cloud文件夹共享功能在AEM Assets已弃用。 了解更多信息并查找[AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)中的替换项。

![整合AEM Assets和Creative Cloud时的数据流](assets/chlimage_1-48.png)

整合AEM Assets和Creative Cloud时的数据流

>[!NOTE]
>
>在Adobe Experience Cloud和Adobe Creative Cloud之间共享资产需要AEM实例的管理员权限。

>[!CAUTION]
>
>Adobe Marketing Cloud被改名为Adobe Experience Cloud。 下面的步骤仍提到Marketing Cloud，以反映当前接口。 这些提及将在以后的日期更改。

## 创建应用程序{#create-an-application}

1. 通过登录[https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)访问Adobe开发人员网关接口。

   >[!NOTE]
   >
   >您需要管理员权限才能创建应用程序 ID。

1. 从左窗格，导航到&#x200B;**[!UICONTROL 开发人员工具]** > **[!UICONTROL 应用程序]**&#x200B;以视图应用程序列表。
1. 单击&#x200B;**[!UICONTROL 添加]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)以创建应用程序。
1. 从&#x200B;**[!UICONTROL 客户端凭据]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 服务帐户（JWT断言）]**，该服务是用于服务器身份验证的服务器到服务器通信服务。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定应用程序的名称和可选说明。
1. 从&#x200B;**[!UICONTROL 组织]**&#x200B;列表中，选择要同步资产的组织。
1. 从&#x200B;**[!UICONTROL 范围]**&#x200B;列表中，选择&#x200B;**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**&#x200B;和&#x200B;**[!UICONTROL cc-share]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。系统会显示一条消息，通知已创建应用程序。

   ![成功创建应用程序以将AEM Assets与AdobeCC集成的通知](assets/chlimage_1-50.png)

1. 复制为新应用程序生成的&#x200B;**[!UICONTROL 应用程序 ID]**。

   >[!CAUTION]
   >
   >请确保您不会无意中复制&#x200B;**[!UICONTROL 应用程序密码]**&#x200B;而不是&#x200B;**[!UICONTROL 应用程序 ID]**。

## 向Marketing Cloud{#add-a-new-configuration-to-marketing-cloud}添加新配置

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 传统Cloud Services]**。

1. 找到&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;服务。 如果不存在配置，请单击&#x200B;**[!UICONTROL Configure Now]**。 如果存在配置，请单击&#x200B;**[!UICONTROL 显示配置]**，然后单击`+`添加新配置。

   >[!NOTE]
   >
   >使用具有组织管理员权限的Adobe ID帐户。

1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定新配置的标题和名称，然后单击&#x200B;**[!UICONTROL 创建]**。

   ![命名新配置以集成AEM Assets和CC](assets/chlimage_1-51.png)

1. 在&#x200B;**[!UICONTROL 租户URL]**&#x200B;字段中，指定AEM Assets的URL。

   >[!CAUTION]
   >
   >由于重新设定了品牌，如果您将租户URL输入为`https://<tenant_id>.marketing.adobe.com`，则需要将其更改为`https://<tenant_id>.experiencecloud.adobe.com.`。为此，请按照以下步骤操作：
   >
   >1. 导航到&#x200B;**工具 > 云服务 > 旧版云服务**。
   1. 在Adobe Marketing Cloud下，单击&#x200B;**显示配置**。
   1. 选择在设置AEM-MAC-CC同步时创建的配置。
   1. 编辑cloudservice配置，将租户URL字段中的&#x200B;**marketing.adobe.com**&#x200B;替换为&#x200B;**experiencecloud.adobe.com**。
   1. 保存配置。
   1. 测试mac-sync复制代理。


1. 在&#x200B;**[!UICONTROL 客户端ID]**&#x200B;字段中，将您复制的应用程序 ID粘贴到过程[创建应用程序](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)末尾。

   ![提供整合AEM Assets和Creative Cloud所需的应用程序 ID价值](assets/cloudservices_tenant_info.png)

1. 在&#x200B;**[!UICONTROL 同步]**&#x200B;下，选择&#x200B;**[!UICONTROL 已启用]**&#x200B;以启用同步，然后单击&#x200B;**[!UICONTROL 确定]**。

   >[!NOTE]
   如果选择&#x200B;**disabled**，则同步将沿单个方向工作。

1. 在配置页中，单击&#x200B;**[!UICONTROL 显示公钥]**&#x200B;以显示为实例生成的公钥。 或者，单击&#x200B;**[!UICONTROL 下载OAuth网关的公钥]**&#x200B;以下载包含公钥的文件。 然后，打开文件以显示公钥。

## 启用同步{#enable-synchronization}

1. 使用过程[的最后一步中提到的以下方法之一显示公钥。向Marketing Cloud](/help/sites-administering/configure-assets-cc-integration.md#add-a-new-configuration-to-marketing-cloud)添加新配置。 单击&#x200B;**[!UICONTROL 显示公钥]**。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 复制公钥并将其粘贴到您在[创建应用程序](/help/sites-administering/configure-assets-cc-integration.md#create-an-application)中创建的应用程序的配置接口的&#x200B;**[!UICONTROL 公钥]**&#x200B;字段中。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。 立即将您的资产与AEM Assets实例同步。

## 测试同步{#test-the-synchronization}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具]**> **[!UICONTROL 部署]** **[!UICONTROL 复制]**，找到为同步创建的复制用户档案。
1. 在&#x200B;**[!UICONTROL 复制]**&#x200B;页面上，单击作者&#x200B;]**上的**[!UICONTROL &#x200B;代理。
1. 在用户档案列表中，单击组织的默认复制用户档案以将其打开。
1. 在对话框中，单击&#x200B;**[!UICONTROL 测试连接]**。

   ![测试连接并设置组织的默认复制用户档案](assets/chlimage_1-54.png)

1. 当复制架完成时，在测试结果末尾检查成功消息。

## 将用户添加到Marketing Cloud{#add-users-to-marketing-cloud}

1. 使用管理员凭据登录Marketing Cloud。
1. 从边栏中，转到&#x200B;**[!UICONTROL 管理]**，然后单击／点按&#x200B;**[!UICONTROL 启动企业仪表板]**。
1. 在边栏中，单击&#x200B;**[!UICONTROL 用户]**&#x200B;以打开&#x200B;**[!UICONTROL 用户管理]**&#x200B;页面。
1. 在工具栏中，单击／点按&#x200B;**添加** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)。
1. 添加一个或多个用户，让您能够与Creative Cloud共享资产。

   >[!NOTE]
   只有您添加到Marketing Cloud的用户才能将资产从AEM Assets共享到Creative Cloud。

## 在AEM Assets和Marketing Cloud之间交换资产{#exchange-assets-between-aem-assets-and-marketing-cloud}

1. 登录 AEM 资产。
1. 在“资产”控制台中，创建一个文件夹，并将一些资产上传到该文件夹。 例如，创建文件夹&#x200B;**mc-demo**&#x200B;并将资产上传到该文件夹。
1. 选择文件夹，然后单击&#x200B;**共享** ![assets_share](assets/assets_share.png)。
1. 从菜单中，选择&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;并单击&#x200B;**[!UICONTROL 共享]**。 系统会显示一条消息，通知已与Marketing Cloud共享文件夹。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   >[!NOTE]
   在Adobe Marketing Cloud进行共享时，不支持共享类型为`sling:OrderedFolder`的Assets文件夹。 如果要共享文件夹，则在AEM Assets创建文件夹时，不要选择&#x200B;**[!UICONTROL Ordered]**&#x200B;选项。

1. 刷新AEM Assets用户界面。 您在本地AEM Assets实例的“资产”控制台中创建的文件夹将复制到Marketing CloudUI。 您上传到AEM Assets的文件夹的资产在AEM服务器处理后，会显示在Marketing Cloud的文件夹副本中。
1. 您还可以在Marketing Cloud中上传文件夹复制副本中的资产。 处理完资产后，资产会显示在AEM Assets的共享文件夹中。

## 在AEM Assets和Creative Cloud之间交换资产{#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
已弃用AEM到Creative Cloud文件夹共享功能。 强烈建议客户使用较新的功能，如[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)或[AEM桌面应用程序](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)。 请阅读[AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)了解更多信息。

AEM Assets允许您与Adobe Creative Cloud用户共享包含资产的文件夹。

1. 在“资产”控制台中，选择要与Creative Cloud共享的文件夹。
1. 在工具栏中，单击&#x200B;**[!UICONTROL 共享]** ![assets_share](assets/assets_share.png)。
1. 在列表中，选择&#x200B;**[!UICONTROL Adobe Creative Cloud]**&#x200B;选项。

   >[!NOTE]
   这些选项对于在根目录上具有读取权限的用户可用。 用户必须具有访问Marketing Cloud的复制代理信息所需的权限。

1. 在&#x200B;**[!UICONTROL Creative Cloud共享]**&#x200B;页面中，添加要与其共享文件夹的用户，并为用户选择角色。 单击&#x200B;**[!UICONTROL 保存]**，然后单击&#x200B;**[!UICONTROL 确定]**。

1. 使用您与其共享文件夹的用户的凭证，登录到 Creative Cloud。此时共享的文件夹便可在 Creative Cloud 中使用。

AEM AssetsMarketing Cloud同步的设计方式是，上传资产的用户计算机实例保留修改资产的权利。 只有这些更改才会传播到其他实例。

例如，如果资产是从AEM Assets（本地）实例上传的，则来自此实例对资产所做的更改会传播到Marketing Cloud实例。 但是，从Marketing Cloud实例对同一资产所做的更改不会传播到AEM实例，从Marketing Cloud上传的资产也会传播到实例，反之亦然。

>[!MORELIKETHIS]
* [AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)
* [AEM到Creative Cloud文件夹共享最佳实践](/help/assets/aem-cc-folder-sharing-best-practices.md)

