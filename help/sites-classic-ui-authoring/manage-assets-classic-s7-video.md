---
title: Sites Classic製作中的影片
description: Assets提供集中式視訊資產管理，讓您可以將視訊直接上傳到Assets以自動編碼到Dynamic Media Classic，並直接從Assets存取Dy視訊以進行頁面編寫。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 59e182c165f6fd4b822eaf0e34f6e4b3bb18eb14
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# 视频{#video}

Assets提供集中式視訊資產管理，讓您可以將視訊直接上傳到Assets以自動編碼到Dynamic Media Classic，並直接從Assets存取Dynamic Media Classic視訊以進行頁面編寫。

Dynamic Media Classic視訊整合可將最佳化的視訊延伸至所有熒幕（自動裝置和頻寬偵測）。

* Dynamic Media Classic視訊元件會自動執行裝置和頻寬偵測，以在桌上型電腦、平板電腦和行動裝置上播放正確格式和正確品質的視訊。
* 資產 — 您可以包含最適化視訊集，而非單一視訊資產。 自我調整視訊集是所有視訊轉譯的容器，這些轉譯都需要在多個熒幕上無縫播放視訊。 「自我調整視訊集」會將使用不同位元速率和格式（例如400 kbps、800 kbps和1000 kbps）編碼的相同視訊版本分組。 您可使用自我調整視訊集和S7視訊元件，在多個熒幕(包括桌上型電腦、iOS、Android™、BlackBerry®和Windows行動裝置)上串流自我調整視訊。 另請參閱 [有關最適化視訊集的Dynamic Media Classic檔案以取得詳細資訊](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## 關於FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

預設的視訊編碼程式是以使用以FFMPEG為基礎的整合與視訊設定檔為基礎。 因此，開箱即用的 [!UICONTROL DAM更新資產] 工作流程包含下列兩個ffmpeg型工作流程步驟：

* FFMPEG縮圖
* FFMPEG編碼

啟用和設定Dynamic Media Classic整合不會自動從現成可用的移除或停用這兩個工作流程步驟 [!UICONTROL DAM更新資產] 擷取工作流程。 如果您在Adobe Experience Manager中已經使用FFMPEG型視訊編碼，則您的編寫環境很可能已安裝FFMPEG。 在此情況下，使用Experience Manager Assets擷取的新視訊會編碼兩次：一次來自FFMPEG編碼器，一次來自Dynamic Media Classic整合。

如果您已設定Experience Manager為FFMPEG的視訊編碼，且已安裝FFMPEG，Adobe建議您從您的檔案移除這兩個FFMPEG工作流程。 [!UICONTROL DAM更新資產] 工作流程。

### 支援的格式 {#supported-formats}

Dynamic Media Classic視訊元件支援下列格式：

* F4V H.264
* MP4 H.264

### 決定上傳視訊的位置 {#deciding-where-to-upload-your-video}

決定上傳視訊資產的位置取決於下列因素：

* 您是否需要視訊資產的工作流程？
* 您是否需要視訊資產的版本控制？

如果以上任一或兩個問題的答案皆為「是」，則直接將影片上傳至AdobeDAM。 如果這兩個問題的答案都為「否」，則直接將您的影片上傳到Dynamic Media Classic。 下節將說明每個案例的工作流程。

#### 如果您要直接將影片上傳至Adobe資產 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要資產的工作流程或版本設定，應先上傳至Adobe資產。 以下是建議的工作流程：

1. 上傳視訊資產至Adobe資產，並自動編碼和發佈至Dynamic Media Classic。
1. 在Experience Manager中，存取WCM中位於以下位置的視訊資產： **[!UICONTROL 影片]** 內容尋找器的索引標籤。
1. 使用Dynamic Media Classic視訊或foundation視訊元件進行製作。

#### 如果您要將影片上傳至Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要資產的工作流程或版本設定，請將資產上傳至Dynamic Media Classic。 以下是建議的工作流程：

1. 在Dynamic Media Classic案頭應用程式中， [設定已排程的FTP上傳和編碼至Dynamic Media Classic （系統自動化）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. 在Experience Manager中，存取WCM中位於以下位置的視訊資產： **[!UICONTROL Dynamic Media Classic]** 內容尋找器的索引標籤。
1. 使用Dynamic Media Classic視訊元件創作。

### 設定與Dynamic Media Classic影片整合 {#configuring-integration-with-scene-video}

1. 在 **[!UICONTROL Cloud Services]**，導覽至 **[!UICONTROL Dynamic Media Classic]** 設定並選取 **[!UICONTROL 編輯]**.
1. 選取 **[!UICONTROL 視訊]** 標籤。

   >[!NOTE]
   >
   >此 **[!UICONTROL 視訊]** 如果頁面沒有雲端設定，索引標籤不會顯示。 另請參閱 [為WCM啟用Dynamic Media Classic](#enablingscene7forwcm).

1. 選取最適化視訊編碼設定檔、現成可用的單一視訊編碼設定檔，或自訂視訊編碼設定檔。

   >[!NOTE]
   >
   >如需視訊預設集含義的詳細資訊，請參閱 [用於編碼視訊檔案的視訊預設集](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe建議您在設定通用預設集時選取兩個最適化視訊集，或選取 **[!UICONTROL 自我調整視訊編碼]** 選項。

1. 選取的編碼設定檔會自動套用至上傳至您為此Dynamic Media Classic雲端設定所設定CQ DAM目標資料夾的所有影片。 您可以使用不同的目標資料夾設定多個Dynamic Media Classic雲端設定，以視需要套用不同的編碼設定檔。

### 更新檢視器和編碼預設集 {#updating-viewer-and-encoding-presets}

如果在Dynamic Media Classic中更新了預設集，請更新Experience Manager中視訊的檢視器和編碼預設集。 在這種情況下，請導覽至雲端設定中的Dynamic Media Classic設定，然後選取 **更新檢視器和編碼預設集**.

![chlimage_1-131](assets/chlimage_1-131.png)

### 上傳您的主要來源影片 {#uploading-your-master-video}

若要從AdobeDAM將主要來源影片上傳至Dynamic Media Classic：

1. 導覽至CQ DAM目標資料夾，您已在其中使用Dynamic Media Classic編碼設定檔設定您的雲端設定。
1. 選取 **[!UICONTROL 上傳]** 上傳主要來源視訊。 影片上傳和編碼於以下時間後完成： [!UICONTROL DAM更新資產] 工作流程已完成，且 **[!UICONTROL 發佈至Dynamic Media Classic]** 有核取記號。

   >[!NOTE]
   >
   >產生視訊縮圖可能需要一些時間。

   將DAM主要來源視訊拖曳至視訊元件時，會存取 *全部* Dynamic Media Classic編碼的Proxy轉譯以進行傳送。

### Foundation視訊元件與Dynamic Media Classic視訊元件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager時，您可以同時存取Sites中可用的視訊元件和Dynamic Media Classic視訊元件。 這些元件不可互換。

Dynamic Media Classic視訊元件僅適用於Dynamic Media Classic視訊。 基礎元件可處理從Experience Manager （使用ffmpeg）儲存的視訊和Dynamic Media Classic視訊。

以下矩陣說明何時應使用哪個元件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic視訊元件可立即使用通用視訊設定檔。 不過，您可以取得HTML5型影片播放器，以供Experience Manager使用。 在Dynamic Media Classic中，複製現成HTML5視訊播放器的內嵌程式碼，並將其放入您的Experience Manager頁面中。

## Experience Manager視訊元件 {#aem-video-component}

即使檢視Dynamic Media Classic影片建議使用Dynamic Media Classic影片元件，本節仍說明如何搭配使用Dynamic Media Classic影片 [!UICONTROL Foundation視訊元件] Experience Manager以取得完整度。

### Experience Manager影片和Dynamic Media Classic影片比較 {#aem-video-and-scene-video-comparison}

下表提供Experience Manager Foundation Video元件和Dynamic Media Classic Video元件之間支援功能的高階比較：

|  | Experience Manager Foundation影片 | Dynamic Media Classic影片 |
|---|---|---|
| 方針 | HTML5優先方法。 Flash僅用於非HTML5遞補內容。 | 在大部分的桌上型電腦上Flash。 HTML5適用於行動裝置和平板電腦。 |
| 交付 | 漸進式 | 最適化串流 |
| 追蹤 | 是 | 是 |
| 擴充性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 設定 {#setting-up}

#### 建立視訊設定檔 {#creating-video-profiles}

根據Dynamic Media Classic雲端設定中選取的Dynamic Media Classic編碼預設集建立各種視訊編碼。 為了讓Foundation視訊元件能夠使用它們，您必須為每個選取的Dynamic Media Classic編碼預設集建立視訊設定檔。 它可讓視訊元件據以選取DAM轉譯。

>[!NOTE]
>
>必須啟動新的視訊設定檔及其變更才能發佈。

1. 在Experience Manager中，前往 **[!UICONTROL 工具]**，然後選取 **[!UICONTROL 設定主控台]**.
1. 在設定控制檯中，瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 視訊設定檔]** 導覽樹狀結構中的。
1. 建立Dynamic Media Classic視訊設定檔。 在 **[!UICONTROL 新增]** 功能表，選取 **[!UICONTROL 建立頁面]**.
1. 選取Dynamic Media Classic視訊設定檔範本。 為新的視訊設定檔頁面命名，然後選取 **[!UICONTROL 建立]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 編輯新的視訊設定檔。 請先選取雲端設定。 然後選取與雲端設定中所選相同的編碼預設集。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 属性 | 描述 |
   |---|---|
   | Dynamic Media Classic雲端設定 | 用於編碼預設集的雲端設定。 |
   | Dynamic Media Classic編碼預設集 | 對應此視訊設定檔的編碼預設集。 |
   | HTML5 视频类型 | 此屬性可讓您設定HTML5視訊來源元素的type屬性值。 Dynamic Media Classic編碼預設集並未提供這項資訊，但使用HTML5視訊元素正確轉譯視訊時需要這項資訊。 提供常見格式的清單，但其他格式可以覆寫。 |

   對雲端設定中選取要用於視訊元件的所有編碼預設集重複此步驟。

#### 設定設計 {#configuring-design}

Foundation視訊元件必須瞭解要使用哪些視訊設定檔，才能建立視訊來源清單。 開啟視訊元件設計對話方塊，並使用新的視訊設定檔來設定元件設計。

>[!NOTE]
>
>如果您在行動頁面上使用foundation視訊元件，請在行動頁面的設計上重複這些步驟。

>[!NOTE]
>
>對設計所做的變更需要啟動設計，才能在發佈時生效。

1. 開啟foundation視訊元件的「設計」對話方塊，並變更為 **[!UICONTROL 設定檔]** 標籤。 然後刪除現成可用的設定檔，並新增新的Dynamic Media Classic視訊設定檔。 設定檔清單在「設計」對話方塊中的順序，以及轉譯時視訊來源元素的順序。
1. 對於不支援HTML5的瀏覽器，視訊元件可讓您設定快閃後援。 開啟視訊元件設計對話方塊，並變更為 **[!UICONTROL Flash]** 標籤。 設定Flash Player設定並指派Flash Player的遞補設定檔。

#### 檢查清單 {#checklist}

1. 建立Dynamic Media Classic雲端設定。 請確定已設定視訊編碼預設集，且匯入工具在執行中。
1. 為雲端設定中選取的每個視訊編碼預設集建立Dynamic Media Classic視訊設定檔。
1. 必須啟動視訊設定檔。
1. 在頁面上設定foundation視訊元件的設計。
1. 完成設計變更後啟動設計。
