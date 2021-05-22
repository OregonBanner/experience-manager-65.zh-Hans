---
title: 与Adobe Marketing Cloud集成
description: 了解如何将Adobe Experience Manager与Adobe Marketing Cloud集成。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# 与Adobe Marketing Cloud集成{#integrating-with-the-adobe-marketing-cloud}

[Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)包含功能强大的Web分析和网站优化产品，可提供可操作的实时数据和洞察信息，以推动成功的在线计划。 它为在线业务优化提供了集成且开放的平台。 云由集成应用程序组成，这些应用程序可收集和释放客户洞察力，从而优化客户获取、转化和保留工作以及内容的创建和分发。

通过Adobe Experience Manager(AEM)，您可以与Adobe Marketing Cloud的以下产品无缝集成：

* Adobe Analytics为营销人员提供有关在线策略和营销计划的可操作实时信息。
* Adobe Target使营销人员能够持续提升其在线内容与其客户的相关性，从而提高转化率。
* AdobeDynamic Media Classic可自动化媒体管理、简化Web发布并增强Web体验，所有这些操作都在托管环境中完成。
* Adobe动态标签管理为营销人员提供了直观的工具，可快速轻松地管理无限数量的Adobe和第三方标签。
* AdobeSearch&amp;Promote使营销人员能够控制和优化其网站上的搜索结果。
* Adobe Campaign允许您直接在Adobe Experience Manager中管理电子邮件投放内容。

此外，您还可以[将AEM与Creative Cloud](/help/assets/aem-cc-integration-best-practices.md)和与[第三方服务](/help/sites-administering/third-party-services.md)集成。

## 与 Adobe Analytics 集成 {#integrating-with-adobe-analytics}

[Adobe](https://www.omniture.com/en/products/analytics/sitecatalyst) 分析是一款行业领先的解决方案，为数字营销人员提供了一个测量、分析和优化跨多个营销渠道所有在线计划的集成数据的位置。它为营销人员提供了有关数字策略和营销计划的可操作实时Web分析智能。 Adobe Analytics可帮助营销人员快速识别通过网站获得最高利润的路径，细分流量以发现高价值Web访客，确定访客在何处导航离开网站，并确定在线营销活动的关键成功量度。

您可以使用Adobe Analytics分析网站中的数据。

与Adobe Analytics集成后，您可以执行以下操作：

* 启用Analytics用户跟踪。
* 将您的运行模式（例如，创作、发布）映射到不同的报表包。
* 将Client Context变量作为转化变量或流量属性提交。
* 使用预定义的变量映射。
* 一次配置整个网站区域。
* 跟踪自定义事件。

有关将AEM与Analytics集成的信息，请参阅[与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md)。

您还可以使用[选择加入向导](/help/sites-administering/opt-in.md)轻松执行集成。

## 与 Adobe Target 集成 {#integrating-with-adobe-target}

[Adobe](https://www.omniture.com/en/products/conversion/test-and-target) 营销人员使用的定位功能，可设计和执行在线测试、创建即时受众区段（基于行为）并自动定位内容和在线体验。

如今，在线消费者的需求不断变化，希望从他们可以选择的各种网站和内容源中获得相关、甚至是个性化的内容。 要吸引在线受众，在线营销人员必须快速确定哪些选件和内容对其受众具有相关性和吸引力，这一点至关重要。 借助这些知识，营销人员需要能够不断改进其网站，并将相应内容定位到不同的受众。

[与Adobe集](/help/sites-administering/target.md) 成Target介绍如何将您的网站与Target集成。

您还可以使用[选择加入向导](/help/sites-administering/opt-in.md)轻松执行集成。

## 选择启用Analytics和Target {#opting-in-to-analytics-and-target}

AEM提供了一个简单的选择加入过程，以便与Adobe Analytics和Adobe Target集成。 当您以管理员身份登录并访问项目控制台时，将显示一个选择加入向导。

![chlimage_1-107](assets/chlimage_1-107a.png)

选择加入与Analytics和/或Target的集成，以便能够使用其页面跟踪和分析功能以及个性化功能。 选择加入后，您需要提供用户帐户信息并指定要跟踪的页面。

有关更多信息，请参阅[选择加入Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 与AdobeDynamic Media Classic {#integrating-with-scene}集成

AdobeDynamic Media Classic是一个托管解决方案，用于发布、管理、增强和将动态营销资产和丰富的可视化促销内容交付到Web、移动设备、电子邮件、社交媒体、连接Internet的显示屏和打印设备。

在Adobe Experience Manager中，您可以将数字资产直接从Adobe Experience Manager发布到Dynamic Media Classic，也可以将数字资产从Dynamic Media Classic发布到Adobe Experience Manager。

此外，您还可以在各种查看器（如基本缩放和视频）中查看在Dynamic Media Classic中发布的Adobe Experience Manager资产。

有关Adobe Experience Manager如何与Dynamic Media Classic集成的更多信息，请参阅[与Dynamic Media Classic集成](/help/sites-administering/scene7.md)文档。

## 与Adobe动态标签管理集成{#integrating-with-adobe-dynamic-tag-management}

[Adobe动态标签](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) 管理为营销人员提供了直观的工具，可快速轻松地管理无限数量的Adobe和第三方标签。您将拥有更多的控制和灵活性，几乎可以在线优化任何内容，同时减少对IT资源的依赖。

[将Adobe动态标](/help/sites-administering/dtm.md) 签管理与AEM集成，以便您能够使用动态标签管理Web属性来跟踪AEM网站。

## 与Adobe Audience Manager集成{#integrating-with-adobe-audience-manager}

Audience Manager集成已在AEM 6.3中删除。

## 与Search&amp;Promote{#integrating-with-search-promote}集成

AdobeSearch&amp;Promote使营销人员能够优化访客在网站和移动网站上浏览、查找、比较和选择相关产品和内容的方式。 企业可以根据业务目标和访客意图轻松促销优先级项目，并通过基于KPI的触发器或量度自动执行促销和促销活动。

AdobeSearch&amp;Promote是一个可靠且可扩展的托管站点搜索应用程序，能够扩展到数百万个页面或产品，适用于从零售到新闻网站等访问量很大的在线业务。 它提供了前所未有的营销人员控制和基于量度的相关性级别。

有关集成AEM和Search&amp;Promote的信息，请参阅[与AdobeSearch&amp;Promote集成](/help/sites-administering/search-and-promote.md)。

## 与Adobe Campaign集成{#integrating-with-adobe-campaign}

[Adobe](https://www.adobe.com/solutions/campaign-management.html) 营销活动允许您直接在Adobe Experience Manager中管理电子邮件投放内容。

有关AEM如何与Adobe Campaign集成的信息，请参阅[与Adobe Campaign集成](/help/sites-administering/campaignstandard.md)。

## 与 Livefyre 集成 {#integrating-with-livefyre}

了解AEM和Livefyre:

* [Livefyre快速入门](https://answers.livefyre.com/developers/getting-started)

* [Livefyre 和 AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
