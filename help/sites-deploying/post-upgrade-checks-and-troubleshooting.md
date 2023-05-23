---
title: 升級後檢查與疑難排解
seo-title: Post Upgrade Checks and Troubleshooting
description: 瞭解如何疑難排解升級後可能出現的問題。
seo-description: Learn how to troubleshoot issues that might appear after an upgrade.
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
feature: Upgrading
exl-id: ceac2b52-6885-496d-9517-5fc7291ad070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1813'
ht-degree: 0%

---

# 升級後檢查與疑難排解{#post-upgrade-checks-and-troubleshooting}

## 升級後檢查 {#post-upgrade-checks}

遵循 [就地升級](/help/sites-deploying/in-place-upgrade.md) 應執行下列活動以完成升級。 假設AEM已使用6.5 jar啟動，且已部署升級的程式碼基底。

* [驗證升級成功的記錄](#main-pars-header-290365562)

* [驗證OSGi組合](#main-pars-header-1637350649)

* [驗證Oak版本](#main-pars-header-1293049773)

* [Inspect PreUpgradeBackup資料夾](#main-pars-header-988995987)

* [頁面初始驗證](#main-pars-header-20827371)
* [套用AEM Service Pack](#main-pars-header-215142387)

* [移轉AEM功能](#main-pars-header-1434457709)

* [驗證排程的維護設定](#main-pars-header-1552730183)

* [啟用復寫代理](#main-pars-header-823243751)

* [啟用自訂排程工作](#main-pars-header-244535083)

* [執行測試計畫](#main-pars-header-1167972233)

### 驗證升級成功的記錄 {#verify-logs-for-upgrade-success}

**upgrade.log**

過去，檢查執行個體的升級後狀態需要仔細檢查各種記錄檔、存放庫部分和啟動板。 產生升級後報告有助於在升級上線前偵測到瑕疵升級。

此功能的主要目的是減少手動解譯或跨多個端點複雜剖析邏輯的需求，這些是確保升級成功所必需的。 此解決方案旨在為外部自動化系統提供明確資訊，以便在更新成功或識別失敗時做出反應。

更具體地說，這可確保：

* 升級架構偵測到的升級故障可集中於單一升級報告中；
* 升級報告包含有關必要手動介入的指標。

為因應此情況，在中產生記錄的方式已有所變更。 `upgrade.log` 檔案。

以下是升級期間未顯示任何錯誤的範例報告：

![1487887443006](assets/1487887443006.png)

以下是範例報告，其中顯示升級過程中未安裝的套件組合：

![1487887532730](assets/1487887532730.png)

**error.log**

在使用目標版本jar啟動AEM期間和之後，應該仔細檢閱error.log。 應檢閱任何警告或錯誤。 一般來說，最好在記錄的開頭尋找問題。 稍後在記錄檔中發生的錯誤，實際上可能是檔案中較早呼叫的根源的副作用。 如果發生重複錯誤和警告，請參閱以下內容 [分析升級相關問題](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade).

### 驗證OSGi組合 {#verify-osgi-bundles}

導覽至OSGi主控台 `/system/console/bundles` 並檢視是否有任何套件組合未啟動。 如果有任何套件組合處於安裝狀態，請參閱 `error.log` 以判斷根問題。

### 驗證Oak版本 {#verify-oak-version}

升級後，您應該會看到Oak版本已更新至 **1.10.2**. 若要驗證Oak版本，請導覽至OSGi主控台，並檢視與Oak套件組合相關聯的版本：Oak Core、Oak Commons、Oak Segment Tar。

### Inspect PreUpgradeBackup資料夾 {#inspect-preupgradebackup-folder}

在升級期間，AEM會嘗試備份自訂並將它們儲存在下方 `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`. 若要以CRXDE Lite檢視此資料夾，您可能需要 [暫時啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

具有時間戳記的資料夾應具有名為的屬性 `mergeStatus` 具有值 `COMPLETED`. 此 **待處理** 資料夾應為空白，且 **已覆寫** node會指出哪些節點在升級期間被覆寫。 下的內容 **剩餘專案** 節點表示在升級期間無法安全合併的內容。 如果您的實施相依於任何子節點（且尚未由升級後的程式碼套件安裝），則需要手動合併。

如果在預備或生產環境中，請停用此練習後的CRXDE Lite。

### 頁面初始驗證 {#initial-validation-of-pages}

對AEM中的數個頁面執行初始驗證。 如果升級作者環境，請開啟開始頁面和歡迎頁面( `/aem/start.html`， `/libs/cq/core/content/welcome.html`)。 在製作和發佈環境中，會開啟一些應用程式頁面，並進行煙霧測試，確保它們可正確呈現。 如果有任何問題，請參閱 `error.log` 進行疑難排解。

### 套用AEM Service Pack {#apply-aem-service-packs}

套用任何相關的AEM 6.5 Service Pack （如果已經發行）。

### 移轉AEM功能 {#migrate-aem-features}

升級後，AEM中的幾項功能需要額外的步驟。 這些功能及在AEM 6.5中移轉這些功能的步驟的完整清單可在以下網址找到： [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md) 頁面。

### 驗證排程的維護設定 {#verify-scheduled-maintenance-configurations}

#### 啟用資料存放區垃圾收集 {#enable-data-store-garbage-collection}

如果使用檔案資料存放區，請確定已啟用資料存放區垃圾收集工作，並將其新增至每週維護清單。 說明已概述 [此處](/help/sites-administering/data-store-garbage-collection.md).

>[!NOTE]
>
>S3自訂資料存放區安裝或使用共用資料存放區時，不建議使用此選項。

#### 啟用線上修訂清除 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK區段格式，請確定已啟用「修訂清除」任務並將其新增到「每日維護」清單中。 說明概述 [此處](/help/sites-deploying/revision-cleanup.md).

### 執行測試計畫 {#execute-test-plan}

依照定義執行詳細的測試計畫 [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md) 在 **測試程式** 區段。

### 啟用復寫代理 {#enable-replication-agents}

發佈環境完成升級和驗證後，請在製作環境中啟用復寫代理。 確認代理程式能夠連線至個別的發佈執行個體。 參閱U [升級程式](/help/sites-deploying/upgrade-procedure.md) 以取得事件順序的詳細資訊。

### 啟用自訂排程工作 {#enable-custom-scheduled-jobs}

此時可以啟用程式碼庫中的任何排程工作。

## 分析升級相關問題 {#analyzing-issues-with-upgrade}

本節包含升級到AEM 6.3的過程中可能會遇到的一些問題案例。

這些案例應該有助於追蹤與升級相關問題的根本原因，並且應該有助於識別專案或產品特定問題。

### 存放庫移轉失敗  {#repository-migration-failing-}

從CRX2到Oak的資料移轉應該適用於任何以根據CQ 5.4的來源例項開始的情境。請務必確實按照本檔案中的升級指示進行，包括準備 `repository.xml`，確認沒有透過JAAS啟動自訂驗證器，且已在開始移轉前檢查執行個體是否不一致。

如果移轉仍然失敗，您可以透過檢查 `upgrade.log`. 如果問題尚未知，請回報客戶支援。

### 升級未執行 {#the-upgrade-did-not-run}

在開始準備步驟之前，請務必執行 **source** 先使用java -jar aem-quickstart.jar命令執行執行個體。 這是必要的，才能確保quickstart.properties檔案已正確產生。 如果遺失，升級將無法運作。 或者，您可以檢視下方，檢查檔案是否存在 `crx-quickstart/conf` 在來源執行個體的安裝資料夾中。 此外，啟動AEM以開始升級時，必須使用java -jar aem-quickstart.jar命令執行。 從啟動指令碼啟動時，AEM不會以升級模式啟動。

### 套件和套件組合無法更新  {#packages-and-bundles-fail-to-update-}

如果在升級期間無法安裝套件，其中包含的套件組合也不會更新。 這類問題通常是由資料存放區設定錯誤所造成。 它們也會顯示為 **錯誤** 和 **警告** error.log中的訊息。 由於多數情況下預設登入可能無法運作，因此您可以直接使用CRXDE來檢查並尋找設定問題。

### 部分AEM套件組合未切換至作用中狀態 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果套件組合未啟動，您應該檢查是否有任何未滿足的相依性。

如果出現此問題，但此問題的基礎是失敗的套件安裝，導致套件組合無法升級，則視為與新版本不相容。 如需疑難排解此問題的詳細資訊，請參閱 **套件和套件組合無法更新** 以上。

此外，也建議將全新AEM 6.5執行個體的套件組合清單與升級後的套件組合清單進行比較，以偵測未升級的套件組合。 這將提供更密切範圍來搜尋以下專案： `error.log`.

### 自訂套件組合未切換至作用中狀態 {#custom-bundles-not-switching-to-the-active-state}

如果您的自訂套件組合未切換至使用中狀態，很可能是因為有程式碼未匯入變更API。 這通常會導致不滿意的相依性。

移除的API應在先前的其中一個版本中標籤為已過時。 您可以在此淘汰通知中找到直接移轉程式碼的相關指示。 Adobe旨在儘可能進行語意版本設定，以便版本可指出重大變更。

另外，最好檢查造成問題的變更是否絕對必要，如果不是，則加以回覆。 此外，在嚴格的語意版本設定後，檢查套件匯出的版本增加是否超過必要。

### 運作不良的平台UI {#malfunctioning-platform-ui}

若某些UI功能在升級後無法正常運作，您應該先檢查介面的自訂覆蓋圖。 有些結構可能已變更，覆蓋可能需要更新或過時。

接下來，請檢查是否有任何Javascript錯誤，可以向下追蹤至連結至使用者端程式庫的自訂新增擴充功能。 這同樣適用於可能造成AEM版面問題的自訂CSS。

最後，檢查Javascript可能無法處理的設定錯誤。 不當停用擴充功能時通常會發生這種情況。

### 故障自訂元件、範本或UI擴充功能 {#malfunctioning-custom-components-templates-or-ui-extensions}

在大多數情況下，這些問題的根本原因與未啟動的套件組合或套件未安裝的套件相同，只是第一次使用元件時問題開始發生。

處理錯誤自訂程式碼的方法是先執行煙霧測試，以找出原因。 找到後，請檢視下列建議 [連結] 章節，以瞭解修正方法。

### /etc下缺少自訂 {#missing-customizations-under-etc}

`/apps` 和 `/libs` 已順利由升級處理，但變更位於 `/etc` 可能需要從手動還原 `/var/upgrade/PreUpgradeBackup` 升級之後。 請務必檢查此位置，找出任何需要手動合併的內容。

### 正在分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多數情況下，需要查閱記錄檔中的錯誤，以找出問題的原因。 不過，升級時也需要監控相依性問題，因為舊套件組合可能未正確升級。

最佳方法是移除error.log，移除所有預期與您面臨的問題無關的訊息。 您可以透過grep等工具使用下列工具執行此操作：

```shell
grep -v UnrelatedErrorString
```

有些錯誤訊息可能不會立即明確。 在此情況下，檢視發生錯誤的前後關聯也有助於瞭解錯誤的建立位置。 您可以使用以下專案來區隔錯誤：

* `grep -B` 用於在錯誤之前新增行；

或

* `grep -A` 用於在後面新增行。

在少數情況下，錯誤也可能會找到WARN訊息，因為可能存在導致此狀態的有效案例，而應用程式並不總是能夠判斷這是否為實際錯誤。 也請務必參閱這些訊息。

### 联系 Adobe 支持 {#contacting-adobe-support}

如果您詳閱過本頁面上的建議，但仍遇到問題，請聯絡Adobe支援。 為了向處理您案例的支援工程師提供儘可能多的資訊，請務必加入升級中的upgrade.log檔案。
