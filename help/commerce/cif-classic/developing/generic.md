---
title: 開發（一般）
seo-title: Developing (generic)
description: 整合架構包含具有API的整合層，可讓您為電子商務功能建置AEM元件
seo-description: The integration framework includes an integration layer with an API, allowing you to build AEM components for eCommerce capabilities
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---

# 開發（一般）{#developing-generic}

>[!NOTE]
>
>[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供使用。

整合架構包含具有API的整合層。 這可讓您為電子商務功能建置AEM元件（不受特定電子商務引擎影響）。 它也可讓您使用內部CRX資料庫或插入電子商務系統，並將產品資料提取到AEM。

許多現成的AEM元件可供使用整合層。 目前包括：

* 產品顯示元件
* 購物車
* 促銷活動和憑單
* 目錄和章節藍圖
* 簽出
* 搜索

對於搜尋，提供的整合鉤子可讓您使用AEM搜尋、第三方搜尋或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務架構可搭配任何電子商務解決方案使用，使用的引擎需由AEM識別 — 即使使用AEM通用引擎亦然：

* 電子商務引擎是支援 `CommerceService` 介面

   * 引擎的辨別方法如下： `commerceProvider` 服務屬性

* AEM支援 `Resource.adaptTo()` 的 `CommerceService` 和 `Product`

   * 此 `adaptTo` 實施會尋找 `cq:commerceProvider` 資源階層中的屬性：

      * 如果找到，則會使用值來篩選商務服務查閱。
      * 如果找不到，則會使用排名最高的商務服務。
   * A `cq:Commerce` mixin用於 `cq:commerceProvider` 可新增至強型別資源。


* 此 `cq:commerceProvider` 屬性也可用來參考適當的商務工廠定義。

   * 例如， `cq:commerceProvider` 具有geometrixx值的屬性將與的OSGi設定相關 **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) — 其中引數 `commerceProvider` 也具有 `geometrixx`.
   * 您可以在此處設定其他屬性（在適當且可用時）。

在標準AEM安裝中，需要特定的實作，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx範例；這包含一般API的最小擴充功能 |

### 示例 {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>您可以使用CRXDE Lite來檢視在AEM一般實作的產品元件中如何處理這種情況：
>
>`/apps/geometrixx-outdoors/components/product`

### 工作階段處理 {#session-handling}

儲存與客戶購物車相關資訊的工作階段。

此 **CommerceSession**：

* 擁有 **購物車**

   * 執行新增/移除/等
   * 在購物車上執行各種計算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 擁有的持續性 **訂購** 資料：

   `CommerceSession.getUserContext()`

* 可使用擷取/更新傳遞詳細資料 `updateOrder(Map<String, Object> delta)`
* 同時擁有 **付款** 正在處理連線
* 同時擁有 **履行** 連線

### 架构 {#architecture}

#### 產品和變體的架構 {#architecture-of-product-and-variants}

單一產品可以有多個變數；例如，可能因顏色和/或大小而異。 產品必須定義哪些屬性會驅動變數；我們將其稱為 *變數軸*.

不過，並非所有屬性都是變數軸。 變化也可能會影響其他屬性；例如，價格可能依大小而定。 購物者無法選取這些屬性，因此不會視為變數軸。

每個產品和/或變體由資源表示，因此將1:1對應到存放庫節點。 必然結果是，特定產品和/或變體可由其路徑唯一識別。

任何產品資源都可以以下列方式表示 `Product API`. 產品API中的大部分呼叫都是變數專用（雖然變數可能會繼承來自祖先的共用值），但也有列出變數集的呼叫( `getVariantAxes()`， `getVariants()`、等)。

>[!NOTE]
>
>實際上，變體軸由任何決定 `Product.getVariantAxes()` 傳回：
>
>* 對於一般實作，AEM會從產品資料中的屬性讀取它( `cq:productVariantAxes`)
>
>雖然產品（一般）可以有許多變體軸，但現成可用的產品元件僅處理兩個變體軸：
>
>1. `size`
>1. 加上一個

>
>   此額外變體是透過 `variationAxis` 產品參考的屬性(通常 `color` (適用於Geometrixx Outdoors)。

#### 產品參考與PIM資料 {#product-references-and-pim-data}

一般而言：

* PIM資料位於 `/etc`

* 下的產品參考 `/content`.

產品變異和產品資料節點之間必須有1:1的對應。

產品參考也必須針對呈現的每個變數有一個節點，但不需要呈現所有變數。 例如，如果產品有S、M、L等變數，則產品資料可能是：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

雖然「大而高」目錄可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最後，不需要使用產品資料。 您可以將所有產品資料放在目錄中的參照下；但這樣一來，您就無法在沒有複製所有產品資料的情況下擁有多個目錄。

**API**

#### com.adobe.cq.commerce.api.Product介面 {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **一般儲存機制**

   * 產品節點非結構化。
   * 產品節點可以是：

      * 產品資料儲存在其他位置的參考：

         * 產品參考包含 `productData` 屬性，指向產品資料(通常位於 `/etc/commerce/products`)。
         * 產品資料為階層式；產品屬性繼承自產品資料節點的祖先。
         * 產品參考也可以包含本機屬性，這會覆寫其產品資料中指定的屬性。
      * 產品本身：

         * 不含 `productData` 屬性。
         * 在本機持有所有屬性（且不包含productData屬性）的產品節點會直接從自己的祖先繼承產品屬性。


* **AEM-generic產品結構**

   * 每個變體都必須有自己的葉節點。
   * 產品介面同時代表產品和變體，但相關的存放庫節點因其特定而有所不同。
   * 產品節點會說明產品屬性和變體軸。

#### 示例 {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### 購物車的架構 {#architecture-of-the-shopping-cart}

**组件**

* 該購物車屬於 `CommerceSession:`

   * 此 `CommerceSession` 執行新增、移除等動作。
   * 此 `CommerceSession` 也會在購物車上執行各種計算。
   * 此 `CommerceSession` 也會套用已觸發購物車的憑單和促銷活動。

* 雖然並非直接與購物車相關，但 `CommerceSession` 也必須提供型錄訂價資訊（因為它擁有訂價）

   * 訂價可能有數個修正因子：

      * 數量折扣。
      * 不同的貨幣。
      * VAT須繳納，且免繳增值稅。
   * 修飾元完全開放至下列介面：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在AEM一般情況下，購物車會儲存在 [ClientContext](/help/sites-administering/client-context.md)

**个性化**

* 個人化應一律透過 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 在所有情況下都會建立cart的：

   * 應使用新增產品 `CommerceSession.addCartEntry()` 方法。

* 以下說明ClientContext購物車中的購物車資訊範例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 結帳架構 {#architecture-of-checkout}

**購物車與訂單資料**

此 `CommerceSession` 擁有三個元素：

1. **購物車內容**

   購物車內容結構已由API修正：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定價**

   API也會修正此定價結構：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **订单详细信息**

   不過，訂單詳細資料為 *not* 由API修正：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**送貨計算**

* 訂單通常需要提供多個送貨選項（和價格）。
* 價格可能會以訂單的專案和詳細資訊為依據，例如重量和（或）交貨地址。
* 此 `CommerceSession` 可存取所有相依性，因此可將其視為類似產品定價的方式：

   * 此 `CommerceSession` 擁有送貨定價。
   * 使用 `updateOrder(Map<String, Object> delta)` 以擷取/更新傳遞詳細資訊。

### 搜尋定義 {#search-definition}

依照標準服務API模型，電子商務專案提供一組搜尋相關API，可供個別商務引擎實作。

>[!NOTE]
>
>目前，只有Hybris引擎會實作立即可用的Search API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。
>
>因此，雖然提供的現成通用實作不會實作此API，您可以擴充它並新增搜尋功能。

電子商務專案包含預設的搜尋元件，位於下列位置：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

這會利用搜尋API來查詢所選的商務引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection))：

#### 搜尋API {#search-api}

核心專案提供了幾個通用/協助程式類別：

1. `CommerceQuery`

   用於說明搜尋查詢（包含有關查詢文字、目前頁面、頁面大小、排序和所選Facet的資訊）。 所有實作搜尋API的電子商務服務都會收到此類別的執行個體，以便執行其搜尋。 A `CommerceQuery` 可從請求物件具現化( `HttpServletRequest`)。

1. `FacetParamHelper`

   是提供一個靜態方法的公用程式類別 —  `toParams`  — 用於產生 `GET` 多面和一個切換值清單中的引數字串。 這在UI端很有用，您需要顯示每個Facet的每個值的超連結，這樣當使用者按一下超連結時，就會切換個別值（也就是說，如果選取它，就會從查詢中移除它，否則會新增）。 這負責處理多個/單一值Facet、覆寫值等的所有邏輯。

搜尋API的進入點為 `CommerceService#search` 傳回「 」的方法 `CommerceResult` 物件。 請參閱API檔案，以取得有關本主題的詳細資訊。

### 開發促銷活動和憑單 {#developing-promotions-and-vouchers}

* 优惠券:

   * 憑單是使用Websites主控台建立/編輯的頁面型元件，並儲存在下列位置：

      `/content/campaigns`

   * 憑單供應：

      * 憑單代碼（由購物者輸入購物車中）。
      * 憑單標籤（在購物者將其輸入購物車後顯示）。
      * 促銷活動路徑（定義憑單套用的動作）。
   * 憑單沒有自己的開啟和結束日期/時間，但會使用其父行銷活動的日期/時間。
   * 外部商務引擎也可以提供憑單；這些至少需要：

      * 憑單代碼
      * 一個 `isValid()` 方法
   * 此 **憑單** 元件( `/libs/commerce/components/voucher`)提供：

      * 憑單管理的轉譯器；這會顯示目前購物車中的任何憑單。
      * 用於管理（新增/移除）憑單的編輯對話方塊（表單）。
      * 在購物車中新增/移除憑單所需的動作。



* 促销活动:

   * 促銷活動是以頁面為基礎的元件，會使用「網站」主控台建立/編輯，並儲存在下列位置：

      `/content/campaigns`

   * 促銷活動提供：

      * 優先順序
      * 推進處理常式路徑
   * 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
   * 您可以將促銷活動連結至體驗，以定義其區段。
   * 未連線至體驗的促銷活動不會自行引發，但仍可由憑單引發。
   * Promotion元件( `/libs/commerce/components/promotion`)包含：

      * 推進管理的轉譯器和對話方塊
      * 用於呈現和編輯升級處理常式專屬設定引數的子元件
   * 現成提供兩個提升處理常式：

      * `DiscountPromotionHandler`，會套用購物車範圍的絕對折扣或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作夥伴產品也在購物車中，則套用產品絕對折扣或百分比折扣
   * ClientContext `SegmentMgr` 解析區段和ClientContext `CartMgr` 解析促銷活動。 至少會引發一個已解析區段的促銷活動。

      * 已引發的促銷活動會透過AJAX呼叫傳回至伺服器，以重新計算購物車。
      * 已引發的促銷活動（以及新增的憑單）也會顯示在「ClientContext」面板中。




從購物車新增/移除憑單是透過 `CommerceSession` API：

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

如此一來， `CommerceSession` 負責檢查憑單是否存在，以及是否可套用。 這可能適用於只有在符合特定條件時才能套用的憑單；例如，當購物車總價大於$100時)。 如果憑單因任何原因而無法套用，則 `addVoucher` 方法會擲回例外狀況。 此外， `CommerceSession` 在新增/移除憑單後，負責更新購物車的價格。

此 `Voucher` 是一個類似Bean的類別，其中包含下列專案的欄位：

* 憑單代碼
* 簡短說明
* 參考指出折扣型態與值的相關促銷

此 `AbstractJcrCommerceSession` 提供可以套用憑單。 類別傳回的憑單 `getVouchers()` 為的例項 `cq:Page` 包含具有以下屬性的jcr：content節點（及其他）：

* `sling:resourceType` （字串） — 這需要 `commerce/components/voucher`

* `jcr:title` （字串） — 憑單說明
* `code` （字串） — 使用者必須輸入以套用此憑單的代碼
* `promotion` （字串） — 要套用的促銷活動；例如 `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促銷處理常式是修改購物車的OSGi服務。 購物車將支援中定義的多個鉤點 `PromotionHandler` 介面。

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

提供三個立即可用的促銷活動處理常式：

* `DiscountPromotionHandler` 套用購物車範圍的絕對或百分比折扣
* `PerfectPartnerPromotionHandler` 如果產品合作夥伴也在購物車中，則套用產品絕對折扣或百分比折扣
* `FreeShippingPromotionHandler` 套用免運費
