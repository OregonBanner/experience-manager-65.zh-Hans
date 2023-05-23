---
title: 使用AEM搭配SAPCommerce Cloud
description: 瞭解如何搭配SAPCommerce Cloud使用AEM。
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

# SAPCOMMERCE CLOUD{#sap-commerce-cloud}

安裝後，您可以設定執行個體：

1. [設定Geometrixx Outdoors的Faceted搜尋](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [設定目錄版本](#configure-the-catalog-version).
1. [設定匯入結構](#configure-the-import-structure).
1. [設定產品屬性以載入](#configure-the-product-attributes-to-load).
1. [匯入產品資料](#importing-the-product-data).
1. [設定目錄匯入工具](#configure-the-catalog-importer).
1. 使用 [匯入工具匯入目錄](#catalog-import) 到AEM中的特定位置。

## 設定Geometrixx Outdoors的Faceted搜尋 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1和更新版本不需要此設定。

1. 在您的瀏覽器中，導覽至 **hybris管理主控台** 於：

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 從側邊欄中選取 **系統**，則 **Facet搜尋**，則 **Facet搜尋設定**.
1. **開啟編輯器** 的 **clothescatalog的Solr設定範例**.

1. 下 **目錄版本** use **新增目錄版本** 新增 `outdoors-Staged` 和 `outdoors-Online` 至清單。
1. **保存配置。**
1. 開啟 **SOLR專案型別** 新增 **SOLR排序** 至 `ClothesVariantProduct`：

   * 關聯性（「關聯性」，分數）
   * name-asc (「名稱（升序）」，名稱)
   * name-desc (&quot;Name (descending)&quot;， name)
   * price-asc (「Price (ascending)」， priceValue)
   * price-desc (&quot;Price (descending)&quot;， priceValue)

   >[!NOTE]
   >
   >使用快顯選單（通常是按一下滑鼠右鍵）來選取 `Create Solr sort`.
   >
   >若為Hybris 5.0.0，請開啟 `Indexed Types` 標籤，按兩下 `ClothesVariantProduct`，然後按一下索引標籤 `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在 **索引型別** 標籤設定 **構成型別** 至：

   `Product - Product`

1. 在 **索引型別** 標籤調整 **索引子查詢** 的 `full`：

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在 **索引型別** 標籤調整 **索引子查詢** 的 `incremental`：

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在 **索引型別** 標籤調整 `category` Facet。 連按兩下類別清單中的最後一個專案，以開啟 **索引屬性** 標籤：

   >[!NOTE]
   >
   >對於hybris 5.2，請確定 `Facet` 根據下列熒幕擷圖，選取「屬性」表格中的attribute：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 開啟 **Facet設定** 標籤並調整欄位值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **保存更改。**
1. 再次從 **SOLR專案型別**，調整 `price` facet的設定如下。 與 `category`，按兩下 `price` 以開啟 **索引屬性** 標籤：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 開啟 **Facet設定** 標籤並調整欄位值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **保存更改。**
1. 開啟 **系統**， **Facet搜尋**，則 **索引器操作精靈**. 啟動cronjob：

   * **索引器作業**： `full`
   * **Solr設定**： `Sample Solr Config for Clothes`

## 設定目錄版本 {#configure-the-catalog-version}

此 **目錄版本** ( `hybris.catalog.version`)時，可透過OSGi服務進行設定：

**Day CQ Commerce Hybris設定**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目錄版本** 通常設為 `Online` 或 `Staged` （預設）。

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 如需可設定引數及其預設值的完整清單，另請參閱主控台。

記錄輸出提供已建立頁面和元件的意見回饋，並報告潛在的錯誤。

## 設定匯入結構 {#configure-the-import-structure}

下列清單顯示預設建立的範例結構（包含資產、頁面和元件）：

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

這類結構是由OSGi服務所建立 `DefaultImportHandler` 實作 `ImportHandler` 介面。 實際匯入工具會呼叫匯入處理常式，以建立產品、產品變化、類別、資產等。

>[!NOTE]
>
>您可以 [實作您自己的匯入處理常式來自訂此程式](#configure-the-import-structure).

匯入時要產生的結構可設定為：

&quot;**Day CQ Commerce Hybris預設匯入處理常式**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 如需可設定引數及其預設值的完整清單，另請參閱主控台。

## 設定產品屬性以載入 {#configure-the-product-attributes-to-load}

回應剖析器可設定為定義要為（變體）產品載入的屬性和屬性：

1. 設定OSGi套件組合：

   **Day CQ Commerce Hybris預設回應剖析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此處定義載入和對映所需的各種選項和屬性。

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 如需可設定引數及其預設值的完整清單，另請參閱主控台。

## 匯入產品資料 {#importing-the-product-data}

匯入產品資料的方式多種多樣。 產品資料可在最初設定環境時匯入，或在hybris資料中進行變更後匯入：

* [完全匯入](#full-import)
* [增量导入](#incremental-import)
* [快速更新](#express-update)

從Hybris匯入的實際產品資訊會儲存在儲存庫中，位於：

`/etc/commerce/products`

下列屬性指出與hybris的連結：

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris實作(即 `geometrixx-outdoors/en_US`)只會將產品ID和其他基本資訊儲存在 `/etc/commerce`.
>
>每次請求產品的相關資訊時，都會參考hybris伺服器。

### 完全匯入 {#full-import}

1. 如有需要，請使用CRXDE Lite刪除所有現有產品資料。

   1. 導覽至儲存產品資料的子樹狀結構：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 刪除儲存產品資料的節點；例如， `outdoors`.
   1. **全部儲存** 以保留變更。

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 設定必要的引數；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 按一下 **匯入目錄** 以開始匯入。

   完成後，您可以驗證匯入的資料：

   ```
       /etc/commerce/products/outdoors
   ```

   您可以使用CRXDE Lite開啟此專案；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量导入 {#incremental-import}

1. 檢查AEM中相關產品的相關資訊（在適當的子樹狀結構下）：

   `/etc/commerce/products`

   您可以使用CRXDE Lite開啟此專案；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在Hybris中，更新相關產品上的資訊。

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選取點選方塊 **增量匯入**.
1. 按一下 **匯入目錄** 以開始匯入。

   完成後，您可以在下方驗證AEM中更新的資料：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

匯入程式可能需要很長的時間，因此，作為「產品同步化」的延伸，您可以為手動觸發的快速更新選取目錄的特定區域。 這會使用匯出摘要與標準屬性設定。

1. 檢查AEM中相關產品的相關資訊（在適當的子樹狀結構下）：

   `/etc/commerce/products`

   您可以使用CRXDE Lite開啟此專案；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在Hybris中，更新相關產品上的資訊。

1. 在hybris中，將產品新增至快速佇列；例如：

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選取點選方塊 **快速更新**.
1. 按一下 **匯入目錄** 以開始匯入。

   完成後，您可以在下方驗證AEM中更新的資料：

   ```
       /etc/commerce/products
   ```

## 設定目錄匯入工具 {#configure-the-catalog-importer}

您可以使用hybris目錄、類別和產品的批次匯入工具，將hybris目錄匯入至AEM。

匯入工具使用的引數可以設定為：

**Day CQ Commerce Hybris目錄匯入工具**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 如需可設定引數及其預設值的完整清單，另請參閱主控台。

## 目錄匯入 {#catalog-import}

hybris套件隨附有目錄匯入工具，可用於設定初始頁面結構。

可從以下網址取得：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

必須提供下列資訊：

* **基礎存放區**
在Hybris中設定的基礎存放區的識別碼。

* **目錄**
要匯入的目錄識別碼。

* **根路徑**
目錄應匯入到的路徑。

## 從目錄中移除產品 {#removing-a-product-from-the-catalog}

若要從目錄中移除一或多個產品：

1. [設定OSGi服務的](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris目錄匯入工具**；另請參閱 [設定目錄匯入工具](#configure-the-catalog-importer).

   啟用下列屬性：

   * **啟用產品移除**
   * **啟用產品資產移除**

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理此類服務的組態設定；請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 如需可設定引數及其預設值的完整清單，另請參閱主控台。

1. 透過執行兩個增量更新來初始化匯入工具(請參閱 [目錄匯入](#catalog-import))：

   * 第一次執行會產生一組已變更的產品 — 如記錄清單中所示。
   * 這是第一次不應更新任何產品。

   >[!NOTE]
   >
   >第一個匯入是初始化產品資訊。 第二次匯入會驗證一切正常運作，且產品集已準備就緒。

1. 檢查包含您要移除之產品的類別頁面。 應會顯示產品詳細資料。

   例如，以下類別顯示Cajamara產品的詳細資料：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 移除hybris主控台中的產品。 使用選項 **變更核准狀態** 若要將狀態設定為 `unapproved`. 產品將從即時摘要中移除。

   例如：

   * 開啟頁面 [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 選取目錄 `Outdoors Staged`
   * 搜索 `Cajamara`
   * 選取此產品並將核准狀態變更為 `unapproved`

1. 執行另一個增量更新(請參閱 [目錄匯入](#catalog-import))。 記錄會列出已刪除的產品。
1. [轉出](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 適當的目錄。 產品和產品頁面已從AEM中移除。

   例如：

   * 打开：

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 轉出 `Hybris Base` 目錄
   * 打开：

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 此 `Cajamara` 產品將會從 `Bike` 類別

1. 若要重新宣告產品：

   1. 在Hybris中，將核准狀態設定回 **已核准**
   1. 在AEM中：

      1. 執行增量更新
      1. 再次轉出適當的目錄
      1. 重新整理適當的類別頁面

## 將訂單歷史記錄特徵新增至使用者端內容 {#add-order-history-trait-to-the-client-context}

若要將訂單歷史記錄新增至 [使用者端內容](/help/sites-developing/client-context.md)：

1. 開啟 [使用者端內容設計頁面](/help/sites-administering/client-context.md)，方法是：

   * 開啟頁面進行編輯，然後使用開啟使用者端內容 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)。 使用使用者端內容左上角的鉛筆圖示可以 **開啟ClientContext設計頁面**.
   * 直接導覽至 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [新增 **訂單歷史記錄** 元件](/help/sites-administering/client-context.md#adding-a-property-component) 至 **購物車**&#x200B;使用者端內容的t元件。
1. 您可以確認使用者端內容顯示訂單歷程記錄的詳細資料。 例如：

   1. 開啟 [使用者端內容](/help/sites-administering/client-context.md).
   1. 新增專案至購物車。
   1. 完成結帳。
   1. 檢查使用者端內容。
   1. 新增其他專案至購物車。
   1. 導覽至結帳頁面：

      * 使用者端內容會顯示訂單歷程記錄的摘要。
      * 畫面會顯示「您是回頭的客戶」訊息。

   >[!NOTE]
   >
   >此訊息的實現方式：
   >
   >* 導覽至 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  行銷活動包含一個體驗。
   >
   >* 按一下區段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 區段是使用 **訂單歷史記錄屬性** 特徵。

