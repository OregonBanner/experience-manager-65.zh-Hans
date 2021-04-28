---
title: 缓存和性能
description: 了解可启用GraphQL和内容缓存以优化商务实施性能的不同配置。
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 1%

---

# 缓存和性能{#caching}

## 组件和GraphQL响应缓存{#graphql}

AEM CIF核心组件已内置了对各个组件的GraphQL响应缓存支持。 此功能可用于大幅减少GraphQL后端调用数。 可以实现有效的缓存，特别是对于重复查询，例如检索导航组件的类别树或提取在产品搜索和类别页面上显示的所有可用聚合/彩块化值。

对于AEM CIF核心组件，缓存是按组件配置的，因此可以控制是否（以及多长时间）为每个组件缓存GraphQL请求/响应。 还可以使用GraphQL客户端为OSGi服务定义缓存行为。

### 配置

为给定组件配置后，缓存开始会按照每个缓存配置条目所定义的方式存储GraphQL查询和响应。 每个条目的缓存大小和缓存持续时间将基于项目进行定义，例如，根据目录数据可能更改的频率、组件总是显示最新可能数据的重要性等。 请注意，没有任何缓存失效，因此，在设置缓存持续时间时要小心。

配置组件缓存时，缓存名称必须是您在项目中定义的&#x200B;**proxy**&#x200B;组件的名称。

在客户端发送GraphQL请求之前，它会检查该&#x200B;**exact**&#x200B;同一GraphQL请求是否已缓存，并可能返回缓存的响应。 要匹配，GraphQL请求必须完全匹配，即查询、操作名称（如果有）、变量（如果有）都必须与缓存的请求相等，并且可能设置的所有自定义HTTP头也必须相同。 例如，Magento`Store`标头必须匹配。

### 示例

我们建议为搜索服务配置一些缓存，以获取产品搜索和类别页面上显示的所有可用聚合/彩块化值。 这些值通常仅在向产品添加新属性时更改，因此，如果产品属性集不经常更改，则此缓存条目的持续时间可以“较大”。 虽然这是特定于项目的，但我们建议在项目开发阶段使用几分钟的值，在稳定的生产系统上使用几小时的值。

这通常使用以下缓存条目进行配置：

```
com.adobe.cq.commerce.core.search.services.SearchFilterService:true:10:3600
```

建议使用GraphQl缓存功能的另一个示例方案是导航组件，因为它在所有页面上发送相同的GraphQL查询。 在这种情况下，缓存条目通常设置为：

```
venia/components/structure/navigation:true:10:600
```

当考虑[Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)时。 请注意组件代理名称`venia/components/structure/navigation`和&#x200B;****&#x200B;的使用情况，`core/cif/components/structure/navigation/v1/navigation`不是CIF导航组件的名称。

其他组件的缓存应根据项目定义，通常与在调度程序级别配置的缓存协调。 请记住，这些缓存没有任何活动失效，因此应仔细设置缓存持续时间。 没有任何“一刀切”的值能够匹配所有可能的项目和使用案例。 请确保在项目级别定义最符合项目要求的缓存策略。

## 调度程序缓存{#dispatcher}

在[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)中缓存AEM页面或片段是任何AEM项目的最佳实践。 通常，它依赖于失效技术，以确保在AEM中更改的任何内容在调度程序中正确更新。 这是AEM Dispatcher缓存策略的核心功能。

除了纯AEM管理内容CIF外，页面通常还可以显示通过GraphQL从Magento动态获取的商务数据。 虽然页面结构本身可能永远不会更改，但商务内容可能会更改，例如，如果某些产品数据（如名称或价格）在Magento中发生更改。

为确保在AEM Dispatcher中缓存CIF页面的时间有限，因此建议在AEM Dispatcher中缓存CIF页面时使用[基于时间的缓存失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-time-based-cache-invalidation-enablettl)（也称为基于TTL的缓存）。 在AEM中，可以使用额外的[ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)包配置此功能。

使用基于TTL的缓存，开发者通常为选定的AEM页面定义一个或多个缓存持续时间。 这可确保在配置的持续时间内，CIF页面仅在AEM Dispatcher中缓存，并且内容将频繁更新。

>[!NOTE]
>
>虽然服务器端数据可以由AEM Dispatcher缓存，但某些CIF组件（如`product`、`productlist`和`searchresults`组件）通常在加载页面时在客户端浏览器请求中重新获取产品价格。 这可确保在页面加载时始终获取关键的动态内容。

## 其他资源

- [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [GraphQL缓存配置](https://github.com/adobe/commerce-cif-graphql-client#caching)
- [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)
