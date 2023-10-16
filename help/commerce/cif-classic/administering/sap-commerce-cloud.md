---
title: 将AEM与SAPCommerce Cloud结合使用
description: 了解如何将Adobe Experience Manager与SAPCommerce Cloud结合使用。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 1%

---

# SAPCOMMERCE CLOUD{#sap-commerce-cloud}

安装后，您可以配置实例：

1. [配置Geometrixx Outdoors的分面搜索](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [配置目录版本](#configure-the-catalog-version).
1. [配置导入结构](#configure-the-import-structure).
1. [配置要加载的产品属性](#configure-the-product-attributes-to-load).
1. [导入产品数据](#importing-the-product-data).
1. [配置目录导入程序](#configure-the-catalog-importer).
1. 使用 [导入程序以导入目录](#catalog-import) 到AEM中的特定位置。

## 配置Geometrixx Outdoors的分面搜索 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1及更高版本不需要此参数。

1. 在浏览器中，导航到 **hybris管理控制台** 在：

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 在侧栏中，选择 **系统**，则 **Facet搜索**，则 **Facet搜索配置**.
1. **打开编辑器** 对于 **clothescatalog的Solr配置示例**.

1. 下 **目录版本** 使用 **添加目录版本** 添加 `outdoors-Staged` 和 `outdoors-Online` 到名单上。
1. **保存配置。**
1. 打开 **SOLR项类型** 添加 **SOLR排序** 到 `ClothesVariantProduct`：

   * 相关性（“相关性”，分数）
   * name-asc (“名称（升序）”， name)
   * name-desc (“Name(descending)”， name)
   * price-asc(“Price(ascending)”， priceValue)
   * price-desc(“价格（降序）”， priceValue)

   >[!NOTE]
   >
   >使用上下文菜单（通常是单击右键）进行选择 `Create Solr sort`.
   >
   >对于Hybris 5.0.0，打开 `Indexed Types` 选项卡，双击 `ClothesVariantProduct`，然后选项卡 `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在 **索引类型** 选项卡，设置 **撰写类型** 至：

   `Product - Product`

1. 在 **索引类型** 选项卡，调整 **索引器查询** 对象 `full`：

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在 **索引类型** 选项卡，调整 **索引器查询** 对象 `incremental`：

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在 **索引类型** 选项卡，调整 `category` 方面。 双击类别列表中的最后一个条目以打开 **索引属性** 选项卡：

   >[!NOTE]
   >
   >对于hybris 5.2 ，确保 `Facet` 根据下面的屏幕快照选择“属性”表格中的属性：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 打开 **Facet设置** 选项卡并调整字段值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **保存更改。**
1. 再次从 **SOLR项类型**，调整 `price` Facet的屏幕截图如下所示。 与 `category`，双击 `price` 以打开 **索引属性** 选项卡：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 打开 **Facet设置** 选项卡并调整字段值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **保存更改。**
1. 打开 **系统**， **Facet搜索**，则 **索引器操作向导**. 启动cronjob：

   * **索引器操作**： `full`
   * **Solr配置**： `Sample Solr Config for Clothes`

## 配置目录版本 {#configure-the-catalog-version}

此 **目录版本** ( `hybris.catalog.version`)可以为OSGi服务配置导入的内容：

**Day CQ Commerce Hybris配置**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目录版本** 设置为 `Online` 或 `Staged` （默认）。

>[!NOTE]
>
>使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。 有关可配置参数及其缺省值的完整列表，另请参阅控制台。

日志输出提供关于所创建页面和组件的反馈，并报告潜在的错误。

## 配置导入结构 {#configure-the-import-structure}

以下列表显示了默认情况下创建的示例结构（由资产、页面和组件组成）：

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

此类结构由OSGi服务创建 `DefaultImportHandler` 实施 `ImportHandler` 界面。 实际导入程序会调用导入处理程序，以创建产品、产品变体、类别、资产等。

>[!NOTE]
>
>您可以 [通过实施您自己的导入处理程序来自定义此流程](#configure-the-import-structure).

可以为以下配置导入时要生成的结构：

&quot;**Day CQ Commerce Hybris默认导入处理程序**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。 有关可配置参数及其缺省值的完整列表，另请参阅控制台。

## 配置要加载的产品属性 {#configure-the-product-attributes-to-load}

响应分析器可以配置为定义要为（变体）产品加载的属性和属性：

1. 配置OSGi捆绑包：

   **Day CQ Commerce Hybris默认响应分析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此定义加载和映射所需的各种选项和属性。

   >[!NOTE]
   >
   >使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。 有关可配置参数及其缺省值的完整列表，另请参阅控制台。

## 导入产品数据 {#importing-the-product-data}

有多种方式可导入产品数据。 可在最初设置环境时或在hybris数据中进行更改后导入产品数据：

* [完全导入](#full-import)
* [增量导入](#incremental-import)
* [快速更新](#express-update)

从hybris导入的实际产品信息保存在存储库中的以下位置：

`/etc/commerce/products`

以下属性指示与hybris的链接：

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris实现(即， `geometrixx-outdoors/en_US`)仅将产品ID和其他基本信息存储在中 `/etc/commerce`.
>
>每次请求有关产品的信息时，都会引用hybris服务器。

### 完全导入 {#full-import}

1. 如有必要，请使用CRXDE Lite删除所有现有的产品数据。

   1. 导航到包含产品数据的子树：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 删除保存产品数据的节点；例如， `outdoors`.
   1. **全部保存** 以保留更改。

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 配置所需的参数；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 单击 **导入目录** 以开始导入。

   完成后，您可以验证导入的数据：

   ```
       /etc/commerce/products/outdoors
   ```

   您可以在CRXDE Lite中打开此项；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量导入 {#incremental-import}

1. 检查AEM中相关产品的信息，位于以下相应子树中：

   `/etc/commerce/products`

   您可以在CRXDE Lite中打开此项；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在Hybris中，更新相关产品上的信息。

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选中复选框 **增量导入**.
1. 单击 **导入目录** 以开始导入。

   完成后，您可以在下面验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

导入过程可能需要较长时间，因此，作为产品同步的扩展，您可以选择目录的特定区域以进行手动触发的快速更新。 这会使用导出信息源以及标准属性配置。

1. 检查AEM中相关产品的信息，位于以下相应子树中：

   `/etc/commerce/products`

   您可以在CRXDE Lite中打开此项；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在Hybris中，更新相关产品上的信息。

1. 在hybris中，将一个或多个产品添加到Express队列；例如：

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. 在AEM中打开hybris导入程序：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选中复选框 **快速更新**.
1. 单击 **导入目录** 以开始导入。

   完成后，您可以在下面验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```

## 配置目录导入程序 {#configure-the-catalog-importer}

使用hybris目录、类别和产品的批次导入器，可以将hybris目录导入AEM。

导入器使用的参数可以配置用于：

**Day CQ Commerce Hybris目录导入程序**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。 有关可配置参数及其缺省值的完整列表，另请参阅控制台。

## 目录导入 {#catalog-import}

hybris包附带一个目录导入程序，用于设置初始页面结构。

该功能可从以下位置获取：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

必须提供以下信息：

* **基础存储**
在hybris中配置的基本存储的标识符。

* **目录**
要导入的目录的标识符。

* **根路径**
目录应导入到的路径。

## 从目录中删除产品 {#removing-a-product-from-the-catalog}

要从目录中删除一个或多个产品，请执行以下操作：

1. [为OSGi服务配置](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris目录导入程序**；另请参阅 [配置目录导入程序](#configure-the-catalog-importer).

   激活以下属性：

   * **启用产品删除**
   * **启用产品资产删除**

   >[!NOTE]
   >
   >使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解全部详细信息。 有关可配置参数及其缺省值的完整列表，另请参阅控制台。

1. 通过执行两次增量更新初始化导入器(请参阅 [目录导入](#catalog-import))：

   * 首次运行会生成一组已更改的产品，如日志列表中所示。
   * 这已是第二次不更新任何产品了。

   >[!NOTE]
   >
   >第一个导入是初始化产品信息。 第二次导入验证所有组件是否正常工作，以及是否已准备好。

1. 选中包含要删除的产品的类别页面。 产品详细信息应可见。

   例如，以下类别显示了Cajamara产品的详细信息：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在hybris控制台中删除该产品。 使用选项 **更改审批状态** 将状态设置为 `unapproved`. 将从实时信息源中删除产品。

   例如：

   * 打开页面 [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 选择目录 `Outdoors Staged`
   * 搜索 `Cajamara`
   * 选择此产品并将审批状态更改为 `unapproved`

1. 执行另一个增量更新(请参阅 [目录导入](#catalog-import))。 日志中列出了已删除的产品。
1. [转出](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 相应的目录。 已从AEM中删除产品和产品页面。

   例如：

   * 打开：

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 转出 `Hybris Base` 目录
   * 打开：

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 此 `Cajamara` 产品已从中删除 `Bike` 类别

1. 要恢复产品，请执行以下操作：

   1. 在hybris中，将审批状态设置为 **已批准**
   1. 在AEM中：

      1. 执行增量更新
      1. 再次转出相应的目录
      1. 刷新相应的类别页面

## 将订单历史记录特征添加到客户端上下文 {#add-order-history-trait-to-the-client-context}

将订单历史记录添加到 [客户端上下文](/help/sites-developing/client-context.md)：

1. 打开 [客户端上下文设计页面](/help/sites-administering/client-context.md)，通过：

   * 打开页面进行编辑，然后使用打开客户端上下文 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)。 使用客户端上下文左上角的铅笔图标可以 **打开“ClientContext设计”页面**.
   * 直接导航到 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [添加 **订单历史记录** 组件](/help/sites-administering/client-context.md#adding-a-property-component) 到 **购物车** t客户端上下文的组件。
1. 您可以确认客户端上下文显示订单历史记录的详细信息。 例如：

   1. 打开 [客户端上下文](/help/sites-administering/client-context.md).
   1. 将项目添加到购物车。
   1. 完成结帐。
   1. 检查客户端上下文。
   1. 将另一项目添加到购物车。
   1. 导航到结账页面：

      * 客户端上下文显示订单历史记录的摘要。
      * 将显示“You are a returning customer（您是旧客户）”消息。

   >[!NOTE]
   >
   >该消息通过以下方式实现：
   >
   >* 导航到 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  营销策划包含一个体验。
   >
   >* 单击区段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 区段是使用 **订单历史记录属性** 特征。
