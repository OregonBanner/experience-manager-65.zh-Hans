---
title: 参与工作流
description: 工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取要執行活動的使用者或群組，並將工作專案指派給該人員或群組。
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# 参与工作流{#participating-in-workflows}

工作流程通常包括需要人員在頁面或資產上執行活動的步驟。 工作流程會選取要執行活動的使用者或群組，並將工作專案指派給該人員或群組。

## 處理您的工作專案 {#processing-your-work-items}

您可以執行下列動作來處理工作專案：

* **完成**

   您可以完成專案以允許工作流程進行到下一個步驟。

* **委派**

   如果步驟已指派給您，但由於任何原因您無法採取行動，則您可以將該步驟委派給其他使用者或群組。

   可委派的使用者取決於工作專案的指派者：

   * 如果工作專案已指派給群組，則群組成員可供使用。
   * 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
   * 如果工作專案指派給單一使用者，則無法委派工作專案。

* **回退**

   如果您發現某個步驟或一系列步驟需要重複，您可以後退。 這可讓您選取工作流程中先前發生的步驟，以便重新處理。 工作流程會回到您指定的步驟，然後從那裡繼續進行。

## 參與工作流程 {#participating-in-a-workflow}

### 已指派工作流程動作的通知 {#notifications-of-assigned-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 此 **狀態** 「網站」主控台的欄會指出頁面何時在工作流程中：

   ![workflowstatus-1](assets/workflowstatus-1.png)

* 當您或您所屬的群組被指派工作專案作為工作流程的一部分時，該工作專案會出現在您的「AEM工作流程收件匣」中。

   ![workflowinbox](assets/workflowinbox.png)

### 完成參與者步驟 {#completing-a-participant-step}

執行指示的動作後，您可以完成工作專案，讓工作流程繼續進行。 使用以下程式完成工作專案。

1. 選取工作流程步驟，然後按一下 **完成** 按鈕來切換視窗。
1. 在產生的對話方塊中選取 **下一步**；也就是接下來要執行的步驟。 下拉式清單會顯示所有適當的目的地。 A **註解** 也可以輸入。

   ![workflowcomplete](assets/workflowcomplete.png)

   列出的步驟數取決於工作流程模型的設計。

1. 按一下 **確定** 以確認動作。

### 委派參與者步驟 {#delegating-a-participant-step}

使用下列程式委派工作專案。

1. 按一下 **委派** 按鈕來切換視窗。
1. 在對話方塊中，使用下拉式清單選取 **使用者** 將工作專案委派給。 您也可以新增 **註解**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. 按一下 **確定** 以確認動作。

### 對參與者步驟執行後退 {#performing-step-back-on-a-participant-step}

請使用下列程式來後退。

1. 按一下頂端導覽列中的「後退」按鈕。
1. 在產生的對話方塊中，選取「上一步」；也就是說，要執行的下一個步驟 — 即使它是工作流程中較早發生的步驟。 下拉式清單會顯示所有適當的目的地。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 按一下「確定」以確認動作。
