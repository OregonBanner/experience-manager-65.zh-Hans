---
title: 使用Adobe Campaign 6.1和Adobe Campaign Standard
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: 您可以在AEM中创建电子邮件内容，并在Adobe Campaign电子邮件中处理这些内容。
seo-description: You can create email content in AEM and process it in Adobe Campaign emails.
uuid: 439df7fb-590b-45b8-9768-565b022a808b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 61b2bd47-dcef-4107-87b1-6bf7bfd3043b
exl-id: a4717cb8-b70c-4150-b816-35e9b871e792
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# 使用Adobe Campaign 6.1和Adobe Campaign Standard{#working-with-adobe-campaign-and-adobe-campaign-standard}

您可以在AEM中创建电子邮件内容，并在Adobe Campaign电子邮件中处理这些内容。 为此，您必须：

1. 从特定于Adobe Campaign的模板在AEM中创建新的新闻稿。
1. 选择 [Adobe Campaign服务](#selectingtheadobecampaigncloudservice) 编辑内容以访问所有功能之前。
1. 编辑内容。
1. 验证内容。

然后，内容可以与Adobe Campaign中的投放同步。 本文档中介绍了详细说明。

>[!NOTE]
>
>在可以使用此功能之前，必须配置AEM以与以下任一功能集成 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## 通过Adobe Campaign发送电子邮件内容 {#sending-email-content-via-adobe-campaign}

配置AEM和Adobe Campaign后，您可以直接在AEM中创建电子邮件投放内容，然后在Adobe Campaign中处理该内容。

在AEM中创建Adobe Campaign内容时，必须先链接到Adobe Campaign服务，然后才能编辑内容以访问所有功能。

有两种可能的情况：

* 内容可以与Adobe Campaign中的投放同步。 这允许您在投放中使用AEM内容。
* (仅限Adobe Campaign内部部署)可以将内容直接发送到Adobe Campaign，后者自动生成新的电子邮件投放。 此模式具有限制。

本文档中介绍了详细说明。

### 创建新电子邮件内容 {#creating-new-email-content}

>[!NOTE]
>
>添加电子邮件模板时，请务必将其添加到 **/content/campaigns** 以便使用。

1. 在AEM中，选择 **网站** 文件夹，然后浏览资源管理器以查找管理电子邮件营销活动的位置。 在以下示例中，相关节点为 **网站** > **营销活动** > **Geometrixx Outdoors** > **电子邮件营销活动**.

   >[!NOTE]
   >
   >[电子邮件示例仅在Geometrixx中可用](/help/sites-developing/we-retail.md#weretail). 请从包共享下载示例Geometrixx内容。

   ![chlimage_1-172](assets/chlimage_1-172.png)

1. 选择 **新** > **新页面** 以创建新的电子邮件内容。
1. 选择特定于Adobe Campaign的可用模板之一，然后填写页面的一般属性。 默认情况下，有三个模板可用：

   * **Adobe Campaign电子邮件(AC 6.1)**：允许您将内容添加到预定义模板，然后再发送到Adobe Campaign 6.1进行交付。
   * **Adobe Campaign电子邮件(ACS)**：允许您将内容添加到预定义模板，然后再发送给Adobe Campaign Standard进行交付。

   ![chlimage_1-173](assets/chlimage_1-173.png)

1. 单击 **创建** 创建电子邮件或新闻稿。

### 选择Adobe Campaign云服务和模板 {#selecting-the-adobe-campaign-cloud-service-and-template}

要与Adobe Campaign集成，您需要将Adobe Campaign云服务添加到页面。 这样，您就可以访问个性化和其他Adobe Campaign信息。

此外，您可能还需要选择Adobe Campaign模板，并更改主题，为那些不会在HTML中查看电子邮件的用户添加纯文本内容。

1. 选择 **页面** 在sidekick中选项卡，然后选择 **页面属性。**
1. 在 **云服务** 选项卡，选择 **添加服务** 添加Adobe Campaign服务并单击 **确定**.

   ![chlimage_1-174](assets/chlimage_1-174.png)

1. 从下拉列表中选择与您的Adobe Campaign实例匹配的配置，然后单击 **确定**.

   >[!NOTE]
   >
   >确保点按/单击 **确定** 或 **应用** 添加云服务之后。 这样可启用 **Adobe Campaign** 按Tab键以正常工作。

1. 如果要应用默认模板以外的特定电子邮件投放模板(来自Adobe Campaign) **邮件** 模板，选择 **页面属性** 再来一次。 在 **Adobe Campaign** 选项卡，在相关的Adobe Campaign实例中输入电子邮件投放模板的内部名称。

   在Adobe Campaign Standard中，模板为 **通过AEM内容投放**. 在Adobe Campaign 6.1中，模板是 **包含AEM内容的电子邮件投放**.

   选择模板后，AEM会自动启用 **Adobe Campaign新闻稿** 组件。

### 编辑电子邮件内容 {#editing-email-content}

您可以在经典用户界面或触控优化用户界面中编辑电子邮件内容。

1. 通过选择输入电子邮件的主题和文本版本 **页面属性** > **电子邮件** 从工具箱中。

   ![chlimage_1-175](assets/chlimage_1-175.png)

1. 通过添加您希望Sidekick中可用的元素来编辑电子邮件内容。 要执行此操作，请拖放它们。 然后双击要编辑的元素。

   例如，您可以添加包含个性化字段的文本。

   ![chlimage_1-176](assets/chlimage_1-176.png)

   参见 [Adobe Campaign组件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) 有关Adobe Campaign新闻稿/电子邮件营销活动可用组件的说明。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 插入个性化 {#inserting-personalization}

编辑内容时，您可以插入：

* Adobe Campaign上下文字段。 这些字段可插入文本中，并根据收件人的数据（例如名字、姓氏或目标维度的任何数据）进行调整。
* Adobe Campaign个性化块。 这些是与收件人数据无关的预定义内容块，例如品牌徽标或指向镜像页面的链接。

参见 [Adobe Campaign组件](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md) 有关Campaign组件的完整说明。

>[!NOTE]
>
>* 仅Adobe Campaign的字段 **配置文件** 定向维度已考虑在内。
>* 从查看属性时 **站点**&#x200B;中，您无权访问Adobe Campaign上下文字段。 编辑时，您可以直接从电子邮件访问这些内容。
>


1. 插入新内容 **新闻稿** > **文本和个性化（营销活动）** 组件。
1. 双击组件以将其打开。 此 **编辑** 窗口具有一项功能，可让您插入个性化元素。

   >[!NOTE]
   >
   >可用的上下文字段对应于 **配置文件** Adobe Campaign中的“定位”维度。
   >
   >参见 [将AEM页面关联到Adobe Campaign电子邮件](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#linkinganaempagetoanadobecampaignemail).

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 选择 **客户端上下文** 在sidekick中使用角色配置文件中的数据测试个性化字段。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 此时将显示一个窗口，允许您选择所需的角色。 个性化字段会自动替换为所选配置文件中的数据。

   ![chlimage_1-180](assets/chlimage_1-180.png)

### 预览新闻稿 {#previewing-a-newsletter}

您可以预览新闻稿的外观以及预览个性化。

1. 打开要预览的新闻稿，然后单击“预览”（放大镜）缩小sidekick。
1. 单击其中一个电子邮件客户端图标，可查看您的新闻稿在每个电子邮件客户端中的外观。

   ![chlimage_1-181](assets/chlimage_1-181.png)

1. 展开sidekick以再次开始编辑。

### 在AEM中审批内容 {#approving-content-in-aem}

内容完成后，您可以开始审批流程。 转到 **工作流** 标签并选取 **批准Adobe Campaign** 工作流。

此现成的工作流包含两个步骤：依次进行修订和批准，或者依次进行修订和拒绝。 然而，该工作流可以扩展并适应更复杂的过程。

![chlimage_1-182](assets/chlimage_1-182.png)

要批准Adobe Campaign的内容，请选择以应用工作流 **工作流** 在副球上选择 **批准Adobe Campaign** 并单击 **启动工作流**. 完成相关步骤并批准内容。 您还可以通过选择拒绝内容 **拒绝** 而不是 **批准** 在最后一个工作流步骤中。

![chlimage_1-183](assets/chlimage_1-183.png)

内容获得批准后，在Adobe Campaign中显示为“已批准”。 然后可以发送电子邮件。

在Adobe Campaign Standard中：

![chlimage_1-184](assets/chlimage_1-184.png)

在Adobe Campaign 6.1中：

![chlimage_1-185](assets/chlimage_1-185.png)

>[!NOTE]
>
>未批准的内容可以与Adobe Campaign中的投放同步，但投放无法执行。 只能通过Campaign投放发送已批准的内容。

## 将AEM与Adobe Campaign Standard和Adobe Campaign 6.1关联 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign}

>[!NOTE]
>
>参见 [将AEM与Adobe Campaign Standard和Adobe Campaign 6.1关联](/help/sites-authoring/campaign.md#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic) 下 [使用Adobe Campaign 6.1和Adobe Campaign Standard](/help/sites-authoring/campaign.md) 详细信息，请参阅标准创作文档。
