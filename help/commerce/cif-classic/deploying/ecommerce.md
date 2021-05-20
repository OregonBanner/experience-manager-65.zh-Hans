---
title: 电子商务概述
seo-title: 电子商务概述
description: AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。
seo-description: AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: 商务集成框架
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 7%

---

# 电子商务概述{#ecommerce-overview}

AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。

Adobe提供了商务集成框架的两个版本：

|  | CIF上线 | CIF云 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | AEM on-prem或AMS 6.x | AEM AMS 6.4和6.5 |
| 后端 | - AEM、Java <br> — 整体集成、预构建映射（模板）<br> - JCR存储库 | -Magento<br>- Java和Javascript <br> — 无商务数据存储在JCR存储库中 |
| 前端 | AEM服务器端渲染的页面 | 混合页面应用程序（混合渲染） |
| 产品目录 | - AEM <br>中的产品导入器、编辑器、缓存 — 具有AEM或代理页面的常规目录 |  — 无产品导入<br> — 通用模板<br> — 通过连接器按需数据 |
| 可扩展性 |  — 最多可支持数百万种产品（取决于用例）<br> - Dispatcher上的缓存 |  — 无卷限制<br> - Dispatcher或CDN上的缓存 |
| 标准化数据模型 | 否 | 是，MagentoGraphQL架构 |
| 可用性 | 是：<br> - SAPCommerce Cloud(扩展已更新以支持AEM 6.4和Hybris 5（默认），并维护与Hybris 4 <br> - SalesforceCommerce Cloud(连接器开源支持AEM 6.4)的兼容性 | 是，可通过GitHub通过开源。 <br> Magento Commerce(支持Magento2.3.2（默认）并与Magento2.3.1兼容)。 |
| 何时使用 | 有限用例：对于可能需要导入小型静态目录的情况 | 大多数用例中的首选解决方案 |


## 部署其他实施{#deploying-other-implementations}

有关AEM和Magento，请参阅使用[商务集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)的[AEM和Magento集成](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)。

>[!NOTE]
>
>有关概念和管理电子商务实施的信息，请参阅[管理电子商务](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>有关扩展电子商务功能的信息，请参阅[开发电子商务](/help/commerce/cif-classic/developing/ecommerce.md)。

