---
title: 与Adobe Experience Cloud集成
description: 了解如何将Adobe Experience Manager与Adobe Experience Cloud集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 4%

---

# 与Adobe Experience Cloud集成{#integrating-with-the-adobe-marketing-cloud}

此 [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html)包括功能强大的Web分析和网站优化产品，这些产品提供可操作的实时数据和见解，以推动成功的在线计划。 它为在线业务优化提供了一个集成和开放的平台。 Cloud由集成的应用程序组成，这些应用程序用于收集并释放客户洞察力，从而优化客户获取、转化和保留工作以及内容的创建和分发。

借助Adobe Experience Manager (AEM)，您可以与以下Adobe Experience Cloud产品无缝集成：

* Adobe Analytics为营销人员提供了有关在线策略和营销活动的可操作、实时的情报。
* Adobe Target使营销人员能够不断使其在线内容与其客户更相关，从而提高转化率。
* Adobe Dynamic Media Classic实现了媒体管理的自动化，简化了Web发布流程，增强了Web体验，所有这些都是在托管环境中实现的。
* AdobeDynamic Tag Management为营销人员提供了直观的工具，可快速轻松地管理无限数量的Adobe和第三方标签。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* 通过Adobe Campaign，可直接在Adobe Experience Manager中管理电子邮件投放内容。

此外，您还可以 [将AEM与Creative Cloud集成](/help/assets/aem-cc-integration-best-practices.md) 和 [第三方服务](/help/sites-administering/third-party-services.md).

## 与 Adobe Analytics 集成 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) 是行业领先的解决方案，为数字营销人员提供一个可以跨多个营销渠道测量、分析和优化所有在线计划的集成数据的位置。 它为营销人员提供了有关数字战略和营销计划的可操作、实时Web分析情报。 Adobe Analytics可帮助营销人员快速找出网站中最有利可图的路径，细分流量以发现高价值Web访客，确定访客离开网站的导航位置，以及确定在线营销活动的关键成功量度。

您可以使用Adobe Analytics分析来自您网站的数据。

与Adobe Analytics集成允许您执行以下操作：

* 启用Analytics用户跟踪。
* 将您的运行模式（例如，创作、发布）映射到不同的报表包。
* 将Client Context变量作为转化变量或流量属性提交。
* 使用预定义的变量映射。
* 一次配置完整的网站区域。
* 跟踪自定义事件。

有关将AEM与Analytics集成的信息，请参阅 [与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md).

您还可以使用 [选择加入向导](/help/sites-administering/opt-in.md) 以轻松执行集成。

## 与 Adobe Target 集成 {#integrating-with-adobe-target}

[营销人员使用 Adobe Target 来设计和执行在线测试、创建动态受众区段（基于行为）以及自动定位内容和在线体验。](https://business.adobe.com/products/target/adobe-target.html)

如今，在线消费者不断演变的需求，期望从各种网站和内容来源获得相关、甚至个性化的内容，以供他们选择。 要吸引在线受众，在线营销人员必须快速确定哪些选件和内容与其受众相关且具有吸引力。 借助这些知识，营销人员需要能够不断改进其站点，并将适当的内容定位到不同的受众。

[与Adobe Target集成](/help/sites-administering/target.md) 介绍如何将您的站点与Target集成。

您还可以使用 [选择加入向导](/help/sites-administering/opt-in.md) 以轻松执行集成。

## 选择启用Analytics和Target {#opting-in-to-analytics-and-target}

AEM提供了一个简单的选择加入过程以与Adobe Analytics和Adobe Target集成。 当您以管理员身份登录并访问“项目”控制台时，您会看到一个选择加入向导。

![chlimage_1-107](assets/chlimage_1-107a.png)

选择与Analytics和/或Target集成，以便能够使用其页面跟踪和分析功能以及个性化功能。 选择加入时，请提供用户帐户信息并指定跟踪的页面。

有关更多信息，请参阅 [选择使用Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 与Adobe Dynamic Media Classic集成 {#integrating-with-scene}

Adobe Dynamic Media Classic是一个托管解决方案，用于发布、管理、增强和提供动态营销资源以及对Web、移动设备、电子邮件、社交媒体、互联网连接显示和打印的丰富可视化促销。

在Adobe Experience Manager中，您可以将数字资源直接从Adobe Experience Manager发布到Dynamic Media Classic，也可以将数字资源从Dynamic Media Classic发布到Adobe Experience Manager。

此外，您还可以通过各种查看器（例如“基本缩放”和“视频”）查看在Dynamic Media Classic中发布的Adobe Experience Manager资源。

有关Adobe Experience Manager如何与Dynamic Media Classic集成的更多信息，请参阅 [与Dynamic Media Classic集成](/help/sites-administering/scene7.md) 文档。

## 与AdobeDynamic Tag Management集成 {#integrating-with-adobe-dynamic-tag-management}

[Adobe动态Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) 为营销人员提供了直观的工具，以便快速轻松地管理无限数量的Adobe和第三方标签。 您拥有更大的控制能力和灵活性，几乎可以在线优化任何内容，同时减少对IT资源的依赖。

[集成AdobeDynamic Tag Management](/help/sites-administering/dtm.md) AEM ，以便您可以使用Dynamic Tag Management Web资产跟踪AEM站点。

## 与Adobe Audience Manager集成 {#integrating-with-adobe-audience-manager}

AEM 6.3中已删除Audience Manager集成。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## 与 Adobe Campaign 集成 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) 允许您直接在Adobe Experience Manager中管理电子邮件投放内容。

有关AEM如何与Adobe Campaign集成的信息，请参阅 [与Adobe Campaign集成](/help/sites-administering/campaignstandard.md).