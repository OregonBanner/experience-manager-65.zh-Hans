---
title: AEM and Adobe Commerce(Magento)Integration using Commerce Integration Framework
description: AEM和Adobe Commerce(Magento)是使用Commerce Integration Framework(CIF)无缝集成的。 CIF使AEM能够访问Magento实例并通过GraphQL与Magento通信。 它还允许AEM作者使用产品和类别选择器以及产品控制台浏览从Magento按需获取的产品和类别数据。 此外，CIF提供开箱即用的店面，可加速商业项目。
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 1%

---

# AEM和Adobe Commerce(Magento)集成使用Commerce Integration Framework {#aem-magento-framework}

Experience Manager和Adobe商务(Magento)使用商务集成框架(CIF)无缝集成。 CIF使AEM能够使用Adobe Commerce的[GraphQL APIs](https://devdocs.magento.com/guides/v2.4/graphql/)直接访问商务实例并与其通信。

## 架构概述{#overview}

总体架构如下：

![CIF架构概述](../assets/AEM_Magento_Architecture.png)

在CIF中，支持服务器端和客户端通信模式。
服务器端API调用是使用内置的通用[GraphQL客户端](https://github.com/adobe/commerce-cif-graphql-client)与商务GraphQL模式的[一组生成的数据模型](https://github.com/adobe/commerce-cif-magento-graphql)组合实现的。 此外，可以使用GQL格式的任何GraphQL查询或变异。

对于使用[React](https://reactjs.org/)构建的客户端组件，使用[Apollo Client](https://www.apollographql.com/docs/react/)。

## AEM CIF核心组件架构{#cif-core-components}

![AEM CIF核心组件架构](../assets/cif-component-architecture.jpg)

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件遵循与AEM WCM核心组件非常相似的设计 [模式和最佳做法](https://github.com/adobe/aem-core-wcm-components)。

AEM CIF核心组件的业务逻辑和与Adobe商务的后端通信在Sling模型中实现。 如果需要自定义此逻辑以满足项目特定的要求，可使用Sling模型的委派模式。

>[!TIP]
>
>[自定义AEM CIF核心组件](../customizing/customize-cif-components.md)页中有一个详细的示例和最佳做法，介绍如何自定义CIF核心组件。

在项目中，AEM CIF核心组件和自定义项目组件可以通过Sling上下文感知配置轻松检索为与AEM页面关联的Adobe商务商店配置的客户端。
