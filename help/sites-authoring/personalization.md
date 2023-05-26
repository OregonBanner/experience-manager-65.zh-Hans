---
title: 个性化和内容定位
seo-title: Personalization and Content Targeting
description: 了解 AEM 如何创建个性化内容
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 35%

---

# 个性化和内容定位 {#personalization}

## 个性化和内容定位 {#personalization-and-content-targeting}

AEM提供了一个工具框架，用于创作目标内容和呈现个性化体验。

## 定位模式 {#targeting-mode}

可使用 AEM 的定位模式[创作目标内容](/help/sites-authoring/content-targeting-touch.md)。定位模式和 Target 组件提供了一些工具，用于为您的营销活动体验创建内容。

## 活动 {#activities}

活动定义并组织您的营销工作。 活动由您定位的受众以及应用定位的时段组成。

例如，We.Retail产品目录包含关注季节性产品的Teaser。 夏季体育活动定义Teaser在夏季月份中定位的营销区段。

活动还标识了 [定位引擎](/help/sites-authoring/personalization.md#targeting-engine) 您的页面使用的区段。

使用 [活动控制台](/help/sites-authoring/activitylib.md) 创建和管理品牌的活动。 您还可以在[创作目标内容](/help/sites-authoring/content-targeting-touch.md)时创建活动。

## 体验 {#experiences}

对于每个活动，您可以定义一个或多个体验来识别要定位的受众。AEM 使您能够控制包含每个体验的内容。

受众基于在AEM或Adobe Target中创建的营销区段。 当访客打开网页时，页面逻辑会确定访客所属的受众，并显示您为该受众创建的内容。

例如，某项活动定义了针对两类不同受众的体验：30 岁以上的女性和 30 岁以下的女性。We.Retail网站的女性页面针对每种体验显示不同的产品。

您可以为活动定义体验。 您可以使用 [活动控制台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) 或 [定位模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) 以向活动添加体验。

## 选件 {#offers}

选件是出现在页面上某个位置以供体验使用的内容。 为不同的体验使用不同的选件，以最大限度地提高内容对受众的有效性。

例如，We.Retail示例网站的女性页面可以使用选件作为显示在页面顶部的Teaser图像。 对30岁以上的女性和30岁以下的女性，则使用不同的优惠作为Teaser。

使用 [优惠控制台](/help/sites-authoring/offerlib.md) 以创建可在多个体验中使用的选件。 在以下情况下创建一次性选件或从选件库添加选件： [创作目标内容](/help/sites-authoring/content-targeting-touch.md).

## 定位引擎 {#targeting-engine}

定位引擎是驱动目标内容逻辑的机制。 [活动](/help/sites-authoring/activitylib.md)会配置为使用以下两个可用的定位引擎之一：AEM 和 Adobe Target。

### AEM {#aem}

AEM提供了一个内置定位引擎，用于处理页面请求并确定要显示的内容。 使用 AEM 定位引擎时，您仅可使用在 AEM 中创建的区段来定义体验受众。

### Adobe Target {#adobe-target}

Adobe Target 定位引擎允许从 Adobe Target 中跟踪的页面访问收集信息。

* 使用此定位引擎时，您可以使用从Adobe Target导入的区段来定义体验的受众。
* 使用Adobe Target引擎的活动包括 [已同步到Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

[与 Adobe Target 集成后](/help/sites-administering/opt-in.md)，您便可以使用此引擎。
