---
title: 安裝及設定ImageMagick
description: 瞭解ImageMagick軟體、如何安裝、設定命令列程式步驟，以及使用它來編輯、撰寫和從影像產生縮圖。
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools
exl-id: 6c149d31-1e64-4d29-a32a-58bd69e9fa98
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# 安裝並設定ImageMagick以搭配使用 [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick是用來建立、編輯、撰寫或轉換點陣圖影像的軟體外掛程式。 它能夠以各種格式（超過200種）讀取和寫入影像，包括PNG、JPEG、JPEG-2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF和SVG。 使用ImageMagick來調整影像大小、翻轉、映象、旋轉、扭曲、傾斜和變形。 您也可以使用ImageMagick調整影像顏色、套用各種特殊效果，或繪製文字、線條、多邊形、橢圓和曲線。

使用 [!DNL Adobe Experience Manager] 從命令列處理媒體處理常式，以透過ImageMagick處理影像。 若要使用ImageMagick處理各種檔案格式，請參閱 [資產檔案格式最佳實務](/help/assets/assets-file-format-best-practices.md). 若要瞭解所有支援的檔案格式，請參閱 [資產支援的格式](/help/assets/assets-formats.md).

若要使用ImageMagick處理大型檔案，請考慮高於一般的記憶體需求、IM原則所需的潛在變更，以及對效能的整體影響。 記憶體需求取決於各種因素，例如解析度、位元深度、色彩設定檔和檔案格式。 如果您要使用ImageMagick處理非常大型的檔案，請將 [!DNL Experience Manager] 伺服器。 最後提供了一些實用的資源。

>[!NOTE]
>
>如果您使用 [!DNL Experience Manager] 於 [!DNL Adobe Managed Services] (AMS)，如果您計畫處理許多高解析度PSD或PSB檔案，請聯絡Adobe客戶支援。 [!DNL Experience Manager] 可能无法处理超过 30000 x 23000 像素的高分辨率 PSB 文件。

## 安裝ImageMagick {#installing-imagemagick}

ImageMagic安裝檔案的多個版本可供各種作業系統使用。 使用適用於您的作業系統的版本。

1. 下載適當的 [ImageMagick安裝檔案](https://www.imagemagick.org/script/download.php) 適用於您的作業系統。
1. 若要在託管ImageMagick的磁碟上安裝 [!DNL Experience Manager] 伺服器，啟動安裝檔案。

1. 將路徑Environment變數設定為ImageMagic安裝目錄。
1. 若要檢查安裝是否成功，請執行 `identify -version` 命令。

## 設定命令列處理步驟 {#set-up-the-command-line-process-step}

您可以針對特定使用案例設定命令列處理步驟。 每次新增JPEG影像檔案至時，請執行這些步驟以產生翻轉的影像和縮圖（140x100、48x48、319x319和1280x1280） `/content/dam` 於 [!DNL Experience Manager] 伺服器：

1. 於 [!DNL Experience Manager] 伺服器，前往工作流程主控台(`https://[aem_server]:[port]/workflow`)並開啟 **[!UICONTROL DAM更新資產]** 工作流程模型。
1. 從 **[!UICONTROL DAM更新資產]** 工作流程模型，開啟 **[!UICONTROL EPS縮圖（由ImageMagick提供技術支援）]** 步驟。
1. 在 **[!UICONTROL 引數標籤]**，新增 `image/jpeg` 至 **[!UICONTROL Mime型別]** 清單。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 在 **[!UICONTROL 命令]** 方塊中，輸入下列指令：

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. 選取 **[!UICONTROL 刪除產生的轉譯]** 和 **[!UICONTROL 產生Web轉譯]** 旗標。

   ![select_flags](assets/select_flags.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 索引標籤中，指定尺寸為1280x1280畫素的轉譯細節。 此外，請指定 `image/jpeg` 在 **[!UICONTROL Mimetype]** 方塊。

   ![web_enabled_image](assets/web_enabled_image.png)

1. 按一下 **[!UICONTROL 確定]** 以儲存變更。

   >[!NOTE]
   >
   >此 `convert` 命令可能無法與某些Windows版本（例如Windows SE）一起執行，因為它與原生版本衝突 `convert` Windows安裝中的公用程式。 在此情況下，請提及ImageMagick公用程式的完整路徑。 例如，指定
   >
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. 開啟 **[!UICONTROL 程式縮圖]** 步驟，並新增MIME型別 `image/jpeg` 在 **[!UICONTROL 略過Mime型別]**.

   ![skip_mime_type](assets/skip_mime_types.png)

1. 在 **[!UICONTROL 啟用Web的影像]** 索引標籤，新增MIME型別 `image/jpeg` 在 **[!UICONTROL 略過清單]**. 按一下 **[!UICONTROL 確定]** 以儲存變更。

   ![web_enabled](assets/web_enabled.png)

1. 儲存工作流程。

1. 若要確認處理正確，請上傳JPG影像至 [!DNL Assets]. 處理完成後，請檢查是否產生翻轉的影像和轉譯。

## 減少安全性弱點 {#mitigating-security-vulnerabilities}

使用ImageMagick處理影像時，有多個安全漏洞。 例如，處理使用者提交的影像涉及遠端程式碼執行(RCE)的風險。

此外，各種影像處理外掛程式取決於ImageMagick資料庫，包括但不限於PHP的影像、Ruby的筆記型與文書夾，以及nodejs的影像彙整型。

如果您使用ImageMagick或受影響的程式庫，Adobe建議您至少執行下列其中一項作業（但最好是兩者）來減少已知漏洞：

1. 確認所有影像檔案的開頭都是預期的 [&quot;magic bytes&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) 與支援的影像檔案型別相對應，然後再傳送給ImageMagick進行處理。
1. 使用原則檔案來停用易受攻擊的ImageMagick編碼器。 ImageMagick的全域原則位於 `/etc/ImageMagick`.
