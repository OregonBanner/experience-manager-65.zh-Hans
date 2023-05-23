---
title: 建立组件数据与 Adobe Analytics 属性的映射
seo-title: Mapping Component Data with Adobe Analytics Properties
description: 瞭解如何使用SiteCatalyst屬性對應元件資料。
seo-description: Learn how to map component data with SiteCatalyst properties.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# 建立组件数据与 Adobe Analytics 属性的映射{#mapping-component-data-with-adobe-analytics-properties}

將元件新增至框架，收集要傳送至Adobe Analytics的資料。 收集Analytics資料而設計的元件，會將資料儲存在適當的位置 **CQ變數**. 當您將這類元件新增到框架時，框架會顯示CQ變數清單，以便您將每個變數新增到適當的 **Analytics變數**.

![aa-11](assets/aa-11.png)

當 **AEM檢視** 開啟，Analytics變數會出現在內容尋找器中。

![aa-12](assets/aa-12.png)

您可以使用相同對應多個Analytics變數 **CQ變數**.

![chlimage_1-68](assets/chlimage_1-68.png)

當頁面載入且符合下列條件時，對應的資料會傳送至Adobe Analytics：

* 頁面與框架相關聯。
* 頁面會使用新增至框架的元件。

使用以下程式，將CQ元件變數與Adobe Analytics報表屬性對應。

1. 在 **AEM檢視**，將追蹤元件從sidekick拖曳至架構上。 例如，拖曳 **頁面** 元件元件來自 **一般** 類別。

   ![aa-13](assets/aa-13.png)

   有多個預設元件群組： **一般**， **商務**， **Communities**、和 **其他**. 您的AEM執行個體可設定為顯示不同的群組和元件。

1. 若要使用元件中定義的變數對應Adobe Analytics變數，請拖曳 **Analytics變數** 從內容尋找器移至追蹤元件上的欄位。 例如，拖曳 `Page Name (pageName)` 至 `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >為架構選取的報表套裝ID (RSID)會決定出現在內容尋找器中的Adobe Analytics變數。

1. 對其他元件和變數重複前兩個步驟。

   >[!NOTE]
   >
   >您可以對應多個Analytics變數(例如 `props`， `eVars`， `events`)至相同的CQ變數(例如： `pagedata.title`)

   >[!CAUTION]
   >
   >強烈建議：
   >
   >* `eVars` 和 `props` 都會對應至開頭為以下列任一專案的CQ變數： `pagedata.X` 或 `eventdata.X`
   >* 而事件應對應至變數，開頭為 `eventdata.events.X`


1. 若要讓架構可用於網站的發佈執行個體，請開啟 **頁面** 索引標籤，然後按一下 **啟動框架。**

## 對應產品相關變數 {#mapping-product-related-variables}

AEM使用慣例來命名產品相關變數和事件，這些變數和事件會對應至Adobe Analytics產品相關屬性：

| CQ變數 | 分析變數 | 描述 |
|--- |--- |--- |
| `product.category` | `product.category` （轉換變數） | 產品類別。 |
| `product.sku` | `product.sku` （轉換變數） | 產品sku。 |
| `product.quantity` | `product.quantity` （轉換變數） | 正在購買的產品數量。 |
| `product.price` | `product.price` （轉換變數） | 產品價格。 |
| `product.events.<eventName>` | 與報表中的產品建立關聯的成功事件。 | `product.events` 是事件的前置詞，命名為 *eventName。* |
| `product.evars.<eVarName>` | 轉換變數( `eVar`)以與產品建立關聯。 | `product.evars` 是以下名稱的eVar變數的前置詞： *eVarName。* |

有幾個AEM Commerce元件會使用這些變數名稱。

>[!NOTE]
>
>請勿將Adobe Analytics產品屬性對應至CQ變數。 依照表格所述設定產品相關對應實際上等同於對應產品變數。

### 在Adobe Analytics上檢查報告 {#checking-reports-on-adobe-analytics}

1. 使用提供給AEM的相同憑證登入Adobe Analytics網站。
1. 請確定選取的RSID是先前步驟中所使用的RSID。
1. 在 **報表** （在頁面左側）選取 **自訂轉換**，則 **自訂轉換1-10** 並選取對應的變數 `eVar7`

1. 根據您使用的Adobe Analytics版本，您平均需要等待45分鐘，以便報表更新所用的搜尋字詞；例如，範例中的茄子

## 搭配Adobe Analytics架構使用內容尋找器(cf#) {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

最初，當您開啟Adobe Analytics架構時，內容尋找器會包含以下預先定義的Analytics變數：

* 流量
* 转化
* 事件

選取RSID時，屬於該RSID的所有變數都會新增到清單中。\
此 `cf#` 需要將Analytics變數對應到出現在不同追蹤元件上的CQ變數。 請參閱設定基本追蹤的框架。

根據為框架選取的檢視，內容尋找器將由Analytics變數(在AEM檢視中)或CQ變數（在Analytics檢視中）填入。

清單可透過下列方式操作：

1. 當在 **AEM檢視**，您可根據使用3個篩選按鈕選取的變數型別來篩選清單：

   * 若 *無按鈕* 選取時，清單會顯示完整清單。
   * 如果 **流量** 按鈕時，清單只會顯示屬於流量區段的變數。
   * 如果 **轉換** 按鈕時，清單只會顯示屬於轉換區段的變數。
   * 如果 **事件** 按鈕時，清單只會顯示屬於事件區段的變數。

   >[!NOTE]
   >
   >一次只能啟用一個篩選按鈕。

   1. 清單也有搜尋功能，可依據在搜尋欄位中輸入的文字篩選元素。
   1. 如果在搜尋清單中的元素時啟用了篩選選項，則顯示的結果也會根據活動按鈕進行篩選。
   1. 清單可隨時使用旋轉箭頭按鈕重新載入。
   1. 如果在架構上選取了多個RSID，清單中的所有變數都會使用選取的RSID內使用的所有標籤來顯示。


1. 在Adobe Analytics檢視中，內容尋找器會顯示屬於CQ檢視中拖曳之追蹤元件的所有CQ變數。

   * 例如，如果 **下載元件** 是 *僅拖曳一個* 在CQ檢視中（其中包含兩個可對應的變數） *eventdata.downloadLink* 和 *eventdata.events.startDownload*)，則內容尋找器切換至Adobe Analytics檢視時看起來會像這樣：

   ![aa-22](assets/aa-22.png)

   * 這些變數可拖放至屬於3個變數區段之一的任何Adobe Analytics變數上(**流量**， **轉換** 和 **事件**)。

   * 將新的追蹤元件拖曳至CQ檢視中的框架時，屬於該元件的CQ變數會自動新增至Adobe Analytics檢視中的內容尋找器(cf#)。
   >[!NOTE]
   >
   >在任何指定時間，只能將一個CQ變數對應至Adobe Analytics變數。

## 使用AEM檢視和Analytics檢視 {#using-aem-view-and-analytics-view}

在任何指定時間，使用者可以選擇在框架頁面上切換檢視Adobe Analytics對應的兩種方式。 從2個不同的角度來看，這2個檢視可提供架構內對應的更佳概述。

### AEM檢視 {#aem-view}

![aa-23](assets/aa-23.png)

以上圖為例， **AEM檢視** 具有以下屬性：

1. 這是框架開啟時的預設檢視。
1. 左側：內容尋找器(cf#)會根據所選RSID由Adobe Analytics變數填入。
1. 索引標籤標題(**AEM檢視** 和 **Analytics檢視**)：使用這些選項可在兩個檢視之間切換。

1. **AEM檢視**：

   1. 如果框架具有從其父項繼承的元件，則會在此處列出這些元件，以及對應到元件的變數。

      1. 繼承的元件已鎖定。
      1. 若要解除鎖定繼承的元件，只要按兩下元件名稱旁的掛鎖即可
      1. 為了恢復繼承，您必須刪除已解鎖的元件；之後它將重新獲得其鎖定狀態。
   1. **將元件拖曳到此處以包含在分析框架中**：元件可從Sidekick拖曳並放置在這裡。
   1. 您可以找到目前包含在分析框架中的所有元件：

      1. 若要新增元件，請從sidekick的「元件」標籤中拖曳一個元件
      1. 若要刪除元件及其所有對映，請從元件的快顯選單中選取「刪除」，然後在確認對話方塊上接受刪除。
      1. 請記住，元件只能從建立該元件的架構中刪除，且無法從傳統意義上的子架構中刪除（只能覆寫）。


### 分析檢視 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 您可以透過切換至 **Analytics檢視** 索引標籤進行編輯。
1. 左側：內容尋找器(cf#)由CQ變數填入，根據在CQ檢視中拖曳到框架上的元件。
1. 索引標籤標題(**AEM檢視** 和 **Analytics檢視**)：使用這些選項可在兩個檢視之間切換。

1. 三個表格（流量、轉換、事件）列出所有可用的Adobe Analytics變數。 屬於所選RSID。 此處顯示的對應應與AEM檢視中的對應相同：

   * **流量**:

      * 流量變數( `prop1`)對應至CQ變數( `eventdata.downloadLink`)

      * 當元件旁邊有掛鎖時，這表示它繼承自父框架，因此無法編輯
   * **转化**:

      * 轉換變數( `eVar1`)對應至CQ變數( `pagedata.title`)

      * 轉換變數( `eVar3`)對應至內嵌新增的javascript運算式，方法是按兩下CQ變數欄位，然後手動輸入程式碼
   * **Event**:

      * 事件變數( `event1`)對應至CQ事件( `eventdata.events.pageView`)



>[!NOTE]
>
>您也可以內嵌填入任何表格的CQ變數欄，方法是按兩下該欄位並新增文字。 這些欄位接受javascript作為輸入。
>
>例如，旁邊的 `prop3` 您可以新增：
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
以傳送 *標題* 與其串連的頁面的 *sitesection* 使用 *：* （冒號）和前置詞 *Adobe* 作為 `prop3`

>[!CAUTION]
在任何指定時間，只能將一個CQ變數對應至Adobe Analytics變數。
