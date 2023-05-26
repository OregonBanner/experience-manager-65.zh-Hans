---
title: 创建有效的新闻稿登陆页面
seo-title: Creating an Effective Newsletter Landing Page
description: 有效的新闻稿登陆页面可帮助您让尽可能多的人注册您的新闻稿（或其他电子邮件营销活动）。 您可以使用从新闻稿注册中收集的信息来获取潜在客户。
seo-description: An effective newsletter landing page helps you get as many people as possible to sign up for your newsletter (or other email marketing campaign). You can use the information you gather from your newsletter sign ups to get leads.
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# 创建有效的新闻稿登陆页面{#creating-an-effective-newsletter-landing-page}

有效的新闻稿登陆页面可帮助您让尽可能多的人注册您的新闻稿（或其他电子邮件营销活动）。 您可以使用从新闻稿注册中收集的信息来获取潜在客户。

要创建有效的新闻稿登陆页面，您需要执行以下操作：

1. 为新闻稿创建列表，以便用户订阅新闻稿。
1. 创建注册表单。 在执行此操作时，请添加一个工作流步骤，该步骤会自动将注册新闻稿的人员添加到您的潜在客户列表中。
1. 创建一个确认页面，以感谢用户注册，并可能为他们提供促销活动。
1. 添加Teaser。

>[!NOTE]
>
>Adobe不打算进一步增强此功能（管理潜在客户和列表）。
>建议利用 [Adobe Campaign和与AEM的集成](/help/sites-administering/campaign.md).

## 为新闻稿创建列表 {#creating-a-list-for-the-newsletter}

创建一个列表，例如， **Geometrixx新闻稿**，用于用户应订阅的新闻稿。 有关创建列表的说明，请参见 [创建列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

下面显示了一个列表示例：

![mcm_listcreate](assets/mcm_listcreate.png)

## 创建注册表单 {#create-a-sign-up-form}

创建新闻稿注册表单，以允许用户订阅标记。 示例Geometrixx网站在Geometrixx工具栏中提供新闻稿页面，您可以在其中创建表单。

要创建您自己的新闻稿表单，请参阅 [Forms文档](/help/sites-authoring/default-components.md#form). 新闻稿使用标记库中的标记。 要添加其他标记，请参阅 [标记管理](/help/sites-authoring/tags.md#tagadministration).

以下示例中的隐藏字段提供了最小信息量（电子邮件）；此外，您可以稍后添加更多字段，但这会影响转化率。

以下示例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html上创建的表单。

1. 创建表单。

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 单击 **编辑** ，以将表单配置为转到感谢页面(请参阅 [创建感谢页面](#creating-a-thank-you-page))。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 设置Form操作（提交表单时将发生这种情况），并配置组以将注册用户分配到您之前创建的列表（例如geometrixx-newsletter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 创建感谢页面 {#creating-a-thank-you-page}

当用户单击时 **立即订阅**，您希望自动打开“感谢”页面。 在Geometrixx新闻稿页面中创建“感谢”页面。 创建新闻稿表单后，编辑表单组件并添加感谢页面的路径。

提交请求会将用户转到 **谢谢** 页面后，他们将收到一封电子邮件。 此“感谢”页面创建于/content/geometrixx/en/toolbar/newsletter/thank_you。

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 添加Teaser {#adding-teasers}

添加 [Teasers](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 以定位特定受众。 例如，您可以将Teaser添加到感谢页面和新闻稿注册页面。

要添加Teaser以使其成为有效的新闻稿登陆页面，请执行以下操作：

1. 为注册礼品创建Teaser段落。 选择 **第一个** 作为策略，并包含通知他们将会收到什么礼物的文本。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 为感谢页面创建Teaser段落。 选择 **第一个** 作为策略，并包含表明礼物即将到来的文本。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用两个Teaser创建营销活动 — 标记一个包含业务，另一个未标记。

### 将内容推送到订阅者 {#pushing-content-to-subscribers}

通过MCM中的新闻稿功能，将任何更改推送到页面。 然后，将更新的内容推送给订阅者。

参见 [发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
