---
title: Campaign Management
seo-title: Campaign Management
description: Campaign管理为数字营销人员提供了交付个性化内容并为访客创建专用体验的机会。 它允许您跨Web、电子邮件和移动服务编排营销活动，从而吸引访客。
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Campaign Management{#campaign-management}

Campaign管理为数字营销人员提供了交付个性化内容并为访客创建专用体验的机会。

它允许您跨Web、电子邮件和移动服务编排营销活动，从而吸引访客。 您可以为特定用户配置文件创建内容、细分访客、推送和提升目标内容以及跨多个渠道管理营销活动。

本文档介绍了构成营销活动的各种元素。 更多详细信息见以下文档：

* [Teaser和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [电子邮件营销](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登录页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target优惠](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用营销活动经理](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [设置活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

营销活动管理由各种元素组成：

* **品牌**
在AEM中，品牌是顶层单位，构成一个集合 
**营销活动**.

* **营销活动**
营销活动是个人的集合 
**体验**.

* **体验**
重点内容构成了各种体验，在提供给访客的 
**Touchpoints**. 有多种类型的体验可用：

   * **Teaser**
      [Teaser页面/段落](#teasers) 用于引导特定访客 **区段** 关注他们兴趣的内容。

      Teaser页面可以：

      * 提供一系列可供访客选择的选项
      * 仅显示基于特定访客区段的Teaser段落；例如，显示的Teaser段落可能取决于访客的年龄。

      通常，Teaser页面是一种临时操作，将持续特定时段，直到它被下一个Teaser页面替换。

   * **快讯**

      [电子邮件通信](#emailmarketing) 用于吸引用户并鼓励他们访问您的网站。 这些通知通常采用新闻稿的形式，发送给贵机构的 **潜在客户** (通常分为 **列表**)。 **注意：** Adobe不打算进一步增强此功能。 建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

   * **Adobe Target**

      这允许与Adobe Target（以前称为Test&amp;Target）集成，后者为营销人员提供了一个转化网站优化工具，该工具提供了必要的功能，以便始终提供与其客户更密切相关的在线内容和选件，从而提高了转化率。 Adobe Target提供了一个直观的界面，可用于设计和执行测试、创建受众区段以及定位内容 — 所有这些都可通过单个应用程序实现。


* **Touchpoints**

   这些是访客与营销活动之间的联系点。 接触点会连接到您创建的体验。

   例如，对于Teaser，它是Teaser段落所在的内容页面；对于新闻稿，它是邮寄列表。

* **潜在客户**

   您收集到的有关访客以及如何联系这些访客的信息构成了潜在客户的基础。 **注意：** Adobe不打算进一步增强此功能。

   建议为 [利用Adobe Campaign以及与AEM的集成](/help/sites-administering/campaign.md).

* **列表**

   潜在客户通常会分组到列表中，以便您能够对其采取集体行动。 注意： **注意：** Adobe不打算进一步增强此功能。

   建议为 [利用Adobe Campaign以及与AEM的集成。](/help/sites-administering/campaign.md)

* **区段**

   网站访客访问网站时具有不同的兴趣和目标。 根据网站上的活动、注册的用户档案信息和其他网站上的活动等因素对此进行分析，可帮助您定义区段。 然后，可以根据访客匹配的区段，专门将内容定位到访客的需求和兴趣上。

* **MCM**

   营销活动管理器(MCM)是一个控制台，允许您访问创建和控制营销活动、品牌、体验、接触点、潜在客户、列表、区段和报告所需的所有功能。

   可从各种位置访问(标记为 **营销活动**)，或者使用URL进行访问：

   `http://localhost:4502/libs/mcm/content/admin.html`
