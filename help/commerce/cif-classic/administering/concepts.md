---
title: '概念 '
description: 使用AEM进行电子商务的一般概念。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '4525'
ht-degree: 1%

---

# 概念 {#concepts}

集成框架提供了以下机制和组件：

* 与电子商务引擎的连接
* 将数据提取到AEM
* 显示该数据并收集购物者的响应
* 返回交易详细信息
* 从两个系统中搜索数据

这意味着：

* 购物者无需等待即可注册和购物。
* 购物者将立即看到价格变化。
* 产品可以根据需要添加。

>[!NOTE]
>
>电子商务框架可与以下内容一起使用：
>
>* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAPCommerce Cloud](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)



>[!CAUTION]
[电子商务集成框架](https://www.adobe.com/solutions/web-experience-management/commerce.html)是AEM附加组件。
您的销售代表将能够根据相应的引擎提供完整的详细信息。

>[!CAUTION]
该框架为您自己的项目提供了基本要求。
要使框架符合您的规范，始终需要进行一定量的开发工作。

>[!CAUTION]
标准AEM安装包括通用AEM(JCR)电子商务实施。
此功能当前用于演示目的，或根据您的要求作为自定义实施的基本基础。

为了优化操作，AEM和电子商务引擎都集中在自己的专业领域。 信息在两者之间实时传输；例如：

* AEM可以：

   * 请求：

      * 电子商务引擎中的产品信息。
   * 提供：

      * 产品信息、购物车和结账的用户查看。
      * 将购物车和结帐信息发送到电子商务引擎。
      * 搜索引擎优化(SEO)。
      * 社区功能。
      * 非结构化的营销互动。


* 电子商务引擎可以：

   * 提供：

      * 数据库中的产品信息。
      * 产品变体管理。
      * 订单管理。
      * ERP（企业资源规划）。
      * 在产品信息中搜索。
   * 进程:

      * 购物车。
      * 结帐。
      * 订单履行。


>[!NOTE]
具体详细信息取决于电子商务引擎和项目实施。

提供了许多现成的AEM组件来使用集成层。 目前，这些服务包括：

* 产品信息
* 购物车
* 结帐
* 我的帐户

还提供各种搜索选项。

## 架构 {#architecture}

集成框架提供了API、一系列用于说明功能的组件以及多个用于提供连接方法示例的扩展：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

利用框架，可访问以下功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 实施 {#implementations}

AEM eCommerce通过电子商务引擎实施：

* 构建电子商务集成框架后，您可以轻松地将电子商务引擎与AEM集成。 用途构建的电子商务引擎控制产品数据、购物车、结帐和订单履行，而AEM则控制数据显示和营销活动。


>[!NOTE]
标准AEM安装包括通用AEM(JCR)电子商务实施。
此功能当前用于演示目的，或根据您的要求作为自定义实施的基本基础。
在AEM中使用基于JCR的通用开发实现的AEM eCommerce包括：
* 一个独立的AEM原生电子商务示例，用于说明API的使用。 它可用于控制产品数据、购物车和结账，以及与现有数据显示和营销活动结合使用。 在这种情况下，产品数据库存储在AEM的本机存储库(Adobe的[JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)实施)中。

标准AEM安装包含[通用电子商务实施](/help/commerce/cif-classic/administering/generic.md)的基础知识。

### 商务提供程序{#commerce-providers}

将数据从商务引擎导入AEM电子商务网站时，会使用商务提供商为导入程序提供数据。 一个商务提供商可以支持多个导入程序。

商务提供商是自定义为以下任一项的AEM代码：

* 后端商务引擎的界面
* 在JCR存储库上实施商务系统

AEM当前提供两个商务提供程序示例：

* geometrixx-hybris的一个
* 适用于geometrixx-generic(JCR)的另一个

尽管通常，项目需要开发他们自己的自定义商务提供商，以特定于其PIM和产品数据架构。

>[!NOTE]
geometrixx导入程序使用CSV文件；其实施上方的注释中提供了已接受的架构（允许使用自定义属性）的描述。

[ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html)维护（通过[OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)）[ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html)和[CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html)接口的实施列表。 导入程序向导的&#x200B;**导入程序/商务提供程序**&#x200B;下拉字段中列出了这些内容（使用`commerceProvider`属性作为名称）。

当下拉菜单中提供了特定的导入器/商务提供程序时，必须在以下任一位置定义所需的任何补充数据（取决于导入器类型）：

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

相应`importers`文件夹下的文件夹必须与导入程序名称匹配；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

源导入文件的格式由导入器定义。 或者，导入程序可以建立与商务引擎的连接（例如WebDAV或http）。

## 角色 {#roles}

集成系统可满足以下角色以维护数据：

* 产品信息管理(PIM)维护以下各项的用户：

   * 产品信息。
   * 分类、分类、批准。
   * 与数字资产管理交互。
   * 定价 — 这通常来自ERP系统，并且没有在商务系统中明确维护。

* 作者/营销经理负责维护：

   * 所有渠道的营销内容。
   * 促销活动.
   * 优惠券.
   * 营销活动.

* 冲浪者/购物者：

   * 查看您的产品信息。
   * 将项目放入购物车。
   * 查他们的订单。
   * 预期订单履行。

尽管实际位置可能取决于您的实施；例如，使用电子商务引擎的通用或：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 产品 {#products}

### 产品数据与营销数据{#product-data-versus-marketing-data}

#### 结构性与营销类别{#structural-versus-marketing-categories}

如果可以区分以下两个类别，则这样您就可以明确具有有意义结构（`cq:Page`节点的树）的URL，因此非常接近经典的AEM内容管理):

* *结构*类别

   定义&#x200B;*什么是产品的类别树*;例如：

   `/products/mens/shoes/sneakers`

* ** 营销类别

   *产品的所有其他类别都属于*;例如：

   `/special-offers/christmas/shoes`)

### 产品数据 {#product-data}

要描述和管理您的产品，您需要掌握与其相关的一系列信息。

产品数据可以是：

* 直接在AEM中维护（通用）。
* 维护，并在AEM中提供。

   根据数据类型，它将根据需要设置为[synchronized](#catalog-maintenance-data-synchronization)，或直接访问；例如，在每个页面请求中，都会从电子商务引擎中检索高度易变且关键的数据（如产品价格），以确保这些数据始终处于最新状态。

无论哪种情况，在将产品数据输入/导入AEM后，都可以从&#x200B;**Products**&#x200B;控制台中查看。 在此，产品的卡片视图和列表视图显示以下信息：

* 图像
* SKU代码
* 上次修改时间

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 产品的系列品种 {#product-variants}

对于适当的产品，还可以保存有关变体的信息。 例如，对于可用不同颜色的服装项目，将作为变体保留：

![ecomcenterproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 产品属性{#product-attributes}

有关每个产品的单个属性可能取决于所使用的电子商务引擎和您的AEM实施。 在查看产品页面和/或编辑产品信息时，这些功能（视情况而定）可用，并且可以包括：

* **图像**

   产品的图像。

* **标题**

   产品名称。

* **描述**

   产品的文本描述。

* **标记**

   用于对相关产品进行分组的标记。

* **默认资产类别**

   资产的默认类别。

* **ERP 数据**

   企业资源规划(ERP)信息。

   * **SKU**

      库存单位(SKU)信息。

   * **颜色**
   * **大小**
   * **价格**

      产品的单价。

* **摘要**

   产品功能的摘要。

* **功能**

   产品功能的更完整详细信息。

### 产品资产{#product-assets}

可为单个产品保留资产选项。 通常包括图像和视频。

## 目录 {#catalogs}

目录可将产品数据分组在一起，以便于管理和呈现给购物者。 通常，目录会根据语言、地理区域、品牌、季节、爱好、体育等属性进行结构化。

### 目录结构{#catalog-structure}

#### 多语言目录{#catalogs-in-multiple-languages}

AEM支持多种语言的产品内容。 在请求数据时，集成框架会从当前树中检索语言（例如，`/content/geometrixx-outdoors/en_US`下页面的`en_US`）。

对于多语言商店，可以单独导入每个语言树的目录（或通过[MSM](/help/sites-administering/msm.md)复制目录）。

#### 多个品牌的目录{#catalogs-for-multiple-brands}

与语言一样，大型跨国公司可能需要满足多个品牌的需求。

#### 按标记列出的目录{#catalogs-by-tags}

标记还可用于将产品分组到目录中。 这些目录可用于更多动态目录，如季节性选件。

### 目录设置（初始导入）{#catalog-setup-initial-import}

根据您的实施，您可以将基础目录所需的产品数据从以下项目导入AEM:

* CSV文件（用于一般实施）
* 电子商务引擎

### 目录维护（数据同步）{#catalog-maintenance-data-synchronization}

产品数据将不可避免地发生进一步的变化：

* 对于通用实施，可以使用[产品编辑器](/help/commerce/cif-classic/administering/generic.md#editing-product-information)管理这些实施
* 使用[eCommerce引擎时，必须同步更改](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 与电子商务引擎的数据同步（持续）{#data-synchronization-with-an-ecommerce-engine-ongoing}

初始导入后，对产品数据的更改将不可避免。

使用电子商务引擎时，产品数据会在该处维护，需要在AEM中可用。 更新后，需要同步此产品数据。

这取决于数据类型：

* 将[周期性同步与更改的数据馈送一起使用](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing)。

   除此之外，您还可以为快速更新选择特定更新。

* 每个页面请求都会从商务引擎中检索高度易变的数据（如价格信息），以确保数据始终为最新。

### 目录 — 性能和缩放{#catalogs-performance-and-scaling}

从电子商务引擎(PIM)导入具有大量产品（通常超过100,000个）的大目录可能会因节点数量过多而影响系统。 如果产品具有关联的资产（如产品图像），则创作实例的速度也可能会减慢。 这是因为这些资产的后处理是CPU和内存密集型的。

您可以选择各种策略来解决这些问题：

* [分段](#bucketing)  — 以满足大量节点的需求
* [将资产后处理卸载到专用实例](#offload-asset-post-processing-to-a-dedicated-instance)
* [仅导入产品数据](#only-import-product-data)
* [导入限制和批量保存](#import-throttling-and-batch-saves)
* [性能测试](#performance-testing)
* [性能 — 其他](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR节点具有许多直接子节点（例如1000个及以上），则需要存储段（虚拟文件夹）以确保性能不受影响。 导入时会根据算法生成这些值。

这些存储段采用虚拟文件夹的形式，这些文件夹已引入目录结构，但可进行配置，以便在公共URL中不显示。

#### 将资产后处理卸载到专用实例{#offload-asset-post-processing-to-a-dedicated-instance}

此方案涉及设置两个创作实例：

1. 主控创作实例

   从PIM导入产品数据，在PIM上，资产路径的后处理被禁用。

1. 专用DAM创作实例

   从PIM导入和后处理产品资产，然后将这些资产复制回主控创作实例以供使用。

![架构图](/help/sites-administering/assets/chlimage_1-8.png)

#### 仅导入产品数据{#only-import-product-data}

如果产品不包含要导入的资产（图像），则您可以导入产品数据，而不会受资产后处理的影响。

![架构图](/help/sites-administering/assets/chlimage_1-9.png)

#### 性能测试{#performance-testing}

必须在AEM电子商务实施中考虑性能测试：

* 创作环境：

   后台（例如，导入）活动可以与正常用户活动（例如，页面编辑）同时发生，即使前端性能（一般）具有更高的优先级，联机作者看到的性能不佳也会导致无法阻止上线决策的问题。

* 发布环境：

   复制是确保内容快速、可靠地发布的关键过程。 作者如何对要发布的内容进行分组可能会对此产生影响。

* 前端：

   前端和缓存无效的混合情况可能会导致性能意外。 测试有助于避免这些问题。

请注意，此性能测试需要您对目标的了解和分析：

* 内容卷

   * 资产
   * 本地化的I18内部产品和SKU

* 用户活动：

   * 批量版
   * 批量发布
   * 密集搜索请求

* 后台进程

   * 导入
   * 同步更新（例如定价）

* 维护要求（备份、Tar PM优化、数据存储垃圾收集等）

#### 性能 — 其他{#performance-miscellaneous}

对于所有实施，可以牢记以下几点：

* 作为产品，库存单位和类别可能数量众多，请尝试使用最少的节点数来对内容进行建模。

   您拥有的节点越多，内容就越灵活（例如parsys）。 但是，一切都是取舍，在处理（例如）30K产品时（默认情况下），您是否需要个人的灵活性？

* 尽量避免重复（查看本地化），或者在复制时考虑复制将导致的节点数。
* 请尽可能多地标记内容，以便准备查询优化。

   例如：

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   每个内容级别应具有一个标记（即国家/地区、语言、类别、品牌、产品）。 搜索

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   和

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   比搜索要快得多

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技术堆栈中，规划非常分工的内容访问模型和服务。 这是一般的最佳实践，但更为关键的是，在优化阶段，您可以为读取频率很高（并且您不希望使用填充包缓存）的数据添加应用程序缓存。

   例如，属性管理经常是缓存的一个好候选项，因为它涉及通过产品导入更新的数据。
* 请考虑使用[代理页面](#proxy-pages)。

### 目录部分页面{#catalog-section-pages}

目录部分提供了以下内容：

* 类别简介（图像和/或文本）；这也可用于横幅和Teaser以推广特殊优惠
* 链接到该类别中的各个产品
* 链接到其他类别

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 产品页面 {#product-pages}

产品页面提供有关各个产品的全面信息。 还反映了中的动态更新；例如，在电子商务引擎中注册的价格更改。

产品页面是使用&#x200B;**Product**&#x200B;组件的AEM页面；例如，在&#x200B;**商务产品**&#x200B;模板中：

![ecommerce_nairobrunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

产品组件提供：

* 一般产品信息；包括文本和图像。
* 定价；通常在每次显示/刷新页面时从电子商务引擎中检索。
* 产品变型信息；例如，颜色和大小。

此信息允许购物者在将项目添加到购物篮时选择以下内容：

* 颜色和大小变体
* 数量

#### 产品登录页面{#product-landing-pages}

这些是主要提供静态信息的AEM页面；例如，包含指向基础产品页面的链接的简介和概述。

### 产品组件 {#product-component}

可以将&#x200B;**Product**&#x200B;组件添加到任何具有父页面的页面，该页面可传送所需的元数据（即`cartPage`和`cartObject`的路径）。 在演示站点Geometrixx Outdoors中，这由`UserInfo.jsp`提供。

也可以根据您的个人要求自定义&#x200B;**Product**&#x200B;组件。

### 代理页{#proxy-pages}

代理页面用于简化存储库的结构并优化大型目录的存储。

创建目录将为每个产品使用十个节点，因为它为每个产品提供可在AEM中更新和自定义的各个组件。 如果您的目录包含数百个甚至数千个产品，则大量节点可能会成为问题。 要避免任何问题，您可以使用代理页面创建目录。

代理页面使用双节点结构（`cq:Page`和`jcr:content`），该结构不包含任何实际的产品内容。 在请求时，可通过引用产品数据和模板页面来生成内容。

然而，这是一种取舍。 您将无法在AEM中自定义产品信息，将使用标准模板（为您的网站定义）。

>[!NOTE]
如果导入的大目录没有代理页面，则不会遇到任何问题。
您可以随时从一种方法转换到另一种方法。 您还可以转换目录的子部分。

## 促销和凭单{#promotions-and-vouchers}

### 优惠券 {#vouchers}

凭单是一种经过试用和测试的提供折扣的方法，可以吸引购物者购买和/或奖励客户的忠诚度。

* 凭证供应：

   * 优惠券代码（由购物者输入购物车）。
   * 凭证标签（在购物者将其输入购物车后显示）。
   * 促销路径（用于定义凭证应用的操作）。

* 外部商务引擎还可以提供凭证。

在AEM中：

* 凭单是使用“网站”控制台创建/编辑的基于页面的组件。
* **凭证**&#x200B;组件提供：

   * 凭证管理的渲染器；这显示购物车中当前的所有凭证。
   * 用于管理（添加/删除）凭证的编辑对话框（表单）。
   * 向购物车添加/删除凭单所需的操作。

* 凭单没有其自己的开启和关闭日期/时间，但使用其父营销活动的日期/时间。

>[!NOTE]
AEM使用术语&#x200B;**Voucher**，这与术语&#x200B;**Coupon**&#x200B;同义。

### 促销活动 {#promotions}

通过促销活动和凭单，您可以实现以下情景：

* 公司为员工提供自定义价格，这是一个手工编制的用户列表。
* 长期客户可享受所有订单的折扣。
* 在明确定义的时间段内提供的销售价格。
* 客户在上次订单超过特定金额时收到凭证。
* 购买&#x200B;*product-X*&#x200B;的客户在&#x200B;*product-Y*（配对产品）上可享受折扣。

促销活动通常不是由产品信息经理维护，而是由营销经理维护：

* 促销活动是使用“网站”控制台创建/编辑的基于页面的组件。 &quot;
* 促销供应：

   * 优先级
   * 升级处理程序路径

* 您可以将促销活动连接到营销活动以定义其开/关日期/时间。
* 您可以将促销活动与体验关联以定义其区段。
* 未连接到体验的促销活动不会自行触发，但仍可以通过凭单触发。
* 升级组件包含：

   * 用于提升管理的渲染器和对话框
   * 用于渲染和编辑特定于升级处理程序的配置参数的子组件

在AEM中，促销活动还集成到[促销活动管理](/help/sites-authoring/personalization.md)中：

* a [campaign](/help/sites-authoring/personalization.md)指定开/关时间
* [营销活动中的](/help/sites-authoring/personalization.md) ** 体验用于根据资产（Teaserpages、促销活动等）对应的受众区段对资产进行分组

可以在体验中或直接在营销策划中进行促销：

* 如果某个促销活动在体验中进行，则该促销活动会自动应用于受众区段。

   例如，在geometrixx-outdoors示例站点中，促销活动：

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   中，因此每当解析区段(`ordervalueover100`)时，都会自动触发。

* 如果某个促销活动未显示在某个体验中（仅在营销活动中），则该促销活动无法自动应用于受众。 但是，如果购物者将优惠券输入购物车且该优惠券引用促销活动，则仍可以触发该优惠券。

   例如，促销活动：

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   在体验之外，因此从不自动触发(即：基于分段)。 但是，它被凭证引用，该凭证可在文章促销活动中的几个体验中找到。 将这些凭单代码输入购物车将导致触发促销活动。

>[!NOTE]
[hybris ](https://www.hybris.com/modules/promotion) promotion和 [hybris ](https://www.hybris.com/en/modules/voucher) voucherscover影响购物车并与定价相关的所有内容。促销活动特定的营销内容（如横幅等）不属于促销活动的一部分。

## 个性化 {#personalization}

### 客户注册和帐户{#customer-registration-and-accounts}

当购物者注册时，需要在AEM和电子商务引擎之间同步帐户详细信息。 敏感数据是独立保存的，但用户档案是共享的：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

具体机制取决于情景：

1. 这两个系统中都存在用户帐户：

   1. 无需执行任何操作。

1. 用户帐户仅存在于AEM中：

   1. 用户将在电子商务引擎中创建，并使用相同的帐户ID和随机密码，该密码将存储在AEM中。
   1. 随机密码是必需的，因为AEM会在首次调用中尝试登录电子商务引擎（例如，当请求产品页面且电子商务引擎引用价格时）。 由于这是在AEM登录后发生的，因此密码不可用。

1. 用户帐户仅存在于电子商务引擎中：

   1. 该帐户将在AEM中使用相同的帐户ID和密码创建。

使用电子商务引擎时，AEM仅存储帐户ID和密码（可选为用户组）。 所有其他信息都存储在电子商务引擎中。

>[!NOTE]
使用电子商务引擎时，您需要确保为登录AEM实例的用户创建的帐户被复制（例如，通过工作流）到与该引擎通信的任何其他AEM实例。
否则，这些其他AEM实例也将尝试为引擎中的相同用户创建帐户。 这些操作将失败，并且引擎中出现`DuplicateUidException`。

### 客户注册{#customer-sign-up}

购物者需要注册才能访问购物车。 这需要注册（创建帐户），以便能够创建特定于客户的帐户。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
还支持匿名购物车和结账。

### 客户登录{#customer-sign-in}

注册后，购物者可以使用其帐户登录，以便跟踪其操作并完成其订单。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 单点登录{#single-sign-on}

提供单点登录(SSO)，以便作者在AEM和电子商务系统中都是已知的，无需两次登录。

### myAccount {#myaccount}

来自电子商务引擎的交易数据将与有关购物者的个人信息组合在一起。 AEM会将其中一些数据用作用户档案数据。 AEM中表单的操作会将信息写回电子商务引擎。

有一个页面可让您轻松管理帐户信息。 您可以通过单击Geometrixx页面顶部的&#x200B;**My Account**&#x200B;或导航到`/content/geometrixx-outdoors/en/user/account.html`来访问该帐户。

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通讯簿 {#address-book}

您的网站需要存储一系列地址；包括交付、帐单和替代地址。 可以使用基于默认地址格式的表单来实施此功能，也可以使用AEM提供的通讯簿组件。

此通讯簿组件允许您：

* 编辑帐簿中的地址
* 从帐簿中选择发运地址
* 从帐簿中选择帐单地址

您可以选择所需的默认地址。

通过单击&#x200B;**通讯簿**&#x200B;或导航到`/content/geometrixx-outdoors/en/user/account/address-book.html`，可从&#x200B;**My Account**&#x200B;页面访问通讯簿组件。

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

您可以单击&#x200B;**添加新地址……**&#x200B;在通讯簿中添加新地址。 它会打开一个您可以填写的表单，然后单击&#x200B;**添加地址**。

>[!NOTE]
您可以在通讯簿中输入多个地址。

购物车结账时，会使用通讯簿：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

地址会保留在`user_home/profile/addresses`下。
例如，对于Alison Parker，它位于/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以选择所需的默认地址，此信息将保留在购物者的配置文件中，而不是包含在地址中。 配置文件属性`address.default`使用选定值地址的路径进行设置。

### 特定于客户的定价{#customer-specific-pricing}

电子商务引擎使用上下文（本质上是购物者信息）来确定其持有的价格，然后将正确的信息提供回AEM。

## 购物车和订单{#shopping-cart-and-orders}

购物时，购物者将浏览产品页面并选择项目，以将它们放入其购物车中。 在他们继续结帐时，可以下订单。

### 匿名购物者{#anonymous-shoppers}

匿名客户可以：

* 查看产品
* 将产品添加到购物车
* 执行结帐以下单

>[!NOTE]
根据您的实例地址信息或客户注册的配置，可能需要在结帐前进行注册。

### 注册购物者{#registered-shoppers}

注册客户可以：

* 登录其帐户
* 查看产品
* 将产品添加到购物车
* 执行结帐以下单
* 查看和跟踪以前的订单

### 购物车内容概述{#shopping-cart-content-overview}

购物车提供：

* 所选项目概述
* 链接到选定项目的产品页面
* 能够：

   * 更新单个物料的数量/数量
   * 删除单个项目

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

购物车根据所使用的引擎进行保存：

* AEM通用程序将购物车存储在Cookie中。
* 某些电子商务引擎可以在会话中存储购物车。

无论哪种情况，物品都会在登录/注销过程中停留在购物车中（并且可以恢复）（但只能在同一台计算机/浏览器上）。 例如：

* 浏览`anonymous`并将产品添加到购物车
* 登录为`Allison Parker` — 她的购物车为空
* 将产品添加到购物车
* 注销 — 购物车将显示`anonymous`的产品

* 再次登录为`Allison Parker` — 她的产品已恢复

>[!NOTE]
匿名购物车只能在同一台计算机/浏览器上还原。

>[!NOTE]
不建议使用`admin`帐户测试恢复购物车内容，因为这可能与电子商务引擎的`admin`帐户（例如hybris）冲突。

>[!NOTE]
hybris可配置为在定义的时间段后删除挂起的购物车。

在结账前，价格变动会在发生时反映（在两个系统中）。

### 订单信息{#order-information}

根据您在电子商务引擎或AEM中保存的订单相关实施信息，此信息由AEM呈现。

存储了各种信息，其中可能包括：

* **订单 ID**

   订单的参考编号。

* **订购时间**

   下订单的日期。

* **状态**

   订单状态；例如，已发运。

* **货币**

   订单的货币。

* **内容项**

   已排序项目的列表。

* **小计**

   订购物料的总成本。

* **税费**

   订单上应缴的税金。

* **运费**

   运费。

* **总计**

   订单的总价值；订购物品、税收和购物。

* **帐单地址**

   应发送发票的地址。

* **付款标记**

   付款方式。

* **付款状态**

   付款的状态。

* **配送地址**

   货物应运到的地址。

* **配送方式**

   运输方式；例如，陆地、海洋或空气。

* **跟踪号**

   运输公司使用的任何跟踪编号。

* **跟踪链接**

   用于在发货时跟踪订单的链接。

>[!NOTE]
创建顺序向导中使用的字段取决于是否为位置定义了触屏优化基架。 在通用示例中，可在以下位置找到该示例：
`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM中保留订单后，“订单”控制台将显示每个订单的以下内容：

* 购物车中的项目数
* 订单的总值
* 下订单时
* 状态

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 订单跟踪{#order-tracking}

下订单后，购物者通常会返回：

* 检查订单状态
* 从订单中删除产品
* 将产品添加到订单

在收到订单交货后，购物者可能还希望查看一段时间内订单的历史记录。

订单履行和跟踪通常由电子商务引擎管理。 AEM可以使用“订单历史记录”组件显示信息，该组件显示所有相关详细信息，包括已应用的凭证和促销。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 签出 {#checkout}

使用标准AEM表单实施结帐。 这允许营销经理自定义营销内容的体验。

然后，电子商务会通过来自AEM表单的输入管理结帐流程。

### 支付安全性{#payment-security}

付款详细信息（包括信用卡信息）通常由电子商务引擎管理。 AEM将此类事务性信息转发到引擎（从那里转发到付款处理服务）。

支付卡行业(PCI)合规性可实现。

### 订单{#confirmation-of-order}的确认

订单在屏幕上得到确认，并可通过[订单跟踪](#order-tracking)进行跟踪。

## 搜索 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由于AEM将标准页面用于产品，因此您可以使用标准搜索组件创建搜索页面。

如果您需要更彻底的实施，则可以：

* 使用所需的功能扩展默认搜索组件。
* 在`CommerceService`中实施搜索方法，然后在搜索页面上使用电子商务搜索组件。

使用电子商务引擎时，电子商务搜索API可以在电子商务引擎解决方案中完全实施，以便您可以使用现成提供的电子商务搜索组件。 多面搜索允许您搜索JCR和/或引擎：
