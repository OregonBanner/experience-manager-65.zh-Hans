---
title: 與Adobe Experience Cloud整合
description: 瞭解如何將Adobe Experience Manager與Adobe Experience Cloud整合。
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

# 與Adobe Experience Cloud整合{#integrating-with-the-adobe-marketing-cloud}

此 [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html)包括功能強大的網站分析和網站最佳化產品，可提供可操作的即時資料和深入分析，以推動成功的線上方案。 它提供整合且開放的平台，用於線上業務最佳化。 Cloud包含整合的應用程式，可收集並釋放客戶洞察的力量，以最佳化客戶贏取、轉換和保留工作，以及內容的建立和分發。

透過Adobe Experience Manager (AEM)，您可以順暢地整合下列Adobe Experience Cloud產品：

* Adobe Analytics為行銷人員提供線上策略和行銷方案的可行、即時資訊。
* Adobe Target可讓行銷人員持續提供與客戶更相關的線上內容，進而提高轉換率。
* Adobe Dynamic Media Classic可自動化媒體管理、簡化Web發佈，以及增強Web體驗，所有這些都可在託管環境中完成。
* Adobe Dynamic Tag Management為行銷人員提供了直覺式工具，可快速輕鬆地管理無限數量的Adobe和協力廠商標籤。
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* Adobe Campaign可讓您直接在Adobe Experience Manager中管理電子郵件傳遞內容。

此外，您可以 [將AEM與Creative Cloud整合](/help/assets/aem-cc-integration-best-practices.md) 和 [協力廠商服務](/help/sites-administering/third-party-services.md).

## 与 Adobe Analytics 集成 {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) 是領先業界的解決方案，為數位行銷人員提供一個可以測量、分析和最佳化多個行銷管道中所有線上方案的整合資料的位置。 它為行銷人員提供有關數位策略和行銷方案的可行、即時Web分析情報。 Adobe Analytics可協助行銷人員快速找出網站中最有利可圖的路徑、劃分流量以找出高價值的網頁訪客、判斷訪客從網站瀏覽至何處，以及找出線上行銷活動的關鍵成功量度。

您可以使用Adobe Analytics來分析來自您網站的資料。

與Adobe Analytics整合可讓您執行下列作業：

* 啟用Analytics使用者追蹤。
* 將您的執行模式（例如作者、發佈）對應至不同的報表套裝。
* 將Client Context變數提交為轉換變數或流量屬性。
* 使用預先定義的變數對應。
* 一次設定完整的網站區域。
* 追蹤自訂定義的事件。

如需整合AEM與Analytics的相關資訊，請參閱 [與Adobe Analytics整合](/help/sites-administering/adobeanalytics.md).

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) 以輕鬆執行整合。

## 与 Adobe Target 集成 {#integrating-with-adobe-target}

[营销人员使用 Adobe Target 来设计和执行在线测试、创建动态受众区段（基于行为）以及自动定位内容和在线体验。](https://business.adobe.com/products/target/adobe-target.html)

現今的線上消費者不斷改變需求，期望從各種網站和內容來源取得相關、甚至個人化的內容。 若要吸引線上受眾，線上行銷人員必須快速找出哪些優惠方案和內容與其受眾相關且吸引人。 有了這些知識，行銷人員需要能夠持續改進其網站，並將適當的內容鎖定在不同對象。

[與Adobe Target整合](/help/sites-administering/target.md) 說明如何將您的網站與Target整合。

您也可以使用 [選擇加入精靈](/help/sites-administering/opt-in.md) 以輕鬆執行整合。

## 選擇加入Analytics和Target {#opting-in-to-analytics-and-target}

AEM提供簡單的選擇加入程式，以便與Adobe Analytics和Adobe Target整合。 當您以管理員身分登入並造訪「專案」主控台時，畫面會顯示選擇加入精靈。

![chlimage_1-107](assets/chlimage_1-107a.png)

選擇與Analytics和/或Target整合，以啟用其頁面追蹤和分析功能及個人化功能。 當您選擇加入時，請提供您的使用者帳戶資訊，並指定追蹤的頁面。

如需詳細資訊，請參閱 [選擇使用Adobe Analytics和Adobe Target。](/help/sites-administering/opt-in.md)

## 與Adobe Dynamic Media Classic整合 {#integrating-with-scene}

Adobe Dynamic Media Classic是託管解決方案，可發佈、管理、增強及提供動態行銷資產，以及針對網路、行動裝置、電子郵件、社群媒體、網際網路連線顯示和列印的豐富視覺銷售。

在Adobe Experience Manager中，您可以直接從Adobe Experience Manager將數位資產發佈到Dynamic Media Classic，也可以從Dynamic Media Classic將數位資產發佈到Adobe Experience Manager。

此外，您也可以使用各種檢視器（例如「基本縮放」和「視訊」）來檢視Dynamic Media Classic中發佈的Adobe Experience Manager資產。

如需Adobe Experience Manager如何與Dynamic Media Classic整合的詳細資訊，請參閱 [與Dynamic Media Classic整合](/help/sites-administering/scene7.md) 說明檔案。

## 與Adobe Dynamic Tag Management整合 {#integrating-with-adobe-dynamic-tag-management}

[AdobeDynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) 提供直覺式工具，讓行銷人員快速輕鬆地管理不限數量的Adobe和協力廠商標籤。 您擁有更多控制能力和彈性，幾乎可將任何線上作業最佳化，同時減少對IT資源的依賴。

[整合AdobeDynamic Tag Management](/help/sites-administering/dtm.md) AEM，讓您能夠使用Dynamic Tag Management Web屬性來追蹤AEM網站。

## 與Adobe Audience Manager整合 {#integrating-with-adobe-audience-manager}

AEM 6.3中已移除Audience Manager整合。

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## 与 Adobe Campaign 集成 {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) 可讓您直接在Adobe Experience Manager中管理電子郵件傳遞內容。

如需AEM如何與Adobe Campaign整合的詳細資訊，請參閱 [與Adobe Campaign整合](/help/sites-administering/campaignstandard.md).