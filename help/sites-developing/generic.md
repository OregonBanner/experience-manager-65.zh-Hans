---
title: 开发（通用）
seo-title: 开发（通用）
description: 集成框架包含带有API的集成层，允许您为电子商务功能构建AEM组件
seo-description: 集成框架包含带有API的集成层，允许您为电子商务功能构建AEM组件
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---


# 开发（通用）{#developing-generic}

>[!NOTE]
>
>[还提供](/help/sites-developing/ecommerce.md#api-documentation) API文档。

该集成框架包含一个带有API的集成层。 这允许您为电子商务功能（独立于您的特定电子商务引擎）构建AEM组件。 它还允许您使用内部CRX数据库或插入电子商务系统并将产品数据拉入AEM。

为使用集成层提供了许多现成的AEM组件。 目前有：

* 产品显示组件
* 购物车
* Promotions and vouchers
* 目录和章节蓝图
* 结帐
* 搜索

对于搜索，会提供集成挂接，允许您使用AEM搜索、第三方搜索(如Search&amp;Promote)或其组合。

## 电子商务引擎选择 {#ecommerce-engine-selection}

电子商务框架可以与任何电子商务解决方案一起使用，所使用的引擎需要由AEM进行标识——即使使用AEM通用引擎也是如此：

* 电子商务引擎是支持接口的OSGi服 `CommerceService` 务

   * 引擎可以由服务属性 `commerceProvider` 区分

* AEM支 `Resource.adaptTo()` 持 `CommerceService` 和 `Product`

   * 实 `adaptTo` 现在资源的 `cq:commerceProvider` 层次结构中查找属性：

      * 如果找到，则使用该值过滤商务服务查找。
      * 如果找不到，则使用排名最高的商务服务。
   * 使 `cq:Commerce` 用混音，以便 `cq:commerceProvider` 可以将其添加到强类型资源。


* 该属 `cq:commerceProvider` 性还用于引用相应的商务工厂定义。

   * 例如，具有 `cq:commerceProvider` 值geometrixx的属性将与Day CQ Commerce Factory for Geometrixx-Outdoors()的 **OSGi配置相关联** -其中`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`参数也具有值 `commerceProvider``geometrixx`。
   * 此处还可以配置其他属性（如果适用并可用）。

在标准AEM安装中，需要特定实施，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx示例； 这包括通用API的最小扩展 |

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
>使用CRXDE Lite，您可以在AEM通用实现的产品组件中查看如何处理该问题：
>
>`/apps/geometrixx-outdoors/components/product`

### 会话处理 {#session-handling}

用于存储与客户购物车相关信息的会话。

CommerceSession ****:

* 拥有购 **物车**

   * 执行add/remove/etc
   * 在购物车上执行各种计算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 拥有订单数 **据** :

   `CommerceSession.getUserContext()`

* 可以使用 `updateOrder(Map<String, Object> delta)`
* 还拥有付 **款处** 理连接
* 还拥有履行 **连接** 。

### 架构 {#architecture}

#### 产品和变体的架构 {#architecture-of-product-and-variants}

一个产品可以有多个变体； 例如，它可能因颜色和／或大小而异。 产品必须定义驱动变化的属性； 我们用这些变 *型轴来定*&#x200B;义。

但是，并非所有属性都是变型轴。 变化也会影响其他属性； 例如，价格可能取决于大小。 Thesper properties cannot be selected by the shopper, and eso not be consured to variant axes.

每个产品和／或变体由资源表示，因此将1:1映射到存储库节点。 由此推论，特定产品和／或变体可以通过其路径唯一标识。

任何产品资源都可以用表示 `Product API`。 产品API中的大多数调用都是特定于变体的（尽管变体可能继承祖先的共享值），但也有列表变体集( `getVariantAxes()`如 `getVariants()`等)的调用。

>[!NOTE]
>
>实际上，变型轴由任何返回决定 `Product.getVariantAxes()` :
>
>* 对于通用实现，AEM从产品数据中的属性读取它( `cq:productVariantAxes`)
>
>
虽然产品（通常）可以有许多变型轴，但现成的产品组件只处理两个：
>
>1. `size`
>1. 再加一个

>
>   
通过产品引用的属性选 `variationAxis` 择此附加变体(通常适 `color` 用于Geometrixx Outdoors)。

#### 产品引用和PIM数据 {#product-references-and-pim-data}

一般而言：

* PIM数据位于 `/etc`

* 产品引用 `/content`。

产品变量和产品数据节点之间必须有1:1的映射。

产品引用还必须为呈现的每个变体提供一个节点，但不要求显示所有变体。 例如，如果产品具有S、M、L变量，则产品数据可能为：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

而“大而高”目录可能只包含：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最后，不需要使用产品数据。 您可以将所有产品数据放在目录引用下； 但是，如果不复制所有产品数据，您就无法真正拥有多个目录。

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

   * 产品节点不是非结构化的。
   * 产品节点可以是：

      * 参考，将产品数据存储在其他位置：

         * 产品引用包 `productData` 含一个属性，它指向产品数据(通常在 `/etc/commerce/products`下)。
         * 产品数据是分层的； 产品属性从产品数据节点的祖先继承。
         * 产品引用还可以包含本地属性，这些属性会覆盖在产品数据中指定的属性。
      * 产品本身：

         * 没有财 `productData` 产。
         * 本地保存所有属性（不包含productData属性）的产品节点直接从其自己的祖先继承产品属性。


* **AEM-generic产品结构**

   * 每个变体必须有其自己的叶节点。
   * 产品界面表示产品和变型，但相关存储库节点特定于它。
   * 产品节点描述产品属性和变型轴。

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

   * 执行 `CommerceSession` 添加、删除等操作。
   * The `CommerceSession` asso perces the various calculations on the cart.
   * The `CommerceSession` also applies vouchers and promotions that have fired to the cart.

* 虽然不是直接与购物车相关的， `CommerceSession` 但还必须提供目录定价信息（因为它拥有定价）

   * 定价可能包含多个修改量：

      * 数量折扣。
      * 不同货币。
      * 增值税免税。
   * 修饰符完全开放，具有以下界面：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在AEM-generic case carts中，购物车存储在ClientContext [中](/help/sites-administering/client-context.md)

**个性化**

* 个性化应始终通过ClientContext [推动](/help/sites-administering/client-context.md)。
* A ClientContext `/version/` of the cart is created in all cases:

   * 应使用该方法添加产 `CommerceSession.addCartEntry()` 品。

* 以下说明了ClientContext购物车中购物车信息的示例：

![chlimage_1-33](assets/chlimage_1-33a.png)

#### 结帐架构 {#architecture-of-checkout}

**购物车和订购数据**

这三 `CommerceSession` 个要素归其所有：

1. **购物车内容**

   购物车内容模式由API修复：

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

   但是，订单详细 *信息* 不由API修复：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**发运计算**

* 订购表单通常需要提供多种送货方式（和价格）。
* 价格可能基于订单的项目和详细信息，如权重和／或投放地址。
* The `CommerceSession` access to all the dependencies, so that is can be a symailly appricing as product pricing:

   * 船 `CommerceSession` 运定价。
   * 用 `updateOrder(Map<String, Object> delta)` 于检索／更新投放详细信息。

### 搜索定义 {#search-definition}

遵循标准服务API模型，电子商务项目提供一组与搜索相关的API，这些API可由单个商务引擎实现。

>[!NOTE]
>
>Currently, only the hybris engine implements the search API out-of-the-box.
>
>但是，搜索API是通用的，可以由每个CommerceService单独实现。
>
>因此，尽管提供的现成通用实现不实现此API，但您可以扩展它并添加搜索功能。

电子商务项目包含默认的搜索组件，位于：

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

这将利用搜索API来查询选定的商务引擎(请参 [阅电子商务引擎选择](#ecommerce-engine-selection)):

#### 搜索API {#search-api}

核心项目提供了几个通用类／帮助程序类：

1. `CommerceQuery`

   用于描述搜索查询(包含有关查询文本、当前页面、页面大小、排序和选定彩块化的信息)。 所有实现搜索API的电子商务服务都将接收此类的实例以执行其搜索。 可 `CommerceQuery` 以从请求对象()实例 `HttpServletRequest`化。

1. `FacetParamHelper`

   是一个实用程序类，它提供一种静态 `toParams` 方法——用于从一列表facet `GET` 和一个切换值生成参数字符串。 这在UI端很有用，您需要为每个facet的每个值显示一个超链接，这样当用户单击超链接时，相应的值将被切换(即，如果选择了该值，则会从查询中删除，否则会添加)。 这将考虑处理多值／单值彩块化、覆盖值等的所有逻辑。

搜索API的入口点是返 `CommerceService#search` 回对象的方 `CommerceResult` 法。 有关此主题的更多信息，请参阅API文档。

### 开发促销和优惠券 {#developing-promotions-and-vouchers}

* 优惠券:

   * A Voucher是使用网站控制台创建／编辑并存储在以下位置的基于页面的组件：

      `/content/campaigns`

   * Vouchers supply:

      * A voucher code(to be typed into the cart by the shopper)。
      * A voucher label(to be displayed after the shopper has entered it into the cart)。
      * A promotion path(which defines the action the voucher applies)。
   * 凭证没有其自己的开／关日期／时间，但使用其父活动的凭证。
   * 外部商务引擎还可以提供凭证； 这些要求至少：

      * 优惠券代码
      * 一种方 `isValid()` 法
   * The **Voucher** component( `/libs/commerce/components/voucher`)provides:

      * 凭证管理的呈现器； 这显示购物车中当前的所有凭证。
      * 用于管理（添加／删除）凭证的编辑对话框（表单）。
      * 添加／删除凭证至购物车／从购物车所需的操作。



* 促销活动:

   * 促销是使用网站控制台创建／编辑并存储在以下位置的基于页面的组件：

      `/content/campaigns`

   * 促销供应：

      * 优先级
      * 升级处理程序路径
   * 您可以将促销活动连接到活动以定义其开／关日期／时间。
   * 您可以将促销活动与体验关联，以定义其区段。
   * 未连接到体验的促销将不会自行触发，但仍可由Voucher触发。
   * 升级组件( `/libs/commerce/components/promotion`)包含：

      * promotion administration的renderers和dialogs
      * 用于渲染和编辑特定于升级处理程序的配置参数的子组件
   * 两个升级处理程序现已提供：

      * `DiscountPromotionHandler`，它应用购物车宽的绝对或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作伙伴产品也在购物车中，则应用产品绝对或百分比折扣
   * ClientContext解析 `SegmentMgr` 区段，ClientContext解析 `CartMgr` 促销。 将触发每个受至少一个已解析区段约束的促销。

      * Fired Promotions are sent back to the server an AJAX call to re-calculate the cart.
      * Fired Promotions(and added Vouchers)也显示在ClientContext面板中。




Adding/Removing a voucher from a cart is impeded by the `CommerceSession` API:

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

这样，The `CommerceSession` is responsibles for checking a voucher exists and if it can be applied or not. 这可能适用于仅在满足特定条件时才能应用的凭证； 例如，当总购物车价格大于$100时)。 如果凭证因任何原因无法应用，则 `addVoucher` 方法将引发异常。 此外， `CommerceSession` The is responsibles for updating the cart&#39;s price(s)after a voucher is added / removed.

类 `Voucher` 似Bean的类包含以下字段：

* 凭证代码
* 简短描述
* 引用指示折扣类型和值的相关促销

提 `AbstractJcrCommerceSession` 供的可以应用凭证。 类返回的凭证 `getVouchers()` 是包含 `cq:Page` jcr:content节点的实例，该节点具有以下属性（等）:

* `sling:resourceType` （字符串）-这需要 `commerce/components/voucher`

* `jcr:title` （字符串）-用于凭证的说明
* `code` （字符串）-用户必须输入以应用此凭证的代码
* `promotion` （字符串）-要应用的促销； 例如， `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促销处理程序是修改购物车的OSGi服务。 购物车将支持在界面中定义的多个挂 `PromotionHandler` 钩。

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
* `PerfectPartnerPromotionHandler` 如果产品合作伙伴也在购物车中，则应用产品绝对或百分比折扣
* `FreeShippingPromotionHandler` 应用免费送货

