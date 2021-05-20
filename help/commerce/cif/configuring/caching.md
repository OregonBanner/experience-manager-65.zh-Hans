---
title: 缓存和性能
description: 了解可启用GraphQL和内容缓存以优化商务实施性能的各种配置。
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 缓存和性能 {#caching}

## 组件和GraphQL响应缓存 {#graphql}

AEM CIF核心组件已内置支持缓存各个组件的GraphQL响应。 此功能可用于大幅减少GraphQL后端调用的数量。 可以实现有效的缓存，特别是对于重复查询，例如检索导航组件的类别树或获取产品搜索和类别页面上显示的所有可用聚合/彩块化值。

对于AEM CIF核心组件，缓存是基于组件配置的，因此可以控制是否为每个组件缓存（以及缓存的时长）GraphQL请求/响应。 还可以使用GraphQL客户端定义OSGi服务的缓存行为。

### 配置

为给定组件配置后，缓存将开始存储由每个缓存配置条目定义的GraphQL查询和响应。 缓存大小和每个条目的缓存持续时间将基于项目进行定义，具体取决于目录数据更改的频率、组件始终显示最新可能数据的关键程度，等等。 请注意，没有任何缓存失效，因此在设置缓存持续时间时要小心。

为组件配置缓存时，缓存名称必须是您在项目中定义的&#x200B;**proxy**&#x200B;组件的名称。

在客户端发送GraphQL请求之前，它会检查是否已缓存&#x200B;**exact**&#x200B;同一GraphQL请求，并可能返回缓存的响应。 要进行匹配，GraphQL请求必须完全匹配，即查询、操作名称（如果有）、变量（如果有）都必须等于缓存的请求，并且所有可能设置的自定义HTTP标头也必须相同。 例如，Magento`Store`标头必须匹配。

### 示例

我们建议为可获取产品搜索和类别页面上显示的所有可用聚合/彩块化值的搜索服务配置一些缓存。 例如，只有在产品中添加了新属性时，这些值通常才会更改，因此，如果产品属性集不经常更改，则此缓存条目的持续时间可能会“较大”。 虽然这是特定于项目的，但我们建议在项目开发阶段使用几分钟的时间值，在稳定的生产系统上使用几小时的值。

这通常使用以下缓存条目进行配置：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建议使用GraphQl缓存功能的另一个示例方案是导航组件，因为它在所有页面上发送相同的GraphQL查询。 在这种情况下，缓存条目通常设置为：

```
venia/components/structure/navigation:true:10:600
```

考虑[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)时，使用。 请注意组件代理名称`venia/components/structure/navigation`的使用，以及&#x200B;**不** CIF导航组件的名称(`core/cif/components/structure/navigation/v1/navigation`)。

其他组件的缓存应根据项目进行定义，通常与在调度程序级别配置的缓存相协调。 请记住，这些缓存没有任何活动失效，因此应仔细设置缓存持续时间。 没有任何“一刀切”的值可匹配所有可能的项目和用例。 确保在项目级别定义最符合项目要求的缓存策略。

## 调度程序缓存 {#dispatcher}

在[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)中缓存AEM页面或片段是任何AEM项目的最佳实践。 通常，它依赖于失效技术来确保在AEM中更改的任何内容在Dispatcher中正确更新。 这是AEM Dispatcher缓存策略的核心功能。

除了纯AEM管理内容CIF之外，页面通常还可以显示通过GraphQL从Magento中动态获取的商务数据。 虽然页面结构本身可能永远不会更改，但商务内容可能会更改，例如，如果某些产品数据（如名称或价格）在Magento中发生更改。

为确保在AEM Dispatcher中缓存CIF页面的时间有限，我们因此建议在AEM Dispatcher中缓存CIF页面时使用[基于时间的缓存失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl)（也称为基于TTL的缓存）。 此功能可以在AEM中使用额外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)包进行配置。

使用基于TTL的缓存，开发人员通常为选定的AEM页面定义一个或多个缓存持续时间。 这可确保在配置的持续时间内，CIF页面仅会缓存在AEM Dispatcher中，并且内容会经常更新。

>[!NOTE]
>
>虽然AEM Dispatcher可能会缓存服务器端数据，但某些CIF组件（如`product`、`productlist`和`searchresults`组件）通常会在加载页面时在客户端浏览器请求中重新获取产品价格。 这可确保在页面加载时始终获取关键的动态内容。

## 其他资源

- [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL缓存配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
