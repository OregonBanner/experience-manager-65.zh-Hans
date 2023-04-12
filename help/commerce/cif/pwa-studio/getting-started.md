---
title: AEM扩展入门PWA Studio
description: 了解如何通过PWA Studio来部署AEM无标题内容和商务项目。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# AEM扩展入门PWA Studio {#getting-started-pwa}

PWA Studio通过GraphQL与Adobe Commerce无缝集成，开箱即用，为创建创新、引人入胜的店面和其他数字体验提供了无限的选项。

内容片段是具有预定义结构的内容片段，允许使用GraphQL作为不同格式（例如JSON、Markdown）的API以无头方式使用，并独立渲染。 内容片段包含GraphQL所需的所有数据类型和字段，以确保您的应用程序仅请求可用内容并接收预期内容。 它们在结构方面提供的灵活性使其非常适合在多个位置和多个渠道中使用。

在Adobe Experience Manager中使用内容片段模型编辑器，可以轻松设计所需的结构。 将Adobe Experience Manager内容片段（或任何其他数据）与PWA Studio应用程序集成的主要挑战是从多个GraphQL端点获取数据。 原因是，PWA Studio可开箱即用于单个Adobe Commerce GraphQL端点。

## 架构 {#architecture}

![PWA无头架构](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## 设置PWA Studio {#setup-pwa}

要设置PWA Studio应用程序，请按照Adobe Commerce [PWA Studio文档](https://developer.adobe.com/commerce/pwa-studio/tutorials/).

要将PWA Studio与AEM的GraphQL端点连接，您可以使用 [AEM扩展for PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions).

1. 签出存储库

1. 在PWA Studio应用程序中，将该扩展添加为开发依赖项。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 将Apollo Link包装器添加到您的PWA Studio应用程序。 在pwa-root/src/index.js中，进行以下更改：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   您可以在 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 要使用博客条目扩展导航组件，请将以下适配添加到pwa-root/local-intercept.js :

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   您可以在 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 和 [扩展性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio文档。

1. Apollo客户端预期AEM GraphQL端点位于 `<https://pwa-studio/endpoint.js>`. 要将端点映射到此位置，请自定义PWA Studio应用程序的UPPRAD配置：a.至 `pwa-root/.env`，添加AEM_CFM_GRAPHQL变量，并对其进行调整以指向AEM内容片段GraphQL端点。

   示例：AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b.将代理解析程序添加到UPPRAD配置。 向上配置示例可能如下所示：

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## 设置AEM {#setup-aem}

按照AEM内容片段文档，为AEM项目设置GraphQL端点。 此外，在您的AEM项目中，添加以下配置，以允许PWA Studio应用程序访问GraphQL端点：

* AdobeGranite跨源资源共享策略(com.adobe.granite.cors.impl.CORSPolicyImpl)

   设置 `allowedorigin` 资产到PWA应用程序的完整主机名。

   示例:  `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling反向链接过滤器(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   将allow.hosts属性设置为PWA应用程序的主机名。

   示例：pwa-studio-test-vflyn.local.pwadev

您可以在此处找到两种配置的完整示例： <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

为了展示GraphQL端点，Adobe通过内容包准备了一些示例内容片段模型和数据。 这些组件可与随PWA Studio扩展提供的React组件一起使用。

## 使用方法 {#how-to-use}

此扩展被视为如何将PWA Studio应用程序与AEM连接以通过GraphQL检索和渲染内容的示例实施。

根据您的用例，您需要创建自己的自定义内容片段模型，从而生成自定义GraphQL模式，然后由您自己的React组件使用该模式。

生产设置可以在多个方面有所不同。

* 您可以使用单个GraphQL联合端点，该端点将AEM和Adobe Commerce GraphQL数据合并，而不是自定义Apollo客户端。
* 您的PWA Studio应用程序可以直接使用AEM GraphQL端点URL，而无需具有UPPRACH的代理。 此外，还可以将代理移动到其他层（例如，CDN）。
* 最适合您的方法还在很大程度上取决于您如何向最终用户交付PWA Studio应用程序。

此扩展包含两个示例。

### 博客 {#blog}

根据某些内容片段模型显示博客帖子。 此外，它还包含如何配置Apollo客户端以与AEM GraphQL端点一起使用以及如何在PWA Studio中扩展导航组件的示例。 请参阅 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 以了解更多详细信息。

### PDP扩充 {#pdp-enrichment}

使营销人员能够通过作为内容片段管理的其他内容轻松扩充PDP。 请参阅 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 以了解更多详细信息。
