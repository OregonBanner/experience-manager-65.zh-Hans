---
title: 電子商務整合框架
description: AEM eCommerce可協助行銷人員跨網路、行動及社交接觸點，提供品牌和個人化的購物體驗。
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 2%

---

# 电子商务{#ecommerce}

* [概念](/help/commerce/cif-classic/administering/concepts.md)
* [管理（一般）](/help/commerce/cif-classic/administering/generic.md)

Adobe提供兩個版本的Commerce Integration Framework：

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF內部部署</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>支持的 AEM 版本</p> </td>
   <td><p>AEM內部部署或AMS 6.x</p> </td>
   <td>AEM AMS 6.4和6.5</td>
  </tr>
  <tr>
   <td><p>後端</p> </td>
   <td>
    <ul>
     <li>AEM， Java</li>
     <li>整體整合、建置前對應（範本）</li>
     <li>JCR存放庫</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java和Javascript</li>
     <li>JCR存放庫中未儲存商業資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>前端</p> </td>
   <td><p>AEM伺服器端轉譯頁面</p> </td>
   <td>混合頁面應用程式（混合呈現）</td>
  </tr>
  <tr>
   <td><p>產品目錄</p> </td>
   <td>
    <ul>
     <li>產品匯入工具、編輯器、AEM中的快取</li>
     <li>具有AEM或Proxy頁面的一般目錄</li>
    </ul> </td>
   <td>
    <ul>
     <li>無產品匯入</li>
     <li>通用範本</li>
     <li>透過聯結器的隨選資料</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>擴充性</p> </td>
   <td>
    <ul>
     <li>最多可支援數百萬種產品（視使用案例而定）</li>
     <li>Dispatcher上的快取</li>
    </ul> </td>
   <td>
    <ul>
     <li>無音量限制</li>
     <li>Dispatcher或CDN上的快取</li>
    </ul> </td>
  </tr>
  <tr>
   <td>標準化資料模型</td>
   <td>否</td>
   <td>是，Adobe Commerce GraphQL結構描述</td>
  </tr>
  <tr>
   <td>可用性</td>
   <td><p>是。SAPCommerce Cloud(擴充功能已更新，以支援AEM 6.4和Hybris 5 （預設），並保持與Hybris 4的相容性</p> <p>SalesforceCommerce Cloud(開放來源以支援AEM 6.4的聯結器)</p> </td>
   <td>是，透過GitHub的開放原始碼。 Adobe Commerce (支援2.3.2 （預設）並與2.3.1相容)。</td>
  </tr>
  <tr>
   <td>何时使用</td>
   <td>有限的使用案例：適用於可能需要匯入小型靜態目錄的情況</td>
   <td>大多數使用案例中偏好的解決方案</td>
  </tr>
 </tbody>
</table>

電子商務與產品資訊管理(PIM)一起，透過線上商店處理專注於銷售產品的網站活動：

* 產品的建立、期限和淘汰
* 價格管理
* 交易管理
* 管理整個目錄
* 即時和集中式儲存記錄
* 網頁介面

AEM eCommerce可協助行銷人員跨網路、行動及社交接觸點，提供品牌和個人化的購物體驗。 AEM製作環境可讓您根據目標訪客內容和銷售策略來自訂頁面和元件；例如：

* 产品页面
* 購物車元件
* 簽出元件

實作可讓您即時存取產品資訊。 這可用來強制執行：

* 產品資訊完整性
* 定價
* 庫存管理
* 購物車狀態的變化

>[!NOTE]
>
>若要與外部電子商務提供者使用整合架構，您首先需要安裝所需的套件。 如需詳細資訊，請參閱 [部署電子商務](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>如需擴充電子商務功能的相關資訊，請參閱 [開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md).

## 主要功能 {#main-features}

AEM eCommerce提供：

* 數量 **現成可用的AEM元件** 若要說明專案可達成的目的：

   * 產品顯示
   * 購物車
   * 簽出
   * 最近檢視的產品
   * 优惠券
   * 和其他

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >AEM提供的整合架構也可讓您為商業功能建立其他AEM元件，不受特定電子商務引擎影響。

* **搜尋**  — 使用：

   * AEM搜尋
   * 電子商務系統的搜尋
   * 第三方搜尋
   * 或兩者的組合。

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* 使用AEM功能來 **在多個管道上顯示您的內容**、完整瀏覽器視窗或行動裝置。 如此一來，您的內容就會以訪客所需的格式傳送。

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* 能夠 **根據以下專案開發您自己的整合實作： [AEM電子商務架構](#the-framework)**.

   目前可用的兩個實作都是以相同的基礎建置 — 在一般API （框架）之上。 實作新整合只需要實作您整合所需的功能。 前端元件可供任何新實施使用，因為它們使用介面（因此獨立於實施）。

* 開發的可能性 **根據購物者資料和活動的體驗導向型商務**. 這可讓您實現許多情境：

   * 例如，當訂單總額超過特定金額時，可減少運費。
   * 另一種方式可讓您提供使用設定檔資料的季節性優惠方案（例如位置）。 然後可反白這些內容，同樣視需要根據其他因素而定。

   在以下範例中，當購物車的內容少於$75美元時，顯示了一個Teaser：

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   當購物車內容超過$75美元時，可以變更此設定：

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* 和其他功能包括：

   * 跨工作階段保留的購物車內容
   * 完整訂單歷史記錄
   * 快速目錄更新

## 框架 {#the-framework}

此 [概念](/help/commerce/cif-classic/administering/concepts.md) 一節會更詳細地涵蓋架構，但下列內容提供架構的高階高速檢視：

### 什麼？ {#what}

* 整合框架提供API、一系列元件來說明功能，而數個擴充功能則提供連線方法的範例。
* 此架構提供專案實作所需的基本結構。
* 此框架可擴充。
* 此架構不提供立即可用網站。 一律需要一定的開發工作，才能讓架構符合您的規格。

### 为什么？ {#why}

* 提供快速實現自訂電子商務網站所需的基本機制。
* Tp提供開發實際電子商務網站所需的彈性。
* 說明最佳做法。
