---
title: 為Adobe InDesign產生僅供放置的轉譯
description: 使用Experience Manager Assets工作流程和ImageMagick產生新資產和現有資產的FPO轉譯。
contentOwner: Vishabh Gupta
role: Admin
feature: Renditions
exl-id: 1e4ddd73-a31c-4ddd-94eb-1dac6a4835b3
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# 為Adobe InDesign產生僅供放置的轉譯 {#fpo-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/configure-fpo-renditions.html?lang=en) |
| AEM 6.5 | 本文 |

將大型資產從Experience Manager放入Adobe InDesign檔案時，創意專業人士必須等待相當長的時間 [放置資產](https://helpx.adobe.com/indesign/using/placing-graphics.html). 同時，使用者會被封鎖而無法使用InDesign。 這會中斷創意流程，並對使用者體驗產生負面影響。 Adobe功能可讓您從InDesign檔案開始暫時放置小型轉譯。 當需要最終輸出時（例如對於列印和發佈工作流程），原始的全解析度資產會在背景中取代暫時轉譯。 這種背景的非同步更新可加快設計流程以提高生產力，且不會阻礙創作流程。

Adobe Experience Manager (AEM)提供僅用於放置的轉譯(FPO)。 這些FPO轉譯檔案大小雖小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程順利進行，而不會出現任何中斷情形。

## 產生FPO轉譯的方法 {#approach-to-generate-fpo-renditions}

Experience Manager可讓許多方法處理可用來產生FPO轉譯的影像。 兩個最常見的方法是使用內建Experience Manager工作流程和ImageMagick。 使用這兩種方法，您可以設定新上傳資產和Experience Manager中現有資產的轉譯產生。

您可以使用ImageMagick來處理影像，包括產生FPO轉譯。 這類轉譯會縮減取樣，也就是說，如果原始影像的PPI大於72，轉譯的畫素尺寸會按比例縮小。 另請參閱 [安裝並設定ImageMagick以搭配Experience Manager Assets使用](best-practices-for-imagemagick.md).

|  | 使用Experience Manager的內建工作流程 | 使用ImageMagick工作流程 | 備註 |
|--- |--- |---|--- |
| 針對新資產 | 啟用FPO轉譯([說明](#generate-renditions-of-new-assets-using-aem-workflow)) | 在Experience Manager工作流程中新增ImageMagick命令列([說明](#generate-renditions-of-new-assets-using-imagemagick)) | Experience Manager會對每次上傳執行DAM更新資產工作流程。 |
| 針對現有資產 | 在新的專用Experience Manager工作流程中啟用FPO轉譯([說明](#generate-renditions-of-existing-assets-using-aem-workflow)) | 在新的專用Experience Manager工作流程中新增ImageMagick命令列([說明](#generate-renditions-of-existing-assets-using-imagemagick)) | 現有資產的FPO轉譯可隨選或大量建立。 |

>[!CAUTION]
>
>建立工作流程以透過修改預設工作流程的副本來產生轉譯。 這可防止在Experience Manager更新時覆寫您的變更，例如藉由安裝新的Service Pack。

## 使用Experience Manager工作流程產生新資產的轉譯 {#generate-renditions-of-new-assets-using-aem-workflow}

以下是設定DAM更新資產工作流程模型以啟用產生轉譯的步驟：

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**. 選取 **[!UICONTROL DAM更新資產]** 模型並按一下 **[!UICONTROL 編輯]**.

1. 選取 **[!UICONTROL 程式縮圖]** 步驟並按一下 **[!UICONTROL 設定]**.

1. 按一下 **[!UICONTROL FPO轉譯]** 標籤。 選取 **[!UICONTROL 啟用FPO轉譯建立]**.

   ![fpo_rendition_damupdateasset_model](assets/fpo_rendition_damupdateasset_model.png)

1. 調整 **[!UICONTROL 品質]** 並新增或修改 **[!UICONTROL 格式清單]** 視需要提供值。 依預設，產生FPO轉譯的MIME型別清單為pjpeg、jpeg、jpg、gif、png、x-png和tiff。 按一下 **[!UICONTROL 完成]**.

   >[!NOTE]
   >
   >JPEG、GIF、PNG、TIFF、PSD和BMP等檔案型別支援產生轉譯。

1. 若要啟用變更，請按一下 **[!UICONTROL 同步]**.

>[!NOTE]
>
>單面大於1280畫素的影像不會保留FPO轉譯中的畫素尺寸。

## 使用ImageMagick產生新資產的轉譯 {#generate-renditions-of-new-assets-using-imagemagick}

在Experience Manager中，DAM更新資產工作流程會在上傳新資產時執行。 若要使用ImageMagick處理新上傳資產的轉譯，請新增命令至工作流程模型。

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 選取 **[!UICONTROL DAM更新資產]** 模型並按一下 **[!UICONTROL 編輯]**.

1. 按一下 **[!UICONTROL 切換側面板]** 並搜尋命令列步驟。

1. 拖曳 **[!UICONTROL 命令列]** 在之前逐步並新增 **[!UICONTROL 程式縮圖]** 步驟。

1. 選取 **[!UICONTROL 命令列]** 步驟並按一下 **[!UICONTROL 設定]**.

1. 將所需的資訊新增為自訂 **[!UICONTROL 標題]** 和 **[!UICONTROL 說明]**. 例如，FPO轉譯（由ImageMagick提供技術支援）。

1. 在 **[!UICONTROL 引數]** 索引標籤，新增相關 **[!UICONTROL Mime型別]** 提供命令套用的檔案格式清單。

   ![imagemagick-mimetype](assets/imagemagick-mimetype.png)

1. 在 **[!UICONTROL 引數]** 標籤，在 **[!UICONTROL 命令]** 區段，新增相關的ImageMagick指令以產生FPO轉譯。

   以下是一個命令範例，可產生JPEG格式的FPO轉譯、縮減取樣至72 PPI、10%品質設定，並透過平面化輸出來處理多層Adobe Photoshop檔案：

   `convert -quality 10% -units PixelsPerInch ${filename} -resample 72 -flatten cq5dam.fpo.jpeg`

1. 若要啟用變更，請按一下 **[!UICONTROL 同步]**.

如需ImageMagick命令列功能的詳細資訊，請參閱 [https://imagemagick.org](https://imagemagick.org).

## 使用Experience Manager工作流程產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-aem-workflow}

若要使用Experience Manager工作流程產生現有資產的FPO轉譯，請建立使用內建FPO轉譯選項的專用工作流程模型。

1. 按一下 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.

1. 若要建立模型，請按一下 **[!UICONTROL 建立]** > **[!UICONTROL 建立模型]**.

1. 新增有意義的內容 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]**.

1. 選取模型並按一下 **[!UICONTROL 編輯]**. 按一下 **[!UICONTROL 頁面資訊]** > **[!UICONTROL 開啟屬性]**，然後選取 **[!UICONTROL 暫時性工作流程]**. 這可改善擴充性和效能。

1. 选择&#x200B;******[!UICONTROL 保存并关闭]**。

1. 按一下 **[!UICONTROL 切換側面板]** 「搜尋程式縮圖」步驟。

1. 選取 **[!UICONTROL 程式縮圖]** 並按一下 **[!UICONTROL 設定]**. 請遵循 [使用Experience Manager工作流程產生新資產轉譯的設定](#generate-renditions-of-new-assets-using-aem-workflow).

1. 若要啟用變更，請按一下 **[!UICONTROL 同步]**.


## 使用ImageMagick產生現有資產的轉譯 {#generate-renditions-of-existing-assets-using-imagemagick}

若要使用ImageMagick處理功能來產生現有資產的FPO轉譯，請建立專用工作流程模型，並使用ImageMagick命令列來執行此操作。

1. 從以下步驟執行步驟1到步驟3 [使用Experience Manager工作流程產生現有資產轉譯的設定](#generate-renditions-of-existing-assets-using-aem-workflow) 區段。

1. 從以下步驟執行步驟4到步驟8： [使用ImageMagick產生新資產轉譯的設定](#generate-renditions-of-new-assets-using-imagemagick) 區段。


## 檢視FPO轉譯 {#view-fpo-renditions}

您可以在工作流程完成後檢查產生的FPO轉譯。 在Experience Manager Assets使用者介面中，按一下資產以開啟大型預覽。 開啟左側邊欄並選取轉譯。 或者，使用鍵盤快速鍵 `Alt + 3` 開啟預覽時。

按一下 **[!UICONTROL FPO轉譯]** 以載入其預覽。 或者，您也可以用滑鼠右鍵按一下轉譯，並將其儲存至您的檔案系統。

![rendition_list](assets/rendition_list.png)


## 提示和限制 {#tips-limitations}

* 若要使用ImageMagick型設定，請將ImageMagick安裝在Experience Manager所在的同一部電腦上。
* 若要產生許多資產或整個存放庫的FPO轉譯，請在低流量期間規劃和執行工作流程。 為大量資產產生FPO轉譯是一項耗用大量資源的活動，且Experience Manager伺服器必須具備足夠的處理能力和可用記憶體。
* 如需效能與擴充性的相關資訊，請參閱 [微調ImageMagick](performance-tuning-guidelines.md).
* 如需資產的一般命令列處理，請參閱 [處理資產的命令列處理常式](media-handlers.md).
