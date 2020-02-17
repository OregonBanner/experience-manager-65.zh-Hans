---
title: 与Adobe Campaign standard集成
seo-title: 与Adobe Campaign standard集成
description: 与Adobe Campaign standard集成。
seo-description: 与Adobe Campaign standard集成。
uuid: ef31339e-d925-499c-b8fb-c00ad01e38ad
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 5c0fec99-7b1e-45d6-a115-e498d288e9e1
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e

---


# 与Adobe Campaign standard集成{#integrating-with-adobe-campaign-standard}

>[!NOTE]
>
>本文档介绍如何将AEM与基于订阅的解决方案Adobe Campaign Standard集成。 如果您使用的是Adobe Campaign 6.1，请参阅 [与Adobe Campaign 6.1集成](/help/sites-administering/campaignonpremise.md) ，以获取这些说明。

Adobe Campaign允许您直接在Adobe Experience Manager中管理电子邮件分发内容和表单。

要同时使用这两个解决方案，您必须首先配置它们以相互连接。 这涉及到Adobe Campaign和Adobe Experience Manager中的配置步骤。 本文档对这些步骤进行了详细说明。

在AEM中使用Adobe Campaign包括通过Adobe Campaign发送电子邮件和表单的功能，有关该功能的介绍，请参阅 [使用Adobe Campaign](/help/sites-authoring/campaign.md)。

此外，将AEM与 [Adobe Campaign集成时，以下主题可能会引起关注](https://docs.campaign.adobe.com/doc/standard/en/home.html):

* [电子邮件模板的最佳实践](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign集成疑难解答](/help/sites-administering/troubleshooting-campaignintegration.md)

如果要扩展与Adobe Campaign的集成，您可能希望看到以下页面：

* [创建自定义扩展](/help/sites-developing/extending-campaign-extensions.md)
* [创建自定义表单映射](/help/sites-developing/extending-campaign-form-mapping.md)

## 配置Adobe Campaign {#configuring-adobe-campaign}

配置Adobe Campaign涉及以下事项：

1. 配置 **aemserver用户** 。
1. 创建专用外部帐户。
1. 验证AEMResourceTypeFilter选项。
1. 创建专用的交付模板。

>[!NOTE]
>
>要执行这些操作，您必须在Adobe Campaign中 **具有** “管理”角色。

### 前提条件 {#prerequisites}

请事先确保您具有以下元素：

* [AEM创作实例](/help/sites-deploying/deploy.md#getting-started)
* [AEM发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign实例](https://docs.adobe.com/content/docs/en/campaign/ACS.html)

>[!CAUTION]
>
>要使AEM与Adobe Campaign之间的集 [成功能正常工作，必须执行配置Adobe Campaign](#configuring-adobe-campaign)[](#configuring-adobe-experience-manager) 和配置Adobe Experience Manager部分中详细介绍的操作。

### 配置aemserver用户 {#configuring-the-aemserver-user}

必须 **在Adobe Campaign中配置** aemserver用户。 aemserver **** 是将AEM服务器连接到Adobe Campaign的技术用户。

转到“管 **理** ”>“用户和安 **全性”** >“用 **户**”，然后选择 **** aemserver用户。 单击它可打开用户设置。

* 您必须为此用户设置口令。 无法通过UI执行此操作。 此配置必须由技术管理员在REST中完成。
* 您可以为此用户分配特定角色，如 **deliveryPrepare**，该角色允许用户创建和编辑分发。

### 配置Adobe Experience manager外部帐户 {#configuring-an-adobe-experience-manager-external-account}

您必须配置一个外部帐户，以便将Adobe Campaign连接到AEM实例。

>[!NOTE]
>
>在AEM中，请确保为campaign-remote用户设置口令。 您需要设置此密码才能将Adobe Campaign与AEM连接。 以管理员身份登录，在用户管理控制台中，搜索营销活动远程用户并单击“设 **置口令”**。

配置AEM外部帐户：

1. 转到“管 **理** ”>“应 **用程序设置** ” **>“**&#x200B;外部帐户”。

   ![chlimage_1-124](assets/chlimage_1-124a.png)

1. 选择默认 **aemInstance** 外部帐户，或通过单击“创建”按钮创建 **新帐户** 。
1. 在“ **类型**”字 **段中选择** Adobe Experience Manager，然后输入用于AEM创作实例的访问参数：服务器地址、帐户名和密码。

   >[!NOTE]
   >
   >请确保不在URL末尾添加 **结尾** /斜杠，否则连接将无法正常工作。

1. 确保选中“已 **启用** ”复选框，然后单击“ **保存** ”以保存修改。

### 验证AEMResourceTypeFilter选项 {#verifying-the-aemresourcetypefilter-option}

AEMResourceTypeFilter **** 选项用于筛选可在Adobe Campaign中使用的AEM资源类型。 这允许Adobe Campaign检索专门设计用于Adobe Campaign的AEM内容。

此选项已预先配置；但是，如果更改此选项，则可能导致无法正常集成。

要验证 **AEMResourceTypeFilter选项是否已配置** ，请执行以下操作：

1. 转到“管 **理** ”>“应 **用程序设置** ” **>“**&#x200B;选项”。
1. 在列表中，您可以确保列 **出AEMResourceTypeFilter** 选项，并确保路径正确。

### 创建特定于AEM的电子邮件分发模板 {#creating-an-aem-specific-email-delivery-template}

默认情况下，Adobe Campaign的电子邮件模板中不启用AEM功能。 您可以配置新的电子邮件分发模板，该模板将用于创建包含AEM内容的电子邮件。

要创建特定于AEM的电子邮件分发模板，请执行以下操作：

1. 转到“资 **源** ”>“模 **板** ” **>“交**&#x200B;付模板”。
1. **通过单击操作栏中的复选标记** ，选择现有的 **Standard电子邮件（邮件）默认模板，然后通过单击复制图标并单击确认来复制该模** 板 ********。
1. 通过单击 **x** ，打开新创建的标准电子邮件（邮件）模板，然后从模板功能板的操作栏中选择 **Edit properties****** ，禁用选择模式。

   您可以修改模板的标 **签**。

1. 在属性内 **容部分** ，将内容 **源更改为****Adobe Experience Manager**。 然后选择之前创建的外部帐户，并单击“确 **认”**。

   单击确认并单击保 **存** ，以保存 **修改。**

   通过此模板创建的电子邮件分发将启用AEM内容功能。

   ![chlimage_1-125](assets/chlimage_1-125a.png)

## Configuring Adobe Experience Manager {#configuring-adobe-experience-manager}

要配置AEM，您必须执行以下操作：

* 在实例之间配置复制。
* 将AEM连接到Adobe Campaign。
* 配置externalizer。

### 在AEM实例之间配置复制 {#configuring-replication-between-aem-instances}

从AEM创作实例创建的内容会首先发送到发布实例。 然后，此发布实例会将内容传输到Adobe Campaign。 因此，必须将复制代理配置为从AEM创作实例复制到AEM发布实例。

>[!NOTE]
>
>如果您不想使用复制URL，而是使用面向公共的URL，则可以在OSGi( **Tools** >**Web Console** > **OSGi Configuration > AEM Campaign Integration - ConfigurationIntegration)中的以下配置设置中设置** Public URL ****:
**** 公共URL:com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

此步骤也是将某些创作实例配置复制到发布实例所必需的。

要在AEM实例之间配置复制，请执行以下操作：

1. 从实例中，选择 **AEM**> **工具 ****图标>** Deployment **>** Replication Agents ********>创作作作者上的ReplicationAgent，然后单击Default Agent的Click Agent（默认ReplicationAgent）。

   ![chlimage_1-126](assets/chlimage_1-126a.png)

   >[!NOTE]
   在配置与Adobe Campaign的集成时，请避免使用localhost（即AEM的本地副本），除非发布和作者实例都位于同一台计算机上。

1. 单击 **编辑** ，然后选择 **传输** 选项卡。
1. 配置URI，方法是将 **localhost替换** （IP地址或AEM发布实例的地址）。

   ![chlimage_1-127](assets/chlimage_1-127a.png)

### 将AEM连接到Adobe Campaign {#connecting-aem-to-adobe-campaign}

在将AEM和Adobe Campaign结合使用之前，您必须在两个解决方案之间建立链接，以便它们能够通信。

1. 连接到AEM创作实例。
1. 选择 **>** >操作 **>** Cloud **>** Cloud **> Tools Cloud Services Now****** Configure The Adobe Campaign部分中的Cloud Configure Configure Services。

   ![chlimage_1-128](assets/chlimage_1-128a.png)

1. 通过输入标题并单击创建 **，创建新配置******，或选择要与Adobe Campaign实例链接的现有配置。
1. 编辑配置，使其与Adobe Campaign实例的参数匹配。

   * **用户名**:aemserver ****,Adobe Campaign AEM集成包运营商，用于在两个解决方案之间建立链接。
   * **密码**:Adobe Campaign aemserver操作员密码。 您可能必须直接在Adobe Campaign中为此操作员重新指定密码。
   * **API端点**:Adobe Campaign实例URL。

1. 选择 **连接到Adobe Campaign** ，然后单 **击确定**。

   ![chlimage_1-129](assets/chlimage_1-129a.png)

   >[!NOTE]
   在创建 [并发布电子邮件后](/help/sites-authoring/campaign.md)，您需要将配置重新发布到发布实例。

   ![chlimage_1-130](assets/chlimage_1-130a.png)

>[!NOTE]
如果连接失败，请确保检查以下内容：
* 在使用与Adobe Campaign实例(https)的安全连接时，您可能会遇到证书问题。 您必须将Adobe Campaign实例证书添加到JDK的**cacerts **文件。
* 此外，请参 [阅AEM/Adobe Campaign集成疑难解答](/help/sites-administering/troubleshooting-campaignintegration.md)。



### 配置外部器 {#configuring-the-externalizer}

您需要在 [创作实例的AEM中配置](/help/sites-developing/externalizer.md) externalizer。 Externalizer是OSGi服务，它允许您将资源路径转换为外部和绝对URL。 此服务提供了配置和构建这些外部URL的中心位置。

有关 [常规说明，请参阅配置](/help/sites-developing/externalizer.md) externalizer。 对于Adobe Campaign集成，请确保在Adobe Campaign控制台可 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl` 访问的服 `localhost:4503` 务器上配置发布服务器，而不是指向服务器。

如果指向Adobe Campaign无 `localhost:4503` 法访问的服务器或其他服务器，则您的图像不会显示在Adobe Campaign控制台上。

![chlimage_1-131](assets/chlimage_1-131a.png)

