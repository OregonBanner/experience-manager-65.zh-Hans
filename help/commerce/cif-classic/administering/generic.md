---
title: 管理一般電子商務
seo-title: Administering generic eCommerce
description: AEM一般解決方案提供管理存放庫中存放的商務資訊的方法。
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 3%

---

# 管理一般電子商務 {#administering-generic-ecommerce}

AEM一般解決方案會提供管理存放庫內儲存的商務資訊的方法（與使用外部電子商務引擎相反）。 这包括：

* [产品](/help/commerce/cif-classic/administering/concepts.md#products)
* [产品的系列品种](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目錄](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促销活动](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [优惠券](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [订单](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Proxy頁面](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>這目前僅供示範之用，或根據您的需求作為自訂實作的基本基礎。

## 產品和產品變數 {#products-and-product-variations}

>[!NOTE]
>
>以下程式適用於產品和產品變體。

建立產品之前，您需要定義 [支架](/help/sites-authoring/scaffolding.md). 這會指定定義產品所需的欄位以及編輯產品的方式。

每個不同的產品型別都需要支架。 適當的支架可透過以下任一方式與產品相關聯：

* 路径
* 產品可參考此支架

>[!NOTE]
>
>Geometrixx-Outdoors商店只有單一產品型別（因此只有單一支架）：
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx — 戶外活動產品型別啟用於：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在此下的任何位置建立新的產品定義，而不需要任何其他設定。

### 正在导入产品 {#importing-products}

#### 匯入產品 — 觸控最佳化UI {#importing-products-touch-optimized-ui}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用 **產品** 主控台導覽至所需位置。
1. 使用 **匯入產品** 圖示以開啟精靈。

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定：

   * **导入程序**

      特定的Importer [商務提供者](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)，預設為 `Geometrixx`.

   * **来源**

      您要匯入的檔案；您可以使用瀏覽器來選取檔案。

   * **增量导入**

      指出這是否為增量匯入（而非完全匯入）。
   >[!NOTE]
   >
   >增量匯入（範例geometrixx-outdoor匯入工具的）會在產品層級運作。
   >
   >您可以定義自訂的匯入工具來視需要操作。

1. 選取 **下一個** 若要匯入產品，將會顯示所採取動作的記錄。

   >[!NOTE]
   >
   >產品將會匯入至目前位置或相對於目前位置。

   >[!NOTE]
   >
   >重複使用 **下一個** 和 **返回** 將重複匯入產品定義。 但是，由於它們的SKU相同，存放庫中存在的資訊只會被覆寫。

1. 選取 **完成** 以關閉精靈。

#### 匯入產品 — Classic UI {#importing-products-classic-ui}

1. 使用 **工具** 主控台開啟 **商務** 資料夾。
1. 按兩下以開啟 **產品匯入工具**：

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定：

   * **存储名称**

      產品將匯入至：

      `/etc/commerce/products/<*store name*>/`

   * **商业提供程序**

      您的匯入工具 [商務提供者](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)；預設Geometrixx。

   * **源文件**

      您要匯入的檔案在存放庫中的位置。

   * **增量导入**

      指出這是否為增量匯入（而非完全匯入）。

1. 按一下 **匯入產品**.

### 建立產品資訊 {#creating-product-information}

>[!NOTE]
>
>標準產品管理是基本功能，因為Geometrixx-Outdoors產品集是基本功能。 複雜性取決於產品 [支架](/help/sites-authoring/scaffolding.md)，有了您自己的產品支架，就能進行更複雜的編輯。

#### 建立產品資訊 — 觸控最佳化UI {#creating-product-information-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至所需位置。
1. 使用 **建立** 圖示以選取（視結構和位置而定）：

   * **创建产品**
   * **建立產品變數**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 精靈將會開啟。 使用 **基本** 和 **產品標籤** 以輸入 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 用於新產品或產品變體。

   >[!NOTE]
   >
   >**標題** 和 **SKU** 是建立產品或變體所需的最低值。

1. 選取 **建立** 以儲存資訊。

>[!NOTE]
>
>許多產品提供多種顏色和/或尺寸。 基本產品和相關產品變體的相關資訊都可從以下網址管理： **產品** 主控台。
>
>產品及其變體會以樹狀結構儲存，產品資訊位於頂端，變體位於下方（此結構由UI強制執行）。

### 編輯產品資訊 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors中的產品影像提供自：
>
>`/etc/commerce/products/...`
>
>這表示預設會加以封鎖， [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans)，請視需要設定。

#### 編輯產品資訊 — 觸控最佳化UI {#editing-product-information-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **檢視產品資料** 圖示：

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 此 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 將會顯示。 使用 **編輯** 和 **完成** 以進行任何變更。

### 顯示產品參考 {#showing-product-references}

#### 顯示產品參考 — 觸控最佳化UI {#showing-product-references-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用圖示開啟「參考」的次要邊欄：

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 選取您需要的產品 — 次要邊欄將更新以顯示可用的參考型別：

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. 按一下/點選參考型別（例如產品頁面）以展開清單。
1. 選取要顯示選項的特定參照：

   * 导航到产品页面
   * 编辑产品页面

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### 搜尋產品 {#search-for-products}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用圖示開啟要搜尋的次要邊欄：

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 有數個Facet可供您搜尋產品。 搜尋只能使用一或多個面向。 找到的產品將會出現：

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. 按一下/點選產品即可將其開啟。 您也可以發佈或檢視產品資料。

#### 延伸搜尋 {#extending-search}

您可以使用CRXDE Lite修改現有多面或新增多面：

1. 导航至：

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以修改將顯示在產品搜尋頁面上的大小。 按一下 `sizegroup` 節點。
1. 按一下 `items` 節點，然後按一下 `propertypredicate` 節點。
1. 您可以修改 `propertyValues`. 例如，您可以新增XS、XXL或移除大小。
1. 按一下 **全部儲存** 並導覽至「產品搜尋」頁面。 您的變更將會顯示。

### 多個資產 {#multiple-assets}

您可以在產品元件中新增多個資產，然後指定將顯示在產品頁面上的資產。

>[!NOTE]
>
>與多個資產相關的所有工作都透過觸控最佳化的UI完成。

#### 新增多個資產 {#adding-multiple-assets}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用 **產品** 主控台，導覽至所需的產品。

   >[!NOTE]
   >
   >您必須處於產品層級，而不是變體層級。

1. 點選/按一下 **檢視產品資料** 圖示來顯示選取模式或快速動作。
1. 點選/按一下編輯圖示。
1. 捲動至 **新增**.

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. 點選/按一下 **新增**. 新的資產預留位置隨即顯示。
1. 點選/按一下**變更**開啟對話方塊，讓您選擇資產。
1. 選取您要新增的資產。

   >[!NOTE]
   >
   >您可以選取的資產來自 [資產](/help/assets/assets.md).

1. 點選/按一下完成圖示。

兩個資產現在儲存在您的產品元件中。 您可以設定要在產品頁面上顯示的專案。 這適用於類別系統。 首先，您需要將類別新增至個別資產：

1. 點選/按一下 **檢視產品資料**.
1. 輸入 **資產類別** 在資產底下，例如 `cat1` 和 `cat2`.

   >[!NOTE]
   >
   >您也可以使用類別的標籤。

1. 點選/按一下完成圖示。 您現在必須 [轉出](#rolling-out-a-catalog) 您的變更。

現在，您在產品元件中的資產有一個類別。 您可以設定將在三個不同層級顯示哪個類別：

* [产品页面](#product-page)
* [目录](#catalog)
* [產品主控台](#products-console)

>[!NOTE]
>
>如果您未設定類別，產品頁面上將顯示第一個資產。

選取要顯示的影像的機制如下：

1. 驗證是否為「產品頁面」設定了類別。
1. 如果沒有，則驗證是否為「目錄」設定了類別。
1. 如果沒有，請確認是否為「產品主控台」設定了類別。

>[!NOTE]
>
>對於目錄層級和產品主控台層級，您必須轉出變更以套用修改，並在產品頁面上檢視差異。

#### 产品页面 {#product-page}

1. 導覽至您的產品頁面。
1. **編輯** 產品元件。
1. 輸入 **影像類別** 您已選擇( `cat1` 例如)。
1. 點選/按一下 **完成**. 頁面會重新整理，且應會顯示正確的資產。

#### 目录  {#catalog}

1. 導覽至您的目錄。
1. 點選/按一下 **檢視屬性**.
1. 点按/单击&#x200B;**编辑**。
1. 點選/按一下 **資產** 標籤。
1. 輸入所需的 **產品資產類別**.
1. 點選/按一下 **完成**.
1. [轉出](#rolling-out-a-catalog) 您的變更。

#### 產品主控台 {#products-console}

1. 使用 **產品** 主控台，導覽至所需的產品。
1. 點選/按一下 **檢視產品資料**.
1. 点按/单击&#x200B;**编辑**。
1. 輸入a **預設資產類別**.
1. 點選/按一下 **完成**.
1. [轉出](#rolling-out-a-catalog) 您的變更。

### 發佈/取消發佈產品資訊 {#publishing-unpublishing-product-information}

#### 發佈/取消發佈產品資訊 — 觸控最佳化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>通常產品資訊會透過參考它的頁面發佈。 例如，發佈參考產品Y的頁面X時，AEM會詢問您是否要同時發佈產品Y。
>
>對於特殊情況，AEM也支援直接從產品資料發佈。

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **發佈** 或 **取消發佈** 圖示依需要：

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   產品資訊將視情況發佈或取消發佈。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 產品更新的事件處理常式 {#event-handler-for-product-updates}

有一個事件處理常式，可在新增、修改或刪除產品以及新增、修改或刪除產品頁面時記錄事件。 有以下OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

對於 `PRODUCT_*` 事件，路徑會指向中的基礎產品 `/etc/commerce/products`. 對於 `PRODUCT_PAGE_*` 事件，路徑指向 `cq:Page` 節點。

您可以在OSGI事件的Web主控台中檢視它們( `/system/console/events`)，例如：

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另請閱讀 [AEM中的事件處理](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### 含有加入購物車連結的影像 {#image-with-add-to-cart-links}

「包含加入購物車連結的影像」元件可讓您在影像上建立與產品連結的熱點，以快速將產品加入購物車。

按一下熱點會開啟一個對話方塊，讓您選擇產品的大小和數量。

1. 導覽至您要新增元件的頁面。
1. 將元件拖放至頁面中。
1. 將元件中的影像從 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. 您可以：

   * 按一下元件，然後按一下「編輯」圖示
   * 進行緩慢連按兩下

1. 按一下全熒幕圖示。

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. 按一下「啟動地圖」圖示。

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. 按一下其中一個形狀圖示。

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 視需要修改和移動形狀。
1. 按一下形狀。
1. 按一下瀏覽圖示會開啟 [資產選取器](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >或者，您可以直接鍵入必須在產品層級（而不是變體層級）的產品路徑。

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. 按兩下確認圖示，然後按一下退出全熒幕。
1. 在頁面上的元件旁的某個位置按一下。 頁面應重新整理，且您應會在影像上看到下列符號：

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切換至 [預覽](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) 模式。
1. 按一下+熱點。 隨即開啟一個對話方塊，您可以在其中選擇所輸入產品的大小和數量 **路徑**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. 輸入大小與數量。
1. 按一下「加入購物車」按鈕。 對話方塊關閉。
1. 導覽至您的購物車。 產品應位於此處。

#### 設定選項 {#configuration-options}

您可以設定當您按一下熱點時對話方塊的外觀：

1. 按一下元件，然後按一下設定圖示。

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下滚动. 有一個 **加入購物車** 標籤。

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. 按一下 **加入購物車**. 有3個組態選項可供您使用。

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. 按一下完成圖示。

## 目錄 {#catalogs}

### 產生目錄 {#generating-a-catalog}

#### 產生目錄 — 觸控最佳化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目錄將參考您的產品資料。

若要產生目錄，請執行下列動作：

1. 開啟Sites主控台(例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 导航到要创建新页面的位置。
1. 若要開啟選項清單，請使用 **建立** 圖示：

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 從清單中選取 **建立目錄**，建立目錄精靈隨即開啟。

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. 導覽至所需的目錄Blueprint。
1. 點選/按一下 **選取** 按鈕並點選/按一下所需的目錄Blueprint。
1. 點選/按一下 **下一個**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. 輸入a **標題** 和 **名稱**.
1. 點選/按一下 **建立** 按鈕。 目錄隨即建立，對話方塊隨即開啟。

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. 點選/按一下 **完成** 按鈕帶您回到Sites主控台，您會在這裡看到您的目錄。

   點選/按一下 **開啟目錄** 按鈕會開啟您的目錄(例如 `http://localhost:4502/editor.html/content/test-catalog.html`)。

#### 產生目錄 — Classic UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目錄將參考您的 [產品資料](#products-and-product-variants).

1. 使用 **網站** 主控台，導覽至 **目錄Blueprint**，然後基本目錄。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用建立新頁面 **區域Blueprint** 範本。

   例如：`Swimwear`。

1. 開啟新的 `Swimwear` 頁面，然後按一下 **編輯Blueprint** 以開啟 **屬性** 對話方塊，您可以在此設定 **產品** 選取。

   例如，開啟 **標籤/關鍵字** 欄位以選取「活動」，然後從「Geometrixx — 戶外」區段選取「游泳」。

1. 按一下 **確定** 以儲存您的屬性；範例產品將顯示在 **產品選擇條件** 在blueprint頁面上。
1. 按一下 **轉出變更……**，選取 **轉出頁面和所有子頁面**，然後按一下 **下一個** 則 **轉出**. 轉出成功完成後， **狀態** 指示器會顯示為綠色。
1. 您現在可以按一下 **關閉** 和勾選新目錄區段；例如，在和底下：

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 再次從Blueprint頁面按一下 **編輯Blueprint** 和 **屬性** 對話方塊開啟 **產生的頁面** 標籤。 在「橫幅」清單欄位中，選取您要顯示的影像；例如， `summer.jpg`
1. 按一下 **確定** 以儲存屬性；橫幅資訊會顯示在 **產品選擇條件** 在blueprint頁面上。
1. 轉出這些新變更。

### 轉出目錄 {#rolling-out-a-catalog}

#### 轉出目錄 — 觸控最佳化UI {#rolling-out-a-catalog-touch-optimized-ui}

轉出目錄：

1. 導覽至 **目錄** 主控台，透過 **商務**.
1. 導覽至您要轉出的目錄。
1. 使用：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **轉出變更** 圖示：

   ![转出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在精靈中，視需要設定轉出，然後點選/按一下 **轉出變更**.
1. 對話方塊開啟。 點選/按一下 **完成** 程式完成時。

#### 轉出目錄 — Classic UI {#rolling-out-a-catalog-classic-ui}

轉出目錄：

1. 導覽至您要轉出的目錄。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 按一下 **轉出變更……**
1. 視需要設定轉出。
1. 按一下 **轉出**.

### Blueprint Importer {#blueprint-importer}

#### Blueprint Importer — 觸控最佳化UI {#blueprint-importer-touch-optimized-ui}

1. 導覽至 **目錄** 主控台，透過 **商務**.
1. 導覽至您要匯入目錄Blueprint的位置。
1. 點選/按一下 **匯入Blueprint** 圖示。

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在精靈中，視需要選取來源，然後點選/按一下 **下一個**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. 點選/按一下 **完成** 匯入完成後。

#### Blueprint Importer — 傳統UI {#blueprint-importer-classic-ui}

1. 使用 **工具** 主控台，導覽至 **商務**.

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 開啟 **目錄Blueprint匯入工具**.
1. 視需要設定匯入。
1. 按一下 **匯入目錄Blueprint**.

## 促销活动 {#promotions}

### 建立促銷活動 {#creating-a-promotion}

#### 建立促銷活動 — Classic UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>下列範例會處理直接在中持有的促銷活動 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)，此資料用於憑單。
>
>促銷活動也可以位於 [體驗](/help/sites-authoring/personalization.md) 在行銷活動中。
>
>如需詳細資訊，請參閱 [促銷活動和憑單](#promotions-and-vouchers).

1. 開啟 **網站** 作者執行個體的主控台。
1. 在左側窗格中，選取您需要的專案 **Campaign**.
1. 按一下 **新增**，選取 **促銷活動** 範本，然後指定 **標題** (和 **名稱** （若有需要）。
1. 单击&#x200B;**创建**。新的促銷活動頁面將顯示在右側窗格中。

1. 編輯 **屬性** 透過以下其中一種方式：

   * 開啟頁面，然後按一下「編輯」按鈕以開啟「屬性」對話方塊
   * 在網站主控台中選取頁面，然後使用內容功能表（通常是滑鼠右鍵）來選取 **屬性……** 並開啟「屬性」對話方塊

   指定 **促銷活動型別**， **折扣型別**， **折扣值** 和任何其他必要欄位。

1. 按一下 **確定** 以儲存。

1. 您現在可以啟動促銷活動，讓購物者可以在發佈執行個體上看到。

## 优惠券 {#vouchers}

### 建立憑單 {#creating-a-voucher}

#### 建立憑單 — 傳統UI {#creating-a-voucher-classic-ui}

1. 開啟 **網站** 作者執行個體的主控台。
1. 在左側窗格中，選取您需要的專案 **Campaign**.
1. 按一下 **新增**，選取 **憑單** 範本，然後指定 **標題** (和 **名稱** （若有需要）。
1. 单击&#x200B;**创建**。新的憑單頁面將顯示在右窗格中。

1. 連按兩下以開啟您的新憑單頁面，然後按一下 **編輯** 以視需要設定資訊。
1. 按一下 **確定** 以儲存。

1. 您現在可以啟用憑單，讓購物者可以在發佈執行個體的購物車中使用它。

### 移除憑單 {#removing-vouchers}

#### 移除憑單 — Classic UI {#removing-vouchers-classic-ui}

若要讓憑單無法供客戶使用，您可以：

* 停用憑單 — 它仍可在作者環境中使用，以便您稍後可以重新啟用。
* 完全刪除。

這兩個動作都可以從 **網站** 主控台。

### 修改憑單 {#modifying-vouchers}

#### 修改憑單 — 傳統UI {#modifying-vouchers-classic-ui}

若要變更憑單或促銷活動的屬性，您可以連按兩下 **網站** 主控台並按一下 **編輯**. 儲存後，您應該將其啟動，以便將變更推送至發佈執行個體。

### 新增憑單至購物車 {#adding-vouchers-to-a-cart}

若要讓使用者將憑單新增至購物車，您可以使用內建的 **憑單** 元件（商務類別）。 您需要將此專案新增到顯示購物車的相同頁面（但非必要）。 憑單元件只是使用者可以輸入憑單代碼的表單，購物車元件實際上會顯示套用憑單及其折扣的清單。

在示範網站(Geometrixx Outdoors文 — 英文)中，您可以在購物車頁面上實際購物車下方看到憑單表單。

## 订单 {#orders}

>[!NOTE]
>
>請記住，現成可用的AEM並不具備與訂單相關的標準功能所需的動作，例如退回商品、更新訂單狀態、執行履行、產生包裝單。 其主要用途為技術預覽。
>
>AEM中的通用訂單管理保持為基本；精靈中可用的欄位取決於支架：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果您建立自訂的支架，可以儲存更多訂單資訊。

>[!NOTE]
>
>訂單主控台會公開永遠不會發佈的廠商訂單資訊。
>
>客戶訂單資訊會儲存在其主目錄中，並由其帳戶的「訂單歷史記錄」顯示。 此資訊會與其主目錄的其他部分一起發佈。

### 建立訂單資訊 {#creating-order-information}

#### 建立訂單資訊 — 觸控最佳化UI {#creating-order-information-touch-optimized-ui}

1. 使用 **訂購** 主控台導覽至所需位置。
1. 使用 **建立** 圖示以選取 **建立訂單**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 精靈將會開啟。 使用 **基本**， **內容**， **付款** 和 **履行** 標籤以輸入 [新訂單的相關資訊](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. 選取 **建立** 以儲存資訊。

### 編輯訂單資訊 {#editing-order-information}

#### 編輯訂單資訊 — 觸控最佳化UI {#editing-order-information-touch-optimized-ui}

1. 使用 **訂購** 主控台導覽至訂單。
1. 使用：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **檢視訂單資料** 圖示：

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 此 [訂單資訊](/help/commerce/cif-classic/administering/concepts.md#order-information) 將會顯示。 使用 **編輯** 和 **完成** 以進行任何變更。

