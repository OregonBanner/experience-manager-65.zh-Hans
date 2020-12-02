---
title: 与Adobe Marketing Cloud整合
seo-title: 与Adobe Marketing Cloud整合
description: 了解如何将AEM与Adobe Marketing Cloud集成。
seo-description: 了解如何将AEM与Adobe Marketing Cloud集成。
uuid: 36d71dd3-7fb0-4237-99d3-4fbb2e162e7b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: ba496f6a-c9aa-49b5-8207-8633748d2c17
translation-type: tm+mt
source-git-commit: 471b57a52efc849eb57201e6397221fa4f88c746
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 2%

---


# 与Adobe Marketing Cloud集成{#integrating-with-the-adobe-marketing-cloud}

[Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html)包含功能强大的网络分析和网站优化产品，这些产品可提供可操作的实时数据和洞察，以推动成功的在线计划。 它优惠了一个集成的开放式平台，用于在线业务优化。 云包括集成应用程序，用于收集和释放客户洞察力，以优化客户赢取、转化和保留工作以及内容的创建和分发。

通过Adobe Experience Manager(AEM)，您可以与Adobe Marketing Cloud的以下产品无缝集成：

* Adobe Analytics公司为营销人员提供有关在线战略和营销计划的可操作实时情报。
* Adobe Target使营销人员能够持续提高其在线内容与其客户的相关性，从而提高转化率。
* Adobe Scene7通过一个托管环境实现媒体管理自动化、简化Web发布并增强Web体验。
* Adobe动态标签管理为营销人员提供了直观的工具，可快速、轻松地管理数量不限的Adobe和第三方标签。
* AdobeSearch&amp;Promote使营销人员能够控制和优化其网站上的搜索结果。
* Adobe Campaign允许您直接在Adobe Experience Manager管理电子邮件投放内容。

此外，还可以[将AEM与Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md)和[第三方服务](/help/sites-administering/third-party-services.md)集成。

## 与 Adobe Analytics 集成 {#integrating-with-adobe-analytics}

[Adobe](https://www.omniture.com/en/products/analytics/sitecatalyst) 分析是行业领先的解决方案，它为数字营销人员提供一个位置来测量、分析和优化来自跨多个营销渠道的所有在线计划的集成数据。它为营销人员提供有关数字战略和营销计划的可操作、实时的Web分析智能。 Adobe Analytics公司帮助营销人员快速确定通过网站获得最高利润的途径、细分流量以发现高价值Web访客、确定访客从网站导航到哪里，并确定在线营销活动的关键成功指标。

您可以使用Adobe Analytics分析站点数据。

与Adobe Analytics集成允许您执行以下操作：

* 启用Analytics用户跟踪。
* 将您的运行模式（例如，创作、发布）映射到不同的报表包。
* 将Client Context变量作为转换变量或流量属性提交。
* 使用预定义的变量映射。
* 一次配置完整的站点部分。
* 跟踪自定义事件。

有关将AEM与Analytics集成的信息，请参阅[与Adobe Analytics集成](/help/sites-administering/adobeanalytics.md)。

您还可以使用[选择加入向导](/help/sites-administering/opt-in.md)轻松执行集成。

## 与 Adobe Target 集成 {#integrating-with-adobe-target}

[Adobe](https://www.omniture.com/en/products/conversion/test-and-target) 营销人员用来设计和执行在线测试、创建实时受众细分（基于行为）并自动定位内容和在线体验。

如今的在线消费者需求不断变化，期望从他们可以选择的各种网站和内容来源获得相关、甚至个性化的内容。 要吸引在线受众，在线营销人员必须快速确定哪些优惠和内容对其受众具有相关性和吸引力，这一点至关重要。 借助这些知识，营销人员需要能够不断改进其网站并将适当的内容目标给不同的受众。

[与AdobeTargetxplains](/help/sites-administering/target.md) 集成，如何将您的站点与目标集成。

您还可以使用[选择加入向导](/help/sites-administering/opt-in.md)轻松执行集成。

## 选择使用分析和目标{#opting-in-to-analytics-and-target}

AEM提供了与Adobe Analytics和Adobe Target集成的简单选择程序。 以管理员身份登录并访问项目控制台时，将显示一个选择加入向导。

![chlimage_1-107](assets/chlimage_1-107a.png)

选择与Analytics和／或目标集成，以启用其页面跟踪和分析功能以及个性化功能。 当您需选择加入要提供用户帐户信息并指定要跟踪的页面时。

有关详细信息，请参阅[选择加入Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 与Scene7集成{#integrating-with-scene}

[Adobe Scene7](https://www.adobe.com/products/scene7.html) 是用于发布、管理、增强和交付动态营销资产以及丰富的可视销售到Web、移动、电子邮件、社交媒体、连接Internet的显示屏和印刷品的托管解决方案。

在AEM中，您可以直接将数字资产从AEM发布到Scene7，也可以将数字资产从Scene7发布到AEM。

此外，您还可以通过各种查看器视图发布在Scene7的AEM资产：

* 基本缩放
* DHTML 弹出缩放
* Flash 弹出缩放
* 视频
* Flash 模板
* 图像模板

有关AEM如何与Scene7集成的详细信息，请参见[与Scene7文档集成](/help/sites-administering/scene7.md)。

## 与Adobe动态标签管理集成{#integrating-with-adobe-dynamic-tag-management}

[Adobe动态标](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) 签管理为营销人员提供了直观的工具，可快速、轻松地管理数量不限的Adobe和第三方标签。您将拥有更多控制和灵活性，几乎可以在线优化任何内容，同时减少对IT资源的依赖。

[将Adobe动态标](/help/sites-administering/dtm.md) 签管理与AEM集成，以便您能够使用动态标签管理Web属性跟踪AEM站点。

## 与Adobe Audience Manager集成{#integrating-with-adobe-audience-manager}

Audience Manager集成在AEM 6.3中已被删除。

## 与Search&amp;Promote{#integrating-with-search-promote}集成

[AdobeSearch&amp;](https://www.omniture.com/en/products/conversion/search-and-promote) Promote使营销人员能够优化访客在网站和移动站点上浏览、查找、比较和选择相关产品和内容的方式。企业可以根据业务目标和访客意图轻松宣传优先项目，并通过基于KPI的触发器或指标实现销售和促销活动自动化。

AdobeSearch&amp;Promote是一个可靠、可扩展的托管站点搜索应用程序，可扩展至数百万个页面或产品，适用于从零售到新闻网站等访问量很大的在线业务。 它优惠了前所未有的营销人员控制和基于指标的相关度。

有关集成AEM和Search&amp;Promote的信息，请参阅[与AdobeSearch&amp;Promote集成](/help/sites-administering/search-and-promote.md)。

## 与Adobe Campaign{#integrating-with-adobe-campaign}集成

[Adobe](https://www.adobe.com/solutions/campaign-management.html) 营销活动可让您直接在Adobe Experience Manager管理电子邮件投放内容。

有关AEM如何与Adobe Campaign集成的信息，请参阅[与Adobe Campaign集成](/help/sites-administering/campaignstandard.md)。

## 与Livefyre{#integrating-with-livefyre}集成

了解AEM和Livefyre:

* [Livefyre入门](https://answers.livefyre.com/developers/getting-started)

* [Livefyre 和 AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

