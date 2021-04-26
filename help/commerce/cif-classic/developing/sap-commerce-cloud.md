---
title: 使用SAPCommerce Cloud进行开发
seo-title: 使用SAPCommerce Cloud进行开发
description: SAPCommerce Cloud集成框架包括一个带API的集成层
seo-description: SAPCommerce Cloud集成框架包括一个带API的集成层
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 0%

---

# 使用SAPCommerce Cloud{#developing-with-sap-commerce-cloud}进行开发

>[!NOTE]
>
>电子商务框架可与任何电子商务解决方案一起使用。 此处处理的特定信息和示例将引用[hybris](https://www.hybris.com/)解决方案。

该集成框架包含一个带有API的集成层。 这允许您：

* 插入电子商务系统并将产品数据拉入AEM

* 构建AEM组件，以便与特定eCommerce引擎无关地获取商务功能

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API文](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 档也可用。

为使用集成层提供了许多现成的AEM组件。 目前有：

* 产品展示组件
* 购物车
* 签出

对于搜索，提供了允许您使用AEM搜索、电子商务系统搜索、第三方搜索(类似Search&amp;Promote)或其组合的集成挂接。

## 电子商务引擎选择{#ecommerce-engine-selection}

电子商务框架可与任何电子商务解决方案一起使用，所使用的引擎需要由AEM识别：

* 电子商务引擎是支持`CommerceService`接口的OSGi服务

   * 引擎可以通过`commerceProvider`服务属性进行区分

* AEM支持`CommerceService`和`Product`的`Resource.adaptTo()`

   * `adaptTo`实现在资源的层次结构中查找`cq:commerceProvider`属性：

      * 如果找到，则使用该值过滤商务服务查找。

      * 如果未找到，则使用排名最高的商务服务。
   * 使用`cq:Commerce`混音，以便将`cq:commerceProvider`添加到强类型资源。


* `cq:commerceProvider`属性还用于引用相应的商务工厂定义。

   * 例如，`cq:commerceProvider`属性(with the value `hybris`)将关联到&#x200B;**Day CQ Commerce Factory for Hybris**(com.adobe.cq.com.hymerce.impl.HybrisServiceFactory) — 其中参数`commerceProvider`也包含值`hybris`。

   * 此处可以配置其他属性，如&#x200B;**目录版本**（如果适用且可用）。

请参阅以下示例：

| `cq:commerceProvider = geometrixx` | 在标准AEM安装中，需要具体实施；例如，geometrixx示例，其中包括对通用API的最小扩展 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris implementation |

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
>Using CRXDE Lite you can see how this is handled in the product component for the hybris implementation:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Developing for hybris 4 {#developing-for-hybris}

The hybris extension of the eCommerce Integration Framework has been updated to support Hybris 5, while maintaining backward compatibility with Hybris 4.

The default settings in the code are tuned for Hybris 5.

To develop for Hybris 4 the following is required:

* 在调用maven时，将以下命令行参数添加到命令

   `-P hybris4`

   它下载预配置的Hybris 4分发并将其嵌入捆绑`cq-commerce-hybris-server`中。

* 在OSGi配置管理器中：

   * 对Default Response Parser服务禁用Hybris 5支持。

   * 确保Hybris Basic Authentication Handler服务的服务级别低于Hybris OAuth Handler服务。

### 会话处理{#session-handling}

hybris uses a user session to store information such the customer&#39;s shopping cart. The session id is returned from hybris in a `JSESSIONID` cookie that needs to be sent on the extensed requests to hybris. 要避免将会话ID存储在存储库中，会将其编码到存储在购物者浏览器中的另一个Cookie中。 将执行以下步骤：

* On the first request no cookie is set on the shopper&#39;s request;so a request is sent to the hybris instance to create a session.

* 会话Cookie会从响应中提取，编码为新Cookie（例如，`hybris-session-rest`），并在对购物者的响应时设置。 需要在新Cookie中进行编码，因为原始Cookie仅对特定路径有效，否则在后续请求中不会从浏览器发回。 路径信息还必须添加到Cookie的值中。

* 在后续请求中，将从`hybris-session-<*xxx*>` cookies中解码cookie，并在用于从hybris请求数据的HTTP客户端上进行设置。

>[!NOTE]
>
>当原始会话不再有效时，将创建一个新的匿名会话。

#### CommerceSession {#commercesession}

* 此会话“拥有”**购物车**

   * 执行add/remove/etc

   * 在购物车上执行各种计算；

      `commerceSession.getProductPrice(Product product)`

* 拥有&#x200B;**order**&#x200B;数据的&#x200B;*存储位置*

   `CommerceSession.getUserContext()`

* 还拥有&#x200B;**payment**&#x200B;处理连接

* 还拥有&#x200B;**履行**&#x200B;连接

### 产品同步和发布{#product-synchronization-and-publishing}

Product data this maintained in hybris needs to be available in AEM. 已执行以下机制：

* An initial load of IDs is provided by hybris as a feed. 此源可能有更新。
* hybris will supply update information via a feed(wich AEM polls)。
* When AEM is using product data， it will send requests back to hybris for the current data(conditional get request using last modified date)。
* On hybris is possible to specify feed contents in a declative way.
* 将源结构映射到AEM内容模型时，会在AEM端的源适配器中发生。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 导入程序(b)用于AEM目录中页面树结构的初始设置。
* Catalog changes in hybris are isaded to AEM via a feed， thes then propagate to AEM(b)

   * 产品已添加/删除/更改目录版本。

   * 已批准产品。

* The hybris extension provides a polling importer(&quot;hybris&quot; scheme&quot;), which can be configured to import changes into AEM at a specified interval(example， ever 24 here the interval is specified in seconds):

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

* 在目录版本之间同步产品需要对相应的AEM页面(a， c)进行(de-)激活

   * 将产品添加到&#x200B;**联机**&#x200B;目录版本需要激活产品页面。

   * 删除产品需要取消激活。

* 在AEM(c)中激活页面需要选中(b)项，仅在

   * 该产品位于产品页面的&#x200B;**Online**&#x200B;目录版本中。

   * 引用的产品在&#x200B;**Online**&#x200B;目录版本中可用于其他页面(例如活动页面)。

* 已激活的产品页面需要访问产品数据的&#x200B;**Online**&#x200B;版本(d)。

* AEM publish instance requires access to hybris for the retrieval of product and personalized data(d)。

### 架构 {#architecture}

#### 产品和变体的架构{#architecture-of-product-and-variants}

一个产品可以有多种变体；例如，它可能因颜色和/或大小而异。 产品必须定义哪些属性驱动变化；我们将这些&#x200B;*变型轴*&#x200B;术语。

但是，并非所有属性都是变型轴。 变化也会影响其他属性；例如，价格可能取决于大小。 These properties cannot be selected by the shopper and there are not be consured variant axes.

每个产品和/或变体由资源表示，因此将1:1映射到存储库节点。 由此推论，特定产品和/或变体可以通过其路径唯一标识。

The product/variant resource does not always hold the actual product dataIt might be representation of data activally held on another system(suchybris)。 例如，产品说明、定价等不存储在AEM中，而是从电子商务引擎实时检索。

任何产品资源都可以用`Product API`表示。 产品API中的大多数调用都特定于变量（尽管变量可能继承祖代的共享值），但也有列表变量集（`getVariantAxes()`、`getVariants()`等）的调用。

>[!NOTE]
>
>实际上，变型轴由`Product.getVariantAxes()`返回的任何值决定：
>* hybris defines it for hybris implementation
>
>
虽然产品（一般）可以有许多变型轴，但现成的产品组件仅处理两个：
>
>1. `size`
   >
   >
1. 加上
>
>
通过产品引用的`variationAxis`属性选择此附加变体(通常`color`用于Geometrixx Outdoors)。

#### 产品引用和产品数据{#product-references-and-product-data}

一般而言：

* 产品数据位于`/etc`下

* 和`/content`下的产品引用。

产品变体和产品数据节点之间必须有1:1映射。

产品引用还必须为呈现的每个变体有一个节点，但不要求显示所有变体。 例如，如果某个产品具有S、M、L变量，则产品数据可能为：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

而“Big and Tall”目录可能仅包含：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

最后，无需使用产品数据。 您可以将所有产品数据放在目录的引用下；但是，如果不复制所有产品数据，您就无法真正拥有多个目录。

**API**

#### com.adobe.cq.commerce.api.Product interface {#com-adobe-cq-commerce-api-product-interface}

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

      * 参考，将产品数据存储在其他位置：

         * 产品引用包含`productData`属性，该属性指向产品数据（通常位于`/etc/commerce/products`下）。

         * 产品数据是分层的；产品属性是从产品数据节点的祖先继承的。

         * 产品引用还可以包含本地属性，这些属性会覆盖在产品数据中指定的属性。
      * 产品本身：

         * 没有`productData`属性。

         * 在本地保存所有属性（不包含productData属性）的产品节点直接从其自己的祖先继承产品属性。


* **AEM-generic产品结构**

   * 每个变体都必须具有自己的叶节点。

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

#### 购物车的架构{#architecture-of-the-shopping-cart}

**组件**

* 购物车归`CommerceSession:`所有

   * `CommerceSession`执行add/remove/etc。
   * `CommerceSession`还对购物车执行各种计算。&quot;

* 虽然不直接与购物车相关，`CommerceSession`还必须提供目录定价信息（因为它拥有定价）

   * 定价可能有以下几种修改量：

      * 数量折扣。
      * 不同的货币。
      * 增值税免税。
   * 这些修饰符完全开放，其界面如下：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * In the hybris case， the hybris server owns the cart.
   * 在AEM-generic案例中，购物车存储在[ClientContext](/help/sites-administering/client-context.md)中。

**个性化**

* 个性化应始终通过[ClientContext](/help/sites-administering/client-context.md)来驱动。
* AClientContext`/version/` of the cart is created in all cases:

   * 应使用`CommerceSession.addCartEntry()`方法添加产品。

* 以下说明了ClientContext车中的购物车信息示例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 结帐{#architecture-of-checkout}的架构

**购物车和订购数据**

`CommerceSession`拥有三个元素：

1. 购物车内容
1. 定价
1. 订单详细信息

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

   但是，订单详细信息&#x200B;*不是*&#x200B;由API修复：

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**发运计算**

* 订购表单通常需要提供多种送货方式（和价格）。
* 价格可能基于订单的项目和详细信息，如权重和/或投放地址。
* `CommerceSession`可以访问所有依赖项，因此可以采用与产品定价类似的方式处理它：

   * `CommerceSession`拥有送货价格。
   * 可以使用`updateOrder(Map<String, Object> delta)`检索/更新投放详细信息

>[!NOTE]
>
>您可以实施一个发运选择器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本质上，这可以是`foundation/components/form/radio`的副本，但对`CommerceSession`的进行了回调：
   >
   >
* 检查方法是否可用
>* 添加定价信息
>* 要使购物者能够更新AEM中的订单页（包括发运方法的超集以及描述它们的文本），同时仍具有显示相关`CommerceSession`信息的控件。


**付款处理**

* `CommerceSession`还拥有付款处理连接。

* 实施者需要向`CommerceSession`实施中添加特定呼叫（到其所选付款处理服务）。

**订单履行**

* `CommerceSession`还拥有实施连接。
* 实施者需要向`CommerceSession`实施添加特定呼叫（到他们选择的付款处理服务）。

### 搜索定义{#search-definition}

遵循标准服务API模型，电子商务项目提供一组可由单个商务引擎实现的与搜索相关的API。

>[!NOTE]
>
>Currently， only the hybris engine implements the search API out-of-the-box.
>
>但是，搜索API是通用的，可以由每个CommerceService单独实现。

电子商务项目包含默认的搜索组件，位于：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

这利用搜索API来查询选定的商务引擎（请参阅[电子商务引擎选择](#ecommerce-engine-selection)）：

#### 搜索API {#search-api}

核心项目提供了几个通用/帮助类：

1. `CommerceQuery`

   用于描述搜索查询(包含有关查询文本、当前页面、页面大小、排序和选定彩块化的信息)。 所有实现搜索API的电子商务服务都将接收此类的实例以执行其搜索。 可以从请求对象(`HttpServletRequest`)实例化`CommerceQuery`。

1. `FacetParamHelper`

   是一个实用程序类，它提供一种静态方法 — `toParams` — 用于从facet列表和一个切换值生成`GET`参数字符串。 这在UI端很有用，您需要为每个facet的每个值显示一个超链接，这样当用户单击超链接时，相应的值即被切换(即，如果选择了该值，则从查询中删除，否则会添加)。 这会处理处理多值/单值彩块化、覆盖值等的所有逻辑。

搜索API的入口点是返回`CommerceResult`对象的`CommerceService#search`方法。 有关此主题的详细信息，请参阅[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)。

### 用户集成{#user-integration}

AEM与各种电子商务系统之间提供集成。 这需要一种在不同系统之间同步购物者的策略，这样AEM特定的代码就只能了解AEM，反之亦然：

* 身份验证

   AEM假定为&#x200B;*仅* web前端，因此执行&#x200B;*all*&#x200B;身份验证。

* Accounts in Hybris

   AEM creates a ecopote(下属)account in hybris for each shopper 此帐户的用户名与AEM用户名相同。 密码随机密码是自动生成并存储在AEM中（加密）的。

#### 预存用户{#pre-existing-users}

A AEM front-end can be plocised in front of an existing hybris implementation. Aso a hybris engine can be added to an existing AEM installation. 为此，系统必须能够正常处理任一系统中的现有用户：

* AEM -> hybris

   * When logging in to hybris， if the AEM user does not already exist:

      * create new hybris user with a cryptographical random password
      * store the hybris username in the user directory of the AEM user
   * 请参阅: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 登录到AEM时，如果系统识别用户：

      * attemt log in to hybris with supplied username/pwd
      * 如果成功，请在AEM中使用相同的口令创建新用户(AEM特定的salt将导致AEM特定的哈希)
   * 上述算法在Sling `AuthenticationInfoPostProcessor`中实现

      * 请参阅: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自定义导入进程{#customizing-the-import-process}

要在现有功能的基础上构建自定义导入处理程序：

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

要使导入程序识别您的自定义处理程序，它必须指定值大于0的`service.ranking`属性；例如。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
