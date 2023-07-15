---
title: 社交组件框架
description: 社交组件框架(SCF)简化了配置、自定义和扩展Communities组件的过程
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 0%

---

# 社交组件框架 {#social-component-framework}

社交组件框架(SCF)简化了服务器端和客户端上配置、自定义和扩展Communities组件的过程。

框架的好处包括：

* **功能**：开箱即用的易集成性，对80%的用例很少或没有自定义设置。
* **可剥皮**：一致地使用HTML属性进行CSS样式设置。
* **可扩展**：组件实施是面向对象的，并且业务逻辑较轻 — 易于在服务器上添加增量业务登录。
* **灵活**：简单的无逻辑JavaScript模板，易于叠加和自定义。
* **可访问**： HTTP API支持从任何客户端（包括移动应用程序）发布内容。
* **便携**：集成/嵌入到基于任何技术构建的任何网页中。

使用交互式浏览创作或发布实例 [社区组件指南](components-guide.md).

## 概述 {#overview}

在SCF中，组件由SocialComponent POJO、Handlebars JS模板（用于渲染组件）和CSS（用于设置组件样式）组成。

Handlebars JS模板可以扩展model/view JS组件，以处理用户与客户端上的组件的交互。

如果组件必须支持数据修改，则可以编写SocialComponent API的实施以支持编辑/保存类似于传统Web应用程序中模型/数据对象的数据。 此外，可以添加操作（控制器）和操作服务以处理操作请求、执行业务逻辑以及调用模型/数据对象上的API。

可以扩展SocialComponent API以提供客户端对视图层或HTTP客户端所需的数据。

### 如何为客户端呈现页面 {#how-pages-are-rendered-for-client}

![scf页面渲染](assets/scf-overview.png)

### 组件自定义和扩展 {#component-customization-and-extension}

要自定义或扩展组件，您只需将叠加和扩展写入/apps目录，这可以简化升级到未来版本的过程。

* 对于外观设置：
   * 仅 [CSS需要编辑](client-customize.md#skinning-css).
* 外观：
   * 更改JS模板和CSS。
* 对于Look、Feel和UX：
   * 更改JS模板、CSS和 [扩展/覆盖JavaScript](client-customize.md#extending-javascript).
* 要修改JS模板或GET端点可用的信息，请执行以下操作：
   * 扩展 [SocialComponent](server-customize.md#socialcomponent-interface).
* 要在操作期间添加自定义处理，请执行以下操作：
   * 写入 [操作扩展](server-customize.md#operationextension-class).
* 要添加自定义操作，请执行以下操作：
   * 新建 [Sling Post操作](server-customize.md#postoperation-class).
   * 使用现有 [操作服务](server-customize.md#operationservice-class) 根据需要。
   * 添加JavaScript代码以根据需要从客户端调用您的操作。

## 服务器端框架 {#server-side-framework}

该框架提供API来访问服务器上的功能，并支持客户端和服务器之间的交互。

### Java™ API {#java-apis}

Java™ API提供了易于继承或子类的抽象类和接口。

有关主要类的说明，请参见 [服务器端自定义](server-customize.md) 页面。

访问 [存储资源提供程序概述](srp.md) 了解有关使用UGC的信息。

### HTTP API {#http-api}

HTTP API支持PhoneGap应用程序、本机应用程序以及其他集成和混合的客户端平台的轻松自定义和选择。 此外，HTTP API允许社区站点作为服务运行，而无需客户端，这样框架组件可以集成到基于任何技术构建的任何网页中。

### HTTP API -GET请求 {#http-api-get-requests}

对于每个SocialComponent，该框架都提供一个基于HTTP的API端点。 通过向具有“.social.json”选择器+扩展名的资源发送GET请求来访问端点。 使用Sling，请求将传递给 `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. 将资源(resourceType)传递给 `SocialComponentFactoryManager` 并接收一个能够选择 `SocialComponent` 表示资源。

1. 调用工厂并接收 `SocialComponent` 能够处理资源和请求。
1. 调用 `SocialComponent`，这将处理请求并返回结果的JSON表示形式。
1. 将JSON响应返回给客户端。

**`GET Request`**

默认GETservlet监听.social.json请求，SocialComponent使用可自定义的JSON响应这些请求。

![scf框架](assets/scf-framework.png)

### HTTP API -POST请求 {#http-api-post-requests}

除了GET（读取）操作外，框架还定义端点模式以启用组件上的其他操作，包括创建、更新和删除。 这些端点是HTTP API，它们接受输入并使用HTTP状态代码或JSON响应对象进行响应。

该框架端点模式使得CUD操作具有可扩展、可重用和可测试的。

**`POST Request`**

每个SocialComponent操作都有一个SlingPOST：操作。 每个操作的业务逻辑和维护代码都封装在OperationService中，该服务可通过HTTP API或从其他位置作为OSGi服务访问。 提供了支持操作之前/操作之后可插拔操作扩展的挂接。

![scf-post-request](assets/scf-post-request.png)

### 存储资源提供程序(SRP) {#storage-resource-provider-srp}

要了解如何处理存储在中的UGC，请执行以下操作 [社区内容存储](working-with-srp.md)，请参见：

* [存储资源提供程序概述](srp.md)  — 简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP API实用程序方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md)  — 编码准则。

### 服务器端自定义 {#server-side-customizations}

访问 [服务器端自定义](server-customize.md) 有关自定义服务器端的Communities组件的业务逻辑和行为的信息。

## Handlebars JS模板语言 {#handlebars-js-templating-language}

新框架中更显着的变化之一是使用了 `Handlebars JS` (HBS)模板语言，一种用于服务器 — 客户端渲染的常用开源技术。

HBS脚本简单、无逻辑、在服务器和客户端上编译、易于叠加和自定义，并且与客户端UX自然绑定，因为HBS支持客户端渲染。

该框架提供了多个 [Handlebars助手](handlebars-helpers.md) 在开发SocialComponents时很有用。

在服务器上，当Sling解析GET请求时，它会标识用于响应请求的脚本。 如果脚本是HBS模板(.hbs)，Sling会将请求委派给Handlebars引擎。 然后，Handlebars引擎将从相应的SocialComponentFactory获取SocialComponent、构建上下文并渲染HTML。

### 无访问限制 {#no-access-restriction}

Handlebars (HBS)模板文件(.hbs)类似于.jsp和.html模板文件，但它们可用于在客户端浏览器和服务器上渲染。 因此，请求客户端模板的客户端浏览器从服务器接收.hbs文件。

这要求Sling搜索路径中的所有HBS模板（/libs/或/apps下的任何.hbs文件）可以由任何用户从创作或发布中获取。

可能不会禁止通过HTTP访问.hbs文件。

### 添加或包含社区组件 {#add-or-include-a-communities-component}

大多数社区组件必须 *已添加* 作为Sling可寻址资源。 选定的几个Communities组件可能是 *已包括* 在模板中作为非现有资源，以允许动态包含和自定义用户生成内容(UGC)的写入位置。

在任一情况下，组件的 [所需的客户端库](clientlibs.md) 也必须存在。

**添加组件**

添加组件是指添加资源（组件）实例的过程，例如从组件浏览器(sidekick)拖动到创作编辑模式下的页面上的过程。

结果是par节点下的JCR子节点，该节点为Sling可寻址。

**包括组件**

包含元件是指将参照添加到 [“非现有”资源](srp.md#for-non-existing-resources-ners) （无JCR节点），例如使用脚本语言。

自Adobe Experience Manager (AEM) 6.1起，如果动态包含而不是添加组件，则可以在创作中编辑组件的属性 *设计* 模式。

只能动态包含少量AEM Communities组件。 它们是：

* [评论](essentials-comments.md)
* [评分](rating-basics.md)
* [审核](reviews-basics.md)
* [投票](essentials-voting.md)

此 [社区组件指南](components-guide.md) 允许将可包含组件从添加更改为包含。

**使用Handlebars** 模板化语言，非现有资源使用 [包含辅助函数](handlebars-helpers.md#include) 通过指定其resourceType：

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP时**，则使用标记包含资源 [cq：include](../../help/sites-developing/taglib.md#lt-cq-include)：

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>要将组件动态添加到页面，而不是在模板中添加或包含组件，请参阅 [组件侧载](sideloading.md).

### Handlebars助手 {#handlebars-helpers}

参见 [SCF Handlebars助手](handlebars-helpers.md) 有关SCF中可用的自定义帮助程序的列表和描述。

## 客户端框架 {#client-side-framework}

### 模型视图JavaScript框架 {#model-view-javascript-framework}

该框架包括以下扩展 [Backbone.js](https://backbonejs.org/)，一个模型视图JavaScript框架，便于开发丰富、交互的组件。 面向对象的性质支持可扩展/可重用的框架。 HTTP API简化了客户端和服务器之间的通信。

框架使用服务器端Handlebars模板渲染客户端的组件。 这些模型基于HTTP API生成的JSON响应。 视图将自己绑定到Handlebars模板生成的HTML并提供交互性。

### CSS约定 {#css-conventions}

以下是定义和使用CSS类的推荐约定：

* 使用命名空间明确的CSS类选择器名称，并避免使用通用名称，如“标题”和“图像”。
* 定义特定的类选择器样式，以便CSS样式表可以很好地与页面上的其他元素和样式配合使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 对于由JavaScript驱动的UX，将用于样式的CSS类与CSS类分开。

### 客户端自定义 {#client-side-customizations}

要自定义客户端上Communities组件的外观和行为，请参阅 [客户端自定义](client-customize.md)，其中包含有关以下项的信息：

* [叠加](client-customize.md#overlays)
* [扩展名](client-customize.md#extensions)
* [HTML标记](client-customize.md#htmlmarkup)
* [设置CSS外观](client-customize.md#skinning-css)
* [扩展JavaScript](client-customize.md#extending-javascript)
* [适用于SCF的Clientlibs](client-customize.md#clientlibs-for-scf)

## 功能和组件要点 {#feature-and-component-essentials}

有关面向开发人员的基本信息，请参见 [功能和组件要点](essentials.md) 部分。

其他开发人员信息可在 [编码准则](code-guide.md) 部分。

## 疑难解答 {#troubleshooting}

有关常见问题和已知问题的说明，请参见 [疑难解答](troubleshooting.md) 部分。
