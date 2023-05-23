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

AEM提供工具架構，用於製作目標內容和呈現個人化體驗。

## 定位模式 {#targeting-mode}

可使用 AEM 的定位模式[创作目标内容](/help/sites-authoring/content-targeting-touch.md)。定位模式和 Target 组件提供了一些工具，用于为您的营销活动体验创建内容。

## 活动 {#activities}

活動可定義及組織您的行銷工作。 活動包含您要鎖定的對象，以及套用鎖定的時段。

例如，We.Retail產品目錄包含著重季節性產品的Teaser。 夏季運動活動會定義Teaser在夏季月份鎖定的行銷區段。

活動也會識別 [目標定位引擎](/help/sites-authoring/personalization.md#targeting-engine) 您的頁面所使用的屬性。

使用 [活動主控台](/help/sites-authoring/activitylib.md) 以建立和管理您品牌的活動。 您还可以在[创作目标内容](/help/sites-authoring/content-targeting-touch.md)时创建活动。

## 体验 {#experiences}

对于每个活动，您可以定义一个或多个体验来识别要定位的受众。AEM 使您能够控制包含每个体验的内容。

對象是根據在AEM或Adobe Target中建立的行銷區段。 當訪客開啟網頁時，頁面邏輯會決定他們所屬的受眾，並顯示您為該受眾建立的內容。

例如，某项活动定义了针对两类不同受众的体验：30 岁以上的女性和 30 岁以下的女性。We.Retail網站的「女性」頁面針對每個體驗顯示不同的產品。

您可以定義活動的體驗。 您可以使用 [活動主控台](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) 或 [目標定位模式](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) 將體驗新增至活動。

## 选件 {#offers}

選件是出現在體驗頁面某個位置的內容。 針對不同的體驗使用不同的選件，為您的對象最大化內容的成效。

例如，We.Retail範例網站的女性頁面可以使用選件作為顯示在頁面頂端的Teaser影像。 不同的優惠方案會用作30歲以上女性體驗和30歲以下女性體驗的Teaser。

使用 [選件主控台](/help/sites-authoring/offerlib.md) 以建立可在多個體驗中使用的選件。 出現下列情況時，請建立單一使用選件或從選件資料庫新增選件： [製作目標內容](/help/sites-authoring/content-targeting-touch.md).

## 定位引擎 {#targeting-engine}

目標定位引擎是驅動目標內容邏輯的機制。 [活动](/help/sites-authoring/activitylib.md)会配置为使用以下两个可用的定位引擎之一：AEM 和 Adobe Target。

### AEM {#aem}

AEM提供內建的鎖定目標引擎，可處理頁面請求並決定要顯示的內容。 使用 AEM 定位引擎时，您仅可使用在 AEM 中创建的区段来定义体验受众。

### Adobe Target {#adobe-target}

Adobe Target 定位引擎允许从 Adobe Target 中跟踪的页面访问收集信息。

* 使用此鎖定目標引擎時，您可以使用從Adobe Target匯入的區段來定義體驗的對象。
* 使用Adobe Target引擎的活動包括 [已同步至Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

[与 Adobe Target 集成后](/help/sites-administering/opt-in.md)，您便可以使用此引擎。
