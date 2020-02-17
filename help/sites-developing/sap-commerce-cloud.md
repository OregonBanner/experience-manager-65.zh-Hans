---
title: 使用SAP Commerce cloud进行开发
seo-title: 使用SAP Commerce cloud进行开发
description: SAP Commerce cloud集成框架包括一个包含API的集成层
seo-description: SAP Commerce cloud集成框架包括一个包含API的集成层
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 96dc0c1a-b21d-480a-addf-c3d0348bd3ad
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 使用SAP Commerce cloud进行开发 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>电子商务框架可与任何电子商务解决方案一起使用。 此处处理的某些特定信息和示例将引用 [hybris](https://www.hybris.com/) solution。

该集成框架包括一个带有API的集成层。 这允许您：

* 插入电子商务系统并将产品数据拉入AEM
* 构建AEM组件，使其能够独立于特定的eCommerce引擎进行商务功能

![chlimage_1-11](assets/chlimage_1-11a.png)

>[!NOTE]
>
>[还提供API文档](/help/sites-developing/ecommerce.md#api-documentation) 。

为使用集成层提供了许多现成的AEM组件。 目前有：

* 产品展示组件
* 购物车
* 结帐

对于搜索，会提供一个集成挂钩，允许您使用AEM搜索、电子商务系统搜索、第三方搜索（如Search&amp;Promote）或其组合。

## 电子商务引擎选择 {#ecommerce-engine-selection}

电子商务框架可与任何电子商务解决方案一起使用，所使用的引擎需要由AEM识别：

* eCommerce Engine是支持界面的OSGi服 `CommerceService` 务

   * 可以通过服务属性来区分 `commerceProvider` 引擎

* AEM支持 `Resource.adaptTo()` 和 `CommerceService``Product`

   * 实 `adaptTo` 现在资源的层 `cq:commerceProvider` 次结构中查找属性：

      * 如果找到，则使用该值过滤商务服务查找。
      * 如果找不到，则使用排名最高的商务服务。
   * 使 `cq:Commerce` 用混音，以便 `cq:commerceProvider` 将其添加到强类型资源。


* 该属 `cq:commerceProvider` 性还用于引用相应的商务工厂定义。

   * 例如，具有 `cq:commerceProvider` 值的属性 `hybris` 将关联到 **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory)的OSGi配置——其中参数也 `commerceProvider` 有值 `hybris`。

   * 此处可以配置其他属性， **如目录版本** （如果适用且可用）。

请参阅以下示例：

| `cq:commerceProvider = geometrixx` | 在标准AEM安装中，需要特定实施；例如，geometrixx示例，其中包括对通用API的最小扩展 |
|---|---|
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
>使用CRXDE Lite，您可以查看this is how handed in the product component for the hybris implementation:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Developing for hybris 4 {#developing-for-hybris}

The hybris extension of the eCommerce Integration Framework has been updated to support Hybris 5, while maintaining backpatibility with Hybris 4.

代码中的默认设置为tuned for Hybris 5。

要develop for Hybris 4，请执行以下操作：

* 在调用maven时，将以下命令行参数添加到命令

   `-P hybris4`

   它下载预配置的Hybris 4分发并将其嵌入bundle:

   ```
   cq-commerce-hybris-server
   ```

* 在OSGi配置管理器中：

   * 禁用Hybris 5对Default Response Parser服务的支持。
   * 确保Hybris Basic Authentication Handler服务的服务级别低于Hybris OAuth Handler服务。

### 会话处理 {#session-handling}

hybris使用用户会话来存储诸如客户购物车等信息。 session id is returned from hybris in a `JSESSIONID` cookie that needs to be sent on extansed requests to hybris. 为避免将会话ID存储在存储库中，会话ID将编码到存储在购物者浏览器中的另一个Cookie中。 将执行以下步骤：

* 第一个请求时，不会对购物者的请求设置Cookie;so a request is sent to the hybris instance to create a session.
* 会话cookies从响应中提取，编码为新cookie(例如， `hybris-session-rest`)，并在对购物者的响应时设置。 新Cookie中的编码是必需的，因为原始Cookie仅对特定路径有效，否则在后续请求中不会从浏览器发回。 路径信息还必须添加到cookie的值中。
* 在后续请求中，cookies从 `hybris-session-<*xxx*>` cookies解码并在用于从hybris请求数据的HTTP客户端上设置。

>[!NOTE]
>
>当原始会话不再有效时，将创建一个新的匿名会话。

#### CommerceSession {#commercesession}

* 此会话“拥有”购 **物车**

   * 执行add/remove/etc
   * 在购物车上执行各种计算；

      `commerceSession.getProductPrice(Product product)`

* 拥有订 *单数据的存* 储位置 ****

   `CommerceSession.getUserContext()`

* 还拥有付款 **处理连** 接
* 还拥有履行 **连接** 。

### 产品同步和发布 {#product-synchronization-and-publishing}

hybris中维护的产品数据需要在AEM中可用。 实施了以下机制：

* An initial load of IDs is provided by hybris as a feed. 此源可能有更新。
* hybris将通过feed(which AEM pols)提供更新信息。
* 当AEM使用产品数据时，它将请求发送回hybris，以获取当前数据（条件获取请求，使用上次修改日期）。
* 在hybris上，可以以声明性方式指定feed内容。
* 将源结构映射到AEM内容模型会在AEM端的源适配器中发生。

![chlimage_1-12](assets/chlimage_1-12a.png)

* 导入程序(b)用于在AEM中为目录初始设置页面树结构。
* hybris中的目录更改通过源指示给AEM，然后这些更改传播到AEM(b)

   * Product added/deleted/changed for catalog version.
   * 已批准产品。

* The hybris extension provides a polling importer(&quot;hybris&quot; scheme&quot;), which can be configured to import changes into AEM at a specified interval（example, example，每隔24小时，其中间隔以秒为单位指定）:

   * 
      ```
      http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
       {
       * "jcr:mixinTypes": ["cq:PollConfig"],
       * "enabled": true,
       * "source": "hybris:outdoors",
       * "jcr:primaryType": "cq:PageContent",
       * "interval": 86400
       }
      ```

* AEM中的目录配置可识别 **分阶段****和联** 机目录版本。

* 在目录版本之间同步产品需要（取消）激活相应的AEM页面(a, c)

   * 将产品添加到 **Online** Catalog版本需要激活产品页面。
   * 删除产品需要取消激活。

* 在AEM(c)中激活页面需要检查(b)，并且仅当

   * 产品位于产品页 **面的Online** Catalog版本中。
   * 引用的产品在其他页 **面** （例如营销活动页面）的在线目录版本中可用。

* 已激活的产品页面需要访问产品数据的 **联机** 版本(d)。

* AEM publish实例需要访问hybris，以检索产品和个性化数据(d)。

### 架构 {#architecture}

#### 产品和变体的架构 {#architecture-of-product-and-variants}

一个产品可以有多个变体；例如，它可能因颜色和／或大小而异。 产品必须定义驱动变化的属性；我们用这些变 *型轴来定*。

但是，并非所有属性都是变型轴。 变化也会影响其他属性；例如，价格可能取决于大小。 这些属性不能由购物者选择，因此不被视为变体轴。

每个产品和／或变体由资源表示，因此将1:1映射到存储库节点。 由此推论，特定产品和／或变体可以通过其路径唯一标识。

product/variant resource does not always hold the actual product dataIt might be representation of data inther system(suchybris)。 例如，产品描述、定价等不存储在AEM中，而是从电子商务引擎实时检索。

任何产品资源都可以用表示 `Product API`。 产品API中的大多数调用都是特定于变量的（尽管变量可能继承祖代的共享值），但也有列出变量集( `getVariantAxes()`、 `getVariants()`等)的调用。

>[!NOTE]
>
>实际上，变型轴由任何返回决定 `Product.getVariantAxes()` :
>
>* hybris defines it for hybris implementation
>
>
虽然产品（通常）可以有许多变体轴，但现成的产品组件只处理两个：
>
>1. `size`
   >
   >
1. 再加一个
   >   通过产品引用的属性(通 `variationAxis` 常用于Geometrixx Outdoors)选择 `color` 此附加变体。
>



#### 产品引用和产品数据 {#product-references-and-product-data}

一般而言：

* 产品数据位于 `/etc`

* 和产品引用 `/content`。

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

最后，无需使用产品数据。 您可以将所有产品数据放在目录中引用下；但是，如果不复制所有产品数据，您就无法真正拥有多个目录。

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

* **常规存储机制**

   * 产品节点为nt:unstructured。
   * 产品节点可以是：

      * 引用，将产品数据存储在其他位置：

         * 产品引用包含 `productData` 一个属性，该属性指向产品数据(通常在下 `/etc/commerce/products`)。
         * 产品数据是分层的；产品属性从产品数据节点的祖先继承。
         * 产品引用还可以包含本地属性，这些属性将覆盖在产品数据中指定的属性。
      * 产品本身：

         * 没有财 `productData` 产。
         * 本地保存所有属性（不包含productData属性）的产品节点直接从其自己的祖先继承产品属性。


* **AEM-generic产品结构**

   * 每个变体都必须有其自己的叶节点。
   * 产品界面表示产品和变体，但相关存储库节点特定于它。
   * 产品节点描述产品属性和变体轴。

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

   * 执行 `CommerceSession` 添加／删除／等操作。
   * The `CommerceSession` asso perces the various calculations on the cart.&quot;

* 虽然不直接与购物车相关，但 `CommerceSession` 必须提供目录定价信息（因为它拥有定价）

   * 定价可能包含多个修改量：

      * 数量折扣。
      * 不同的货币。
      * 增值税免税。
   * 这些修饰符完全开放，并具有以下界面：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在hybris case中， the hybris server owns the cart.
   * 在AEM通用型案例购物车中，购物车存储在 [ClientContext中](/help/sites-administering/client-context.md)。

**个人信息**

* 个性化应始终通过 [ClientContext驱动](/help/sites-administering/client-context.md)。
* 在所有情 `/version/` 况下，都会创建购物车的ClientContext:

   * 应使用该方法添加产 `CommerceSession.addCartEntry()` 品。

* 以下说明了ClientContext购物车中购物车信息的示例：

![chlimage_1-13](assets/chlimage_1-13a.png)

#### 结帐架构 {#architecture-of-checkout}

**购物车和订单数据**

The `CommerceSession` own the 3 elements:

1. 购物车内容
1. 定价
1. 订单详细信息

1. **购物车内容**

   购物车内容架构由API修复：

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

   但是，订单详细信 *息不* 由API修复：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**送货计算**

* 订单表单通常需要提供多个送货选项（和价格）。
* 价格可能基于订单的项目和详细信息，如重量和／或交货地址。
* The access `CommerceSession` access to all the dependiences, so the access a limally as product pricing:

   * The own `CommerceSession` shipping pricing.
   * 可以使用 `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>您可以实施发运选择器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本质上，这可以是副本， `foundation/components/form/radio`但会回调以下对象 `CommerceSession` :
   >
   >
* 检查方法是否可用
>* 添加定价信息
>* 要使购物者能够更新AEM中的订单页面（包括送货方法的超集以及描述它们的文本），同时仍具有显示相关信息的控 `CommerceSession` 制权。


**付款处理**

* The `CommerceSession` allown the payment processing connection.
* 实施者需要向实施添加特定呼叫（到他们选择的支付处理服务） `CommerceSession` 。

**订单履行**

* 实 `CommerceSession` 施连接也归Adobe所有。
* 实施者需要向实施中添加特定呼叫（到他们选择的支付处理服务） `CommerceSession` 。

### 搜索定义 {#search-definition}

遵循标准服务API模型，电子商务项目提供一组可由单个商务引擎实现的与搜索相关的API。

>[!NOTE]
>
>当前，仅hybris引擎实现搜索API out-of-the-box。
>
>但是，搜索API是通用的，每个CommerceService都可以单独实现。

电子商务项目包含默认的搜索组件，位于：

`/libs/commerce/components/search`

![chlimage_1-14](assets/chlimage_1-14a.png)

这利用搜索API查询选定的商务引擎(请参阅 [eCommerce Engine选择](#ecommerce-engine-selection)):

#### 搜索API {#search-api}

核心项目提供了几个通用／帮助类：

1. `CommerceQuery`

   用于描述搜索查询（包含有关查询文本、当前页面、页面大小、排序和选定彩块化的信息）。 所有实现搜索API的电子商务服务都将接收此类的实例以执行其搜索。 可 `CommerceQuery` 以从请求对象( `HttpServletRequest`)实例化。

1. `FacetParamHelper`

   是一个实用程序类，它提供一种静态方法- `toParams` -用于从facet列表和一个切换的 `GET` 值生成参数字符串。 这在UI端很有用，您需要为每个facet的每个值显示一个超链接，这样当用户单击该超链接时，相应的值将被切换（即，如果选择了该值，则从查询中删除它，否则将添加）。 这将考虑处理多／单值彩块化、覆盖值等的所有逻辑。

搜索API的入口点是返回 `CommerceService#search` 对象的方 `CommerceResult` 法。 有关此主 [题的更多信息](/help/sites-developing/ecommerce.md#api-documentation) ，请参阅API文档。

### 用户集成 {#user-integration}

AEM与各种电子商务系统之间提供集成。 这需要一种在不同系统之间同步购物者的策略，以便AEM特定代码只能了解AEM，反之亦然：

* 身份验证

   假定AEM是唯一的 *Web前端* ，因此执行所 *有身份验证* 。

* 从帐户

   AEM为每个购物者在hybris中创建从帐户。 从帐户的用户名与AEM用户名相同。 密码随机密码是自动生成的，并在AEM中存储（加密）。

#### 预先存在的用户 {#pre-existing-users}

AEM前端可定位在现有hybris实施的前面。 此外，hybris引擎可添加到现有AEM安装。 为此，系统必须能够妥善地处理任一系统中的现有用户：

* AEM -> hybris

   * 登录到hybris时，如果AEM用户不存在：

      * 使用加密随机密码创建新的hybris用户
      * store hybris username in the user directory of the AEM user
   * See: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 登录AEM时，如果系统识别用户：

      * attempt in to hybris with supplied username/pwd
      * 如果成功，请在AEM中使用相同的口令创建新用户（AEM特定的salt将导致AEM特定的哈希）
   * 在Sling中实现了上述算法 `AuthenticationInfoPostProcessor`

      * See: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自定义导入过程 {#customizing-the-import-process}

要在现有功能的基础上构建自定义导入处理程序：

* 必须实现接 `ImportHandler` 口

* 可以扩展 `DefaultImportHandler`

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

要使导入程序识别您的自定义处理程序，它必须指 `service.ranking`定值大于0的属性；例如：

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler {
    ...
}
```

