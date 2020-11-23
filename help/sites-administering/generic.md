---
title: 管理通用电子商务
seo-title: 管理通用电子商务
description: AEM通用解决方案提供了管理存储库中的商务信息的方法。
seo-description: AEM通用解决方案提供了管理存储库中的商务信息的方法。
uuid: 8d2b02a6-0658-4957-a366-29a59350f3e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 9167cbe2-2efb-422d-b58b-0c24b9476fe6
docset: aem65
translation-type: tm+mt
source-git-commit: 06d6696a5493f0e166e400bcd9a379b7be062c1e
workflow-type: tm+mt
source-wordcount: '3011'
ht-degree: 4%

---


# 管理通用电子商务 {#administering-generic-ecommerce}

AEM通用解决方案提供了管理存储库中的商务信息的方法（与使用外部电子商务引擎相比）。 这包括：

* [产品](/help/sites-administering/concepts.md#products)
* [产品的系列品种](/help/sites-administering/concepts.md#product-variants)
* [目录](/help/sites-administering/concepts.md#catalogs)
* [促销活动](/help/sites-administering/concepts.md#promotions)
* [优惠券](/help/sites-administering/concepts.md#vouchers)
* [订单](/help/sites-administering/concepts.md#shopping-cart-and-orders)
* [代理页](/help/sites-administering/concepts.md#proxy-pages)

>[!NOTE]
>
>标准AEM安装包括通用AEM(JCR)电子商务实施。
>
>它当前用于演示目的，或根据您的要求作为自定义实施的基本基础。

## 产品和产品变量 {#products-and-product-variations}

>[!NOTE]
>
>以下过程适用于产品和产品变体。

在创建产品之前，您需要定义基 [架](/help/sites-authoring/scaffolding.md)。 这指定了定义产品以及编辑产品时所需的字段。

每个不同的产品类型都需要一个scaffold。 相应的scaffold通过以下任一方式与产品关联：

* 路径
* product can reference the scaffold

>[!NOTE]
>
>Geometrixx-Outdoors商店具有单一产品类型（因此为单一基架）:
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-Outdoors产品类型在以下位置处处于活动状态：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在其下的任意位置创建新产品定义，而无需任何其他设置。

### 正在导入产品 {#importing-products}

#### 导入产品——触屏优化UI {#importing-products-touch-optimized-ui}

1. 通过商务 **导航到** “产品” **控制台**。
1. 使用产 **品控制台** ，导航到所需的位置。
1. 使用“ **导入产品** ”图标打开向导。

   ![chlimage_1-1](do-not-localize/chlimage_1-13.png)

1. 指定：

   * **导入程序**

      默认情况下，特定商 [务提供程序](/help/sites-administering/concepts.md#commerce-providers)的导入程序 `Geometrixx`。

   * **源**

      要导入的文件；您可以使用浏览器选择文件。

   * **增量导入**

      指示这是否是增量导入（与完全导入相对）。
   >[!NOTE]
   >
   >增量导入（示例geometrixx-outdoor导入程序的）在产品级别操作。
   >
   >可以根据需要定义自定义导入程序以运行。

1. 选 **择** “下一步”以导入产品，将显示所执行操作的日志。

   >[!NOTE]
   >
   >产品将导入到当前位置或相对于当前位置。

   >[!NOTE]
   >
   >重复使 **用** Next **和Back** 将重复导入产品定义。 但是，由于它们有相同的SKU，存储库中的现有信息将被覆盖。

1. 选择 **完成** ，以关闭向导。

#### 导入产品——经典UI {#importing-products-classic-ui}

1. 使用工 **具控制台** ，打开商 **务文** 件夹。
1. 多次-单击以打开产 **品导入程序**:

   ![chlimage_1-22](assets/chlimage_1-22.jpeg)

1. 指定：

   * **存储名称**

      产品将导入到：

      `/etc/commerce/products/<*store name*>/`

   * **商业提供程序**

      您的商务提供商 [的导入程序](/help/sites-administering/concepts.md#commerce-providers);默认Geometrixx。

   * **源文件**

      要导入的文件在存储库中的位置。

   * **增量导入**

      指示这是否是增量导入（与完全导入相对）。

1. 单击“ **导入产品**”。

### 创建产品信息 {#creating-product-information}

>[!NOTE]
>
>标准产品管理是基本的，因为Geometrixx-Outdoors产品集一直是基本的。 复杂性基于产品基架 [](/help/sites-authoring/scaffolding.md)，因此使用您自己的产品基架可以实现更复杂的编辑。

#### 创建产品信息——触屏优化UI {#creating-product-information-touch-optimized-ui}

1. 使用产 **品控制台** (通过 **商务**)导航到所需的位置。
1. 使用创 **建图** 标选择以下任一选项（取决于结构和位置）:

   * **创建产品**
   * **创建产品变体**

   ![chlimage_1-14](do-not-localize/chlimage_1-14.png)

1. 将打开向导。 使用 **基本** 和 **产品选项卡** ，输入新产 [品或产品变](/help/sites-administering/concepts.md#product-attributes) 型的产品属性。

   >[!NOTE]
   >
   >**标题** 和 **** SKU是创建产品或变型所需的最低版本。

1. 选择 **创建** ，以保存信息。

>[!NOTE]
>
>许多产品提供各种颜色和／或尺寸。 有关基本产品和相关产品变体的信息都可以从“产品”控制台 **进行** 管理。
>
>产品及其变体以树结构形式存储，产品信息位于顶部，变体位于下面（此结构由UI强制实施）。

### 编辑产品信息 {#editing-product-information}

>[!NOTE]
>
>Product images in geometrixx-outdoors are served from:
>
>`/etc/commerce/products/...`
>
>这意味着，默认情况下，调度程序会阻止 [它们](https://helpx.adobe.com/cn/experience-manager/dispatcher/using/dispatcher-configuration.html)，因此请根据需要进行配置。

#### 编辑产品信息——触屏优化UI {#editing-product-information-touch-optimized-ui}

1. 使用产 **品控制台** (通过 **商务**)导航到您的产品信息。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择“ **视图产品** ”图标：

   ![chlimage_1-3](do-not-localize/chlimage_1-15.png)

1. 将 [显示产](/help/sites-administering/concepts.md#product-attributes) 品属性。 使用 **编辑****和完** 成进行任何更改。

### 显示产品引用 {#showing-product-references}

#### Showing Product References - Touch-optimized UI {#showing-product-references-touch-optimized-ui}

1. 使用产 **品控制台** (通过 **商务**)导航到您的产品信息。
1. 打开引用的辅助边栏，并显示以下图标：

   ![chlimage_1-4](do-not-localize/chlimage_1-16.png)

1. 选择所需产品——辅助边栏将更新以显示可用的引用类型：

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 单击／点按引用类型（例如产品页面）以展开列表。
1. 选择特定引用以显示选项：

   * 导航到产品页面
   * 编辑产品页面

   ![chlimage_1-89](assets/chlimage_1-89.png)

### Search for Products {#search-for-products}

1. 通过商务 **导航到** “产品” **控制台**。
1. 使用图标打开“搜索”的辅助边栏：

   ![](do-not-localize/chlimage_1-17.png)

1. 您可以使用多个彩块化来搜索产品。 搜索只能使用一个或多个彩块化。 将显示找到的产品：

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 单击／点按产品可打开它。 您还可以发布产品或视图产品数据。

#### 扩展搜索 {#extending-search}

您可以修改现有彩块化或添加新彩块，使用CRXDE Lite:

1. 导航至:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以修改将在产品搜索页面上显示的大小。 单击节 `sizegroup` 点。
1. 单击 `items` 节点，然后单击 `propertypredicate` 节点。
1. 您可以修改 `propertyValues`。 例如，您可以添加XS、XXL或删除大小。
1. 单击 **全部保存** ，然后导航到产品搜索页面。 您所做的更改应当出现。

### 多个资产 {#multiple-assets}

您可以在产品组件中添加多个资产，然后指定将在产品页面上显示的资产。

>[!NOTE]
>
>与多个资产相关的所有操作均可通过触屏优化UI完成。

#### 添加多个资产 {#adding-multiple-assets}

1. 通过商务 **导航到** “产品” **控制台**。
1. 使用产 **品控制台** ，导航到所需的产品。

   >[!NOTE]
   >
   >您必须处于产品级别，而不是变体级别。

1. 点按／单击 **视图产品** “数据”图标以进行选择模式或快速操作。
1. 点按／单击编辑图标。
1. 滚动到 **添加**。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 点按／单击 **添加**。 此时会显示新的资产占位符。
1. 点按／单击**更改**会打开一个对话框，通过该对话框可以选择资产。
1. 选择要添加的资产。

   >[!NOTE]
   >
   >您可以选择的资产来自 [资产](https://helpx.adobe.com/experience-manager/aem-previous-versions.html#assets)。

1. 点按／单击完成图标。

现在，两个资产存储在您的产品组件中。 您可以配置产品页面上将显示哪个页面。 这适用于类别系统。 首先，您需要向单个资产添加类别:

1. 点按／单击 **视图产品数据**。
1. 在资产 **下键入资** 产类别 `cat1` ，例如 `cat2`和。

   >[!NOTE]
   >
   >您还可以对类别使用标记。

1. 点按／单击完成图标。 您现在必须转 [出您](#rolling-out-a-catalog) 的更改。

现在，您的资产在产品组件中具有类别。 您可以配置在三个不同级别显示哪些类别:

* [产品页面](#product-page)
* [目录](#catalog)
* [产品控制台](#products-console)

>[!NOTE]
>
>如果您未设置类别，则第一个资产将显示在产品页面上。

选择要显示的图像的机制如下：

1. 验证是否已为产品页面设置类别。
1. 否则，验证是否为目录设置了类别。
1. 否则，验证是否已为产品控制台设置类别。

>[!NOTE]
>
>对于目录级别和产品控制台级别，您必须转出更改以应用修改并查看产品页面上的差异。

#### 产品页面 {#product-page}

1. 导航到您的产品页面。
1. **编辑** “产品”组件。
1. 键入您 **选择的图** 像类别 `cat1` （例如）。
1. 点按／单击 **完成**。 页面会刷新，此时应显示正确的资产。

#### 目录  {#catalog}

1. 导航到您的目录。
1. 点按／单击 **视图属性**。
1. Tap/click **Edit**.
1. 点按／单击资 **产选** 项卡。
1. 键入所需的 **产品资产类别**。
1. 点按／单击 **完成**。
1. [转出您](#rolling-out-a-catalog) 的更改。

#### 产品控制台 {#products-console}

1. 使用产 **品控制台** ，导航到所需的产品。
1. 点按／单击 **视图产品数据**。
1. Tap/click **Edit**.
1. 键入默 **认资产类别**。
1. 点按／单击 **完成**。
1. [转出您](#rolling-out-a-catalog) 的更改。

### 发布／取消发布产品信息 {#publishing-unpublishing-product-information}

#### 发布／取消发布产品信息——触屏优化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>产品信息通常通过引用它的页面发布。 例如，在发布引用产品Y的页面X时，AEM将询问您是否也要发布产品Y。
>
>对于特殊情况，AEM还支持从产品数据直接发布。

1. 使用产 **品控制台** (通过 **商务**)导航到您的产品信息。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   根据需要 **选择** “发 **布”或** “取消发布”图标：

   ![chlimage_1-6](do-not-localize/chlimage_1-18.png) ![chlimage_1-7](do-not-localize/chlimage_1-19.png)

   将根据需要发布或取消发布产品信息。

### Product Feed {#product-feed}

Search&amp;Promote集成允许您：

* 使用独立于基础存储库结构和商务平台的eCommerce API。
* 利用Search&amp;Promote的索引连接器功能以XML格式提供产品源。
* 利用Search&amp;Promote的远程控制功能执行产品源的按需或计划请求
* 不同Search&amp;Promote帐户的源生成，配置为云服务配置。

有关详细信息，请阅 [读产品信息](/help/sites-administering/product-feed.md)。

### 产品更新的事件处理程序 {#event-handler-for-product-updates}

有一个事件处理程序，它在添加、修改或删除产品以及添加、修改或删除产品页面时记录事件。 有以下OSGi事件:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

对于 `PRODUCT_*` 事件，路径指向中的基本产品 `/etc/commerce/products`。 对于 `PRODUCT_PAGE_*` 事件，路径指向节 `cq:Page` 点。

您可以在OSGI事件()的Web控制台中查 `/system/console/events`看它们，例如：

![](do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另请阅读 [AEM中的事件处理](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)。 [](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)

### 添加到购物车图像链接 {#image-with-add-to-cart-links}

The Image with Add to Cart Links component allows you to quickly add a product to the cart by creating a hotspot linked with a product on an image.

单击热点会打开一个对话框，通过该对话框可选择产品的大小和数量。

1. 导航到要添加组件的页面。
1. 在页面中拖放组件。
1. 从资产浏览器在组件中拖放 [图像](/help/sites-authoring/author-environment-tools.md#assets-browser)。
1. 您可以：

   * 单击组件，然后单击编辑图标
   * 慢速单击多次

1. 单击全屏图标。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 单击启动映射图标。

   ![chlimage_1-93](assets/chlimage_1-93.png)

1. 单击其中一个形状图标。

   ![chlimage_1-29](do-not-localize/chlimage_1-21.png)

1. 根据需要修改和移动形状。
1. 单击形状。
1. 单击浏览图标可打开资产 [选取器](../assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，您也可以直接键入必须位于产品级别而非变体级别的产品路径。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 单击确认图标两次，然后单击退出全屏。
1. 单击组件旁边的页面上的某处。 页面应刷新，并且图像上应显示以下符号：

   ![](do-not-localize/chlimage_1-22.png)

1. Switch to [preview](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) mode.
1. 单击+热点。 此时会打开一个对话框，您可以从中选择您在路径中输入的产品的大小和 **数量**。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 输入大小和数量。
1. 单击“添加到购物车”按钮。 对话框关闭。
1. 导航到购物车。 产品应该在此处。

#### Configuration Options {#configuration-options}

您可以配置单击热点时对话框的外观：

1. 单击组件，然后单击配置图标。

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. 向下滚动. “ADD TO **CART”（添加到购物车）选** 项卡。

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. 单击 **添加到购物车**。 您可以使用3个配置选项。

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. 单击完成图标。

## 目录 {#catalogs}

### 生成目录 {#generating-a-catalog}

#### 生成目录——触屏优化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目录将引用您的产品数据。

要生成目录，请执行以下操作：

1. 打开“站点”控制台（例如，[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)）。
1. 导航到要创建新页面的位置。
1. 要打开选项列表，请使用“**创建**”图标：

   ![](do-not-localize/chlimage_1-23.png)

1. From the list select **Create Catalog**, the Create Catalog wizard will open.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. 导航到所需的Catalog Blueprint。
1. 点按／单 **击** “选择”按钮，然后点按／单击所需的目录Blueprint。
1. Tap/click **Next**.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. 键入 **标题** 和 **名称**。
1. 点按／单击创 **建** 按钮。 将创建目录并打开一个对话框。

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. 点按／单 **击** “完成”按钮将返回站点控制台，您将能够在该控制台中看到您的目录。

   点按／单 **击“打开** 目录”按钮可打开您的目录(例如 `http://localhost:4502/editor.html/content/test-catalog.html`)。

#### 生成目录——经典UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目录将引用您的 [产品数据](#products-and-product-variants)。

1. 使用网 **站** 控制台，依次导航到 **目录Blueprint**、基本目录。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用Section Blueprint模板创 **建新页面** 。

   For example, `Swimwear`.

1. 打开新页 `Swimwear` 面，然后单 **击Edit Blueprint** ，打开 **“属性** ”对话框，在该对话框中可设置“产 **品** ”选项。

   例如，打开“标 **签／关键字** ”字段以选择活动，然后从“Geometrixx-户外”部分中选择“游泳”。

1. 单击 **确定** ，以保存您的属性；示例产品将显示在blueprint页 **面的“产品选择** 标准”下。
1. 单击“转 **出更改……**”，选择“转 **出”页和所有子页**，然后单击“下一 **步** ”, **再**&#x200B;单击转出。 成功完成转出后，状 **态** 指示符将显示为绿色。
1. 您现在可以单击“ **关闭** ”并检查新目录部分；例如，on和under:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 再次从Blueprint页面单击 **编辑Blueprint** ，在“属性” **对话框中打开** “生 **成的页面** ”选项卡。 在“横幅列表”字段中，选择要显示的图像；例如， `summer.jpg`
1. 单击 **确定** ，以保存您的属性；横幅信息将显示在blueprint页 **面的“产品选择** 标准”下。
1. 转出这些新更改。

### Rolling Out a Catalog {#rolling-out-a-catalog}

#### Rolling out a Catalog - Touch-optimized UI {#rolling-out-a-catalog-touch-optimized-ui}

转出目录：

1. 通过商务 **导航到** “目录” **控制台**。
1. 导航到要转出的目录。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择转 **出更改** 图标：

   ![](do-not-localize/chlimage_1-24.png)

1. 在向导中，根据需要设置转出，然后点按／单击转 **出更改**。
1. 将打开一个对话框。 在流程完 **成后** ，点按／单击完成。

#### Rolling out a Catalog - Classic UI {#rolling-out-a-catalog-classic-ui}

转出目录：

1. 导航到要转出的目录。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 单击 **转出更改……**
1. 根据需要设置转出。
1. 单击 **转出**。

### Blueprint Importer {#blueprint-importer}

#### Blueprint Importer —— 触屏优化UI {#blueprint-importer-touch-optimized-ui}

1. 通过商务 **导航到** “目录” **控制台**。
1. 导航到要导入目录蓝图的位置。
1. 点按／单击“导 **入Blueprint** ”图标。

   ![](do-not-localize/chlimage_1-13.png)

1. 在向导中，根据需要选择源，然后点按／单击 **下一步**。

   ![chlimage_1-340](assets/chlimage_1-102.png)

1. 完成导入 **后** ，点按／单击完成。

#### Blueprint Importer - Classic UI {#blueprint-importer-classic-ui}

1. 使用工 **具控制** 台，导航到 **商务**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 打开“ **目录蓝印导入程序**”。
1. 根据需要设置导入。
1. 单击“ **导入目录Blueprint**”。

## 促销活动 {#promotions}

### 创建促销 {#creating-a-promotion}

#### 创建促销——经典UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>以下示例处理直接在活动中持有的促销 [](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md),this用于凭证。
>
>促销活动也可以包含 [在活动](/help/sites-authoring/personalization.md) 中的体验中。
>
>有关详细信息，请 [参阅Promotions and Vouchers](#promotions-and-vouchers)。

1. 打开创 **作实例** 的网站控制台。
1. 在左窗格中，选择所需的 **活动**。
1. 单击“ **新建**”，选 **择“升级** ”模板，然后为新凭证指 **定标题** ( **** 如果需要，请指定名称)。
1. 单击&#x200B;**创建**。新的促销页面将显示在右侧窗格中。

1. 通过以下任 **一方** 式编辑属性：

   * 打开页面，然后单击编辑按钮以打开属性对话框
   * 在“网站”控制台中选择页面，然后使用上下文菜单（通常是鼠标右键）选 **择“属性。.** .”并打开属性对话框

   根据需 **要指定**“促销 **类型”**、“折扣类型 **”、“折** 扣值”和任何其他字段。

1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活您的促销，以便购物者在发布实例中看到它。

## 优惠券 {#vouchers}

### 创建凭证 {#creating-a-voucher}

#### 创建凭证——经典UI {#creating-a-voucher-classic-ui}

1. 打开创 **作实例** 的网站控制台。
1. 在左窗格中，选择所需的 **活动**。
1. 单击“ **新建**”，选 **择凭证模板，然后为新凭证指** 定标题 **(****** 如果需要，请指定名称)。
1. 单击&#x200B;**创建**。The new voucher page will be shown in the right-hand pane.

1. 打开新的凭证页面并多次单击，然后单 **击** Edit以根据需要配置信息。
1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活您的凭证，以便购物者可以在发布实例上的购物车中使用它。

### 删除凭证 {#removing-vouchers}

#### 删除凭证——经典UI {#removing-vouchers-classic-ui}

In order to make a voucher unavailable to customers, you can either:

* 取消激活凭证——它将保留在作者环境上，以便您稍后重新激活它。
* 完全删除它。

这两种操作都可以从网站控 **制台完** 成。

### Modifying Vouchers {#modifying-vouchers}

#### Modifying Vouchers - Classic UI {#modifying-vouchers-classic-ui}

要更改凭证或促销的属性，可以在“网站”控制台上多次并 **单击** “编辑 **”**。 保存后，应激活它，以便将更改推送到发布实例。

### 将优惠券添加到购物车 {#adding-vouchers-to-a-cart}

要允许用户向购物车添加凭证，您可以使用内置的 **凭证** 组件(商务类别)。 您需要将它添加到显示购物车的同一页面（但不是强制）。 The vouchers component is only a form which the user can enter a voucher code, it is the shopping cart component that actually shows the列表 of applied vouchers and their discount.

在demo site(Geometrixx Outdoors语——英语)中，您可以在购物车页面上的实际购物车下看到凭证表单。

## 订单 {#orders}

>[!NOTE]
>
>应记住，现成的AEM没有与订单相关的标准功能（如退货、更新订单状态、执行、生成装箱单）所需的操作。 它主要用作技术预览。
>
>AEM的通用订单管理一直是基本的；向导中可用的字段取决于scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果创建自定义基架，则可以存储更多订单信息。

>[!NOTE]
>
>订单控制台会显示供应商订单信息，该信息从不发布。
>
>客户订单信息保留在其主目录中，并由其帐户的订单历史记录公开。 此信息与其主目录的其余部分一起发布。

### 创建订单信息 {#creating-order-information}

#### 创建订单信息——触屏优化UI {#creating-order-information-touch-optimized-ui}

1. 使用“订 **单** ”控制台定位到所需的位置。
1. 使用创 **建图** 标选择 **创建顺序**。

   ![](do-not-localize/chlimage_1-14.png)

1. 将打开向导。 使用“基 **本**”、“ **内容**”、“ **付款”** 和“履行”标签 ****[](/help/sites-administering/concepts.md#order-information)输入有关新订单的信息。

1. 选择 **创建** ，以保存信息。

### 编辑订单信息 {#editing-order-information}

#### 编辑订单信息——触屏优化UI {#editing-order-information-touch-optimized-ui}

1. 使用“订 **单** ”控制台定位至订单。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择“ **视图顺序** ”图标：

   ![](do-not-localize/chlimage_1-15.png)

1. 将 [显示订](/help/sites-administering/concepts.md#order-information) 单信息。 使用 **编辑****和完** 成进行任何更改。

