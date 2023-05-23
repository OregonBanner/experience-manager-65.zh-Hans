---
title: 活動資料流功能
seo-title: Activity Streams Feature
description: 已登入社群成員的活動
seo-description: Activities of a signed-in community member
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# 活動資料流功能 {#activity-streams-feature}

## 简介 {#introduction}

已登入社群成員的活動（例如張貼至論壇或部落格）會收集到資料流中，並可透過設定的以各種方式篩選和顯示。 `Activity Streams` 元件。

當社群成員關注感興趣的張貼或關注其他社群成員的活動時，關注功能會新增另一個活動檢視。

本檔案說明：

* 將「活動串流」元件新增至AEM網站
* 活動串流元件的組態設定

### 新增活動資料流至頁面 {#adding-activity-streams-to-a-page}

如果需要新增 `Activity Streams` 元件至作者模式下的頁面，請使用元件瀏覽器來尋找

* `Communities / Activity Streams`

並將其拖曳至應顯示活動資料流的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](/help/communities/basics.md).

當 [必要的使用者端程式庫](/help/communities/essentials-activities.md#essentials-for-client-side) 包含，這就是 `Activity Streams` 元件隨即出現：

![活動資料流](assets/activity-component.png)

### 設定活動資料流 {#configuring-activity-streams}

選取已放置的 `Activity Streams` 元件以存取及選取 `Configure` 圖示來開啟「編輯」對話方塊。

![設定](assets/configure-new.png)

在 **使用者活動** 索引標籤中，指定要顯示的活動：

![user-activities](assets/user-activities.png)

* **活动最大数量**

   要顯示的活動數

* **流资源路径**

   留空則預設為社群網站或社群群組。 串流資源路徑可識別活動的來源。 預設為空白。

* **显示“用户活动”视图**

   如果勾選，活動頁面將包含一個標籤，該標籤會根據目前成員在社群內產生的活動來篩選活動。 預設為已核取。

* **显示“全部活动”视图**

   如果勾選，活動頁面將包含一個標籤，其中包含目前成員有權存取的社群內產生的所有活動。 預設為已核取。

* **显示“关注”视图**

   如果勾選，活動頁面將包含一個索引標籤，該索引標籤會根據目前成員所關注的活動來篩選活動。 預設為已核取。

### 下列檢視 {#following-view}

元件必須設定為啟用下列功能。 允許追蹤的功能包括 [部落格](/help/communities/blog-feature.md)， [論壇](/help/communities/forum.md)， [QnA](/help/communities/working-with-qna.md)， [行事曆](/help/communities/calendar.md)， [檔案庫](/help/communities/file-library.md)、和 [評論](/help/communities/comments.md).

![following-view](assets/following-activities.png)

此 **追隨** 按鈕提供將專案視為活動來追蹤的方法， [通知](/help/communities/notifications.md)，或 [訂閱](/help/communities/subscriptions.md). 每次 **追隨** 按鈕已選取，可以開啟或關閉選取專案。 此 `Email Subscriptions` 選取範圍只有在設定後才存在。

如果選取了任何跟隨方法，按鈕的文字將變更為 **關注**. 為方便起見，您可以選取 `Unfollow All` 以關閉所有方法。

此 **追隨** 按鈕隨即出現：

* 檢視其他成員的設定檔時。
* 在主要功能頁面上，例如論壇、QnA和部落格。

   * 遵循該一般功能的所有活動。

* 適用於特定專案，例如論壇主題、QnA問題或部落格。

   * 追蹤該特定專案的所有活動。

### 附加信息 {#additional-information}

如需詳細資訊，請參閱 [活動串流Essentials](/help/communities/essentials-activities.md) 適用於開發人員的頁面。
