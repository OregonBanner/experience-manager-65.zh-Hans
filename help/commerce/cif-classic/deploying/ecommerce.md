---
title: 电子商务概述
seo-title: eCommerce Overview
description: AEM通用电子商务作为标准安装的一部分提供，它为您提供了电子商务框架的完整功能。
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# 电子商务概述{#ecommerce-overview}

AEM通用电子商务作为标准安装的一部分提供，它为您提供了电子商务框架的完整功能。

Adobe提供了两个版本的Commerce Integration Framework：

|                         | CIF内部部署 | CIF云 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | 内部部署AEM或AMS 6.x | AEM AMS 6.4和6.5 |
| 后端 | - AEM、Java <br>  — 整体集成，预构建映射（模板）<br> - JCR存储库 | - ADOBE COMMERCE <br>- Java和JavaScript <br>- JCR存储库中未存储任何Commerce数据 |
| 前端 | AEM服务器端渲染的页面 | 混合页面应用程序（混合渲染） |
| 产品目录 |  — 产品导入器、编辑器、AEM中的缓存 <br> — 包含AEM或代理页面的常规目录 |  — 无产品导入 <br> — 通用模板 <br> — 通过连接器按需提供数据 |
| 可扩展性 |  — 最多可支持数百万个产品（取决于用例） <br> - Dispatcher上的缓存 |  — 无音量限制 <br> — 在Dispatcher或CDN上缓存 |
| 标准化数据模型 | 否 | 是，Adobe Commerce GraphQL架构 |
| 可用性 | 是：<br> - SAPCommerce Cloud(扩展已更新，可支持AEM 6.4和Hybris 5 （默认），并保持与Hybris 4的兼容性 <br>- SalesforceCommerce Cloud(支持AEM 6.4的开放源连接器) | 通过GitHub的开源提供。 <br> Adobe Commerce (支持2.3.2（默认）并与2.3.1兼容)。 |
| 何时使用 | 有限用例：适用于可能需要导入小型静态目录的情况 | 大多数用例中的首选解决方案 |


## 部署其他实施 {#deploying-other-implementations}

对于AEM和Adobe Commerce，请参阅 [AEM与Adobe Commerce集成](/help/commerce/cif/integrating/magento.md) 使用 [Commerce集成框架](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>有关概念和管理电子商务实施的信息，请参阅 [管理电子商务](/help/commerce/cif-classic/administering/ecommerce.md).
>
>有关扩展电子商务功能的信息，请参阅 [发展电子商务](/help/commerce/cif-classic/developing/ecommerce.md).
