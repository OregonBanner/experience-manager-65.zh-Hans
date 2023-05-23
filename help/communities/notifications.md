---
title: 社群通知
seo-title: Communities Notifications
description: AEM Communities有顯示登入社群成員感興趣之事件的通知
seo-description: AEM Communities has notifications that display events of interest to the signed-in community member
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# 社群通知 {#communities-notifications}

## 概述 {#overview}

AEM Communities提供通知區段，顯示已登入社群成員感興趣的事件。

通知類似於 [活動](/help/communities/essentials-activities.md) 和 [訂閱](/help/communities/subscriptions.md) 原因可能是：

* 成員張貼內容。
* 選擇跟隨其他成員的成員。
* 選擇遵循特定主題、文章和其他內容主旨的成員。
* 成員標籤(@mention)使用者產生的內容中的另一個社群成員。

通知與活動和訂閱的區別在於：

* 指向通知區段的連結一律會顯示在社群網站的標題中：

   * 活動需要 [活動資料流函式](/help/communities/functions.md#activity-stream-function) 將包含在社群網站的結構中。
   * 訂閱需要 [電子郵件的設定](/help/communities/email.md).

* 通知的實作透過可擴充和可插拔的管道進行：

   * 活動只能在Web上使用。
   * 訂閱只能透過電子郵件取得。

截至社群 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知管道包括：

* 網路頻道，存取方式： `Notifications` 連結。
* 電子郵件頻道，在正確設定電子郵件時可用。

未來的頻道包括行動裝置和桌上型電腦。

### 要求 {#requirements}

**設定電子郵件**

必須設定電子郵件，電子郵件通道才能讓通知正常運作。

如需設定電子郵件的指示，請參閱 [設定電子郵件](/help/communities/analytics.md).

**啟用追隨**

元件必須設定為啟用下列功能。 允許追蹤的功能包括 [部落格](/help/communities/blog-feature.md)， [論壇](/help/communities/forum.md)， [QnA](/help/communities/working-with-qna.md)， [行事曆](/help/communities/calendar.md)， [檔案庫](/help/communities/file-library.md)、和 [評論](/help/communities/comments.md).

**注意**:

* 社群內使用的元件 [網站範本](/help/communities/sites.md) 和 [群組範本](/help/communities/tools-groups.md) 可能已設定為遵循。

* 成員設定檔已設定為允許其他成員跟隨。

## 來自以下專案的通知 {#notifications-from-following}

![通知](assets/notifications.png)

此 **[!UICONTROL 追隨]** button提供將專案視為活動、訂閱和/或通知來追蹤的方法。 每次 **[!UICONTROL 追隨]** 按鈕已選取，可以開啟或關閉選取專案。 此 `Email Subscriptions` 選取範圍只有在設定後才存在。

如果選取了任何跟隨方法，按鈕的文字將變更為 **[!UICONTROL 關注]**. 為方便起見，您可以選取 `Unfollow All` 以關閉所有方法。

此 **[!UICONTROL 追隨]** 按鈕隨即出現：

* 檢視其他成員的設定檔時。
* 在論壇、QnA和部落格等主要功能頁面上：

   * 遵循該一般功能的所有活動。

* 針對特定專案，例如論壇主題、問題與解答問題或部落格：

   * 追蹤該特定專案的所有活動。

## 管理通知設定 {#managing-notification-settings}

從「通知」頁面選取「通知設定」連結，便可以讓每個成員管理接收通知的方式。

Web Channel一律啟用。

![notifications14](assets/notifications1.png)

電子郵件頻道，需仰賴適當的 [電子郵件的設定](/help/communities/email.md)，提供與網頁頻道相同的設定。

電子郵件通道預設為關閉。

![notifications2](assets/notifications2.png)

可由成員開啟，但仍取決於設定的電子郵件。

![notifications3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### 網頁通知 {#web-notifications}

A [精靈已建立的社群網站](/help/communities/sites-console.md) 現在包含連結至 `Notifications` 橫幅上方的網站標題列功能。 與訊息不同，會為每個社群網站建立通知，而訊息必須在網站建立過程中啟用。

造訪已發佈的網站時，選取 `Notifications` 連結將顯示成員的所有通知。

![notifications4](assets/notifications4.png)

### 电子邮件通知 {#email-notifications}

啟用電子郵件通道時，成員會收到包含網頁內容連結的電子郵件。

![notifications5](assets/notifications5.png)

## 自訂電子郵件通知 {#customize-email-notifications}

組織可以透過以下方式自訂電子郵件通知 [覆蓋](/help/communities/client-customize.md#overlays) 範本位於 **/libs/settings/community/templates/email/html**.

例如，若要修改提及電子郵件通知（對於communities元件），請新增 **如果** 動詞的條件 **提及** 在您已啟用的元件範本中 **@mentions** 支援。

若要修改電子郵件通知範本以新@mention部落格評論，請將現成可用的範本放置於： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
