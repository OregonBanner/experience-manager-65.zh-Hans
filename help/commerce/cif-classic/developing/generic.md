---
title: 开发（通用）
description: 集成框架包括带有API的集成层，允许您为电子商务功能构建AEM组件。
contentOwner: Guillaume Carlino
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 0%

---

# 开发（通用）{#developing-generic}

>[!NOTE]
>
>[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可用。

集成框架包括带有API的集成层。 这使您能够为电子商务功能构建AEM组件（独立于您的特定电子商务引擎）。 它还允许您使用内部CRX数据库或插入电子商务系统并将产品数据提取到AEM中。

提供了多个现成的AEM组件以使用集成层。 目前，这些方法包括：

* 产品显示组件
* 购物车
* 促销和优惠券
* 目录和章节Blueprint
* 结帐
* 搜索

对于搜索，提供了一个集成挂接，允许您使用Adobe Experience Manager (AEM)搜索、第三方搜索或它们的组合。

## 电子商务引擎选择 {#ecommerce-engine-selection}

电子商务框架可与任何电子商务解决方案一起使用，使用的引擎必须由AEM标识 — 即使使用AEM通用引擎时也是如此：

* 电子商务引擎是支持 `CommerceService` 界面

   * 可以通过以下方式区分引擎 `commerceProvider` 服务属性

* AEM支持 `Resource.adaptTo()` 对象 `CommerceService` 和 `Product`

   * 此 `adaptTo` 实施将查找 `cq:commerceProvider` 资源层次结构中的属性：

      * 如果找到，该值将用于筛选Commerce服务查找。
      * 如果未找到，则使用排名最高的商务服务。

   * A `cq:Commerce` mixin用于 `cq:commerceProvider` 可以添加到强类型资源中。

* 此 `cq:commerceProvider` 属性还用于引用相应的商务工厂定义。

   * 例如， `cq:commerceProvider` 属性，其值Geometrixx与的OSGi配置关联 **Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) — 其中，参数 `commerceProvider` 还具有值 `geometrixx`.
   * 此处可以配置其他属性（在适当且可用时）。

在标准AEM安装中，需要特定实施，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx示例；这包括通用API的最小扩展 |

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
>通过使用CRXDE Lite，您可以了解在AEM常规实施的产品组件中如何处理这种情况：
>
>`/apps/geometrixx-outdoors/components/product`

### 会话处理 {#session-handling}

用于存储与客户购物车相关的信息的会话。

此 **CommerceSession**：

* 拥有 **购物车**

   * 执行添加/删除/等
   * 在购物车上执行各种计算；

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 拥有的持久性 **订购** 数据：

  `CommerceSession.getUserContext()`

* 可以使用检索/更新投放详细信息 `updateOrder(Map<String, Object> delta)`
* 拥有 **付款** 正在处理连接
* 拥有 **履行** 连接

### 架构 {#architecture}

#### 产品和变体的架构 {#architecture-of-product-and-variants}

单个产品可以有多个变体；例如，它可能因颜色和/或大小而异。 产品必须定义哪些属性会驱动变化；Adobe术语如下 *变量轴*.

但是，并非所有属性都是变量轴。 变体也可能会影响其他属性；例如，价格可能取决于大小。 购物者无法选择这些属性，因此不被视为变量轴。

每个产品和/或变体由一个资源表示，因此将1:1映射到存储库节点。 由此推断，特定产品和/或变体可通过其路径唯一标识。

任何产品资源都可以用 `Product API`. 产品API中的大多数调用均特定于变体（尽管变体可能继承来自祖先的共享值），但也有列出变体集的调用( `getVariantAxes()`， `getVariants()`，等等)。

>[!NOTE]
>
>实际上，变轴由任何参数决定 `Product.getVariantAxes()` 返回：
>
>* 对于通用实施，AEM会从产品数据( `cq:productVariantAxes`)
>
>虽然产品（通常）可以具有多个变体轴，但现成的产品组件仅处理两个变体轴：
>
>1. `size`
>1. 再加一个
>
>   通过以下方式选择此附加变体： `variationAxis` 产品引用的属性(通常 `color` (对于Geometrixx Outdoors)。

#### 产品引用和PIM数据 {#product-references-and-pim-data}

一般而言：

* PIM数据位于 `/etc`

* 下的产品引用 `/content`.

产品变体和产品数据节点之间必须是1:1映射。

产品引用还必须具有呈现每个变体的节点 — 但不要求呈现所有变体。 例如，如果产品具有S、M、L变体，则产品数据可能为：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

而“大而高”的目录可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最后，无需使用产品数据。 您可以将所有产品数据放置在目录中的引用下；但是，如果不复制所有产品数据，则实际上不能有多个目录。

**API**

#### com.adobe.cq.commerce.api.Product接口 {#com-adobe-cq-commerce-api-product-interface}

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
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

* **一般存储机制**

   * 产品节点nt：unstructured。
   * 产品节点可以是：

      * 引用，将产品数据存储在其他位置：

         * 产品引用包含 `productData` 属性，指向产品数据(通常位于 `/etc/commerce/products`)。
         * 产品数据是分层的；产品属性继承自产品数据节点的祖先。
         * 产品引用还可以包含本地属性，这些属性将覆盖产品数据中指定的属性。

      * 产品本身：

         * 不带 `productData` 属性。
         * 在本地保存所有属性（并且不包含productData属性）的product节点直接从自己的祖先继承product属性。

* **AEM-generic产品结构**

   * 每个变体必须具有自己的叶节点。
   * 产品界面既表示产品，又表示变体，但相关的存储库节点特定于它。
   * product节点描述产品属性和变体轴。

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

#### 购物车的架构 {#architecture-of-the-shopping-cart}

**组件**

* 该购物车属于 `CommerceSession:`

   * 此 `CommerceSession` 执行添加、删除等操作。
   * 此 `CommerceSession` 还会在购物车上执行各种计算。
   * 此 `CommerceSession` 还会将已触发的优惠券和促销活动应用于购物车。

* 虽然不直接与购物车相关，但是 `CommerceSession` 还必须提供目录定价信息（因为它拥有定价）

   * 定价可能有几个修饰符：

      * 数量折扣。
      * 不同的货币。
      * 应缴纳增值税且免纳增值税。

   * 修饰符是开放的，接口如下：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**存储**

* 存储

   * 在AEM一般情况下，购物车存储在 [ClientContext](/help/sites-administering/client-context.md)

**个性化**

* 始终通过以下方式推动个性化 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 在所有情况下都会创建Cart的：

   * 应使用添加产品 `CommerceSession.addCartEntry()` 方法。

* 下面说明了ClientContext车中的购物车信息示例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 结账的架构 {#architecture-of-checkout}

**购物车和订单数据**

此 `CommerceSession` 拥有三个元素：

1. **购物车内容**

   购物车内容架构由API修复：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定价**

   定价模式也由API修复：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **订单详细信息**

   但是，订单详情如下 *非* 由API修复：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**配送费计算**

* 订单通常必须提供多种送货选项（和价格）。
* 价格可能基于物料和订单详细信息，如重量和/或交货地址。
* 此 `CommerceSession` 有权访问所有依赖项，因此可以采用与产品定价类似的方式对其进行处理：

   * 此 `CommerceSession` 拥有配送定价。
   * 使用 `updateOrder(Map<String, Object> delta)` 以检索/更新投放详细信息。

### 搜索定义 {#search-definition}

遵循标准服务API模型，电子商务项目提供一组搜索相关的API，它们可以由商业引擎实现。

>[!NOTE]
>
>目前，只有hybris引擎可开箱即用地实施搜索API。
>
>但是，搜索API是通用的，可以由每个CommerceService单独实施。
>
>因此，尽管提供的现成通用实施不实施此API，但您可以对其进行扩展并添加搜索功能。

电子商务项目包含以下位置中的默认搜索组件：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

这将使用搜索API查询选定的商务引擎(请参阅 [电子商务引擎选择](#ecommerce-engine-selection))：

#### 搜索API {#search-api}

核心项目提供了几个通用/帮助程序类：

1. `CommerceQuery`

   用于描述搜索查询（包含有关查询文本、当前页面、页面大小、排序和所选彩块化的信息）。 所有实施搜索API的电子商务服务都接收此类的实例以执行其搜索。 A `CommerceQuery` 可以从请求对象实例化( `HttpServletRequest`)。

1. `FacetParamHelper`

   是一个实用程序类，它提供一个静态方法 —  `toParams`  — 用于生成 `GET` 多面和一个切换值列表中的参数字符串。 这在UI端很有用，您需要为每个Facet的每个值显示超链接，这样当用户单击超链接时，将切换相应的值。 也就是说，如果选定了它，则会将其从查询中删除，否则会添加它。 这解决了处理多个/单值Facet、覆盖值等操作的所有逻辑。

搜索API的入口点为 `CommerceService#search` 返回 `CommerceResult` 对象。 有关此主题的更多信息，请参阅API文档。

### 开发促销和优惠券 {#developing-promotions-and-vouchers}

* 优惠券:

   * 优惠券是一种基于页面的组件，使用网站控制台创建/编辑并存储在以下位置：

     `/content/campaigns`

   * 优惠券供应：

      * 优惠券代码（由购物者键入购物车中）。
      * 优惠券标签（在购物者将其输入购物车后显示）。
      * 提升路径（定义凭证应用的操作）。

   * 优惠券没有自己的开始和结束日期/时间，但会使用父营销活动的日期/时间。
   * 外部商业引擎也可以提供凭证；这些凭证至少需要：

      * 优惠券代码
      * An `isValid()` 方法

   * 此 **优惠券** 组件( `/libs/commerce/components/voucher`)提供：

      * 凭证管理的呈现器；这将显示当前购物车中的任何凭证。
      * 用于管理（添加/删除）优惠券的编辑对话框（表单）。
      * 在购物车中添加/删除优惠券所需的操作。

* 促销活动:

   * 促销活动是一个基于页面的组件，它使用“网站”控制台创建/编辑并存储在以下位置：

     `/content/campaigns`

   * 促销供应：

      * 优先级
      * 提升处理程序路径

   * 您可以将促销活动关联到促销活动，以定义其打开/关闭日期/时间。
   * 您可以将促销活动连接到体验以定义其区段。
   * 与体验无关的促销活动不会自行触发，但优惠券仍可以触发。
   * 提升组件( `/libs/commerce/components/promotion`)包含：

      * 用于提升管理的渲染器和对话框
      * 用于呈现和编辑特定于提升处理程序的配置参数的子组件

   * 提供了两个现成的提升处理程序：

      * `DiscountPromotionHandler`，应用购物车范围的绝对折扣或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作伙伴产品也在购物车中，则应用产品绝对折扣或百分比折扣

   * ClientContext `SegmentMgr` 解析区段和ClientContext `CartMgr` 解析促销活动。 至少具有一个已解析区段的每个促销活动都会触发。

      * 已触发的促销活动将通过AJAX调用发送回服务器以重新计算购物车。
      * ClientContext面板中还会显示触发的促销活动（和添加的优惠券）。

在购物车中添加/删除优惠券是通过 `CommerceSession` API：

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

这边， `CommerceSession` 负责检查凭单是否存在以及凭单是否可以应用。 这可能适用于只有在满足特定条件时才能应用的凭单。 例如，当购物车总价格大于$100时。 如果由于任何原因无法应用优惠券，则 `addVoucher` 方法引发异常。 此外， `CommerceSession` 负责在添加/删除优惠券后更新购物车的价格。

此 `Voucher` 是一个类Bean，其中包含下列字段：

* 优惠券代码
* 简短描述
* 引用指示折扣类型和值的相关促销

此 `AbstractJcrCommerceSession` 提供申请优惠券的功能。 类返回的凭证 `getVouchers()` 的实例 `cq:Page` 包含具有以下属性（及其他）的jcr：content节点：

* `sling:resourceType` （字符串） — 这需要 `commerce/components/voucher`

* `jcr:title` （字符串） — 用于优惠券的描述
* `code` （字符串） — 用户必须输入以应用此优惠券的代码
* `promotion` （字符串） — 要应用的促销活动；例如， `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促销处理程序是修改购物车的OSGi服务。 购物车支持在中定义的多个挂钩。 `PromotionHandler` 界面。

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

提供了三个现成的提升处理程序：

* `DiscountPromotionHandler` 应用购物车范围的绝对折扣或百分比折扣
* `PerfectPartnerPromotionHandler` 如果产品合作伙伴也在购物车中，则应用产品绝对折扣或百分比折扣
* `FreeShippingPromotionHandler` 应用免运费
