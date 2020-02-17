---
title: 营销活动管理
seo-title: 营销活动管理
description: 营销活动管理为数字营销人员提供了发布个性化内容，进而为访客创建专有体验的机会。它可让您通过网络、电子邮件和移动服务精心策划市场营销活动，以此来吸引您的访客。
seo-description: 营销活动管理为数字营销人员提供了发布个性化内容，进而为访客创建专有体验的机会。它可让您通过网络、电子邮件和移动服务精心策划市场营销活动，以此来吸引您的访客。
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 营销活动管理{#campaign-management}

营销活动管理为数字营销人员提供了发布个性化内容，进而为访客创建专有体验的机会。

它可让您通过网络、电子邮件和移动服务精心策划市场营销活动，以此来吸引您的访客。您可以创建内容、划分访客区段、向特定的用户个人资料推动和宣传目标内容，并且通过多种渠道管理营销活动。

本文档介绍了组成营销活动的各种元素。有关更多详细信息，请参阅以下文档：

* [Teaser 和战略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [电子邮件营销](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target 选件](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用营销活动管理器](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [设置您的营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

营销活动管理由多种元素组成：

* **品牌**
In AEM, brands are the top level unit and form a collection of **Campaigns**.

* **营销活动**&#x200B;营销活动是各个&#x200B;**体验**&#x200B;的集合。

* **体验**&#x200B;有目标性的内容构成了各种体验，在&#x200B;**触点**&#x200B;呈现给访客。有若干类型的体验：

   * **Teaser**
      [Teaser页面／段落](#teasers) ，用于将特定访客区段定向 **** 到其感兴趣的内容。

      Teaser 页面可以：

      * 呈现一系列选项以供访客选择
      * 仅显示一个基于特定访客段的 Teaser 段落；例如，显示的 Teaser 段落可能取决于访客的年龄。
      通常，Teaser 页面是一个临时操作，它将持续特定时间段，直到由下一个 Teaser 页面取代。

   * **新闻稿**

      [可使用电子邮件通信](#emailmarketing)来吸引用户，并鼓励他们访问您的网站。它们通常采用新闻稿的形式，新闻稿会发送给您的&#x200B;**潜在客户**（通常分组到&#x200B;**列表**&#x200B;中）。**注意：** Adobe 不打算进一步增强此功能。Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

   * **Adobe Target**

      这允许与 Adobe Target（以前为 Test&amp;Target）相集成，Adobe Target 为营销人员提供了转化网站优化工具，该工具可以持续保持在线内容和选件与其客户的相关性，从而提高转化率。Adobe Target 提供了直观界面，可用于设计和执行测试、创建受众区段以及对内容定位 - 所有这些只需一个应用程序。


* **触点**

   这些是访客与您的营销活动之间的接触点。这些触点与您创建的体验相关联。

   例如，对于 teaser，它是 teaser 段落所在的内容页面；对于 newsletter，它是邮寄列表。

* **潜在客户**

   您收集的关于您的访客及其联系方式的信息构成了潜在客户的基本内容。**注意：** Adobe 不打算进一步增强此功能。

   Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

* **列表**

   潜在客户通常被划分到列表中，这样您可以对他们采取同样的操作。**注意：** Adobe 不打算进一步增强此功能。

   Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

* **区段**

   站点访客在访问站点时的兴趣和目标各不相同。根据各种因素（如网站上的活动、注册的个人资料信息和其他网站上的活动）对此进行分析可帮助您定义区段。然后，可以根据访客所在的区段来向访客提供满足其需要和兴趣的内容。

* **MCM**

   营销活动管理器 (MCM) 是一个控制台，可让您访问需要创建的所有功能并控制您的营销活动、品牌、体验、触点、潜在客户、列表、区段和报告。

   可以从各种位置（标记为&#x200B;**营销活动**）或使用 URL 来访问它，例如：

   `http://localhost:4502/libs/mcm/content/admin.html`

