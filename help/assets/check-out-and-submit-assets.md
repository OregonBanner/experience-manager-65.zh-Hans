---
title: 存回和取出檔案 [!DNL Assets]
description: 瞭解如何簽出資產進行編輯，並在變更完成後重新簽入。
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# 在中籤入和簽出檔案 [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 可讓您出庫資產以進行編輯，並在完成變更後重新入庫。 出庫資產後，只有您可以編輯、註釋、發佈、移動或刪除資產。 出庫資產會鎖定資產。 在您重新將資產簽入到之前，其他使用者無法對資產執行任何這些操作 [!DNL Assets]. 不過，他們仍可變更已鎖定資產的中繼資料。

若要能夠簽出/簽入資產，您需要對資產的寫入許可權。

此功能有助於防止其他使用者覆寫作者所做的變更，因為有多位使用者跨團隊共同編輯工作流程。

## 簽出資產 {#checking-out-assets}

1. 從 [!DNL Assets] 使用者介面，選取您要出庫的資產。 您也可以選取多個要出庫的資產。
1. 在工具列中按一下 **[!UICONTROL 簽出]**. 此 **[!UICONTROL 簽出]** 選項切換至 **[!UICONTROL 簽入]**.
若要確認其他使用者是否可編輯您出庫的資產，請以其他使用者身分登入。 在您出庫的資產縮圖上會顯示鎖定符號。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   選取資產。 請注意，工具列不會顯示任何可讓您編輯、註釋、發佈或刪除資產的選項。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   若要編輯已鎖定資產的中繼資料，請按一下 **[!UICONTROL 檢視屬性]**.

1. 按一下 **[!UICONTROL 編輯]** ，以在編輯模式中開啟資產。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您也可以選擇註釋或發佈資產。

1. 從中選擇已編輯的資產 [!DNL Assets] 介面，然後按一下 **[!UICONTROL 簽入]** （從工具列）。 已修改的資產已入庫至 [!DNL Assets] 和可供其他使用者編輯。

## 強制籤入 {#forced-check-in}

管理員可以簽入由其他使用者簽出的資產。

1. 登入 [!DNL Assets] 作為管理員。
1. 從 [!DNL Assets] 使用者介面選取一個或多個已由其他使用者出庫的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具列中按一下 **[!UICONTROL 解除鎖定]**. 資產會重新入庫，以供其他使用者編輯。

## 最佳作法和限制 {#tips-limitations}

* 可以刪除 *資料夾* 包含已取出資產檔案的檔案。 刪除資料夾之前，請確保使用者未簽出任何數位資產。

>[!MORELIKETHIS]
>
>* [了解籤入和簽出 [!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解籤入和簽出的影片教學課程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

