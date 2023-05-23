---
title: 延遲內容移轉
seo-title: Lazy Content Migration
description: 瞭解AEM 6.4中的延遲內容移轉。
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# 延遲內容移轉 {#lazy-content-migration}

為了回溯相容性，中的內容和設定 **/etc** 和 **/content** 從AEM 6.3開始，升級後不會立即觸及或轉換。 這麼做是為了確保客戶應用程式對這些結構的相依性保持不變。 即使現成可用的AEM 6.5中的內容會託管在其他位置，與這些內容結構相關的功能仍相同。

雖然並非所有這些位置都可自動轉換，但有一些延遲 `CodeUpgradeTasks` 也稱為「延遲內容移轉」。 這可讓客戶透過使用此系統屬性重新啟動執行個體，以觸發這些自動轉換：

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

這將導致 `CodeUpgradeTasks` 將在移轉期間執行。

雖然目標是有效率地執行，但此升級程式是同步的，因此會根據需要處理的內容量而產生停機。 建議在生產系統之前評估中繼環境中的執行時間，以計畫相應的維護時段。

由於這通常也需要調整應用程式，此活動應該與對應的應用程式部署一起執行。

以下為完整清單 `CodeUpgradeTasks` 6.5引入：

| **名称** | **相關** **適用於以下版本之前的AEM** | **移轉** **型別** | **详细信息** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即时 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即时 | 偵測全部 `LiveRelationShips` 從 `VersionStorage` 已刪除，並將排除屬性新增至父項 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即时 | 根據預設設定，重新建構cloudservices以提供安全性 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即时 | 從移除屬性型連結 **/content** 至 **/conf** （由OSGi機製取代），產生對應的OSGi設定 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即时 | 由於merge_preserve處理安全（預設）拒絕規則會覆寫指定的許可權，導致升級時需要重新排序 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即时 | 利用Html5SmartFile Widget偵測元件、搜尋元件在內容中的使用情況並重新建構持續性、有效地將二進位檔案下移一層，而不是儲存在元件層級。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即时 | 移動舊樣式專案 **/etc/projects** 至 **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即时 | 將容器圖層引入階層（「區域」）並調整參照。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即时 | 設定目標元件的固定位置名稱。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即时 | 工作流程模型的複雜轉換可追溯至6.2結構、例項、通知，然後從備份位置合併回來 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即时 | 從以下位置移動資產、自訂中繼資料結構描述和處理設定檔： **/apps** 至 **/conf** 和會將中繼資料結構描述和中繼資料設定檔表單從coral2轉譯為coral3。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即时 | 將資產和自訂搜尋Facet從 **/apps** 至 **/conf** 和會將中繼資料結構描述和中繼資料設定檔表單從coral2轉譯為coral3。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即时 | 更新InboxItems以排序收件匣專案（調整中繼資料以有效排序） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即时 | 將相對路徑取代為以調整資料夾的metadataSchema屬性 **/conf** 取代 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即时 | 調整導覽結構 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即时 | 移動監控儀表板的自訂設定 **/libs** 和 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即时 | 轉譯Assets中的processingProfile屬性（直到6.1使用），以符合6.3和更新版本結構。 也會將設定檔的相對路徑調整為 **/conf** 取代 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即时 | 升級工作，移除升級時過時的CRXDE Lite和Web主控台功能表專案。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 已延遲 | 移動SRP雲端設定、社群標語設定、清除 **/etc/social** 和 **/etc/enablement** （執行延遲移轉時，需要調整任何參考資料和資料 — 應用程式部分不應再依賴此結構）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 已延遲 | 清除 **/etc/cloudsettings** （包含ContextHub設定）。 首次存取時自動移轉設定。 萬一延遲內容移轉已開始，同時將此內容升級至 **/etc/cloudsettings** 必須在升級前透過套件保留，並重新安裝才能開始隱含轉換，以及完成後後續解除安裝套件。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 已延遲 | 將舊版標題結構調整為使用者設定檔節點中的標題。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 已延遲 | 從移轉商務內容 **/etc/commerce** 至 **/var/commerce**. 在移轉期間，會移動內容並更新對已移動內容的引用，以反映新位置。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 已延遲 | 從移轉舊版目錄設定和Dynamic MediaCloud Services設定 **/etc** 至 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 已延遲 | 清理下存在的舊版clientlibs **/etc/clientlibs** |
