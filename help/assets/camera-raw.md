---
title: '"[!DNL Adobe Camera Raw] 支援處理數位資產」'
description: 瞭解如何啟用 [!DNL Adobe Camera Raw] 中的支援 [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# 處理影像，使用 [!DNL Adobe Camera Raw] {#camera-raw-support}

您可以啟用 [!DNL Adobe Camera Raw] 支援處理原始檔案格式（例如CR2、NEF和RAF），並以JPEG格式轉譯影像。 支援的功能 [!DNL Adobe Experience Manager Assets] 使用 [Camera Raw封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) 可透過Software Distribution取得。

>[!NOTE]
>
>功能僅支援JPEG轉譯。 Windows 64位元、Mac作業系統和RHEL 7.x均支援此功能。

若要啟用 [!DNL Camera Raw] 中的支援 [!DNL Experience Manager Assets]，請遵循下列步驟：

1. 下載 [[!DNL Camera Raw] 封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) 從 [!DNL Software Distribution].
1. 访问 `https://[aem_server]:[port]/workflow`. 開啟 **[!UICONTROL DAM更新資產]** 工作流程。
1. 編輯 **[!UICONTROL 程式縮圖]** 步驟。
1. 在「 」中提供下列設定 **[!UICONTROL 縮圖]** 標籤：

   * **[!UICONTROL 縮圖]**： `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL 跳过 MIME 类型]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 標籤，在 **[!UICONTROL 略過清單]** 欄位，指定 `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. 從側面板新增 **[!UICONTROL Camera Raw/DNG處理常式]** 步驟低於 **[!UICONTROL 程式縮圖]** 步驟。
1. 在 **[!UICONTROL Camera Raw/DNG處理常式]** 步驟，將下列設定新增至 **[!UICONTROL 引數]** 標籤：

   * **[!UICONTROL Mime型別]**： `image/dng` 和 `image/x-raw-(.*)`
   * **[!UICONTROL 命令]**：

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. 单击“**[!UICONTROL 保存]**”。

>[!NOTE]
>
>確保上述設定與 **[!UICONTROL 具有Camera Raw和DNG處理步驟的DAM更新資產範例]** 設定。

您現在可以將Camera Raw檔案匯入「資產」。 安裝Camera Raw套件並設定所需的工作流程後， **[!UICONTROL 影像調整]** 選項會顯示在側窗格清單中。

![chlimage_1-131](assets/chlimage_1-337.png)

*圖：側窗格中的選項。*

![chlimage_1-132](assets/chlimage_1-338.png)

*圖：使用選項對影像進行輕量編輯。*

將編輯儲存至後 [!DNL Camera Raw] 影像，新轉譯 `AdjustedPreview.jpg` 會為影像產生。 對於其他影像型別，除了 [!DNL Camera Raw]，變更會反映在所有轉譯中。

## 最佳實務、已知問題和限制 {#best-practices}

功能具有下列限制：

* 功能僅支援JPEG轉譯。 Windows 64位元、Mac作業系統和RHEL 7.x均支援此功能。
* RAW和DNG格式不支援中繼資料回寫。
* 此 [!DNL Camera Raw] 程式庫一次可處理的總畫素數存在限制。 目前，它最多可在檔案長邊處理65000個畫素，或處理先遇到的任何條件的512 MP。
