---
title: 社交组件框架
seo-title: Social Component Framework
description: 社交组件框架(SCF)简化了配置、自定义和扩展社区组件的过程
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: 1d5cfff10735ea31dc0289b6909851b8717936eb
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 0%

---

# 社交组件框架 {#social-component-framework}

社交组件框架(SCF)简化了在服务器端和客户端上配置、自定义和扩展社区组件的过程。

该框架的好处：

* **功能**:开箱即用的集成，80%的用例很少或没有自定义。
* **斯金纳布尔**:一致地使用HTML属性来进行CSS样式设置。
* **可扩展**:组件实施是面向对象的，并且轻松利用业务逻辑 — 易于在服务器上添加增量业务登录。
* **灵活**:易于覆盖和自定义的简单无逻辑Javascript模板。
* **无障碍**:HTTP API支持从任何客户端（包括移动设备应用程序）发布内容。
* **便携式**:集成/嵌入任何基于任何技术构建的网页。

使用交互式浏览创作或发布实例 [社区组件指南](components-guide.md).

## 概述 {#overview}

在SCF中，组件由SocialComponent POJO、Handlebars JS模板（用于渲染组件）和CSS（用于设置组件样式）组成。

Handlebars JS模板可以扩展模型/视图JS组件，以处理用户与客户端上组件的交互。

如果组件需要支持数据的修改，则可以编写SocialComponent API的实现以支持编辑/保存与传统Web应用程序中的模型/数据对象类似的数据。 此外，可以添加操作（控制器）和操作服务以处理操作请求、执行业务逻辑以及在模型/数据对象上调用API。

SocialComponent API可以扩展，以提供客户端为视图层或HTTP客户端所需的数据。

### 如何为客户端呈现页面 {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### 组件自定义和扩展 {#component-customization-and-extension}

要自定义或扩展组件，您只需将叠加和扩展写入/apps目录，这简化了升级到未来版本的过程。

* 对于外观：
   * 仅 [CSS需要编辑](client-customize.md#skinning-css).
* 外观：
   * 更改JS模板和CSS。
* 外观和UX:
   * 更改JS模板、CSS和 [扩展/覆盖Javascript](client-customize.md#extending-javascript).
* 要修改JS模板或GET端点的可用信息，请执行以下操作：
   * 扩展 [SocialComponent](server-customize.md#socialcomponent-interface).
* 要在操作期间添加自定义处理，请执行以下操作：
   * 编写 [OperationExtension](server-customize.md#operationextension-class).
* 要添加新的自定义操作，请执行以下操作：
   * 新建 [Sling后操作](server-customize.md#postoperation-class).
   * 使用现有 [OperationServices](server-customize.md#operationservice-class) 根据需要。
   * 添加Javascript代码，以根据需要从客户端调用操作。

## 服务器端框架 {#server-side-framework}

该框架提供了用于访问服务器上功能的API，并支持客户端与服务器之间的交互。

### Java API {#java-apis}

Java API提供易于继承或子类化的抽象类和接口。

主要类在 [服务器端自定义](server-customize.md) 页面。

访问 [存储资源提供程序概述](srp.md) 以了解如何与UGC合作。

### HTTP API {#http-api}

HTTP API支持轻松自定义和选择PhoneGap应用程序、本机应用程序以及其他集成和混合的客户端平台。 此外，HTTP API允许社区站点在没有客户端的情况下作为服务运行，这样框架组件就可以集成到基于任何技术构建的任何网页中。

### HTTP API -GET请求 {#http-api-get-requests}

对于每个SocialComponent，框架都提供基于HTTP的API端点。 通过使用“.social.json”选择器+扩展向资源发送GET请求来访问端点。 使用Sling，会将请求转发给 `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. 将资源(resourceType)传递到 `SocialComponentFactoryManager` 并接收能够选择 `SocialComponent` 表示资源。

1. 调用工厂并接收 `SocialComponent` 能够处理资源和请求。
1. 调用 `SocialComponent`，用于处理请求并返回结果的JSON表示形式。
1. 将JSON响应返回给客户端。

**`GET Request`**

默认GETServlet侦听.social.json请求，SocialComponent将使用可自定义的JSON对其做出响应。

![scf-framework](assets/scf-framework.png)

### HTTP API -POST请求 {#http-api-post-requests}

除了GET（读取）操作之外，该框架还定义了端点模式，以对组件启用其他操作，包括创建、更新和删除。 这些端点是接受输入并以HTTP状态代码或JSON响应对象进行响应的HTTP API。

该框架端点模式使CUD操作具有可扩展性、可重用性和可测试性。

**`POST Request`**

每个SocialComponent操作都有一个SlingPOST：操作。 每个操作的业务逻辑和维护代码都封装在OperationService中，该OperationService可通过HTTP API访问，或从其他位置作为OSGi服务访问。 提供了支持在操作之前/之后可插拔操作扩展的挂钩。

![scf-post-request](assets/scf-post-request.png)

### 存储资源提供程序(SRP) {#storage-resource-provider-srp}

要了解如何处理存储在 [社区内容存储](working-with-srp.md)，请参阅：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC要点](srp-and-ugc.md) - SRP API实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。

### 服务器端自定义 {#server-side-customizations}

访问 [服务器端自定义](server-customize.md) 有关自定义服务器端社区组件的业务逻辑和行为的信息。

## Handlebars JS模板语言 {#handlebars-js-templating-language}

新框架中更显着的更改之一是使用 `Handlebars JS` (HBS)模板语言，一种用于服务器客户端渲染的常用开源技术。

HBS脚本简单、无逻辑、可在服务器和客户端上编译、易于覆盖和自定义，并且与客户端UX自然绑定，因为HBS支持客户端渲染。

该框架提供了以下几项 [Handlebars帮助程序](handlebars-helpers.md) 在开发SocialComponents时非常有用。

在服务器上，当Sling解析GET请求时，它会标识将用于响应请求的脚本。 如果脚本是HBS模板(.hbs),Sling会将请求委派给Handlebars引擎。 然后，Handlebars引擎将从相应的SocialComponentFactory中获取SocialComponent，构建上下文并渲染HTML。

### 无访问限制 {#no-access-restriction}

Handlebars(HBS)模板文件(.hbs)类似于.jsp和.html模板文件，不同之处在于它们可用于在客户端浏览器和服务器上渲染。 因此，请求客户端模板的客户端浏览器将从服务器接收.hbs文件。

这要求任何用户都可以从创作或发布中获取Sling搜索路径中的所有HBS模板（/libs/或/apps下的任何.hbs文件）。

不得禁止对.hbs文件的HTTP访问。

### 添加或包含社区组件 {#add-or-include-a-communities-component}

大多数社区组件必须 *添加* 作为Sling可寻址资源。 可以选择以下社区组件 *包含* 在模板中作为非现有资源，以允许动态包含和自定义用户生成内容(UGC)的写入位置。

无论哪种情况，组件的 [必需客户端库](clientlibs.md) 也必须存在。

**添加组件**

添加组件是指添加资源（组件）实例的过程，例如在创作编辑模式下从组件浏览器(Sidekick)拖动到页面上的过程。

结果会在par节点下方生成一个JCR子节点，该节点是Sling可寻址的。

**包含组件**

包括组件是指向 [“非现有”资源](srp.md#for-non-existing-resources-ners) （无JCR节点），例如使用脚本语言。

自AEM 6.1起，如果组件是动态包含的而不是添加的，则可以在创作*设计*模式中编辑组件的属性。

只能动态包含一些选定的AEM Communities组件。 它们是：

* [评论](essentials-comments.md)
* [评级](rating-basics.md)
* [审核](reviews-basics.md)
* [投票](essentials-voting.md)

的 [社区组件指南](components-guide.md) 允许将可包含的组件从添加切换到包含。

**使用Handlebars时** 模板语言，非现有资源则使用 [包含帮助程序](handlebars-helpers.md#include) 通过指定其resourceType:

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP时**，则使用标记包含资源 [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>要将组件动态添加到页面，而不是在模板中添加或包含组件，请参阅 [组件侧加载](sideloading.md).

### Handlebars Helpers {#handlebars-helpers}

请参阅 [SCF Handlebars Helpers](handlebars-helpers.md) 有关SCF中提供的自定义帮助程序的列表和说明。

## 客户端框架 {#client-side-framework}

### 模型视图Javascript框架 {#model-view-javascript-framework}

该框架包括 [Backbone.js](https://www.backbonejs.org/)，是一种模型视图的JavaScript框架，用于促进开发丰富的交互式组件。 面向对象的性质支持可扩展/可重用框架。 通过HTTP API简化了客户端与服务器之间的通信。

该框架利用服务器端Handlebars模板来为客户端渲染组件。 这些模型基于由HTTP API生成的JSON响应。 视图将自身绑定到由Handlebars模板生成的HTML，并提供交互性。

### CSS惯例 {#css-conventions}

以下是定义和使用CSS类的推荐约定：

* 使用明确命名的CSS类选择器名称，并避免使用通用名称，如“标题”、“图像”等。
* 定义特定的类选择器样式，以便CSS样式表能够很好地与页面上的其他元素和样式一起使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 对于由JavaScript驱动的UX，请将样式的CSS类与CSS类分开。

### 客户端自定义 {#client-side-customizations}

要自定义客户端上社区组件的外观和行为，请参考 [客户端自定义](client-customize.md)，其中包括以下信息：

* [叠加](client-customize.md#overlays)
* [扩展名](client-customize.md#extensions)
* [HTML标记](client-customize.md#htmlmarkup)
* [设置CSS外观](client-customize.md#skinning-css)
* [扩展Javascript](client-customize.md#extending-javascript)
* [用于SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能和组件要点 {#feature-and-component-essentials}

有关开发人员的基本信息，请参阅 [功能和组件要点](essentials.md) 中。

其他开发人员信息可在 [编码准则](code-guide.md) 中。

## 疑难解答 {#troubleshooting}

有关常见问题和已知问题，请参见 [疑难解答](troubleshooting.md) 中。
