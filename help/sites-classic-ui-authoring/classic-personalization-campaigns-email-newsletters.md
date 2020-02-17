---
title: 将电子邮件发布到电子邮件服务提供商
seo-title: 将电子邮件发布到电子邮件服务提供商
description: 您可以将新闻稿发布到电子邮件服务，如 ExactTarget 和 Silverpop Engage。
seo-description: 您可以将新闻稿发布到电子邮件服务，如 ExactTarget 和 Silverpop Engage。
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 将电子邮件发布到电子邮件服务提供商{#publishing-an-email-to-email-service-providers}

您可以将新闻稿发布到电子邮件服务，如 ExactTarget 和 Silverpop Engage。本文档介绍如何配置 AEM 以将新闻稿发布到这些电子邮件服务。

>[!NOTE]
>
>您需要先配置服务提供商，然后才能创建和发布电子邮件。See [Configuring ExactTarget](/help/sites-administering/exacttarget.md) and [Configuring Silverpop Engage](/help/sites-administering/silverpop.md) for more information.

要将您的电子邮件发布到电子邮件服务提供商，您需要执行以下步骤：

1. 创建电子邮件。
1. 将电子邮件服务配置应用到电子邮件。
1. 发布电子邮件。

>[!NOTE]
>
>如果没有先将新闻稿发布到发布实例，或发布实例不可用，则以下操作将失败：更新电子邮件提供商、执行试运行，或发送新闻稿。请务必发布您的新闻稿，并确保发布实例已启动且正在运行。

## 创建电子邮件 {#creating-an-email}

An email or newsletter that you want to publish to an e-mail service can be created under a campaign using the **Geometrixx Newsletter** template. You can also use the **Geometrixx Outdoors E-Mail** template. 基于 **Geometrixx Outdoors电子邮件模板的示例电子邮件** /新闻稿 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`，请访问。

要创建发布到已配置电子邮件服务的新电子邮件，请执行以下操作：

1. Go to **Websites** and then **Campaigns**. 选择营销活动。
1. 单击&#x200B;**新建**&#x200B;以打开&#x200B;**创建页面**&#x200B;窗口。
1. 输入标题、名称，然后从可用模板列表中选择 **Geometrixx 新闻稿**&#x200B;模板。
1. 单击&#x200B;**创建**。
1. 打开创建的电子邮件。
1. 切换到设计模式以选择要在 Sidekick 中显示的组件。
1. Switch to edit mode and start adding content (text, images, [email tools](#adding-exacttarget-email-tools-to-your-email), [personalization variables](#adding-text-and-personalization-tool-to-your-e-mail), and so on) to your email.

### 将 ExactTarget 电子邮件工具添加到电子邮件 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>此部分内容针对的是 ExactTarget 服务。

The **Email Tools** component for ExactTarget can add more email functionality to your email/newsletter.

1. 打开要发布到 ExactTarget 的电子邮件。
1. 使用 Sidekick 将 **ET - 电子邮件工具**&#x200B;组件添加到您的页面。以编辑模式打开组件。

   ![chlimage_1](assets/chlimage_1.gif)

1. 从&#x200B;**选项**&#x200B;菜单中选择一个选项：

<table>
 <tbody>
  <tr>
   <td>邮寄地址(必需)</td>
   <td>此组件会在电子邮件中插入贵组织的邮寄地址。</td>
  </tr>
  <tr>
   <td>个人资料中心(必需)</td>
   <td>个人资料中心网页可供订阅者输入和维护您保存的与其有关的个人信息。</td>
  </tr>
  <tr>
   <td>以网页的形式查看电子邮件</td>
   <td>此组件允许用户以网页的形式查看电子邮件.</td>
  </tr>
  <tr>
   <td>隐私政策</td>
   <td>This component inserts the link to your privacy policy in the email.<br /> </td>
  </tr>
  <tr>
   <td>取消订阅中心</td>
   <td>为用户提供取消订阅邮寄列表的选项.</td>
  </tr>
  <tr>
   <td>订阅中心</td>
   <td>订阅中心是一个网页，订阅者可以在该网页中控制他们从您的组织收到的消息。</td>
  </tr>
  <tr>
   <td>跟踪电子邮件打开次数</td>
   <td>A hidden component that allows you to use ExactTarget tracking feature.<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只有对电子邮件应用了 ExactTarget 配置，才会填充&#x200B;**选项**&#x200B;下拉菜单。See [Applying Email Service Configuration to Email Settings](#applying-e-mail-service-configuration-to-e-mail-settings) for more information.

1. 将电子邮件发布到 ExactTarget。

   具有电子邮件工具的电子邮件可在已配置的 ExactTarget 帐户中使用。

>[!NOTE]
>
>* The URLs within the email tools are replaced (in the received email) by their actual values only when an email is sent using **Simple Send** or **Guided Send** but not **Test Send**.
   >
   >
* 以下两个电子邮件工具是必需的：**邮寄地址（必需）**&#x200B;和&#x200B;**个人资料中心（必需）**。如果将电子邮件发布到 ExactTarget，这两个电子邮件工具默认均会被添加到每封邮件的底部。
>



### 将文本和个性化工具添加到电子邮件 {#adding-text-and-personalization-tool-to-your-e-mail}

您可以通过将&#x200B;**文本与个性化**&#x200B;组件添加到页面，在电子邮件中添加个性化字段：

1. 打开要发布到电子邮件服务的电子邮件。
1. 要从电子邮件服务中启用个性化字段，请在配置电子邮件服务时添加框架配置。See [configuring Silverpop Engage](/help/sites-administering/silverpop.md) and [configuring Exact Target](/help/sites-administering/exacttarget.md) for more information.
1. Add the component **Text &amp; Personalization** from the sidekick. 此组件是新闻稿组的一部分。以编辑模式打开此组件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 通过从下拉菜单中选择字段并单击&#x200B;**插入**，将所需的个性化字段添加到文本中。
1. 单击&#x200B;**确定**&#x200B;以完成。

## 将电子邮件服务配置应用到电子邮件设置 {#applying-e-mail-service-configuration-to-e-mail-settings}

要将电子邮件服务配置应用到新闻稿，请执行以下操作：

1. 创建电子邮件服务配置。
1. 打开您的电子邮件/新闻稿。
1. Open the email/newsletter settings by either clicking **Settings** or by clicking **Page Properties in** the sidekick.
1. 单击&#x200B;**云服务**&#x200B;选项卡中的&#x200B;**添加服务**。您将看到服务列表。从下拉列表的列表中选择所需的配置 - **ExactTarget** 或 **Silverpop**。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 单击&#x200B;**确定**。

## 将电子邮件发布到电子邮件服务 {#publishing-emails-to-email-service}

可以通过以下步骤将电子邮件/新闻稿发布到电子邮件服务：

1. 打开电子邮件。
1. 在发布电子邮件之前，请确保您已将正确的配置应用到电子邮件。
1. 单击&#x200B;**发布**。This opens the **Publish Newsletter To E-mail Service Provider** window.
1. 填写&#x200B;**新闻稿名称**&#x200B;字段。系统会使用此名称将电子邮件/新闻稿发布到电子邮件服务提供商。如果未提供电子邮件名称，则会使用AEM中新闻稿的页面名称发布电子邮件。
1. 单击&#x200B;**发布**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果发布成功，AEM 会确认您可以在 ExactTarget 或 Silverpop Engage 中查看电子邮件。

   In the case of ExactTarget the published email can ve viewed by clicking **View Published Email**. This takes you directly to the published newsletter in the ExactTarget ([https://members.exacttarget.com/](https://members.exacttarget.com/).).

>[!NOTE]
>
>如果发布的电子邮件/新闻稿与此前已发布的电子邮件/新闻稿名称相同，则早期的电子邮件/新闻稿不会被替换。系统而是会使用同一名称创建一个新的电子邮件/新闻稿（但这两个新闻稿的 ID 不同）。
>
>将电子邮件/新闻稿发布到电子邮件服务提供商还会将电子邮件/新闻稿发布到 AEM 发布实例。


### 更新发布的电子邮件 {#updating-a-published-e-mail}

The **Update** button on the Publish dialog box lets you update a newsletter already published to an E-mail Service Provider. 如果新闻稿尚未发布，而您单击了&#x200B;**更新**&#x200B;按钮，则会显示&#x200B;**新闻稿未发布**&#x200B;消息。

要更新已发布的电子邮件，请执行以下操作：

1. 打开之前已发布到电子邮件服务提供商的电子邮件/新闻稿，您希望对该电子邮件/新闻稿进行更改，然后再重新发布。
1. 单击&#x200B;**发布**。The **Publish Newsletter to Email Service Provider** window displays. Click **Update**.

   To check if the email/newsletter has been updated on ExactTarget, click **View Published Email**. 此操作会使您转到 ExactTarget 中的已发布电子邮件。

   要检查 Silverpop 电子邮件服务中的电子邮件/新闻稿是否已更新，请访问 Silverpop Engage 站点。

