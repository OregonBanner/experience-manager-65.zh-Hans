---
title: 电子邮件营销
seo-title: 电子邮件营销
description: 电子邮件营销（例如新闻稿）是所有市场营销的重要组成部分，因为您可以通过这种方式将内容推送到您的潜在客户。在 AEM 中，您可以根据现有 AEM 内容创建新闻稿，也可以添加特定于新闻稿的新内容。
seo-description: 电子邮件营销（例如新闻稿）是所有市场营销的重要组成部分，因为您可以通过这种方式将内容推送到您的潜在客户。在 AEM 中，您可以根据现有 AEM 内容创建新闻稿，也可以添加特定于新闻稿的新内容。
uuid: 565943bf-fe37-4d5c-98c3-7c629c4ba264
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 69ca5acb-83f9-4e1b-9639-ec305779c931
docset: aem65
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 电子邮件营销{#e-mail-marketing}

>[!NOTE]
>
>Adobe 不打算进一步增强对 AEM SMTP 服务发送的打开/弹回（不可交付）电子邮件的跟踪。
>Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

电子邮件营销（例如新闻稿）是所有市场营销的重要组成部分，因为您可以通过这种方式将内容推送到您的潜在客户。在 AEM 中，您可以根据现有 AEM 内容创建新闻稿，也可以添加特定于新闻稿的新内容。

创建新闻稿后，您可以立即将新闻稿发送到特定用户组，或者在其他预定时间发送（通过使用工作流）。此外，用户可以订阅使用其所选格式的新闻稿。

并且，使用 AEM 可以管理 Newsletter 功能，包括维护主题、归档 Newsletter 以及查看 Newsletter 统计数据。

>[!NOTE]
>
>在 Geometrixx 中，Newsletter 模板可自动打开电子邮件编辑器。您可以在要发送邀请函等格式的电子邮件使用的其他模板中使用电子邮件编辑器。电子邮件编辑器随时显示从 **mcm/components/newsletter/page** 继承的页面。

本文档介绍了在 AEM 中创建新闻稿的基础知识。有关如何使用电子邮件营销的更多详细信息，请参阅以下文档：

* [创建有效的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-landingpage.md)
* [管理订阅](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-subscriptions.md)
* [将电子邮件发布到电子邮件服务提供商](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-newsletters.md)
* [跟踪弹回的电子邮件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email-tracking-bounces.md)

>[!NOTE]
>
>如果没有先将新闻稿发布到发布实例，或发布实例不可用，则以下操作将失败：更新电子邮件提供商、执行试运行，或发送新闻稿。请务必发布您的新闻稿，并确保发布实例已启动且正在运行。

## 创建新闻稿体验 {#creating-a-newsletter-experience}

>[!NOTE]
>
>需要通过 OSGi 配置来配置电子邮件通知。请参阅[配置电子邮件通知](/help/sites-administering/notification.md)。

1. 在左边窗格中选择您的新营销活动，或者在右边窗格中双击它。

1. 使用此图标选择列表视图：

   ![](do-not-localize/mcm_icon_listview-1.png)

1. 单击&#x200B;**新建...**

   您可以指定&#x200B;**标题**、**名称**&#x200B;和要创建的体验类型；在此示例中，即为 Newsletter。

   ![mcm_createnewsletter](assets/mcm_createnewsletter.png)

1. 单击&#x200B;**创建**。

1. 新对话框将立即打开。您可在此输入新闻稿的属性。

   **默认收件人列表**&#x200B;为必填字段，因为它构成了新闻稿的触点（请参阅[使用列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#workingwithlists)，以了解更多有关列表的信息）。

   ![mcm_newnewsletterdialog](assets/mcm_newnewsletterdialog.png)

   * **发件人姓名** 应显示为新闻稿发件人的姓名。

   * **发件人地址** 应显示为新闻稿发件人的邮件地址。

   * **主题** 新闻稿的主题。

   * **回复** 应负责处理已发送新闻稿的回复的邮件地址。

   * **描述** 新闻稿的描述。

   * **开始时间** 发送新闻稿的开始时间。

   * **默认收件人列表** 应接收新闻稿的默认列表。
   稍后可以从&#x200B;**属性...** 对话框更新这些内容。

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 向新闻稿中添加内容 {#adding-content-to-newsletters}

您可以在新闻稿中添加内容（包括动态内容），就像在任何 AEM 组件中一样。在 Geometrixx 中，Newsletter 模板具有可用于在 Newsletter 中添加和修改内容的特定组件。

1. 在 MCM 中，单击“**市场活动**”选项卡，并双击要在其中添加内容或进行编辑的 Newsletter。该 Newsletter 将打开。

1. 如果组件不可见，请在开始编辑之前先转到“设计”视图，启用必需的组件（例如 Newsletter 组件）。
1. 根据需要输入所有新文本、图像或其他组件。在 Geometrixx 示例中，有 4 个组件可用：文本、图像、标题和 2 列。您的新闻稿可以包含更多或更少的组件，具体取决于如何设置。

   >[!NOTE]
   >
   >您可以使用变量来对新闻稿进行个性化设置。在 Geometrixx 新闻稿中，可在文本组件中使用变量。变量值继承自用户个人资料信息。

   ![mcm_newsletter_content](assets/mcm_newsletter_content.png)

1. 要插入变量，请从列表中选择变量，并单击&#x200B;**插入**。变量根据个人资料进行填充。

## 对新闻稿进行个性化设置 {#personalizing-newsletters}

通过在 Geometrixx 中新闻稿的文本组件中插入预定义的变量，可以对新闻稿进行个性化设置。变量值继承自用户个人资料信息。

您还可以通过使用客户段上下文并加载个人资料来模拟如何个性化设置 Newsletter。

个性化设置 Newsletter 和模拟其外观：

1. 在 MCM 中，打开要自定义其设置的 Newsletter。

1. 打开要个性化设置的文本组件。

1. 将光标置于要显示变量的位置，从下拉列表中选择一个变量，并单击&#x200B;**插入**。对所需数量的变量执行此操作，并单击&#x200B;**确定**。

   ![mcm_newsletter_variables](assets/mcm_newsletter_variables.png)

1. 要模拟变量发送后的外观，请按 CTRL+ALT+c 打开 Client Context，并选择&#x200B;**加载**。从列表中选择要加载其个人资料的用户，并单击&#x200B;**确定**。

   系统会使用加载的个人资料中的信息填充变量。

   ![mc_newsletter_testvariables](assets/mc_newsletter_testvariables.png)

## 在其他电子邮件客户端中测试新闻稿 {#testing-newsletters-in-different-e-mail-clients}

>[!NOTE]
>
>Before sending newsletters, check the OSGi configuration for Day CQ Link Externalizer at `https://localhost:4502/system/console/configMgr`.
>
>默认情况下，参数的值为 `localhost:4502`，并且如果运行实例的端口发生更改，将无法完成操作。

在常用的电子邮件客户端之间切换，查看您的新闻稿在潜在客户端的外观如何。默认情况下，您的新闻稿打开时，不会选中任何电子邮件客户端。

现在，您可以在以下电子邮件客户端查看新闻稿：

* Yahoo 邮件
* Gmail
* Hotmail
* Thunderbird
* Microsoft Outlook 2007
* Apple Mail

要在客户端之间切换，请单击相应的图标，以查看该电子邮件客户端中的新闻稿：

1. 在 MCM 中，打开要自定义其设置的 Newsletter。

1. 在顶部图标栏中单击某电子邮件客户端，以查看 Newsletter 在该客户端中显示的外观。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 对要查看的所有其他电子邮件客户端重复执行该步骤。

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 自定义新闻稿设置 {#customizing-newsletter-settings}

虽然只有授权用户可以发送新闻稿，但您应自定义以下内容：

* 主题行，以使用户愿意打开您的电子邮件，同时确保您的新闻稿不会被标记为垃圾邮件。
* 发件人地址（例如 noreply@geometrixx.com），以使用户接收来自指定地址的电子邮件。

自定义 Newsletter 设置：

1. 在 MCM 中，打开要自定义其设置的 Newsletter。

   ![mcm_newsletter_open](assets/mcm_newsletter_open.png)

1. 在 Newsletter 顶部，单击&#x200B;**设置**。

   ![mcm_newsletter_settings](assets/mcm_newsletter_settings.png)
1. 输入&#x200B;**发件人**&#x200B;电子邮件地址

1. 根据需要修改电子邮件的&#x200B;**主题**。

1. 从下拉列表中选择一个&#x200B;**默认收件人列表**&#x200B;列表。

1. 单击&#x200B;**确定**。

   当您测试或发送新闻稿时，收件人将收到具有指定电子邮件地址和主题的电子邮件。

## 试运行新闻稿 {#flight-testing-newsletters}

虽然试运行不是强制的，但在发出新闻稿之前，可能需要对其进行测试，以此确保其按所需形式显示。

使用试运行，可以执行以下操作：

* 在[所有预期客户端](#testing-newsletters-in-different-e-mail-clients)中查看新闻稿。
* 验证是否已正确设置邮件服务器。
* 确定是否将您的电子邮件标记为垃圾邮件。（确保将您自己包括在收件人列表中。）

>[!NOTE]
>
>如果没有先将新闻稿发布到发布实例，或发布实例不可用，则以下操作将失败：更新电子邮件提供商、执行试运行，或发送新闻稿。请务必发布您的新闻稿，并确保发布实例已启动且正在运行。

要试运行新闻稿，请执行以下操作：

1. 在 MCM 中，打开要测试和发送的 Newsletter。

1. 在 Newsletter 顶部，单击&#x200B;**测试**&#x200B;以在发送前进行测试。

   ![mcm_newsletter_testsettings](assets/mcm_newsletter_testsettings.png)

1. 输入您希望将新闻稿发送到的测试邮件地址，并单击&#x200B;**发送**。如果要更改个人资料，请在 Client Context 中加载其他个人资料。为此，请按 CTRL+ALT+c 并选择“加载”，然后加载个人资料。

## 发送新闻稿 {#sending-newsletters}

>[!NOTE]
>
>Adobe 不打算进一步增强对 AEM SMTP 服务发送的打开/弹回（不可交付）电子邮件的跟踪。
>Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

您可以从营销活动或列表发出新闻稿。下面介绍这两个过程。

>[!NOTE]
>
>Before sending newsletters, check the OSGi configuration for Day CQ Link Externalizer at `https://localhost:4502/system/console/configMgr`.
>
>默认情况下，参数的值为 `localhost:4502`，并且如果运行实例的端口发生更改，将无法完成操作。

>[!NOTE]
>
>如果没有先将新闻稿发布到发布实例，或发布实例不可用，则以下操作将失败：更新电子邮件提供商、执行试运行，或发送新闻稿。请务必发布您的新闻稿，并确保发布实例已启动且正在运行。

### 从营销活动发送新闻稿 {#sending-newsletters-from-a-campaign}

要从营销活动中发出新闻稿，请执行以下操作：

1. 在 MCM 中，打开要发送的新闻稿。

   >[!NOTE]
   >
   >在发出之前，请确保您已通过[自定义新闻稿设置](#customizing-newsletter-settings)对新闻稿的主题和源电子邮件地址进行了自定义。
   >
   >
   >建议在发送之前先[试运行](#flight-testing-newsletters)新闻稿。

1. 在新闻稿顶部，单击&#x200B;**发送**。Newsletter 向导将打开。

1. 在收件人列表中，选择要接收 Newsletter 的列表，并单击&#x200B;**下一步**。

   ![mcm_newslettersend](assets/mcm_newslettersend.png)

1. 确认设置完成。单击&#x200B;**发送**&#x200B;以实际发送新闻稿。

   ![mcm_newslettersendconfirm](assets/mcm_newslettersendconfirm.png)

   >[!NOTE]
   >
   >确保您是收件人之一，以此确保收到 Newsletter。

### 从列表发送 Newsletter {#sending-newsletters-from-a-list}

要从列表中发出新闻稿，请执行以下操作：

1. 在 MCM 中，单击左侧窗格中的&#x200B;**列表**。

   >[!NOTE]
   >
   >在发出之前，请确保您已通过[自定义新闻稿设置](#customizing-newsletter-settings)对新闻稿的主题和源电子邮件地址进行了自定义。如果从列表发送新闻稿，则不能测试新闻稿；如果从营销活动发送新闻稿，则可以进行[试运行](#flight-testing-newsletters)。

1. 选中要将 Newsletter 发送到的 Lead 列表旁的复选框。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**发送新闻稿**。**发送新闻稿**&#x200B;窗口将打开。

   ![mcm_newslettersendfromlist](assets/mcm_newslettersendfromlist.png)

1. 在 **Newsletter** 字段中，选择要发送的 Newsletter，并单击&#x200B;**下一步**。

   ![mcm_newslettersenddialog](assets/mcm_newslettersenddialog.png)

1. 确认设置完成。单击&#x200B;**发送**&#x200B;将所选新闻稿发送到指定的潜在客户列表。

   ![mcm_newslettersenddialog_confirmation](assets/mcm_newslettersenddialog_confirmation.png)

   Newsletter 将发送到所选收件人。

## 订阅新闻稿 {#subscribing-to-a-newsletter}

此部分介绍如何订阅新闻稿。

### 订阅新闻稿 {#subscribing-to-a-newsletter-1}

订阅 Newsletter（以 Geometrixx 网站为例）：

1. 单击“**网站**”，导航到 Geometrixx 的“**工具栏**”并将其打开。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 在 Geometrixx 新闻稿的&#x200B;**注册**&#x200B;字段中，输入您的电子邮件地址并单击&#x200B;**注册**。现在，您已订阅 Newsletter。
