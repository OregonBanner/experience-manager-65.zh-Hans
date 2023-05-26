---
title: 配置AEM Assets与Experience Cloud的集成
description: 了解如何配置AEM Assets与Experience Cloud的集成。
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# 配置AEM Assets与Experience Cloud的集成 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience Cloud客户，则可以将Adobe Experience Manager Assets中的资源与Adobe Creative Cloud同步，反之亦然。 您还可以将资源与Experience Cloud同步，反之亦然。 您可以通过以下方式设置此同步 [!DNL Adobe I/O]. 更新后的名称 [!DNL Adobe Marketing Cloud] 是 [!DNL Adobe Experience Cloud].

设置此集成的工作流是：

1. 在中创建身份验证 [!DNL Adobe I/O] 使用公共网关获取应用程序ID。
1. 使用应用程序ID在AEM Assets实例上创建配置文件。
1. 使用此配置可同步您的资产。

在后端，AEM服务器通过网关验证您的配置文件，然后在Assets和Experience Cloud之间同步数据。

>[!NOTE]
>
>此功能在中已弃用 [!DNL Assets]. 在中查找替换部件 [AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md). 如果您有任何查询， [联系Adobe客户支持](https://www.adobe.com/cn/account/sign-in.supportportal.html).

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 创建应用程序 {#create-an-application}

1. 通过以下方式访问Adobe Developer网关界面： [https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/).

   >[!NOTE]
   >
   >您需要管理员权限才能创建应用程序ID。

1. 从左窗格中，导航到 **[!UICONTROL 开发人员工具]** > **[!UICONTROL 应用程序]** 查看应用程序列表。
1. 单击 **[!UICONTROL 添加]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png) 创建应用程序。
1. 从 **[!UICONTROL 客户端凭据]** 列表，选择 **[!UICONTROL 服务帐户（JWT断言）]**，是用于服务器身份验证的服务器到服务器通信服务。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定应用程序的名称和可选说明。
1. 从 **[!UICONTROL 组织]** 列表中，选择要为其同步资产的组织。
1. 从 **[!UICONTROL 范围]** 列表，选择 **[!UICONTROL dam-read]**， **[!UICONTROL dam-sync]**， **[!UICONTROL dam-write]**、和 **[!UICONTROL cc-share]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。此时将显示一条消息，通知应用程序已创建。

   ![成功创建应用程序以将AEM Assets与Creative Cloud集成的通知](assets/chlimage_1-50.png)

1. 复制 **[!UICONTROL 应用程序ID]** 为新的应用程序生成的属性。

   >[!CAUTION]
   >
   >确保您不会无意中复制 **[!UICONTROL 应用程序密码]** 而不是 **[!UICONTROL 应用程序ID]**.

## 向Experience Cloud添加新配置 {#add-a-new-configuration}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL 旧版Cloud Services]**.

1. 找到 **[!UICONTROL Adobe Experience Cloud]** 服务。 如果不存在配置，请单击 **[!UICONTROL 立即配置]**. 如果存在配置，请单击 **[!UICONTROL 显示配置]** 并单击 `+` 以添加新配置。

   >[!NOTE]
   >
   >使用具有组织管理员权限的Adobe ID帐户。

1. 在 **[!UICONTROL 创建配置]** 对话框，指定新配置的标题和名称，然后单击 **[!UICONTROL 创建]**.

   ![命名新配置以集成AEM Assets和Creative Cloud](assets/aem-ec-integration-config1.png)

1. 在 **[!UICONTROL 租户URL]** 字段中，指定AEM Assets的URL。 过去，如果URL定义为 `https://<tenant_id>.marketing.adobe.com`，将其更改为 `https://<tenant_id>.experiencecloud.adobe.com`.

   1. 导航到&#x200B;**工具 > 云服务 > 旧版云服务**。在Adobe Experience Cloud下，单击 **显示配置**.
   1. 选择要编辑的现有配置。 编辑配置并替换 `marketing.adobe.com` 到 `experiencecloud.adobe.com`.
   1. 保存配置。测试MAC-sync复制代理。

1. 在 **[!UICONTROL 客户端ID]** 字段，粘贴您在过程结束时复制的应用程序ID [创建应用程序](#create-an-application).

   ![提供集成AEM Assets和Creative Cloud所需的应用程序ID值](assets/cloudservices_tenant_info.png)

1. 下 **[!UICONTROL 同步]** 选择 **[!UICONTROL 已启用]** 启用同步并单击 **[!UICONTROL 确定]**. 如果您选择 **已禁用**，同步在单个方向上工作。

1. 在配置页面中，单击 **[!UICONTROL 显示公钥]** 以显示为您的实例生成的公共密钥。 或者，单击 **[!UICONTROL 下载OAuth网关的公共密钥]** 下载包含公钥的文件。 然后，打开文件以显示公钥。

## 启用同步 {#enable-synchronization}

1. 使用该过程的最后一步中提到的以下方法之一显示公钥 [向Experience Cloud添加新配置](#add-a-new-configuration). 单击 **[!UICONTROL 显示公钥]**.

1. 复制公钥并将其粘贴到 **[!UICONTROL 公钥]** 您在中创建的应用程序的配置界面的字段 [创建应用程序](#create-an-application).

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。立即将您的资源与AEM Assets实例同步。

## 测试同步 {#test-the-synchronization}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到 **[!UICONTROL 工具]**> **[!UICONTROL 部署]**> **[!UICONTROL 复制]**定位为同步创建的复制配置文件。
1. 在 **[!UICONTROL 复制]** 页面，单击 **[!UICONTROL 作者代理]**.
1. 从配置文件列表中，单击贵组织的默认复制配置文件以将其打开。
1. 在对话框中，单击 **[!UICONTROL 测试连接]**.

   ![测试连接并为您的组织设置默认复制配置文件](assets/chlimage_1-54.png)

1. 复制休息完成后，在测试结果结束时检查是否显示成功消息。

## 将用户添加到Experience Cloud {#add-users-to-experience-cloud}

1. 使用管理员凭据登录Experience Cloud。
1. 从滑轨，转到 **[!UICONTROL 管理]** 然后单击 **[!UICONTROL 启动Enterprise Dashboard]**.
1. 在边栏中，单击 **[!UICONTROL 用户]** 以打开 **[!UICONTROL User Management]** 页面。
1. 在工具栏中，单击 **添加** ![aem_assets_add_icon](assets/aem_assets_add_icon.png).
1. 添加一个或多个要提供与Creative Cloud共享资源的用户。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## 在AEM Assets和Experience Cloud之间交换资源 {#exchange-assets-between-aem-and-experience-cloud}

1. 登录到AEM Assets。
1. 在Assets控制台中，创建一个文件夹并将一些资产上传到该文件夹。 例如，创建一个文件夹 **mc-demo** 并将资产上传到其中。
1. 选择文件夹并单击 **共享** ![assets_share](assets/do-not-localize/assets_share.png).
1. 从菜单中，选择 **[!UICONTROL Adobe Experience Cloud]** 和点击 **[!UICONTROL 共享]**. 此时将显示一条消息，通知该文件夹已与Experience Cloud共享。

   >[!NOTE]
   >
   >共享该类型的资产文件夹 `sling:OrderedFolder`在Adobe Experience Cloud中共享的上下文中不支持。 如果要共享文件夹，则在AEM Assets中创建该文件夹时，请勿选择 **[!UICONTROL 已排序]** 选项。

1. 刷新AEM Assets用户界面。 您在本地AEM Assets实例的Assets控制台中创建的文件夹将会复制到Experience Cloud用户界面。 在AEM服务器处理上传到AEM Assets中文件夹的资源后，该资源将显示在Experience Cloud中的文件夹副本中。
1. 您还可以在Experience Cloud中上传文件夹的已复制副本中的资源。 处理完资源后，该资源将显示在AEM Assets的共享文件夹中。

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
>* [资源和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)

