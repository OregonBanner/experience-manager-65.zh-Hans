---
title: Teaser和策略
seo-title: Teasers and Strategies
description: 行銷活動通常使用Teaser當作吸引特定訪客群體進入關注其興趣內容的機制。 為特定行銷活動定義一或多個Teaser。
seo-description: Campaigns often use teasers as a mechanism to entice a specific segment of the visitor population through to content focused on their interests. One or more teasers are defined for a specific campaign.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 5%

---

# Teaser和策略{#teasers-and-strategies}

行銷活動通常使用Teaser當作吸引特定訪客群體進入關注其興趣內容的機制。 為特定行銷活動定義一或多個Teaser。

>[!NOTE]
>
>AEM 6.2已棄用Teaser元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 而非。

* **品牌頁面** 儲存在網站的Campaigns區段中。 品牌包含個別行銷活動。
* **行銷活動頁面** 儲存在網站的Campaigns區段中。 每個行銷活動都有個別頁面，每個頁面底下都會儲存Teaser定義。 容器或概觀頁面也包含有關個別Teaser頁面的某些資訊和統計資料。

AEM內的Teaser由幾個部分組成：

* **Teaser頁面** 儲存在適當的行銷活動頁面下，並保留每個特定行銷活動可用的Teaser段落定義。 顯示Teaser段落時，會使用這些定義，包括內容變數、用於選取變數和提升因子的區段。
* 此 **Teaser元件** 立即可用，並可讓您在內容頁面中建立特定Teaser段落的例項。 您可以從sidekick拖曳Teaser元件，然後指定您的Teaser定義以建立您自己的Teaser段落。 **注意：** AEM 6.2已棄用Teaser元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 而非。
* **Teaser段落** 是內容頁面中Teaser的實際例項。 這些功能可吸引部分訪客前往關注其興趣的內容。
* 包含以特定訪客區段為焦點之促銷活動內容的頁面。 通常Teaser段落會將訪客導向到這類頁面。

## 策略 {#strategies}

將Teaser段落新增至頁面時，您需要定義 **策略**.

這是因為，當其指派的區段都成功解析時，有數個Teaser可供選擇。 此 **策略** 然後指定用於選取所顯示Teaser的額外條件：

* **點按資料流分數**，根據訪客使用者端內容中保留的標籤和相關標籤點選（顯示訪客點按包含個別標籤的頁面的頻率）。 系統會比較Teaser頁面上定義之標籤的點選率。
* **Random**，針對「隨機」選擇；使用針對頁面產生的隨機因子，這可以透過以下方式檢視 [使用者端內容](/help/sites-administering/client-context.md).
* **第一個** 已解析區段清單中。 順序是行銷活動容器頁面中Teaser的順序。

此 [提升因數](/help/sites-administering/campaign-segmentation.md#boost-factor) 區段的「 」也會影響選取範圍。 這是新增至區段定義的加權因子，可增加/減少選取該區段的相對可能性。

各種選擇標準的流程和相互關係以範例最能說明（此方法也可用來確保您的Teaser將觸及所需對象）。

如果已建立下列區段並指派其各自的Boost因子：

| 市场细分 | 提升因數 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

我們使用下列Teaser定義：

<table>
 <tbody>
  <tr>
   <td>营销活动</td>
   <td>Teaser</td>
   <td>指派的區段</td>
   <td>指派的標籤 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1， S2</td>
   <td>商業、行銷</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>行銷</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商务<br /> </td>
  </tr>
 </tbody>
</table>

那麼如果我們將此套用至訪客，其中：

* **S1**， **S2** 和 **S6** 已成功解析

* 標籤 **行銷** 有3個點選
* 標籤 **企業** 有6次點選

我們可以看到結果：

* 匹配成功 — 指派給Teaser的任何區段是否成功解析為目前訪客？
* 提升因子 — 所有適用區段中的最高提升因子
* 點按流分數 — 所有適用標籤點選的累加總數

在套用適當策略之前計算得出的值：

<table>
 <tbody>
  <tr>
   <td>营销活动</td>
   <td>Teaser</td>
   <td>指派的區段</td>
   <td>标记 </td>
   <td>相符成功？</td>
   <td>產生的提升因數</td>
   <td>產生的Clickstream分數 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1， S2</td>
   <td>商業、行銷</td>
   <td>是</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>是</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
   <td>否</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
   <td>是<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1、S2、S6</td>
   <td>行銷</td>
   <td>是</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商务</td>
   <td>是</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

這些值用於決定訪客將看到的Teaser，取決於 **策略** 套用至Teaser段落：

<table>
 <tbody>
  <tr>
   <td>战略</td>
   <td>產生的Teaser</td>
   <td>评论</td>
  </tr>
  <tr>
   <td>第一个</td>
   <td>T5</td>
   <td>只有T5和T6被視為其區段全部解析 <i>和</i> 它們具有最高的提升因子。 傳回的清單順序為T5、T6；因此會選取並顯示T5。</td>
  </tr>
  <tr>
   <td>随机</td>
   <td>T5或T6</td>
   <td>這兩個Teaser都有完全解決和相同提升因子的區段。 因此，這兩個Teaser會以相等比例顯示。</td>
  </tr>
  <tr>
   <td>點按資料流分數</td>
   <td>T6</td>
   <td><p>T1、T4、T5和T6的區段都會解析給訪客。 T5和T6的較高提升因子則排除T1和T4。 最後，T6的點按資料流分數越高，系統就會選取此專案。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果在上述解析度技巧之後，有多個Teaser可供選擇，則內部選擇（隨機）將選擇單個Teaser進行顯示。
>
>例如，如果策略為「點按資料流分數」，且T5的「點按資料流分數」與T6相同（即6而非3），則會使用內部選擇（隨機）來選取這兩個專案之一。

Teaser頁面/段落可用來將特定訪客區段引導至聚焦於其興趣的內容。 附註可呈現一系列選項供訪客選擇，或僅顯示一個根據特定訪客區段的Teaser段落；例如，顯示的Teaser段落可能取決於訪客的年齡。

通常Teaser頁面是暫時性動作，會持續一段特定時間，直到被下一個Teaser頁面取代。

建立您的品牌和行銷活動後，您可以建立和設定您的Teaser體驗。

### 為您的Teaser建立接觸點 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>AEM 6.2已棄用Teaser元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 而非。

1. 導覽至您要放置Teaser段落的內容頁面，此段落將導向您的行銷活動頁面。
1. 新增 **Teaser** 元件(可在 **個人化** 部分)。 首次建立時，將顯示尚未設定行銷活動路徑：

   ![chlimage_1](assets/chlimage_1.png)

1. 編輯Teaser元件以新增：

   * **行銷活動路徑**
包含個別Teaser頁面的促銷活動頁面路徑；區段會確切決定要顯示哪個Teaser。

   * **[策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
成功解析多個區段時用於選取的方法。
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 按一下 **確定** 以儲存。 根據您在Teaser上設定的區段以及您目前以身分登入之使用者的設定檔，將顯示適當的內容：

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 將滑鼠移至Teaser段落上方，以顯示問號圖示（元件的右下角）。 按一下以檢視套用的區段以及它們目前是否解析。

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Teaser概述 {#teaser-overview}

除了MCM中的行銷活動檢視外，行銷活動頁面也會提供與其連線的Teaser的相關資訊：

1. 從 **網站** 主控台，開啟促銷活動頁面；例如：

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   以下顯示Teaser定義和檢視統計資料的概觀：

   ![chlimage_1-4](assets/chlimage_1-4.png)
