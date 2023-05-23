---
title: 連結檢查程式
description: 連結檢查器可協助驗證內部和外部連結，並允許連結重寫。
exl-id: 8ec4c399-b192-46fd-be77-3f49b83ce711
source-git-commit: 0b9de3261d8747f3e7107962b6aea1dbdf9d6773
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# 連結檢查程式 {#the-link-checker}

內容作者不必自行驗證其內容頁面所包含的每個連結。

連結檢查器會自動執行，以協助內容作者使用其連結，包括：

* 在新增至內容時驗證連結
* 顯示內容中所有外部連結的清單
* 執行連結轉換

連結檢查器有許多 [設定選項](#configuring) 例如定義驗證內部、允許驗證中省略某些連結或連結模式，以及重寫連結重寫規則。

連結檢查器會驗證兩者 [內部連結](#internal) 和 [外部連結。](#external)

>[!NOTE]
>
>由於「連結檢查器」會檢查每個內容頁面的連結，因此「連結檢查器」可能會影響大型存放庫的效能。 在這種情況下，您可能需要 [設定連結檢查器的執行頻率](#configuring) 或 [停用它。](#disabling)

## 內部連結檢查 {#internal}

內部連結是指向AEM存放庫中其他內容的連結。 可以使用RTE的路徑選擇器或使用自訂元件來新增內部連結。 例如：

* 您的頁面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含連結 `/content/wknd/us/en/adventures/extreme-ironing.html` 在 [文字元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

內容作者新增內部連結至頁面時，就會驗證內部連結。 如果連結無效：

* 它會從發行者中移除。 連結的文字會保留，但連結本身會移除。
* 在製作介面中會顯示為中斷連結。

![編寫頁面時中斷的內部連結](assets/link-checker-invalid-link-internal.png)

## 外部連結檢查 {#external}

外部連結是指向AEM存放庫外部內容的連結。 可以使用RTE或使用自訂元件來新增外部連結。 例如：

* 您的頁面 `/content/wknd/us/en/adventures/ski-touring.html`
* 包含連結 `https://bunwarmerthermalunderwear.com` 在 [文字元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html)

外部連結的語法及可用性會經過驗證。 此檢查會在可設定的內部以非同步方式完成。 如果連結檢查器發現外部連結無效：

* 它會從發行者中移除。 連結的文字會保留，但連結本身會移除。
* 在製作介面中會顯示為中斷連結。

![編寫頁面時中斷的內部連結](assets/link-checker-invalid-link-external.png)

此外， [外部連結檢查程式](#external-link-checker) 介面會提供內容頁面上所有外部連結的概觀。

### 使用外部連結檢查程式 {#external-link-checker}

若要使用外部連結檢查器：

1. 使用 **導覽**，選取 **工具**，則 **網站**.
1. 選取 **外部連結檢查程式** 並會顯示所有外部連結的清單。

![外部連結檢查器視窗](assets/external-link-checker.png)

會顯示下列資訊：

* **狀態**  — 連結的驗證狀態，可為下列其中一項：
   * **有效**  — 連結檢查器可存取外部連結
   * **擱置中**  — 外部連結已新增至網站內容，但尚未通過連結檢查器驗證
   * **無效**  — 連結檢查器無法存取外部連結
* **URL**  — 外部連結
* **反向連結**  — 包含外部連結的內容頁面
   * 此僅填入 [若已設定。](#configuring)
* **上次檢查**  — 連結檢查器上次驗證外部連結的時間
   * 檢查連結的頻率 [是可設定的。](#configuring)
* **上次狀態**  — 上次檢查連結時傳回的最後一個HTML狀態代碼，上次檢查外部連結
* **上次可用**  — 連結檢查器上次使用連結後的時間
* **上次存取**  — 自上次在編寫介面中存取具有外部連結的頁面以來的時間

您可以使用連結清單頂端的兩個按鈕來操作視窗的內容：

* **重新整理**  — 重新整理清單的內容
* **Check**  — 檢查清單中選取的個別外部連結

### 外部連結檢查器的運作方式 {#how-it-works}

雖然外在連結檢查器使用簡單，但需仰賴許多服務，並瞭解其運作方式，協助您瞭解如何 [設定連結檢查器](#configuring) 以符合您的需求。

1. 每當內容作者儲存任何頁面的連結時，就會觸發事件處理常式。
1. 事件處理常式會周遊下的所有內容 `/content` 和會檢查新連結或更新連結，並將其新增至連結檢查器的快取。
1. 此 **Day CQ連結檢查器服務** 然後定期執行以檢查快取中的專案是否為有效語法。
1. 然後，語法驗證的連結會出現在 [外部連結檢查程式](#external-link-checker) 視窗。 不過，它們會位於 **擱置中** 州別。
1. 此 **Day CQ連結檢查器任務** 然後定期執行，藉由進行GET呼叫來驗證連結。
1. 此 **Day CQ連結檢查器任務** 然後，會以GET呼叫的結果來更新「外部連結檢查器」視窗中的專案。

## 設定連結檢查器 {#configuring}

「連結檢查程式」可在AEM中自動使用且立即可用。 不過，可以修改許多OSGi設定以變更其行為：

* **Day CQ連結檢查器資訊儲存服務**  — 此服務定義存放庫中Link Checker快取的大小。
* **Day CQ連結檢查器服務**  — 此服務會執行外部連結語法的非同步檢查。 您可以定義檢查期間，以及檢查器會略過哪些型別的連結，還有其他選項。
* **Day CQ連結檢查器任務**  — 此服務會執行外部連結的GET驗證。 它允許間隔的單獨定義，以檢查其他選項中的壞連結和好連結。
* **Day CQ連結檢查器轉換器**  — 允許根據使用者定義的規則集轉換連結。

檢視檔案 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md) 如需如何變更OSGi設定的詳細資訊。

## 停用連結檢查程式 {#disabling}

您可以選擇完全停用「連結檢查器」。 若要這麼做：

1. 開啟OSGi主控台。
1. 編輯 **Day CQ連結檢查器轉換器**
1. 勾選您要停用的選項：
   * **停用檢查**  — 停用連結驗證
   * **停用重新寫入**  — 停用連結轉換

>[!NOTE]
>
>如果您在開始建立內容後停用連結檢查，您仍可能會看到 [外部連結檢查器視窗](#external-link-checker)，但不會再更新。
