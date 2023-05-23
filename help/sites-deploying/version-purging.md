---
title: 版本清除
seo-title: Version Purging
description: 本文介紹版本清除的可用選項。
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---

# 版本清除{#version-purging}

在標準安裝中，當您在更新內容後啟動頁面時，AEM會建立新版本的頁面或節點。

>[!NOTE]
>
>如果未進行任何內容變更，您會看到訊息，指出頁面已啟動，但不會建立新版本

您可以應要求使用「 」建立其他版本 **版本設定** 索引標籤。 這些版本會儲存在存放庫中，並可在必要時還原。

這些版本永遠不會清除，因此存放庫大小會隨著時間增長，因此需要管理。

AEM隨附各種機制，協助您管理存放庫：

* 此 [版本管理員](#version-manager)
這可以設定為在建立新版本時清除舊版本。

* 此 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具這是用來監控及維護存放庫的一部分。
它可讓您根據下列引數，介入以移除舊版本的節點或節點階層：

   * 要保留在存放庫中的版本數目上限。
超過此數目時，會移除最舊的版本。

   * 任何版本保留在存放庫中的最長存留期。
當版本的使用期限超過此值時，就會從存放庫中清除該版本。

* 此 [版本清除維護任務](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). 您可以排定「版本永久刪除」維護作業，以自動刪除舊版本。 如此一來，手動使用「版本清除」工具的必要性就降至最低。

>[!CAUTION]
>
>為了最佳化存放庫大小，您應該經常執行版本清除任務。 當流量有限時，應該將任務排程在營業時間以外。

## 版本管理員 {#version-manager}

除了使用清除工具來明確清除之外，您也可以將「版本管理員」設定為在建立新版本時清除舊版本。

若要設定「版本管理員」， [建立設定](/help/sites-deploying/configuring-osgi.md) 適用於：

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下选项可供选择：

* `versionmanager.createVersionOnActivation` （布林值，預設值： true）指定是否要在啟動頁面時建立版本。
除非將復寫代理設定為抑製版本的建立，否則會建立版本，而版本管理員會遵循此設定。
只有當啟動發生在包含的路徑上時，才會建立版本 `versionmanager.ivPaths` （請參閱下文）。

* `versionmanager.ivPaths`(字串[]，預設： `{"/"}`)指定在下列情況下，會在哪一個路徑上隱含建立版本： `versionmanager.createVersionOnActivation` 設為true。

* `versionmanager.purgingEnabled` （布林值，預設值： false）定義在建立新版本時是否啟用清除。

* `versionmanager.purgePaths` (字串[]，預設值： {&quot;/content&quot;})指定建立新版本時清除版本的路徑。

* `versionmanager.maxAgeDays` （int，預設值： 30）在版本清除時，將移除任何早於設定值的版本。 如果值小於1，則不會根據版本的年齡執行清除。

* `versionmanager.maxNumberVersions` （int，預設值5）在版本清除時，任何早於第n個最新版本的版本都會被移除。 如果值小於1，則不會根據版本數執行永久刪除。

* `versionmanager.minNumberVersions` （int，預設0）不論版本保留時間長短，版本數目下限。 如果該值設定為小於1的值，則不會保留版本的最小數量。

>[!NOTE]
>
>不建議在存放庫中保留大量版本。 因此，在設定版本清除操作時，請注意不要從清除中排除太多版本，否則存放庫大小將無法正確最佳化。 如果您因業務需求而保留大量版本，請聯絡Adobe支援以尋找最佳化存放庫大小的替代方法。

### 結合保留選項 {#combining-retention-options}

定義應如何保留哪些版本的選項( `maxAgeDays`， `maxNumberVersions`， `minNumberVersions`)，可根據您的需求進行組合。

例如，定義要保留的版本數目上限和要保留的最舊版本時：

* 设置:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 替換為：

   * 過去60天內製作的10個版本
   * 其中3個版本是在過去30天內建立

* 將表示：

   * 將保留最後3個版本

例如，定義要保留的最大AND最小版本數以及要保留的最舊版本時：

* 设置:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 替換為：

   * 60天前製作的5個版本

* 將表示：

   * 將保留3個版本

## 清除版本工具 {#purge-versions-tool}

此 [清除版本](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 工具用於清除存放庫中節點版本或節點階層。 其主要用途是透過移除舊版本的節點來協助您縮小存放庫的大小。
