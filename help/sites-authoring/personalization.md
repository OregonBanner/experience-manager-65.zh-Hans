---
title: 个性化和内容定位
seo-title: 个性化和内容定位
description: 了解AEM如何创建个性化内容
seo-description: 了解AEM如何创建个性化内容
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 80%

---


# 个性化和内容定位 {#personalization}

## 个性化和内容定位 {#personalization-and-content-targeting}

AEM 为创作目标内容和呈现个性化体验提供了一个工具框架。

## 定位模式  {#targeting-mode}

[可使用 AEM 的定位模式创作目标内容。](/help/sites-authoring/content-targeting-touch.md)定位模式和 Target 组件提供了一些工具，用于为您的营销活动体验创建内容。

## 活动 {#activities}

活动定义和组织您的营销工作。活动包括您定位的受众以及应用定位的时间段。

例如，We.Retail产品目录包含关注季节性产品的Teaser。 夏季体育活动定义 Teaser 在夏季月份中定位的营销区段。

活动还标识您的页面使用的[定位引擎](/help/sites-authoring/personalization.md#targeting-engine)。

使用[“活动”控制台](/help/sites-authoring/activitylib.md)可为您的品牌创建和管理活动。您还可以在[创作目标内容](/help/sites-authoring/content-targeting-touch.md)时创建活动。

## 体验 {#experiences}

对于每个活动，您可以定义一个或多个体验来识别要定位的受众。AEM使您能够控制包含每种体验的内容。

受众基于在 AEM 或 Adobe Target 中创建的营销区段。当访客打开网页时，页面逻辑会确定他们所属的受众，并显示您为该受众创建的内容。

例如，某项活动定义了针对两类不同受众的体验：30 岁以上的女性和 30 岁以下的女性。We.Retail网站的“女性”页面显示每种体验的不同产品。

您可以为活动定义体验。您可以使用[“活动”控制台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console)或[定位模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode)将体验添加到活动中。

## 选件  {#offers}

选件是指显示在页面上的某个位置以提供体验的内容。可针对不同的体验使用不同的选件，以最大限度地提高受众内容的有效性。

例如，We.Retail示例网站的“妇女”页面可以使用优惠作为显示在页面顶部的Teaser图像。 对于 30 岁以上的女性体验和 30 岁以下的女性体验，将使用不同的选件作为 Teaser。

使用[“选件”控制台](/help/sites-authoring/offerlib.md)，可创建您可以在多个体验中使用的选件。[创作目标内容](/help/sites-authoring/content-targeting-touch.md)时，可创建单次使用选件或添加选件库中的选件。

## 定位引擎  {#targeting-engine}

定位引擎是驱动目标内容逻辑的机制。[活动](/help/sites-authoring/activitylib.md)会配置为使用以下两个可用的定位引擎之一：AEM 和 Adobe Target。

### AEM {#aem}

AEM 提供了一个内置定位引擎，用于处理页面请求并确定要显示的内容。使用 AEM 定位引擎时，您仅可使用在 AEM 中创建的区段来定义体验受众。

### Adobe Target {#adobe-target}

Adobe Target 定位引擎允许从 Adobe Target 中跟踪的页面访问收集信息。

* 使用此定位引擎时，您可以使用从 Adobe Target 导入的区段来定义体验受众。
* 使用 Adobe Target 引擎的活动会[同步到 Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target)。

将[与Adobe Target](/help/sites-administering/opt-in.md)集成后，可使用此引擎。
