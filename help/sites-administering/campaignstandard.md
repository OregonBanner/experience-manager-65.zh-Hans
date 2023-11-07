---
title: 将AEM 6.5与Adobe Campaign Standard集成
description: 了解如何将AEM 6.5与Adobe Campaign Standard集成。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: caa43d80-1f38-46fc-a8b9-9485c235c0ca
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 17%

---


# 将AEM 6.5与Adobe Campaign Standard集成 {#integrating-with-adobe-campaign-standard}

通过将AEM 6.5与Adobe Campaign Standard (ACS)集成，您可以直接在AEM中管理电子邮件投放、内容和表单。 需要同时执行Adobe Campaign Standard和AEM的配置步骤才能在解决方案之间实现双向通信。

此集成允许单独使用AEM和Adobe Campaign Standard。 营销人员可以在Adobe Campaign中创建活动并使用定位，而内容创建者则可以同时在AEM中进行内容设计。 借助该集成，Adobe Campaign可以定位和交付在AEM中创建的营销活动的内容和设计。

>[!INFO]
>
>本文档详细介绍如何将Adobe Campaign Standard与AEM 6.5集成。有关其他Campaign集成，请参阅文档 [将AEM 6.5与Adobe Campaign集成。](campaign.md)

## 集成步骤 {#integration-steps}

配置AEM与Adobe Campaign Standard之间的集成需要在这两个解决方案中执行多个步骤。

1. [配置 ](#aemserver-user)
1. [验证 ](#resource-type-filter)
1. [在Campaign中创建特定于AEM的电子邮件投放模板](#aem-email-delivery-template)
1. [在AEM中配置Campaign集成](#campaign-integration)
1. [配置到AEM发布实例的复制](#replication)
1. [配置 AEM 外部化器](#externalizer)
1. [配置 ](#campaign-remote-user)
1. [在Campaign中配置AEM外部帐户](#acc-external-user)

本文档将详细介绍每一个步骤.

## 前提条件 {#prerequisites}

* Adobe Campaign Standard的管理员访问权限
   * 如果您需要有关如何设置和配置Adobe Campaign Standard的更多详细信息，请参阅 [Adobe Campaign Standard文档。](https://experienceleague.adobe.com/docs/campaign-standard/using/campaign-standard-home.html)
* 管理员访问AEM

## 在Campaign中配置aemserver用户 {#aemserver-user}

默认情况下，Adobe Campaign Standard附带 `aemserver` AEM用于连接到Adobe Campaign的用户。 您必须为此用户分配适当的安全组并设置其密码。

1. 以管理员身份登录Adobe Campaign。

1. 点按或单击菜单栏左上角的Adobe Campaign徽标以打开全局导航，然后选择 **管理** > **用户和安全性** > **用户** 导航菜单。

1. 点按或单击 `aemserver` 用户控制台中的用户。

1. 确保 `aemserver` 至少将用户分配给具有角色的安全组 `deliveryPrepare` 分配给它。 默认情况下，组 `Standard Users` 具有此角色。

   ![Adobe Campaign中的aemserver用户](assets/acs-aemserver-user.png)

1. 点击或单击&#x200B;**保存**&#x200B;以保存更改。

您的 `aemserver` 用户现在拥有必要的权限，以便AEM可以使用该权限与Adobe Campaign通信。

但是，在AEM可以使用 `aemserver` 用户，必须设置其密码。 这不能通过Adobe Campaign完成。 必须由Adobe支持工程师执行。 [向Adobe客户关怀部门提交票证](https://experienceleague.adobe.com/?support-tab=home#support) 请求重置 `aemserver` 密码。 获得Adobe客户关怀团队提供的密码后，请将其保存在安全位置。

## 验证Campaign中的AEMResourceTypeFilter {#resource-type-filter}

此 `AEMResourceTypeFilter` 是Adobe Campaign中的一个选项，用于筛选可以在Adobe Campaign中使用的AEM资源。 由于AEM包含大量内容，因此此选项将用作过滤器，允许Adobe Campaign仅检索专门设计用于Adobe Campaign的类型的AEM内容。

此选项是预配置的。 但是，如果您自定义了AEM的Campaign组件，则可能需要更新它。 验证 `AEMResourceTypeFilter` 选项，请按照以下步骤操作。

1. 以管理员身份登录Adobe Campaign。

1. 点按或单击菜单栏左上角的Adobe Campaign徽标以打开全局导航，然后选择 **管理** > **应用程序设置** > **选项** 导航菜单。

1. 点按或单击 `AEMResourceTypeFilter` 在选项控制台中。

1. 确认配置 `AEMResourceTypeFilter`. 路径以逗号分隔，默认包含：

   * `mcm/campaign/components/newsletter`
   * `mcm/campaign/components/campaign_newsletterpage`
   * `mcm/neolane/components/newsletter`

   ![AEMResourceTypeFilter](assets/acs-aem-resource-type-filter.png)

1. 点击或单击&#x200B;**保存**&#x200B;以保存更改。

您的 `AEMResourceTypeFilter` 现在配置为从AEM检索正确的内容。

## 在Campaign中创建特定于AEM的电子邮件投放模板 {#aem-email-delivery-template}

默认情况下，Adobe Campaign的电子邮件模板中未启用AEM。 您必须配置新的电子邮件投放模板，该模板可用于使用AEM内容创建电子邮件。 要创建特定于AEM的电子邮件投放模板，请执行以下步骤。

1. 以管理员身份登录Adobe Campaign。

1. 点按或单击菜单栏左上角的Adobe Campaign徽标以打开全局导航，然后选择 **资源** > **模板** > **投放模板** 导航菜单。

1. 在投放模板控制台中，找到默认电子邮件模板 **通过电子邮件发送（邮件）** 然后将鼠标悬停在表示该卡的卡或线上，可显示相应的选项。 单击 **重复元素**.

   ![重复元素](assets/acs-copy-template.png)

1. 在 **确认** 对话框，请单击 **确认** 以复制模板。

   ![确认对话框](assets/acs-confirmation.png)

1. 此时将打开模板编辑器，其中显示您的 **通过电子邮件发送（邮件）** 模板。 单击 **编辑属性** 图标（位于窗口的右上方）。

   ![模板编辑器](assets/acs-template-editor.png)

1. 在属性窗口中，更改 **标签** 字段以描述新的AEM模板。

1. 单击 **内容** 标题以将其展开并选择 **Adobe Experience Manager** 在 **内容源** 下拉菜单。

1. 这会显示 **Adobe Experience Manager帐户** 字段。 使用下拉菜单选择 **Adobe Experience Manager实例(aemInstance)** 用户。 这是AEM集成的默认外部用户。

![配置模板属性](assets/acs-template-properties.png)

1. 单击 **确认** 以保存对属性所做的更改。

1. 在模板编辑器中，单击 **保存** 保存修改后的电子邮件模板副本，以用于AEM。

现在，您有一个可以使用AEM内容的电子邮件模板。

## 在AEM中配置Campaign集成 {#campaign-integration}

AEM使用内置集成与Adobe Campaign进行通信，并且 `aemserver` 您在Adobe Campaign中配置的用户。 按照以下步骤配置此集成。

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧栏中，选择&#x200B;**“工具”**>**“Cloud Service”**＞**“传统 Cloud Service”**>**“Adobe Campaign”**，然后单击&#x200B;**“立即配置”**。

   ![配置 Adobe Campaign](assets/configure-campaign-service.png)

1. 在对话框中，通过输入&#x200B;**“标题”**&#x200B;并单击&#x200B;**“创建”**&#x200B;来创建 Campaign 服务配置。

   ![配置 Campaign 对话框](assets/configure-campaign-dialog.png)

1. 会打开新窗口和对话框会，用以编辑配置。 提供必要的信息。

   * **用户名**  — 这是 [该 `aemserver` 您在上一步中配置的Adobe Campaign中的用户。](#aemserver-user)默认情况下，这是 `aemserver`。
   * **密码**  — 这是的密码 [该 `aemserver` 您在上一步中从Adobe客户关怀部门请求的Adobe Campaign中的用户。](#aemserver-user)
   * **API 端点** – 这是 Adobe Campaign 实例 URL。

   ![在 AEM 中配置 Adobe Campaign](assets/configure-campaign.png)

1. 选择&#x200B;**“连接到 Adobe Campaign”**&#x200B;以验证连接，然后单击&#x200B;**确定**。

AEM 现在可以与 Adobe Campaign 通信。

>[!NOTE]
>
>确保您的 Adobe Campaign 服务器可以通过 Internet 访问。AEM无法访问专用网络。

## 配置到AEM发布实例的复制 {#replication}

Campaign内容由内容作者在AEM创作实例上创建。 此实例通常仅在贵组织内部可用。 要使营销活动的收件人能够访问图像和资产等内容，您需要发布该内容。

复制代理负责将内容从AEM创作实例发布到发布实例，必须设置该代理才能使集成正常工作。 此外，还需要执行此步骤以将某些创作实例配置复制到发布实例。

要配置从AEM创作实例到发布实例的复制，请执行以下操作：

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧边栏中，选择 **工具** > **部署** > **复制** > **作者代理**，然后点按或单击 **默认代理（发布）**.

   ![配置复制代理](assets/acc-replication-config.png)

1. 点击或单击 **编辑** 然后选择 **传输** 选项卡。

1. 配置 **URI** 字段，以替换默认值 `localhost` 值为AEM发布实例的IP地址。

   ![“传输”选项卡](assets/acc-transport-tab.png)

1. 点击或单击 **确定** 保存对代理设置所做的更改。

您已配置复制到AEM发布实例，以便活动收件人可以访问您的内容。

>[!NOTE]
>
>如果您不想使用复制URL，而是使用面向公众的URL，则可以通过OSGi在下面的配置设置中设置公共URL
>
>从全局导航侧边栏中，选择 **工具** > **操作** > **Web控制台** > **OSGi配置** 和搜索 **AEM Campaign集成 — 配置**. 编辑配置并更改字段 **公共URL** (`com.day.cq.mcm.campaign.impl.IntegrationConfigImpl#aem.mcm.campaign.publicUrl`)。

## 配置 AEM 外部化器 {#externalizer}

[外部化器是 AEM 中的一个 OSGi 服务，它可将资源路径转换为外部和绝对 URL，这是 AEM 提供 Campaign 可以使用的内容所必需的。](/help/sites-developing/externalizer.md)您必须对其进行配置以使Campaign集成正常工作。

1. 以管理员身份登录到 AEM 创作实例。
1. 从全局导航侧边栏中，选择 **工具** > **操作** > **Web控制台** > **OSGi配置** 和搜索 **Day CQ链接外部化器**.
1. 默认情况下， **域** 字段适用于发布实例。 更改URL的默认设置 `http://localhost:4503` 发布实例来进行其他更改。

   ![配置外部化器](assets/acc-externalizer-config.png)

1. 点按或单击&#x200B;**保存**。

您已配置外部化器，Adobe Campaign现在可以访问您的内容。

>[!NOTE]
>
发布实例必须可以从 Adobe Campaign 服务器中访问。如果它指向 `localhost:4503` 或者Adobe Campaign无法访问的其他服务器，来自AEM的图像将不会显示在Adobe Campaign控制台中。

## 在AEM中配置活动远程用户 {#campaign-remote-user}

正如AEM在Adobe Campaign中需要用户可以与Adobe Campaign通信一样，Adobe Campaign也需要AEM中的用户才能与AEM通信。 默认情况下，Campaign集成会创建 `campaign-remote` user in AEM. 按照以下步骤配置此用户。

1. 以管理员身份登录 AEM。
1. 在主导航控制台上，单击左栏中的&#x200B;**“工具”**。
1. 然后单击 **安全性** > **用户** 以打开用户管理控制台。
1. 找到`campaign-remote`用户。
1. 选择`campaign-remote`用户，然后单击&#x200B;**“属性”**&#x200B;来编辑用户。
1. 在&#x200B;**“编辑用户设置”**&#x200B;窗口中，单击&#x200B;**“更改密码”**。
1. 为用户提供新密码，并将密码记在安全位置以备将来使用。
1. 单击&#x200B;**“保存”**&#x200B;以保存密码更改。
1. 单击&#x200B;**“保存并关闭”**&#x200B;以将更改保存到`campaign-remote`用户。

## 在Campaign中配置AEM外部帐户 {#acc-external-user}

当您 [创建了一个特定于AEM的电子邮件投放模板，](#aem-email-delivery-template) 您已指定模板应使用 `aemInstance` 用于与AEM通信的外部帐户。 要启用这两种解决方案之间的双向通信，您需要在Adobe Campaign中配置此帐户。

1. 以管理员身份登录Adobe Campaign。

1. 点按或单击菜单栏左上角的Adobe Campaign徽标以打开全局导航，然后选择 **管理** > **应用程序设置** > **外部帐户** 导航菜单。

1. 点按或单击 **Adobe Experience Manager实例(aemInstance)** 用户控制台中的用户。

1. 确保用户具有 **Adobe Experience Manager** 作为 **类型**.

1. 在 **连接** 部分，定义以下字段：

   1. 服务器：这是AEM创作服务器的URL。 不应以斜杠结尾。
   1. 帐户：这是 `campaign-remote` 使用您 [之前在AEM中配置。](#campaign-remote-user)
   1. 密码：此密码用于 `campaign-remote`使用您 [之前在AEM中配置。](#campaign-remote-user)

   ![编辑aemInstance用户](assets/acs-external-acount-editor.png)

1. 确保 **已启用** 复选框，然后单击 **保存** 以保存更改。

恭喜！您已完成AEM与Adobe Campaign Standard之间的集成！

## 后续步骤 {#next-steps}

在配置Adobe Campaign Classic和AEM后，集成现已完成。

您现在可以通过继续阅读[本文档](/help/sites-authoring/campaign.md)学习如何在 Adobe Experience Manager 中创建新闻稿。
