---
title: 社交组件框架
seo-title: 社交组件框架
description: 社交组件框架(SCF)简化了配置、自定义和扩展Communities组件的过程
seo-description: 社交组件框架(SCF)简化了配置、自定义和扩展Communities组件的过程
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# 社交组件框架 {#social-component-framework}

社交组件框架(SCF)简化了在服务器端和客户端上配置、自定义和扩展Communities组件的过程。

该框架的优势：

* **功能**:80%的用例只需进行少量或无自定义，即可轻松实现集成。
* **可设计外观**:一致地使用HTML属性进行CSS样式设置。
* **可扩展**:组件实现是面向对象的，并且业务逻辑简单——易于在服务器上添加增量式业务登录。
* **灵活**:轻松覆盖和自定义的简单无逻辑Javascript模板。
* **可访问**:HTTP API支持从任何客户端发布内容，包括移动应用程序。
* **便携**:集成／嵌入任何基于任何技术构建的网页。

使用交互式社区组件指南浏览创作或发 [布实例](components-guide.md)。

## 概述 {#overview}

在SCF中，组件由SocialComponent POJO、Handlebars JS模板（用于渲染组件）和CSS（用于设计组件样式）组成。

Handlebars JS模板可扩展模型/视图JS组件，以处理用户与客户端组件的交互。

如果某个组件需要支持修改数据，则可以编写SocialComponent API的实现以支持编辑／保存与传统Web应用程序中的模型／数据对象相似的数据。 此外，可以添加操作（控制器）和操作服务以处理操作请求，执行业务逻辑，以及调用模型／数据对象上的API。

SocialComponent API可以扩展以提供客户端对视图层或HTTP客户端所需的数据。

### 如何为客户呈现页面 {#how-pages-are-rendered-for-client}

![chlimage_1-25](assets/chlimage_1-25.png)

### 组件自定义和扩展 {#component-customization-and-extension}

要自定义或扩展组件，您只需将叠加和扩展写入/apps目录，这样可简化升级到未来版本的过程。

* 对于外观：
   * 只有 [CSS需要编辑](client-customize.md#skinning-css)。
* 外观：
   * 更改JS模板和CSS。
* 对于外观、感觉和UX:
   * 更改JS模板、CSS和扩 [展／覆盖Javascript](client-customize.md#extending-javascript)。
* 要修改JS模板或GET端点的可用信息，请执行以下操作：
   * 扩展 [SocialComponent](server-customize.md#socialcomponent-interface)。
* 要在操作过程中添加自定义处理，请执行以下操作：
   * 编写一 [个OperationExtension](server-customize.md#operationextension-class)。
* 添加新的自定义操作：
   * 创建新的 [Sling Post操作](server-customize.md#postoperation-class)。
   * 根据需 [要使用现有](server-customize.md#operationservice-class) OperationServices。
   * 根据需要，添加Javascript代码以从客户端调用您的操作。

## 服务器端框架 {#server-side-framework}

该框架提供API以访问服务器上的功能并支持客户端与服务器之间的交互。

### Java API {#java-apis}

Java API提供易于继承或子类的抽象类和接口。

主类在服务器端自定 [义页面上有介绍](server-customize.md) 。

访问 [存储资源提供商概述](srp.md) ，了解如何使用UGC。

### HTTP API {#http-api}

HTTP API支持PhoneGap应用程序、本机应用程序以及其他集成和混合的轻松自定义和客户端平台选择。 此外，HTTP API允许社区站点作为服务运行而无需客户端，这样框架组件可以集成到任何基于任何技术构建的任何网页中。

### HTTP API - GET请求 {#http-api-get-requests}

对于每个SocialComponent，该框架都提供一个基于HTTP的API端点。 通过向资源发送GET请求并使用“.social.json”选择器+扩展名来访问端点。 使用Sling，请求将递交给 `DefaultSocialGetServlet`。

**`DefaultSocialGetServlet`**

1. 将资源(resourceType)传递给 `SocialComponentFactoryManager` 并接收能够选择表示资源的 `SocialComponent` SocialComponentFactory。

1. 调用工厂并接收能 `SocialComponent` 够处理资源和请求的设备。
1. 调用 `SocialComponent`该函数，它处理请求并返回结果的JSON表示形式。
1. 将JSON响应返回给客户端。

**`GET Request`**

默认GET servlet监听。social.json请求，SocialComponent将用可自定义的JSON响应这些请求。

![chlimage_1-26](assets/chlimage_1-26.png)

### HTTP API - POST请求 {#http-api-post-requests}

除了GET（读取）操作之外，框架还定义端点模式以对组件启用其他操作，包括创建、更新和删除。 这些端点是接受输入并使用HTTP状态代码或JSON响应对象进行响应的HTTP API。

该框架端点模式使CUD操作具有可扩展性、可重用性和可测试性。

**`POST Request`**

每个SocialComponent操作都有一个Sling POST：操作。 每个操作的业务逻辑和维护代码都打包在OperationService中，OperationService可通过HTTP API访问，或从OSGi服务的其他位置访问。 提供了支持用于前／后操作的可插拔操作扩展的钩子。

![chlimage_1-27](assets/chlimage_1-27.png)

### 存储资源提供商(SRP) {#storage-resource-provider-srp}

要了解如何处理存储在社区内容 [存储中的UGC](working-with-srp.md)，请参阅：

* [存储资源提供者概述](srp.md) -简介和存储库使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP API实用程序方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) —— 编码准则访问UGC。

### 服务器端自定义 {#server-side-customizations}

有关 [在服务器端自定义Communities组件的业务逻辑和行为的信息](server-customize.md) ，请访问服务器端自定义。

## Handlebars JS模板语言 {#handlebars-js-templating-language}

在新框架中，一个更显着的变化是使用 [Handlebars JS模板语言(HBS)](https://www.handlebarsjs.com/)，这是一种用于服务器客户端渲染的流行开源技术。

HBS脚本简单、无逻辑、可在服务器和客户端上进行编译、易于叠加和自定义，并且与客户端UX自然绑定，因为HBS支持客户端渲染。

该框架提供了几个 [Handlebars帮助器](handlebars-helpers.md) ，这些帮助器在开发SocialComponents时非常有用。

在服务器上，当Sling解析GET请求时，它标识将用于响应请求的脚本。 如果脚本是HBS模板(.hbs),Sling将将请求委派给Handlebars引擎。 然后，Handlebars引擎将从相应的SocialComponentFactory获取SocialComponent，构建上下文并渲染HTML。

### 无访问限制 {#no-access-restriction}

Handlebars(HBS)模板文件(.hbs)与。jsp和。html模板文件类似，不同之处在于它们可用于在客户端浏览器中和服务器上进行渲染。 因此，请求客户端模板的客户端浏览器将从服务器接收。hbs文件。

这要求任何用户都可以从作者或发布中获取sling搜索路径中的所有HBS模板（/libs/或/apps下的任何。hbs文件）。

不禁止对。hbs文件进行HTTP访问。

### 添加或包含社区组件 {#add-or-include-a-communities-component}

大多数Communities组件必须 *作为* Sling可寻址资源添加。 在模板中，可以 *将* “社区”组件中的若干个作为非现有资源包含在模板中，以允许动态包含和自定义写入用户生成内容(UGC)的位置。

无论哪种情况，组件所需 [的客户端库](clientlibs.md) 都必须存在。

**添加组件**

添加组件是指添加资源（组件）实例的过程，例如在创作编辑模式下从组件浏览器(Sidekick)拖动到页面时。

结果是par节点下的JCR子节点，该节点是Sling可寻址的。

**包括组件**

包括组件是指在模板中添加对“非现有”资源 [](srp.md#for-non-existing-resources-ners) （无JCR节点）的引用的过程，如使用脚本语言。

自AEM 6.1起，当动态包含组件而不是添加组件时，可以在作者*design *mode中编辑组件的属性。

只能动态包含少数几个AEM Communities组件。 它们是：

* [评论](essentials-comments.md)
* [评级](rating-basics.md)
* [审核](reviews-basics.md)
* [投票](essentials-voting.md)

社 [区组件指南](components-guide.md) ，允许将可包含的组件从添加切换为包含的组件。

**使用Handlebars模板语言时** ，通过指定resourceType，使用 [include helper](handlebars-helpers.md#include) 来包含非现有资源：

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**使用JSP**&#x200B;时，将使用标记 [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>要将组件动态添加到页面，而不是在模板中添加组件或将其包含在模板中，请参阅 [组件侧传](sideloading.md)。


### Handlebars Helpers {#handlebars-helpers}

请参 [阅SCF Handlebars Helpers](handlebars-helpers.md) ，了解SCF中可用的定制帮助器的列表和说明。

## 客户端框架 {#client-side-framework}

### 模型视图Javascript框架 {#model-view-javascript-framework}

该框架包括 [Backbone.js的扩展](https://www.backbonejs.org/)，这是一个模型视图的JavaScript框架，用于促进丰富的交互式组件的开发。 面向对象的性质支持可扩展／可重用的框架。 通过HTTP API简化了客户端与服务器之间的通信。

该框架利用服务器端的Handlebars模板为客户端渲染组件。 这些模型基于HTTP API生成的JSON响应。 这些视图将自己绑定到由Handlebars模板生成的HTML并提供交互性。

### CSS惯例 {#css-conventions}

以下是定义和使用CSS类的推荐约定：

* 使用名称清晰的CSS类选择器名称并避免使用“标题”、“图像”等通用名称。
* 定义特定类选择器样式，使CSS样式表能与页面上的其他元素和样式很好地配合使用。 例如：`.social-forum .topic-list .li { color: blue; }`
* 使用JavaScript驱动的UX的样式设计CSS类与CSS类分开。

### 客户端自定义 {#client-side-customizations}

要自定义客户端上的社区组件的外观和行为，请参考客户端自 [定义](client-customize.md)，其中包括以下信息：

* [叠加](client-customize.md#overlays)
* [扩展](client-customize.md#extensions)
* [HTML标记](client-customize.md#htmlmarkup)
* [设置CSS外观](client-customize.md#skinning-css)
* [扩展Javascript](client-customize.md#extending-javascript)
* [SCF的Clientlib](client-customize.md#clientlibs-for-scf)

## 功能和组件基本功能 {#feature-and-component-essentials}

有关开发人员的基本信息，请参阅功能 [和组件基本信息](essentials.md) 。

有关其他开发人员信息，请参阅编码 [准则部分](code-guide.md) 。

## 疑难解答 {#troubleshooting}

疑难解答部分介绍了常见问题和已 [知问题](troubleshooting.md) 。

