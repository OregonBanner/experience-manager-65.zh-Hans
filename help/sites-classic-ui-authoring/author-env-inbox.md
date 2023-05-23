---
title: 您的收件箱
description: 您可以從AEM的各個區域接收通知，例如有關工作專案的通知或代表您需要對頁面內容執行的動作的任務。
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 您的收件箱{#your-inbox}

您可以從AEM的各個區域接收通知，例如有關工作專案的通知或代表您需要對頁面內容執行的動作的任務。

您會在兩個收件匣中收到這些通知，收件匣之間會依通知型別進行分隔：

* 下節將說明您可在其中檢視因訂閱而收到之通知的收件匣。
* 有關工作流程專案的專用收件匣的詳情，請參閱 [參與工作流程](/help/sites-classic-ui-authoring/classic-workflows-participating.md) 檔案。

## 檢視您的通知 {#viewing-your-notifications}

若要檢視您的通知：

1. 開啟通知收件匣：在 **網站** 主控台，按一下右上角的「使用者」按鈕並選取 **通知收件匣**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 將會列出您的通知。 您可以視需要執行動作：

   * [訂閱通知](#subscribing-to-notifications)
   * [處理您的通知](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## 訂閱通知 {#subscribing-to-notifications}

若要訂閱通知：

1. 開啟通知收件匣：在 **網站** 主控台，按一下右上角的「使用者」按鈕並選取 **通知收件匣**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 按一下 **設定……** 以開啟設定對話方塊。

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. 選取通知頻道：

   * **收件匣**：通知會顯示在AEM收件匣中。
   * **電子郵件**：通知會以電子郵件傳送至您使用者設定檔中定義的電子郵件地址。

   >[!NOTE]
   >
   >需要設定一些設定，才能透過電子郵件接收通知。 您也可以自訂電子郵件範本，或新增新語言的電子郵件範本。 請參閱 [設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification) 以在AEM中設定電子郵件通知。

1. 選取要通知的頁面動作：

   * 已啟動：頁面已啟動時。
   * 已停用：頁面已停用時。
   * 已刪除（整合）：當頁面已複製刪除時，即複製在頁面上執行的刪除動作時。
刪除或移動頁面時，系統會自動複製刪除動作：在執行刪除動作的來源執行處理上，以及複製代理程式定義的目的地執行處理上，會刪除頁面。

   * 已修改：頁面已修改時。
   * 已建立：頁面建立時。
   * 已刪除：透過頁面刪除動作刪除頁面時。
   * 已轉出：頁面已轉出時。

1. 定義您將收到通知的頁面的路徑：

   * 按一下 **新增** 以新增資料列至表格。
   * 按一下 **路徑** 表格儲存格並輸入路徑，例如 `/content/docs`.

   * 若要收到屬於子樹狀結構之所有頁面的通知，請設定 **是否準確？** 至 **否**.
若要只收到路徑所定義頁面上動作的通知，請設定 **是否準確？** 至 **是**.

   * 若要允許規則，請設定 **規則** 至 **允許**. 若設為 **拒絕**，規則遭到拒絕但未移除，之後可允許。

   若要移除定義，請按一下表格儲存格並選取列 **刪除**.

1. 按一下 **確定** 以儲存設定。

## 處理您的通知 {#processing-your-notifications}

如果您已選擇在AEM收件匣中接收通知，則收件匣中會填滿通知。 您可以 [檢視您的通知](#viewing-your-notifications) 然後選取所需的通知，以便：

* 按一下以核准 **核准**：中的值 **讀取** 欄設定為 **true**.

* 按一下以刪除它 **刪除**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
