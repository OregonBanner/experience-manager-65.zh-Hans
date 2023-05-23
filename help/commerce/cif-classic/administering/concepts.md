---
title: 概念
description: 使用AEM的電子商務一般概念。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '4514'
ht-degree: 1%

---

# 概念{#concepts}

整合架構提供以下用途的機制和元件：

* 電子商務引擎的連線
* 將資料提取至AEM
* 顯示該資料並收集購物者的回應
* 傳回交易詳細資料
* 搜尋來自兩個系統的資料

这意味着：

* 購物者無需等待即可註冊及購物。
* 消費者將會立即看到價格變更。
* 產品可依需求新增。

>[!NOTE]
>
>電子商務架構可搭配下列專案使用：
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAPCOMMERCE CLOUD](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
>


>[!CAUTION]
>
>此 [電子商務整合框架](https://www.adobe.com/solutions/web-experience-management/commerce.html) 是AEM附加元件。
>
>您的銷售代表將能根據適當的引擎提供完整詳細資訊。

>[!CAUTION]
>
>此架構提供您專案的基本需求。
>
>一律需要一定的開發工作，才能讓架構符合您的規格。

>[!CAUTION]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>這目前僅供示範之用，或根據您的需求作為自訂實作的基本基礎。

為了最佳化營運，AEM和電子商務引擎都專注於各自的專業領域。 資訊會即時在兩者之間傳送；例如：

* AEM可以：

   * 要求：

      * 電子商務引擎的產品資訊。
   * 提供：

      * 使用者檢視產品資訊、購物車和結帳。
      * 購物車和結帳資訊至電子商務引擎。
      * 搜尋引擎最佳化(SEO)。
      * 社群功能。
      * 非結構化行銷互動。


* 電子商務引擎可以：

   * 提供：

      * 資料庫中的產品資訊。
      * 產品變體管理。
      * 訂單管理。
      * ERP （企業資源規劃）。
      * 搜尋產品資訊。
   * 进程:

      * 購物車。
      * 結帳。
      * 訂單履行。


>[!NOTE]
>
>確切的詳細資訊將取決於電子商務引擎和專案實施。

許多現成的AEM元件可供使用整合層。 目前包括：

* 產品資訊
* 購物車
* 簽出
* 我的帐户

您也可以使用各種搜尋選項。

## 架构 {#architecture}

整合框架提供API、一系列元件來說明功能，而數個擴充功能則提供連線方法的範例：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

此框架可讓您存取以下功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 實作 {#implementations}

AEM電子商務是使用電子商務引擎實作：

* 電子商務整合架構的建置可讓您輕鬆地將電子商務引擎與AEM整合。 專門建立的電子商務引擎可控制產品資料、購物車、結帳和訂單履行，而AEM則可控制資料顯示和行銷活動。


>[!NOTE]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>這目前僅供示範之用，或根據您的需求作為自訂實作的基本基礎。
>
>使用以JCR為基礎的一般開發在AEM內實作的AEM電子商務是：
>
>* 獨立AEM原生電子商務範例，說明如何使用API。 結合現有的資料顯示和行銷活動，可用於控制產品資料、購物車和結帳。 在此情況下，產品資料庫會儲存在AEM原生存放庫中(Adobe的 [JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))。
>
>  標準AEM安裝包含 [通用電子商務實施](/help/commerce/cif-classic/administering/generic.md).

### 商務提供者 {#commerce-providers}

將資料從商務引擎匯入您的AEM電子商務網站時，會使用商務提供者為匯入者提供資料。 一個商務提供者可支援多個匯入工具。

商務提供者是AEM程式碼，自訂為：

* 後端商務引擎的介面
* 在JCR存放庫上實作商業系統

AEM目前提供兩個範例商務提供者：

* 一個用於geometrixx-hybris
* geometrixx-generic (JCR)的另一個

雖然通常專案將需要開發自己的、自訂的、特定於其PIM和產品資料結構描述的商務提供者。

>[!NOTE]
>
>geometrixx匯入工具使用CSV檔案；其實作上方的註解中有接受的結構描述（允許自訂屬性）。

此 [產品服務管理員](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 維護(透過 [osgi](/help/sites-deploying/configuring.md#osgi-configuration-settings))的實作清單  [產品匯入工具](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 和 [CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 介面。 這些專案會列於 **匯入工具/商務提供者** 匯入工具精靈的下拉式清單欄位(使用 `commerceProvider` 屬性作為名稱)。

當下拉式清單中提供特定的匯入工具/商務提供者時，您必須在以下任一項中定義所需的任何補充資料（視匯入工具型別而定）：

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

適當底下的資料夾 `importers` 資料夾必須與匯入工具名稱相符；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

來源匯入檔案的格式由匯入工具定義。 或者，匯入工具可能會建立與商務引擎的連線（例如WebDAV或http）。

## 角色 {#roles}

整合的系統會針對下列角色來維護資料：

* 維護下列專案的產品資訊管理(PIM)使用者：

   * 產品資訊。
   * 分類、分類、核准。
   * 與數位資產管理互動。
   * 定價 — 通常來自ERP系統，商業系統不會明確維護此價格。

* 維護下列專案的作者/行銷經理：

   * 所有管道的行銷內容。
   * 促销活动.
   * 优惠券.
   * 营销活动.

* 瀏覽網路者/購物者：

   * 檢視您的產品資訊。
   * 將專案放入購物車。
   * 檢查他們的訂單。
   * 預期訂單履行。

雖然實際位置可能會視您的實作而定；例如，通用或使用電子商務引擎：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 产品 {#products}

### 產品資料與行銷資料的比較 {#product-data-versus-marketing-data}

#### 結構性與行銷類別 {#structural-versus-marketing-categories}

如果您可以區分以下兩個類別，這可讓您以有意義的結構來清除URL (樹狀結構： `cq:Page` 節點)，因此非常接近經典的AEM內容管理)：

* *結構*類別

   類別樹狀結構定義 *什麼是產品*；例如：

   `/products/mens/shoes/sneakers`

* *行銷* 類別

   所有其他類別a *產品可屬於*；例如：

   `/special-offers/christmas/shoes`)

### 产品数据 {#product-data}

為了描繪和管理您的產品，您需要儲存一系列關於它們的資訊。

產品資料可以是：

* 直接在AEM中維護（一般）。
* 在電子商務引擎中維護，並可在AEM中使用。

   視資料型別而定 [已同步](#catalog-maintenance-data-synchronization) 如有需要，或直接存取；例如，產品價格等極不穩定且重要的資料會從每個頁面請求的電子商務引擎中擷取，以確保這些資料隨時保持最新。

無論是哪種情況，當產品資料已輸入/匯入AEM時，都可以從 **產品** 主控台。 在此處，產品的卡片和清單檢視會顯示資訊，例如：

* 影像
* SKU程式碼
* 上次修改時間

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 产品的系列品种 {#product-variants}

如需適當的產品資訊，也可以儲存變體的相關資訊。 例如，對於服裝專案，可用的不同顏色會以變體形式持有：

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 產品屬性 {#product-attributes}

各產品的個別屬性可能取決於所使用的電子商務引擎和您的AEM實作。 檢視產品頁面和/或編輯產品資訊時，這些選項都可（視情況而定）使用，可能包括：

* **图像**

   產品的影像。

* **标题**

   產品名稱。

* **描述**

   產品的文字說明。

* **标记**

   用於對相關產品進行分組的標籤。

* **預設資產類別**

   資產的預設類別。

* **ERP 数据**

   企業資源規劃(ERP)資訊。

   * **SKU**

      庫存單位(SKU)資訊。

   * **颜色**
   * **大小**
   * **价格**

      產品的單價。

* **摘要**

   產品功能摘要。

* **功能**

   更完整的產品功能細節。

### 產品資產 {#product-assets}

可以為個別產品保留一系列資產。 通常包括影像和影片。

## 目錄 {#catalogs}

目錄會將產品資料分組在一起，既方便管理，又能向購物者呈現。 目錄通常會根據語言、地理區域、品牌、季節、愛好、運動等屬性來建構。

### 目錄結構 {#catalog-structure}

#### 多國語言的目錄 {#catalogs-in-multiple-languages}

AEM支援多種語言的產品內容。 請求資料時，整合架構會從目前的樹狀結構中擷取語言(例如 `en_US` 對於底下的頁面 `/content/geometrixx-outdoors/en_US`)。

對於多語言存放區，您可以個別匯入每個語言樹狀結構的目錄（或透過以下方式複製） [MSM](/help/sites-administering/msm.md))。

#### 多個品牌的目錄 {#catalogs-for-multiple-brands}

與語言一樣，大型跨國企業可能需要滿足多個品牌的需求。

#### 依標籤的目錄 {#catalogs-by-tags}

標籤也可用來將產品分組到目錄中。 這些可用於更具活力的目錄，例如季節性優惠。

### 目錄設定（初始匯入） {#catalog-setup-initial-import}

根據您的實作，您可以從下列位置將基礎目錄所需的產品資料匯入AEM：

* CSV檔案（用於一般實作）
* 電子商務引擎

### 目錄維護（資料同步） {#catalog-maintenance-data-synchronization}

產品資料的進一步變更將不可避免：

* 對於一般實作，這些可透過 [產品編輯器](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* 使用 [電子商務引擎必須同步變更](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 與電子商務引擎進行資料同步（進行中） {#data-synchronization-with-an-ecommerce-engine-ongoing}

首次匯入後，您的產品資料不可避免地會變更。

使用電子商務引擎時，會在該處維護產品資料，而且需要可在AEM中使用。 進行更新時，需要同步處理此產品資料。

這可能取決於資料型別：

* A [定期同步會與變更的資料摘要一起使用](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

   除此之外，您還可以為快速更新選取特定更新。

* 系統會從商業引擎為每個頁面請求擷取高度不穩定的資料（例如價格資訊），以確保其隨時保持最新狀態。

### 目錄 — 效能與擴充能力 {#catalogs-performance-and-scaling}

從電子商務引擎(PIM)匯入含有大量產品（通常超過100,000）的大型目錄時，由於節點數量龐大，可能會影響系統。 如果產品有關聯資產（例如產品影像），也可能會減慢編寫執行個體的速度。 這是因為這些資產的後處理需要密集CPU和記憶體。

您可選擇使用多種策略來解決這些問題：

* [分段](#bucketing)  — 滿足大量節點的需求
* [將資產後處理解除安裝到專用執行個體](#offload-asset-post-processing-to-a-dedicated-instance)
* [僅匯入產品資料](#only-import-product-data)
* [匯入節流和批次儲存](#import-throttling-and-batch-saves)
* [性能测试](#performance-testing)
* [績效 — 其他](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR節點有許多直接子節點（例如1000個以上），則需要貯體（虛擬資料夾），以確保效能不受影響。 匯入時會根據演演算法產生這些值。

這些貯體採用引入目錄結構的虛擬資料夾形式，但可以設定為在公共URL中不明顯。

#### 將資產後處理解除安裝到專用執行個體 {#offload-asset-post-processing-to-a-dedicated-instance}

此情境涉及設定兩個作者執行個體：

1. 主要作者執行個體

   從已停用資產路徑後續處理的PIM匯入產品資料。

1. 專用DAM作者執行個體

   從PIM匯入產品資產並進行後續處理，然後將這些資產復寫回主要製作執行個體以供使用。

![架構圖](/help/sites-administering/assets/chlimage_1-8.png)

#### 僅匯入產品資料 {#only-import-product-data}

如果產品不包含要匯入的資產（影像），您可以匯入產品資料而不受資產後處理的影響。

![架構圖](/help/sites-administering/assets/chlimage_1-9.png)

#### 性能测试 {#performance-testing}

必須在AEM電子商務實作上考量效能測試：

* 作者環境：

   背景（例如匯入）活動可能會與一般使用者活動（例如頁面編輯）同時發生，而且即使前端效能（通常）被指定較高優先順序，線上作者看到的效能不佳也會導致無法封鎖上線決定的挫折。

* 發佈環境：

   復寫是確保內容快速可靠地發佈的關鍵程式。 這可能受到作者如何分組要發佈的內容所影響。

* 前端：

   前端和快取無效混合使用可能導致效能出乎意料。 測試有助於避免這些問題。

請注意，此效能測試需要您目標的知識和分析：

* 內容量

   * Assets
   * 本地化、I18ned產品和SKU

* 使用者活動：

   * 大量版本
   * 大量發佈
   * 大量搜尋請求

* 背景程式

   * 匯入
   * 同步處理更新（例如定價）

* 維護需求（備份、Tar PM最佳化、資料存放區垃圾收集等）

#### 績效 — 其他 {#performance-miscellaneous}

對於所有實作，請謹記以下幾點：

* 由於產品、庫存單位和類別可能會很多，請嘗試使用儘可能少的節點數來建立內容模型。

   節點越多，內容就越有彈性（例如parsys）。 不過，一切都是權衡取捨，您在操作（例如）30,000種產品時，是否需要個別的彈性（依預設）？

* 儘可能避免重複（請參閱本地化），或在您這樣做時，考慮您的重複會產生多少節點。
* 請儘量標籤您的內容，以準備查詢最佳化。

   例如：

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   每個內容層級（即國家、語言、類別、品牌、產品）應有一個標籤。 正在搜尋

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   和

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   會比搜尋快很多

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技術棧疊中，規劃非常分解的內容存取模式與服務。 此為一般最佳實務，但更重要的是，因為您可以在最佳化階段為經常讀取（且您不想使用填滿套件快取的）資料新增應用程式快取。

   例如，屬性管理經常是快取的良好候選者，因為它與透過產品匯入更新的資料有關。
* 考慮使用 [proxy頁面](#proxy-pages).

### 目錄區段頁面 {#catalog-section-pages}

例如，目錄區段會提供您下列資訊：

* 類別簡介（影像和/或文字）；這也可以用於橫幅和Teaser以促銷特殊優惠方案
* 該類別中個別產品的連結
* 其他類別的連結

![eCommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 产品页面 {#product-pages}

產品頁面提供個別產品的完整資訊。 來自的動態更新也會反映出來；例如，在電子商務引擎上註冊的價格變更。

AEM產品頁面為使用 **產品** 元件；例如， **商業產品** 範本：

![e-commerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

「產品」元件提供：

* 一般產品資訊；包括文字和影像。
* 定價；這通常會在每次顯示/重新整理頁面時從電子商務引擎擷取。
* 產品變體資訊；例如，顏色和大小。

此資訊可讓購物者在將專案新增至購物籃時選取下列專案：

* 顏色和大小變數
* 数量

#### 產品登陸頁面 {#product-landing-pages}

這些主要是提供靜態資訊的AEM頁面；例如，包含基礎產品頁面連結的簡介和概觀。

### 产品组件 {#product-component}

此 **產品** 元件可新增至任何具有提供所需中繼資料(亦即 `cartPage` 和 `cartObject`)。 在示範網站Geometrixx Outdoors中，這由以下提供 `UserInfo.jsp`.

此 **產品** 您也可以根據個別需求自訂元件。

### Proxy頁面 {#proxy-pages}

Proxy頁面可用來簡化存放庫結構，以及最佳化大型目錄的儲存空間。

建立目錄時，每個產品將使用10個節點，因為每個產品都有個別的元件，您可以在AEM中更新和自訂。 如果您的目錄包含數百甚至數千種產品，那麼如此大量的節點可能會成為一個問題。 若要避免任何問題，您可以使用Proxy頁面建立目錄。

Proxy頁面使用雙節點結構( `cq:Page` 和 `jcr:content`)，不包含任何實際產品內容。 內容是在請求時透過參考產品資料和範本頁面產生的。

不過，還是需要權衡取捨。 您將無法在AEM內自訂您的產品資訊，將使用標準範本（為您的網站定義）。

>[!NOTE]
>
>如果您匯入沒有Proxy頁面的大型目錄，則不會遇到任何問題。
>
>您可以隨時從一種方法轉換為另一種方法。 您也可以轉換目錄的子區段。

## 促銷活動和憑單 {#promotions-and-vouchers}

### 优惠券 {#vouchers}

憑單是經過驗證和測試的提供折扣方法，可吸引購物者進行購買和/或獎勵客戶的忠誠度。

* 憑單供應：

   * 憑單代碼（由購物者輸入購物車中）。
   * 憑單標籤（在購物者將其輸入購物車後顯示）。
   * 促銷活動路徑（定義憑單套用的動作）。

* 外部商務引擎也可以提供憑單。

在AEM中：

* 憑單是使用「網站」主控台建立/編輯的頁面型元件。
* 此 **憑單** 元件提供：

   * 憑單管理的轉譯器；這會顯示目前購物車中的任何憑單。
   * 用於管理（新增/移除）憑單的編輯對話方塊（表單）。
   * 在購物車中新增/移除憑單所需的動作。

* 憑單沒有自己的開啟和結束日期/時間，但會使用其父行銷活動的日期/時間。

>[!NOTE]
>
>AEM使用術語 **憑單**，這是辭彙的同義詞 **抵用券**.

### 促销活动 {#promotions}

促銷活動與憑單一起，可讓您實現以下情況：

* 公司為員工提供自訂價格，這是一份手工製作的使用者清單。
* 長期客戶會收到所有訂單的折扣。
* 在明確定義的時間段內提供的銷售價格。
* 當客戶先前的訂單超過特定金額時，客戶會收到憑單。
* 購買產品的客戶 *product-X* 折扣為： *product-Y* （配對產品）。

促銷活動通常不是由產品資訊管理員維護，而是由行銷管理員維護：

* 促銷活動是使用「網站」主控台建立/編輯的頁面型元件。 &quot;
* 促銷活動提供：

   * 優先順序
   * 推進處理常式路徑

* 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
* 您可以將促銷活動連結至體驗，以定義其區段。
* 未連線至體驗的促銷活動不會自行引發，但仍可由憑單引發。
* 「推進」元件包含：

   * 推進管理的轉譯器和對話方塊
   * 用於呈現和編輯升級處理常式專屬設定引數的子元件

在AEM中，促銷活動也會整合至 [Campaign Management](/help/sites-authoring/personalization.md)：

* a [行銷活動](/help/sites-authoring/personalization.md) 指定開啟/關閉時間
* [體驗](/help/sites-authoring/personalization.md) *範圍* 行銷活動用於根據資產（Teaserpages、促銷活動等）對應的受眾區段來分組資產

促銷活動可在體驗中或直接在行銷活動中進行：

* 如果促銷活動在體驗中進行，則會自動套用至對象區段。

   例如，在geometrixx-outdoors範例網站中，促銷活動：

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   位在體驗中，因此每當區段( `ordervalueover100`)解析。

* 如果促銷活動未出現在體驗中（僅在行銷活動中），則無法自動套用至對象。 但是，如果購物者在其購物車中輸入憑單，且該憑單參考促銷活動，則仍可觸發此訊息。

   例如，促銷活動：

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   位於體驗外部，因此絕不會自動引發（即：根據分段）。 不過，可在文章行銷活動內的數個體驗中找到的憑單會參考此內容。 將這些憑單代碼輸入購物車將導致促銷活動觸發。

>[!NOTE]
>
>[hybris促銷活動](https://www.hybris.com/modules/promotion) 和 [hybris憑單](https://www.hybris.com/en/modules/voucher) 涵蓋影響購物車及與定價相關的所有專案。 促銷特定行銷內容（例如橫幅等）不是Hybris促銷活動的一部分。

## 个性化 {#personalization}

### 客戶註冊與帳戶 {#customer-registration-and-accounts}

當購物者註冊時，帳戶詳細資料需要在AEM和電子商務引擎之間同步。 敏感資料會獨立儲存，但會共用設定檔：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

確切的機製取決於以下情況：

1. 使用者帳戶存在於兩個系統中：

   1. 不需要採取任何動作。

1. 使用者帳戶僅存在於AEM中：

   1. 系統會在電子商務引擎中建立使用者，並使用相同的帳戶ID和隨機密碼(將儲存於AEM)。
   1. AEM在第一次呼叫時會嘗試登入電子商務引擎（例如，要求產品頁面且價格參考電子商務引擎時），因此隨機密碼是必要的。 由於這會在AEM登入後發生，因此密碼無法使用。

1. 使用者帳戶僅存在於電子商務引擎中：

   1. 該帳戶將使用相同的帳戶ID和密碼在AEM中建立。

使用電子商務引擎時，AEM只會儲存帳戶ID和密碼（可選擇性地儲存使用者群組）。 所有其他資訊都會儲存在電子商務引擎中。

>[!NOTE]
>
>使用電子商務引擎時，您必須確保將為登入AEM執行個體之使用者建立的帳戶，會複製（例如透過工作流程）至與該引擎通訊的任何其他AEM執行個體。
>
>否則，這些其他AEM執行個體也會嘗試為引擎中的相同使用者建立帳戶。 這些動作會失敗，並會 `DuplicateUidException` 來自引擎。

### 客戶註冊 {#customer-sign-up}

通常需要註冊才能讓購物者存取購物車。 這需要註冊（建立帳戶），以便建立客戶特定的帳戶。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>也支援匿名購物車和結帳。

### 客戶登入 {#customer-sign-in}

註冊後，購物者可以使用帳戶登入，以便可以追蹤他們的動作並完成他們的訂單。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 單一登入 {#single-sign-on}

提供單一登入(SSO)，讓作者在AEM和電子商務系統中皆為人所知，不需登入兩次。

### myAccount {#myaccount}

來自電子商務引擎的交易資料會與購物者的個人資訊結合。 AEM會將部分資料用作設定檔資料。 表單在AEM中的動作會將資訊寫回電子商務引擎。

有一個頁面可讓您輕鬆管理帳戶資訊。 您可以按一下以存取它 **我的帳戶** ，或導覽至「 」頁面 `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通讯簿 {#address-book}

您的網站將需要儲存一系列地址；包括傳送、帳單和替代地址。 您可以使用根據預設地址格式的表單來實作此功能，也可以使用AEM提供的通訊錄元件。

此通訊錄元件可讓您：

* 編輯報表簿中的地址
* 從出貨地址簿中選取一個地址
* 從帳本中選取帳單地址的地址

您可以選擇預設地址。

通訊錄元件可從 **我的帳戶** 按一下以建立頁面 **通訊錄** 或透過導覽至 `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

您可以按一下 **新增地址……** 以新增通訊錄中的地址。 它會開啟一個您可以填寫的表單，然後按一下 **新增地址**.

>[!NOTE]
>
>您可以在通訊錄中輸入多個地址。

在您結帳購物車時會使用通訊錄：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

位址持續存在下方 `user_home/profile/addresses`.
例如，對於Alison Parker，其會位於/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以選擇想要哪個地址作為預設地址，此資訊會保留在購物者的設定檔中，而不是地址中。 設定檔屬性 `address.default` 以選取之值的位址的路徑設定。

### 客戶特定定價 {#customer-specific-pricing}

電子商務引擎會使用內容（主要是購物者資訊）來決定價格，然後向AEM提供正確的資訊。

## 購物車與訂單 {#shopping-cart-and-orders}

購物時，購物者會瀏覽產品頁面並選取專案，以將他們放入購物車中。 當他們繼續結帳時，可以下訂單。

### 匿名購物者 {#anonymous-shoppers}

匿名客戶可以：

* 檢視產品
* 將產品新增至購物車
* 執行結帳以下訂單

>[!NOTE]
>
>根據您執行個體位址資訊的設定，或客戶註冊可能會在結帳前需要。

### 註冊購物者 {#registered-shoppers}

註冊客戶可以：

* 登入其帳戶
* 檢視產品
* 將產品新增至購物車
* 執行結帳以下訂單
* 檢視及追蹤先前的訂單

### 購物車內容概觀 {#shopping-cart-content-overview}

購物車提供：

* 所選專案的概觀
* 所選專案的產品頁面連結
* 具備以下功能：

   * 更新個別料號的數目/數量
   * 移除個別專案

![e-commerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

購物車會根據使用的引擎儲存：

* AEM generic會將購物車儲存在Cookie中。
* 某些電子商務引擎可將購物車儲存在工作階段中。

無論哪種情況，專案都會在登入/登出期間保留在購物車中（且可以還原） （但僅限於同一部電腦/瀏覽器上）。 例如：

* 瀏覽身份 `anonymous` 並將產品新增至購物車
* 登入身份 `Allison Parker`  — 她的購物車是空的
* 新增產品至購物車
* 登出 — 購物車將顯示產品 `anonymous`

* 再次登入身份 `Allison Parker`  — 她的產品已還原

>[!NOTE]
>
>匿名購物車只能在相同的電腦/瀏覽器上還原。

>[!NOTE]
>
>不建議使用測試還原購物車內容 `admin` 帳戶，因為這可能會與 `admin` 電子商務引擎的帳戶（例如hybris）。

>[!NOTE]
>
>hybris可設定為在定義的時間段後移除擱置中的購物車。

結帳前，價格變更會在發生時反映在（兩個系統）中。

### 訂單資訊 {#order-information}

根據您有關訂單的實作資訊儲存在電子商務引擎或AEM中，此資訊會由AEM呈現。

會儲存各種資訊，其中可能包括：

* **订单 ID**

   訂單的參考編號。

* **订购时间**

   下訂單的日期。

* **状态**

   訂單的狀態；例如，已出貨。

* **货币**

   訂單的貨幣。

* **內容專案**

   排序的專案清單。

* **小计**

   訂購料號的總成本。

* **税费**

   訂單上任何應付稅款的金額。

* **运费**

   運費。

* **总计**

   訂單的總值；訂購的專案、稅金和折扣。

* **帐单地址**

   商業發票應傳送的地址。

* **付款标记**

   付款方式。

* **付款状态**

   付款的狀態。

* **配送地址**

   貨品應運往的地址。

* **配送方式**

   出貨方法；例如，陸路、海上或空中。

* **跟踪号**

   送貨公司使用的任何追蹤號碼。

* **跟踪链接**

   此連結用於在出貨時追蹤訂單。

>[!NOTE]
>
>建立訂單精靈中使用的欄位取決於為位置定義的觸控最佳化支架。 在一般範例中，這可在下列位置找到：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM中保留訂單時，「訂單」主控台會針對每個訂單顯示下列內容：

* 購物車中的專案數
* 訂單的總值
* 下訂單的時間
* 狀態

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 訂單追蹤 {#order-tracking}

下訂單後，購物者通常會返回：

* 檢查其訂單的狀態
* 從訂單中移除產品
* 新增產品至訂單

收到訂單遞送後，購物者可能也想要檢視一段時間內所訂購的訂單歷史記錄。

訂單履行與追蹤通常由電子商務引擎管理。 AEM可以使用「訂單歷史記錄」元件來顯示資訊，該元件會顯示所有相關細節，包括套用的憑單和促銷活動。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 签出 {#checkout}

使用標準AEM表單實作結帳。 這可讓行銷經理使用行銷內容自訂體驗。

電子商務接著會使用AEM表單的輸入來管理結帳程式。

### 付款安全性 {#payment-security}

付款詳細資料（包括信用卡資訊）通常由電子商務引擎管理。 AEM將這類交易資訊轉送至引擎（再從此處轉送至付款處理服務）。

可符合支付卡產業(PCI)規範。

### 訂單確認 {#confirmation-of-order}

此訂單已在畫面上確認，並可透過以下方式追蹤： [訂單追蹤](#order-tracking).

## 搜索 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由於AEM對產品使用標準頁面，因此您可以使用標準搜尋元件來建立搜尋頁面。

如果您需要更徹底的實作，您可以：

* 使用您需要的功能擴充預設搜尋元件。
* 在您的中實作搜尋方法 `CommerceService` 然後使用搜尋頁面上的電子商務搜尋元件。

使用電子商務引擎時，電子商務搜尋API可以在電子商務引擎解決方案中完全實作，因此您可以使用現成提供的電子商務搜尋元件。 多面向搜尋可讓您搜尋JCR和/或引擎：
