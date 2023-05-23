---
title: 360/VR影片
description: 瞭解如何在Dynamic Media中使用360和虛擬現實(VR)影片。
uuid: c21bf2c0-7acc-401f-857e-0186de86e7a1
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: aac3c850-ae84-4bff-80de-d370e150f675
docset: aem65
feature: 360 VR Video
role: User, Admin
exl-id: 0c2077a7-bd16-484b-980f-4d4a1a681491
source-git-commit: c0a60ec39e35fa8113ce9e1795561709b9c7e289
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---

# 360/VR影片 {#vr-video}

360度影片會同時記錄每個方向的檢視。 它們使用全方位相機或一系列相機拍攝。 在平面顯示器上播放期間，使用者可以控制視角；行動裝置上的播放通常使用其內建的陀螺儀控制項。

Dynamic Media - Scene7模式包含原生支援，可傳送360個視訊資產。 依預設，檢視或播放不需要額外的設定。 您會使用標準視訊副檔名（例如.mp4、.mkv和.mov）來傳送360視訊。 最常見的轉碼器是H.264。

本節說明如何使用360/VR視訊檢視器來轉譯等矩形視訊，以獲得房間、屬性、位置、橫向、醫療程式等的沈浸式檢視體驗。

目前不支援空間音訊；如果音訊混合在立體聲中，平衡(L/R)不會隨著客戶變更相機視角而改變。

另請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

## 360影片運作中 {#video-in-action}

選取 [360號空間站](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) 開啟瀏覽器視窗並觀看360度影片。 在視訊播放期間，將滑鼠指標拖曳至新位置以變更視角。

![360個視訊樣本，國際空間站漂浮在外層空間，地球和太陽在其後面。](assets/6_5_360videoiss_simplified.png)
*來自空間站360的視訊影格*

## 360/VR視訊與Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

您可以使用AdobePremier Pro來檢視和編輯360/VR素材。 例如，您可以在場景中正確放置圖志和文字，並套用專為等矩形媒體設計的效果和轉場。

另請參閱 [編輯360/VR影片](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## 上傳資產以與360視訊檢視器搭配使用 {#uploading-assets-for-use-with-the-video-viewer}

上傳至Adobe Experience Manager的360個視訊資產會標示為 **多媒體** 資產頁面上，與一般視訊資產類似。

![6_5_360video-selecttopreview](assets/6_5_360video-selecttopreview.png)
*在卡片檢視中看到的已上傳360視訊資產。 資產標示為多媒體。*

**上傳資產以搭配360視訊檢視器使用：**

1. 已建立專用於您的360度影片資產的資料夾。
1. [將最適化視訊設定檔套用至資料夾](/help/assets/video-profiles.md#applying-a-video-profile-to-folders).

   與標準非360度視訊內容相比，轉譯360度視訊內容對來源視訊解析度和編碼轉譯解析度的需求更高。

   您可以使用隨Dynamic Media提供的現成最適化視訊設定檔。 不過，若使用非360視訊檢視器轉譯的相同設定進行編碼，會產生明顯較低的360視訊品質。 因此，如果需要高品質360視訊，請執行下列動作：

   * 理想情況下，您原本的360度影片內容最好具備下列其中一種解析度：

      * 1080p - 1920 x 1080，稱為Full HD或FHD解析度，或
      * 2160p - 3840 x 2160，稱為4k、UHD或UltraHD解析度。 這種大型顯示器解析度最常出現在高檔電視機和電腦顯示器上。 2160p解析度通常稱為「4k」，因為寬度接近4000畫素。 換句話說，它提供1080p畫素的四倍。
   * [建立自訂最適化視訊設定檔](/help/assets/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) 提供更高品質的轉譯。 例如，建立包含下列三個設定的最適化視訊設定檔：

      * width=auto； height=720； bitrate=2500 kbps
      * width=auto； height=1080； bitrate=5000 kbps
      * width=auto； height=1440； bitrate=6600 kbps
   * 處理360影片資產專屬資料夾中的360影片內容。

   此方法對使用者的網路和CPU提出了更高的要求。

1. [將視訊上傳至資料夾](/help/assets/managing-video-assets.md#upload-and-preview-video-assets).

## 覆寫360部影片的預設外觀比例  {#overriding-the-default-aspect-ratio-of-videos}

若要讓上傳的資產符合您要搭配360視訊檢視器使用的360視訊資格，該資產的外觀比例必須為2。

根據預設，如果視訊的外觀比例（寬度/高度）為2.0，Experience Manager會將視訊偵測為「360」。如果您是管理員，可以透過設定選擇性來覆寫預設外觀比例設定2 `s7video360AR` 屬性的CRXDE Lite：

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

   * **屬性型別**  — 兩次
   * **值**  — 浮點外觀比例，預設值2.0。

設定此屬性後，現有視訊和新上傳的視訊都會立即生效。

外觀比例會套用至資產詳細資訊頁面的360個視訊資產，以及 [360度影片媒體WCM元件](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

先從上傳360部影片開始。

## 預覽360度影片 {#previewing-video}

您可以使用「預覽」來檢視您的360影片對客戶看起來是什麼樣子，並確保它如預期般運作。

另請參閱 [編輯檢視器預設集](/help/assets/managing-viewer-presets.md#editing-viewer-presets).

當您對360視訊感到滿意時，可以將其發佈。

另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
另請參閱 [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容具有具有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).

**若要預覽360度影片：**

1. 在 **[!UICONTROL 資產]**，導覽至您建立的現有360影片。 選取360視訊資產，以便您可以在預覽模式下將其開啟。

   ![6_5_360video-selecttopreview-1](assets/6_5_360video-selecttopreview-1.png)

   選取360度影片資產，以便預覽影片。

1. 在預覽頁面頁面的左上角附近，選取下拉式清單，然後選取 **[!UICONTROL 檢視者]**.

   ![6_5_360video-preview-viewers](assets/6_5_360video-preview-viewers.png)

   從「檢視器」清單中選取 **[!UICONTROL Video360_social]**，然後執行下列任一項作業：

   * 如果要改變靜態場景的視角，請將滑鼠指標拖曳到視訊上。
   * 選取視訊的 **[!UICONTROL 播放]** 按鈕。 播放視訊時，拖曳滑鼠指標橫跨視訊以改變視角。

   ![外太空浮動的國際空間站熒幕擷圖，背景為地球和太陽&#x200B;](assets/6_5_360video-preview-video360-social.png)*360度影片截圖。*

   * 從「檢視器」清單中選取 **[!UICONTROL Video360VR]**.

      虛擬現實(VR)視訊是使用虛擬現實耳機存取的沈浸式視訊內容。 和一般視訊一樣，您一開始會使用360度攝影機錄製或擷取視訊，藉此建立VR視訊。
   ![浮動於外太空的國際空間站特寫熒幕擷圖，背景部分可見地球和太陽](assets/6_5_360video-preview-video360vr.png)
   *360 VR視訊熒幕擷圖。*

1. 在預覽頁面的右上角附近，選取 **[!UICONTROL 關閉]**.

## 發佈360度影片 {#publishing-video}

發佈360影片以便使用。 發佈360影片會啟用URL和內嵌程式碼。 此外，該公司也會將360影片發佈至Dynamic Media雲端，此雲端已與CDN整合，提供可擴充且優異的傳送效能。

另請參閱 [發佈Dynamic Media資產](/help/assets/publishing-dynamicmedia-assets.md) 以取得發佈360度影片的詳細資訊。
另請參閱 [將視訊或影像檢視器內嵌在網頁上](/help/assets/embed-code.md).
另請參閱 [將URL連結至您的網頁應用程式](/help/assets/linking-urls-to-yourwebapplication.md). 如果您的互動式內容具有具有具有相對URL的連結，尤其是指向Experience Manager Sites頁面的連結，則無法採用URL型連結方法。
另請參閱 [將Dynamic Media資產新增至頁面](/help/assets/adding-dynamic-media-assets-to-pages.md).
