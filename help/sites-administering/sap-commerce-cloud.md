---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 了解如何将AEM与SAPCommerce Cloud结合使用。
seo-description: 了解如何将AEM与SAPCommerce Cloud结合使用。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 9474519d-14cc-49e0-a81d-9319966fd1f6
pagetitle: Administering hybris
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 1%

---


# SAPCommerce Cloud{#sap-commerce-cloud}

安装后，您可以配置实例：

1. [为Geometrixx Outdoors配置强制搜索](#configure-the-facetted-search-for-geometrixx-outdoors)。
1. [配置目录版本](#configure-the-catalog-version)。
1. [配置导入结构](#configure-the-import-structure)。
1. [配置要加载的产品属性](#configure-the-product-attributes-to-load)。
1. [导入产品数据](#importing-the-product-data)。
1. [配置目录导入程序](#configure-the-catalog-importer)。
1. 使用[导入程序将目录](#catalog-import)导入AEM中的特定位置。

## 为Geometrixx Outdoors{#configure-the-facetted-search-for-geometrixx-outdoors}配置强制搜索

>[!NOTE]
>
>This is not needed for hybris 5.3.0.1 and later.

1. 在您的浏览器中，导航到&#x200B;**hybris管理控制台**，网址为：

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 从提要栏中，选择&#x200B;**System**，然后选择&#x200B;**Facet search**，然后选择&#x200B;**Facet Search Config**。
1. **打开** Editor，以获 **取服装目录的示例Solr配置**。

1. 在&#x200B;**目录版本**&#x200B;下，使用&#x200B;**添加目录版本**&#x200B;将`outdoors-Staged`和`outdoors-Online`添加到列表。
1. **保存配置。**
1. 打开&#x200B;**SOLR项目类型**，将&#x200B;**SOLR排序**&#x200B;添加到`ClothesVariantProduct`:

   * 相关性（“相关性”，得分）
   * name-asc(&quot;Name(ascending)&quot;, name)
   * name-desc(&quot;Name(descending)&quot;, name)
   * price-asc(&quot;Price(asceng)&quot;, priceValue)
   * price-desc(“Price(descending)”,priceValue)

   >[!NOTE]
   >
   >使用上下文菜单（通常右键单击）选择`Create Solr sort`。
   >
   >For Hybris 5.0.0 open the `Indexed Types` tab,多次-单击`ClothesVariantProduct`, the tab `SOLR Sort`。

   ![chlimage_1-36](assets/chlimage_1-36a.png)

1. 在&#x200B;**索引类型**&#x200B;选项卡中，将&#x200B;**合成类型**&#x200B;设置为：

   `Product - Product`

1. 在&#x200B;**索引类型**&#x200B;选项卡中，调整`full`的&#x200B;**索引器查询**:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在&#x200B;**索引类型**&#x200B;选项卡中，调整`incremental`的&#x200B;**索引器查询**:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在&#x200B;**索引类型**&#x200B;选项卡中，调整`category`facet。 多次-单击类别列表中的最后一个条目以打开&#x200B;**索引属性**&#x200B;选项卡：

   >[!NOTE]
   >
   >For hybris 5.2确保根据以下屏幕截图选择Properties表中的`Facet`属性：

   ![chlimage_1-37](assets/chlimage_1-37a.png) ![chlimage_1-38](assets/chlimage_1-38a.png)

1. 打开&#x200B;**Facet设置**&#x200B;选项卡并调整字段值：

   ![chlimage_1-39](assets/chlimage_1-39a.png)

1. **保存更改。**
1. 再次从&#x200B;**SOLR项类型**&#x200B;中，根据以下屏幕截图调整`price`彩块。 与`category`一样，多次单击`price`打开&#x200B;**索引属性**&#x200B;选项卡：

   ![chlimage_1-40](assets/chlimage_1-40a.png)

1. 打开&#x200B;**Facet设置**&#x200B;选项卡并调整字段值：

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. **保存更改。**
1. 打开&#x200B;**系统**、**Facet搜索**，然后打开&#x200B;**索引器操作向导**。 开始cronjob:

   * **索引器操作**:  `full`
   * **Solr配置**:  `Sample Solr Config for Clothes`

## 配置目录版本{#configure-the-catalog-version}

可以为OSGi服务配置导入的&#x200B;**目录版本**(`hybris.catalog.version`):

**Day CQ Commerce Hybris Configuration**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目** 录版本通常设置为 `Online` 或 `Staged` （默认）。

>[!NOTE]
>
>与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。 另请参阅控制台，获得可配置参数及其默认值的完整列表。

日志输出提供对创建的页面和组件的反馈，并报告潜在错误。

## 配置导入结构{#configure-the-import-structure}

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

这种结构由实现`ImportHandler`接口的OSGi服务`DefaultImportHandler`创建。 实际导入程序调用导入处理程序以创建产品、产品变量、类别、资产等。

>[!NOTE]
>
>您可以通过实现自己的导入处理程序[自定义此过程。](#configure-the-import-structure)

可以为以下对象配置导入时要生成的结构：

&quot;**Day CQ Commerce Hybris Default Import Handler**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`

与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。 另请参阅控制台，获得可配置参数及其默认值的完整列表。

## 配置要加载{#configure-the-product-attributes-to-load}的产品属性

响应分析器可以配置为定义要加载（变量）产品的属性和属性：

1. 配置OSGi捆绑包：

   **Day CQ Commerce Hybris Default Response Parser**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此处定义加载和映射所需的各种选项和属性。

   >[!NOTE]
   >
   >与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。 另请参阅控制台，获得可配置参数及其默认值的完整列表。

## 导入产品数据{#importing-the-product-data}

导入产品数据有多种方法。 The product data can be imported when initimally setting the环境, or after changes have been the hybris data:

* [完全导入](#full-import)
* [增量导入](#incremental-import)
* [快速更新](#express-update)

Actual product information imported from hybris is held in the repository under:

`/etc/commerce/products`

以下属性指示link with hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>The hybris implementation(i.e.`geometrixx-outdoors/en_US`)仅在`/etc/commerce`下存储产品ID和其他基本信息。
>
>The hybris server is referenced every information about a product is requested.

### 完整导入{#full-import}

1. 如果需要，请使用CRXDE Lite删除所有现有产品数据。

   1. 导航到包含产品数据的子树：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 删除保存产品数据的节点；例如，`outdoors`。
   1. **保存** 全部以保留更改。

1. 打开AEM中的hybris importer:

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 配置所需参数；例如：

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 单击&#x200B;**导入目录**&#x200B;以开始导入。

   完成后，您可以验证导入的数据：

   ```
       /etc/commerce/products/outdoors
   ```

   你可以用CRXDE Lite打开它；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量导入 {#incremental-import}

1. 检查AEM中相关产品的信息，位于以下相应子树中：

   `/etc/commerce/products`

   你可以用CRXDE Lite打开它；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, update the information held on the revelant product(s)。

1. 打开AEM中的hybris importer:

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框&#x200B;**增量导入**。
1. 单击&#x200B;**导入目录**&#x200B;以开始导入。

   完成后，您可以验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```


### 快速更新{#express-update}

导入过程可能需要很长时间，因此作为产品同步的扩展，您可以选择目录的特定区域以执行手动触发的快速更新。 这将导出源与标准属性配置结合使用。

1. 检查AEM中相关产品的信息，位于以下相应子树中：

   `/etc/commerce/products`

   你可以用CRXDE Lite打开它；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. In hybris, update the information held on the revelant product(s)。

1. In hybris, add the product(s)to the Express Queue;例如：

   ![chlimage_1-43](assets/chlimage_1-43a.png)

1. 打开AEM中的hybris importer:

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框&#x200B;**Express Update**。
1. 单击&#x200B;**导入目录**&#x200B;以开始导入。

   完成后，您可以验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```

   ` [](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

## 配置目录导入程序{#configure-the-catalog-importer}

The hybris catalog can be imported into AEM, using the batch importer for hybris catalogs,类别和products.

可以为以下对象配置导入程序使用的参数：

**Day CQ Commerce Hybris Catalog Importer**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。 另请参阅控制台，获得可配置参数及其默认值的完整列表。

## 目录导入{#catalog-import}

The hybris package wish a catalog importer for setting up the initial page structure.

可从以下网站获取该功能：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](assets/ecommerceimportconsole.png)

必须提供以下信息：

* **Base**
storeThe identifier of the base store configured in hybris.

* **目**
录要导入的目录的标识符。

* **根**
路径应导入目录的路径。

## 从目录{#removing-a-product-from-the-catalog}中删除产品

要从目录中删除一个或多个产品，请执行以下操作：

1. [配置for OSGi ](/help/sites-deploying/configuring-osgi.md) **serviceDay CQ Commerce Hybris Catalog Importer**;另请参阅 [配置目录导入程序](#configure-the-catalog-importer)。

   激活以下属性：

   * **启用产品删除**
   * **启用产品资产删除**

   >[!NOTE]
   >
   >与AEM合作时，有多种方法管理此类服务的配置设置；有关详细信息，请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)。 另请参阅控制台，获得可配置参数及其默认值的完整列表。

1. 通过执行两个增量更新来初始化导入程序（请参阅[目录导入](#catalog-import)）:

   * 第一次运行会生成一组更改的产品——在日志列表中指示。
   * 第二次不应更新任何产品。

   >[!NOTE]
   >
   >第一次导入是初始化产品信息。 第二次导入会验证所有功能是否正常，并且is产品集是否已就绪。

1. 检查包含要删除的产品的类别页。 产品详细信息应可见。

   例如，以下类别显示了Cajamara产品的详细信息：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Remove the product in the hybris console. 使用选项&#x200B;**更改批准状态**&#x200B;将状态设置为`unapproved`。 产品将从实时源中删除。

   例如：

   * 打开页面[http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 选择目录`Outdoors Staged`
   * 搜索 `Cajamara`
   * 选择此产品，并将批准状态更改为`unapproved`

1. 执行另一个增量更新（请参阅[目录导入](#catalog-import)）。 日志将列表已删除的产品。
1. [转](/help/sites-administering/generic.md#rolling-out-a-catalog) 出相应的目录。产品和产品页面将从AEM中删除。

   例如：

   * 打开：

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 转出`Hybris Base`目录
   * 打开：

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * `Cajamara`产品将从`Bike`类别中删除

1. 要重新安装产品，请执行以下操作：

   1. 在hybris中，将approval状态设置回&#x200B;**approved**
   1. 在AEM中：

      1. 执行增量更新
      1. 再次转出适当的目录
      1. 刷新相应的类别页

## 向Client Context {#add-order-history-trait-to-the-client-context}添加订单历史记录特征

要向[client context](/help/sites-developing/client-context.md)添加订单历史记录，请执行以下操作：

1. 通过以下任一方式打开[客户端上下文设计页面](/help/sites-administering/client-context.md):

   * 打开要编辑的页面，然后使用&#x200B;**Ctrl-Alt-c**(windows)或&#x200B;**control-option-c**(Mac)打开Client Context。 使用Client Context左上角的铅笔图标&#x200B;**打开ClientContext设计页面**。
   * 直接导航到[http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [将“订 **单历** ](/help/sites-administering/client-context.md#adding-a-property-component) 史记录”组件 **添**&#x200B;加到Client Context的“购物车”组件。
1. 您可以确认Client Context显示了订单历史记录的详细信息。 例如：

   1. 打开[client context](/help/sites-administering/client-context.md)。
   1. 向购物车中添加商品。
   1. 完成结帐。
   1. 检查Client Context。
   1. 向购物车中添加其他项目。
   1. 导航到结帐页：

      * Client Context显示订单历史记录的摘要。
      * 将显示消息“您是退回客户”。

   >[!NOTE]
   >
   >消息的实现方式：
   >
   >* 导航到[http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  活动包含一种体验。
   >
   >* 单击段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * 段是使用&#x200B;**顺序历史记录属性**&#x200B;特征构建的。

