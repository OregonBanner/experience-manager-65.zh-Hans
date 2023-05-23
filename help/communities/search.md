---
title: 搜尋功能
seo-title: Search Feature
description: 將搜尋新增及設定至社群網站
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# 搜尋功能 {#search-feature}

搜尋功能可與各種其他功能（例如論壇）搭配使用，以提供搜尋內容的功能。

新增搜尋社群成員輸入的貼文(稱為使用者產生的內容(UGC))的功能時，有兩個元件： [搜尋](#search) 和 [搜尋結果](#search-results).

包含下列專案的頁面 `Search Results` 元件支援搜尋和顯示結果。

包含下列專案的頁面 `Search` 元件會提供位置來啟動搜尋，搜尋結果會顯示在 `Search Results` 頁面。

搜尋功能可搭配任何其他功能使用，以允許網站訪客和成員檢視內容。

## 搜索 {#search-features}

### 將搜尋新增至頁面 {#add-search-to-a-page}

若要新增 `Search` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找 `Communities / Search` 並將其拖曳至頁面上的適當位置。 使用 `Search` 需要「 」的第二個頁面 `Search Results.`

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當需要使用者端程式庫時， `cq.social.hbs.search`，包含，這就是 `Search` 元件隨即出現。

![add-search](assets/add-search.png)

### 設定新增的搜尋 {#configure-the-added-search}

選取已放置的 `Search` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 搜尋設定]** 索引標籤中，指定當訪客輸入查詢時，要如何搜尋路徑。

![search-settings](assets/search-settings.png)

* **[!UICONTROL 搜尋路徑]**
使用「新增專案」按鈕新增搜尋路徑，會限制內容搜尋。 例如，若要將搜尋限制在特定論壇，請選取置於頁面內的論壇元件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果頁面]**
結果會顯示在透過使用瀏覽器來選取包含 
`Search Results` 组件.

## 搜索结果 {#search-results}

### 將搜尋結果新增至頁面 {#add-search-results-to-a-page}

若要新增 `Search Results` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Search Results`

並將其拖曳至頁面上的適當位置。 與搜尋元件不同，不需要第二個頁面，因為結果將顯示在相同頁面上。

如果在網站內的其他位置使用「搜尋」，此頁面會顯示 `Search Results` 可設定為 `Result Page` 的任何或所有例項 `Search`.

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當需要使用者端程式庫時， `cq.social.hbs.search`，包含，這就是 `Search Result` 元件將會出現：

![search-result](assets/search-result1.png)

### 設定新增的搜尋結果 {#configure-the-added-search-result}

選取已放置的 `Search Results` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **[!UICONTROL 搜尋結果設定]** 索引標籤中，可指定當訪客輸入查詢時搜尋中包含哪些路徑。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 每页的搜索结果数]**

   定義每頁顯示的主題/帖子數。 預設值為10。

* **[!UICONTROL 搜尋路徑]**

   使用「新增專案」按鈕新增搜尋路徑，會限制內容搜尋。

## 附加信息 {#additional-information}

如需詳細資訊，請參閱 [搜尋Essentials](search-implementation.md) 適用於開發人員的頁面。
