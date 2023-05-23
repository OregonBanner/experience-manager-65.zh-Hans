---
title: Communities 订阅
seo-title: Communities Subscriptions
description: 社群成員透過電子郵件與其他成員互動
seo-description: Community members interact with other members through email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Communities 订阅 {#communities-subscriptions}

## 概述 {#overview}

截至社群 [FP1](deploy-communities.md#latestfeaturepack)，社群成員可使用稱為訂閱的功能，透過電子郵件與社群互動。

訂閱類似於 [通知](notifications.md) 成員可在關注部落格、論壇主題或QnA問題時訂閱。

訂閱與通知的區別在於：

* 下列其他成員時，成員不得訂閱。
* 成員唯一要採取的動作是選取 `Email Subscriptions` 進行下列操作時。
* 設定電子郵件回覆時，成員只需回覆收到的電子郵件，即可有效發佈內容。

### 要求 {#requirements}

**設定電子郵件**

若要讓訂閱正常運作，且成員能透過電子郵件回覆，則必須設定電子郵件。

如需設定電子郵件的指示，請參閱 [設定電子郵件](email.md).

**啟用訂閱並關注**

元件必須設定為啟用訂閱 *和* 後續專案。 允許訂閱的功能包括 [部落格](blog-feature.md)， [論壇](forum.md) 和 [QnA](working-with-qna.md).

## 來自以下專案的訂閱 {#subscriptions-from-following}

![subscription-flowing](assets/subscription-following.png)

此 **追隨** button提供將專案視為活動、訂閱和/或通知來追蹤的方法。 每次 **追隨** 按鈕已選取，可以開啟或關閉選取專案。

如果選取了任何跟隨方法，按鈕的文字將變更為 **關注**. 為方便起見，您可以選取 `Unfollow All` 以關閉所有方法。

此 **追隨** 按鈕將包含 `Email Subscriptions` 選項，但僅限於論壇、QnA或部落格設定為啟用電子郵件訂閱時。 此按鈕將會出現：

* 在啟用的論壇、QnA或部落格的主要功能頁面上，將針對該功能下的所有活動傳送電子郵件。

* 針對特定專案，例如論壇主題、QnA問題或部落格。當存在該特定專案的活動時，將傳送電子郵件。

## 透過電子郵件回覆 {#reply-by-email}

當電子郵件為 [設定為透過電子郵件回覆](email.md#configure-polling-importer)，訂閱的成員將收到一封電子郵件，其中包含張貼的內容和線上內容的連結。

如果他們回覆電子郵件，他們在回覆中輸入的內容將顯示為線上內容。

![email-reply](assets/email-reply.png)

張貼回覆所花的時間由 [polling importer的更新間隔](email.md#configure-polling-importer).

![QA](assets/qa.png)
