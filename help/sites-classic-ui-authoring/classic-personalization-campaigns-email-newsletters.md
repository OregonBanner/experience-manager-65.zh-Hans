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
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 75%

---

# 将电子邮件发布到电子邮件服务提供商{#publishing-an-email-to-email-service-providers}

您可以将新闻稿发布到电子邮件服务，如 ExactTarget 和 Silverpop Engage。本文档介绍如何配置 AEM 以将新闻稿发布到这些电子邮件服务。

>[!NOTE]
>
>您需要先配置服务提供商，然后才能创建和发布电子邮件。有关更多信息，请参阅[配置ExactTarget](/help/sites-administering/exacttarget.md)和[配置Silverpop Engage](/help/sites-administering/silverpop.md)。

要将您的电子邮件发布到电子邮件服务提供商，您需要执行以下步骤：

1. 创建电子邮件。
1. 将电子邮件服务配置应用到电子邮件。
1. 发布电子邮件。

>[!NOTE]
>
>如果没有先将新闻稿发布到发布实例，或发布实例不可用，则以下操作将失败：更新电子邮件提供商、执行试运行，或发送新闻稿。请务必发布您的新闻稿，并确保发布实例已启动且正在运行。

## 创建电子邮件  {#creating-an-email}

您可以使用&#x200B;**Geometrixx新闻稿**&#x200B;模板在营销活动下创建要发布到电子邮件服务的电子邮件或新闻稿。 您也可以使用 **Geometrixx Outdoors 电子邮件**&#x200B;模板。基于&#x200B;**Geometrixx Outdoors电子邮件**&#x200B;模板的示例电子邮件/新闻稿可在`https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`中找到。

要创建发布到所配置电子邮件服务的新电子邮件，请执行以下操作：

1. 转到&#x200B;**网站**，然后转到&#x200B;**营销活动**。 选择营销活动。
1. 单击&#x200B;**新建**&#x200B;以打开&#x200B;**创建页面**&#x200B;窗口。
1. 输入标题、名称，然后从可用模板列表中选择 **Geometrixx 新闻稿**&#x200B;模板。
1. 单击&#x200B;**创建**。
1. 打开创建的电子邮件。
1. 切换到设计模式以选择要在 Sidekick 中显示的组件。
1. 切换到编辑模式，然后开始向电子邮件中添加内容（文本、图像、[电子邮件工具](#adding-exacttarget-email-tools-to-your-email)、[个性化变量](#adding-text-and-personalization-tool-to-your-e-mail)等）。

### 将 ExactTarget 电子邮件工具添加到电子邮件 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>此部分内容针对的是 ExactTarget 服务。

使用 ExactTarget 的&#x200B;**电子邮件工具**&#x200B;组件，可以向电子邮件/新闻稿中添加更多电子邮件功能。

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
   <td>此组件会在电子邮件中插入指向隐私政策的链接。<br /> </td>
  </tr>
  <tr>
   <td>取消订阅中心</td>
   <td>为用户提供取消订阅邮寄列表的选项.</td>
  </tr>
  <tr>
   <td>订阅中心</td>
   <td>订阅中心是一个网页，订阅者可以在该网页中控制他们从贵组织收到的消息。</td>
  </tr>
  <tr>
   <td>跟踪电子邮件打开次数</td>
   <td>允许您使用ExactTarget跟踪功能的隐藏组件。<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>只有对电子邮件应用了 ExactTarget 配置，才会填充&#x200B;**选项**&#x200B;下拉菜单。有关更多信息，请参阅[将电子邮件服务配置应用到电子邮件设置](#applying-e-mail-service-configuration-to-e-mail-settings)。

1. 将电子邮件发布到 ExactTarget。

   具有电子邮件工具的电子邮件可在已配置的 ExactTarget 帐户中使用。

>[!NOTE]
>
>* 仅当使用&#x200B;**Simple Send**&#x200B;或&#x200B;**Guided Send**（而非&#x200B;**Test Send**）发送电子邮件时，电子邮件工具中的URL才会被其实际值替换（在收到的电子邮件中）。
   >
   >
* 以下两个电子邮件工具是必需的：**邮寄地址（必需）**&#x200B;和&#x200B;**个人资料中心（必需）**。如果将电子邮件发布到 ExactTarget，这两个电子邮件工具默认均会被添加到每封邮件的底部。

>



### 将文本和个性化工具添加到电子邮件  {#adding-text-and-personalization-tool-to-your-e-mail}

您可以通过将&#x200B;**文本与个性化**&#x200B;组件添加到页面，在电子邮件中添加个性化字段：

1. 打开要发布到电子邮件服务的电子邮件。
1. 要从电子邮件服务中启用个性化字段，请在配置电子邮件服务时添加框架配置。有关更多信息，请参阅[配置Silverpop Engage](/help/sites-administering/silverpop.md)和[配置ExactTarget](/help/sites-administering/exacttarget.md)。
1. 从Sidekick中添加组件&#x200B;**Text &amp; Personalization**。 此组件是新闻稿组的一部分。以编辑模式打开此组件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 通过从下拉菜单中选择字段并单击&#x200B;**插入**，将所需的个性化字段添加到文本中。
1. 单击&#x200B;**确定**&#x200B;以完成。

## 将电子邮件服务配置应用到电子邮件设置 {#applying-e-mail-service-configuration-to-e-mail-settings}

要将电子邮件服务配置应用到新闻稿，请执行以下操作：

1. 创建电子邮件服务配置。
1. 打开您的电子邮件/新闻稿。
1. 通过单击&#x200B;**设置**&#x200B;或单击Sidekick中的&#x200B;**页面属性，打开电子邮件/新闻稿设置。**
1. 单击&#x200B;**云服务**&#x200B;选项卡中的&#x200B;**添加服务**。您将看到服务列表。从下拉列表的列表中选择所需的配置 - **ExactTarget** 或 **Silverpop**。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 单击&#x200B;**确定**。

## 将电子邮件发布到电子邮件服务 {#publishing-emails-to-email-service}

可以通过以下步骤将电子邮件/新闻稿发布到电子邮件服务：

1. 打开电子邮件。
1. 在发布电子邮件之前，请确保您已将正确的配置应用到电子邮件。
1. 单击&#x200B;**发布**。此操作将打开&#x200B;**将新闻稿发布到电子邮件服务提供商**&#x200B;窗口。
1. 填写&#x200B;**新闻稿名称**&#x200B;字段。系统会使用此名称将电子邮件/新闻稿发布到电子邮件服务提供商。如果未提供电子邮件名称，则会使用 AEM 中新闻稿的页面名称发布电子邮件。
1. 单击&#x200B;**发布**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果发布成功，AEM 会确认您可以在 ExactTarget 或 Silverpop Engage 中查看电子邮件。

   对于ExactTarget，可以通过单击&#x200B;**查看已发布的电子邮件**&#x200B;来查看已发布的电子邮件。 这会将您直接转到ExactTarget([https://members.exacttarget.com/](https://members.exacttarget.com/))中发布的Newsletter。

>[!NOTE]
>
>如果发布的电子邮件/新闻稿与此前已发布的电子邮件/新闻稿名称相同，则早期的电子邮件/新闻稿不会被替换。系统而是会使用同一名称创建一个新的电子邮件/新闻稿（但这两个新闻稿的 ID 不同）。
>
>将电子邮件/新闻稿发布到电子邮件服务提供商还会将电子邮件/新闻稿发布到 AEM 发布实例。


### 更新发布的电子邮件 {#updating-a-published-e-mail}

通过“发布”对话框上的&#x200B;**更新**&#x200B;按钮，您可以更新已发布到电子邮件服务提供商的新闻稿。 如果新闻稿尚未发布，而您单击了&#x200B;**更新**&#x200B;按钮，则会显示&#x200B;**新闻稿未发布**&#x200B;消息。

要更新已发布的电子邮件，请执行以下操作：

1. 打开之前已发布到电子邮件服务提供商的电子邮件/新闻稿，您希望对该电子邮件/新闻稿进行更改，然后再重新发布。
1. 单击&#x200B;**发布**。此时会显示&#x200B;**将新闻稿发布到电子邮件服务提供商**&#x200B;窗口。 单击&#x200B;**Update**。

   要检查ExactTarget上的电子邮件/Newsletter是否已更新，请单击&#x200B;**查看已发布的电子邮件**。 此操作会使您转到 ExactTarget 中的已发布电子邮件。

   要检查 Silverpop 电子邮件服务中的电子邮件/新闻稿是否已更新，请访问 Silverpop Engage 站点。
