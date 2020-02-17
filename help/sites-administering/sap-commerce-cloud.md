---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: 了解如何将AEM与SAP Commerce cloud结合使用。
seo-description: 了解如何将AEM与SAP Commerce cloud结合使用。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 9474519d-14cc-49e0-a81d-9319966fd1f6
pagetitle: Administering hybris
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# SAP Commerce Cloud{#sap-commerce-cloud}

安装后，您可以配置实例：

1. [为Geometrixx Outdoors配置“受限搜索”](#configure-the-facetted-search-for-geometrixx-outdoors)。
1. [配置目录版本](#configure-the-catalog-version)。
1. [配置导入结构](#configure-the-import-structure)。
1. [配置要加载的产品属性](#configure-the-product-attributes-to-load)。
1. [导入产品数据](#importing-the-product-data)。
1. [配置目录导入程序](#configure-the-catalog-importer)。
1. 使用导 [入程序将目录导入](#catalog-import) AEM中的特定位置。

## 为Geometrixx Outdoors配置受影响的搜索 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1和更高版本不需要This。

1. 在您的浏览器中，导航到 **hybris管理控制台** :

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 从提要栏中，依次 **选择System**、 **Facet搜索**、 **Facet搜索配置**。
1. **打开Editor** ，以查看 **Clothescatalog的示例Solr配置**。

1. 在目 **录版本下** ，使 **用“添加目录”版本** ，将其添 `outdoors-Staged``outdoors-Online` 加到列表中。
1. ****&#x200B;保存配置。
1. 打开 **SOLR项目类型** ，将 **SOLR排序添加到**`ClothesVariantProduct`:

   * 相关性（“相关性”，得分）
   * name-asc(&quot;Name(ascending)&quot;, name)
   * name-desc(&quot;Name(descending)&quot;, name)
   * price-asc(“Price(asceng)”, priceValue)
   * price-desc(“Price(descending)”, priceValue)
   >[!NOTE]
   >
   >使用上下文菜单（通常是右键单击）进行选择 `Create Solr sort`。
   >
   >For Hybris 5.0.0 open the `Indexed Types` tab, double-click on `ClothesVariantProduct`, then the tab `SOLR Sort`.

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 在“索引 **类型** ”选项卡中，将“合 **成类型”设置为** :

   `Product - Product`

1. 在“索引 **类型** ”选项卡中，调 **整索引器查询**`full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在“索引 **类型** ”选项卡中，调 **整索引器查询**`incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在索引 **类型选项卡中** ，调整彩块 `category` 化。 双击类别列表中的最后一个条目以打开索引属 **性选项卡** :

   >[!NOTE]
   >
   >For hybris 5.2确保根据以 `Facet` 下屏幕截图选择“属性”表中的属性：

   ![chlimage_1-37](assets/chlimage_1-37a.png) ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 打开Facet **设置选项卡** ，并调整字段值：

   ![chlimage_1-39](assets/chlimage_1-39a.png)

1. **保存更改。**
1. 再次从 **SOLR项目类型中**，根据以 `price` 下屏幕截图调整facet。 与之一 `category`样，双击以打开“索引 `price` 属性” **选项卡** :

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. 打开Facet **设置选项卡** ，并调整字段值：

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. **保存更改。**
1. 打开 **System**、 **Facet搜索**，然后 **打开Indexer操作向导**。 启动cronjob:

   * **索引器操作**: `full`
   * **Solr配置**: `Sample Solr Config for Clothes`

## 配置目录版本 {#configure-the-catalog-version}

可 **以为OSGi服务配置导入的目录版本**`hybris.catalog.version`():

**Day CQ Commerce Hybris Configuration**( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目录版本** ，通常设置为 `Online` 或 `Staged` （默认）。

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details. 另请参阅控制台，以获得可配置参数及其默认值的完整列表。

日志输出提供有关创建的页面和组件的反馈，并报告潜在错误。

## 配置导入结构 {#configure-the-import-structure}

以下列表显示了默认创建的示例结构（资产、页面和组件）:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

这种结构由实现该接口的OSGi `DefaultImportHandler` 服务创 `ImportHandler` 建。 实际导入程序调用导入处理程序以创建产品、产品变量、类别、资产等。

>[!NOTE]
>
>您可以通 [过实施自己的导入处理程序来自定义此过程](#configure-the-import-structure)。

可以为以下对象配置导入时要生成的结构：

&quot;**Day CQ Commerce Hybris Default Import Handler**`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details. 另请参阅控制台，以获得可配置参数及其默认值的完整列表。

## 配置要加载的产品属性 {#configure-the-product-attributes-to-load}

响应分析器可配置为定义要为（变量）产品加载的属性和属性：

1. 配置OSGi包：

   **Day CQ Commerce Hybris Default Response Parser**(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此处定义加载和映射所需的各种选项和属性。

   >[!NOTE]
   >
   >When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details. 另请参阅控制台，以获得可配置参数及其默认值的完整列表。

## 导入产品数据 {#importing-the-product-data}

导入产品数据有多种方式。 The product data can be imported when initially setting the environment, or after changes have be make in the hybris data:

* [完全导入](#full-import)
* [增量导入](#incremental-import)
* [快速更新](#express-update)

从hybris导入的Actual product information is held in the repository under:

`/etc/commerce/products`

以下属性指示链接with hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>The hybris implementation(i.e.) `geometrixx-outdoors/en_US`仅存储产品ID和下的其他基本信息 `/etc/commerce`。
>
>The hybris server is referenced eventy information about a product is requested.

### 完全导入 {#full-import}

1. 如果需要，请使用CRXDE Lite删除所有现有产品数据。

   1. 导航到包含产品数据的子树：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 删除保存产品数据的节点；例如， `outdoors`。
   1. **保存全部** ，以保留更改。

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 配置所需参数；例如：

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 单击 **“导入目录** ”以开始导入。

   完成后，您可以验证导入的数据：

   ```
       /etc/commerce/products/outdoors
   ```

   您可以在CRXDE Lite中打开它；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量导入 {#incremental-import}

1. 检查AEM中有关相关产品的信息（位于以下位置的相应子树中）:

   `/etc/commerce/products`

   您可以在CRXDE Lite中打开它；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新在revelant产品上保留的信息。

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框增 **量导入**。
1. 单击 **“导入目录** ”以开始导入。

   完成后，您可以验证在AEM中更新的数据：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

导入过程可能需要很长时间，因此作为产品同步的扩展，您可以选择目录的特定区域以执行手动触发的快速更新。 这将导出源与标准属性配置一起使用。

1. 检查AEM中有关相关产品的信息（位于以下位置的相应子树中）:

   `/etc/commerce/products`

   您可以在CRXDE Lite中打开它；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新在revelant产品上保留的信息。

1. 在hybris中，将product(s)添加到Express Queue;例如：

   ![chlimage_1-43](assets/chlimage_1-43a.png)

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框“快 **速更新”**。
1. 单击 **“导入目录** ”以开始导入。

   完成后，您可以验证在AEM中更新的数据：

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## 配置目录导入程序 {#configure-the-catalog-importer}

The hybris catalog can be imported into AEM, using the batch importer for hybris catalogs, categories and products.

可以为以下对象配置导入程序使用的参数：

**Day CQ Commerce Hybris Catalog Importer**( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details. 另请参阅控制台，以获得可配置参数及其默认值的完整列表。

## 目录导入 {#catalog-import}

The hybris package with a catalog importer for setting the initial page structure.

可从以下网址获取该功能：

`http://localhost:4502/etc/importers/hybris.html`

![commerceimportconsole](assets/ecommerceimportconsole.png)

必须提供以下信息：

* **Base store** The identifier of the base store configured in hybris.

* **目录**&#x200B;要导入的目录的标识符。

* **根路径**&#x200B;应导入目录的路径。

## 从目录中删除产品 {#removing-a-product-from-the-catalog}

要从目录中删除一个或多个产品，请执行以下操作：

1. [配置for OSGi service](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris Catalog Importer**;另请参阅 [配置目录导入程序](#configure-the-catalog-importer)。

   激活以下属性：

   * **启用产品删除**
   * **启用删除产品资产**
   >[!NOTE]
   >
   >When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for full details. 另请参阅控制台，以获得可配置参数及其默认值的完整列表。

1. 通过执行两个增量更新来初始化导入程序(请参 [阅目录导入](#catalog-import)):

   * 第一次运行会生成一组已更改的产品——在日志列表中指示。
   * 第二次不应更新任何产品。
   >[!NOTE]
   >
   >第一次导入是初始化产品信息。 第二次导入会验证所有操作均正常，且产品集已准备就绪。

1. 检查包含要删除的产品的类别页面。 产品详细信息应当可见。

   例如，以下类别显示了Cajamara产品的详细信息：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在hybris控制台中删除产品。 使用选项“ **更改批准状态** ”将状态设置为 `unapproved`。 产品将从实时源中删除。

   例如：

   * 打开页面http://localhost:9001/productcockpit [更多](http://localhost:9001/productcockpit)
   * 选择目录 `Outdoors Staged`
   * 搜索 `Cajamara`
   * 选择此产品，并将批准状态更改为 `unapproved`

1. 执行另一个增量更新(请参 [阅目录导入](#catalog-import))。 日志将列出已删除的产品。
1. [转出](/help/sites-administering/generic.md#rolling-out-a-catalog) ，相应的目录。 产品和产品页面将从AEM中删除。

   例如：

   * 打开：

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 转出目 `Hybris Base` 录
   * 打开：

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 产 `Cajamara` 品将从类别中删 `Bike` 除

1. 要重新安装产品，请执行以下操作：

   1. 在hybris中，将批准状态设置回 **approved**
   1. 在AEM中：

      1. 执行增量更新
      1. 再次转出相应的目录
      1. 刷新相应的类别页面

## 向Client context添加订单历史记录特征 {#add-order-history-trait-to-the-client-context}

要向Client Context添加订单历史记录，请执 [行以下操作](/help/sites-developing/client-context.md):

1. 通过以下任 [一方式打开Client Context设计页面](/help/sites-administering/client-context.md):

   * 打开要编辑的页面，然后使用 **Ctrl-Alt-c** (Windows)或 **control-option-c** (Mac)打开Client Context。 使用Client Context左上角的铅笔图标打开ClientContext **设计页面**。
   * 直接导航到 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [将“订 **单历史** ”组件添](/help/sites-administering/client-context.md#adding-a-property-component) 加到 **** Client Context的“购物车”组件。
1. 您可以确认Client Context显示了订单历史记录的详细信息。 例如：

   1. Open the [client context](/help/sites-administering/client-context.md).
   1. 向购物车中添加商品。
   1. 完成结帐。
   1. 检查Client Context。
   1. 向购物车中添加其他物品。
   1. 导航到结帐页面：

      * Client Context显示订单历史记录的摘要。
      * 此时将显示消息“您是退回客户”。
   >[!NOTE]
   >
   >消息的实现方式为：
   >
   >* 导航到 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  该营销活动包含一个体验。
   >
   >* 单击区段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * 段是使用“订单历史记录属 **性”特征构建** 的。

