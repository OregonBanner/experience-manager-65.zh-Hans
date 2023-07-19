---
title: 将电子邮件发布到电子邮件服务提供商
seo-title: Publishing an Email to Email Service Providers
description: 您可以将新闻稿发布到电子邮件服务，例如ExactTarget和Silverpop Engage。
seo-description: You can publish newsletters to e-mail services such as ExactTarget and Silverpop Engage.
uuid: 1a7adcfe-8e52-49f4-9a00-99ac99881225
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b9618913-5433-4baf-9ff6-490a26860505
exl-id: c07692f7-3618-4e8c-96d7-4db09f2d9896
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 3%

---

# 将电子邮件发布到电子邮件服务提供商{#publishing-an-email-to-email-service-providers}

您可以将新闻稿发布到电子邮件服务，例如ExactTarget和Silverpop Engage。 本文档介绍如何配置AEM以向这些电子邮件服务发布新闻稿。

>[!NOTE]
>
>您需要先配置服务提供商，然后才能创建和发布电子邮件。 参见 [配置ExactTarget](/help/sites-administering/exacttarget.md) 和 [配置Silverpop Engage](/help/sites-administering/silverpop.md) 了解更多信息。

要将电子邮件发布到电子邮件服务提供商，您需要执行以下步骤：

1. 创建电子邮件。
1. 将电子邮件服务配置应用于电子邮件。
1. 发布电子邮件。

>[!NOTE]
>
>如果您更新电子邮件提供商、进行试运行测试或发送新闻稿，则当新闻稿未先发布到发布实例或者发布实例不可用时，这些操作将失败。 确保发布新闻稿，并确保Publish实例已启动且正在运行。

## 创建电子邮件 {#creating-an-email}

可以在营销策划下使用创建要发布到电子邮件服务的电子邮件或新闻稿 **Geometrixx新闻稿** 模板。 您还可以使用 **Geometrixx Outdoors电子邮件** 模板。 基于的示例电子邮件/新闻稿 **Geometrixx Outdoors电子邮件** 模板位于 `https://<hostname>:<port>/cf#/content/campaigns/geometrixx-outdoors/e-mails.html`.

要创建发布到配置的电子邮件服务的新电子邮件，请执行以下操作：

1. 转到 **网站** 然后 **营销活动**. 选择营销策划。
1. 单击 **新** 以打开 **创建页面** 窗口。
1. 输入标题、名称，然后选择 **Geometrixx新闻稿** 模板。
1. 单击&#x200B;**创建**。
1. 打开创建的电子邮件。
1. 切换到设计模式以选择要在Sidekick中显示的组件。
1. 切换到编辑模式并开始添加内容(文本、图像、 [电子邮件工具](#adding-exacttarget-email-tools-to-your-email)， [个性化变量](#adding-text-and-personalization-tool-to-your-e-mail)，以此类推)添加到您的电子邮件中。

### 将ExactTarget电子邮件工具添加到电子邮件 {#adding-exacttarget-email-tools-to-your-email}

>[!NOTE]
>
>此部分特定于ExactTarget服务。

此 **电子邮件工具** exacttarget组件可以为您的电子邮件/新闻稿添加更多电子邮件功能。

1. 打开电子邮件以发布到ExactTarget。
1. 添加组件 **ET — 电子邮件工具** 使用副手进入您的页面。 在编辑模式下打开组件。

   ![chlimage_1](assets/chlimage_1.gif)

1. 从中选择选项 **选项** 菜单：

<table>
 <tbody>
  <tr>
   <td>邮寄地址(必需)</td>
   <td>此组件在电子邮件中插入贵组织的实际邮寄地址。</td>
  </tr>
  <tr>
   <td>个人资料中心(必需)</td>
   <td>用户档案中心是一个网页，订阅者可以在其中输入和维护您保留的有关他们的个人信息。</td>
  </tr>
  <tr>
   <td>以网页的形式查看电子邮件</td>
   <td>此组件允许用户以网页的形式查看电子邮件。</td>
  </tr>
  <tr>
   <td>隐私政策</td>
   <td>此组件在电子邮件中插入指向您的隐私策略的链接。<br /> </td>
  </tr>
  <tr>
   <td>取消订阅中心</td>
   <td>为用户提供了取消订阅邮寄列表的选项。</td>
  </tr>
  <tr>
   <td>订阅中心</td>
   <td>订阅中心是一个网页，订阅者可以在其中控制从您的组织接收的消息。</td>
  </tr>
  <tr>
   <td>跟踪电子邮件打开次数</td>
   <td>一个允许您使用ExactTarget跟踪功能的隐藏组件。<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 **选项** 仅当将ExactTarget配置应用于电子邮件时，才会填充下拉菜单。 参见 [将电子邮件服务配置应用到电子邮件设置](#applying-e-mail-service-configuration-to-e-mail-settings) 了解更多信息。

1. 将电子邮件发布到ExactTarget。

   带有电子邮件工具的电子邮件可在配置的ExactTarget帐户中使用。

>[!NOTE]
>
>* 仅当使用发送电子邮件时，电子邮件工具中的URL（在收到的电子邮件中）才会被替换为实际值 **简单发送** 或 **引导式发送** 但不是 **测试发送**.
>
>* 需要以下两种电子邮件工具： **邮寄地址（必需）** 和 **配置文件中心（必需）**. 将电子邮件发布到ExactTarget后，默认情况下会将这两个电子邮件工具添加到每封邮件的底部。
>

### 向电子邮件添加文本和个性化工具 {#adding-text-and-personalization-tool-to-your-e-mail}

您可以通过添加 **文本和个性化** 页面组件：

1. 打开要发布到电子邮件服务的电子邮件。
1. 要启用电子邮件服务中的个性化字段，请在配置电子邮件服务时添加框架配置。 参见 [配置Silverpop Engage](/help/sites-administering/silverpop.md) 和 [配置Exact Target](/help/sites-administering/exacttarget.md) 了解更多信息。
1. 添加组件 **文本和个性化** 从副手手手手里。 此组件是新闻稿组的一部分。 在编辑模式下打开此组件。

   ![chlimage_1-110](assets/chlimage_1-110a.png)

1. 通过从下拉菜单中选择所需的个性化字段并单击 **插入**.
1. 单击 **确定** 完成。

## 将电子邮件服务配置应用到电子邮件设置 {#applying-e-mail-service-configuration-to-e-mail-settings}

要将电子邮件服务配置应用到新闻稿，请执行以下操作：

1. 创建电子邮件服务配置。
1. 打开您的电子邮件/新闻稿。
1. 通过单击以下任一按钮打开电子邮件/新闻稿设置 **设置** 或通过单击 **中的页面属性** 副手。
1. 单击 **添加服务** 在 **Cloud Services** 选项卡。 您会看到服务列表。 选择所需的配置 —  **ExactTarget** 或 **Silverpop**  — 从下拉列表中的列表。

   ![chlimage_1-5](assets/chlimage_1-5a.jpeg)

1. 单击&#x200B;**确定**。

## 将电子邮件发布到电子邮件服务 {#publishing-emails-to-email-service}

可以按照以下步骤将电子邮件/新闻稿发布到您的电子邮件服务：

1. 打开电子邮件。
1. 在发布电子邮件之前，请确保已将正确的配置应用于电子邮件。
1. 单击&#x200B;**发布**。这将打开 **将新闻稿发布到电子邮件服务提供商** 窗口。
1. 填写 **新闻稿名称** 字段。 电子邮件/新闻稿将发布到此名称的电子邮件服务提供商。 如果未提供电子邮件名称，则使用AEM中新闻稿的页面名称发布电子邮件。
1. 单击&#x200B;**发布**。

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

   如果成功，AEM将确认您可以在ExactTarget或Silverpop Engage中查看电子邮件。

   对于ExactTarget，可以通过单击 **查看已发布的电子邮件**. 这会将您直接转到ExactTarget中已发布的新闻稿([https://members.exacttarget.com/](https://members.exacttarget.com/).)。

>[!NOTE]
>
>如果电子邮件/新闻稿的发布名称与已发布的电子邮件/新闻稿的名称相同，则不会替换之前的电子邮件/新闻稿。 而是使用相同的名称创建新的电子邮件/新闻稿（但两个新闻稿的ID不同）。
>
>将电子邮件/新闻稿发布到电子邮件服务提供商还会将电子邮件/新闻稿发布到AEM发布实例。
>

### 更新已发布的电子邮件 {#updating-a-published-e-mail}

此 **更新** 通过“发布”对话框上的按钮，您可以更新已发布到电子邮件服务提供商的新闻稿。 如果新闻稿尚未发布，并且 **更新** 已单击按钮，a **新闻稿未发布** 将显示消息。

要更新已发布的电子邮件，请执行以下操作：

1. 打开之前已发布到电子邮件服务提供商的电子邮件/新闻稿，在对电子邮件/新闻稿进行更改后，您要重新发布该电子邮件服务提供商。
1. 单击&#x200B;**发布**。此 **将新闻稿发布到电子邮件服务提供商** 窗口随即显示。 单击&#x200B;**更新**。

   要检查电子邮件/新闻稿是否已在ExactTarget上更新，请单击 **查看已发布的电子邮件**. 这会将您转到在ExactTarget中发布的电子邮件。

   要检查Silverpop电子邮件服务上的电子邮件/新闻稿是否已更新，请访问Silverpop Engage网站。
