---
title: 审核文件夹资源和收藏集
description: 為資料夾或收藏集中的資產設定稽核工作流程，並與稽核者或創意合作夥伴分享，以徵求意見反應。
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# 审核文件夹资源和收藏集 {#review-folder-assets-and-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | 本文 |

為資料夾或收藏集中的資產設定稽核工作流程，並與稽核者或創意合作夥伴分享，以徵求意見反應。

[!DNL Adobe Experience Manager Assets] 可讓您為資料夾或集合內的資產設定隨選稽核工作流程，並與稽核者或創意合作夥伴共用該工作流程，以徵求意見反應。

您可以將稽核工作流程與專案建立關聯，也可以建立獨立的稽核任務。

共用資產後，稽核者可以核准或拒絕資產。 通知會在工作流程的不同階段傳送，以通知預期的收件者有關各種任務的完成。 例如，當您共用資料夾或集合時，稽核者會收到資料夾/集合已共用供稽核的通知。

複查者完成複查（核准或拒絕資產）後，您會收到複查完成通知。

## 建立資料夾的稽核任務 {#creating-a-review-task-for-folders}

1. 從 [!DNL Assets] 使用者介面，選取您要建立稽核任務的資料夾。
1. 在工具列中按一下 **[!UICONTROL 建立稽核任務]** ![建立稽核任務](assets/do-not-localize/create-review-task.png) 以開啟 **[!UICONTROL 評論任務]** 頁面。 如果您在工具列中看不到選項，請按一下 **[!UICONTROL 更多]** 然後選取選項。

1. （選用）從 **[!UICONTROL 專案]** 清單中，選取要與稽核任務相關聯的專案。 根據預設， **[!UICONTROL 無]** 選項時才會選擇此選項。 如果您不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您擁有編輯器層級許可權（或更高版本）的專案才會顯示在 **[!UICONTROL 專案]** 清單。

1. 輸入稽核工作的名稱，然後從中選擇核准者 **[!UICONTROL 指派給]** 清單。

   >[!NOTE]
   >
   >所選專案的成員/群組可作為核准者出現在 **[!UICONTROL 指派給]** 清單。

1. 輸入複查工作的描述、工作優先順序和到期日。

   ![task_details](assets/task_details.png)

1. 在進階索引標籤中，輸入要用來建立URI的標籤。

   ![review_name](assets/review_name.png)

1. 按一下 **[!UICONTROL 提交]**，然後按一下 **[!UICONTROL 完成]** 以關閉確認訊息。 新任务的通知将发送给审批者。
1. 登入 [!DNL Assets] 以核准者身分導覽至 [!DNL Assets] UI。 若要核准資產，請按一下 **[!UICONTROL 通知]** 然後從清單中選取稽核任務。

   ![資產通知](assets/aemAssetsNotification.png)

1. 在 **[!UICONTROL 評論任務]** 頁面，檢查複查工作的詳細資訊，然後按一下 **[!UICONTROL 檢閱]**.
1. 在 **[!UICONTROL 評論任務]** 頁面，選取資產，然後按一下 **[!UICONTROL 核准/拒絕]** 以核准或拒絕（視情況而定）。

   ![review_task](assets/review_task.png)

1. 按一下 **[!UICONTROL 完成]** （從工具列）。 在對話方塊中，輸入註解並按一下  **[!UICONTROL 完成]** 以確認。
1. 導覽至 [!DNL Assets] 使用者介面並開啟資料夾。 資產的核准狀態圖示會出現在卡片檢視和清單檢視中。

   **信息卡视图**

   ![檢閱卡片檢視中顯示的狀態](assets/chlimage_1-404.png)

   **列表视图**

   ![檢閱狀態（如清單檢視中所示）](assets/review_status_listview.png)

## 建立集合的稽核任務 {#creating-a-review-task-for-collections}

1. 從「集合」頁面中，選取您要建立稽核任務的集合。
1. 在工具列中按一下 **[!UICONTROL 建立稽核任務]** ![建立稽核任務](assets/do-not-localize/create-review-task.png) 以開啟 **[!UICONTROL 評論任務]** 頁面。 如果您在工具列上看不到選項，請按一下 **[!UICONTROL 更多]** 然後選取選項。

1. （選用）從 **[!UICONTROL 專案]** 清單中，選取要與稽核任務相關聯的專案。 根據預設， **[!UICONTROL 無]** 選項時才會選擇此選項。 如果您不想將任何專案與稽核任務相關聯，請保留此選擇。

   >[!NOTE]
   >
   >只有您擁有編輯器層級許可權（或更高版本）的專案才會顯示在 **[!UICONTROL 專案]** 清單。

1. 輸入稽核工作的名稱，然後從中選擇核准者 **[!UICONTROL 指派給]** 清單。

   >[!NOTE]
   >
   >所選專案的成員/群組可作為核准者出現在 **[!UICONTROL 指派給]** 清單。

1. 輸入複查工作的描述、工作優先順序和到期日。

   ![task_details-collection](assets/task_details-collection.png)

1. 按一下 **[!UICONTROL 提交]**，然後按一下 **[!UICONTROL 完成]** 以關閉確認訊息。 新任务的通知将发送给审批者。
1. 登入 [!DNL Assets] 以核准者身分導覽至 [!DNL Assets] 主控台。 若要核准資產，請按一下 **[!UICONTROL 通知]** 然後從清單中選取稽核任務。
1. 在 **[!UICONTROL 評論任務]** 頁面，檢查複查工作的詳細資訊，然後按一下 **[!UICONTROL 檢閱]**.
1. 收藏集中的所有資產都會顯示在稽核頁面上。 選取資產並按一下 **[!UICONTROL 核准/拒絕]** 以核准或拒絕資產。

   ![review_task_collection](assets/review_task_collection.png)

1. 按一下 **[!UICONTROL 完成]** （從工具列）。 在對話方塊中，輸入註解並按一下 **[!UICONTROL 完成]** 以確認。
1. 導覽至「系列」主控台，並開啟系列。 資產的核准狀態圖示會顯示在「卡片」和「清單」檢視中。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *圖：卡片檢視。*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *圖：清單檢視。*
