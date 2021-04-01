---
title: 配置AEM Assets与Experience Cloud的集成
description: 了解如何配置AEM Assets与Experience Cloud的集成。
contentOwner: AG
feature: 资产管理
role: 业务从业者、架构师、管理员
translation-type: tm+mt
source-git-commit: 4cc8e60694e2aea74dfedd0bbcb8d47a208d45d1
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---


# 配置AEM Assets与Experience Cloud {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}的集成

如果您是Adobe Experience Cloud客户，则可以将Adobe Experience Manager资产内的资产与Adobe Creative Cloud同步，反之亦然。 您还可以将资产与Experience Cloud同步，反之亦然。 可以通过[!DNL Adobe I/O]设置此同步。 [!DNL Adobe Marketing Cloud]的更新名称为[!DNL Adobe Experience Cloud]。

设置此集成的工作流是：

1. 在[!DNL Adobe I/O]中使用公共网关创建身份验证并获取应用程序 ID。
1. 使用用户档案在AEM Assets实例上创建应用程序 ID。
1. 使用此配置可同步您的资产。

在后端，AEM服务器使用网关对您的用户档案进行身份验证，然后在资产和Experience Cloud之间同步数据。

>[!CAUTION]
>
>此功能在AEM Assets中已弃用。 在[AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)中查找替换项。 如果您有任何查询，请[与Adobe客户服务部门](https://www.adobe.com/account/sign-in.supportportal.html)联系。

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 创建应用程序{#create-an-application}

1. 通过登录[https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)访问Adobe Developer网关接口。

   >[!NOTE]
   >
   >您需要管理员权限才能创建应用程序 ID。

1. 从左侧窗格，导航到&#x200B;**[!UICONTROL 开发人员工具]** > **[!UICONTROL 应用程序]**&#x200B;以视图列表应用程序。
1. 单击&#x200B;**[!UICONTROL 添加]** ![ aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)以创建应用程序。
1. 在&#x200B;**[!UICONTROL 客户端凭据]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 服务帐户（JWT断言）]**，该服务是用于服务器身份验证的服务器到服务器通信服务。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定应用程序的名称和可选说明。
1. 从&#x200B;**[!UICONTROL 组织]**&#x200B;列表中，选择要为其同步资产的组织。
1. 在&#x200B;**[!UICONTROL 范围]**&#x200B;列表中，选择&#x200B;**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**&#x200B;和&#x200B;**[!UICONTROL cc-share]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。将显示一条消息，通知已创建应用程序。

   ![成功创建应用程序以将AEM Assets与Adobe CC集成的通知](assets/chlimage_1-50.png)

1. 复制为新应用程序生成的&#x200B;**[!UICONTROL 应用程序 ID]**。

   >[!CAUTION]
   >
   >请确保您不要无意中复制&#x200B;**[!UICONTROL 应用程序密码]**，而不是&#x200B;**[!UICONTROL 应用程序 ID]**。

## 向Experience Cloud{#add-a-new-configuration}添加新配置

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 旧Cloud Services]**。

1. 找到&#x200B;**[!UICONTROL Adobe Experience Cloud]**&#x200B;服务。 如果不存在配置，请单击&#x200B;**[!UICONTROL 立即配置]**。 如果存在配置，请单击&#x200B;**[!UICONTROL 显示配置]** ，然后单击`+`添加新配置。

   >[!NOTE]
   >
   >使用具有组织管理员权限的Adobe ID帐户。

1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定新配置的标题和名称，然后单击&#x200B;**[!UICONTROL 创建]**。

   ![命名新配置以集成AEM Assets和CC](assets/chlimage_1-51.png)

1. 在&#x200B;**[!UICONTROL 租户URL]**&#x200B;字段中，指定AEM Assets的URL。 在过去，如果URL定义为`https://<tenant_id>.marketing.adobe.com`，则将其更改为`https://<tenant_id>.experiencecloud.adobe.com`。

   1. 导航到&#x200B;**工具 > 云服务 > 旧版云服务**。在Adobe Experience Cloud下，单击&#x200B;**显示配置**。
   1. 选择要编辑的现有配置。 编辑配置，将`marketing.adobe.com`替换为`experiencecloud.adobe.com`。
   1. 保存配置。测试MAC同步复制代理。

1. 在&#x200B;**[!UICONTROL 客户端ID]**&#x200B;字段中，粘贴您在过程[结束时复制的应用程序 ID，创建应用程序](#create-an-application)。

   ![提供集成AEM Assets和Creative Cloud所需的应用程序 ID值](assets/cloudservices_tenant_info.png)

1. 在&#x200B;**[!UICONTROL 同步]**&#x200B;下，选择&#x200B;**[!UICONTROL 已启用]**&#x200B;以启用同步，然后单击&#x200B;**[!UICONTROL 确定]**。 如果选择&#x200B;**disabled**，则同步将单向工作。

1. 在配置页中，单击&#x200B;**[!UICONTROL 显示公钥]**&#x200B;以显示为实例生成的公钥。 或者，单击&#x200B;**[!UICONTROL 下载OAuth Gateway]**&#x200B;的公钥，下载包含公钥的文件。 然后，打开文件以显示公钥。

## 启用同步{#enable-synchronization}

1. 使用过程[的最后一步中提到的以下方法之一显示公钥，向Experience Cloud](#add-a-new-configuration)添加新配置。 单击&#x200B;**[!UICONTROL 显示公钥]**。

   ![chlimage_1-52](assets/chlimage_1-52.png)

1. 复制公钥并将其粘贴到您在[中创建应用程序](#create-an-application)的应用程序的配置接口的&#x200B;**[!UICONTROL 公钥]**&#x200B;字段中。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。 立即将您的资产与AEM Assets实例同步。

## 测试同步{#test-the-synchronization}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，并导航到&#x200B;**[!UICONTROL Tools]**> **[!UICONTROL Deployment]**> **[!UICONTROL Replication]**，以找到为同步创建的复制用户档案。
1. 在&#x200B;**[!UICONTROL 复制]**&#x200B;页面上，单击作者&#x200B;]**上的**[!UICONTROL &#x200B;代理。
1. 在用户档案列表中，单击组织的默认复制用户档案以将其打开。
1. 在对话框中，单击&#x200B;**[!UICONTROL 测试连接]**。

   ![测试连接并设置组织的默认复制用户档案](assets/chlimage_1-54.png)

1. 当复制余留完成时，在测试结果末尾检查成功消息。

## 将用户添加到Experience Cloud{#add-users-to-experience-cloud}

1. 使用管理员凭据登录到Experience Cloud。
1. 在边栏中，转到&#x200B;**[!UICONTROL 管理]**，然后单击/点按&#x200B;**[!UICONTROL 启动企业仪表板]**。
1. 在边栏中，单击&#x200B;**[!UICONTROL 用户]**&#x200B;以打开&#x200B;**[!UICONTROL 用户管理]**&#x200B;页面。
1. 在工具栏中，单击&#x200B;**添加** ![ aem_assets_add_icon](assets/aem_assets_add_icon.png)。
1. 添加一个或多个用户，以便让用户能够与Creative Cloud共享资产。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## 在AEM Assets和Experience Cloud{#exchange-assets-between-aem-and-experience-cloud}之间交换资源

1. 登录 AEM Assets。
1. 在“资产”控制台中，创建一个文件夹，然后将一些资产上传到该文件夹。 例如，创建一个文件夹&#x200B;**mc-demo**，然后将资产上传到该文件夹。
1. 选择文件夹，然后单击&#x200B;**共享** ![assets_share](assets/do-not-localize/assets_share.png)。
1. 从菜单中，选择&#x200B;**[!UICONTROL Adobe Experience Cloud]**，然后单击&#x200B;**[!UICONTROL 共享]**。 系统会显示一条消息，通知您已与Experience Cloud共享文件夹。

   >[!NOTE]
   >
   >在Adobe Experience Cloud中进行共享时，不支持共享类型为`sling:OrderedFolder`的Assets文件夹。 如果要共享文件夹，则在AEM Assets中创建文件夹时，请勿选择&#x200B;**[!UICONTROL Ordered]**&#x200B;选项。

1. 刷新AEM Assets用户界面。 您在本地AEM Assets实例的“资产”控制台中创建的文件夹会复制到Experience Cloud用户界面。 您上传到AEM Assets中文件夹的资产，在AEM服务器处理后会显示在Experience Cloud中该文件夹的副本中。
1. 您还可以在Experience Cloud中上传文件夹的复制副本中的资产。 处理完资产后，该资产会显示在AEM Assets的共享文件夹中。

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and vice versa for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [资产和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)
>* [共享最佳实践的资产到Creative Cloud文件夹](/help/assets/aem-cc-folder-sharing-best-practices.md)

