---
title: 同步應用程式
seo-title: Synchronizing the app
description: 將行動裝置上的AEM Forms應用程式與AEM Forms伺服器同步。
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 同步應用程式{#synchronizing-the-app}

## 同步應用程式 {#synchronizing-the-app-1}

應用程式中的表單會從AEM Forms伺服器下載。 表單下載至「任務」和「Forms」標籤下方。 從表單建立的草稿會下載到草稿索引標籤中，而從任務建立的草稿則會下載到任務索引標籤中。 若為OSGi伺服器上的獨立表單，表單和草稿會分別在Forms和草稿索引標籤中下載。

完成並提交表單後，如果應用程式上線，表單會立即上傳回AEM Forms伺服器。 應用程式同步處理時，會從伺服器擷取表單。 不過，如果應用程式上線，草稿會立即與伺服器同步。

使用AEM Forms伺服器上線時，應用程式預設會每15分鐘同步處理一次。 不過，您可以選擇變更同步化頻率。 或者，您也可以隨時手動同步應用程式。

**手動同步應用程式**

點選「同步」按鈕 ![同步應用程式](assets/sync-app.png) 位於首頁畫面的右下角。

**變更同步處理頻率**

1. 若要移至「設定」畫面，請點選「首頁」畫面左上角的功能表按鈕，然後點選 **設定**.
1. 在「設定」畫面中，點選「一般」標籤。

   ![「一般設定」視窗中的同步頻率設定](assets/gen-settings-2.png)

1. 在「同步頻率」選項上，點選「同步頻率」右邊的值。
1. 在下拉式清單中，選取新的同步化頻率。

### 技術規格 {#technical-specifications}

* 將離線應用程式資料提交至AEM Forms伺服器的主要邏輯包含在runtime/offline/util/offline.js中。
* 在.js中，對processOfflineSubmittedSavedTasks(...)函式的呼叫會將已儲存/已提交的工作傳送至伺服器。 它也會處理同步處理過程中的任何錯誤或衝突。 如果任務提交失敗，應用程式上的任務會標示為失敗。 此外，任務仍會保留在寄件匣中。
* syncSubmittedTask()和syncSavedTask()函式會針對個別工作執行作業。
* 在使用者選擇同步處理伺服器的離線狀態或背景執行緒自動同步之後，工作清單元件會起始對processOfflineSubmittedSavedTasks()函式的呼叫。
