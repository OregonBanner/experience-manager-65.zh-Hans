---
title: AEM Livefyre方法
seo-title: AEM Livefyre方法
description: 关于Adobe Experience Manager Livefyre常见用例的分步说明。
seo-description: 关于Adobe Experience Manager Livefyre常见用例的分步说明。
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# AEM Livefyre方法{#aem-livefyre-recipes}

关于Adobe Experience Manager Livefyre常见用例的分步说明。

## 使用现成的Livefyre AEM组件创建UGC，并使用Livefyre Media Wall进行显示 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

媒体墙将社交和本机Livefyre内容流化到实时社交墙中。 根据您的用例和要求，在AEM中实施媒体墙有多种方法。

AEM Livefyre包提供开箱即用的实施，而传统集成则提供创建自定义Livefyre AEM组件的功能。

### AEM集成 {#aem-integration}

Livefyre Adobe Experience manager包可用于AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参 [阅与Livefyre集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

要了解支持哪些Livefyre应用程序，请参阅 [Livefyre应用程序的AEM支持列表](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)。

### 传统实施（针对自定义AEM组件） {#traditional-implementation-for-customized-aem-components}

在自定义AEM组件或其他CMS（如WordPress、Sitecore或DemandWare）中实施Livefyre有三种方法。 传统的Livefyre集成与CMS无关。

**方法1:设计人员应用程序实施**

* **** 什么：集成Livefyre应用程序最简单、最快捷的方法。 您可以设计、配置和生成自定义的JavaScript嵌入代码，以便在几分钟内将媒体墙应用程序集成到页面上。
* **** 操作方法： 创 [建、预览、发布和嵌入媒体墙应用程序](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 示例： [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法2:SDK实施**

* **** 什么：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是为站点上的应用程序和身份验证提供支持的核心库。 它定义了全局 *窗口。Livefyre* 对象和单个公共方法 *Livefyre.require*，该方法可用于加载其他Livefyre javaScript库，这些库有助于嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **操作方式**:使 [用Livefyre javaScript SDK的streamhub-wallpackage](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration)

* **示例**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

有关使用SDK的高级自定义，请参阅 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法3:API实施**

* 为了创建自定义体验和数据可视化，可以使用Bootstrap和流API从头开始创建Livefyre应用程序，并使用Livefyre和 [社交数据](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

确保在构建UGC的 [UI时遵循Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html)、 [Facebook](https://en.facebookbrand.com/guidelines/brand)、 [](https://en.instagram-brand.com/) Instagram显示指南。

### 媒体墙身份验证集成 {#media-wall-authentication-integration}

有关需要身份验证的媒体墙集成，请参阅：

* [为AEM Identity Management自定义](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) “集成时单点登录”
* [第三方身份验证平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （标识集成）

### 用例概述 {#use-case-overview}

作为AEM客户，我希望使用现成的Livefyre AEM组件创建UGC，并使用Livefyre Media Wall进行显示：

实施步骤：

1. [入门](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [将AEM配置为使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [将AEM媒体墙组件拖放到页面上](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [配置流并添加规则，以创建UGC并在媒体墙组件上显示](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

有关流式UGC的培训视频，请参 [阅在Adobe Experience Manager Livefyre中创建自动内容流和搜索社交内容](https://helpx.adobe.com/experience-manager/tutorials.html)。

### 客户示例 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA巡回媒体墙](https://www.pgatour.com/social-hub.html)

为了创建自定义体验和数据可视化，可以使用Bootstrap和流API从头开始创建Livefyre应用程序，并使用Livefyre和 [社交数据](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

有关需要身份验证的Livefyre应用程序，请参 [阅适用于第三方身份验证平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) 。

* [PGA巡回媒体墙](https://www.pgatour.com/social-hub.html)
* [超时](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## 使用AEM组件或传统的Livefyre集成来集成Livefyre注释 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM集成 {#aem-integration-1}

Livefyre Adobe Experience manager包可用于AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参 [阅与Livefyre集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

### 传统实施（针对自定义AEM组件） {#traditional-implementation-for-customized-aem-components-1}

在自定义AEM组件或其他CMS（如WordPress、Sitecore或DemandWare）中实施Livefyre注释应用程序有三种方法。 传统的Livefyre集成与CMS无关。

**方法1:设计人员应用程序实施**

* **** 什么：集成Livefyre应用程序最简单、最快捷的方法。 您可以设计、配置和生成自定义的JavaScript嵌入代码，以便在几分钟内将媒体墙应用程序集成到页面上。
* **** 操作方法：创 [建、预览、发布和嵌入注释应用程序](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 示例： [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法2:SDK实施**

* **** 什么：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是为站点上的应用程序和身份验证提供支持的核心库。 它定义了全局 *窗口。Livefyre* 对象和单个公共方法 *Livefyre.require*，该方法可用于加载其他Livefyre javaScript库，这些库有助于嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **操作方法：**

   * 使用CollectionMeta令牌创建集合/ [应用程序](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html)。
   * 使用 [Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) .js嵌入代码结构将注释应用程序集成到站点中。

* **** 示例： [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

有关使用SDK的高级自定义，请参 [阅StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法3:API实施**

* 为了创建自定义体验和数据可视化，可以使用Bootstrap和流API从头开始创建Livefyre应用程序，并使用Livefyre和 [社交数据](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html)。

### 注释应用程序身份验证集成 {#comments-app-authentication-integration}

* [为AEM Identity Management自定义](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) “集成时单点登录”
* [第三方身份验证平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （标识集成）

### 客户示例 {#customer-examples-1}

* [Pose(Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## 使用Livefyre AEM Assets集成在AEM Assets中导入UGC {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre设置（针对UGC特选和权限管理）:**

1. [配置“流”和“添加规则”，将UGC组织到Livefyre资产库文件夹](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)。

   1. 有关流式UGC的培训视频，请参 [阅在Adobe Experience Manager Livefyre中创建自动内容流和搜索社交内容](https://helpx.adobe.com/experience-manager/tutorials.html)。

1. [在Livefyre资产库文件夹中收集、组织和管理精选的UGC](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html)。

   1. 有关在Livefyre Studio资产库中创建和管理文件夹的培训视频，请参 [阅使用Adobe Experience Manager Livefyre中的资产](https://helpx.adobe.com/experience-manager/tutorials.html)。

1. [请求使用Livefyre studio的精选UGC的权限](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html)。

**AEM设置（用于将UGC导入AEM资产）:**

1. [入门](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [将AEM配置为使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [将Livefyre创建的UGC导入AEM资产](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [澳大利亚旅游局](https://www.australia.com/en-us)

## 使用AEM组件或传统的Livefyre集成来集成Livefyre审阅 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM集成 {#aem-integration-2}

Livefyre Adobe Experience manager包可用于AEM 6.1、6.2SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参 [阅与Livefyre集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)。

审阅组件不是AEM 6.1支持的组件。请查看 [AEM支持列表以了解所有Livefyre应用程序](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)。

### 传统实施（针对自定义AEM组件） {#traditional-implementation-for-customized-aem-components-2}

有两种方法可将Livefyre Reviews应用程序实施到自定义AEM组件或WordPress、Sitecore或DemandWare等其他CMS中。 传统的Livefyre集成与CMS无关。

**方法1:SDK实施**

* **** 什么：Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) .js是为站点上的应用程序和身份验证提供支持的核心库。 它定义了全局 *窗口。Livefyre* 对象和单个公共方法 *Livefyre.require*，该方法可用于加载其他Livefyre javaScript库，这些库有助于嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **操作方法：**

   * 创建Reviews [CollectionMeta令牌](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) ，以指定要存储在Reviews Collection中的元数据。
   * 使用 [Livefyre.js嵌入代码结构](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) ，将审阅应 ** 用程序集成到站点中

* **** 示例： [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

有关使用SDK的高级自定义，请参 [阅StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)。

**方法2:API实施**

* 为了创建自定义的体验和数据可视化，可以使用Bootstrap和Stream API从头开始创建Livefyre应用程序和社交数据。

此处可找到其他评级和评 [论API](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)。

### 注释应用程序身份验证集成 {#comments-app-authentication-integration-1}

* [为AEM Identity Management自定义](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) “集成时单点登录”
* [第三方身份验证平台的Identity Integration](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) （标识集成）

### 客户示例 {#customer-examples-2}

* [超时](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

