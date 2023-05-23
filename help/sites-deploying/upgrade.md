---
title: 升級至AEM 6.5
seo-title: Upgrading to AEM 6.5
description: 瞭解將舊版AEM安裝升級至AEM 6.5的基本知識。
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# 升級至AEM 6.5 {#upgrading-to-aem}

在本節中，我們會介紹AEM安裝升級至AEM 6.5：

* [規劃升級](/help/sites-deploying/upgrade-planning.md)
* [使用模式偵測器評估升級複雜性](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5的回溯相容性](/help/sites-deploying/backward-compatibility.md)

   <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [升級程式](/help/sites-deploying/upgrade-procedure.md)
* [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [執行就地升級](/help/sites-deploying/in-place-upgrade.md)
* [升級後檢查與疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [可持续升级](/help/sites-deploying/sustainable-upgrades.md)
* [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md)

為了更方便參考這些程式中涉及的AEM執行個體，以下辭彙用於這些文章：

* 此 *source* 執行個體是您要升級的AEM執行個體。
* 此 *目標* 執行個體是您要升級到的執行個體。

>[!NOTE]
>
>為了改善升級的可靠性，AEM進行了全面的存放庫重組。 如需如何與新結構對齊的詳細資訊，請參閱 [AEM中的存放庫重組。](/help/sites-deploying/repository-restructuring.md)

## 有什麼改變？ {#what-has-changed}

以下是AEM最後幾個版本中的主要附註變更：

AEM 6.0推出新的Jackrabbit Oak存放庫。 永續性管理員已取代為 [微核心](/help/sites-deploying/platform.md#contentbody_title_4). 從6.1版開始，不再支援CRX2。 需要執行名為crx2oak的移轉工具，才能從5.6.1執行個體移轉CRX2存放庫。 如需詳細資訊，請參閱 [使用CRX2OAK移轉工具](/help/sites-deploying/using-crx2oak.md).

如果要使用Assets Insights且從AEM 6.2之前的版本升級，則必須移轉資產，且透過JMX Bean產生ID。 在我們的內部測試中，TarMK環境上的125K資產在一小時內即完成移轉，但結果可能會有所不同。

6.3推出新的格式 `SegmentNodeStore`，這是TarMK實作的基礎。 如果您從AEM 6.3之前的版本升級，這需要在升級過程中移轉存放庫，包括系統停機。

Adobe工程部門估計約需20分鐘。 請注意，不需要重新索引。 此外，已發行新版crx2oak工具，可與新存放庫格式搭配使用。

**從AEM 6.3升級至AEM 6.5時，不需要進行此移轉。**

已最佳化升級前維護任務，以支援自動化。

crx2oak工具命令列使用方式選項已變更為易於自動化，並支援更多升級路徑。

升級後的檢查也讓自動化變得易用。

修訂版本的定期垃圾收集與資料存放區垃圾收集現在是需要定期執行的例行維護任務。 隨著AEM 6.3的推出，Adobe支援並建議線上修訂清除。 另請參閱 [修訂清除](/help/sites-deploying/revision-cleanup.md) 瞭解如何設定這些工作的相關資訊。

AEM最近推出 [模式偵測器](/help/sites-deploying/pattern-detector.md) 以便在您開始規劃升級時評估升級的複雜性。 6.5也特別強調 [回溯相容性](/help/sites-deploying/backward-compatibility.md) 功能。 最後，最佳作法 [可持續升級](/help/sites-deploying/sustainable-upgrades.md) 也會新增。

如需有關近期AEM版本中其他變更的詳細資訊，請參閱完整發行說明：

* [Adobe Experience Manager 6.5最新Service Pack發行說明](/help/release-notes/release-notes.md)

## 升級概觀 {#upgrade-overview}

升級AEM需要多個步驟，有時需要多個月。 以下概述已提供升級專案中所包含的內容以及本檔案中所包含內容的概述：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升級流程 {#upgrade-overview-1}

下圖擷取整體建議流程，強調升級方法。 請注意我們推出新功能的相關內容。 升級應該從模式偵測器開始(請參閱 [使用模式偵測器評估升級複雜性](/help/sites-deploying/pattern-detector.md))，可讓您根據產生的報告中的模式，決定要採取與AEM 6.4相容的路徑。

6.5非常著重保持所有新功能向後相容，但如果您仍然看到一些向後相容性問題，相容性模式可讓您暫時延遲開發，以保持自訂程式碼與6.5相容。此方法可協助您在升級後立即避免開發工作(請參閱 [AEM 6.5的回溯相容性](/help/sites-deploying/backward-compatibility.md))。

最後，在您的6.5開發週期中，可持續升級下推出的功能(請參閱 [永續升級](/help/sites-deploying/sustainable-upgrades.md))可協助您遵循最佳實務，讓未來的升級更有效率、更順暢。

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
