---
title: 使用PDF模擬轉譯器產生轉譯
description: 使用Adobe PDF模擬轉譯器資料庫產生高品質的縮圖和轉譯。
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 使用PDF模擬轉譯器 {#using-pdf-rasterizer}

上傳大型內容密集型PDF或AI檔案至 [!DNL Adobe Experience Manager Assets]，預設程式庫可能不會產生準確的輸出。 與預設程式庫的輸出相比，Adobe的PDF模擬轉譯器程式庫可以產生更可靠和準確的輸出。 Adobe建議在下列情況下使用PDF模擬轉譯器資料庫：

Adobe建議針對下列專案使用PDF模擬轉譯器資料庫：

* 大量且需要大量內容的AI檔案或PDF檔案。
* AI檔案和PDF檔案，其中包含預設不會產生的縮圖。
* 具有Pantone Matching System (PMS)顏色的AI檔案。

使用PDF模擬轉譯器產生的縮圖和預覽品質比現成可用的輸出更好，因此可提供跨裝置的一致檢視體驗。 Adobe PDF模擬轉譯器資料庫不支援任何色域轉換。 無論來源檔案的色域為何，一律會輸出為RGB。

1. 將PDF模擬轉譯器套件安裝在您的 [!DNL Adobe Experience Manager] 部署來源 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >PDF模擬轉譯器程式庫僅適用於Windows和Linux。

1. 存取 [!DNL Assets] 工作流程控制檯位於 `https://[aem_server]:[port]/workflow`. 開啟 [!UICONTROL DAM更新資產] 工作流程。

1. 若要防止使用預設方法為PDF檔案和AI檔案產生縮圖和網頁轉譯，請遵循以下步驟：

   * 開啟 **[!UICONTROL 程式縮圖]** 步驟，並新增 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 略過Mime型別]** 欄位位於 **[!UICONTROL 縮圖]** 標籤以視需要顯示。

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * 在 **[!UICONTROL 啟用Web的影像]** 標籤，新增 `application/pdf` 或 `application/postscript` 在 **[!UICONTROL 略過清單]** 視您的需求而定。

   ![跳過影像格式縮圖處理的設定](assets/web_enabled_imageskiplist.png)

1. 開啟 **[!UICONTROL 點陣化PDF/AI影像預覽轉譯]** 步驟，並移除您要略過預設產生預覽影像轉譯的MIME型別。 例如，移除MIME型別 `application/pdf`， `application/postscript`，或 `application/illustrator` 從 **[!UICONTROL MIME型別]** 清單。

   ![process_arguments](assets/process_arguments.png)

1. 拖曳 **[!UICONTROL PDF模擬轉譯器處理常式]** 從側面板逐步移至 **[!UICONTROL 程式縮圖]** 步驟。
1. 設定以下引數 **[!UICONTROL PDF模擬轉譯器處理常式]** 步驟：

   * MIME型別： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小：319:319、140:100、48:48。 視需要新增自訂縮圖設定。

   的命令列引數 `PDFRasterizer` 命令可以包括下列內容：

   * `-d`：此旗標可讓您順暢地呈現文字、向量圖稿和影像。 建立品質更好的影像。 但是，包含此引數會導致命令執行速度緩慢並增加影像大小。

   * `-s`：影像尺寸上限（高度或寬度）。 這會轉換為每一頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設值為實際頁面大小。

   * `-t`：輸出影像型別。 有效型別為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`：輸入PDF的路徑。 此為必要引數。

   * `-h`: 帮助


1. 若要刪除中繼轉譯，請選取 **[!UICONTROL 刪除產生的轉譯]**.
1. 若要讓PDF模擬轉譯器產生網頁轉譯，請選取 **[!UICONTROL 產生Web轉譯]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. 指定中的設定 **[!UICONTROL 啟用Web的影像]** 標籤。

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. 儲存工作流程。
1. 若要啟用PDF模擬轉譯器以使用PDF資料庫處理PDF頁面，請開啟 **[!UICONTROL DAM程式子資產]** 模型來自 [!UICONTROL 工作流程] 主控台。
1. 從側面板，將「PDF模擬轉譯器處理常式」步驟拖曳至 **[!UICONTROL 建立可支援Web的影像轉譯]** 步驟。
1. 設定以下引數 **[!UICONTROL PDF模擬轉譯器處理常式]** 步驟：

   * MIME型別： `application/pdf` 或 `application/postscript`
   * 命令: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * 新增縮圖大小： `319:319`， `140:100`， `48:48`. 視需要新增自訂縮圖設定。

   的命令列引數 `PDFRasterizer` 命令可以包括下列內容：

   * `-d`：此旗標可讓您順暢地呈現文字、向量圖稿和影像。 建立品質更好的影像。 但是，包含此引數會導致命令執行速度緩慢並增加影像大小。

   * `-s`：影像尺寸上限（高度或寬度）。 這會轉換為每一頁的DPI。 如果頁面大小不同，每個頁面可能會以不同的數量縮放。 預設值為實際頁面大小。

   * `-t`：輸出影像型別。 有效型別為JPEG、PNG、GIF和BMP。 預設值為JPEG。

   * `-i`：輸入PDF的路徑。 此為必要引數。

   * `-h`: 帮助


1. 若要刪除中繼轉譯，請選取 **[!UICONTROL 刪除產生的轉譯]**.
1. 若要讓PDF模擬轉譯器產生網頁轉譯，請選取 **[!UICONTROL 產生Web轉譯]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. 指定中的設定 **[!UICONTROL 啟用Web的影像]** 標籤。

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. 儲存工作流程。
1. 上傳PDF檔案或AI檔案至 [!DNL Experience Manager Assets]. PDF模擬轉譯器會產生檔案的縮圖和Web轉譯。
