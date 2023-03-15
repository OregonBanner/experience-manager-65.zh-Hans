---
title: 使用SAPCommerce Cloud进行开发
seo-title: Developing with SAP Commerce Cloud
description: SAPCommerce Cloud集成框架包括一个集成层和API
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

# 使用SAPCommerce Cloud进行开发 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>电子商务框架可与任何电子商务解决方案一起使用。 此处介绍的某些细节和示例将参考 [hybris](https://www.hybris.com/) 解决方案。

集成框架包括带有API的集成层。 这允许您：

* 插入电子商务系统并将产品数据提取到AEM中

* 为独立于特定电子商务引擎的商务功能构建AEM组件

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可用。

提供了许多现成的AEM组件以使用集成层。 目前，这些解决方案包括：

* 产品展示组件
* 购物车
* 结账

为了搜索，提供了一种集成挂钩，它允许您使用AEM搜索、电子商务系统搜索、第三方搜索或它们的组合。

## 电子商务引擎选择 {#ecommerce-engine-selection}

电子商务框架可与任何电子商务解决方案一起使用，使用的引擎需要由AEM识别：

* 电子商务引擎是支持 `CommerceService` 界面

   * 可以通过以下方式识别引擎 `commerceProvider` 服务属性

* AEM支持 `Resource.adaptTo()` 对象 `CommerceService` 和 `Product`

   * 此 `adaptTo` 实施会查找 `cq:commerceProvider` 资源层次结构中的属性：

      * 如果找到，则使用值筛选Commerce服务查找。

      * 如果未找到，则使用排名最高的商务服务。
   * A `cq:Commerce` mixin用于 `cq:commerceProvider` 可以添加到强类型资源中。


* 此 `cq:commerceProvider` 属性还用于引用相应的商务工厂定义。

   * 例如， `cq:commerceProvider` 具有值的属性 `hybris` 将与的OSGi配置相关联 **Day CQ Commerce Factory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) — 其中参数 `commerceProvider` 还具有值 `hybris`.

   * 下面是其他属性，例如 **目录版本** 可以配置（在适当和可用时）。

请参阅以下示例：

| `cq:commerceProvider = geometrixx` | 在标准AEM安装中，需要特定的实施；例如，geometrixx示例，其中包含通用API的最小扩展 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris实现 |

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
>通过使用CRXDE Lite，您可以看到在Hybris实施的产品组件中如何处理这种情况：
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### 针对hybris 4进行开发 {#developing-for-hybris}

电子商务集成框架的hybris扩展已更新，以支持Hybris 5，同时保持与Hybris 4的向后兼容性。

代码中的默认设置是针对Hybris 5调整的。

要为Hybris 4开发，需要满足以下条件：

* 调用maven时，将以下命令行参数添加到命令中

   `-P hybris4`

   它下载预配置的Hybris 4分发并将其嵌入捆绑包中 `cq-commerce-hybris-server`.

* 在OSGi配置管理器中：

   * 禁用默认响应分析器服务的Hybris 5支持。

   * 确保Hybris基本身份验证处理程序服务的服务排名低于Hybris OAuth处理程序服务。

### 会话处理 {#session-handling}

hybris使用用户会话来存储信息，例如客户的购物车。 会话ID从hybris返回 `JSESSIONID` 后续请求中需要发送到hybris的Cookie。 为避免将会话id存储在存储库中，会将其编码到购物者的浏览器中存储的另一个Cookie中。 执行以下步骤：

* 在第一个请求中，购物者的请求未设置Cookie，因此会向hybris实例发送请求以创建会话。

* 会话Cookie是从响应中提取的，并在新的Cookie中进行编码(例如， `hybris-session-rest`)，并在对购物者的响应中设置。 新Cookie中的编码是必需的，因为原始Cookie仅对特定路径有效，否则在后续请求中不会从浏览器发送回。 还必须将路径信息添加到Cookie的值中。

* 在后续请求中，Cookie将从 `hybris-session-<*xxx*>` Cookie ，并在用于从hybris请求数据的HTTP客户端上设置。

>[!NOTE]
>
>当原始会话不再有效时，将创建一个新的匿名会话。

#### CommerceSession {#commercesession}

* 此会话“拥有” **购物车**

   * 执行添加/删除等操作

   * 在购物车上执行各种计算；

      `commerceSession.getProductPrice(Product product)`

* 拥有 *存储位置* 对于 **订购** 数据

   `CommerceSession.getUserContext()`

* 还拥有 **付款** 正在处理连接

* 还拥有 **履行** 连接

### 产品同步和发布 {#product-synchronization-and-publishing}

在Hybris中维护的产品数据需要在AEM中可用。 已实施以下机制：

* hybris会提供ID的初始负载作为馈送。 可以更新此信息源。
* hybris将通过信息源(AEM轮询)提供更新信息。
* 当AEM使用产品数据时，它将向hybris发送有关当前数据的请求（使用上次修改日期的有条件get请求）。
* 在hybris上，可以声明方式指定馈送内容。
* 将馈送结构映射到AEM内容模型会在AEM端的馈送适配器中进行。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 导入器(b)用于初始设置AEM中的目录页面树结构。
* Hybris中的目录更改通过信息源指示给AEM，然后传播到AEM (b)

   * 与目录版本相关的产品已添加/已删除/已更改。

   * 产品已批准。

* hybris扩展提供了一个轮询导入程序（“hybris”方案），可以将其配置为按指定的时间间隔（例如，每24小时，其中时间间隔以秒为单位）将更改导入AEM：

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

* AEM中的目录配置可识别 **已暂存** 和 **在线** 目录版本。

* 在目录版本之间同步产品将需要（取消）激活相应的AEM页面(a，c)

   * 将产品添加到 **在线** 目录版本要求激活产品页面。

   * 删除产品需要停用。

* 在AEM (c)中激活页面需要选中(b)，并且仅当满足以下条件时才能激活

   * 产品位于 **在线** 产品页面的目录版本。

   * 引用的产品位于 **在线** 其他页面的目录版本（例如营销活动页面）。

* 激活的产品页面需要访问产品数据的 **在线** 版本(d)。

* AEM发布实例需要访问hybris以检索产品和个性化数据(d)。

### 架构 {#architecture}

#### 产品和变体的架构 {#architecture-of-product-and-variants}

单个产品可以有多个变体；例如，它可能因颜色和/或大小而异。 产品必须定义哪些属性会驱动变化；我们将其称为 *变量轴*.

但是，并非所有属性都是变量轴。 各种变化也可能会影响其他属性；例如，价格可能取决于大小。 购物者无法选择这些属性，因此不被视为变量轴。

每个产品和/或变体由一个资源表示，因此将1:1映射到存储库节点。 必然的结果是，特定产品和/或变体可以通过其路径进行唯一标识。

产品/变体资源并不总是包含实际产品数据。它可能表示实际包含在其他系统上的数据（如hybris）。 例如，产品描述、定价等不会存储在AEM中，而是从电子商务引擎中实时检索。

任何产品资源都可以用 `Product API`. 产品API中的大多数调用都是特定于变体的（尽管变体可能继承来自祖先的共享值），但也有列出变体集的调用( `getVariantAxes()`， `getVariants()`、等)。

>[!NOTE]
>
>实际上，变体轴由任何东西决定 `Product.getVariantAxes()` 返回：
>* hybris为hybris实现定义它
>
>虽然产品（通常）可以具有多个变体轴，但现成的产品组件仅处理两个变体轴：
>
>1. `size`
>
>1. 再加一个

>
>通过以下方式选择此附加变体： `variationAxis` 产品引用的属性(通常 `color` (对于Geometrixx Outdoors)。

#### 产品引用和产品数据 {#product-references-and-product-data}

一般而言：

* 产品数据位于 `/etc`

* 和产品引用 `/content`.

产品变体与产品数据节点之间必须是1:1映射。

产品引用还必须具有呈现每个变体的节点，但不需要呈现所有变体。 例如，如果产品具有S、M、L变体，则产品数据可能为：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

虽然“大而高”目录可能只有：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

   * 产品节点为 `nt:unstructured`.

   * 产品节点可以是：

      * 引用，将产品数据存储在其他位置：

         * 产品引用包含 `productData` 属性，指向产品数据(通常位于 `/etc/commerce/products`)。

         * 产品数据是分层的；产品属性继承自产品数据节点的祖先。

         * 产品引用还可以包含本地属性，这些属性会覆盖产品数据中指定的属性。
      * 产品本身：

         * 不带 `productData` 属性。

         * 在本地保存所有属性（且不包含productData属性）的product节点直接从自己的祖先继承产品属性。


* **AEM-generic产品结构**

   * 每个变体必须具有自己的叶节点。

   * 产品界面既表示产品，又表示变体，但相关的存储库节点特定于它本身。

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

   * 此 `CommerceSession` 执行添加/删除等操作。
   * 此 `CommerceSession` 也会在购物车上执行各种计算。”

* 虽然不直接与购物车相关，但是 `CommerceSession` 还必须提供目录定价信息（因为它拥有定价）

   * 定价可能有几个修改量：

      * 数量折扣。
      * 不同的货币。
      * 应缴纳增值税且免纳增值税。
   * 修改量完全开放，界面如下：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**存储**

* 存储

   * 在hybris示例中，hybris服务器拥有购物车。
   * 在AEM一般情况下，购物车存储在 [ClientContext](/help/sites-administering/client-context.md).

**个性化**

* 应始终通过以下方式推动个性化 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 在所有情况下都会创建Cart的：

   * 应使用添加产品 `CommerceSession.addCartEntry()` 方法。

* 下面说明了ClientContext车中的购物车信息示例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 签出架构 {#architecture-of-checkout}

**购物车和订单数据**

此 `CommerceSession` 拥有三个元素：

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

   但是，订单详细信息包括 *非* 通过API修复：

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**配送费计算**

* 订单通常需要提供多种送货选项（和价格）。
* 价格可能基于订单的物料和详细信息，如重量和/或交货地址。
* 此 `CommerceSession` 有权访问所有依赖项，因此可以采用与产品定价类似的方式处理依赖项：

   * 此 `CommerceSession` 拥有装运定价。
   * 可以使用检索/更新投放详细信息 `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>您可以实施送货选择器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本质上，这可以是 `foundation/components/form/radio`，但是通过回调到 `CommerceSession` 对于：
>
>* 检查方法是否可用
>* 添加定价信息
>* 使购物者能够更新AEM中的订单页面（包括配送方法的超集和描述这些方法的文本），同时仍有权公开相关 `CommerceSession` 信息。


**付款处理**

* 此 `CommerceSession` 还拥有支付处理连接。

* 实施人员需要将特定呼叫（添加到其选择的支付处理服务）添加到 `CommerceSession` 实现。

**订单履行**

* 此 `CommerceSession` 还拥有履行连接。
* 实施人员需要将特定呼叫（添加到其选择的支付处理服务）添加到 `CommerceSession` 实现。

### 搜索定义 {#search-definition}

遵循标准服务API模型，电子商务项目提供一组搜索相关的API，它们可以由各个商业引擎实现。

>[!NOTE]
>
>目前，只有hybris引擎实现了现成的搜索API。
>
>但是，搜索API是通用的，可以由每个CommerceService单独实现。

电子商务项目包含一个默认搜索组件，位于以下位置：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

这将利用搜索API来查询选定的商务引擎(请参阅 [电子商务引擎选择](#ecommerce-engine-selection))：

#### 搜索API {#search-api}

核心项目提供了几个通用/帮助程序类：

1. `CommerceQuery`

   用于描述搜索查询（包含有关查询文本、当前页面、页面大小、排序和所选彩块化的信息）。 所有实施搜索API的电子商务服务都将接收此类的实例，以便执行其搜索。 A `CommerceQuery` 可以从请求对象实例化( `HttpServletRequest`)。

1. `FacetParamHelper`

   是一个实用程序类，它提供一个静态方法 —  `toParams`  — 用于生成 `GET` 多面和一个切换值的列表中的参数字符串。 这在UI端很有用，您需要为每个Facet的每个值显示超链接，这样当用户单击超链接时，相应的值会切换（即，如果选中它，则会从查询中删除它，否则会添加）。 这解决了处理多个/单值Facet、覆盖值等的所有逻辑。

搜索API的入口点是 `CommerceService#search` 返回值的方法 `CommerceResult` 对象。 请参阅 [API文档](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 以了解有关此主题的详细信息。

### 用户集成 {#user-integration}

在AEM和各种电子商务系统之间提供集成。 这需要一种在不同系统之间同步购物者的策略，以便特定于AEM的代码只需了解AEM，反之亦然：

* 身份验证

   推定AEM为 *仅限* web前端，因此执行 *所有* 身份验证。

* Hybris中的帐户

   AEM会在每个购物者的hybris中创建相应的(下属)帐户。 此帐户的用户名与AEM用户名相同。 加密随机密码会自动生成，并存储在AEM中（加密）。

#### 预先存在的用户 {#pre-existing-users}

AEM前端可以位于现有Hybris实施的前面。 此外，还可以将hybris引擎添加到现有AEM安装中。 要实现此目的，系统必须能够正常处理任一系统中的现有用户：

* AEM -> hybris

   * 登录到hybris时，如果AEM用户尚不存在：

      * 使用随机密码创建新的hybris用户
      * 将hybris用户名存储在AEM用户的用户目录中
   * 请参阅: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 在登录到AEM时，如果系统识别了用户，则：

      * 尝试使用提供的用户名/密码登录hybris
      * 如果成功，请在AEM中使用相同的密码创建新用户(特定于AEM的salt将产生AEM特定的哈希)
   * 上述算法在Sling中实现 `AuthenticationInfoPostProcessor`

      * 请参阅: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自定义导入流程 {#customizing-the-import-process}

要基于现有功能构建自定义导入处理程序，请执行以下操作：

* 必须实施 `ImportHandler` 界面

* 可以扩展 `DefaultImportHandler`.

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

要使导入程序能够识别您的自定义处理程序，它必须指定 `service.ranking`值大于0的属性；例如。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
