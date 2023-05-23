---
title: 使用停止的操作和分支
seo-title: Working with stalled operations and branches
description: 「停止的作業」頁面和「停止的分支」頁面會顯示已停止的程式。
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 使用停止的操作和分支 {#working-with-stalled-operations-and-branches}

「停止的作業」頁面和「停止的分支」頁面會顯示已停止的程式。 當作業執行期間或之後發生錯誤，或由於處理程式中的刻意延遲作業而發生錯誤時，處理程式可能會延遲：

* 作業可能因未預期的錯誤而停止。 但是，流程中的「停止分支」操作會故意阻止流程進一步執行，並要求管理員介入。
* 在規則評估期間，分支可能會在操作之間停頓。

當處理序停止時，不會執行進一步的作業，直到問題解決且作業或分支重新啟動為止。

對於每個停頓的專案，清單會顯示下列資訊：

**作業名稱或分支名稱：** 作業或分支的名稱。

**狀態：** 對於停頓的專案，一律停頓。

**錯誤：** 問題的簡短說明。

**程式ID：** 形成工作流程在程式例項化時（即當使用者或自動化步驟啟動程式時）指派的正整數。 您可以使用此識別碼來追蹤流程例證整個生命週期。

**程式名稱 — 版本：** 在Workbench中指派的處理名稱。

**已停止日期：** 作業或分支停止的日期和時間。

您可以在「停止的操作」或「停止的分支」頁面上執行下列工作：

* 選取錯誤以檢視其詳細資訊。 選取錯誤時，會顯示「錯誤詳細資訊」頁面。
* 終止或重試停止的操作或重試停止的分支。

## 終止或重試停止的操作或分支 {#terminating-or-retrying-stalled-operations-or-branches}

在「停頓的操作」頁面上，您可以終止顯示的程式例證。

當您終止處理序執行個體時，它會停止執行，並且不會發生進一步的操作。 通常只有在處理程式因錯誤而遭到封鎖或無法使用，且無法修復和重新啟動時，您才會終止該處理程式。

您可以在「停頓的作業」頁面或「停頓的分支」頁面上，重試作業或分支。

當您重試操作時，會傳送Forms工作流程請求以重新啟動操作。 如果造成處理序停止的錯誤已經修正，且重試要求成功，處理序會從停止點開始再次執行，其狀態會變更為「執行中」。 如果無法重新啟動作業，作業會維持在「已停止」狀態，您可能需要終止作業。

### 終止停止的作業 {#terminate-a-stalled-operation}

1. 在Administration Console中，按一下「服務>表單工作流程>停止的操作錯誤」。
1. 在「停頓的作業」頁面上，選取要終止的專案，然後按一下「終止」。

### 重試停止的操作或分支 {#retry-a-stalled-operation-or-branch}

1. 在管理控制檯中，按一下「服務>表單工作流程」，然後按一下「停止的操作錯誤」或「停止的分支錯誤」。
1. 在「停止的操作」或「停止的分支」頁面上，選取要重試的專案，然後按一下「重試」。

## 檢視有關停止的操作或分支的錯誤詳細資料 {#viewing-error-details-about-stalled-operations-or-branches}

如果您從「停止的作業」或「停止的分支」頁面上的停止專案清單中選取錯誤，則會顯示「錯誤詳細資訊」頁面，其中顯示可協助您疑難排解問題的錯誤詳細資訊。

頁面底部的方塊包含錯誤資訊。

您也可以從「錯誤詳細資料」頁面終止或重試停止的作業，以及重試停止的分支。

## 當向上呈報使用者不存在時，處理程式不會停頓 {#process-does-not-stall-when-escalation-user-does-not-exist}

當AEM Forms使用者服務中的「指派工作」作業設定為在特定時段後將工作升級給另一個使用者，且升級使用者在「指派工作」作業執行之後但在升級發生之前被刪除時，就會發生錯誤。

發生此情況時，流程和任務的狀態不會在設定的升級時間變更，而且升級不會發生，但流程不會停頓。 下列訊息會顯示在伺服器記錄檔中：

「針對taskID指定的提升主體無效： *數字*，佇列已指定： *數字*.」

如果在產生任務之前（在指派任務作業執行之前）刪除提升使用者，則程式會停止或擲回InvalidPrincipal例外狀況事件。

為避免此問題，當您刪除使用者時，請搜尋屬於該使用者的任務並據以處理。 (請參閱 [使用任務](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
