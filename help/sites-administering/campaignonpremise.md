---
title: 与Adobe Campaign Classic集成
seo-title: 与Adobe Campaign Classic集成
description: 了解如何将AEM与Adobe Campaign Classic集成
seo-description: 了解如何将AEM与Adobe Campaign Classic集成
uuid: 3c998b0e-a885-4aa9-b2a4-81b86f9327d3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: df94dd1b-1b65-478b-a28d-81807a8084b1
exl-id: a7281ca0-461f-4762-a631-6bb539596200
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 0%

---

# 与Adobe Campaign Classic集成{#integrating-with-adobe-campaign-classic}

>[!NOTE]
>
>本文档介绍如何将AEM与内部部署解决方案Adobe Campaign Classic集成。 如果您使用的是Adobe Campaign Standard，请参阅[与Adobe Campaign Standard集成](/help/sites-administering/campaignstandard.md)以获取这些说明。

Adobe Campaign允许您直接在Adobe Experience Manager中管理电子邮件投放内容和表单。

要同时使用两个解决方案，您必须首先将它们配置为彼此连接。 这涉及在Adobe Campaign和Adobe Experience Manager中执行配置步骤。 本文档详细介绍了这些步骤。

在AEM中使用Adobe Campaign包括通过Adobe Campaign发送电子邮件的功能，有关该功能的介绍，请参阅[使用Adobe Campaign](/help/sites-authoring/campaign.md)。 它还包括在AEM页面上使用表单来处理数据。

此外，将AEM与[Adobe Campaign](https://helpx.adobe.com/support/campaign/classic.html)集成时，可能会关注以下主题：

* [电子邮件模板最佳实践](/help/sites-administering/best-practices-for-email-templates.md)
* [Adobe Campaign集成故障诊断](/help/sites-administering/troubleshooting-campaignintegration.md)

如果您要扩展与Adobe Campaign的集成，则可能希望看到以下页面：

* [创建自定义扩展](/help/sites-developing/extending-campaign-extensions.md)
* [创建自定义表单映射](/help/sites-developing/extending-campaign-form-mapping.md)

## AEM和Adobe Campaign集成工作流{#aem-and-adobe-campaign-integration-workflow}

本节介绍创建营销活动和投放内容时AEM和Adobe Campaign之间的典型工作流程。

典型的工作流涉及以下内容，并对其进行了详细描述：

1. 开始构建您的营销活动(在Adobe Campaign和AEM中)。
1. 在链接内容和交付之前，请先在AEM中个性化您的内容，并在Adobe Campaign中创建交付。
1. 在Adobe Campaign中链接内容和交付。

### 开始构建营销活动{#start-building-your-campaign}

您可以随时开始构建营销活动。 在链接内容之前，AEM和AC是独立的。这意味着营销人员可以在Adobe Campaign中开始创建他们的营销活动和定位，而内容创建者则在AEM中处理设计。

### 在链接内容和投放之前{#before-linking-content-and-delivery}

在链接内容并创建投放机制之前，您需要执行以下操作：

**在AEM中**

* 使用&#x200B;**文本与个性化**&#x200B;组件中的个性化字段进行个性化

**在 Adobe Campaign 中：**

* 创建类型&#x200B;**aemContent**&#x200B;的投放

### 链接内容并设置投放{#linking-content-and-setting-delivery}

准备好内容以进行链接和交付后，您可以准确确定链接内容的方式和位置。

所有这些步骤均在Adobe Campaign中完成。

1. 指定要使用的AEM实例。
1. 单击同步按钮以同步内容。
1. 打开内容选取器以选取您的内容。

### 如果您是初次使用AEM {#if-you-are-new-to-aem}

如果您是初次使用AEM，可能会发现以下链接有助于您了解AEM:

* [启动AEM](/help/sites-deploying/deploy.md)
* [了解复制代理](/help/sites-deploying/replication.md)
* [查找和使用日志文件](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)
* [AEM平台简介](/help/sites-deploying/platform.md)

## 配置Adobe Campaign {#configuring-adobe-campaign}

配置Adobe Campaign涉及以下事项：

1. 在Adobe Campaign中安装AEM集成包。
1. 配置外部帐户。
1. 验证AEMResourceTypeFilter是否正确配置。

此外，您还可以进行一些高级配置，包括：

* 管理内容块
* 管理个性化字段

请参阅[高级配置](#advanced-configurations)。

>[!NOTE]
>
>要执行这些操作，您必须在Adobe Campaign中具有&#x200B;**administration**&#x200B;角色。

### 前提条件 {#prerequisites}

请事先确保您具有以下元素：

* [AEM创作实例](/help/sites-deploying/deploy.md#getting-started)
* [AEM发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)
* [Adobe Campaign Classic实例](https://helpx.adobe.com/support/campaign/classic.html)  — 包括客户端和服务器
* Internet Explorer 11

>[!NOTE]
>
>如果您运行的版本低于Adobe Campaign Classic内部版本8640，请参阅[升级文档](https://docs.campaign.adobe.com/doc/AC6.1/en/PRO_Updating_Adobe_Campaign_Upgrading.html)以了解更多信息。 请注意，必须将客户端和数据库都升级到同一内部版本。

>[!CAUTION]
>
>要使AEM与Adobe Campaign之间的集成功能正常工作，必须在[配置Adobe Campaign](#configuring-adobe-campaign)和[配置Adobe Experience Manager](#configuring-adobe-experience-manager)部分中详细介绍的操作。

### 安装AEM集成包{#installing-the-aem-integration-package}

必须在Adobe Campaign中安装&#x200B;**AEM Integration**&#x200B;包。 要执行此操作：

1. 转到要与AEM链接的Adobe Campaign实例。
1. 选择&#x200B;*工具* > *高级* > *导入包……*。

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. 单击&#x200B;**安装标准包**，然后选择&#x200B;**AEM Integration**&#x200B;包。

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. 单击&#x200B;**Next**，然后单击&#x200B;**Start**。

   此包包含&#x200B;**aemserver**&#x200B;运算符，该运算符将用于将AEM服务器连接到Adobe Campaign。

   >[!CAUTION]
   >
   >默认情况下，不会为此运算符配置安全区域。 要通过AEM连接到Adobe Campaign，必须选择一个。
   >
   >在&#x200B;**serverConf.xml**&#x200B;文件中，必须将选定安全区域的&#x200B;**allowUserPassword**&#x200B;属性设置为&#x200B;**true**，以授权AEM通过登录/密码连接Adobe Campaign。
   >
   >我们强烈建议创建一个专用于AEM的安全区，以避免出现任何安全问题。 有关更多信息，请参阅[安装指南](https://docs.campaign.adobe.com/doc/AC/en/INS_Additional_configurations_Configuring_Campaign_server.html)。

   ![chlimage_1-134](assets/chlimage_1-134a.png)

### 配置AEM外部帐户{#configuring-an-aem-external-account}

您必须配置一个外部帐户，以便将Adobe Campaign连接到AEM实例。

>[!NOTE]
>
>* 安装&#x200B;**AEM Integration**&#x200B;包时，会创建外部AEM帐户。 您可以通过该实例配置与AEM实例的连接，也可以创建一个新实例。
>* 在AEM中，确保为campaign-remote用户设置密码。 您需要设置此密码才能将Adobe Campaign与AEM连接。 以管理员身份登录，在用户管理控制台中，搜索campaign-remote用户，然后单击&#x200B;**设置密码**。

>



要配置外部AEM帐户，请执行以下操作：

1. 转到&#x200B;**Administration** > **Platform** > **External Accounts**&#x200B;节点。
1. 创建新的外部帐户并选择&#x200B;**AEM**&#x200B;类型。
1. 输入AEM创作实例的访问参数：用于连接到此实例的服务器地址以及ID和密码。 campaign-api用户帐户密码与您在AEM中为设置密码的campaign-remote用户相同。

   >[!NOTE]
   >
   >确保服务器地址&#x200B;**不**&#x200B;以尾随斜杠结尾。 例如，输入`https://yourserver:4502`，而不是`https://yourserver:4502/`

   ![chlimage_1-135](assets/chlimage_1-135a.png) ![chlimage_1-136](assets/chlimage_1-136a.png)

1. 确保选中&#x200B;**Enabled**&#x200B;复选框。

### 验证AEMResourceTypeFilter选项{#verifying-the-aemresourcetypefilter-option}

**AEMResourceTypeFilter**&#x200B;选项用于筛选可在Adobe Campaign中使用的AEM资源类型。 这允许Adobe Campaign检索专门设计为仅在Adobe Campaign中使用的AEM内容。

此选项应进行预配置；但是，如果更改此选项，可能会导致集成无法正常运行。

要验证&#x200B;**AEMResourceTypeFilter**&#x200B;选项的配置情况：

1. 转到&#x200B;**Platform** >**Options**。
1. 在&#x200B;**AEMResourceTypeFilter**&#x200B;选项中，检查路径是否正确。 此字段必须包含值：

   **mcm/campaign/components/newsletter，mcm/campaign/components/campaign_newsletterpage，mcm/neolane/components/newsletter**

   或者在某些情况下，该值如下所示：

   **mcm/campaign/components/newsletter**

   ![chlimage_1-137](assets/chlimage_1-137a.png)

## 配置Adobe Experience Manager {#configuring-adobe-experience-manager}

要配置AEM，您必须执行以下操作：

* 配置实例之间的复制。
* 通过AEM将Cloud Services连接到Adobe Campaign。
* 配置外部器。

### 在AEM实例{#configuring-replication-between-aem-instances}之间配置复制

首先，从AEM创作实例创建的内容会发送到发布实例。 您需要进行发布，以便新闻稿中的图像可在发布实例上和新闻稿的收件人获得。 因此，必须将复制代理配置为从AEM创作实例复制到AEM发布实例。

>[!NOTE]
>
>如果您不想使用复制URL，而是使用面向公众的URL，则可以在OSGi的以下配置设置中设置&#x200B;**公共URL**(**AEM徽标** > **工具**&#x200B;图标> **操作** > **Web控制台** > **OSGi配置** **促销活动 — 配置**):
**公共URL:** com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl

要将某些创作实例配置复制到发布实例中，还需要执行此步骤。

要在AEM实例之间配置复制，请执行以下操作：

1. 在创作实例中，选择&#x200B;**AEM徽标**> **工具**&#x200B;图标> **部署** > **复制** > **创作上的代理**，然后单击&#x200B;**默认代理**。

   ![chlimage_1-138](assets/chlimage_1-138a.png)

   >[!NOTE]
   配置与Adobe Campaign的集成时，请避免使用localhost(AEM的本地副本)，除非发布和创作实例都位于同一台计算机上。

1. 点按或单击&#x200B;**编辑** ，然后选择&#x200B;**传输**&#x200B;选项卡。
1. 通过将&#x200B;**localhost**&#x200B;替换为AEM发布实例的IP地址或地址来配置URI。

   ![chlimage_1-139](assets/chlimage_1-139a.png)

### 将AEM连接到Adobe Campaign {#connecting-aem-to-adobe-campaign}

在将AEM和Adobe Campaign结合使用之前，您必须在两个解决方案之间建立链接，以便它们能够进行通信。

1. 连接到AEM创作实例。
1. 选择&#x200B;**AEM徽标** > **工具**&#x200B;图标> **部署** > **Cloud Services**，然后在Adobe Campaign部分中选择&#x200B;**立即配置**。

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. 通过输入&#x200B;**标题**&#x200B;并单击&#x200B;**创建**&#x200B;创建新配置，或选择要与Adobe Campaign实例链接的现有配置。
1. 编辑配置，使其与Adobe Campaign实例的参数匹配。

   * **用户名**: **aemserver**,Adobe Campaign AEM集成包运算符，用于在两个解决方案之间建立链接。
   * **密码**:Adobe Campaign aemserver操作员密码。您可能需要直接在Adobe Campaign中为此运算符重新指定密码。
   * **API端点**:Adobe Campaign实例URL。

1. 选择&#x200B;**连接到Adobe Campaign**&#x200B;并单击&#x200B;**确定**。

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   >[!NOTE]
   在[创建并发布电子邮件](/help/sites-authoring/campaign.md)后，您需要将配置重新发布到发布实例。

   ![chlimage_1-142](assets/chlimage_1-142a.png)

>[!NOTE]
如果连接失败，请确保检查以下内容：
* 使用到Adobe Campaign实例(https)的安全连接时，您可能会遇到证书问题。 您必须将Adobe Campaign实例证书添加到AEM实例JDK的&#x200B;**cacherts**&#x200B;文件中。
* 必须在Adobe Campaign中为[aemserver运算符](#connecting-aem-to-adobe-campaign)配置安全区域。 此外，在&#x200B;**serverConf.xml**&#x200B;文件中，必须将安全区域的&#x200B;**allowUserPassword**&#x200B;属性设置为&#x200B;**true**，以使用登录/密码模式授权AEM与Adobe Campaign的连接。

此外，请参阅[对AEM/Adobe Campaign集成进行故障诊断](/help/sites-administering/troubleshooting-campaignintegration.md)。

### 配置外部器{#configuring-the-externalizer}

您需要在创作实例的AEM中[配置外部器](/help/sites-developing/externalizer.md)。 外部器是一种OSGi服务，它允许您将资源路径转换为外部URL和绝对URL。 此服务提供了一个配置和构建这些外部URL的中心位置。

有关常规说明，请参阅[配置外部器](/help/sites-developing/externalizer.md)。 对于Adobe Campaign集成，请确保在`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`配置发布服务器，其位置不是`localhost:4503`，而是指向Adobe Campaign控制台可访问的服务器。

如果指向`localhost:4503`或Adobe Campaign无法访问的其他服务器，则您的图像将不会显示在Adobe Campaign控制台上。

![chlimage_1-143](assets/chlimage_1-143a.png)

## 高级配置{#advanced-configurations}

您还可以执行一些高级配置，即：

* 管理个性化字段和块。
* 停用个性化块。
* 管理Target扩展数据。

### 管理个性化字段和块{#managing-personalization-fields-and-blocks}

用于在AEM中向电子邮件内容添加个性化的字段和块由Adobe Campaign管理。

提供了默认列表，但可以修改。 您还可以添加或隐藏个性化字段和块。

#### 添加个性化字段{#adding-a-personalization-field}

要向已有可用的个性化字段添加新个性化字段，您必须按如下方式扩展Adobe Campaign **nms:seedMember**&#x200B;模式：

>[!CAUTION]
您需要添加的字段必须已通过收件人模式扩展(**nms:recipient**)添加。 有关详细信息，请参阅[Configuration](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Editing_schemas.html)指南。

1. 在Adobe Campaign导航中，转到&#x200B;**Administration** > **Configuration** > **Data schemas**&#x200B;节点。
1. 选择&#x200B;**新建**。

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. 在弹出窗口中，选择&#x200B;**使用扩展架构扩展表中的数据，然后单击**&#x200B;下一步&#x200B;**。**

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. 输入扩展架构的不同参数：

   * **架构**:选择 **nms:** seedMemberschema。窗口中的其他字段会自动填写。
   * **命名空间**:个性化扩展架构的命名空间。

1. 编辑架构的XML代码，以指定要添加到该架构的字段。 有关在Adobe Campaign中扩展架构的更多信息，请参阅[配置指南](https://docs.campaign.adobe.com/doc/AC6.1/en/CFG_Editing_schemas_Extending_a_schema.html)。
1. 保存您的架构，然后通过控制台中的&#x200B;**Tools** > **Advanced** > **Update database structure**&#x200B;菜单更新Adobe Campaign数据库结构。
1. 断开连接，然后重新连接到Adobe Campaign控制台以保存更改。 现在，新字段会显示在AEM中可用的个性化字段列表中。

#### 示例 {#example}

要添加&#x200B;**Registration Number**&#x200B;字段，您必须具有以下元素：

* **nms:recipient**&#x200B;模式扩展名为&#x200B;**cus:recipient**&#x200B;包含：

```xml
<element desc="Recipient table (profiles)" img="nms:recipient.png" label="Recipients" labelSingular="Recipient" name="recipient">

  <attribute dataPolicy="smartCase" desc="Recipient registration number"
  label="Registration Number"
  length="50" name="registrationNumber" type="string"/>

</element>
```

**nms:seedMember**&#x200B;模式扩展名为&#x200B;**cus:seedMember**，包含：

```xml
<element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">

  <element name="custom_nms_recipient">
    <attribute name="registrationNumber"
    template="cus:recipient:recipient/@registrationNumber"/>
  </element>

</element>
```

**注册编号**&#x200B;字段现在是可用个性化字段的一部分：

![chlimage_1-146](assets/chlimage_1-146.png)

#### 隐藏个性化字段{#hiding-a-personalization-field}

要在已有可用的个性化字段中隐藏个性化字段，必须扩展Adobe Campaign **nms:seedMember**&#x200B;模式，如[添加个性化字段](#adding-a-personalization-field)一节中所述。 应用以下步骤：

1. 复制您要从扩展架构（例如&#x200B;**cus:seedMember**）的&#x200B;**nms:seedMember**&#x200B;架构中获取的字段。
1. 将&#x200B;**advanced=&quot;true&quot;** XML属性添加到字段。 它不再显示在AEM中可用的个性化字段列表中。

   例如，要隐藏&#x200B;**Middle Name**&#x200B;字段，**cud:seedMember**&#x200B;架构必须包含以下元素：

   ```xml
   <element desc="Seed to insert in the export files" img="nms:unknownad.png" label="Seed addresses" labelSingular="Seed" name="seedMember">
   
     <element name="custom_nms_recipient">
       <attribute advanced="true" name="middleName"/>
     </element>
   
   </element>
   ```

### 停用个性化块{#deactivating-a-personalization-block}

要取消激活可用个性化块中的个性化块，请执行以下操作：

1. 在Adobe Campaign导航中，转到&#x200B;**资源** > **促销活动管理** > **个性化块**&#x200B;节点。
1. 选择要在AEM中停用的个性化块。
1. 清除自定义菜单&#x200B;**中的**&#x200B;可见复选框并保存更改。 块不再显示在Adobe Campaign中可用的个性化块列表中。

   ![chlimage_1-147](assets/chlimage_1-147a.png)

### 管理目标扩展数据{#managing-target-extension-data}

您还可以插入Target扩展数据以进行个性化。 Target扩展数据（也称为“Target数据”）来自于例如在营销活动工作流中扩充查询或在查询中添加数据。 有关更多信息，请参阅[创建查询](https://docs.campaign.adobe.com/doc/AC/en/PTF_Creating_queries_About_queries_in_Campaign.html)和[扩充数据](https://docs.campaign.adobe.com/doc/AC/en/WKF_Use_cases_Enriching_data.html)一节。

>[!NOTE]
只有将AEM内容与Adobe Campaign交付同步时，目标中的数据才可用。 请参阅[将AEM中创建的内容与Adobe Campaign的投放同步](/help/sites-authoring/campaign.md#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)。

![chlimage_1-148](assets/chlimage_1-148a.png)
