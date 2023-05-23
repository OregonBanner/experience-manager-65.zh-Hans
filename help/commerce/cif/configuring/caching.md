---
title: 快取與效能
description: 瞭解可啟用GraphQL和內容快取的各種設定，以最佳化商務實作的效能。
exl-id: ecce64bf-5960-4ddb-b6e3-dad401038c11
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 2%

---

# 快取與效能 {#caching}

## 元件和GraphQL回應快取 {#graphql}

AEM CIF核心元件已內建對快取個別元件的GraphQL回應的支援。 此功能可用來大幅減少GraphQL後端呼叫的數量。 尤其是對於重複查詢而言，例如擷取導覽元件的類別樹狀結構，或擷取產品搜尋和類別頁面上顯示的所有可用彙總/多面向值，可獲得有效的快取。

對於AEM CIF核心元件，快取是根據元件來設定，因此可以控制是否對每個元件快取GraphQL請求/回應（以及快取多長時間）。 您也可以使用GraphQL使用者端定義OSGi服務的快取行為。

### 配置

為指定元件設定後，快取會依照每個快取設定專案的定義，開始儲存GraphQL查詢和回應。 快取的大小和每個專案的快取期間會根據專案來定義，例如根據目錄資料變更的頻率、元件一律顯示最新可能資料的重要程度等等。 請注意，沒有任何快取失效，因此在設定快取期間時請小心。

為元件設定快取時，快取名稱必須是 **proxy** 您在專案中定義的元件。

在使用者端傳送GraphQL請求之前，會檢查是否要 **確切** 已快取相同的GraphQL請求，並且可能會傳回快取的回應。 為了符合，GraphQL請求必須完全符合，即查詢、操作名稱（如果有）、變數（如果有）都必須等於快取請求，而且可能設定的所有自訂HTTP標頭也必須相同。 例如Adobe Commerce `Store` 標頭必須相符。

### 示例

我們建議您為搜尋服務設定一些快取，以便擷取產品搜尋和類別頁面上顯示的所有可用彙總/面向值。 這些值通常只有在新屬性（例如，新增至產品時）才會變更，因此，如果產品屬性集不經常變更，則此快取專案的持續時間可能會「很大」。 雖然這是專案專用的，我們建議在專案開發階段使用幾分鐘的值，並在穩定生產系統上使用幾小時。

這通常會使用下列快取專案進行設定：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

另一個建議使用GraphQl快取功能的範例案例是導覽元件，因為它會在所有頁面上傳送相同的GraphQL查詢。 在這種情況下，快取專案通常會設為：

```
venia/components/structure/navigation:true:10:600
```

考慮 [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) 已使用。 請注意元件Proxy名稱的使用 `venia/components/structure/navigation`、和 **not** CIF導覽元件的名稱(`core/cif/components/structure/navigation/v1/navigation`)。

其他元件的快取應根據專案來定義，通常與在Dispatcher層級設定的快取協調。 請記住，這些快取沒有任何作用中的失效機制，因此應謹慎設定快取持續時間。 沒有任何「一刀切」的值會符合所有可能的專案和使用案例。 請務必在專案層級定義最符合專案需求的快取策略。

## Dispatcher快取 {#dispatcher}

在中快取AEM頁面或片段 [AEM傳送器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html) 是任何AEM專案的最佳實務。 通常，它仰賴失效技術，以確保在AEM中變更的任何內容在Dispatcher中正確更新。 這是AEM Dispatcher快取策略的核心功能。

除了純粹的AEM受管內容CIF之外，頁面通常可以顯示透過GraphQL從Adobe Commerce動態擷取的商務資料。 雖然頁面結構本身可能不會變更，但商務內容可能會變更，例如，如果Adobe Commerce中的某些產品資料（例如名稱或價格）變更。

為了確保CIF頁面可以在AEM Dispatcher中的有限時間內快取，我們建議使用 [基於時間的快取失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl) （也稱為TTL型快取）在AEM Dispatcher中快取CIF頁面時。 此功能可在AEM中設定，使用額外的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) 封裝。

透過TTL型快取，開發人員通常會為選取的AEM頁面定義一或多個快取持續時間。 這可確保AEM Dispatcher中僅快取CIF頁面，直到設定的持續時間為止，並且內容將經常更新。

>[!NOTE]
>
>雖然AEM Dispatcher可能會快取伺服器端資料，但某些CIF元件(例如 `product`， `productlist`、和 `searchresults` 載入頁面時，元件通常會一律在使用者端瀏覽器請求中重新擷取產品價格。 這可確保在頁面載入時一律會擷取重要的動態內容。

## 其他资源

- [Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL快取設定](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM傳送器](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
