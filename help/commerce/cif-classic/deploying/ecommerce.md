---
title: 电子商务概述
description: AEM通用电子商务作为标准安装的一部分提供，它提供了电子商务框架的完整功能。
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 3%

---

# 电子商务概述{#ecommerce-overview}

AEM通用电子商务作为标准安装的一部分提供，它提供了电子商务框架的完整功能。

Adobe提供以下两个版本的Commerce integration framework：

|                         | CIF内部部署 | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | 内部部署AEM或AMS 6.x | AEM AMS 6.4和6.5 |
| 后端 | - AEM、Java <br>  — 整体集成，预建映射（模板）<br> - JCR存储库 | - ADOBE COMMERCE <br>- Java和JavaScript <br>- JCR存储库中未存储Commerce数据 |
| 前端 | AEM服务器端渲染的页面 | 混合页面应用程序（混合渲染） |
| 产品目录 |  — 产品导入器、编辑器、AEM中的缓存 <br> — 包含AEM或代理页面的常规目录 |  — 无产品导入 <br> — 通用模板 <br> — 通过连接器按需提供数据 |
| 可扩展性 |  — 最多可支持数百万个产品（取决于用例） <br> - Dispatcher上的缓存 |  — 无音量限制 <br>- Dispatcher或CDN上的缓存 |
| 标准化数据模型 | 否 | 是，Adobe Commerce GraphQL架构 |
| 可用性 | 是：<br> - SAPCommerce Cloud(扩展已更新，以支持AEM 6.4和Hybris 5 （默认），并保持与Hybris 4的兼容性 <br>- SalesforceCommerce Cloud(支持AEM 6.4的开放源连接器) | 通过GitHub的开源提供。 <br> Adobe Commerce (支持2.3.2（默认）并与2.3.1兼容)。 |
| 何时使用 | 有限用例：适用于可能需要导入小型静态目录的情况 | 大多数用例中的首选解决方案 |


## 部署其他实施 {#deploying-other-implementations}

有关AEM和Adobe Commerce的信息，请参阅 [AEM与Adobe Commerce集成](/help/commerce/cif/integrating/magento.md) 使用 [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>有关概念和管理电子商务实施的信息，请参阅 [管理电子商务](/help/commerce/cif-classic/administering/ecommerce.md).
>
>有关扩展电子商务功能的信息，请参阅 [发展电子商务](/help/commerce/cif-classic/developing/ecommerce.md).
