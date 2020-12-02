---
title: '概念 '
seo-title: '概念 '
description: 与AEM的电子商务的一般概念。
seo-description: 与AEM的电子商务的一般概念。
uuid: 9a4cc154-d82b-43e0-a66c-3edf059e8b75
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 6d595c46-b04e-400b-a014-fbecd2010f5f
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '4532'
ht-degree: 1%

---


# 概念 {#concepts}

集成框架提供了以下机制和组件：

* 连接到eCommerce引擎
* 将数据拉进AEM
* 显示该数据并收集购物者的答复
* 返回事务详细信息
* 从两个系统中搜索数据

这意味着：

* 购物者无需等待即可注册和购物。
* 价格变化将立即由购物者看到。
* 可以根据需要添加产品。

>[!NOTE]
>
>电子商务框架可与以下对象一起使用：
>
>* [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
>* [SAPCommerce Cloud](/help/sites-administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)

>



>[!CAUTION]
>
>[电子商务集成框架](https://www.adobe.com/solutions/web-experience-management/commerce.html)是AEM Add-On。
>
>您的销售代表可以根据相应的引擎提供完整的详细信息。

>[!CAUTION]
>
>该框架为您自己的项目提供了基本要求。
>
>总是需要一定量的开发工作来调整框架，使其符合您的规范。

>[!CAUTION]
>
>标准AEM安装包括通用AEM(JCR)电子商务实施。
>
>它当前用于演示目的，或根据您的要求作为自定义实施的基本基础。

为了优化操作，AEM和电子商务引擎都集中在自己的专业领域。 信息在两者之间实时传输；例如：

* AEM can:

   * 请求：

      * 电子商务引擎中的产品信息。
   * 提供：

      * 用户视图获取产品信息、购物车和结帐。
      * 购物车和结帐信息到eCommerce引擎。
      * 搜索引擎优化(SEO)。
      * 社区功能。
      * 非结构化的营销交互。


* 电子商务引擎可以：

   * 提供：

      * 数据库中的产品信息。
      * 产品变体管理。
      * 订单管理。
      * ERP(Enterprise Resource Planning)。
      * 在产品信息中搜索。
   * 进程:

      * 购物车。
      * 结帐。
      * 订单履行。


>[!NOTE]
>
>具体详细信息取决于电子商务引擎和项目实施。

提供了许多现成的AEM组件以使用集成层。 目前包括：

* 产品信息
* 购物车
* 结帐
* 我的帐户

还提供各种搜索选项。

## 架构 {#architecture}

集成框架提供API、用于说明功能的一系列组件以及提供连接方法示例的几个扩展：

![chlimage_1-4](assets/chlimage_1-4.png)

该框架允许您访问以下功能：

![chlimage_1-5](assets/chlimage_1-5.png)

### 实现{#implementations}

AEM eCommerce is implemented with an eCommerce engine:

* 电子商务集成框架已构建为允许您将电子商务引擎轻松与AEM集成。 目的构建的电子商务引擎控制产品数据、购物车、结帐和订单履行，而AEM控制数据显示和营销活动。


>[!NOTE]
>
>标准AEM安装包括通用AEM(JCR)电子商务实施。
>
>它当前用于演示目的，或根据您的要求作为自定义实施的基本基础。
>
>AEM eCommerce implemented in AEM using generic development based on JCR is:
>
>* 用于说明API的使用的独立的AEM-native eCommerce示例。 这可用于控制产品数据、购物车和结帐以及现有的数据显示和营销活动。 在这种情况下，产品数据库存储在AEM的本机存储库中(Adobe[JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)的实现)。
>
>  
标准AEM安装包含[通用eCommerce实现](/help/sites-administering/generic.md)的基础知识。

### 商务提供程序{#commerce-providers}

将数据从商务引擎导入AEM eCommerce站点时，将使用商务提供程序为导入程序提供数据。 一个商务提供商可以支持多个导入器。

商务提供商是AEM代码，自定义为：

* 后端商务引擎的接口
* 在JCR存储库顶部实施商务系统

AEM目前提供两个商务提供商示例：

* one for geometrixx-hybris
* another for geometrixx-generic(JCR)

尽管通常，项目需要开发其自己的、自定义的、特定于其PIM和产品数据模式的商务提供商。

>[!NOTE]
>
>geometrixx导入器使用CSV文件；在模式实现的上方的注释中，提供了接受的客户（允许自定义属性）的描述。

[ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html)维护（通过[OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)）[ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html)和[CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html)接口的实现列表。 这些属性列在导入程序向导的&#x200B;**导入程序／商务提供程序**&#x200B;下拉字段中（使用`commerceProvider`属性作为名称）。

当特定的导入程序／商务提供程序可从下拉菜单中访问时，必须在以下任一位置定义它需要的任何补充数据（取决于导入程序类型）:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

相应`importers`文件夹下的文件夹必须与导入程序名称匹配；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

源导入文件的格式由导入程序定义。 或者，导入程序可以建立到商务引擎的连接（如WebDAV或http）。

## 角色 {#roles}

集成系统满足以下角色以维护数据：

* 产品信息管理(PIM)维护者：

   * 产品信息。
   * 分类、分类、批准。
   * 与数字资产管理交互。
   * 定价——通常来自ERP系统，并且不在商务系统中明确维护。

* 负责维护的作者／营销经理：

   * 适用于所有渠道的营销内容。
   * 促销活动.
   * 优惠券.
   * 营销活动.

* Surfer / Shopper who:

   * 视图您的产品信息。
   * 将商品放入购物车。
   * 检查他们的订单。
   * 预计订单履行。

尽管实际位置取决于您的实施；例如，generic或with an eCommerce engine:

![chlimage_1-6](assets/chlimage_1-6.png)

## 产品 {#products}

### 产品 数据与营销数据{#product-data-versus-marketing-data}

#### 结构性与营销类别{#structural-versus-marketing-categories}

如果可以区分以下两个类别，则这允许您用有意义的结构（`cq:Page`节点的树）明确URL，因此非常接近经典AEM内容管理:

* *结构性*类别

   定义&#x200B;*什么是产品*&#x200B;的类别树；例如：

   `/products/mens/shoes/sneakers`

* *营* 销类别

   所有其他类别a *产品可以属于*;例如：

   `/special-offers/christmas/shoes`)

### 产品数据 {#product-data}

要描述和管理您的产品，您需要保留一系列相关信息。

产品数据可以是：

* maintained directly in AEM(generic)。
* maintained in eCommerce engine and made available in AEM.

   根据数据类型，它根据需要为[synchronized](#catalog-maintenance-data-synchronization)，或直接访问；例如，在每个页面请求中从ecommerce引擎检索产品价格等高波动性和关键数据，以确保它们始终处于最新状态。

无论哪种情况，在将产品数据输入／导入AEM后，都可以从&#x200B;**产品**&#x200B;控制台中查看。 此处是产品的卡和列表视图，显示以下信息：

* 图像
* SKU代码
* 上次修改时间

![chlimage_1-7](assets/chlimage_1-7.png)

### 产品的系列品种 {#product-variants}

对于相应的产品，还可以保留有关变体的信息。 例如，对于可用颜色不同的服装，它们以变体形式保留：

![ecommerceproductvariants](assets/ecommerceproductvariants.png)

### 产品属性{#product-attributes}

每个产品的各个属性可能取决于所使用的电子商务引擎和AEM实施。 在查看产品页面和／或编辑产品信息时，这些选项（视情况而定）可用，可包括：

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

可以为单个产品保留一系列资产。 通常包括图像和视频。

## 目录 {#catalogs}

A catalog groups product data together for both ease of management and representation to the shopper. 通常，目录根据语言、地理区域、品牌、季节、爱好、体育等属性进行结构化。

### 目录结构{#catalog-structure}

#### 多语言目录{#catalogs-in-multiple-languages}

AEM支持多种语言的产品内容。 在请求数据时，集成框架从当前树中检索语言（例如，`/content/geometrixx-outdoors/en_US`下的页面的`en_US`）。

对于多语言商店，可以单独导入每个语言树的目录（或通过[MSM](/help/sites-administering/msm.md)复制目录）。

#### 多品牌目录{#catalogs-for-multiple-brands}

与语言一样，大型跨国公司需要满足多个品牌的需求。

#### Catalogs by Tags {#catalogs-by-tags}

标记还可以用于将产品组合到目录中。 这些目录可用于更动态的目录，如季节性优惠。

### 目录设置（初始导入）{#catalog-setup-initial-import}

根据您的实施，您可以将基本目录所需的产品数据从以下位置导入AEM::

* CSV文件（用于通用实现）
* eCommerce engine

### 目录维护（数据同步）{#catalog-maintenance-data-synchronization}

产品数据的进一步变化将不可避免：

* 对于通用实现，可以使用[产品编辑器](/help/sites-administering/generic.md#editing-product-information)管理这些组件
* 使用[eCommerce引擎时，必须同步更改](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 与eCommerce Engine（正在进行）{#data-synchronization-with-an-ecommerce-engine-ongoing}进行数据同步

初次导入后，对产品数据的更改是不可避免的。

使用电子商务引擎时，产品数据会保留在此处，并且需要在AEM中可用。 进行更新时，需要同步此产品数据。

这取决于数据类型：

* 将[周期同步与更改的数据供给一起使用。](/help/sites-developing/sap-commerce-cloud.md#product-synchronization-and-publishing)

   除此之外，您还可以为快速更新选择特定更新。

* 从商务引擎中检索每个页面请求的高度易变性数据（如价格信息），以确保其始终处于最新状态。

### 目录——性能和缩放{#catalogs-performance-and-scaling}

从电子商务引擎(PIM)导入包含大量产品（通常超过100,000个）的大型目录可能会因节点数过多而影响系统。 如果产品具有关联的资产（如产品图像），则还可以减慢创作实例的速度。 这是由于这些资产的后处理需要占用大量CPU和内存。

您可以选择各种策略来解决这些问题：

* [Bucketing](#bucketing) -以满足大量节点
* [将资产后处理卸载到专用实例](#offload-asset-post-processing-to-a-dedicated-instance)
* [仅导入产品数据](#only-import-product-data)
* [导入限制和批量保存](#import-throttling-and-batch-saves)
* [性能测试](#performance-testing)
* [性能——杂项](#performance-miscellaneous)

#### Bucketing {#bucketing}

如果JCR节点有许多直接子节点（如1000个及以上），则需要存储段（幻像文件夹）以确保性能不受影响。 导入时根据算法生成这些值。

这些存储段采用引入到目录结构的幻像文件夹的形式，但可以进行配置，使其在公共URL中不明显。

#### 将资产后处理卸载到专用实例{#offload-asset-post-processing-to-a-dedicated-instance}

此方案涉及设置两个作者实例：

1. 主控作者实例

   从PIM导入产品数据，在其上禁用资产路径的后处理。

1. 专用DAM作者实例

   从PIM导入和后处理产品资产，然后将这些资产复制回主控的作者实例以供使用。

![架构图](assets/chlimage_1-8.png)

#### 仅导入产品数据{#only-import-product-data}

对于产品不包含要导入的资产（图像）的情况，您可以导入产品数据，而不会受资产后期处理的影响。

![架构图](assets/chlimage_1-9.png)

<!--delete
#### Import Throttling and Batch Saves {#import-throttling-and-batch-saves}

[Import throttling](/help/sites-deploying/scaling.md#import-throttling) and [batch saves](/help/sites-deploying/scaling.md#batch-saves) are two general [scaling](/help/sites-deploying/scaling.md) mechanisms that can help when importing large volumes of data.-->

#### 性能测试{#performance-testing}

必须考虑AEM eCommerce实施的性能测试：

* 作者环境:

   背景（如导入）活动可以与普通用户活动（如页面编辑）同时发生，即使前端性能（通常）被赋予更高的优先级，在线作者看到的不良性能也会导致阻碍实时决策的沮丧。

* 出版环境:

   复制是确保快速、可靠地发布内容的关键过程。 这可能受作者如何对要发布的内容进行分组的影响。

* 前端：

   前端和缓存失效的混合可能导致性能意外。 测试有助于避免这些问题。

请注意，此性能测试需要您目标的知识和分析:

* 内容卷

   * 资产
   * 本地化的I18ned产品和SKU

* 用户活动:

   * 批量版
   * 批量发布
   * 强烈搜索请求

* 后台进程

   * 导入
   * 同步更新（例如定价）

* 维护要求（备份、Tar PM优化、数据存储垃圾收集等）

#### 性能——其他{#performance-miscellaneous}

对于所有实施，可以记住以下几点：

* 由于产品、库存单位和类别可以很多，请尝试使用最少的节点数来模拟内容。

   您拥有的节点越多，您的内容就越灵活（例如parsys）。 但是，一切都是权衡，在处理（例如）30K产品时，您是否需要个别的灵活性（默认情况）?

* 尽可能避免重复(请参阅本地化)，或者当您这样做时，请考虑您的重复将导致的节点数。
* 尝试尽可能多地标记您的内容，以准备查询优化。

   例如：

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   每个内容级别(即国家／地区、语言、类别、品牌、产品)应有一个标签。 搜索

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   和

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   比寻找要快得多

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技术堆栈中，规划非常分工的内容访问模型和服务。 这是一般的最佳实践，但更重要的是，在优化阶段，您可以为读取频繁的数据添加应用程序缓存（并且您不想用它填充捆绑缓存）。

   例如，属性管理经常是缓存的一个好候选项，因为它涉及通过产品导入更新的数据。
* 考虑使用[代理页](/help/sites-administering/concepts.md#proxy-pages)。

### 目录部分页{#catalog-section-pages}

Catalog sections provide you with, for example:

* 介绍（图像和／或文本）类别;这也可用于横幅和Teaser以提升特殊优惠
* 链接到该类别中的单个产品
* 链接到其他类别

![ecommerce_categoryrunning](assets/ecommerce_categoryrunning.png)

### 产品页面 {#product-pages}

产品页面提供有关各个产品的全面信息。 还反映了动态更新；例如，在eCommerce引擎上注册的价格更改。

产品页是使用&#x200B;**Product**&#x200B;组件的AEM页；例如，在&#x200B;**Commerce Product**&#x200B;模板中：

![ecommerce_nairobrunnergreen](assets/ecommerce_nairobirunnersgreen.png)

产品组件提供：

* 一般产品信息；包括文本和图像。
* 定价；这通常在每次显示／刷新页面时从eCommerce引擎中检索。
* 产品变体信息；例如，颜色和大小。

此信息允许购物者在将项目添加到其购物篮时选择以下内容：

* 颜色和大小变体
* 数量

#### 产品登陆页{#product-landing-pages}

这些是AEM页面，主要提供静态信息；例如，包含指向基础产品页面的链接的简介和概述。

### 产品组件 {#product-component}

可以将&#x200B;**Product**&#x200B;组件添加到具有父页面的任何页面，该页面提供所需的元数据（即到`cartPage`和`cartObject`的路径）。 在演示站点中，Geometrixx Outdoors由`UserInfo.jsp`提供。

**Product**&#x200B;组件也可以根据您的个人要求进行自定义。

### 代理页{#proxy-pages}

代理页面用于简化存储库的结构并优化大型目录的存储。

创建目录将使每个产品使用十个节点，因为它为每个产品提供可在AEM中更新和自定义的单独组件。 如果您的目录包含数百甚至数千个产品，则此大量节点可能会成为问题。 要避免任何问题，您可以使用代理页面创建目录。

代理页使用双节点结构（`cq:Page`和`jcr:content`），它不包含任何实际的产品内容。 在请求时，通过引用产品数据和模板页面生成内容。

然而，这是一种取舍。 您将无法在AEM中自定义您的产品信息，将使用标准模板（为您的站点定义）。

>[!NOTE]
>
>如果导入没有代理页的大型目录，则不会遇到任何问题。
>
>您可以随时从一种方法转换为另一种方法。 您还可以转换目录的子部分。

## Promotions and Vouchers {#promotions-and-vouchers}

### 优惠券 {#vouchers}

Vouchers are a tried and tested method of offering discounts to either attract shoppers into making a purchase and/or rewarding customer&#39;s loyalty.

* Vouchers supply:

   * A voucher code(to be typed into the cart by the shopper)。
   * A voucher label(to be displayed after the shopper has entered it into the cart)。
   * A promotion path(which defines the action the voucher applies)。

* 外部商务引擎还可以提供凭证。

在AEM中：

* A voucher is a page-based component that is created / edited with the Websites console.
* **凭证**&#x200B;组件提供：

   * 凭证管理的呈现器；这显示购物车中当前的所有凭证。
   * 用于管理（添加／删除）凭证的编辑对话框（表单）。
   * 添加／删除凭证至购物车／从购物车所需的操作。

* 凭证没有其自己的开／关日期／时间，但使用其父活动的凭证。

>[!NOTE]
>
>AEM使用术语&#x200B;**Voucher**，这与术语&#x200B;**Coupon**&#x200B;同义。

### 促销活动 {#promotions}

Promotions，连同vouchers, allow you to realize scenarios such as:

* 公司为员工提供自定义价格，这是一个手工制作的用户列表。
* 长期客户可享受所有订单的折扣。
* 在明确定义的时间段内提供的销售价格。
* 客户在其上一订单超过特定金额时收到凭证。
* 购买&#x200B;*product-X*&#x200B;的客户在购买&#x200B;*product-Y*（对产品）时可享受折扣。

促销通常不由产品信息经理维护，而是由营销经理维护：

* 促销是使用网站控制台创建／编辑的基于页面的组件。 &quot;
* 促销供应：

   * 优先级
   * 升级处理程序路径

* 您可以将促销活动连接到活动以定义其开／关日期／时间。
* 您可以将促销活动与体验关联，以定义其区段。
* 未连接到体验的促销将不会自行触发，但仍可由Voucher触发。
* 升级组件包含：

   * promotion administration的renderers和dialogs
   * 用于渲染和编辑特定于升级处理程序的配置参数的子组件

在AEM中，促销还集成到[活动管理](/help/sites-authoring/personalization.md)中：

* a [活动](/help/sites-authoring/personalization.md)指定开／关时间
* [活动](/help/sites-authoring/personalization.md) ** 中的体验用于根据受众段对资产（Teaserpages、促销等）进行分组，这些资产对应于

促销活动可以在体验中进行，也可以直接在活动中进行：

* 如果促销在体验中持有，则可自动将其应用于受众区段。

   例如，在geometrixx-outdoors示例站点中，升级：

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   is in an experience, and so fires automatically when the segment(`ordervalueover100`)resolves.

* 如果促销未在体验中显示(仅在活动中)，则无法自动将其应用于受众。 但是，如果Shopper enters a voucher into their cart and that voucher references the promotion，则仍可触发它。

   例如，促销：

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   is outside and so never fires automatically(ie:基于分段)。 但是，它被引用了，该凭证可在文章活动内的几个体验中找到。 将这些凭单代码输入购物车将导致升级触发。

>[!NOTE]
>
>[hybris ](https://www.hybris.com/modules/promotion) promotion [和hybris voucherscover ](https://www.hybris.com/en/modules/voucher) everythings that implements the shopping cart and is related to pricing.Promotion specific marketing content(such as banners, etc)is not part of the hybris promotion.

## 个性化 {#personalization}

### 客户注册和帐户{#customer-registration-and-accounts}

当购物者注册时，帐户详细信息需要在AEM和eCommerce引擎之间同步。 敏感数据是独立保存的，但用户档案是共享的：

![chlimage_1-10](assets/chlimage_1-10.png)

具体机制取决于情景：

1. 这两个系统中都存在用户帐户：

   1. 无需执行任何操作。

1. 用户帐户仅在AEM中存在：

   1. 用户将在电子商务引擎中创建，其帐户ID和随机密码将存储在AEM中。
   1. 随机密码是必需的，因为AEM会尝试在第一次调用时登录到电子商务引擎（例如，当请求产品页面且电子商务引擎引用价格时）。 由于这在AEM登录后发生，因此密码不可用。

1. 用户帐户仅存在于电子商务引擎中：

   1. 帐户将在AEM中创建，并使用相同的帐户ID和密码。

使用电子商务引擎时，AEM仅存储帐户ID和密码（可选为用户组）。 所有其他信息都存储在电子商务引擎中。

>[!NOTE]
>
>使用电子商务引擎时，您需要确保为登录AEM实例的用户创建的帐户被复制(例如，通过工作流)到与该引擎通信的任何其他AEM实例。
>
>否则，这些其他AEM实例还将尝试为引擎中的相同用户创建帐户。 这些操作将失败，引擎中出现`DuplicateUidException`。

### 客户注册{#customer-sign-up}

购物者必须注册才能访问购物车。 这需要注册（创建帐户），以便创建客户特定的帐户。

![chlimage_1-11](assets/chlimage_1-11.png)

>[!NOTE]
>
>还支持匿名购物车和结帐。

### 客户登录{#customer-sign-in}

注册后，购物者可以使用其帐户登录，以便跟踪其活动并完成其订单。

![chlimage_1-12](assets/chlimage_1-12.png)

### 单一登录{#single-sign-on}

提供单点登录(SSO)，这样作者在AEM和电子商务系统中都是已知的，无需登录两次。

### myAccount {#myaccount}

来自电子商务引擎的事务数据与有关购物者的个人信息相结合。 AEM将部分数据用作用户档案数据。 AEM中表单的操作会将信息写回电子商务引擎。

有一个页面，允许您轻松管理帐户信息。 您可以通过单击geometrixx页面顶部的&#x200B;**我的帐户**&#x200B;或导航到`/content/geometrixx-outdoors/en/user/account.html`来访问它。

![chlimage_1-13](assets/chlimage_1-13.png)

### 通讯簿 {#address-book}

您的站点需要存储一系列地址；包括投放、帐单和替代地址。 这可以基于默认地址格式使用表单实现，也可以使用AEM提供的通讯簿组件。

此通讯簿组件允许您：

* 编辑书籍中的地址
* 从帐簿中选择地址作为发运地址
* 从帐簿中选择地址作为帐单地址

您可以选择默认的地址。

可通过单击&#x200B;**通讯簿**&#x200B;或导航到`/content/geometrixx-outdoors/en/user/account/address-book.html`，从&#x200B;**我的帐户**&#x200B;页面访问通讯簿组件。

![chlimage_1-14](assets/chlimage_1-14.png)

您可以单击&#x200B;**添加新地址……**&#x200B;在通讯簿中添加新地址。 它打开一个可填写的表单，然后单击&#x200B;**添加地址**。

>[!NOTE]
>
>您可以在通讯簿中输入多个地址。

The Address Book is used when you checkout your cart:

![chlimage_1-15](assets/chlimage_1-15.png)

地址会保留在`user_home/profile/addresses`下。
例如，对于Alison Parker，它位于/home/users/geometrixx/aparker@geometrixx.info/用户档案/addresses下

您可以选择您希望使用的默认地址，此信息将保留在购物者的用户档案中，而不是包含地址。 用户档案属性`address.default`设置为选定地址的值路径。

### 客户特定定价{#customer-specific-pricing}

电子商务引擎使用上下文（实质上是购物者信息）来确定其所持的价格，然后将正确的信息提供回AEM。

## 购物车和订单{#shopping-cart-and-orders}

当购物时，购物者将浏览产品页面并选择项目以将它们放入其购物车中。 当他们继续结帐时，可以下订单。

### 匿名购物者{#anonymous-shoppers}

匿名客户可以：

* 视图产品
* 将产品添加到购物车
* 执行结帐以下单

>[!NOTE]
>
>在结帐之前，可能需要执行实例地址信息或客户注册的配置操作。

### 注册购物者{#registered-shoppers}

注册客户可以：

* 登录其帐户
* 视图产品
* 将产品添加到购物车
* 执行结帐以下单
* 视图和跟踪以前的订单

### 购物车内容概述{#shopping-cart-content-overview}

购物车提供：

* 所选项目概述
* 指向所选项目的产品页面的链接
* 能够：

   * 更新单个物料的数量／数量
   * 删除单个项目

![ecommerce_shoppingcart](assets/ecommerce_shoppingcart.png)

购物车根据所使用的引擎进行保存：

* AEM generic stores the cart in a cookie.
* 某些电子商务引擎可以在会话中存储购物车。

无论哪种情况，项目都会停留在购物车中（并且可以恢复），而不是登录／注销（但只是在同一台机器／浏览器上）。 例如：

* 浏览为`anonymous`并将产品添加到购物车
* 以`Allison Parker`身份登录——她的购物车为空
* 将产品添加到她的购物车
* 注销——购物车将显示`anonymous`的产品

* 以`Allison Parker`身份再次登录——恢复其产品

>[!NOTE]
>
>匿名购物车只能在同一台机器／浏览器上还原。

>[!NOTE]
>
>不建议使用`admin`帐户测试恢复购物车内容，因为这可能与eCommerce engine（例如hybris）的`admin`帐户发生冲突。

>[!NOTE]
>
>hybris can be configured to remove pending carts after a defined period of time.

在结帐前，价格更改会在发生时反映（在两个系统中）。

### 订单信息{#order-information}

根据您的订单实施信息在电子商务引擎或AEM中保留，此信息由AEM提供。

存储了各种信息，其中可以包括：

* **订单 ID**

   订单的参考编号。

* **订购时间**

   下订单的日期。

* **状态**

   订单的状态；例如，“已发运”。

* **货币**

   订单的货币。

* **内容项**

   订购的列表项。

* **小计**

   订购物料的总成本。

* **税费**

   订单上应付的税金额。

* **运费**

   运费。

* **总计**

   订单的总价值；订购的物品、税和垃圾。

* **帐单地址**

   发票应发送的地址。

* **付款标记**

   付款方式。

* **付款状态**

   付款的状态。

* **配送地址**

   货物应装运到的地址。

* **配送方式**

   运输方式；例如，陆地、海洋或空气。

* **跟踪号**

   发运公司使用的任何跟踪编号。

* **跟踪链接**

   用于跟踪发运订单的链接。

>[!NOTE]
>
>创建顺序向导中使用的字段取决于是否存在为位置定义的触屏优化基架。 在通用示例中，可以在以下位置找到该示例：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM中保留订单时，订单控制台会为每个订单显示以下内容：

* 购物车中的项目数
* 订单的总值
* 下订单的时间
* 状态

![chlimage_1-16](assets/chlimage_1-16.png)

### 订单跟踪{#order-tracking}

下订单后，购物者通常返回：

* 检查订单状态
* 从订单中删除产品
* 将产品添加到订单

在收到订单投放后，购物者可能还希望视图一段时间内完成的订单的历史记录。

订单履行和跟踪通常由电子商务引擎管理。 信息可由AEM使用订单历史记录组件显示，该组件显示所有相关详细信息，包括已应用的凭证和促销。 例如：

![chlimage_1-17](assets/chlimage_1-17.png)

## 签出 {#checkout}

结帐是使用标准AEM表单实现的。 这使营销经理能够自定义营销内容的体验。

然后，电子商务使用AEM表单的输入管理结帐过程。

### 付款安全性{#payment-security}

付款详细信息（包括信用卡信息）通常由电子商务引擎管理。 AEM将此类交易信息转发给引擎（从此处转发给付款处理服务）。

可实现支付卡行业(PCI)合规性。

### 订单{#confirmation-of-order}的确认

订单在屏幕上确认，可以使用[订单跟踪](#order-tracking)进行跟踪。

## 搜索 {#search-features}

![chlimage_1-18](assets/chlimage_1-18.png)

由于AEM将标准页面用于产品，因此您可以使用标准搜索组件创建搜索页面。

如果您需要更彻底的实施，您可以：

* 使用您需要的功能扩展默认搜索组件。
* 在`CommerceService`中实施搜索方法，然后在搜索页面上使用eCommerce搜索组件。

使用电子商务引擎时，电子商务搜索API可以在电子商务引擎解决方案中完全实现，因此您可以使用现成提供的电子商务搜索组件。 多面搜索允许您搜索JCR和／或引擎：

