---
title: 电子邮件营销
seo-title: E-mail Marketing
description: 电子邮件营销（例如，新闻稿）是任何营销活动的重要组成部分，因为您会使用它们向潜在客户推送内容。 在AEM中，您可以从现有AEM内容创建新闻稿并添加新内容（特定于新闻稿）。
seo-description: E-mail marketing (for example, newsletters) are an important part of any marketing campaign as you use them to push content to your leads. In AEM, you can create newsletters from existing AEM content as well as add new content, specific to the newsletters.
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
exl-id: a1d8b74e-67eb-4338-9e8e-fd693b1dbd48
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 1%

---

# 电子邮件营销{#e-mail-marketing}

>[!NOTE]
>
>Adobe不打算进一步增强对AEM SMTP服务发送的未结/退回（无法投放）的电子邮件跟踪。
>建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

电子邮件营销（例如，新闻稿）是任何营销活动的重要组成部分，因为您会使用它们向潜在客户推送内容。 在AEM中，您可以从现有AEM内容创建新闻稿并添加新内容（特定于新闻稿）。

创建后，您可以立即或在另一个计划时间（通过使用工作流）向特定用户组发送新闻稿。 此外，用户可以按自己选择的格式订阅新闻稿。

此外，通过AEM可以管理新闻稿功能，包括维护主题、存档新闻稿和查看新闻稿统计数据。

>[!NOTE]
>
>在Geometrixx中，新闻稿模板会自动打开电子邮件编辑器。 您可以在希望在其中发送电子邮件的其他模板（例如，邀请）中使用电子邮件编辑器。 无论从何时继承页面，都会显示电子邮件编辑器 **mcm/components/newsletter/page**.

本文档介绍了在AEM中创建新闻稿的基础知识。 有关如何使用电子邮件营销的更多详细信息，请参阅以下文档：

* [创建有效的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理订阅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [将电子邮件发布到电子邮件服务提供商](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [跟踪退回的电子邮件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果您更新电子邮件提供商、进行试运行测试或发送新闻稿，则当新闻稿未先发布到发布实例或者发布实例不可用时，这些操作将失败。 确保发布新闻稿，并确保Publish实例已启动且正在运行。

## 创建新闻稿体验 {#creating-a-newsletter-experience}

>[!NOTE]
>
>需要通过osgi配置来配置电子邮件通知。 参见 [配置电子邮件通知。](/help/sites-administering/notification.md)

1. 在左窗格中选择新营销活动，或在右窗格中双击该营销活动。

1. 使用图标选择列表视图：

   ![列表视图](do-not-localize/mcm_icon_listview-1.png)

1. 单击 **新建……**

   您可以指定 **标题**， **名称** 和要创建的体验类型；在本例中，为“新闻稿”。

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. 单击&#x200B;**创建**。

1. 随即会立即打开一个新对话框。 您可以在此处输入新闻稿的属性。

   此 **默认收件人列表** 是必填字段，因为这会形成新闻稿的接触点(请参阅 [使用列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists) （以了解有关列表的详细信息）。

   ![mcm_newsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **发件人名称**
应显示为Newsletter发件人的名称。

   * **发件人地址**
应显示为Newsletter发件人的邮件地址。

   * **主题**
新闻稿的主题。

   * **回复**
邮件地址，用于处理已发送新闻稿的回复。

   * **描述**
新闻稿的说明。

   * **准时**
发送新闻稿的准时。

   * **默认收件人列表**
应接收新闻稿的默认列表。

   可在稍后的阶段从 **属性……** 对话框。

1. 单击 **确定** 以保存。

## 向新闻稿添加内容 {#adding-content-to-newsletters}

您可以将内容（包括动态内容）添加到新闻稿中，就像在任何AEM组件中一样。 在Geometrixx中，“新闻稿”模板包含某些组件，可用于添加和修改新闻稿中的内容。

1. 在MCM中，单击 **营销活动** 选项卡，并双击要向其添加内容或编辑的新闻稿。 新闻稿随即打开。

1. 如果组件不可见，请转到“设计”视图并启用必要的组件（例如，新闻稿组件），然后再开始编辑。
1. 根据需要输入任何新文本、图像或其他组件。 在Geometrixx示例中，提供了4个组件：文本、图像、标题和2列。 新闻稿的组件数量可能会多或少，具体取决于您的设置方式。

   >[!NOTE]
   >
   >您可以使用变量对新闻稿进行个性化设置。 在Geometrixx新闻稿中，变量位于文本组件中。 变量的值继承自用户配置文件中的信息。

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 要插入变量，请从列表中选择该变量并单击 **插入**. 变量从配置文件中填充。

## 个性化新闻稿 {#personalizing-newsletters}

可通过在Geometrixx新闻稿的文本组件中插入预定义变量来对新闻稿进行个性化设置。 变量的值继承自用户配置文件中的信息。

您还可以通过使用客户端上下文和加载用户档案，模拟新闻稿的个性化方式。

个性化新闻稿并模拟其外观：

1. 从MCM中，打开要自定义其设置的新闻稿。

1. 打开要个性化的文本组件。

1. 将光标放在要显示变量的位置，然后从下拉列表中选择一个变量，然后单击 **插入**. 根据需要为任意数量的变量执行此操作，然后单击 **确定**.

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 要模拟发送变量时的外观，请按CTRL+ALT+c打开客户端上下文并选择 **加载**. 从列表中选择要加载其配置文件的用户，然后单击 **确定**.

   您加载的配置文件中的信息已填充变量。

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 在不同电子邮件客户端中测试新闻稿 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>在发送新闻稿之前，请检查Day CQ Link Externalizer的OSGi配置 `https://localhost:4502/system/console/configMgr`.
>
>默认情况下，参数的值为 `localhost:4502` 如果正在运行的实例的端口发生更改，则无法完成和操作。

在常用的电子邮件客户端之间切换，查看您的新闻稿在潜在客户端的外观如何。默认情况下，您的新闻稿会打开，但不会选择任何电子邮件客户端。

目前，您可以在以下电子邮件客户端中查看新闻稿：

* Yahoo邮件
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple Mail

要在客户端之间切换，请单击相应的图标以查看该电子邮件客户端中的新闻稿：

1. 从MCM中，打开要自定义其设置的新闻稿。

1. 单击顶部栏中的电子邮件客户端，可查看新闻稿在该客户端中的外观。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 对您希望查看的任何其他电子邮件客户端重复此步骤。

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 自定义新闻稿设置 {#customizing-newsletter-settings}

虽然只有授权用户可以发送新闻稿，但您应自定义以下内容：

* 主题行，以便用户希望打开您的电子邮件，并确保您的新闻稿最终不会被标记为垃圾邮件。
* 发件人地址，例如noreply@geometrixx.com ，以便用户从指定的地址接收电子邮件。

要自定义新闻稿设置，请执行以下操作：

1. 从MCM中，打开要自定义其设置的新闻稿。

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. 在新闻稿的顶部，单击 **设置**.

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. 输入 **起始日期** 电子邮件地址

1. 修改 **主题** （如有必要）。

1. 选择 **默认收件人列表** 下拉列表中。

1. 单击&#x200B;**确定**。

   当您测试或发送新闻稿时，收件人将收到包含指定电子邮件地址和主题的电子邮件。

## 飞行测试通讯 {#flight-testing-newsletters}

虽然飞行测试不是强制性的，但在您发送新闻稿之前，您可能需要测试它以确保它按您想要的方式显示。

试运行测试允许您执行以下操作：

* 在中查看新闻稿 [所有目标客户端](#testing-newsletters-in-different-e-mail-clients).
* 验证邮件服务器是否正确设置。
* 确定您的电子邮件是否被标记为垃圾邮件。 （确保将您自己包含在收件人列表中。）

>[!NOTE]
>
>如果您更新电子邮件提供商、进行试运行测试或发送新闻稿，则当新闻稿未先发布到发布实例或者发布实例不可用时，这些操作将失败。 确保发布新闻稿，并确保Publish实例已启动且正在运行。

试飞通讯：

1. 从MCM中，打开要测试的新闻稿并发送。

1. 在新闻稿的顶部，单击 **测试** 以在发送之前进行测试。

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. 输入要发送新闻稿的测试邮件地址，然后单击 **发送**. 如果要更改配置文件，请在客户端上下文中加载另一个配置文件。 要执行此操作，请按CTRL+ALT+c并选择“加载”并加载配置文件。

## 发送新闻稿 {#sending-newsletters}

>[!NOTE]
>
>Adobe不打算进一步增强对AEM SMTP服务发送的未结/退回（无法投放）的电子邮件跟踪。
>建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

您可以从新闻稿或列表发送新闻稿。 这两个过程都进行了描述。

>[!NOTE]
>
>在发送新闻稿之前，请检查Day CQ Link Externalizer的OSGi配置 `https://localhost:4502/system/console/configMgr`.
>
>默认情况下，参数的值为 `localhost:4502` 如果正在运行的实例的端口发生更改，则无法完成和操作。

>[!NOTE]
>
>如果您更新电子邮件提供商、进行试运行测试或发送新闻稿，则当新闻稿未先发布到发布实例或者发布实例不可用时，这些操作将失败。 确保发布新闻稿，并确保Publish实例已启动且正在运行。

### 从营销活动发送新闻稿 {#sending-newsletters-from-a-campaign}

要从营销活动内发送新闻稿，请执行以下操作：

1. 从MCM中，打开要发送的新闻稿。

   >[!NOTE]
   >
   >在发送之前，请确保已自定义新闻稿的主题和原始电子邮件地址 [自定义其设置](#customizing-newsletter-settings).
   >
   >
   >[飞行试验](#flight-testing-newsletters) 建议在发送前发送新闻稿。

1. 在新闻稿的顶部，单击 **发送**. 新闻稿向导将打开。

1. 在收件人列表中，选择要接收新闻稿的列表，然后单击 **下一个**.

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 已确认安装完成。 单击 **发送** 才能真正发送新闻稿。

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >确保您是收件者之一，这样您就可以确保新闻稿已收到。

### 从列表发送新闻稿 {#sending-newsletters-from-a-list}

要从列表发送新闻稿，请执行以下操作：

1. 在MCM中，单击 **列表** 左窗格中的。

   >[!NOTE]
   >
   >在发送之前，请确保已自定义新闻稿的主题和原始电子邮件地址 [自定义其设置](#customizing-newsletter-settings). 如果从列表中发送新闻稿，则无法对其进行测试；您可以 [飞行试验](#flight-testing-newsletters) 如果是从新闻稿发送的。

1. 选中要向其发送新闻稿的潜在客户列表旁边的复选框。

1. 在 **工具** 菜单，选择 **发送新闻稿**. 此 **发送新闻稿** 窗口打开。

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 在 **新闻稿** 字段中，选择要发送的新闻稿，然后单击 **下一个**.

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 已确认安装完成。 单击 **发送** 将所选新闻稿发送到指定的潜在客户列表。

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   新闻稿将发送给选定的收件人。

## 订阅新闻稿 {#subscribing-to-a-newsletter}

本节介绍如何订阅新闻稿。

### 订阅新闻稿 {#subscribing-to-a-newsletter-1}

要订阅新闻稿(以Geometrixx网站为例)，请执行以下操作：

1. 单击 **网站** 并导航到Geometrixx **工具栏** 打开它。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在Geometrixx新闻稿中 **注册** 字段中，输入您的电子邮件地址，然后单击 **注册**. 您现已订阅了新闻稿。
