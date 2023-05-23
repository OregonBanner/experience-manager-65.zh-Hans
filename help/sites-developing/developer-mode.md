---
title: 开发人员模式
seo-title: Developer Mode
description: 開發人員模式會開啟一個側面板，其中包含數個標籤，為開發人員提供有關目前頁面的資訊
seo-description: Developer mode opens a side panel with several tabs that provide a developer with infomation about the current page
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# 开发人员模式{#developer-mode}

在AEM中編輯頁面時，有數個 [模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) 可用，包括開發人員模式。 這會開啟一個側面板，其中包含數個標籤，為開發人員提供有關目前頁面的資訊。 三個標籤為：

* **[元件](#components)** 以檢視結構和效能資訊。
* **[測試](#tests)** 以執行測試和分析結果。
* **[錯誤](#errors)** 檢視發生的任何問題。

這些功能可協助開發人員：

* 探索：組成頁面的專案。
* 偵錯：隨時隨地發生的狀況，進而有助於解決問題。
* 測試：應用程式的行為是否符合預期。

>[!CAUTION]
>
>开发人员架构:
>
>* 僅適用於觸控式UI （編輯頁面時）。
>* 不適用於行動裝置或桌上型電腦上的小型視窗（因為空間限制）。
   >
   >   * 當寬度小於1024畫素時，就會發生這種情況。
>* 僅適用於屬於以下群組的使用者： `administrators` 群組。


>[!CAUTION]
>
>開發人員模式僅適用於未使用nosamplecontent執行模式的標準制作執行個體。
>
>如有需要，可將其設定為使用：
>
>* 在使用nosamplecontent執行模式的作者執行個體上
>* 發佈執行個體
>
>使用後應再次停用。

>[!NOTE]
>
>請參閱：
>
>* 知識庫文章， [疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得進一步的提示和工具。
>* AEM Gems課程關於 [AEM 6.0開發人員模式](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).
>


## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式會實作為頁面編輯器的側面板。 若要開啟面板，請選取 **開發人員** 從頁面編輯器工具列中的模式選取器：

![chlimage_1-11](assets/chlimage_1-11.png)

面板分為兩個標籤：

* **[元件](/help/sites-developing/developer-mode.md#components)**  — 這個選項會顯示元件樹，類似於 [內容樹狀結構](/help/sites-authoring/author-environment-tools.md#content-tree) 作者

* **[錯誤](/help/sites-developing/developer-mode.md#errors)**  — 發生問題時，會顯示每個元件的詳細資料。

### 组件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

這顯示一個元件樹狀結構，其中：

* 概述在頁面上呈現的元件和範本鏈（SLY、JSP等）。 可展開樹狀結構以顯示階層內的前後關聯。
* 顯示轉譯元件所需的伺服器端運算時間。
* 可讓您展開樹狀結構並選取樹狀結構中的特定元件。 選取範圍可讓您存取元件詳細資訊，例如：

   * 存放庫路徑
   * 指令碼連結(以CRXDE Lite存取)

* 選取的元件（在內容流程中，以藍色邊框表示）將在內容樹狀結構中反白顯示（反之亦然）。

這有助於：

* 決定並比較每個元件的演算時間。
* 檢視並瞭解階層。
* 找出緩慢的元件，瞭解並改善頁面載入時間。

每個元件專案可顯示（例如）：

![chlimage_1-13](assets/chlimage_1-13.png)

* **檢視詳細資料**：清單的連結，其中顯示：

   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的存放庫內容路徑。

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **編輯指令碼**：連結：

   * 以CRXDE Lite開啟元件指令碼。

* 展開元件專案（箭頭標頭）也可顯示：

   * 所選元件內的階層。
   * 所選元件的單獨呈現時間、任何巢狀在其中的個別元件以及合併總數。

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>有些連結會指向下的指令碼 `/libs`. 不過，這些僅供參考，您 **不得** 編輯下的任何專案 `/libs`，因為您所做的任何變更都可能遺失。 這是因為每當您升級或套用Hotfix/Feature Pack時，此分支隨時可能變更。 您所需的任何變更都應該在 `/apps`，請參閱 [覆蓋和覆寫](/help/sites-developing/overlays.md).

### 错误 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望 **錯誤** 索引標籤一律為空白（如上所述），但發生問題時，會顯示每個元件的下列詳細資料：

* 如果元件將專案寫入錯誤記錄檔，連同錯誤的詳細資訊以及指向CRXDE Lite內適當程式碼的直接連結，會出現警告。
* 如果元件開啟管理員工作階段，會出現警告。

例如，在呼叫未定義的方法的情況下，產生的錯誤將顯示在 **錯誤** 標籤：

![chlimage_1-17](assets/chlimage_1-17.png)

發生錯誤時，「元件」標籤樹狀結構中的元件專案也會標示一個指示器。

### 测试 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，開發人員模式的測試功能已重新實作為獨立的工具應用程式。
>
>如需完整詳細資訊，請參閱 [測試您的UI](/help/sites-developing/hobbes.md).
