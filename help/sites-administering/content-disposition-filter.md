---
title: 內容處置篩選
seo-title: Content Disposition Filter
description: 瞭解如何使用內容處置篩選器來防止XSS攻擊。
seo-description: Learn how to use the Content Disposition Filter to prevent XSS attacks.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 內容處置篩選 {#content-disposition-filter}

內容處置篩選器是抵禦SVG檔案XSS攻擊的安全功能。

安裝後，篩選器會封鎖對所有資產的存取。 例如，您無法線上上檢視PDF。 本節說明如何根據您的需求設定篩選器。

## 設定內容處置篩選 {#configure-content-disposition-filter}

您可以檢視 [GitHub中的Apache Sling內容處置篩選器](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

「內容處置篩選」選項提供下列功能：

* **內容處置路徑：** 將套用篩選的路徑清單，後跟在該路徑上要排除的mime型別清單。此路徑必須是絕對路徑，並且可以包含萬用字元(`*`)結尾處的「 」，以將每個資源路徑與給定的路徑前置詞相符。 例如： `/content/*:image/jpeg,image/svg+xml` 會將篩選器套用至中的每個節點 `/content?` jpg和svg影像除外

* **排除的資源路徑：** 排除的資源的清單，每個資源路徑都必須提供為絕對和完整路徑。 不支援字首比對/萬用字元。

* **為所有資源路徑啟用：** 此旗標可控制是否針對所有路徑（排除的資源路徑所定義的排除路徑除外）啟用此篩選。 將此項設為「true」會導致忽略內容處置路徑。 與設定無關，只涵蓋包含下列屬性的資源路徑： `jcr:data` 或 `jcr:content/jcr:data`.
