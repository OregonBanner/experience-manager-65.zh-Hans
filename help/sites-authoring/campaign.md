---
title: 使用 Adobe Campaign Classic 和 Adobe Campaign Standard
seo-title: 使用 Adobe Campaign 6.1 和 Adobe Campaign Standard
description: 您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理
seo-description: 您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理
uuid: 23195f0b-71c0-4554-8c8b-b0e7704d71d7
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 2fd0047d-d0f6-4289-98cf-454486f9cd61
translation-type: tm+mt
source-git-commit: 69226ffeb79e0b425b28456cbc64192432863f5d
workflow-type: tm+mt
source-wordcount: '2780'
ht-degree: 74%

---


# 使用 Adobe Campaign Classic 和 Adobe Campaign Standard{#working-with-adobe-campaign-classic-and-adobe-campaign-standard}

您可以在 AEM 中创建电子邮件内容，然后在 Adobe Campaign 电子邮件中对其进行处理。要执行此操作，您必须：

1. 在 AEM 中从特定于 Adobe Campaign 的模板创建新闻稿。
1. 在编辑内容之前，选择 [Adobe Campaign 服务](#selecting-the-adobe-campaign-cloud-service-and-template)以便访问所有功能。
1. 编辑内容。
1. 验证内容。

之后，可以将内容与 Adobe Campaign 中的分发同步。本文档提供了相关详细说明。

另请参阅[在 AEM 中创建 Adobe Campaign 表单](/help/sites-authoring/adobe-campaign-forms.md)。

>[!NOTE]
>
>在使用此功能之前，您必须先将 AEM 配置为与 [Adobe Campaign](/help/sites-administering/campaignonpremise.md) 或 [Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) 集成。

## 通过 Adobe Campaign 发送电子邮件内容 {#sending-email-content-via-adobe-campaign}

配置 AEM 和 Adobe Campaign 后，您可以直接在 AEM 中创建电子邮件分发内容，然后在 Adobe Campaign 中对其进行处理。

在AEM中创建Adobe Campaign内容时，您必须先链接到Adobe Campaign服务，然后才能编辑内容以访问所有功能。

以下是两种可能的情况：

* 内容可以与 Adobe Campaign 中的分发同步。这使您能够在分发中使用 AEM 内容。
* （仅适用于 Adobe Campaign Classic）内容可以直接发送到 Adobe Campaign，由其自动生成新的电子邮件分发。此模式存在限制。

本文档提供了相关详细说明。

### 创建新的电子邮件内容 {#creating-new-email-content}

>[!NOTE]
>
>When adding email templates, be sure to add them under **/content/campaigns** to make them available.


#### 创建新的电子邮件内容 {#creating-new-email-content-1}

1. In AEM select **Sites** then **Campaigns**, then browse to where your email campaigns are managed. In the following example, the path is **Sites** > **Campaigns** > **Geometrixx Outdoors** > **Email Campaigns**.

   >[!NOTE]
   >
   >[仅 Geometrixx 中提供了电子邮件示例](/help/sites-developing/we-retail.md)。请从包共享下载示例Geometrixx内容。

   ![chlimage_1-15](assets/chlimage_1-15a.png)

1. 选择&#x200B;**创建**，然后选择&#x200B;**创建页面**。
1. 选择您所连接到的 Adobe Campaign 所对应的可用模板之一，然后单击&#x200B;**下一步**。默认情况下，有两种模板可用：

   * **Adobe Campaign Classic电邮**:允许您在将内容发送到Adobe Campaign Classic进行投放之前，将内容添加到预定义的模板（两列）。
   * **Adobe Campaign Standard电邮**:允许您在将内容发送到Adobe Campaign Standard进行投放之前，将内容添加到预定义的模板（两列）。

1. Fill in the **Title** and optionally the **Description** and click **Create**. 标题将用作新闻稿/电子邮件的主题，除非您在编辑电子邮件时覆盖此标题。

### 选择 Adobe Campaign 云服务和模板 {#selecting-the-adobe-campaign-cloud-service-and-template}

要与 Adobe Campaign 集成，您需要将 Adobe Campaign 云服务添加到页面。通过执行此操作，您可以访问个性化设置和其他 Adobe Campaign 信息。

此外，您可能还需要选择 Adobe Campaign 模板，同时更改主题，并为那些不以 HTML 形式查看电子邮件的用户添加纯文本内容。

您可以从&#x200B;**站点**&#x200B;选项卡中，或从创建的电子邮件/新闻稿中选择云服务。

建议从&#x200B;**站点**&#x200B;选项卡中选择云服务。要从电子邮件/新闻稿中选择云服务，需要使用相应的解决方法。

从&#x200B;**站点**&#x200B;页面中：

1. 在 AEM 中，选择电子邮件页面，然后单击&#x200B;**查看属性**。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Select **Edit** and then the **Cloud services** tab and scroll down to the bottom and click the + sign to add a configuration and then select **Adobe Campaign**.

   ![chlimage_1-17](assets/chlimage_1-17a.png)

1. 从下拉列表中选择与您的 Adobe Campaign 实例相匹配的配置，然后单击&#x200B;**保存**&#x200B;以进行确认。
1. 您可以通过单击 **Adobe Campaign** 选项卡来查看电子邮件应用的模板。如果您想要选择其他模板，则可以在编辑时从电子邮件中访问该模板。

   If you would like to apply a specific email delivery template (from Adobe Campaign), other than the default mail template, in **Properties**, select the **Adobe Campaign** tab. 输入电子邮件分发模板在相关 Adobe Campaign 实例中的内部名称。

   所选的模板将决定可从 Adobe Campaign 中使用哪些个性化字段。

   ![chlimage_1-18](assets/chlimage_1-18a.png)

在处于创作状态的新闻稿/电子邮件中，由于布局方面的问题，您可能无法在&#x200B;**页面属性**&#x200B;中选择 Adobe Campaign 云服务配置。您可以使用下面介绍的解决方法：

1. 在 AEM 中，选择电子邮件页面，然后单击&#x200B;**编辑**。单击&#x200B;**打开属性**。

   ![chlimage_1-19](assets/chlimage_1-19a.png)

1. Select **Cloud services** and click **+** to add a configuration. 选择任意可见配置（不论哪个均可）。单击或点按 **+** 符号以添加另一个配置，然后选择 **Adobe Campaign**。

   >[!NOTE]
   >
   >或者，也可以在&#x200B;**站点**&#x200B;选项卡中选择&#x200B;**查看属性**，从而选择云服务。

1. 从下拉Adobe Campaign中选择与您的列表实例匹配的配置，删除您创建的第一个非Adobe Campaign配置，然后单击复选标记进行确认。
1. 继续执行上述操作过程中的步骤 4，以选择模板并添加纯文本。

### 编辑电子邮件内容 {#editing-email-content}

要编辑电子邮件内容，请执行以下操作：

1. 打开电子邮件，默认情况下，您会进入编辑模式。

   ![chlimage_1-20](assets/chlimage_1-20a.png)

1. If you would like to change the subject of the email or add plain text for those users who will not view the email in HTML, select **Email** and add a subject and text. 选择页面图标，以自动从 HTML 生成纯文本版本。完成后，单击复选标记。

   您可以使用 Adobe Campaign 个性化字段对新闻稿进行个性化设置。要添加个性化字段，请单击显示 Adobe Campaign 徽标的按钮，以打开个性化字段选取器。您可以从所有可用于此新闻稿的字段中进行选择。

   >[!NOTE]
   >
   >如果属性中的个性化字段在编辑器内呈灰显状态，请重新检查您的配置。

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Open the components panel on left side of screen and select **Adobe Campaign Newsletter** from the drop-down menu to find those components.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. 将这些组件直接拖到页面上，并对其进行相应编辑。例如，您可以拖动&#x200B;**文本与个性化（营销活动）**&#x200B;组件，并添加个性化文本。

   ![chlimage_1-23](assets/chlimage_1-23a.png)

   See [Adobe Campaign Components](/help/sites-authoring/adobe-campaign-components.md) for a detailed description of each component.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

### 插入个性化 {#inserting-personalization}

编辑内容时，您可以插入：

* Adobe Campaign 上下文字段。这些字段可以插入文本中，并根据收件人的数据(例如名、姓或目标维的任何数据)进行调整。
* Adobe Campaign 个性化基块。这些是与收件人数据无关的预定义内容块，如品牌徽标或指向镜像页面的链接。

有关营销活动组件的完整说明，请参阅 [Adobe Campaign 组件](/help/sites-authoring/adobe-campaign-components.md)。

>[!NOTE]
>
>* 只会考虑 Adobe Campaign **配置文件**&#x200B;定位维度的字段。
>* When viewing Properties from **Sites**, you do not have access to the Adobe Campaign context fields. 您可以在编辑时直接从电子邮件中访问这些字段。

>



要插入个性化，请执行以下操作：

1. Insert a new **Newsletter** > **Text &amp; Personalization (Campaign)** component by dragging it onto the page.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. 单击铅笔图标，以打开该组件。随即会打开就地编辑器。

   ![chlimage_1-26](assets/chlimage_1-26a.png)

   >[!NOTE]
   >
   >**对于 Adobe Campaign Standard：**
   >
   >* 可用的上下文字段与 Adobe Campaign 中的&#x200B;**配置文件**&#x200B;定位维度相对应。
   >* See [Linking an AEM page to an Adobe Campaign email](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard).

   >
   >**对于 Adobe Campaign Classic：**
   >
   >* Available context fields are dynamically recovered from the Adobe Campaign **nms:seedMember** schema. 目标扩展数据是从包含与内容同步的分发的工作流中动态获取的。(See the [Synchronizing content created in AEM with a delivery from Adobe Campaign](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic) section).
      >
      >
   * To add or hide personalization elements, see [Managing personalization fields and blocks](/help/sites-administering/campaignonpremise.md#managing-personalization-fields-and-blocks).
   >* **重要信息**：收件人表（或相应的联系人表）也必须包含所有种子表字段。


1. 通过键入方式插入文本。通过单击 Adobe Campaign 组件并选择这些组件，插入上下文字段或个性化基块。完成后，选择复选标记。

   ![chlimage_1-27](assets/chlimage_1-27a.png)

   插入上下文字段或个性化基块后，您可以预览新闻稿并对字段进行测试。See [Previewing a Newsletter](#previewing-a-newsletter).

### 预览新闻稿 {#previewing-a-newsletter}

您可以预览新闻稿的外观以及个性化。

1. 打开新闻稿后，单击 AEM 右上角的&#x200B;**预览**。AEM显示Newsletter在用户收到时的外观。

   ![chlimage_1-28](assets/chlimage_1-28a.png)

   >[!NOTE]
   >
   >如果您在使用 Adobe Campaign Standard 以及示例模板，则在分发过程中导入内容时，显示初始内容的两个个性化基块（**&quot;&lt;%@ include view=&quot;MirrorPage&quot; %>&quot;** 和 **&quot;&lt;%@ include view=&quot;UnsubscriptionLink&quot; %>&quot;**）将会抛出错误。您可以通过使用个性化基块选取器选择相应的基块来进行调整。

1. 要预览个性化，请单击/点按工具栏中的相应图标以打开 ContextHub。现在，个性化字段标记已替换为选定人物的种子数据。请查看在 ContextHub 中切换人物时变量是如何调整的。

   ![chlimage_1-29](assets/chlimage_1-29a.png)

1. 您可以查看来自 Adobe Campaign 的与当前选定人物关联的种子数据。为此，请单击/点按 ContextHub 栏中的 Adobe Campaign 模块。此时会打开一个对话框，其中显示了当前配置文件的所有种子数据。同样，在切换到其他人物时，这些数据会相应地调整。

   ![chlimage_1-30](assets/chlimage_1-30a.png)

### 在 AEM 中批准内容 {#approving-content-in-aem}

内容完成后，您可以启动批准流程。Go to the **Workflow** tab of the toolbox and select the **Approve for Adobe Campaign** workflow.

该现成的工作流包含两个步骤：修订然后批准，或者修订然后拒绝。不过，可以扩展并调整此工作流以适应更复杂的过程。

![chlimage_1-31](assets/chlimage_1-31a.png)

To approve content for Adobe Campaign, apply the workflow by selecting **Workflow** and selecting **Approve for Adobe Campaign** and click **Start Workflow**. 完成这些步骤并批准内容。 您也可以拒绝该内容，方法是在上一个工作流步骤中选择&#x200B;**拒绝**&#x200B;而不是&#x200B;**批准**。

![chlimage_1-32](assets/chlimage_1-32a.png)

内容获得批准后，它会在 Adobe Campaign 中显示为已批准。之后，便可以发送电子邮件。

在 Adobe Campaign Standard 中：

![chlimage_1-33](assets/chlimage_1-33a.png)

在 Adobe Campaign Classic 中：

![chlimage_1-34](assets/chlimage_1-34a.png)

>[!NOTE]
未经批准的内容可以与 Adobe Campaign 中的分发同步，但无法执行分发。只有经过批准的内容才可以通过营销活动分发来发送。

## 将 AEM 与 Adobe Campaign Standard 和 Adobe Campaign Classic 链接 {#linking-aem-with-adobe-campaign-standard-and-adobe-campaign-classic}

如何将 AEM 与 Adobe Campaign 链接或同步，取决于您使用的是基于订阅的 Adobe Campaign Standard，还是基于内部部署的 Adobe Campaign Classic。

请根据您使用的 Adobe Campaign 解决方案参阅以下相应部分的说明：

* [将 AEM 页面链接到 Adobe Campaign 电子邮件 (Adobe Campaign Standard)](#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard)
* [将 AEM 中创建的内容与 Adobe Campaign Classic 中的分发同步](#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic)

### 将 AEM 页面链接到 Adobe Campaign 电子邮件 (Adobe Campaign Standard) {#linking-an-aem-page-to-an-adobe-campaign-email-adobe-campaign-standard}

Adobe Campaign Standard 允许您获取 AEM 中创建的内容并将其与以下项目链接：

* 电子邮件。
* 电子邮件模板。

链接后，您可以分发内容。通过页面上显示的代码，您可以了解新闻稿是否已链接到单个分发。

![chlimage_1-35](assets/chlimage_1-35a.png)

>[!NOTE]
如果新闻稿已链接到多个投放，则链接的投放数（但不显示每个ID）。

要将 AEM 中创建的页面与 Adobe Campaign 中的电子邮件相链接，请执行以下操作：

1. 基于特定于 AEM 的电子邮件模板创建新的电子邮件。Refer to [Creating emails in Adobe Campaign Standard](https://helpx.adobe.com/cn/campaign/standard/channels/using/creating-an-email.html) for more information.

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 从分发功能板中打开&#x200B;**内容**&#x200B;块。

   ![chlimage_1-37](assets/chlimage_1-37a.png)

1. Select **Link with an Adobe Experience Manager content** in the toolbar to access the list of contents available in AEM.

   >[!NOTE]
   If the **Link with an Adobe Experience Manager** option does not appear in the action bar, check that the **Content editing mode** is correctly configured set to **Adobe Experience Manager** in the email properties.

   ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 选择要在电子邮件中使用的内容。

   此列表指定了以下各项：

   * AEM 中的内容标签。
   * AEM 中的内容批准状态。如果内容未获得批准，您可以对其进行同步，但是必须批准内容，之后才能发送分发。不过，您可以执行一些特定操作，例如发送证据或进行预览测试。
   * 内容的上次修改日期。
   * 已链接到分发的所有内容。

   >[!NOTE]
   默认情况下，已与分发同步的内容会处于隐藏状态。但是，您可以显示并使用这些内容。例如，如果您要将内容用作多次分发的模板，则可以显示该内容。

   将电子邮件链接到 AEM 内容后，将无法在 Adobe Campaign 中编辑该内容。

1. 在电子邮件功能板中指定电子邮件的其他参数（受众、执行计划等）。
1. 执行电子邮件分发。在分发分析过程中，会检索最新版本的 AEM 内容。

   >[!NOTE]
   将内容链接到电子邮件后，如果在 AEM 中更新了该内容，则也会在 Adobe Campaign 中的分析过程中自动更新该内容。也可以使用内容操作栏中的&#x200B;**刷新 Adobe Experience Manager 内容**&#x200B;来手动执行同步。
   您可以使用内容操作栏中的&#x200B;**删除与 Adobe Experience Manager 内容的链接**&#x200B;来取消电子邮件与 AEM 内容之间的链接。仅当内容已与分发链接时，此按钮才可用。要将其他内容与分发链接，您必须删除当前的内容链接，然后才能建立新链接。
   删除链接后，系统会保留本地内容，并可在 Adobe Campaign 中对其进行编辑。如果在对内容进行修改后重新链接该内容，则所有更改均会丢失。

### 将 AEM 中创建的内容与 Adobe Campaign Classic 中的分发同步 {#synchronizing-content-created-in-aem-with-a-delivery-from-adobe-campaign-classic}

Adobe Campaign 允许您获取 AEM 中创建的内容并将其与以下项目同步：

* 营销活动分发
* 营销活动工作流中的分发活动
* 周期性分发
* 连续分发
* 消息中心分发
* 分发模板

在 AEM 中，如果新闻稿已链接到单个分发，则页面上会显示分发代码。

![chlimage_1-39](assets/chlimage_1-39a.png)

>[!NOTE]
如果新闻稿已链接到多个投放，则链接的投放数（但不显示每个ID）。
[!NOTE]
AEM 6.1 中已弃用以下工作流步骤：**发布到 Adobe Campaign**。这曾是 AEM 6.0 与 Adobe Campaign 集成中包含的一个步骤，现在已不再需要。

要将 AEM 中创建的内容与 Adobe Campaign 中的分发同步，请执行以下操作：

1. Create a delivery or add a delivery activity to a campaign workflow by selecting the **Email delivery with AEM content (mailAEMContent)** delivery template.

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. Select **Synchronize** in the toolbar to access the list of contents available in AEM.

   >[!NOTE]
   If the **Synchronize** option does not appear in the delivery&#39;s toolbar, check that the **Content editing mode** field is correctly configured in **AEM** by selecting **Properties** > **Advanced**.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 选择要与分发同步的内容。

   此列表指定了以下各项：

   * AEM 中的内容标签。
   * AEM 中的内容批准状态。如果内容未获得批准，您可以对其进行同步，但是必须批准内容，之后才能发送分发。不过，您可以执行一些特定操作，例如发送 BAT 或进行预览测试。
   * 内容的上次修改日期。
   * 已链接到分发的所有内容。

   >[!NOTE]
   默认情况下，已与分发同步的内容会处于隐藏状态。但是，您可以显示并使用这些内容。例如，如果您要将内容用作多次分发的模板，则可以显示该内容。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 指定分发的其他参数（目标等）。
1. 如有必要，在 Adobe Campaign 中启动分发批准流程。除了 Adobe Campaign 中配置的批准（预算批准、目标批准等）之外，还需要在 AEM 中批准内容。仅当在 AEM 中已批准内容时，才能在 Adobe Campaign 中执行内容批准。
1. 执行分发。在分发分析过程中，会获取最新版本的 AEM 内容。

   >[!NOTE]
   * 将分发和内容同步后，Adobe Campaign 中的分发内容会变为只读。电子邮件主题及其内容将无法再修改。
   * 将内容链接到 Adobe Campaign 中的分发后，如果在 AEM 中更新了该内容，则也会在分发分析过程中自动更新该内容。The synchronization can also be executed manually using the **Refresh content now** button.
   * You can cancel synchronization between a delivery and AEM content using the **Desynchronize** button. 仅当内容已与分发同步时，此按钮才可用。要将其他内容与分发同步，您必须取消当前的内容同步，然后才能建立新链接。
   * 如果取消同步，系统会保留本地内容，并可在 Adobe Campaign 中对其进行编辑。如果在对内容进行修改后重新同步该内容，则会丢失所有更改。
   * 对于周期性分发和连续分发，每次执行分发时系统都会停止与 AEM 内容的同步。

