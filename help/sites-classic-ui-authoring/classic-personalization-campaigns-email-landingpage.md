---
title: 创建有效的新闻稿登陆页面
seo-title: 创建有效的新闻稿登陆页面
description: 有效的新闻稿登陆页面可帮助您获取尽可能多的用户注册您的新闻稿（或其他电子邮件营销活动）。您可以使用通过新闻稿注册收集的信息来获取潜在客户。
seo-description: 有效的新闻稿登陆页面可帮助您获取尽可能多的用户注册您的新闻稿（或其他电子邮件营销活动）。您可以使用通过新闻稿注册收集的信息来获取潜在客户。
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 创建有效的新闻稿登陆页面{#creating-an-effective-newsletter-landing-page}

有效的新闻稿登陆页面可帮助您获取尽可能多的用户注册您的新闻稿（或其他电子邮件营销活动）。您可以使用通过新闻稿注册收集的信息来获取潜在客户。

要创建有效的新闻稿登陆页面，您需要执行以下操作：

1. 为新闻稿创建列表，以使用户可以订阅新闻稿。
1. 创建注册表单。在执行该操作时，添加一个工作流步骤，以便自动将注册新闻稿的用户添加到潜在客户列表。
1. 创建确认页面，感谢用户注册，也可以向其提供促销活动。
1. 添加 Teaser。

>[!NOTE]
>
>Adobe 不打算进一步增强此功能（管理潜在客户和列表）。
>Adobe 的建议是利用 [Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

## 为新闻稿创建列表 {#creating-a-list-for-the-newsletter}

在 MCM 中为用户订阅的新闻稿创建列表，例如 **Geometrixx 新闻稿**。[创建列表](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists)中介绍了如何创建列表。

列表示例如下所示：

![mcm_listcreate](assets/mcm_listcreate.png)

## 创建注册表单 {#create-a-sign-up-form}

创建新闻稿注册表单，以便用户订阅标记。示例 Geometrixx 网站在 Geometrixx 工具栏中提供了新闻稿页面，您可在此创建表单。

要创建自己的新闻稿表单，请参阅[表单文档](/help/sites-authoring/default-components.md#form)中有关创建表单的信息。新闻稿会使用标记库中的标记。要添加其他标记，请参阅[标记管理](/help/sites-authoring/tags.md#tagadministration)。

以下示例中的隐藏字段提供最少量的信息（电子邮件）；此外，您以后还可以添加更多字段，但这样会影响转换速率。

以下示例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html上创建的表单。

1. 创建表单。

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 在表单组件中单击&#x200B;**编辑**&#x200B;以配置表单，使其转到感谢页面（请参阅[创建感谢页面](#creating-a-thank-you-page)）。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 设置表单操作（即提交表单时执行的操作），并配置组，以将注册用户分配到之前创建的列表（例如 Geometrixx-Newsletter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 创建感谢页面 {#creating-a-thank-you-page}

当用户单击&#x200B;**立即订阅**&#x200B;时，需要感谢页面自动打开。在 Geometrixx 新闻稿页面中创建感谢页面。在创建 Newsletter 表单后，编辑该表单组件，并在感谢页面中添加路径。

提交请求操作将使用户转到&#x200B;**感谢**&#x200B;页面，随后用户会收到一封电子邮件。该感谢页面是在 /content/geometrixx/cn/toolbar/newsletter/thank_you 创建的。

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 添加 Teaser {#adding-teasers}

可添加 [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 来定位特定受众。例如，您可以向感谢页面和 Newsletter 注册页面添加 Teaser。

添加 Teaser 以制作有效的 Newsletter 登陆页面：

1. 为注册礼品创建 Teaser 段落。选择&#x200B;**第一个**&#x200B;作为战略，并包含通知用户他们将收到的礼品的文本。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 为感谢页面创建 Teaser 段落。选择&#x200B;**第一个**&#x200B;作为战略，并包含指示礼品已发出的文本。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用两个 Teaser 创建市场活动 -- 一个带有企业标记，一个没有企业标记。

### 将内容推送给订阅者 {#pushing-content-to-subscribers}

通过 MCM 中的新闻稿功能将所有更改内容推送到页面中。然后向订阅者推送更新内容。

请参阅[发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)。
