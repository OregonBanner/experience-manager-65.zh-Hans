---
title: 使用Commerce Integration Framework集成AEM和Adobe Commerce
description: AEM和Adobe Commerce使用Commerce Integration Framework (CIF)无缝集成。 CIF允许AEM访问Adobe Commerce实例，并通过GraphQL与Adobe Commerce通信。 它还允许AEM作者使用产品和类别选取器以及产品控制台浏览从Adobe Commerce按需获取的产品和类别数据。 此外，CIF提供了一个现成的店面，可以加快商业项目的执行。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# 使用Commerce Integration Framework集成AEM和Adobe Commerce(Magento) {#aem-commerce-framework}

使用Commerce Integration Framework (CIF)无缝集成Experience Manager和Adobe Commerce。 CIF使AEM能够使用Adobe Commerce直接访问商务实例并与之通信 [GRAPHQL API](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
>支持的最低GraphQL API版本为2.3.5。仅较新版本或仅在Adobe Commerce版本中支持某些功能。

## 架构概述 {#overview}

整体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置通用工具实现的 [GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client) 与 [生成的数据模型集](https://github.com/adobe/commerce-cif-magento-graphql) 用于商务GraphQL架构。 此外，还可以使用GQL格式的任何GraphQL查询或变异。

对于客户端组件，使用构建 [React](https://reactjs.org/)，则 [Apollo客户端](https://www.apollographql.com/docs/react/) 已使用。

## AEM CIF核心组件架构 {#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 遵循与非常相似的设计模式和最佳实践 [AEM WCM核心组件](https://github.com/adobe/aem-core-wcm-components).

在Sling模型中实现了用于AEM CIF核心组件的业务逻辑和与Adobe Commerce的后端通信。 如果需要自定义此逻辑以满足项目特定的要求，可以使用Sling模型的委托模式。

>[!TIP]
>
>此 [自定义AEM CIF核心组件](../customizing/customize-cif-components.md) 页面提供了有关如何自定义CIF核心组件的详细示例和最佳实践。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置，轻松检索与AEM页面关联的Adobe Commerce商店的配置客户端。
