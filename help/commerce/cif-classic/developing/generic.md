---
title: 开发（一般）
seo-title: Developing (generic)
description: 集成框架包含带有API的集成层，允许您为电子商务功能构建AEM组件
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

# 开发（一般）{#developing-generic}

>[!NOTE]
>
>[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 中，此变量将被删除。

集成框架包括一个带有API的集成层。 这允许您为电子商务功能构建AEM组件（独立于您的特定电子商务引擎）。 它还允许您使用内部CRX数据库，或插入电子商务系统并将产品数据提取到AEM。

提供了许多现成的AEM组件来使用集成层。 目前，这些是：

* 产品显示组件
* 购物车
* 促销和凭单
* 目录和分区蓝图
* 结帐
* 搜索

为了搜索，提供了集成挂接，用于使用AEM搜索、第三方搜索或其组合。

## 电子商务引擎选择 {#ecommerce-engine-selection}

电子商务框架可以与任何电子商务解决方案一起使用，使用的引擎需要由AEM标识，即使在使用AEM通用引擎时也是如此：

* 电子商务引擎是支持 `CommerceService` 界面

   * 引擎可通过 `commerceProvider` 服务属性

* AEM支持 `Resource.adaptTo()` 表示 `CommerceService` 和 `Product`

   * 的 `adaptTo` 实施需要 `cq:commerceProvider` 资源层次结构中的属性：

      * 如果找到，则使用值过滤商务服务查找。
      * 如果未找到，则使用排名最高的商务服务。
   * A `cq:Commerce` 使用mixin， `cq:commerceProvider` 可添加到强类型资源中。


* 的 `cq:commerceProvider` 属性还用于引用相应的商务工厂定义。

   * 例如， `cq:commerceProvider` 值geometrixx的属性将与的OSGi配置相关联 **Day CQ Commerce Factory for Day-Outdoors(Day CQ Commerce Factory for Day CQ Commerce Factory for Autdoors for Day CQ Commerce Factory for Autdoors for Day CQ Commerce Factory for Autoudors-Outdoors(DayCGeometrixx工厂)** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) — 其中参数 `commerceProvider` 也具有值 `geometrixx`.
   * 此处可以配置其他属性（如果适用且可用）。

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
>使用CRXDE Lite，您可以在AEM通用实施的产品组件中查看如何处理该问题：
>
>`/apps/geometrixx-outdoors/components/product`

### 会话处理 {#session-handling}

用于存储与客户购物车相关的信息的会话。

的 **商务会话**:

* 拥有 **购物车**

   * 执行添加/删除/等
   * 在购物车上执行各种计算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 拥有 **订购** 数据：

   `CommerceSession.getUserContext()`

* 可以使用 `updateOrder(Map<String, Object> delta)`
* 还拥有 **付款** 处理连接
* 还拥有 **履行** 连接

### 架构 {#architecture}

#### 产品和变体的架构 {#architecture-of-product-and-variants}

单个产品可以有多个变体；例如，它可能因颜色和/或大小而异。 产品必须定义驱动变量的属性；我们称这些 *变量轴*.

但是，并非所有属性都是变型轴。 变化也会影响其他属性；例如，价格可能取决于规模。 购物者无法选择这些属性，因此不会将其视为变体轴。

每个产品和/或变体都由资源表示，因此将1:1映射到存储库节点。 由此可推论，特定产品和/或变体可以通过其路径唯一标识。

任何产品资源都可以由 `Product API`. 产品API中的大多数调用都特定于变量（尽管变量可能会继承父代的共享值），但也有一些调用列出了变量集( `getVariantAxes()`, `getVariants()`等)。

>[!NOTE]
>
>实际上，变轴由任何 `Product.getVariantAxes()` 返回：
>
>* 对于通用实施， AEM会从产品数据( `cq:productVariantAxes`)
>
>虽然产品（通常）可以具有多个变体轴，但现成的产品组件仅处理两个：
>
>1. `size`
>1. 再加一个

>
>   通过 `variationAxis` 产品引用的属性(通常 `color` (对于Geometrixx Outdoors)。

#### 产品引用和PIM数据 {#product-references-and-pim-data}

一般而言：

* PIM数据位于 `/etc`

* 下的产品参考 `/content`.

产品变体与产品数据节点之间必须存在1:1映射。

产品引用还必须具有每个显示的变体的节点，但不要求显示所有变体。 例如，如果产品具有S、M、L变量，则产品数据可能为：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

而“大而高”目录可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最后，无需使用产品数据。 您可以将所有产品数据放在目录的引用下；但是，如果不复制所有产品数据，您就无法真正拥有多个目录。

**API**

#### com.adobe.cq.commerce.api.Product界面 {#com-adobe-cq-commerce-api-product-interface}

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

* **一般存储机制**

   * 产品节点不是：非结构化的。
   * 产品节点可以是：

      * 将产品数据存储在其他位置的引用：

         * 产品引用包含 `productData` 属性，指向产品数据(通常位于 `/etc/commerce/products`)。
         * 产品数据是分层的；产品属性继承自产品数据节点的祖先。
         * 产品引用还可以包含本地属性，这些属性会覆盖其产品数据中指定的属性。
      * 产品本身：

         * 没有 `productData` 属性。
         * 在本地保存所有属性（且不包含productData属性）的产品节点会直接从其祖先继承产品属性。


* **AEM-generic Product Structure**

   * 每个变体必须具有其自己的叶节点。
   * 产品界面同时表示产品和变体，但相关存储库节点是特定的。
   * 产品节点描述产品属性和变量轴。

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

* 购物车归 `CommerceSession:`

   * 的 `CommerceSession` 执行添加、删除等操作。
   * 的 `CommerceSession` 还会对购物车执行各种计算。
   * 的 `CommerceSession` 还应用已触发到购物车的凭单和促销活动。

* 虽然与购物车不直接相关，但 `CommerceSession` 还必须提供目录定价信息（因为它拥有定价）

   * 定价可能具有以下几个修改量：

      * 数量折扣。
      * 不同的货币。
      * 增值税免税。
   * 这些修饰符在以下界面中完全开放：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在AEM-generic的示例中，购物车存储在 [ClientContext](/help/sites-administering/client-context.md)

**个性化**

* 个性化应始终通过 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 在所有情况下创建的购物车：

   * 应使用 `CommerceSession.addCartEntry()` 方法。

* 下面展示了ClientContext车中购物车信息的示例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 结帐架构 {#architecture-of-checkout}

**购物车和订购数据**

的 `CommerceSession` 拥有以下三个元素：

1. **购物车内容**

   购物车内容架构已由API修复：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定价**

   定价架构也由API修复：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **订单详细信息**

   但是，订单详细信息包括 *not* 由API修复：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**装运计算**

* 订单通常需要显示多个送货选项（和价格）。
* 价格可能基于订单的项目和详细信息，如重量和/或交货地址。
* 的 `CommerceSession` 具有对所有依赖项的访问权限，因此可以采用与产品定价类似的方式对其进行处理：

   * 的 `CommerceSession` 拥有送货定价。
   * 使用 `updateOrder(Map<String, Object> delta)` 以检索/更新投放详细信息。

### 搜索定义 {#search-definition}

遵循标准服务API模型，电子商务项目提供了一组可由单个商务引擎实施的与搜索相关的API。

>[!NOTE]
>
>目前，只有hybris引擎会实施现成的搜索API。
>
>但是，搜索API是通用的，可由每个CommerceService单独实施。
>
>因此，尽管提供的现成通用实施不实施此API，但您可以扩展此API并添加搜索功能。

电子商务项目包含默认搜索组件，该组件位于：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

这会利用搜索API查询选定的商务引擎(请参阅 [电子商务引擎选择](#ecommerce-engine-selection)):

#### 搜索API {#search-api}

核心项目提供了几个通用/帮助程序类：

1. `CommerceQuery`

   用于描述搜索查询（包含有关查询文本、当前页面、页面大小、排序和选定彩块化的信息）。 所有实施搜索API的电子商务服务都将接收此类的实例，以执行其搜索。 A `CommerceQuery` 可以从请求对象( `HttpServletRequest`)。

1. `FacetParamHelper`

   是一个实用程序类，提供一个静态方法 —  `toParams`  — 用于生成 `GET` facet列表和一个切换值中的参数字符串。 这在UI端非常有用，在UI端，您需要为每个facet的每个值显示一个超链接，这样当用户单击该超链接时，相应的值即会被切换（即，如果已选择该值，则会从查询中删除，否则会添加）。 这会处理处理多个/单值彩块化、覆盖值等的所有逻辑。

搜索API的入口点是 `CommerceService#search` 返回 `CommerceResult` 对象。 有关此主题的更多信息，请参阅API文档。

### 开发促销和凭证 {#developing-promotions-and-vouchers}

* 优惠券:

   * 凭单是基于页面的组件，使用“网站”控制台创建/编辑并存储在以下位置：

      `/content/campaigns`

   * 凭证供应：

      * 优惠券代码（由购物者输入购物车）。
      * 凭证标签（在购物者将其输入购物车后显示）。
      * 促销路径（用于定义凭证应用的操作）。
   * 凭单没有其自己的开启和关闭日期/时间，但使用其父营销活动的日期/时间。
   * 外部商务引擎也可提供凭证；这些要求至少满足以下条件：

      * 凭证代码
      * 安 `isValid()` 方法
   * 的 **优惠券** 组件( `/libs/commerce/components/voucher`)提供：

      * 凭证管理的渲染器；这显示购物车中当前的所有凭证。
      * 用于管理（添加/删除）凭证的编辑对话框（表单）。
      * 向购物车添加/删除凭单所需的操作。



* 促销活动:

   * 促销活动是一个基于页面的组件，可通过“网站”控制台创建/编辑并存储在以下位置：

      `/content/campaigns`

   * 促销供应：

      * 优先级
      * 升级处理程序路径
   * 您可以将促销活动连接到营销活动以定义其开/关日期/时间。
   * 您可以将促销活动与体验关联以定义其区段。
   * 未连接到体验的促销活动不会自行触发，但仍可以通过凭单触发。
   * 促销组件( `/libs/commerce/components/promotion`)包含：

      * 用于提升管理的渲染器和对话框
      * 用于渲染和编辑特定于升级处理程序的配置参数的子组件
   * 两个升级处理程序现成提供：

      * `DiscountPromotionHandler`，应用购物车范围的绝对或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作伙伴产品也在购物车中，则应用产品绝对或百分比折扣
   * ClientContext `SegmentMgr` 解析区段和ClientContext `CartMgr` 解析促销活动。 将触发至少一个已解析区段的每个促销活动。

      * 已触发的促销活动将通过AJAX调用发送回服务器以重新计算购物车。
      * 触发的促销活动（和添加的凭证）也会显示在ClientContext面板中。




通过 `CommerceSession` API:

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

这边， `CommerceSession` 负责检查凭证是否存在以及是否可以应用。 这可能适用于仅在满足特定条件时才能应用的凭证；例如，当购物车总价格大于$100时。 如果凭单因任何原因无法应用，则 `addVoucher` 方法将引发异常。 此外， `CommerceSession` 负责在添加/删除凭证后更新购物车的价格。

的 `Voucher` 是一个类bean类，其中包含以下字段：

* 凭证代码
* 简短描述
* 引用指示折扣类型和值的相关促销活动

的 `AbstractJcrCommerceSession` 提供的可以申请凭单。 班级返回的凭单 `getVouchers()` 是实例 `cq:Page` 包含具有以下属性的jcr:content节点（其中包括）：

* `sling:resourceType` （字符串） — 这需要 `commerce/components/voucher`

* `jcr:title` （字符串） — 用于凭证的说明
* `code` （字符串） — 用户必须输入以应用此凭证的代码
* `promotion` （字符串） — 要应用的促销活动；例如 `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促销处理程序是修改购物车的OSGi服务。 购物车将支持在 `PromotionHandler` 界面。

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

提供了三个现成的升级处理程序：

* `DiscountPromotionHandler` 应用购物车范围的绝对或百分比折扣
* `PerfectPartnerPromotionHandler` 如果产品合作伙伴也在购物车中，则应用产品绝对折扣或百分比折扣
* `FreeShippingPromotionHandler` 应用免运费
