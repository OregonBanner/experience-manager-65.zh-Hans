---
title: 将AEM与SAP结合使用Commerce Cloud
description: 了解如何将AEM与SAPCommerce Cloud结合使用。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 1%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

安装后，您可以配置实例：

1. [配置推荐搜索Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [配置目录版本](#configure-the-catalog-version).
1. [配置导入结构](#configure-the-import-structure).
1. [配置要加载的产品属性](#configure-the-product-attributes-to-load).
1. [导入产品数据](#importing-the-product-data).
1. [配置目录导入器](#configure-the-catalog-importer).
1. 使用 [导入程序导入目录](#catalog-import) 到AEM中的特定位置。

## 配置推荐搜索Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1及更高版本不需要此设置。

1. 在您的浏览器中，导航到 **hybris管理控制台** at:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 在侧栏中，选择 **系统**，则 **Facet搜索**，则 **Facet搜索配置**.
1. **Open Editor** 对于 **服装目录的示例Solr配置**.

1. 在 **目录版本** use **添加目录版本** 添加 `outdoors-Staged` 和 `outdoors-Online` 到列表。
1. **保存配置。**
1. 打开 **SOLR物料类型** 添加 **SOLR排序** to `ClothesVariantProduct`:

   * 相关性（“相关性”，分数）
   * name-asc(&quot;Name（升序）&quot;, name)
   * name-desc(&quot;Name(descending)&quot;, name)
   * price-asc(&quot;Price(ascheng)&quot;, priceValue)
   * price-desc(&quot;Price(descending)&quot;, priceValue)

   >[!NOTE]
   >
   >使用上下文菜单（通常是右键单击）选择 `Create Solr sort`.
   >
   >对于Hybris 5.0.0，打开 `Indexed Types` ，双击 `ClothesVariantProduct`，然后选择选项卡 `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在 **索引类型** 选项卡设置 **合成类型** 至：

   `Product - Product`

1. 在 **索引类型** 选项卡调整 **索引器查询** 表示 `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在 **索引类型** 选项卡调整 **索引器查询** 表示 `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在 **索引类型** 选项卡调整 `category` 面。 双击类别列表中的最后一个条目以打开 **索引属性** 选项卡：

   >[!NOTE]
   >
   >对于hybris 5.2，请确保 `Facet` 属性表中的属性将根据以下屏幕截图进行选择：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 打开 **Facet设置** ，并调整字段值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **保存更改。**
1. 从 **SOLR物料类型**，调整 `price` facet会根据以下屏幕截图显示。 与 `category`，双击 `price` 打开 **索引属性** 选项卡：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 打开 **Facet设置** ，并调整字段值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **保存更改。**
1. 打开 **系统**, **Facet搜索**，则 **索引器操作向导**. 启动cronjob:

   * **索引器操作**: `full`
   * **Solr配置**: `Sample Solr Config for Clothes`

## 配置目录版本 {#configure-the-catalog-version}

的 **目录版本** ( `hybris.catalog.version`)，可以为OSGi服务配置：

**Day CQ Commerce Hybris Configuration**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目录版本** 通常设置为 `Online` 或 `Staged` （默认）。

>[!NOTE]
>
>使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整详细信息。 另请参阅控制台，获取可配置参数及其默认值的完整列表。

日志输出可提供有关已创建页面和组件的反馈，并报告潜在错误。

## 配置导入结构 {#configure-the-import-structure}

以下列表显示了默认创建的示例结构（资产、页面和组件）：

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
>您可以 [通过实施您自己的导入处理程序来自定义此过程](#configure-the-import-structure).

可以为以下对象配置导入时要生成的结构：

&quot;**Day CQ Commerce Hybris默认导入处理程序**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整详细信息。 另请参阅控制台，获取可配置参数及其默认值的完整列表。

## 配置要加载的产品属性 {#configure-the-product-attributes-to-load}

响应解析器可配置为定义要为（变量）产品加载的属性和属性：

1. 配置OSGi包：

   **Day CQ Commerce Hybris默认响应分析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   在此，您可以定义加载和映射所需的各种选项和属性。

   >[!NOTE]
   >
   >使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整详细信息。 另请参阅控制台，获取可配置参数及其默认值的完整列表。

## 导入产品数据 {#importing-the-product-data}

有多种方法可导入产品数据。 可在最初设置环境时或在hybris数据中进行更改后导入产品数据：

* [完全导入](#full-import)
* [增量导入](#incremental-import)
* [快速更新](#express-update)

从hybris导入的实际产品信息保存在存储库中，位于：

`/etc/commerce/products`

以下属性指示具有hybris的链接：

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris实施(即 `geometrixx-outdoors/en_US`)仅存储产品ID和 `/etc/commerce`.
>
>每次请求有关产品的信息时，都会引用hybris服务器。

### 完全导入 {#full-import}

1. 如果需要，请使用CRXDE Lite删除所有现有产品数据。

   1. 导航到包含产品数据的子树：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 删除保存产品数据的节点；例如， `outdoors`.
   1. **全部保存** 来保留更改。

1. 在AEM中打开hybris导入器：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 配置所需参数；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 单击 **导入目录** 以开始导入。

   完成后，您可以验证在以下位置导入的数据：

   ```
       /etc/commerce/products/outdoors
   ```

   可以在CRXDE Lite中打开；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量导入 {#incremental-import}

1. 在以下相应子树中查看AEM中有关相关产品的信息：

   `/etc/commerce/products`

   可以在CRXDE Lite中打开；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有关相关产品的信息。

1. 在AEM中打开hybris导入器：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框 **增量导入**.
1. 单击 **导入目录** 以开始导入。

   完成后，您可以在以下位置验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

导入过程可能需要较长时间，因此作为产品同步的扩展，您可以为手动触发的快速更新选择目录的特定区域。 这会将导出信息源与标准属性配置结合使用。

1. 在以下相应子树中查看AEM中有关相关产品的信息：

   `/etc/commerce/products`

   可以在CRXDE Lite中打开；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有关相关产品的信息。

1. 在hybris中，将产品添加到Express Queue;例如：

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. 在AEM中打开hybris导入器：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 选择单击框 **快速更新**.
1. 单击 **导入目录** 以开始导入。

   完成后，您可以在以下位置验证AEM中更新的数据：

   ```
       /etc/commerce/products
   ```

## 配置目录导入器 {#configure-the-catalog-importer}

hybris目录可以使用hybris目录、类别和产品的批处理导入器导入到AEM中。

可以为导入器使用的参数配置：

**Day CQ Commerce Hybris Catalog Importer**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整详细信息。 另请参阅控制台，获取可配置参数及其默认值的完整列表。

## 目录导入 {#catalog-import}

hybris包随目录导入器一起提供，用于设置初始页面结构。

可从以下位置获取：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

必须提供以下信息：

* **基本存储**
在hybris中配置的基本存储的标识符。

* **目录**
要导入的目录的标识符。

* **根路径**
应将目录导入的路径。

## 从目录中删除产品 {#removing-a-product-from-the-catalog}

要从目录中删除一个或多个产品，请执行以下操作：

1. [为OSGi服务配置](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris Catalog Importer**;另请参阅 [配置目录导入器](#configure-the-catalog-importer).

   激活以下属性：

   * **启用产品移除**
   * **启用产品资产移除**

   >[!NOTE]
   >
   >使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解完整详细信息。 另请参阅控制台，获取可配置参数及其默认值的完整列表。

1. 通过执行两个增量更新来初始化导入器(请参阅 [目录导入](#catalog-import)):

   * 第一次运行会生成一组更改的产品，如日志列表所示。
   * 第二次不应更新任何产品。

   >[!NOTE]
   >
   >第一个导入操作是初始化产品信息。 第二次导入会验证所有操作是否正常，且产品集已准备就绪。

1. 检查包含要删除的产品的类别页面。 产品详细信息应该可见。

   例如，以下类别显示了Cajamara产品的详细信息：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在hybris控制台中删除产品。 使用选项 **更改批准状态** 将状态设置为 `unapproved`. 产品将从实时馈送中删除。

   例如：

   * 打开页面 [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 选择目录 `Outdoors Staged`
   * 搜索 `Cajamara`
   * 选择此产品，然后将审批状态更改为 `unapproved`

1. 执行其他增量更新(请参阅 [目录导入](#catalog-import))。 日志将列出已删除的产品。
1. [转出](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 相应的目录。 产品和产品页面将从AEM中删除。

   例如：

   * 打开：

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 转出 `Hybris Base` 目录
   * 打开：

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 的 `Cajamara` 产品将从 `Bike` 类别

1. 要重新声明产品，请执行以下操作：

   1. 在hybris中，将批准状态设置回 **已批准**
   1. 在AEM中：

      1. 执行增量更新
      1. 再次转出相应的目录
      1. 刷新相应的类别页面

## 将订单历史记录特征添加到Client Context {#add-order-history-trait-to-the-client-context}

将订单历史记录添加到 [客户端上下文](/help/sites-developing/client-context.md):

1. 打开 [客户端上下文设计页面](/help/sites-administering/client-context.md)，通过以下任一方式：

   * 打开要编辑的页面，然后使用 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)。 使用Client Context左上角的铅笔图标，可 **打开ClientContext设计页面**.
   * 直接导航到 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [添加 **订单历史记录** 组件](/help/sites-administering/client-context.md#adding-a-property-component) 到 **购物车**&#x200B;客户端上下文的t组件。
1. 您可以确认Client Context显示了订单历史记录的详细信息。 例如：

   1. 打开 [客户端上下文](/help/sites-administering/client-context.md).
   1. 向购物车中添加商品。
   1. 完成结帐。
   1. 检查客户端上下文。
   1. 向购物车中添加其他项目。
   1. 导航到结帐页面：

      * Client Context显示订单历史记录的摘要。
      * 此时将显示消息“您是回访客户”。

   >[!NOTE]
   >
   >该消息的实现方式为：
   >
   >* 导航到 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  营销活动包含一个体验。
   >
   >* 单击区段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 区段是使用 **订单历史记录属性** 特征。

