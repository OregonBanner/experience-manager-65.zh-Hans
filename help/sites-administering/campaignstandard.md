---
title: 与Adobe Campaign Standard集成
seo-title: 与Adobe Campaign Standard集成
description: 与Adobe Campaign Standard整合。
seo-description: 与Adobe Campaign Standard整合。
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: f951c195c581f770dcc87fdf4a89d40ee6dd9ec0
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---


# 与Adobe Campaign Standard集成{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本文档介绍如何将AEM与基于订阅的解决方案Adobe Campaign Standard集成。 如果您使用Adobe Campaign6.1，请参阅[与Adobe Campaign6.1](/help/sites-administering/campaignonpremise.md)集成，以获取这些说明。

Adobe Campaign允许您直接在Adobe Experience Manager管理电子邮件投放内容和表单。

要同时使用这两种解决方案，您必须首先配置它们以彼此连接。 这涉及Adobe Campaign和Adobe Experience Manager中的配置步骤。 本文档详细介绍了这些步骤。

在AEM中使用Adobe Campaign包括通过Adobe Campaign发送电子邮件和表单的功能，有关说明，请参阅[使用Adobe Campaign](/help/sites-authoring/campaign.md)。

此外，将AEM与[Adobe Campaign](https://docs.campaign.adobe.com/doc/standard/en/home.html)集成时，以下主题可能会引起关注：

* [电子邮件模板的最佳实践](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign集成故障排除](/help/sites-administering/troubleshooting-campaignintegration.md)

如果要扩展与Adobe Campaign的集成，您可能希望看到以下页面：

* [创建自定义扩展](/help/sites-developing/extending-campaign-extensions.md)
* [创建自定义表单映射](/help/sites-developing/extending-campaign-form-mapping.md)

## 配置Adobe Campaign{#configuring-adobe-campaign}

配置Adobe Campaign涉及以下方面：

1. 配置&#x200B;**aemserver**&#x200B;用户。
1. 创建专用外部帐户。
1. 验证AEMResourceTypeFilter选项。
1. 创建专用投放模板。

>[!NOTE]
>
>要执行这些操作，您必须具有&#x200B;**administration**&#x200B;角色作为Adobe Campaign。

### 前提条件 {#prerequisites}

请事先确保您具有以下元素：

* [AEM创作实例](/help/sites-deploying/deploy.md#getting-started)
* [AEM发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign实例](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>要使AEM与Adobe Campaign之间的集成功能正常工作，必须在[配置Adobe Campaign](#configuring-adobe-campaign)和[配置Adobe Experience Manager](#configuring-adobe-experience-manager)部分中详细介绍的操作。

### 配置aemserver用户{#configuring-the-aemserver-user}

**aemserver**&#x200B;用户必须配置为Adobe Campaign。 **aemserver**&#x200B;是技术用户，将用于将AEM服务器连接到Adobe Campaign。

转至&#x200B;**管理** > **用户与安全** > **用户**，然后选择&#x200B;**aemserver**&#x200B;用户。 单击它以打开用户设置。

* 您必须为此用户设置口令。 无法通过UI完成此操作。 此配置必须由技术管理员在REST中完成。
* 您可以为此用户分配特定角色，如&#x200B;**deliveryPrepare**，这允许用户创建和编辑投放。

### 配置Adobe Experience Manager外部帐户{#configuring-an-adobe-experience-manager-external-account}

您必须配置一个外部帐户，允许您将Adobe Campaign连接到AEM实例。

>[!NOTE]
>
>在AEM中，确保为活动远程用户设置口令。 您需要设置此密码才能将Adobe Campaign与AEM连接。 以管理员身份登录，在“用户管理”控制台中，搜索活动远程用户，然后单击“设置口令”**。**

配置AEM外部帐户:

1. 转到&#x200B;**管理** > **应用程序设置** > **外部帐户**。

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 选择默认的&#x200B;**aemInstance**&#x200B;外部帐户，或通过单击&#x200B;**创建**&#x200B;按钮创建新实例。
1. 在&#x200B;**Type**&#x200B;字段中选择&#x200B;**Adobe Experience Manager** i，并输入用于AEM创作实例的访问参数：服务器地址、帐户名和密码。

   >[!NOTE]
   >
   >请确保不在URL末尾添加结尾&#x200B;**/**&#x200B;斜杠，否则连接将不工作。

1. 确保选中&#x200B;**已启用**&#x200B;复选框，然后单击&#x200B;**保存**&#x200B;以保存修改。

### 验证AEMResourceTypeFilter选项{#verifying-the-aemresourcetypefilter-option}

**AEMResourceTypeFilter**&#x200B;选项用于筛选可用于Adobe Campaign的AEM资源的类型。 这允许Adobe Campaign检索专门设计用于Adobe Campaign的AEM内容。

此选项已预先配置；但是，如果更改此选项，可能会导致集成无法正常工作。

要验证&#x200B;**AEMResourceTypeFilter**&#x200B;选项是否已配置：

1. 转到&#x200B;**管理** > **应用程序设置** > **选项**。
1. 在该列表中，您可以确保列出&#x200B;**AEMResourceTypeFilter**&#x200B;选项并确保路径正确。

### 创建AEM特定的电子邮件投放模板{#creating-an-aem-specific-email-delivery-template}

默认情况下，Adobe Campaign的电子邮件模板中不启用AEM功能。 您可以配置新的电子邮件投放模板，该电子邮件将用于创建包含AEM内容的电子邮件。

要创建AEM特定的电子邮件投放模板，请执行以下操作：

1. 转至&#x200B;**资源** > **模板** > **投放模板**。
1. **启** 用选择，方法是单击操作栏中的复选标记，选择现有 **Standard电子邮件（邮件）** 默认模板，然后单击“文本”图标并单 **** 击“确认”来 **重复它**。
1. 单击&#x200B;**x**&#x200B;并打开新创建的&#x200B;**标准电子邮件（邮件）**&#x200B;模板，然后从模板仪表板的操作栏中选择&#x200B;**编辑属性**，以禁用选择模式。

   您可以修改模板的&#x200B;**标签**。

1. 在属性&#x200B;**内容**&#x200B;部分，将&#x200B;**内容源**&#x200B;更改为&#x200B;**Adobe Experience Manager**。 然后选择之前创建的外部帐户，并单击&#x200B;**确认**。

   单击&#x200B;**确认**&#x200B;并单击&#x200B;**保存，以保存修改。**

   通过此模板创建的电子邮件投放将启用AEM内容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## 配置Adobe Experience Manager{#configuring-adobe-experience-manager}

要配置AEM，您必须执行以下操作：

* 在实例之间配置复制。
* 将AEM连接到Adobe Campaign。
* 配置外部器。

### 在AEM实例{#configuring-replication-between-aem-instances}之间配置复制

首先从AEM创作实例创建的内容将发送到发布实例。 然后，此发布实例会将内容传输到Adobe Campaign。 因此，必须将复制代理配置为从AEM创作实例复制到AEM发布实例。

>[!NOTE]
>
>如果不想使用复制URL，而是使用面向公共的URL，可以在OSGi(**Tools** > **Web控制台** > **OSGi配置> AEM)中的以下配置设置中设置** Public URL **活动集成——配置**):
**公共URL:** com.day.cq.mcm.活动.impl.IntegrationConfigImpl#aem.mcm.活动.publicUrl

此步骤也是将某些创作实例配置复制到发布实例所必需的。

要在AEM实例之间配置复制，请执行以下操作：

1. 在创作实例中，选择&#x200B;**AEM徽标**> **工具** > **部署** > **复制** > **作者**&#x200B;上的代理，然后单击&#x200B;**默认代理**。

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   配置与Adobe Campaign的集成时，请避免使用localhost(即AEM的本地副本)，除非发布和作者实例都位于同一台计算机上。

1. 单击&#x200B;**编辑**，然后选择&#x200B;**传输**&#x200B;选项卡。
1. 通过将&#x200B;**localhost**&#x200B;替换为AEM发布实例的IP地址或地址来配置URI。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 将AEM连接到Adobe Campaign{#connecting-aem-to-adobe-campaign}

在将AEM和Adobe Campaign结合使用之前，您必须建立两个解决方案之间的链接，以便它们能够通信。

1. 连接到AEM创作实例。
1. 选择&#x200B;**工具** > **操作** > **云** > **Cloud Services**，然后在Adobe Campaign部分中选择&#x200B;**立即配置**。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 通过输入&#x200B;**标题**&#x200B;并单击&#x200B;**创建**&#x200B;创建新配置，或选择要与Adobe Campaign实例链接的现有配置。
1. 编辑配置，使其与Adobe Campaign实例的参数匹配。

   * **用户名**: **aemserver**,Adobe CampaignAEM集成包运营商，用于建立两个解决方案之间的链接。
   * **密码**:Adobe CampaignAemserver操作员密码。您可能必须直接以Adobe Campaign重新指定此运算符的密码。
   * **API端点**:Adobe Campaign实例URL。

1. 选择&#x200B;**连接到Adobe Campaign**&#x200B;并单击&#x200B;**确定**。

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   在[创建电子邮件并发布它](/help/sites-authoring/campaign.md)后，您需要将配置重新发布到发布实例。

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果连接失败，请确保检查以下内容：
* 使用与Adobe Campaign实例(https)的安全连接时，可能会遇到证书问题。 您必须将Adobe Campaign实例证书添加到JDK的**cacerts **文件。
* 此外，请参阅[AEM/Adobe Campaign集成疑难解答](/help/sites-administering/troubleshooting-campaignintegration.md)。



### 配置外部器{#configuring-the-externalizer}

您需要在创作实例的AEM中配置外部器[。 ](/help/sites-developing/externalizer.md)Externalizer是OSGi服务，它允许您将资源路径转换为外部和绝对URL。 此服务提供一个中心位置来配置这些外部URL并构建它们。

有关一般说明，请参见[配置外部器](/help/sites-developing/externalizer.md)。 对于Adobe Campaign集成，请确保在`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`配置发布服务器，该服务器不指向`localhost:4503`，而是指向Adobe Campaign控制台可以访问的服务器。

如果它指向`localhost:4503`或Adobe Campaign无法访问的其他服务器，则您的图像将不会显示在Adobe Campaign控制台上。

![chlimage_1-131](assets/chlimage_1-131a.png)

