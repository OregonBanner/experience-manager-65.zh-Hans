---
title: 使用Adobe Campaign Classic和Adobe Campaign Standard
seo-title: Working with Adobe Campaign 6.1 and Adobe Campaign Standard
description: 您可以在AEM中创建电子邮件内容，并在Adobe Campaign电子邮件中处理这些内容
seo-description: You can create email content in AEM and process it in Adobe Campaign emails
uuid: 23195f0b-71c0-4554-8c8b-b0e7704d71d7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 2fd0047d-d0f6-4289-98cf-454486f9cd61
exl-id: d7e4d424-0ca7-449f-95fb-c4fe19dd195d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2758'
ht-degree: 0%

---

# 使用Adobe Campaign Classic和Adobe Campaign Standard{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

您可以在AEM中创建电子邮件内容，并在Adobe Campaign电子邮件中处理这些内容。 为此，您必须：

1. 从特定于Adobe Campaign的模板在AEM中创建新的新闻稿。
1. 选择 [Adobe Campaign服务](#selecting-the-adobe-campaign-cloud-service-and-template) 编辑内容以访问所有功能之前。
1. 编辑内容。
1. 验证内容。

然后，内容可以与Adobe Campaign中的投放同步。 本文档中介绍了详细说明。

另请参阅 [在AEM中创建Adobe Campaign Forms](/help/sites-authoring/adobe-campaign-forms.md).

>[!NOTE]
>
>在可以使用此功能之前，必须配置AEM以与以下任一功能集成 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md).

## 通过Adobe Campaign发送电子邮件内容 {#sending-email-content-via-adobe-campaign}

配置AEM和Adobe Campaign后，您可以直接在AEM中创建电子邮件投放内容，然后在Adobe Campaign中处理该内容。

在AEM中创建Adobe Campaign内容时，必须先链接到Adobe Campaign服务，然后才能编辑内容以访问所有功能。

有两种可能的情况：

* 内容可以与Adobe Campaign中的投放同步。 这允许您在投放中使用AEM内容。
* (仅限Adobe Campaign Classic)可以将内容直接发送到Adobe Campaign，后者自动生成新的电子邮件投放。 此模式具有限制。

本文档中介绍了详细说明。

### 创建新电子邮件内容 {#creating-new-email-content}

>[!NOTE]
>
>添加电子邮件模板时，请务必将其添加到 **/content/campaigns** 以便使用。

#### 创建新电子邮件内容 {#creating-new-email-content-1}

1. 在AEM中，选择 **站点** 则 **营销活动**，然后浏览到管理电子邮件营销活动的位置。 在以下示例中，路径为 **站点** > **营销活动** > **Geometrixx Outdoors** > **电子邮件营销活动**.

   >[!NOTE]
   >
   >[电子邮件示例仅在Geometrixx中可用](/help/sites-developing/we-retail.md). 请从包共享下载示例Geometrixx内容。

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. 选择 **创建** 则 **创建页面**.
1. 选择您连接到Adobe Campaign的特定可用模板之一，然后单击 **下一个**. 默认情况下，有三个模板可用：

   * **Adobe Campaign Classic电子邮件**：用于将内容在发送到Adobe Campaign Classic进行交付之前添加到预定义模板（两列）。
   * **Adobe Campaign Standard电子邮件**：用于将内容在发送到Adobe Campaign Standard进行交付之前添加到预定义模板（两列）。

1. 填写 **标题** 以及（可选） **描述** 并单击 **创建**. 标题用作新闻稿/电子邮件的主题，除非您在编辑电子邮件时覆盖它。

### 选择Adobe Campaign云服务和模板 {#selecting-the-adobe-campaign-cloud-service-and-template}

要与Adobe Campaign集成，您需要将Adobe Campaign云服务添加到页面。 这样，您就可以访问个性化和其他Adobe Campaign信息。

此外，您可能还需要选择Adobe Campaign模板，并更改主题，为那些不会在HTML中查看电子邮件的用户添加纯文本内容。

您可以从以下任一位置选择云服务 **站点** 选项卡，或者在创建后从电子邮件/新闻稿中访问。

从中选择云服务 **站点** 推荐的方法是tab键。 从电子邮件/新闻稿中选择云服务需要一种解决方法。

从 **站点** 页面：

1. 在AEM中，选择电子邮件页面并单击 **查看属性**.

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 选择 **编辑** 然后 **云服务** Tab键并向下滚动到底部，单击+号以添加配置，然后选择 **Adobe Campaign**.

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. 从下拉列表中选择与您的Adobe Campaign实例匹配的配置，然后单击进行确认 **保存**.
1. 您可以通过单击&#x200B;**Adobe Campaign** 选项卡。 如果要选择其他模板，您可以在编辑时从电子邮件中访问该模板。

   如果要应用默认邮件模板以外的特定电子邮件投放模板(来自Adobe Campaign)，请在 **属性**，选择 **Adobe Campaign** 选项卡。 在相关的Adobe Campaign实例中输入电子邮件投放模板的内部名称。

   您选择的模板决定了Adobe Campaign中可用的个性化字段。

   ![chlimage_1-18](assets/chlimage_1-18a.png)

在创作时从新闻稿/电子邮件中，您可能无法选择中的Adobe Campaign云服务配置 **页面属性** 由于布局问题。 您可以使用此处描述的解决方法：

1. 在AEM中，选择电子邮件页面并单击 **编辑**. 单击 **打开属性**.

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. 选择 **云服务** 并单击 **+** 以添加配置。 选择任何可见的配置（无论哪个配置）。 单击或点按 **+** 签名以添加其他配置，然后选择 **Adobe Campaign**.

   >[!NOTE]
   >
   >或者，您可以通过选择 **查看属性** 在 **站点** 选项卡。

1. 从下拉列表中选择与您的Adobe Campaign实例匹配的配置，删除您创建的不适用于Adobe Campaign的第一个配置，然后单击复选标记进行确认。
1. 继续上一过程中的步骤4，选择模板并添加纯文本。

### 编辑电子邮件内容 {#editing-email-content}

要编辑电子邮件内容，请执行以下操作：

1. 打开电子邮件，并默认进入编辑模式。

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. 如果要更改电子邮件的主题或为那些不会在HTML中查看电子邮件的用户添加纯文本，请选择 **电子邮件** 并添加主题和文本。 选择页面图标以从HTML自动生成纯文本版本。 完成后，单击复选标记。

   您可以使用Adobe Campaign个性化字段对新闻稿进行个性化。 要添加个性化字段，请单击显示Adobe Campaign徽标的按钮以打开个性化字段选取器。 然后，您可以从可用于此新闻稿的所有字段中进行选择。

   >[!NOTE]
   >
   >如果编辑器中的属性中的个性化字段显示为灰色，请重新检查您的配置。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. 打开屏幕左侧的组件面板，然后选择 **Adobe Campaign新闻稿** 以查找这些组件。

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 将组件直接拖动到页面上，并相应地编辑它们。 例如，您可以拖动 **文本和个性化（营销活动）** 组件并添加个性化文本。

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   参见 [Adobe Campaign组件](/help/sites-authoring/adobe-campaign-components.md) 以了解每个组件的详细说明。

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### 插入个性化 {#inserting-personalization}

编辑内容时，您可以插入：

* Adobe Campaign上下文字段。 这些字段可插入文本中，并根据收件人的数据（例如名字、姓氏或目标维度的任何数据）进行调整。
* Adobe Campaign个性化块。 这些是与收件人数据无关的预定义内容块，例如品牌徽标或指向镜像页面的链接。

参见 [Adobe Campaign组件](/help/sites-authoring/adobe-campaign-components.md) 有关Campaign组件的完整说明。

>[!NOTE]
>
>* 仅Adobe Campaign的字段 **配置文件** 定向维度已考虑在内。
>* 从查看属性时 **站点**&#x200B;中，您无权访问Adobe Campaign上下文字段。 编辑时，您可以直接从电子邮件访问这些内容。


要插入个性化设置，请执行以下操作：

1. 插入新内容 **新闻稿** > **文本和个性化（营销活动）** 组件，方法是将其拖动到页面上。

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 单击铅笔图标以打开组件。 将打开就地编辑器。

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**对于Adobe Campaign Standard：**
   >
   >* 可用的上下文字段对应于 **配置文件** Adobe Campaign中的“定位”维度。
   >* 参见 [将AEM页面关联到Adobe Campaign电子邮件](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard).

   >
   >**对于Adobe Campaign Classic：**
   >
   >* 可用的上下文字段会从Adobe Campaign中动态恢复 **nms：seedMember** 架构。 目标扩展数据可从包含与内容同步的投放的工作流中动态恢复。 (请参阅 [将AEM中创建的内容与Adobe Campaign中的投放同步](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic) 部分)。
   >
   >* 要添加或隐藏个性化元素，请参阅 [管理个性化字段和块](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks).
   >* **重要**：所有种子表字段还必须位于收件人表（或相应的联系人表）中。


1. 通过键入插入文本。 通过单击Adobe Campaign组件并选择它们来插入上下文字段或个性化块。 完成后，选中复选标记。

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   插入上下文字段或个性化块后，您可以预览新闻稿并测试字段。 参见 [预览新闻稿](#previewing-a-newsletter).

### 预览新闻稿 {#previewing-a-newsletter}

您可以预览新闻稿的外观以及预览个性化。

1. 在新闻稿打开时，单击 **预览** 在AEM的右上角。 AEM显示用户收到新闻稿时的外观。

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >如果您使用Adobe Campaign Standard并使用示例模板，则显示初始内容的两个个性化块 —  **&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** 和 **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;**  — 在交付期间导入内容时将引发错误。 您可以使用个性化块选取器选择相应的块来调整这些内容。

1. 要预览个性化，请单击/点按工具栏中的相应图标以打开ContextHub。 个性化字段标记现在由所选角色的种子数据替换。 了解在ContextHub中切换角色时，变量如何适应。

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. 您可以查看来自Adobe Campaign且与当前所选角色关联的种子数据。 为此，请单击/点按ContextHub栏中的Adobe Campaign模块。 这将打开一个对话框，其中显示当前配置文件的所有种子数据。 同样，当切换到其他角色时，数据会进行相应的调整。

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### 在AEM中审批内容 {#approving-content-in-aem}

内容完成后，您可以开始审批流程。 转到 **工作流** 标签并选取 **批准Adobe Campaign** 工作流。

此现成的工作流包含两个步骤：依次进行修订和批准，或者依次进行修订和拒绝。 然而，该工作流可以扩展并适应更复杂的过程。

![chlimage_1-31](assets/chlimage_1-31a.png)

要批准Adobe Campaign的内容，请选择以应用工作流 **工作流** 和选择 **批准Adobe Campaign** 并单击 **启动工作流**. 完成相关步骤并批准内容。 您还可以通过选择拒绝内容 **拒绝** 而不是 **批准** 在最后一个工作流步骤中。

![chlimage_1-32](assets/chlimage_1-32a.png)

内容获得批准后，在Adobe Campaign中显示为“已批准”。 然后可以发送电子邮件。

在Adobe Campaign Standard中：

![chlimage_1-33](assets/chlimage_1-33a.png)

在Adobe Campaign Classic中：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
未批准的内容可以与Adobe Campaign中的投放同步，但投放无法执行。 只能通过Campaign投放发送已批准的内容。

## 将AEM与Adobe Campaign Standard和Adobe Campaign Classic关联 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

如何将AEM与Adobe Campaign链接或同步取决于您使用的是基于订阅的Adobe Campaign Standard还是基于内部部署的Adobe Campaign Classic。

有关基于您的Adobe Campaign解决方案的说明，请参阅以下部分：

* [将AEM页面关联到Adobe Campaign电子邮件(Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [将AEM中创建的内容与Adobe Campaign Classic中的投放同步](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### 将AEM页面关联到Adobe Campaign电子邮件(Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard允许您恢复在AEM中创建的内容并将其链接到以下内容：

* 电子邮件。
* 电子邮件模板。

这样做可以让您交付内容。 您可以看到新闻稿是否通过页面上显示的代码链接到单个投放。

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
如果新闻稿链接到多个投放，则会显示链接投放的数量（但并非显示每个ID）。

要将在AEM中创建的页面链接到来自Adobe Campaign的电子邮件，请执行以下操作：

1. 根据AEM特定的电子邮件模板创建新电子邮件。 请参阅 [在Adobe Campaign Standard中创建电子邮件](https://helpx.adobe.com/campaign/standard/channels/using/creating-an-email.html) 了解更多信息。

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 打开 **内容** 阻止投放。

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. 选择 **与Adobe Experience Manager内容链接** 以访问AEM中可用的内容列表。

   >[!NOTE]
   如果 **与Adobe Experience Manager链接** 选项不会出现在操作栏中，请检查 **内容编辑模式** 已正确配置，设置为 **Adobe Experience Manager** 在电子邮件属性中。

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 选择要在电子邮件中使用的内容。

   此列表指定：

   * AEM中内容的标签。
   * AEM中内容的审批状态。 如果内容未获得批准，您可以同步内容，但必须在发送投放之前批准该内容。 但是，您可以执行某些操作，例如发送验证或预览测试。
   * 上次修改内容的日期。
   * 任何已链接到投放的内容。

   >[!NOTE]
   默认情况下，已与投放同步的内容处于隐藏状态。 但是，您可以显示并使用它。 例如，如果您希望将内容用作多个投放的模板。

   当电子邮件链接到AEM内容时，无法在Adobe Campaign中编辑该内容。

1. 从仪表板（受众、执行计划）指定电子邮件的其他参数。
1. 执行电子邮件投放。 在投放分析期间，将检索AEM内容的最新版本。

   >[!NOTE]
   如果内容在链接到电子邮件时在AEM中更新，则在分析期间会在Adobe Campaign中自动更新。 也可以使用手动执行同步 **刷新Adobe Experience Manager内容** 从内容操作栏中。
   您可以使用取消电子邮件与AEM内容之间的链接 **删除包含Adobe Experience Manager内容的链接** 从内容操作栏中。 仅当内容已链接到投放时，此按钮才可用。 要将其他内容与投放链接，必须先删除当前内容链接，然后才能建立新链接。
   删除链接后，本地内容会保留并在Adobe Campaign中变为可编辑。 如果在修改内容后再次链接该内容，则所有更改都将丢失。

### 将AEM中创建的内容与Adobe Campaign Classic中的投放同步 {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign允许您恢复在AEM中创建的内容并与以下内容同步：

* 营销活动投放
* 活动工作流中的投放活动
* 循环投放
* 连续投放
* 消息中心投放
* 投放模板

在AEM中，如果新闻稿链接到单个投放，则投放代码将显示在页面上。

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
如果新闻稿链接到多个投放，则会显示链接投放的数量（但不会显示每个ID）。
[!NOTE]
工作流步骤 **发布到Adobe Campaign** 在AEM 6.1中已弃用。此步骤是AEM 6.0与Adobe Campaign集成的一部分，不再需要。

要将AEM中创建的内容与Adobe Campaign中的投放同步，请执行以下操作：

1. 通过选择 **使用AEM内容发送电子邮件(mailAEMContent)** 投放模板。

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. 选择 **同步** 以访问AEM中可用的内容列表。

   >[!NOTE]
   如果 **同步** 选项不会出现在投放的工具栏中，请检查 **内容编辑模式** 字段配置正确 **AEM** 通过选择 **属性** > **高级**.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 选择要与投放同步的内容。

   此列表指定：

   * AEM中内容的标签。
   * AEM中内容的审批状态。 如果内容未获得批准，您可以同步内容，但必须在发送投放之前批准该内容。 但是，您可以执行某些操作，如发送BAT或预览测试。
   * 上次修改内容的日期。
   * 任何已链接到投放的内容。

   >[!NOTE]
   默认情况下，已与投放同步的内容处于隐藏状态。 但是，您可以显示并使用它。 例如，如果您希望将内容用作多个投放的模板。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 指定投放的其他参数（目标等）
1. 如有必要，请在Adobe Campaign中启动投放批准流程。 除了在Adobe Campaign中配置的审批（预算、目标等）之外，还需要AEM中的内容审批。 仅当Adobe Campaign中的内容已在AEM中获得批准时，该内容才可能获得批准。
1. 执行投放。 在投放分析期间，将恢复AEM内容的最新版本。

   >[!NOTE]
   * 在投放和内容同步后，Adobe Campaign中的投放内容变为只读。 无法再修改电子邮件主题及其内容。
   * 如果内容在链接到Adobe Campaign中的投放时在AEM中更新，则在投放分析期间会在投放中自动更新。 也可以使用手动执行同步 **立即刷新内容** 按钮。
   * 您可以使用取消投放与AEM内容之间的同步 **取消同步** 按钮。 仅当内容已与投放同步时，此项才可用。 要将其他内容与投放同步，必须先取消当前内容同步，然后才能建立新链接。
   * 如果取消同步，本地内容将保留并在Adobe Campaign中变为可编辑。 如果在修改内容后重新同步该内容，则将丢失所有更改。
   * 对于循环和连续投放，每次执行投放时都会停止与AEM内容的同步。

