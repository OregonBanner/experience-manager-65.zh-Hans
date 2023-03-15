---
title: AEMPWA Studio扩展快速入门
description: 了解如何使用PWA Studio部署AEM Headless Content and Commerce项目。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# AEMPWA Studio扩展快速入门 {#getting-started-pwa}

开箱即用的PWA Studio通过GraphQL与Adobe Commerce无缝集成，提供无限种选项，用于创建创新且富有吸引力的店面和其他数字体验。

内容片段是带有预定义结构的内容片段，允许以Headless方式使用GraphQL作为API，以各种格式（例如JSON、Markdown）进行使用并独立渲染。 内容片段包括GraphQL所需的所有数据类型和字段，以确保您的应用程序仅请求可用内容并接收预期内容。 它们在结构上提供了灵活性，非常适合在多个位置和多个渠道上使用。

使用Adobe Experience Manager中的内容片段模型编辑器，可以轻松设计所需的结构。 将Adobe Experience Manager内容片段（或任何其他数据）与PWA Studio应用程序集成的主要挑战是从多个GraphQL端点获取数据。 这是因为开箱即用PWA Studio可与单个Adobe Commerce GraphQL端点配合使用。

## 架构 {#architecture}

![PWAHeadless体系结构](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## 设置PWA Studio {#setup-pwa}

关注Adobe Commerce [PWA Studio文档](https://developer.adobe.com/commerce/pwa-studio/tutorials/) 以设置您的PWA Studio应用程序。

要将PWA Studio连接到AEM的GraphQL端点，您可以使用 [适用于PWA Studio的AEM扩展](https://github.com/adobe/aem-pwa-studio-extensions).

1. 签出存储库

1. 在PWA Studio应用程序中，将扩展添加为开发依赖项。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 将Apollo Link包装器添加到您的PWA Studio应用程序。 在pwa-root/src/index.js中，进行以下更改：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   有关Apollo客户端自定义设置的更多详细信息，请参阅 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js).

1. 要使用博客条目扩展导航组件，请将以下自适应内容添加到pwa-root/local-intercept.js：

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   您可以在中找到有关自定义导航组件的更多详细信息 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 和 [可扩展性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio的文档。

1. Apollo客户端将预期AEM GraphQL端点位于 <https://pwa-studio/endpoint.js>. 要将端点映射到此位置，您需要自定义PWA Studio应用程序的UPPER配置： a。将AEM_CFM_GRAPHQL变量添加到pwa-root/.env，并将其调整为指向您的AEM内容片段GraphQL端点。

   示例： AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b.向UPGRADE配置添加代理解析器。 UPWARD配置示例可能如下所示：

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

按照AEM内容片段文档，为您的AEM项目设置GraphQL端点。 此外，在您的AEM项目中，添加以下配置以允许PWA Studio应用程序访问GraphQL端点：

* AdobeGranite跨源资源共享策略(com.adobe.granite.cors.impl.CORSPolicyImpl)

   将allowedorigin属性设置为PWA应用程序的完整主机名。

   示例:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Apache Sling引用过滤器(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   将allow.hosts属性设置为PWA应用程序的主机名。

   示例： pwa-studio-test-vflyn.local.pwadev

您可以在此处找到这两种配置的完整示例： <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>.

为了展示GraphQL端点，我们通过内容包准备了一些示例内容片段模型和数据。 这些组件与随PWA Studio扩展一起提供的React组件可以很好地配合使用。

## 使用方法 {#how-to-use}

此扩展被视为如何将PWA Studio应用程序与AEM连接以通过GraphQL检索和渲染内容的示例实施。

根据您的用例，您希望创建自己的自定义内容片段模型，该模型会生成自定义GraphQL架构，然后您自己的React组件可以使用该架构。

生产设置可能在多个方面有所不同。

* 您可以具有一个联合GraphQL端点，它结合了AEM和Adobe Commerce GraphQL数据，而不是自定义Apollo客户端。
* 您的PWA Studio应用程序可以直接使用AEM GraphQL端点URL，而无需具有UPLOAD的代理。 代理也可以移到其他层（例如CDN）。
* 哪一种方法最适合您在很大程度上取决于您如何将PWA Studio应用程序交付给最终用户。

此扩展提供了两个示例。

### 博客 {#blog}

根据某些内容片段模型显示博客帖子。 此外，它还包含有关如何配置Apollo客户端以使用AEM GraphQL端点的示例以及如何在PWA Studio中扩展导航组件的示例。 参见 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 了解更多详细信息。

### PDP扩充 {#pdp-enrichment}

使营销人员能够轻松地使用作为内容片段管理的附加内容扩充PDP。  参见 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 了解更多详细信息。
