---
title: AEM Livefyre 指南
seo-title: AEM Livefyre Recipes
description: 关于 Adobe Experience Manager Livefyre 常见用例的分步说明。
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# AEM Livefyre 指南{#aem-livefyre-recipes}

关于 Adobe Experience Manager Livefyre 常见用例的分步说明。

## 使用现成的Livefyre AEM组件策划UGC，并使用Livefyre Media Wall进行显示 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall将社交和原生Livefyre内容流式传输到实时社交留言板中。 在AEM中实施Media Wall的方法多种多样，具体取决于您的用例和要求。

AEM Livefyre包提供了开箱即用的实施，而传统集成提供了创建自定义Livefyre AEM组件的功能。

### AEM集成 {#aem-integration}

Livefyre Adobe Experience Manager软件包适用于AEM 6.1、6.2 SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参阅 [与Livefyre集成](https://helpx.adobe.com/cn/experience-manager/6-4/sites/administering/using/livefyre.html).

要查看支持的Livefyre应用程序，请参阅 [适用于Livefyre应用程序的AEM支持列表](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 传统实施(适用于自定义AEM组件) {#traditional-implementation-for-customized-aem-components}

有三种方法可以在自定义AEM组件或其他CMS（如WordPress、Sitecore或DemandWare）中实施Livefyre。 传统的Livefyre集成与CMS无关。

**方法1：设计器应用程序实施**

* **内容：** 集成Livefyre应用程序的最简单、最快的方法。 您可以设计、配置和生成自定义的JavaScript嵌入代码，以便在几分钟内将媒体墙应用程序集成到页面上。
* **方法：**  [创建、预览、发布和嵌入Media Wall应用程序](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **示例：** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法2：SDK实施**

* **内容：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是支持网站上的应用程序和身份验证的核心库。 它定义了全局 *window.Livefyre* 对象和单一公共方法， *Livefyre.require*，可用于加载其他Livefyre JavaScript库，帮助嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **如何**： [使用Livefyre JavaScript SDK的streamhub-wallpackage](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **示例**： [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

有关使用SDK的高级自定义设置，请参阅 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法3：API实施**

* 为了创建自定义体验和数据可视化图表，可以通过使用Livefyre和社交数据，从头开始创建Livefyre应用程序。 [Bootstrap和流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

确保关注 [twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html)， [facebook](https://en.facebookbrand.com/guidelines/brand)、和 [instagram](https://en.instagram-brand.com/) 在为UGC构建UI时显示准则。

### Media Wall身份验证集成 {#media-wall-authentication-integration}

对于需要身份验证的Media Wall集成，请参阅：

* [自定义单点登录集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 适用于AEM Identity Management
* [身份集成](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 适用于第三方身份验证平台

### 用例概述 {#use-case-overview}

作为AEM客户，我想使用开箱即用的Livefyre AEM组件策划UGC，并使用Livefyre Media Wall进行显示：

实施步骤：

1. [快速入门](https://helpx.adobe.com/cn/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [配置AEM以使用Livefyre](https://helpx.adobe.com/cn/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [将AEM Media Wall组件拖放到页面上](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [配置流并添加规则以策划UGC并在Media Wall组件上显示](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

有关流UGC的培训视频，请参阅 [在Adobe Experience Manager Livefyre中创建自动内容流并搜索社交内容](https://helpx.adobe.com/experience-manager/tutorials.html).

### 客户示例 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA导览媒体墙](https://www.pgatour.com/social-hub.html)

为了创建自定义体验和数据可视化图表，可以通过使用Livefyre和社交数据，从头开始创建Livefyre应用程序。 [Bootstrap和流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

对于需要身份验证的Livefyre应用程序，请参阅 [身份集成](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 适用于第三方身份验证平台。

* [PGA导览媒体墙](https://www.pgatour.com/social-hub.html)
* [超时](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## 使用AEM组件或传统的Livefyre集成来集成Livefyre注释 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM集成 {#aem-integration-1}

Livefyre Adobe Experience Manager软件包适用于AEM 6.1、6.2 SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参阅 [与Livefyre集成](https://helpx.adobe.com/cn/experience-manager/6-4/sites/administering/using/livefyre.html).

### 传统实施(适用于自定义AEM组件) {#traditional-implementation-for-customized-aem-components-1}

有三种方法可以在自定义AEM组件或其他CMS（如WordPress、Sitecore或DemandWare）中实施Livefyre注释应用程序。 传统的Livefyre集成与CMS无关。

**方法1：设计器应用程序实施**

* **内容：** 集成Livefyre应用程序的最简单、最快的方法。 您可以设计、配置和生成自定义的JavaScript嵌入代码，以便在几分钟内将媒体墙应用程序集成到页面上。
* **方法：** [创建、预览、发布和嵌入评论应用程序](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **示例：** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法2：SDK实施**

* **内容：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是支持网站上的应用程序和身份验证的核心库。 它定义了全局 *window.Livefyre* 对象和单一公共方法， *Livefyre.require*，可用于加载其他Livefyre JavaScript库，帮助嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **方法：**

   * 使用以下方式创建收藏集/应用程序 [CollectionMeta标记](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * 集成 [评论应用程序](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) 嵌入到使用Livefyre.js嵌入代码结构的网站中。

* **示例：**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

有关使用SDK的高级自定义设置，请参阅 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法3：API实施**

* 为了创建自定义体验和数据可视化图表，可以通过使用Livefyre和社交数据，从头开始创建Livefyre应用程序。 [Bootstrap和流API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Comments应用程序身份验证集成 {#comments-app-authentication-integration}

* [自定义单点登录集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 适用于AEM Identity Management
* [身份集成](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 适用于第三方身份验证平台

### 客户示例 {#customer-examples-1}

* [波伊西（金伯利·克拉克）](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## 使用Livefyre AEM Assets集成在AEM Assets中导入UGC {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre设置(用于UGC管理和Rights Management)：**

1. [配置流并添加规则以将UGC策划到Livefyre资产库文件夹](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. 有关流UGC的培训视频，请参阅 [在Adobe Experience Manager Livefyre中创建自动内容流并搜索社交内容](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [在Livefyre资产库文件夹中收集、组织和管理策划的UGC](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. 有关在Livefyre Studio资产库中创建和管理文件夹的培训视频，请参阅 [在Adobe Experience Manager Livefyre中使用资源](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [使用Livefyre Studio策划的UGC的请求权限](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM设置(用于将UGC导入AEM Assets)：**

1. [快速入门](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [配置AEM以使用Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [将Livefyre策划的UGC导入AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [澳大利亚旅游](https://www.australia.com/en-us)

## 使用AEM组件或传统Livefyre集成来集成Livefyre审阅 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM集成 {#aem-integration-2}

Livefyre Adobe Experience Manager软件包适用于AEM 6.1、6.2 SP1、6.3、6.4和6.4 SP1。 不支持AEM 5.x和6.0。 有关详细说明，请参阅 [与Livefyre集成](https://helpx.adobe.com/cn/experience-manager/6-4/sites/administering/using/livefyre.html).

审核组件不是AEM 6.1支持的组件。请查看 [适用于所有Livefyre应用程序的AEM支持列表](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 传统实施(适用于自定义AEM组件) {#traditional-implementation-for-customized-aem-components-2}

有两种方法可以将Livefyre审阅应用程序实施到自定义AEM组件或其他CMS（如WordPress、Sitecore或DemandWare）中。 传统的Livefyre集成与CMS无关。

**方法1：SDK实施**

* **内容：** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 是支持网站上的应用程序和身份验证的核心库。 它定义了全局 *window.Livefyre* 对象和单一公共方法， *Livefyre.require*，可用于加载其他Livefyre JavaScript库，帮助嵌入Livefyre应用程序并与第三方用户身份验证平台集成。

* **方法：**

   * 创建审核 [CollectionMeta标记](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 指定要在审阅收藏集中存储的元数据。
   * 集成 [审核应用程序](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 到站点 *Livefyre.js* 嵌入代码结构

* **示例：**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

有关使用SDK的高级自定义设置，请参阅 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**方法2：API实施**

* 为了创建自定义体验和数据可视化图表，可以通过使用Bootstrap和流API使用Livefyre和社会数据从头开始创建Livefyre应用程序。

可以找到其他评级和审核API [此处](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Comments应用程序身份验证集成 {#comments-app-authentication-integration-1}

* [自定义单点登录集成](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 适用于AEM Identity Management
* [身份集成](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 适用于第三方身份验证平台

### 客户示例 {#customer-examples-2}

* [超时](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [霉菌](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
