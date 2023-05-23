---
title: 基礎元件
seo-title: Foundation Components
description: 基礎元件
seo-description: null
uuid: 3caf9123-ae58-4590-af2f-57ef076daf7f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: ea2a523e-8d26-4be4-822f-35f153e40308
docset: aem65
legacypath: /content/docs/en/aem/6-2/author/page-authoring/default-components/editmode
pagetitle: Foundation Components
exl-id: 278701f3-3f0c-45f4-90b7-c0e316a7da8a
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '7200'
ht-degree: 9%

---

# 基礎元件 {#foundation-components}

>[!CAUTION]
>
>AEM 6.5已棄用大部分的基礎元件。請參閱 [發行說明](/help/release-notes/deprecated-removed-features.md) 以取得進一步資訊。
>
>Adobe建議使用更現代、更可擴充的 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 在AEM專案中。 這些元件是 [We.Retail範例內容](/help/sites-developing/we-retail.md) 也可以 [另外安裝並用於開發](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html) 由您的管理員提供。
>
>您可以使用 [AEM Modernize Tools Suite](https://opensource.adobe.com/aem-modernize-tools/) 以重構您的基礎元件型網站來使用核心元件。

基礎元件是專為製作標準網頁的內容而設計。 這些元件是AEM標準安裝中現成可用的元件子集。

有些可透過元件瀏覽器立即取得。 您也可以使用取得其他各種資訊。 [設計模式](/help/sites-authoring/default-components-designmode.md) （如果頁面是以靜態範本為基礎）或 [編輯範本](/help/sites-authoring/templates.md) （如果頁面是以可編輯的範本為基礎）。

支援使用基礎元件，但基礎元件已基本淘汰，由核心元件取代，提供更大的擴充性和靈活性。

>[!NOTE]
>
>本節僅討論標準AEM安裝中現成可用的元件。
>
>根據您的執行個體，您可能已針對您的需求明確開發自訂元件。 這些自訂元件的名稱甚至可能與此處討論的部分元件相同。

這些元件可在 **元件** 頁面編輯器側面板的索引標籤 [編輯頁面](/help/sites-authoring/editing-content.md).

您可以選取元件，並將其拖曳至頁面上的所需位置。 然後，您可以使用以下方式編輯它：

* [配置属性](/help/sites-authoring/editing-page-properties.md)
* [编辑内容](/help/sites-authoring/editing-content.md)

* [编辑内容 – 全屏模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

元件會根據稱為元件群組的各種類別排序，包括：

* [一般](#general)：包括基本元件，包括文字、影像、表格和圖表。
* [欄](#columns)：包含組織內容版面配置所需的元件。
* [表單](#formgroup)：包含建立表單所需的所有元件。

## 常规 {#general}

一般元件是您用來建立內容的基本元件。

### 帐户项 {#account-item}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

您可以定義具有標題和說明的連結。

![chlimage_1-88](assets/chlimage_1-88.png)

### 自适应图像 {#adaptive-image}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [影像核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html) 而非。

Adaptive Image Foundation元件會產生大小適合開啟網頁之視窗的影像。 若要使用元件，請提供檔案系統或DAM中的影像資源。 開啟網頁時，網頁瀏覽器會下載已調整大小的影像復本，以適合目前的視窗。

下列特性可決定視窗的大小：

* 裝置畫面：行動裝置通常會顯示網頁，以便橫跨整個畫面。
* 網頁瀏覽器視窗大小：筆記型電腦和桌上型電腦的使用者可以調整網頁瀏覽器視窗的大小。

例如，在手機上開啟網頁時，元件會產生一個小影像，而在平板電腦上開啟時，則會產生一個中等大小的影像。 在筆記型電腦上，當頁面在最大化的網頁瀏覽器中開啟時，元件會建立並傳送大型影像。 當網頁瀏覽器調整大小以適合熒幕的一部分時，元件會透過提供較小的影像進行調整，並重新整理檢視。

#### 支援的影像格式 {#supported-image-formats}

您可以將下列副檔名的影像檔案搭配最適化影像元件使用：

* .jpg
* .jpeg
* .png
* .gif &#42;&#42;

>[!CAUTION]
>
>AEM不支援動畫GIF檔案，以進行最適化轉譯。

#### 影像大小和品質 {#images-sizes-and-quality}

下表列出針對指定檢視區寬度產生的影像寬度。 計算產生影像的高度是為了維持不變的外觀比例，且影像邊緣內不會出現空白字元。 可使用裁切來避免出現空白字元。

當影像為JPEG影像時，檢視區大小也會影響JPEG品質。 可以使用下列JPEG品質：

* 低(0.42)
* 中(0.82)
* 高(1.00)

| **檢視區寬度範圍（畫素）** | **影像寬度（畫素）** | **JPEG 质量** | **目標裝置型別** |
|---|---|---|---|
| 寬度&lt;= 319 | 320 | 低 |  |
| 寬度= 320 | 320 | 中 | 行動電話（直向） |
| 320 &lt;寬度&lt; 481 | 480 | 中 | 行動電話（橫向） |
| 480 &lt;寬度&lt; 769 | 476 | 高 | 平板電腦（縱向） |
| 768 &lt;寬度&lt; 1025 | 620 | 高 | 平板電腦（橫向） |
| 寬度&lt;= 1025 | 完整（原始大小） | 高 | 桌面 |

#### 属性 {#properties}

此對話方塊可讓您編輯最適化影像元件執行個體的屬性，其中許多屬性與其所依據的影像元件共用。 屬性位於兩個標籤中：

* **图像**

   * **影像**
從內容尋找器拖曳影像，或按一下以開啟瀏覽視窗，您可在此載入影像。 載入影像後，您可以裁切、旋轉或刪除影像。 若要放大和縮小影像，請使用影像下方的投影列（在「確定」和「取消」按鈕上方）

   * **裁切**
裁剪部分影像。 拖曳邊框以裁切影像。

   * **旋轉**
重複按一下「旋轉」，直到視需要旋轉影像為止。

   * **清除**
移除目前的影像。

* **高级**

   * **標題**
最適化影像元件未使用此屬性。

   * **替代文字**
用於影像的替代文字。

   * **連結至**
最適化影像元件未使用此屬性。

   * **說明**
最適化影像元件未使用此屬性。

#### 擴充最適化影像元件 {#extending-the-adaptive-image-component}

如需自訂最適化影像元件的詳細資訊，請參閱 [瞭解自我調整影像元件](/help/sites-developing/responsive.md#using-adaptive-images).

### 轮盘 {#carousel}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [傳送核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html) 而非。

「輪播」元件可讓您顯示與個別頁面相關聯的影像：

* 一次一個
* 短時間
* 依照您指定的順序
* 具有您指定的時間延遲

可點按控制項也可讓使用者依需求即時循環顯示頁面。 選取目前可見的頁面影像會前往該頁面。 換言之，輪播會作為導覽控制項。

#### 属性 {#properties-1}

這些屬性位於兩個標籤中：

* **輪播**
您可在此處指定輪播的運作方式：

   * 播放速度下一張投影片顯示前的時間（毫秒）。
   * 切換時間兩張幻燈片之間的切換時間（毫秒）。
   * 控制項樣式下拉式選單中有多種選項；例如「上一個/下一個按鈕」、「右上切換」。

* **列表**

   您可在此處指定轉盤中包含頁面的方式：

   * **使用以下專案建立清單**
建立頁面清單有數種方式 — 子頁面、固定清單、搜尋或進階搜尋（全部說明如下）。
無論您選擇哪種方法，您包含在清單中的頁面都應該已有一個與頁面相關聯的影像。 這是轉盤中顯示的影像。 如果特定頁面的頁面屬性下沒有特定頁面的影像，您應該先將影像與頁面建立關聯，然後再開始。 如果沒有顯示，輪播會顯示大部分空白頁面。 另請參閱 [編輯頁面屬性](/help/sites-authoring/editing-page-properties.md).
視您選擇的專案而定，會出現新面板：

      * **子页面选项**

         * **父頁面**
手動或使用選取器指定路徑。 留空將使用目前頁面作為父頁面。
      * **固定列表选项**

         * **頁面**
選取頁面清單。 使用 
`+` 以新增更多專案，並按「向上/向下」按鈕以調整順序。
      * **搜索选项**

         * **開始於**
手動或使用選取器輸入起始路徑。

         * **搜尋查詢**
您可以輸入純文字搜尋查詢。
      * **高级搜索选项**

         * **QueryBuilder述詞記號**
您可以使用Querybuilder述詞記號來輸入搜尋查詢。 例如，您可以輸入&quot;fulltext=Marketing&quot;，讓內容中包含&quot;Marketing&quot;的所有頁面顯示在輪播中。
另請參閱 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) 以完整討論查詢運算式和更多範例。
   * **排序方式**
選取 
`jcr:title`， `jcr:created`， `cq:lastModified`，或 `cq:template` 下拉式選單中的。

   * **限制**
選填。 您想在輪播中使用的專案數上限。





>[!NOTE]
>
>您可以為Adobe Experience Manager建立自訂轉盤元件，在AEM DAM中顯示數位資產。 另請參閱 [建立Adobe Experience Manager的自訂轉盤元件](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en).

### 图表 {#chart}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

圖表元件可讓您新增長條圖、折線圖或圓餅圖。 AEM會根據您提供的資料建立圖表。 您可以直接在「資料」標籤中輸入，或複製並貼上試算表，以提供資料。

* **数据**

   * **圖表資料**
使用CSV格式輸入您的圖表資料；逗號分隔值格式使用逗號(&quot;，&quot;)作為欄位分隔符號。

* **高级**

   * **圖表型別**
從圓形圖、折線圖和長條圖選取。

   * **替代文字**
顯示替代文字而非圖表。

   * **寬度**
圖表的寬度（畫素）。

   * **高度**
圖表的高度（畫素）。

以下顯示圖表資料的範例，後面接著產生的長條圖：

![chlimage_1-89](assets/chlimage_1-89.png) ![dc_chart_use](assets/dc_chart_use.png)

>[!NOTE]
>
>您可以建立自訂AEM圖表控制項，在AEM JCR中顯示資料。 如需詳細資訊，請參閱 [在圖表中顯示Adobe Experience Manager資料](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en).

### 内容片段 {#content-fragment}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 而非。

[內容片段](/help/sites-authoring/content-fragments.md) 會建立和管理為不受頁面影響的資產。 您随后可以在创作内容页面时使用这些片段及其变体。

### 设计导入程序 {#design-importer}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

此元件可讓您上傳包含設計封裝的zip檔案。

### 下载 {#download}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

下載元件會在選取的網頁上建立連結，以下載特定檔案。 您可以從「內容尋找器」拖曳資產或上傳檔案。

* **下载**

   * **說明**
與下載連結一起顯示的簡短說明。

   * **檔案**
可在產生的網頁上下載的檔案。 從內容尋找器拖曳資產或選取區域，以便上傳您要下載的檔案。

以下範例顯示Geometrixx的下載元件：

![dc_download_use](assets/dc_download_use.png)

### 外部 {#external}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

外部應用程式整合元件(**外部**)可讓您使用iframe將外部應用程式內嵌至AEM頁面。

* **外部**

   * **目標應用程式**
指定要整合的Web應用程式的URL；例如：

      ```
      https://en.wikipedia.org/wiki/Main_Page
      ```

   * **傳遞引數**
核取方塊，讓引數在需要時傳遞至應用程式。

   * **寬度和高度**定義iframe的大小

外部應用程式已整合至AEM頁面的段落系統；例如，使用 `https://en.wikipedia.org/wiki/Main_Page`：

![chlimage_1-90](assets/chlimage_1-90.png)

>[!NOTE]
>
>視您的使用案例而定，整合外部應用程式可使用其他選項，例如 [Portlet的整合](/help/sites-administering/aem-as-portal.md).

### 闪光灯 {#flash}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

Flash元件可讓您載入Flash影片。 您可以從內容尋找器將Flash資產拖曳至元件，也可以使用對話方塊：

* **闪光灯**

   * **Flash 影片**

      Flash影片檔案。 從內容尋找器拖曳資產，或按一下以開啟瀏覽視窗。

   * **大小**

      Dimension（以畫素為單位）的容納影片的顯示區域。

* **备用图像**

   要顯示的替代影像

* **高级**

   * **上下文菜单**

      指示應顯示或隱藏內容功能表。

   * **視窗模式**

      視窗的顯示方式，例如不透明、透明或作為不同（實心）視窗。

   * **背景颜色**

      從提供的色彩圖表中選取的背景色彩。

   * **最低版本**

      執行影片所需的最低AdobeFlash Player版本。 預設值為9.0.0。

   * **属性**

      需要任何進一步的屬性。

### 图像 {#image}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [影像核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html) 而非。

影像元件會根據指定的引數顯示影像和隨附文字。

您可以上傳影像，然後編輯和處理影像（例如，裁切、旋轉、新增連結/標題/文字）。

您可以從「 」拖放影像 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser) 直接連結至元件或其 [設定對話方塊](/help/sites-authoring/editing-content.md#component-edit-dialog). 您也可以從「設定」對話方塊上傳影像；此對話方塊也會控制影像的所有定義與操作：

![chlimage_1-91](assets/chlimage_1-91.png)

影像上傳後（而非上傳前），您可以使用 [就地編輯](/help/sites-authoring/editing-content.md#edit-content) 若要視需要裁切/旋轉影像：

![](do-not-localize/chlimage_1-15.png)

>[!NOTE]
>
>就地編輯器在編輯時會使用影像的原始大小和外觀比例。 您也可以指定高度和寬度屬性。 儲存編輯變更時，會套用屬性中定義的任何大小及外觀比例限制。
>
>視您的執行個體而定，可能也會對您施加最小和最大限制 [頁面設計](/help/sites-developing/designer.md). 這些限制是在專案實作期間制定的。

全熒幕編輯模式中有數個其他選項可供使用；例如，地圖和縮放：

![](do-not-localize/chlimage_1-16.png)

>[!NOTE]
>
>無法使用Internet Explorer監視上傳進度。
>
>Internet Explorer使用者必須上傳影像並按一下 **確定**，然後重新開啟影像以在預覽中檢視上傳的檔案，並能夠執行修改（即裁切）。
>
>請參閱 [認證平台](/help/release-notes/release-notes.md#certifiedplatforms) 區段以取得AEM所使用HTML5功能的詳細資訊。

載入影像時，您可以設定下列專案：

* **地图**

   若要對應影像，請選取「對應」。 您可以指定建立影像地圖的方式（矩形、多邊形等）以及區域應指向的位置。

* **裁剪**

   若要裁剪掉部分影像，請選取「裁切」。 使用滑鼠裁切影像。

* **旋转**

   若要旋轉影像，請選取「旋轉」。 重複使用，直到影像以您想要的方式旋轉。

* **清除**

   移除目前的影像。

* **标题**

   影像的標題。

* **替换文本**

   建立無障礙內容時使用的替代文字。

* **連結至**

   建立資產或網站內其他頁面的連結。

* **描述**

   影像的說明。

* **大小**

   設定影像的高度和寬度。

>[!NOTE]
>
>部分選項僅在全熒幕編輯器中可用。

最終影像(包含 **標題** 和 **說明**)可顯示為：

![chlimage_1-92](assets/chlimage_1-92.png)

### 布局容器 {#layout-container}

此元件提供格點段落系統，讓您在 [回應式格線](/help/sites-authoring/responsive-layout.md). 您可以根據目標裝置的寬度（包括各種手機、平板電腦和桌上型電腦）定義不同的內容配置。

![chlimage_1-93](assets/chlimage_1-93.png)

>[!NOTE]
>
>此元件已透過實作 [HTML範本語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).

### 列表 {#list}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [列出核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) 而非。

List元件可讓您設定顯示清單的搜尋條件：

* **列表**

   * **生成列表对象**

      您可在此處指定清單擷取其內容的位置。 有數種方法：

   * 視您選擇的專案而定，會出現新面板：

      * **子页面选项**

         * **子項** （父頁面）

            手動或使用選取器指定路徑。 留空將使用目前頁面作為父頁面。
      * **固定列表选项**

         * **页面**

            選取頁面清單。 使用+以新增更多專案，並使用向上/向下按鈕調整順序。
      * **搜索选项**

         * 开始

            手動或使用選取器輸入起始路徑。

         * 搜索查询

            您可以輸入純文字搜尋查詢。
      * **高级搜索选项**

         * **QueryBuilder 谓词记号**

            您可以使用Querybuilder述詞記號來輸入搜尋查詢。 例如，您可以輸入&quot;fulltext=Marketing&quot;，讓內容中包含&quot;Marketing&quot;的所有頁面顯示在輪播中。

            另請參閱 [QueryBuilder API](/help/sites-developing/querybuilder-api.md) 以完整討論查詢運算式和更多範例。
      * **标记**

         指定 **上層頁面**， **標籤/關鍵字**，以及您所需的符合條件。
   * **显示方式**

      您希望專案列出的方式；包括連結、Teaser和新聞。

   * **排序依据**

      是否要排序清單，如果是，則為用於排序的條件。 您可以輸入條件，或從提供的下拉式清單中選取條件。

   * **限制**

      指定您要在清單中顯示的最大專案數。

   * **启用信息源**

      指示是否應針對清單啟動RSS摘要。

   * **每页显示条目数**

      您可以在此處指定要一次顯示的清單專案數量。 專案數量超過指定數量的清單會使用分頁功能將清單分成數個部分顯示。






下列範例顯示 **清單** 以元件顯示子頁面清單的方式（設計由網站設計的自訂CSS定義控制）。

![dc_list_use](assets/dc_list_use.png)

### 登录 {#login}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

提供使用者名稱和密碼欄位。

![chlimage_1-94](assets/chlimage_1-94.png)

您可以設定：

* 登录

   * 区域标签

      輸入欄位的匯入文字。

   * 用户名标签

      標示使用者名稱欄位的文字。

   * 密码标签

      標籤密碼欄位的文字。

   * “登录”按钮标签

      登入按鈕的文字。

   * 重新導向至

      您可以在您的網站上指定當使用者登入後應該開啟的頁面。

* 已登录

   * “继续”按钮标签

      表示使用者已登入的文字。

### 订单状态 {#order-status}

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

* **标题**

   * **标题**

      指定您要顯示的標題文字。

   * **链接**

      指定應顯示訂單狀態的頁面（產品）。

   * **类型/大小**

      從提供的選取範圍中選取。

![chlimage_1-95](assets/chlimage_1-95.png)

### 引用 {#reference}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html) 而非。

此 **參考資料** 元件可讓您參照AEM網站其他頁面（在目前執行個體內）的文字。 參考段落的內容會出現在目前頁面上。 內容會在來源段落變更時更新（可能需要重新整理頁面）。

* **段落引用**

   * **引用**

      指定您要參考的頁面和段落的路徑（包含內容）。

若要指定段落的路徑，您必須在路徑（頁面）的結尾加上：

`.../jcr:content/par/<paragraph-ID>`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par/similar-products`

除了參照特定段落之外，還可以修改路徑以指定整個段落系統。 您可以使用下列字尾來參照路徑：

`/jcr:content/par`

例如：

`/content/geometrixx-outdoors/en/equipment/biking/cajamara/jcr:content/par`

設定後，內容會完全顯示在來源頁面上。 只有在開啟元件進行編輯時，才會看到它是參照：

![chlimage_1-96](assets/chlimage_1-96.png)

### 搜索 {#searching}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [快速搜尋核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/quick-search.html) 而非。

搜尋元件會將搜尋功能新增至您的頁面。

您可以設定：

* 搜索

   * **节点类型**

      如果搜尋僅限於特定節點型別，請在此處列出它們；例如， `cq:Page`.

   * **搜索路径**

      指定您要搜尋的分支的根頁面。

   * **搜索按钮文本**

      實際搜尋按鈕上顯示的名稱。

   * **統計資料文字**

      搜尋結果上方顯示的文字。

   * **无结果文本**

      如果沒有結果，則會顯示在此處輸入的文字。

   * **拼写检查文本**

      如果有人輸入類似的詞語，此文字會顯示在該詞語之前。
例如，如果您輸入 `Geometrixxe`，系統會顯示「您是不是要這麼做？ Geometrixx&quot;.

   * **類似頁面文字**

      在類似頁面的結果旁邊顯示的文字。 若要檢視具有類似內容的頁面，請按一下此連結。

   * **相關搜尋文字**

      旁邊顯示的文字會搜尋相關辭彙和主題。

   * **搜尋趨勢文字**

      使用者輸入的搜尋字詞上方標題。

   * **結果頁面標籤**

      此清單底部顯示的文字，包含其他結果頁面的連結。

   * **上一個標籤**

      顯示在先前搜尋頁面連結上的名稱。

   * **下一個標籤**

      顯示在後續搜尋頁面連結上的名稱。

下列範例顯示搜尋單字後的「搜尋」元件 *`geometrixx`* 從標準安裝的根目錄。 它也會說明結果的分頁：

![dc_search_use](assets/dc_search_use.png)

下列範例顯示一個搜尋字詞，拼字錯誤且無法使用：

![dc_search_usenotfound](assets/dc_search_usenotfound.png)

### Sitemap {#sitemap}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [導覽](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/navigation.html)， [語言導覽](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/language-navigation.html)、和 [階層連結核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/breadcrumb.html) 而非。

自動的網站地圖清單（使用預設設定）會列出目前網站中的所有頁面（作為作用中連結）。 例如，擷取會顯示：

![dc_sitemap_use](assets/dc_sitemap_use.png)

如有需要，您可以設定下列專案：

* **Sitemap**

   * **根路径**

      清單開始位置的路徑。

### 幻灯片放映 {#slideshow}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [傳送核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html) 而非。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

此元件可讓您載入一系列影像，以便在頁面上以投影片形式顯示。 您可以新增或移除影像，並為每個影像指派標題。 在「進階」下，您也可以指定顯示區域的大小。

您可以設定：

* **幻灯片**

   * **新幻灯片**

      您可以使用 **新增** (和 **移除**)按鈕。

   * **标题**

      視需要指定標題。 標題覆蓋在適當的幻燈片上。

* **高级**

   * **大小**

      以畫素為單位指定寬度和高度。

然後投影片元件會依序重複顯示每個投影片，並停留一小段時間，然後再淡入下一張投影片：

![dc_slideshow_use](assets/dc_slideshow_use.png)

### 表 {#table}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) 而非。

>[!NOTE]
>
>此 **表格** 基礎元件是以 [RTF編輯器](/help/sites-authoring/rich-text-editor.md)，如下所示 **[文字](#text)** 基礎元件。

此 **表格** 元件已預先設定為可讓您建構、填滿及格式化表格。 使用對話方塊，您可以透過以下任一方式設定表格並建立內容：

* 從頭開始
* 從外部編輯器（例如Excel、OpenOffice和Notepad）複製和貼上試算表或表格。

您可以使用內嵌編輯器對內容進行基本變更：

![dc_table](assets/dc_table.png)

在全熒幕模式中，您可以設定表格版面配置：

![chlimage_1-97](assets/chlimage_1-97.png)

下列熒幕擷圖顯示表格元件的範例；設計由網站特定的CSS決定：

![dc_table_use](assets/dc_table_use.png)

### 标记云 {#tag-cloud}

標籤雲會以圖形呈現選取的標籤，這些標籤已套用至您網站內的內容：

![dc_tagclouduse](assets/dc_tagclouduse.png)

設定Tag Cloud元件時，您可以指定：

* **要显示的标记**

   要顯示的標籤收集來源。 從頁面、具有所有子項或所有標籤的頁面中選取。

* **页面**

   選取要參考的頁面。

* **标记上无链接**

   顯示的標籤是否應該做為連結。

如需套用標籤的詳細資訊，請造訪 [使用標籤](/help/sites-authoring/tags.md).

### 文本 {#text}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) 而非。

>[!NOTE]
>
>此 **文字** 基礎元件是以 [RTF編輯器](/help/sites-authoring/rich-text-editor.md)，如下所示 **表格** 基礎元件。

文字元件可讓您使用WYSIWYG編輯器輸入文字區塊，其功能由 [RTF編輯器](/help/sites-authoring/rich-text-editor.md). 選取的圖示可讓您格式化文字，包括字型特性、對齊、連結、清單和縮排。

![chlimage_1-98](assets/chlimage_1-98.png)

當您開啟 **設定** 對話方塊，您也可以設定：

* **分隔条**
* **文本样式**

格式化文字會顯示在頁面上。 實際設計取決於網站CSS：

![dc_text_use](assets/dc_text_use.png)

如需文字元件和RTF編輯器所提供功能的詳細資訊，請參閱 [RTF編輯器](/help/sites-authoring/rich-text-editor.md) 頁面。

#### 就地編輯 {#inplace-editing}

除了對話方塊式RTF編輯模式外，AEM還提供 [就地編輯](/help/sites-authoring/editing-content.md)，可讓您直接編輯顯示在頁面版面中的文字。

### 文本与图像 {#text-image}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [影像](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html) 和 [文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html) 而非。

文字和影像元件會新增文字區塊和影像。 您也可以分別新增和編輯文字與影像。 請參閱 [文字](#text) 和 [影像](#image) 元件以取得詳細資訊。

![chlimage_1-99](assets/chlimage_1-99.png)

您可以設定：

* **元件樣式** (**樣式**)

   您可以在此向左或向右對齊影像。 預設值為 **左側** 對齊，與左側的影像對齊。

* **影像屬性** (**進階影像屬性**)

   可讓您指定下列專案：

   * **图像资源**

      上傳所需的影像。

   * **标题**

      區塊標題，由mouseover顯示。

   * **替换文本**

      影像無法顯示時所要顯示的替代文字。 如果留空，則使用標題。

   * **链接到**

      指定目標路徑。

   * **描述**

      影像的說明。

   * **大小**

      設定影像的高度和寬度。

下列範例顯示文字影像元件，該元件會以左對齊方式顯示影像：

![dc_textimage_use](assets/dc_textimage_use.png)

### 标题 {#title}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [標題核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) 而非。

標題元件可以：

* 將「標題」欄位保留空白以顯示目前頁面的名稱。
* 顯示您在「標題」欄位中指定的文字。

您可以設定：

* **标题**

   如果您想使用頁面標題以外的名稱，請在此處輸入名稱。

* **链接**

   URI （如果標題要當作連結運作）。

* **类型/大小**

   從下拉式清單中選取「小」或「大」。 「小」會產生為影像。 大型會以文字形式產生。

下列範例顯示 **標題** 顯示的元件；設計由網站特定的CSS決定。

![dc_title_use](assets/dc_title_use.png)

### 视频 {#video}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件內嵌元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html) 而非。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

此 **視訊** 元件可讓您將預先定義的現成視訊元素放置在頁面上。

另請參閱 [設定您的視訊設定檔](/help/sites-administering/config-video.md#configuringvideoprofiles) 與HTML5元素搭配使用。

將元件的例項放在頁面上後，您可以設定下列專案：

* 视频

   * **视频资产**

      上傳或放置您的視訊資產。

   * **大小**

      視訊的原生大小（寬度x高度，以畫素為單位）會顯示在「大小」旁的方塊中（請參閱上文）。 如果您想要覆寫視訊的原生尺寸，請在此手動輸入寬度和高度尺寸。 選取 **確定** 會關閉對話方塊。

>[!NOTE]
>
>支援的格式包括：
>
>* `.mp4`
>* `Ogg`
>* `FLV` (Flash影片)


## 列 {#columns}

欄是控制AEM中內容配置的機制。 在標準安裝中，提供了用於建立兩欄或三欄的元件。

下列範例顯示兩個使用中的Columns元件。 您可以為新元件使用預留位置：

![dc_columncontroluse](assets/dc_columncontroluse.png)

### 2 列 {#columns-1}

預設為兩個相等欄的「欄控制」元件。

### 3 列 {#columns-2}

預設為三個相等欄的「欄控制」元件。

### 列控件 {#column-control}

欄控制元件可讓使用者選擇如何將網頁主面板中的內容分割成多欄。 使用者可以選取所需的欄數（從預先定義的清單中），然後在每個欄中建立、刪除或移動內容。

* **列控件**

   * **列布局**

      選取您要轉譯的欄數。 建立後，每欄都有自己的連結，可在新增內容時拖曳元件或資產。

## 表单 {#form}

>[!CAUTION]
>
>基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

表單元件可用來建立表單，以供訪客提交輸入。 Forms和表單元件可用來收集包含使用者意見回饋（例如客戶滿意度問卷）和使用者資訊（例如使用者註冊）的資訊。

>[!NOTE]
>
>另請參閱 [AEM Forms說明](/help/forms/home.md) 以取得AEM Forms的相關資訊。

Forms由數個不同元件建置：

* **表单**

   表單元件會定義頁面上新表單的開頭和結尾。 其他元件可置於這些元素（例如表格）與下載之間。

* **表單欄位和元素**

   表單欄位和元素可包含文字方塊、選項按鈕和影像。 使用者通常會在表單欄位中完成動作，例如輸入文字。 如需詳細資訊，請參閱個別表單元素。

* **設定檔元件**

   個人資料元件與用於社交合作和需要訪客個人化的其他領域的訪客個人資料相關。

以下顯示範例表單。 它由 **表單** 元件（開始和結束），帶兩個 **表單** **文字** 用於輸入的欄位，a **一般** **文字** 用於潛在客戶輸入文字的欄位和 **提交** 按鈕。

![dc_form](assets/dc_form.png)

>[!NOTE]
>
>開發和自訂表單的相關資訊可在以下網址取得： [開發Forms頁面](/help/sites-developing/developing-forms.md). 此功能包括新增動作、限制、預先載入欄位，以及使用指令碼來呼叫動作服務等。

### （許多）表單元件的通用設定 {#settings-common-to-many-form-components}

雖然每個表單元件的用途不同，但許多表單元件是由類似的選項和引數所組成。

設定任何表單元件時，對話方塊中會顯示下列標籤：

* **标题与文本**

   您必須在此指定基本資訊，例如表單標題及任何隨附文字。 適當時，它也可讓您定義其他關鍵資訊，例如欄位是否可多重選取，以及是否可供選取的專案。

* **初始值**

   可讓您指定預設值。

* **约束**

   您可以在此指定欄位是否為必要欄位，並在該欄位上設定限制（例如，必須為數字）。

* **样式**

   指示欄位的大小和樣式。

>[!NOTE]
>
>您看到的欄位會依個別元件而有很大的差異。

這些標籤會提供您必要的引數。 這些標籤可依個別元件型別而定，但可包括下列內容：

* **标题与文本**

   * **元素名称**

      表單元素的名稱。 它指出資料在存放庫中的儲存位置。
此欄位為必要欄位，僅可包含以下字元：

      * 英數字元
      * `_ . / : -`
   * **标题**

      欄位顯示的標題。 如果保留為空白，則會顯示預設標題。

   * **描述**

      可讓您視需要為使用者提供其他資訊。 在表單上，它會顯示在欄位下方，且字型比標題小。

   * **显示/隐藏**

      決定欄位何時可見。


* **初始值**

   * **默认值**

      開啟表單時顯示在欄位中的值。 也就是說，在使用者進行任何輸入之前。

* **约束**

   * **必填**

      限制取決於表單元件型別，但提供一個或多個按一下方塊來指示此欄位為必要欄位，或此欄位的某些部分為必要欄位。

   * **必需的消息**

      通知使用者此欄位為必填欄位的訊息。 必填欄位也會以星號標幟。

   * **约束**

      可供選取的限制取決於表單元件型別。

   * **约束消息**

      通知使用者所需內容的訊息。

* **样式**

   * **大小**

      列和欄中。

   * **宽度**

      按像素。

   * **CSS**

### 表單（元件） {#form-component}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單容器核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) 而非。

表單元件會使用定義表單的開頭和結尾， **表單開始** 和 **表單結尾** 元素。 起點和終點一律配對，以確保表單已正確定義。

![dc_form-1](assets/dc_form-1.png)

在表單的開頭和結尾之間，您可以新增表單元件，以定義使用者的實際輸入欄位。

>[!NOTE]
>
>基礎元件表單元件僅支援使用其他基礎元件表單元件（按鈕、文字、隱藏等等）。 使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 不支援基礎元件表單中的表單元件（反之）。

#### 表单的开头 {#start-of-form}

此元件會定義頁面上新表單的開頭。 您可以設定：

* **表单**

   * **感谢页面**

      要參照以感謝訪客提供其輸入的頁面。 如果保留為空白，表單會在提交後重新顯示。

   * **启动工作流**

      決定提交表單後觸發的工作流程。

* **高级**

   * **操作类型**

      表單需要動作。 動作會使用使用者提交的資料定義為執行而觸發的操作(類似HTML中的action= )。 有些客戶需要對應的 **動作設定**.
標準AEM安裝包含一系列動作型別：

      * **帐户请求**
      * **创建内容**
      * **创建潜在客户**
      * **创建和更新帐户**
      * **电子邮件服务: 创建订阅者并添加到列表**
      * **电子邮件服务: 发送自动回复的电子邮件**
      * **电子邮件服务: 使用户从列表中取消订阅**
      * **编辑社区**
      * **編輯資源**
      * **編輯工作流程控制的資源**
      * **邮件**
      * **所下的订单明细**
      * **个人资料更新**
      * **重置密码**
      * **设置密码**
      * **存储内容**

         預設動作型別。

      * **透過上傳儲存內容**
      * **提交订单**
      * **取消订阅者的订阅**
      * **更新订单**
   * **表单标识符**

      表單識別碼可唯一識別表單。 如果您在單一頁面上有多個表單，請使用表單識別碼；請確定它們有不同的識別碼。

   * **加载路径**

      節點屬性的路徑，用於將預先定義的值載入表單欄位。

      選擇性欄位，指定存放庫中節點的路徑。 當此節點具有符合欄位名稱的屬性時，則表單上的適當欄位將使用這些屬性的值預先載入。 如果不存在相符專案，則欄位包含預設值。

      使用 **載入路徑** 您可以預先載入包含必填欄位值的表單。 另請參閱 [預先載入表單值](/help/sites-developing/developing-forms.md#preloading-form-values).

   * **客户端验证**

      指出此表單是否需要使用者端驗證（伺服器驗證） *一律* （發生）。 使用者端驗證可透過以下方式達成： **Forms驗證碼** 元件。

   * **验证资源类型**

      如果您想要驗證整個表單（而不是個別欄位），請定義表單驗證資源型別。 如果您要驗證完整的表單，請一併包含下列其中一項：

      * 使用者端驗證的指令碼：

         `/apps/<*myApp*>/form/<*myValidation*>/formclientvalidation.jsp`

      * 伺服器端驗證的指令碼：

         `/apps/<*myApp*>/form/<*myValidation*>/formservervalidation.jsp`
   * **操作配置**

      中可用的選項 **動作設定** 視選取的專案而定 **動作型別**：

      * **帐户请求**

         * **创建帐户页**

            建立帳戶時使用的頁面。
      * **创建内容**

         * 内容路径

            表單傾印的任何內容的內容路徑。 輸入以斜線結尾的路徑 `/`. 斜線表示對於每個表單連線埠，會在指定位置建立新節點；例如：

            `/forms/feedback/`

         * **类型**

            選取所需的型別。

         * **表单**

            指定表單。

         * **呈现工具**

            從清單中選取所需的選項。

         * **资源类型**

            如果設定，則會新增至每個註解作為 `sling:resourceType`

         * **视图选择器**
      * **创建潜在客户**

         * **潛在客戶已新增至此清單**

            指定必要的潛在客戶清單。
      * **创建和更新帐户**

         * **初始的组**

            要指派新使用者的群組。

         * **起始**

            成功登入後顯示的頁面。

         * **路径**

            建立及儲存新帳戶的路徑（相對）。

         * **查看数据...**

            選取此按鈕可存取「大量編輯器」中有關表單結果的資訊。 從這裡，您可以將資訊匯出至 `.tsv` （以Tab分隔）檔案（例如用於Excel試算表）。
      * **邮件**

         * **发件人**

            輸入電子郵件的來源電子郵件地址。

         * **发送到**

            輸入一或多個傳送表單的電子郵件地址。

         * **抄送**

            輸入一或多個CC電子郵件地址。

         * **BCC**

            輸入一或多個密件副本電子郵件地址。

         * **主题**

            輸入電子郵件的主旨。
      * **重置密码**

         * **更改密码页**

            變更密碼時使用的頁面。
      * **存储内容**

         * **内容路径**

            表單傾印的任何內容的內容路徑。 輸入以斜線結尾的路徑 `/`. 斜線表示對於每個表單連線埠，會在指定位置建立新節點；例如：
            `/forms/feedback/`

         * **查看数据...**

            按一下此按鈕，即可在「大量編輯器」中存取有關表單結果的資訊。 從這裡，您可以將資訊匯出至.tsv （以Tab分隔）檔案（例如用於Excel試算表）。
      * **通过上传存储内容**

         具有與相同的選項 **存放區內容**.

      * **取消订阅者的订阅**

         * **銷售機會已從此清單中刪除**

            指定必要的潛在客戶清單。










#### 表单结尾 {#end-of-form}

標籤表單的結尾。 您可以設定下列專案：

* **表单结尾**

   * **显示提交按钮**

      指示是否應該顯示提交按鈕。

   * **提交名**

      識別碼（如果您在表單中使用多個提交按鈕）。

   * **提交标题**

      按鈕上顯示的名稱，例如「提交」或「傳送」。

   * **显示重设按钮**

      選取此核取方塊可顯示「重設」按鈕。

   * **重置标题**

      顯示在[重設]按鈕上的名稱。

   * **描述**

      顯示在按鈕下方的資訊。

### 帐户名称 {#account-name}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) 而非。

讓使用者輸入帳戶名稱：

![dc_form_accountname](assets/dc_form_accountname.png)

### 地址 {#address}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) 而非。

可讓您新增具有以下格式的國際位址列位：

![dc_form_addressfield](assets/dc_form_addressfield.png)

元件已設定為立即使用，但您可以視需要變更設定。 例如，可以為地址的個別元素新增限制。 將欄位留空表示使用預設設定。

### 验证码 {#captcha}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

>[!CAUTION]
>
>若無廣泛的專案層級自訂，此元件就不能再立即運作。

Captcha元件會要求使用者輸入熒幕上顯示的英數字串。 字串會隨著每次重新整理而變更。

![dc_form_captcha](assets/dc_form_captcha.png)

您可以為此元件設定各種引數，包括驗證碼字串無效時顯示的訊息。

### 复选框组 {#checkbox-group}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單選項核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) 而非。

核取方塊可讓您建立一個或多個核取方塊的清單，其中多個核取方塊可同時選取。

![dc_form_checkboxgroupuse](assets/dc_form_checkboxgroupuse.png)

您可以指定各種引數，包括標題、說明和元素名稱。 您可以使用+和 — 按鈕來新增或移除專案，然後使用向上和向下箭頭來放置它們。

>[!NOTE]
>
>使用 **專案載入路徑** 您可以使用值預先載入核取方塊群組清單。
>
>另請參閱 [預先載入具有多個值的表單欄位](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### 信用卡详细信息 {#credit-card-details}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

可讓您提供輸入信用卡詳細資料所需的欄位。 您可以將其設定為指定接受的卡片型別和所需的資訊（例如安全碼）。

![chlimage_1-100](assets/chlimage_1-100.png)

### 下拉列表 {#dropdown-list}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單選項核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) 而非。

下拉式清單可設定為您提供一系列的值供您選取：

![dc_form_dropdownlistuse](assets/dc_form_dropdownlistuse.png)

您可以指定要顯示在清單中的標題和專案。 使用+和 — 按鈕可以新增或移除清單專案，然後使用向上和向下按鈕來定位它們。 您可以指定是否允許使用者從清單中選取數個專案，以及在第一次開啟清單時應該自動選取的任何專案（初始值）。

>[!NOTE]
>
>使用 **專案載入路徑** 您可以使用值預先載入下拉式清單。
>
>另請參閱 [預先載入具有多個值的表單欄位](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### 文件上传 {#file-upload}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

檔案上傳元件為使用者提供了一種選擇和上傳檔案的機制。

![dc_form_fileupload](assets/dc_form_fileupload.png)

>[!NOTE]
>
>您可以建立自訂上傳元件以將檔案上傳到Sling Servlet。 如需詳細資訊，請參閱 [將檔案上傳至Adobe Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-cloud-service-create-asset-servlet-for-uploading-small-files/td-p/404276).

### 隐藏字段 {#hidden-field}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單隱藏核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-hidden.html) 而非。

可讓您建立隱藏欄位。 這些隱藏欄位可用於各種用途。 例如，在提交表單後必須執行動作，或在後處理中需要隱藏資料時。

![dc_form_hiddenfield](assets/dc_form_hiddenfield.png)

>[!NOTE]
>
>您也可以根據表單中其他欄位的值，自訂表單以顯示或隱藏特定表單元件。 只有在特定條件下才需要表單欄位時，變更欄位的可見度會很有用。
>
>另請參閱 [顯示和隱藏表單元件](/help/sites-developing/developing-forms.md#showing-and-hiding-form-components).

### 图像按钮 {#image-button}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單按鈕核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) 而非。

影像按鈕可讓您使用自己的影像和文字建立按鈕：

![dc_form_imagebutton](assets/dc_form_imagebutton.png)

### 图像上传 {#image-upload}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

影像上傳元件為使用者提供選擇和上傳影像檔案的機制。

![dc_form_imageupload](assets/dc_form_imageupload.png)

### 链接字段 {#link-field}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

連結欄位可讓使用者指定URL：

![dc_form_link](assets/dc_form_link.png)

最常用於日曆事件表單，其中用於事件的URL/連結欄位。

### 密码字段 {#password-field}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

允許使用者輸入密碼：

![dc_form_password](assets/dc_form_password.png)

### 密码重置 {#password-reset}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

此元件提供使用者以下兩個欄位：

* 密碼的輸入
* 重複輸入密碼以檢查輸入內容是否正確。

使用預設設定時，元件會顯示如下：

![dc_password_reset](assets/dc_password_reset.png)

### 单选按钮组 {#radio-group}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單選項核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-options.html) 而非。

選項群組會提供您多個選項核取方塊的清單，您只可以在任何特定時間選取其中一個選項核取方塊。

您可以指定元素名稱以及標題和說明。 您可以使用+和 — 按鈕來新增或移除專案、使用向上和向下箭頭來放置專案，以及指定預設值（如有必要）：

![dc_form_radiogroupuse](assets/dc_form_radiogroupuse.png)

>[!NOTE]
>
>使用 **專案載入路徑** 您可以使用值預先載入選項群組。
>
>另請參閱 [預先載入具有多個值的表單欄位](/help/sites-developing/developing-forms.md#preloading-form-fields-with-multiple-values).

### “提交”按钮 {#submit-button}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單按鈕核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) 而非。

此元件可讓您建立具有預設文字的提交按鈕：

![dc_form_submitbutton](assets/dc_form_submitbutton.png)

或是使用您自己的文字：

![dc_form_submitbuttonuse](assets/dc_form_submitbuttonuse.png)

### 标记字段 {#tags-field}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 而非。

此欄位可讓您選取標籤：

![dc_form_tags_use](assets/dc_form_tags_use.png)

您可以使用專用標籤來指定各種引數，包括可以使用的名稱空間：

* **标记字段**

   * **允许的命名空间**

      * **Geometrixx Outdoors**
      * **工作流**
      * **论坛**
      * **Stock Photography**
      * **Geometrixx Media**
      * **标准标记**
      * **行銷**
      * **资产属性**
      * **以像素为单位的宽度**
      * **弹出窗口大小**

### 文本字段 {#text-field}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單文字核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-text.html) 而非。

標準文字欄位可設定為您所需的大小，並在訊息中擁有您自己的銷售機會：

![dc_form_text](assets/dc_form_text.png)

### 工作流提交按钮 {#workflow-submit-button-s}

>[!CAUTION]
>
>此基礎元件已過時。 Adobe建議使用 [表單按鈕核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-button.html) 而非。

可讓您建立「提交」按鈕以用於工作流程。

![chlimage_1-101](assets/chlimage_1-101.png)
