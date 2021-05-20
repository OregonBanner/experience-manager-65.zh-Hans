---
title: 使用SAP进行开发Commerce Cloud
seo-title: 使用SAP进行开发Commerce Cloud
description: SAPCommerce Cloud集成框架包括一个与API的集成层
seo-description: SAPCommerce Cloud集成框架包括一个与API的集成层
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 0%

---

# 使用SAPCommerce Cloud{#developing-with-sap-commerce-cloud}进行开发

>[!NOTE]
>
>电子商务框架可与任何电子商务解决方案一起使用。 此处介绍的某些具体说明和示例将参考[hybris](https://www.hybris.com/)解决方案。

集成框架包括一个带有API的集成层。 这样，您就可以：

* 插入电子商务系统并将产品数据提取到AEM

* 构建AEM组件以实现独立于特定电子商务引擎的商务功能

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[还提](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 供了API文档。

提供了许多现成的AEM组件来使用集成层。 目前，这些是：

* 产品显示组件
* 购物车
* 结帐

为了搜索，提供了集成挂接，它允许您使用AEM搜索、电子商务系统的搜索、第三方搜索(如Search&amp;Promote)或其组合。

## 电子商务引擎选择{#ecommerce-engine-selection}

电子商务框架可与任何电子商务解决方案一起使用，所使用的引擎需要可由AEM识别：

* 电子商务引擎是支持`CommerceService`接口的OSGi服务

   * 引擎可通过`commerceProvider`服务属性进行区分

* AEM支持`CommerceService`和`Product`的`Resource.adaptTo()`

   * `adaptTo`实施会在资源的层次结构中查找`cq:commerceProvider`属性：

      * 如果找到，则使用值过滤商务服务查找。

      * 如果未找到，则使用排名最高的商务服务。
   * 使用`cq:Commerce` mixin，以便将`cq:commerceProvider`添加到强类型资源中。


* `cq:commerceProvider`属性还用于引用相应的商务工厂定义。

   * 例如，值为`hybris`的`cq:commerceProvider`属性将与&#x200B;**Day CQ Commerce Factory for Hybris**(com.adobe.cq.com.hybris.mpl.HybrisServiceFactory)的OSGi配置相关联 — 其中参数`commerceProvider`还具有值`hybris`。

   * 此处可以配置其他属性，如&#x200B;**目录版本**（如果适用且可用）。

请参阅以下示例：

| `cq:commerceProvider = geometrixx` | 在标准AEM安装中，需要特定实施；例如，geometrixx示例，其中包含对通用API的最小扩展 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris实施 |

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
>使用CRXDE Lite，您可以在hybris实施的产品组件中查看如何处理该事件：
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### 为hybris 4 {#developing-for-hybris}开发

eCommerce Integration Framework的hybris扩展已更新以支持Hybris 5，同时保持与Hybris 4的向后兼容性。

代码中的默认设置将针对Hybris 5进行调整。

要为Hybris 4开发，需要满足以下条件：

* 调用maven时，将以下命令行参数添加到命令

   `-P hybris4`

   它将下载预配置的Hybris 4分发并将其嵌入包`cq-commerce-hybris-server`中。

* 在OSGi配置管理器中：

   * 禁用Hybris 5对Default Response Parser服务的支持。

   * 确保Hybris Basic Authentication Handler服务的服务排名低于Hybris OAuth Handler服务。

### 会话处理{#session-handling}

hybris使用用户会话存储客户购物车等信息。 会话id在`JSESSIONID` cookie中从hybris返回，该cookie需要在后续请求时发送到hybris。 为避免将会话ID存储在存储库中，会将该会话ID编码为存储在购物者浏览器中的其他Cookie中。 将执行以下步骤：

* 在第一次请求时，不会对购物者的请求设置Cookie;因此，请求将发送到hybris实例以创建会话。

* 会话Cookie将从响应中提取，以新Cookie（例如`hybris-session-rest`）进行编码，并在对购物者的响应中设置。 需要在新Cookie中进行编码，因为原始Cookie仅对特定路径有效，否则在后续请求中将不会从浏览器发送回来。 路径信息还必须添加到Cookie的值中。

* 在后续请求中，将从`hybris-session-<*xxx*>` Cookie解码Cookie，并在用于从Hybris请求数据的HTTP客户端上设置Cookie。

>[!NOTE]
>
>当原始会话不再有效时，将创建新的匿名会话。

#### 商务会话 {#commercesession}

* 此会话“拥有”**购物车**

   * 执行添加/删除/等

   * 在购物车上执行各种计算；

      `commerceSession.getProductPrice(Product product)`

* 拥有&#x200B;*存储位置*，用于&#x200B;**order**&#x200B;数据

   `CommerceSession.getUserContext()`

* 还拥有&#x200B;**payment**&#x200B;处理连接

* 还拥有&#x200B;**fulfillment**&#x200B;连接

### 产品同步和发布{#product-synchronization-and-publishing}

在hybris中维护的产品数据需要在AEM中可用。 已实施以下机制：

* hybris作为信息源提供ID的初始加载。 此信息源可能有更新。
* hybris将通过信息源(哪些AEM轮询)提供更新信息。
* 当AEM使用产品数据时，它将将当前数据的请求发送回hybris（使用上次修改日期的条件获取请求）。
* 在混合中，可以以声明方式指定信息源内容。
* 将馈送结构映射到AEM内容模型时，会在AEM侧的馈送适配器中进行。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 导入器(b)用于在AEM中为目录初始设置页面树结构。
* hybris中的目录更改通过信息源指示给AEM，然后传播到AEM(b)

   * 已添加/删除/更改与目录版本有关的产品。

   * 产品已批准。

* hybris扩展提供轮询导入程序（“hybris”方案”），可将其配置为按指定的间隔（例如，每24小时指定间隔，以秒为单位）将更改导入AEM:

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

* AEM中的目录配置可识别&#x200B;**Staged**&#x200B;和&#x200B;**Online**&#x200B;目录版本。

* 在目录版本之间同步产品将需要（取消）激活相应的AEM页面(a、c)

   * 将产品添加到&#x200B;**Online**&#x200B;目录版本需要激活产品页面。

   * 删除产品需要停用。

* 在AEM(c)中激活页面时，需要勾选(b)，并且仅当

   * 产品位于产品页面的&#x200B;**Online**&#x200B;目录版本中。

   * 引用的产品可在&#x200B;**Online**&#x200B;目录版本中用于其他页面（例如促销活动页面）。

* 已激活的产品页面需要访问产品数据的&#x200B;**Online**&#x200B;版本(d)。

* AEM publish实例需要访问hybris以检索产品和个性化数据(d)。

### 架构 {#architecture}

#### 产品和变体的架构{#architecture-of-product-and-variants}

单个产品可以有多个变体；例如，它可能因颜色和/或大小而异。 产品必须定义驱动变量的属性；我们对这些&#x200B;*变体轴*&#x200B;进行术语。

但是，并非所有属性都是变型轴。 变化也会影响其他属性；例如，价格可能取决于规模。 购物者无法选择这些属性，因此不会将其视为变体轴。

每个产品和/或变体都由资源表示，因此将1:1映射到存储库节点。 由此可推论，特定产品和/或变体可以通过其路径唯一标识。

产品/变体资源并非始终包含实际的产品数据。它可能是其他系统（如hybris）上实际保存的数据的表示形式。 例如，产品描述、定价等不会存储在AEM中，而是会从电子商务引擎中实时检索。

任何产品资源都可以用`Product API`表示。 产品API中的大多数调用都是特定于变量的调用（尽管变量可能会继承父代的共享值），但也有一些调用列出了变量集（`getVariantAxes()`、`getVariants()`等）。

>[!NOTE]
>
>实际上，变化轴由`Product.getVariantAxes()`返回的任何值决定：
>* hybris为hybris实施定义它
>
>
虽然产品（通常）可以具有多个变体轴，但现成的产品组件仅处理两个：
>
>1. `size`
   >
   >
1. 再加一个
>
>
通过产品引用的`variationAxis`属性选择此其他变体(通常为`color`，用于Geometrixx Outdoors)。

#### 产品引用和产品数据{#product-references-and-product-data}

一般而言：

* 产品数据位于`/etc`下

* 和`/content`下的产品参考。

产品变体与产品数据节点之间必须存在1:1映射。

产品引用还必须具有每个显示的变体的节点，但不要求显示所有变体。 例如，如果产品具有S、M、L变量，则产品数据可能为：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

而“大而高”目录可能只有：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

最后，无需使用产品数据。 您可以将所有产品数据放在目录的引用下；但是，如果不复制所有产品数据，您就无法真正拥有多个目录。

**API**

#### com.adobe.cq.commerce.api.Product接口{#com-adobe-cq-commerce-api-product-interface}

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

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

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

   * 产品节点为`nt:unstructured`。

   * 产品节点可以是：

      * 将产品数据存储在其他位置的引用：

         * 产品引用包含`productData`属性，该属性指向产品数据（通常位于`/etc/commerce/products`下）。

         * 产品数据是分层的；产品属性继承自产品数据节点的祖先。

         * 产品引用还可以包含本地属性，这些属性会覆盖其产品数据中指定的属性。
      * 产品本身：

         * 没有`productData`属性。

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

#### 购物车的架构{#architecture-of-the-shopping-cart}

**组件**

* 购物车归`CommerceSession:`所有

   * `CommerceSession`执行添加/删除/等操作。
   * `CommerceSession`还会在购物车上执行各种计算。&quot;

* `CommerceSession`不直接与购物车相关，但还必须提供目录定价信息（因为它拥有定价）

   * 定价可能具有以下几个修改量：

      * 数量折扣。
      * 不同的货币。
      * 增值税免税。
   * 这些修饰符在以下界面中完全开放：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在hybris案例中，hybris服务器拥有购物车。
   * 在AEM-generic的用例中，购物车存储在[ClientContext](/help/sites-administering/client-context.md)中。

**个性化**

* 个性化应始终通过[ClientContext](/help/sites-administering/client-context.md)来驱动。
* 购物车的ClientContext`/version/`在所有情况下均会创建：

   * 应使用`CommerceSession.addCartEntry()`方法添加产品。

* 下面展示了ClientContext车中购物车信息的示例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 结帐的架构{#architecture-of-checkout}

**购物车和订购数据**

`CommerceSession`拥有三个元素：

1. 购物车内容
1. 定价
1. 订单详细信息

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

   但是，订单详细信息由API修复： *not*:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**装运计算**

* 订单通常需要显示多个送货选项（和价格）。
* 价格可能基于订单的项目和详细信息，如重量和/或交货地址。
* `CommerceSession`有权访问所有依赖项，因此可以采用与产品定价类似的方式处理它：

   * `CommerceSession`拥有发运定价。
   * 可以使用`updateOrder(Map<String, Object> delta)`检索/更新投放详细信息

>[!NOTE]
>
>您可以实施送货选择器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本质上讲，这可以是`foundation/components/form/radio`的副本，但对`CommerceSession`的回调有：
   >
   >
* 检查方法是否可用
>* 添加定价信息
>* 为了使购物者能够更新AEM中的订单页面（包括装运方法的超集以及描述它们的文本），同时仍具有显示相关`CommerceSession`信息的控件。


**付款处理**

* `CommerceSession`还拥有付款处理连接。

* 实施人员需要向`CommerceSession`实施添加特定调用（添加到其所选的支付处理服务）。

**订单履行**

* `CommerceSession`还拥有履行连接。
* 实施人员需要向`CommerceSession`实施添加特定调用（添加到其所选的支付处理服务）。

### 搜索定义{#search-definition}

遵循标准服务API模型，电子商务项目提供了一组可由单个商务引擎实施的与搜索相关的API。

>[!NOTE]
>
>目前，只有hybris引擎会实施现成的搜索API。
>
>但是，搜索API是通用的，可由每个CommerceService单独实施。

电子商务项目包含默认搜索组件，该组件位于：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

这利用搜索API查询选定的商务引擎（请参阅[电子商务引擎选择](#ecommerce-engine-selection)）：

#### 搜索API {#search-api}

核心项目提供了几个通用/帮助程序类：

1. `CommerceQuery`

   用于描述搜索查询（包含有关查询文本、当前页面、页面大小、排序和选定彩块化的信息）。 所有实施搜索API的电子商务服务都将接收此类的实例，以执行其搜索。 可以从请求对象(`HttpServletRequest`)实例化`CommerceQuery`。

1. `FacetParamHelper`

   是一个实用程序类，它提供一种静态方法 — `toParams` — 用于从facet列表和一个切换值生成`GET`参数字符串。 这在UI端非常有用，在UI端，您需要为每个facet的每个值显示一个超链接，这样当用户单击该超链接时，相应的值即会被切换（即，如果已选择该值，则会从查询中删除，否则会添加）。 这会处理处理多个/单值彩块化、覆盖值等的所有逻辑。

搜索API的入口点是返回`CommerceResult`对象的`CommerceService#search`方法。 有关此主题的更多信息，请参阅[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)。

### 用户集成{#user-integration}

AEM与各种电子商务系统之间提供集成。 这需要一种策略来在各种系统之间同步购物者，以便AEM特定的代码只能了解AEM，反之亦然：

* 身份验证

   AEM假定为&#x200B;*仅* web前端，因此执行&#x200B;*所有*&#x200B;身份验证。

* Hybris中的帐户

   AEM在hybris中为每个购物者创建相应的(下属)帐户。 此帐户的用户名与AEM用户名相同。 加密随机密码是自动生成的，并存储（加密）在AEM中。

#### 预先存在的用户{#pre-existing-users}

AEM前端可位于现有hybris实施的前面。 此外，还可以将hybris引擎添加到现有AEM安装中。 为此，系统必须能够妥善处理任一系统中的现有用户：

* AEM -> hybris

   * 登录到hybris时，如果AEM用户不存在：

      * 使用加密随机密码创建新hybris用户
      * 将hybris用户名存储在AEM用户的用户目录中
   * 请参阅: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 登录AEM时，如果系统识别用户：

      * 尝试使用提供的username/pwd登录hybris
      * 如果成功，请在AEM中使用相同的密码创建新用户(AEM特定的salt将生成AEM特定的哈希)
   * 上述算法在Sling `AuthenticationInfoPostProcessor`中实施

      * 请参阅: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自定义导入进程{#customizing-the-import-process}

要基于现有功能构建自定义导入处理程序：

* 必须实现`ImportHandler`接口

* 可以扩展`DefaultImportHandler`。

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

对于导入程序要识别的自定义处理程序，必须指定值大于0的`service.ranking`属性；例如。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
