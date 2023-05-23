---
title: 建立和管理表單中資產的稽核
seo-title: Creating and managing reviews for assets in forms
description: 檢閱是一種機制，可讓一個或多個檢閱者對表單中可用的資產進行評論。
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: 4edfc51227607b4fb3ee4b97443d2040015b6a65
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 建立和管理表單中資產的稽核{#creating-and-managing-reviews-for-assets-in-forms}

## 审核 {#review}

檢閱是一種機制，可讓一個或多個檢閱者對表單中可用的資產進行評論。

## 設定稽核 {#setting-up-a-review}

1. 導覽至Forms索引標籤並選取表單。
1. 如果資產沒有正在進行的稽核，則開始稽核 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示會出現在「動作」列中。 按一下開始複查 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示。
1. 輸入下列資訊：

   * 稽核名稱：必要，可包含英數字元、連字型大小或底線。
   * 檢閱說明：選擇性，檢閱目的/內容的說明。
   * 稽核截止日期：選擇性，稽核結束的日期。 超過截止日期時，任務會顯示為「過期」。
   * 稽核者：至少必須有一個。 使用下拉式方塊來新增稽核者。 輸入名稱會列出所有相符的名稱；請選取一個名稱，然後按一下「新增」。

1. 填寫其餘所有詳細資料，然後按一下[開始]。

### 設定稽核時發生的動作 {#actions-that-occur-when-a-review-is-set-up}

本節說明建立或設定稽核時會發生什麼情況。

1. 建立新的稽核任務並指派給稽核發起人。
1. 所有稽核者都會被指派稽核任務。 任務會出現在其通知區段中。 檢閱者可以按一下通知，或前往「收件匣」檢視工作。 稽核者可以按一下以開啟稽核任務、檢視表單並開始新增註釋。

   ![檢閱者通知警報](assets/noti.png)

   檢閱者通知警報

1. 註解方塊可供資產的發起者和檢閱者使用。 其他人可以檢視註解，但無法寫入註解。

## 管理評論 {#managing-a-review}

>[!NOTE]
>
>只能修改正在進行的稽核。 無法修改已完成的稽核。

1. 導覽至Forms索引標籤並選取表單。

1. 如果資產正在進行檢閱，而您是檢閱的發起人，則需執行「管理檢閱」 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) 圖示會出現在「動作」列中。 只有稽核發起人可以管理（更新/結束）稽核。

   按一下「管理檢閱」 ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)圖示。

   對於啟動器以外的使用者，管理檢閱圖示會停用。

1. 您會看到一個顯示資訊的畫面：

   * **評論名稱**：無法編輯。

   * **檢閱說明**：可供編輯。

   * **檢閱期限**：可供編輯。 您可以將截止日期修改為目前日期及時間之後的任何日期及時間。

   * **檢閱者**：可供編輯。 您可以新增或移除稽核者。 如果任務過期，您只能在截止日期延長至目前日期之後新增稽核者。

1. 若要結束檢閱，請按一下「結束」。

### 修改稽核時發生的動作 {#actions-that-occur-when-a-review-is-modified}

本節說明檢閱結束/修改時會發生什麼情況：

1. 如果修改了「稽核」描述，則會更新稽核者和發起者的相應任務。
1. 如果修改了稽核截止日期，稽核者的對應任務會以新日期更新。

1. 如果移除稽核者：

   ![移除稽核者](assets/removeduser.png)

   移除稽核者

   1. 如果未完成，則指派的任務會終止。
   1. 檢閱者無法再評論該資產。

1. 如果新增稽核者：

   ![新增稽核者](assets/addedreviewer.png)

   新增稽核者

   1. 稽核任務已建立並指派給新加入的稽核者。
   1. 新新增的稽核者可以為資產新增註釋。

1. 當稽核結束時：

   1. **檢閱者**：對於每個稽核者，與稽核相關的未完成任務會終止。 任務在檢閱者的「通知」區段中不再顯示為「待定」。
   1. **發起人**：指派給檢閱發起人的任務已標籤為完成。 任務會從稽核發起人的Notification區段中移除。
   1. **全部**：評論會顯示在「先前的評論」區段中。 無法新增更多註解。
