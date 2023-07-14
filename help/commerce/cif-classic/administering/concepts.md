---
title: 概念
description: 使用Adobe Experience Manager实现电子商务的一般概念。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 681d1e6bd885b801b930e580d95645f160f17cea
workflow-type: tm+mt
source-wordcount: '4483'
ht-degree: 1%

---

# 概念{#concepts}

集成框架为以下项目提供机制和组件：

* 连接到电子商务引擎
* 将数据提取到Adobe Experience Manager (AEM)
* 显示数据并收集购物者的响应
* 返回交易详细信息
* 搜索来自两个系统的数据

这意味着：

* 购物者无需等待即可注册和购物。
* 消费者毫不拖延地看到价格变化。
* 可以根据需要添加产品。

>[!NOTE]
>
>电子商务框架可以与：
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [SAPCOMMERCE CLOUD](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [SalesforceCommerce Cloud](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>此 [电子商务集成框架](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) 是一个AEM加载项。
>
>您的销售代表可以根据相应的引擎提供完整的详细信息。

>[!CAUTION]
>
>该框架为您自己的项目提供了基本要求。
>
>始终需要执行一定数量的开发工作来使框架适应您的规范。

>[!CAUTION]
>
>标准AEM安装包括通用AEM (JCR)电子商务实施。
>
>这用于演示目的，或作为自定义实施的基本基础（根据您的要求）。

为了优化操作，AEM和电子商务引擎都专注于各自的专业领域。 信息在两者之间实时传输；例如：

* AEM可以：

   * 请求：

      * 电子商务引擎中的产品信息。

   * 提供：

      * 用户查看产品信息、购物车和结帐。
      * 将购物车和结帐信息发送到电子商务引擎。
      * 搜索引擎优化(SEO)。
      * 社区功能。
      * 非结构化营销互动。

* 电子商务引擎可以：

   * 提供：

      * 数据库中的产品信息。
      * 产品变型管理。
      * Order Management。
      * ERP（企业资源规划）。
      * 搜索产品信息。

   * 进程:

      * 购物车。
      * 结帐。
      * 订单履行。

>[!NOTE]
>
>确切的详细信息取决于电子商务引擎和项目实施。

提供了多个现成的AEM组件以使用集成层。 目前，这些方法包括：

* 产品信息
* 购物车
* 结帐
* 我的帐户

还可以使用各种搜索选项。

## 架构 {#architecture}

集成框架提供了API、一系列用于说明功能的组件，以及多个用于提供连接方法示例的扩展：

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

通过框架，您可以访问以下功能：

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### 实施 {#implementations}

AEM eCommerce通过电子商务引擎实现：

* 电子商务集成框架已经构建，可让您轻松地将电子商务引擎与AEM集成。 专门构建的电子商务引擎控制产品数据、购物车、结账和订单履行，而AEM控制数据展示和营销活动。


>[!NOTE]
>
>标准AEM安装包括通用AEM (JCR)电子商务实施。
>
>这用于演示目的，或作为自定义实施的基本基础（根据您的要求）。
>
>使用基于JCR的通用开发在AEM中实现的AEM电子商务是：
>
>* 一个独立的AEM原生电子商务示例，用于说明API的使用。 这可用于通过现有数据展示和营销活动控制产品数据、购物车和结账。 在这种情况下，产品数据库存储在AEM本地的存储库中(Adobe的 [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html))。
>
>  标准AEM安装包含 [通用电子商务实施](/help/commerce/cif-classic/administering/generic.md).

### 商业提供程序 {#commerce-providers}

将数据从商业引擎导入到AEM电子商务网站时，使用商业提供程序向导入程序提供数据。 一个商务提供商可以支持多个导入程序。

Commerce提供程序是自定义到的AEM代码：

* 后端商务引擎的接口
* 在JCR存储库上实施商业系统

AEM当前提供两个示例商业提供程序：

* 一个用于geometrixx-hybris
* geometrixx-generic (JCR)的另一个

尽管通常项目需要开发他们自己的、特定于其PIM和产品数据架构的自定义商业提供程序。

>[!NOTE]
>
>Geometrixx导入程序使用CSV文件；其实现上方的注释中对接受的架构（允许自定义属性）进行了描述。

此 [产品服务经理](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) 维护(通过 [osgi](/help/sites-deploying/configuring.md#osgi-configuration-settings))的实施列表 [产品导入程序](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) 和 [CatalogBlueprintImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) 界面。 这些项目列于 **导入程序/商务提供程序** 导入器向导的下拉字段(使用 `commerceProvider` 属性作为名称)。

当下拉列表中提供特定的导入程序/商务提供程序时，必须在以下任一位置定义所需的任何补充数据（取决于导入程序类型）：

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

文件夹位于相应的 `importers` 文件夹必须与导入程序名称匹配；例如：

* `.../importproductswizard/importers/geometrixx/.content.xml`

源导入文件的格式由导入器定义。 或者，导入程序可能会建立与商业引擎的连接（例如WebDAV或http）。

## 角色 {#roles}

集成系统满足以下角色对数据的维护需求：

* 维护以下功能的产品信息管理(PIM)用户：

   * 产品信息。
   * 分类，分类，批准。
   * 与数字资产管理交互。
   * 定价 — 通常来自ERP系统，在商业系统中没有明确维护。

* 负责维护以下内容的作者/营销经理：

   * 所有渠道的营销内容。
   * 促销活动.
   * 优惠券.
   * 营销活动.

* 冲浪者/购物者：

   * 查看您的产品信息。
   * 将商品放入购物车。
   * 查出他们的订单。
   * 期望订单履行。

虽然实际位置可能取决于您的实施；例如，通用或使用电子商务引擎：

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## 产品 {#products}

### 产品数据与营销数据 {#product-data-versus-marketing-data}

#### 结构类别与营销类别 {#structural-versus-marketing-categories}

如果可以区分以下两个类别，那么通过这可以让您使用有意义的结构(树 `cq:Page` 因此，非常接近经典的AEM内容管理)：

* *结构*类别

  类别树定义 *什么是产品*；例如：

  `/products/mens/shoes/sneakers`

* *营销* 类别

  所有其他类别 *产品可以属于*；例如：

  `/special-offers/christmas/shoes`)

### 产品数据 {#product-data}

为了描绘和管理您的产品，您需要保存有关它们的一系列信息。

产品数据可以是：

* 直接在AEM中维护（通用）。
* 在电子商务引擎中维护，并在AEM中提供。

  根据数据类型而定 [已同步](#catalog-maintenance-data-synchronization) 在必要时，或直接访问；例如，从每个页面请求的电子商务引擎中检索高度易变和关键的数据（如产品价格），以确保它们始终保持最新。

无论属于哪种情况，当产品数据已输入/导入AEM时，都可以从 **产品** 控制台。 在此处，产品的信息卡和列表视图显示如下信息：

* 图像
* SKU代码
* 上次修改时间

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### 产品的系列品种 {#product-variants}

对于相应的产品，还可以保存有关变体的信息。 例如，对于服装项目，可用的不同颜色会作为变体保留：

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### 产品属性 {#product-attributes}

每个产品拥有的各个属性可能取决于所使用的电子商务引擎和您的AEM实施。 在查看产品页面和/或编辑产品信息时，这些选项可用（如果适用），可以包括：

* **图像**

  产品的图像。

* **标题**

  产品名称。

* **描述**

  产品的文本描述。

* **标记**

  用于对相关产品进行分组的标记。

* **默认资源类别**

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

  产品功能摘要。

* **功能**

  更全面的产品功能详细信息。

### 产品资产 {#product-assets}

可以为单个产品持有精选资产。 通常包括图像和视频。

## 目录 {#catalogs}

目录将产品数据分组在一起，以便于管理，并向购物者呈现。 通常，目录是根据语言、地理区域、品牌、季节、嗜好、体育等属性来构建的。

### 目录结构 {#catalog-structure}

#### 多种语言的目录 {#catalogs-in-multiple-languages}

AEM支持多种语言的产品内容。 在请求数据时，集成框架会从当前树中检索语言(例如， `en_US` 对于下面的页面 `/content/geometrixx-outdoors/en_US`)。

对于多语言存储，您可以单独导入每个语言树的目录（或复制该目录时使用） [MSM](/help/sites-administering/msm.md))。

#### 多个品牌的目录 {#catalogs-for-multiple-brands}

与语言一样，大型跨国企业必须满足多个品牌的需求。

#### 按标记列出的目录 {#catalogs-by-tags}

标记也可用于将产品分组到一个目录中。 它们可用于更具动态的目录，例如季节性优惠。

### 目录设置（初始导入） {#catalog-setup-initial-import}

根据您的实施，您可以从以下位置将基础目录所需的产品数据导入AEM：

* CSV文件（用于一般实施）
* 电子商务引擎

### 目录维护（数据同步） {#catalog-maintenance-data-synchronization}

产品数据的进一步更改是不可避免的：

* 对于通用实施，可以使用管理这些实施 [产品编辑器](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* 使用 [电子商务引擎更改必须同步](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### 与电子商务引擎的数据同步（持续） {#data-synchronization-with-an-ecommerce-engine-ongoing}

初次导入后，产品数据的更改在所难免。

使用电子商务引擎时，产品数据会保留在那里，并且必须在AEM中可用。 在进行更新时，必须同步此产品数据。

这可能取决于数据类型：

* A [定期同步与更改的数据馈送一起使用](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  除此之外，您还可以为快速更新选择特定更新。

* 从商业引擎为每个页面请求检索高度易失的数据（例如价格信息），以确保该数据始终保持最新。

### 目录 — 性能和扩展 {#catalogs-performance-and-scaling}

从电子商务引擎(PIM)导入具有大量产品（超过100,000）的大型目录可能会由于节点数量众多而影响系统。 如果产品具有关联的资产（例如，产品图像），它也会减慢创作实例的速度。 这是因为这些资产的后处理需要占用大量CPU和内存。

您可以选择多种策略来解决这些问题：

* [分段](#bucketing)  — 用于满足大量节点的需求
* [将资产后处理卸载到专用实例](#offload-asset-post-processing-to-a-dedicated-instance)
* [仅导入产品数据](#only-import-product-data)
* [导入限制和批量保存](#import-throttling-and-batch-saves)
* [性能测试](#performance-testing)
* [绩效 — 其他](#performance-miscellaneous)

#### 分段 {#bucketing}

如果JCR节点具有许多直接子节点（例如，1000个及更多），则需要存储段（虚拟文件夹）以确保性能不受影响。 这些内容在导入时根据算法生成。

这些存储段采用引入目录结构的幻像文件夹形式，但可以对其进行配置，以便在公共URL中不显示这些文件夹。

#### 将资产后处理卸载到专用实例 {#offload-asset-post-processing-to-a-dedicated-instance}

此方案涉及设置两个创作实例：

1. 主控创作实例

   从禁用资产路径后处理的PIM导入产品数据。

1. 专用DAM创作实例

   从PIM导入产品资产并对其进行后处理，然后将它们复制回主控的创作实例以供使用。

![架构图](/help/sites-administering/assets/chlimage_1-8.png)

#### 仅导入产品数据 {#only-import-product-data}

如果产品不包含要导入的资产（图像），则可以导入产品数据，而不受资产后处理的影响。

![架构图](/help/sites-administering/assets/chlimage_1-9.png)

#### 性能测试 {#performance-testing}

必须在AEM电子商务实施中考虑性能测试：

* 创作环境：

  后台（例如，导入）活动可与正常用户活动（例如，页面编辑）同时发生，并且即使（通常）前端性能被赋予较高的优先级，在线作者看到的性能不佳也会导致无法阻止上线决策的失败。

* 发布环境：

  复制是确保快速、可靠地发布内容的关键过程。 这可能受作者如何对要发布的内容进行分组的影响。

* 前端：

  前端和缓存失效的结合可能会导致性能意外情况。 测试有助于避免出现这种情况。

请注意，此性能测试需要目标知识和分析：

* 内容卷

   * 资源
   * 本地化的I18ned产品和SKU

* 用户活动：

   * 批量编辑
   * 批量发布
   * 大量搜索请求

* 后台进程

   * 导入
   * 同步更新（例如，定价）

* 维护要求（备份、Tar PM优化、数据存储垃圾收集等）

#### 绩效 — 其他 {#performance-miscellaneous}

对于所有实施，请牢记以下几点：

* 作为产品，库存单位和类别可以很多，请尝试使用尽可能少的节点数来建模内容。

  拥有的节点越多，内容就越灵活（例如，parsys）。 但是，所有东西都是权衡取舍，在操作（例如）30K产品时，是否需要个人的灵活性（默认情况下）？

* 尽量避免重复（请参阅本地化），或者在这样做时，考虑重复导致多少个节点。
* 尽可能多地标记您的内容以准备查询优化。

  例如：

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  每个内容级别应具有一个标记（即国家/地区、语言、类别、品牌、产品）。 正在搜索

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  和

  `@category='shoe' and @brand='reebok' and @product='pump']`

  会比寻找

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* 在您的技术栈栈中，规划工厂化的内容访问模型和服务。 这是一个常规的最佳实践，但在这里更加重要，因为在优化阶段，您可以为经常读取（并且您不希望使用填充捆绑包缓存）的数据添加应用程序缓存。

  例如，属性管理通常是缓存的良好候选项，因为它涉及通过产品导入更新的数据。
* 考虑使用 [代理页面](#proxy-pages).

### 目录部分页面 {#catalog-section-pages}

例如，目录部分为您提供：

* 类别的简介（图像和/或文本）；这还可用于横幅和Teaser以促销特殊优惠
* 指向该类别中各个产品的链接
* 指向其他类别的链接

![e-commerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### 产品页面 {#product-pages}

产品页面提供有关各个产品的全面信息。 来自的动态更新也会反映出来；例如，在电子商务引擎上注册的价格变化。

AEM产品页面是指使用 **产品** 组件；例如，在 **商业产品** 模板：

![e-commerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

产品组件提供：

* 一般产品信息；包括文本和图像。
* 定价；每次显示/刷新页面时，都会从电子商务引擎中检索此价格。
* 产品变型信息；例如，颜色和大小。

此信息允许购物者在将商品添加到购物篮时选择以下选项：

* 颜色和大小变量
* 数量

#### 产品登陆页面 {#product-landing-pages}

这些主要是提供静态信息的AEM页面；例如，包含基础产品页面链接的简介和概述。

### 产品组件 {#product-component}

此 **产品** 组件可以添加到任何页面，这些页面具有提供所需元数据(即 `cartPage` 和 `cartObject`)。 在演示站点Geometrixx Outdoors中，这由以下提供 `UserInfo.jsp`.

此 **产品** 组件也可以根据您的具体要求进行自定义。

### 代理页面 {#proxy-pages}

代理页面用于简化存储库的结构并优化大型目录的存储。

创建目录时，每个产品将使用10个节点，因为它会为您可在AEM中更新和自定义的每个产品提供各个组件。 如果您的目录包含数百甚至数千个产品，那么如此大量的节点可能会成为一个问题。 要避免出现任何问题，您可以使用代理页面创建目录。

代理页面使用双节点结构( `cq:Page` 和 `jcr:content`)，不包含任何实际产品内容。 在请求时，通过引用产品数据和模板页面生成内容。

然而，这其中有一个取舍。 您将无法在AEM中自定义产品信息，将使用标准模板（为您的站点定义）。

>[!NOTE]
>
>如果导入的大目录没有代理页面，则不会遇到任何问题。
>
>您可以随时从一种方法转换为另一种方法。 您还可以转换目录的子部分。

## 促销和优惠券 {#promotions-and-vouchers}

### 优惠券 {#vouchers}

优惠券是一种经过实践检验的方法，提供折扣来吸引购物者进行购买和/或奖励客户的忠诚度。

* 优惠券供应：

   * 优惠券代码（由购物者键入购物车中）。
   * 优惠券标签（在购物者将其输入购物车后显示）。
   * 提升路径（定义凭证应用的操作）。

* 外部商业引擎也可以提供优惠券。

在AEM中：

* 优惠券是一种基于页面的组件，使用“网站”控制台创建/编辑。
* 此 **优惠券** 组件提供：

   * 凭证管理的呈现器；这将显示当前购物车中的任何凭证。
   * 用于管理（添加/删除）优惠券的编辑对话框（表单）。
   * 在购物车中添加/删除优惠券所需的操作。

* 优惠券没有自己的开始和结束日期/时间，但会使用父营销活动的日期/时间。

>[!NOTE]
>
>AEM使用术语 **优惠券**，这是术语的同义词 **优惠券**.

### 促销活动 {#promotions}

促销活动与优惠券一起，允许您实现以下场景：

* 公司为员工提供定制价格，这是手工编制的用户列表。
* 长期客户可获得所有订单的折扣。
* 在定义好的时间段内提供的销售价格。
* 当客户的先前订单超过特定金额时，客户会收到凭证。
* 购买产品的客户 *product-X* 在以下时段提供折扣： *product-Y* （配对产品）。

促销活动不是由产品信息经理维护的，而是由营销经理维护的：

* 促销活动是基于页面的组件，使用“网站”控制台创建/编辑。 ”
* 促销供应：

   * 优先级
   * 提升处理程序路径

* 您可以将促销活动关联到促销活动，以定义其打开/关闭日期/时间。
* 您可以将促销活动连接到体验以定义其区段。
* 未与体验关联的促销活动将不会自行触发，但优惠券仍可以触发。
* 提升组件包含：

   * 用于提升管理的渲染器和对话框
   * 用于呈现和编辑特定于提升处理程序的配置参数的子组件

在AEM中，促销活动还集成在 [Campaign Management](/help/sites-authoring/personalization.md)：

* a [营销活动](/help/sites-authoring/personalization.md) 指定开启/关闭时间
* [体验](/help/sites-authoring/personalization.md) *范围* 营销活动用于根据相应的受众区段对资产（Teaser页面、促销活动等）进行分组

促销可以在体验中或直接在营销策划中进行：

* 如果促销活动在体验中进行，则会自动将其应用于受众区段。

  例如，在geometrixx-outdoors示例站点中，促销活动包括：

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  位于体验中，因此每当区段( `ordervalueover100`)解析。

* 如果促销活动未出现在体验中（仅在营销活动中），则无法自动将其应用于受众。 但是，如果购物者在其购物车中输入优惠券，并且该优惠券引用了促销活动，则仍可以触发此事件。

  例如，促销活动：

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  位于体验之外，因此绝不会自动触发（即：基于分段）。 但是，从可在文章营销活动中的若干体验中找到的优惠券中可以找到它。 将这些优惠券代码输入购物车会导致促销触发。

>[!NOTE]
>
>[hybris促销活动](https://www.hybris.com/modules/promotion) 和 [hybris优惠券](https://www.hybris.com/en/modules/voucher) 覆盖影响购物车并与定价相关的所有内容。 促销特定的营销内容（如横幅等） 并不是hybris促销活动的一部分。

## 个性化 {#personalization}

### 客户注册和帐户 {#customer-registration-and-accounts}

购物者注册时，帐户详细信息必须在AEM和电子商务引擎之间同步。 敏感数据是独立保留的，但用户档案是共享的：

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

确切的机制可能取决于以下情况：

1. 这两个系统中都存在用户帐户：

   1. 无需执行任何操作。

1. 用户帐户仅存在于AEM中：

   1. 用户是在电子商务引擎中创建的，其帐户ID和随机密码均相同，并将存储在AEM中。
   1. 当AEM尝试在第一次调用（例如，请求产品页面并且价格引用电子商务引擎）时登录到电子商务引擎时，随机密码是必需的。 由于这种情况发生在AEM登录之后，因此密码不可用。

1. 用户帐户仅存在于电子商务引擎中：

   1. 该帐户在AEM中创建，具有相同的帐户ID和密码。

使用电子商务引擎时，AEM仅存储帐户ID和密码（可以选择用户组）。 所有其他信息都存储在电子商务引擎中。

>[!NOTE]
>
>在使用电子商务引擎时，您必须确保将为登录到AEM实例的用户创建的帐户复制（例如，通过工作流）到与该引擎通信的任何其他AEM实例。
>
>否则，这些其他AEM实例还将尝试为引擎中的相同用户创建帐户。 这些操作因 `DuplicateUidException` 从引擎里出来。

### 客户注册 {#customer-sign-up}

购物者通常需要注册才能访问购物车。 这需要注册（创建帐户），以便创建特定于客户的帐户。

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>还支持匿名购物车和结帐。

### 客户登录 {#customer-sign-in}

注册后，购物者可以使用他们的帐户登录，以便可以跟踪他们的操作并完成他们的订单。

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### 单点登录 {#single-sign-on}

提供单点登录(SSO)，以便作者在AEM和电子商务系统中都可知晓，而无需登录两次。

### myAccount {#myaccount}

来自电子商务引擎的交易数据与购物者的个人信息相结合。 AEM将这些数据中的一部分用作配置文件数据。 AEM中的表单操作会将信息写回电子商务引擎。

有一个页面可让您轻松管理帐户信息。 您可以通过单击 **我的帐户** Geometrixx ，或者导航到 `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### 通讯簿 {#address-book}

您的网站需要存储一系列地址；包括投放、帐单和备用地址。 您可以使用基于默认地址格式的表单来实现此功能，也可以使用AEM提供的通讯簿组件。

此通讯簿组件允许您：

* 编辑帐簿中的地址
* 从装运地址簿中选择一个地址
* 从帐簿中选择帐单地址的地址

您可以选择默认地址。

通讯簿组件可从 **我的帐户** 页面（通过单击） **通讯簿** 或通过导航到 `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

您可以单击 **添加新地址……** 在通讯簿中添加地址。 它会打开一个您可以填写的表单，然后单击 **添加地址**.

>[!NOTE]
>
>您可以在通讯簿中输入多个地址。

“结帐”购物车时使用通讯簿：

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

地址保留如下 `user_home/profile/addresses`.
例如，对于Alison Parker，它位于/home/users/geometrixx/aparker@geometrixx.info/profile/addresses下

您可以选择想要作为默认地址的地址，此信息将保留在购物者的个人资料中，而不是地址中。 配置文件属性 `address.default` 设置为值所选地址的路径。

### 客户特定的定价 {#customer-specific-pricing}

电子商务引擎使用上下文（主要是购物者信息）来确定其持有的价格，然后将正确信息提供回AEM。

## 购物车和订单 {#shopping-cart-and-orders}

购物时，购物者浏览产品页面并选择商品以将其放入购物车中。 当他们开始结帐时，可以下订单。

### 匿名购物者 {#anonymous-shoppers}

匿名客户可以：

* 查看产品
* 将产品添加到购物车
* 执行结帐以下订单

>[!NOTE]
>
>根据实例地址信息或客户注册的配置，可能需要在结账前进行注册。

### 注册购物者 {#registered-shoppers}

注册客户可以：

* 登录到他们的帐户
* 查看产品
* 将产品添加到购物车
* 执行结帐以下订单
* 查看和跟踪以前的订单

### 购物车内容概述 {#shopping-cart-content-overview}

购物车提供：

* 所选项目的概述
* 指向所选项目的产品页面的链接
* 能够：

   * 更新单个物料的数量/数量
   * 删除单个项目

![e-commerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

根据使用的引擎保存购物车：

* AEM generic将购物车存储在Cookie中。
* 某些电子商务引擎可以在会话中存储购物车。

无论哪种情况，项目都会在登录/注销过程中保留在购物车中（并且可以进行恢复）（但只能在同一台计算机/浏览器上进行）。 例如：

* 浏览方式 `anonymous` 并将产品添加到购物车
* 登录身份 `Allison Parker` - Allison的购物车是空的
* 将产品添加到Allison的购物车
* 注销 — 购物车显示产品 `anonymous`

* 再次登录身份 `Allison Parker` - Allison的产品已恢复

>[!NOTE]
>
>匿名购物车只能在同一计算机/浏览器上恢复。

>[!NOTE]
>
>不建议测试使用还原购物车内容 `admin` 帐户，因为这可能与 `admin` 电子商务引擎的帐户（例如，hybris）。

>[!NOTE]
>
>hybris可以配置为在定义的时间段后删除挂起的购物车。

在结帐之前，价格更改会在发生更改时反映在（两个系统中）系统中。

### 订单信息 {#order-information}

根据有关订单的实施信息保存在电子商务引擎或AEM中，此信息由AEM呈现。

存储各种信息，其中可能包括：

* **订单 ID**

  订单的参考编号。

* **订购时间**

  下订单的日期。

* **状态**

  订单的状态；例如，已发运。

* **货币**

  订单的货币。

* **内容项目**

  已排序的项的列表。

* **小计**

  所订购物料的总成本。

* **税费**

  订单上到期的任何税额。

* **运费**

  运费。

* **总计**

  订单的总值；订购的项目、税费和运费。

* **帐单地址**

  发票应发送到的地址。

* **付款标记**

  付款方式。

* **付款状态**

  付款的状态。

* **配送地址**

  货物应装运到的地址。

* **配送方式**

  运输方法；例如，陆地、海上或空中。

* **跟踪号**

  装运公司使用的任何跟踪编号。

* **跟踪链接**

  用于在发运时跟踪订单的链接。

>[!NOTE]
>
>创建订单向导中使用的字段取决于为该位置定义的触屏优化基架。 在常规示例中，这可以在以下位置找到：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

在AEM中保留订单后，订单控制台将为每个订单显示以下内容：

* 购物车中的项目数
* 订单的总值
* 下订单的时间
* 状态

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### 订单跟踪 {#order-tracking}

下订单后，购物者通常会返回：

* 检查其订单的状态
* 从订单中删除产品
* 将产品添加到订单

在收到订单交付后，购物者可能还希望查看一段时间内订单的历史记录。

订单履行和跟踪由电子商务引擎管理。 AEM可以使用“订单历史记录”组件来显示信息，该组件会显示所有相关详细信息，包括应用的优惠券和促销活动。 例如：

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## 签出 {#checkout}

使用标准AEM表单执行结账。 这允许营销经理使用营销内容自定义体验。

然后，电子商务利用AEM表单中的输入来管理结账过程。

### 支付安全性 {#payment-security}

包括信用卡信息在内的付款详细信息通常由电子商务引擎管理。 AEM将此类交易信息转发到引擎（然后从引擎转发到支付处理服务）。

可实现支付卡行业(PCI)合规性。

### 订单确认 {#confirmation-of-order}

订单已在屏幕上确认，并且可以通过以下链接进行跟踪： [订单跟踪](#order-tracking).

## 搜索 {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

由于AEM对产品使用标准页面，因此您可以使用标准搜索组件来创建搜索页面。

如果需要更全面的实施，您可以：

* 使用所需的功能扩展默认搜索组件。
* 在中实施搜索方法 `CommerceService` 然后使用搜索页面上的电子商务搜索组件。

使用电子商务引擎时，可以在电子商务引擎解决方案中完全实施电子商务搜索API，因此您可以使用提供的现成的电子商务搜索组件。 多面搜索允许您搜索JCR和/或引擎：
