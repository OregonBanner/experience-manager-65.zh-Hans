---
title: 使用 Adobe Campaign 6.1 和 Adobe Campaign Standard
seo-title: 使用 Adobe Campaign 6.1 和 Adobe Campaign Standard
description: 您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理。
seo-description: 您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理。
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 67%

---

# 使用 Adobe Campaign 6.1 和 Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理。要执行此操作，您必须：

1. 在 AEM 中从特定于 Adobe Campaign 的模板创建新闻稿。
1. 在编辑内容之前，选择 [Adobe Campaign 服务](#selectingtheadobecampaigncloudservice)以便访问所有功能。
1. 编辑内容。
1. 验证内容。

之后，可以将内容与 Adobe Campaign 中的分发同步。本文档提供了相关详细说明。

>[!NOTE]
>
>在使用此功能之前，您必须先将 AEM 配置为与 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) 集成。

## 通过 Adobe Campaign 发送电子邮件内容  {#sending-email-content-via-adobe-campaign}

配置 AEM 和 Adobe Campaign 后，您可以直接在 AEM 中创建电子邮件分发内容，然后在 Adobe Campaign 中对其进行处理。

在AEM中创建Adobe Campaign内容时，必须先链接到Adobe Campaign服务，然后才能编辑内容以访问所有功能。

以下是两种可能的情况：

* 内容可以与 Adobe Campaign 中的分发同步。这使您能够在分发中使用 AEM 内容。
* （仅适用于 Adobe Campaign On Premise）内容可以直接发送到 Adobe Campaign，由其自动生成新的电子邮件分发。此模式存在限制。

本文档提供了相关详细说明。

### 创建新的电子邮件内容  {#creating-new-email-content}

>[!NOTE]
>
>添加电子邮件模板时，请务必在&#x200B;**/content/campaigns**&#x200B;下添加这些模板，以使其可用。


1. 在AEM中，选择&#x200B;**Websites**&#x200B;文件夹，然后浏览资源管理器以查找管理电子邮件促销活动的位置。 在以下示例中，相关节点为&#x200B;**网站** > **促销活动** > **Geometrixx Outdoors** > **电子邮件促销活动**。

   >[!NOTE]
   >
   >[仅 Geometrixx 中提供了电子邮件示例](/help/sites-developing/we-retail.md#weretail)。请从“包共享”中下载 Geometrixx 示例内容。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. 选择&#x200B;**新建** > **新建页面**&#x200B;以创建新的电子邮件内容。
1. 选择特定于 Adobe Campaign 的可用模板之一，然后填写页面的常规属性。默认情况下，有两种模板可用：

   * **Adobe Campaign 电子邮件 (AC 6.1)**：允许您先在预定义的模板中添加内容，然后再将其发送到 Adobe Campaign 6.1 以供分发。
   * **Adobe Campaign 电子邮件 (ACS)**：允许您先在预定义的模板中添加内容，然后再将其发送到 Adobe Campaign Standard 以供分发。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 单击&#x200B;**创建**&#x200B;以创建电子邮件或新闻稿。

### 选择 Adobe Campaign 云服务和模板 {#selecting-the-adobe-campaign-cloud-service-and-template}

要与 Adobe Campaign 集成，您需要将 Adobe Campaign 云服务添加到页面。通过执行此操作，您可以访问个性化设置和其他 Adobe Campaign 信息。

此外，您可能还需要选择 Adobe Campaign 模板，同时更改主题，并为那些不以 HTML 形式查看电子邮件的用户添加纯文本内容。

1. 在Sidekick中选择&#x200B;**页面**&#x200B;选项卡，然后选择&#x200B;**页面属性。**
1. 在弹出窗口的&#x200B;**云服务**&#x200B;选项卡中，选择&#x200B;**添加服务**&#x200B;以添加Adobe Campaign服务，然后单击&#x200B;**确定**。

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 从下拉列表中选择与您的 Adobe Campaign 实例相匹配的配置，然后单击&#x200B;**确定**。

   >[!NOTE]
   >
   >请务必在添加云服务后点按/单击&#x200B;**确定**&#x200B;或&#x200B;**应用**。这样才能正常使用 **Adobe Campaign** 选项卡。

1. 如果要应用特定的电子邮件投放模板(来自Adobe Campaign)，而不是默认的&#x200B;**mail**&#x200B;模板，请再次选择&#x200B;**页面属性**。 在&#x200B;**Adobe Campaign**&#x200B;选项卡中，输入电子邮件投放模板在相关Adobe Campaign实例中的内部名称。

   在 Adobe Campaign Standard 中，模板为&#x200B;**使用 AEM 内容的分发**。在 Adobe Campaign 6.1 中，模板为&#x200B;**使用 AEM 内容的电子邮件分发**。

   选择模板时， AEM会自动启用&#x200B;**Adobe Campaign Newsletter**&#x200B;组件。

### 编辑电子邮件内容 {#editing-email-content}

您可以在经典用户界面或触屏优化用户界面中编辑电子邮件内容。

1. 通过从工具箱中选择&#x200B;**页面属性** > **电子邮件**，输入电子邮件的主题和文本版本。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 通过从 Sidekick 中的可用元素中添加所需的元素，编辑电子邮件内容。要执行此操作，可拖放这些元素。然后，双击您要编辑的元素。

   例如，您可以添加包含个性化字段的文本。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   有关可用于 Adobe Campaign 新闻稿/电子邮件营销活动的组件的说明，请参阅 [Adobe Campaign 组件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 插入个性化 {#inserting-personalization}

编辑内容时，您可以插入：

* Adobe Campaign 上下文字段。这些字段可以插入到文本中，并根据收件人的数据（例如名字、姓氏或目标维度的任何数据）进行相应调整。
* Adobe Campaign 个性化基块。这些是与收件人数据无关的预定义内容块，例如品牌徽标或指向镜像页面的链接。

有关营销活动组件的完整说明，请参阅 [Adobe Campaign 组件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md)。

>[!NOTE]
>
>* 只会考虑 Adobe Campaign **配置文件**&#x200B;定位维度的字段。
>* 从&#x200B;**Sites**&#x200B;查看属性时，您无权访问Adobe Campaign上下文字段。 您可以在编辑时直接从电子邮件中访问这些字段。

>



1. 插入新的&#x200B;**Newsletter** > **文本与个性化（营销活动）**&#x200B;组件。
1. 双击该组件以将其打开。**编辑**&#x200B;窗口中提供了用于插入个性化元素的功能。

   >[!NOTE]
   >
   >可用的上下文字段与 Adobe Campaign 中的&#x200B;**配置文件**&#x200B;定位维度相对应。
   >
   >请参阅[将AEM页面链接到Adobe Campaign电子邮件](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail)。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 在Sidekick中选择&#x200B;**Client Context** ，以使用角色配置文件中的数据测试个性化字段。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 此时会显示一个窗口，您可以在其中选择所需的人物。个性化字段将自动替换为所选配置文件中的数据。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 预览新闻稿 {#previewing-a-newsletter}

您可以预览新闻稿的外观以及个性化。

1. 打开要预览的新闻稿，然后单击“预览”（放大镜）以缩小 Sidekick。
1. 单击其中一个电子邮件客户端图标，以查看新闻稿在每种电子邮件客户端中的外观。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 展开 Sidekick 以再次开始编辑。

### 在 AEM 中批准内容  {#approving-content-in-aem}

内容完成后，您可以启动批准流程。转到工具箱的&#x200B;**Workflow**&#x200B;选项卡，然后选择&#x200B;**批准Adobe Campaign**&#x200B;工作流。

该现成的工作流包含两个步骤：修订然后批准，或者修订然后拒绝。不过，可以扩展并调整此工作流以适应更复杂的过程。

![chlimage_1-182](assets/chlimage_1-182.png)

要批准Adobe Campaign的内容，请应用该工作流，方法是：在Sidekick中选择&#x200B;**Workflow**，然后选择&#x200B;**批准Adobe Campaign**，然后单击&#x200B;**启动工作流**。 完成各个步骤并批准该内容。您也可以拒绝该内容，方法是在上一个工作流步骤中选择&#x200B;**拒绝**&#x200B;而不是&#x200B;**批准**。

![chlimage_1-183](assets/chlimage_1-183.png)

内容获得批准后，它会在 Adobe Campaign 中显示为已批准。之后，便可以发送电子邮件。

在 Adobe Campaign Standard 中：

![chlimage_1-184](assets/chlimage_1-184.png)

在 Adobe Campaign 6.1 中：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>未经批准的内容可以与 Adobe Campaign 中的分发同步，但无法执行分发。只有经过批准的内容才可以通过营销活动分发来发送。

## 将 AEM 与 Adobe Campaign Standard 和 Adobe Campaign 6.1 链接  {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>有关详细信息，请参阅标准创作文档中[使用Adobe Campaign 6.1和Adobe Campaign Standard](/help/sites-authoring/campaign.md)下的[将AEM与Adobe Campaign Standard和Adobe Campaign 6.1](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic)关联。
