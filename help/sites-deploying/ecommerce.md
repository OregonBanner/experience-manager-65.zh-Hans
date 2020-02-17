---
title: 电子商务概述
seo-title: 电子商务概述
description: AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。
seo-description: AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7

---


# 电子商务概述{#ecommerce-overview}

AEM通用电子商务作为标准安装的一部分提供，并为您提供电子商务框架的完整功能。

Adobe提供两个版本的Commerce Integration Framework:

|  | CIF上印 | CIF云 |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | AEM on-prem或AMS 6.x | AEM AMS 6.4和6.5 |
| 后端 | - AEM、Java <br> -整体集成、预构建映射（模板）<br> - JCR存储库 | - Magento <br>- Java和Javascript <br>- JCR存储库中不存储商务数据 |
| 前端 | AEM服务器端呈现的页面 | 混合页面应用程序（混合渲染） |
| 产品目录 | -产品导入程序、编辑器、AEM中的缓存 <br>-包含AEM或代理页面的常规目录 | -无产品导 <br>入——通用模 <br>板——通过连接器点播数据 |
| 可伸缩性 | -最多可支持几百万种产品（取决于用例） <br> - Dispatcher上的缓存 | -无卷限制 <br>-在Dispatcher或CDN上缓存 |
| 标准化的数据模型 | 否 | 是，Magento GraphQL架构 |
| 可用性 | <br> 是：- SAP Commerce Cloud(Extension updated to support AEM 6.4 and Hybris 5(default)and maintains compatibility with Hybris 4 <br>- Salesforce Commerce Cloud(Connector open-sourced to support AEM 6.4) | 是，通过GitHub通过开放源代码。 <br> Magento Commerce(支持Magento 2.3.2（默认），并与Magento 2.3.1兼容)。 |
| 何时使用 | 有限用例：对于需要导入小型静态目录的情况 | 大多数用例中的首选解决方案 |


## 部署其他实施 {#deploying-other-implementations}

对于AEM和Magento，请使用 [Commerce Integration Framework查看](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) AEM和Magento集 [成](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)。

>[!NOTE]
>
>有关概念和管理电子商务实施的信息，请参 [阅管理电子商务](/help/sites-administering/ecommerce.md)。
>
>有关扩展电子商务功能的信息，请参 [阅开发电子商务](/help/sites-developing/ecommerce.md)。

