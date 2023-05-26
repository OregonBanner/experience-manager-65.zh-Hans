---
title: 如何构建目标内容的多站点管理
seo-title: How Multisite Management for Targeted Content is Structured
description: 下图显示了如何构建目标内容的多站点支持
seo-description: A diagram shows how multisite support for targeted content is structured
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 36%

---

# 如何构建目标内容的多站点管理{#how-multisite-management-for-targeted-content-is-structured}

下图显示了如何构建对目标内容的多站点支持。

**/content/campaigns/&lt;brand>** 下方显示了区域，默认情况下，每个品牌都有一个自动创建的主区域。每个区域都包含自身的一组活动、体验和选件。

![chlimage_1-268](assets/chlimage_1-268.png)

要查找目标内容，页面或网站可以映射到某个区域。 如果未配置区域，则AEM将回退到此特定品牌的主控区域。

下图是该逻辑如何为三个站点（名为 site1、site2 和 site3）工作的示例。

![chlimage_1-269](assets/chlimage_1-269.png)

* 站点1基于区域映射查找myarea1 for brand1和otherarea2 for brand2。
* 站点2查找myarea1 for brand1和主控区域for brand2 ，因为只定义了brand1的区域映射。
* 站点3查找brand1和brand2的主控区域，因为根本未为此站点定义其他区域映射。
