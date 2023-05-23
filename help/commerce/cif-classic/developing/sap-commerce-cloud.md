---
title: 使用SAPCommerce Cloud進行開發
seo-title: Developing with SAP Commerce Cloud
description: SAPCommerce Cloud整合架構包含具有API的整合層
seo-description: The SAP Commerce Cloud integration framework includes an integration layer with an API
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 0%

---

# 使用SAPCommerce Cloud進行開發 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>電子商務架構可與任何電子商務解決方案搭配使用。 在此處理的特定細節和範例將參考 [hybris](https://www.hybris.com/) 解決方案。

整合架構包含具有API的整合層。 這可讓您：

* 插入電子商務系統，將產品資料提取至AEM

* 為獨立於特定電子商務引擎的商務功能建置AEM元件

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可供使用。

許多現成的AEM元件可供使用整合層。 目前包括：

* 產品顯示元件
* 購物車
* 結帳

對於搜尋，提供的整合鉤子可讓您使用AEM搜尋、電子商務系統搜尋、第三方搜尋或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務架構可搭配任何電子商務解決方案使用，所使用的引擎必須可由AEM識別：

* 電子商務引擎是支援 `CommerceService` 介面

   * 引擎的辨別方法如下： `commerceProvider` 服務屬性

* AEM支援 `Resource.adaptTo()` 的 `CommerceService` 和 `Product`

   * 此 `adaptTo` 實施會尋找 `cq:commerceProvider` 資源階層中的屬性：

      * 如果找到，則會使用值來篩選商務服務查閱。

      * 如果找不到，則會使用排名最高的商務服務。
   * A `cq:Commerce` mixin用於 `cq:commerceProvider` 可新增至強型別資源。


* 此 `cq:commerceProvider` 屬性也可用來參考適當的商務工廠定義。

   * 例如， `cq:commerceProvider` 具有值的屬性 `hybris` 將與的OSGi設定相關聯 **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) — 其中的引數 `commerceProvider` 也具有 `hybris`.

   * 此處提供其他屬性，例如 **目錄版本** 可設定（在適當且可用時）。

請參閱下列範例：

| `cq:commerceProvider = geometrixx` | 在標準AEM安裝中，需要特定的實作；例如geometrixx範例，其中包含一般API的最低擴充功能 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris實作 |

### 示例 {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
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
>您可以使用CRXDE Lite來檢視在Hybris實作的產品元件中如何處理此問題：
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### 針對hybris 4開發 {#developing-for-hybris}

更新eCommerce Integration Framework的hybris擴充功能，以支援Hybris 5，同時維持與Hybris 4的回溯相容性。

程式碼中的預設設定是針對Hybris 5調整的。

若要針對Hybris 4開發，需要下列專案：

* 叫用maven時，請將以下命令列引數新增到命令中

   `-P hybris4`

   它會下載預先設定的Hybris 4發佈，並將其嵌入套件組合中 `cq-commerce-hybris-server`.

* 在OSGi設定管理員中：

   * 停用預設回應剖析器服務的Hybris 5支援。

   * 請確定Hybris基本驗證處理常式服務的服務排名低於Hybris OAuth處理常式服務。

### 工作階段處理 {#session-handling}

hybris會使用使用者工作階段來儲存資訊，例如客戶的購物車。 工作階段ID會從hybris傳回，位於 `JSESSIONID` 後續要求傳送給hybris的Cookie。 為避免將工作階段ID儲存在存放庫中，它會編碼到儲存在購物者瀏覽器中的另一個Cookie。 會執行下列步驟：

* 第一次請求時，購物者的請求上未設定Cookie，因此會傳送請求給hybris執行個體以建立工作階段。

* 工作階段Cookie會從回應中擷取，並在新的Cookie中編碼(例如 `hybris-session-rest`)並在對購物者的回應中設定。 新Cookie中的編碼為必填，因為原始Cookie僅對特定路徑有效，否則在後續請求中不會從瀏覽器傳回。 路徑資訊也必須新增至Cookie的值。

* 在後續的請求中，Cookie會從 `hybris-session-<*xxx*>` Cookie，並在用來向hybris要求資料的HTTP使用者端上設定。

>[!NOTE]
>
>當原始工作階段不再有效時，會建立新的匿名工作階段。

#### CommerceSession {#commercesession}

* 此工作階段「擁有」 **購物車**

   * 執行新增/移除/等

   * 在購物車上執行各種計算；

      `commerceSession.getProductPrice(Product product)`

* 擁有 *儲存位置* 的 **訂購** 資料

   `CommerceSession.getUserContext()`

* 同時擁有 **付款** 正在處理連線

* 同時擁有 **履行** 連線

### 產品同步與發佈 {#product-synchronization-and-publishing}

在Hybris中維護的產品資料需要可在AEM中使用。 已實作下列機制：

* hybris會提供ID的初始載入作為摘要。 此摘要可能有更新。
* hybris會透過摘要(AEM輪詢)提供更新資訊。
* 當AEM使用產品資料時，它會傳送要求傳回hybris以取得目前資料（條件式取得要求使用上次修改日期）。
* 在Hybris上，可以宣告方式指定摘要內容。
* 將摘要結構對應至AEM內容模型會在AEM端的摘要配接器中進行。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 匯入工具(b)用於初始設定AEM中的目錄頁面樹狀結構。
* Hybris中的目錄變更會透過摘要指示給AEM，然後這些變更會傳播給AEM (b)

   * 與目錄版本相關的產品已新增/刪除/變更。

   * 產品已核准。

* Hybris擴充功能提供輪詢匯入工具（「hybris」配置），可設定為以指定的間隔（例如，每24小時，其間隔以秒為單位）將變更匯入AEM：

   ```JavaScript
       http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
        {
        * "jcr:mixinTypes": ["cq:PollConfig"],
        * "enabled": true,
        * "source": "hybris:outdoors",
        * "jcr:primaryType": "cq:PageContent",
        * "interval": 86400
        }
   ```

* AEM中的目錄設定可辨識 **已分段** 和 **線上** 目錄版本。

* 在目錄版本之間同步產品需要（停用）啟用對應的AEM頁面(a、c)

   * 將產品新增至 **線上** 目錄版本需要啟動產品頁面。

   * 移除產品需要停用。

* 在AEM (c)中啟動頁面需要檢查(b)，並且只有在

   * 產品位於 **線上** 產品頁面的目錄版本。

   * 參考的產品位於 **線上** 其他頁面的目錄版本（例如行銷活動頁面）。

* 啟用的產品頁面需要存取產品資料的 **線上** 版本(d)。

* AEM發佈執行個體需要存取hybris，以擷取產品和個人化資料(d)。

### 架构 {#architecture}

#### 產品和變體的架構 {#architecture-of-product-and-variants}

單一產品可以有多個變數；例如，可能因顏色和/或大小而異。 產品必須定義哪些屬性會驅動變數；我們將其稱為 *變數軸*.

不過，並非所有屬性都是變數軸。 變化也可能會影響其他屬性；例如，價格可能依大小而定。 購物者無法選取這些屬性，因此不會視為變數軸。

每個產品和/或變體由資源表示，因此將1:1對應到存放庫節點。 必然結果是，特定產品和/或變體可由其路徑唯一識別。

產品/變體資源並不總是包含實際產品資料。它可能表示實際包含在其他系統上的資料（例如hybris）。 例如，產品說明、定價等不會儲存在AEM中，而是從電子商務引擎即時擷取。

任何產品資源都可以以下列方式表示 `Product API`. 產品API中的大部分呼叫都是變數專用（雖然變數可能會繼承來自祖先的共用值），但也有列出變數集的呼叫( `getVariantAxes()`， `getVariants()`、等)。

>[!NOTE]
>
>實際上，變體軸由任何決定 `Product.getVariantAxes()` 傳回：
>* hybris會為hybris實作定義
>
>雖然產品（一般）可以有許多變體軸，但現成可用的產品元件僅處理兩個變體軸：
>
>1. `size`
>
>1. 加上一個

>
>此額外變體是透過 `variationAxis` 產品參考的屬性(通常 `color` (適用於Geometrixx Outdoors)。

#### 產品參考和產品資料 {#product-references-and-product-data}

一般而言：

* 產品資料位於 `/etc`

* 下的和產品參考 `/content`.

產品變異和產品資料節點之間必須有1:1的對應。

產品參考也必須針對呈現的每個變數有一個節點，但不需要呈現所有變數。 例如，如果產品有S、M、L等變數，則產品資料可能是：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

雖然「大而高」目錄可能只有：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

   * 產品節點為 `nt:unstructured`.

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

   * 此 `CommerceSession` 執行新增/移除/等等。
   * 此 `CommerceSession` 也會在購物車上執行各種計算。&quot;

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

   * 在hybris案例中，hybris伺服器擁有購物車。
   * 在AEM一般情況下，購物車會儲存在 [ClientContext](/help/sites-administering/client-context.md).

**个性化**

* 個人化應一律透過 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 在所有情況下都會建立cart的：

   * 應使用新增產品 `CommerceSession.addCartEntry()` 方法。

* 以下說明ClientContext購物車中的購物車資訊範例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 結帳架構 {#architecture-of-checkout}

**購物車與訂單資料**

此 `CommerceSession` 擁有三個元素：

1. 購物車內容
1. 定價
1. 訂單詳細資料

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
   * 可使用擷取/更新傳遞詳細資料 `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>您可以實作送貨選擇器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 基本上，這可以是 `foundation/components/form/radio`，但回撥至 `CommerceSession` 適用於：
>
>* 檢查方法是否可用
>* 新增定價資訊
>* 讓購物者能夠更新AEM中的訂單頁面（包括送貨方法的超集以及描述這些方法的文字），同時仍可控制以公開相關的 `CommerceSession` 資訊。


**付款處理**

* 此 `CommerceSession` 也擁有付款處理連線。

* 實作者需要將特定呼叫（新增至其選擇的付款處理服務）新增至 `CommerceSession` 實作。

**訂單履行**

* 此 `CommerceSession` 也擁有履行連線。
* 實作者需要將特定呼叫（新增至其選擇的付款處理服務）新增至 `CommerceSession` 實作。

### 搜尋定義 {#search-definition}

依照標準服務API模型，電子商務專案提供一組搜尋相關API，可供個別商務引擎實作。

>[!NOTE]
>
>目前，只有Hybris引擎會實作立即可用的Search API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。

電子商務專案包含預設的搜尋元件，位於下列位置：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

這會利用搜尋API來查詢所選的商務引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection))：

#### 搜尋API {#search-api}

核心專案提供了幾個通用/協助程式類別：

1. `CommerceQuery`

   用於說明搜尋查詢（包含有關查詢文字、目前頁面、頁面大小、排序和所選Facet的資訊）。 所有實作搜尋API的電子商務服務都會收到此類別的執行個體，以便執行其搜尋。 A `CommerceQuery` 可從請求物件具現化( `HttpServletRequest`)。

1. `FacetParamHelper`

   是提供一個靜態方法的公用程式類別 —  `toParams`  — 用於產生 `GET` 多面和一個切換值清單中的引數字串。 這在UI端很有用，您需要顯示每個Facet的每個值的超連結，這樣當使用者按一下超連結時，就會切換個別值（也就是說，如果選取它，就會從查詢中移除它，否則會新增）。 這負責處理多個/單一值Facet、覆寫值等的所有邏輯。

搜尋API的進入點為 `CommerceService#search` 傳回「 」的方法 `CommerceResult` 物件。 請參閱 [API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 以取得有關本主題的詳細資訊。

### 使用者整合 {#user-integration}

提供AEM與各種電子商務系統之間的整合。 這需要在不同系統之間同步處理購物者的策略，以便AEM特定的程式碼只需瞭解AEM，反之亦然：

* 身份验证

   AEM被推定為 *僅限* Web前端，因此可執行 *全部* 驗證。

* Hybris中的帳戶

   AEM會為每個購物者以hybris建立對應的（下屬）帳戶。 此帳戶的使用者名稱與AEM使用者名稱相同。 加密隨機密碼會自動產生，並儲存在AEM中（加密）。

#### 既有使用者 {#pre-existing-users}

AEM前端可放置在現有Hybris實作的前面。 您也可以將hybris引擎新增至現有的AEM安裝。 要執行此操作，系統必須能夠妥善處理任一系統中的現有使用者：

* AEM -> hybris

   * 登入Hybris時，如果AEM使用者尚不存在：

      * 使用隨機密碼建立新的hybris使用者
      * 將hybris使用者名稱儲存在AEM使用者的使用者目錄中
   * 请参阅: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 登入AEM時，如果系統辨識出使用者：

      * 嘗試使用提供的使用者名稱/密碼登入hybris
      * 如果成功，請在AEM中使用相同的密碼建立新使用者(AEM特定的salt將導致AEM特定的雜湊)
   * 上述演演算法是在Sling中實作 `AuthenticationInfoPostProcessor`

      * 请参阅: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自訂匯入程式 {#customizing-the-import-process}

若要以現有功能為基礎建置自訂匯入處理常式：

* 必須實作 `ImportHandler` 介面

* 可以擴充 `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

若要讓匯入工具識別您的自訂處理常式，必須指定 `service.ranking`值高於0的屬性，例如。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
