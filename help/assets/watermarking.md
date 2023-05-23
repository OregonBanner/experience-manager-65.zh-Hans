---
title: 為您的數位資產新增浮水印
description: 瞭解如何使用浮水印功能為資產新增數位浮水印。
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 2%

---

# 為您的數位資產加上浮水印 {#watermarking}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 可讓您為資產新增數位浮水印，協助使用者驗證資產的真實性和版權所有權。 [!DNL Experience Manager Assets] 支援在PNG和JPEG檔案上當作浮水印使用的文字。

若要在資產上套用浮水印，請在 [!UICONTROL DAM更新資產] 工作流程。

1. 存取 [!DNL Experience Manager] 使用者介面，並前往 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
1. 從 **[!UICONTROL 工作流程模型]** 頁面，選取 **[!UICONTROL DAM更新資產]** 工作流程與點按 **[!UICONTROL 編輯]**.

1. 從側面板拖曳 **[!UICONTROL 新增浮水印]** 步驟至 [!UICONTROL DAM更新資產] 工作流程。

   ![拖曳 [!UICONTROL 新增浮水印] 步驟並新增至 [!UICONTROL DAM更新資產] 工作流程](assets/add_watermark_step_aem_assets.png)

   *圖：拖曳 [!UICONTROL 新增浮水印] 步驟並新增至 [!UICONTROL DAM更新資產] 工作流程。*

   >[!NOTE]
   >
   >放置 [!UICONTROL 新增浮水印] 步驟之前的任何位置 [!UICONTROL 程式縮圖] 步驟。

1. 開啟 **[!UICONTROL 新增浮水印]** 步驟以顯示其屬性。
1. 在 **[!UICONTROL 引數]** 標籤，指定各種欄位中的有效值，包括文字、字型型別、大小、顏色、位置、方向等等。 若要確認變更，請按一下 **[!UICONTROL 完成]**.

   ![在中的新增浮水印步驟中提供引數 [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *圖：在新增浮水印步驟中提供引數 [!DNL Assets].*

1. 儲存 **[!UICONTROL DAM更新資產]** 包含浮水印步驟的工作流程。
1. 從 [!DNL Assets] 使用者介面，上傳範例資產。 浮水印會以字型大小、顏色等顯示在您在上述步驟中設定的位置。

若要以程式設計方式或使用動態資訊為PDF檔案加上浮水印，請考慮使用 [Experience Manager檔案服務](/help/forms/using/overview-aem-document-services.md) 方案。

## 提示和限制 {#tips-limitations}

* 僅支援文字型浮水印。 即使您可在建立影像時上傳影像，影像也不會作為浮水印 [!UICONTROL 新增浮水印程式].
* 僅支援PNG和JPEG檔案加注水印。 其他資產格式不會加上浮水印。
