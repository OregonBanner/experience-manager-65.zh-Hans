---
title: 了解分段
seo-title: 了解分段
description: 分段是创建营销活动时的主要考虑事项。
seo-description: 分段是创建营销活动时的主要考虑事项。
uuid: 900da068-5dda-4b6b-8be3-4b7ad614126d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 36c87684-e62a-4983-b123-87f56dbf7bc5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 71%

---


# 了解分段{#understanding-segmentation}

分段是创建营销活动时的主要考虑事项。大多数情况下，您需要在开始营销活动之前先定义区段。

站点访客在访问站点时的兴趣和目标各不相同。了解这些目标并满足预期是在线营销活动的一个重要成功因素。

分段可通过分析访客并描述访问的特征来帮助实现此目标：

* 在网站上的活动
* 配置文件
* 在其他网站上的活动

内容可以特别针对于访客的需求和兴趣，具体取决于他们匹配的区段。

## 使用分段  {#using-segmentation}

区段在[配置分段](/help/sites-administering/campaign-segmentation.md)过程中进行定义。它们用于控制特定目标受众看到的实际内容。

## 分段术语  {#segmentation-terminology}

在讨论分段时，会用到以下术语：

**访** 客访客是访问网站的人。访客的访问通常从引用页面开始，然后移动到您自己网站上的一个或多个页面视图。可以根据访客访问的详细信息创建行为配置文件。

**用** 户用户是在网站上注册以接收帐户用户档案的访客。要生成配置文件，访客需要提供其他标识，如电子邮件地址和性别等等。还可以收集其他信息，包括社区活动和购买模式等等。根据配置文件中提供的信息，可以创建人口统计配置文件。

**特** 征A特征是访客的特征或属性，可用于确定特定区段中的成员资格。

**SegmentA** 区段是共享某些特征的访客集合。区段应该与众不同，与其他区段之间具有尽可能少的重叠。

**行为** 特征行为特征是指与访客在网站上的行为相关的特征。这些 Cookie 包括：

* 在网站中的兴趣；包括访问的页面和购买的产品。
* 在引用网站中的兴趣；包括使用的搜索词或点击的广告。
* 在其他站点中的兴趣；使用 Spyjax 之类的工具确定。
* 访客忠诚度；访问的持续时间和访问频率。

**人口** 特征这些是所选人口特征，包括：

* 年龄
* 收入
* 家庭人数
* 婚姻状况
* 性别
* 位置

**衍生的特征**&#x200B;在未注册的情况下，有些人口统计特征很难确定，但可以通过组合行为和人口统计特征来推断。

例如，通过将引用 URL（作为行为特征）与人口统计数据（通过 [Google Ad Planner](https://www.google.com/adplanner/) 之类的工具获取）相结合，站点所有者可以推断出访客的人口统计特征。

**子** 段A段可细分为多个子段。这可以通过定义其他特征来完成。

**Teaser页** 面Teaser页面定向到特定受众。它包含可在 Teaser 段落中使用的可重用内容。

**营销** 活动活动是Teaser页面和电子邮件营销页面（如新闻稿或邀请）的集合。通常，营销活动只运行一段有限的时间，随后会被其他营销活动取代。

**Teaser** Paragraph这是从另一个依赖于选择策略的页面中提取内容的段落。此选择战略可以将区段和营销活动考虑在内。

**列** 表从注册用户的区段中提取列表。例如，用于控制 Teaser 段落内容的位置。

>[!NOTE]
>
>有关AEM中区段的更多信息，请参见[分段](/help/sites-administering/campaign-segmentation.md)。

