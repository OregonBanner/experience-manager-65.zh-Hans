---
title: 共用資產的私人資料夾
description: 瞭解如何在中建立私人資料夾 [!DNL Adobe Experience Manager Assets] 並與其他使用者共用，且指派各種許可權給他們。
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 2%

---

# 中的私人資料夾 [!DNL Adobe Experience Manager Assets] {#private-folder}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | 本文 |

您可以在中建立私人資料夾 [!DNL Adobe Experience Manager Assets] 您專屬的使用者介面。 您可以與其他使用者共用此私人資料夾，並為其指派各種許可權。 根據您指派的許可權層級，使用者可以在資料夾上執行各種工作，例如檢視資料夾內的資產或編輯資產。

>[!NOTE]
>
>私人資料夾至少有一個成員具有擁有者角色。

## 私人資料夾的建立和共用 {#create-share-private-folder}

若要建立和共用私人資料夾：

1. 在 [!DNL Assets] 主控台，按一下 **[!UICONTROL 建立]** 從工具列中，然後選擇 **[!UICONTROL 資料夾]** 功能表中的。

   ![建立資產資料夾](assets/Create-folder.png)

1. 在 **[!UICONTROL 建立資料夾]** 對話方塊，輸入資料夾的標題和名稱（選擇性），然後選取 **[!UICONTROL 私人]** 選項。

1. 单击&#x200B;**[!UICONTROL 创建]**。已建立私人資料夾。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 若要與其他使用者共用資料夾以及為其指派許可權，請選取該資料夾，然後按一下 **[!UICONTROL 屬性]** （從工具列）。

   ![資訊選項](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共用資料夾之前，其他使用者看不到該資料夾。

1. 在 **[!UICONTROL 資料夾屬性]** 頁面，從中選擇使用者 **[!UICONTROL 新增使用者]** 清單、指派角色給私人資料夾中的使用者，然後按一下 **[!UICONTROL 新增]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以指派各種角色，例如 `Editor`， `Owner`，或 `Viewer` 共用資料夾的使用者。 如果您指派 `Owner` 角色至使用者，使用者具有 `Editor` 檔案夾的許可權。 此外，使用者可以與其他人共用資料夾。 如果您指派 `Editor` 角色，則使用者可編輯您私人資料夾中的資產。 如果您指派檢視器角色，則使用者只能檢視您私人資料夾中的資產。

   >[!NOTE]
   >
   >私人資料夾至少有一個成員具有 `Owner` 角色。 因此，管理員無法從私人資料夾中移除所有擁有者成員。 但是，若要從私人資料夾中移除現有的擁有者（以及管理員本身），管理員必須新增另一個使用者作為擁有者。

1. 单击“**[!UICONTROL 保存]**”。根據您指派的角色，當使用者登入時，會指派一組許可權給使用者您的私人資料夾 [!DNL Assets].
1. 按一下 **[!UICONTROL 確定]** 以關閉確認訊息。
1. 共用資料夾的使用者會收到共用通知。 登入 [!DNL Assets] 具有檢視通知的使用者認證。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 按一下 [!UICONTROL 通知] 以開啟通知清單。

   ![通知清單](assets/Assets-Notification.png)

1. 按一下管理員共用的私人資料夾專案，開啟該資料夾。

>[!NOTE]
>
>若要建立私人資料夾，您需要讀取和修改 [存取控制許可權](/help/sites-administering/security.md#permissions-in-aem) 建立私人資料夾的父資料夾上。 如果您不是管理員，預設不會在上為您啟用這些許可權。 `/content/dam`. 在這種情況下，請先取得這些使用者ID/群組的許可權，然後再嘗試建立私人資料夾。

## 私人資料夾刪除 {#delete-private-folder}

您可以選取資料夾並選取「 」，刪除資料夾 [!UICONTROL 刪除] 選項，或使用鍵盤上的退格鍵。

![刪除頂端選單中的選項](assets/delete-option.png)

>[!CAUTION]
>
>如果您從CRXDE Lite中刪除私人資料夾，則多餘的使用者群組會留在存放庫中。

>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則相關聯的使用者群組也會被刪除。
>
>但是，現有的備援、未使用和自動產生的使用者群組可以使用從存放庫中移除 `clean` 編寫執行個體中的JMX方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。
