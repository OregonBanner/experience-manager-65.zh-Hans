---
title: AEM和第三方商务集成（使用Commerce Integration Framework）
description: 企业可能需要额外的第三方商务解决方案来支持其店面。 Commerce Integration Framework(CIF)可用于此类集成方案，以使用I/O Runtime将第三方商务解决方案连接到Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# AEM和第三方商务集成（使用Commerce Integration Framework {#aem-third-party}）

非Adobe商务解决方案的集成是CIF的常见情况。 具有不同API和模式的第三方解决方案通过集成层连接。

## 架构 {#architecture}

总体架构如下：

![AEM非Magento/第三方架构概述](../assets//AEM_nonMagento_Architecture.png)

此集成层的用途是将第三方API和模式映射到受支持的Adobe Commerce GraphQL API和Experience Manager之外的模式。 借助这种封装，集成逻辑和系统可以更新，而无需更改Experience Manager内的代码。

## 集成的解决方案要求

当Experience Manager检索数据点播时，需要实时API来获取产品目录。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例[Magento开放源](https://magento.com/products/magento-open-source)。

无需实施完整的GraphQL模式，只需模式的对象即可启用所需的用例。

## 后端使用案例

CIF通过实时产品目录访问和产品体验管理工具扩展Experience Manager。 这种无缝集成使作者能够在需要时使用嵌入式UI访问商务数据，而无需离开内容上下文。

解锁这些用例需要集成产品目录API。

## 前端用例

[AEM CIF核心组](https://github.com/adobe/aem-core-cif-components) 件通过CIF支持的Adobe商务API检索和交换数据。要重复使用组件，需要实现相应的API。

性能关键型客户端组件的建议是直接与第三方解决方案通信以避免延迟。

## 开发集成{#develop-integration}

我们建议对集成层使用[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)。 它包括在第三方的CIF附加服务中。 由于它使用微服务类方法，因此非常适合于轻松集成多个解决方案。

[引用实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)是构建与您的商务解决方案集成的绝佳起点。 尽管它支持GraphQL，但也可以与任何其他类型的API（如REST）集成。

如果第三方层可用（例如Mulesoft）或集成构建在第三方解决方案之上，则不需要此集成层。
