---
title: 電子商務概觀
seo-title: eCommerce Overview
description: AEM通用電子商務是標準安裝的一部分，為您提供電子商務框架的完整功能。
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# 電子商務概觀{#ecommerce-overview}

AEM通用電子商務是標準安裝的一部分，為您提供電子商務框架的完整功能。

Adobe提供兩個版本的Commerce Integration Framework：

|  | CIF內部部署 | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | AEM內部部署或AMS 6.x | AEM AMS 6.4和6.5 |
| 後端 | - AEM、Java <br>  — 整體整合，建置前對應（範本）<br> - JCR存放庫 | - ADOBE COMMERCE <br>- Java和Javascript <br>- JCR存放庫中不會儲存任何Commerce資料 |
| 前端 | AEM伺服器端轉譯頁面 | 混合頁面應用程式（混合呈現） |
| 產品目錄 |  — 產品匯入工具、編輯器、AEM中的快取 <br> — 具有AEM或Proxy頁面的一般目錄 |  — 無產品匯入 <br> — 一般範本 <br> — 透過聯結器的隨選資料 |
| 擴充性 |  — 最多可支援數百萬種產品（視使用案例而定） <br> - Dispatcher上的快取 |  — 無音量限制 <br>- Dispatcher或CDN上的快取 |
| 標準化資料模型 | 否 | 是，Adobe Commerce GraphQL結構描述 |
| 可用性 | 是：<br> - SAPCommerce Cloud(擴充功能已更新，以支援AEM 6.4和Hybris 5 （預設），並保持與Hybris 4的相容性 <br>- SalesforceCommerce Cloud(以支援AEM 6.4為開放來源的聯結器) | 是，透過GitHub的開放原始碼。 <br> Adobe Commerce (支援2.3.2 （預設）並與2.3.1相容)。 |
| 何时使用 | 有限的使用案例：適用於可能需要匯入小型靜態目錄的情況 | 大多數使用案例中偏好的解決方案 |


## 部署其他實作 {#deploying-other-implementations}

若為AEM和Adobe Commerce，請參閱 [AEM與Adobe Commerce整合](/help/commerce/cif/integrating/magento.md) 使用 [Commerce整合框架](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>如需有關概念和管理電子商務實作的資訊，請參閱 [管理電子商務](/help/commerce/cif-classic/administering/ecommerce.md).
>
>如需擴充電子商務功能的相關資訊，請參閱 [開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md).
