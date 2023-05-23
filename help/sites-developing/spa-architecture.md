---
title: 为 AEM 开发 SPA
seo-title: Developing SPAs for AEM
description: 本文介紹當請前端開發人員為AEM開發SPA時應考慮的重要問題，並概述AEM關於SPA的架構，以在在AEM上部署開發的SPA時牢記這一點。
seo-description: This article presents important questions to consider when engaging a front-end developer to develop a SPA for AEM as well as gives an overview of the architecture of AEM with respect to SPAs to keep in mind when deploying a developed SPA on AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 8%

---

# 为 AEM 开发 SPA{#developing-spas-for-aem}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用 SPA 框架构建站点，而作者则希望能够在 AEM 中顺畅地为使用此类框架构建的站点编辑内容。

本文介紹當讓前端開發人員開發SPA for AEM時需要考慮的重要問題，並提供AEM架構概述以在AEM上部署SPA。

>[!NOTE]
>
>SPA編輯器是建議解決方案，適用於需要SPA架構使用者端轉譯的專案(例如React或Angular)。

## AEM的SPA開發原則 {#spa-development-principles-for-aem}

在 AEM 上开发单页应用程序时，假定前端开发人员在创建 SPA 时遵循标准最佳实践。如果您身為前端開發人員，遵循這些一般最佳實務以及少數AEM特定原則，您的SPA將能透過 [AEM及其內容製作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[可攜性](/help/sites-developing/spa-architecture.md#portability) -** 與任何元件一樣，元件應儘可能建置為可攜式。 应使用可移植且可重用的组件构建 SPA。
* **[AEM 推动站点结构](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** – 前端开发人员创建组件并拥有其内部结构，但依赖 AEM 来定义站点的内容结构。
* **[动态呈现](/help/sites-developing/spa-architecture.md#dynamic-rendering)** – 所有呈现都应是动态的。
* **[動態路由](#dynamic-routing) -** SPA負責路由，AEM會監聽路由並根據路由進行擷取。 任何路由也应是动态的。

如果您在開發SPA時牢記這些原則，在啟用所有支援的AEM編寫功能時，將會儘可能靈活且經得起未來考驗。

如果您不需要支援AEM編寫功能，您可能需要考慮其他功能 [SPA設計模型](/help/sites-developing/spa-architecture.md#spa-design-models).

### 可攜性 {#portability}

如同開發任何元件一樣，元件的設計應儘可能提高可攜性。 應避免任何影響元件可移植性或可重複使用的模式，以確保未來相容性、彈性和可維護性。

產生的SPA應使用可攜性強且可重複使用的元件建置。

### AEM磁碟機網站結構 {#aem-drives-site-structure}

前端開發人員必須自行負責建立用於建置應用程式的SPA元件資料庫。 前端開發人員可完全控制元件的內部結構。 [不過AEM始終擁有網站結構。](/help/sites-developing/spa-overview.md)

這表示前端開發人員可以在元件的進入點之前或之後新增客戶內容，且也可以在元件內進行第三方呼叫。 不過，前端開發人員無法完全控制元件的巢狀內嵌方式。

### 動態演算 {#dynamic-rendering}

SPA應該僅依賴內容的動態呈現。 這是AEM擷取並轉譯內容結構之所有子項的預設預期。

任何指向特定內容的明確呈現都會視為靜態呈現，雖然支援此功能，但不會與AEM內容製作功能相容。 這也違反以下原則： [可攜性](/help/sites-developing/spa-architecture.md#portability).

### 動態路由 {#dynamic-routing}

如同演算一樣，所有路由也應該是動態的。 在AEM中， [SPA應一律擁有路由](/help/sites-developing/spa-routing.md) 和AEM會監聽它，並根據它擷取內容。

任何靜態路由都適用於 [可攜性原則](/help/sites-developing/spa-architecture.md#portability) 和會因為與AEM的內容製作功能不相容而限製作者。 例如，使用靜態路由，如果內容作者想要變更路由或變更頁面，他或她必須要求前端開發人員執行此操作。

## AEM 项目原型 {#aem-project-archetype}

任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## SPA設計模型 {#spa-design-models}

如果 [在AEM中開發SPA的原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) 之後，您的SPA將可使用所有支援的AEM內容製作功能。

不過，在某些情況下，這並非完全必要。 下表概述各種設計模型、其優點和缺點。

<table>
 <tbody>
  <tr>
   <th><strong>設計模型<br /> </strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作Headless CMS，而不使用 <a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDK架構。</a></td>
   <td>前端開發人員可完全控制應用程式。</td>
   <td><p>內容作者無法運用AEM內容製作體驗。</p> <p>如果程式碼包含靜態參照或路由，則無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>前端開發人員使用SPA Editor SDK架構，但只對內容作者開啟某些區域。</td>
   <td>開發人員只會在應用程式的受限制區域中啟用撰寫，就能保持對應用程式的控制。</td>
   <td><p>內容作者受限於有限的AEM內容製作體驗。</p> <p>如果程式碼包含靜態參考或路由，則可能無法移植或重複使用。</p> <p>不允許使用範本編輯器，因此前端開發人員必須透過JCR維護可編輯的範本。</p> </td>
  </tr>
  <tr>
   <td>專案完全運用SPA編輯器SDK，前端元件會開發為程式庫，而應用程式的內容結構會委派給AEM。</td>
   <td><p>應用程式可重複使用且可移植。</p> <p>內容作者可使用AEM內容製作體驗來編輯應用程式。<br /> </p> <p>SPA與範本編輯器相容。</p> </td>
   <td><p>開發人員無法控制應用程式的結構和委派給AEM的內容部分。</p> <p>開發人員仍可保留應用程式的區域，以供不應使用AEM編寫的內容使用。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>雖然AEM支援所有模型，但僅實作第三種（因此遵循建議的） [AEM中的SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))內容作者是否能夠在AEM中與慣用的SPA內容互動及編輯內容。

## 將現有SPA移轉至AEM {#migrating-existing-spas-to-aem}

一般而言，如果您的SPA遵循 [AEM的SPA開發原則](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，則您的SPA將在AEM中運作，並可使用AEM SPA編輯器編輯。

請依照下列步驟，讓現有的SPA準備好與AEM搭配使用。

1. **將您的JS元件模組化。**

   使其能夠以任何順序、位置和大小呈現。
1. **使用我們的SDK提供的容器，將您的元件放在熒幕上。**

   AEM提供頁面和段落系統元件供您使用。
1. **為每個JS元件建立AEM元件。**

   AEM元件會定義對話方塊和JSON輸出。

## 面向前端開發人員的說明 {#instructions-for-front-end-developers}

鼓勵前端開發人員建立AEM適用的SPA的主要工作是就元件及其JSON模型達成共識。

以下概述前端開發人員在開發SPA for AEM時需要遵循的步驟。

1. **同意元件及其JSON模型**

   前端開發人員和後端AEM開發人員需要就哪些元件是必要元件和型號達成一致，以便從SPA元件到後端元件進行一對一比對。

   AEM元件仍然主要用於提供編輯對話方塊和匯出元件模型。

1. **在React元件中，透過以下方式存取模型`this.props.cqModel`**

   在同意元件及JSON模型就緒後，前端開發人員即可自由開發SPA，並可透過以下方式存取JSON模型 `this.props.cqModel`.

1. **實作元件的 `render()` 方法**

   前端開發人員實作 `render()` 方法會被視為適合，且可以使用 `cqModel` 屬性。 這會輸出將插入頁面的DOM和HTML片段。 這是在React中建立應用程式的標準方式。

1. **透過以下方式將元件對應到AEM資源型別`MapTo()`**

   對應會儲存元件類別，並由提供的在內部使用 `Container` 根據指定的資源型別擷取及動態例項化元件的元件。

   這是前端與後端之間的「粘合劑」，因此編輯器可以知道react元件對應到哪些元件。

   此 `Page` 和 `ResponsiveGrid` 是延伸基底類別的良好範例 `Container`.

1. **定義元件的 `EditConfig` 作為引數`MapTo()`**

   只要尚未轉譯或沒有可轉譯的內容，此引數是告訴編輯器元件應如何命名所必需的。

1. **擴充提供的 `Container` 頁面和容器的類別**

   頁面和段落系統應該擴充此類別，好讓委派給內部元件的功能如預期般運作。

1. **實作路由解決方案，該解決方案使用HTML5 `History` API。**

   當 `ModelRouter` 已啟用，呼叫 `pushState` 和 `replaceState` 函式會觸發要求 `PageModelManager` 以擷取模型的遺失片段。

   目前版本的 `ModelRouter` 僅支援使用指向Sling模型進入點的實際資源路徑的URL。 不支援使用虛名URL或別名。

   此 `ModelRouter` 可停用或設定為忽略規則運算式清單。

## 與AEM無關 {#aem-agnostic}

這些程式碼區塊說明您的React和Angular元件如何不需要任何特定於Adobe或AEM的內容。

* JavaScript元件內的所有內容都與AEM無關。
* 但AEM的專屬之處在於，JS元件必須透過MapTo Helper對應至AEM元件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

此 `MapTo` helper是「粘合劑」，可讓後端和前端元件搭配使用：

* 它會告訴JS容器（或JS段落系統）哪個JS元件負責轉譯JSON中存在的每個元件。
* 它會將HTML資料屬性新增至JS元件轉譯的HTML，以便SPA編輯器知道在編輯元件時向作者顯示的對話方塊。

如需關於使用的詳細資訊 `MapTo` 以及建置SPA for AEM的一般資訊，請參閱所選架構的快速入門手冊。

* [AEM中的SPA快速入門 — React](/help/sites-developing/spa-getting-started-react.md)
* [AEM中的SPA快速入門 — Angular](/help/sites-developing/spa-getting-started-angular.md)

## AEM架構與SPA {#aem-architecture-and-spas}

AEM的一般架構，包括開發、製作和發佈環境，在使用SPA時不會變更。 不過，瞭解SPA開發如何適應此架構很有幫助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **构建环境**

   這是SPA應用程式來源和元件來源出庫的位置。

   * NPM clientlib產生器會從SPA專案建立使用者端程式庫。
   * 該程式庫將由Maven取得，並由Maven Build外掛程式與元件部署到AEM作者。

* **AEM Author**

   內容是在AEM作者上建立的，包括編寫SPA。

   在製作環境中使用SPA編輯器編輯SPA時：

   1. SPA要求外部HTML。
   1. CSS已載入。
   1. SPA應用程式的Javascript已載入。
   1. 執行SPA應用程式時，系統會要求JSON，讓應用程式建立頁面的DOM，包括 `cq-data` 屬性。
   1. 此 `cq-data` 屬性可讓編輯器載入其他頁面資訊，以便知道哪些編輯設定可供元件使用。

* **AEM 发布**

   這是發佈編寫的內容和編譯的程式庫(包括SPA應用程式人工因素、clientlibs和元件)以供公眾使用的位置。

* **Dispatcher / CDN**

   Dispatcher是網站訪客的AEM快取階層。

   * 請求的處理方式與它們在AEM作者上的處理方式類似，但不會請求頁面資訊，因為編輯器只需要它。
   * 快取Javascript、CSS、JSON和HTML，最佳化頁面以快速傳送。

>[!NOTE]
>
>在AEM內部，不需要執行Javascript建置機制或執行Javascript本身。 AEM僅代管來自SPA應用程式的編譯成品。

## 后续步骤 {#next-steps}

如需如何在AEM中建構簡單SPA及其運作方式的概觀，請參閱兩者的快速入門手冊 [React](/help/sites-developing/spa-getting-started-react.md) 和 [angular](/help/sites-developing/spa-getting-started-angular.md).

如需建立您自己的SPA的逐步指南，請參閱 [AEM SPA編輯器快速入門 — WKND事件教學課程](https://helpx.adobe.com/cn/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

如需有關動態模型到元件對應的更多詳細資訊，以及它在AEM中SPA的運作方式，請參閱文章 [SPA的動態模型到元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

如果您想在AEM中為React或Angular以外的框架實作SPA，或只是想深入瞭解AEM適用的SPA SDK的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
