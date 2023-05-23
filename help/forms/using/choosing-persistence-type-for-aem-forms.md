---
title: 為AEM Forms安裝選擇持續性型別
seo-title: Choosing a persistence type for an AEM Forms installation
description: 明智地選擇持續性型別。 它可協助您建立有效率且可擴充的AEM Forms環境。
seo-description: Choose a persistence type wisely. It helps you build an efficient and scale able AEM Forms environment.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# 為AEM Forms安裝選擇持續性型別 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地選擇持續性型別。 它可協助您建立有效率且可擴充的AEM Forms環境。

持續性是在實體儲存裝置上儲存內容的方法。 它會定義資料的實際資料結構和儲存機制。 MicroKernels在AEM Forms中擔任持續性管理員。 AEM Forms支援TarMK、MongoMK和RDBMK型別的持續性（微核心）。 您可以根據AEM Forms執行個體的用途和部署型別（單一伺服器、陣列或叢集），為AEM Forms選擇持續性型別。

>[!NOTE]
>
>LiveCycleES4 SP1使用TarPM持續性來儲存內容。

下表列出所有支援的持續性型別以及各種引數，以幫助您為您的環境選擇持續性型別：

<table>
 <tbody>
  <tr>
   <th><strong>安裝型別/成本</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>獨立設定</strong></th>
   <td>支持<br /> </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>叢集設定</strong></th>
   <td>不支持</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>授權成本</strong></th>
   <td>包含在AEM中 </td>
   <td>需要單獨的授權</td>
   <td>需要單獨的授權</td>
  </tr>
 </tbody>
</table>

TarMK是專為效能而設計，而MongoMK和RDBMK則是專為擴充性而設計。 Adobe強烈建議將TarMK設為所有AEM Forms部署案例（製作和發佈執行個體均適用）的預設持續性技術，但一節中概述的使用案例除外 [選擇Mongo或TarMK上的關聯式資料庫微核心](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

如需支援的微核心清單，請參閱 [AEM Forms on OSGi技術要求](/help/sites-deploying/technical-requirements.md) 或 [JEE支援的AEM Forms平台組合](/help/forms/using/aem-forms-jee-supported-platforms.md) 文章。

## 選擇Mongo或TarMK上的關聯式資料庫微核心 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可擴充（叢集）的AEM Forms環境是由兩個或多個水準設定的作用中製作執行個體所組成。 如果支援所有同時編寫活動的單一伺服器無法再持續運作，您可以選擇執行多個編寫執行個體。

JEE環境的可擴充（叢集） AEM Forms僅支援MongoMK和RDBMK持續性型別。 伺服器數量或可擴充環境的大小因每次安裝而異。 如需考量事項和範例的清單，請參閱 [建議的部署](/help/sites-deploying/recommended-deploys.md) 和或 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md) 文章。 您也可以聯絡AEM Forms支援，以取得有關使用RDBMK和TarMK的AEM Forms容量規劃的詳細資訊。
