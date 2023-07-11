---
title: 使用Commerce Integration Framework进行AEM和第三方商务集成
description: 企业可能需要其他第三方商业解决方案来强化其店面。 Commerce Integration Framework (CIF)可用于此类集成方案，以使用I/O运行时将第三方商业解决方案连接到Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# 使用Commerce Integration Framework进行AEM和第三方商务集成 {#aem-third-party}

非Adobe Commerce解决方案的集成是CIF的常见场景。 通过集成层连接具有不同API和架构的第三方解决方案。

## 架构 {#architecture}

整体架构如下：

![AEM非Magento/第三方架构概述](../assets//AEM_nonMagento_Architecture.png)

此集成层的目的是根据Experience Manager外部支持的Adobe Commerce GraphQL API和架构映射第三方API和架构。 借助这种封装，集成逻辑和系统可以在不更改Experience Manager内部代码的情况下进行更新。

## 集成的解决方案要求

在Experience Manager按需检索数据时，需要产品目录的实时API。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例 [Magento开源](https://business.adobe.com/products/magento/open-source.html).

无需实施完整的GraphQL架构，只需实施架构的对象即可启用所需的用例。

## 后端用例

CIF通过实时产品目录访问和产品体验管理工具扩展了Experience Manager。 这种无缝集成使作者能够在需要时随时使用嵌入式UI访问商务数据，而无需离开内容上下文。

需要集成产品目录API才能解锁这些用例。

## 前端用例

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 通过支持的CIF Adobe Commerce API检索和交换数据。 要重用组件，必须实施相应的API。

对性能关键的客户端组件的建议是直接与第三方解决方案通信以避免延迟。

## 开发集成 {#develop-integration}

Adobe建议使用 [Adobe I/O Runtime](https://developer.adobe.com/apis/experienceplatform/runtime.html) 用于集成层。 它包含在第三方的CIF加载项中。 由于它可与类似微服务的方法配合使用，因此非常适合轻松集成多个解决方案。

此 [参考实现](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是构建与商业解决方案集成的绝佳起点。 尽管它支持GraphQL，但它也可以与其他任何类型的API（如REST）集成。

如果第三方层可用（例如Mulesoft），或者集成基于第三方解决方案构建，则不需要此集成层。

## 预建连接器 {#connectors}

连接器为项目提供了一个良好的开端。 它们附带商业解决方案特定的连接和默认API映射。 这些连接器由第三方构建，不由Adobe维护。 有关信息，请与相应的合作伙伴联系。

* [SAP商务](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由Diconium构建
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由Diconium构建

>[!TIP]
>
>虽然连接器可帮助项目加快商业集成，但它们并非即插即用。 企业商务解决方案经过高度自定义，需要自定义集成。 需要很好地了解Commerce平台、Adobe Commerce GraphQL架构和Adobe I/O Runtime。
