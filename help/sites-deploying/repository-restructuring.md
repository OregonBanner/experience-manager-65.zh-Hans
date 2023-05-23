---
title: AEM 6.5中的存放庫重組
seo-title: Repository Restructuring in AEM 6.5
description: 瞭解AEM 6.5中存放庫重組的基礎知識和推理
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# AEM 6.5中的存放庫重組{#repository-restructuring-in-aem}

## 简介 {#introduction}

在AEM 6.4之前，客戶程式碼部署在JCR不可預測的區域，這些區域在升級時可能會變更。 因此，正式AEM發行版本通常會覆寫自訂程式碼、設定或內容。 此外，客戶變更有時會覆寫AEM產品程式碼或內容，破壞產品功能。

透過清楚界定AEM產品程式碼和客戶程式碼的階層，可以避免這些衝突。

為此，從AEM 6.4開始，並在未來版本中繼續，內容正在從/etc重新構建到存放庫中的其他資料夾，以及關於內容去向的准則，遵守以下高級規則：

* AEM產品程式碼一律會放在/libs中，自訂程式碼不可加以覆寫
* 自訂程式碼應放在/apps、/content和/conf中

## 對6.5升級的影響 {#impact-on-upgrades}

升級至AEM 6.5時，/etc底下內容的大量子集將會在存放庫的其他資料夾中重複。 這些新位置是參照內容的偏好位置。 不過，為了能夠回溯相容於/etc資料夾中先前的位置，AEM 6.5升級的所有嘗試都已進行，因此在大多數情況下，AEM程式碼將繼續參考舊位置，直到在客戶的應用程式中主動變更（且多數情況下是手動變更）為止。 從時間軸的角度來看，變更分為兩類：

* 升級至6.5 — 少數/etc重組變更無法回溯相容，因此應規劃修改，並在AEM 6.5升級中實作。
* 在未來的升級之前 — 大部分/etc重組變更可以延遲到未來的升級後的一段時間。 如先前所述，AEM 6.5程式碼將繼續參考舊位置，直到修改在客戶版本中實作為止。 雖然沒有應進行變更的強制時間表，但建議在將來的升級之前進行這些變更，因為未來的功能可能會依賴所參考的新位置。 此外，根據慣例，指定功能的檔案將參照新位置，因此，如果仍在使用舊位置，可能會造成混淆。

### 重組指南 {#restructuring-guidance}

在規劃升級至AEM 6.5時，應參考以下每個解決方案的頁面，以評估工作量：

* [所有AEM解決方案通用的存放庫重組](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [AEM Sites存放庫重組](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [AEM Assets存放庫重組](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [AEM Assets Dynamic Media存放庫重組](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [AEM Forms存放庫重組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [AEM Communities存放庫重組](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM Commerce存放庫重組](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

每個頁面都包含兩個區段，分別對應於必要變更的緊急程度。 「含6.5升級」區段下的任何專案都應在AEM 6.5升級專案中處理。 「未來升級之前」下的任何專案都可選擇延遲到升級後。

頁面上的每個專案都包含「重組指引」欄位，該欄位詳細說明了建議的技術策略，以便與新的6.5存放庫模型保持一致，從而為先前位於/etc資料夾下的內容引用新位置。 額外的「附註」欄位可提供任何其他有用的內容。
