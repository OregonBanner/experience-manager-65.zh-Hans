---
title: Communities元件基本知識
seo-title: Communities Components Basics
description: 在編輯模式下將Communities功能新增至AEM網站並設定元件
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# Communities元件基本知識 {#communities-components-basics}

## 概述 {#overview}

本檔案的製作區段會說明如何在作者編輯模式下將Communities功能新增至AEM網站，並說明元件設定。

您可以使用AEM例項和互動式來探索元件 [社群元件指南](components-guide.md).

## 存取Communities元件 {#accessing-communities-components}

編寫頁面內容時，如果基礎範本允許對頁面設計進行變更，則可以啟用元件瀏覽器中尚未提供的元件，作為網站設計的一部分。

列出可用的Communities元件 [此處](author-communities.md#available-communities-components).

>[!NOTE]
>
>如需一般撰寫資訊，請檢視 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).
>
>若不熟悉AEM，請檢視以下說明檔案： [基本處理](../../help/sites-authoring/basic-handling.md).

### 進入設計模式 {#entering-design-mode}

若為 **Communities** 元件瀏覽器(sidekick)中找不到元件，必須輸入 `Design Mode` 以新增其他Communities元件。 [必要的使用者端程式庫](#required-clientlibs) (clientlibs)可能也需要新增。

如需詳細資訊，請參閱 [在設計模式中設定元件](../../help/sites-authoring/default-components-designmode.md).

以下是選取一些Communities元件並在元件瀏覽器中檢視這些元件的影像：

![component-design](assets/component-design.png)

元件瀏覽器現在提供選取的元件：

![component-design1](assets/component-design1.png)

## 必要的Clientlibs {#required-clientlibs}

[使用者端程式庫](../../help/sites-developing/clientlibs.md) 元件的正常運作(JavaScript)和樣式(CSS)需要(clientlibs)。

將Communities元件新增至頁面時，如果結果為錯誤或意外外觀，首先要嘗試為Communities元件新增必要的clientlibs。 如需詳細資訊，請參閱 [Communities元件的Clientlibs](clientlibs.md).

### 範例：最初放置的檢閱沒有使用者端資料庫…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...以及使用使用者端資料庫 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 标记 {#tagging}

許多Communities功能可設定為允許成員標籤在發佈環境中輸入（發佈）的內容。

如果允許標籤，則可設定社群網站的設定，以限制向發佈環境中的成員顯示的名稱空間。 請參閱 [社群網站主控台](sites-console.md#tagging).

允許標籤的功能： [部落格](blog-feature.md)， [行事曆](calendar.md)， [檔案庫](file-library.md)， [論壇](forum.md)

使用標籤的功能： [搜尋](search.md)， [社交標籤雲](tagcloud.md)

如需製作資訊：

* [使用标记](../../help/sites-authoring/tags.md)

如需管理資訊：

* 建立標籤名稱空間（分類法）： [管理標籤](../../help/sites-administering/tags.md)
* 社群網站設定：請參閱 [標籤](sites-console.md#tagging)
* [標籤使用者產生的內容](../../help/sites-authoring/tags.md)

如需開發人員資訊：

* [AEM 标记框架](../../help/sites-developing/framework.md)
* [標籤Essentials](tag.md)
